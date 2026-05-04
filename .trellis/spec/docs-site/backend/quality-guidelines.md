# Quality Guidelines

> Quality standards for static docs content and configuration.

## Content Quality

- Keep every page's frontmatter accurate.
- Register new public pages in `docs.json`.
- Keep old public URLs covered by redirects when routes change.
- Keep examples synchronized with current Trellis CLI flags and package names.
- Use real file paths and command names in docs examples.
- Keep English and Chinese docs consistent where both exist.

## Mintlify Patterns

- Use Mintlify components such as `Info`, `Tip`, `Steps`, `Step`, `Frame`,
  `CardGroup`, `Card`, `AccordionGroup`, and `Accordion` where they make docs
  easier to scan.
- Keep code blocks fenced with language identifiers when possible.
- Store images under `images/` and reference them with root-relative paths such
  as `/images/checks-passed.png`.
- Keep custom CSS classes scoped. Existing terminal demo classes use `td-`.

## Examples

- `docs-site/index.mdx` uses `CardGroup` and `Card` for primary navigation.
- `docs-site/quickstart.mdx` documents prerequisites, install commands, platform
  flags, and generated `.trellis/` structure.
- `docs-site/docs.json` maintains separate `RC` and `Release` versions for
  English and Chinese navigation.

## Verification

```bash
mint dev
mint broken-links
```

Also validate JSON after editing `docs.json`, and manually preview custom CSS/JS
pages such as `showcase/terminal-demo`.

## Forbidden Patterns

- Do not add placeholder docs pages to navigation.
- Do not duplicate large sections between RC/release/Chinese docs without
  checking whether version differences are intentional.
- Do not use unscoped CSS selectors for feature-specific custom styling unless
  the selector intentionally targets Mintlify global UI.
