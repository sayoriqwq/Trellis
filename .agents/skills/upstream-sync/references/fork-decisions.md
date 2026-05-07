# Fork Decisions For Upstream Sync

Use these decisions when merging `mindfold-ai/Trellis` into this fork.

## Preserve

- Package name: `trellis-sq`.
- CLI binary: `trellis-sq`; do not restore upstream `trellis` / `tl` binaries.
- Repository URL: `https://github.com/sayoriqwq/Trellis.git`.
- Author / fork identity: `sayoriqwq` where the fork has intentionally set it.
- Root scripts: use `pnpm --filter trellis-sq ...`.
- Human-facing fork docs: `change.md`, `features.md`, `.trellis/user/**/*.md`,
  onboarding notes, and project context docs should use Simplified Chinese.
- Internal Trellis workflow names: keep names such as `trellis-check`,
  `trellis-implement`, `/trellis:finish-work`, and `.trellis/` paths unless the
  upstream change requires a specific internal contract update.
- Single source package boundary: `packages/cli` is the active package.
- `docs-site` and `marketplace` submodules are not active local packages in this
  fork. Do not reintroduce `.gitmodules`, submodule entries, or release checks
  that require those submodules unless the user explicitly changes this policy.
- `sayoriqwq` local workspace and active tasks. Do not import upstream developer
  journals, workspaces, or dogfood task backlog as active local state.
- `.trellis/user/` maintenance workflow. If upstream changes workflow,
  session-start hooks, skills, or templates, reapply the rule that agents must
  decide whether both `.trellis/spec/` and `.trellis/user/` need updates.

## Usually Take From Upstream

- Runtime and CLI bug fixes.
- Migration manifests and version comparison fixes.
- Hook reliability fixes, path normalization, disabled-hook env vars, and
  degraded-mode handling.
- Sub-agent recursion guards and dispatch protocol improvements.
- Platform template compatibility fixes.
- Tests covering upstream bug fixes.

## Usually Remove During Merge

- Upstream dogfood task directories unrelated to this fork's active work.
- Upstream developer workspace journals for maintainers other than `sayoriqwq`.
- Docs-site / marketplace submodule files and release-only artifacts not used by
  this fork.

