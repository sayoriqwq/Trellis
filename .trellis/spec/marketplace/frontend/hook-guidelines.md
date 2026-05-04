# Hook Guidelines

> Hook guidance belongs inside frontend spec templates, not marketplace runtime.

## Overview

Marketplace does not execute React hooks. It stores reusable hook guidelines for
target projects.

## Template Patterns

- Next.js frontend templates include `hooks.md` for query and mutation hooks,
  React Query integration, and API client usage.
- Electron templates include `hooks.md` plus IPC/Electron-specific frontend
  guidance.
- Skills may describe measurement or diagnostic workflows but should not include
  app-specific hooks unless they are clearly examples.

## Examples

- `marketplace/specs/nextjs-fullstack/frontend/hooks.md` is referenced by the
  Next.js frontend index as the hook pattern document.
- `marketplace/specs/electron-fullstack/frontend/hooks.md` is the Electron
  hook guidance entry.
- `marketplace/skills/frontend-fullchain-optimization/SKILL.md` discusses
  browser APIs such as `requestAnimationFrame`, `requestIdleCallback`, and
  `scheduler.postTask` as performance strategies.

## Writing Rules

- Explain when a hook should exist and when logic belongs in a plain helper.
- Include cache/query key conventions if the target stack uses data fetching.
- Include cleanup rules for effects that subscribe to external events.
- Label framework-specific APIs clearly.

## Forbidden Patterns

- Do not add executable hook modules to marketplace.
- Do not write hook guidance that assumes one private app's module aliases.
- Do not omit cleanup/error cases from hook examples.
