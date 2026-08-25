## 第 11 章 异常处理：让程序更健壮

**Chapter 11: Exception Handling: Making Programs More Robust**

再完美的代码，运行时也可能遇到意外：用户输了字母、文件被删了、除以零……**异常处理**就是给程序装上的"安全气囊"，让它在出错时优雅应对，而不是直接崩溃。

No matter how perfect the code, unexpected things can happen at runtime: a user types letters, a file gets deleted, you divide by zero… **Exception handling** is the "airbag" you install in your program so it responds gracefully to errors instead of crashing outright.

![异常处理示意](../images/exceptions.svg)

### 11.1 try / except 基本结构
**11.1 The Basic try / except Structure**

```python
try:
    n = int(input("请输入一个数字: "))
    print(10 / n)
except ValueError:
    print("你输入的不是数字！")
except ZeroDivisionError:
    print("不能除以 0！")
```

执行逻辑：

Execution logic:

1. 先运行 `try` 里的代码。
1. First, run the code inside `try`.

2. 若抛出 `except` 指定的异常类型，就跳去执行对应的补救代码。
2. If an exception of the type named in `except` is raised, jump to the corresponding recovery code.

3. 若没出错，`except` 整段被跳过。
3. If nothing goes wrong, the entire `except` block is skipped.

### 11.2 else 与 finally
**11.2 else and finally**

```python
try:
    f = open("data.txt", "r", encoding="utf-8")
except FileNotFoundError:
    print("文件不存在")
else:
    print("文件打开成功")   # 没出错才执行
    f.close()
finally:
    print("无论如何都会执行")  # 常用于清理资源
```

- `else`：仅当 `try` 没出错时执行。
- `else`: Executes only when `try` raised no error.

- `finally`：无论对错都执行，常用于释放资源、关闭连接。
- `finally`: Executes no matter what; commonly used to release resources and close connections.

### 11.3 常见内置异常
**11.3 Common Built-in Exceptions**

| 异常 | 触发场景 |
| --- | --- |
| `ValueError` | 类型对但值不合适（如 `int("abc")`） |
| `TypeError` | 操作类型不匹配（如 `"a" + 1`） |
| `FileNotFoundError` | 打开不存在的文件 |
| `IndexError` | 列表下标越界 |
| `KeyError` | 访问字典不存在的键 |
| `ZeroDivisionError` | 除以零 |

| Exception | When it is raised |
| --- | --- |
| `ValueError` | Correct type but unsuitable value (e.g. `int("abc")`) |
| `TypeError` | Operation on mismatched types (e.g. `"a" + 1`) |
| `FileNotFoundError` | Opening a file that does not exist |
| `IndexError` | List index out of range |
| `KeyError` | Accessing a non-existent dictionary key |
| `ZeroDivisionError` | Dividing by zero |

### 11.4 自定义异常
**11.4 Custom Exceptions**

当内置异常不够语义化时，可以自定义：

When the built-in exceptions are not expressive enough, you can define your own:

```python
class AgeError(Exception):
    pass

def set_age(age):
    if age < 0:
        raise AgeError("年龄不能为负数")
    print("年龄设置成功")

try:
    set_age(-1)
except AgeError as e:
    print(e)
```

> 用 `raise` 主动抛出异常，是写"健壮库/函数"的好习惯——把问题及早暴露，而不是带着错误值继续跑。

> Proactively raising exceptions with `raise` is good practice when writing "robust libraries/functions"—surface problems early instead of continuing with wrong values.

### 11.5 异常进阶：自定义异常带参数、断言与异常链
**11.5 Advanced Exceptions: Parameterized Custom Exceptions, Assertions, and Exception Chaining**

**(1) 自定义异常携带信息**：让异常对象本身带上出错的细节，方便排查。

**(1) Custom exceptions carrying information**: Let the exception object itself carry the error details for easier debugging.

```python
class AgeError(Exception):
    def __init__(self, age):
        self.age = age
        super().__init__(f"非法年龄：{age}")   # 把消息传给父类

raise AgeError(200)    # 抛出后 e.age 可取到 200
```

**(2) 断言 `assert`**：用于"程序内部本不该发生的条件"。条件为假时抛 `AssertionError`，常用于开发期自检。

**(2) The `assert` statement**: Used for "conditions that should never happen inside the program." When the condition is false it raises `AssertionError`, commonly used for self-checks during development.

```python
def avg(nums):
    assert len(nums) > 0, "列表不能为空"
    return sum(nums) / len(nums)
```

> ⚠️ **`assert` 不是用来做用户输入校验的**。因为运行 `python -O 脚本.py` 会**关闭所有断言**，到时你的校验就失效了。用户输入、文件读取等"外部不可信"场景，请老老实实用 `if` + `raise`。

> ⚠️ **`assert` is not for validating user input.** Because running `python -O script.py` will **disable all assertions**, your checks would stop working. For "untrusted external" scenarios like user input or file reading, honestly use `if` + `raise`.

**(3) 异常链 `raise ... from`**：当在一处捕获异常、又想抛出另一种异常时，用它保留原始错误，调试时能看清来龙去脉。

**(3) Exception chaining with `raise ... from`**: When you catch an exception in one place but want to raise a different one, use this to preserve the original error so debugging can trace the whole story.

```python
try:
    num = int("abc")
except ValueError as e:
    raise RuntimeError("配置解析失败") from e
```

> ✏️ **小练习**：把 11.4 的 `set_age` 改写：当 `age < 0` 或 `age > 150` 时，抛出带参数的自定义 `AgeError`，并在 `except` 里打印 `e.age` 和报错消息。

> ✏️ **Exercise**: Rewrite the `set_age` from 11.4: when `age < 0` or `age > 150`, raise a parameterized custom `AgeError`, and in `except` print both `e.age` and the error message.

---

