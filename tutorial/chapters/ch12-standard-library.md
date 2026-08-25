## 第 12 章 常用标准库：站在巨人的肩膀上

**Chapter 12: Common Standard Libraries: Standing on the Shoulders of Giants**

**标准库**随 Python 一起安装，无需 `pip` 就能 `import` 使用。它是你日常开发最可靠的"官方工具箱"。

The **standard library** ships with Python, so you can `import` and use it without `pip`. It is your most reliable "official toolkit" for everyday development.

![常用标准库](../images/stdlib.svg)

### 12.1 os / pathlib：与文件系统打交道
**12.1 os / pathlib: Working with the File System**

```python
import os
print(os.listdir("."))          # 当前目录文件列表
print(os.getcwd())               # 当前工作目录
os.makedirs("a/b/c", exist_ok=True)  # 递归创建目录

# 更现代的写法：pathlib（面向对象，推荐）
from pathlib import Path
p = Path("data/test.txt")
print(p.name)        # test.txt
print(p.suffix)      # .txt
p.parent.mkdir(parents=True, exist_ok=True)
```

### 12.2 sys：与解释器交互
**12.2 sys: Interacting with the Interpreter**

```python
import sys
print(sys.version)    # Python 版本信息
print(sys.argv)       # 命令行参数列表（sys.argv[0] 是脚本名）
```

### 12.3 math：数学运算
**12.3 math: Mathematical Operations**

```python
import math
math.sqrt(2)    # 开方
math.factorial(5)  # 120  阶乘
math.pi        # 圆周率
```

### 12.4 datetime：处理日期时间
**12.4 datetime: Working with Dates and Times**

```python
from datetime import datetime, timedelta

now = datetime.now()
print(now)                       # 2026-08-25 18:47:35.xxx
print(now.strftime("%Y-%m-%d"))  # 2026-08-25  格式化输出

later = now + timedelta(days=7)  # 7 天后
print(later)
```

### 12.5 random：随机数
**12.5 random: Random Numbers**

```python
import random
print(random.randint(1, 100))     # 1~100 随机整数
print(random.choice(["红", "绿", "蓝"]))  # 随机选一个
random.shuffle([1, 2, 3, 4])     # 原地打乱
```

### 12.6 re：正则表达式
**12.6 re: Regular Expressions**

用于复杂的文本匹配与提取：

Used for complex text matching and extraction:

```python
import re
text = "我的邮箱是 hello@python.com"
match = re.search(r"\w+@\w+\.\w+", text)
if match:
    print(match.group())   # hello@python.com
```

### 12.7 json：结构化数据
**12.7 json: Structured Data**

（已在第 10 章文件操作中介绍，是 Web 开发、配置文件、接口通信的基石。）

(Covered in the file operations of Chapter 10; it is the cornerstone of web development, configuration files, and API communication.)

### 12.8 collections：增强容器
**12.8 collections: Enhanced Containers**

```python
from collections import Counter, deque

# Counter：快速计数
print(Counter("aabbbc"))   # Counter({'b': 3, 'a': 2, 'c': 1})

# deque：双端队列，头尾增删都很快
dq = deque([1, 2, 3])
dq.appendleft(0)           # 头部插入
print(dq)                  # deque([0, 1, 2, 3])
```

### 12.9 其他值得认识的标准库
**12.9 Other Standard Libraries Worth Knowing**

| 库 | 用途 |
| --- | --- |
| `argparse` | 解析命令行参数（写 CLI 工具必备） |
| `itertools` | 迭代器工具（排列、组合、循环） |
| `logging` | 写日志（比 `print` 更专业，可分级） |
| `time` / `datetime` | 时间相关 |
| `subprocess` | 在 Python 里调用系统命令 |

| Library | Purpose |
| --- | --- |
| `argparse` | Parse command-line arguments (essential for CLI tools) |
| `itertools` | Iterator tools (permutations, combinations, looping) |
| `logging` | Write logs (more professional than `print`, with levels) |
| `time` / `datetime` | Time-related |
| `subprocess` | Invoke system commands from Python |

> 遇到需求，先想"标准库有没有现成的"，再考虑装第三方库。标准库经过千锤百炼，稳定又无需额外依赖。

