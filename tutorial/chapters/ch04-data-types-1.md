## 第 4 章 数据类型（一）：数字、字符串、布尔

**Chapter 4: Data Types (1): Numbers, Strings, Booleans**

数据在程序里都要"装"在某种类型里。Python 的数据类型可以分为**不可变类型**（内容创建后不能改）和**可变类型**（内容可增删改）。本章先讲不可变的三种基础类型。

In a program, every piece of data has to be "held" in some type. Python's data types fall into **immutable types** (contents can't change once created) and **mutable types** (contents can be added to, removed, or modified). This chapter covers the three basic immutable types first.

### 4.1 数字：int 与 float

**4.1 Numbers: int and float**

```python
a = 10        # int 整数
b = 3.14      # float 浮点数（带小数）

print(a + b)  # 13.14  加法
print(a - b)  # 6.86   减法
print(a * b)  # 31.4   乘法
print(a / b)  # 3.18... 除法（结果永远是 float）
print(a // 3) # 3      整除（丢弃小数）
print(a % 3)  # 1      取余
print(a ** 2) # 100    幂运算（a 的 2 次方）
```

常用数学函数（来自标准库 `math`，详见第 12 章）：

Common math functions (from the `math` standard library—see Chapter 12 for details):

```python
import math
print(math.sqrt(16))  # 4.0  开方
print(math.floor(3.9))# 3    向下取整
print(math.ceil(3.1)) # 4    向上取整
print(math.pi)        # 3.141592... 圆周率
```

### 4.2 字符串：str

**4.2 Strings: str**

字符串是用**单引号 `'` 或双引号 `"`** 包裹的文本。

A string is text wrapped in **single quotes `'` or double quotes `"`**.

```python
s = "Hello, Python"
print(len(s))          # 13        字符串长度
print(s.upper())       # HELLO, PYTHON  转大写
print(s.lower())       # hello, python  转小写
print(s.replace("Python", "World"))  # Hello, World  替换
print("Py" in s)       # True  判断是否包含子串
```

**字符串拼接与格式化**（非常重要，日常高频）：

**String concatenation and formatting** (very important, used constantly in daily work):

```python
name = "小明"
age = 18

# 方式一：f-string（推荐，最直观，Python 3.6+）
print(f"{name}今年{age}岁")          # 小明今年18岁

# 方式二：.format()
print("{}今年{}岁".format(name, age))

# 方式三：拼接（注意类型要一致）
print(name + "今年" + str(age) + "岁")
```

> f-string 是目前最推荐的写法：在字符串前加 `f`，用 `{变量}` 直接嵌入，既清晰又不易出错。

> The f-string is currently the most recommended approach: put an `f` before the string and embed values directly with `{variable}`—it's both clear and less error-prone.

**字符串切片**（截取其中一段）：

**String slicing** (extracting a section of it):

```python
s = "abcdef"
print(s[0])     # a    取下标 0（第一个）
print(s[1:4])   # bcd  取下标 1 到 3（含头不含尾）
print(s[:3])    # abc  从头取到下标 2
print(s[::2])   # ace  每隔一个取一个
print(s[::-1])  # fedcba  反转字符串
```

下标从 0 开始数，这是编程世界的通用约定，务必适应。

Indexing starts at 0—a universal convention in the programming world, so get used to it.

### 4.3 布尔：bool

**4.3 Booleans: bool**

布尔类型只有两个值：`True`（真）和 `False`（假），常用于条件判断。

The boolean type has only two values—`True` and `False`—and is mainly used in conditional tests.

```python
print(3 > 2)    # True
print(3 == 2)   # False  注意：判断相等用 ==，一个 = 是赋值
print(3 != 2)   # True   不等于
print(3 > 1 and 1 > 0)  # True  并且（都成立才真）
print(3 > 1 or 1 > 9)   # True  或者（有一个成立就真）
print(not True)         # False 取反
```

> 记住一个易错点：**赋值用 `=`，判断相等用 `==`**。初学者最常见的 bug 就是把 `if x == 5` 写成 `if x = 5`。

> Remember this common trap: **use `=` to assign, and `==` to test equality**. The most frequent beginner bug is writing `if x = 5` when you meant `if x == 5`.

### 4.4 字符串与数字的更多细节

**4.4 More Details on Strings and Numbers**

**(1) 转义字符**：让字符串里能放引号、换行等特殊符号。

**(1) Escape characters**: these let you put quotes, newlines, and other special symbols inside a string.

```python
print("他说：\"你好\"")   # 用 \" 在字符串里放一个双引号
print("第一行\n第二行")    # \n 表示换行
print("C:\\Users\\name")  # \\ 表示一个真正的反斜杠
print(r"C:\Users\name")   # 前缀 r 让反斜杠"不转义"（原始字符串）
```

**(2) f-string 进阶**：除了 `{变量}`，还能控制格式。

**(2) Advanced f-strings**: beyond `{variable}`, you can also control formatting.

```python
x = 3.14159
print(f"{x:.2f}")         # 3.14        保留两位小数
print(f"{x=}")            # x=3.14159   调试神器：连变量名一起打印
name = "python"
print(f"{name:>10}")      # "    python" 右对齐，总宽 10
print(f"{name:*^10}")     # "**python**" 居中，用 * 填充两侧
```

格式说明符结构：`{变量:对齐 宽度.精度 类型}`，记住常用几个即可：`>10` 右对齐、`<10` 左对齐、`^10` 居中、`.2f` 两位小数、`,` 千分位。

The structure of a format specifier is `{variable:alignment width.precision type}`. Just remember the common ones: `>10` right-align, `<10` left-align, `^10` center, `.2f` two decimal places, `,` thousands separator.

**(3) 进制表示**：计算机世界常用二进制、八进制、十六进制。

**(3) Number bases**: the computing world commonly uses binary, octal, and hexadecimal.

```python
print(0b1010)   # 10   二进制前缀 0b
print(0o17)     # 15   八进制前缀 0o
print(0xff)     # 255  十六进制前缀 0x
print(bin(10))  # 0b1010   十进制转二进制
print(hex(255)) # 0xff      十进制转十六进制
```

> ✏️ **小练习**：用 f-string 把 `price = 9.9` 格式化为 `￥9.90`（提示：用 `:.2f` 得到 `9.90`，再拼接 `￥`）；再用 `bin()` 打印数字 8 的二进制形式。

> ✏️ **Exercise**: use an f-string to format `price = 9.9` as `￥9.90` (hint: use `:.2f` to get `9.90`, then concatenate `￥`); then use `bin()` to print the binary form of the number 8.

---

