# 项目上下文总览

## 这个目录的作用

`.trellis/user/` 和 `.trellis/spec/` 的职责一致：保存这个项目的真实上下文、约定和边界。

区别在于读者不同：

| 目录 | 主要读者 | 写法 |
| --- | --- | --- |
| `.trellis/spec/` | agent | 更像执行规范，强调必须遵守的规则、检查项、禁止模式 |
| `.trellis/user/` | user | 更像项目说明书，强调背景、结构、为什么这样做、怎么理解代码库 |

这里的文档使用简体中文，技术术语保留 English。它们不是替代 spec，而是帮助人先建立项目地图，再决定要读哪些 spec 或代码。

## 项目一眼看懂

这个 repository 是 Trellis 自身的工作区。它同时包含三个 package：

| Package | 路径 | 角色 |
| --- | --- | --- |
| `trellis` | `packages/cli` | Trellis CLI，本项目的核心 npm package |
| `docs-site` | `docs-site` | Mintlify 文档站 submodule |
| `marketplace` | `marketplace` | Trellis resource marketplace submodule |

三者的关系可以这样理解：

- `packages/cli` 负责把 Trellis 安装到用户项目里，包括 workflow、skills、agents、hooks、templates、migrations。
- `docs-site` 负责对外解释 Trellis 怎么用、怎么工作、怎么贡献。
- `marketplace` 负责存放可下载的 spec templates 和 skills，供 Trellis CLI 或用户安装使用。

## 先读什么

如果你是第一次看这个项目，建议按这个顺序：

1. 读本文件，先知道项目分成哪几块。
2. 读 [Trellis CLI 项目说明](./trellis.md)，理解核心代码在哪里。
3. 如果要改文档站，读 [Docs-Site 项目说明](./docs-site.md)。
4. 如果要改 marketplace 资源，读 [Marketplace 项目说明](./marketplace.md)。
5. 真正开始改代码或文档前，再去读对应的 `.trellis/spec/<package>/...`。

## 当前工作区的特殊状态

`docs-site` 和 `marketplace` 是 git submodule。当前 task 探索时发现，主仓库记录的 submodule gitlink commit 无法从远端直接获取，所以本轮 user/spec 文档中的这两部分是基于各自 remote `origin/main` 的可用内容总结出来的。

这意味着：

- 这些说明足够描述仓库职责和常规改动方式。
- 如果你要实际编辑 `docs-site` 或 `marketplace` 内容，先确认 submodule 能 checkout 到你要改的 revision。
- 不要把这两个目录当作普通子目录；它们是独立 repository。

## 和 `.trellis/spec/` 的配合方式

`.trellis/user/` 解决“我现在在哪、这个项目怎么组织”的问题。

`.trellis/spec/` 解决“我要动某个地方时，必须遵守什么规则”的问题。

例如：

- 你想知道 Trellis CLI 是什么，先读 `user/trellis.md`。
- 你要改 `packages/cli/src/commands/init.ts`，再读 `spec/trellis/backend/index.md` 和相关 backend specs。
- 你要改 Mintlify navigation，先读 `user/docs-site.md`，再读 `spec/docs-site/frontend/*` 和 `spec/docs-site/backend/*`。
- 你要加一个 marketplace skill，先读 `user/marketplace.md`，再读 `spec/marketplace/*`。

## 写作约定

- 用简体中文解释上下文。
- 保留 English 技术术语，例如 CLI、TypeScript、submodule、Mintlify、MDX、template、manifest。
- 优先解释项目真实现状，不写愿景式描述。
- 面向 user 的文档可以更连贯、更具叙述性；面向 agent 的 spec 保持规则化。
