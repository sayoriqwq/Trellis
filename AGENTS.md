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

If you're using Codex or another agent-capable tool, additional project-scoped helpers may live in:
- `.agents/skills/` — reusable Trellis skills
- `.codex/agents/` — optional custom subagents

## Subagents

- ALWAYS wait for every spawned subagent to reach a terminal status before yielding, acting on partial results, or spawning followups.
  - On Codex, this means calling the `wait` tool with the subagent's thread id (requires `multi_agent_v2`). Do NOT infer completion from elapsed time.
  - On Claude Code / OpenCode, this means awaiting the Task/agent tool result before continuing.
- NEVER cancel or re-spawn a subagent that hasn't finished. If a subagent appears stuck, raise the wait timeout (Codex default 30s, max 1h) before judging it broken.
- Spawn subagents automatically when:
  - Parallelizable work (e.g., install + verify, npm test + typecheck, multiple tasks from plan)
  - Long-running or blocking tasks where a worker can run independently
  - Isolation for risky changes or checks

Keep this managed block so 'trellis-sq update' can refresh the instructions.

Managed by Trellis. Edits outside this block are preserved; edits inside may be overwritten by a future `trellis-sq update`.

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

## upstream sync workflow

- 当用户要求同步 `mindfold-ai/Trellis`、merge upstream、解决 upstream 冲突、查看上游
  新增功能并合并到本 fork 时，必须使用 `.agents/skills/upstream-sync/SKILL.md`。
- 这个 workflow 的默认目标是保留 `sayoriqwq` fork 决策，同时吸收上游 CLI、hooks、
  subagent、template、migration 和测试修复。
- 同步时默认保留 `trellis-sq` package/binary 身份、单 package 工作树、中文
  human-facing docs、`change.md`/`features.md` 账本，以及 `sayoriqwq` workspace。
- 同步完成前必须检查冲突是否重新引入 `docs-site`/`marketplace` submodule、上游
  dogfood tasks/workspace、`@mindfoldhq/trellis` package 身份、或删除 `.trellis/user/`
  维护规则。
