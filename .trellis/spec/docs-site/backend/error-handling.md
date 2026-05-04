# Error Handling

> Docs-site errors are content, navigation, and validation problems.

## Overview

There is no runtime exception boundary in docs-site. Error handling means making
broken docs states easy to catch before deploy: invalid JSON, invalid MDX,
broken links, missing navigation entries, missing assets, and stale redirects.

## Validation Patterns

- Use `mint dev` for local preview.
- Use `mint broken-links` for link validation when changing routes or links.
- Keep `docs.json` valid JSON; unlike `.mdx`, comments are not allowed.
- Validate custom JavaScript in `terminal-demo.js` manually in the browser
  because it is loaded through `"js": "/terminal-demo.js"`.

## Redirects and Missing Pages

When moving pages:

- Update `docs.json` navigation.
- Add or update `redirects` for old routes if published links exist.
- Update English, Chinese, RC, and release variants where relevant.
- Check references in related MDX files.

## Examples

- `docs-site/docs.json` contains redirects from old `/guide/ch01-what-is-trellis`
  style paths to current routes.
- `docs-site/development.mdx` documents Mintlify's behavior when port 3000 is in
  use and how to run broken-link validation.
- `docs-site/styles.css` uses scoped terminal demo classes with `td-` prefixes
  to avoid global style collisions.

## Forbidden Patterns

- Do not ignore a Mintlify 404 by only checking that the file exists.
- Do not remove redirects for previously published URLs without a migration
  reason.
- Do not add custom JavaScript that assumes a DOM element exists without
  checking for it first; follow `terminal-demo.js` defensive query patterns.
