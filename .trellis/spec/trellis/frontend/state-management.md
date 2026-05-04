# State Management

> The CLI has no browser/client state. State is either module-local or persisted
> project files.

## Overview

Avoid adding global mutable state. The package mostly passes options through
functions and persists durable state in files under `.trellis/` or platform
directories.

## Existing State Patterns

- `packages/cli/src/utils/file-writer.ts` has module-local `globalWriteMode`
  controlled by `setWriteMode` and `getWriteMode`.
- `packages/cli/src/commands/update.ts` reads template hashes and current
  project files to classify update state.
- `packages/cli/src/utils/project-detector.ts` derives project/package state
  from repository files rather than keeping a cache.
- Task/session state belongs to generated `.trellis/tasks/**` and
  `.trellis/workspace/**` files.

## Rules

- Prefer passing options as function parameters over introducing module globals.
- If global state is necessary, expose a resettable setter/getter and reset it
  in tests.
- Persist durable user state through the existing `.trellis/` file contracts.
- Keep derived state recomputable from files whenever possible.

## Examples

`packages/cli/test/utils/file-writer.test.ts` resets `setWriteMode("ask")` in
`afterEach`, showing the expected hygiene for module-local state.

`packages/cli/src/commands/update.ts` builds a `ChangeAnalysis` from hashes and
filesystem content instead of storing update state elsewhere.

`packages/cli/src/utils/project-detector.ts` returns `DetectedPackage[]` from
workspace files, `.gitmodules`, and package manifests.

## Forbidden Patterns

- Do not add browser-like stores, React context, Redux, Zustand, or similar
  state libraries to the CLI package.
- Do not let tests depend on state leaked from previous tests.
- Do not store derived command state in hidden files unless the workflow
  contract explicitly requires it.
