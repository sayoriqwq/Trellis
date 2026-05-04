# Logging Guidelines

> Docs-site has no backend logger.

## Overview

There is no application logger or server-side logging layer in docs-site.
Operational feedback comes from Mintlify CLI commands, markdown linters, git
diffs, and browser console output for custom JavaScript.

## What Counts as Logging Here

- Mintlify CLI output from `mint dev` and `mint broken-links`.
- Markdown/lint output from repository checks.
- Browser console diagnostics while testing `terminal-demo.js`.

## Rules

- Do not add permanent `console.log` statements to `terminal-demo.js`.
- Use comments in CSS/JS to explain non-obvious layout or timing contracts, as
  `styles.css` already does for CJK diagrams and terminal demo animation.
- Keep troubleshooting instructions in docs pages, not hidden in scripts.

## Examples

- `docs-site/development.mdx` tells users how to run `mint dev`,
  `mint broken-links`, and `mint update`.
- `docs-site/terminal-demo.js` currently relies on DOM checks such as
  `if (body)` and `if (fill)` instead of logging missing elements.
- `docs-site/styles.css` documents why `pre.cjk-diagram b` has a fixed `2ch`
  width.

## Forbidden Patterns

- Do not introduce a logging framework.
- Do not leave debug output in custom browser scripts.
- Do not use console output as the only validation for docs changes.
