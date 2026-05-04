# Docs-Site Frontend Guidelines

> Frontend conventions for Mintlify MDX, global CSS, and custom browser JS.

## Overview

Docs-site is a Mintlify documentation frontend, not a React app owned by this
repository. The frontend surface is MDX content, Mintlify components, global CSS
overrides, static images, and a small custom script for the terminal demo.

## Guidelines Index

| Guide | Description | Status |
|-------|-------------|--------|
| [Directory Structure](./directory-structure.md) | MDX, assets, language/version layout | Filled |
| [Component Guidelines](./component-guidelines.md) | Mintlify components and custom HTML usage | Filled |
| [Hook Guidelines](./hook-guidelines.md) | No React hooks; MutationObserver script patterns | Filled |
| [State Management](./state-management.md) | Navigation, URL, and demo interaction state | Filled |
| [Quality Guidelines](./quality-guidelines.md) | Preview, links, CSS/JS, bilingual checks | Filled |
| [Type Safety](./type-safety.md) | JSON/MDX/JS validation rules | Filled |

## Pre-Development Checklist

- Read `docs-site/docs.json` before changing routes, languages, versions, or
  page visibility.
- Read nearby MDX pages in the same section and language before adding content.
- For custom visual behavior, inspect `docs-site/styles.css` and
  `docs-site/terminal-demo.js`.
- Preview in Mintlify for CSS/JS or navigation changes.

**Language**: Guideline docs are English. Product docs may target English or
Chinese routes.
