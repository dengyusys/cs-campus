# AGENTS.md — 本仓库的 AI 协作规范

本仓库是校园计算机科学学习项目集合，核心内容是 `docs/` 下的 **Java 入门教程（从语法到完整项目）**（Docsify 文档站），另有 Git / Python / Markdown 等延伸教程。任何编码代理在本仓库工作前，请先读完本文件。

## 项目背景（一句话）

面向零基础的 Java 入门教程站：Markdown 为文档源，Docsify + mermaid@10 渲染，教学设计为「快速过语法 → 尽快实践 → 每天费曼输出」，最终项目是控制台学生管理系统。

## 常用命令

```bash
# 起本地文档服务（改完文档必须用它验证；--bind 127.0.0.1 让输出直观且只监听本机）
python -m http.server 3000 --directory docs --bind 127.0.0.1
```

没有构建步骤、没有测试框架——**验证方式是浏览器人工检查**（或用浏览器自动化工具）。统一用 Python 起服务，不推荐 `npx serve` 等 Node 方案。

## 修改文档的规则

### 文件与导航

- 每日文档位于 `docs/java/`，命名格式 `dayXX-主题.md`（两位数字 + 中文主题）
- **新增每日文档后必须同步更新 `docs/java/_sidebar.md`**（Java 分区的子侧边栏），否则侧边栏不可见
- 文档末尾保留三连导航：`[⬅️ 上一天](...) ｜ [🏠 返回首页](/) ｜ [下一天 ➡️](...)`

### 侧边栏：门户式两层结构

- 根侧边栏 `docs/_sidebar.md` 是**门户**：只放首页、各主题入口（Java 两个阶段入口 + 每份延伸教程一行），不放每日明细——保持短小
- 大型主题（如 Java 计划）在**自己的目录**放 `_sidebar.md` 子侧边栏，列出全部明细；进入该主题的页面时 docsify 自动切换，无需 alias 配置（`index.html` 里不要再加全局 alias 强制根侧边栏）
- 新增一个主题目录时：根侧边栏加一行入口；若内容超过 ~10 篇，为该目录建自己的 `_sidebar.md`，并在顶部放「🏠 返回首页」链接
- 子侧边栏内的链接用站点根绝对路径（如 `/java/day01-xxx.md`），避免相对路径歧义

### 站点主题（docsify v5）

- 站点基于 **docsify v5**：主题分层加载 `dist/themes/core.min.css`（基座）→ `dist/themes/addons/vue.min.css`（vue 变体）→ `docs/theme-claude.css`（Claude 风格覆盖层，默认启用）
- 两套主题：**vue**（前两层）与 **Claude**（三层全开）；右上角按钮切换，选择存于 `localStorage` 的 `cs-theme` 键（`claude` / `vue`），`index.html` head 内联脚本在首屏前禁用覆盖层以防止闪烁
- 切换按钮基础样式内联在 `index.html`，Claude 形态写在 `theme-claude.css`
- 侧边栏手柄是 v5 原生造型（全高热区 + 内嵌竖条）；`<body class="sidebar-toggle-hamburger">` 启用汉堡图标变体；Claude 配色通过 `theme-claude.css` 里的 `--sidebar-toggle-*` 变量驱动
- **插件包名注意**：代码复制插件是 `docsify-copy-code`（带连字符，v4 时代误写成 `docsify-copycode` 导致长期 404 未生效）；mermaid 用 mermaid@10 + docsify-mermaid@2（v5 下实测兼容）
- 修改 `theme-claude.css` 只影响 Claude 主题；适配 v5 样式时优先用官方 CSS 变量，其次才是选择器覆盖

### 内容模板（保持一致性）

每日文档固定五段式，emoji 板块标题不要改：

1. 🎯 今日目标（≤3 条）
2. ⚡ 知识点速览（最小必要知识 + mermaid 图）
3. 💻 跟着写（代码任务，占篇幅大头）
4. 🧠 费曼时刻（教学卡片模板，用 ```markdown 代码块承载）
5. ✅ 自测清单（checkbox 列表）

### mermaid 图表约束

- 渲染器是 **mermaid@10**（经 docsify-mermaid@2 加载），可用类型：`flowchart` / `classDiagram` / `mindmap` / `sequenceDiagram`
- 节点文字含 `(` `)` `,` 等特殊字符时必须整体加引号：`A["文字（注意）"]`，否则渲染为 Syntax error
- `mindmap` 节点文字避免圆括号（其语法中括号有含义）
- 改动或新增图表后，必须起服务在浏览器确认渲染为图形而非源码文本

### 教学内容红线

- **禁止提供完整参考答案**：只给骨架代码（带 TODO）、提示（`<details>` 折叠块）和关键片段，这是刻意设计
- 代码示例必须 JDK 21 可直接运行，零外部依赖、零框架；示例遵守计划已教的子集（不用未讲到的语言特性，如流 API、Lambda 之外的进阶特性）
- 术语类比要生活化（图纸/房子、菜谱、储物柜…），风格与既有文档一致
- 全部内容使用简体中文

## 提交规范

### commit message 格式（简化版 Conventional Commits，不带 scope）

```
<type>: <中文描述>
```

- **type**（必填，英文小写）：
  - `docs` —— 文档内容的新增/修改（本仓库最常见）
  - `feat` —— 新的教程模块、新功能
  - `fix` —— 修 bug：断链、渲染错误、示例代码跑不通
  - `refactor` —— 不改行为的结构调整
  - `chore` —— 配置、`.gitignore` 等杂项
- **中文描述**（必填）：用简体中文说清「做了什么」，结尾不加句号

示例：

- `docs: 新增 Git 入门教程（拉取、推送与合并）`
- `fix: 修复侧边栏到 Git 教程的断链`
- `chore: 忽略 IDE 配置文件`

### 提交纪律

- 一个 commit 只做一件事；文档内容与配置改动分开提交
- 改动文档的 commit 前必须完成「典型任务的验证清单」中的浏览器检查
- 不要提交 `.zcode/`、`node_modules/`、IDE 配置、编译产物（已在 `.gitignore`）
- 仓库全部历史已合并为单一的初始提交，此后所有提交遵循本规范

## 典型任务的验证清单

改完任何文档后，在浏览器（http://127.0.0.1:3000）检查：

1. 所在分区的侧边栏能看到新/改的文档且能打开（Java 文档看 `docs/java/_sidebar.md`，其余页面看根侧边栏；改过侧边栏或 `index.html` 后用 Ctrl+F5 强制刷新，避免旧缓存）
2. 页内 mermaid 图渲染为图形，无 Syntax error、无源码泄漏
3. 文内链接（上一天/下一天、跨教程引用）不断链；跨目录引用一律用站点根绝对路径（如 `/java/day01-xxx.md`）

> 注：本站未启用全文搜索插件，验证以侧边栏导航和链接为主。

## 未来可能的扩展方向（做之前和用户确认）

- 新的学习计划（数据库 / 前端等）：在 `docs/<topic>/` 下新建目录，沿用既有风格；根侧边栏加入口，内容多则建子侧边栏（规则见「侧边栏」一节）
- Java 示例代码目录（`code/`）：提供练习骨架工程时，保持与文档 TODO 编号对应
- 部署 GitHub Pages：`docs/` 目录已放 `.nojekyll`，开启 Pages 指向 `docs/` 即可
