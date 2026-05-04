# Component Guidelines

> The Trellis CLI has no React component system.

## Overview

Do not add React components to `packages/cli` for command-line interactions.
The package uses Commander for command routing and Inquirer for prompts.

If future work introduces a web UI, create a separate package or clearly scoped
frontend directory and write new specs from the actual framework choices.

## Current Interaction Patterns

- CLI commands are declared in `packages/cli/src/cli/index.ts`.
- Interactive prompts use `inquirer`, for example conflict handling in
  `packages/cli/src/utils/file-writer.ts` and command confirmations in
  `packages/cli/src/commands/uninstall.ts`.
- Visual terminal output uses `chalk` and plain text, not component renderers.

## Template Content

Some generated assets contain command/skill prose, Markdown, TOML, JSON, or
Python. Treat these as template files, not frontend components:

- `packages/cli/src/templates/common/`
- `packages/cli/src/templates/markdown/`
- `packages/cli/src/templates/trellis/`
- `packages/cli/src/templates/shared-hooks/`

## Accessibility

For terminal prompts, prefer standard Inquirer controls instead of custom
terminal UI. Make prompt messages clear and provide safe defaults for non-TTY
execution where needed.

## Common Mistakes

- Adding a React component to solve terminal prompt flow.
- Embedding large UI strings directly in configurators instead of template
  modules.
- Updating generated Markdown text without updating tests that assert installed
  files or template hashes.
