## 第 6 章 控制流：条件判断与循环

**Chapter 6: Control Flow: Conditionals and Loops**

没有控制流，程序就只能从上到下直线执行。有了它，程序才能"看情况办事"（条件判断）和"重复劳动"（循环）。

Without control flow, a program can only run straight from top to bottom. With it, a program can "act according to the situation" (conditionals) and "repeat work" (loops).

![控制流示意](../images/controlflow.svg)

### 6.1 条件判断 if / elif / else

**6.1 Conditionals: if / elif / else**

```python
score = 85

if score >= 90:
    print("优秀")
elif score >= 60:      # else if 的缩写
    print("及格")
else:
    print("不及格")
```

执行逻辑：

Execution logic:

- 先判断 `if` 后的条件，成立就执行它的代码块，然后跳过其余部分。
- First, the condition after `if` is evaluated; if it holds, its block runs and the rest is skipped.
- 不成立就依次看 `elif`，谁成立执行谁。
- If not, each `elif` is checked in turn, and the first one that holds runs.
- 全都落空，才执行 `else`。
- Only when none match does the `else` block run.

条件可以组合，用 `and`（且）、`or`（或）、`not`（非）：

Conditions can be combined using `and` (and), `or` (or), and `not` (not):

```python
if age >= 18 and age < 60:
    print("成年劳动力")
```

### 6.2 for 循环：遍历序列

**6.2 for Loops: Iterating Over Sequences**

`for` 用于"把序列里的每个元素都处理一遍"，**次数通常已知**。

`for` is used to "process every element in a sequence one by one"; **the number of iterations is usually known in advance**.

```python
fruits = ["苹果", "香蕉", "橙子"]
for fruit in fruits:
    print(fruit)

# 配合 range() 生成数字序列
for i in range(5):       # 0,1,2,3,4
    print(i)

for i in range(1, 6):    # 1,2,3,4,5（含头不含尾）
    print(i)

for i in range(0, 10, 2):# 0,2,4,6,8  步长为 2
    print(i)
```

### 6.3 while 循环：条件驱动

**6.3 while Loops: Condition-Driven**

`while` 用于"只要条件成立就一直做"，**次数常未知**。

`while` is used to "keep doing something as long as a condition holds"; **the number of iterations is often unknown**.

```python
count = 0
while count < 5:
    print(count)
    count += 1    # 别忘了让条件最终变为 False，否则死循环！
```

### 6.4 break 与 continue

**6.4 break and continue**

- `break`：**立刻结束整个循环**。
- `break`: **immediately ends the entire loop**.
- `continue`：**跳过本次循环剩余代码，进入下一轮**。
- `continue`: **skips the remaining code of the current iteration and moves to the next one**.

```python
for i in range(10):
    if i == 3:
        continue   # 跳过 3
    if i == 7:
        break      # 到 7 直接结束
    print(i)       # 输出：0 1 2 4 5 6
```

### 6.5 for 与 while 怎么选

**6.5 How to Choose Between for and while**

| 场景 | 推荐 |
| --- | --- |
| 已知要遍历一个列表/字符串/范围 | `for` |
| 次数未知，靠条件控制（如"直到用户输入 q"） | `while` |
| 希望对每个元素做统一处理 | `for`（代码更简洁） |

| Scenario | Recommended |
| --- | --- |
| Need to iterate over a list / string / range | `for` |
| Number of iterations unknown, controlled by a condition (e.g. "until the user enters q") | `while` |
| Want uniform processing for each element | `for` (cleaner code) |

> 经验法则：能写 `for` 就写 `for`，它更不容易出 bug（不用担心漏写计数器导致死循环）。

> Rule of thumb: write a `for` loop whenever you can—it is less prone to bugs (you won't forget a counter and cause an infinite loop).

### 6.6 循环进阶：for-else、enumerate、zip 与实战

**6.6 Loops Advanced: for-else, enumerate, zip, and Practice**

**(1) `for...else`**：循环**正常结束**（没被 `break` 打断）时才执行 `else`，常用于"找了一圈没找到"的场景。

**(1) `for...else`**: the `else` runs only if the loop **finishes normally** (i.e. is not interrupted by `break`). It is commonly used for the "searched everywhere but found nothing" scenario.

```python
for n in range(2, 10):
    if n % 2 == 0:
        print(n, "是偶数")
        break
else:
    print("没有偶数")   # 上面 break 了，所以不会执行
```

**(2) `enumerate`**：遍历时同时拿到「下标 + 元素」，不必自己维护计数器。

**(2) `enumerate`**: get both the **index and the element** while iterating, without maintaining your own counter.

```python
for i, fruit in enumerate(["苹果", "香蕉"], start=1):
    print(i, fruit)     # 1 苹果 / 2 香蕉
```

**(3) `zip`**：把多个序列"按位置配对"一起遍历。

**(3) `zip`**: iterate over multiple sequences "paired by position" together.

```python
names = ["小明", "小红"]
ages  = [18, 20]
for name, age in zip(names, ages):
    print(name, age)    # 小明 18 / 小红 20
```

**(4) 实战：打印九九乘法表**（嵌套 `for` 的经典例子）。

**(4) Practice: printing the multiplication table** (a classic example of nested `for` loops).

```python
for i in range(1, 10):
    for j in range(1, i + 1):
        print(f"{j}×{i}={i*j}", end="\t")   # end="\t" 不换行、用制表符分隔
    print()              # 每行结束换一行
```

> ✏️ **小练习**：用 `for` 配合 `if` 找出 1~100 中所有的质数（质数是只能被 1 和自身整除的数）；提示：可用 `for d in range(2, n)` 试除。

> ✏️ **Exercise**: use `for` together with `if` to find all prime numbers from 1 to 100 (a prime is divisible only by 1 and itself); hint: you can test divisors with `for d in range(2, n)`.

---

