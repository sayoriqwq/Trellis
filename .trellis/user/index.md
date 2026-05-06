# 项目上下文总览

## 这个仓库是什么

这个 repository 是 `sayoriqwq` fork 原
`mindfold-ai/Trellis` 项目后用于个人自定义和改造 Trellis 的工作区。

它的目标是服务个人使用：保留 Trellis 原有的 AI workflow、spec、task、
workspace memory、platform adapter 和 skills 思路，同时根据 `sayoriqwq`
自己的使用习惯调整 CLI、模板和本地规则。

## 项目边界

当前仓库只把 `packages/cli` 作为核心 source package：

| Package | 路径 | 角色 |
| --- | --- | --- |
| `trellis` | `packages/cli` | fork 后的 Trellis SQ CLI 源码，发布/链接后提供 `trellis-sq` 命令 |

原上游仓库里的 `docs-site` 和 `marketplace` git submodule 已经从本 fork
移除。本仓库不再把文档站或 marketplace 资源仓库作为本地 package 维护。

## 先读什么

如果你是第一次看这个 fork，建议按这个顺序：

1. 读本文件，先确认这是个人 fork，不是上游主仓库。
2. 读 [Trellis CLI 项目说明](./trellis.md)，理解核心代码在哪里。
3. 看根目录 [`change.md`](../../change.md)，了解本 fork 相对上游的长期差异。
4. 真正开始改代码或模板前，再读 `.trellis/spec/trellis/...` 中对应 specs。

## 命令命名

这个 fork 的 CLI binary 是 `trellis-sq`：

```bash
trellis-sq init -u sayoriqwq
trellis-sq update
trellis-sq uninstall
```

内部 workflow、skill、agent 和平台 command 仍然沿用 Trellis 语义，例如
`trellis-before-dev`、`trellis-check`、`/trellis:finish-work`。这些名字属于
工作流内部 contract，不要因为 CLI binary 变成 `trellis-sq` 就自动批量重命名。

## 和 `.trellis/spec/` 的配合方式

`.trellis/user/` 解决“这个 fork 是什么、现在在哪、为什么这样组织”的问题。

`.trellis/spec/` 解决“改某个地方时必须遵守什么规则”的问题。

例如：

- 你想知道 Trellis SQ CLI 是什么，先读 `user/trellis.md`。
- 你要改 `packages/cli/src/commands/init.ts`，再读
  `spec/trellis/backend/index.md` 和相关 backend specs。
- 你要改 generated skills 或 platform templates，读对应 template 旁边的实现，
  并检查 `.trellis/spec/trellis/frontend/*` 和 backend template 规则。

## 什么时候维护这个目录

Trellis workflow 的收尾阶段会要求同时判断两类知识是否需要更新：

- `.trellis/spec/`：当改动产生新的 executable coding contract、约定、测试要求或防错规则时更新。
- `.trellis/user/`：当改动改变项目地图、package 角色、阅读顺序、架构理解、常见坑或 onboarding 语境时更新。

两者不要机械互相复制。spec 写给 agent 执行，user docs 写给人理解；同一件事经常需要在两个目录里用不同写法记录。

## 写作约定

- 用简体中文解释上下文。
- 保留 English 技术术语，例如 CLI、TypeScript、submodule、template、manifest。
- 优先解释项目真实现状，不写愿景式描述。
- 面向 user 的文档可以更连贯、更具叙述性；面向 agent 的 spec 保持规则化。
