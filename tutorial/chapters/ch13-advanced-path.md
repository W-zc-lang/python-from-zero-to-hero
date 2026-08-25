## 第 13 章 进阶与精通之路

**Chapter 13: The Path to Advanced and Proficient Python**

走到这里，你已经掌握了 Python 的骨架。下面这些"工程化"能力，是把你从"会写"推向"写得专业"的关键。

By now you have mastered the skeleton of Python. The "engineering" skills below are what take you from "able to write" to "writing professionally."

### 13.1 虚拟环境

**13.1 Virtual Environments**

不同项目可能需要同一个库的不同版本，装在一起会冲突。**虚拟环境**为每个项目创建独立的库空间：

Different projects may need different versions of the same library, and installing them together causes conflicts. A **virtual environment** gives each project its own isolated library space:

```bash
python -m venv venv        # 创建名为 venv 的虚拟环境
source venv/bin/activate   # macOS/Linux 激活
venv\Scripts\activate      # Windows 激活
pip install requests       # 只在当前环境安装
deactivate                 # 退出环境
```

> 经验：每个新项目都先建虚拟环境，再装依赖。这是专业开发的标配。

> Tip: For every new project, create a virtual environment first, then install dependencies. This is standard practice in professional development.

### 13.2 代码风格与规范（PEP 8）

**13.2 Code Style and Conventions (PEP 8)**

Python 有一套官方推荐的代码风格 PEP 8，遵守它能让代码更统一、更易读：

Python has an officially recommended code style, PEP 8. Following it makes your code more consistent and readable:

- 缩进 4 个空格。
- Indent with 4 spaces.
- 变量/函数名用小蛇式 `my_var`，类名用大驼峰 `MyClass`。
- Use `snake_case` for variables and functions, and `CamelCase` for class names.
- 运算符两边加空格：`x = 1 + 2`。
- Put spaces around operators: `x = 1 + 2`.
- 一行不超过约 79 个字符。
- Keep lines under about 79 characters.

可以用 `flake8` / `black` 等工具自动检查和格式化。

You can use tools like `flake8` / `black` to automatically check and format your code.

### 13.3 调试技巧

**13.3 Debugging Tips**

- 多用 `print()` 看中间值（初学者最快上手）。
- Use `print()` often to inspect intermediate values—the fastest way for beginners to get started.
- 学会用编辑器**断点调试**（VS Code 的 Debug 面板），一步步看变量变化。
- Learn to use the editor's **breakpoint debugging** (the Debug panel in VS Code) to watch variables change step by step.
- 读懂报错信息：报错最后一行通常是关键，往上找你自己的文件那一行。
- Learn to read error messages: the last line of a traceback is usually the key—then look upward to the line in your own file.

### 13.4 单元测试

**13.4 Unit Testing**

用标准库 `unittest` 或第三方 `pytest` 为函数写测试，确保改动不破坏旧功能：

Use the standard library's `unittest` or the third-party `pytest` to write tests for your functions, ensuring changes don't break existing features:

```python
# test_math.py
def add(a, b):
    return a + b

def test_add():
    assert add(2, 3) == 5
    assert add(-1, 1) == 0
```

```bash
pip install pytest
pytest test_math.py
```

### 13.5 版本控制（Git）

**13.5 Version Control (Git)**

把代码放进 Git 仓库（如 GitHub），能记录每一次改动、方便协作和回滚：

Putting your code into a Git repository (such as GitHub) records every change and makes collaboration and rollbacks easy:

```bash
git init
git add .
git commit -m "完成基础功能"
git push origin main
```

### 13.6 学习路线图

**13.6 Learning Roadmap**

![学习路线图](../images/roadmap.svg)

| 阶段 | 目标 | 推荐小项目 |
| --- | --- | --- |
| 1 入门 | 语法与基础 | 计算器、猜数字游戏 |
| 2 进阶 | 组织与复用 | 通讯录、待办清单（含文件存储） |
| 3 熟练 | 标准库与生态 | 批量文件重命名、简易爬虫 |
| 4 精通 | 工程化与方向 | Web 应用、数据分析报告、开源贡献 |
| ★ 专家 | 方向深耕 | 读源码、写轮子、教别人 |

| Stage | Goal | Recommended Mini-Project |
| --- | --- | --- |
| 1 Beginner | Syntax & Basics | Calculator, number-guessing game |
| 2 Intermediate | Organization & Reuse | Address book, to-do list (with file storage) |
| 3 Proficient | Standard Library & Ecosystem | Batch file renaming, simple scraper |
| 4 Mastery | Engineering & Direction | Web app, data analysis report, open-source contribution |
| ★ Expert | Deep Specialization | Read source code, build your own libraries, teach others |

---

