# 📘 Typst Homework Template

这是一个专为 **计算机科学 (CS)** 和 **数学** 作业设计的 Typst 模版。

它基于 `showybox` 构建，内置了智能的配色方案、自动机绘制支持、抽象语法树绘制支持以及优雅的代码块排版。

## ✨ 特性 (Features)

*   **🎨 智能配色**：题目颜色基于题号自动轮转（蓝 -> 橙 -> 紫 -> 橄榄 -> 红...），无需手动指定。
*   **📦 一体化设计**：题目（Problem）与解答（Solution）整合在同一个漂亮的圆角框中。
*   **🧠 智能布局**：
    *   **有题有解**：由虚线优雅分隔。
    *   **只有题目**：自动隐藏虚线和 Solution 标题。
    *   **只有解答**：自动适配纯代码或纯证明的提交。
*   **💻 代码美化**：预设了类似 IDE 的代码块样式（灰色背景、圆角、行号）。
*   **🔤 字体回退**：优先使用 *Linux Libertine* 和 *思源宋体*；若系统未安装，自动回退到 *Times New Roman* 和 *中易宋体*，**保证不报错**。
*   **🛠️ 开箱即用**：预装且修复了 `finite` (自动机) 和 `fletcher` (绘图) 的集成问题。

## 🚀 快速开始

### 1. 文件结构
确保你的作业目录包含以下文件：
- `assignment.typ`: 模版核心文件（包含所有样式逻辑）。
- `hw1.typ`: 你的作业主文件。

### 2. 编写作业 (`hw1.typ`)

```typst
#import "assignment.typ": *
// 如果需要画自动机或图，取消下面这行的注释
// #import "@preview/finite:0.5.0": automaton
// #import "@preview/fletcher:0.5.8" as fletcher: diagram, node, edge

#show: homework.with(
  title: "Assignment 1",
  course: "Compiler Principles",
  author: "你的名字",
  student-id: "你的学号",
  date: datetime.today().display()
)

// 开始写题...
```

## 📖 使用指南

模版核心是 `prob` 函数，支持三种模式：

### 1. 标准模式（题目 + 答案）
```typst
#prob(
  title: "Regular Expressions", // 可选标题
  solution: [
    这里写解答。
    $ Sigma = { a, b } $
  ]
)[
  这里写题目描述...
]
```

### 2. 只有题目（无解答）
适用于只抄题或者 Open Problem。
```typst
#prob(title: "Thinking")[
  只写题目内容。
  盒子中间不会出现虚线。
]
```

### 3. 只有答案（无题目）
适用于老师让你只交答案的情况。**注意末尾加上空的 `[]`**。
```typst
#prob(
  title: "Code Submission",
  solution: [
    ```python
    def solve(): return 42
    ```
  ]
)[] // <--- 关键：这里留空
```

## ⚠️ 常见问题与避坑 (Troubleshooting)

由于 Typst 与 LaTeX 语法不同，新手常遇到以下报错：

### 1. 变量报错 `unknown variable: igma` / `dash`
*   **原因**：Typst 的数学模式**不需要反斜杠**转义。
*   **解决**：
    *   ❌ `$ \Sigma $`, `$ \{ a, b \} $`
    *   ✅ `$ Sigma $`, `$ { a, b } $` (直接写变量名，集合直接用花括号)

### 2. 复杂变量名报错 `unknown variable: NP`
*   **原因**：数学模式下，两个字母连在一起（如 NP）会被视为一个未定义的变量或函数。
*   **解决**：
    *   ❌ `$ P = NP $`
    *   ✅ `$ P = "NP" $` (加上双引号使其变为文本)

### 3. 自动机状态报错 `found integer`
*   **原因**：`finite` 包要求状态名称必须是**字符串**。
*   **解决**：
    *   ❌ `(0: 1)`
    *   ✅ `("0": "1")` (这是字典的键值对，数字两边要加引号)

### 4. 字体警告 `unknown font family`
*   **说明**：这是正常的。模版会尝试加载 *Linux Libertine*，如果找不到，会自动切换到 Windows 自带的 *Times New Roman*。这不会影响 PDF 的生成。

## 📦 依赖

本模版使用了以下 Typst Packages (编译时自动下载)：
*   `@preview/showybox:2.0.3` (请务必使用 2.0.3 以修复 margin bug)
*   `@preview/finite:0.5.0`
*   `@preview/fletcher:0.5.8`

---
*Happy Typsting!*