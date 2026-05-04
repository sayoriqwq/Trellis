# brainstorm: Trellis 核心模块中文学习文档

## Goal

生成一份面向 TypeScript/前端背景开发者的中文学习文档，帮助快速上手 Trellis 项目的核心模块。文档从架构、核心逻辑链、关键模块代码分析三个角度展开，并在末尾附上练习题，帮助读者把 CLI、工作流、模板、任务系统等核心概念串起来。

## What I already know

* 目标仓库就是当前 Trellis 仓库。
* 用户希望开启一个新 task，以学习和上手项目核心模块为目标。
* 文档语言为中文。
* 文档需要覆盖三个主视角：架构、核心逻辑链、关键模块代码分析。
* 文档末尾需要附习题。
* 用户 TypeScript 经验较多，偏前端，最近在研究 CLI。
* 用户日常终端是 fish；面向用户的 shell 命令应优先使用 fish 兼容写法，避免 bash/zsh 专属 heredoc 等语法。
* 用户对函数式语言感兴趣，接触过 TypeScript Effect、Haskell、不可变数据、纯函数、ADT/判别联合、模式匹配等思想，但对 monad、stream/lazy 实践较少。
* Trellis 顶层 README 将产品模型概括为 `.trellis/spec/`、`.trellis/tasks/`、`.trellis/workspace/`、`.trellis/workflow.md` 和平台 adapters 五层。
* 代码主包是 `packages/cli`，`package.json` 暴露 `trellis` / `tl` 两个 bin，运行时依赖集中在 `commander`、`inquirer`、`chalk`、`giget`、`undici`。
* TypeScript 侧核心职责是安装、更新、卸载 Trellis 管理的文件；Python 脚本和 hooks 是安装到用户项目后的运行期。
* CLI 入口 `packages/cli/src/cli/index.ts` 用 commander 注册 `init`、`update`、`uninstall`，并在 `.trellis/` 存在时做版本检查。
* `init` 链路负责 Python 版本检查、项目/monorepo 检测、远程 spec template 下载、`.trellis/` 结构创建、平台 configurator 执行、hash 初始化、bootstrap/joiner task 创建。
* `update` 链路负责从模板收集当前版本文件、通过 `.trellis/.template-hashes.json` 区分用户改动和模板升级、保护用户数据目录、执行迁移和安全删除。
* `configurators/index.ts` 和 `types/ai-tools.ts` 共同构成多平台 registry：新增平台需要更新平台数据、配置器、模板、CLI flag 和测试。
* `templates/trellis/` 是用户项目 `.trellis/` 的模板源，包含 workflow、config、gitignore 和 Python scripts；`templates/common/` 是跨平台 commands/skills 的单一来源。
* `shared-hooks/session-start.py` 负责 session 启动上下文注入；`inject-subagent-context.py` 负责 sub-agent 启动前按 task jsonl 注入 PRD/spec/research 上下文。
* `templates/trellis/scripts/task.py` 是用户项目内 task 操作入口，实际命令逻辑拆在 `common/task_store.py`、`common/task_context.py`、`common/active_task.py` 等模块。

## Assumptions (temporary)

* 该任务的交付物可以先放在本 task 目录下，作为学习材料草稿，而不是直接进入产品文档站。
* 文档应该偏“代码导览 + mental model”，而不是完整 API 参考。
* 习题应该包含阅读题、代码追踪题和小改动练习，难度从入门到进阶递增。

## Open Questions

* 是否需要把 task 内学习文档后续提升到正式 docs-site。MVP 先不做。

## Requirements (evolving)

* 输出一份中文学习文档。
* 文档覆盖 Trellis 架构、核心逻辑链、关键模块代码分析。
* 文档需要根据用户背景调整解释方式：TS/前端友好、CLI 入门友好、适当类比函数式思想。
* 文档内给出的 shell 命令应使用 fish 兼容写法。
* 文档末尾附习题。
* 文档先落在 task 目录下，作为个人学习材料草稿。
* 文档需要明确区分 TypeScript CLI 安装/更新链路与 Python/hook 运行期链路。
* 文档需要包含建议阅读顺序。

## Acceptance Criteria (evolving)

* [x] 文档能让读者理解 Trellis CLI 的整体模块分层。
* [x] 文档能追踪至少一条核心命令链路，从 CLI 入口到文件系统/template 变更。
* [x] 文档能点名并解释关键源码文件和模块职责。
* [x] 文档包含适合用户背景的函数式/类型系统视角提示。
* [x] 文档包含习题，覆盖概念理解、代码阅读和小型实践。
* [x] 文档中的命令示例不依赖 bash/zsh 专属 heredoc。

## Definition of Done (team quality bar)

* Tests added/updated if behavior changes.
* Lint / typecheck / CI green if code changes.
* Docs/notes updated if behavior changes.
* Rollout/rollback considered if risky.

## Out of Scope (explicit)

* 不修改 Trellis CLI 行为。
* 不引入新依赖。
* 不重构核心模块。
* 不把学习文档发布到 docs-site，除非后续明确选择该范围。
* 不把本文档当成完整 API reference 或逐行源码注释。

## Technical Notes

* 交付物：`.trellis/tasks/05-04-trellis-core-learning-doc/learning.md`。
* 核心入口：`packages/cli/src/cli/index.ts`。
* 核心命令：`packages/cli/src/commands/init.ts`、`packages/cli/src/commands/update.ts`、`packages/cli/src/commands/uninstall.ts`。
* 多平台抽象：`packages/cli/src/types/ai-tools.ts`、`packages/cli/src/configurators/index.ts`、`packages/cli/src/configurators/shared.ts`。
* `.trellis/` 结构创建：`packages/cli/src/configurators/workflow.ts`、`packages/cli/src/templates/trellis/index.ts`、`packages/cli/src/templates/extract.ts`。
* 运行期 hooks：`packages/cli/src/templates/shared-hooks/session-start.py`、`packages/cli/src/templates/shared-hooks/inject-subagent-context.py`。
* 用户项目 task runtime：`packages/cli/src/templates/trellis/scripts/task.py`、`packages/cli/src/templates/trellis/scripts/common/task_store.py`、`packages/cli/src/templates/trellis/scripts/common/task_context.py`、`packages/cli/src/templates/trellis/scripts/common/active_task.py`、`packages/cli/src/templates/trellis/scripts/common/session_context.py`。
* 更新/迁移支撑：`packages/cli/src/utils/template-hash.ts`、`packages/cli/src/migrations/index.ts`。
* 质量入口：`pnpm --filter @mindfoldhq/trellis test`、`lint`、`typecheck`，测试分布在 `packages/cli/test/{commands,configurators,templates,utils,...}`。
