# Fork 用户能力清单

这个文件维护 `sayoriqwq/Trellis` 相对原始
`mindfold-ai/Trellis` 项目的“用户可感知能力”。它不是 append-only，不记录每天做了
什么；它是从 [`change.md`](./change.md) 的流水账和最新修改中提炼出来的当前规范。

维护这个文件的目的：

- 使用本 fork 时，能快速知道自己实际多了哪些能力。
- 后续改动时，能判断一次修改是否改变了用户能力，需要不要更新这里。
- 同步 upstream 时，能明确哪些 fork-local 能力要保留、哪些冲突要按本 fork 的规则
  解决。

这里的“feature”指使用中能感到差异的模块单元。纯内部重排、一次性清理、任务归档、
实现细节，除非改变了使用体验或同步策略，否则不要单独列成 feature。

## 维护规则

- `change.md` 是历史流水账；`features.md` 是当前能力归纳。
- 新增、删除或改变用户可感知能力时，先在 `change.md` 记录发生了什么，再更新本文件
  的当前状态。
- 同步 upstream 后，如果 upstream 改动影响下面任一能力，要在合并结果中显式保留或
  有意识地移除，并把决策写回 `change.md`。
- 本文件写给 `sayoriqwq` 和后续 developer 阅读，必须使用简体中文；必要技术术语可以
  保留英文。

## 面向中文协作的 developer profile

**使用时的感知**

- 这个 fork 默认服务 `sayoriqwq` 这个 developer。
- 和 agent 沟通、阅读 fork-local user docs、查看学习材料时，默认进入中文协作语境。
- 面向 user 或 developer 阅读的上下文文档使用简体中文，例如 `features.md`、
  `.trellis/user/**/*.md`、学习笔记和 onboarding 资料。

**维护边界**

- `.trellis/spec/` 是 agent-executable 规则，可以保留对应 spec 文件自己的语言约定。
- 中文 user docs 可以保留必要 English 技术术语，例如 CLI、template、subagent、
  manifest、workspace、spec。

**同步 upstream 时**

- 如果 upstream 更新 `AGENTS.md`、README、模板说明或 user docs 生成逻辑，要保留本
  fork 的中文 user-doc policy。
- 如果冲突涉及 `.trellis/spec/` 的英文规则和 `.trellis/user/` 的中文说明，不要简单
  统一语言；按“spec 给 agent 执行、user docs 给人理解”的分工处理。

## `trellis-sq` 命令身份

**使用时的感知**

- 安装或本地链接后，对外使用 `trellis-sq init`、`trellis-sq update`、
  `trellis-sq uninstall`。
- npm package 名是 `trellis-sq`，不是上游的 `@mindfoldhq/trellis`。
- README、contributing 文档和模板说明都把这个仓库呈现为 `sayoriqwq` 的个人 fork。

**维护边界**

- CLI binary 和 package identity 要使用 `trellis-sq`。
- 内部 workflow、skill、agent 和平台 command 仍保持 Trellis 语义，例如
  `trellis-before-dev`、`trellis-check`、`/trellis:finish-work`。

**同步 upstream 时**

- 冲突出现在 `package.json`、`packages/cli/package.json`、CLI help、README、模板文案
  时，优先保留对外 `trellis-sq` 身份。
- 不要因为 package 改名就批量重命名内部 workflow contract；只有任务明确要求时才改。

## 精简的单 package 工作树

**使用时的感知**

- 这个 fork 的主工作区只维护 `packages/cli`。
- 本地不再需要 `docs-site` 和 `marketplace` submodule 才能进行日常开发、测试和发布
  准备。
- `.trellis/config.yaml` 的 package map 聚焦当前实际维护的 CLI package。

**维护边界**

- `docs-site` 和 `marketplace` 不作为本 fork 的本地 source package。
- release 脚本不应依赖本地 docs-site changelog preflight。

**同步 upstream 时**

- 如果 upstream 恢复或修改 `docs-site` / `marketplace` submodule、`.gitmodules`、
  docs-site release 检查，默认视为冲突点。
- 除非明确决定重新引入这些仓库边界，否则保留本 fork 的单 package 工作树。

## Codex 优先的本地 Trellis 工作区

**使用时的感知**

- 在这个仓库里使用 Codex 时，可以直接读取项目级 `AGENTS.md`、`.agents/skills/` 和
  `.codex/agents/`。
- 本地有适配 Codex 的 `implement`、`check`、`research` 等 subagent 配置。
- session-start、hooks、subagent context 注入围绕这个 fork 的 Trellis 工作流服务。

**维护边界**

- `.agents/skills/`、`.codex/agents/`、`.codex/hooks/` 和对应模板/配置共同组成这项
  能力。
- 本地生成文件和 `packages/cli/src/templates/` 之间要保持同步；只改本地文件会导致
  后续 init/update 漂移。

**同步 upstream 时**

- upstream 对 Codex、shared skills、subagent 或 hooks 的更新要合并，但不能覆盖本
  fork 的中文协作规则、`AGENTS.md` fork-local 规则和 `sayoriqwq` workspace 语境。
- 如果模板和本地生成文件同时冲突，优先让“未来用户运行 `trellis-sq init/update` 后
  也得到同等能力”这个目标成立。

## 上游稳定性更新：hooks、subagent 与多平台兼容

**使用时的感知**

