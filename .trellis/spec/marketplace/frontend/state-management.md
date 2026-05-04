# State Management

> State-management guidance is template content for target projects.

## Overview

Marketplace itself has no client state. State-management files explain how
target applications should manage state after installing a spec template.

## Template Patterns

- Next.js templates prefer URL state with `nuqs`, React Query for server state,
  and React Context for scoped shared UI state.
- Electron templates include desktop and IPC-aware state concerns.
- Cloudflare Workers templates document frontend state appropriate to the
  generated stack.

## Examples

- `marketplace/specs/nextjs-fullstack/frontend/state-management.md` is indexed
  by the Next.js frontend template.
- `marketplace/specs/electron-fullstack/frontend/state-management.md` is the
  Electron state guide.
- `marketplace/specs/nextjs-fullstack/frontend/index.md` summarizes the rule
  "Store shareable state in URL with nuqs".

## Writing Rules

- Distinguish local UI state, URL/shareable state, server cache state, and
  global application state.
- Prefer target-stack libraries already named by the template.
- Include forbidden patterns and concrete examples.
- Keep backend/frontend contract guidance in shared or cross-layer guides when
  state depends on API payloads.

## Forbidden Patterns

- Do not add a marketplace-level state library.
- Do not recommend state tools that are absent from the template's tech stack
  without explaining the dependency change.
- Do not duplicate backend data models in frontend state examples when imported
  types are the intended contract.
