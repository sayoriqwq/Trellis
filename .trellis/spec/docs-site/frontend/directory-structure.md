# Frontend Directory Structure

> MDX and asset organization for the docs frontend.

## Overview

Routes are file-based but curated through `docs.json`. Do not assume that adding
a file is enough to publish it.

## Layout

```text
docs-site/
├── index.mdx
├── start/
├── advanced/
├── concepts/
├── guides/
├── showcase/
├── skills-market/
├── templates/
├── changelog/
├── release/
├── zh/
├── images/
├── logo/
├── styles.css
└── terminal-demo.js
```

## Placement Rules

- Put English RC docs in the root section directories.
- Put stable release docs under `release/`.
- Put Chinese docs under `zh/`; stable Chinese release docs go under
  `zh/release/`.
- Put static screenshots and diagrams under `images/`.
- Put theme logos under `logo/`.
- Put global Mintlify CSS overrides in `styles.css`.
- Put custom browser behavior in `terminal-demo.js` and include it through
  `docs.json`.

## Examples

- `docs-site/start/install-and-first-task.mdx` is an English RC start page.
- `docs-site/zh/start/install-and-first-task.mdx` is the localized equivalent.
- `docs-site/release/start/install-and-first-task.mdx` is the stable release
  version.
- `docs-site/images/checks-passed.png` is referenced from `development.mdx`.

## Forbidden Patterns

- Do not create React component directories. Mintlify owns rendering.
- Do not place custom JS beside an MDX page unless `docs.json` loads it.
- Do not add assets without checking path references and case sensitivity.
