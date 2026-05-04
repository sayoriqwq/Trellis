# Frontend Quality Guidelines

> Quality standards for frontend-oriented marketplace templates and skills.

## Content Quality

- Make guidance executable: include rules, examples, anti-patterns, and
  verification points.
- Keep examples framework-specific but application-neutral.
- Reference actual files from the template index.
- Keep `README.md`, layer indexes, and file names synchronized.

## Performance Skill Quality

`marketplace/skills/frontend-fullchain-optimization/SKILL.md` is an example of a
high-density frontend skill. It includes:

- metric thresholds for LCP, FCP, INP, CLS, TTFB, FID, and TBT
- diagnostic decision tree
- optimization strategies by metric
- examples for CDN purge, image adaptation, and SSR/Redis cache
- manual measurement requirements
- delivery template

Follow that level of specificity for new performance or diagnostic skills.

## Spec Template Quality

- Frontend indexes should tell agents which documents are must-read.
- Quality docs should include pre-commit or pre-merge checklists.
- Type-safety docs should align with shared TypeScript guidance.
- CSS/layout docs should include browser-specific gotchas if the target stack
  needs them.

## Examples

- `marketplace/specs/nextjs-fullstack/frontend/index.md` has quick navigation by
  task and core rules summary.
- `marketplace/specs/nextjs-fullstack/frontend/quality.md` is the quality
  checklist target for that template.
- `marketplace/specs/electron-fullstack/frontend/react-pitfalls.md` captures
  framework-specific mistakes.

## Forbidden Patterns

- Do not publish vague "best practices" without code examples.
- Do not add frontend guidance that conflicts with the template's shared
  TypeScript/dependency docs.
- Do not leave "To fill" placeholders in marketplace templates.
