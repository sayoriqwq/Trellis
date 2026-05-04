# Quality Guidelines

> Quality standards for registry entries, skills, and spec templates.

## Registry Quality

- `index.json` remains valid JSON.
- Each `id` is unique, stable, and matches the directory name where practical.
- `name` is human-readable.
- `description` explains the use case.
- `path` points to an existing directory.
- `tags` are lowercase and relevant.

## Skill Quality

- `SKILL.md` starts with YAML frontmatter containing `name` and `description`.
- The trigger description states when to use the skill.
- Long skills are structured with headings, prerequisites, steps, examples, and
  checklists.
- References live under `references/` and are linked from the skill.

## Spec Template Quality

- Layer indexes match the files that actually exist.
- Guidelines include concrete patterns, forbidden patterns, and examples.
- Template examples with code should be copyable and clearly scoped.
- Shared rules belong in `shared/`; layer-specific rules belong in `backend/`
  or `frontend/`.

## Examples

- `marketplace/skills/frontend-fullchain-optimization/SKILL.md` includes
  metric thresholds, diagnostic paths, implementation examples, and delivery
  templates.
- `marketplace/specs/nextjs-fullstack/shared/typescript.md` documents
  Zod-first types, discriminated unions, no `any`, no non-null assertions, and
  explicit exported return types.
- `marketplace/specs/cf-workers-fullstack/backend/index.md` separates backend
  framework, database, environment, security, and quality docs.

## Forbidden Patterns

- Do not publish placeholder spec files.
- Do not add generic advice without making it executable enough for agents.
- Do not let marketplace docs drift from CLI install behavior.
