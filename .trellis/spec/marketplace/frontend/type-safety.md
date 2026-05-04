# Type Safety

> Type-safety guidance for marketplace frontend templates.

## Overview

Marketplace stores TypeScript guidance for generated projects. The registry
itself has no TypeScript build, but template examples should model safe
TypeScript for target apps.

## Shared Pattern

Use shared template docs when rules apply across backend and frontend. For
example, `marketplace/specs/nextjs-fullstack/shared/typescript.md` documents:

- Zod-first type definitions.
- Importing/infering API types instead of redefining them.
- Discriminated unions.
- Standard response formats.
- No `any`.
- No non-null assertions.
- No `@ts-expect-error` or `@ts-ignore`.
- `import type` for type-only imports.
- Explicit return types for exports.

## Frontend-Specific Pattern

Frontend type-safety docs should explain:

- How to import types from backend/API packages.
- How to infer query and mutation result types.
- How to validate untrusted data at boundaries.
- How to type view models without duplicating API contracts.
- How to keep hook return types inferred where appropriate.

## Examples

- `marketplace/specs/nextjs-fullstack/frontend/type-safety.md` is the frontend
  type-safety guide for the Next.js template.
- `marketplace/specs/nextjs-fullstack/shared/typescript.md` provides the shared
  TypeScript baseline.
- `marketplace/specs/cf-workers-fullstack/backend/type-safety.md` and
  `frontend/type-safety.md` split layer-specific concerns in that template.

## Forbidden Patterns

- Do not put `any` in examples unless it is explicitly labeled bad.
- Do not use non-null assertions in recommended code.
- Do not redefine backend DTOs in frontend examples when imported or inferred
  types should be used.
- Do not include private app aliases such as `@/modules/foo` unless the template
  defines them.
