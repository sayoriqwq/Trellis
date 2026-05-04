# Hook Guidelines

> No React hooks exist in the Trellis CLI package.

## Overview

The word "hook" in this repository usually means AI platform lifecycle hooks,
not React hooks. These are generated Python scripts and platform configuration
entries, not frontend state hooks.

## AI Platform Hooks

Generated hook templates live in:

- `packages/cli/src/templates/shared-hooks/session-start.py`
- `packages/cli/src/templates/shared-hooks/inject-shell-session-context.py`
- `packages/cli/src/templates/shared-hooks/inject-subagent-context.py`
- `packages/cli/src/templates/shared-hooks/inject-workflow-state.py`

Platform hook configuration lives in template/configurator pairs such as:

- `packages/cli/src/templates/codex/hooks.json`
- `packages/cli/src/configurators/codex.ts`
- `packages/cli/src/templates/claude/settings.json`
- `packages/cli/src/configurators/claude.ts`

## Rules

- Do not add React `use*` hooks to this package.
- Keep generated hook scripts platform-neutral where possible and resolve
  platform differences through configurators.
- If a hook command needs `python` vs `python3`, use
  `getPythonCommandForPlatform` and placeholder replacement helpers.
- Keep hooks idempotent; they run repeatedly during AI sessions.

## Common Mistakes

- Confusing AI lifecycle hooks with React hooks when naming files or docs.
- Hard-coding `python3` in generated content without passing through placeholder
  resolution.
- Updating a hook template without updating tests for platform generation.
