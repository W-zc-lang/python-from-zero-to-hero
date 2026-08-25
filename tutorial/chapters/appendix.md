## 附录：常见错误与调试、推荐资源

**Appendix: Common Errors, Debugging, Recommended Resources**

### A.1 初学者最常犯的 10 个错误

**A.1 The 10 Most Common Beginner Mistakes**

1. **把 `=` 和 `==` 搞混**：`if x = 5` 应为 `if x == 5`。
1. **Mixing up `=` and `==`**: `if x = 5` should be `if x == 5`.
2. **缩进不一致**：混用 Tab 和空格，统一用 4 个空格。
2. **Inconsistent indentation**: mixing tabs and spaces—use 4 spaces consistently.
3. **下标从 0 开始忘**：第一个元素是 `[0]` 不是 `[1]`。
3. **Forgetting indices start at 0**: the first element is `[0]`, not `[1]`.
4. **忘记 `input()` 返回字符串**：做运算前要 `int()` / `float()` 转换。
4. **Forgetting `input()` returns a string**: convert with `int()` / `float()` before calculating.
5. **`range(n)` 不含 n**：`range(5)` 是 0~4。
5. **`range(n)` excludes n**: `range(5)` is 0–4.
6. **修改字符串**：字符串不可变，`s[0] = "a"` 会报错，要用切片或重新赋值。
6. **Modifying a string**: strings are immutable, so `s[0] = "a"` errors—use slicing or reassign.
7. **遍历列表时删除元素**：会导致漏删，应遍历副本或倒序。
7. **Deleting elements while iterating a list**: causes skipped deletions—iterate a copy or go in reverse.
8. **变量名拼错**：Python 区分大小写，`Name` ≠ `name`。
8. **Misspelling variable names**: Python is case-sensitive, `Name` ≠ `name`.
9. **忘记关文件**：用 `with` 语句即可避免。
9. **Forgetting to close files**: use a `with` statement to avoid this.
10. **中文路径/编码乱码**：打开文件指定 `encoding="utf-8"`。
10. **Chinese paths/encoding garble**: specify `encoding="utf-8"` when opening files.

### A.2 读懂报错信息

**A.2 Reading Error Messages**

Python 报错并不可怕，它其实在帮你。一个典型报错：

Python errors aren't scary—they're actually helping you. A typical error:

```
Traceback (most recent call last):
  File "test.py", line 3, in <module>
    print(x)
NameError: name 'x' is not defined
```

- `line 3` 告诉你出错在第 3 行。
- `line 3` tells you the error is on line 3.
- `NameError: name 'x' is not defined` 说明变量 `x` 没定义——通常是拼错或忘了赋值。
- `NameError: name 'x' is not defined` means the variable `x` is not defined—usually a typo or a forgotten assignment.

遇到报错，先搜索报错关键词（如 `NameError python`），十有八九别人也踩过。

When you hit an error, first search its keywords (e.g. `NameError python`)—nine times out of ten someone else has stepped on it too.

### A.3 推荐学习资源

**A.3 Recommended Learning Resources**

- **官方文档**：[docs.python.org/zh-cn](https://docs.python.org/zh-cn/)（权威、有中文）
- **Official docs**: [docs.python.org/zh-cn](https://docs.python.org/zh-cn/) (authoritative, with Chinese)
- **交互练习**：[Python 官方入门教程](https://docs.python.org/zh-cn/3/tutorial/)
- **Interactive practice**: [Official Python tutorial](https://docs.python.org/zh-cn/3/tutorial/)
- **刷题巩固**：LeetCode、牛客网的 Python 入门题
- **Practice problems**: Python beginner problems on LeetCode and Nowcoder
- **项目驱动**：想做什么就做什么，从"自动重命名桌面文件"这种小需求开始
- **Project-driven**: build whatever you want to build, starting with small needs like "auto-rename desktop files"

### A.4 最后的话

**A.4 Final Words**

编程不是"看懂教程"的学问，而是"写出来的"学问。这本书里每一段代码，都请你亲手敲一遍、改一改、故意写错看看报什么错。**写得越多，懂得越透。** 祝你从入门到精通，一路顺畅。

Programming isn't the study of "understanding tutorials," but the study of "writing." For every snippet in this book, please type it out yourself, tweak it, and deliberately write it wrong to see what error appears. **The more you write, the deeper you understand.** May your journey from beginner to master be smooth.

---

> 📘 本文为系统化学习笔记，配套示意图位于 `images/` 目录。欢迎在 GitHub 上 Star、Fork 与指正。

> 📘 This is a systematic study note; the accompanying diagrams live in the `images/` directory. Feel free to Star, Fork, and give feedback on GitHub.
