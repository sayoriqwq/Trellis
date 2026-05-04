# Directory Structure

> Static docs configuration and content layout.

## Overview

Docs-site is organized for Mintlify. There is no backend `src/`, `routes/`, or
server module. Treat `docs.json` as the central routing/navigation contract and
MDX files as page content.

## Directory Layout

```text
docs-site/
├── docs.json                 # Mintlify config, nav, redirects, excludes
├── index.mdx                 # English RC landing page
├── quickstart.mdx            # Quickstart page
├── development.mdx           # Mintlify local development page
├── advanced/                 # Advanced RC docs
├── start/                    # Getting started RC docs
├── guides/                   # Guide pages
├── changelog/                # RC changelog pages
├── release/                  # Stable release version docs
├── zh/                       # Chinese docs mirror
├── api-reference/            # API reference pages and openapi.json
├── images/                   # Static images used by MDX
├── logo/                     # Theme logos
├── styles.css                # Global Mintlify CSS overrides
└── terminal-demo.js          # Custom browser script for terminal demo
```

## Content Organization

- `docs.json` owns navigation groups, versions, languages, redirects, theme
  colors, global anchors, custom JS, and excluded paths.
- Top-level directories such as `advanced/`, `start/`, `showcase/`, `blog/`,
  and `skills-market/` map directly to Mintlify page routes.
- `zh/` mirrors localized Chinese pages.
- `release/` and `zh/release/` hold stable release docs while the root and
  `zh/` paths can represent RC docs.
- `api-reference/openapi.json` is static API documentation data, not a live API
  implementation.

## Examples

- `docs-site/docs.json` registers language/version navigation and redirects old
  `/guide/...` routes to current pages.
- `docs-site/index.mdx` uses YAML frontmatter plus Mintlify components such as
  `CardGroup` and `Card`.
- `docs-site/development.mdx` documents `mint dev`, custom ports, link
  validation, and deployment checks.

## Forbidden Patterns

- Do not add backend framework directories such as `server/`, `api/`, or
  `routes/` to docs-site unless the repository architecture changes.
- Do not rely on filesystem presence alone; pages must be reachable from
  `docs.json` navigation or intentionally linked.
- Do not put generated marketplace source content into public navigation unless
  it is meant to be documentation.
