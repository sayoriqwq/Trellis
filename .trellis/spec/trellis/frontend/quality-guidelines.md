# Frontend-Adjacent Quality Guidelines

> Quality rules for templates, generated content, and any future frontend code.

## Template Quality

- Keep generated assets deterministic.
- Update tests when changing generated platform files.
- Preserve managed-block behavior for files like `AGENTS.md`.
- Keep platform-specific differences in configurators, not copied prose.
- Use placeholder helpers in `packages/cli/src/configurators/shared.ts` for
  command references, Python command names, and conditional content.

## Examples

- `packages/cli/src/configurators/shared.ts` resolves `{{PYTHON_CMD}}`,
  `{{CMD_REF:name}}`, and conditional blocks.
- `packages/cli/src/commands/update.ts` replaces only the Trellis managed block
  in `AGENTS.md` when markers are present.
- `packages/cli/test/commands/init.integration.test.ts` asserts which platform
  directories and skills are created for selected flags.

## If Real Frontend Code Is Added

- Keep it in a separate package or clearly isolated directory.
- Add actual framework-specific specs before implementation.
- Use strict TypeScript, explicit exported return types, and the existing lint
  rules as the baseline.
- Add tests that render or exercise user-visible behavior, not only file
  existence.

## Forbidden Patterns

- Do not duplicate the same generated prose across multiple configurators.
- Do not add one-off template substitutions when `resolvePlaceholders` can own
  the behavior.
- Do not skip tests for generated outputs; template regressions are user-facing.
