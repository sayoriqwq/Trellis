---
name: upstream-sync
description: Merge upstream mindfold-ai/Trellis changes into the sayoriqwq/Trellis fork, inspect upstream feature changes, resolve merge conflicts, preserve fork-local decisions such as trellis-sq identity and Chinese human-facing docs, update change.md/features.md/AGENTS.md as needed, run validation, and complete the merge commit. Use when the user asks to sync upstream, merge mindfold-ai/Trellis:main, pull official commits, resolve upstream conflicts, or make future upstream-sync workflow reusable.
---

# Upstream Sync

## Overview

Use this skill to merge official `mindfold-ai/Trellis` changes into the
`sayoriqwq/Trellis` fork without losing fork-local behavior. The output should
be an inspectable merge result, not a blind overwrite of local policy.

Load `references/fork-decisions.md` before resolving conflicts.

## Workflow

1. Confirm the current branch and worktree state:
   ```bash
   rtk git status --short --branch
   rtk git remote -v
   ```

2. Fetch the official upstream target. If no `upstream` remote exists, fetch by
   URL into a remote-tracking ref instead of adding persistent config unless the
   user asks for a remote:
   ```bash
   rtk git fetch https://github.com/mindfold-ai/Trellis.git main:refs/remotes/upstream/main
   ```

3. Summarize what upstream adds before merging:
   ```bash
   rtk git rev-list --left-right --count HEAD...refs/remotes/upstream/main
   rtk git log --oneline --no-merges HEAD..refs/remotes/upstream/main --max-count=80
   rtk git diff --stat HEAD..refs/remotes/upstream/main
   ```
   Prefer release manifests under
   `packages/cli/src/migrations/manifests/*.json` for feature-level summaries.

4. Merge upstream:
   ```bash
   rtk git merge refs/remotes/upstream/main
   ```

5. Resolve conflicts by category:
   - Take upstream for CLI/runtime bug fixes, hook fixes, migrations, templates,
     tests, and platform compatibility work.
   - Preserve fork identity and policy from `references/fork-decisions.md`.
   - Keep source templates and dogfooded local files aligned when both exist.
   - Remove reintroduced upstream-only dogfood state unless the user explicitly
     wants it.

6. Check conflict completion:
   ```bash
   rtk git diff --name-only --diff-filter=U
   rtk rg -n "^(<<<<<<<|=======|>>>>>>>)" .
   ```

7. Update fork docs:
   - Append a dated entry to `change.md` with upstream ref, major upstream
     functionality, and conflict decisions.
   - Update `features.md` if the merge changes user-perceivable fork behavior.
   - Update `AGENTS.md` if future agent workflow rules changed.

8. Validate:
   ```bash
   rtk pnpm --filter trellis-sq lint
   rtk pnpm --filter trellis-sq typecheck
   rtk pnpm --filter trellis-sq test
   ```
   If a full command is too slow or blocked, run the most relevant focused test
   and state the residual risk.

9. Complete the merge with a merge commit unless the user asked not to commit:
   ```bash
   rtk git status --short
   rtk git commit
   ```
   Use a clear merge message naming the upstream ref and preserved fork policy.

## Conflict Priorities

When conflict decisions compete, use this order:

1. Keep the repository buildable and tests meaningful.
2. Preserve explicit fork-local user-facing decisions.
3. Prefer upstream implementation fixes over stale local generated copies.
4. Keep generated templates, local dogfood files, and tests consistent.
5. Document any intentional divergence in `change.md`.

