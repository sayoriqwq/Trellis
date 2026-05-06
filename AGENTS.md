<!-- TRELLIS:START -->
# Trellis Instructions

These instructions are for AI assistants working in this project.

Use the `/trellis:start` command when starting a new session to:
- Initialize your developer identity
- Understand current project context
- Read relevant guidelines

Use `@/.trellis/` to learn:
- Development workflow (`workflow.md`)
- Project structure guidelines (`spec/`)
- Human-facing project context docs (`user/`)
- Developer workspace (`workspace/`)

If you're using Codex, project-scoped helpers may also live in:
- `.agents/skills/` for reusable Trellis skills
- `.codex/agents/` for optional custom subagents

Keep this managed block so 'trellis-sq update' can refresh the instructions.

<!-- TRELLIS:END -->

## language

- 面向本 fork user 或 developer 阅读的文档必须使用简体中文，包括
  `features.md`、`.trellis/user/**/*.md`、onboarding 笔记，以及写给
  `sayoriqwq` 或后续 developer 的项目上下文文档。
- 将 `sayoriqwq` 视为本 fork 默认 Trellis developer profile；这个 developer
  偏好中文协作和中文 human-facing docs。
- 可以保留必要 English 技术术语，例如 CLI、template、subagent、manifest、
  workspace、spec。`.trellis/spec/` 是 agent-executable 规则；当本地 spec 明确有
  自己的语言约定时，按对应 spec 执行。

## fork change log

- 将 `change.md` 视为 `sayoriqwq` fork 的 append-only 变更账本。
- 本 fork 的本地历史从 `sayoriqwq` 第一个 local commit 开始计算：
  `430783134018e691b974eafdc5abfde3505ff723`.
- 任何非平凡仓库改动完成前，都要给 `change.md` 追加带日期的条目，记录改了什么、
  为什么改、未来 upstream sync 必须保留哪些 fork-local 决策。
- 不要改写旧的 `change.md` 条目；如果旧记录不完整，追加新的 backfill/correction
  entry，并说明覆盖的 commit 范围。

## fork feature map

- 将 `features.md` 视为本 fork 当前的用户可感知能力地图，不要当作 append-only
  changelog。
- `features.md` 应从 `change.md` 流水账和最新仓库状态中归纳。当改动新增、删除、
  重命名或实质改变 `sayoriqwq` 在使用中能感到的能力时，更新 `features.md`。
- 每个 feature 都应服务未来使用和 upstream sync：说明用户能感到什么、哪些文件或
  模块维持这项能力、遇到 upstream 冲突时应如何处理。
- 不要把纯实现 churn 列为 feature，除非它改变 user-facing 行为或 upstream-sync
  contract。
