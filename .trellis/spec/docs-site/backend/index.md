# Docs-Site Backend Guidelines

> The docs-site package is a static Mintlify documentation repository.

## Overview

`docs-site` does not contain a backend application, database, ORM, API server, or
service layer. Its backend-facing surface is configuration and content:
`docs.json`, `api-reference/openapi.json`, MDX documentation pages, redirects,
and static assets.

The local submodule gitlink currently points at a commit that could not be
fetched, so these guidelines are based on the available `docs-site` remote
`origin/main` tree. File paths below are the expected paths when the submodule
is checked out.

## Guidelines Index

| Guide | Description | Status |
|-------|-------------|--------|
| [Directory Structure](./directory-structure.md) | Mintlify content and config layout | Filled |
| [Database Guidelines](./database-guidelines.md) | No database; JSON/MDX content contracts | Filled |
| [Error Handling](./error-handling.md) | Validation, redirects, broken links, docs fallbacks | Filled |
| [Quality Guidelines](./quality-guidelines.md) | MDX, navigation, bilingual, and release quality | Filled |
| [Logging Guidelines](./logging-guidelines.md) | No runtime logging; validation output only | Filled |

## Pre-Development Checklist

- Read `docs-site/docs.json` before adding, moving, or deleting pages.
- Check both English and `zh/` paths for mirrored content expectations.
- Check `release/` and `zh/release/` when changing release-version docs.
- Run or recommend Mintlify validation (`mint dev`, `mint broken-links`) for
  navigation and link changes.

## Common Mistakes

- Adding an MDX page without registering it in `docs.json` navigation.
- Editing only RC docs while forgetting the release copy, or editing English
  without considering `zh/`.
- Leaving marketplace/spec template source visible in docs output instead of
  excluding it through `docs.json`.

**Language**: Project guideline docs are English. Product docs may be English or
Chinese depending on the target docs path.
