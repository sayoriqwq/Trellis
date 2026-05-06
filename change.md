# Fork Change Log

This file is append-only. Record fork-local changes relative to the original
open-source Trellis project here, in a changeset-like format. Do not rewrite old
entries when syncing from upstream; append a new entry that explains what
changed and why.

## 2026-05-06 - fork identity and command rename

### Summary

Clarify that this repository is `sayoriqwq`'s personal fork of the original
`mindfold-ai/Trellis` project, used to customize and adapt Trellis for personal
AI-assisted development workflows.

### Changes

- Removed `docs-site` and `marketplace` git submodules from the fork working
  tree.
- Removed `.gitmodules` because the fork no longer tracks those submodules.
- Removed local `.trellis/user/` and `.trellis/spec/` docs that treated
  `docs-site` and `marketplace` as active packages in this repository.
- Changed the CLI package identity from `@mindfoldhq/trellis` to `trellis-sq`.
- Changed the exposed binary from `trellis` / `tl` to `trellis-sq`.
- Updated CLI help, generated prompt text, README files, contributing docs, and
  Trellis meta skill descriptions to use `trellis-sq init/update/uninstall` for
  external CLI usage.
- Kept internal workflow names such as `trellis-before-dev`, `trellis-check`,
  and `/trellis:finish-work` unchanged. These remain workflow/platform entry
  contracts rather than npm binary names.
- Updated `.trellis/config.yaml` so the current project package map contains
  only `packages/cli`.
- Removed docs-site changelog preflight calls from fork release scripts because
  the docs-site submodule is no longer present.

### Upstream Sync Notes

- Keep upstream as a separate remote, for example:

  ```bash
  git remote add upstream https://github.com/mindfold-ai/Trellis.git
  git fetch upstream
  ```

- Prefer syncing with a small, inspectable integration branch:

  ```bash
  git switch -c sync/upstream-YYYY-MM-DD
  git merge upstream/main
  ```

- Expect conflicts around `package.json`, README files, generated templates,
  and `.trellis/` docs. Resolve those by preserving this fork's identity:
  `trellis-sq` for the CLI binary/package and no active docs-site/marketplace
  submodules.
- After every upstream sync, append a new entry to this file listing the
  upstream ref merged and any fork-local conflict decisions.

## 2026-05-06 - backfill from sayoriqwq fork bootstrap commits

### Summary

Backfill this ledger from `sayoriqwq`'s first local commit,
`430783134018e691b974eafdc5abfde3505ff723`, through the early fork setup
commits before the dedicated `trellis-sq` identity entry above. This makes the
fork-local history count from the first `sayoriqwq` commit rather than only from
the later package rename.

### Commit Scope

- `430783134018e691b974eafdc5abfde3505ff723` -
  `chore(task): archive 00-bootstrap-guidelines`
- `4c1a91db880eda11c89328198103a194dd4742b5` -
  `chore: sync trellis workspace assets`
- `f29cbc96cb0a44049e3a2d90e646f6ed89c0dbfd` -
  `chore: maintain user docs in codex workflow`
- `b56a818d4b597175e64a015abbeaf1b1613d6ef2` -
  `docs: add trellis core learning task`

The later `3de7e1a4e6b48b0cb3baf9ed261a05aa0756a1ce` fork identity commit is
covered by the preceding `fork identity and command rename` entry.

### Changes

- Pruned the inherited upstream dogfood task backlog from the local task tree
  and kept a small local bootstrap archive under
  `.trellis/tasks/archive/2026-05/00-bootstrap-guidelines`.
- Reset the Trellis workspace to `sayoriqwq` by replacing prior developer
  journals and workspace docs with `.trellis/workspace/sayoriqwq/` assets.
- Synced local agent/workflow assets for Codex use, including `.agents/skills/`,
  `.codex/agents/`, `.codex/hooks/`, workflow scripts, multi-agent helpers,
  and template hashes.
- Reorganized project specs and human-facing docs into the local package map so
  Trellis context loading can describe the fork's packages and reading order.
- Added generated `.trellis/user/` support to the CLI template set and hash
  tracking so new Trellis installs include human-facing project context.
- Updated check, finish-work, update-spec, session-start, subagent, and
  Trellis meta skill guidance so agents consider `.trellis/user/` alongside
  `.trellis/spec/` after implementation.
- Created the active `05-04-maintain-user-docs-workflow` task to preserve the
  user-doc maintenance workflow requirements and session traces.
- Added the `05-04-trellis-core-learning-doc` task with a Chinese learning note
  for the Trellis core module.

## 2026-05-06 - require agents to maintain fork change log

### Summary

Make fork-local change tracking an explicit agent instruction so future sessions
continue updating this ledger after meaningful repository changes.

### Changes

- Added an `AGENTS.md` rule outside the Trellis managed block that points agents
  to `change.md` as the append-only fork ledger.
- Documented `430783134018e691b974eafdc5abfde3505ff723` as the baseline commit
  for counting `sayoriqwq` fork-local history.
- Instructed future agents to append dated backfill or correction entries
  instead of rewriting existing `change.md` records.

## 2026-05-06 - add fork feature map and Chinese user-doc policy

### Summary

Add a current-state feature map for the fork and make the Chinese documentation
preference explicit for human-facing docs.

### Changes

- Added `features.md` as the maintained current feature map for this fork,
  separate from the append-only historical ledger in `change.md`.
- Documented that this fork targets the `sayoriqwq` Trellis developer profile,
  whose collaboration and human-facing docs should use Simplified Chinese.
- Updated `AGENTS.md` so future agents preserve the Chinese user-doc policy and
  know that `.trellis/spec/` may keep stricter agent-facing language rules.
- Added `features.md` to the `.trellis/user/` reading order and README fork
  notes.

## 2026-05-06 - refine feature map as user capability contract

### Summary

Reposition `features.md` from a broad fork difference list into a maintained
user-perceivable capability contract for day-to-day use and upstream sync.

### Changes

- Rewrote `features.md` around capability units that `sayoriqwq` can feel while
  using the fork.
- Documented that `features.md` is not append-only; it is distilled from
  `change.md` and current repository state.
- Added per-feature guidance for user experience, maintenance boundaries, and
  upstream conflict handling.
- Updated `AGENTS.md` so future agents know when and how to revise
  `features.md` after changes.
