# Type Safety

> TypeScript rules for frontend-adjacent Trellis CLI code.

## Overview

Even though the package has no frontend runtime, any `.ts` or future `.tsx`
code must follow the same strict TypeScript rules as backend CLI code.

## Required Patterns

- Use `import type` for type-only imports.
- Add explicit return types to exported functions.
- Prefer discriminated unions or literal union types for modes and actions.
- Use `unknown` plus narrowing for untrusted input.
- Use `as const` for stable constant maps.

## Examples

`packages/cli/src/utils/file-writer.ts` defines:

```ts
export type WriteMode = "ask" | "force" | "skip" | "append";
```

`packages/cli/src/utils/template-fetcher.ts` defines narrow registry error
types:

```ts
export type RegistryErrorKind =
  | "auth"
  | "git-unavailable"
  | "invalid-json"
  | "network"
  | "not-found"
  | "path-not-found"
  | "ref-not-found"
  | "unknown";
```

`packages/cli/src/constants/paths.ts` uses `as const` for workflow path
constants.

## JSON and Template Data

- Define interfaces for parsed JSON such as template indexes and task metadata.
- Validate shape enough before trusting user-controlled JSON.
- For template registries, prefer explicit types such as `SpecTemplate`,
  `RegistrySource`, and `RegistryProbeResult`.

## Forbidden Patterns

- No `any`.
- No non-null assertions.
- No blind casts from parsed JSON without checks or narrow use.
- No duplicated string unions across files; centralize them where behavior is
  shared.
