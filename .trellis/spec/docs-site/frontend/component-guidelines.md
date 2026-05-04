# Component Guidelines

> Use Mintlify components and scoped custom HTML/CSS.

## Overview

Docs pages are MDX. Prefer Mintlify's built-in components over custom HTML when
they match the content shape.

## Common Components

Examples from the repo:

- `docs-site/index.mdx` uses `CardGroup` and `Card` for major entry points.
- `docs-site/quickstart.mdx` uses `Tip` and `CardGroup`.
- `docs-site/development.mdx` uses `Info`, `Steps`, `Step`, `Frame`,
  `AccordionGroup`, and `Accordion`.

## Frontmatter

Use frontmatter on pages:

```mdx
---
title: 'Development'
description: 'Preview changes locally to update your docs'
---
```

Keep titles short and descriptions literal.

## Custom HTML and Styling

- Use custom HTML only when Mintlify components are insufficient.
- Scope custom classes to a feature prefix. The terminal demo uses `td-`.
- Keep image paths root-relative, such as `/images/checks-passed.png`.
- For custom frames or images, include meaningful `alt` text.

## Code Blocks

- Use fenced code blocks with language names: `bash`, `json`, `mdx`,
  `markdown`, or `text`.
- Keep CLI examples current with `@mindfoldhq/trellis` and supported flags.

## Forbidden Patterns

- Do not add unexplained raw HTML when a Mintlify component fits.
- Do not use unscoped CSS class names for page-specific demos.
- Do not add interactive widgets that require a framework runtime.
