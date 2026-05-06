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
