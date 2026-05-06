# Quality Guidelines

> Standards for TypeScript CLI code in `packages/cli`.

## TypeScript and Formatting

The package uses strict TypeScript and stylistic ESLint:

- `target`: `ES2022`
- `module` and `moduleResolution`: `NodeNext`
- `strict`: `true`
- explicit return types required for exported functions and most named
  functions
- `no-explicit-any`: error
- `no-non-null-assertion`: error
- `prefer-nullish-coalescing` and `prefer-optional-chain`: error

Formatting comes from `packages/cli/.prettierrc`: double quotes, semicolons,
2-space indentation, trailing commas, and 80-column print width.

## Testing Patterns

- Use Vitest.
- Put command integration coverage under `packages/cli/test/commands/`.
- Put focused utility tests under `packages/cli/test/utils/`.
- Use temp directories via `fs.mkdtempSync(path.join(os.tmpdir(), "..."))`.
- Restore mocks and remove temp dirs in `afterEach`.
- Mock external dependencies at the top of test files with `vi.mock`.

Examples:

- `packages/cli/test/commands/init.integration.test.ts`
- `packages/cli/test/utils/file-writer.test.ts`
- `packages/cli/test/utils/project-detector.test.ts`

## Change Scope

- Keep each change tied to a command, configurator, utility, template, or test.
- If a generated template changes, check tests that assert installed files and
  template hashes.
- If workflow or knowledge-capture templates change, check both `.trellis/spec/`
  and `.trellis/user/` docs for sync: spec captures executable agent rules,
  user docs explain project context for humans.
- If a path constant changes, search for the literal and update tests,
  templates, migrations, and docs as needed.
- For platform support, update the platform configurator, template collection,
  tests, and package docs together.

## Verification Commands

```bash
pnpm --filter trellis-sq lint
pnpm --filter trellis-sq typecheck
pnpm --filter trellis-sq test
```

Use the root shortcuts (`pnpm lint`, `pnpm typecheck`, `pnpm test`) when working
from the repository root.

## Forbidden Patterns

- Do not use `any` to get around generic or JSON typing problems. Use `unknown`,
  type guards, or explicit interfaces.
- Do not add non-null assertions. Narrow with checks.
- Do not add broad refactors while fixing command behavior.
- Do not update `.trellis/spec/` from `trellis-sq update`; update protects specs as
  user-owned content.
- Do not rely only on snapshot-like filesystem existence checks when behavior
  needs content assertions.