- Codex 项目配置默认启用 `multi_agent_v2`，并把 subagent wait 最小等待时间设为 8
  分钟，减少父线程过早判断 subagent 卡住的问题。
- 可以用 `TRELLIS_HOOKS=0` 或 `TRELLIS_DISABLE_HOOKS=1` 临时关闭 Trellis hooks。
- session-start、workflow-state、subagent context 注入在 Codex、Claude、Cursor、
  OpenCode、Gemini、Qoder、Kiro、CodeBuddy、Droid、Pi 等平台上更稳。
- Windows / Git Bash / Cygwin / WSL 路径、Python <= 3.11、Codex Linux sandbox、
  Gemini CLI 0.40.x、OpenCode plugin 版本等场景吸收了上游修复。

**维护边界**

- 这项能力由 `.codex/config.toml`、平台 hooks、`.agents/skills/trellis-*`、平台
  agent 定义、`packages/cli/src/templates/**`、migration manifests 和对应测试共同
  维护。
- 本 fork 在吸收上游稳定性修复时，仍保留 `.trellis/user/` 同步判断和中文
  human-facing docs policy。

**同步 upstream 时**

- hooks、subagent、platform template、migration、version compare 相关修复默认优先
  吸收。
- 如果 upstream 删除或改写本 fork 的 `.trellis/user/` 维护提示，需要在本地和模板中
  重新补回。

## 可复用 upstream sync workflow

**使用时的感知**

- 以后要求“看看上游新增了什么”“merge upstream”“解决 upstream 冲突”时，agent 会使用
  `.agents/skills/upstream-sync/SKILL.md` 里的固定流程。
- 同步前会先查看上游 commit / manifest / diff；同步中会按 fork 决策解决冲突；同步后
  会更新 `change.md`、必要时更新 `features.md`，并运行验证。

**维护边界**

- `upstream-sync` skill 的核心流程在 `.agents/skills/upstream-sync/SKILL.md`。
- 长期冲突决策放在
  `.agents/skills/upstream-sync/references/fork-decisions.md`，避免每次重新推断。
- `AGENTS.md` 负责让未来 agent 知道何时必须使用这个 skill。

**同步 upstream 时**

- 如果本 fork 的冲突决策变化，先更新 `references/fork-decisions.md`，再同步
  `AGENTS.md` 和本节。
- 不要让 upstream merge 重新引入上游 dogfood workspace、task backlog、
  `@mindfoldhq/trellis` package 身份或 docs-site/marketplace submodule，除非用户明确
  改变 fork 策略。

## 面向人的 `.trellis/user/` 项目上下文

**使用时的感知**

- `.trellis/user/` 用中文解释这个 fork 是什么、核心 package 在哪、阅读顺序是什么。
- 新 agent 或未来的自己可以先读 `.trellis/user/index.md` 和 `features.md`，再进入
  `.trellis/spec/` 的执行规则。
- 工作流收尾时，agent 不只判断 `.trellis/spec/` 是否要同步，也判断 `.trellis/user/`
  是否要更新。

**维护边界**

- `.trellis/user/` 写给人理解，`.trellis/spec/` 写给 agent 执行。
- CLI 模板要能生成 `.trellis/user/index.md`；这些 docs 是 user-owned context，不作为
  普通模板文件自动覆盖。
- `check`、`finish-work`、`update-spec`、session-start、subagent、Trellis meta skill
  都应保留 user docs 同步提醒。

**同步 upstream 时**

- 如果 upstream 修改 workflow、skills、session-start 或模板收尾规则，要检查是否仍
  保留 `.trellis/user/` 同步判断。
- 如果 upstream 没有 `.trellis/user/` 概念，冲突时不要删除本 fork 的 user docs
  workflow；除非明确决定退回纯 spec 模式。

## Fork 知识账本：`change.md` + `features.md`

**使用时的感知**

- `change.md` 让你知道 fork 历史上每次为什么改。
- `features.md` 让你知道当前应该保留哪些用户能力。
- 后续 agent 在非平凡改动后会补 `change.md`，在用户能力变化时会同步修订
  `features.md`。

**维护边界**

- `change.md` append-only，不改写旧记录；需要纠正时追加 backfill/correction entry。
- `features.md` 不是 append-only，应保持当前能力清单准确、去重、可执行。
- `AGENTS.md` 管理后续 agent 对这两个文件的维护规则。

**同步 upstream 时**

- upstream sync 完成后，先补 `change.md` 记录 upstream ref 和冲突决策。
- 再检查本文件每个 feature 是否仍成立；若能力被 upstream 合并、替代、拆分或删除，
  更新本文件的当前描述。

## 中文学习与长期理解材料

**使用时的感知**

- 本 fork 可以保存面向 `sayoriqwq` 的中文学习材料，例如 Trellis 核心模块学习文档。
- 这些内容帮助理解工作流、模块边界和代码结构，不要求写成上游 release note 风格。

**维护边界**

- 学习材料属于 human-facing docs，使用简体中文。
- 如果学习材料沉淀出可执行规则，再提炼到 `.trellis/spec/`；不要把笔记原样塞进
  spec。

**同步 upstream 时**

- upstream 不一定有对应中文学习材料；同步时默认保留本 fork 的学习任务和学习笔记。
- 如果 upstream 改了被学习材料引用的核心模块，更新学习材料中的事实描述。
