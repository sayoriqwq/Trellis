# Trellis SQ

这是 `sayoriqwq` fork 原
[mindfold-ai/Trellis](https://github.com/mindfold-ai/Trellis) 项目的仓库。

这个 fork 的定位不是重新维护一个公共文档站或 marketplace，而是用于个人使用：
自定义、改造和验证 Trellis 工作流，让它更贴合 `sayoriqwq` 自己的 AI
开发习惯。它保留 Trellis 的 workflow、templates、agents、skills、task
system 和 workspace memory，但默认 CLI 命令改为 `trellis-sq`。

## 范围

- 个人 fork，用于本地 workflow、自定义技能、平台模板和 CLI 行为改造。
- 主要源码 package：`packages/cli`。
- 生成和维护的 workflow surface：`.trellis/`、`.agents/`、`.codex/`、
  `.claude/`、`.cursor/`、`.opencode/`、`.pi/` 以及相关模板。
- 原来的 `docs-site` 和 `marketplace` git submodule 已从本 fork 工作区移除。

## 命令

这个 fork 暴露的新 CLI 命令是：

```bash
trellis-sq init -u your-name
trellis-sq update
trellis-sq uninstall
```

内部 Trellis workflow 的命名暂时保持 Trellis 语义，例如
`trellis-before-dev`、`trellis-check`、`/trellis:finish-work`。这些名字属于
生成文件和平台入口的 workflow contract，不等同于 npm/CLI binary 名。

## 开发

```bash
pnpm install
pnpm build
pnpm lint
pnpm typecheck
pnpm test
```

常用 package-scoped 命令：

```bash
pnpm --filter trellis-sq build
pnpm --filter trellis-sq lint
pnpm --filter trellis-sq typecheck
pnpm --filter trellis-sq test
```

## 让其他项目用到这个 fork 的最新修改

每次在这个 fork 里合并上游或修改 CLI 后，先在本仓库刷新本机全局链接的
`trellis-sq`：

```bash
pnpm --filter trellis-sq build
pnpm --dir packages/cli link --global
trellis-sq --version
```

当前 pnpm 版本下，`pnpm --filter trellis-sq link --global` 可能会因为
`Unknown option: 'recursive'` 失败；使用上面的 `--dir packages/cli` 写法。

已经使用 `trellis-sq` 的其他项目不会自动拿到新的 `.trellis/`、`.agents/`、
`.codex/`、`.claude/` 或平台模板文件。需要进入每个目标项目执行：

```bash
trellis-sq update
```

如果目标项目非常旧，早于 0.5 migration chain，则执行：

```bash
trellis-sq update --migrate
```

新项目先初始化：

```bash
trellis-sq init -u your-name
```

## Fork 说明

- 上游项目：<https://github.com/mindfold-ai/Trellis>
- 当前 fork：<https://github.com/sayoriqwq/Trellis>
- 本地改造记录：[`change.md`](./change.md)

后续从上游同步时，把 `change.md` 当成 fork-local ledger。新增个人改造只往里
append，不重写旧记录，这样 rebase 或 merge 以后更容易看清哪些是本 fork 的长期差异。
