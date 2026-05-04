# Error Handling

> CLI commands should fail clearly at the boundary and recover locally from
> optional file detection problems.

## Overview

The top-level CLI catches command failures in `packages/cli/src/cli/index.ts`.
Command and utility modules should throw meaningful `Error` objects for true
failures and return safe fallbacks for optional detection/parsing paths.

## CLI Boundary

Each Commander action wraps command execution:

```ts
try {
  await init(options);
} catch (error) {
  console.error(
    chalk.red("Error:"),
    error instanceof Error ? error.message : error,
  );
  if (process.env.DEBUG || process.env.TRELLIS_DEBUG) {
    console.error(error instanceof Error ? error.stack : error);
  }
  process.exit(1);
}
```

Follow this boundary. Lower-level code should not usually call `process.exit`.

## Recoverable Errors

Use local `try/catch` with fallback when probing optional project state:

- `packages/cli/src/utils/project-detector.ts` catches missing/malformed config
  while detecting workspace packages.
- `packages/cli/src/commands/update.ts` catches missing workflow files when
  building templates and falls back to bundled content.
- `packages/cli/src/utils/template-fetcher.ts` classifies registry failures with
  `RegistryBackendError` and a `kind` field.

## Fatal Errors

Throw `Error` with a user-actionable message when a required invariant is
missing:

- Unsupported Python version in `requireSupportedPython`.
- Missing skill description in `wrapWithSkillFrontmatter`.
- Invalid registry source in `parseRegistrySource`.
- Unsafe or unsupported update/uninstall operation.

## Error Message Style

- Tell the user what failed and what value/path caused it.
- Use command names or file paths in messages where useful.
- Avoid stack traces by default; reserve them for `DEBUG` or `TRELLIS_DEBUG`.
- Do not log secrets, tokens, or full proxy credentials. Use masking helpers
  such as `maskProxyUrl` when proxy values are displayed.

## Forbidden Patterns

- Do not swallow command failures silently. If the operation cannot continue,
  throw.
- Do not throw from optional feature detection if a fallback can preserve CLI
  behavior.
- Do not call `process.exit` from utility modules.
- Do not rely on `error as Error` without an `instanceof Error` check at output
  boundaries.
