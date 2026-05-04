# Type Safety

> Docs-site uses JSON, MDX, CSS, and plain JavaScript rather than TypeScript.

## Overview

There is no TypeScript compiler in docs-site. Type safety here means preserving
valid structured content and writing defensive JavaScript.

## JSON Safety

- Keep `docs.json` valid JSON.
- Preserve the Mintlify schema reference.
- Use arrays/objects consistently in `navigation.languages[].versions[].groups`.
- Keep redirect objects shaped as `{ "source": "...", "destination": "..." }`.

## MDX Safety

- Keep frontmatter delimited with `---`.
- Close all JSX-like Mintlify components.
- Escape braces in examples when MDX would parse them as expressions.
- Prefer fenced code blocks for code examples instead of inline pseudo-code
  when syntax contains braces.

## JavaScript Safety

- Use feature-scoped DOM queries.
- Check elements before reading properties.
- Avoid permanent globals.
- Keep functions small and named, as in `initTerminalDemo(wrap)`.

## Examples

- `docs-site/docs.json` uses schema-backed JSON for navigation and redirects.
- `docs-site/development.mdx` closes nested `Steps` and `Step` components.
- `docs-site/terminal-demo.js` guards optional elements with checks such as
  `if (fill)` and `if (body && lines[lastVisible])`.

## Forbidden Patterns

- Do not add TypeScript-only syntax to `.js` files.
- Do not add trailing comments to `docs.json`.
- Do not write MDX examples that accidentally execute as JSX.
