# Trellis CLI 项目说明

## 它是什么

`packages/cli` 是 `@mindfoldhq/trellis` 的核心 package。它是一个 Node.js CLI，用 TypeScript 编写，发布后提供 `trellis` 和 `tl` 两个命令。

这个 CLI 的职责不是运行一个 server，也不是渲染 UI，而是把 Trellis 工作流安装、更新、卸载到用户项目里。它管理的内容包括：

- `.trellis/` workflow、tasks、spec、workspace、scripts。
- `.trellis/user/` 中面向 human 的项目地图、阅读顺序和架构说明。
- 各 AI platform 的配置目录，例如 `.claude/`、`.codex/`、`.cursor/`、`.agents/skills/`。
- templates、hooks、commands、skills、agents 的生成逻辑。
- update/uninstall 时的 migration、hash manifest 和用户改动保护。

## 核心目录怎么理解

`packages/cli/src` 是主要源码：

| 路径 | 作用 |
| --- | --- |
| `cli/` | Commander 入口，注册 `init`、`update`、`uninstall` |
| `commands/` | 用户命令的实际实现 |
| `configurators/` | 各 AI platform 的安装和配置逻辑 |
| `templates/` | 安装到用户项目中的文件模板 |
| `migrations/` | update 时使用的版本迁移和 manifest |
| `constants/` | 路径、版本等共享常量 |
| `utils/` | 文件写入、项目检测、template fetch、hash 等工具 |
| `types/` | 共享 TypeScript 类型 |

测试放在 `packages/cli/test`，通常按 `commands/`、`utils/`、`templates/` 等维度组织。

## 最重要的项目边界

`packages/cli` 是 CLI package，不是 frontend app。

它的 frontend-adjacent 内容主要是“会被复制到用户项目中的模板”，例如 Markdown、TOML、JSON、Python hooks、skill 文档。不要因为看到 `jsx: "react-jsx"` 就把它理解成 React 项目。

它也不是 backend service。这里没有 HTTP API、ORM、database migration。所谓 backend 规则，主要指 CLI runtime、filesystem persistence、template generation、migration 和 error handling。

## 改动时最容易踩的点

第一类是只改了本地生成文件，忘了改 template。

Trellis 自己也使用 `.trellis/`、`.codex/`、`.agents/` 等目录，但这些本地文件不是用户安装时的唯一来源。如果你希望未来用户运行 `trellis init` 或 `trellis update` 后得到同样变化，就要检查 `packages/cli/src/templates/` 和对应 `configurators/`。

第二类是随手写路径 literal。

`.trellis`、`tasks`、`workspace`、`.current-task` 这类路径应优先从 `packages/cli/src/constants/paths.ts` 获取。路径散落会让 update、uninstall、tests、templates 很容易漂移。

第三类是破坏非交互环境。

CLI 会在 CI、pipe、agent 环境中运行。像 `file-writer.ts` 这样的底层工具已经处理了 non-TTY fallback。新增 prompt 时要确认不会在 non-TTY 下卡住或崩溃。

第四类是只更新 agent-facing spec，忘了同步 human-facing user docs。

现在 Trellis workflow 把 Phase 3.3 定义为 knowledge docs update：实现结束后要同时判断 `.trellis/spec/` 和 `.trellis/user/` 是否需要更新。前者记录可执行的 coding contract，后者解释项目地图、package 职责、阅读顺序、架构背景和常见坑。涉及 workflow、template、hook、platform adapter、package map 的改动尤其容易同时影响两者。

## 质量基线

这个 package 使用 strict TypeScript 和 ESLint：

- exported function 要有明确 return type。
- 不使用 `any`。
- 不使用 non-null assertion。
- TypeScript import 需要符合 NodeNext，源码里的相对 import 使用 `.js` extension。
- 格式化使用 Prettier，双引号、分号、2 spaces、trailing comma。

常用检查：

```bash
pnpm --filter @mindfoldhq/trellis lint
pnpm --filter @mindfoldhq/trellis typecheck
pnpm --filter @mindfoldhq/trellis test
```

## 如果你要开始改 Trellis CLI

先判断改动属于哪一类：

- 改 CLI command 行为：看 `src/cli/index.ts`、对应 `src/commands/*.ts` 和 `test/commands/*`。
- 改 platform 支持：看 `src/configurators/<platform>.ts`、`src/templates/<platform>/` 和相关 integration tests。
- 改 `.trellis/` 生成内容：看 `src/templates/trellis/`，并确认 update migration 是否需要同步。
- 改文件写入或 update/uninstall 行为：看 `file-writer.ts`、`template-hash.ts`、`update.ts`、`uninstall.ts`。

然后再读 `.trellis/spec/trellis/backend/` 或 `.trellis/spec/trellis/frontend/` 中对应的 agent specs。
