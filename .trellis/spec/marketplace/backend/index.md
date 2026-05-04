# Marketplace Backend Guidelines

> Marketplace is a static registry of downloadable Trellis resources.

## Overview

`marketplace` does not contain a backend service. Its backend-facing contract is
the registry and template content consumed by the Trellis CLI:

- `index.json` lists downloadable templates.
- `skills/**` contains skill packages with `SKILL.md` and references.
- `specs/**` contains `.trellis/spec/` templates.

The local submodule gitlink currently points at an unavailable commit, so these
guidelines are based on the available `marketplace` remote `origin/main` tree.
File paths below are the expected paths when the submodule is checked out.

## Guidelines Index

| Guide | Description | Status |
|-------|-------------|--------|
| [Directory Structure](./directory-structure.md) | Registry, skills, and spec template layout | Filled |
| [Database Guidelines](./database-guidelines.md) | JSON registry and static content contracts | Filled |
| [Error Handling](./error-handling.md) | Registry/template validation and failure modes | Filled |
| [Quality Guidelines](./quality-guidelines.md) | Template completeness and examples | Filled |
| [Logging Guidelines](./logging-guidelines.md) | No runtime logging; validation output only | Filled |

## Pre-Development Checklist

- Read `marketplace/index.json` before adding, renaming, or moving templates.
- Read the target skill or spec template README/index before editing files
  inside it.
- For spec templates, keep `backend/`, `frontend/`, `shared/`, and `guides/`
  indexes aligned with actual files.
- For skills, keep YAML frontmatter accurate and references reachable.

**Language**: Marketplace content should be English unless a template explicitly
documents another language.
