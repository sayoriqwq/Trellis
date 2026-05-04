# Logging Guidelines

> Trellis CLI uses console output as user interface, not structured service
> logging.

## Overview

There is no backend logger or telemetry pipeline in `packages/cli`. CLI output
is intentionally human-readable, usually with `chalk` color. Keep output concise
and reserve verbose diagnostics for debug mode.

## Output Conventions

- Use `console.log` for normal progress and plan output.
- Use `console.error` for command failures at the CLI boundary.
- Use `chalk` consistently for emphasis, warnings, and success states.
- Keep command output stable enough for users to understand, but do not treat
  colored text as a machine API.
- Use `DEBUG` or `TRELLIS_DEBUG` to show stack traces in
  `packages/cli/src/cli/index.ts`.

## Examples

`packages/cli/src/commands/uninstall.ts` renders grouped plans with headings:
files to delete, files to modify, skipped missing entries, then a confirmation.

`packages/cli/src/utils/file-writer.ts` prints short status lines for conflicts:
overwritten, skipped, or appended.

`packages/cli/src/commands/init.ts` prints platform/Python adaptation notices
with `chalk.blue` so users understand why generated commands use `python` or
`python3`.

## Sensitive Data

- Never print raw proxy URLs with credentials. Use `maskProxyUrl` from
  `packages/cli/src/utils/proxy.ts`.
- Avoid dumping full environment objects.
- Do not log full remote registry auth tokens or headers.

## Forbidden Patterns

- Do not add `console.log` debugging in library utilities and leave it there.
- Do not introduce a logging dependency unless the CLI architecture changes.
- Do not emit stack traces by default.
- Do not use logs as control flow in tests; assert filesystem state and return
  values instead.
