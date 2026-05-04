# Maintain User Docs In Trellis Workflow

## Goal

Make `.trellis/user/` a first-class knowledge surface in Trellis workflow maintenance, not only a directory created during `init`.

## Requirements

- Update generated workflow guidance so Phase 3 requires checking both `.trellis/spec/` and `.trellis/user/`.
- Update generated agent instructions so new sessions know `.trellis/user/` is the human-facing project map.
- Update relevant shared skills/commands so check, update-spec, and finish-work remind agents to maintain user docs when project context changes.
- Update `trellis-meta` references so local architecture documentation lists `.trellis/user/` as an editable generated path.
- Keep `.trellis/user/` protected user-owned content; do not make `trellis update` overwrite it.
- Add tests that assert the generated templates mention the `.trellis/user/` maintenance contract.

## Acceptance Criteria

- `trellis init` generated files include `.trellis/user/` in workflow and AGENTS guidance.
- The update-spec/check/finish-work generated guidance includes a `.trellis/user/` sync check.
- Template tests or init integration tests fail if the `.trellis/user/` maintenance text disappears.
- Local dogfood files are aligned with the generated templates where applicable.

## Out Of Scope

- No changes to runtime task state storage.
- No automatic content generation for `.trellis/user/`.
- No migration that edits existing users' `.trellis/user/` content.
