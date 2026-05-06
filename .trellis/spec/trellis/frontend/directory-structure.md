# Frontend Directory Structure

> Frontend boundaries for the Trellis CLI package.

## Overview

There is no browser application in `packages/cli`. Do not create `app/`,
`pages/`, `components/`, or `hooks/` inside the CLI package unless the product
explicitly adds a frontend package.

Frontend-adjacent files are templates and documentation assets that are copied
into user projects.

## Existing Relevant Layout

```text
packages/cli/src/templates/
├── common/          # Shared command/skill template content
├── markdown/        # AGENTS.md and markdown helper templates
├── codex/           # Codex config/hook templates
├── claude/          # Claude Code templates
├── cursor/          # Cursor templates
├── trellis/         # .trellis workflow/config/spec templates
└── shared-hooks/    # Python hook templates
```

## Placement Rules

- Platform-specific generated files belong under
  `packages/cli/src/templates/<platform>/` and the matching
  `packages/cli/src/configurators/<platform>.ts`.
- Shared command/skill content belongs under `packages/cli/src/templates/common/`
  and is resolved by `packages/cli/src/configurators/shared.ts`.
- Markdown root templates such as `AGENTS.md` belong under
  `packages/cli/src/templates/markdown/`.
- Do not put public documentation-site or marketplace content in `packages/cli`
  unless this fork explicitly adopts those repositories again.

## Examples

- `packages/cli/src/templates/codex/config.toml` and
  `packages/cli/src/configurators/codex.ts` are a template/configurator pair.
- `packages/cli/src/templates/shared-hooks/session-start.py` is generated hook
  code, not runtime frontend code.
- `packages/cli/src/templates/markdown/agents.md` is the source for managed
  `AGENTS.md` blocks.

## Forbidden Patterns

- Do not add a component tree inside `packages/cli/src`.
- Do not edit generated local files only; update the source template when the
  installed output should change for users.
- Do not mix platform-specific template paths in shared rendering helpers.
