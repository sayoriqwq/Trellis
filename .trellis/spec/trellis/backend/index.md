# Trellis SQ CLI Backend Guidelines

> Project-specific standards for the `trellis-sq` package.

## Overview

`packages/cli` is a Node.js CLI written in strict TypeScript. Treat its
backend layer as all non-UI runtime code: CLI command handlers, filesystem
workflow management, template/configuration installers, migration logic, remote
template fetching, and tests.

There is no HTTP server, database service, or long-running process in this
package. Most state is read from and written to files under `.trellis/`, agent
platform directories, and template hash manifests.

## Guidelines Index

| Guide | Description | Status |
|-------|-------------|--------|
| [Directory Structure](./directory-structure.md) | Module organization and package layout | Filled |
| [Database Guidelines](./database-guidelines.md) | Filesystem persistence, JSON manifests, migrations | Filled |
| [Error Handling](./error-handling.md) | CLI error boundaries, recoverable parsing, debug output | Filled |
| [Quality Guidelines](./quality-guidelines.md) | TypeScript, lint, testing, and change scope | Filled |
| [Logging Guidelines](./logging-guidelines.md) | CLI output conventions and debug logging | Filled |

## Pre-Development Checklist

- Read `packages/cli/package.json` for scripts and runtime dependencies.
- Read `packages/cli/tsconfig.json` and `packages/cli/eslint.config.js` before
  changing TypeScript patterns.
- For command behavior, compare against examples in `packages/cli/src/commands/`
  and matching tests under `packages/cli/test/commands/`.
- For template/platform changes, inspect both `packages/cli/src/configurators/`
  and `packages/cli/src/templates/`.
- For `.trellis/`, `.claude/`, `.codex/`, `.cursor/`, or hook changes, check
  whether generated templates also need the same change.

## Core Rules Summary

| Rule | Source |
|------|--------|
| Keep exported functions explicitly typed | `packages/cli/eslint.config.js` |
| Do not use `any` or non-null assertions | `packages/cli/eslint.config.js` |
| Use constants for workflow paths | `packages/cli/src/constants/paths.ts` |
| Preserve user files unless a mode or migration explicitly allows writing | `packages/cli/src/utils/file-writer.ts`, `packages/cli/src/commands/update.ts` |
| Commands throw errors upward; the CLI entry point owns process exit | `packages/cli/src/cli/index.ts` |
| Tests use Vitest with temp directories and mocked external dependencies | `packages/cli/test/commands/init.integration.test.ts` |

## Common Mistakes

- Updating project-local `.trellis/` or platform config without updating the
  templates that install those files into user projects.
- Adding new path literals instead of extending `DIR_NAMES`, `FILE_NAMES`, or
  `PATHS`.
- Prompting from lower-level utilities in ways that break non-TTY execution.
- Reintroducing docs-site or marketplace as source packages in this fork without
  an explicit repository-boundary decision.

**Language**: All documentation should be written in English.
