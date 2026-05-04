# Directory Structure

> How backend code is organized in the Trellis CLI package.

## Overview

The main package lives at `packages/cli`. Source files are TypeScript ESM under
`packages/cli/src`, compiled to `dist` by `tsc`, and exposed through
`packages/cli/bin/trellis.js`.

Keep feature code in the directory that owns the behavior. Do not add catch-all
folders for single-use helpers.

## Directory Layout

```text
packages/cli/
├── bin/                 # Published executable entry
├── scripts/             # Build/release helper scripts
├── src/
│   ├── cli/             # Commander setup and top-level error boundary
│   ├── commands/        # trellis init/update/uninstall implementations
│   ├── configurators/   # Platform-specific install/update logic
│   ├── constants/       # Shared path/version constants
│   ├── migrations/      # File migrations and version manifests
│   ├── templates/       # Files rendered into user projects
│   ├── types/           # Shared TypeScript types
│   └── utils/           # Focused pure or filesystem helpers
└── test/                # Vitest unit and integration tests
```

## Module Organization

- `src/cli/index.ts` wires Commander commands and owns `process.exit(1)` after
  logging top-level errors.
- `src/commands/*.ts` implements user-facing operations. Examples:
  `init.ts`, `update.ts`, and `uninstall.ts`.
- `src/configurators/*.ts` contains platform adapters such as `codex.ts`,
  `claude.ts`, and `cursor.ts`. Shared rendering helpers live in
  `configurators/shared.ts`.
- `src/templates/**` is the source of generated project files. If behavior
  changes in local `.trellis/`, `.codex/`, `.claude/`, or `.agents/` assets,
  check whether the corresponding template must be updated.
- `src/utils/*.ts` holds reusable logic with narrow responsibilities:
  `file-writer.ts`, `project-detector.ts`, `template-fetcher.ts`,
  `template-hash.ts`, and similar helpers.

## Naming Conventions

- Use kebab-case for filenames: `file-writer.ts`, `project-detector.ts`,
  `template-fetcher.ts`.
- Use named exports for utilities and command helpers.
- Keep constants in uppercase object exports where they represent stable
  workflow names, as in `DIR_NAMES`, `FILE_NAMES`, and `PATHS`.
- Use `.js` extensions in relative TypeScript imports because the package uses
  `moduleResolution: "NodeNext"`.

## Examples

- `packages/cli/src/constants/paths.ts` centralizes workflow path names and
  helper path builders.
- `packages/cli/src/utils/file-writer.ts` keeps conflict handling in one module
  instead of duplicating overwrite/skip/append logic in commands.
- `packages/cli/src/configurators/shared.ts` contains platform-neutral
  placeholder and skill/command wrapper utilities used by multiple
  configurators.

## Forbidden Patterns

- Do not introduce new root-level runtime folders when an existing layer owns
  the behavior.
- Do not hard-code `.trellis`, `.current-task`, or platform paths in feature
  code when `constants/paths.ts` or configurator constants already exist.
- Do not place platform-specific branching inside unrelated utilities. Add or
  update the relevant configurator instead.
