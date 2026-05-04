# 项目上下文文档

## 这个目录的作用

`.trellis/user/` 和 `.trellis/spec/` 都用于保存这个项目的真实上下文、约定和边界。

区别在于读者不同：

| 目录 | 主要读者 | 写法 |
| --- | --- | --- |
| `.trellis/spec/` | agent | 更像执行规范，强调必须遵守的规则、检查项、禁止模式 |
| `.trellis/user/` | user | 更像项目说明书，强调背景、结构、为什么这样做、怎么理解代码库 |

这里的文档默认使用简体中文，技术术语保留 English。它们不是替代 spec，而是帮助人先建立项目地图，再决定要读哪些 spec 或代码。

## Bootstrap 时应该补充什么

第一次填充 `.trellis/spec/` 时，请同步补充 `.trellis/user/`：

- 用简体中文写面向 user 的项目上下文说明。
- 技术术语保留 English，例如 CLI、backend、frontend、submodule、template、manifest。
- 解释 package/目录职责、常见改动入口、容易踩的坑。
- 不要写成 agent checklist；把 `.trellis/spec/` 中的规则转化成更可读的说明。

## 建议结构

单仓库项目可以从这些文件开始：

```text
.trellis/user/
├── index.md      # 项目总览和阅读顺序
├── backend.md    # 后端上下文（如果适用）
└── frontend.md   # 前端上下文（如果适用）
```

Monorepo 项目可以按 package 拆分：

```text
.trellis/user/
├── index.md
├── <package-a>.md
└── <package-b>.md
```

## 和 spec 的关系

- `.trellis/user/` 解决“我现在在哪、这个项目怎么组织”的问题。
- `.trellis/spec/` 解决“我要动某个地方时，必须遵守什么规则”的问题。
- 两者应该同步维护：如果 spec 里新增了重要项目约定，user 文档也应该用人能读懂的方式解释它。
