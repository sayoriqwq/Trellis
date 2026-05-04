# Directory Structure

> Static marketplace registry layout.

## Overview

Marketplace content is organized by downloadable resource type. Do not add
server modules or package runtime code unless the repository architecture
changes.

## Directory Layout

```text
marketplace/
├── README.md
├── index.json
├── skills/
│   ├── trellis-meta/
│   ├── cc-codex-spec-bootstrap/
│   └── frontend-fullchain-optimization/
└── specs/
    ├── electron-fullstack/
    ├── nextjs-fullstack/
    └── cf-workers-fullstack/
```

## Registry Organization

- `index.json` is the public template registry consumed by Trellis CLI remote
  template fetching.
- `skills/<id>/SKILL.md` is the skill entry point.
- `skills/<id>/references/**` contains supporting documents referenced by a
  skill.
- `specs/<id>/README.md` describes a spec template.
- `specs/<id>/{backend,frontend,shared,guides}/index.md` lists files in that
  layer.

## Examples

- `marketplace/index.json` declares `electron-fullstack`, `nextjs-fullstack`,
  `cf-workers-fullstack`, `trellis-meta`, and
  `frontend-fullchain-optimization`.
- `marketplace/skills/trellis-meta/SKILL.md` is a long-form skill with
  compatibility matrices and reference links.
- `marketplace/specs/nextjs-fullstack/backend/index.md` documents a fullstack
  Next.js backend spec template.

## Forbidden Patterns

- Do not add API handlers, DB schemas, or build output to the registry.
- Do not move a template directory without updating `index.json`.
- Do not leave orphaned reference files that are not linked from `SKILL.md` or a
  template index.
