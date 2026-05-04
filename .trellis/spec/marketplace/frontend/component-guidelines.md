# Component Guidelines

> Marketplace component guidance is written as reusable spec-template content.

## Overview

Do not implement components in marketplace. Document how generated project specs
should guide components in target applications.

## Template Patterns

- Next.js templates emphasize Server Components by default, semantic HTML,
  `next/image`, Radix UI, and TailwindCSS.
- Electron templates include desktop-specific frontend concerns such as browser
  API restrictions and IPC usage.
- Cloudflare Workers templates include React/frontend conventions appropriate to
  that stack.

## Examples

- `marketplace/specs/nextjs-fullstack/frontend/index.md` lists
  `components.md` as a must-read guide for Server/Client components, semantic
  HTML, and images.
- `marketplace/specs/electron-fullstack/frontend/components.md` is the component
  guidance entry for Electron + React templates.
- `marketplace/specs/cf-workers-fullstack/frontend/components.md` is the
  component guidance entry for Workers + frontend templates.

## Writing Rules

- Include concrete good/bad examples in template specs.
- Prefer framework-native primitives in the target stack.
- Document accessibility and semantic HTML requirements when relevant.
- Keep examples generic enough to copy into user projects after adapting names.

## Forbidden Patterns

- Do not add live React component implementations to marketplace.
- Do not make component guidance depend on a private application path.
- Do not publish component examples without explaining the target framework.
