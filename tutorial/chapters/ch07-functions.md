## 第 7 章 函数：封装可复用的代码

**Chapter 7: Functions: Encapsulating Reusable Code**

当你发现同一段逻辑要写好几遍时，就该用函数了。函数是一段**有名字、可重复调用**的代码块，是"把复杂问题拆小"的核心工具。

When you find yourself writing the same logic several times, it is time to use a function. A function is a **named, reusable** block of code—the core tool for "breaking a complex problem into smaller pieces".

![函数结构示意](../images/functions.svg)

### 7.1 定义与调用

**7.1 Definition and Calling**

```python
def add(a, b):
    """返回两个数之和（这是文档字符串，可用 help(add) 查看）"""
    result = a + b
    return result

print(add(3, 5))   # 8
```

- `def` 是定义函数的关键字。
- `def` is the keyword used to define a function.
- `add` 是函数名，命名规则和变量一致。
- `add` is the function name; naming rules are the same as for variables.
- `(a, b)` 是**参数**，调用时传进来的数据。
- `(a, b)` are the **parameters**—the data passed in when the function is called.
- `return` 把结果"交还"给调用者；不写 `return` 默认返回 `None`。
- `return` "hands back" the result to the caller; without a `return`, the function returns `None` by default.

### 7.2 四种参数

**7.2 Four Kinds of Parameters**

```python
# 1. 位置参数：按先后位置对应
def greet(name, age):
    print(f"{name}今年{age}岁")

greet("小明", 18)

# 2. 默认参数：调用时不传就用默认值
def greet(name, age=18):
    print(f"{name}今年{age}岁")

greet("小红")          # 小红今年18岁
greet("小红", 20)      # 小红今年20岁

# 3. 可变参数 *args：接收任意个位置参数，打包成元组
def total(*args):
    return sum(args)

print(total(1, 2, 3))  # 6

# 4. 关键字参数 **kwargs：接收任意个键值对，打包成字典
def show(**kwargs):
    print(kwargs)

show(name="小明", age=18)   # {'name': '小明', 'age': 18}
```

> 默认参数必须放在普通参数之后，否则会报错。这是初学者常踩的坑。

> Default parameters must come after ordinary parameters, otherwise an error occurs. This is a common pitfall for beginners.

### 7.3 返回值

**7.3 Return Values**

函数可以返回任意类型，甚至返回多个值（本质是返回一个元组）：

A function can return any type, and can even return multiple values (which is essentially returning a tuple):

```python
def min_max(nums):
    return min(nums), max(nums)

low, high = min_max([3, 1, 9, 2])
print(low, high)   # 1 9
```

### 7.4 作用域：变量能"看到"的范围

**7.4 Scope: the Range Variables Can "See"**

- **局部变量**：在函数内部定义的变量，只在函数内有效。
- **Local variables**: defined inside a function and valid only within that function.
- **全局变量**：在函数外部定义的变量，整个文件都能用。
- **Global variables**: defined outside any function and usable throughout the whole file.

```python
x = 10          # 全局变量

def foo():
    x = 5       # 局部变量，和外面的 x 互不干扰
    print(x)    # 5

foo()
print(x)        # 10
```

如果想在函数里修改全局变量，需要用 `global` 声明：

If you want to modify a global variable inside a function, you must declare it with `global`:

```python
count = 0
def increment():
    global count
    count += 1

increment()
print(count)    # 1
```

> 实际开发中，应尽量少依赖全局变量，多用参数传递和返回值，代码更可控、更好测。

> In real development, you should rely on global variables as little as possible—use parameter passing and return values instead, which makes the code more controllable and easier to test.

### 7.5 匿名函数 lambda

**7.5 Anonymous Functions (lambda)**

`lambda` 用于定义"一句话小函数"，常用于排序或作为参数传递：

`lambda` is used to define "one-line mini-functions", often for sorting or as arguments passed to other functions:

```python
square = lambda x: x * x
print(square(4))              # 16

# 常见用法：按对象的某个字段排序
students = [{"name": "A", "score": 90}, {"name": "B", "score": 70}]
students.sort(key=lambda s: s["score"])
print(students)   # 按分数从低到高排
```

### 7.6 函数进阶：递归、文档字符串、类型标注与 \_\_main\_\_

**7.6 Functions Advanced: Recursion, Docstrings, Type Hints, and \_\_main\_\_**

**(1) 递归**：函数自己调用自己，必须配有"终止条件"，否则会无限递归直到报错。

**(1) Recursion**: a function calls itself. It must have a "termination condition", otherwise it recurses infinitely until an error is raised.

```python
def factorial(n):
    if n == 0:              # 终止条件
        return 1
    return n * factorial(n - 1)

print(factorial(5))         # 120  = 5×4×3×2×1
```

递归适合"大问题能拆成相同结构的小问题"的场景，如遍历文件夹、斐波那契数列等。但要注意：太深的递归会消耗大量内存。

Recursion fits scenarios where "a big problem can be broken into smaller problems of the same structure", such as traversing folders or computing the Fibonacci sequence. But note: recursion that is too deep consumes a lot of memory.

**(2) 文档字符串（docstring）**：用三个引号写在函数第一行，可用 `help()` 查看，是"自解释"的好习惯。

**(2) Docstrings**: written on the first line of a function using triple quotes and viewable via `help()`. It is a good habit that makes code "self-explanatory".

```python
def add(a, b):
    """返回 a 与 b 的和。"""
    return a + b

help(add)    # 会显示上面的说明文字
```

**(3) 类型标注（Type Hints）**：给参数和返回值"标注类型"，**不影响运行**，但能让编辑器实时提示、让读代码的人更清楚（Python 3.5+）。

**(3) Type Hints**: "annotate" the parameters and return value with types. This **does not affect execution**, but lets the editor give real-time hints and makes the code clearer to readers (Python 3.5+).

```python
def greet(name: str, age: int) -> str:
    return f"{name} 今年 {age} 岁"
```

**(4) `if __name__ == "__main__"`**：让同一个文件"既能当模块被别人导入，又能自己直接运行"。

**(4) `if __name__ == "__main__"`**: lets the same file "act as an importable module for others, yet also run directly on its own".

```python
def main():
    print("程序入口逻辑写这里")

if __name__ == "__main__":
    main()   # 只有用 python app.py 直接运行时才执行；被 import 时不执行
```

> ✏️ **小练习**：写一个递归函数 `sum_to(n)`，计算 `1 + 2 + ... + n`；再用类型标注改写你之前写过的某个函数。

> ✏️ **Exercise**: write a recursive function `sum_to(n)` that computes `1 + 2 + ... + n`; then rewrite one of your earlier functions using type hints.

---

