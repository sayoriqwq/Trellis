# Data Guidelines

> Docs-site has no database. Data is static JSON, MDX, and assets.

## Overview

Do not introduce database patterns for docs-site. The content source of truth is
the checked-in repository:

- `docs.json` for navigation, redirects, excludes, and theme configuration.
- `api-reference/openapi.json` for API reference data.
- MDX frontmatter for page title and description.
- Static assets under `images/`, `logo/`, and `favicon.svg`.

## JSON Contracts

`docs.json` must remain valid JSON matching Mintlify's schema. It currently
contains:

- `$schema`: `https://mintlify.com/docs.json`
- `theme`, `colors`, `favicon`, `logo`, and custom `js`
- `navigation.languages` with English and Chinese versions
- `exclude` patterns for `.trellis/**`, agent instructions, and marketplace
  source directories
- `redirects` for old guide URLs

## MDX Frontmatter

Most pages use frontmatter:

```mdx
---
title: 'Quickstart'
description: 'Set up Trellis in your project'
---
```

Keep titles and descriptions accurate because Mintlify uses them for page
metadata and navigation surfaces.

## Examples

- `docs-site/docs.json` excludes `marketplace/specs/**` so template source files
  do not become public docs pages.
- `docs-site/api-reference/openapi.json` is static OpenAPI data consumed by
  Mintlify.
- `docs-site/changelog/v0.5.0-rc.0.mdx` and related changelog pages encode
  release history as content, not database rows.

## Forbidden Patterns

- Do not add ORM, migration, or DB client dependencies.
- Do not store navigation state in separate JSON files unless `docs.json` is
  updated to reference them.
- Do not hand-edit generated OpenAPI content without knowing its upstream source
  contract.