> When you have a need, first ask "does the standard library already have it," then consider installing a third-party library. The standard library is battle-tested, stable, and needs no extra dependencies.

### 12.10 更多标准库速览与第三方生态
**12.10 More Standard Libraries at a Glance and the Third-Party Ecosystem**

除了前面讲到的，下表这些标准库也常在实战中露面：

Besides those covered above, these standard libraries also show up often in real projects:

| 库 | 一句话用途 | 关键用法示例 |
| --- | --- | --- |
| `time` | 休眠、时间戳 | `time.sleep(1)`、`time.time()` |
| `hashlib` | 生成 MD5 / SHA 摘要 | `hashlib.sha256(b"x").hexdigest()` |
| `base64` | 编码 / 解码 | `base64.b64encode(data)` |
| `sqlite3` | 轻量文件型数据库 | 内嵌 SQL，无需单独装服务 |
| `threading` | 多线程并发 | 把耗时任务放到后台跑 |
| `gzip` / `zipfile` | 压缩与解压 | 处理 `.gz`、`.zip` 文件 |

| Library | One-line purpose | Key usage example |
| --- | --- | --- |
| `time` | Sleep, timestamps | `time.sleep(1)`, `time.time()` |
| `hashlib` | Generate MD5 / SHA digests | `hashlib.sha256(b"x").hexdigest()` |
| `base64` | Encode / decode | `base64.b64encode(data)` |
| `sqlite3` | Lightweight file-based database | Embedded SQL, no separate service needed |
| `threading` | Multi-threaded concurrency | Run time-consuming tasks in the background |
| `gzip` / `zipfile` | Compression and decompression | Handle `.gz`, `.zip` files |

**当你要的能力标准库没有时**，就要请出**第三方库**（需 `pip install`）。下面这些几乎是每个方向都绕不开的"明星库"：

**When the standard library doesn't have what you need**, bring in **third-party libraries** (requires `pip install`). The ones below are "star libraries" almost every domain relies on:

| 方向 | 代表库 | 说明 |
| --- | --- | --- |
| HTTP 请求 | `requests` | 比标准库 `urllib` 好用十倍 |
| 数据分析 | `pandas`、`numpy` | 表格处理与高性能数值计算 |
| 可视化 | `matplotlib` | 画折线图、柱状图、散点图 |
| Web 后端 | `flask`、`django` | 搭建网站与接口 |
| 图像处理 | `pillow` | 缩放、裁剪、加水印 |
| 爬虫 | `beautifulsoup4`、`scrapy` | 解析网页、批量采集 |

| Domain | Representative library | Notes |
| --- | --- | --- |
| HTTP requests | `requests` | Ten times more pleasant than the standard `urllib` |
| Data analysis | `pandas`, `numpy` | Tabular processing and high-performance numerics |
| Visualization | `matplotlib` | Line, bar, and scatter plots |
| Web back-end | `flask`, `django` | Build websites and APIs |
| Image processing | `pillow` | Resize, crop, add watermarks |
| Web scraping | `beautifulsoup4`, `scrapy` | Parse web pages, batch collection |

> 💡 **选择建议**：第三方库前，先到 [PyPI](https://pypi.org)（Python 包索引）搜一搜，优先选"星标多、更新勤、文档全"的库。装之前看一眼它依赖什么、是否支持你当前的 Python 版本。

> 💡 **Selection tip**: Before choosing a third-party library, search [PyPI](https://pypi.org) (the Python Package Index) and prefer libraries that are "heavily starred, frequently updated, and well documented." Before installing, check what it depends on and whether it supports your current Python version.

> ✏️ **小练习**：用 `time` 库写一段代码，借助 `time.sleep(1)` 每隔 1 秒打印一次当前时间，共打印 3 次（提示：`from datetime import datetime` 取当前时间）；再用 `pip install requests` 装好 `requests`，试试用它 `requests.get("https://www.baidu.com")` 并查看返回的状态码 `r.status_code`。

> ✏️ **Exercise**: Using the `time` library, write code that prints the current time once per second with `time.sleep(1)`, three times in total (hint: `from datetime import datetime` to get the current time); then `pip install requests`, try `requests.get("https://www.baidu.com")` and inspect the returned status code `r.status_code`.

---

