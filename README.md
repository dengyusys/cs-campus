# cs-campus

校园计算机科学学习项目集合。当前包含：**Java 入门教程**、**Python / Markdown / Git / MySQL / Linux / Redis / HTTP / MyBatis** 八份入门教程，以及一份**用 ZCode（AI 编程代理）创建学习教程的方法手册**。

## 📚 Java 入门：从语法到完整项目

一套面向**零基础学习者**的 Java 入门计划，核心理念：

- **快速过语法，尽早实践** —— 每天只讲最小必要知识，60% 时间在写代码
- **费曼学习法** —— 每天用大白话输出一张「教学卡片」，讲不清的地方就是没懂的地方
- **图文并茂** —— 全程配套 mermaid 流程图、类图、思维导图
- **以项目收尾** —— 6 天时间从零做出「控制台学生管理系统」（增删改查 / 文件持久化 / 输入校验）

## 🔧 延伸教程

- **[Git 入门：拉取、推送与合并](docs/git/README.md)**（约 1.5 小时）—— 版本控制工具：四个区域模型、`push` / `pull` / `merge` 三件套、冲突解决五步法，含本地模拟两人协作的练习。建议在 Java 计划 Day 9 前后完成
- **[Python 入门：快速上手与实践](docs/python/README.md)**（约 2 小时）—— 另一门主流语言的最小集入门：变量、流程控制、数据结构四件套、函数、文件读写；练习题复刻 Java 计划经典题目，同题异构对比两门语言
- **[Markdown 入门：写作即排版](docs/markdown/README.md)**（约 1 小时）—— 程序员的通用写作格式：标题、列表、表格、代码块、mermaid 图表与折叠块；练习包括把费曼卡片排版成 Markdown、写自我介绍 README

### 🗄️ 进阶：MySQL

**[MySQL 入门：从 SQL 到 JDBC](docs/mysql/README.md)**（约 2.5 小时）—— Java 进阶路线第一站：SQL 建表与增删改查、`WHERE`/`ORDER BY`/`LIKE`/`AVG`、`JOIN` 多表关联、JDBC 五步走，并动手把学生管理系统从文件持久化迁移到数据库。

### 💻 Linux 入门

**[Linux 入门：与命令行做朋友](docs/linux/README.md)**（约 2 小时）—— 服务器世界的语言：导航、文件、搜索、权限、进程等高频命令，在 WSL 里亲手做一遍「命令行冒险」练习。

### ⚡ Redis 入门

**[Redis 入门：把数据放进内存](docs/redis/README.md)**（约 2 小时）—— 内存数据库的定位（对比 MySQL）、五种数据结构、缓存旁路 Cache-Aside、过期时间；综合练习给学生管理系统加缓存。

### 🌐 HTTP / REST 入门

**[HTTP / REST 入门](docs/http/README.md)**（约 2 小时）—— Web 世界的语言：请求方法、状态码含义、RESTful 资源接口设计、JSON 数据传输，为把学生管理系统升级成 Web 应用打基础。

### 📝 MyBatis 入门

**[MyBatis 入门](docs/mybatis/README.md)**（约 2 小时）—— Java 持久层框架：Mapper 接口 + XML 分离 SQL、`#{}` 参数占位防注入、自动映射与动态 SQL，把 MySQL 教程的 JDBC 代码升级成 MyBatis。

### 🤖 元技能：用 ZCode 创建教程

**[用 ZCode 创建入门教程：从想法到上线](docs/zcode/README.md)**（约 40 分钟）—— 复盘本站的真实创建过程，提炼「让 AI 为你定制学习教程」的完整流程：需求一句话模板、三个关键决策、审计划要点、验收清单、迭代提示词，以及用 AGENTS.md 沉淀长期约定。

## 🚀 快速开始

### 环境要求

