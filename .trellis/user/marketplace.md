# Marketplace 项目说明

## 它是什么

`marketplace` 是 Trellis 的资源市场 repository，以 git submodule 的形式挂在主仓库下。它不是运行时服务，而是一个 static registry，用来存放可下载的 Trellis resources。

主要资源包括：

- spec templates，用于快速生成 `.trellis/spec/`。
- skills，用于扩展 agent 或用户 workflow。
- 未来也可能包含 commands、agents 或 full project templates。

## 核心文件和目录

| 路径 | 作用 |
| --- | --- |
| `index.json` | marketplace registry，列出可下载资源 |
| `README.md` | marketplace 使用说明 |
| `skills/<id>/SKILL.md` | skill 入口文件 |
| `skills/<id>/references/` | skill 的补充参考资料 |
| `specs/<id>/README.md` | spec template 说明 |
| `specs/<id>/backend/` | backend specs |
| `specs/<id>/frontend/` | frontend specs |
| `specs/<id>/shared/` | backend/frontend 共享规则 |
| `specs/<id>/guides/` | thinking guides 或 cross-layer guides |

## `index.json` 是什么

可以把 `index.json` 理解成 marketplace 的数据库。Trellis CLI 的 remote template fetch 逻辑会读取它，找到某个 template 的 `id`、`type`、`path` 和 metadata。

一个 registry entry 通常包含：

```json
{
  "id": "nextjs-fullstack",
  "type": "spec",
  "name": "Next.js + oRPC + PostgreSQL",
  "description": "Full-stack Next.js application with oRPC API layer, Drizzle ORM, and PostgreSQL",
  "path": "specs/nextjs-fullstack",
  "tags": ["nextjs", "react", "typescript", "orpc"]
}
```

如果移动、重命名或新增资源，`index.json` 必须同步更新。

## skill 怎么理解

一个 skill 是一个可被 agent 使用的能力包。`SKILL.md` 是入口，通常包含 YAML frontmatter：

```markdown
---
name: trellis-meta
description: "..."
---
```

好的 skill 应该说明：

- 什么时候使用。
- 前置条件是什么。
- 执行步骤是什么。
- 需要读哪些 references。
- 结果怎么验证。

例如 `frontend-fullchain-optimization` 是一个面向 frontend performance 的 skill，它描述 Web Vitals、diagnostic decision tree、manual measurement 和 delivery template。

## spec template 怎么理解

spec template 是给用户项目初始化 `.trellis/spec/` 的起点。它不是某个具体项目的最终规范，而是一套针对技术栈的高质量默认规则。

例如：

- `nextjs-fullstack` 面向 Next.js、oRPC、PostgreSQL、Drizzle。
- `electron-fullstack` 面向 Electron、React、SQLite。
- `cf-workers-fullstack` 面向 Cloudflare Workers、Hono、Turso。

每个 template 都应该包含清晰的 index，告诉 agent 或 user 哪些文件必须读，哪些是 reference。

## 改动时最容易踩的点

- 新增目录但忘记在 `index.json` 注册。
- 改了 spec 文件名但忘记更新对应 `index.md`。
- skill 的 `SKILL.md` frontmatter 写错，导致 agent 无法正确识别。
- references 文件移动后，`SKILL.md` 里的链接失效。
- spec template 里留下 placeholder 或泛泛而谈的 best practices。

## 如果你要开始改 marketplace

先确认 submodule 已经 checkout 到正确 revision。然后：

1. 判断你改的是 registry、skill，还是 spec template。
2. 如果改 registry，先看 `index.json`。
3. 如果改 skill，先看对应 `SKILL.md` 和 `references/`。
4. 如果改 spec template，先看该 template 的 `README.md` 和各层 `index.md`。
5. 再读 `.trellis/spec/marketplace/` 中对应 specs，确认质量和结构要求。

Marketplace 的原则是：内容要能被下载、能被 agent 执行、能被 user 理解。只写漂亮描述不够，路径、frontmatter、index 和示例都要对得上。
