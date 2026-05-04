# Error Handling

> Marketplace failure modes are registry and content validation problems.

## Overview

There is no runtime error boundary in marketplace. The Trellis CLI reads this
repository through registry fetching logic in `packages/cli/src/utils/template-fetcher.ts`.
Marketplace changes should avoid producing states that the CLI would classify
as invalid JSON, not found, path not found, or unsupported template data.

## Validation Rules

- `index.json` must parse as JSON.
- Every template `path` must exist.
- Every skill path must contain `SKILL.md`.
- Every `SKILL.md` must have valid YAML frontmatter with `name` and
  `description`.
- Every spec template should have indexes that point to existing files.
- Reference links inside skills should be relative and valid.

## Examples

- `marketplace/skills/cc-codex-spec-bootstrap/SKILL.md` links to
  `references/mcp-setup.md`; that referenced file must exist.
- `marketplace/skills/trellis-meta/SKILL.md` links to `references/core/`,
  `references/claude-code/`, `references/how-to-modify/`, and `references/meta/`.
- `marketplace/specs/nextjs-fullstack/backend/index.md` points to files such as
  `directory-structure.md`, `orpc-usage.md`, and `quality.md`.

## Common Failure Modes

- Registry `path` typo.
- Missing `SKILL.md` after adding a skill entry.
- Renamed spec file not updated in `index.md`.
- YAML frontmatter contains unescaped quotes or malformed multiline text.

## Forbidden Patterns

- Do not rely on the docs-site copy of marketplace files as the source of
  truth; edit marketplace content itself.
- Do not leave `index.json` pointing at experimental directories.
- Do not publish a skill that requires unavailable local-only tools without
  documenting prerequisites.
