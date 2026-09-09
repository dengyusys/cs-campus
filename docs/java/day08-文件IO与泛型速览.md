# Day 8 · 文件 IO 与泛型速览

> 📅 阶段一：语法速过（收官） ｜ ⏱ 建议用时：1.5~2 小时 ｜ 💻 数据能存进硬盘，程序才算有了「记忆」

## 🎯 今日目标

1. 会用字符流把文本**写入文件**、从文件**读出来**
2. 掌握 `try-with-resources` 自动关流
3. 完成练习：学生数据存取 —— 这就是实战项目「持久化」模块的预演

## ⚡ 知识点速览

### 为什么需要文件？

程序里的数据（变量、数组、集合）都活在**内存**里 —— 程序一关，全部蒸发。想让数据活过下一次开机，就得写进**文件**（硬盘）：

```mermaid
flowchart LR
  A["内存中的数据<br>（List&lt;Student&gt;）"] -->|"写文件<br>save"| B["硬盘上的文件<br>students.txt"]
  B -->|"读文件<br>load"| A
```

这个「写出去 / 读回来」的动作，就是**持久化（Persistence）**。Day 12 给学生管理系统装上它。

### Java IO 的派系（扫一眼就好）

Java IO 类巨多，是因为两两组合：字节流/字符流 × 输入/输出 × 普通流/缓冲流。**我们只学字符缓冲流这一条线**（纯文本场景够用）：

| 类 | 方向 | 关键方法 |
|---|---|---|
| `BufferedWriter` | 往文件写 | `write(s)`、`newLine()` |
| `BufferedReader` | 从文件读 | `readLine()` 读一行（没有更多行返回 `null`） |

### 写文件：try-with-resources

```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class WriteDemo {
    public static void main(String[] args) {
        //                  文件名        true = 追加模式（不写则覆盖）
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("students.txt", true))) {
            bw.write("1001,小明,20,88.5");
            bw.newLine();                       // 换行
            bw.write("1002,小红,19,92.0");
            bw.newLine();
        } catch (IOException e) {
            System.out.println("写文件失败：" + e.getMessage());
        }
    }
}
```

> 💡 `try (...)` 括号里创建的对象，**用完自动关闭**，不用手写 `bw.close()`（忘关流会导致数据丢失/文件被占用）。这个语法叫 try-with-resources，今天起养成习惯。
>
> 💡 文件写在**项目根目录**（和 `src` 同级），去资源管理器里找到它用记事本打开看看。

### 读文件：readLine 循环

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class ReadDemo {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("students.txt"))) {
            String line;
            while ((line = br.readLine()) != null) {   // 一行行读，读到 null 为止
                System.out.println("读到：" + line);
            }
        } catch (IOException e) {
            System.out.println("读文件失败：" + e.getMessage());
        }
    }
}
```

`(line = br.readLine()) != null` 这个「赋值 + 判断」连招是固定套路：读一行、存进 line、不是 null 就处理。

### 文本格式设计：CSV 风格

一行一条记录，字段用逗号隔开 —— 简单、人类可读、Excel 都能打开：

```
1001,小明,20,88.5
1002,小红,19,92.0
```

读回来时用 Day 6 学的 `split(",")` 拆开：

```java
String[] parts = line.split(",");
// parts[0]="1001"  parts[1]="小明"  parts[2]="20"  parts[3]="88.5"

int id = Integer.parseInt(parts[0]);          // 字符串 → int
int age = Integer.parseInt(parts[2]);
double score = Double.parseDouble(parts[3]);  // 字符串 → double
// 拿着这四个值 new Student(...) —— 文件里的字复活成了对象！
```

### 编码一句话

文件编码统一 **UTF-8**。如果读出来是乱码，多半是文件不是 UTF-8 存的（记事本另存为时可选编码）。

## 💻 跟着写

### 练习 1：名片本（跟打，约 20 分钟）

程序循环问「输入一句留言（直接回车结束）」，每句追加写入 `notes.txt`；退出后自动读一遍文件把所有留言打印出来。跑两遍程序，确认第二次的内容还在（追加模式的意义）。

### 练习 2：学生存档（核心练习，项目预演，约 35 分钟）

1. 复用你的 `Student` 类（字段：id、name、age、score）
2. main 里建 `List<Student>` 装 3 个学生
3. 写方法 `static void saveStudents(List<Student> list)`：**覆盖模式**写入 `students.txt`，一行一个，逗号分隔
4. 写方法 `static List<Student> loadStudents()`：读文件，`split` 解析，`new Student(...)` 装回列表并返回
5. main 里：save 之后再 load，遍历打印验证「复活」成功

卡壳检查点：
- 写出的文件内容看不到？→ 用记事本打开 `students.txt` 确认
- 解析报 `NumberFormatException`？→ 打印 `line` 和 `parts` 看哪一段不是纯数字；常见凶手：写文件时末尾多了个空行、逗号是中文全角的
- 循环里拼每行用什么来着？→ `StringBuilder` 或直接 `bw.write(s.getId() + "," + ...)` 皆可，行数少无所谓

### 练习 3：日志小工具（独立，约 15 分钟）

写方法 `static void log(String message)`：把 `当前时间 + 消息` 追加写入 `app.log`。时间一行白嫖：

```java
import java.time.LocalDateTime;
String now = LocalDateTime.now().withNano(0).toString();   // 2026-09-09T19:30:00
```

## 🧠 费曼时刻

**教学卡片**：

```markdown
## Day 8 教学卡片：文件 IO
- 「流」的类比讲讲：水从哪流到哪？write 和 read 分别是什么动作？
- try-with-resources 帮我省了什么事？不关流会怎样？
- save 和 load 各做了哪几步？（对象 → 文本 / 文本 → 对象）
- 明天的项目里，为什么保存数据必须先“变成字符串”？
- 我讲卡壳的地方：
```

## ✅ 自测清单

- [ ] 会默写 try-with-resources 写文件、while-readLine 读文件两个套路
- [ ] 知道 FileWriter 第二个参数 true 是干嘛的
- [ ] 会用 `Integer.parseInt` 把字符串转成数字
- [ ] 学生存档练习完成：保存 → 删掉内存数据 → 加载 → 数据复活
- [ ] 完成了今天的教学卡片

---
[⬅️ 上一天](day07-异常与集合.md) ｜ [🏠 返回首页](/) ｜ [下一阶段：项目实战 Day 9 ➡️](day09-项目启动.md)

🎉 **恭喜！语法速过阶段结束。** 你已经集齐了实战项目的全部零件：类与对象（Day 4-5）、集合（Day 7）、文件 IO（Day 8）、安全输入（Day 7）。接下来 6 天，把它们组装成一部完整的软件。
