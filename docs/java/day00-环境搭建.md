# Day 0 · 环境搭建

> 📅 阶段一：语法速过 ｜ ⏱ 建议用时：1~1.5 小时 ｜ 🎯 今天不学语法，只做一件事：**让 Java 程序在你的电脑上跑起来**

## 🎯 今日目标

1. 装好 JDK 21 和 IntelliJ IDEA 社区版
2. 用命令行和 IDEA 各跑通一次 Hello World
3. 大致明白「Java 程序是怎么运行的」

## ⚡ 知识点速览

### 三个名词，一句话说清

| 名词 | 是什么 | 类比 |
|---|---|---|
| **JVM**（Java 虚拟机） | 真正运行 Java 程序的「虚拟电脑」 | 播放器 |
| **JRE**（Java 运行环境） | JVM + 一些基础库 | 播放器 + 解码器 |
| **JDK**（开发工具包） | JRE + 编译器等开发工具 | 制作工具 |

我们要装的是 **JDK**（开发者用），版本选 **21**（长期支持版 LTS）。

### Java 程序的运行过程

你写的 `.java` 文件（源代码）不能直接运行，要先「编译」成 `.class` 文件（字节码），再交给 JVM 执行：

```mermaid
flowchart LR
  A["Hello.java<br>源代码（人写的）"] -->|"javac 编译"| B["Hello.class<br>字节码（中间产物）"]
  B -->|"java 运行"| C["JVM<br>Java 虚拟机"]
  C --> D["控制台输出<br>Hello, World!"]
```

因为有 JVM 这一层「中间商」，同一个 `.class` 文件在 Windows / Mac / Linux 上都能跑 —— 这就是 Java 著名的 **「一次编写，到处运行」**。

## 💻 跟着写

### 任务 1：安装 JDK 21（约 20 分钟）

1. 打开 [Adoptium 官网](https://adoptium.net/)（Eclipse Temurin，免费开源）
2. 选择 **JDK 21，Windows，x64，msi** 安装包下载
3. 安装时一路下一步，**保持默认的「设置 JAVA_HOME」选项勾选**
4. 验证：打开终端（`Win + R` 输入 `cmd` 回车），输入：

```bash
java -version
javac -version
```

看到版本号里有 `21` 就成功了。

> ⚠️ 常见坑：提示 `'javac' 不是内部或外部命令` —— 说明安装时没勾选加入 PATH。重新运行安装包选 Modify，或手动把 JDK 的 `bin` 目录加入系统环境变量 PATH。

### 任务 2：命令行版 Hello World（约 20 分钟）

先感受一次「最原始」的编译运行，以后再让 IDE 替我们干这些活。

1. 新建文件夹 `D:\java-learn`，在里面新建文本文件 `Hello.java`（注意：**文件名必须和类名完全一致**）
2. 用记事本（推荐先装个 [VS Code](https://code.visualstudio.com/) 编辑）写入：

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

3. 在该文件夹打开终端（资源管理器地址栏输入 `cmd` 回车），执行：

```bash
javac Hello.java    # 编译，会生成 Hello.class
java Hello          # 运行（注意：不带 .class 后缀）
```

看到 `Hello, World!` 输出，恭喜 —— 你已经完整走过一次 Java 的生命周期了。

> ⚠️ 中文乱码的话：文件用 UTF-8 编码保存，或编译时用 `javac -encoding UTF-8 Hello.java`。

### 任务 3：IDEA 版 Hello World（约 20 分钟）

命令行每次都要手动编译太麻烦，专业工具 **IntelliJ IDEA** 会一键搞定。

1. 下载 [IntelliJ IDEA 社区版](https://www.jetbrains.com/idea/download/)（Community Edition，**免费**，页面往下滑一点就能看到，别下成旗舰版）
2. 新建项目：`File → New → Project`，Name 填 `java-learn`，JDK 选 21，Create
3. 在 `src` 文件夹上右键 `New → Java Class`，命名 `Hello`
4. IDEA 会生成类骨架，在里面敲 `main` 然后**按 Tab 键**（代码补全），再敲 `sout` 按 Tab，你会得到打印语句
5. 点击代码左侧绿色 ▶️ 运行，下方控制台输出 `Hello, World!`

> 💡 从今天起，所有代码都在 IDEA 里写。快捷键先记两个：`sout + Tab` 生成打印语句，`Shift + F10` 运行。

## 🧠 费曼时刻

假设朋友问你：**「Java 不是说跨平台吗？为什么还要装 JDK？」**

试着用今天学的图讲给他听：源代码 → 字节码 → JVM 的三步流程，以及「跨平台」跨的是哪一步（JVM 屏蔽了不同操作系统的差异）。

**教学卡片**（复制到自己的笔记里填写）：

```markdown
## Day 0 教学卡片：Java 程序是怎么运行的
- 用我自己的话讲：
  - （写 3~5 句大白话，不许出现「编译原理」这类术语）
- 我讲卡壳的地方：
  - （哪句讲不下去了？回去重看哪个图？）
- 一个生活中的类比：
  - （比如：点菜 → 后厨加工 → 上菜？）
```

## ✅ 自测清单

- [ ] `java -version` 能看到 21
- [ ] 我在命令行用 `javac` 和 `java` 跑通过 Hello World
- [ ] 我在 IDEA 里跑通过 Hello World，会用 `sout` 补全
- [ ] 能说出 `.java`、`.class`、JVM 三者之间的关系
- [ ] 完成了今天的教学卡片

---
[🏠 返回首页](/) ｜ [下一天：第一个程序与变量 ➡️](day01-第一个程序与变量.md)
