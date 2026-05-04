# Frontend Quality Guidelines

> Quality checks for MDX, Mintlify config, CSS, and custom JS.

## Before Editing

- Inspect nearby pages for tone, structure, and component usage.
- Check `docs.json` to understand where the page appears.
- For localized docs, compare the corresponding `zh/` page.

## Checks

- `docs.json` is valid JSON.
- New pages have frontmatter.
- Public pages are included in navigation.
- Removed or moved pages have redirects when needed.
- Links and image paths resolve.
- Custom CSS does not leak unexpectedly.
- Custom JS is manually previewed.

## Examples

- `docs-site/styles.css` explains why global selectors hide Mintlify language
  flag indicators and why `pre code` uses Menlo for diagrams.
- `docs-site/styles.css` scopes terminal demo styles with `td-` classes.
- `docs-site/terminal-demo.js` uses `MutationObserver` so it works with
  Mintlify's rendering lifecycle.

## Verification Commands

```bash
mint dev
mint broken-links
```

For CSS/JS changes, manually inspect the affected page in light and dark mode
when possible.

## Forbidden Patterns

- Do not leave placeholder frontmatter.
- Do not use stale install commands or package names.
- Do not add global CSS selectors for feature-specific elements.
- Do not rely only on Markdown preview outside Mintlify for component-heavy
  pages.
