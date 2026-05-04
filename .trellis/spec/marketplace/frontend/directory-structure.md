# Frontend Directory Structure

> Where frontend guidance lives in marketplace.

## Overview

There is no app frontend directory. Frontend files are documentation templates
under `specs/<template>/frontend/` and frontend-related skills under `skills/`.

## Layout

```text
marketplace/
├── skills/
│   └── frontend-fullchain-optimization/
│       └── SKILL.md
└── specs/
    ├── electron-fullstack/frontend/
    ├── nextjs-fullstack/frontend/
    └── cf-workers-fullstack/frontend/
```

## Placement Rules

- Put framework-specific frontend rules in the matching spec template, for
  example `specs/nextjs-fullstack/frontend/`.
- Put cross-layer TypeScript or dependency rules in `shared/` when they apply to
  both backend and frontend.
- Put reusable performance workflow guidance in a skill if it applies across
  projects, as with `frontend-fullchain-optimization`.
- Put copyable design examples in explicit example directories with
  `.template` suffixes when they are not normal Markdown specs.

## Examples

- `marketplace/specs/nextjs-fullstack/frontend/index.md` indexes components,
  authentication, oRPC usage, hooks, state management, CSS layout, and quality.
- `marketplace/specs/electron-fullstack/frontend/state-management.md` documents
  Electron/React state patterns.
- `marketplace/specs/cf-workers-fullstack/frontend/examples/frontend-design/`
  contains template examples for frontend design guidance.

## Forbidden Patterns

- Do not add `src/components` or app code to marketplace.
- Do not put backend-only rules in frontend template files.
- Do not create a new frontend template directory without adding its indexes and
  registry metadata when it is downloadable.
