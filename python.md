# Python: From Absolute Basics to Production

Python from zero, in **levels**: **Basic** (running Python, variables, numbers, strings, decisions, loops) → **Easy** (lists, tuples, dictionaries, sets, comprehensions, functions) → **Moderate** (errors, files, modules and uv, the standard library, classes, dataclasses, type hints, decorators, generators, context managers, regex, Pythonic style, pytest, logging) → **Advanced** (internals, descriptors and metaclasses, threads, processes, free-threading, asyncio, performance, databases, scripting, production tooling, packaging, what's new in 3.12–3.14) → **Interview Prep**. **Each part uses only what earlier parts taught.**

Every section has the same shape: a **picture** where it helps, **theory** in plain words, **Python** examples, **common mistakes**, and **practice** with hidden answers and links. Every example was run on **Python 3.14**, and the text under **Output** is exactly what it printed (a few timing-dependent results are marked as such).

Each part ends with a ✅ **checkpoint**. After this file: `dsa-python.md` for algorithms, `fastapi.md` for web APIs, and `data-science.md` to start the AI/ML track.

## Table of Contents

**[Part 1 — Basic: First Steps](#part-1--basic-first-steps)**

1. [Getting Started: What Python Is and Your First Program](#1-getting-started-what-python-is-and-your-first-program)
2. [Variables: Names for Values](#2-variables-names-for-values)
3. [Numbers, Operators and Type Conversion](#3-numbers-operators-and-type-conversion)
4. [Strings: Working with Text](#4-strings-working-with-text)
5. [Making Decisions: if, elif, else and match](#5-making-decisions-if-elif-else-and-match)
6. [Loops: while, for and range](#6-loops-while-for-and-range)

**[Part 2 — Easy: Collections and Functions](#part-2--easy-collections-and-functions)**

7. [Lists: Ordered, Changeable Collections](#7-lists-ordered-changeable-collections)
8. [Tuples and Unpacking](#8-tuples-and-unpacking)
9. [Dictionaries: Looking Things Up by Key](#9-dictionaries-looking-things-up-by-key)
10. [Sets: Unique Items and Fast Membership](#10-sets-unique-items-and-fast-membership)
11. [Looping Helpers and Comprehensions](#11-looping-helpers-and-comprehensions)
12. [Functions: Reusable Blocks of Code](#12-functions-reusable-blocks-of-code)
13. [Scope, Lambda and Functional Tools (map, filter, sorted, reduce)](#13-scope-lambda-and-functional-tools-map-filter-sorted-reduce)

**[Part 3 — Moderate: Writing Real Programs](#part-3--moderate-writing-real-programs)**

14. [Errors and Exceptions: try, except, raise](#14-errors-and-exceptions-try-except-raise)
15. [Files and Data Formats: pathlib, Text Files, JSON and CSV](#15-files-and-data-formats-pathlib-text-files-json-and-csv)
16. [Modules, Packages, Virtual Environments and uv](#16-modules-packages-virtual-environments-and-uv)
17. [The Standard Library Essentials](#17-the-standard-library-essentials)
18. [Classes and Objects](#18-classes-and-objects)
19. [Inheritance, Composition, Abstract Classes and Protocols](#19-inheritance-composition-abstract-classes-and-protocols)
20. [Special (Dunder) Methods: Making Objects Feel Built-In](#20-special-dunder-methods-making-objects-feel-built-in)
21. [Dataclasses, Enums and __slots__](#21-dataclasses-enums-and-__slots__)
22. [Type Hints and Static Type Checking](#22-type-hints-and-static-type-checking)

**[Part 4 — Moderate: Pythonic Techniques, Testing and Logging](#part-4--moderate-pythonic-techniques-testing-and-logging)**

23. [Closures and Decorators](#23-closures-and-decorators)
24. [Iterators and Generators: Producing Values Lazily](#24-iterators-and-generators-producing-values-lazily)
25. [Context Managers: with, Setup and Clean-Up](#25-context-managers-with-setup-and-clean-up)
26. [Regular Expressions](#26-regular-expressions)
27. [Pythonic Code: Idioms, PEP 8 and Linters](#27-pythonic-code-idioms-pep-8-and-linters)
28. [Testing with pytest](#28-testing-with-pytest)
29. [Logging and Debugging](#29-logging-and-debugging)

**[Part 5 — Advanced: Internals, Concurrency, Performance and Real-World Tools](#part-5--advanced-internals-concurrency-performance-and-real-world-tools)**

30. [How Python Runs: Bytecode, Memory and Garbage Collection](#30-how-python-runs-bytecode-memory-and-garbage-collection)
31. [Advanced Classes: Attribute Lookup, Descriptors, Class Hooks and Metaclasses](#31-advanced-classes-attribute-lookup-descriptors-class-hooks-and-metaclasses)
32. [Concurrency: Threads, Processes, the GIL and Free-Threaded Python](#32-concurrency-threads-processes-the-gil-and-free-threaded-python)
33. [asyncio: async and await](#33-asyncio-async-and-await)
34. [Performance: Measuring and Speeding Up Python](#34-performance-measuring-and-speeding-up-python)
35. [Working with Databases: sqlite3, psycopg and SQLAlchemy](#35-working-with-databases-sqlite3-psycopg-and-sqlalchemy)
36. [Scripting and Automation: CLIs, subprocess, Files and Scheduling](#36-scripting-and-automation-clis-subprocess-files-and-scheduling)

**[Part 6 — Advanced: Production Python](#part-6--advanced-production-python)**

37. [Production-Grade Python: Project Layout, Configuration, Tooling and CI](#37-production-grade-python-project-layout-configuration-tooling-and-ci)
38. [Packaging and Publishing a Library](#38-packaging-and-publishing-a-library)
39. [What's New in Python 3.12, 3.13 and 3.14](#39-whats-new-in-python-312-313-and-314)

**[Part 7 — Interview Prep: Revision](#part-7--interview-prep-revision)**

40. [Python's Toolbox for Data Structures and Algorithms](#40-pythons-toolbox-for-data-structures-and-algorithms)
41. [Interview Coding: Classic Python Problems](#41-interview-coding-classic-python-problems)
42. [Output-Based Questions (Predict the Output)](#42-output-based-questions-predict-the-output)
43. [Python Cheat Sheet](#43-python-cheat-sheet)
44. [Most Asked Python Interview Questions](#44-most-asked-python-interview-questions)

---

# Part 1 — Basic: First Steps

> **Goal:** Run Python, store values in variables, work with numbers and text, make decisions and repeat work with loops.  
> **You need:** Nothing: this is the very beginning.

---

## 1. Getting Started: What Python Is and Your First Program

![The learning path](images/python/00-roadmap.svg)

### Theory

> **In simple words:** a program is a list of instructions for a computer. **Python** is a language for writing those instructions that reads almost like English: `print("Hello")` prints Hello. It's the most popular programming language in the world in 2026, used for automation scripts, websites and APIs (Django, FastAPI), data analysis (pandas), machine learning and AI (PyTorch, LLM apps), testing, and teaching. It's a great first language because you can do useful things quickly, and it's also a serious professional tool.

**How these notes are organised:**

| Part | Level | You learn |
|---|---|---|
| 1 | Basic | Running Python, variables, numbers, strings, decisions, loops |
| 2 | Easy | Lists, tuples, dictionaries, sets, comprehensions, functions |
| 3 | Moderate | Errors, files, modules and packages, the standard library, classes and objects, type hints |
| 4 | Moderate | Decorators, generators, context managers, regular expressions, Pythonic style, testing, logging |
| 5 | Advanced | How Python runs, advanced classes, concurrency (threads, processes, free-threading), asyncio, performance, databases, scripting |
| 6 | Advanced | Production Python: project layout, tooling, packaging, and what's new in Python 3.12–3.14 |
| 7 | Interview Prep | Coding problems, output questions, cheat sheet, most-asked questions |

**How to use them:** read a section, **type the examples yourself** (don't copy-paste), change them and see what happens, then do the practice question before opening the answer. Every example was run on **Python 3.14**, and the text under **Output** is exactly what it printed. Each part ends with a ✅ **checkpoint**: if you can do everything on it without looking, move on.

**Installing Python (2026):**

- **Windows / macOS:** download from [python.org](https://www.python.org/downloads/) (tick "Add python.exe to PATH" on Windows), or use `uv` (below).
- **Linux:** usually preinstalled as `python3`; install a newer one with your package manager or `uv`.
- **The modern way on any OS:** install **uv** (a fast Python project manager) and run `uv python install 3.14`. Section [16](#16-modules-packages-virtual-environments-and-uv) explains uv properly.

Check it works in a terminal: `python --version` (or `python3 --version` on macOS/Linux) should print something like `Python 3.14.7`.

**Two ways to run Python:**

| Way | How | Good for |
|---|---|---|
| **Interactive (REPL)** | Type `python` in a terminal; you get a `>>>` prompt; each line runs immediately. `exit()` to leave | Trying things out, quick calculations |
| **Script file** | Save code in `hello.py`, run `python hello.py` | Real programs you keep and rerun |

An **editor** makes life easier: VS Code (with the Python extension), PyCharm, or Cursor. Jupyter notebooks are popular for data work (`data-science.md`).

**The basic building blocks you'll use from day one:**

- `print(...)` shows values on the screen.
- `input("prompt")` waits for the user to type a line and gives it back as **text**.
- `#` starts a **comment**: text for humans that Python ignores.
- **Indentation** (spaces at the start of a line) is part of the language: it shows which lines belong together (Section [5](#5-making-decisions-if-elif-else-and-match)). Use 4 spaces.
- Python runs a file **top to bottom**, one line at a time, and stops at the first error, telling you the line and the kind of error.

### Python

```python
# My first program: everything after # is a comment
print("Hello, world!")
print("Python", "is", "fun")          # several values: separated by spaces
print("a", "b", "c", sep="-")          # choose the separator
print("no newline here", end=" ")      # choose what goes at the end (default is a newline)
print("-> continued")
print(2 + 3, 10 / 4, 7 * 6)            # Python is also a calculator
```

**Output:**

```text
Hello, world!
Python is fun
a-b-c
no newline here -> continued
5 2.5 42
```

`input()` pauses the program and waits for the user, so it can't show output here; this is what a run looks like when the user types `Asha`:

<!-- no-run (waits for keyboard input) -->
```python
name = input("What's your name? ")     # the user types: Asha
print("Nice to meet you,", name)
```

```text
What's your name? Asha
Nice to meet you, Asha
```

**Errors are normal.** Everybody sees them all day; the skill is reading them. Python prints a **traceback**: the file and line, then the error **type** and a message on the last line. Read the last line first.

```python
import traceback

try:
    exec('print("Hello"')                   # a missing closing bracket
except SyntaxError as e:
    print(type(e).__name__, "-", e.msg)

try:
    print(score)                            # a name that was never created
except NameError as e:
    print(type(e).__name__, "-", e)
```

**Output:**

```text
SyntaxError - '(' was never closed
NameError - name 'score' is not defined
```

(`try`/`except`, used here to catch the errors and keep going, is taught in Section [14](#14-errors-and-exceptions-try-except-raise); for now just read the messages.) Python 3.14's messages even suggest fixes, like "Did you mean…?" for misspelled names.

| Error | Usually means |
|---|---|
| `SyntaxError` | The code isn't valid Python: a missing bracket, quote or colon |
| `IndentationError` | Spaces at the start of lines don't line up |
| `NameError` | You used a name that doesn't exist (typo, or not created yet) |
| `TypeError` | Wrong type for an operation, like `"5" + 3` |
| `ValueError` | Right type, bad value, like `int("abc")` |

**Getting help:** `help(print)` in the REPL shows documentation; `dir("text")` lists what you can do with a value; and the official [Python tutorial](https://docs.python.org/3/tutorial/) is excellent.

**Common mistakes:**

- ❌ Typing `python hello.py` inside the `>>>` REPL (that's a terminal command; exit the REPL first).
- ❌ Mixing tabs and spaces for indentation (configure your editor to insert 4 spaces).
- ❌ Smart quotes “ ” pasted from documents instead of plain quotes `"`.
- ❌ Ignoring the error message; the last line of the traceback usually tells you exactly what's wrong.

### Practice

1. Write a program that prints your name, then your city on the same line separated by ` | `, then the result of 365 × 24 (hours in a year).

<details>
<summary><b>Answer</b></summary>

```python
print("Asha", "Pune", sep=" | ")
print(365 * 24)
```

**Output:**

```text
Asha | Pune
8760
```

</details>

**Learn more:** [The official Python tutorial](https://docs.python.org/3/tutorial/) · [What's new in Python 3.14](https://docs.python.org/3/whatsnew/3.14.html) · [uv documentation](https://docs.astral.sh/uv/)

---

## 2. Variables: Names for Values

### Theory

> **In simple words:** a **variable** is a **name** you give to a value so you can use it later. `age = 25` means "from now on, the name `age` refers to 25". Think of a sticky note with a name on it, stuck onto a value. You can move the sticky note to another value at any time (`age = 26`), and you can stick two notes onto the same value.

**Creating and changing variables:** `name = value`. The `=` means "assign" (make the name refer to the value), not "equals" in the maths sense. Python works out the right side first, then sticks the name on the result, which is why `count = count + 1` makes sense.

**Naming rules:**

- Letters, digits and underscores; can't **start** with a digit (`user1` ✅, `1user` ❌).
- **Case-sensitive:** `age`, `Age` and `AGE` are three different names.
- Can't be a **keyword** (`if`, `for`, `class`, `def`, `True`, `None`, `import`, `return`, …).
- Style (PEP 8): `snake_case` for variables and functions (`total_price`), `UPPER_CASE` for constants (`MAX_USERS = 100`), `PascalCase` for classes.
- Use meaningful names: `total_price`, not `tp` or `x`.

**Dynamic typing:** you never declare a type; the **value** has a type, and a name can later point to a value of another type (allowed, but confusing; avoid it). `type(value)` tells you the type.

**Going deeper: names and objects.** Every value in Python is an **object** with an identity (`id()`), a type and a value. A variable holds a **reference** to an object; assigning one variable to another **doesn't copy** the object, it makes both names refer to the same one. This matters once values can change (lists, Section [7](#7-lists-ordered-changeable-collections)): `b = a` then changing `a`'s list changes what `b` sees too. `==` asks "equal values?", `is` asks "the very same object?" (use `is` only for `None`, `True`, `False`).

### Python

```python
name = "Asha"             # text: a string (str)
age = 25                  # a whole number: an integer (int)
height = 1.62             # a decimal number: a float
is_student = True         # True or False: a boolean (bool)
print(name, age, height, is_student)
print(type(name), type(age), type(height), type(is_student))

age = age + 1             # right side first (25 + 1), then the name moves to 26
age += 1                  # shortcut for age = age + 1
print("age is now", age)

x, y, z = 1, 2, 3         # several names at once
a = b = 0                 # two names, same value
x, y = y, x               # swap without a temporary variable
print(x, y, z, a, b)
```

**Output:**

```text
Asha 25 1.62 True
<class 'str'> <class 'int'> <class 'float'> <class 'bool'>
age is now 27
2 1 3 0 0
```

Names are labels on objects, not boxes holding copies:

```python
scores = [90, 85]             # a list (Part 2): a value that can change
backup = scores               # NOT a copy: a second label on the same list
scores.append(70)             # change the list through one name...
print(backup)                 # ...and the other name sees it
print(backup is scores, id(backup) == id(scores))

real_copy = list(scores)      # a new, separate list
real_copy.append(100)
print(scores, real_copy, real_copy == scores, real_copy is scores)
```

**Output:**

```text
[90, 85, 70]
True True
[90, 85, 70] [90, 85, 70, 100] False False
```

**Common mistakes:**

- ❌ `2nd_place = "A"` or `class = "10A"` (starts with a digit / is a keyword: `SyntaxError`).
- ❌ Thinking `b = a` copies a list: both names share one list.
- ❌ Using `is` to compare numbers or strings (`x is 1000`); use `==`. Keep `is` for `None`.
- ❌ Reusing one name for different kinds of things (`data = "5"` then `data = 5`).
- ❌ Shadowing built-in names like `list = [1, 2]` or `str = "x"`: you lose the built-in `list()`/`str()` for the rest of the file.

### Practice

1. Create `price = 499` and `quantity = 3`, compute `total`, then apply a 10% discount by updating `total` with `*=`. Print both values.

<details>
<summary><b>Answer</b></summary>

```python
price = 499
quantity = 3
total = price * quantity
print("before discount:", total)
total *= 0.9
print("after discount:", total)
```

**Output:**

```text
before discount: 1497
after discount: 1347.3
```

</details>

**Learn more:** [Python tutorial: an informal introduction](https://docs.python.org/3/tutorial/introduction.html) · [Ned Batchelder: facts and myths about Python names and values](https://nedbatchelder.com/text/names.html)

---

## 3. Numbers, Operators and Type Conversion

### Theory

> **In simple words:** Python has two main kinds of numbers: **integers** (`int`, whole numbers like 7 or -3, as big as you like) and **floats** (`float`, numbers with a decimal point like 2.5). **Operators** are the symbols that do things with values: `+ - * /` for arithmetic, `==` and `<` for comparing, `and`/`or`/`not` for combining true/false. **Type conversion** changes a value from one type to another, like turning the text `"42"` typed by a user into the number `42`.

**Arithmetic operators:**

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `+ - *` | add, subtract, multiply | `7 * 3` | `21` |
| `/` | divide (always gives a float) | `7 / 2` | `3.5` |
| `//` | floor division (round down to a whole number) | `7 // 2` | `3` |
| `%` | remainder (modulo) | `7 % 2` | `1` |
| `**` | power | `2 ** 10` | `1024` |

**Order (precedence)** is like school maths: `**` first, then `* / // %`, then `+ -`. Use brackets to make it obvious: `(a + b) * c`.

**Comparison operators** give `True` or `False`: `==` equal, `!=` not equal, `< <= > >=`. They can be **chained**: `0 <= score <= 100`.

**Logical operators:** `and` (both true), `or` (at least one true), `not` (flip). They **short-circuit**: in `a and b`, if `a` is false, `b` isn't even evaluated.

**Assignment shortcuts:** `x += 1`, `x -= 2`, `x *= 3`, `x /= 4`, `x //= 2`, `x %= 5`, `x **= 2`.

**Modules:** `import math` makes Python's `math` toolbox available (`math.sqrt`, `math.pi`, `math.isclose`). Modules are explained in Part 3; for now, `import name` at the top is all you need.

**Floats are approximate.** Computers store floats in binary, so `0.1 + 0.2` is `0.30000000000000004`. Never compare floats with `==`; use `math.isclose`, and use `decimal.Decimal` for money (or store paise/cents as integers).

**Type conversion:** `int("42")`, `float("3.5")`, `str(99)`, `bool(0)`. `int(3.9)` cuts off the decimals (→ 3); `round(3.5)` rounds to the nearest **even** number on ties (→ 4, and `round(2.5)` → 2, "banker's rounding"). Converting text that isn't a number raises `ValueError`.

**Truthiness:** in an `if` or `while`, every value counts as true or false. **False-y** values: `False`, `None`, `0`, `0.0`, `""` (empty string), and empty collections (`[]`, `{}`, `()`, `set()`). Everything else is truthy.

**Other number types:** `complex` (`3 + 4j`), `decimal.Decimal` (exact decimals), `fractions.Fraction` (exact fractions). Big integers just work: `2 ** 100` is exact. Underscores make long numbers readable: `1_000_000`.

### Python

```python
print(7 / 2, 7 // 2, 7 % 2, 2 ** 10)
print(-7 // 2, -7 % 2)                 # floor division rounds DOWN (towards minus infinity)
print(2 + 3 * 4, (2 + 3) * 4)           # precedence
print(2 ** 100)                        # integers have no size limit
print(1_000_000 * 3)

print(0.1 + 0.2, 0.1 + 0.2 == 0.3)     # floats are approximate
import math
print(math.isclose(0.1 + 0.2, 0.3))
from decimal import Decimal
print(Decimal("0.1") + Decimal("0.2"))  # exact decimal arithmetic for money

score = 72
print(score >= 50, score == 100, 0 <= score <= 100)
print(score > 50 and score < 60, score < 50 or score > 70, not score > 50)
```

**Output:**

```text
3.5 3 1 1024
-4 1
14 20
1267650600228229401496703205376
3000000
0.30000000000000004 False
True
0.3
True False True
False True False
```

```python
print(int("42") + 1, float("3.5") * 2, str(99) + "!")
print(int(3.9), round(3.9), round(3.5), round(2.5), round(3.14159, 2))
print(bool(0), bool(7), bool(""), bool("hi"), bool([]), bool([0]))

try:
    int("forty-two")
except ValueError as e:
    print("ValueError:", e)

print("5" * 3)                         # repetition, not maths!
try:
    print("5" + 3)
except TypeError as e:
    print("TypeError:", e)
print(int("5") + 3)
```

**Output:**

```text
43 7.0 99!
3 4 4 2 3.14
False True False True False True
ValueError: invalid literal for int() with base 10: 'forty-two'
555
TypeError: can only concatenate str (not "int") to str
8
```

**Common mistakes:**

- ❌ Forgetting that `input()` returns text: `input() + 1` fails; convert with `int(...)`.
- ❌ Comparing floats with `==`; use `math.isclose` or `Decimal`.
- ❌ Expecting `/` to give an integer (`6 / 3` is `2.0`); use `//` when you want whole numbers.
- ❌ Writing `if x == True:`; just write `if x:`.
- ❌ Using `=` (assign) where you meant `==` (compare).

### Practice

1. A bill of ₹1,234 is split between 5 friends. Print how much each pays in whole rupees (rounded down) and how many rupees are left over. Then convert 98.6 °F to °C (`(f - 32) * 5 / 9`), rounded to 1 decimal.

<details>
<summary><b>Answer</b></summary>

```python
bill, friends = 1234, 5
print("each pays", bill // friends, "and", bill % friends, "rupees are left over")
f = 98.6
print(round((f - 32) * 5 / 9, 1), "°C")
```

**Output:**

```text
each pays 246 and 4 rupees are left over
37.0 °C
```

</details>

**Learn more:** [Python docs: numeric types](https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex) · [Floating-point arithmetic: issues and limitations](https://docs.python.org/3/tutorial/floatingpoint.html)

---

## 4. Strings: Working with Text

### Theory

> **In simple words:** a **string** (`str`) is a piece of text: a sequence of characters inside quotes, like `"hello"` or `'Pune'`. You can glue strings together, repeat them, pick out single characters or pieces, search inside them, and change their case. Strings are **immutable**: every "change" creates a **new** string; the original never changes.

**Creating strings:** single or double quotes are the same (`'hi'` == `"hi"`); triple quotes (`"""..."""`) span several lines. **Escape sequences** start with a backslash: `\n` newline, `\t` tab, `\\` a backslash, `\"` a quote. A **raw string** `r"C:\new"` keeps backslashes as they are (handy for Windows paths and regular expressions).

**Indexing and slicing:** characters are numbered from **0**. `s[0]` is the first, `s[-1]` the last. `s[start:stop]` takes a slice from `start` up to **but not including** `stop`; `s[::-1]` reverses. Going past the end with an index is an error; with a slice it's fine.

**f-strings** (the modern way to build text): `f"Hello {name}, you are {age} years old"`. Inside `{}` you can put any expression and a **format spec** after a colon: `{price:.2f}` (2 decimals), `{n:,}` (thousands separators), `{x:>8}` (right-align in 8 characters), `{ratio:.1%}` (percentage). `{value=}` prints the name and value, great for debugging.

**Useful methods** (each returns a new string):

| Method | Does |
|---|---|
| `upper()`, `lower()`, `title()`, `capitalize()` | Change case |
| `strip()`, `lstrip()`, `rstrip()` | Remove spaces (or given characters) at the ends |
| `split(sep)`, `sep.join(items)` | Text → list of pieces, and back |
| `replace(old, new)` | Replace all occurrences |
| `find(sub)` (-1 if missing), `index(sub)` (error if missing), `count(sub)` | Search |
| `startswith()`, `endswith()`, `in` | Check |
| `isdigit()`, `isalpha()`, `isalnum()`, `isspace()` | Test character types |
| `removeprefix()`, `removesuffix()` | Remove a known start/end |
| `zfill()`, `center()`, `ljust()`, `rjust()` | Pad |

**Unicode:** Python strings are Unicode, so Hindi, emoji and any language work: `len("नमस्ते")` counts code points (which can differ from what a reader sees as "letters"). Text that travels over networks or into files is **bytes**; convert with `.encode("utf-8")` and `.decode("utf-8")`.

**Building long strings:** `+=` in a big loop creates a new string each time; collect pieces in a list (Part 2) and `"".join(pieces)` once at the end.

### Python

```python
city = "Bengaluru"
print(len(city), city[0], city[-1], city[0:4], city[4:], city[::-1])
print(city.upper(), city.lower(), "  padded  ".strip() + "|")
print("pune,delhi,goa".split(","), " + ".join(["a", "b", "c"]))
print("banana".count("a"), "banana".find("n"), "banana".find("z"), "nan" in "banana")
print("Order #90312".removeprefix("Order #"), "report.pdf".endswith(".pdf"), "2026".isdigit())
print("Hello" + " " + "world", "ab" * 3)
print("Line one\nLine two\tafter a tab")
print(r"C:\new\table", len("नमस्ते"), "café".encode("utf-8"))

try:
    city[0] = "b"                          # strings are immutable
except TypeError as e:
    print("TypeError:", e)
```

**Output:**

```text
9 B u Beng aluru urulagneB
BENGALURU bengaluru padded|
['pune', 'delhi', 'goa'] a + b + c
3 2 -1 True
90312 True True
Hello world ababab
Line one
Line two	after a tab
C:\new\table 6 b'caf\xc3\xa9'
TypeError: 'str' object does not support item assignment
```

```python
name, price, qty, ratio = "Asha", 1499.5, 12000, 0.4567
print(f"{name} bought {qty:,} items at ₹{price:.2f} ({ratio:.1%} of budget)")
print(f"[{name:>8}] [{name:<8}] [{name:^8}] [{7:03d}]")
print(f"{price * 2 = }")                    # debugging: shows the expression and its value
width = 10
print(f"{'total':<{width}}|{price:>{width},.1f}")

```

**Output:**

```text
Asha bought 12,000 items at ₹1499.50 (45.7% of budget)
[    Asha] [Asha    ] [  Asha  ] [007]
price * 2 = 2999.0
total     |   1,499.5
```

**Common mistakes:**

- ❌ Expecting `s.upper()` to change `s`: strings never change; write `s = s.upper()`.
- ❌ Off-by-one slices: `s[0:3]` is 3 characters (indexes 0, 1, 2).
- ❌ `"Total: " + 5` (TypeError); use an f-string: `f"Total: {5}"`.
- ❌ Windows paths like `"C:\new"` where `\n` becomes a newline; use raw strings or `pathlib`.
- ❌ Building huge strings with `+=` in loops instead of `"".join(...)`.

### Practice

1. Given `email = "  Asha.Rao@Example.COM "`, print the cleaned lower-case email, the username (before `@`), and the domain (after `@`). Then print the username with the first letter of each part capitalised ("Asha.Rao" → "Asha Rao").

<details>
<summary><b>Answer</b></summary>

```python
email = "  Asha.Rao@Example.COM "
clean = email.strip().lower()
user, domain = clean.split("@")
print(clean, user, domain)
print(user.replace(".", " ").title())
```

**Output:**

```text
asha.rao@example.com asha.rao example.com
Asha Rao
```

</details>

**Learn more:** [Python docs: string methods](https://docs.python.org/3/library/stdtypes.html#string-methods) · [Format specification mini-language](https://docs.python.org/3/library/string.html#formatspec) · [fstring.help cheat sheet](https://fstring.help/cheat/)

---

## 5. Making Decisions: if, elif, else and match

### Theory

> **In simple words:** programs need to choose: *if* the password is right, log in; *otherwise*, show an error. `if` runs a block of code only when a condition is true; `elif` ("else if") checks another condition when the earlier ones were false; `else` catches everything left. The block that belongs to each branch is the **indented** lines under it.

**The shape:**

```text
if condition:
    lines that run when condition is true      ← indented 4 spaces
elif another_condition:
    lines that run when the first was false and this is true
else:
    lines that run when nothing above was true
next line (not indented) runs in every case
```

Only **one** branch runs: the first whose condition is true. The colon `:` at the end of the `if` line and the indentation are required.

**Conditions** are any expression: comparisons (`age >= 18`), combinations (`age >= 18 and has_id`), or any value using truthiness (`if name:` is true for non-empty text, Section [3](#3-numbers-operators-and-type-conversion)).

**Nested ifs** (an `if` inside another) work, but more than two levels get hard to read: combine conditions with `and`, or return early (functions, Part 2).

**Conditional expression** (one-line if): `status = "adult" if age >= 18 else "minor"`. Good for simple choices between two values; don't nest them.

**`match` (structural pattern matching, Python 3.10+)** compares one value against several **patterns**, like a switch statement but more powerful: it can match literal values, several alternatives with `|`, and conditions with `if` guards; `case _:` is the default. Later you'll see it also unpacks lists, dictionaries and objects (Part 2 and Part 3).

**`pass`** is a placeholder statement that does nothing, for a branch you'll fill in later.

### Python

```python
def grade(score):                     # functions come in Part 2; here it just lets us try several scores
    if score >= 90:
        return "A"
    elif score >= 75:
        return "B"
    elif score >= 50:
        return "C"
    else:
        return "fail"

print(grade(95), grade(80), grade(75), grade(49))

age, has_ticket = 17, True
if age >= 18 and has_ticket:
    print("enter")
elif has_ticket:
    print("enter with an adult")
else:
    print("buy a ticket first")

status = "adult" if age >= 18 else "minor"
print(status)

name = ""
if not name:                          # empty string is false-y
    print("name is missing")
```

**Output:**

```text
A B B fail
enter with an adult
minor
name is missing
```

(`def` defines a reusable function and `return` gives back a value; Part 2 covers them fully. Here they just let us test four scores in one go.)

```python
def http_message(code):
    match code:
        case 200:
            return "OK"
        case 301 | 302:
            return "Redirect"
        case 404:
            return "Not found"
        case n if 500 <= n <= 599:        # a guard: extra condition
            return "Server error"
        case _:                            # default
            return "Unknown"

print(http_message(200), http_message(302), http_message(404), http_message(503), http_message(999))
```

**Output:**

```text
OK Redirect Not found Server error Unknown
```

**Common mistakes:**

- ❌ Forgetting the `:` or the indentation (`SyntaxError`/`IndentationError`).
- ❌ Ordering conditions badly: `if score >= 50` before `if score >= 90` means 95 gets a C.
- ❌ `if x = 5:` (assignment) instead of `if x == 5:`.
- ❌ `if colour == "red" or "blue":` is always true (`"blue"` is truthy on its own); write `colour in ("red", "blue")` or `colour == "red" or colour == "blue"`.
- ❌ Deep nesting; combine conditions or return early.

### Practice

1. Write `ticket_price(age)` returning 0 for under 3, 100 for 3–12, 250 for 13–59 and 150 for 60 and over. Print it for ages 2, 12, 30 and 65.

<details>
<summary><b>Answer</b></summary>

```python
def ticket_price(age):
    if age < 3:
        return 0
    elif age <= 12:
        return 100
    elif age < 60:
        return 250
    else:
        return 150

print(ticket_price(2), ticket_price(12), ticket_price(30), ticket_price(65))
```

**Output:**

```text
0 100 250 150
```

</details>

**Learn more:** [Python tutorial: if statements](https://docs.python.org/3/tutorial/controlflow.html#if-statements) · [PEP 636: structural pattern matching tutorial](https://peps.python.org/pep-0636/)

---

## 6. Loops: while, for and range

### Theory

> **In simple words:** a **loop** repeats a block of code. A **`while` loop** repeats **as long as** a condition is true ("keep asking until the password is right"). A **`for` loop** repeats **once for each item** in a sequence ("for each character in this word", "for each number from 1 to 10"). Loops are how programs do a lot of work with a little code.

**`while condition:`** checks the condition, runs the block, checks again, and so on. Something inside must eventually make the condition false, or the loop runs forever (press Ctrl+C to stop a stuck program).

**`for item in sequence:`** takes each item in turn. Sequences you know so far: strings (each character) and **`range`**:

| Call | Produces |
|---|---|
| `range(5)` | 0, 1, 2, 3, 4 (starts at 0, stops **before** 5) |
| `range(2, 6)` | 2, 3, 4, 5 |
| `range(0, 20, 5)` | 0, 5, 10, 15 (a step of 5) |
| `range(10, 0, -3)` | 10, 7, 4, 1 (counting down) |

**Controlling loops:**

- `break` leaves the loop immediately.
- `continue` skips the rest of this round and goes to the next.
- `else` on a loop runs only if the loop finished **without** `break` (useful for "searched everything, didn't find it").

**Nested loops** (a loop inside a loop) handle two dimensions: rows and columns, every pair of items. The inner loop runs completely for each round of the outer loop, so 10 × 10 rounds = 100 runs: nested loops get slow quickly (`dsa-python.md` covers this as time complexity).

**Accumulator pattern:** start a variable before the loop (`total = 0`), update it inside (`total += x`), use it after. Almost every loop you'll write is a variation of this: counting, summing, finding the maximum, building a string.

**Which loop?** Use `for` when you know what you're looping over (a range, a string, later a list). Use `while` when you loop until something happens (user input, a condition changes).

### Python

```python
count = 3
while count > 0:                      # runs while the condition is true
    print("countdown", count)
    count -= 1                        # without this, the loop never ends
print("lift-off!")

for letter in "Pune":
    print(letter, end=" ")
print()

for i in range(1, 6):
    print(i, "squared is", i ** 2)

total = 0
for n in range(1, 101):               # accumulator: sum of 1..100
    total += n
print("sum 1..100 =", total)
```

**Output:**

```text
countdown 3
countdown 2
countdown 1
lift-off!
P u n e 
1 squared is 1
2 squared is 4
3 squared is 9
4 squared is 16
5 squared is 25
sum 1..100 = 5050
```

```python
for n in range(1, 20):
    if n % 2 == 0:
        continue                      # skip even numbers
    if n > 9:
        break                         # stop completely after 9
    print(n, end=" ")
print()

word = "python"
for ch in word:
    if ch in "aeiou":
        print("first vowel:", ch)
        break
else:                                 # runs only if the loop did NOT break
    print("no vowels")

for row in range(1, 4):               # nested loops: a small times table
    line = ""
    for col in range(1, 5):
        line += f"{row * col:4}"
    print(line)

for size in range(1, 5):              # a pattern: a staircase of stars
    print("*" * size)
```

**Output:**

```text
1 3 5 7 9 
first vowel: o
   1   2   3   4
   2   4   6   8
   3   6   9  12
*
**
***
****
```

**Common mistakes:**

- ❌ Infinite `while` loops (the condition never becomes false).
- ❌ Off-by-one: `range(1, 10)` stops at 9; use `range(1, 11)` for 1..10.
- ❌ Changing the loop variable inside a `for` to skip items (it's reset each round); use `continue`.
- ❌ Misunderstanding loop `else` (it's "no break", not "if the loop didn't run").
- ❌ Starting the accumulator inside the loop, so it resets every round.

### Practice

1. Print the numbers 1 to 20, but print "Fizz" for multiples of 3, "Buzz" for multiples of 5 and "FizzBuzz" for multiples of both (on one line, separated by spaces).
2. Count how many digits are in the number 9_876_543_210 using a `while` loop (keep dividing by 10).

<details>
<summary><b>Answer</b></summary>

```python
for n in range(1, 21):
    if n % 15 == 0:
        print("FizzBuzz", end=" ")
    elif n % 3 == 0:
        print("Fizz", end=" ")
    elif n % 5 == 0:
        print("Buzz", end=" ")
    else:
        print(n, end=" ")
print()

n, digits = 9_876_543_210, 0
while n > 0:
    n //= 10
    digits += 1
print(digits, "digits")
```

**Output:**

```text
1 2 Fizz 4 Buzz Fizz 7 8 Fizz Buzz 11 Fizz 13 14 FizzBuzz 16 17 Fizz 19 Buzz 
10 digits
```

Checking 15 **first** matters: a multiple of 15 is also a multiple of 3, and only the first true branch runs.

</details>

---

### ✅ Part 1 checkpoint

Without looking, can you:

- [ ] Run Python in the REPL and as a script, and read an error message?
- [ ] Create variables, explain that names refer to objects, and convert between types?
- [ ] Use arithmetic (including `//`, `%`, `**`), comparisons, and `and`/`or`/`not`, and explain why `0.1 + 0.2 != 0.3`?
- [ ] Slice strings, use common string methods, and format output with f-strings?
- [ ] Write `if`/`elif`/`else` and `match`, and `while`/`for` loops with `range`, `break`, `continue`?

**Learn more:** [Python tutorial: for statements and range](https://docs.python.org/3/tutorial/controlflow.html#for-statements) · [Python tutorial: break, continue and else on loops](https://docs.python.org/3/tutorial/controlflow.html#break-and-continue-statements-and-else-clauses-on-loops)

---

# Part 2 — Easy: Collections and Functions

> **Goal:** Organise data with lists, tuples, dictionaries and sets, write comprehensions, and package logic into functions.  
> **You need:** Part 1.

---

## 7. Lists: Ordered, Changeable Collections

![A list stores references in numbered slots; indexes count from 0 at the front and from -1 at the back; slicing takes a range; appending is fast, inserting at the front shifts everything](images/python/01-list.svg)

### Theory

> **In simple words:** a **list** holds many values in order, inside square brackets: `scores = [90, 72, 85]`. You can add items, remove them, change them, sort them and loop over them. It's the collection you'll use most. Unlike strings, lists are **mutable**: you change the list itself, and every name that refers to it sees the change.

**Basics:** `len(items)`, indexing `items[0]`, `items[-1]`, slicing `items[1:3]` (same rules as strings), `x in items`. Items can be of any type, even mixed or other lists (`[[1, 2], [3, 4]]` is a grid).

**Changing a list (these modify it in place and return `None`):**

| Method | Does | Speed |
|---|---|---|
| `append(x)` | Add at the end | Fast (O(1)) |
| `extend(other)` / `+=` | Add many at the end | Proportional to the added items |
| `insert(i, x)` | Add at position i | Slow for big lists: shifts everything after i (O(n)) |
| `pop()` / `pop(i)` | Remove and return the last / item i | Last: fast; front: slow |
| `remove(x)` | Remove the first item equal to x | O(n) |
| `items[i] = x`, `del items[i]` | Replace / delete by position | |
| `sort()`, `reverse()` | Sort / reverse in place | |
| `clear()` | Empty it | |

**Not changing it:** `sorted(items)` returns a **new** sorted list; `items.index(x)`, `items.count(x)`, `min`, `max`, `sum`.

**Sorting with a key:** `sorted(words, key=len)` sorts by length; `reverse=True` for descending. The key is a function applied to each item (`key=str.lower` for case-insensitive). Python's sort is **stable**: equal items keep their original order, so you can sort by a second criterion first and the main one second.

**Copies:** `b = a` shares one list (Section [2](#2-variables-names-for-values)). `a.copy()`, `list(a)` or `a[:]` make a **shallow copy**: a new outer list, but inner lists are still shared. For nested lists use `copy.deepcopy(a)`.

**How lists work inside:** a list is an array of references with spare room at the end, so reading `items[i]` and `append` are fast, while inserting or deleting at the front moves every other element. If you need fast adds/removes at both ends, use `collections.deque` (Section [17](#17-the-standard-library-essentials)).

### Python

```python
fruits = ["apple", "banana", "cherry"]
fruits.append("mango")
fruits.insert(0, "kiwi")
print(fruits, len(fruits), fruits[0], fruits[-1], fruits[1:3])
fruits.remove("banana")
last = fruits.pop()
print(fruits, "popped:", last, "| 'kiwi' in fruits:", "kiwi" in fruits)
fruits[0] = "grape"
print(fruits)

nums = [5, 2, 9, 1, 7]
print(sorted(nums), nums)                  # sorted() gives a new list, nums is unchanged
nums.sort(reverse=True)                    # sort() changes nums itself and returns None
print(nums, sum(nums), min(nums), max(nums))
result = nums.sort()
print(result)                              # a classic trap

words = ["pear", "Fig", "banana", "apple", "kiwi"]
print(sorted(words), sorted(words, key=str.lower), sorted(words, key=len))
```

**Output:**

```text
['kiwi', 'apple', 'banana', 'cherry', 'mango'] 5 kiwi mango ['apple', 'banana']
['kiwi', 'apple', 'cherry'] popped: mango | 'kiwi' in fruits: True
['grape', 'apple', 'cherry']
[1, 2, 5, 7, 9] [5, 2, 9, 1, 7]
[9, 7, 5, 2, 1] 24 1 9
None
['Fig', 'apple', 'banana', 'kiwi', 'pear'] ['apple', 'banana', 'Fig', 'kiwi', 'pear'] ['Fig', 'pear', 'kiwi', 'apple', 'banana']
```

```python
import copy

grid = [[1, 2], [3, 4]]
shallow = grid.copy()
deep = copy.deepcopy(grid)
grid[0].append(99)                         # change an INNER list
print(shallow, deep)                       # the shallow copy shares inner lists

row = [0] * 3                              # fine: numbers are immutable
bad_board = [[0] * 3] * 3                  # trap: three references to ONE inner list
bad_board[0][0] = "X"
good_board = [[0] * 3 for _ in range(3)]   # a comprehension (later in this part) makes separate rows
good_board[0][0] = "X"
print(bad_board)
print(good_board)

scores = [72, 95, 88]
for i in range(len(scores)):               # works, but enumerate (later in this part) is nicer
    scores[i] += 5
print(scores)
```

**Output:**

```text
[[1, 2, 99], [3, 4]] [[1, 2], [3, 4]]
[['X', 0, 0], ['X', 0, 0], ['X', 0, 0]]
[['X', 0, 0], [0, 0, 0], [0, 0, 0]]
[77, 100, 93]
```

**Common mistakes:**

- ❌ `x = items.sort()` (x is `None`); use `sorted(items)` when you need the result.
- ❌ `[[0] * 3] * 3` for a grid: all rows are the same list.
- ❌ Removing items from a list while looping over it (items get skipped); loop over a copy or build a new list.
- ❌ Using `insert(0, x)`/`pop(0)` in a loop over a big list (slow); use `deque`.
- ❌ Expecting `copy()` to copy nested lists.

### Practice

1. From `temps = [31, 35, 29, 40, 33, 38]`, print the three hottest temperatures (highest first), the average rounded to 1 decimal, and a new list with only the temperatures above 32 (use a loop).

<details>
<summary><b>Answer</b></summary>

```python
temps = [31, 35, 29, 40, 33, 38]
print(sorted(temps, reverse=True)[:3])
print(round(sum(temps) / len(temps), 1))
hot = []
for t in temps:
    if t > 32:
        hot.append(t)
print(hot)
```

**Output:**

```text
[40, 38, 35]
34.3
[35, 40, 33, 38]
```

</details>

**Learn more:** [Python tutorial: more on lists](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists) · [Sorting HOW TO](https://docs.python.org/3/howto/sorting.html) · [Time complexity of Python operations](https://wiki.python.org/moin/TimeComplexity)

---

## 8. Tuples and Unpacking

### Theory

> **In simple words:** a **tuple** is like a list that **can't be changed**: `point = (3, 4)`. Use it for a fixed group of values that belong together, such as coordinates, an RGB colour, or a row from a database. **Unpacking** splits a tuple (or any sequence) into separate variables in one line: `x, y = point`.

**Why have an unchangeable list?**

- **Safety:** a function receiving a tuple can't accidentally modify your data.
- **Hashable:** tuples of immutable values can be dictionary keys and set members (lists can't), e.g. `distances[("Pune", "Mumbai")] = 150`.
- **Meaning:** a tuple usually means "one record with fixed positions" (`(name, age)`), a list means "many items of the same kind".
- Slightly smaller and faster than lists.

**Syntax:** the **comma** makes a tuple, not the brackets: `t = 1, 2, 3` is a tuple; a one-item tuple needs a trailing comma: `(5,)`; `()` is empty. Tuples support indexing, slicing, `len`, `in`, `count`, `index`, but no `append`/`remove`.

**Unpacking:** `a, b = b, a` swaps (the right side makes a tuple, then it's unpacked). `first, *rest = [1, 2, 3, 4]` puts the leftovers in a list with `*`. Use `_` for values you don't need. Functions return several values as a tuple (`return total, average`), which the caller unpacks. Unpacking works in `for` loops too: `for name, score in results:`.

**Named tuples** give positions names: `collections.namedtuple` (and `typing.NamedTuple`, written as a class, Part 3) let you write `p.x` instead of `p[0]` while staying a tuple. (Dataclasses, Section [21](#21-dataclasses-enums-and-__slots__), are usually a better choice for records you design yourself.)

**Immutability is shallow:** a tuple containing a list can't swap that list for another, but the list itself can still change.

### Python

```python
point = (3, 4)
x, y = point
print(point, x, y, point[0], len(point))
single, empty = (5,), ()
pair = 1, 2                                  # the comma makes the tuple
print(type(single), type((5)), empty, pair)

first, *middle, last = [10, 20, 30, 40, 50]
print(first, middle, last)
name, _, city = ("Asha", 29, "Pune")        # ignore the age
print(name, city)

results = [("Asha", 91), ("Ravi", 78), ("Meera", 85)]
for student, score in results:              # unpacking in a loop
    print(f"{student:6} {score}")

try:
    point[0] = 10
except TypeError as e:
    print("TypeError:", e)

team = ("A", ["Asha"])
team[1].append("Ravi")                       # the inner list can still change
print(team)
```

**Output:**

```text
(3, 4) 3 4 3 2
<class 'tuple'> <class 'int'> () (1, 2)
10 [20, 30, 40] 50
Asha Pune
Asha   91
Ravi   78
Meera  85
TypeError: 'tuple' object does not support item assignment
('A', ['Asha', 'Ravi'])
```

A **named tuple** is still a tuple, but its positions have names:

```python
from collections import namedtuple

Point = namedtuple("Point", ["x", "y"])       # a new tuple type with named positions
p = Point(3, 4)
print(p, p.x, p[1], p._replace(x=10))
```

**Output:**

```text
Point(x=3, y=4) 3 4 Point(x=10, y=4)
```

**Common mistakes:**

- ❌ `(5)` for a one-item tuple (it's just 5); write `(5,)`.
- ❌ Unpacking with the wrong number of names (`ValueError: too many values to unpack`).
- ❌ Using a list as a dictionary key (`TypeError: unhashable type: 'list'`); use a tuple.
- ❌ Assuming a tuple's contents are fully frozen when it holds lists or dicts.

### Practice

1. `orders = [("A12", 499.0, 2), ("B07", 1299.0, 1), ("C33", 99.0, 5)]` holds (id, price, quantity). Loop with unpacking to print each order's total, and find the id of the most expensive order total.

<details>
<summary><b>Answer</b></summary>

```python
orders = [("A12", 499.0, 2), ("B07", 1299.0, 1), ("C33", 99.0, 5)]
best_id, best_total = None, 0
for order_id, price, qty in orders:
    total = price * qty
    print(order_id, total)
    if total > best_total:
        best_id, best_total = order_id, total
print("largest:", best_id, best_total)
```

**Output:**

```text
A12 998.0
B07 1299.0
C33 495.0
largest: B07 1299.0
```

</details>

**Learn more:** [Python tutorial: tuples and sequences](https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences) · [typing.NamedTuple](https://docs.python.org/3/library/typing.html#typing.NamedTuple)

---

## 9. Dictionaries: Looking Things Up by Key

![A dictionary hashes each key to find a slot, so lookups jump straight to the value instead of scanning; keys must be hashable (immutable)](images/python/02-dict.svg)

### Theory

> **In simple words:** a **dictionary** (`dict`) stores **key → value** pairs, like a real dictionary maps a word to its meaning: `prices = {"apple": 40, "mango": 120}`. You look values up by key (`prices["mango"]`) instead of by position, and lookup is **fast no matter how big the dictionary is**. Dictionaries are everywhere in Python: JSON data, configuration, counting things, grouping things, caching results.

**Basics:**

| Operation | Example | Notes |
|---|---|---|
| Create | `{"a": 1}`, `dict(a=1)`, `{}` | `{}` is an empty dict, not a set |
| Read | `d["a"]` | `KeyError` if missing |
| Read safely | `d.get("a")`, `d.get("a", 0)` | `None` or a default if missing |
| Add / change | `d["b"] = 2` | Adds if new, replaces if it exists |
| Delete | `del d["a"]`, `d.pop("a", None)` | `pop` returns the value |
| Check | `"a" in d` | Checks **keys** |
| Loop | `for k in d`, `for k, v in d.items()`, `d.keys()`, `d.values()` | Keys come out in **insertion order** |
| Merge | `d1 \| d2`, `d1 \|= d2`, `d.update(d2)` | Right side wins on duplicate keys |
| Default | `d.setdefault("k", [])` | Insert a default if missing, then return the value |

**Keys must be hashable** (immutable): strings, numbers, tuples of those. Lists and dicts can't be keys. Values can be anything, including lists and other dicts (nested data like JSON).

**How it works (why it's fast):** Python computes a **hash** (a number) from the key and uses it to jump straight to a slot in an internal table, so `d[key]` takes about the same time for 10 or 10 million entries (average O(1)). That's also why keys must not change: a changed key would hash to a different slot and be lost.

**Two helpers from `collections`** you'll use constantly: `Counter` (counts things) and `defaultdict` (creates a default value for missing keys, perfect for grouping). Section [17](#17-the-standard-library-essentials) has more.

**Iteration order** is the order keys were inserted (guaranteed since Python 3.7). Don't add or remove keys while looping over a dict (`RuntimeError`); loop over `list(d)` instead.

### Python

```python
prices = {"apple": 40, "banana": 10, "mango": 120}
print(prices["mango"], prices.get("kiwi"), prices.get("kiwi", 0), "apple" in prices)
prices["kiwi"] = 25                      # add
prices["apple"] = 45                     # change
removed = prices.pop("banana")
print(prices, "removed:", removed, "size:", len(prices))

for fruit, price in prices.items():
    print(f"{fruit:6} ₹{price}")
print(list(prices.keys()), list(prices.values()), sum(prices.values()))

defaults = {"theme": "light", "lang": "en"}
user = {"lang": "hi"}
print(defaults | user)                   # merge: the right side wins

try:
    prices["papaya"]
except KeyError as e:
    print("KeyError:", e)
```

**Output:**

```text
120 None 0 True
{'apple': 45, 'mango': 120, 'kiwi': 25} removed: 10 size: 3
apple  ₹45
mango  ₹120
kiwi   ₹25
['apple', 'mango', 'kiwi'] [45, 120, 25] 190
{'theme': 'light', 'lang': 'hi'}
KeyError: 'papaya'
```

**Counting and grouping** are the two dictionary patterns you'll write most:

```python
from collections import Counter, defaultdict

text = "the cat and the hat and the bat"
counts = {}
for word in text.split():
    counts[word] = counts.get(word, 0) + 1          # manual counting
print(counts)
print(Counter(text.split()).most_common(2))          # the same with Counter

students = [("Asha", "A"), ("Ravi", "B"), ("Meera", "A"), ("Kabir", "C"), ("Zoya", "B")]
by_section = defaultdict(list)                        # missing keys start as []
for name, section in students:
    by_section[section].append(name)
print(dict(by_section))

order = {"id": "90312", "customer": {"name": "Asha", "city": "Pune"}, "items": [{"sku": "P1", "qty": 2}]}
print(order["customer"]["city"], order["items"][0]["qty"])
print(order.get("shipping", {}).get("eta", "unknown"))   # safe access into nested data
```

**Output:**

```text
{'the': 3, 'cat': 1, 'and': 2, 'hat': 1, 'bat': 1}
[('the', 3), ('and', 2)]
{'A': ['Asha', 'Meera'], 'B': ['Ravi', 'Zoya'], 'C': ['Kabir']}
Pune 2
unknown
```

**Common mistakes:**

- ❌ `d[key]` for keys that may be missing; use `get`, `in`, or `defaultdict`.
- ❌ Using lists as keys (`TypeError: unhashable type`); use tuples.
- ❌ Adding/removing keys while looping over the dict.
- ❌ Confusing `{}` (empty dict) with an empty set (`set()`).
- ❌ Searching values with `in` (`x in d` checks keys; use `x in d.values()`, which is slow for big dicts).

### Practice

1. Count the characters in `"mississippi"` with a plain dict (no `Counter`), then print the most common character and its count.
2. Invert `{"a": 1, "b": 2, "c": 1}` into a dict mapping each value to the list of keys that had it.

<details>
<summary><b>Answer</b></summary>

```python
counts = {}
for ch in "mississippi":
    counts[ch] = counts.get(ch, 0) + 1
best = max(counts, key=counts.get)          # the key with the largest count
print(counts, best, counts[best])

inverted = {}
for key, value in {"a": 1, "b": 2, "c": 1}.items():
    inverted.setdefault(value, []).append(key)
print(inverted)
```

**Output:**

```text
{'m': 1, 'i': 4, 's': 4, 'p': 2} i 4
{1: ['a', 'c'], 2: ['b']}
```

`max(counts, key=counts.get)` loops over the keys and compares them by their counts. With a tie (`i` and `s` both appear 4 times) it returns the first one it sees.

</details>

**Learn more:** [Python tutorial: dictionaries](https://docs.python.org/3/tutorial/datastructures.html#dictionaries) · [collections: Counter and defaultdict](https://docs.python.org/3/library/collections.html)

---

## 10. Sets: Unique Items and Fast Membership

### Theory

> **In simple words:** a **set** is a bag of **unique** items with no order: `{"pune", "delhi", "goa"}`. Adding something that's already there does nothing. Sets answer "is X in here?" instantly (like dictionary keys) and do maths-style operations: what's in both groups, in either, or in one but not the other.

**Creating:** `{1, 2, 3}`, `set(some_list)` (removes duplicates), `set()` for empty (not `{}`, which is an empty dict). Items must be hashable, like dict keys. A `frozenset` is an immutable set (it can itself be a set member or dict key).

**Operations:**

| Operation | Operator | Method | Result |
|---|---|---|---|
| Union (in either) | `a \| b` | `a.union(b)` | everything |
| Intersection (in both) | `a & b` | `a.intersection(b)` | common items |
| Difference (in a, not b) | `a - b` | `a.difference(b)` | |
| Symmetric difference (in exactly one) | `a ^ b` | `a.symmetric_difference(b)` | |
| Subset / superset | `a <= b`, `a >= b` | `issubset`, `issuperset` | True/False |

Changing: `add(x)`, `update(items)`, `remove(x)` (error if missing), `discard(x)` (no error), `pop()`.

**When to use a set:** removing duplicates, fast membership tests in loops (`if user_id in seen:` is O(1) for a set but O(n) for a list), comparing two groups (who registered but didn't pay?). To remove duplicates **and keep order**, use `list(dict.fromkeys(items))`.

### Python

```python
emails = ["a@x.com", "b@x.com", "a@x.com", "c@x.com", "b@x.com"]
unique = set(emails)
print(len(emails), len(unique), sorted(unique))
print(list(dict.fromkeys(emails)))              # de-duplicate, keeping first-seen order

registered = {"asha", "ravi", "meera", "kabir"}
paid = {"ravi", "kabir", "zoya"}
print("paid and registered:", sorted(registered & paid))
print("registered, not paid:", sorted(registered - paid))
print("paid, not registered:", sorted(paid - registered))
print("everyone:", sorted(registered | paid))
print("in exactly one:", sorted(registered ^ paid))
print({"ravi"} <= paid, "asha" in paid)

seen = set()
for n in [3, 1, 3, 2, 1, 4]:
    if n in seen:
        print("first repeat:", n)
        break
    seen.add(n)
```

**Output:**

```text
5 3 ['a@x.com', 'b@x.com', 'c@x.com']
['a@x.com', 'b@x.com', 'c@x.com']
paid and registered: ['kabir', 'ravi']
registered, not paid: ['asha', 'meera']
paid, not registered: ['zoya']
everyone: ['asha', 'kabir', 'meera', 'ravi', 'zoya']
in exactly one: ['asha', 'meera', 'zoya']
True False
first repeat: 3
```

The speed difference is real. Checking membership in a list scans every item; a set jumps straight to the answer:

```python
import timeit

items_list = list(range(100_000))
items_set = set(items_list)
t_list = timeit.timeit(lambda: 99_999 in items_list, number=200)
t_set = timeit.timeit(lambda: 99_999 in items_set, number=200)
print(f"list is roughly {t_list / t_set:,.0f}x slower than set for this lookup")
```

<!-- the exact ratio depends on the machine, so it's not shown as fixed output -->

On a typical laptop the list lookup is thousands of times slower. (`timeit` runs a small function many times and measures it; `lambda` is a tiny unnamed function, explained in Section [13](#13-scope-lambda-and-functional-tools-map-filter-sorted-reduce).)

**Common mistakes:**

- ❌ `x = {}` for an empty set (that's a dict).
- ❌ Expecting sets to keep order or support indexing (`s[0]` fails).
- ❌ Using a list for membership checks inside a big loop.
- ❌ Putting lists or dicts in a set (unhashable).

### Practice

1. Two friends' playlists are `a = ["song1", "song2", "song3", "song5"]` and `b = ["song2", "song4", "song5", "song5"]`. Print the songs both like, the songs only friend A likes, and how many different songs there are in total.

<details>
<summary><b>Answer</b></summary>

```python
a = ["song1", "song2", "song3", "song5"]
b = ["song2", "song4", "song5", "song5"]
print(sorted(set(a) & set(b)), sorted(set(a) - set(b)), len(set(a) | set(b)))
```

**Output:**

```text
['song2', 'song5'] ['song1', 'song3'] 5
```

</details>

**Learn more:** [Python tutorial: sets](https://docs.python.org/3/tutorial/datastructures.html#sets) · [Python docs: set types](https://docs.python.org/3/library/stdtypes.html#set-types-set-frozenset)

---

## 11. Looping Helpers and Comprehensions

### Theory

> **In simple words:** Python has small tools that make loops shorter and clearer. `enumerate` gives you the position **and** the item; `zip` walks through two lists side by side; `sorted`, `reversed`, `sum`, `min`, `max`, `any` and `all` answer common questions in one call. A **comprehension** builds a new list, set or dict from a loop in a single readable line: `[x * x for x in nums if x > 0]` means "the square of each positive number".

**Iteration helpers:**

| Helper | Example | Gives |
|---|---|---|
| `enumerate(items, start=1)` | `for i, name in enumerate(names, 1)` | (position, item) pairs |
| `zip(a, b)` | `for name, score in zip(names, scores)` | Pairs from both; stops at the shorter (`strict=True` raises if lengths differ) |
| `reversed(items)` | `for x in reversed(items)` | Items backwards, without copying |
| `sorted(items, key=..., reverse=...)` | | A new sorted list |
| `any(conditions)` / `all(conditions)` | `any(s < 40 for s in scores)` | True if at least one / every item is true |
| `sum`, `min`, `max` | `max(words, key=len)` | Aggregates; `key` chooses what to compare |

**Comprehension shapes:**

| Kind | Syntax |
|---|---|
| List | `[expression for item in iterable if condition]` |
| Set | `{expression for item in iterable}` |
| Dict | `{key_expr: value_expr for item in iterable}` |
| Generator expression | `(expression for item in iterable)`: produces items one at a time without building a list (Section [24](#24-iterators-and-generators-producing-values-lazily)); inside a function call the brackets can be dropped: `sum(x * x for x in nums)` |

Read a comprehension left to right as English: "`x * 2` **for** each `x` **in** `nums` **if** `x` is odd". The `if` at the end **filters**; an `a if cond else b` at the front **transforms** every item.

**When not to use them:** if it needs more than one `for` and one `if`, or has side effects (printing, appending elsewhere), write a normal loop. Readability wins.

### Python

```python
names = ["Asha", "Ravi", "Meera"]
scores = [91, 78, 85]
for i, name in enumerate(names, start=1):
    print(i, name)
for name, score in zip(names, scores):
    print(f"{name}: {score}")
print(dict(zip(names, scores)))
print(list(reversed(names)), max(names, key=len))
print(any(s < 80 for s in scores), all(s >= 75 for s in scores))
try:
    list(zip(names, [1, 2], strict=True))
except ValueError as e:
    print("ValueError:", e)
```

**Output:**

```text
1 Asha
2 Ravi
3 Meera
Asha: 91
Ravi: 78
Meera: 85
{'Asha': 91, 'Ravi': 78, 'Meera': 85}
['Meera', 'Ravi', 'Asha'] Meera
True True
ValueError: zip() argument 2 is shorter than argument 1
```

```python
nums = [3, -1, 4, -1, 5, -9, 2, 6]
squares = [n * n for n in nums]
positives = [n for n in nums if n > 0]
labels = ["pos" if n > 0 else "neg" for n in nums]          # transform every item
print(squares)
print(positives)
print(labels)
print({n % 3 for n in nums})                                # a set comprehension
print({name: len(name) for name in ["Asha", "Ravi", "Meera"]})   # a dict comprehension
print(sum(n * n for n in nums if n > 0))                    # generator expression: no list built

grid = [[r * 3 + c for c in range(3)] for r in range(3)]    # nested: a 3x3 grid
flat = [x for row in grid for x in row]                     # flatten: loops in the same order as nested for-loops
print(grid, flat)

prices = {"apple": 40, "mango": 120, "kiwi": 25}
cheap = {fruit: p for fruit, p in prices.items() if p < 50}
print(cheap, {p: fruit for fruit, p in prices.items()})     # filter; invert
```

**Output:**

```text
[9, 1, 16, 1, 25, 81, 4, 36]
[3, 4, 5, 2, 6]
['pos', 'neg', 'pos', 'neg', 'pos', 'neg', 'pos', 'pos']
{0, 1, 2}
{'Asha': 4, 'Ravi': 4, 'Meera': 5}
90
[[0, 1, 2], [3, 4, 5], [6, 7, 8]] [0, 1, 2, 3, 4, 5, 6, 7, 8]
{'apple': 40, 'kiwi': 25} {40: 'apple', 120: 'mango', 25: 'kiwi'}
```

**Common mistakes:**

- ❌ `for i in range(len(items)): item = items[i]` when `enumerate` or a plain `for item in items` is clearer.
- ❌ Comprehensions used only for side effects (`[print(x) for x in xs]`); use a loop.
- ❌ Unreadable comprehensions with several `for`s and conditions.
- ❌ Forgetting that `zip` silently drops extra items from the longer list (use `strict=True` when lengths must match).

### Practice

1. From `words = ["Python", "is", "a", "Great", "language", "to", "LEARN"]`, build: the list of words longer than 2 letters in lower case; a dict mapping each such word to its length; and whether any word is all upper-case.

<details>
<summary><b>Answer</b></summary>

```python
words = ["Python", "is", "a", "Great", "language", "to", "LEARN"]
long_words = [w.lower() for w in words if len(w) > 2]
print(long_words)
print({w: len(w) for w in long_words})
print(any(w.isupper() for w in words))
```

**Output:**

```text
['python', 'great', 'language', 'learn']
{'python': 6, 'great': 5, 'language': 8, 'learn': 5}
True
```

</details>

**Learn more:** [Python tutorial: list comprehensions](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions) · [Built-in functions (enumerate, zip, any, all)](https://docs.python.org/3/library/functions.html)

---

## 12. Functions: Reusable Blocks of Code

### Theory

> **In simple words:** a **function** is a named, reusable piece of code. You **define** it once with `def`, give it **parameters** (inputs), and it can **return** a result. Then you **call** it as often as you like: `area(3, 4)`. Functions let you break a big problem into small named steps, avoid repeating yourself, and test each step on its own.

**Anatomy:**

```text
def function_name(parameter1, parameter2="default"):
    """Docstring: what the function does."""
    ...body...
    return result          # optional; without it the function returns None
```

**Parameters and arguments** (parameters are the names in the definition; arguments are the values you pass):

| Kind | Definition | Call |
|---|---|---|
| Positional | `def f(a, b)` | `f(1, 2)` |
| Keyword arguments | | `f(b=2, a=1)`: order doesn't matter, clearer |
| Default values | `def f(a, b=10)` | `f(1)` |
| Any number of positional (`*args`) | `def f(*args)` | `f(1, 2, 3)` → `args` is a tuple |
| Any number of keyword (`**kwargs`) | `def f(**kwargs)` | `f(x=1, y=2)` → `kwargs` is a dict |
| Keyword-only | `def f(a, *, verbose=False)` | `verbose` must be passed by name |
| Positional-only | `def f(a, b, /)` | `a`, `b` can't be passed by name |

Order in a definition: positional-only, `/`, normal, `*args` (or a bare `*`), keyword-only, `**kwargs`. `*` and `**` also **unpack** when calling: `f(*my_list)`, `f(**my_dict)`.

**Return values:** `return` ends the function immediately. Return several values as a tuple (`return low, high`) and unpack them. A function without `return` returns `None`.

**The mutable default trap:** default values are created **once**, when the function is defined. `def add(item, bucket=[])` shares one list between all calls. Use `None` and create the list inside.

**Functions are objects:** you can store them in variables, put them in lists and dicts, and pass them to other functions (like `key=len` in `sorted`). This is the basis of callbacks, decorators and much more.

**Docstrings and type hints:** a string right after `def` documents the function (`help(f)` shows it). Type hints like `def area(w: float, h: float) -> float:` document the expected types (Section [22](#22-type-hints-and-static-type-checking)).

**Recursion:** a function that calls itself on a smaller problem, with a **base case** that stops it. Python limits the depth (about 1000 calls by default), so loops are preferred for long repetitive work; recursion shines for tree-shaped problems (`dsa-python.md`).

**Good functions:** do **one** thing, have a clear name (a verb: `calculate_total`, `send_email`), take inputs as parameters instead of reading global variables, return results instead of printing them, and stay short.

### Python

```python
def area(width, height=1):
    """Return the area of a rectangle."""
    return width * height

print(area(3, 4), area(5), area(height=2, width=7))

def stats(numbers):
    return min(numbers), max(numbers), sum(numbers) / len(numbers)

low, high, mean = stats([4, 8, 15, 16, 23, 42])
print(low, high, round(mean, 2))

def greet(name):
    print("Hi", name)                        # prints, but returns nothing

result = greet("Asha")
print(result)

def total(*prices, discount=0):              # any number of prices, keyword-only discount
    return sum(prices) * (1 - discount)

print(total(100, 200, 50), total(100, 200, discount=0.1))

def make_profile(name, **details):
    return {"name": name, **details}

print(make_profile("Ravi", city="Pune", age=31))
args = [2, 5]
opts = {"height": 3}
print(area(*args), area(4, **opts))          # unpacking when calling
```

**Output:**

```text
12 5 14
4 42 18.0
Hi Asha
None
350 270.0
{'name': 'Ravi', 'city': 'Pune', 'age': 31}
10 12
```

```python
def add_item_bad(item, bucket=[]):          # the default list is created ONCE
    bucket.append(item)
    return bucket

print(add_item_bad("a"), add_item_bad("b"))  # surprise: both calls share one list

def add_item(item, bucket=None):
    if bucket is None:
        bucket = []                          # a new list for every call
    bucket.append(item)
    return bucket

print(add_item("a"), add_item("b"))

def shout(text):
    return text.upper() + "!"

def whisper(text):
    return text.lower() + "..."

styles = {"loud": shout, "quiet": whisper}    # functions stored in a dict
for mood, fn in styles.items():
    print(mood, fn("Hello"))

def factorial(n):
    if n <= 1:                                # base case
        return 1
    return n * factorial(n - 1)               # smaller problem

print(factorial(5), factorial(20))
help(area)
```

**Output:**

```text
['a', 'b'] ['a', 'b']
['a'] ['b']
loud HELLO!
quiet hello...
120 2432902008176640000
Help on function area in module __main__:

area(width, height=1)
    Return the area of a rectangle.
```

**Common mistakes:**

- ❌ Mutable default arguments (`=[]`, `={}`); use `None`.
- ❌ Printing inside a function instead of returning the value (the caller can't use it).
- ❌ Forgetting `return`, so the function silently returns `None`.
- ❌ Calling a function without brackets (`area` is the function; `area()` calls it).
- ❌ Functions that do many unrelated things or depend on global variables.

### Practice

1. Write `word_stats(text, *, ignore_case=True)` that returns a tuple `(number_of_words, longest_word, dict_of_word_counts)`. Test it on `"The cat saw the other cat"` with and without `ignore_case`.

<details>
<summary><b>Answer</b></summary>

```python
def word_stats(text, *, ignore_case=True):
    words = text.lower().split() if ignore_case else text.split()
    counts = {}
    for w in words:
        counts[w] = counts.get(w, 0) + 1
    return len(words), max(words, key=len), counts

print(word_stats("The cat saw the other cat"))
print(word_stats("The cat saw the other cat", ignore_case=False))
```

**Output:**

```text
(6, 'other', {'the': 2, 'cat': 2, 'saw': 1, 'other': 1})
(6, 'other', {'The': 1, 'cat': 2, 'saw': 1, 'the': 1, 'other': 1})
```

</details>

**Learn more:** [Python tutorial: defining functions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions) · [PEP 570: positional-only parameters](https://peps.python.org/pep-0570/) · [PEP 257: docstring conventions](https://peps.python.org/pep-0257/)

---

## 13. Scope, Lambda and Functional Tools (map, filter, sorted, reduce)

### Theory

> **In simple words:** **scope** answers "where can this name be seen?". A variable created inside a function is **local**: it exists only while the function runs and is invisible outside. A **lambda** is a tiny one-line function without a name, handy when you need a quick function for `sorted`, `max` or `map`. `map` applies a function to every item, `filter` keeps items that pass a test, and `reduce` combines all items into one value.

**The LEGB rule:** when Python meets a name, it looks in this order:

1. **L**ocal: names created inside the current function.
2. **E**nclosing: names in outer functions (when functions are nested).
3. **G**lobal: names at the top level of the file (module).
4. **B**uilt-in: `print`, `len`, `range`, …

**Changing outer variables:** assigning to a name inside a function creates a **local** name, even if a global one exists. To rebind a global, declare `global name`; to rebind an enclosing function's variable, `nonlocal name`. Both are rarely needed: prefer passing values in and returning results out. (Mutating an outer list with `.append` is not rebinding, so it works without declarations, but it's a hidden side effect.)

**Lambda:** `lambda params: expression` creates a function with one expression and no name. `lambda x: x * 2` is the same as `def double(x): return x * 2`. Use lambdas inline (`key=lambda p: p["price"]`); if you want to name it or it's longer than one short expression, use `def`.

**Functional tools:**

| Tool | Does | Usually clearer as |
|---|---|---|
| `map(f, items)` | f applied to each item (lazily) | `[f(x) for x in items]` |
| `filter(pred, items)` | Items where pred(x) is true | `[x for x in items if pred(x)]` |
| `functools.reduce(f, items, start)` | Combines items pairwise into one value | `sum`, `max`, `"".join`, or a loop |
| `sorted/min/max(items, key=f)` | Order/compare by f(x) | Use these often |
| `operator.itemgetter`, `attrgetter` | Ready-made key functions | `key=itemgetter("price")` |
| `functools.partial(f, arg)` | A new function with some arguments filled in | |

In modern Python, comprehensions usually replace `map` and `filter`, while `key=` functions (often lambdas) are used everywhere.

### Python

```python
tax_rate = 0.18                          # global

def price_with_tax(price):
    tax = price * tax_rate               # tax is local; tax_rate is found in the global scope
    return price + tax

print(price_with_tax(100))
try:
    print(tax)
except NameError as e:
    print("NameError:", e)

counter = 0
def increment_wrong():
    try:
        counter += 1                     # assignment makes counter local → it has no value yet
    except UnboundLocalError as e:
        print("UnboundLocalError:", e)

def increment():
    global counter                       # works, but global state is hard to reason about
    counter += 1

increment_wrong()
increment(); increment()
print("counter =", counter)

def make_counter():
    count = 0
    def step():
        nonlocal count                   # rebind the enclosing function's variable
        count += 1
        return count
    return step

tick = make_counter()
print(tick(), tick(), tick())
```

**Output:**

```text
118.0
NameError: name 'tax' is not defined
UnboundLocalError: cannot access local variable 'counter' where it is not associated with a value
counter = 2
1 2 3
```

(`make_counter` returns a function that remembers `count`: that's a **closure**, covered with decorators in Section [23](#23-closures-and-decorators).)

```python
from functools import partial, reduce
from operator import itemgetter

products = [{"name": "pen", "price": 20}, {"name": "bag", "price": 899}, {"name": "book", "price": 350}]
print(sorted(products, key=lambda p: p["price"], reverse=True)[0]["name"])
print(min(products, key=itemgetter("price"))["name"])

nums = [1, 2, 3, 4, 5, 6]
print(list(map(lambda n: n * 10, nums)), [n * 10 for n in nums])
print(list(filter(lambda n: n % 2 == 0, nums)), [n for n in nums if n % 2 == 0])
print(reduce(lambda acc, n: acc * n, nums, 1))            # 1*2*3*4*5*6

def power(base, exponent):
    return base ** exponent

square = partial(power, exponent=2)
print(square(9), list(map(square, [1, 2, 3])))
```

**Output:**

```text
bag
pen
[10, 20, 30, 40, 50, 60] [10, 20, 30, 40, 50, 60]
[2, 4, 6] [2, 4, 6]
720
81 [1, 4, 9]
```

**Common mistakes:**

- ❌ `UnboundLocalError` from assigning to a global name inside a function without `global` (better: pass it in and return the new value).
- ❌ Long, complex lambdas; use `def` with a name.
- ❌ Assigning a lambda to a name (`f = lambda x: ...`); PEP 8 says use `def`.
- ❌ Forgetting that `map`/`filter` return lazy iterators (wrap in `list()` to see or reuse the results).

### Practice

1. Sort `people = [("Asha", 29, "Pune"), ("Ravi", 35, "Delhi"), ("Meera", 29, "Agra")]` by age ascending, and by city within the same age. Then use `reduce` to find the longest name (without `max`).

<details>
<summary><b>Answer</b></summary>

```python
people = [("Asha", 29, "Pune"), ("Ravi", 35, "Delhi"), ("Meera", 29, "Agra")]
print(sorted(people, key=lambda p: (p[1], p[2])))            # a tuple key sorts by age, then city
print(reduce(lambda a, b: a if len(a) >= len(b) else b, [p[0] for p in people]))
```

**Output:**

```text
[('Meera', 29, 'Agra'), ('Asha', 29, 'Pune'), ('Ravi', 35, 'Delhi')]
Meera
```

Returning a **tuple** from the key sorts by the first element, then the second on ties: the easiest way to sort by several criteria.

</details>

---

### ✅ Part 2 checkpoint

Without looking, can you:

- [ ] Choose between a list, tuple, dict and set for a job, and explain why lookups in dicts and sets are fast?
- [ ] Add, remove, slice, sort (with `key`) and copy lists, and avoid the shared-inner-list trap?
- [ ] Count and group with dicts, `Counter` and `defaultdict`, and use set operations?
- [ ] Use `enumerate`, `zip`, `any`/`all` and list/dict/set comprehensions?
- [ ] Write functions with defaults, `*args`, `**kwargs` and keyword-only parameters, and avoid the mutable default trap?
- [ ] Explain LEGB scope and use lambdas as `key` functions?

**Learn more:** [Python tutorial: scopes and namespaces](https://docs.python.org/3/tutorial/classes.html#python-scopes-and-namespaces) · [Functional programming HOWTO](https://docs.python.org/3/howto/functional.html) · [functools](https://docs.python.org/3/library/functools.html)

---

# Part 3 — Moderate: Writing Real Programs

> **Goal:** Handle errors, work with files and data formats, use modules and packages, the standard library, classes and type hints.  
> **You need:** Parts 1–2.

---

## 14. Errors and Exceptions: try, except, raise

### Theory

> **In simple words:** when something goes wrong while a program runs (a file is missing, a user types "abc" where a number was expected, a network call fails), Python **raises an exception**: it stops normal execution and looks for code that says how to handle that problem. `try:` marks code that might fail; `except SomeError:` says what to do if that error happens. If nobody handles it, the program stops and prints a traceback. You can also **raise** your own exceptions when your code detects a problem.

**The full shape:**

```text
try:
    risky code
except ValueError as e:        ← handle one kind of error (e is the exception object)
    ...
except (KeyError, IndexError): ← handle several kinds
    ...
else:
    runs only if NO exception happened
finally:
    ALWAYS runs (clean-up: close files, release locks)
```

**The exception hierarchy:** exceptions are classes arranged in a family tree. `Exception` is the parent of almost everything you'll catch: `ValueError`, `TypeError`, `KeyError` and `IndexError` (both are `LookupError`s), `ZeroDivisionError` (an `ArithmeticError`), `FileNotFoundError` (an `OSError`), and more. Catching a parent catches all its children. `KeyboardInterrupt` (Ctrl+C) and `SystemExit` are deliberately **not** under `Exception`, so `except Exception` doesn't swallow them.

**Raising:** `raise ValueError("age must be positive")`. Create **custom exceptions** by subclassing `Exception` (classes are in Section [18](#18-classes-and-objects); for now: `class OutOfStockError(Exception): pass` creates a new error type). Custom errors let callers handle your specific problem.

**Chaining:** `raise NewError("...") from e` keeps the original cause in the traceback. A bare `raise` inside `except` re-raises the current exception (after logging, for example).

**Exception groups (3.11+):** when several things fail at once (e.g. many concurrent tasks), Python can raise an `ExceptionGroup`; handle parts of it with `except* ValueError:`. You'll meet these with `asyncio.TaskGroup` (Section [33](#33-asyncio-async-and-await)).

**Two styles:** *LBYL* ("look before you leap": `if key in d:`) and *EAFP* ("easier to ask forgiveness than permission": `try: d[key] except KeyError:`). Python code often prefers EAFP, especially when the check and the action could race (files that disappear between check and open).

**Good practice:**

- Catch the **most specific** exception you can handle, as close to the problem as makes sense.
- Never write a bare `except:` or silently `pass`: you'll hide bugs (including typos that raise `NameError`).
- Keep the `try` block small, so you don't accidentally catch errors from unrelated lines.
- Add context when re-raising (`raise ... from e`), and log unexpected errors with the traceback.
- Use `finally` or, better, `with` (Section [25](#25-context-managers-with-setup-and-clean-up)) for clean-up.

### Python

```python
def parse_age(text):
    try:
        age = int(text)
    except ValueError:
        return f"{text!r} is not a number"
    else:
        if age < 0:
            return "age can't be negative"
        return f"age {age} ok"
    finally:
        print(f"  (checked {text!r})")     # always runs, even after return

for value in ["29", "abc", "-4"]:
    print(parse_age(value))
```

**Output:**

```text
  (checked '29')
age 29 ok
  (checked 'abc')
'abc' is not a number
  (checked '-4')
age can't be negative
```

```python
class OutOfStockError(Exception):
    """Raised when an order asks for more items than we have."""

STOCK = {"pen": 10, "bag": 0}

def reserve(item, qty):
    if item not in STOCK:
        raise KeyError(f"unknown item {item!r}")
    if qty > STOCK[item]:
        raise OutOfStockError(f"only {STOCK[item]} {item}(s) left, asked for {qty}")
    STOCK[item] -= qty
    return f"reserved {qty} {item}"

for item, qty in [("pen", 3), ("bag", 1), ("cup", 1)]:
    try:
        print(reserve(item, qty))
    except OutOfStockError as e:
        print("sorry:", e)
    except LookupError as e:                 # KeyError is a LookupError
        print("error:", type(e).__name__, e)

def load_config(text):
    try:
        return int(text)
    except ValueError as e:
        raise RuntimeError("config value 'workers' is invalid") from e

try:
    load_config("four")
except RuntimeError as e:
    print(e, "| caused by:", repr(e.__cause__))

try:
    raise ExceptionGroup("batch failed", [ValueError("bad row 3"), KeyError("id"), ValueError("bad row 9")])
except* ValueError as group:
    print("value errors:", [str(x) for x in group.exceptions])
except* KeyError as group:
    print("key errors:", [str(x) for x in group.exceptions])

print(KeyError.__mro__)                      # the family tree of KeyError
```

**Output:**

```text
reserved 3 pen
sorry: only 0 bag(s) left, asked for 1
error: KeyError "unknown item 'cup'"
config value 'workers' is invalid | caused by: ValueError("invalid literal for int() with base 10: 'four'")
value errors: ['bad row 3', 'bad row 9']
key errors: ["'id'"]
(<class 'KeyError'>, <class 'LookupError'>, <class 'Exception'>, <class 'BaseException'>, <class 'object'>)
```

**Common mistakes:**

- ❌ `except:` or `except Exception: pass` hiding real bugs.
- ❌ A huge `try` block around many lines; you can't tell which line failed or whether you handled the right thing.
- ❌ Using exceptions for normal control flow in hot loops when a simple check would do.
- ❌ Losing the original error when wrapping it (use `raise ... from e`).
- ❌ Returning error strings or `None` for real failures where raising an exception would be clearer.

### Practice

1. Write `safe_divide(a, b)` that returns `a / b`, returns `None` and prints a message on division by zero, and lets other errors (like dividing a string) propagate. Test `safe_divide(10, 4)`, `safe_divide(1, 0)` and `safe_divide("x", 2)` (catch the last one outside and print its type).

<details>
<summary><b>Answer</b></summary>

```python
def safe_divide(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        print("can't divide by zero")
        return None

print(safe_divide(10, 4))
print(safe_divide(1, 0))
try:
    safe_divide("x", 2)
except TypeError as e:
    print(type(e).__name__, "-", e)
```

**Output:**

```text
2.5
can't divide by zero
None
TypeError - unsupported operand type(s) for /: 'str' and 'int'
```

</details>

**Learn more:** [Python tutorial: errors and exceptions](https://docs.python.org/3/tutorial/errors.html) · [Built-in exception hierarchy](https://docs.python.org/3/library/exceptions.html#exception-hierarchy) · [PEP 654: exception groups](https://peps.python.org/pep-0654/)

---

## 15. Files and Data Formats: pathlib, Text Files, JSON and CSV

### Theory

> **In simple words:** programs read and save data in **files**. Python's `pathlib` handles file **paths** (names and folders) in a way that works on Windows, macOS and Linux. You open a file, read or write **text**, and close it; the `with` statement closes it for you automatically, even if an error happens. **JSON** and **CSV** are the two formats you'll meet most: JSON for nested data (APIs, config files), CSV for tables (spreadsheets).

**Paths with `pathlib`:**

| Code | Meaning |
|---|---|
| `Path("data") / "sales.csv"` | Join paths with `/` (works on every OS) |
| `p.name`, `p.stem`, `p.suffix`, `p.parent` | `sales.csv`, `sales`, `.csv`, `data` |
| `p.exists()`, `p.is_file()`, `p.is_dir()` | Checks |
| `p.mkdir(parents=True, exist_ok=True)` | Create folders |
| `p.read_text(encoding="utf-8")`, `p.write_text(...)` | Whole-file read/write in one call |
| `p.glob("*.csv")`, `p.rglob("*.py")` | Find files (`rglob` searches subfolders) |
| `Path.cwd()`, `Path.home()`, `p.resolve()` | Current folder, home folder, absolute path |

**Opening files:** `open(path, mode, encoding="utf-8")`. Modes: `"r"` read (default), `"w"` write (**erases** the file first), `"a"` append, `"x"` create (fails if it exists), add `"b"` for binary (`"rb"` for images, PDFs). **Always pass `encoding="utf-8"`** for text; the default differs between systems. Use `with open(...) as f:` so the file is closed automatically.

**Reading:** `f.read()` (everything), `for line in f:` (line by line, memory-friendly for big files), `f.readlines()` (list of lines). Lines keep their `\n`; `line.rstrip("\n")` removes it.

**JSON** (`import json`): `json.dumps(obj)` → string, `json.loads(text)` → Python objects; `json.dump(obj, f)`/`json.load(f)` for files. JSON objects become dicts, arrays become lists, `true/false/null` become `True/False/None`. `indent=2` for readable output, `ensure_ascii=False` to keep non-English characters readable. Dates, sets and custom objects aren't JSON-serialisable by default: convert them first (e.g. `date.isoformat()`).

**CSV** (`import csv`): `csv.reader`/`csv.writer` for rows as lists, `csv.DictReader`/`csv.DictWriter` for rows as dicts keyed by the header. Open CSV files with `newline=""`. Everything read from CSV is **text**: convert numbers yourself. For real data analysis, pandas (`data-science.md`) reads CSV, Excel, JSON and Parquet in one line.

**Safe writing:** writing directly over an important file can leave it half-written if the program crashes. Write to a temporary file in the same folder and then `Path.replace()` it onto the target (an atomic rename).

### Python

```python
from pathlib import Path

folder = Path("demo_files")
folder.mkdir(exist_ok=True)
notes = folder / "notes.txt"
notes.write_text("first line\nsecond line\n", encoding="utf-8")
with open(notes, "a", encoding="utf-8") as f:          # append mode
    f.write("third line\n")

with open(notes, encoding="utf-8") as f:
    for number, line in enumerate(f, start=1):         # line by line
        print(number, line.rstrip("\n"))

print(notes.name, notes.stem, notes.suffix, notes.parent, notes.exists())
print(len(notes.read_text(encoding="utf-8").splitlines()), "lines")
print(sorted(p.name for p in folder.glob("*.txt")))

try:
    open(folder / "missing.txt", encoding="utf-8")
except FileNotFoundError as e:
    print("FileNotFoundError:", e.filename)
```

**Output:**

```text
1 first line
2 second line
3 third line
notes.txt notes .txt demo_files True
3 lines
['notes.txt']
FileNotFoundError: demo_files/missing.txt
```

```python
import csv
import json

order = {"id": "90312", "customer": "Asha", "items": [{"sku": "P1", "qty": 2, "price": 499.0}], "paid": True, "coupon": None}
text = json.dumps(order, indent=2)
print(text)
back = json.loads(text)
print(back == order, back["items"][0]["price"])
(folder / "order.json").write_text(json.dumps(order, ensure_ascii=False), encoding="utf-8")

rows = [{"name": "Asha", "city": "Pune", "score": 91}, {"name": "Ravi", "city": "Delhi", "score": 78}]
with open(folder / "scores.csv", "w", newline="", encoding="utf-8") as f:
    writer = csv.DictWriter(f, fieldnames=["name", "city", "score"])
    writer.writeheader()
    writer.writerows(rows)

print((folder / "scores.csv").read_text(encoding="utf-8"))
with open(folder / "scores.csv", newline="", encoding="utf-8") as f:
    for row in csv.DictReader(f):
        print(row, "→ score as a number:", int(row["score"]) + 0)
```

**Output:**

```text
{
  "id": "90312",
  "customer": "Asha",
  "items": [
    {
      "sku": "P1",
      "qty": 2,
      "price": 499.0
    }
  ],
  "paid": true,
  "coupon": null
}
True 499.0
name,city,score
Asha,Pune,91
Ravi,Delhi,78

{'name': 'Asha', 'city': 'Pune', 'score': '91'} → score as a number: 91
{'name': 'Ravi', 'city': 'Delhi', 'score': '78'} → score as a number: 78
```

**Common mistakes:**

- ❌ Opening files without `with` (they may stay open) or without `encoding="utf-8"`.
- ❌ Opening an important file with `"w"` by mistake (it's erased immediately).
- ❌ Building paths by gluing strings with `"\\"` or `"/"`; use `pathlib`.
- ❌ Forgetting that CSV values are strings (`"91" + 1` fails).
- ❌ Reading a multi-gigabyte file with `read()`; iterate line by line.

### Practice

1. Write `word_count(path)` that returns the number of lines, words and characters in a text file (like the `wc` command). Test it on `demo_files/notes.txt`. Then save the result as JSON to `demo_files/stats.json` and read it back.

<details>
<summary><b>Answer</b></summary>

```python
def word_count(path):
    lines = words = chars = 0
    with open(path, encoding="utf-8") as f:
        for line in f:
            lines += 1
            words += len(line.split())
            chars += len(line)
    return {"lines": lines, "words": words, "chars": chars}

stats = word_count(folder / "notes.txt")
(folder / "stats.json").write_text(json.dumps(stats), encoding="utf-8")
print(json.loads((folder / "stats.json").read_text(encoding="utf-8")))
```

**Output:**

```text
{'lines': 3, 'words': 6, 'chars': 34}
```

</details>

**Learn more:** [pathlib](https://docs.python.org/3/library/pathlib.html) · [Python tutorial: reading and writing files](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files) · [json](https://docs.python.org/3/library/json.html) · [csv](https://docs.python.org/3/library/csv.html)

---

## 16. Modules, Packages, Virtual Environments and uv

![A project folder with src/shop package, tests, pyproject.toml and a .venv; pip or uv installs third-party packages from PyPI into the virtual environment](images/python/03-project.svg)

### Theory

> **In simple words:** a **module** is just a `.py` file; `import` lets one file use code from another. A **package** is a folder of modules. Python comes with a big **standard library** (json, pathlib, datetime…), and hundreds of thousands of **third-party packages** (requests, pandas, FastAPI…) live on **PyPI**, the Python Package Index. You install them into a **virtual environment**: a private folder of packages for one project, so different projects can use different versions without clashing. In 2026 the recommended tool for all of this is **uv**.

**Importing:**

| Form | Use |
|---|---|
| `import math` | Use as `math.sqrt(9)`: clear where names come from |
| `from math import sqrt, pi` | Use `sqrt(9)` directly |
| `import numpy as np` | A short alias (common conventions: `np`, `pd`, `plt`) |
| `from package.module import name` | From inside a package |
| `from .sibling import name` | Relative import within your own package |
| ❌ `from module import *` | Pollutes your namespace; avoid |

**How `import` finds modules:** it searches `sys.path` (the script's folder, the standard library, then installed packages). The first import **runs the module's top-level code once** and caches it in `sys.modules`; later imports reuse it.

**`if __name__ == "__main__":`** Every module has a `__name__`. When you run a file directly it's `"__main__"`; when it's imported it's the module's name. Code under this check runs only when the file is executed as a script, not when imported, so a file can be both a reusable module and a runnable program.

**Packages:** a folder with `__init__.py` (runs on import; can expose a tidy public API). Name your files carefully: a file called `random.py` or `json.py` in your project **shadows** the standard library module.

**Circular imports** (a imports b, b imports a) cause errors like "partially initialized module". Fix by moving shared code into a third module, or importing inside the function that needs it.

**Virtual environments and installing packages:**

| Task | Classic tools | uv (recommended) |
|---|---|---|
| Create a project | make folders by hand | `uv init myproject` |
| Create a virtual environment | `python -m venv .venv`, then activate it | automatic (`.venv` created on first use) |
| Add a dependency | `pip install requests` (+ edit requirements.txt) | `uv add requests` (updates `pyproject.toml` and `uv.lock`) |
| Dev-only tools | `pip install pytest` | `uv add --dev pytest ruff` |
| Run code in the environment | activate, then `python main.py` | `uv run main.py` |
| Reproduce on another machine | `pip install -r requirements.txt` | `uv sync` (exact versions from the lock file) |
| Install a Python version | download an installer | `uv python install 3.14` |
| Run a tool once | `pipx run ruff` | `uvx ruff check` |

**`pyproject.toml`** is the standard project file: name, version, required Python, dependencies, and tool settings (ruff, pytest, mypy). A **lock file** (`uv.lock`) records the exact version of every package, including dependencies of dependencies, so everyone gets identical installs. Commit both; never commit `.venv/`.

**Version specifiers:** `requests>=2.32` (at least), `~=2.32` (compatible: 2.32.x and later 2.x), `==2.32.3` (exact; for applications use the lock file instead of pinning by hand).

### Python

A module is a file. Here we create a tiny package on disk and import it, to see `__name__` and the import cache in action:

```python
import sys
from pathlib import Path

pkg = Path("shoptools")
pkg.mkdir(exist_ok=True)
(pkg / "__init__.py").write_text('from .pricing import add_tax\n__all__ = ["add_tax"]\n', encoding="utf-8")
(pkg / "pricing.py").write_text('''
print("  pricing.py is running (only on first import)")
TAX = 0.18

def add_tax(amount):
    return round(amount * (1 + TAX), 2)

if __name__ == "__main__":
    print("run directly:", add_tax(100))
else:
    print("  imported as", __name__)
''', encoding="utf-8")

sys.path.insert(0, str(Path.cwd()))          # make the current folder importable (a normal script's folder already is)
import shoptools
from shoptools.pricing import TAX
import shoptools.pricing                      # already cached: the module doesn't run again
print(shoptools.add_tax(100), TAX, "shoptools.pricing" in sys.modules)
print(__name__)                               # this code is the main program
```

**Output:**

```text
  pricing.py is running (only on first import)
  imported as shoptools.pricing
118.0 0.18 True
__main__
```

The standard library in a few imports:

```python
import math, random, statistics
from datetime import date, timedelta

random.seed(7)                                 # fixed seed: the same "random" numbers every run
print(math.sqrt(144), round(math.pi, 4), math.gcd(84, 36))
print(random.randint(1, 6), random.choice(["red", "green", "blue"]))
print(statistics.mean([4, 8, 15]), statistics.median([4, 8, 15, 16]))
print(date(2026, 9, 25) + timedelta(days=10))
```

**Output:**

```text
12.0 3.1416 12
3 red
9 11.5
2026-10-05
```

A typical uv workflow in the terminal (not Python code):

```text
uv init shop-api && cd shop-api     # creates pyproject.toml, main.py, .python-version
uv add fastapi httpx                # installs into .venv, records versions in pyproject.toml + uv.lock
uv add --dev pytest ruff            # development-only tools
uv run main.py                      # runs inside the project's environment
uv run pytest                       # run tests
uv sync                             # on another machine: install exactly what uv.lock says
```

**Common mistakes:**

- ❌ Installing packages globally with `sudo pip install` (breaks system Python); always use a virtual environment (or uv).
- ❌ Naming your own file `random.py`, `json.py` or `test.py` and wondering why imports break.
- ❌ `from module import *`.
- ❌ Committing `.venv/` to git, or not committing the lock file.
- ❌ Putting slow work (network calls, big computations) at module top level; it runs on import.

### Practice

1. Add a function `apply_coupon(amount, percent)` to `shoptools/pricing.py` (by editing the text and re-importing with `importlib.reload`), then call it. Why is `reload` needed here?

<details>
<summary><b>Answer</b></summary>

```python
import importlib

source = (pkg / "pricing.py").read_text(encoding="utf-8")
source += "\ndef apply_coupon(amount, percent):\n    return round(amount * (1 - percent / 100), 2)\n"
(pkg / "pricing.py").write_text(source, encoding="utf-8")
importlib.reload(shoptools.pricing)             # modules run once; reload forces a re-run
print(shoptools.pricing.apply_coupon(1000, 15))
```

**Output:**

```text
  pricing.py is running (only on first import)
  imported as shoptools.pricing
850.0
```

Modules are cached in `sys.modules` after the first import, so a plain `import` wouldn't see the change. `reload` runs the module's top-level code again: that's why its two messages appear a second time. In real projects you just restart the program; `reload` is for experiments in a REPL or notebook.

</details>

**Learn more:** [Python tutorial: modules](https://docs.python.org/3/tutorial/modules.html) · [uv: projects guide](https://docs.astral.sh/uv/guides/projects/) · [Python Packaging User Guide: pyproject.toml](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/)

---

## 17. The Standard Library Essentials

### Theory

> **In simple words:** Python is "batteries included": it ships with hundreds of ready-made modules. Before installing a package or writing something yourself, check the standard library: counting, queues, dates with time zones, combinations, caching, random numbers, secure tokens, file operations and running other programs are all built in, tested and fast.

**The modules you'll use most:**

| Module | Highlights |
|---|---|
| `collections` | `Counter` (counting), `defaultdict` (grouping), `deque` (fast queue at both ends), `namedtuple`, `ChainMap` |
| `itertools` | `chain`, `islice`, `groupby`, `product`, `permutations`, `combinations`, `accumulate`, `pairwise`, `batched` (3.12+) |
| `functools` | `cache`/`lru_cache` (memoise results), `partial`, `reduce`, `wraps`, `cached_property`, `total_ordering`, `singledispatch` |
| `datetime`, `zoneinfo` | Dates, times, durations; real time zones (`ZoneInfo("Asia/Kolkata")`) |
| `heapq`, `bisect` | Priority queues; binary search in sorted lists (`dsa-python.md`) |
| `random`, `secrets` | Random for simulations and games; `secrets` for passwords, tokens (cryptographically secure) |
| `pathlib`, `shutil`, `os`, `sys` | Paths; copy/move/delete trees; environment variables (`os.environ`); interpreter info and `sys.argv` |
| `subprocess` | Run other programs (Section [36](#36-scripting-and-automation-clis-subprocess-files-and-scheduling)) |
| `json`, `csv`, `sqlite3`, `tomllib` | Data formats and a built-in database; `tomllib` reads `pyproject.toml`-style files |
| `re` | Regular expressions (Section [26](#26-regular-expressions)) |
| `logging`, `argparse`, `unittest` | Logs, command-line arguments, tests (pytest is usually preferred) |
| `time`, `timeit` | Timestamps, sleeping, measuring code |
| `uuid`, `hashlib`, `base64` | Unique ids, hashes (SHA-256), encoding |
| `dataclasses`, `enum`, `typing` | Records, named constants, type hints (Part 3) |
| `concurrent.futures`, `asyncio` | Concurrency (Part 5) |

**Dates and times done right:** store and compute in **UTC** with time-zone-aware datetimes (`datetime.now(UTC)`), convert to local time only for display (`.astimezone(ZoneInfo("Asia/Kolkata"))`). "Naive" datetimes (no time zone) cause bugs around daylight saving and between servers. `date.fromisoformat("2026-09-25")` and `.isoformat()` handle the standard text format.

**Caching:** `@cache` (or `@lru_cache(maxsize=...)`) above a function remembers results for arguments it has seen, turning slow repeated calls into instant lookups. The `@` syntax is a *decorator*, explained in Section [23](#23-closures-and-decorators); for now read it as "add caching to this function". Arguments must be hashable.

### Python

```python
from collections import Counter, defaultdict, deque

votes = Counter(["tea", "coffee", "tea", "juice", "tea", "coffee"])
print(votes.most_common(1), votes["tea"], votes["water"])     # missing keys count as 0
votes.update(["juice", "juice"])
print(votes)

queue = deque(["a", "b", "c"], maxlen=4)      # fast appends/pops at both ends; keeps the last 4
queue.append("d")
queue.append("e")                             # full (maxlen 4): "a" falls off the front
print(queue)
first = queue.popleft()
print(first, queue)

from itertools import accumulate, batched, chain, combinations, groupby, islice, pairwise, product
print(list(chain([1, 2], [3], [4, 5])), list(islice(range(100), 3)))
print(list(combinations("ABC", 2)), len(list(product(range(3), repeat=3))))
print(list(accumulate([5, 10, 20])), list(pairwise([1, 4, 9, 16])))
print(list(batched(range(7), 3)))
for key, group in groupby(sorted(["apple", "avocado", "banana", "blueberry", "cherry"]), key=lambda w: w[0]):
    print(key, list(group))
```

**Output:**

```text
[('tea', 3)] 3 0
Counter({'tea': 3, 'juice': 3, 'coffee': 2})
deque(['b', 'c', 'd', 'e'], maxlen=4)
b deque(['c', 'd', 'e'], maxlen=4)
[1, 2, 3, 4, 5] [0, 1, 2]
[('A', 'B'), ('A', 'C'), ('B', 'C')] 27
[5, 15, 35] [(1, 4), (4, 9), (9, 16)]
[(0, 1, 2), (3, 4, 5), (6,)]
a ['apple', 'avocado']
b ['banana', 'blueberry']
c ['cherry']
```

```python
from datetime import UTC, date, datetime, timedelta
from functools import cache
from zoneinfo import ZoneInfo
import secrets, uuid, hashlib

meeting = datetime(2026, 9, 25, 9, 30, tzinfo=UTC)
print(meeting.isoformat())
print(meeting.astimezone(ZoneInfo("Asia/Kolkata")).strftime("%d %b %Y, %I:%M %p %Z"))
print(meeting.astimezone(ZoneInfo("America/New_York")).strftime("%H:%M %Z"))
due = date(2026, 9, 25) + timedelta(days=45)
print(due, due.strftime("%A"), (due - date(2026, 9, 25)).days, "days")

@cache
def fib(n):
    return n if n < 2 else fib(n - 1) + fib(n - 2)

print(fib(90), fib.cache_info().hits)          # instant thanks to caching

print(len(secrets.token_urlsafe(16)) > 16, uuid.uuid4().version)
print(hashlib.sha256(b"hello").hexdigest()[:16])
```

**Output:**

```text
2026-09-25T09:30:00+00:00
25 Sep 2026, 03:00 PM IST
05:30 EDT
2026-11-09 Monday 45 days
2880067194370816120 88
True 4
2cf24dba5fb0a30e
```

(Without `@cache`, `fib(90)` would make about 10¹⁹ calls, far longer than a lifetime; with it, each value is computed once.)

**Common mistakes:**

- ❌ Naive datetimes and `datetime.utcnow()` (deprecated); use `datetime.now(UTC)`.
- ❌ `random` for passwords or tokens; use `secrets`.
- ❌ Reinventing `Counter`, `defaultdict`, `deque` or `itertools` functions with loops.
- ❌ `groupby` on unsorted data (it only groups **consecutive** equal keys).
- ❌ Caching functions whose results depend on changing outside state, or with unhashable arguments.

### Practice

1. You receive login events `[("asha", "09:00"), ("ravi", "09:05"), ("asha", "09:30"), ("meera", "10:00"), ("asha", "11:00"), ("ravi", "12:00")]`. Print the user with the most logins, the logins grouped by user (a dict of lists of times), and all possible pairs of distinct users.

<details>
<summary><b>Answer</b></summary>

```python
events = [("asha", "09:00"), ("ravi", "09:05"), ("asha", "09:30"), ("meera", "10:00"), ("asha", "11:00"), ("ravi", "12:00")]
print(Counter(user for user, _ in events).most_common(1))
by_user = defaultdict(list)
for user, time in events:
    by_user[user].append(time)
print(dict(by_user))
print(list(combinations(sorted(by_user), 2)))
```

**Output:**

```text
[('asha', 3)]
{'asha': ['09:00', '09:30', '11:00'], 'ravi': ['09:05', '12:00'], 'meera': ['10:00']}
[('asha', 'meera'), ('asha', 'ravi'), ('meera', 'ravi')]
```

</details>

**Learn more:** [The Python Standard Library](https://docs.python.org/3/library/index.html) · [itertools recipes](https://docs.python.org/3/library/itertools.html#itertools-recipes) · [Doug Hellmann: Python Module of the Week](https://pymotw.com/3/)

---

## 18. Classes and Objects

![A class is a blueprint with methods and class attributes; each object created from it has its own instance attributes; calling a method passes the object as self](images/python/04-class.svg)

### Theory

> **In simple words:** a **class** is a blueprint for a kind of thing, like "bank account": it says what data each account has (owner, balance) and what it can do (deposit, withdraw). An **object** (or **instance**) is one actual thing made from the blueprint: Asha's account, Ravi's account. Grouping data with the functions that work on it keeps programs organised, and it's how most Python libraries are built (a pandas `DataFrame`, a FastAPI `app`, an `anthropic.Anthropic()` client are all objects).

**The pieces:**

| Piece | Example | Meaning |
|---|---|---|
| Class definition | `class Account:` | Class names use `PascalCase` |
| Constructor | `def __init__(self, owner, balance=0):` | Runs when you create an object; sets up its data |
| `self` | `self.balance = balance` | The object the method is working on (Python passes it automatically) |
| Instance attribute | `self.owner` | Data that belongs to one object |
| Class attribute | `interest_rate = 0.04` (in the class body) | Shared by all objects of the class |
| Method | `def deposit(self, amount):` | A function inside a class; called as `acct.deposit(100)` |
| Creating an object | `acct = Account("Asha", 500)` | Calls `__init__` |

**Three kinds of methods:**

| Kind | First parameter | Use |
|---|---|---|
| Instance method | `self` | Works with one object's data (the normal case) |
| `@classmethod` | `cls` (the class) | Alternative constructors: `Account.from_csv_row(row)` |
| `@staticmethod` | none | A helper that belongs with the class but needs neither |

**Properties** turn methods into attribute-style access with validation: `@property def balance(self)` lets code read `acct.balance`, and a matching `@balance.setter` runs checks on assignment. By convention, a leading underscore (`self._balance`) marks an attribute as **internal** ("please don't touch from outside"); Python doesn't enforce privacy. A double underscore (`self.__secret`) triggers **name mangling** (renamed to `_Account__secret`) to avoid clashes in subclasses, not for security.

**The class-attribute trap:** a mutable class attribute (`members = []` in the class body) is **shared** by all instances. Put per-object data in `__init__`.

**`__repr__`** (Section [20](#20-special-dunder-methods-making-objects-feel-built-in)) controls how an object prints; define it early, it makes debugging much easier.

**When to write a class:** when you have data plus behaviour that belong together and several instances (accounts, orders, API clients), or state that persists between calls. For plain records use a dataclass (Section [21](#21-dataclasses-enums-and-__slots__)); for a single operation, a function is simpler.

### Python

```python
class Account:
    interest_rate = 0.04                          # class attribute: shared

    def __init__(self, owner, balance=0):
        self.owner = owner                        # instance attributes: per object
        self._balance = balance                   # "internal" by convention

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("deposit must be positive")
        self._balance += amount
        return self._balance

    def withdraw(self, amount):
        if amount > self._balance:
            raise ValueError(f"insufficient funds: balance {self._balance}, asked {amount}")
        self._balance -= amount
        return self._balance

    @property
    def balance(self):                            # read like an attribute: acct.balance
        return self._balance

    def add_interest(self):
        self._balance = round(self._balance * (1 + self.interest_rate), 2)

    @classmethod
    def from_text(cls, text):                     # alternative constructor: "Asha,500"
        owner, amount = text.split(",")
        return cls(owner, float(amount))

    @staticmethod
    def is_valid_owner(name):
        return name.replace(" ", "").isalpha()

    def __repr__(self):
        return f"Account(owner={self.owner!r}, balance={self._balance})"

asha = Account("Asha", 500)
ravi = Account.from_text("Ravi,1200")
asha.deposit(250)
ravi.withdraw(200)
asha.add_interest()
print(asha, ravi, asha.balance)
print(Account.is_valid_owner("Asha Rao"), Account.is_valid_owner("R2D2"))
try:
    asha.withdraw(10_000)
except ValueError as e:
    print("ValueError:", e)
try:
    asha.balance = 1_000_000                      # a property without a setter is read-only
except AttributeError as e:
    print("AttributeError:", e)
print(type(asha).__name__, isinstance(asha, Account), vars(asha))
```

**Output:**

```text
Account(owner='Asha', balance=780.0) Account(owner='Ravi', balance=1000.0) 780.0
True False
ValueError: insufficient funds: balance 780.0, asked 10000
AttributeError: property 'balance' of 'Account' object has no setter
Account True {'owner': 'Asha', '_balance': 780.0}
```

The shared-class-attribute trap, and the fix:

```python
class TeamBad:
    members = []                                  # ONE list for every team
    def add(self, name):
        self.members.append(name)

class Team:
    def __init__(self):
        self.members = []                         # a new list per team
    def add(self, name):
        self.members.append(name)

a, b = TeamBad(), TeamBad()
a.add("Asha")
print(b.members)                                  # b "has" Asha too
c, d = Team(), Team()
c.add("Asha")
print(c.members, d.members)
```

**Output:**

```text
['Asha']
['Asha'] []
```

**Common mistakes:**

- ❌ Forgetting `self` as the first parameter of a method (`TypeError: takes 0 positional arguments but 1 was given`).
- ❌ Mutable class attributes meant to be per-object.
- ❌ Getter/setter methods for everything (`get_name()`); use plain attributes, and properties only when you need logic.
- ❌ Giant "god classes" that do everything; split responsibilities.
- ❌ Writing a class where a function or a dataclass would do.

### Practice

1. Write a `Cart` class with `add(item, price, qty=1)`, a `total` property, and `remove(item)`. Keep items in a dict `{item: [price, qty]}`. Add two pens (₹20 each) and a bag (₹899), remove the pens, and print the total before and after.

<details>
<summary><b>Answer</b></summary>

```python
class Cart:
    def __init__(self):
        self.items = {}

    def add(self, item, price, qty=1):
        if item in self.items:
            self.items[item][1] += qty
        else:
            self.items[item] = [price, qty]

    def remove(self, item):
        self.items.pop(item, None)

    @property
    def total(self):
        return sum(price * qty for price, qty in self.items.values())

cart = Cart()
cart.add("pen", 20, 2)
cart.add("bag", 899)
print(cart.total)
cart.remove("pen")
print(cart.total, cart.items)
```

**Output:**

```text
939
899 {'bag': [899, 1]}
```

</details>

**Learn more:** [Python tutorial: classes](https://docs.python.org/3/tutorial/classes.html) · [Real Python: OOP in Python](https://realpython.com/python3-object-oriented-programming/) · [property](https://docs.python.org/3/library/functions.html#property)

---

## 19. Inheritance, Composition, Abstract Classes and Protocols

### Theory

> **In simple words:** **inheritance** lets a new class start from an existing one and add or change behaviour: a `SavingsAccount` *is an* `Account` with interest rules. **Composition** builds a class out of other objects instead: a `Car` *has an* `Engine`. Both are ways to reuse code; modern advice is to **prefer composition** and use inheritance for genuine "is a" relationships. Together with **encapsulation** (hiding details behind methods) and **polymorphism** (different classes answering the same method call in their own way), these are the "four pillars" of object-oriented programming.

**Inheritance basics:**

- `class Child(Parent):` inherits every attribute and method of `Parent`.
- **Overriding:** define a method with the same name to replace the parent's version.
- `super().method(...)` calls the parent's version (almost always in `__init__`: `super().__init__(...)`).
- `isinstance(obj, Parent)` is true for children too; `issubclass(Child, Parent)`.

**Multiple inheritance and the MRO:** a class can inherit from several parents. Python decides where to look for methods using the **Method Resolution Order** (C3 linearisation): the class, then its parents left to right, each class appearing once, before its own parents. `Class.__mro__` shows it. `super()` follows the MRO, which lets cooperative classes (mixins) chain calls correctly.

**Mixins** are small classes that add one capability (`JsonMixin` adds `to_json()`), meant to be combined with a main base class.

**Abstract base classes** (`abc.ABC` + `@abstractmethod`) define a required interface: you can't create an object of a class that hasn't implemented all abstract methods, which catches mistakes early.

**Duck typing and Protocols:** Python cares about what an object **can do**, not what class it is ("if it walks like a duck…"): any object with a `.read()` method can be used where a file is expected. `typing.Protocol` writes such an interface down for type checkers without requiring inheritance (Section [22](#22-type-hints-and-static-type-checking)).

**Polymorphism:** code like `for shape in shapes: total += shape.area()` works for circles, squares and any future shape: each class provides its own `area`.

**Composition over inheritance:** deep inheritance trees are rigid (a change in the base ripples everywhere, and "is a" rarely stays true). Holding other objects as attributes and delegating to them is more flexible and easier to test: pass a `notifier` object into an `OrderService` instead of inheriting from `EmailSender`.

**SOLID in one line each:** Single responsibility (one reason to change) · Open/closed (extend without editing) · Liskov substitution (a subclass must work wherever the parent does) · Interface segregation (small, focused interfaces) · Dependency inversion (depend on abstractions, pass dependencies in).

### Python

```python
from abc import ABC, abstractmethod
import math

class Shape(ABC):
    def __init__(self, name):
        self.name = name

    @abstractmethod
    def area(self):
        """Every shape must implement this."""

    def describe(self):                                   # shared behaviour
        return f"{self.name} with area {self.area():.2f}"

class Circle(Shape):
    def __init__(self, radius):
        super().__init__("circle")
        self.radius = radius

    def area(self):
        return math.pi * self.radius ** 2

class Rectangle(Shape):
    def __init__(self, w, h):
        super().__init__("rectangle")
        self.w, self.h = w, h

    def area(self):
        return self.w * self.h

class Square(Rectangle):                                  # a square IS a rectangle
    def __init__(self, side):
        super().__init__(side, side)
        self.name = "square"

shapes = [Circle(1), Rectangle(2, 3), Square(4)]
for s in shapes:                                          # polymorphism
    print(s.describe())
print(isinstance(Square(1), Rectangle), Square.__mro__)
try:
    Shape("blob")
except TypeError as e:
    print("TypeError:", e)
```

**Output:**

```text
circle with area 3.14
rectangle with area 6.00
square with area 16.00
True (<class '__main__.Square'>, <class '__main__.Rectangle'>, <class '__main__.Shape'>, <class 'abc.ABC'>, <class 'object'>)
TypeError: Can't instantiate abstract class Shape without an implementation for abstract method 'area'
```

```python
import json

class JsonMixin:
    def to_json(self):
        return json.dumps(vars(self))

class LoggedMixin:
    def save(self):
        print(f"[log] saving {type(self).__name__}")
        return super().save()                           # continue along the MRO

class Model:
    def save(self):
        return "saved"

class User(LoggedMixin, JsonMixin, Model):
    def __init__(self, name, email):
        self.name, self.email = name, email

u = User("Asha", "asha@example.com")
print(u.to_json(), u.save())
print([c.__name__ for c in User.__mro__])

class EmailNotifier:                                      # composition: pass collaborators in
    def send(self, to, text):
        return f"email to {to}: {text}"

class SmsNotifier:
    def send(self, to, text):
        return f"SMS to {to}: {text}"

class OrderService:
    def __init__(self, notifier):
        self.notifier = notifier                          # "has a" notifier
    def place(self, customer, order_id):
        return self.notifier.send(customer, f"order {order_id} confirmed")

print(OrderService(EmailNotifier()).place("asha@example.com", "90312"))
print(OrderService(SmsNotifier()).place("+91-98xxxxxx", "90313"))   # duck typing: any object with .send works
```

**Output:**

```text
[log] saving User
{"name": "Asha", "email": "asha@example.com"} saved
['User', 'LoggedMixin', 'JsonMixin', 'Model', 'object']
email to asha@example.com: order 90312 confirmed
SMS to +91-98xxxxxx: order 90313 confirmed
```

**Common mistakes:**

- ❌ Forgetting `super().__init__(...)`, so the parent's attributes are never set.
- ❌ Deep inheritance hierarchies for code reuse; prefer composition.
- ❌ Subclasses that break the parent's promises (Liskov), e.g. a "read-only list" subclass whose `append` raises.
- ❌ Checking types with `type(x) == Parent` (fails for subclasses); use `isinstance`, or better, rely on duck typing.

### Practice

1. Add a `Triangle(base, height)` shape and a `FakeNotifier` class that `OrderService` could use in tests (it records messages in a list instead of sending them). Show that `OrderService` works with it unchanged.

<details>
<summary><b>Answer</b></summary>

```python
class Triangle(Shape):
    def __init__(self, base, height):
        super().__init__("triangle")
        self.base, self.height = base, height

    def area(self):
        return 0.5 * self.base * self.height

class FakeNotifier:                                     # a test double: no real emails
    def __init__(self):
        self.sent = []
    def send(self, to, text):
        self.sent.append((to, text))
        return "recorded"

print(Triangle(4, 5).describe())
fake = FakeNotifier()
print(OrderService(fake).place("ravi@example.com", "777"), fake.sent)
```

**Output:**

```text
triangle with area 10.00
recorded [('ravi@example.com', 'order 777 confirmed')]
```

Because `OrderService` receives its notifier instead of creating it, tests can pass a fake one: composition makes code **testable**.

</details>

**Learn more:** [Python tutorial: inheritance](https://docs.python.org/3/tutorial/classes.html#inheritance) · [abc module](https://docs.python.org/3/library/abc.html) · [Raymond Hettinger: super() considered super](https://rhettinger.wordpress.com/2011/05/26/super-considered-super/)

---

## 20. Special (Dunder) Methods: Making Objects Feel Built-In

### Theory

> **In simple words:** methods with **d**ouble **under**scores on both sides, like `__init__`, `__repr__` or `__add__`, are called **dunder** (or magic) methods. Python calls them for you when you use normal syntax: `print(obj)` calls `obj.__str__()`, `a + b` calls `a.__add__(b)`, `len(x)` calls `x.__len__()`, `for item in x` calls `x.__iter__()`. Defining them lets your own classes behave like built-in types.

**The most useful ones:**

| Syntax / function | Dunder | Notes |
|---|---|---|
| `repr(x)`, shown in the REPL and lists | `__repr__` | Unambiguous, for developers; ideally looks like code that recreates the object |
| `str(x)`, `print(x)` | `__str__` | Friendly text for users; falls back to `__repr__` |
| `x == y`, `x != y` | `__eq__` | Default compares identity; define to compare values |
| `hash(x)`, dict key, set member | `__hash__` | Equal objects must have equal hashes; defining `__eq__` sets `__hash__` to `None` unless you define it |
| `<`, `<=`, `>`, `>=` | `__lt__` … | `functools.total_ordering` fills in the rest from `__eq__` and `__lt__` |
| `+ - * /` … | `__add__`, `__sub__`, `__mul__`, `__truediv__` | `__radd__` for `3 + x`; return `NotImplemented` for unsupported types |
| `len(x)`, `bool(x)` | `__len__`, `__bool__` | `bool` falls back to `len` |
| `x[key]`, `x[key] = v`, `del x[key]` | `__getitem__`, `__setitem__`, `__delitem__` | Slices arrive as `slice` objects |
| `item in x` | `__contains__` | |
| `for item in x` | `__iter__` (and `__next__` on the iterator) | Section [24](#24-iterators-and-generators-producing-values-lazily) |
| `x(...)` | `__call__` | Objects that act like functions |
| `with x:` | `__enter__`, `__exit__` | Section [25](#25-context-managers-with-setup-and-clean-up) |
| `format(x, spec)`, f-strings | `__format__` | Custom format specs |

**Value objects** (money, coordinates, dates) should usually define `__repr__`, `__eq__` and `__hash__` and be immutable, so they can be dict keys and compared safely. Dataclasses generate most of this for you (next section).

**Returning `NotImplemented`** (not raising) from a binary operator tells Python "I don't know how to handle this type"; Python then tries the other operand's reflected method (`__radd__`) and only raises `TypeError` if both decline.

### Python

```python
from functools import total_ordering

@total_ordering
class Money:
    def __init__(self, amount, currency="INR"):
        self.amount, self.currency = round(amount, 2), currency

    def __repr__(self):
        return f"Money({self.amount!r}, {self.currency!r})"

    def __str__(self):
        symbol = {"INR": "₹", "USD": "$"}.get(self.currency, self.currency + " ")
        return f"{symbol}{self.amount:,.2f}"

    def __eq__(self, other):
        if not isinstance(other, Money):
            return NotImplemented
        return (self.amount, self.currency) == (other.amount, other.currency)

    def __hash__(self):
        return hash((self.amount, self.currency))

    def __lt__(self, other):
        if not isinstance(other, Money) or other.currency != self.currency:
            return NotImplemented
        return self.amount < other.amount

    def __add__(self, other):
        if isinstance(other, Money) and other.currency == self.currency:
            return Money(self.amount + other.amount, self.currency)
        return NotImplemented

    def __radd__(self, other):                      # makes sum() work: sum starts with 0 + first item
        return self if other == 0 else NotImplemented

    def __mul__(self, factor):
        return Money(self.amount * factor, self.currency)

prices = [Money(499), Money(1299.5), Money(99)]
print(prices)                                       # lists show repr
print(str(sum(prices)), max(prices), Money(10) * 3)
print(Money(10) == Money(10.0), Money(5) <= Money(7), len({Money(1), Money(1)}))
try:
    Money(1) + Money(1, "USD")
except TypeError as e:
    print("TypeError:", e)
```

**Output:**

```text
[Money(499, 'INR'), Money(1299.5, 'INR'), Money(99, 'INR')]
₹1,897.50 ₹1,299.50 ₹30.00
True True 1
TypeError: unsupported operand type(s) for +: 'Money' and 'Money'
```

```python
class Playlist:
    def __init__(self, name, songs=None):
        self.name, self.songs = name, list(songs or [])

    def __len__(self):
        return len(self.songs)

    def __getitem__(self, index):                    # indexing AND slicing AND iteration
        result = self.songs[index]
        return Playlist(self.name, result) if isinstance(index, slice) else result

    def __contains__(self, song):
        return song.lower() in (s.lower() for s in self.songs)

    def __repr__(self):
        return f"Playlist({self.name!r}, {self.songs!r})"

class Multiplier:
    def __init__(self, factor):
        self.factor = factor
    def __call__(self, x):                           # instances can be called like functions
        return x * self.factor

p = Playlist("road trip", ["Kun Faya Kun", "Ilahi", "Safarnama", "Musafir"])
print(len(p), p[0], p[-1], p[1:3], "ilahi" in p, bool(Playlist("empty")))
for song in p:                                       # works via __getitem__ (or define __iter__)
    print("-", song)
triple = Multiplier(3)
print(triple(7), list(map(triple, [1, 2, 3])))
```

**Output:**

```text
4 Kun Faya Kun Musafir Playlist('road trip', ['Ilahi', 'Safarnama']) True False
- Kun Faya Kun
- Ilahi
- Safarnama
- Musafir
21 [3, 6, 9]
```

**Common mistakes:**

- ❌ Defining `__eq__` without `__hash__` and then using objects as dict keys (`TypeError: unhashable`).
- ❌ Mutable objects with value-based `__hash__` (changing them breaks dicts and sets).
- ❌ Raising `TypeError` in operators instead of returning `NotImplemented`.
- ❌ A `__repr__` that is vague (`<Money object>`); debugging becomes painful.
- ❌ Calling dunders directly (`x.__len__()`); use `len(x)`.

### Practice

1. Write a `Vector(x, y)` class supporting `+`, `-`, multiplication by a number (both `v * 3` and `3 * v`), `abs(v)` (length) and `==`, with a clear `__repr__`.

<details>
<summary><b>Answer</b></summary>

```python
import math

class Vector:
    def __init__(self, x, y):
        self.x, self.y = x, y
    def __repr__(self):
        return f"Vector({self.x}, {self.y})"
    def __add__(self, o):
        return Vector(self.x + o.x, self.y + o.y)
    def __sub__(self, o):
        return Vector(self.x - o.x, self.y - o.y)
    def __mul__(self, k):
        return Vector(self.x * k, self.y * k)
    __rmul__ = __mul__                               # 3 * v uses the same logic
    def __abs__(self):
        return math.hypot(self.x, self.y)
    def __eq__(self, o):
        return isinstance(o, Vector) and (self.x, self.y) == (o.x, o.y)

v, w = Vector(3, 4), Vector(1, 1)
print(v + w, v - w, v * 2, 2 * v, abs(v), v == Vector(3, 4))
```

**Output:**

```text
Vector(4, 5) Vector(2, 3) Vector(6, 8) Vector(6, 8) 5.0 True
```

</details>

**Learn more:** [Python data model](https://docs.python.org/3/reference/datamodel.html) · [Luciano Ramalho, Fluent Python (book)](https://www.fluentpython.com/)

---

## 21. Dataclasses, Enums and __slots__

### Theory

> **In simple words:** many classes are mostly **data**: an order has an id, a customer, a total. Writing `__init__`, `__repr__` and `__eq__` by hand for each is boring and error-prone. `@dataclass` writes them for you from a list of typed fields. An **Enum** is a fixed set of named constants (`Status.PAID`, `Status.SHIPPED`), much safer than passing strings like `"paid"` around.

**`@dataclass` options you'll use:**

| Option | Effect |
|---|---|
| (default) | Generates `__init__`, `__repr__`, `__eq__` from the annotated fields |
| `field(default_factory=list)` | A fresh mutable default per object (never `= []`) |
| `frozen=True` | Immutable (assigning raises); also makes it hashable |
| `order=True` | Generates `<`, `<=`, … comparing fields in order |
| `slots=True` | Uses `__slots__`: less memory, faster attribute access, no accidental new attributes |
| `kw_only=True` | All fields must be passed by name |
| `__post_init__` | A method that runs after `__init__`, for validation or computed fields |

`dataclasses.asdict(obj)` converts to a dict (e.g. for JSON), `replace(obj, field=new)` makes a modified copy (handy with frozen dataclasses).

**Dataclass vs alternatives:**

| Tool | Best for |
|---|---|
| `dataclass` | Your own records and value objects in normal code |
| `NamedTuple` | Lightweight immutable records that must also behave like tuples |
| `TypedDict` | Type hints for plain dicts (e.g. JSON you don't convert) |
| **Pydantic** (third-party) | Data from outside (API requests, config, LLM output): **validates and converts** types at runtime; used by FastAPI (`fastapi.md`) |
| `attrs` (third-party) | The ancestor of dataclasses, with more features |

Dataclasses **don't validate types** at runtime: `Order(total="abc")` is accepted. Validate in `__post_init__`, or use Pydantic at system boundaries.

**Enums:** `class Status(Enum): PAID = "paid"`. Members have `.name` and `.value`, compare by identity (`order.status is Status.PAID`), can be iterated, and catch typos (`Status.PIAD` is an error; the string `"piad"` would silently pass). `StrEnum` members are also strings (easy JSON), `IntEnum` also ints, `Flag` combines with `|`. `auto()` picks values.

**`__slots__`:** declaring `__slots__ = ("x", "y")` stores attributes in fixed slots instead of a per-object dict: useful when you create millions of small objects. `@dataclass(slots=True)` does it for you.

### Python

```python
from dataclasses import asdict, dataclass, field, replace
from enum import Enum, StrEnum, auto

class Status(StrEnum):
    PENDING = auto()                  # value "pending"
    PAID = auto()
    SHIPPED = auto()

@dataclass
class Item:
    sku: str
    price: float
    qty: int = 1

@dataclass
class Order:
    order_id: str
    customer: str
    items: list[Item] = field(default_factory=list)      # a new list per order
    status: Status = Status.PENDING

    def __post_init__(self):
        if not self.order_id.isdigit():
            raise ValueError(f"bad order id {self.order_id!r}")

    @property
    def total(self):
        return sum(i.price * i.qty for i in self.items)

order = Order("90312", "Asha", [Item("P1", 499.0, 2), Item("P9", 99.0)])
print(order)
print(order.total, order.status, order.status == "pending", order == Order("90312", "Asha", [Item("P1", 499.0, 2), Item("P9", 99.0)]))
order.status = Status.PAID
print(asdict(order))
print([s.value for s in Status], Status("shipped").name)
try:
    Order("A-1", "Ravi")
except ValueError as e:
    print("ValueError:", e)
```

**Output:**

```text
Order(order_id='90312', customer='Asha', items=[Item(sku='P1', price=499.0, qty=2), Item(sku='P9', price=99.0, qty=1)], status=<Status.PENDING: 'pending'>)
1097.0 pending True True
{'order_id': '90312', 'customer': 'Asha', 'items': [{'sku': 'P1', 'price': 499.0, 'qty': 2}, {'sku': 'P9', 'price': 99.0, 'qty': 1}], 'status': <Status.PAID: 'paid'>}
['pending', 'paid', 'shipped'] SHIPPED
ValueError: bad order id 'A-1'
```

```python
@dataclass(frozen=True, order=True, slots=True)
class Version:
    major: int
    minor: int
    patch: int = 0

    def __str__(self):
        return f"{self.major}.{self.minor}.{self.patch}"

versions = [Version(3, 14, 7), Version(3, 9), Version(3, 13, 12)]
print(sorted(versions), max(versions))                  # order=True compares fields in order
v = Version(3, 14)
print(str(replace(v, patch=1)), {v: "current"}[Version(3, 14)])   # frozen → hashable
try:
    v.major = 4
except Exception as e:
    print(type(e).__name__, "-", e)

@dataclass(slots=True)
class Pixel:
    x: int
    y: int

px = Pixel(1, 2)
try:
    px.colour = "red"                                   # slots: no attributes outside the declared fields
except AttributeError as e:
    print("AttributeError:", e)

class Colour(Enum):
    RED = 1
    GREEN = 2
try:
    Colour(3)
except ValueError as e:
    print("ValueError:", e)
```

**Output:**

```text
[Version(major=3, minor=9, patch=0), Version(major=3, minor=13, patch=12), Version(major=3, minor=14, patch=7)] 3.14.7
3.14.1 current
FrozenInstanceError - cannot assign to field 'major'
AttributeError: 'Pixel' object has no attribute 'colour' and no __dict__ for setting new attributes
ValueError: 3 is not a valid Colour
```

**Common mistakes:**

- ❌ `items: list = []` in a dataclass (Python raises an error; use `field(default_factory=list)`).
- ❌ Expecting dataclasses to check types (they don't; use `__post_init__` or Pydantic).
- ❌ Passing status strings around instead of an Enum.
- ❌ Mutating objects used as dict keys; use `frozen=True`.

### Practice

1. Create a frozen dataclass `Point(x: float, y: float)` with a method `distance_to(other)`, and an Enum `Direction` with `N, E, S, W` whose values are `(dx, dy)` tuples. Move a point 3 steps East and 2 North using `replace`, and print its distance from the origin.

<details>
<summary><b>Answer</b></summary>

```python
import math

@dataclass(frozen=True)
class Point:
    x: float
    y: float
    def distance_to(self, other):
        return math.hypot(self.x - other.x, self.y - other.y)

class Direction(Enum):
    N = (0, 1)
    E = (1, 0)
    S = (0, -1)
    W = (-1, 0)

def move(p, direction, steps):
    dx, dy = direction.value
    return replace(p, x=p.x + dx * steps, y=p.y + dy * steps)

origin = Point(0, 0)
p = move(move(origin, Direction.E, 3), Direction.N, 2)
print(p, round(p.distance_to(origin), 3))
```

**Output:**

```text
Point(x=3, y=2) 3.606
```

</details>

**Learn more:** [dataclasses](https://docs.python.org/3/library/dataclasses.html) · [enum HOWTO](https://docs.python.org/3/howto/enum.html) · [Pydantic docs](https://docs.pydantic.dev/)

---

## 22. Type Hints and Static Type Checking

### Theory

> **In simple words:** **type hints** are labels saying what kind of values a variable, parameter or return value should hold: `def total(prices: list[float]) -> float:`. Python itself **ignores them when running** your code, but editors use them for autocomplete and **type checkers** (mypy, Pyright, and newer fast ones like `ty` and Pyrefly) read them to find bugs **before** you run anything: passing a string where a number is expected, forgetting that a value can be `None`. On any project bigger than a script, type hints pay for themselves quickly; FastAPI and Pydantic even use them to validate data at runtime.

**The essentials (modern syntax, Python 3.10+):**

| Hint | Meaning |
|---|---|
| `int`, `str`, `float`, `bool`, `bytes` | Basic types (an `int` is accepted where `float` is expected) |
| `list[str]`, `dict[str, int]`, `set[int]`, `tuple[int, str]`, `tuple[int, ...]` | Collections with their item types |
| `str \| None` | A string or `None` (an "optional" value); the checker forces you to handle `None` |
| `int \| str` | Either type (a union) |
| `Callable[[int], str]` | A function taking an int and returning a str (from `collections.abc`) |
| `Iterable[T]`, `Sequence[T]`, `Mapping[K, V]` | Accept anything that behaves like these (more flexible parameters) |
| `Any` | Opt out of checking (use sparingly) |
| `Literal["asc", "desc"]` | Only these exact values |
| `Final`, `ClassVar` | Constants; class-level attributes |
| `TypedDict` | The shape of a dict with known keys (e.g. JSON) |
| `Protocol` | Structural interface: "anything with these methods" |
| `Self` | The current class (for methods returning `self`) |
| `type Alias = ...` (3.12+) | A type alias |
| `def first[T](items: list[T]) -> T:` (3.12+) | A generic function: works for any item type T and keeps it |

**Type narrowing:** after `if value is None: return`, the checker knows `value` isn't `None` below; `isinstance` checks narrow unions too.

**Annotations are lazy in 3.14:** annotations are now evaluated only when something asks for them, so forward references (a class mentioning itself) work without quotes and cost nothing at import time.

**Practical tips:** annotate function signatures first (parameters and returns); accept general types (`Iterable`) and return specific ones (`list`); run the checker in CI; don't fight it with `Any` everywhere. Hints are also documentation that can't go out of date without the checker noticing.

### Python

```python
from collections.abc import Callable, Iterable
from typing import Literal, Protocol, TypedDict

def average(values: Iterable[float]) -> float:
    items = list(values)
    return sum(items) / len(items) if items else 0.0

def find_user(users: dict[str, str], user_id: str) -> str | None:
    return users.get(user_id)

name = find_user({"u1": "Asha"}, "u2")
if name is None:                                 # narrowing: below here, name is a str
    print("not found")
else:
    print(name.upper())

def first[T](items: list[T]) -> T:               # generic (3.12+ syntax)
    return items[0]

type Matrix = list[list[float]]                   # type alias (3.12+)

def apply(fn: Callable[[int], int], values: list[int]) -> list[int]:
    return [fn(v) for v in values]

def sort_by(field: str, order: Literal["asc", "desc"] = "asc") -> str:
    return f"ORDER BY {field} {order.upper()}"

class OrderDict(TypedDict):
    id: str
    total: float

class SupportsArea(Protocol):
    def area(self) -> float: ...

class Square:                                     # doesn't inherit from SupportsArea
    def __init__(self, side: float) -> None:
        self.side = side
    def area(self) -> float:
        return self.side ** 2

def total_area(shapes: Iterable[SupportsArea]) -> float:
    return sum(s.area() for s in shapes)

order: OrderDict = {"id": "90312", "total": 998.0}
grid: Matrix = [[1.0, 2.0], [3.0, 4.0]]
print(average([90, 72.5]), first(["a", "b"]), apply(lambda x: x * 2, [1, 2]))
print(sort_by("price", "desc"), order["total"], total_area([Square(2), Square(3)]), grid[1][0])
print(average.__annotations__)
```

**Output:**

```text
not found
81.25 a [2, 4]
ORDER BY price DESC 998.0 13 3.0
{'values': collections.abc.Iterable[float], 'return': <class 'float'>}
```

Hints aren't enforced at runtime, which is exactly why a checker is useful. Here we run **mypy** (`uv add --dev mypy`, then `uv run mypy file.py`) on a file with two bugs:

```python
import subprocess, sys
from pathlib import Path

Path("typed_demo.py").write_text('''
def find_user(users: dict[str, str], user_id: str) -> str | None:
    return users.get(user_id)

def greeting(user_id: str) -> str:
    name = find_user({"u1": "Asha"}, user_id)
    return "Hello " + name.upper()          # bug 1: name may be None

def total(prices: list[float]) -> float:
    return sum(prices)

print(total(["499", "99"]))                # bug 2: strings, not floats
''', encoding="utf-8")
result = subprocess.run([sys.executable, "-m", "mypy", "typed_demo.py"], capture_output=True, text=True)
print(result.stdout.strip())
```

**Output:**

```text
typed_demo.py:7: error: Item "None" of "str | None" has no attribute "upper"  [union-attr]
typed_demo.py:12: error: List item 0 has incompatible type "str"; expected "float"  [list-item]
typed_demo.py:12: error: List item 1 has incompatible type "str"; expected "float"  [list-item]
Found 3 errors in 1 file (checked 1 source file)
```

Both bugs are found without running the program (the second is reported once per bad list item); at runtime, the first would only crash for unknown users (maybe weeks later in production).

**Common mistakes:**

- ❌ Believing hints are checked at runtime (they aren't, except by tools like Pydantic).
- ❌ `def f(x: list = [])`: hints don't fix the mutable-default trap.
- ❌ Old-style `List[str]`, `Optional[str]`, `Union[a, b]` in new code; use `list[str]`, `str | None`, `a | b`.
- ❌ Scattering `Any` and `# type: ignore` until the checker is silent but useless.
- ❌ Over-specific parameter types (`list[int]` when any iterable would do).

### Practice

1. Add type hints to this function and make it handle a missing discount safely:
   `def final_price(price, discounts, code): return price * (1 - discounts[code])`
   where `discounts` maps codes to fractions and `code` may be `None`.

<details>
<summary><b>Answer</b></summary>

```python
def final_price(price: float, discounts: dict[str, float], code: str | None = None) -> float:
    if code is None or code not in discounts:
        return price
    return round(price * (1 - discounts[code]), 2)

codes = {"DIWALI": 0.2}
print(final_price(1000, codes, "DIWALI"), final_price(1000, codes), final_price(1000, codes, "XYZ"))
```

**Output:**

```text
800.0 1000 1000
```

</details>

---

### ✅ Part 3 checkpoint

Without looking, can you:

- [ ] Handle errors with `try`/`except`/`else`/`finally`, raise your own exceptions, and explain why bare `except:` is dangerous?
- [ ] Read and write text, JSON and CSV files safely with `pathlib` and `with`?
- [ ] Import modules, explain `if __name__ == "__main__"`, and set up a project with uv (or venv + pip) and `pyproject.toml`?
- [ ] Reach for `Counter`, `defaultdict`, `deque`, `itertools`, `@cache` and time-zone-aware datetimes?
- [ ] Write classes with `__init__`, properties, class/static methods, inheritance with `super()`, and choose composition when it fits?
- [ ] Implement `__repr__`, `__eq__`/`__hash__` and operators, use dataclasses and Enums, and add type hints a checker can use?

**Learn more:** [typing module](https://docs.python.org/3/library/typing.html) · [mypy cheat sheet](https://mypy.readthedocs.io/en/stable/cheat_sheet_py3.html) · [PEP 695: type parameter syntax](https://peps.python.org/pep-0695/) · [PEP 649: deferred annotations (3.14)](https://peps.python.org/pep-0649/)

---

# Part 4 — Moderate: Pythonic Techniques, Testing and Logging

> **Goal:** Use decorators, generators, context managers and regular expressions; write idiomatic, tested, well-logged code.  
> **You need:** Parts 1–3.

---

## 23. Closures and Decorators

### Theory

> **In simple words:** a **closure** is a function that **remembers** variables from the place where it was created, even after that place has finished running (like `make_counter` in Section [13](#13-scope-lambda-and-functional-tools-map-filter-sorted-reduce)). A **decorator** uses this to **wrap** a function with extra behaviour (timing, logging, caching, retrying, checking permissions) without changing the function's own code. Writing `@timer` above `def f` is shorthand for `f = timer(f)`.

**How a decorator works, step by step:**

1. A decorator is a function that **takes a function** and **returns a new function** (the wrapper).
2. The wrapper usually accepts `*args, **kwargs`, does something before, **calls the original**, does something after, and returns the original's result.
3. `@decorator` above a `def` replaces the function with the wrapper.
4. `@functools.wraps(func)` on the wrapper copies the original's name, docstring and signature, so debugging, `help()` and frameworks still see the real function. **Always use it.**

**Decorators with arguments** (`@retry(times=3)`) need **three levels**: an outer function that takes the arguments and returns the actual decorator, which takes the function and returns the wrapper.

**Stacking:** `@a` above `@b` above `def f` means `f = a(b(f))`: the decorator closest to the function wraps first; `a`'s code runs outermost.

**Where you've seen decorators:** `@property`, `@classmethod`, `@staticmethod`, `@dataclass` (a class decorator), `@cache`, `@app.get("/items")` in FastAPI, `@pytest.fixture`, `@tool` in LangChain.

**The late-binding trap with closures:** closures remember **variables**, not values. Functions created in a loop all see the loop variable's **final** value. Fix with a default argument (`lambda i=i: i`) or `functools.partial`.

### Python

```python
import functools
import time

def timer(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)               # call the original
        elapsed = time.perf_counter() - start
        print(f"[timer] {func.__name__} took {'<1' if elapsed < 0.001 else round(elapsed * 1000)} ms")
        return result
    return wrapper

@timer                                               # same as: slow_sum = timer(slow_sum)
def slow_sum(n):
    """Add the numbers 0..n-1."""
    return sum(range(n))

print(slow_sum(1000), slow_sum.__name__, slow_sum.__doc__)

def retry(times=3, exceptions=(Exception,)):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(1, times + 1):
                try:
                    return func(*args, **kwargs)
                except exceptions as e:
                    print(f"[retry] attempt {attempt} failed: {e}")
                    if attempt == times:
                        raise
        return wrapper
    return decorator

calls = {"n": 0}

@retry(times=3, exceptions=(ConnectionError,))
def flaky_fetch():
    calls["n"] += 1
    if calls["n"] < 3:
        raise ConnectionError("network blip")
    return "data"

print(flaky_fetch())
```

**Output:**

```text
[timer] slow_sum took <1 ms
499500 slow_sum Add the numbers 0..n-1.
[retry] attempt 1 failed: network blip
[retry] attempt 2 failed: network blip
data
```

```python
def require_role(role):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(user, *args, **kwargs):
            if role not in user.get("roles", []):
                raise PermissionError(f"{user['name']} needs role {role!r}")
            return func(user, *args, **kwargs)
        return wrapper
    return decorator

def log_calls(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        print(f"[log] {func.__name__}{args}")
        return func(*args, **kwargs)
    return wrapper

@log_calls                                            # outermost: runs first
@require_role("admin")
def delete_order(user, order_id):
    return f"order {order_id} deleted by {user['name']}"

print(delete_order({"name": "Asha", "roles": ["admin"]}, "90312"))
try:
    delete_order({"name": "Ravi", "roles": []}, "90313")
except PermissionError as e:
    print("PermissionError:", e)

late = [lambda: i for i in range(3)]                  # all three see the final i
fixed = [lambda i=i: i for i in range(3)]             # default argument captures each value
print([f() for f in late], [f() for f in fixed])
```

**Output:**

```text
[log] delete_order({'name': 'Asha', 'roles': ['admin']}, '90312')
order 90312 deleted by Asha
[log] delete_order({'name': 'Ravi', 'roles': []}, '90313')
PermissionError: Ravi needs role 'admin'
[2, 2, 2] [0, 1, 2]
```

**Common mistakes:**

- ❌ Forgetting `@functools.wraps` (the function's name and docstring become `wrapper`'s).
- ❌ Forgetting to `return` the original function's result inside the wrapper.
- ❌ Wrappers that only accept fixed arguments instead of `*args, **kwargs`.
- ❌ `@retry` instead of `@retry()` for a decorator that takes arguments (or vice versa).
- ❌ Closures in loops capturing the variable, not its value.

### Practice

1. Write a decorator `count_calls` that counts how many times a function is called and exposes the count as `func.calls`. Apply it to a `greet(name)` function and call it three times.

<details>
<summary><b>Answer</b></summary>

```python
def count_calls(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        wrapper.calls += 1
        return func(*args, **kwargs)
    wrapper.calls = 0                                  # functions are objects: they can have attributes
    return wrapper

@count_calls
def greet(name):
    return f"hi {name}"

for n in ["Asha", "Ravi", "Meera"]:
    greet(n)
print(greet.calls, greet.__name__)
```

**Output:**

```text
3 greet
```

</details>

**Learn more:** [Real Python: primer on decorators](https://realpython.com/primer-on-python-decorators/) · [functools.wraps](https://docs.python.org/3/library/functools.html#functools.wraps) · [PEP 318: decorators](https://peps.python.org/pep-0318/)

---

## 24. Iterators and Generators: Producing Values Lazily

### Theory

> **In simple words:** an **iterator** hands out values **one at a time**, on request, instead of building a whole list first. A **generator** is the easiest way to write one: a function that uses `yield` instead of `return`. Each `yield` produces one value and **pauses** the function; the next request resumes it right where it stopped. This lets you process a 50 GB log file, an endless stream of events, or a paginated API with almost no memory.

**Iterable vs iterator:**

- An **iterable** is anything you can loop over: lists, strings, dicts, files, ranges. It has `__iter__`, which returns a fresh iterator.
- An **iterator** remembers its position and has `__next__`, which returns the next value or raises `StopIteration` when done. An iterator is **used up** after one pass.
- `for x in thing:` is really: `it = iter(thing)`, then `next(it)` repeatedly until `StopIteration`.

**Generators:**

| Form | Example |
|---|---|
| Generator function | `def count_up(n): i = 0; while i < n: yield i; i += 1` |
| Generator expression | `(line.strip() for line in f)`: like a list comprehension with `()`, lazy |
| Delegation | `yield from other_generator` passes through all its values |

Calling a generator function **doesn't run it**: it returns a generator object; code runs only as values are requested.

**Why lazy is powerful:**

- **Memory:** a list of 10 million items uses hundreds of MB; a generator producing them uses a few hundred bytes.
- **Pipelines:** chain small generators (read lines → parse → filter → transform); each item flows through the whole pipeline before the next is read, like a factory conveyor.
- **Infinite sequences:** ids, retries with back-off, streams of events; take what you need with `itertools.islice`.
- **Early exit:** `any(...)`, `next(...)` stop as soon as they have an answer.

**Trade-offs:** you can iterate a generator only once, can't index it or ask its `len`, and debugging is less direct. If you need the data several times, make a list.

**Advanced (rarely needed):** `gen.send(value)` sends a value into a paused generator; `gen.close()`; a generator's `return value` becomes `StopIteration.value` (and the result of `yield from`). This machinery is what `async`/`await` grew out of (Section [33](#33-asyncio-async-and-await)).

### Python

```python
numbers = [10, 20, 30]
it = iter(numbers)
print(next(it), next(it), next(it))
try:
    next(it)
except StopIteration:
    print("StopIteration: the iterator is used up")

def countdown(n):
    print("  (generator started)")
    while n > 0:
        yield n                           # produce a value and pause here
        n -= 1
    print("  (generator finished)")

gen = countdown(3)                        # nothing runs yet
print(type(gen).__name__)
for value in gen:
    print(value)
print(list(gen))                          # already exhausted: empty

import sys
squares_list = [n * n for n in range(1_000_000)]
squares_gen = (n * n for n in range(1_000_000))
print(f"list: {sys.getsizeof(squares_list):,} bytes, generator: {sys.getsizeof(squares_gen)} bytes")
print(sum(squares_gen))
```

**Output:**

```text
10 20 30
StopIteration: the iterator is used up
generator
  (generator started)
3
2
1
  (generator finished)
[]
list: 8,448,728 bytes, generator: 208 bytes
333332833333500000
```

A **pipeline** over a (simulated) log file: each stage is a generator, and only one line is in memory at a time.

```python
from itertools import count, islice
from pathlib import Path

Path("app.log").write_text(
    "INFO start\nERROR db timeout\nINFO request /home\nERROR payment failed code=402\nINFO stop\n", encoding="utf-8")

def read_lines(path):
    with open(path, encoding="utf-8") as f:
        for line in f:
            yield line.rstrip("\n")

def only_errors(lines):
    return (line for line in lines if line.startswith("ERROR"))

def messages(lines):
    for line in lines:
        yield line.split(" ", 1)[1]

for msg in messages(only_errors(read_lines("app.log"))):
    print(msg)

def ids(prefix):
    for n in count(1):                    # infinite
        yield f"{prefix}-{n:04d}"

print(list(islice(ids("ORD"), 3)))

def paginate(total_items, page_size):
    for start in range(0, total_items, page_size):
        yield list(range(start, min(start + page_size, total_items)))   # e.g. one API page

def all_items(total, size):
    for page in paginate(total, size):
        yield from page                   # flatten pages into single items

print(list(all_items(7, 3)), next(n for n in all_items(100, 10) if n % 17 == 0 and n > 0))
```

**Output:**

```text
db timeout
payment failed code=402
['ORD-0001', 'ORD-0002', 'ORD-0003']
[0, 1, 2, 3, 4, 5, 6] 17
```

**Common mistakes:**

- ❌ Iterating a generator twice and getting nothing the second time.
- ❌ `len(gen)` or `gen[0]` (not supported); convert to a list if you need that.
- ❌ Building a huge list just to loop over it once.
- ❌ Forgetting that code in a generator function doesn't run until iteration starts (errors appear later than you expect).
- ❌ Returning a generator from inside a `with open(...)` block in a regular function (the file is closed before iteration); make the whole function a generator as `read_lines` does.

### Practice

1. Write a generator `chunks(items, size)` that yields lists of `size` items (the last may be shorter) without using `itertools.batched`, and a generator `running_average(values)` that yields the average so far after each value.

<details>
<summary><b>Answer</b></summary>

```python
def chunks(items, size):
    batch = []
    for item in items:
        batch.append(item)
        if len(batch) == size:
            yield batch
            batch = []
    if batch:
        yield batch

def running_average(values):
    total = 0
    for i, v in enumerate(values, start=1):
        total += v
        yield total / i

print(list(chunks(range(7), 3)), list(running_average([10, 20, 60])))
```

**Output:**

```text
[[0, 1, 2], [3, 4, 5], [6]] [10.0, 15.0, 30.0]
```

</details>

**Learn more:** [Python docs: generators](https://docs.python.org/3/howto/functional.html#generators) · [David Beazley: generator tricks for systems programmers](https://www.dabeaz.com/generators/) · [itertools](https://docs.python.org/3/library/itertools.html)

---

## 25. Context Managers: with, Setup and Clean-Up

### Theory

> **In simple words:** many resources must be **released** after use: files closed, locks unlocked, database transactions committed or rolled back, temporary folders deleted. A **context manager** pairs the setup with the clean-up, and the `with` statement guarantees the clean-up runs **even if an error happens** inside the block. You've used one already: `with open(path) as f:` closes the file for you.

**How `with` works:**

```text
with manager as value:      1. calls manager.__enter__(); its return value goes into `value`
    block                   2. runs the block
                            3. calls manager.__exit__(exc_type, exc, traceback), ALWAYS
```

If `__exit__` returns `True`, an exception from the block is **suppressed**; otherwise it continues outwards. Most context managers return `False`/`None`.

**Two ways to write one:**

| Way | When |
|---|---|
| A class with `__enter__` and `__exit__` | Reusable objects with state (a connection, a timer object) |
| `@contextlib.contextmanager` on a generator | Quick ones: code before `yield` is setup, the yielded value is the `as` target, code after `yield` (in `finally`) is clean-up |

**Useful ready-made ones:** `open`, `threading.Lock()`, `sqlite3` connections (commit/rollback), `tempfile.TemporaryDirectory()`, `contextlib.suppress(FileNotFoundError)` (ignore one specific error), `contextlib.chdir(path)`, `contextlib.redirect_stdout`, `contextlib.ExitStack` (manage a variable number of resources), `decimal.localcontext()`. Several managers can share one `with` using brackets:

```text
with (open("in.txt") as src,
      open("out.txt", "w") as dst):
    ...
```

`async with` is the asynchronous version (Section [33](#33-asyncio-async-and-await)).

### Python

```python
import time
from contextlib import contextmanager, suppress
from pathlib import Path

class Timer:
    def __enter__(self):
        self.start = time.perf_counter()
        return self                                   # becomes the `as` value
    def __exit__(self, exc_type, exc, tb):
        self.elapsed = time.perf_counter() - self.start
        print(f"[timer] block finished ({'with ' + exc_type.__name__ if exc_type else 'no error'})")
        return False                                  # don't hide exceptions

with Timer() as t:
    total = sum(range(100_000))
print(total, t.elapsed < 1)

try:
    with Timer():
        1 / 0
except ZeroDivisionError:
    print("the error still reached us, and the clean-up ran first")

@contextmanager
def transaction(log):
    log.append("BEGIN")
    try:
        yield log                                     # the with-block runs here
        log.append("COMMIT")
    except Exception:
        log.append("ROLLBACK")
        raise
    finally:
        log.append("release connection")

log = []
with transaction(log):
    log.append("insert order")
try:
    with transaction(log):
        log.append("insert payment")
        raise ValueError("card declined")
except ValueError:
    pass
print(log)

with suppress(FileNotFoundError):                     # ignore exactly this error
    Path("does-not-exist.tmp").unlink()
print("carried on")
```

**Output:**

```text
[timer] block finished (no error)
4999950000 True
[timer] block finished (with ZeroDivisionError)
the error still reached us, and the clean-up ran first
['BEGIN', 'insert order', 'COMMIT', 'release connection', 'BEGIN', 'insert payment', 'ROLLBACK', 'release connection']
carried on
```

**Common mistakes:**

- ❌ Opening files, locks or connections without `with` and forgetting to close them on errors.
- ❌ A `@contextmanager` generator without `try`/`finally` around `yield` (clean-up is skipped when the block raises).
- ❌ Returning `True` from `__exit__` by accident, silently swallowing errors.
- ❌ Using the resource after the `with` block has closed it.

### Practice

1. Write a context manager `temporary_file(text)` with `@contextmanager` that writes `text` to a new file, yields its path, and deletes the file afterwards. Show that the file exists inside the block and not after.

<details>
<summary><b>Answer</b></summary>

```python
@contextmanager
def temporary_file(text, name="tmp_demo.txt"):
    path = Path(name)
    path.write_text(text, encoding="utf-8")
    try:
        yield path
    finally:
        path.unlink(missing_ok=True)

with temporary_file("hello") as p:
    print(p.exists(), p.read_text(encoding="utf-8"))
print(p.exists())
```

**Output:**

```text
True hello
False
```

</details>

**Learn more:** [contextlib](https://docs.python.org/3/library/contextlib.html) · [The with statement (PEP 343)](https://peps.python.org/pep-0343/)

---

## 26. Regular Expressions

### Theory

> **In simple words:** a **regular expression** (regex) is a small pattern language for finding text that has a certain **shape**: "a word followed by `@` and a domain", "six digits", "a date like 2026-09-25". Python's `re` module searches, extracts, splits and replaces text with such patterns. Regexes are powerful but easy to make unreadable, so use them for shapes, and plain string methods (`in`, `startswith`, `split`) for simple checks.

**Pattern building blocks:**

| Pattern | Matches |
|---|---|
| `abc` | The literal text |
| `.` | Any character except newline |
| `\d`, `\w`, `\s` | A digit, a word character (letter, digit, `_`), whitespace; `\D`, `\W`, `\S` are the opposites |
| `[aeiou]`, `[A-Z0-9]`, `[^0-9]` | One of these characters; a range; NOT these |
| `*`, `+`, `?` | 0 or more, 1 or more, 0 or 1 of the previous item |
| `{3}`, `{2,5}` | Exactly 3; between 2 and 5 |
| `^`, `$`, `\b` | Start of text (or line), end, a word boundary |
| `a\|b` | a or b |
| `( … )` | A group (captured); `(?P<name> … )` a named group; `(?: … )` groups without capturing |
| `*?`, `+?` | **Lazy**: as few as possible (the default is greedy: as many as possible) |

Always write patterns as **raw strings** (`r"\d+"`) so backslashes reach `re` untouched.

**Functions:**

| Function | Returns |
|---|---|
| `re.search(p, s)` | The first match anywhere (a `Match` or `None`) |
| `re.match(p, s)` / `re.fullmatch(p, s)` | A match at the start / of the whole string (validation) |
| `re.findall(p, s)` | A list of all matches (or of the groups, if the pattern has groups) |
| `re.finditer(p, s)` | Match objects one by one (positions, named groups) |
| `re.sub(p, repl, s)` | Replace; `repl` can use `\1` or `\g<name>`, or be a function |
| `re.split(p, s)` | Split on a pattern |
| `re.compile(p, flags)` | A reusable pattern object |

Flags: `re.IGNORECASE`, `re.MULTILINE` (`^`/`$` per line), `re.DOTALL` (`.` matches newlines), `re.VERBOSE` (allow spaces and comments in the pattern for readability).

**Limits:** don't parse HTML, JSON or complex nested formats with regex (use a parser); real email validation is famously hard (check the shape loosely, then send a confirmation email); badly written patterns with nested quantifiers can take exponential time on some inputs ("ReDoS"), a security issue for user-supplied text.

### Python

```python
import re

text = "Order 90312 shipped on 2026-09-21; order 88213 delivered on 2026-09-12. Contact: help@shopkart.example"
print(re.findall(r"\b\d{5}\b", text))                              # five-digit order ids
print(re.findall(r"\d{4}-\d{2}-\d{2}", text))
m = re.search(r"[\w.+-]+@[\w-]+(\.[\w-]+)+", text)
print(m.group(), m.start())

date_pattern = re.compile(r"(?P<year>\d{4})-(?P<month>\d{2})-(?P<day>\d{2})")
for match in date_pattern.finditer(text):
    print(match["day"], match["month"], match["year"])
print(date_pattern.sub(r"\g<day>/\g<month>/\g<year>", text[:40]))   # reformat dates

print(bool(re.fullmatch(r"[6-9]\d{9}", "9876543210")), bool(re.fullmatch(r"[6-9]\d{9}", "12345")))
print(re.split(r"[;,\s]+", "a, b;c  d"))
print(re.sub(r"\s+", " ", "too    many     spaces").strip())

html = "<b>bold</b> and <i>italic</i>"
print(re.findall(r"<.+>", html), re.findall(r"<.+?>", html))       # greedy vs lazy
print(re.sub(r"\d+", lambda m: str(int(m.group()) * 2), "2 apples and 15 pears"))

pan = re.compile(r"""
    ^[A-Z]{5}      # five letters
    \d{4}          # four digits
    [A-Z]$         # one letter
""", re.VERBOSE)
print(bool(pan.match("ABCDE1234F")), bool(pan.match("ABCD1234F")))
```

**Output:**

```text
['90312', '88213']
['2026-09-21', '2026-09-12']
help@shopkart.example 81
21 09 2026
12 09 2026
Order 90312 shipped on 21/09/2026; order
True False
['a', 'b', 'c', 'd']
too many spaces
['<b>bold</b> and <i>italic</i>'] ['<b>', '</b>', '<i>', '</i>']
4 apples and 30 pears
True False
```

**Common mistakes:**

- ❌ Forgetting the `r` prefix (`"\b"` is a backspace character, not a word boundary).
- ❌ `re.match` when you meant `re.search` (match only checks the start).
- ❌ Greedy `.*` swallowing too much; use `.*?` or a precise character class.
- ❌ Using regex to parse HTML/JSON; use a parser.
- ❌ Unreadable one-line patterns; use `re.VERBOSE` with comments and named groups.

### Practice

1. From `log = "2026-09-25 10:01:07 ERROR [payments] code=402 user=u17\n2026-09-25 10:02:11 INFO [auth] user=u3\n2026-09-25 10:05:40 ERROR [orders] code=500 user=u17"`, extract a list of `(time, service, code)` for ERROR lines using one regex with named groups.

<details>
<summary><b>Answer</b></summary>

```python
log = ("2026-09-25 10:01:07 ERROR [payments] code=402 user=u17\n"
       "2026-09-25 10:02:11 INFO [auth] user=u3\n"
       "2026-09-25 10:05:40 ERROR [orders] code=500 user=u17")
pattern = re.compile(r"^\S+ (?P<time>[\d:]+) ERROR \[(?P<service>\w+)\] code=(?P<code>\d+)", re.MULTILINE)
print([(m["time"], m["service"], int(m["code"])) for m in pattern.finditer(log)])
```

**Output:**

```text
[('10:01:07', 'payments', 402), ('10:05:40', 'orders', 500)]
```

</details>

**Learn more:** [Regular expression HOWTO](https://docs.python.org/3/howto/regex.html) · [re module](https://docs.python.org/3/library/re.html) · [regex101 (test patterns online, choose "Python")](https://regex101.com/)

---

## 27. Pythonic Code: Idioms, PEP 8 and Linters

### Theory

> **In simple words:** "Pythonic" code uses the language the way it was designed to be used: short, clear, and obvious to other Python programmers. Code is read far more often than it's written, so a consistent **style** (PEP 8) and a few common **idioms** make a big difference. In 2026 you don't format code by hand: a **formatter** (`ruff format`, or Black) lays it out, and a **linter** (`ruff check`) points out bugs and non-idiomatic code in milliseconds.

**The Zen of Python** (`import this`) in practice: beautiful is better than ugly · explicit is better than implicit · simple is better than complex · flat is better than nested · readability counts · errors should never pass silently · there should be one obvious way to do it.

**PEP 8 essentials:** 4-space indentation · `snake_case` for functions and variables, `PascalCase` for classes, `UPPER_CASE` for constants · lines around 88–100 characters (the formatter decides) · two blank lines between top-level definitions · imports at the top, grouped standard library / third-party / local · spaces around operators (`x = a + b`), not inside brackets · `is None`, not `== None` · no bare `except:`.

**Idioms that separate beginners from fluent Python programmers:**

| Instead of | Write |
|---|---|
| `for i in range(len(xs)): print(xs[i])` | `for x in xs:` (or `enumerate(xs)` if you need i) |
| `if len(items) > 0:` / `if flag == True:` | `if items:` / `if flag:` |
| manual swap with a temp variable | `a, b = b, a` |
| `if x == 1 or x == 2 or x == 3:` | `if x in (1, 2, 3):` (a set for many values) |
| building a list with a loop and `append` | a comprehension |
| `d[k] if k in d else default` | `d.get(k, default)` |
| `"" + a + ", " + b` | f-strings, `", ".join(parts)` |
| `f = open(...); ...; f.close()` | `with open(...) as f:` |
| index-juggling over two lists | `zip(a, b)` |
| checking before acting (race-prone) | EAFP: `try`/`except` |
| `result = []` ... `return result` for huge data | a generator with `yield` |
| type checks with `type(x) == list` | `isinstance(x, list)`, or duck typing |
| `x = x if x is not None else default` | `x = default if x is None else x` (clear), or `x or default` when 0/"" can't occur |
| a long if/elif chain on one value | a dict lookup or `match` |

**The walrus operator `:=`** assigns inside an expression: `while (line := f.readline()):` or `if (m := re.search(p, s)):`. Use it when it removes duplication, not to be clever.

**Tooling (2026 default):** `ruff format` (formatting) and `ruff check --fix` (hundreds of lint rules: unused imports, bugs, modernisation, security) configured in `pyproject.toml`, a type checker (mypy, Pyright or ty), and `pre-commit` hooks so everything runs before each commit.

### Python

```python
data = {"Asha": [91, 85], "Ravi": [], "Meera": [78]}

# Non-Pythonic
names = list(data.keys())
result = []
for i in range(len(names)):
    if len(data[names[i]]) > 0:
        result.append(names[i] + ": " + str(sum(data[names[i]]) / len(data[names[i]])))
print(result)

# Pythonic
print([f"{name}: {sum(s) / len(s)}" for name, s in data.items() if s])

import re
for line in ["no digits here", "order 90312 shipped"]:
    if (m := re.search(r"\d+", line)):              # walrus: assign and test in one step
        print("found", m.group())

ROUTES = {"GET": "read", "POST": "create", "DELETE": "remove"}   # dict dispatch instead of if/elif
print(ROUTES.get("POST", "unsupported"), ROUTES.get("PATCH", "unsupported"))
```

**Output:**

```text
['Asha: 88.0', 'Meera: 78.0']
['Asha: 88.0', 'Meera: 78.0']
found 90312
create unsupported
```

Running the linter on some un-Pythonic code (`ruff check` with a few extra rule sets enabled):

```python
import subprocess, sys
from pathlib import Path

Path("messy.py").write_text('''import os, sys
def Process(items=[]):
    result = []
    for i in range(len(items)):
        if items[i] == None:
            continue
        result.append(items[i])
    try:
        return result
    except:
        pass
''', encoding="utf-8")
out = subprocess.run([sys.executable, "-m", "ruff", "check", "--select", "E,F,B,N,SIM", "--output-format", "concise", "--no-cache", "messy.py"],
                     capture_output=True, text=True).stdout
print(out.strip())
```

**Output:**

```text
messy.py:1:1: E401 [*] Multiple imports on one line
messy.py:1:8: F401 [*] `os` imported but unused
messy.py:1:12: F401 [*] `sys` imported but unused
messy.py:2:5: N802 Function name `Process` should be lowercase
messy.py:2:19: B006 Do not use mutable data structures for argument defaults
messy.py:5:24: E711 Comparison to `None` should be `cond is None`
messy.py:10:5: E722 Do not use bare `except`
Found 7 errors.
[*] 3 fixable with the `--fix` option (2 hidden fixes can be enabled with the `--unsafe-fixes` option).
```

Each message names a rule (look it up on the ruff website), the line and the problem: unused imports, a function name that isn't snake_case, the mutable default, `== None`, and the bare `except`. Many can be fixed automatically with `ruff check --fix`.

**Common mistakes:**

- ❌ Arguing about formatting in code review; let the formatter decide.
- ❌ Clever one-liners (nested comprehensions, chained walruses) that nobody can read.
- ❌ Ignoring linter warnings instead of fixing or consciously disabling a rule.
- ❌ Applying Java habits (getters/setters everywhere, deep class hierarchies, `i` counters).

### Practice

1. Rewrite this Pythonically: 

   ```text
   total = 0
   for i in range(len(prices)):
       if prices[i] != None and prices[i] > 100:
           total = total + prices[i]
   ```

<details>
<summary><b>Answer</b></summary>

```python
prices = [120, None, 80, 300, None, 150]
total = sum(p for p in prices if p is not None and p > 100)
print(total)
```

**Output:**

```text
570
```

</details>

**Learn more:** [PEP 8](https://peps.python.org/pep-0008/) · [PEP 20: the Zen of Python](https://peps.python.org/pep-0020/) · [Ruff rules](https://docs.astral.sh/ruff/rules/) · [Raymond Hettinger: transforming code into beautiful, idiomatic Python (talk)](https://www.youtube.com/watch?v=OSGv2VnC0go)

---

## 28. Testing with pytest

### Theory

> **In simple words:** a **test** is a small piece of code that runs your code with known inputs and **checks** the result: "`add_tax(100)` should be `118.0`". You write tests once, and then run all of them in seconds after every change, so you find out immediately if something broke. **pytest** is the standard Python testing tool: tests are plain functions whose names start with `test_`, and checks are plain `assert` statements.

**Why test?** Confidence to change code (refactoring without fear), fewer bugs reaching users, living documentation of how code should behave, and better design (code that's easy to test is usually well structured). Tests are also how AI coding assistants and CI (continuous integration) know whether a change works.

**pytest essentials:**

| Feature | Use |
|---|---|
| `def test_something(): assert result == expected` | A test; pytest shows both values when it fails |
| `pytest.raises(ValueError, match="...")` | Assert that code raises an error |
| `pytest.approx(0.3)` | Compare floats |
| `@pytest.mark.parametrize("a, b, expected", [...])` | Run one test with many inputs |
| **Fixtures** (`@pytest.fixture`) | Reusable setup (a temp database, a sample object), injected by naming it as a parameter; `yield` inside for teardown |
| Built-in fixtures | `tmp_path` (a temporary folder), `monkeypatch` (replace attributes/env vars), `capsys` (capture printed output) |
| `unittest.mock` (`Mock`, `patch`) | Replace slow or external things (network, time, payment APIs) with fakes |
| Markers, `-k`, `-x`, `--lf` | Select tests, stop at first failure, re-run last failures |
| `pytest-cov` | Measure which lines tests execute (`--cov`) |

**What to test:** normal cases, **edge cases** (empty input, zero, negative, huge, unicode), and error cases. Test **behaviour** (inputs → outputs), not internal details, so you can refactor freely.

**Test types:** **unit** tests (one function, fast, many), **integration** tests (several parts together: code + real database), **end-to-end** tests (the whole app, few). Aim for many fast unit tests and a smaller number of integration tests. **Property-based testing** (the `hypothesis` library) generates hundreds of random inputs to find edge cases you didn't think of.

**Structure:** tests live in a `tests/` folder (`tests/test_pricing.py`), mirroring your package. Arrange (set up) → Act (call) → Assert (check). One behaviour per test, with a descriptive name (`test_discount_never_makes_price_negative`).

**TDD** (test-driven development): write a failing test first, make it pass with the simplest code, then clean up. Useful for well-defined logic and bug fixes (first write a test that reproduces the bug).

### Python

We write a small module and its tests to files, then run pytest on them (normally you'd just type `uv run pytest` in the terminal):

```python
import subprocess, sys
from pathlib import Path

Path("pricing.py").write_text('''
def apply_discount(price: float, percent: float) -> float:
    if not 0 <= percent <= 100:
        raise ValueError("percent must be between 0 and 100")
    return round(price * (1 - percent / 100), 2)

def parse_price(text: str) -> float:
    return float(text.replace("₹", "").replace(",", "").strip())
''', encoding="utf-8")

Path("test_pricing.py").write_text('''
import pytest
from pricing import apply_discount, parse_price

def test_ten_percent_off():
    assert apply_discount(1000, 10) == 900

@pytest.mark.parametrize("price, percent, expected", [
    (100, 0, 100), (100, 100, 0), (200, 25, 150), (0, 30, 0),
])
def test_discount_cases(price, percent, expected):
    assert apply_discount(price, percent) == pytest.approx(expected)

def test_invalid_percent_raises():
    with pytest.raises(ValueError, match="between 0 and 100"):
        apply_discount(100, 120)

@pytest.fixture
def price_file(tmp_path):                       # tmp_path: a fresh temporary folder per test
    path = tmp_path / "prices.txt"
    path.write_text("₹1,499\\n₹ 99\\n", encoding="utf-8")
    return path

def test_parse_prices_from_file(price_file):
    prices = [parse_price(line) for line in price_file.read_text(encoding="utf-8").splitlines()]
    assert prices == [1499.0, 99.0]

def test_parse_price_bug_hunt():
    assert parse_price("1,499.50") == 1499.5
    assert parse_price("Rs. 200") == 200.0      # this will fail: we never handled "Rs."
''', encoding="utf-8")

import re
result = subprocess.run([sys.executable, "-m", "pytest", "-q", "--tb=short", "-p", "no:cacheprovider", "test_pricing.py"],
                        capture_output=True, text=True)
print(re.sub(r" in [\d.]+s", "", result.stdout.strip()))      # drop the timing, which changes every run
```

**Output:**

```text
.......F                                                                 [100%]
=================================== FAILURES ===================================
__________________________ test_parse_price_bug_hunt ___________________________
test_pricing.py:30: in test_parse_price_bug_hunt
    assert parse_price("Rs. 200") == 200.0      # this will fail: we never handled "Rs."
           ^^^^^^^^^^^^^^^^^^^^^^
pricing.py:8: in parse_price
    return float(text.replace("₹", "").replace(",", "").strip())
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
E   ValueError: could not convert string to float: 'Rs. 200'
=========================== short test summary info ============================
FAILED test_pricing.py::test_parse_price_bug_hunt - ValueError: could not con...
1 failed, 7 passed
```

pytest shows exactly which line failed and why: `parse_price` doesn't understand "Rs.". The test found a real gap; fix the function (or decide it's out of scope) and run again.

**Mocking** replaces something external so tests are fast and deterministic. Here a function calls a (pretend) payment API; the test swaps in a `Mock`:

```python
from unittest.mock import Mock

def charge(client, order_id, amount):
    response = client.post("/charges", json={"order": order_id, "amount": amount})
    if response["status"] != "succeeded":
        raise RuntimeError(f"payment failed: {response['status']}")
    return response["id"]

fake_client = Mock()
fake_client.post.return_value = {"status": "succeeded", "id": "ch_123"}
print(charge(fake_client, "90312", 998))
fake_client.post.assert_called_once_with("/charges", json={"order": "90312", "amount": 998})

fake_client.post.return_value = {"status": "declined", "id": None}
try:
    charge(fake_client, "90313", 50)
except RuntimeError as e:
    print("RuntimeError:", e, "| calls made:", fake_client.post.call_count)
```

**Output:**

```text
ch_123
RuntimeError: payment failed: declined | calls made: 2
```

**Common mistakes:**

- ❌ Only testing the happy path; edge cases and errors are where bugs live.
- ❌ Tests that depend on each other, on the current time, on the network or on test order.
- ❌ Mocking so much that the test only checks the mocks, not real behaviour.
- ❌ Chasing 100% coverage with meaningless tests; cover important behaviour.
- ❌ Not running tests automatically in CI on every push.

### Practice

1. Add a test that `apply_discount` never returns a negative price for any `percent` from 0 to 100 (loop over `range(0, 101, 5)` with `price=59.99`), and fix `parse_price` so `"Rs. 200"` works. Run the tests again.

<details>
<summary><b>Answer</b></summary>

```python
source = Path("pricing.py").read_text(encoding="utf-8")
Path("pricing.py").write_text(source.replace(
    'return float(text.replace("₹", "").replace(",", "").strip())',
    'return float(text.replace("₹", "").replace("Rs.", "").replace(",", "").strip())'), encoding="utf-8")
with open("test_pricing.py", "a", encoding="utf-8") as f:
    f.write('''
def test_never_negative():
    for percent in range(0, 101, 5):
        assert apply_discount(59.99, percent) >= 0
''')
result = subprocess.run([sys.executable, "-m", "pytest", "-q", "-p", "no:cacheprovider", "test_pricing.py"],
                        capture_output=True, text=True)
print(re.sub(r" in [\d.]+s", "", result.stdout.strip().splitlines()[-1]))
```

**Output:**

```text
9 passed
```

</details>

**Learn more:** [pytest documentation](https://docs.pytest.org/) · [unittest.mock](https://docs.python.org/3/library/unittest.mock.html) · [Hypothesis (property-based testing)](https://hypothesis.readthedocs.io/) · [Brian Okken, Python Testing with pytest (book)](https://pragprog.com/titles/bopytest2/python-testing-with-pytest-second-edition/)

---

## 29. Logging and Debugging

### Theory

> **In simple words:** `print` is fine while you're experimenting, but real programs use **logging**: messages with a **level** (how serious), a timestamp and the place they came from, which can be switched on or off, filtered, and sent to files or monitoring systems without changing code. **Debugging** is finding out why code doesn't do what you expect: read the traceback, reproduce the problem, inspect values (with a debugger rather than scattered prints), fix, and add a test so it never comes back.

**Log levels** (lowest to highest): `DEBUG` (details for developers) · `INFO` (normal events: "order 90312 created") · `WARNING` (something unexpected, but we carried on) · `ERROR` (an operation failed) · `CRITICAL` (the app may not continue). A logger shows messages at or above its configured level.

**How to use `logging` properly:**

- In each module: `logger = logging.getLogger(__name__)` (names follow your package structure, so you can tune them separately).
- Configure **once**, at the program's entry point: `logging.basicConfig(level=logging.INFO, format=...)` or `logging.config.dictConfig({...})` for real apps. Libraries should never configure logging, only create loggers.
- Use lazy formatting: `logger.info("order %s created", order_id)`: the string is only built if the message is actually shown.
- `logger.exception("...")` inside `except` logs the message **plus the full traceback**.
- Add context (`extra={"order_id": ...}`) and, in production, log **structured JSON** (the `structlog` library, or a JSON formatter) so tools like Grafana Loki, Datadog or CloudWatch can search fields.
- **Never log secrets** (passwords, tokens, card numbers) or unnecessary personal data.

**Debugging toolkit:**

| Tool | Use |
|---|---|
| Read the traceback bottom-up | The last line is the error; the lines above show the call path |
| `breakpoint()` | Pauses the program and opens `pdb`: `n` next line, `s` step into, `c` continue, `p expr` print, `l` list code, `w` where, `q` quit |
| Your editor's debugger (VS Code, PyCharm) | Breakpoints, watches and stepping with a GUI; the most productive option |
| `python -X importtime`, `faulthandler`, `tracemalloc` | Slow imports; crash dumps; memory growth |
| `print(f"{x=}")` | Quick checks (remove them afterwards) |
| `logging` at DEBUG | Permanent, switchable diagnostics |
| Python 3.14: `python -m pdb -p PID` | Attach the debugger to an already running process |

**A debugging method that works:** reproduce reliably → make the failing case as small as possible → form a hypothesis → check it (debugger/logs) → fix the cause, not the symptom → add a regression test. When stuck, explain the problem out loud to someone (or to a rubber duck).

### Python

```python
import logging
import sys

logging.basicConfig(                             # configure once, at program start
    level=logging.INFO,
    format="%(levelname)-8s %(name)s: %(message)s",   # real apps also add %(asctime)s
    stream=sys.stdout,
    force=True,
)
logger = logging.getLogger("shop.orders")

def create_order(order_id, amount):
    logger.debug("validating order %s", order_id)       # hidden: level is INFO
    if amount <= 0:
        logger.warning("order %s has non-positive amount %s", order_id, amount)
        return None
    logger.info("order %s created for ₹%s", order_id, amount)
    return order_id

create_order("90312", 998)
create_order("90313", 0)

logging.getLogger("shop.orders").setLevel(logging.DEBUG)  # turn on details for one module only
create_order("90314", 150)
```

**Output:**

```text
INFO     shop.orders: order 90312 created for ₹998
WARNING  shop.orders: order 90313 has non-positive amount 0
DEBUG    shop.orders: validating order 90314
INFO     shop.orders: order 90314 created for ₹150
```

`logger.exception` inside an `except` block logs the message **and** the traceback. Here it runs as a small script so the traceback shows a real file name:

```python
import subprocess
from pathlib import Path

Path("crash_demo.py").write_text('''import logging, sys
logging.basicConfig(stream=sys.stdout, format="%(levelname)s %(name)s: %(message)s")
log = logging.getLogger("shop.config")

def load_setting(settings, key):
    return settings[key]

try:
    load_setting({"workers": 4}, "timeout")
except KeyError:
    log.exception("setting missing")
''', encoding="utf-8")
output = subprocess.run([sys.executable, "crash_demo.py"], capture_output=True, text=True).stdout
print(output.replace(str(Path.cwd()) + "/", "").strip())        # shorten absolute paths for display
```

**Output:**

```text
ERROR shop.config: setting missing
Traceback (most recent call last):
  File "crash_demo.py", line 9, in <module>
    load_setting({"workers": 4}, "timeout")
    ~~~~~~~~~~~~^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "crash_demo.py", line 6, in load_setting
    return settings[key]
           ~~~~~~~~^^^^^
KeyError: 'timeout'
```

Read it bottom-up: the error (`KeyError: 'timeout'`), the line that raised it (inside `load_setting`), and the call that led there.

**Common mistakes:**

- ❌ `print` for diagnostics in production code.
- ❌ Calling `logging.basicConfig` inside library modules, or configuring logging in many places.
- ❌ f-strings in log calls on hot paths (`logger.debug(f"...")` builds the string even when DEBUG is off).
- ❌ Logging an exception without the traceback (`logger.error(e)` instead of `logger.exception(...)`).
- ❌ Logging passwords, tokens or full card numbers.

### Practice

1. Create a logger `"shop.payments"` that shows only WARNING and above, log one INFO and one WARNING message, and check with `logger.isEnabledFor(logging.INFO)` whether INFO messages are enabled.

<details>
<summary><b>Answer</b></summary>

```python
payments = logging.getLogger("shop.payments")
payments.setLevel(logging.WARNING)
payments.info("charging card")                   # not shown
payments.warning("retrying charge for order %s", "90312")
print(payments.isEnabledFor(logging.INFO))
```

**Output:**

```text
False
```

</details>

---

### ✅ Part 4 checkpoint

Without looking, can you:

- [ ] Write a decorator with `functools.wraps`, and one that takes arguments?
- [ ] Explain iterators vs iterables, write generators with `yield`, and build a lazy pipeline?
- [ ] Write context managers as a class and with `@contextmanager`, with clean-up that survives errors?
- [ ] Use regular expressions with groups, `findall`, `sub` and flags, and know when not to?
- [ ] Write Pythonic code and use ruff to format and lint it?
- [ ] Write pytest tests with parametrize, fixtures and mocks, and log with levels instead of printing?

**Learn more:** [Logging HOWTO](https://docs.python.org/3/howto/logging.html) · [pdb](https://docs.python.org/3/library/pdb.html) · [structlog](https://www.structlog.org/) · [VS Code: Python debugging](https://code.visualstudio.com/docs/python/debugging)

---

# Part 5 — Advanced: Internals, Concurrency, Performance and Real-World Tools

> **Goal:** Understand how Python runs, advanced class machinery, threads, processes, free-threading and asyncio, performance, databases and scripting.  
> **You need:** Parts 1–4.

---

## 30. How Python Runs: Bytecode, Memory and Garbage Collection

![Source code is compiled to bytecode, cached in __pycache__, and executed by the interpreter loop; objects live on the heap with a reference count, and the cycle collector cleans up reference cycles](images/python/05-runtime.svg)

### Theory

> **In simple words:** when you run `python app.py`, Python first **compiles** your code into **bytecode**, a list of simple instructions for a virtual machine, and then the **interpreter** executes those instructions one by one. Every value is an **object** stored in memory with a counter of how many names and containers refer to it; when the count drops to zero, the memory is freed immediately. Knowing this explains many "weird" behaviours: why `is` sometimes works for small numbers, why copying matters, why some code is slow.

**From source to running program (CPython, the standard implementation):**

1. **Parse** the text into a syntax tree, then **compile** it to **bytecode** (you can see it with the `dis` module).
2. Imported modules' bytecode is cached as `.pyc` files in `__pycache__/`, so the next import skips compilation.
3. The **interpreter loop** executes the bytecode. Since 3.11 it **specialises** hot instructions for the types it sees (the "faster CPython" work made 3.11–3.14 considerably faster); 3.13 added an experimental **JIT** compiler, still maturing in 3.14.
4. Other implementations exist: **PyPy** (a JIT, often much faster for pure-Python loops), MicroPython (microcontrollers), GraalPy.

**Memory management:**

- Every object has a **reference count** (`sys.getrefcount`). When it reaches 0, the object is freed right away (that's why files get closed when their last reference disappears, although you should still use `with`).
- **Reference cycles** (A refers to B, B refers to A) never reach zero, so a **cycle garbage collector** (`gc` module) periodically finds and frees unreachable groups; 3.14 made it **incremental**, reducing long pauses.
- Small objects use a special fast allocator; memory freed inside Python isn't always returned to the operating system immediately.

**Identity quirks you can now explain:**

- **Small integer cache:** CPython pre-creates the integers −5 to 256, so `a = 256; b = 256; a is b` is true, but not for 1000 (implementation detail: always use `==`).
- **String interning:** identifier-like strings and compile-time constants may be shared.
- **Mutable vs immutable:** "changing" an int or string creates a new object; lists/dicts are changed in place.

**Copying:** `copy.copy` (shallow: new container, same items) vs `copy.deepcopy` (recursively copies everything). Function arguments are passed **by object reference**: the function gets a reference to the same object, so mutating a list argument is visible to the caller, but rebinding the parameter is not.

**The GIL** (global interpreter lock) and the new **free-threaded** build are explained with concurrency in Section [32](#32-concurrency-threads-processes-the-gil-and-free-threaded-python).

### Python

```python
import dis

def add_tax(price):
    return price * 1.18

dis.dis(add_tax)                              # the bytecode the interpreter runs
```

**Output:**

```text
  3           RESUME                   0

  4           LOAD_FAST_BORROW         0 (price)
              LOAD_CONST               0 (1.18)
              BINARY_OP                5 (*)
              RETURN_VALUE
```

```python
import copy
import gc
import sys

data = []
print(sys.getrefcount(data))                  # includes a temporary reference from the call itself
alias = data
container = [data, data]
print(sys.getrefcount(data))

a, b = 256, 256
c = int("1000"); d = int("1000")               # created at runtime: separate objects
print(a is b, c is d, c == d)

def modify(items, label):
    items.append("added")                     # mutates the caller's list
    label = "changed"                         # rebinds a local name only
    return label

my_list, my_label = [], "original"
modify(my_list, my_label)
print(my_list, my_label)

nested = {"tags": ["a"], "meta": {"v": 1}}
shallow, deep = copy.copy(nested), copy.deepcopy(nested)
nested["tags"].append("b")
print(shallow["tags"], deep["tags"])

class Node:
    def __init__(self):
        self.partner = None

x, y = Node(), Node()
x.partner, y.partner = y, x                   # a reference cycle
del x, y                                      # counts don't reach zero...
print("unreachable objects collected:", gc.collect() >= 2)   # ...the cycle collector frees them
print(sys.getsizeof(0), sys.getsizeof(2 ** 100), sys.getsizeof([]), sys.getsizeof([1, 2, 3]))
```

**Output:**

```text
2
5
True False True
['added'] original
['a', 'b'] ['a']
unreachable objects collected: True
28 40 56 88
```

**Common mistakes:**

- ❌ Relying on `is` for numbers or strings (implementation details); use `==`.
- ❌ Assuming a function can't change your list because "Python passes by value".
- ❌ Expecting `sys.getsizeof` to include the objects a container refers to (it counts only the container).
- ❌ Micro-optimising based on bytecode guesses instead of measuring (Section [34](#34-performance-measuring-and-speeding-up-python)).

### Practice

1. Use `dis` to compare `def f(): return [x * 2 for x in range(3)]` with a version using a `for` loop and `append`. How does each add an item to the list? (Look for `LIST_APPEND` vs a method call.)

<details>
<summary><b>Answer</b></summary>

```python
def with_comprehension():
    return [x * 2 for x in range(3)]

def with_loop():
    out = []
    for x in range(3):
        out.append(x * 2)
    return out

def ops(fn):
    return [i.opname for i in dis.get_instructions(fn)]

print("LIST_APPEND" in ops(with_comprehension), "CALL" in ops(with_loop))
```

**Output:**

```text
True True
```

The comprehension uses a dedicated `LIST_APPEND` instruction, while the loop looks up the `append` method and calls it each time: one reason comprehensions are a bit faster.

</details>

**Learn more:** [dis module](https://docs.python.org/3/library/dis.html) · [gc module](https://docs.python.org/3/library/gc.html) · [What's new in Python 3.14 (incremental GC, JIT)](https://docs.python.org/3/whatsnew/3.14.html) · [Anthony Shaw, CPython Internals (book)](https://realpython.com/products/cpython-internals-book/)

---

## 31. Advanced Classes: Attribute Lookup, Descriptors, Class Hooks and Metaclasses

### Theory

> **In simple words:** when you write `obj.name`, Python follows a precise lookup procedure, and it lets classes hook into every step. **Descriptors** are objects that control what happens when an attribute is read or set (that's how `@property`, methods and Django/SQLAlchemy model fields work). `__init_subclass__` runs code whenever someone subclasses your class (great for plugin registries). **Metaclasses** customise how classes themselves are created; you'll rarely write one, but frameworks use them. You mostly need this section to **understand** libraries and interviews, not for daily code.

**How `obj.attr` is looked up:**

1. Look for `attr` in the class and its parents (following the MRO). If found and it's a **data descriptor** (has `__set__` or `__delete__`, like a property), call its `__get__` and stop.
2. Otherwise look in the object's own `__dict__`; if found, return it.
3. Otherwise, if the class attribute from step 1 is a **non-data descriptor** (only `__get__`, like a plain function), call `__get__` (this is how functions become **bound methods** with `self` filled in); else return the class attribute.
4. Otherwise call `__getattr__(self, name)` if defined; else raise `AttributeError`.

**Hooks:**

| Hook | Called when |
|---|---|
| `__getattr__` | Normal lookup **failed** (safe place for fallbacks, proxies, lazy loading) |
| `__getattribute__` | **Every** attribute access (powerful and easy to break; rarely needed) |
| `__setattr__`, `__delattr__` | Every assignment/deletion |
| `__get__`, `__set__`, `__set_name__` (on a descriptor) | Reading/setting the attribute it manages; `__set_name__` tells the descriptor its attribute name |
| `__init_subclass__(cls, **kw)` | A subclass is defined |
| `__class_getitem__` | `MyClass[int]` (generic syntax) |
| Metaclass `__new__`/`__init__`/`__call__` | A class is created / instantiated |

**Weak references** (`weakref`) refer to an object **without** keeping it alive; useful for caches and observer lists that shouldn't leak memory (`WeakValueDictionary`, `WeakSet`).

**Rule of thumb:** property < descriptor < `__init_subclass__` / class decorator < metaclass. Use the simplest tool that works.

### Python

A reusable **validation descriptor**: one class that manages any number of checked attributes, like model fields in an ORM.

```python
class Positive:
    def __set_name__(self, owner, name):             # called once, with the attribute's name
        self.private = "_" + name

    def __get__(self, obj, objtype=None):
        if obj is None:
            return self                              # accessed on the class itself
        return getattr(obj, self.private)

    def __set__(self, obj, value):
        if value <= 0:
            raise ValueError(f"{self.private[1:]} must be positive, got {value}")
        setattr(obj, self.private, value)

class Product:
    price = Positive()                               # descriptors live on the class
    stock = Positive()

    def __init__(self, name, price, stock):
        self.name, self.price, self.stock = name, price, stock

p = Product("pen", 20, 100)
p.price = 25
print(p.price, p.stock, vars(p))
try:
    p.stock = 0
except ValueError as e:
    print("ValueError:", e)

class Config:
    def __init__(self, **values):
        self._values = values
    def __getattr__(self, name):                     # only called when normal lookup fails
        try:
            return self._values[name]
        except KeyError:
            raise AttributeError(f"no setting {name!r}") from None

cfg = Config(workers=4, debug=False)
print(cfg.workers, cfg.debug)
try:
    cfg.timeout
except AttributeError as e:
    print("AttributeError:", e)
print(type(Product.__init__).__name__, type(p.__init__).__name__)   # functions become bound methods via __get__
```

**Output:**

```text
25 100 {'name': 'pen', '_price': 25, '_stock': 100}
ValueError: stock must be positive, got 0
4 False
AttributeError: no setting 'timeout'
function method
```

`__init_subclass__` builds a **plugin registry** automatically; a tiny **metaclass** shows the same idea one level up; `weakref` avoids keeping objects alive:

```python
class Exporter:
    registry = {}
    def __init_subclass__(cls, fmt, **kwargs):
        super().__init_subclass__(**kwargs)
        Exporter.registry[fmt] = cls                 # every subclass registers itself

class CsvExporter(Exporter, fmt="csv"):
    def export(self, rows): return "\n".join(",".join(map(str, r)) for r in rows)

class JsonExporter(Exporter, fmt="json"):
    def export(self, rows): return str([list(r) for r in rows])

print(sorted(Exporter.registry), Exporter.registry["csv"]().export([(1, 2), (3, 4)]))

class UpperAttrs(type):                              # a metaclass: a class whose instances are classes
    def __new__(mcls, name, bases, namespace):
        renamed = {k if k.startswith("__") else k.upper(): v for k, v in namespace.items()}
        return super().__new__(mcls, name, bases, renamed)

class Settings(metaclass=UpperAttrs):
    timeout = 30

print(Settings.TIMEOUT, hasattr(Settings, "timeout"), type(Settings).__name__)

import weakref

class Session:
    pass

cache = weakref.WeakValueDictionary()
s = Session()
cache["user-1"] = s
print(len(cache))
del s                                                # the only strong reference is gone...
print(len(cache))                                    # ...so the cache entry disappears
```

**Output:**

```text
['csv', 'json'] 1,2
3,4
30 False UpperAttrs
1
0
```

**Common mistakes:**

- ❌ Overriding `__getattribute__` when `__getattr__` is enough (and causing infinite recursion by using `self.x` inside it; use `super().__getattribute__`).
- ❌ Writing a metaclass where a class decorator or `__init_subclass__` would do.
- ❌ Descriptors that store values on the descriptor itself (shared by all instances); store them on `obj`.
- ❌ Forgetting `from None`/`from e` when converting exceptions in `__getattr__`.

### Practice

1. Write a `TypeChecked(expected_type)` descriptor that raises `TypeError` when a value of the wrong type is assigned, and use it for `name: str` and `age: int` on a `Person` class.

<details>
<summary><b>Answer</b></summary>

```python
class TypeChecked:
    def __init__(self, expected_type):
        self.expected_type = expected_type
    def __set_name__(self, owner, name):
        self.name = name
    def __get__(self, obj, objtype=None):
        return self if obj is None else obj.__dict__[self.name]
    def __set__(self, obj, value):
        if not isinstance(value, self.expected_type):
            raise TypeError(f"{self.name} must be {self.expected_type.__name__}, got {type(value).__name__}")
        obj.__dict__[self.name] = value              # same name in the instance dict is fine for a data descriptor

class Person:
    name = TypeChecked(str)
    age = TypeChecked(int)
    def __init__(self, name, age):
        self.name, self.age = name, age

print(vars(Person("Asha", 29)))
try:
    Person("Ravi", "thirty")
except TypeError as e:
    print("TypeError:", e)
```

**Output:**

```text
{'name': 'Asha', 'age': 29}
TypeError: age must be int, got str
```

</details>

**Learn more:** [Descriptor HowTo Guide](https://docs.python.org/3/howto/descriptor.html) · [Python data model: customising class creation](https://docs.python.org/3/reference/datamodel.html#customizing-class-creation) · [weakref](https://docs.python.org/3/library/weakref.html)

---

## 32. Concurrency: Threads, Processes, the GIL and Free-Threaded Python

![Three ways to do several things at once: threads share memory and suit waiting on I/O; processes each have their own interpreter and suit CPU work; asyncio runs many tasks on one thread by switching while they wait](images/python/06-concurrency.svg)

### Theory

> **In simple words:** most programs spend their time either **waiting** (for the network, a database, a disk) or **computing** (maths, parsing, image processing). Doing several things at once helps both, but in different ways. While one download waits, another can start: that's **concurrency**, and **threads** or **asyncio** do it well. Using several CPU cores to compute at the same moment is **parallelism**, and in classic Python that needs **processes**, because of the **GIL**. Python 3.13 introduced, and 3.14 officially supports, a **free-threaded** build without the GIL, where threads can compute in parallel too.

**The GIL (Global Interpreter Lock):** in standard CPython, only one thread executes Python bytecode at a time. Threads still help with I/O, because a thread **releases** the GIL while it waits (for a socket, a file, `time.sleep`) and many C libraries (NumPy, compression, hashing) release it during heavy work. But pure-Python CPU work in several threads runs no faster than in one.

**Free-threaded Python (PEP 703, 779):** a separate build (`python3.14t`, installable with `uv python install 3.14t`) without the GIL. CPU-bound threads then use all cores. Costs: single-threaded code is somewhat slower (roughly 5–10% in 3.14), and C extensions must be updated to support it (most major ones have been). It's officially supported but not yet the default; check your dependencies before relying on it.

**Choosing a tool:**

| Work | Tool | Why |
|---|---|---|
| Many network/file/database waits | `asyncio` (Section [33](#33-asyncio-async-and-await)) or threads (`ThreadPoolExecutor`) | Waiting doesn't need a core; asyncio scales to thousands of connections |
| CPU-heavy pure Python | `ProcessPoolExecutor` / `multiprocessing`, or free-threaded Python | Several interpreters (or no GIL) use several cores |
| Numeric work | NumPy/pandas/Polars (vectorised, releases the GIL), or Numba | Often 10–100× faster than any pure-Python parallelism |
| Several independent interpreters in one process | `concurrent.interpreters` (new in 3.14, PEP 734) | Isolation like processes, lower overhead |
| Big distributed jobs | Celery, RQ, Dask, Ray | Queues and clusters |

**`concurrent.futures`** gives one simple API for both: `with ThreadPoolExecutor(max_workers=8) as ex: results = list(ex.map(fn, items))`, or `ex.submit(fn, x)` returning a **Future** (`.result()` waits for it; `as_completed` yields futures as they finish).

**Shared-state dangers (threads):** threads share memory, so two threads updating the same data can interleave and lose updates (a **race condition**); `counter += 1` is several steps, not one. Protect shared data with a `threading.Lock` (`with lock:`), or better, **avoid sharing**: give each worker its own data and combine results at the end, or pass messages through a `queue.Queue`. With free-threading, races that the GIL used to hide become more likely, so this discipline matters more.

**Processes:** each has its own memory; arguments and results are **pickled** (serialised) to move between them, so pass modest amounts of data, and the worker function must be importable (defined at module top level). Scripts using process pools must protect their entry point with `if __name__ == "__main__":`. Python 3.14 uses the `forkserver` start method on Linux by default (safer than `fork`).

### Python

Threads for **waiting**: five simulated downloads that each take 0.2 s finish in about 0.2 s total, not 1 s.

```python
import threading
import time
from concurrent.futures import ThreadPoolExecutor, as_completed

def download(page):
    time.sleep(0.2)                              # stands in for a network request (releases the GIL)
    return f"page {page}: {len(str(page)) * 100} bytes"

start = time.perf_counter()
with ThreadPoolExecutor(max_workers=5) as pool:
    results = list(pool.map(download, range(1, 6)))    # results come back in input order
elapsed = time.perf_counter() - start
print(results[:2], "...")
print("finished in under 0.5 s:", elapsed < 0.5)

with ThreadPoolExecutor(max_workers=3) as pool:
    futures = {pool.submit(download, p): p for p in [10, 20, 30]}
    done = sorted(f.result() for f in as_completed(futures))   # as_completed: in finishing order
print(done)

counter = 0
lock = threading.Lock()

def add_many(n):
    global counter
    for _ in range(n):
        with lock:                               # only one thread at a time changes counter
            counter += 1

threads = [threading.Thread(target=add_many, args=(50_000,)) for _ in range(4)]
for t in threads:
    t.start()
for t in threads:
    t.join()                                     # wait for all to finish
print("counter:", counter)
```

**Output:**

```text
['page 1: 100 bytes', 'page 2: 100 bytes'] ...
finished in under 0.5 s: True
['page 10: 200 bytes', 'page 20: 200 bytes', 'page 30: 200 bytes']
counter: 200000
```

Processes for **computing**. Process workers must be importable, so this runs as a small script file (the usual way you'd write it anyway):

```python
import subprocess, sys
from pathlib import Path

Path("cpu_work.py").write_text('''
from concurrent.futures import ProcessPoolExecutor

def count_primes(limit):
    count = 0
    for n in range(2, limit):
        if all(n % d for d in range(2, int(n ** 0.5) + 1)):
            count += 1
    return count

if __name__ == "__main__":                     # required: child processes import this file
    limits = [20_000, 40_000, 60_000, 80_000]
    with ProcessPoolExecutor() as pool:
        for limit, primes in zip(limits, pool.map(count_primes, limits)):
            print(f"primes below {limit:,}: {primes:,}")
''', encoding="utf-8")
print(subprocess.run([sys.executable, "cpu_work.py"], capture_output=True, text=True).stdout.strip())
```

**Output:**

```text
primes below 20,000: 2,262
primes below 40,000: 4,203
primes below 60,000: 6,057
primes below 80,000: 7,837
```

**Free-threading in action.** The same CPU-bound function run in 4 threads, on the standard build and on the free-threaded build (`python3.14t`). Timings vary between machines, so this output is from one real run on a 4-core machine rather than a checked example:

<!-- no-run (timing-dependent; output below is from one run on a 4-core machine) -->
```python
import sys, time
from concurrent.futures import ThreadPoolExecutor

def work(n):
    total = 0
    for i in range(n):
        total += i * i
    return total

N = 3_000_000
start = time.perf_counter(); [work(N) for _ in range(4)]; serial = time.perf_counter() - start
start = time.perf_counter()
with ThreadPoolExecutor(4) as ex:
    list(ex.map(work, [N] * 4))
threaded = time.perf_counter() - start
print(f"GIL enabled: {sys._is_gil_enabled()}, speed-up with 4 threads: {serial / threaded:.1f}x")
```

```text
$ python3.14 ft.py
GIL enabled: True, speed-up with 4 threads: 0.9x
$ python3.14t ft.py
GIL enabled: False, speed-up with 4 threads: 3.1x
```

With the GIL, four threads are no faster than one (slightly slower, from switching). Without it, the same code uses the cores: about 3× on 4 cores.

**Common mistakes:**

- ❌ Using threads to speed up pure-Python CPU work on the standard build.
- ❌ Sharing mutable data between threads without locks (or without redesigning to avoid sharing).
- ❌ Starting a process pool without `if __name__ == "__main__":`, or passing huge objects to workers.
- ❌ Creating thousands of threads; use a pool with a sensible `max_workers`, or asyncio.
- ❌ Reaching for parallelism before vectorising with NumPy or fixing the algorithm.

### Practice

1. Use a `ThreadPoolExecutor` to "check" 8 URLs concurrently with a fake `check(url)` that sleeps 0.1 s and returns `(url, len(url) % 3 != 0)`. Print the URLs that failed, in sorted order, and confirm the total time is under 0.5 s.

<details>
<summary><b>Answer</b></summary>

```python
def check(url):
    time.sleep(0.1)
    return url, len(url) % 3 != 0

urls = [f"https://site{i}.example/{'x' * i}" for i in range(8)]
start = time.perf_counter()
with ThreadPoolExecutor(max_workers=8) as pool:
    results = list(pool.map(check, urls))
print(sorted(url for url, ok in results if not ok), time.perf_counter() - start < 0.5)
```

**Output:**

```text
['https://site2.example/xx', 'https://site5.example/xxxxx'] True
```

</details>

**Learn more:** [concurrent.futures](https://docs.python.org/3/library/concurrent.futures.html) · [Python support for free threading](https://docs.python.org/3/howto/free-threading-python.html) · [PEP 703: making the GIL optional](https://peps.python.org/pep-0703/) · [PEP 734: multiple interpreters in the stdlib](https://peps.python.org/pep-0734/)

---

## 33. asyncio: async and await

### Theory

> **In simple words:** `asyncio` lets **one thread** juggle thousands of tasks that spend most of their time **waiting** (web requests, database queries, websockets, LLM API calls). An `async def` function is a **coroutine**: when it reaches `await something_slow`, it **pauses** and hands control back to the **event loop**, which runs another task that's ready. When the slow thing finishes, the paused task continues. It's like a chef who puts water on to boil and chops vegetables meanwhile, instead of staring at the pot.

**The vocabulary:**

| Term | Meaning |
|---|---|
| `async def f():` | Defines a coroutine function; calling `f()` creates a coroutine object but runs nothing yet |
| `await x` | Pause here until `x` (a coroutine, task or future) is done; only allowed inside `async def` |
| Event loop | The scheduler that runs tasks; start it with `asyncio.run(main())` (once, at the top) |
| Task | A coroutine scheduled to run concurrently: `asyncio.create_task(coro)` |
| `asyncio.TaskGroup` (3.11+) | Structured concurrency: start tasks in an `async with` block; it waits for all, and if one fails it cancels the rest and raises an `ExceptionGroup` |
| `asyncio.gather(*coros)` | Run several and collect results in order (older style; `return_exceptions=True` to collect errors) |
| `asyncio.timeout(s)` | Cancel whatever's inside if it takes too long |
| `asyncio.Semaphore(n)` | Allow at most n tasks into a section at once (e.g. limit concurrent API calls) |
| `asyncio.Queue` | Producer/consumer pipelines between tasks |
| `asyncio.to_thread(fn, ...)` | Run a **blocking** function in a thread without freezing the loop |

**The golden rule: never block the event loop.** `time.sleep(1)`, `requests.get(...)`, heavy CPU loops, or a synchronous database driver inside a coroutine freeze **every** task. Use async libraries (`httpx.AsyncClient`, `asyncpg`/`psycopg` async, `aiofiles`, the async clients of LLM SDKs like `anthropic.AsyncAnthropic`), `await asyncio.sleep`, or `asyncio.to_thread` for unavoidable blocking calls.

**asyncio vs threads:** asyncio switches only at `await` points (so fewer race conditions, and it scales to tens of thousands of connections cheaply), but everything in the call chain must be async ("function colouring"). Threads work with any blocking library but cost more memory per task. Web frameworks like FastAPI (`fastapi.md`) are built on asyncio.

**Python 3.14 extras:** `python -m asyncio ps PID` and `pstree PID` show the running tasks of a live program, a big help when debugging stuck async code.

### Python

```python
import asyncio
import time

async def fetch(name, delay):
    await asyncio.sleep(delay)                   # a non-blocking wait (stands in for a network call)
    return f"{name} done after {delay}s"

async def main():
    start = time.perf_counter()
    one_by_one = [await fetch("a", 0.2), await fetch("b", 0.2)]            # sequential: ~0.4 s
    mid = time.perf_counter()
    together = await asyncio.gather(fetch("c", 0.2), fetch("d", 0.2), fetch("e", 0.2))   # concurrent: ~0.2 s
    end = time.perf_counter()
    print(one_by_one, round(mid - start, 1))
    print(together, round(end - mid, 1))

asyncio.run(main())
```

**Output:**

```text
['a done after 0.2s', 'b done after 0.2s'] 0.4
['c done after 0.2s', 'd done after 0.2s', 'e done after 0.2s'] 0.2
```

**Structured concurrency, timeouts and limits:**

```python
async def call_api(i, sem, log):
    async with sem:                               # at most 2 calls in flight
        log.append(f"start {i}")
        await asyncio.sleep(0.05)
        if i == 4:
            raise ValueError(f"request {i} failed")
        return i * 10

async def with_taskgroup():
    sem, log = asyncio.Semaphore(2), []
    try:
        async with asyncio.TaskGroup() as tg:
            tasks = [tg.create_task(call_api(i, sem, log)) for i in range(1, 6)]
    except* ValueError as group:
        print("TaskGroup failed:", [str(e) for e in group.exceptions])
    print("started:", log)
    ok = await asyncio.gather(*(call_api(i, asyncio.Semaphore(2), []) for i in (1, 2, 3)))
    print("gather results:", ok)

async def with_timeout():
    try:
        async with asyncio.timeout(0.1):
            await asyncio.sleep(1)                # too slow
    except TimeoutError:
        print("timed out after 0.1 s")

def blocking_io():
    time.sleep(0.1)                               # a blocking call we can't change
    return "blocking work finished"

async def main():
    await with_taskgroup()
    await with_timeout()
    print(await asyncio.to_thread(blocking_io))  # runs in a thread; the loop stays responsive

asyncio.run(main())
```

**Output:**

```text
TaskGroup failed: ['request 4 failed']
started: ['start 1', 'start 2', 'start 3', 'start 4', 'start 5']
gather results: [10, 20, 30]
timed out after 0.1 s
blocking work finished
```

**Producer/consumer with a queue:** workers process jobs as they arrive.

```python
async def producer(queue, n):
    for i in range(1, n + 1):
        await queue.put(f"job-{i}")
    for _ in range(2):
        await queue.put(None)                     # one "stop" signal per worker

async def worker(name, queue, results):
    while (job := await queue.get()) is not None:
        await asyncio.sleep(0.01)                 # process the job
        results.append((name, job))

async def main():
    queue, results = asyncio.Queue(maxsize=3), []
    await asyncio.gather(producer(queue, 6), worker("w1", queue, results), worker("w2", queue, results))
    print(len(results), "jobs processed:", sorted(job for _, job in results))

asyncio.run(main())
```

**Output:**

```text
6 jobs processed: ['job-1', 'job-2', 'job-3', 'job-4', 'job-5', 'job-6']
```

**Common mistakes:**

- ❌ `time.sleep`, `requests`, or other blocking calls inside `async def` (the whole app freezes).
- ❌ Calling a coroutine without `await` (it never runs; Python warns "coroutine was never awaited").
- ❌ `create_task` without keeping a reference or awaiting it (the task can be garbage-collected or its errors lost); prefer `TaskGroup`.
- ❌ Unlimited concurrency against an external API (use a `Semaphore`; respect rate limits).
- ❌ Calling `asyncio.run` inside code that's already running in an event loop (e.g. Jupyter: use `await main()` there).

### Practice

1. Write `async def fetch_all(urls, limit)` that "fetches" each URL with `asyncio.sleep(0.05)` under a semaphore of size `limit` and returns a dict `{url: len(url)}`. Run it for 6 URLs with `limit=3` and check it takes roughly 0.1 s (two rounds), not 0.3 s.

<details>
<summary><b>Answer</b></summary>

```python
async def fetch_all(urls, limit):
    sem = asyncio.Semaphore(limit)
    async def one(url):
        async with sem:
            await asyncio.sleep(0.05)
            return url, len(url)
    return dict(await asyncio.gather(*(one(u) for u in urls)))

urls = [f"https://api.example/items/{i}" for i in range(6)]
start = time.perf_counter()
result = asyncio.run(fetch_all(urls, limit=3))
elapsed = time.perf_counter() - start
print(len(result), 0.08 < elapsed < 0.25)
```

**Output:**

```text
6 True
```

</details>

**Learn more:** [asyncio documentation](https://docs.python.org/3/library/asyncio.html) · [asyncio.TaskGroup](https://docs.python.org/3/library/asyncio-task.html#task-groups) · [Real Python: async IO in Python](https://realpython.com/async-io-python/) · [httpx async client](https://www.python-httpx.org/async/)

---

## 34. Performance: Measuring and Speeding Up Python

### Theory

> **In simple words:** make it **work**, make it **right**, then make it **fast**, and only where measurements show it's slow. Programmers are famously bad at guessing where time goes. **Profile** first (find the 5% of code that takes 95% of the time), then fix that part, usually with a better algorithm or data structure, or by moving the heavy loop into fast C code (built-ins, NumPy). Micro-tweaks come last.

**Measuring:**

| Tool | Answers |
|---|---|
| `timeit` (`python -m timeit "..."`, or `%timeit` in Jupyter) | How long does this small snippet take? (repeats it many times) |
| `cProfile` + `pstats` (`python -m cProfile -s cumtime app.py`) | Which functions take the time? |
| `py-spy`, `scalene`, `pyinstrument` | Sampling profilers for running programs; scalene also shows memory |
| `tracemalloc`, `memray` | Where is memory allocated? |
| `python -X importtime` | Which imports make start-up slow? |

**Where speed comes from (biggest wins first):**

1. **A better algorithm/data structure:** a set instead of a list for membership (O(1) vs O(n)), a dict index instead of nested loops, sorting once instead of repeatedly, `heapq` for top-k. Turning O(n²) into O(n log n) beats any micro-optimisation (`dsa-python.md`).
2. **Do less work:** cache results (`@cache`), avoid repeated computation inside loops, stop early (`any`, `break`), process lazily (generators).
3. **Push loops into C:** built-ins (`sum`, `max`, `sorted`, `"".join`, `collections.Counter`), comprehensions, `itertools`; for numbers, **NumPy/pandas/Polars** vectorisation (10–100×).
4. **Better I/O:** batch database queries, reuse HTTP connections, concurrency for waiting (Part 5).
5. **Compile or parallelise:** Numba (JIT for numeric loops), Cython, mypyc, Rust extensions via PyO3 (how Polars, pydantic-core and ruff are built), processes or free-threading; newer CPython versions are themselves faster (3.11+ gained 25–60% over 3.10 on many workloads).
6. **Micro-optimisations** (last): local variable lookups, avoiding attribute lookups in tight loops, `str.join` vs `+=`.

**Big-O of common operations:** `list` index/append O(1), `insert(0)`/`pop(0)`/`in` O(n); `dict`/`set` get/set/`in` O(1) average; `deque` appends/pops at both ends O(1); `sort` O(n log n); `heapq.push/pop` O(log n); `bisect` O(log n).

### Python

```python
import timeit

setup = "data = list(range(10_000)); as_set = set(data)"
t_list = timeit.timeit("9_999 in data", setup=setup, number=1_000)
t_set = timeit.timeit("9_999 in as_set", setup=setup, number=1_000)
print("set membership is faster:", t_set < t_list)

def slow_join(n):
    s = ""
    for i in range(n):
        s += str(i)
    return s

def fast_join(n):
    return "".join(map(str, range(n)))

print(slow_join(1000) == fast_join(1000))

def pairs_with_sum_slow(nums, target):          # O(n^2): compare every pair
    return {(a, b) for i, a in enumerate(nums) for b in nums[i + 1:] if a + b == target}

def pairs_with_sum_fast(nums, target):          # O(n): remember what we've seen
    seen, found = set(), set()
    for n in nums:
        if target - n in seen:
            found.add((target - n, n))
        seen.add(n)
    return found

nums = list(range(0, 3000, 3))
print(len(pairs_with_sum_slow(nums, 3000)) == len(pairs_with_sum_fast(nums, 3000)))
slow = timeit.timeit(lambda: pairs_with_sum_slow(nums, 3000), number=3)
fast = timeit.timeit(lambda: pairs_with_sum_fast(nums, 3000), number=3)
print("the O(n) version is more than 10x faster:", slow / fast > 10)
```

**Output:**

```text
set membership is faster: True
True
True
the O(n) version is more than 10x faster: True
```

(Exact timings depend on the machine, so the checks print comparisons instead of seconds.)

**Profiling** shows where the time goes. Here a function spends most of its time in a helper we might not have suspected:

```python
import cProfile
import io
import pstats

def parse(line):
    return [int(x) for x in line.split(",")]

def is_valid(row):
    return all(v >= 0 for v in row) and sorted(row) == sorted(set(row))   # sorting twice: wasteful

def process(lines):
    return sum(1 for line in lines if is_valid(parse(line)))

lines = [",".join(str((i * 7 + j) % 1000) for j in range(50)) for i in range(2000)]
profiler = cProfile.Profile()
profiler.enable()
process(lines)
profiler.disable()
stream = io.StringIO()
stats = pstats.Stats(profiler, stream=stream).sort_stats("tottime")
top = [(func[2], calls) for func, (calls, _, tottime, _, _) in sorted(stats.stats.items(), key=lambda kv: -kv[1][2])[:2]]
print("functions using the most time:", [name for name, _ in top])
print("calls:", {name: calls for name, calls in top if name in ("is_valid", "parse")})
```

**Output:**

```text
functions using the most time: ['is_valid', 'parse']
calls: {'is_valid': 2000, 'parse': 2000}
```

`is_valid` comes first: it sorts every row **twice** and builds a set, just to check for duplicates. `len(set(row)) == len(row)` does the same check with no sorting, so that's the line to fix first. Without the profile you might have optimised `parse` instead.

**Common mistakes:**

- ❌ Optimising without measuring, or optimising code that runs once.
- ❌ Micro-tuning a quadratic algorithm instead of replacing it.
- ❌ Python loops over big numeric arrays instead of NumPy.
- ❌ Building strings with `+=` in large loops; repeated `list.pop(0)`; `in` checks against lists inside loops.
- ❌ Benchmarking with one run, cold caches or a debugger attached.

### Practice

1. `find_duplicates(items)` below is O(n²). Rewrite it in O(n) with a set and check both return the same result on `list(range(2000)) + [5, 10, 5]`.

   ```text
   def find_duplicates(items):
       dups = []
       for i, x in enumerate(items):
           if x in items[i + 1:] and x not in dups:
               dups.append(x)
       return dups
   ```

<details>
<summary><b>Answer</b></summary>

```python
def find_duplicates_slow(items):
    dups = []
    for i, x in enumerate(items):
        if x in items[i + 1:] and x not in dups:
            dups.append(x)
    return dups

def find_duplicates(items):
    seen, dups = set(), []
    for x in items:
        if x in seen and x not in dups:          # dups is tiny here; use a set if it can grow large
            dups.append(x)
        seen.add(x)
    return dups

data = list(range(2000)) + [5, 10, 5]
print(sorted(find_duplicates_slow(data)), sorted(find_duplicates(data)))
```

**Output:**

```text
[5, 10] [5, 10]
```

</details>

**Learn more:** [Python profilers](https://docs.python.org/3/library/profile.html) · [timeit](https://docs.python.org/3/library/timeit.html) · [TimeComplexity wiki](https://wiki.python.org/moin/TimeComplexity) · [Scalene profiler](https://github.com/plasma-umass/scalene)

---

## 35. Working with Databases: sqlite3, psycopg and SQLAlchemy

### Theory

> **In simple words:** a **database** stores data safely and lets many programs query it with **SQL** (`sql-postgresql.md` teaches SQL itself). From Python you **connect**, send SQL with **parameters** (never by gluing strings together), fetch rows, and **commit** changes. Python ships with `sqlite3` (a whole database in one file, perfect for scripts, tests and small apps); for PostgreSQL you use `psycopg` (version 3). Bigger apps often use **SQLAlchemy** to manage connections and map rows to Python objects.

**The DB-API pattern** (the same shape for every driver):

```text
conn = driver.connect(...)            # open a connection (reuse it; use a pool in web apps)
with conn:                            # a transaction: commit on success, rollback on error
    cur = conn.execute(sql, params)   # parameters are sent separately from the SQL
    rows = cur.fetchall()             # or fetchone(), or iterate over cur
conn.close()
```

**SQL injection** is one of the most common and dangerous bugs: if user input is pasted into the SQL text (`f"... WHERE name = '{name}'"`), an attacker can type SQL that changes the query (`' OR '1'='1`, or worse). **Always use placeholders** (`?` in sqlite3, `%s` in psycopg) and pass values separately; the driver sends them as data, never as SQL.

**Transactions:** a group of changes that succeed or fail **together** (move money: debit one account AND credit the other). In `sqlite3`, `with conn:` commits if the block succeeds and rolls back if it raises.

**Useful features:** `executemany` for bulk inserts, `conn.row_factory = sqlite3.Row` to access columns by name, `INSERT ... ON CONFLICT DO UPDATE` (upsert) and `RETURNING` (get generated ids back), indexes for speed (`sql-postgresql.md`).

**Choosing an approach:**

| Approach | Good for |
|---|---|
| Raw SQL with a driver (`sqlite3`, `psycopg`, `asyncpg`) | Full control, performance, reporting queries |
| SQLAlchemy Core | Building SQL safely in Python, connection pooling, multiple databases |
| SQLAlchemy ORM / SQLModel / Django ORM | Apps with many models and relationships; less boilerplate |
| Migrations: Alembic (SQLAlchemy), Django migrations | Changing the schema safely over time |

Whatever you choose: keep SQL in a **repository** layer (functions like `get_order(conn, order_id)`), not scattered through the code, so it's easy to test and change.

### Python

```python
import sqlite3

conn = sqlite3.connect(":memory:")                  # an in-memory database (use a file path to persist)
conn.row_factory = sqlite3.Row                      # rows behave like dicts
conn.execute("""CREATE TABLE products (
    id INTEGER PRIMARY KEY, sku TEXT UNIQUE NOT NULL, name TEXT NOT NULL, price REAL NOT NULL CHECK (price >= 0), stock INTEGER NOT NULL)""")

with conn:                                          # one transaction
    conn.executemany("INSERT INTO products (sku, name, price, stock) VALUES (?, ?, ?, ?)",
                     [("P1", "Pen", 20, 100), ("P2", "Notebook", 60, 40), ("P3", "Bag", 899, 5)])

rows = conn.execute("SELECT sku, name, price FROM products WHERE price < ? ORDER BY price", (100,)).fetchall()
print([dict(r) for r in rows])

row = conn.execute("""INSERT INTO products (sku, name, price, stock) VALUES (?, ?, ?, ?)
                      ON CONFLICT(sku) DO UPDATE SET price = excluded.price, stock = stock + excluded.stock
                      RETURNING id, sku, price, stock""", ("P1", "Pen", 25, 50)).fetchone()
conn.commit()
print(dict(row))

try:
    with conn:                                      # both updates or neither
        conn.execute("UPDATE products SET stock = stock - 3 WHERE sku = 'P3'")
        conn.execute("UPDATE products SET price = -1 WHERE sku = 'P2'")   # violates CHECK → error
except sqlite3.IntegrityError as e:
    print("rolled back:", e)
print(conn.execute("SELECT stock FROM products WHERE sku = 'P3'").fetchone()["stock"])   # still 5
```

**Output:**

```text
[{'sku': 'P1', 'name': 'Pen', 'price': 20.0}, {'sku': 'P2', 'name': 'Notebook', 'price': 60.0}]
{'id': 1, 'sku': 'P1', 'price': 25.0, 'stock': 150}
rolled back: CHECK constraint failed: price >= 0
5
```

**SQL injection, shown safely:**

```python
evil = "x' OR '1'='1"
unsafe_sql = f"SELECT sku FROM products WHERE name = '{evil}'"      # ❌ never build SQL like this
print("unsafe query returned:", [r["sku"] for r in conn.execute(unsafe_sql)])
safe = conn.execute("SELECT sku FROM products WHERE name = ?", (evil,)).fetchall()   # ✅ placeholder
print("safe query returned:", [r["sku"] for r in safe])

def get_product(conn, sku):                          # a tiny repository function
    row = conn.execute("SELECT * FROM products WHERE sku = ?", (sku,)).fetchone()
    return dict(row) if row else None

print(get_product(conn, "P2"), get_product(conn, "P9"))
conn.close()
```

**Output:**

```text
unsafe query returned: ['P1', 'P2', 'P3']
safe query returned: []
{'id': 2, 'sku': 'P2', 'name': 'Notebook', 'price': 60.0, 'stock': 40} None
```

The attacker's text turned the unsafe query into "return every product". With a placeholder, the same text is just a (non-matching) name.

PostgreSQL with `psycopg` 3 looks almost the same (needs a running server, so it's not executed here):

<!-- no-run (needs a PostgreSQL server) -->
```python
import psycopg
from psycopg.rows import dict_row

with psycopg.connect("postgresql://app:secret@localhost:5432/shop", row_factory=dict_row) as conn:
    with conn.transaction():
        conn.execute("UPDATE accounts SET balance = balance - %s WHERE id = %s", (500, 1))
        conn.execute("UPDATE accounts SET balance = balance + %s WHERE id = %s", (500, 2))
    orders = conn.execute("SELECT id, total FROM orders WHERE customer_id = %s ORDER BY id DESC LIMIT 10", (7,)).fetchall()
```

**Common mistakes:**

- ❌ Building SQL with f-strings or `+` from user input (SQL injection).
- ❌ Forgetting to commit (changes vanish) or committing half of a multi-step change.
- ❌ Opening a new connection per query in a web app (use a pool).
- ❌ `SELECT *` everywhere and loading whole tables into Python to filter them (filter in SQL).
- ❌ Running queries in a loop (N+1) instead of one query with `IN` or a join.

### Practice

1. Add an `orders` table (`id`, `sku`, `qty`) to a new in-memory database with the same products, insert three orders, and write one SQL query (with a join) that returns each product's name and total quantity ordered, highest first.

<details>
<summary><b>Answer</b></summary>

```python
conn = sqlite3.connect(":memory:")
conn.executescript("""
CREATE TABLE products (sku TEXT PRIMARY KEY, name TEXT);
CREATE TABLE orders (id INTEGER PRIMARY KEY, sku TEXT REFERENCES products(sku), qty INTEGER);
INSERT INTO products VALUES ('P1', 'Pen'), ('P2', 'Notebook'), ('P3', 'Bag');
INSERT INTO orders (sku, qty) VALUES ('P1', 10), ('P2', 3), ('P1', 5);
""")
query = """SELECT p.name, COALESCE(SUM(o.qty), 0) AS total
           FROM products p LEFT JOIN orders o ON o.sku = p.sku
           GROUP BY p.sku ORDER BY total DESC"""
print(conn.execute(query).fetchall())
```

**Output:**

```text
[('Pen', 15), ('Notebook', 3), ('Bag', 0)]
```

</details>

**Learn more:** [sqlite3](https://docs.python.org/3/library/sqlite3.html) · [psycopg 3](https://www.psycopg.org/psycopg3/docs/) · [SQLAlchemy unified tutorial](https://docs.sqlalchemy.org/en/20/tutorial/) · [OWASP: SQL injection](https://owasp.org/www-community/attacks/SQL_Injection)

---

## 36. Scripting and Automation: CLIs, subprocess, Files and Scheduling

### Theory

> **In simple words:** one of Python's superpowers is **automating boring tasks**: renaming a thousand files, cleaning a folder of CSVs every morning, calling an API and emailing a report, running other programs. A good script is a small program with a clear **command-line interface** (arguments like `--dry-run`), sensible defaults, helpful output, a proper **exit code**, and no secrets written in the code.

**Anatomy of a good script:**

1. A docstring saying what it does.
2. A `main()` function, and `if __name__ == "__main__": sys.exit(main())`.
3. Arguments parsed with `argparse` (standard library) or **Typer**/**Click** (friendlier, third-party).
4. Configuration and secrets from **environment variables** (`os.environ["API_KEY"]`) or a `.env` file, never hard-coded.
5. A `--dry-run` option for anything destructive: show what would happen first.
6. Logging instead of prints for anything that runs unattended.
7. **Exit code** 0 for success, non-zero for failure, so other tools (cron, CI) can tell.

**Running other programs:** `subprocess.run(["git", "status"], capture_output=True, text=True, check=True)`. Pass the command as a **list** (no shell): this avoids **shell injection** when arguments contain user input. `check=True` raises if the command fails; `timeout=` stops hung commands.

**Scheduling:** cron (Linux/macOS: `0 7 * * * /path/.venv/bin/python /path/report.py`), Windows Task Scheduler, systemd timers, GitHub Actions on a schedule, or cloud schedulers. For in-process scheduling, the `schedule` or APScheduler libraries.

**Single-file scripts with dependencies:** PEP 723 lets a script declare its dependencies in a comment block at the top; `uv run script.py` then creates the environment automatically:

```text
# /// script
# requires-python = ">=3.12"
# dependencies = ["httpx", "rich"]
# ///
```

**Handy libraries:** `httpx`/`requests` (HTTP), `rich` (pretty terminal output and progress bars), `typer` (CLIs), `openpyxl`/pandas (Excel), `watchdog` (react to file changes), `playwright` (browser automation), `paramiko`/`fabric` (SSH).

### Python

A small but complete CLI script: organise files in a folder into sub-folders by extension, with `--dry-run`:

```python
import subprocess, sys
from pathlib import Path

Path("organise.py").write_text('''"""Move files into sub-folders named after their extension."""
import argparse
import sys
from pathlib import Path

def parse_args(argv=None):
    parser = argparse.ArgumentParser(description=__doc__)
    parser.add_argument("folder", type=Path, help="folder to organise")
    parser.add_argument("--dry-run", action="store_true", help="only show what would happen")
    return parser.parse_args(argv)

def main(argv=None):
    args = parse_args(argv)
    if not args.folder.is_dir():
        print(f"error: {args.folder} is not a folder", file=sys.stderr)
        return 2
    moved = 0
    for path in sorted(args.folder.iterdir()):
        if path.is_file():
            target = args.folder / (path.suffix.lstrip(".").lower() or "no_extension") / path.name
            print(f"{'would move' if args.dry_run else 'moving'} {path.name} -> {target.parent.name}/")
            if not args.dry_run:
                target.parent.mkdir(exist_ok=True)
                path.rename(target)
            moved += 1
    print(f"{moved} file(s) {'to move' if args.dry_run else 'moved'}")
    return 0

if __name__ == "__main__":
    sys.exit(main())
''', encoding="utf-8")

inbox = Path("inbox")
inbox.mkdir(exist_ok=True)
for name in ["report.PDF", "photo.jpg", "data.csv", "notes", "summary.pdf"]:
    (inbox / name).write_text("x", encoding="utf-8")

def run(*args):
    result = subprocess.run([sys.executable, "organise.py", *args], capture_output=True, text=True)
    print(result.stdout.strip() or result.stderr.strip(), f"(exit code {result.returncode})")

run("inbox", "--dry-run")
run("inbox")
run("missing_folder")
print(sorted(str(p.relative_to(inbox)) for p in inbox.rglob("*") if p.is_file()))
```

**Output:**

```text
would move data.csv -> csv/
would move notes -> no_extension/
would move photo.jpg -> jpg/
would move report.PDF -> pdf/
would move summary.pdf -> pdf/
5 file(s) to move (exit code 0)
moving data.csv -> csv/
moving notes -> no_extension/
moving photo.jpg -> jpg/
moving report.PDF -> pdf/
moving summary.pdf -> pdf/
5 file(s) moved (exit code 0)
error: missing_folder is not a folder (exit code 2)
['csv/data.csv', 'jpg/photo.jpg', 'no_extension/notes', 'pdf/report.PDF', 'pdf/summary.pdf']
```

`--help` comes for free with argparse:

```python
run("--help")
```

**Output:**

```text
usage: organise.py [-h] [--dry-run] folder

Move files into sub-folders named after their extension.

positional arguments:
  folder      folder to organise

options:
  -h, --help  show this help message and exit
  --dry-run   only show what would happen (exit code 0)
```

**Running other programs safely:**

```python
import os

result = subprocess.run([sys.executable, "--version"], capture_output=True, text=True, check=True)
print(result.stdout.strip())

user_input = "notes; rm -rf ~"                    # malicious text
result = subprocess.run(["echo", user_input], capture_output=True, text=True)   # list form: no shell, no injection
print(result.stdout.strip())

try:
    subprocess.run([sys.executable, "-c", "import sys; sys.exit(3)"], check=True)
except subprocess.CalledProcessError as e:
    print("command failed with exit code", e.returncode)

api_key = os.environ.get("SHOP_API_KEY", "<not set>")        # secrets come from the environment
print("API key configured:", api_key != "<not set>")
```

**Output:**

```text
Python 3.14.7
notes; rm -rf ~
command failed with exit code 3
API key configured: False
```

**Common mistakes:**

- ❌ `subprocess.run(f"cmd {user_input}", shell=True)` (shell injection); use a list without `shell=True`.
- ❌ Hard-coded paths and secrets; use arguments, config files and environment variables.
- ❌ Destructive scripts with no `--dry-run` and no confirmation.
- ❌ Always exiting with 0, so cron/CI never notices failures.
- ❌ Scripts that only work from one particular current directory (build paths from `Path(__file__).parent` or arguments).

### Practice

1. Add a `--ext` option (may be repeated, e.g. `--ext pdf --ext csv`) to `organise.py` that limits which extensions are moved. Hint: `parser.add_argument("--ext", action="append")`. Test it with a dry run on a fresh folder.

<details>
<summary><b>Answer</b></summary>

```python
source = Path("organise.py").read_text(encoding="utf-8")
source = source.replace('    return parser.parse_args(argv)',
                        '    parser.add_argument("--ext", action="append", help="only these extensions (repeatable)")\n'
                        '    return parser.parse_args(argv)')
source = source.replace('        if path.is_file():',
                        '        if path.is_file() and (not args.ext or path.suffix.lstrip(".").lower() in args.ext):')
Path("organise.py").write_text(source, encoding="utf-8")

fresh = Path("inbox2")
fresh.mkdir(exist_ok=True)
for name in ["a.pdf", "b.csv", "c.jpg"]:
    (fresh / name).write_text("x", encoding="utf-8")
run("inbox2", "--dry-run", "--ext", "pdf", "--ext", "csv")
```

**Output:**

```text
would move a.pdf -> pdf/
would move b.csv -> csv/
2 file(s) to move (exit code 0)
```

</details>

---

### ✅ Part 5 checkpoint

Without looking, can you:

- [ ] Explain bytecode, reference counting and the cycle collector, and the difference between shallow and deep copies?
- [ ] Explain attribute lookup, write a descriptor, and use `__init_subclass__`?
- [ ] Choose between threads, processes, asyncio and free-threaded Python for a task, and protect shared data?
- [ ] Write async code with `TaskGroup`, timeouts, semaphores and queues without blocking the loop?
- [ ] Profile before optimising, and fix the algorithm first?
- [ ] Query a database with parameters and transactions, and write a safe CLI script with argparse and subprocess?

**Learn more:** [argparse tutorial](https://docs.python.org/3/howto/argparse.html) · [subprocess](https://docs.python.org/3/library/subprocess.html) · [Typer](https://typer.tiangolo.com/) · [PEP 723: inline script metadata](https://peps.python.org/pep-0723/)

---

# Part 6 — Advanced: Production Python

> **Goal:** Structure, configure, check, package and publish Python projects, and know what's new in Python 3.12–3.14.  
> **You need:** Parts 1–5.

---

## 37. Production-Grade Python: Project Layout, Configuration, Tooling and CI

### Theory

> **In simple words:** code that runs on your laptop once is a script; code that a team maintains for years and that runs for customers is a **product**. Production Python adds a predictable **project layout**, **configuration** that comes from the environment and is validated at start-up, **automatic checks** (formatter, linter, type checker, tests) on every change, reproducible **dependencies**, safe handling of **secrets**, and good **logs**. None of it is hard; it's a set of habits.

**Project layout (the `src/` layout):**

```text
shop-api/
├── pyproject.toml         # metadata, dependencies, tool settings (ruff, pytest, mypy)
├── uv.lock                # exact versions of everything (commit it)
├── README.md
├── .env.example           # documented config names, no real secrets (.env itself is git-ignored)
├── src/
│   └── shop/
│       ├── __init__.py
│       ├── config.py      # settings loaded and validated once
│       ├── domain/        # business logic, no frameworks: pure, easy to test
│       ├── adapters/      # database, HTTP clients, queues: talk to the outside world
│       └── api/           # web layer (FastAPI routes) or cli.py
└── tests/
    ├── unit/
    └── integration/
```

The `src/` folder forces tests to run against the **installed** package, catching packaging mistakes. Keeping business logic separate from I/O (the "functional core, imperative shell" idea) makes most code testable without databases or networks.

**Configuration (12-factor style):** settings come from **environment variables** (and a local `.env` for development), are validated **once at start-up** (fail fast with a clear error if something is missing), and are passed to the code that needs them. `pydantic-settings` does this in a few lines. Secrets (API keys, database passwords) never go in code or git; in production they come from the platform's secret manager.

**The tool chain (2026 defaults):**

| Job | Tool |
|---|---|
| Environments, dependencies, Python versions | **uv** |
| Formatting + linting | **ruff** (`ruff format`, `ruff check --fix`) |
| Type checking | **mypy**, **Pyright**, or the newer **ty** / Pyrefly |
| Tests + coverage | **pytest**, pytest-cov, hypothesis |
| Run checks before each commit | **pre-commit** (or `prek`) |
| Security | `pip-audit`/`uv` audit for vulnerable dependencies, `bandit` (ruff's `S` rules), secret scanning, Dependabot/Renovate for updates |
| CI | GitHub Actions / GitLab CI: install with `uv sync --locked`, then lint, type-check, test on every push |
| Containers | A slim Docker image with the locked dependencies, run as a non-root user |

**Runtime habits:** structured logging (Section [29](#29-logging-and-debugging)) with request ids; timeouts and retries (with backoff) on every network call; health-check endpoints; graceful shutdown; metrics and tracing (OpenTelemetry); feature flags for risky changes; don't catch-and-ignore errors; pin the Python version.

### Python

**Validated configuration with `pydantic-settings`:**

```python
import os
from pydantic import Field, SecretStr, ValidationError
from pydantic_settings import BaseSettings, SettingsConfigDict

class Settings(BaseSettings):
    model_config = SettingsConfigDict(env_prefix="SHOP_", env_file=".env", extra="ignore")

    database_url: str
    api_key: SecretStr                                       # never printed in logs by accident
    workers: int = Field(default=4, ge=1, le=64)
    debug: bool = False

os.environ.update({"SHOP_DATABASE_URL": "postgresql://app@db/shop", "SHOP_API_KEY": "sk-live-123", "SHOP_WORKERS": "8"})
settings = Settings()
print(settings.workers, settings.debug, settings.api_key, settings.api_key.get_secret_value()[:7] + "…")

os.environ["SHOP_WORKERS"] = "many"                          # a typo in deployment config
try:
    Settings()
except ValidationError as e:
    print("config error:", e.errors()[0]["loc"], e.errors()[0]["msg"])
```

**Output:**

```text
8 False ********** sk-live…
config error: ('workers',) Input should be a valid integer, unable to parse string as an integer
```

Environment variables are always text; the settings class converts `"8"` to `8`, checks the range, hides the secret in `repr`, and fails loudly at start-up if a value is invalid, instead of crashing mysteriously an hour later.

**The tool settings live in `pyproject.toml`.** A typical configuration, read here with the standard library's `tomllib`:

```python
import tomllib

pyproject = """
[project]
name = "shop-api"
version = "1.4.0"
requires-python = ">=3.13"
dependencies = ["fastapi>=0.115", "httpx>=0.28", "pydantic-settings>=2.6"]

[dependency-groups]
dev = ["pytest>=8", "pytest-cov", "ruff", "mypy"]

[tool.ruff]
line-length = 100
[tool.ruff.lint]
select = ["E", "F", "I", "B", "UP", "S", "SIM"]    # errors, pyflakes, imports, bugbear, pyupgrade, security, simplify

[tool.pytest.ini_options]
testpaths = ["tests"]
addopts = "-q --strict-markers"

[tool.mypy]
strict = true
"""
config = tomllib.loads(pyproject)
print(config["project"]["name"], config["project"]["requires-python"], config["tool"]["ruff"]["lint"]["select"])
```

**Output:**

```text
shop-api >=3.13 ['E', 'F', 'I', 'B', 'UP', 'S', 'SIM']
```

A minimal CI workflow (GitHub Actions, `.github/workflows/ci.yml`):

```text
name: ci
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      - uses: astral-sh/setup-uv@v6
      - run: uv sync --locked            # exact versions from uv.lock
      - run: uv run ruff format --check .
      - run: uv run ruff check .
      - run: uv run mypy src
      - run: uv run pytest --cov=shop
```

**Common mistakes:**

- ❌ Reading `os.environ[...]` all over the code (scattered, unvalidated config).
- ❌ Secrets in git (including in old commits); rotate any key that ever leaked.
- ❌ "Works on my machine" dependencies: no lock file, unpinned Python version.
- ❌ Business logic mixed into route handlers and SQL, so nothing can be tested in isolation.
- ❌ No CI, or CI that doesn't block merging when checks fail.

### Practice

1. Add a `timeout_seconds: float` setting that defaults to 10 and must be greater than 0 and at most 120. Show that `SHOP_TIMEOUT_SECONDS=0` is rejected.

<details>
<summary><b>Answer</b></summary>

```python
class Settings2(Settings):
    timeout_seconds: float = Field(default=10, gt=0, le=120)

os.environ["SHOP_WORKERS"] = "8"
print(Settings2().timeout_seconds)
os.environ["SHOP_TIMEOUT_SECONDS"] = "0"
try:
    Settings2()
except ValidationError as e:
    print("config error:", e.errors()[0]["loc"], e.errors()[0]["msg"])
del os.environ["SHOP_TIMEOUT_SECONDS"]
```

**Output:**

```text
10.0
config error: ('timeout_seconds',) Input should be greater than 0
```

</details>

**Learn more:** [The Twelve-Factor App: config](https://12factor.net/config) · [pydantic-settings](https://docs.pydantic.dev/latest/concepts/pydantic_settings/) · [Hynek Schlawack: testing & packaging](https://hynek.me/articles/testing-packaging/) · [uv: using uv in GitHub Actions](https://docs.astral.sh/uv/guides/integration/github/)

---

## 38. Packaging and Publishing a Library

### Theory

> **In simple words:** **packaging** turns your code into a file others can install with `pip install your-package` or `uv add your-package`. You describe the project in `pyproject.toml`, a **build backend** produces a **wheel** (`.whl`, a ready-to-install zip) and a **source distribution** (`.tar.gz`), and you upload them to **PyPI**. Even if you never publish publicly, the same steps let you install your own code cleanly in other projects, CI and Docker images.

**The vocabulary:**

| Term | Meaning |
|---|---|
| Distribution name | What you `pip install` (`shop-utils`); the import name can differ (`shop_utils`) |
| Wheel (`.whl`) | Built package, installs by unzipping: fast, no build step; `py3-none-any` means pure Python for any OS |
| sdist (`.tar.gz`) | Source archive; installers build a wheel from it when no suitable wheel exists |
| Build backend | The tool that builds: `hatchling`, `setuptools`, `flit-core`, `uv_build`, `maturin` (Rust extensions) |
| Build frontend | The command you run: `uv build` or `python -m build` |
| Entry points / scripts | `[project.scripts] shop = "shop_utils.cli:main"` installs a `shop` command |
| Extras | Optional dependency sets: `pip install shop-utils[excel]` |

**`pyproject.toml` essentials:** `[build-system]` (which backend), `[project]` (name, version, description, readme, `requires-python`, license, authors, dependencies, classifiers, URLs), optional `[project.optional-dependencies]` and `[project.scripts]`.

**Versions (PEP 440):** `1.4.0`, pre-releases `2.0.0rc1`, post-releases `1.4.0.post1`, dev builds `1.5.0.dev3`. Most libraries follow semantic-versioning-like rules: bump the major version for breaking changes. Libraries should declare **ranges** (`httpx>=0.27`), not exact pins, so they don't conflict with other libraries; applications pin exactly via a lock file.

**Publishing safely:** test on **TestPyPI** first; publish from CI using **Trusted Publishing** (PyPI trusts your GitHub Actions workflow through OIDC, so no long-lived API token exists to leak); enable 2FA; sign/attest releases (PyPI supports digital attestations); keep a changelog.

**Checklist:** `src/` layout · tests pass against the **built wheel**, not just the source folder · `py.typed` marker file if you ship type hints · README renders on PyPI · `requires-python` is honest · no secrets or large data files in the package.

### Python

Build a tiny library from scratch and inspect what's inside the wheel:

```python
import subprocess, sys, zipfile
from pathlib import Path

root = Path("shop-utils")
(root / "src" / "shop_utils").mkdir(parents=True, exist_ok=True)
(root / "pyproject.toml").write_text('''[build-system]
requires = ["setuptools>=77"]
build-backend = "setuptools.build_meta"

[project]
name = "shop-utils"
version = "0.1.0"
description = "Small helpers for prices and GST"
readme = "README.md"
requires-python = ">=3.12"
license = "MIT"
dependencies = []

[project.scripts]
gst = "shop_utils.cli:main"
''', encoding="utf-8")
(root / "README.md").write_text("# shop-utils\n\nHelpers for prices and GST.\n", encoding="utf-8")
(root / "src" / "shop_utils" / "__init__.py").write_text('''"""Price helpers."""
__version__ = "0.1.0"

def with_gst(amount: float, rate: float = 0.18) -> float:
    return round(amount * (1 + rate), 2)
''', encoding="utf-8")
(root / "src" / "shop_utils" / "cli.py").write_text('''import sys
from shop_utils import with_gst

def main() -> None:
    print(with_gst(float(sys.argv[1])))
''', encoding="utf-8")
(root / "src" / "shop_utils" / "py.typed").write_text("", encoding="utf-8")

result = subprocess.run([sys.executable, "-m", "build", str(root)], capture_output=True, text=True)
built = sorted(p.name for p in (root / "dist").iterdir())
print(built)
wheel = next((root / "dist").glob("*.whl"))
print(sorted(zipfile.ZipFile(wheel).namelist()))
```

**Output:**

```text
['shop_utils-0.1.0-py3-none-any.whl', 'shop_utils-0.1.0.tar.gz']
['shop_utils-0.1.0.dist-info/METADATA', 'shop_utils-0.1.0.dist-info/RECORD', 'shop_utils-0.1.0.dist-info/WHEEL', 'shop_utils-0.1.0.dist-info/entry_points.txt', 'shop_utils-0.1.0.dist-info/top_level.txt', 'shop_utils/__init__.py', 'shop_utils/cli.py', 'shop_utils/py.typed']
```

The wheel contains the package, the typing marker, and metadata (including the `gst` command in `entry_points.txt`). Pure-Python wheels are zip files that Python can even import from directly, which is a quick way to test the **built** artifact rather than the source folder:

```python
sys.path.insert(0, str(wheel))
import shop_utils
print(shop_utils.__version__, shop_utils.with_gst(1000), shop_utils.__file__.split("/")[-2:])
metadata = zipfile.ZipFile(wheel).read("shop_utils-0.1.0.dist-info/METADATA").decode()
print([line for line in metadata.splitlines() if line.startswith(("Name:", "Version:", "Requires-Python:", "License-Expression:"))])
```

**Output:**

```text
0.1.0 1180.0 ['shop_utils', '__init__.py']
['Name: shop-utils', 'Version: 0.1.0', 'License-Expression: MIT', 'Requires-Python: >=3.12']
```

The equivalent with uv, and publishing (terminal commands):

```text
uv init --lib shop-utils          # creates a src/ layout library with uv_build as backend
uv build                          # → dist/shop_utils-0.1.0-py3-none-any.whl and .tar.gz
uv publish --index testpypi       # try TestPyPI first; in CI use trusted publishing (no token)
uv publish
```

**Common mistakes:**

- ❌ Testing only from the source folder (a missing file or wrong package config is discovered by users).
- ❌ Exact pins (`requests==2.31.0`) in a library's dependencies.
- ❌ Publishing with a personal, long-lived API token stored in many places; use trusted publishing.
- ❌ Forgetting `requires-python`, or claiming support for versions you never test.
- ❌ Reusing a version number (PyPI doesn't allow re-uploading the same version; bump it).

### Practice

1. Bump the version to `0.2.0` in both `pyproject.toml` and `__init__.py`, rebuild, and list the files in `dist/`. Why is there still a 0.1.0 wheel, and what should CI do about old files?

<details>
<summary><b>Answer</b></summary>

```python
for path in [root / "pyproject.toml", root / "src" / "shop_utils" / "__init__.py"]:
    path.write_text(path.read_text(encoding="utf-8").replace("0.1.0", "0.2.0"), encoding="utf-8")
subprocess.run([sys.executable, "-m", "build", str(root)], capture_output=True, text=True)
print(sorted(p.name for p in (root / "dist").iterdir()))
```

**Output:**

```text
['shop_utils-0.1.0-py3-none-any.whl', 'shop_utils-0.1.0.tar.gz', 'shop_utils-0.2.0-py3-none-any.whl', 'shop_utils-0.2.0.tar.gz']
```

Building never deletes old artifacts, so `dist/` now has both versions; uploading `dist/*` would try to re-upload 0.1.0 (which PyPI rejects). CI should build into a clean folder (a fresh checkout, or delete `dist/` first) and upload only the new files. Keeping the version in one place (e.g. `dynamic = ["version"]` reading it from the package) avoids editing two files.

</details>

**Learn more:** [Python Packaging User Guide](https://packaging.python.org/) · [uv: building and publishing](https://docs.astral.sh/uv/guides/package/) · [PyPI: trusted publishers](https://docs.pypi.org/trusted-publishers/) · [PEP 440: version identification](https://peps.python.org/pep-0440/)

---

## 39. What's New in Python 3.12, 3.13 and 3.14

### Theory

> **In simple words:** Python releases a new version every October and supports each for five years. Recent versions made Python **faster**, gave **much better error messages**, added a **free-threaded** (no-GIL) build and an experimental **JIT**, and added handy syntax. In 2026, new projects should target **3.13 or 3.14**; 3.10 and older are out of or near the end of support. This section is a map of the changes you're most likely to meet in code reviews and interviews.

**Python 3.12 (October 2023):**

- **Type parameter syntax:** `def first[T](xs: list[T]) -> T:`, `class Box[T]:`, `type Alias = ...` (Section [22](#22-type-hints-and-static-type-checking)).
- **f-strings** can nest the same quotes and span lines (`f"{d["key"]}"` now works).
- `itertools.batched`, `Path.walk`, `@override` decorator (typing), better error messages ("Did you forget to import 'sys'?").
- Per-interpreter GIL (groundwork for 3.14's `concurrent.interpreters`); `distutils` removed.

**Python 3.13 (October 2024):**

- A new **interactive REPL**: colours, multi-line editing, history, `help`/`exit` without brackets.
- **Experimental free-threaded build** (`python3.13t`) and an **experimental JIT** (off by default).
- Coloured tracebacks; `locals()` semantics defined (PEP 667); `copy.replace()`.
- Many long-deprecated modules removed ("dead batteries": `cgi`, `telnetlib`, `imghdr`…).
- iOS and Android become supported platforms.

**Python 3.14 (October 2025):**

- **Free-threaded Python officially supported** (PEP 779), still a separate build; big progress in library support (Section [32](#32-concurrency-threads-processes-the-gil-and-free-threaded-python)).
- **Template strings (t-strings, PEP 750):** `t"Hello {name}"` creates a `Template` object that keeps the text and the values **separate**, so libraries can safely escape values for HTML, SQL or shell before combining them (the safe cousin of f-strings).
- **Deferred evaluation of annotations** (PEP 649/749) and the `annotationlib` module: forward references just work, imports are faster.
- **Multiple interpreters** in the standard library (`concurrent.interpreters`, PEP 734).
- **`except A, B:`** without brackets (PEP 758); warnings for `return`/`break` inside `finally` (PEP 765).
- `compression.zstd` (Zstandard, PEP 784); `uuid.uuid7()` (time-ordered UUIDs, great as database keys); `Path.copy()`/`move()`; `heapq` max-heap functions.
- Debugging: attach `pdb` to a running process (`python -m pdb -p PID`), `python -m asyncio ps/pstree PID`, a safe external-debugger interface (PEP 768).
- Incremental garbage collector; syntax highlighting in the REPL; `-X importtime` improvements; official Windows install manager.

**Upgrading safely:** read the "What's New" page's *Porting* section, run your tests with warnings enabled (`python -W error::DeprecationWarning -m pytest`), let `ruff check --select UP` modernise syntax, and check that key dependencies publish wheels for the new version.

### Python

```python
import sys
print(sys.version_info[:2])

from string.templatelib import Template
import html

user_input = "<script>alert('hi')</script>"
f_string = f"<p>Hello {user_input}</p>"                  # an f-string is already a finished str: unsafe
template = t"<p>Hello {user_input}</p>"                 # a t-string keeps text and values apart

def render_html(tpl: Template) -> str:
    parts = []
    for item in tpl:                                     # iterates over strings and Interpolation objects
        parts.append(item if isinstance(item, str) else html.escape(str(item.value)))
    return "".join(parts)

print(type(f_string).__name__, "|", f_string)
print(type(template).__name__, "|", template.strings, [i.value for i in template.interpolations])
print(render_html(template))

try:
    int("x")
except ValueError, TypeError:                           # 3.14: no brackets needed
    print("caught without brackets")

import uuid
a, b = uuid.uuid7(), uuid.uuid7()
print(a.version, a < b)                                  # time-ordered: later ids sort after earlier ones

from compression import zstd
data = b"order placed;" * 1000
packed = zstd.compress(data)
print(len(data), "→", len(packed), "bytes", zstd.decompress(packed) == data)

import heapq
scores = [40, 95, 70]
heapq.heapify_max(scores)                                # 3.14: max-heaps without negating values
print(heapq.heappop_max(scores))

class Tree:
    def children(self) -> list[Tree]:                    # forward reference without quotes (deferred annotations)
        return []
print(Tree.children.__annotations__)
```

**Output:**

```text
(3, 14)
str | <p>Hello <script>alert('hi')</script></p>
Template | ('<p>Hello ', '</p>') ["<script>alert('hi')</script>"]
<p>Hello &lt;script&gt;alert(&#x27;hi&#x27;)&lt;/script&gt;</p>
caught without brackets
7 True
13000 → 31 bytes True
95
{'return': list[__main__.Tree]}
```

**Common mistakes:**

- ❌ Starting new projects on old Python versions without a reason.
- ❌ Assuming the free-threaded build or JIT is on by default (they aren't).
- ❌ Using f-strings to build HTML or SQL from user input; use t-string-aware libraries or proper escaping/parameters.
- ❌ Upgrading Python without running the test suite with deprecation warnings visible.

### Practice

1. Write `render_sql(tpl)` that turns a t-string like `t"SELECT * FROM users WHERE name = {name} AND age > {age}"` into a tuple `(sql_with_placeholders, params)` for `sqlite3`, i.e. `("SELECT ... name = ? AND age > ?", ["Asha", 25])`.

<details>
<summary><b>Answer</b></summary>

```python
def render_sql(tpl: Template):
    sql, params = [], []
    for item in tpl:
        if isinstance(item, str):
            sql.append(item)
        else:
            sql.append("?")
            params.append(item.value)
    return "".join(sql), params

name, age = "Asha'; DROP TABLE users; --", 25
print(render_sql(t"SELECT * FROM users WHERE name = {name} AND age > {age}"))
```

**Output:**

```text
('SELECT * FROM users WHERE name = ? AND age > ?', ["Asha'; DROP TABLE users; --", 25])
```

The malicious name stays a **parameter**, never part of the SQL text: t-strings make the safe way as easy to write as the unsafe one.

</details>

---

### ✅ Part 6 checkpoint

Without looking, can you:

- [ ] Lay out a project with `src/`, load validated settings from the environment, and keep secrets out of code?
- [ ] Set up ruff, a type checker, pytest and CI for a project with uv?
- [ ] Build a wheel, check what's inside, and explain trusted publishing and version ranges?
- [ ] Name the main changes in Python 3.12–3.14 (type syntax, free-threading, JIT, t-strings, deferred annotations)?

**Learn more:** [What's new in Python 3.14](https://docs.python.org/3/whatsnew/3.14.html) · [What's new in 3.13](https://docs.python.org/3/whatsnew/3.13.html) · [PEP 750: template strings](https://peps.python.org/pep-0750/) · [Python release status](https://devguide.python.org/versions/)

---

# Part 7 — Interview Prep: Revision

> **Goal:** Revise with the DSA toolbox, classic coding problems, predict-the-output questions, a cheat sheet and the most-asked questions.  
> **You need:** Parts 1–6.

---

## 40. Python's Toolbox for Data Structures and Algorithms

### Theory

> **In simple words:** coding interviews test problem solving with data structures (arrays, hash maps, stacks, queues, heaps, trees, graphs) and algorithms (sorting, searching, two pointers, BFS/DFS, dynamic programming). The full, step-by-step course is **`dsa-python.md`**. This section is the Python-specific toolbox: which built-in structure plays each role and how fast each operation is, so your interview solutions are short **and** efficient.

| Classic structure | In Python | Key operations and cost |
|---|---|---|
| Dynamic array | `list` | index O(1), append/pop end O(1), insert/pop front O(n), `in` O(n) |
| Hash map / hash set | `dict`, `set`, `Counter`, `defaultdict` | get/set/`in` O(1) average |
| Stack | `list` (`append`, `pop`) | O(1) |
| Queue / deque | `collections.deque` (`append`, `popleft`) | O(1) at both ends |
| Priority queue (min-heap) | `heapq` on a list; push tuples `(priority, item)` | push/pop O(log n), peek `h[0]` O(1); 3.14 adds max-heap functions |
| Sorted list + binary search | `sorted`, `bisect.bisect_left/insort` | search O(log n); insort O(n) (shifting) |
| Linked list, tree, graph | Small classes (`Node`) or dicts of lists (`graph[u] = [v, …]`) | |
| Matrix / grid | list of lists; `(r, c)` tuples in sets for visited cells | |
| Memoised recursion (DP) | `@functools.cache` | turns exponential recursion into polynomial |

**Python-specific interview tips:** use `enumerate`, `zip`, slicing and comprehensions for short code; `sorted(..., key=...)` for custom orders; tuples as dict keys for 2-D states; `float("inf")` for initial minimums; raise the recursion limit or use an explicit stack for deep DFS; say the complexity out loud; and remember that clean, correct code beats clever code.

### Python

```python
import heapq
from bisect import bisect_left, insort
from collections import deque

# Stack: are brackets balanced?
def balanced(s):
    pairs, stack = {")": "(", "]": "[", "}": "{"}, []
    for ch in s:
        if ch in "([{":
            stack.append(ch)
        elif ch in pairs:
            if not stack or stack.pop() != pairs[ch]:
                return False
    return not stack

print(balanced("{[()()]}"), balanced("([)]"), balanced("(("))

# Heap: the k largest numbers without sorting everything (O(n log k))
print(heapq.nlargest(3, [5, 1, 9, 3, 7, 9, 2]))
tasks = []
for priority, name in [(3, "email"), (1, "fix prod bug"), (2, "review PR")]:
    heapq.heappush(tasks, (priority, name))
print([heapq.heappop(tasks)[1] for _ in range(3)])

# Binary search in a sorted list
scores = [35, 50, 62, 70, 88, 95]
print(bisect_left(scores, 70), bisect_left(scores, 71))
insort(scores, 75)
print(scores)

# BFS on a grid: shortest path length from S to E avoiding walls (#)
grid = ["S.#.",
        "..#.",
        "...E"]
def shortest_path(grid):
    rows, cols = len(grid), len(grid[0])
    start = next((r, c) for r in range(rows) for c in range(cols) if grid[r][c] == "S")
    queue, seen = deque([(start, 0)]), {start}
    while queue:
        (r, c), dist = queue.popleft()
        if grid[r][c] == "E":
            return dist
        for dr, dc in ((1, 0), (-1, 0), (0, 1), (0, -1)):
            nr, nc = r + dr, c + dc
            if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] != "#" and (nr, nc) not in seen:
                seen.add((nr, nc))
                queue.append(((nr, nc), dist + 1))
    return -1

print(shortest_path(grid))
```

**Output:**

```text
True False False
[9, 9, 7]
['fix prod bug', 'review PR', 'email']
3 4
[35, 50, 62, 70, 75, 88, 95]
5
```

**Common mistakes:**

- ❌ `list.pop(0)` as a queue (O(n)); use `deque.popleft()`.
- ❌ `x in some_list` inside a loop (O(n²) overall); use a set.
- ❌ Forgetting that `heapq` is a **min**-heap (negate values, or use the 3.14 `*_max` functions, for a max-heap).
- ❌ Recursion depth errors on big inputs; use iteration or `sys.setrecursionlimit` carefully.

### Practice

1. Return the **k most frequent** words in `"the cat the dog the cat a bird"` (k = 2) using `Counter` and `heapq.nlargest`, breaking ties alphabetically.

<details>
<summary><b>Answer</b></summary>

```python
from collections import Counter

words = "the cat the dog the cat a bird".split()
counts = Counter(words)
print(heapq.nsmallest(2, counts, key=lambda w: (-counts[w], w)))   # highest count first, then alphabetical
```

**Output:**

```text
['the', 'cat']
```

</details>

**Learn more:** [dsa-python.md (the full course)](dsa-python.md) · [heapq](https://docs.python.org/3/library/heapq.html) · [bisect](https://docs.python.org/3/library/bisect.html) · [NeetCode roadmap](https://neetcode.io/roadmap)

---

## 41. Interview Coding: Classic Python Problems

### Theory

> **In simple words:** Python interviews usually include a few short coding problems that test whether you can use the language fluently: strings, dictionaries, sorting, generators, classes and decorators. The approach: repeat the problem in your own words, ask about edge cases, write a simple correct solution, test it on examples (including empty input), then state its time and space complexity and improve if needed.

| Problem | Key idea | Complexity |
|---|---|---|
| Anagram groups | Sorted letters (or a letter count) as a dict key | O(n·k log k) |
| First non-repeating character | `Counter`, then one pass in order | O(n) |
| Two sum | Dict of value → index while scanning | O(n) |
| Flatten a nested list | Recursion or an explicit stack; a generator with `yield from` | O(total items) |
| LRU cache | `OrderedDict` with `move_to_end` / `popitem(last=False)` | O(1) per operation |
| Merge overlapping intervals | Sort by start, extend or append | O(n log n) |
| Retry/timing decorator | `functools.wraps`, `*args, **kwargs` | |
| Word frequency in a big file | Stream lines + `Counter` | O(n) time, O(unique words) memory |

### Python

```python
from collections import Counter, OrderedDict, defaultdict

def group_anagrams(words):
    groups = defaultdict(list)
    for w in words:
        groups["".join(sorted(w))].append(w)
    return list(groups.values())

def first_unique_char(s):
    counts = Counter(s)
    return next((ch for ch in s if counts[ch] == 1), None)

def two_sum(nums, target):
    seen = {}
    for i, n in enumerate(nums):
        if target - n in seen:
            return seen[target - n], i
        seen[n] = i
    return None

def flatten(items):
    for x in items:
        if isinstance(x, list):
            yield from flatten(x)
        else:
            yield x

def merge_intervals(intervals):
    merged = []
    for start, end in sorted(intervals):
        if merged and start <= merged[-1][1]:
            merged[-1][1] = max(merged[-1][1], end)
        else:
            merged.append([start, end])
    return merged

print(group_anagrams(["eat", "tea", "tan", "ate", "nat", "bat"]))
print(first_unique_char("swiss"), first_unique_char("aabb"))
print(two_sum([2, 7, 11, 15], 9), two_sum([1, 2], 10))
print(list(flatten([1, [2, [3, [4]], 5], []])))
print(merge_intervals([(1, 3), (8, 10), (2, 6), (15, 18), (17, 20)]))
```

**Output:**

```text
[['eat', 'tea', 'ate'], ['tan', 'nat'], ['bat']]
w None
(0, 1) None
[1, 2, 3, 4, 5]
[[1, 6], [8, 10], [15, 20]]
```

```python
class LRUCache:
    def __init__(self, capacity):
        self.capacity, self.data = capacity, OrderedDict()

    def get(self, key):
        if key not in self.data:
            return -1
        self.data.move_to_end(key)                  # mark as recently used
        return self.data[key]

    def put(self, key, value):
        self.data[key] = value
        self.data.move_to_end(key)
        if len(self.data) > self.capacity:
            self.data.popitem(last=False)           # evict the least recently used

cache = LRUCache(2)
cache.put("a", 1); cache.put("b", 2)
cache.get("a")                                      # "a" is now most recent
cache.put("c", 3)                                   # evicts "b"
print(cache.get("b"), cache.get("a"), cache.get("c"), list(cache.data))

def is_palindrome(s):
    cleaned = [ch.lower() for ch in s if ch.isalnum()]
    return cleaned == cleaned[::-1]

def compress(s):                                    # "aaabcc" → "a3b1c2"
    if not s:
        return ""
    out, run_char, run_len = [], s[0], 1
    for ch in s[1:]:
        if ch == run_char:
            run_len += 1
        else:
            out.append(f"{run_char}{run_len}")
            run_char, run_len = ch, 1
    out.append(f"{run_char}{run_len}")
    return "".join(out)

print(is_palindrome("A man, a plan, a canal: Panama"), is_palindrome("Python"))
print(compress("aaabcc"), compress(""), compress("z"))
```

**Output:**

```text
-1 1 3 ['a', 'c']
True False
a3b1c2  z1
```

**Common mistakes:**

- ❌ Jumping into code before clarifying input size and edge cases.
- ❌ O(n²) solutions (nested loops, `in` on lists) when a dict or set gives O(n).
- ❌ Not testing the empty input, single element and duplicates.
- ❌ Mutating the caller's input without saying so.

### Practice

1. Write `top_k_words(text, k)` returning the k most common words (case-insensitive, ignoring punctuation), and `rotate(matrix)` that rotates a square matrix 90° clockwise (return a new matrix).

<details>
<summary><b>Answer</b></summary>

```python
import re

def top_k_words(text, k):
    return [w for w, _ in Counter(re.findall(r"[a-z']+", text.lower())).most_common(k)]

def rotate(matrix):
    return [list(row) for row in zip(*matrix[::-1])]    # reverse the rows, then transpose

print(top_k_words("The cat. The dog! the CAT? A bird.", 2))
print(rotate([[1, 2, 3], [4, 5, 6], [7, 8, 9]]))
```

**Output:**

```text
['the', 'cat']
[[7, 4, 1], [8, 5, 2], [9, 6, 3]]
```

</details>

**Learn more:** [LeetCode](https://leetcode.com/) · [NeetCode 150](https://neetcode.io/practice) · [dsa-python.md](dsa-python.md)

---

## 42. Output-Based Questions (Predict the Output)

### Theory

> **In simple words:** "what does this print?" questions test whether you really understand Python's rules: names and mutability, default arguments, closures, scope, integer caching, truthiness, generators and inheritance. For each one below, **predict the output first**, then open the answer. Every answer was produced by running the code.

### Python

**1. Mutable default argument**

```python
def add(item, bucket=[]):
    bucket.append(item)
    return bucket

print(add(1), add(2), add(3, []), add(4))
```

<details>
<summary><b>Answer</b></summary>

**Output:**

```text
[1, 2, 4] [1, 2, 4] [3] [1, 2, 4]
```

The default list is created once and shared by calls that don't pass `bucket`; all three shared-list results are the **same list object**, printed after all appends. The call with `[]` gets its own list.

</details>

**2. Late-binding closures**

```python
funcs = [lambda: i * 10 for i in range(3)]
print([f() for f in funcs])
```

<details>
<summary><b>Answer</b></summary>

**Output:**

```text
[20, 20, 20]
```

Each lambda looks up `i` when called, after the loop finished. Fix: `lambda i=i: i * 10`.

</details>

**3. Aliasing and `+=`**

```python
a = [1, 2]
b = a
a += [3]          # in-place for lists
c = (1, 2)
d = c
c += (3,)         # creates a new tuple
print(a, b, c, d)
```

<details>
<summary><b>Answer</b></summary>

**Output:**

```text
[1, 2, 3] [1, 2, 3] (1, 2, 3) (1, 2)
```

`+=` mutates lists in place (so `b` sees it) but rebinds for immutable tuples.

</details>

**4. The grid trap**

```python
grid = [[0] * 2] * 2
grid[0][0] = 9
print(grid)
```

<details>
<summary><b>Answer</b></summary>

**Output:**

```text
[[9, 0], [9, 0]]
```

Both rows are the same list. Use `[[0] * 2 for _ in range(2)]`.

</details>

**5. `is` vs `==`**

```python
x = int("256"); y = int("256")
p = int("257"); q = int("257")
print(x is y, p is q, p == q)
```

<details>
<summary><b>Answer</b></summary>

**Output:**

```text
True False True
```

CPython caches small integers (−5..256); 257 created at runtime is a new object each time. Never rely on this: use `==`.

</details>

**6. Truthiness and short-circuiting**

```python
print(0 or "default", "" and "never", [] or [0], None or 0 or "last", 3 and 5)
```

<details>
<summary><b>Answer</b></summary>

**Output:**

```text
default  [0] last 5
```

`or` returns the first truthy value (or the last value); `and` returns the first falsy value (or the last value).

</details>

**7. Scope**

```python
x = "global"
def outer():
    x = "enclosing"
    def inner():
        return x
    x = "changed later"
    return inner()
print(outer(), x)
```

<details>
<summary><b>Answer</b></summary>

**Output:**

```text
changed later global
```

`inner` reads `x` from the enclosing scope **when it runs**, after it was reassigned.

</details>

**8. Generators are used up**

```python
squares = (n * n for n in range(4))
print(sum(squares), sum(squares), list(squares))
```

<details>
<summary><b>Answer</b></summary>

**Output:**

```text
14 0 []
```

</details>

**9. Class attributes vs instance attributes**

```python
class Counter:
    count = 0
    def __init__(self):
        self.count += 1          # reads the class attribute, then creates an INSTANCE attribute

a, b = Counter(), Counter()
print(a.count, b.count, Counter.count)
```

<details>
<summary><b>Answer</b></summary>

**Output:**

```text
1 1 0
```

`self.count += 1` becomes `self.count = self.count + 1`: it reads 0 from the class and stores 1 on the instance. Use `Counter.count += 1` (or `type(self).count`) to change the shared value.

</details>

**10. MRO and super()**

```python
class A:
    def hi(self): return "A"
class B(A):
    def hi(self): return "B" + super().hi()
class C(A):
    def hi(self): return "C" + super().hi()
class D(B, C):
    def hi(self): return "D" + super().hi()
print(D().hi(), [k.__name__ for k in D.__mro__])
```

<details>
<summary><b>Answer</b></summary>

**Output:**

```text
DBCA ['D', 'B', 'C', 'A', 'object']
```

`super()` follows the MRO (D, B, C, A), not just "the parent": B's `super()` is C here.

</details>

**11. `finally` wins**

```python
def f():
    try:
        return "try"
    finally:
        print("finally runs first")

print(f())
```

<details>
<summary><b>Answer</b></summary>

**Output:**

```text
finally runs first
try
```

`finally` always runs before the function actually returns. (A `return` *inside* `finally` would override the try's return; Python 3.14 warns about that because it silently swallows exceptions.)

</details>

**12. Dict ordering and updates**

```python
d = {"b": 1, "a": 2}
d["c"] = 3
d["b"] = 10                      # updating keeps the original position
del d["a"]; d["a"] = 0           # re-inserting goes to the end
print(list(d.items()), {1: "int", 1.0: "float", True: "bool"})
```

<details>
<summary><b>Answer</b></summary>

**Output:**

```text
[('b', 10), ('c', 3), ('a', 0)] {1: 'bool'}
```

`1`, `1.0` and `True` are equal and hash the same, so they're one key: the first key object is kept, the last value wins.

</details>

---

## 43. Python Cheat Sheet

**Basics:**

```text
x = 5; name = "Asha"; ok = True; nothing = None      type(x), isinstance(x, int)
int("42"), float("3.5"), str(9), bool(0)              7 / 2 = 3.5, 7 // 2 = 3, 7 % 2 = 1, 2 ** 10
f"{name:>8} {price:,.2f} {ratio:.1%} {x=}"            s[0], s[-1], s[1:4], s[::-1], s.split(), " ".join(xs)
if a: ... elif b: ... else: ...                       x if cond else y
match cmd: case "go" | "run": ...  case _: ...
for i in range(0, 10, 2): ...   while cond: ...       break / continue / loop-else (runs if no break)
```

**Collections:**

```text
list   [1, 2]    append, extend, insert, pop, remove, sort(key=, reverse=), sorted(), copy(), in (O(n))
tuple  (1, 2)    immutable, hashable; a, *rest = xs; a, b = b, a
dict   {"k": 1}  d[k], d.get(k, default), d.items(), d | other, setdefault, pop; Counter, defaultdict
set    {1, 2}    add, discard, a | b, a & b, a - b, a ^ b; in is O(1)
[f(x) for x in xs if p(x)]   {k: v for k, v in pairs}   {x for x in xs}   (x for x in xs)  ← lazy
enumerate(xs, 1), zip(a, b, strict=True), any(), all(), sum(), min/max(key=), reversed()
```

**Functions:**

```text
def f(pos, /, normal, *args, kw_only=1, **kwargs) -> int: """docstring"""
defaults evaluated ONCE → use None for mutable defaults        lambda x: x * 2
LEGB scope; global / nonlocal to rebind                          @decorator = f = decorator(f); use functools.wraps
yield → generator (lazy, single pass); yield from sub            @functools.cache for memoisation
```

**Classes:**

```text
class A(Base):                      super().__init__(...)          @property / @x.setter
    cls_attr = 0                    @classmethod def from_x(cls)   @staticmethod
    def __init__(self, v): self.v = v
__repr__ __str__ __eq__ __hash__ __lt__ __len__ __getitem__ __iter__ __contains__ __call__ __enter__/__exit__ __add__/__radd__
@dataclass(frozen=True, slots=True, order=True); field(default_factory=list); Enum / StrEnum; ABC + @abstractmethod; Protocol
```

**Errors, files, modules:**

```text
try: ... except (A, B) as e: ... else: ... finally: ...     raise X("msg") from e      except* for ExceptionGroup
with open(p, "w", encoding="utf-8") as f:                    Path("a") / "b.txt", p.read_text(), p.glob("*.csv")
json.dumps/loads(indent=2)   csv.DictReader/DictWriter(newline="")   if __name__ == "__main__": main()
uv init / uv add pkg / uv add --dev pytest / uv run app.py / uv sync / uvx ruff check
```

**Concurrency:**

```text
I/O-bound: asyncio (async def / await / TaskGroup / Semaphore / timeout / to_thread) or ThreadPoolExecutor
CPU-bound: ProcessPoolExecutor, NumPy, or free-threaded python3.14t        never block the event loop
```

**Complexity:** list index/append O(1), insert(0)/pop(0)/in O(n) · dict/set O(1) avg · deque ends O(1) · heapq push/pop O(log n) · sort O(n log n) · bisect O(log n).

**Tooling:** ruff (format + lint) · mypy/Pyright/ty (types) · pytest (+ fixtures, parametrize, mock) · logging (not print) · cProfile/timeit before optimising · pydantic(-settings) for external data and config · pre-commit + CI.

**Gotchas:** mutable defaults · `[[0]*n]*m` · `b = a` doesn't copy · closures bind late · `is` for `None` only · `0.1 + 0.2 != 0.3` · generators are single-use · `sort()` returns None · strings are immutable · `==` vs `is` for small ints · shadowing built-ins (`list = ...`) · file named like a stdlib module.

---

## 44. Most Asked Python Interview Questions

**Basics**

1. **What are Python's key features?** → Interpreted (compiled to bytecode), dynamically and strongly typed, garbage-collected, multi-paradigm, huge standard library and ecosystem, readable syntax with significant indentation.
2. **Mutable vs immutable types?** → Mutable objects can change in place (list, dict, set, most user objects); immutable can't (int, float, str, tuple, frozenset, bytes). Only immutable (hashable) objects can be dict keys or set members.
3. **List vs tuple vs set vs dict?** → Ordered mutable sequence; ordered immutable record; unordered unique items with O(1) membership; key→value mapping with O(1) lookup.
4. **`is` vs `==`?** → `==` compares values (`__eq__`); `is` compares identity (same object). Use `is` only for `None`, `True`, `False` and sentinels.
5. **How are arguments passed?** → By object reference ("call by sharing"): the function receives a reference to the same object; mutating it is visible to the caller, rebinding the parameter isn't.
6. **What is the mutable default argument problem?** → Defaults are evaluated once at definition time, so a `[]` default is shared across calls; use `None` and create inside.
7. **Shallow vs deep copy?** → Shallow copies the container but shares inner objects (`copy.copy`, `list(x)`, `x[:]`); deep copies recursively (`copy.deepcopy`).
8. **What are `*args` and `**kwargs`?** → Collect extra positional arguments into a tuple and extra keyword arguments into a dict; `*`/`**` also unpack when calling.
9. **What is a list comprehension vs a generator expression?** → `[...]` builds the whole list immediately; `(...)` produces items lazily, one at a time, using little memory.
10. **Explain LEGB.** → Name lookup order: Local, Enclosing, Global, Built-in; `global` and `nonlocal` allow rebinding outer names.

**Intermediate**

11. **What is a decorator?** → A callable that takes a function and returns a replacement (usually a wrapper adding behaviour); `@d` means `f = d(f)`; use `functools.wraps`.
12. **What is a closure?** → A function that remembers variables from its enclosing scope after that scope has finished; closures bind variables late.
13. **Iterator vs iterable vs generator?** → Iterable has `__iter__`; iterator has `__next__` and keeps position; a generator is an iterator created by a function with `yield`.
14. **What does `yield from` do?** → Delegates to a sub-iterator, yielding all its values (and receiving its return value).
15. **What are context managers?** → Objects with `__enter__`/`__exit__` used with `with` to guarantee clean-up; write them as classes or with `@contextmanager`.
16. **`@staticmethod` vs `@classmethod` vs instance methods?** → No implicit argument; receives the class (`cls`, e.g. alternative constructors); receives the instance (`self`).
17. **What is the MRO?** → The C3-linearised order Python searches classes for attributes with multiple inheritance; `super()` follows it.
18. **What are dunder methods?** → Special methods Python calls for syntax and built-ins (`__len__`, `__add__`, `__eq__`, `__iter__`, `__repr__`), letting classes behave like built-ins.
19. **What are dataclasses and when would you use Pydantic instead?** → Dataclasses generate `__init__`/`__repr__`/`__eq__` for plain records without validation; Pydantic validates and converts external data at runtime.
20. **EAFP vs LBYL?** → "Easier to ask forgiveness" (try/except) vs "look before you leap" (check first); Python favours EAFP, especially where checks can race.
21. **How do you handle exceptions well?** → Catch specific exceptions, keep `try` small, never bare `except`, chain with `from`, clean up with `finally`/`with`, log tracebacks.
22. **What are type hints for?** → Documentation, editor support and static checking (mypy/Pyright); not enforced at runtime except by libraries like Pydantic/FastAPI.
23. **What is `__name__ == "__main__"`?** → True only when the file is run directly, so code under it doesn't run on import.
24. **How do virtual environments work, and what is uv?** → A per-project folder with its own interpreter link and packages; uv is a fast tool that manages Python versions, environments, dependencies and lock files.

**Advanced**

25. **What is the GIL, and what changed recently?** → A lock letting one thread run Python bytecode at a time in CPython; threads still help I/O. Python 3.13 added and 3.14 officially supports a free-threaded build without the GIL.
26. **Threads vs processes vs asyncio?** → Threads: I/O with blocking libraries; processes: CPU parallelism (separate memory, pickling); asyncio: very many concurrent I/O tasks on one thread with `await`.
27. **How does memory management work?** → Reference counting frees objects immediately at zero; a (3.14: incremental) cycle collector frees reference cycles; small-object allocator.
28. **What are descriptors?** → Objects with `__get__`/`__set__`/`__delete__` controlling attribute access; properties, methods, `classmethod` and ORM fields are built on them.
29. **What is a metaclass?** → The class of a class (`type` by default), customising class creation; usually replaced by class decorators or `__init_subclass__`.
30. **`__getattr__` vs `__getattribute__`?** → `__getattr__` runs only when normal lookup fails; `__getattribute__` runs for every access.
31. **What are `__slots__`?** → A fixed set of attributes stored without a per-instance `__dict__`: less memory, faster access, no new attributes.
32. **How do you optimise Python code?** → Measure (cProfile, timeit), fix algorithms and data structures, use built-ins/comprehensions, vectorise with NumPy, cache, use concurrency for I/O and processes/free-threading for CPU, then consider Cython/Numba/Rust.
33. **What are generators good for in production?** → Streaming large files and API pages with constant memory, pipelines, infinite sequences.
34. **How do you make Python code production-ready?** → src layout, pyproject + lock file, validated config from the environment, logging, tests in CI, ruff + type checking, dependency auditing, secrets management.
35. **What is new in Python 3.14?** → Official free-threading support, t-strings (PEP 750), deferred annotations, `concurrent.interpreters`, `except A, B:`, zstd compression, `uuid7`, remote debugger attach, incremental GC.
36. **How does `asyncio` work under the hood?** → An event loop runs tasks; `await` suspends a coroutine until its awaitable is ready, letting others run; built on generators/coroutines and non-blocking I/O selectors.
37. **What is monkey patching and when is it acceptable?** → Replacing attributes at runtime; acceptable in tests (`monkeypatch`, `mock.patch`), risky in production code.
38. **How do you prevent SQL and shell injection in Python?** → Parameterised queries; `subprocess.run([...])` with a list and no `shell=True`; validate input; t-strings with escaping libraries.
39. **Explain `functools.lru_cache`.** → Memoises function results keyed by arguments (must be hashable), with an optional size limit using least-recently-used eviction.
40. **How would you process a 50 GB log file?** → Stream it line by line (generators), aggregate incrementally (Counter/dicts), parallelise by chunks with processes if CPU-bound, or use tools like DuckDB/Polars; never load it all into memory.

---