| 工具 | 用途 | 说明 |
|---|---|---|
| Git | 克隆仓库 | [下载](https://git-scm.com/downloads) |
| Python 3 | 起本地文档服务 | [下载](https://www.python.org/downloads/) |
| 浏览器 | 阅读文档 | Chrome / Edge 均可 |

> 学习 Java 本身需要 JDK 21 + IntelliJ IDEA，详见 [Day 0 · 环境搭建](docs/java/day00-环境搭建.md)。

### 三步开始阅读

```bash
# 1. 克隆仓库
git clone <仓库地址>
cd cs-campus

# 2. 起本地文档服务（推荐用 Python；也可用 VS Code 的 Live Server 插件）
python -m http.server 3000 --directory docs --bind 127.0.0.1

# 3. 浏览器打开
# http://127.0.0.1:3000
```

打开后左侧是完整的天数导航。从 [Day 0 · 环境搭建](docs/java/day00-环境搭建.md) 开始学习。

## 📖 学习者使用指引

**每天的学习流程（约 1.5~2 小时）：**

1. 打开当天文档，先看 🎯 今日目标，明确今天要会什么
2. 快速过 ⚡ 知识点速览（控制在 20~30 分钟，不纠缠细节）
3. 大部分时间留给 💻 跟着写——在 IDEA 里亲手敲每一个练习
4. 完成 🧠 费曼时刻：把当天的知识用自己的话写成教学卡片（文档里附卡片模板）
5. 过一遍 ✅ 自测清单，全部能答上来才进入下一天

**几条建议：**

- 阶段一（Day 0–8）的练习不是孤立的，它们是最终项目的零件，别跳过
- 代码一定要手敲，不要复制粘贴；报错了自己读最后一行找原因
- 中断一两天没关系，但别断一周；首页的「学习进度打卡」可以边学边勾
- 文档刻意**不提供完整参考答案**——卡住时先看提示（可展开的折叠块），再看知识点回顾

## ✏️ 贡献者/维护者指引

### 修改或新增文档

- 文档源是 `docs/` 下的纯 Markdown，每日文档在 `docs/java/`，命名格式：`dayXX-主题.md`
- **新增一篇每日文档后，必须同步更新 `docs/java/_sidebar.md`**（Java 分区的子侧边栏），否则侧边栏不显示
- **新增一个主题目录时**（如再来一门语言的教程）：在根侧边栏 `docs/_sidebar.md` 加一行入口；内容较多（约 10 篇以上）就为该目录建自己的 `_sidebar.md`（顶部放「🏠 返回首页」，链接用站点根绝对路径如 `/python/xxx.md`）
- 每日文档保持统一的五段式模板：🎯 今日目标 → ⚡ 知识点速览 → 💻 跟着写 → 🧠 费曼时刻 → ✅ 自测清单
- 文档末尾保留「上一天 / 首页 / 下一天」的导航链接

### 图表（mermaid）注意事项

- 站点使用 [mermaid@10](https://mermaid.js.org/) 渲染图表，支持的类型：`flowchart`、`classDiagram`、`mindmap`、`sequenceDiagram`
- 节点文字含括号、逗号等特殊字符时，用引号包裹：`A["文字（含括号）"]`，否则解析失败会显示 Syntax error
- 提交前务必本地起服务确认新图表渲染正常（见下方验证步骤）

### 修改后如何验证

```bash
python -m http.server 3000 --directory docs
# 浏览器打开 http://127.0.0.1:3000，检查：
# 1) 侧边栏能看到并打开新/改的文档
# 2) mermaid 图表渲染为图形而非源码文本
# 3) 文内链接（上一天/下一天、跨教程引用）不断链
```

### 内容红线

- **不要往文档里补完整参考答案**——骨架、提示、关键片段是刻意的教学设计（费曼式学习）
- 代码示例保持可在 JDK 21 直接运行，不引入框架和外部依赖

## ❓ 常见问题

| 问题 | 解决办法 |
|---|---|
| 页面空白/一直「正在加载」 | 首次打开需联网加载 CDN 上的 JS；确认网络后刷新 |
| 端口被占用 | 换个端口：`python -m http.server 3001 --directory docs --bind 127.0.0.1` |
| 终端打印 `Serving HTTP on :: port 3000` | 正常现象：`::` 表示「监听本机所有网卡」，不是可访问的网址；浏览器访问 `http://127.0.0.1:3000` 即可。想让它打印得直观，就按上方命令加上 `--bind 127.0.0.1` |
| 改了文档或侧边栏，页面看起来没变 | 浏览器缓存了旧的 Markdown 文件：按 `Ctrl + F5` 强制刷新；仍不行就重启本地服务 |
| 窄窗口下侧边栏不见了 | docsify 响应式设计，点击左下角 ☰ 按钮展开，或把窗口拉宽 |
| 不想起服务，能看吗 | 可以：GitHub 上直接浏览 `docs/java/` 下的 md 文件（GitHub 原生渲染 mermaid）；或用 VS Code 打开 |
| 学到一半电脑换了 | 进度在文档里勾选的状态不会跨设备保存，用自己笔记里的教学卡片续接即可 |

## 项目结构

```
cs-campus/
├── docs/                # 学习计划文档站（Docsify）
│   ├── index.html       # 站点入口（CDN 加载 docsify + mermaid）
│   ├── README.md        # 计划总览（站点首页）
│   ├── _sidebar.md      # 根侧边栏（门户式：只放各主题入口）
│   ├── java/            # Java 计划 Day 0 ~ Day 14 每日文档（含自己的 _sidebar.md）
│   ├── git/             # Git 入门教程（拉取/推送/合并）
│   ├── python/          # Python 入门教程
│   ├── markdown/        # Markdown 入门教程
│   ├── mysql/           # MySQL 入门教程（SQL + JDBC）
│   ├── linux/           # Linux 入门教程（命令行）
│   ├── redis/           # Redis 入门教程（内存数据库）
│   ├── http/            # HTTP / REST 入门教程
│   ├── mybatis/         # MyBatis 入门教程（持久层框架）
│   └── zcode/           # 用 ZCode 创建教程的方法手册
├── AGENTS.md            # AI 协作规范（给编码代理的仓库约定）
└── README.md
```

## 参与贡献

1. Fork 本仓库并创建你的分支：`git checkout -b feature/your-feature`
2. 提交更改：`git commit -m "Add your feature"`
3. 推送分支：`git push origin feature/your-feature`
4. 发起 Pull Request

## 许可证

[MIT](LICENSE)
