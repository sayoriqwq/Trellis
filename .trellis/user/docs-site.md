# Docs-Site 项目说明

## 它是什么

`docs-site` 是 Trellis 的文档站 repository，以 git submodule 的形式挂在主仓库下。它基于 Mintlify，主要内容是 MDX 文档、`docs.json` navigation 配置、静态图片、全局 CSS 和少量 custom JavaScript。

它不是 backend app，也不是本项目自己维护的 React app。Mintlify 负责渲染，仓库负责提供内容和配置。

## 核心文件

| 路径 | 作用 |
| --- | --- |
| `docs.json` | Mintlify 主配置，控制 navigation、languages、versions、redirects、theme、exclude |
| `index.mdx` | 英文 RC 文档入口 |
| `zh/index.mdx` | 中文 RC 文档入口 |
| `release/` | stable Release 文档 |
| `zh/release/` | 中文 stable Release 文档 |
| `advanced/`、`start/`、`guides/` | 主要英文文档章节 |
| `changelog/` | RC changelog |
| `api-reference/openapi.json` | 静态 OpenAPI 数据 |
| `styles.css` | Mintlify 全局样式覆盖 |
| `terminal-demo.js` | terminal demo 的 custom browser script |

## 文档站的心智模型

Mintlify 不会简单地把所有文件自动变成你想要的导航。`docs.json` 是核心 contract。

添加、移动、删除页面时，一般要同时考虑：

- 文件是否存在。
- `docs.json` navigation 是否引用它。
- 旧 URL 是否需要 redirects。
- 英文和中文是否都要更新。
- RC 和 Release 是否都要更新。
- 图片、链接、代码块是否能在 Mintlify 里正常渲染。

## 语言和版本的关系

文档站同时维护 English 和 Chinese，并且有 RC 与 Release 两条版本轨道。

粗略理解：

- 根目录英文页面和 `zh/` 通常表示当前 RC 文档。
- `release/` 和 `zh/release/` 表示 stable release 文档。
- `docs.json` 的 navigation 同时描述 languages 和 versions。

所以，文档改动不能只问“这个文件在哪”，还要问“这个内容属于哪个 language 和哪个 version”。

## 自定义前端行为

当前 docs-site 的 custom frontend 主要是 `styles.css` 和 `terminal-demo.js`。

`styles.css` 有两类重要用途：

- 覆盖 Mintlify 默认 UI，例如隐藏 language switcher 的 flag。
- 支撑 terminal demo 和 CJK diagram 这类特殊展示。

`terminal-demo.js` 使用 plain JavaScript，不使用 React hooks。它通过 `MutationObserver` 等方式等待 Mintlify 渲染内容后初始化页面交互。

## 改动时最容易踩的点

- 新增 MDX 文件但忘记加入 `docs.json`。
- 只改 English，忘记 `zh/`。
- 只改 RC，忘记 Release，或反过来。
- 删除页面但没有处理 redirects。
- 写了 custom CSS，却没有给 feature-specific selector 加前缀，导致污染 Mintlify 全局样式。
- 在 MDX 里写了会被解析成 JSX 的示例代码，却没有放进 fenced code block。

## 如果你要开始改 docs-site

先确认 submodule 已经 checkout 到正确 revision。然后：

1. 读 `docs.json`，确认目标页面属于哪个 navigation group、language、version。
2. 读同目录附近的 MDX，保持写法和语气一致。
3. 如果改了 navigation、links、CSS 或 JS，使用 Mintlify preview 检查。
4. 再读 `.trellis/spec/docs-site/` 中对应 specs，确认具体规则。

常用命令：

```bash
mint dev
mint broken-links
```
