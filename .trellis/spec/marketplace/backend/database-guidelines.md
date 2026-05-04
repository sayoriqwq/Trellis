# Registry Data Guidelines

> Marketplace has no database. `index.json` is the registry.

## Overview

The registry is static JSON and markdown content. Treat `index.json` as the
database-like source of truth for downloadable resources.

## `index.json` Contract

`marketplace/index.json` has this shape:

```json
{
  "version": 1,
  "templates": [
    {
      "id": "nextjs-fullstack",
      "type": "spec",
      "name": "Next.js + oRPC + PostgreSQL",
      "description": "...",
      "path": "specs/nextjs-fullstack",
      "tags": ["nextjs", "react", "typescript"]
    }
  ]
}
```

Rules:

- `id` must be stable and unique.
- `type` should match the installer contract (`spec`, `skill`, `command`, or
  `full` if supported by the CLI).
- `path` must point to an existing directory in the marketplace repo.
- `tags` should be lowercase and useful for discovery.

## Template Data

- Skills use YAML frontmatter in `SKILL.md`.
- Spec templates use Markdown indexes and guideline files.
- Example files intended as copyable templates may use `.template` suffixes, as
  seen in frontend design examples under spec templates.

## Examples

- `marketplace/index.json` maps `trellis-meta` to `skills/trellis-meta`.
- `marketplace/specs/electron-fullstack/backend/index.md` lists backend files
  for the Electron template.
- `marketplace/specs/cf-workers-fullstack/frontend/examples/frontend-design/`
  stores copyable `.template` example assets.

## Forbidden Patterns

- Do not add a DB, ORM, or migration layer.
- Do not duplicate registry metadata inside template README files without
  keeping `index.json` canonical.
- Do not use a path in `index.json` that depends on generated build output.
