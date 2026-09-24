# Python — Complete Notes

> Every major Python concept, each with an explanation, 2–3 examples and interview questions.
> Covers core language, data structures, functions, decorators, generators, OOP, typing, concurrency (threads, processes, asyncio), testing, internals and production best practices.
> The **Output-Based Questions** and **Most Asked Interview Questions** are at the end.

---

## Table of Contents

1. [Getting Started: What is Python & Your First Program](#1-getting-started-what-is-python--your-first-program)
2. [Variables](#2-variables)
3. [Data Types & Type Conversion](#3-data-types--type-conversion)
4. [Operators](#4-operators)
5. [Strings](#5-strings)
6. [Lists](#6-lists)
7. [Tuples](#7-tuples)
8. [Sets](#8-sets)
9. [Dictionaries](#9-dictionaries)
10. [Control Flow & match-case](#10-control-flow--match-case)
11. [Loops, range, enumerate, zip](#11-loops-range-enumerate-zip)
12. [Comprehensions](#12-comprehensions)
13. [Functions & Arguments](#13-functions--arguments)
14. [Lambda, map, filter, reduce, sorted](#14-lambda-map-filter-reduce-sorted)
15. [Scope: LEGB, global, nonlocal](#15-scope-legb-global-nonlocal)
16. [Closures](#16-closures)
17. [Decorators](#17-decorators)
18. [Iterators & Generators](#18-iterators--generators)
19. [OOP: Classes & Objects](#19-oop-classes--objects)
20. [OOP: 4 Pillars, Inheritance & MRO](#20-oop-4-pillars-inheritance--mro)
21. [Dunder (Magic) Methods](#21-dunder-magic-methods)
22. [Dataclasses, Enums, NamedTuple, __slots__](#22-dataclasses-enums-namedtuple-__slots__)
23. [Exceptions & Error Handling](#23-exceptions--error-handling)
24. [Context Managers](#24-context-managers)
25. [Modules & Packages](#25-modules--packages)
26. [Installing Packages: pip, venv, uv & pyproject.toml](#26-installing-packages-pip-venv-uv--pyprojecttoml)
27. [File Handling, pathlib, JSON, CSV](#27-file-handling-pathlib-json-csv)
28. [Databases Without an ORM (sqlite3, psycopg 3)](#28-databases-without-an-orm-sqlite3-psycopg-3)
29. [Standard Library Essentials](#29-standard-library-essentials)
30. [Scripting & Automation](#30-scripting--automation)
31. [Type Hints & typing](#31-type-hints--typing)
32. [How Python Runs: Bytecode, Memory & Internals](#32-how-python-runs-bytecode-memory--internals)
33. [Advanced Python: Attribute Access, Descriptors, Metaclasses & Weak References](#33-advanced-python-attribute-access-descriptors-metaclasses--weak-references)
34. [Concurrency: GIL, Threads, Processes](#34-concurrency-gil-threads-processes)
35. [asyncio](#35-asyncio)
36. [Testing with pytest](#36-testing-with-pytest)
37. [Logging & Debugging](#37-logging--debugging)
38. [Regular Expressions](#38-regular-expressions)
39. [Code Style: PEP 8 & the Zen of Python](#39-code-style-pep-8--the-zen-of-python)
40. [Pythonic Idioms](#40-pythonic-idioms)
41. [Performance](#41-performance)
42. [Production-Grade Python](#42-production-grade-python)
43. [Packaging & Publishing a Python Library](#43-packaging--publishing-a-python-library)
44. [Data Structures & Algorithms in Python](#44-data-structures--algorithms-in-python)
45. [Coding Questions (with solutions)](#45-coding-questions)
46. [Output-Based Questions](#46-output-based-questions)
47. [Most Asked Interview Questions](#47-most-asked-interview-questions)

---

## 1. Getting Started: What is Python & Your First Program

**Python** is a simple, readable, general-purpose programming language. You write instructions in plain-English-like code, and Python runs them line by line.

Why people use it:
- **Easy to read and write** — no semicolons or curly braces; indentation shows structure.
- **Runs everywhere** — Windows, macOS, Linux.
- **Huge ecosystem** — web backends (FastAPI, Django), data science & AI (pandas, PyTorch), automation scripts, testing.
- **Interpreted** — you run the file directly; no separate compile step for you to do.
- **Dynamically typed** — you don't declare types; Python figures them out when the code runs.

### Install & check Python

```bash
# Download from python.org, or on macOS: brew install python
python3 --version        # e.g. Python 3.13.x
```

(On Windows the command is often `python` or `py` instead of `python3`.)

### Two ways to run Python

**1. Interactive mode (REPL)** — type code, get the result instantly. Great for experimenting.

```bash
$ python3
>>> 2 + 3
5
>>> "hello".upper()
'HELLO'
>>> exit()
```

**2. Run a file** — save code in a `.py` file and run it.

```python
# hello.py
print("Hello, World!")
```

```bash
python3 hello.py         # → Hello, World!
```

Use an editor like **VS Code** (with the Python extension) or PyCharm.

### print() — showing output

```python
print("Hello")                    # Hello
print("Age:", 25)                 # Age: 25   (items separated by a space)
print("a", "b", "c", sep="-")     # a-b-c
print("Loading", end="...")       # no newline at the end
print()                           # empty line

name = "Rohit"
age = 25
print(f"My name is {name} and I am {age} years old")   # f-string: put variables inside {}
```

### input() — reading from the user

`input()` **always returns a string**. Convert it if you need a number.

```python
name = input("What is your name? ")
print(f"Hello, {name}!")

age = int(input("Your age? "))        # "25" → 25
print(f"Next year you'll be {age + 1}")

price = float(input("Price? "))       # "99.5" → 99.5
```

```python
# Common mistake
age = input("Age? ")      # "25" (a string)
print(age + 1)            # TypeError: can only concatenate str (not "int") to str
```

### Comments

```python
# This is a single-line comment — Python ignores it

total = 100  # comments can go at the end of a line too

"""
Triple-quoted strings are often used as multi-line notes
or as documentation at the top of a file/function (docstrings).
"""
```

Write comments to explain **why** something is done, not what the code obviously does.

### Indentation — how Python groups code

Python uses **indentation (4 spaces)** instead of `{}` to show which lines belong together. A line ending with `:` starts a block.

```python
age = 20
if age >= 18:
    print("You can vote")        # inside the if (indented)
    print("Welcome!")            # also inside
print("This always runs")        # outside (not indented)
```

```python
if age >= 18:
print("oops")                    # IndentationError: expected an indented block
```

Don't mix tabs and spaces — let your editor insert 4 spaces.

### Your first small programs

```python
# 1. Simple calculator
a = float(input("First number: "))
b = float(input("Second number: "))
print("Sum:", a + b)
print("Difference:", a - b)
print("Product:", a * b)
if b != 0:
    print("Division:", a / b)
else:
    print("Can't divide by zero")
```

```python
# 2. Even or odd
n = int(input("Enter a number: "))
if n % 2 == 0:
    print(f"{n} is even")
else:
    print(f"{n} is odd")
```

```python
# 3. Multiplication table
n = int(input("Table of: "))
for i in range(1, 11):
    print(f"{n} x {i} = {n * i}")
```

### Common beginner errors (and what they mean)

| Error | Cause | Example |
|---|---|---|
| `SyntaxError` | Code isn't valid Python (missing `:`, bracket, quote) | `if x > 5 print(x)` |
| `IndentationError` | Wrong/missing indentation | a block not indented after `if` |
| `NameError` | Using a variable that doesn't exist (often a typo) | `print(nmae)` |
| `TypeError` | Operation on the wrong type | `"5" + 5` |
| `ValueError` | Right type, bad value | `int("abc")` |
| `ZeroDivisionError` | Dividing by zero | `10 / 0` |
| `IndexError` | List index doesn't exist | `[1, 2][5]` |
| `KeyError` | Dict key doesn't exist | `{"a": 1}["b"]` |

**Read the last line of the error message first** — it tells you the error type and the reason; the lines above show where it happened.

### Built-in help

```python
help(print)          # documentation
type(42)             # <class 'int'> — what type is this?
dir("hello")         # list everything you can do with a string
```

**Interview Qs**
- What is Python and what is it used for?
- Is Python compiled or interpreted? → You run it directly; internally it's compiled to bytecode and then interpreted (see "How Python Runs" in the Internals section).
- What does `input()` return? → Always a string.
- How does Python define code blocks? → Indentation.
- Dynamic typing vs static typing? → Python checks types while running; you don't declare them.

---

## 2. Variables

A **variable** is a name that stores a value so you can use it later. You create one by assigning with `=` — no keyword or type needed.

```python
name = "Rohit"        # text (string)
age = 25              # whole number (int)
height = 5.9          # decimal number (float)
is_student = True     # True/False (bool)

print(name, age)      # Rohit 25
age = 26              # change the value any time
age = age + 1         # 27
age += 1              # shortcut for age = age + 1 → 28
```

### Naming rules

- Can contain letters, digits and `_`, but **can't start with a digit**: `user1` ✅, `1user` ❌.
- **Case-sensitive**: `age` and `Age` are different variables.
- Can't be a **keyword**: `if`, `for`, `class`, `def`, `True`, `None`, `import`, `return`…
- Convention: `snake_case` for variables (`first_name`, `total_price`), `UPPER_CASE` for constants (`MAX_USERS = 100`).
- Use meaningful names: `total_price` not `tp`.

```python
first_name = "Rohit"   # ✅
firstName = "Rohit"    # works, but not Python style
2nd_place = "A"        # ❌ SyntaxError
class = "10th"         # ❌ SyntaxError (keyword)
```

### Multiple assignment & swapping

```python
x, y, z = 1, 2, 3        # assign several at once
a = b = 0                # same value to two names
a, b = 10, 20
a, b = b, a              # swap → a = 20, b = 10 (no temp variable needed)
```

### Checking a variable's type

```python
type(name)     # <class 'str'>
type(age)      # <class 'int'>
type(height)   # <class 'float'>
```

Python is **dynamically typed** — the same variable can later hold a different type (possible, but usually a bad idea):

```python
value = 10
value = "ten"    # allowed
```

### Constants

Python has no true constants; by convention, UPPER_CASE names mean "don't change this".

```python
PI = 3.14159
MAX_LOGIN_ATTEMPTS = 3
```

---

### Going deeper: names, objects & mutability

In Python, a **variable is a name (label) bound to an object**. Assignment never copies — it binds another name to the same object.

Every object has:
- **identity** (`id(obj)` — memory address in CPython),
- **type** (`type(obj)`),
- **value**.

### Example 1 — names point to objects

```python
a = [1, 2, 3]
b = a            # b points to the SAME list
b.append(4)
print(a)         # [1, 2, 3, 4]
print(a is b)    # True — same identity
print(id(a) == id(b))  # True
```

### Example 2 — mutable vs immutable

| Immutable | Mutable |
|---|---|
| `int`, `float`, `bool`, `str`, `tuple`, `frozenset`, `bytes`, `None` | `list`, `dict`, `set`, `bytearray`, most custom objects |

```python
x = 10
y = x
y += 1           # creates a NEW int object; x unaffected
print(x, y)      # 10 11

s = "hi"
s += "!"         # new string object (strings are immutable)

t = (1, [2, 3])
t[1].append(4)   # allowed! the tuple is immutable but the list inside is mutable
print(t)         # (1, [2, 3, 4])
```

### Example 3 — `is` vs `==`

- `==` compares **values** (calls `__eq__`).
- `is` compares **identity** (same object).

```python
a = [1, 2]
b = [1, 2]
a == b   # True
a is b   # False

x = None
if x is None: ...   # ✅ always use `is` for None, True, False singletons
```

### Multiple assignment & swapping

```python
a, b, c = 1, 2, 3
a, b = b, a                  # swap without temp
x = y = z = 0                # same object bound to 3 names
first, *rest = [1, 2, 3, 4]  # first=1, rest=[2, 3, 4]
*init, last = [1, 2, 3]      # init=[1, 2], last=3
```

### Pass-by-object-reference

Python passes **references to objects** ("call by sharing"). Mutating a mutable argument affects the caller; rebinding the parameter does not.

```python
def modify(lst):
    lst.append(99)     # mutates the caller's list
    lst = [0]          # rebinds local name only

nums = [1]
modify(nums)
print(nums)            # [1, 99]
```

**Interview Qs**
- Is Python pass-by-value or pass-by-reference? → Neither exactly: pass-by-object-reference.
- `is` vs `==`? (above)
- Mutable vs immutable types? Why does it matter? → Shared references, dict keys must be hashable (immutable), default args trap.

---

## 3. Data Types & Type Conversion

```python
n = 42               # int (arbitrary precision — no overflow!)
big = 2 ** 100       # 1267650600228229401496703205376
f = 3.14             # float (64-bit double)
c = 2 + 3j           # complex
b = True             # bool (subclass of int: True == 1)
s = "hello"          # str (unicode)
by = b"bytes"        # bytes
nothing = None       # NoneType

type(42)             # <class 'int'>
isinstance(True, int)  # True
```

### Type conversion

```python
int("42")        # 42
int("101", 2)    # 5 (binary)
int(3.99)        # 3 (truncates)
float("3.5")     # 3.5
str(100)         # "100"
bool("")         # False
list("abc")      # ['a', 'b', 'c']
tuple([1, 2])    # (1, 2)
set([1, 1, 2])   # {1, 2}
dict([("a", 1)]) # {'a': 1}
int("abc")       # ValueError
```

### Truthiness

Falsy values: `False`, `None`, `0`, `0.0`, `0j`, `""`, `[]`, `()`, `{}`, `set()`, `range(0)`, and objects whose `__bool__` returns False or `__len__` returns 0. Everything else is truthy.

```python
if []: print("never")
if [0]: print("non-empty list is truthy")   # prints
if "False": print("non-empty string is truthy")  # prints
```

### Numbers gotchas

```python
0.1 + 0.2 == 0.3                  # False (floating point)
import math
math.isclose(0.1 + 0.2, 0.3)      # True
from decimal import Decimal
Decimal("0.1") + Decimal("0.2")   # Decimal('0.3') — use for money
from fractions import Fraction
Fraction(1, 3) + Fraction(1, 6)   # Fraction(1, 2)

7 / 2    # 3.5 (true division, always float)
7 // 2   # 3   (floor division)
-7 // 2  # -4  (floors toward negative infinity!)
7 % 3    # 1
-7 % 3   # 2   (result has the sign of the divisor)
divmod(7, 2)  # (3, 1)
round(2.5)    # 2 — banker's rounding (round half to even)
round(3.5)    # 4
```

**Interview Qs**
- Does Python have integer overflow? → No, ints have arbitrary precision.
- Why is `round(2.5)` 2? → Banker's rounding.
- How to handle money? → `Decimal` or integer cents.

---

## 4. Operators

```python
# Arithmetic: + - * / // % **
2 ** 10         # 1024

# Comparison — can be CHAINED
x = 5
1 < x < 10      # True (same as 1 < x and x < 10)
a == b == c

# Logical: and, or, not — return one of the operands (short-circuit)
"" or "default"      # 'default'
0 or None or []      # [] (last operand)
"a" and "b"          # 'b'
not []               # True
name = user_input or "Guest"

# Identity & membership
x is None
"a" in "abc"         # True
3 in [1, 2, 3]       # True
"key" in {"key": 1}  # True (checks keys)

# Bitwise: & | ^ ~ << >>
5 & 3, 5 | 3, 5 ^ 3, ~5, 1 << 3   # 1 7 6 -6 8

# Walrus operator := (assignment expression, 3.8+)
if (n := len(data)) > 10:
    print(f"too long ({n} items)")

while (line := file.readline()):
    process(line)

# Ternary
status = "adult" if age >= 18 else "minor"
```

No `++` / `--` in Python — use `x += 1`.

---

## 5. Strings

Strings are **immutable sequences of Unicode characters**.

```python
s = "Hello, World"
s[0]        # 'H'
s[-1]       # 'd'
s[0:5]      # 'Hello'  (slice: start inclusive, end exclusive)
s[::2]      # 'Hlo ol' (step)
s[::-1]     # 'dlroW ,olleH' (reverse)
len(s)      # 12

s.lower(); s.upper(); s.title(); s.capitalize(); s.swapcase()
s.strip(); s.lstrip(); s.rstrip("!")
s.split(", ")              # ['Hello', 'World']
", ".join(["a", "b"])      # 'a, b'
s.replace("World", "Py")
s.find("o")                # 4 (-1 if not found)
s.index("o")               # 4 (ValueError if not found)
s.count("l")               # 3
s.startswith("He"); s.endswith("ld")
"42".isdigit(); "abc".isalpha(); "a1".isalnum(); "  ".isspace()
"5".zfill(3)               # '005'
"hi".center(10, "*")       # '****hi****'
s.removeprefix("Hello, ")  # 'World' (3.9+)
s.partition(", ")          # ('Hello', ', ', 'World')
```

### f-strings (formatting)

```python
name, price, ratio = "Rohit", 1234.5678, 0.4567
f"Hi {name}"                  # 'Hi Rohit'
f"{price:.2f}"                # '1234.57'
f"{price:,.2f}"               # '1,234.57'
f"{ratio:.1%}"                # '45.7%'
f"{42:05d}"                   # '00042'
f"{'left':<10}|{'right':>10}" # alignment
f"{name!r}"                   # "'Rohit'" (repr)
f"{price=}"                   # 'price=1234.5678' (debug, 3.8+)
f"{2 + 3}"                    # expressions allowed

"{} is {}".format("Python", "fun")   # older style
"%s is %d" % ("age", 25)             # oldest style
```

### Multi-line, raw & byte strings

```python
text = """Line 1
Line 2"""
path = r"C:\new\folder"        # raw string — backslashes not escaped (regex, Windows paths)
data = "héllo".encode("utf-8") # b'h\xc3\xa9llo'
data.decode("utf-8")           # 'héllo'
```

### Building strings efficiently

```python
# ❌ O(n²) in a loop — creates a new string every time
result = ""
for w in words:
    result += w

# ✅
result = "".join(words)
```

**Interview Qs**
- Are strings mutable? → No.
- `find` vs `index`? → find returns -1; index raises ValueError.
- How to reverse a string? → `s[::-1]`.

---

## 6. Lists

Ordered, mutable, allow duplicates, can hold mixed types. Implemented as **dynamic arrays**.

```python
nums = [3, 1, 4]
nums.append(1)          # [3, 1, 4, 1]           O(1)
nums.extend([5, 9])     # [3, 1, 4, 1, 5, 9]
nums.insert(0, 0)       # insert at index         O(n)
nums.remove(1)          # remove first occurrence  O(n)
nums.pop()              # remove & return last      O(1)
nums.pop(0)             # remove first               O(n) — use deque for queues
nums.index(4)           # position
nums.count(1)
nums.sort()             # in place, returns None!
nums.sort(reverse=True)
sorted(nums)            # returns NEW list
nums.reverse()
nums.copy()             # shallow copy (same as nums[:] or list(nums))
nums.clear()
del nums[0:2]           # delete a slice
```

### Slicing

```python
a = [0, 1, 2, 3, 4, 5]
a[1:4]      # [1, 2, 3]
a[:3]       # [0, 1, 2]
a[3:]       # [3, 4, 5]
a[-2:]      # [4, 5]
a[::-1]     # reversed copy
a[1:3] = ["x", "y", "z"]   # slice assignment can change length
```

### Common traps

```python
# 1. sort() returns None
result = nums.sort()   # result is None!

# 2. Multiplying lists of lists shares the inner list
grid = [[0] * 3] * 3
grid[0][0] = 1
print(grid)            # [[1, 0, 0], [1, 0, 0], [1, 0, 0]] ❌
grid = [[0] * 3 for _ in range(3)]  # ✅ independent rows

# 3. Modifying a list while iterating
for x in nums:
    if x < 0:
        nums.remove(x)   # skips elements
nums = [x for x in nums if x >= 0]  # ✅
```

### Sorting with key

```python
users = [{"name": "Zed", "age": 30}, {"name": "amy", "age": 25}]
sorted(users, key=lambda u: u["age"])
sorted(users, key=lambda u: u["name"].lower())
sorted(users, key=lambda u: (-u["age"], u["name"]))  # age desc, then name asc

from operator import itemgetter, attrgetter
sorted(users, key=itemgetter("age"))
```

Python's sort is **Timsort**: stable, O(n log n).

### Time complexity

| Operation | Complexity |
|---|---|
| index `a[i]`, `append`, `pop()` | O(1) |
| `insert(0, x)`, `pop(0)`, `remove`, `in` | O(n) |
| `sort` | O(n log n) |
| slice `a[i:j]` | O(j - i) |

---

## 7. Tuples

Ordered, **immutable**, allow duplicates. Faster and smaller than lists; **hashable** (if contents are) → usable as dict keys / set members.

```python
point = (3, 4)
single = (5,)          # comma makes the tuple, not parentheses!
not_tuple = (5)        # just int 5
empty = ()
coords = 1, 2, 3       # parentheses optional (packing)

x, y = point           # unpacking
a, (b, c) = 1, (2, 3)  # nested unpacking

locations = {(28.6, 77.2): "Delhi"}   # tuple as dict key

def min_max(nums):
    return min(nums), max(nums)        # returns a tuple
lo, hi = min_max([3, 1, 4])
```

### namedtuple — readable tuples

```python
from collections import namedtuple
Point = namedtuple("Point", ["x", "y"])
p = Point(3, 4)
p.x, p[1]             # 3 4
p._replace(x=10)      # new Point(x=10, y=4)
p._asdict()           # {'x': 3, 'y': 4}

from typing import NamedTuple
class User(NamedTuple):
    id: int
    name: str
    active: bool = True
```

**List vs Tuple**: list for homogeneous, changing collections; tuple for fixed records (x, y), dict keys, returning multiple values, and data that must not change.

---

## 8. Sets

Unordered collection of **unique, hashable** items. Backed by a hash table → O(1) average membership test.

```python
s = {1, 2, 3}
empty = set()          # {} is an empty DICT
s.add(4); s.remove(4)  # remove raises KeyError if missing
s.discard(99)          # no error
3 in s                 # O(1)

a, b = {1, 2, 3}, {2, 3, 4}
a | b      # union               {1, 2, 3, 4}
a & b      # intersection        {2, 3}
a - b      # difference          {1}
a ^ b      # symmetric diff      {1, 4}
a <= b     # subset?             False
a.isdisjoint({9})                # True

frozen = frozenset([1, 2])       # immutable, hashable set
```

```python
# Remove duplicates while preserving order
items = [3, 1, 3, 2, 1]
list(dict.fromkeys(items))   # [3, 1, 2]
list(set(items))             # order NOT guaranteed

# Fast membership in loops
banned = set(banned_ids)     # O(1) lookups instead of O(n) list scans
clean = [u for u in users if u.id not in banned]
```

---

## 9. Dictionaries

Key → value mapping backed by a **hash table**. Keys must be **hashable** (immutable: str, int, tuple…). Since Python 3.7, dicts **preserve insertion order**.

```python
user = {"name": "Rohit", "age": 25}
user["city"] = "Delhi"            # add/update
user["name"]                      # 'Rohit'
user["email"]                     # KeyError!
user.get("email")                 # None
user.get("email", "n/a")          # default
user.setdefault("tags", []).append("admin")  # get or insert default
user.pop("age")                   # remove & return
user.pop("missing", None)         # no error with default
del user["city"]
"name" in user                    # True (checks keys)

user.keys(); user.values(); user.items()
for key, value in user.items():
    print(key, value)

user.update({"age": 26, "role": "dev"})
merged = defaults | overrides     # merge (3.9+), right side wins
config |= {"debug": True}         # in-place merge
merged2 = {**defaults, **overrides}  # older way

dict.fromkeys(["a", "b"], 0)      # {'a': 0, 'b': 0}
dict(zip(["a", "b"], [1, 2]))     # {'a': 1, 'b': 2}
```

### Example — counting & grouping

```python
words = "the cat and the hat".split()

# counting
counts = {}
for w in words:
    counts[w] = counts.get(w, 0) + 1

from collections import Counter, defaultdict
Counter(words).most_common(2)    # [('the', 2), ('cat', 1)]

# grouping
groups = defaultdict(list)
for w in words:
    groups[len(w)].append(w)      # {3: ['the', 'cat', 'and', 'the', 'hat']}
```

### Example — nested dicts safely

```python
data = {"user": {"profile": {"city": "Delhi"}}}
city = data.get("user", {}).get("profile", {}).get("city")

# sorting a dict by value
scores = {"a": 3, "b": 1, "c": 2}
dict(sorted(scores.items(), key=lambda kv: kv[1], reverse=True))  # {'a': 3, 'c': 2, 'b': 1}

# inverting
{v: k for k, v in scores.items()}
```

### Why must keys be hashable?

The dict stores entries by `hash(key)`. If a key could change after insertion, its hash would change and the entry would be lost. That's why lists can't be keys but tuples can.

```python
{[1, 2]: "x"}   # TypeError: unhashable type: 'list'
{(1, 2): "x"}   # ✅
```

**Complexity**: get/set/delete/`in` → O(1) average, O(n) worst case (hash collisions).

**Interview Qs**
- How does a dict work internally? → Hash table with open addressing; compact array of entries preserves order.
- `dict[key]` vs `dict.get(key)`? → KeyError vs default.
- Are dicts ordered? → Yes, insertion order guaranteed since 3.7.

---

## 10. Control Flow & match-case

### if / elif / else

```python
if score >= 90:
    grade = "A"
elif score >= 75:
    grade = "B"
else:
    grade = "C"

# Truthiness checks
if not items: ...          # empty
if user is None: ...
if name: ...               # non-empty string
```

### match-case — Structural Pattern Matching (3.10+)

More than a switch: matches **shapes** of data (literals, sequences, mappings, classes) and **destructures** them.

```python
def http_status(code: int) -> str:
    match code:
        case 200 | 201:
            return "OK"
        case 404:
            return "Not Found"
        case 500 | 502 | 503:
            return "Server Error"
        case _:
            return "Unknown"          # _ = wildcard (default)
```

```python
# Matching sequences & mappings (e.g. parsing commands / JSON events)
def handle(command: list[str]):
    match command:
        case ["quit"]:
            return "bye"
        case ["go", direction]:
            return f"going {direction}"
        case ["drop", *items]:
            return f"dropping {items}"
        case _:
            return "unknown command"

def process(event: dict):
    match event:
        case {"type": "click", "x": x, "y": y}:
            return f"click at {x},{y}"
        case {"type": "keypress", "key": str(key)} if key.isalpha():   # guard
            return f"letter {key}"
        case {"type": t}:
            return f"unhandled {t}"
```

```python
# Matching classes
from dataclasses import dataclass

@dataclass
class Circle: radius: float
@dataclass
class Rect: w: float; h: float

def area(shape):
    match shape:
        case Circle(radius=r):
            return 3.14159 * r * r
        case Rect(w=w, h=h):
            return w * h
```

---

## 11. Loops, range, enumerate, zip

```python
for i in range(5): ...            # 0..4
for i in range(2, 10, 2): ...     # 2, 4, 6, 8
for i in range(10, 0, -1): ...    # countdown

for index, fruit in enumerate(["apple", "mango"], start=1):
    print(index, fruit)           # 1 apple, 2 mango

names, ages = ["a", "b"], [20, 30]
for name, age in zip(names, ages):
    print(name, age)
zip(names, ages, strict=True)     # 3.10+: error if lengths differ

for key, value in config.items(): ...
for ch in "hello": ...
for line in open("file.txt"): ... # file objects are iterable

count = 0
while count < 3:
    count += 1
```

### break, continue, pass, and loop-else

```python
for n in nums:
    if n < 0:
        continue      # skip
    if n == 99:
        break         # exit loop
    process(n)

def todo(): pass      # placeholder that does nothing

# for-else: `else` runs only if the loop did NOT break
for user in users:
    if user.is_admin:
        print("found admin")
        break
else:
    print("no admin found")
```

### Useful iteration helpers

```python
reversed([1, 2, 3])
sorted(items, key=len)
any(x > 10 for x in nums)
all(x > 0 for x in nums)
sum(prices); min(nums); max(nums, key=abs)

import itertools
itertools.chain([1, 2], [3])          # 1 2 3
itertools.islice(gen, 5)              # first 5 items of any iterable
itertools.pairwise([1, 2, 3])         # (1,2), (2,3)   3.10+
itertools.batched(range(7), 3)        # (0,1,2) (3,4,5) (6,)   3.12+
itertools.product("ab", repeat=2)     # aa ab ba bb
itertools.permutations([1, 2, 3], 2)
itertools.combinations([1, 2, 3], 2)
itertools.groupby(sorted_data, key=f) # group consecutive items
itertools.accumulate([1, 2, 3])       # 1 3 6
itertools.count(start=1)              # infinite counter
```

---

## 12. Comprehensions

Concise, readable (and fast) way to build collections.

```python
# List comprehension: [expression for item in iterable if condition]
squares = [x * x for x in range(10)]
evens = [x for x in range(20) if x % 2 == 0]
labels = ["even" if x % 2 == 0 else "odd" for x in range(5)]  # if/else goes BEFORE for

# Nested loops (flatten)
matrix = [[1, 2], [3, 4]]
flat = [n for row in matrix for n in row]          # [1, 2, 3, 4]
transposed = [[row[i] for row in matrix] for i in range(2)]  # [[1, 3], [2, 4]]

# Dict comprehension
prices = {"apple": 100, "mango": 150}
discounted = {k: v * 0.9 for k, v in prices.items() if v > 120}

# Set comprehension
unique_lengths = {len(w) for w in ["hi", "hey", "yo"]}   # {2, 3}

# Generator expression (lazy — no list built in memory)
total = sum(x * x for x in range(1_000_000))
any(u.is_admin for u in users)
```

**Best practice**: keep comprehensions to one condition and one or two loops. If it doesn't fit on ~2 lines, use a normal loop.

**List comprehension vs generator expression**: `[...]` builds the whole list in memory; `(...)` yields items one by one (use for large data or when passing straight to `sum/any/max`).

---

## 13. Functions & Arguments

```python
def greet(name: str, greeting: str = "Hello") -> str:
    """Return a greeting."""
    return f"{greeting}, {name}!"

greet("Rohit")                     # positional
greet(name="Rohit", greeting="Hi") # keyword arguments
```

Functions without `return` return `None`. Functions are **first-class objects**: assign, pass, return, store in dicts.

### All kinds of parameters

```python
def func(pos_only, /, normal, *args, kw_only, **kwargs):
    ...
# pos_only   → must be passed positionally (before /)
# normal     → positional or keyword
# *args      → extra positional args as a tuple
# kw_only    → must be passed by keyword (after * or *args)
# **kwargs   → extra keyword args as a dict

func(1, 2, 3, 4, kw_only=5, extra=6)
# pos_only=1, normal=2, args=(3, 4), kw_only=5, kwargs={'extra': 6}
```

```python
def total(*nums):
    return sum(nums)
total(1, 2, 3)            # 6
total(*[1, 2, 3])         # unpack a list into args

def build_user(**fields):
    return fields
build_user(name="A", age=3)          # {'name': 'A', 'age': 3}
build_user(**{"name": "B"})          # unpack a dict into kwargs

# Keyword-only args make call sites readable and safe
def create_user(name, *, is_admin=False, send_email=True): ...
create_user("Rohit", is_admin=True)   # create_user("Rohit", True) → TypeError
```

### The mutable default argument trap (very common interview Q)

Default values are evaluated **once**, when the function is defined — not on every call.

```python
# ❌
def add_item(item, cart=[]):
    cart.append(item)
    return cart

add_item("a")   # ['a']
add_item("b")   # ['a', 'b']  ← shared list across calls!

# ✅
def add_item(item, cart=None):
    if cart is None:
        cart = []
    cart.append(item)
    return cart
```

### Returning multiple values

```python
def stats(nums):
    return min(nums), max(nums), sum(nums) / len(nums)   # tuple

low, high, avg = stats([1, 2, 3])
```

### Functions as objects

```python
def shout(text): return text.upper()
def whisper(text): return text.lower()

handlers = {"loud": shout, "quiet": whisper}
handlers["loud"]("hi")        # 'HI'

def apply(fn, value): return fn(value)
apply(shout, "hey")

shout.__name__, shout.__doc__
```

### Recursion

```python
def factorial(n: int) -> int:
    return 1 if n <= 1 else n * factorial(n - 1)

import sys
sys.getrecursionlimit()   # 1000 by default — Python has no tail-call optimization
```

**Interview Qs**
- `*args` vs `**kwargs`?
- Why is a mutable default argument dangerous?
- What are positional-only (`/`) and keyword-only (`*`) parameters?
- Does Python support function overloading? → Not by signature; the last definition wins. Use default args, `*args`, or `functools.singledispatch`.

---

## 14. Lambda, map, filter, reduce, sorted

**Lambda** = small anonymous single-expression function.

```python
square = lambda x: x * x
add = lambda a, b: a + b

sorted(words, key=lambda w: (len(w), w))
max(users, key=lambda u: u["score"])
```

```python
nums = [1, 2, 3, 4]
list(map(lambda x: x * 2, nums))          # [2, 4, 6, 8]
list(filter(lambda x: x % 2 == 0, nums))  # [2, 4]

from functools import reduce
reduce(lambda acc, x: acc + x, nums, 0)   # 10

# Pythonic alternatives (usually preferred)
[x * 2 for x in nums]
[x for x in nums if x % 2 == 0]
sum(nums)
```

`map` and `filter` return **lazy iterators** in Python 3 (wrap with `list()` to see values).

**Lambda limitations**: one expression only, no statements/annotations. Named `def` functions are better for anything non-trivial (readable tracebacks).

---

## 15. Scope: LEGB, global, nonlocal

Python resolves names in this order — **LEGB**:
1. **L**ocal — inside the current function
2. **E**nclosing — inside enclosing functions (closures)
3. **G**lobal — module level
4. **B**uilt-in — `len`, `print`, `range`…

```python
x = "global"

def outer():
    x = "enclosing"
    def inner():
        x = "local"
        print(x)       # local
    inner()
    print(x)           # enclosing

outer()
print(x)               # global
```

Blocks (`if`, `for`, `while`, `with`) do **NOT** create a new scope (unlike JS `let`):

```python
for i in range(3):
    pass
print(i)   # 2 — loop variable leaks

if True:
    y = 10
print(y)   # 10
```

### global & nonlocal

Assigning to a name inside a function makes it local — unless you declare otherwise.

```python
counter = 0
def increment():
    global counter      # modify the module-level variable
    counter += 1

def make_counter():
    count = 0
    def inc():
        nonlocal count  # modify the enclosing function's variable
        count += 1
        return count
    return inc
```

```python
# UnboundLocalError trap
total = 10
def add():
    total += 1   # UnboundLocalError: assignment makes `total` local, read before assignment
```

**Best practice**: avoid `global`; pass values in and return results.

**Don't shadow built-ins**: `list = [1, 2]` breaks `list()` later in that scope. Same for `id`, `type`, `input`, `sum`, `max`, `dict`, `str`.

---

## 16. Closures

A **closure** is an inner function that **remembers variables from its enclosing scope** even after the outer function has returned.

```python
def multiplier(factor):
    def multiply(n):
        return n * factor     # `factor` is remembered
    return multiply

double = multiplier(2)
triple = multiplier(3)
double(5), triple(5)          # 10 15
double.__closure__[0].cell_contents  # 2
```

```python
# Stateful closure (private state)
def make_bank_account(balance=0):
    def deposit(amount):
        nonlocal balance
        balance += amount
        return balance
    return deposit

deposit = make_bank_account(100)
deposit(50)   # 150
```

### Late binding trap (closures in loops)

Closures capture **variables**, not values. The value is looked up when the function is **called**.

```python
funcs = [lambda: i for i in range(3)]
[f() for f in funcs]          # [2, 2, 2] ❌

funcs = [lambda i=i: i for i in range(3)]   # default arg captures the current value
[f() for f in funcs]          # [0, 1, 2] ✅

from functools import partial
funcs = [partial(lambda x: x, i) for i in range(3)]
```

Use cases: decorators, factories, callbacks, memoization, data hiding.

---

## 17. Decorators

A **decorator** is a function that takes a function and returns a new function that adds behaviour — without changing the original code. `@decorator` is syntax sugar for `func = decorator(func)`.

### Example 1 — basic decorator with functools.wraps

```python
import functools
import time

def timer(func):
    @functools.wraps(func)          # keeps __name__, __doc__ of the original
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)
        elapsed = time.perf_counter() - start
        print(f"{func.__name__} took {elapsed:.4f}s")
        return result
    return wrapper

@timer
def slow_add(a, b):
    time.sleep(0.5)
    return a + b

slow_add(1, 2)   # prints "slow_add took 0.50..s", returns 3
```

Without `@functools.wraps`, `slow_add.__name__` would be `"wrapper"` — breaking logging, debugging and frameworks that inspect functions.

### Example 2 — decorator with arguments (3 levels)

```python
def retry(times=3, delay=0.5, exceptions=(Exception,)):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(1, times + 1):
                try:
                    return func(*args, **kwargs)
                except exceptions as e:
                    if attempt == times:
                        raise
                    print(f"Attempt {attempt} failed: {e}. Retrying…")
                    time.sleep(delay * 2 ** (attempt - 1))   # exponential backoff
        return wrapper
    return decorator

@retry(times=3, exceptions=(ConnectionError,))
def fetch_data():
    ...
```

### Example 3 — real-world decorators

```python
# Caching
@functools.lru_cache(maxsize=128)
def fib(n):
    return n if n < 2 else fib(n - 1) + fib(n - 2)
fib(100)             # instant
fib.cache_info()

@functools.cache     # unbounded cache (3.9+)
def load_config(): ...

# Auth check (like a web framework)
def require_role(role):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(user, *args, **kwargs):
            if role not in user.roles:
                raise PermissionError(f"{role} required")
            return func(user, *args, **kwargs)
        return wrapper
    return decorator

@require_role("admin")
def delete_user(user, user_id): ...

# Registering functions (plugins / routes)
HANDLERS = {}
def register(event):
    def decorator(func):
        HANDLERS[event] = func
        return func
    return decorator

@register("signup")
def on_signup(data): ...
```

### Stacking decorators

Applied **bottom-up**, executed **top-down**:

```python
@timer
@retry(times=2)
def job(): ...
# job = timer(retry(times=2)(job))
```

### Class decorators & decorators as classes

```python
def singleton(cls):
    instances = {}
    @functools.wraps(cls)
    def get(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]
    return get

@singleton
class Database: ...

class CountCalls:                        # a class used as a decorator
    def __init__(self, func):
        functools.update_wrapper(self, func)
        self.func = func
        self.calls = 0
    def __call__(self, *args, **kwargs):
        self.calls += 1
        return self.func(*args, **kwargs)

@CountCalls
def hello(): print("hi")
hello(); hello()
hello.calls   # 2
```

Built-in decorators: `@property`, `@staticmethod`, `@classmethod`, `@functools.cache`, `@functools.lru_cache`, `@functools.wraps`, `@dataclass`, `@contextlib.contextmanager`, `@abc.abstractmethod`, `@typing.override`.

**Interview Qs**
- What is a decorator? Write one that logs/times a function.
- Why use `functools.wraps`?
- How do you write a decorator that takes arguments?
- Order of stacked decorators?
- Real uses? → logging, timing, caching, retries, auth, validation, route registration (Flask/FastAPI use decorators for routes).

---

## 18. Iterators & Generators

### Iterable vs iterator

- **Iterable**: object you can loop over — has `__iter__()` (list, str, dict, file…).
- **Iterator**: object with `__next__()` that returns the next item and raises `StopIteration` when done; also has `__iter__()` returning itself.
- `for` loops call `iter()` then `next()` repeatedly.

```python
nums = [1, 2, 3]
it = iter(nums)
next(it)   # 1
next(it)   # 2
next(it)   # 3
next(it)   # StopIteration

# Custom iterator
class Countdown:
    def __init__(self, start):
        self.current = start
    def __iter__(self):
        return self
    def __next__(self):
        if self.current <= 0:
            raise StopIteration
        self.current -= 1
        return self.current + 1

list(Countdown(3))   # [3, 2, 1]
```

### Generators

A function with `yield` returns a **generator** — an iterator that produces values **lazily**, pausing after each `yield` and keeping its local state.

```python
def countdown(n):
    while n > 0:
        yield n
        n -= 1

gen = countdown(3)
next(gen)          # 3
list(gen)          # [2, 1]  (a generator can be consumed only ONCE)
```

### Example 1 — processing huge files with constant memory

```python
def read_large_file(path):
    with open(path) as f:
        for line in f:           # files are lazy iterators too
            yield line.rstrip("\n")

def errors_only(lines):
    return (line for line in lines if "ERROR" in line)   # generator expression

for line in errors_only(read_large_file("app.log")):     # pipeline, 1 line in memory at a time
    print(line)
```

### Example 2 — infinite sequences & pagination

```python
def fibonacci():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

from itertools import islice
list(islice(fibonacci(), 10))   # [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]

def fetch_all_pages(client, url):
    while url:
        data = client.get(url).json()
        yield from data["items"]       # delegate to another iterable
        url = data.get("next")
```

### Example 3 — send(), return values, yield from

```python
def running_average():
    total, count = 0, 0
    average = None
    while True:
        value = yield average      # receives values via send()
        total += value
        count += 1
        average = total / count

avg = running_average()
next(avg)          # prime the generator
avg.send(10)       # 10.0
avg.send(20)       # 15.0
```

### Generator vs list

| List | Generator |
|---|---|
| All items in memory | One item at a time (lazy) |
| Reusable, indexable, `len()` | Single pass, no indexing |
| Good for small/medium data you reuse | Good for large/infinite streams, pipelines |

```python
import sys
sys.getsizeof([x for x in range(1_000_000)])   # ~8 MB
sys.getsizeof((x for x in range(1_000_000)))   # ~200 bytes
```

**Interview Qs**
- Iterable vs iterator vs generator?
- `yield` vs `return`? → yield pauses and resumes; return ends the function.
- What does `yield from` do? → Delegates to a sub-iterator.
- Why generators? → Memory efficiency, lazy evaluation, pipelines, infinite sequences.

---

## 19. OOP: Classes & Objects

```python
class BankAccount:
    bank_name = "PyBank"              # class attribute — shared by all instances
    interest_rate = 0.04

    def __init__(self, owner: str, balance: float = 0):   # initializer (not constructor)
        self.owner = owner            # instance attributes — per object
        self._balance = balance       # "internal" by convention

    def deposit(self, amount: float) -> "BankAccount":     # instance method
        if amount <= 0:
            raise ValueError("Amount must be positive")
        self._balance += amount
        return self                   # enables chaining

    @property                         # getter — accessed like an attribute
    def balance(self) -> float:
        return self._balance

    @classmethod                      # gets the class, not the instance → alternative constructors
    def from_csv_row(cls, row: str) -> "BankAccount":
        owner, balance = row.split(",")
        return cls(owner, float(balance))

    @staticmethod                     # no self/cls — utility that belongs to the class namespace
    def is_valid_amount(amount) -> bool:
        return isinstance(amount, (int, float)) and amount > 0

    def __repr__(self):
        return f"BankAccount(owner={self.owner!r}, balance={self._balance})"

acc = BankAccount("Rohit", 100).deposit(50)
acc.balance                                # 150 — no parentheses
BankAccount.from_csv_row("Asha,500")
BankAccount.is_valid_amount(-5)            # False
```

### `self`

`self` is the instance, passed **explicitly** as the first parameter. `acc.deposit(50)` is really `BankAccount.deposit(acc, 50)`.

### `__new__` vs `__init__`

- `__new__(cls)` **creates** and returns the instance (rarely overridden: singletons, immutable subclasses).
- `__init__(self)` **initializes** the already-created instance.

### Instance vs class attributes — the trap

```python
class Dog:
    tricks = []                  # ❌ shared by ALL dogs
    def __init__(self, name):
        self.name = name
    def add_trick(self, t):
        self.tricks.append(t)

a, b = Dog("a"), Dog("b")
a.add_trick("roll")
b.tricks                         # ['roll'] ❌

class Dog2:
    def __init__(self, name):
        self.name = name
        self.tricks = []         # ✅ per instance
```

### Methods comparison

| | Instance method | `@classmethod` | `@staticmethod` |
|---|---|---|---|
| First arg | `self` (instance) | `cls` (class) | none |
| Access instance data | ✅ | ❌ | ❌ |
| Access class data | ✅ (via `self.__class__`) | ✅ | ❌ |
| Use for | Behaviour of an object | Factory/alternative constructors, class-level state | Helper related to the class |

### Properties with validation (setter & deleter)

```python
class Product:
    def __init__(self, price):
        self.price = price               # goes through the setter

    @property
    def price(self):
        return self._price

    @price.setter
    def price(self, value):
        if value < 0:
            raise ValueError("Price can't be negative")
        self._price = round(value, 2)

    @property
    def price_with_tax(self):            # computed, read-only
        return round(self._price * 1.18, 2)

p = Product(100)
p.price = -5        # ValueError
p.price_with_tax    # 118.0
```

### Dynamic attributes & introspection

```python
getattr(acc, "owner")                 # 'Rohit'
getattr(acc, "missing", None)
setattr(acc, "nickname", "Ro")
hasattr(acc, "deposit")               # True
vars(acc)                             # instance __dict__
isinstance(acc, BankAccount)
type(acc).__name__                    # 'BankAccount'
dir(acc)                              # all attributes
```

---

## 20. OOP: 4 Pillars, Inheritance & MRO

### 1. Encapsulation

Bundle data + behaviour and control access. Python has **no true private** members — it relies on conventions:

| Syntax | Meaning |
|---|---|
| `name` | public |
| `_name` | internal/protected — "please don't touch" (convention) |
| `__name` | name-mangled to `_ClassName__name` — avoids clashes in subclasses (not security) |

```python
class Account:
    def __init__(self):
        self.__pin = 1234

a = Account()
a.__pin                 # AttributeError
a._Account__pin         # 1234 — still accessible (name mangling, not real privacy)
```

Use `@property` to expose read-only or validated attributes.

### 2. Abstraction — `abc` module

```python
from abc import ABC, abstractmethod

class PaymentGateway(ABC):
    @abstractmethod
    def charge(self, amount: float) -> str: ...

    @abstractmethod
    def refund(self, tx_id: str) -> None: ...

    def pay(self, amount: float) -> str:          # concrete shared logic (template method)
        if amount <= 0:
            raise ValueError("Invalid amount")
        return self.charge(amount)

class StripeGateway(PaymentGateway):
    def charge(self, amount): return "stripe_tx_1"
    def refund(self, tx_id): ...

PaymentGateway()        # TypeError: Can't instantiate abstract class
StripeGateway().pay(100)
```

### 3. Inheritance

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary
    def annual(self):
        return self.salary * 12
    def __repr__(self):
        return f"{type(self).__name__}({self.name!r})"

class Manager(Employee):
    def __init__(self, name, salary, reports=None):
        super().__init__(name, salary)         # call parent initializer
        self.reports = reports or []
    def annual(self):                          # override
        return super().annual() + 10_000 * len(self.reports)

m = Manager("Rohit", 100_000, ["a", "b"])
m.annual()                        # 1,220,000
isinstance(m, Employee)           # True
issubclass(Manager, Employee)     # True
```

### Multiple inheritance & MRO

Python supports multiple inheritance. The **Method Resolution Order (MRO)** — computed with the **C3 linearization** algorithm — decides which parent's method is used.

```python
class A:
    def hello(self): return "A"
class B(A):
    def hello(self): return "B " + super().hello()
class C(A):
    def hello(self): return "C " + super().hello()
class D(B, C):
    def hello(self): return "D " + super().hello()

D().hello()        # 'D B C A'
D.__mro__          # (D, B, C, A, object)
```

`super()` means "**next class in the MRO**", not "my parent" — that's why B's super() calls C here. This is the **diamond problem** solved by MRO.

### Mixins

Small classes that add one capability, meant to be combined.

```python
import json

class JsonMixin:
    def to_json(self):
        return json.dumps(self.__dict__)

class TimestampMixin:
    def touch(self):
        from datetime import datetime, UTC
        self.updated_at = datetime.now(UTC).isoformat()

class User(JsonMixin, TimestampMixin):
    def __init__(self, name):
        self.name = name

u = User("Rohit"); u.touch(); u.to_json()
```

### 4. Polymorphism & duck typing

Same interface, different behaviour. Python uses **duck typing**: if an object has the method, it works — no common base class required.

```python
class Dog:
    def speak(self): return "Woof"
class Cat:
    def speak(self): return "Meow"
class Robot:
    def speak(self): return "Beep"

for thing in (Dog(), Cat(), Robot()):
    print(thing.speak())     # no shared parent needed

len("abc"), len([1, 2]), len({"a": 1})   # built-in polymorphism via __len__
```

`typing.Protocol` formalizes duck typing for type checkers (see Type Hints).

### Composition over inheritance

```python
class Engine:
    def start(self): return "vroom"

class Car:
    def __init__(self, engine: Engine):
        self.engine = engine            # has-a
    def drive(self):
        return self.engine.start()

Car(Engine()).drive()
```

### SOLID in Python (short)

- **S**: one reason to change per class (split `UserService`, `UserRepository`, `EmailSender`).
- **O**: extend with new classes/strategies instead of editing `if/elif` chains.
- **L**: subclasses must honour the parent's contract.
- **I**: small Protocols instead of giant base classes.
- **D**: depend on abstractions (Protocols/ABCs) and inject dependencies (constructor args, FastAPI `Depends`).

**Interview Qs**
- Is there private in Python? → No; `_` convention and `__` name mangling.
- What is MRO? Explain `super()` with multiple inheritance.
- What is the diamond problem and how does Python solve it? → C3 linearization.
- Abstract class vs Protocol? → ABC requires inheritance (nominal); Protocol is structural (duck typing).
- classmethod vs staticmethod?

---

## 21. Dunder (Magic) Methods

"Double underscore" methods let your objects work with Python syntax and built-ins.

| Category | Methods |
|---|---|
| Creation | `__new__`, `__init__`, `__del__` |
| String | `__repr__` (developers/debugging), `__str__` (users/print), `__format__` |
| Comparison | `__eq__`, `__ne__`, `__lt__`, `__le__`, `__gt__`, `__ge__`, `__hash__` |
| Arithmetic | `__add__`, `__sub__`, `__mul__`, `__truediv__`, `__radd__`, `__iadd__`… |
| Containers | `__len__`, `__getitem__`, `__setitem__`, `__delitem__`, `__contains__`, `__iter__`, `__reversed__` |
| Callable | `__call__` |
| Context manager | `__enter__`, `__exit__` (async: `__aenter__`, `__aexit__`) |
| Attribute access | `__getattr__`, `__getattribute__`, `__setattr__` |
| Truthiness | `__bool__` |

### Example 1 — value object with repr, equality, hashing & ordering

```python
from functools import total_ordering

@total_ordering                               # fills in <=, >, >= from __eq__ and __lt__
class Money:
    def __init__(self, amount: int, currency: str = "INR"):
        self.amount = amount                  # in paise
        self.currency = currency

    def __repr__(self):
        return f"Money({self.amount}, {self.currency!r})"
    def __str__(self):
        return f"₹{self.amount / 100:,.2f}"

    def __eq__(self, other):
        if not isinstance(other, Money):
            return NotImplemented
        return (self.amount, self.currency) == (other.amount, other.currency)
    def __hash__(self):                       # needed if __eq__ is defined and objects are used in sets/dict keys
        return hash((self.amount, self.currency))
    def __lt__(self, other):
        return self.amount < other.amount

    def __add__(self, other):
        if self.currency != other.currency:
            raise ValueError("Currency mismatch")
        return Money(self.amount + other.amount, self.currency)
    def __radd__(self, other):                # so sum([...]) works (0 + Money)
        return self if other == 0 else self.__add__(other)
    def __bool__(self):
        return self.amount != 0

total = sum([Money(1000), Money(2550)])
print(total)            # ₹35.50
repr(total)             # Money(3550, 'INR')
Money(5) < Money(10)    # True
{Money(5), Money(5)}    # one item
```

Defining `__eq__` without `__hash__` makes instances **unhashable** (Python sets `__hash__ = None`).

### Example 2 — container behaviour

```python
class Playlist:
    def __init__(self, songs):
        self._songs = list(songs)
    def __len__(self):
        return len(self._songs)
    def __getitem__(self, index):          # enables indexing, slicing AND iteration
        return self._songs[index]
    def __contains__(self, song):
        return song in self._songs
    def __iter__(self):
        return iter(self._songs)

p = Playlist(["a", "b", "c"])
len(p), p[0], p[1:], "b" in p, list(p)
```

### Example 3 — callable objects

```python
class RateLimiter:
    def __init__(self, max_calls):
        self.max_calls = max_calls
        self.calls = 0
    def __call__(self, func_name):
        self.calls += 1
        return self.calls <= self.max_calls

allow = RateLimiter(2)
allow("x"), allow("y"), allow("z")    # True True False
```

**`__repr__` vs `__str__`**: `repr` should be unambiguous (ideally valid code to recreate the object) — used in the REPL, logs, and containers. `str` is for end users. If only `__repr__` is defined, `str()` falls back to it.

---

## 22. Dataclasses, Enums, NamedTuple, __slots__

### dataclasses — auto-generate `__init__`, `__repr__`, `__eq__`

```python
from dataclasses import dataclass, field, asdict

@dataclass
class User:
    id: int
    name: str
    email: str
    tags: list[str] = field(default_factory=list)   # never use a mutable default directly
    active: bool = True

    def __post_init__(self):                        # validation after init
        if "@" not in self.email:
            raise ValueError("invalid email")

u = User(1, "Rohit", "r@x.com")
u                          # User(id=1, name='Rohit', email='r@x.com', tags=[], active=True)
u == User(1, "Rohit", "r@x.com")   # True
asdict(u)                  # dict

@dataclass(frozen=True, slots=True, order=True)     # immutable, hashable, memory-efficient, sortable
class Point:
    x: float
    y: float

p = Point(1, 2)
p.x = 5                    # FrozenInstanceError
sorted([Point(2, 1), Point(1, 5)])
```

**dataclass vs Pydantic**: dataclasses don't validate types at runtime; **Pydantic** models do (used by FastAPI).

### Enum

```python
from enum import Enum, IntEnum, StrEnum, auto

class Status(StrEnum):          # 3.11+: members are also strings
    PENDING = auto()            # "pending"
    PAID = auto()
    SHIPPED = auto()

class Priority(IntEnum):
    LOW = 1
    HIGH = 3

Status.PAID                     # <Status.PAID: 'paid'>
Status.PAID == "paid"           # True (StrEnum)
Status("shipped")               # lookup by value
[s.value for s in Status]       # ['pending', 'paid', 'shipped']
Priority.HIGH > Priority.LOW    # True
```

Enums replace magic strings — typos become errors, IDEs autocomplete.

### `__slots__`

Replaces the per-instance `__dict__` with fixed slots → **less memory, faster attribute access**, and no accidental new attributes.

```python
class Pixel:
    __slots__ = ("x", "y", "color")
    def __init__(self, x, y, color):
        self.x, self.y, self.color = x, y, color

px = Pixel(1, 2, "red")
px.alpha = 1       # AttributeError — can't add new attributes
```

Useful when creating millions of small objects.

---

## 23. Exceptions & Error Handling

```python
try:
    value = int(user_input)
    result = 100 / value
except ValueError:
    print("Not a number")
except ZeroDivisionError as e:
    print("Division by zero:", e)
except (TypeError, KeyError) as e:     # multiple types
    print("Other error:", e)
else:
    print("Runs only if NO exception happened:", result)
finally:
    print("Always runs (cleanup)")
```

### Exception hierarchy (partial)

```
BaseException
 ├── SystemExit, KeyboardInterrupt, GeneratorExit   ← don't catch these normally
 └── Exception
      ├── ValueError, TypeError, KeyError, IndexError, AttributeError
      ├── ZeroDivisionError (ArithmeticError)
      ├── FileNotFoundError, PermissionError (OSError)
      ├── TimeoutError, ConnectionError
      ├── NotImplementedError (RuntimeError)
      └── StopIteration, ImportError, ModuleNotFoundError ...
```

### Raising & custom exceptions

```python
class AppError(Exception):
    """Base class for all app errors."""
    status_code = 500

class NotFoundError(AppError):
    status_code = 404
    def __init__(self, resource: str, id_):
        super().__init__(f"{resource} {id_} not found")
        self.resource = resource
        self.id = id_

class ValidationError(AppError):
    status_code = 400

def get_user(user_id):
    user = db.get(user_id)
    if user is None:
        raise NotFoundError("User", user_id)
    return user

try:
    get_user(42)
except NotFoundError as e:
    print(e, e.status_code)      # User 42 not found 404
```

### Exception chaining

```python
try:
    config = json.loads(raw)
except json.JSONDecodeError as e:
    raise AppError("Invalid config file") from e   # keeps the original as __cause__

raise AppError("clean message") from None          # hide the original context
```

### Re-raising

```python
try:
    process()
except Exception:
    logger.exception("process failed")   # logs with traceback
    raise                                 # re-raise the SAME exception (keeps traceback)
```

### ExceptionGroup & except* (3.11+)

For multiple simultaneous errors (e.g. concurrent tasks).

```python
try:
    raise ExceptionGroup("batch failed", [ValueError("a"), TypeError("b")])
except* ValueError as eg:
    print("value errors:", eg.exceptions)
except* TypeError as eg:
    print("type errors:", eg.exceptions)
```

### EAFP vs LBYL

- **LBYL** (Look Before You Leap): check first — `if key in d: d[key]`.
- **EAFP** (Easier to Ask Forgiveness than Permission): try it and handle the exception — Pythonic, and avoids race conditions.

```python
# LBYL
if os.path.exists(path):
    with open(path) as f: ...      # file could be deleted between check and open (race)

# EAFP
try:
    with open(path) as f: ...
except FileNotFoundError:
    ...
```

### Best practices

- Catch **specific** exceptions. Never bare `except:` (it catches `KeyboardInterrupt`/`SystemExit` too). Avoid `except Exception: pass`.
- Keep `try` blocks **small** — only the lines that can fail.
- Use a custom exception hierarchy for your app/library.
- Add context with `raise ... from e`.
- Log with `logger.exception()` inside `except` to capture the traceback.
- Clean up with `finally` or (better) context managers.

**Interview Qs**
- Purpose of `else` and `finally` in try?
- How to create custom exceptions?
- `raise` vs `raise e` vs `raise X from e`? → `raise` re-raises preserving traceback; `raise e` re-raises from this line; `from e` chains a new exception.
- EAFP vs LBYL?

---

## 24. Context Managers

A **context manager** sets something up and **guarantees cleanup**, even if an exception happens. Used with `with`.

```python
with open("data.txt") as f:        # file closed automatically
    data = f.read()

with lock:                          # threading lock released automatically
    counter += 1

with db.session() as session:       # commit/rollback + close
    ...
```

### Example 1 — class-based (`__enter__` / `__exit__`)

```python
import time

class Timer:
    def __enter__(self):
        self.start = time.perf_counter()
        return self                        # bound to the `as` variable
    def __exit__(self, exc_type, exc, tb):
        self.elapsed = time.perf_counter() - self.start
        print(f"took {self.elapsed:.3f}s")
        return False                       # False → don't suppress exceptions

with Timer() as t:
    sum(range(10_000_000))
```

### Example 2 — generator-based with `contextlib`

```python
from contextlib import contextmanager

@contextmanager
def transaction(conn):
    cursor = conn.cursor()
    try:
        yield cursor              # code inside `with` runs here
        conn.commit()
    except Exception:
        conn.rollback()
        raise
    finally:
        cursor.close()

with transaction(conn) as cur:
    cur.execute("UPDATE accounts SET balance = balance - 100 WHERE id = 1")
    cur.execute("UPDATE accounts SET balance = balance + 100 WHERE id = 2")
```

### Example 3 — useful contextlib helpers

```python
from contextlib import suppress, ExitStack, asynccontextmanager, chdir

with suppress(FileNotFoundError):       # ignore a specific exception
    os.remove("tmp.txt")

with ExitStack() as stack:              # dynamic number of context managers
    files = [stack.enter_context(open(p)) for p in paths]

with open("in.txt") as src, open("out.txt", "w") as dst:   # multiple in one line
    dst.write(src.read())

@asynccontextmanager
async def lifespan(app):                # FastAPI lifespan uses this
    await connect_db()
    yield
    await disconnect_db()
```

---

## 25. Modules & Packages

- **Module**: a `.py` file.
- **Package**: a directory of modules (with `__init__.py`, optional for namespace packages).

```
myapp/
├── pyproject.toml
├── src/
│   └── myapp/
│       ├── __init__.py
│       ├── main.py
│       ├── config.py
│       ├── services/
│       │   ├── __init__.py
│       │   └── users.py
│       └── utils/
│           └── dates.py
└── tests/
```

```python
import math
import numpy as np                       # alias
from datetime import datetime, timedelta
from myapp.services.users import get_user    # absolute import (preferred)
from .users import get_user              # relative import (inside a package)
from ..utils.dates import parse_date
from math import *                       # ❌ pollutes namespace — avoid
```

### `if __name__ == "__main__":`

`__name__` is `"__main__"` when the file is run directly, and the module name when imported. Guard script code so it doesn't run on import.

```python
# utils.py
def add(a, b): return a + b

if __name__ == "__main__":
    print(add(2, 3))     # runs with `python utils.py`, not with `import utils`
```

### How imports work

1. Check `sys.modules` cache → modules execute **once** per process (singleton-like).
2. Search `sys.path` (script dir, PYTHONPATH, site-packages).
3. Execute the module top to bottom, create the module object, cache it.

```python
import sys
sys.path
import importlib
importlib.reload(module)   # re-execute (dev only)
```

### `__init__.py` uses

- Marks a regular package, runs on package import.
- Re-export a clean public API: `from .users import get_user` → `from myapp.services import get_user`.
- `__all__ = ["get_user"]` controls `from package import *`.

### Circular imports

`a` imports `b` which imports `a` → partially initialized module errors. Fix: move shared code to a third module, import inside functions, or import the module (`import a`) rather than names.

---

## 26. Installing Packages: pip, venv, uv & pyproject.toml

You need this once you use **third-party packages** (requests, FastAPI, pandas…) or start a real project. Plain Python scripts that only use the standard library don't need any of it.

### Virtual environments

Isolate each project's dependencies so projects don't conflict.

```bash
python3 -m venv .venv            # create
source .venv/bin/activate        # activate (macOS/Linux)
.venv\Scripts\activate           # Windows
pip install requests fastapi     # installs into .venv only
pip freeze > requirements.txt    # pin exact versions
pip install -r requirements.txt
deactivate
```

### uv — the modern fast tool (recommended)

`uv` (by Astral) replaces pip, venv, pip-tools, pyenv and poetry — and is 10–100x faster.

```bash
uv init my-app          # creates pyproject.toml
uv add fastapi httpx    # add deps (updates pyproject + uv.lock)
uv add --dev pytest ruff mypy
uv run main.py          # runs inside the project venv automatically
uv sync                 # install exactly from the lockfile
uv python install 3.13  # manage Python versions
```

### pyproject.toml — the standard project config

```toml
[project]
name = "my-app"
version = "0.1.0"
requires-python = ">=3.12"
dependencies = [
  "fastapi>=0.115",
  "httpx>=0.27",
]

[dependency-groups]
dev = ["pytest>=8", "ruff>=0.6", "mypy>=1.11"]

[tool.ruff]
line-length = 100

[tool.pytest.ini_options]
testpaths = ["tests"]
```

Other tools: **poetry**, **pipenv**, **conda** (data science), **pyenv** (Python versions).

Building and publishing your **own** package (wheels, the `src` layout, `py.typed`, versions, PyPI): Section 43.

**Interview Qs**
- Why virtual environments? → Per-project dependency isolation, reproducibility.
- requirements.txt vs pyproject.toml vs lockfile? → requirements lists packages (often pinned); pyproject declares project metadata & deps; lockfiles (uv.lock/poetry.lock) pin the full dependency tree.

---

## 27. File Handling, pathlib, JSON, CSV

```python
# Modes: "r" read, "w" write (truncate), "a" append, "x" create (fail if exists), "b" binary, "+" read/write
with open("notes.txt", "w", encoding="utf-8") as f:
    f.write("line 1\n")
    f.writelines(["line 2\n", "line 3\n"])

with open("notes.txt", encoding="utf-8") as f:
    content = f.read()          # whole file
with open("notes.txt", encoding="utf-8") as f:
    for line in f:              # line by line — memory efficient
        print(line.strip())

with open("image.png", "rb") as f:
    header = f.read(8)
```

Always pass `encoding="utf-8"` — the default depends on the OS.

### pathlib (modern, preferred over os.path)

```python
from pathlib import Path

base = Path(__file__).resolve().parent
config_path = base / "config" / "settings.json"     # "/" joins paths
config_path.exists(); config_path.is_file()
config_path.name, config_path.stem, config_path.suffix, config_path.parent
text = config_path.read_text(encoding="utf-8")
Path("out.txt").write_text("hello", encoding="utf-8")
Path("logs").mkdir(parents=True, exist_ok=True)
for py in Path("src").rglob("*.py"):                 # recursive glob
    print(py)
Path("old.txt").rename("new.txt")
Path("tmp.txt").unlink(missing_ok=True)
```

### JSON

```python
import json

data = {"name": "Rohit", "skills": ["py", "js"], "active": True, "score": None}
text = json.dumps(data, indent=2)          # dict → str   (True→true, None→null)
obj = json.loads(text)                      # str → dict

with open("data.json", "w", encoding="utf-8") as f:
    json.dump(data, f, indent=2, ensure_ascii=False)
with open("data.json", encoding="utf-8") as f:
    loaded = json.load(f)

# Non-serializable types (datetime, Decimal, sets) → default=
from datetime import datetime
json.dumps({"at": datetime.now()}, default=str)
```

### CSV

```python
import csv

with open("users.csv", newline="", encoding="utf-8") as f:
    for row in csv.DictReader(f):            # each row is a dict keyed by header
        print(row["name"], row["email"])

with open("out.csv", "w", newline="", encoding="utf-8") as f:
    writer = csv.DictWriter(f, fieldnames=["name", "email"])
    writer.writeheader()
    writer.writerows([{"name": "A", "email": "a@x.com"}])
```

---

## 28. Databases Without an ORM (sqlite3, psycopg 3)

ORMs (SQLAlchemy — see `fastapi.md`) are great for applications, but you should also be comfortable with **plain SQL from Python**: scripts, data jobs, reports, performance-critical queries, and understanding what the ORM does for you.

### 1. The DB-API pattern

Almost every Python database driver follows **DB-API 2.0 (PEP 249)**:

```
connect → cursor → execute(sql, params) → fetchone / fetchall / iterate → commit (or rollback) → close
```

### 2. sqlite3 (built in — no server needed)

```python
import sqlite3
from contextlib import closing

def connect(path: str = "shop.db") -> sqlite3.Connection:
    conn = sqlite3.connect(path)
    conn.row_factory = sqlite3.Row                     # rows behave like dicts: row["email"]
    conn.execute("PRAGMA foreign_keys = ON")           # OFF by default in SQLite!
    conn.execute("PRAGMA journal_mode = WAL")          # better concurrency for readers + a writer
    return conn

with closing(connect(":memory:")) as conn:             # closing() actually closes the connection
    with conn:                                         # transaction: commit on success, rollback on exception
        conn.executescript("""
            CREATE TABLE users (
                id INTEGER PRIMARY KEY,
                email TEXT NOT NULL UNIQUE,
                name TEXT NOT NULL,
                created_at TEXT NOT NULL DEFAULT (datetime('now'))
            );
            CREATE TABLE orders (
                id INTEGER PRIMARY KEY,
                user_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
                total_paise INTEGER NOT NULL CHECK (total_paise >= 0)
            );
            CREATE INDEX idx_orders_user ON orders(user_id);
        """)

    with conn:
        cur = conn.execute("INSERT INTO users (email, name) VALUES (?, ?)", ("r@x.com", "Rohit"))
        user_id = cur.lastrowid
        conn.executemany(
            "INSERT INTO orders (user_id, total_paise) VALUES (?, ?)",
            [(user_id, 49900), (user_id, 129900)],
        )

    row = conn.execute("SELECT id, email, name FROM users WHERE email = ?", ("r@x.com",)).fetchone()
    print(row["name"], dict(row))                      # Rohit {'id': 1, 'email': 'r@x.com', 'name': 'Rohit'}

    total = conn.execute(
        "SELECT COALESCE(SUM(total_paise), 0) FROM orders WHERE user_id = :uid", {"uid": user_id}   # named params
    ).fetchone()[0]                                    # 179800
```

**Gotcha**: `with sqlite3.connect(...) as conn:` manages the **transaction**, it does **not close** the connection. Use `contextlib.closing(...)` or call `conn.close()`.

### 3. SQL injection — always use parameters

```python
email = "x' OR '1'='1"

# ❌ string formatting → the input becomes SQL
conn.execute(f"SELECT * FROM users WHERE email = '{email}'")            # returns EVERY user

# ✅ placeholders → the driver sends the value separately; it can never change the query
conn.execute("SELECT * FROM users WHERE email = ?", (email,))            # returns nothing
```

Placeholders work only for **values**, not identifiers (table/column names) or keywords (`ASC`/`DESC`). For dynamic identifiers, **whitelist**:

```python
SORTABLE = {"name": "name", "newest": "created_at"}

def list_users(conn, sort: str = "newest", descending: bool = True, limit: int = 20):
    column = SORTABLE.get(sort)
    if column is None:
        raise ValueError(f"invalid sort: {sort}")
    direction = "DESC" if descending else "ASC"          # chosen by code, not copied from input
    return conn.execute(f"SELECT id, email, name FROM users ORDER BY {column} {direction} LIMIT ?", (limit,)).fetchall()
```

### 4. Transactions

A **transaction** makes several statements **all-or-nothing**.

```python
import sqlite3

class InsufficientFunds(Exception): ...

def transfer(conn: sqlite3.Connection, from_id: int, to_id: int, amount_paise: int) -> None:
    if amount_paise <= 0:
        raise ValueError("amount must be positive")
    with conn:                                           # BEGIN … COMMIT, or ROLLBACK on any exception
        cur = conn.execute(
            "UPDATE accounts SET balance = balance - ? WHERE id = ? AND balance >= ?",
            (amount_paise, from_id, amount_paise),       # condition in SQL → no race between check & update
        )
        if cur.rowcount != 1:
            raise InsufficientFunds(f"account {from_id} can't send {amount_paise}")
        conn.execute("UPDATE accounts SET balance = balance + ? WHERE id = ?", (amount_paise, to_id))
```

- Keep transactions **short**; never wait on user input or slow network calls inside one.
- Check-then-update in Python (`SELECT balance` → `if` → `UPDATE`) is a **race condition** under concurrency — put the condition in the `UPDATE`, use `SELECT … FOR UPDATE` (Postgres) or a unique constraint.
- Postgres isolation levels: `READ COMMITTED` (default), `REPEATABLE READ`, `SERIALIZABLE` (retry on serialization failures).

### 5. Upserts, RETURNING & bulk inserts

```python
# Upsert: insert or update on conflict (SQLite 3.24+, Postgres)
conn.execute(
    """INSERT INTO inventory (sku, qty) VALUES (?, ?)
       ON CONFLICT (sku) DO UPDATE SET qty = inventory.qty + excluded.qty""",
    ("PH-1", 5),
)

# RETURNING: get generated values without a second query (SQLite 3.35+, Postgres)
new_id = conn.execute("INSERT INTO users (email, name) VALUES (?, ?) RETURNING id", ("a@x.com", "A")).fetchone()[0]

# Bulk insert in batches, one transaction per batch
from itertools import islice

def insert_many(conn, rows, batch_size: int = 1000) -> int:
    it, inserted = iter(rows), 0
    while batch := list(islice(it, batch_size)):
        with conn:
            conn.executemany("INSERT INTO events (kind, payload) VALUES (?, ?)", batch)
        inserted += len(batch)
    return inserted
```

### 6. A tiny repository layer

```python
import sqlite3
from dataclasses import dataclass

@dataclass(frozen=True)
class User:
    id: int
    email: str
    name: str

class UserRepository:
    def __init__(self, conn: sqlite3.Connection):
        self.conn = conn

    def get_by_email(self, email: str) -> User | None:
        row = self.conn.execute("SELECT id, email, name FROM users WHERE email = ?", (email.lower(),)).fetchone()
        return User(**dict(row)) if row else None

    def create(self, email: str, name: str) -> User:
        with self.conn:
            row = self.conn.execute(
                "INSERT INTO users (email, name) VALUES (?, ?) RETURNING id, email, name", (email.lower(), name)
            ).fetchone()
        return User(**dict(row))

    def page_after(self, after_id: int = 0, limit: int = 20) -> list[User]:      # keyset pagination
        rows = self.conn.execute(
            "SELECT id, email, name FROM users WHERE id > ? ORDER BY id LIMIT ?", (after_id, limit)
        ).fetchall()
        return [User(**dict(r)) for r in rows]
```

### 7. Minimal migrations with `PRAGMA user_version`

For small tools/scripts (use Alembic for real apps):

```python
import sqlite3

MIGRATIONS = [
    "CREATE TABLE notes (id INTEGER PRIMARY KEY, body TEXT NOT NULL)",                   # version 1
    "ALTER TABLE notes ADD COLUMN created_at TEXT NOT NULL DEFAULT (datetime('now'))",   # version 2
    "CREATE INDEX idx_notes_created ON notes(created_at)",                               # version 3
]

def migrate(conn: sqlite3.Connection) -> int:
    current = conn.execute("PRAGMA user_version").fetchone()[0]
    for version, statement in enumerate(MIGRATIONS[current:], start=current + 1):
        with conn:
            conn.execute(statement)
            conn.execute(f"PRAGMA user_version = {int(version)}")     # int() — never interpolate raw input
    return conn.execute("PRAGMA user_version").fetchone()[0]
```

### 8. PostgreSQL with psycopg 3

```python
import psycopg
from psycopg import sql
from psycopg.rows import dict_row
from psycopg_pool import ConnectionPool

DSN = "postgresql://app:secret@localhost:5432/shop"

# Connection as context manager: commits on success, rolls back on error, then closes
with psycopg.connect(DSN, row_factory=dict_row) as conn:
    user = conn.execute("SELECT id, email FROM users WHERE email = %s", ("r@x.com",)).fetchone()   # %s placeholders
    conn.execute(
        "INSERT INTO audit_log (user_id, action) VALUES (%(uid)s, %(action)s)",
        {"uid": user["id"], "action": "login"},
    )

# Safe dynamic identifiers
query = sql.SQL("SELECT {col} FROM {table} WHERE id = %s").format(
    col=sql.Identifier("email"), table=sql.Identifier("users")
)

# Connection pool for services (reuse connections instead of opening one per request)
pool = ConnectionPool(DSN, min_size=2, max_size=10, kwargs={"row_factory": dict_row})
with pool.connection() as conn:
    rows = conn.execute("SELECT id, email FROM users ORDER BY id LIMIT %s", (20,)).fetchall()

# Fastest bulk load: COPY
with psycopg.connect(DSN) as conn, conn.cursor() as cur:
    with cur.copy("COPY events (kind, payload) FROM STDIN") as copy:
        for kind, payload in events:
            copy.write_row((kind, payload))
```

Async: `psycopg.AsyncConnection` / `psycopg_pool.AsyncConnectionPool`, or **asyncpg** (very fast, `$1, $2` placeholders).

Placeholder styles differ by driver: sqlite3 `?` / `:name`, psycopg `%s` / `%(name)s`, asyncpg `$1`. None of them are Python string formatting.

### 9. Performance basics

```python
conn.execute("EXPLAIN QUERY PLAN SELECT * FROM orders WHERE user_id = ?", (1,)).fetchall()
# → [(…, 'SEARCH orders USING INDEX idx_orders_user (user_id=?)')]  — uses the index ✅ (no "SCAN orders")
```

- Index columns used in `WHERE`, `JOIN`, `ORDER BY`; check plans (`EXPLAIN QUERY PLAN` in SQLite, `EXPLAIN ANALYZE` in Postgres).
- Select only needed columns; paginate with keyset (`WHERE id > ?`) for large tables.
- Batch writes in transactions (one transaction per row is slow, especially in SQLite).
- Stream large results (`for row in cursor`) instead of `fetchall()`.
- Reuse connections (pools) in services.

### Best practices

- Parameters for every value; whitelist identifiers.
- Transactions around multi-step writes; conditions in SQL to avoid races.
- Constraints in the database (`NOT NULL`, `UNIQUE`, `CHECK`, foreign keys — remember `PRAGMA foreign_keys = ON` in SQLite).
- Close connections (`closing()`, pools); keep transactions short.
- Money as integer minor units; timestamps in UTC (ISO strings in SQLite, `timestamptz` in Postgres).
- Versioned migrations; in-memory SQLite or a disposable Postgres for tests.

### Interview Qs

1. What is DB-API 2.0? Walk through connect → cursor → execute → commit.
2. How do parameterized queries prevent SQL injection? Why can't you parameterize a table name?
3. What does `with sqlite3.connect() as conn` do (and not do)?
4. How do you make a money transfer safe under concurrent requests?
5. Upsert and `RETURNING` — why use them?
6. How do you insert a million rows efficiently?
7. What is keyset pagination and why is it faster than `OFFSET`?

---

## 29. Standard Library Essentials

### collections

```python
from collections import Counter, defaultdict, deque, OrderedDict, ChainMap

Counter("mississippi").most_common(2)      # [('i', 4), ('s', 4)]
Counter(a=3) + Counter(a=1, b=2)           # Counter({'a': 4, 'b': 2})

graph = defaultdict(list)
graph["a"].append("b")                     # no KeyError

q = deque([1, 2, 3], maxlen=5)             # O(1) appends/pops at BOTH ends
q.appendleft(0); q.pop(); q.popleft(); q.rotate(1)

lru = OrderedDict()                        # move_to_end / popitem(last=False) → LRU caches
settings = ChainMap(cli_args, env_vars, defaults)   # layered lookups
```

### functools

```python
from functools import lru_cache, cache, partial, reduce, wraps, cached_property, singledispatch

pow2 = partial(pow, exp=2)          # pre-fill arguments
pow2(5)                             # 25

class Report:
    @cached_property                # computed once per instance, then cached
    def data(self): return expensive_query()

@singledispatch                     # function overloading by type of first arg
def to_json(obj): raise TypeError
@to_json.register
def _(obj: list): return "[...]"
@to_json.register
def _(obj: dict): return "{...}"
```

### datetime & zoneinfo

```python
from datetime import datetime, date, timedelta, UTC
from zoneinfo import ZoneInfo

now = datetime.now(UTC)                         # ✅ timezone-aware
ist = now.astimezone(ZoneInfo("Asia/Kolkata"))
tomorrow = date.today() + timedelta(days=1)
now.isoformat()                                  # '2026-09-24T07:30:00.123456+00:00'
datetime.fromisoformat("2026-09-24T10:00:00+05:30")
now.strftime("%d %b %Y, %H:%M")                  # format
datetime.strptime("24/09/2026", "%d/%m/%Y")      # parse
(datetime(2026, 12, 25, tzinfo=UTC) - now).days
```

Avoid naive datetimes (`datetime.now()` without tz, `datetime.utcnow()` is deprecated). Store UTC, convert for display.

### os, sys, shutil, subprocess

```python
import os, sys, shutil, subprocess
os.environ.get("DATABASE_URL", "sqlite:///dev.db")
os.getcwd(); os.listdir(".")
sys.argv; sys.exit(1); sys.version
shutil.copy("a.txt", "b.txt"); shutil.rmtree("build")
result = subprocess.run(["git", "status"], capture_output=True, text=True, check=True)
result.stdout
```

### Others worth knowing

`math`, `statistics`, `random` (use `secrets` for tokens/passwords!), `secrets.token_urlsafe(32)`, `uuid.uuid4()`, `hashlib.sha256()`, `hmac`, `base64`, `itertools`, `heapq` (priority queue), `bisect` (binary search on sorted lists), `argparse` (CLIs), `logging`, `time`, `copy`, `pprint`, `textwrap`, `tempfile`, `sqlite3`, `urllib.parse`, `http.server`, `concurrent.futures`, `asyncio`, `typing`, `dataclasses`, `enum`, `abc`, `contextlib`, `pathlib`, `json`, `csv`, `re`, `unittest`.

```python
import heapq
tasks = []
heapq.heappush(tasks, (2, "write code"))
heapq.heappush(tasks, (1, "drink coffee"))
heapq.heappop(tasks)                 # (1, 'drink coffee') — min-heap
heapq.nlargest(3, scores)

import bisect
grades = [60, 70, 80, 90]
bisect.bisect(grades, 85)            # 3 — insertion index (binary search O(log n))

import secrets
secrets.token_hex(16)                # cryptographically secure
```

---

## 30. Scripting & Automation

Python's superpower for everyday work: automate boring tasks (renaming files, reports, backups, data cleanup, API syncs, scraping) with small, reliable scripts.

### 1. Anatomy of a good script

```python
#!/usr/bin/env python3
"""Clean up old log files. Usage: python cleanup.py LOG_DIR --days 30 [--dry-run]"""
import argparse
import logging
import sys
import time
from pathlib import Path

log = logging.getLogger("cleanup")

def parse_args(argv=None):
    parser = argparse.ArgumentParser(description="Delete log files older than N days.")
    parser.add_argument("log_dir", type=Path, help="folder containing .log files")
    parser.add_argument("--days", type=int, default=30, help="age threshold in days (default: 30)")
    parser.add_argument("--dry-run", action="store_true", help="show what would be deleted, delete nothing")
    parser.add_argument("-v", "--verbose", action="store_true")
    return parser.parse_args(argv)

def find_old_files(folder: Path, days: int, now: float | None = None) -> list[Path]:
    cutoff = (now or time.time()) - days * 86_400
    return sorted(p for p in folder.glob("*.log") if p.is_file() and p.stat().st_mtime < cutoff)

def main(argv=None) -> int:
    args = parse_args(argv)
    logging.basicConfig(level=logging.DEBUG if args.verbose else logging.INFO, format="%(levelname)s %(message)s")
    if not args.log_dir.is_dir():
        log.error("Not a directory: %s", args.log_dir)
        return 2                                        # non-zero exit code = failure (for cron/CI)
    old = find_old_files(args.log_dir, args.days)
    for path in old:
        if args.dry_run:
            log.info("[dry-run] would delete %s", path)
        else:
            path.unlink()
            log.info("deleted %s", path)
    log.info("%d file(s) %s", len(old), "matched" if args.dry_run else "deleted")
    return 0

if __name__ == "__main__":
    sys.exit(main())
```

Good-script checklist:
- `main()` + `if __name__ == "__main__":` → importable and testable.
- **argparse/typer** for arguments with `--help`; sensible defaults.
- **`--dry-run`** for anything destructive; confirm before bulk deletes.
- **logging** instead of print; `-v` for verbose.
- **Exit codes**: `0` success, non-zero failure (cron, CI and shell scripts rely on them).
- **Idempotent**: safe to run twice (skip already-processed items).
- Config/secrets from **env vars / `.env`**, never hard-coded.
- Handle errors per item (log and continue) vs fail fast — decide deliberately.

### 2. CLIs with subcommands: argparse, click & typer

```python
# argparse subcommands: tool.py users list --active / tool.py users add NAME
import argparse

def build_parser():
    parser = argparse.ArgumentParser(prog="tool")
    sub = parser.add_subparsers(dest="command", required=True)

    users = sub.add_parser("users", help="manage users").add_subparsers(dest="action", required=True)
    list_cmd = users.add_parser("list")
    list_cmd.add_argument("--active", action="store_true")
    add_cmd = users.add_parser("add")
    add_cmd.add_argument("name")
    add_cmd.add_argument("--role", choices=["admin", "viewer"], default="viewer")
    return parser

args = build_parser().parse_args(["users", "add", "Rohit", "--role", "admin"])
# Namespace(command='users', action='add', name='Rohit', role='admin')
```

```python
# click — decorators, used by Flask, pip-tools, and many CLIs
import click

@click.group()
def cli():
    """Shop admin tool."""

@cli.command()
@click.argument("name")
@click.option("--role", type=click.Choice(["admin", "viewer"]), default="viewer", show_default=True)
@click.option("--notify/--no-notify", default=True)
def add_user(name, role, notify):
    """Add a user."""
    click.echo(f"Added {name} as {role}" + (" (notified)" if notify else ""))

if __name__ == "__main__":
    cli()
```

```python
# typer — built on click, uses type hints (the FastAPI of CLIs)
import typer

app = typer.Typer(help="Shop admin tool")

@app.command()
def add_user(name: str, role: str = "viewer", notify: bool = True):
    """Add a user."""
    typer.echo(f"Added {name} as {role}")

@app.command()
def export(path: str = "users.csv", limit: int = typer.Option(100, min=1, max=10_000)):
    """Export users to CSV."""
    ...

if __name__ == "__main__":
    app()          # python admin.py add-user Rohit --role admin --no-notify
```

Pretty terminal output: **rich** (tables, progress bars, colored logs), **tqdm** (progress bars).

### 3. Files & folders: batch jobs with pathlib

```python
from pathlib import Path
import shutil

CATEGORIES = {
    "images": {".jpg", ".jpeg", ".png", ".gif", ".webp"},
    "docs": {".pdf", ".docx", ".txt", ".md"},
    "archives": {".zip", ".tar", ".gz"},
}

def organize(folder: Path, dry_run: bool = False) -> dict[str, int]:
    """Move files into subfolders by type (Downloads cleanup)."""
    moved: dict[str, int] = {}
    for file in folder.iterdir():
        if not file.is_file():
            continue
        category = next((c for c, exts in CATEGORIES.items() if file.suffix.lower() in exts), "other")
        target_dir = folder / category
        target = target_dir / file.name
        counter = 1
        while target.exists():                               # never overwrite: add a suffix
            target = target_dir / f"{file.stem} ({counter}){file.suffix}"
            counter += 1
        if not dry_run:
            target_dir.mkdir(exist_ok=True)
            shutil.move(file, target)
        moved[category] = moved.get(category, 0) + 1
    return moved

def bulk_rename(folder: Path, prefix: str) -> list[tuple[str, str]]:
    """photo.jpg, img2.jpg → trip_001.jpg, trip_002.jpg (sorted by modification time)."""
    files = sorted((p for p in folder.glob("*.jpg")), key=lambda p: p.stat().st_mtime)
    renames = []
    for i, path in enumerate(files, start=1):
        new_path = path.with_name(f"{prefix}_{i:03d}{path.suffix}")
        path.rename(new_path)
        renames.append((path.name, new_path.name))
    return renames

def largest_files(folder: Path, n: int = 10) -> list[tuple[int, Path]]:
    files = ((p.stat().st_size, p) for p in folder.rglob("*") if p.is_file())
    return sorted(files, reverse=True)[:n]
```

Also: `shutil.copytree`, `shutil.make_archive("backup", "zip", folder)`, `tempfile.TemporaryDirectory()` for scratch work, `hashlib` to find duplicate files by content hash.

### 4. Running other programs: subprocess

```python
import subprocess

# ✅ list of args (no shell), capture output, fail on error, timeout
result = subprocess.run(
    ["git", "log", "-1", "--pretty=%h %s"],
    capture_output=True, text=True, check=True, timeout=10,
)
print(result.stdout.strip())

try:
    subprocess.run(["pg_dump", "--version"], check=True, capture_output=True, text=True, timeout=10)
except FileNotFoundError:
    print("pg_dump is not installed")
except subprocess.CalledProcessError as e:
    print("failed:", e.returncode, e.stderr)
except subprocess.TimeoutExpired:
    print("took too long")

# Stream output of a long-running command line by line
with subprocess.Popen(["ping", "-c", "3", "example.com"], stdout=subprocess.PIPE, text=True) as proc:
    for line in proc.stdout:
        print(">", line.rstrip())
```

**Never** `subprocess.run(f"convert {user_input}", shell=True)` — shell injection. Pass a list of arguments.

### 5. HTTP automation (APIs)

```python
import httpx
import time
from pathlib import Path

def fetch_all_pages(base_url: str, token: str) -> list[dict]:
    """Paginate through an API politely: timeouts, retries on 429/5xx, rate limiting."""
    items, url = [], f"{base_url}/items?page=1"
    headers = {"Authorization": f"Bearer {token}"}
    with httpx.Client(timeout=httpx.Timeout(10.0, connect=3.0), headers=headers) as client:   # reuse connections
        while url:
            for attempt in range(4):
                resp = client.get(url)
                if resp.status_code == 429 or resp.status_code >= 500:
                    wait = int(resp.headers.get("Retry-After", 2 ** attempt))
                    time.sleep(wait)                         # back off
                    continue
                resp.raise_for_status()
                break
            else:
                raise RuntimeError(f"giving up on {url}")
            data = resp.json()
            items.extend(data["items"])
            url = data.get("next")                           # None on the last page
            time.sleep(0.2)                                  # stay under rate limits
    return items

def download(url: str, dest: Path) -> None:
    """Stream large downloads to disk (constant memory)."""
    with httpx.stream("GET", url, timeout=30, follow_redirects=True) as r:
        r.raise_for_status()
        with dest.open("wb") as f:
            for chunk in r.iter_bytes(chunk_size=1 << 16):
                f.write(chunk)
```

For many concurrent requests use `httpx.AsyncClient` + `asyncio.gather` with a `Semaphore` (see asyncio).

### 6. Web scraping (responsibly)

**Prefer an official API.** If you must scrape: check the site's **Terms of Service** and **robots.txt**, identify your bot (User-Agent), rate-limit, cache pages, and never scrape personal data you're not allowed to collect.

```python
import httpx
from bs4 import BeautifulSoup
from urllib.robotparser import RobotFileParser

BASE = "https://books.toscrape.com/"                      # a sandbox site made for practice
robots = RobotFileParser(BASE + "robots.txt"); robots.read()

def scrape_books(page_url: str) -> list[dict]:
    if not robots.can_fetch("MyBot/1.0", page_url):
        raise PermissionError("Disallowed by robots.txt")
    html = httpx.get(page_url, headers={"User-Agent": "MyBot/1.0 (contact@example.com)"}, timeout=10).text
    soup = BeautifulSoup(html, "html.parser")
    books = []
    for card in soup.select("article.product_pod"):       # CSS selectors
        books.append({
            "title": card.h3.a["title"],
            "price": card.select_one(".price_color").get_text(strip=True),
            "in_stock": "In stock" in card.select_one(".availability").get_text(),
        })
    return books
```

JavaScript-rendered sites → **Playwright** (headless browser). Large crawls → **Scrapy** (scheduling, retries, pipelines, throttling built in).

### 7. CSV, Excel & JSON data processing

```python
import csv
import logging
from collections import defaultdict
from decimal import Decimal
from pathlib import Path

def sales_by_region(csv_path: Path) -> dict[str, Decimal]:
    """Stream a big CSV row by row (constant memory)."""
    totals: dict[str, Decimal] = defaultdict(Decimal)
    with csv_path.open(newline="", encoding="utf-8") as f:
        for row in csv.DictReader(f):
            try:
                region, amount = row["region"].strip(), Decimal(row["amount"])
            except (KeyError, ArithmeticError):             # Decimal("abc") raises InvalidOperation (an ArithmeticError)
                logging.warning("skipping bad row: %r", row)
                continue
            totals[region] += amount                        # parse FIRST: `totals[k] += Decimal(bad)` would still
    return dict(totals)                                     # create totals[k] = 0 before the conversion fails

def write_report(rows: list[dict], out: Path) -> None:
    with out.open("w", newline="", encoding="utf-8") as f:
        writer = csv.DictWriter(f, fieldnames=["region", "total"])
        writer.writeheader()
        writer.writerows(rows)
```

```python
# pandas for analysis / Excel (pip install pandas openpyxl)
import pandas as pd

df = pd.read_csv("sales.csv", parse_dates=["date"])
df = df.dropna(subset=["amount"])
summary = (
    df.assign(month=df["date"].dt.to_period("M"))
      .groupby(["month", "region"], as_index=False)["amount"].sum()
      .sort_values(["month", "amount"], ascending=[True, False])
)
summary.to_excel("monthly_sales.xlsx", index=False)      # Excel output
pd.read_excel("input.xlsx", sheet_name="Orders")          # Excel input

# Huge files: process in chunks
for chunk in pd.read_csv("huge.csv", chunksize=100_000):
    process(chunk)
```

### 8. Scheduling scripts

| Option | Use for |
|---|---|
| **cron** (Linux/macOS) | Classic: `0 2 * * * /usr/bin/python3 /opt/jobs/backup.py >> /var/log/backup.log 2>&1` (daily 2 AM) |
| **systemd timers** | Linux servers; better logging/retries than cron |
| **GitHub Actions `schedule`** | Scripts living in a repo (reports, syncs) — no server needed |
| **APScheduler** / `schedule` library | Scheduling inside a long-running Python process |
| **Celery beat** / cloud schedulers (EventBridge, Cloud Scheduler) | Production apps & distributed jobs |
| Windows Task Scheduler | Windows machines |

```
# cron format:  minute hour day-of-month month day-of-week
*/15 * * * *   every 15 minutes
0 9 * * 1-5    09:00 on weekdays
30 1 1 * *     01:30 on the 1st of every month
```

Cron gotchas: minimal environment (use absolute paths, set PATH, activate the venv's Python directly: `/opt/app/.venv/bin/python`), log output to a file, make jobs **idempotent** and prevent overlapping runs (lock file, `flock`).

### 9. Config & secrets for scripts

```python
import os
from dotenv import load_dotenv          # pip install python-dotenv

load_dotenv()                            # reads .env in the current folder (never commit it)
API_TOKEN = os.environ["API_TOKEN"]      # KeyError → fail fast if missing
DB_URL = os.getenv("DB_URL", "sqlite:///local.db")
```

### 10. Packaging a CLI tool

```toml
# pyproject.toml
[project]
name = "shoptool"
version = "0.1.0"
dependencies = ["typer>=0.12", "httpx>=0.27"]

[project.scripts]
shoptool = "shoptool.cli:app"          # creates a `shoptool` command on install
```

```bash
uv tool install .        # or: pipx install .   → `shoptool --help` works anywhere, in its own venv
```

This builds even without a `[build-system]` table (installers fall back to setuptools), but declare one explicitly. For a full walkthrough, see Section 43.

### Best practices

- Start small: a function + `main()`; grow into a package only when needed.
- `--dry-run`, logging, clear exit codes, `--help` text.
- Use `pathlib`, `with` for files, `encoding="utf-8"`, streaming for big data.
- Timeouts and retries for every network call; respect rate limits and robots.txt.
- Idempotent & resumable jobs (checkpoint progress for long runs).
- Keep secrets in env vars; never print them.
- Test the core functions (pure logic) with pytest; use `tmp_path` for file tests.

### Interview Qs

1. How do you structure a Python script so it's reusable and testable?
2. `argparse` vs `click` vs `typer`?
3. Why avoid `shell=True` in `subprocess`? How do you handle timeouts and failures?
4. How do you process a 10 GB CSV file in Python?
5. How do you scrape a website responsibly? When would you use Playwright or Scrapy?
6. How do you schedule a Python job? What are common cron pitfalls?
7. What do exit codes mean and why do they matter?

---

## 31. Type Hints & typing

Type hints are **optional annotations** checked by static tools (**mypy**, **pyright**/Pylance) — Python does **not** enforce them at runtime (Pydantic/FastAPI do use them at runtime for validation).

```python
def greet(name: str, times: int = 1) -> str:
    return (f"Hi {name} " * times).strip()

age: int = 25
names: list[str] = []
scores: dict[str, float] = {}
point: tuple[int, int] = (1, 2)
values: tuple[int, ...] = (1, 2, 3)      # variable length
maybe: str | None = None                  # Optional[str] (3.10+ syntax)
id_: int | str = 5                        # Union
```

### typing essentials

```python
from typing import Any, Literal, Final, TypedDict, Protocol, Callable, Iterable, Iterator, Sequence, Mapping, TypeAlias, Self, override
from collections.abc import Awaitable

Mode = Literal["read", "write"]           # only these values
MAX_RETRIES: Final = 3                     # constant (don't reassign)
UserId: TypeAlias = int
type Vector = list[float]                  # 3.12+ type alias syntax

Handler = Callable[[str, int], bool]       # function taking (str, int) returning bool

def total(items: Iterable[float]) -> float: # accept ANY iterable (list, tuple, generator) — be liberal in inputs
    return sum(items)

class Movie(TypedDict):                    # typed dict shape (e.g. JSON)
    title: str
    year: int

class Builder:
    def set_name(self, name: str) -> Self:  # returns the same class (works with subclasses)
        self.name = name
        return self
```

### Generics

```python
# 3.12+ syntax
def first[T](items: Sequence[T]) -> T | None:
    return items[0] if items else None

class Stack[T]:
    def __init__(self) -> None:
        self._items: list[T] = []
    def push(self, item: T) -> None:
        self._items.append(item)
    def pop(self) -> T:
        return self._items.pop()

s = Stack[int]()
s.push(1)
s.push("x")      # mypy error

# Older syntax
from typing import TypeVar, Generic
T = TypeVar("T")
class Box(Generic[T]):
    def __init__(self, item: T): self.item = item
```

### Protocol — structural typing (static duck typing)

```python
from typing import Protocol

class Notifier(Protocol):
    def send(self, to: str, message: str) -> None: ...

class EmailNotifier:                        # doesn't inherit Notifier!
    def send(self, to: str, message: str) -> None:
        print(f"email to {to}: {message}")

def alert(n: Notifier) -> None:
    n.send("admin@x.com", "Disk full")

alert(EmailNotifier())                      # ✅ type-checks because the shape matches
```

### Type narrowing

```python
def length(x: str | list[str] | None) -> int:
    if x is None:
        return 0
    if isinstance(x, str):
        return len(x)        # x: str here
    return sum(len(s) for s in x)   # x: list[str]
```

**Best practices**: annotate function signatures (public APIs especially), run mypy/pyright in CI, prefer abstract input types (`Iterable`, `Mapping`) and concrete return types, avoid `Any`, use `TypedDict`/dataclasses/Pydantic for structured data.

---

## 32. How Python Runs: Bytecode, Memory & Internals

### How Python runs: source → bytecode → PVM

```
your_code.py
   │  1. Lexing & parsing → AST
   ▼
bytecode (.pyc in __pycache__)
   │  2. compiled to bytecode (cached)
   ▼
Python Virtual Machine (PVM)
   │  3. interprets bytecode instruction by instruction
   ▼
output
```

- **CPython**: the reference implementation (written in C) — what you get from python.org.
- Others: **PyPy** (JIT, faster for long-running pure-Python code), Jython (JVM), MicroPython.
- Recent CPython versions: 3.11 was ~25% faster, 3.13 added an experimental JIT and a **free-threaded** (no-GIL) build, and 3.14 made free-threading officially supported (still opt-in).

```python
import dis

def add(a, b):
    return a + b

dis.dis(add)   # shows the bytecode: LOAD_FAST a, LOAD_FAST b, BINARY_OP +, RETURN_VALUE
```

```python
# Strong typing
"1" + 1        # TypeError: can only concatenate str (not "int") to str
"1" + str(1)   # "11"
int("1") + 1   # 2

# Dynamic typing
x = 10
x = "now a string"   # fine
```

### Reference counting + garbage collector

CPython frees objects when their **reference count** drops to 0. A **cyclic garbage collector** (generational: gen 0/1/2) cleans up reference cycles that refcounting can't.

```python
import sys, gc
a = []
sys.getrefcount(a)     # 2 (a + the temporary argument)
b = a
sys.getrefcount(a)     # 3
del b

x = {}; y = {}
x["y"] = y; y["x"] = x   # cycle — freed by gc, not refcounting
del x, y
gc.collect()
```

`del` removes a **name**, not the object; the object is freed when nothing references it.

### Shallow vs deep copy

```python
import copy
original = [[1, 2], [3, 4]]

alias = original               # same object
shallow = original.copy()      # or list(original), original[:], copy.copy(original)
deep = copy.deepcopy(original)

original[0].append(99)
shallow[0]   # [1, 2, 99] — inner lists shared
deep[0]      # [1, 2]     — fully independent
```

### Integer caching & string interning

```python
a = 256; b = 256
a is b          # True — CPython caches small ints (-5..256)
a = 257; b = 257
a is b          # may be False (implementation detail!)

s1 = "hello"; s2 = "hello"
s1 is s2        # True — identifier-like strings are interned
```

Never rely on `is` for numbers/strings — use `==`.

### Everything is an object

```python
def f(): pass
type(f)            # <class 'function'>
type(int)          # <class 'type'> — classes are objects too (instances of `type`, the metaclass)
f.custom = 1       # functions can have attributes
```

### Metaclasses (brief)

A metaclass is the "class of a class" (`type` by default) — controls how classes are created. Used by ORMs/frameworks (Django models, Pydantic, Enum). You rarely need one — class decorators or `__init_subclass__` usually suffice.

```python
class Plugin:
    registry = []
    def __init_subclass__(cls, **kwargs):     # runs whenever a subclass is created
        super().__init_subclass__(**kwargs)
        Plugin.registry.append(cls)

class CsvExporter(Plugin): ...
class PdfExporter(Plugin): ...
Plugin.registry     # [CsvExporter, PdfExporter]
```

---

## 33. Advanced Python: Attribute Access, Descriptors, Metaclasses & Weak References

The machinery behind `property`, methods, `dataclasses`, Django/SQLAlchemy models, Pydantic and Enum. You rarely write these daily, but they explain "how Python works" and come up in senior interviews.

### 1. How attribute lookup works (`obj.name`)

```
obj.name
  1. type(obj).__getattribute__(obj, "name")   ← runs for EVERY attribute access
       a. data descriptor on the class (defines __get__ AND __set__/__delete__, e.g. property)?  → use it
       b. obj.__dict__["name"]  (instance attribute)?                                          → return it
       c. non-data descriptor / plain class attribute (functions, classmethod, staticmethod)?  → use it
  2. not found → AttributeError → type(obj).__getattr__(obj, "name") if defined (fallback hook)
```

This order explains why a `property` can't be shadowed by an instance attribute, while a method can be.

### 2. `__getattr__`, `__getattribute__`, `__setattr__`, `__delattr__`

| Hook | Called when | Typical use |
|---|---|---|
| `__getattr__(self, name)` | Normal lookup **failed** | Fallbacks, proxies/delegation, lazy loading, dynamic APIs |
| `__getattribute__(self, name)` | **Every** attribute access | Rare — tracing/auditing (easy to break) |
| `__setattr__(self, name, value)` | Every assignment `obj.x = v` | Validation, read-only objects, change tracking |
| `__delattr__(self, name)` | `del obj.x` | Protect attributes |

```python
# Example 1 — delegation proxy: wrap an object, add behaviour, forward everything else
class LoggingProxy:
    def __init__(self, target):
        object.__setattr__(self, "_target", target)   # bypass our own __setattr__

    def __getattr__(self, name):                      # only for attributes NOT found on the proxy
        attr = getattr(self._target, name)
        if callable(attr):
            def wrapper(*args, **kwargs):
                print(f"calling {name}{args}")
                return attr(*args, **kwargs)
            return wrapper
        return attr

    def __setattr__(self, name, value):
        print(f"setting {name}={value!r}")
        setattr(self._target, name, value)

items = LoggingProxy([])
items.append(1)          # calling append(1,)
len(items._target)       # 1
```

```python
# Example 2 — dict with attribute access (config objects)
class AttrDict(dict):
    def __getattr__(self, name):
        try:
            value = self[name]
        except KeyError:
            raise AttributeError(name) from None      # must raise AttributeError (hasattr/getattr rely on it)
        return AttrDict(value) if isinstance(value, dict) else value

    def __setattr__(self, name, value):
        self[name] = value

cfg = AttrDict({"db": {"host": "localhost", "port": 5432}, "debug": True})
cfg.db.host          # 'localhost'
cfg.debug = False
```

```python
# Example 3 — immutable object via __setattr__
class Point:
    __slots__ = ("x", "y")
    def __init__(self, x, y):
        object.__setattr__(self, "x", x)
        object.__setattr__(self, "y", y)
    def __setattr__(self, name, value):
        raise AttributeError(f"{type(self).__name__} is immutable")
```

**Pitfalls**
- Inside `__setattr__`/`__getattribute__`, writing `self.x = …` or reading `self.x` calls the hook again → **infinite recursion**. Use `object.__setattr__(self, ...)` / `super().__getattribute__(...)`.
- `__getattr__` must raise **`AttributeError`**, not `KeyError`, or `hasattr()`/`getattr(obj, n, default)` break.
- Heavy magic hurts readability, IDE autocomplete and type checking — prefer explicit attributes/properties.

### 3. Descriptors

A **descriptor** is an object, stored as a **class attribute**, that defines any of `__get__`, `__set__`, `__delete__` (and optionally `__set_name__`). It controls what happens when that attribute is accessed on instances.

- **Data descriptor**: defines `__set__` or `__delete__` → wins over the instance `__dict__` (e.g. `property`).
- **Non-data descriptor**: only `__get__` → the instance `__dict__` wins (e.g. functions/methods, `cached_property`).

#### Example — reusable validated fields (how ORMs/validation libraries work)

```python
class Field:
    def __init__(self, *, type_, min_value=None):
        self.type_ = type_
        self.min_value = min_value

    def __set_name__(self, owner, name):          # called at class creation: learns its attribute name
        self.public_name = name
        self.private_name = f"_{name}"

    def __get__(self, obj, objtype=None):
        if obj is None:                            # accessed on the class itself (Product.price)
            return self
        return getattr(obj, self.private_name)

    def __set__(self, obj, value):
        if not isinstance(value, self.type_):
            raise TypeError(f"{self.public_name} must be {self.type_.__name__}")
        if self.min_value is not None and value < self.min_value:
            raise ValueError(f"{self.public_name} must be >= {self.min_value}")
        setattr(obj, self.private_name, value)

class Product:
    name = Field(type_=str)
    price = Field(type_=int, min_value=0)          # price in paise
    stock = Field(type_=int, min_value=0)

    def __init__(self, name, price, stock=0):
        self.name, self.price, self.stock = name, price, stock   # every assignment is validated

p = Product("Phone", 19999, 5)
p.price = -1        # ValueError: price must be >= 0
p.stock = "many"    # TypeError: stock must be int
```

One `Field` class replaces dozens of repetitive `@property` getters/setters.

#### How built-ins use descriptors

```python
# property is a data descriptor — a pure-Python equivalent:
class my_property:
    def __init__(self, fget=None, fset=None):
        self.fget, self.fset = fget, fset
    def __get__(self, obj, objtype=None):
        return self if obj is None else self.fget(obj)
    def __set__(self, obj, value):
        if self.fset is None:
            raise AttributeError("read-only")
        self.fset(obj, value)
    def setter(self, fset):
        return type(self)(self.fget, fset)

class Circle:
    def __init__(self, r): self.r = r
    @my_property
    def area(self): return 3.14159 * self.r ** 2

Circle(2).area       # 12.56636
```

- **Methods**: functions are non-data descriptors; `obj.method` calls `function.__get__(obj, type)` which returns a **bound method** (that's where `self` comes from).
- **`classmethod` / `staticmethod`**: descriptors that bind to the class / don't bind at all.
- **`functools.cached_property`**: non-data descriptor that computes once and stores the result in the instance `__dict__`, which then shadows the descriptor on later reads.

```python
def greet(self): return f"hi {self.name}"
class P: name = "A"
bound = greet.__get__(P(), P)     # what `P().greet` does under the hood
bound()                           # 'hi A'
```

### 4. Class creation hooks: `__init_subclass__` & `__set_name__`

Most things people used metaclasses for can now be done with these simpler hooks.

```python
class Plugin:
    registry: dict[str, type] = {}

    def __init_subclass__(cls, *, name: str, **kwargs):    # runs when a SUBCLASS is defined
        super().__init_subclass__(**kwargs)
        if not hasattr(cls, "run"):
            raise TypeError(f"{cls.__name__} must define run()")
        Plugin.registry[name] = cls

class CsvExporter(Plugin, name="csv"):
    def run(self, data): return ",".join(map(str, data))

class JsonExporter(Plugin, name="json"):
    def run(self, data): return str(list(data))

Plugin.registry["csv"]().run([1, 2, 3])     # '1,2,3'
```

### 5. Metaclasses

Classes are objects too; the thing that creates them is a **metaclass** (`type` by default). `class Foo: ...` is roughly `Foo = type("Foo", (bases), namespace)`.

```python
# Creating a class dynamically
User = type("User", (), {"greet": lambda self: "hello", "role": "user"})
User().greet()        # 'hello'
type(User)            # <class 'type'>
type(type)            # <class 'type'>
```

A custom metaclass customizes **class creation** (`__new__`/`__init__`) or **instance creation** (`__call__`).

```python
# Example 1 — Singleton via metaclass __call__ (controls `Cls()` calls)
class SingletonMeta(type):
    _instances: dict = {}
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]

class Config(metaclass=SingletonMeta):
    def __init__(self): self.values = {}

Config() is Config()     # True
```

```python
# Example 2 — ORM-style field collection at class creation
class ModelMeta(type):
    def __new__(mcls, name, bases, namespace):
        fields = {k: v for k, v in namespace.items() if isinstance(v, Field)}
        cls = super().__new__(mcls, name, bases, namespace)
        cls._fields = list(fields)                 # every model knows its fields
        cls._table = namespace.get("__table__", name.lower() + "s")
        return cls

class Model(metaclass=ModelMeta):
    def to_dict(self):
        return {f: getattr(self, f) for f in self._fields}

class Order(Model):
    __table__ = "orders"
    amount = Field(type_=int, min_value=0)
    status = Field(type_=str)
    def __init__(self, amount, status): self.amount, self.status = amount, status

Order._fields                               # ['amount', 'status']
Order(500, "paid").to_dict()                # {'amount': 500, 'status': 'paid'}
```

**When to use what**

| Need | Simplest tool |
|---|---|
| Modify/validate one class | Class decorator |
| React whenever a subclass is created (registry, checks) | `__init_subclass__` |
| Per-attribute behaviour | Descriptor (+ `__set_name__`) |
| Control class creation deeply, customize `isinstance`, class namespace, or instance creation for a whole hierarchy | Metaclass |

"Metaclasses are deeper magic than 99% of users should ever worry about" — reach for them last. (Pitfall: a class can't combine two unrelated metaclasses → "metaclass conflict".)

### 6. Weak references (`weakref`)

A **weak reference** refers to an object **without keeping it alive**. When no strong references remain, the object is garbage collected and the weak reference returns `None`. Used for caches, registries and observer lists that shouldn't cause memory leaks.

```python
import weakref

class Image:
    def __init__(self, path): self.path = path

# Example 1 — cache that doesn't keep images alive forever
_cache: "weakref.WeakValueDictionary[str, Image]" = weakref.WeakValueDictionary()

def load_image(path: str) -> Image:
    img = _cache.get(path)
    if img is None:
        img = Image(path)           # expensive load
        _cache[path] = img
    return img

a = load_image("logo.png")
b = load_image("logo.png")
a is b                          # True — cached while someone uses it
del a, b                        # no strong refs left → entry disappears from the cache automatically
len(_cache)                     # 0 (in CPython, immediately)
```

```python
# Example 2 — attach extra data to objects you don't own, without leaking them
metadata = weakref.WeakKeyDictionary()      # keys held weakly
req = Image("x.png")
metadata[req] = {"seen_at": 123}

# Example 3 — callbacks when an object dies
ref = weakref.ref(req)
ref() is req                    # True
weakref.finalize(req, print, "image freed")   # runs cleanup when req is collected (better than __del__)
del req                         # prints "image freed"; ref() is now None
```

Notes: `int`, `str`, `tuple`, `list`, `dict` instances can't be weakly referenced directly; classes with `__slots__` need `"__weakref__"` in their slots. `WeakSet` is handy for observer lists.

### 7. More useful dunder hooks & functools helpers

```python
# __missing__ — dict subclass fallback for missing keys
class DefaultZero(dict):
    def __missing__(self, key):
        return 0
counts = DefaultZero(); counts["x"] += 1     # {'x': 1}

# __class_getitem__ — make a class subscriptable (like list[int])
class Box:
    def __class_getitem__(cls, item):
        return f"Box of {item.__name__}"
Box[int]                                     # 'Box of int'
```

```python
from functools import singledispatchmethod

class Formatter:
    @singledispatchmethod
    def format(self, value):                   # fallback
        return str(value)

    @format.register
    def _(self, value: int):
        return f"{value:,}"

    @format.register
    def _(self, value: list):
        return ", ".join(self.format(v) for v in value)

f = Formatter()
f.format(1234567)          # '1,234,567'
f.format([1000, "a"])      # '1,000, a'
```

### Best practices

- Prefer **plain attributes → `@property` → descriptors → metaclasses**, in that order of escalating magic.
- Descriptors for **reusable** per-field logic (validation, lazy loading, type conversion).
- `__init_subclass__` for registries/validation of subclasses instead of metaclasses.
- Always raise `AttributeError` from `__getattr__`; avoid `__getattribute__` unless you really need it.
- Use `weakref` containers for caches/registries of objects owned elsewhere; use `weakref.finalize` instead of `__del__`.
- Document magic behaviour clearly — future readers and type checkers can't see it.

### Interview Qs

1. Explain Python's attribute lookup order. Why can't an instance attribute shadow a `property`?
2. `__getattr__` vs `__getattribute__`? What's the recursion trap in `__setattr__`?
3. What is a descriptor? Data vs non-data descriptors?
4. How are `property`, bound methods, `classmethod` and `cached_property` implemented with descriptors?
5. What does `__set_name__` do?
6. What is a metaclass? How does `type(name, bases, ns)` relate to `class` statements?
7. Metaclass vs class decorator vs `__init_subclass__` — when to use each?
8. How would you implement a singleton? (module-level instance, metaclass `__call__`, or `__new__`)
9. What are weak references and when would you use `WeakValueDictionary`?
10. What does `__missing__` do?

---

## 34. Concurrency: GIL, Threads, Processes

### The GIL (Global Interpreter Lock)

In standard CPython, the **GIL** allows only **one thread to execute Python bytecode at a time** in a process.

- **I/O-bound** work (network, disk, DB): threads **do** help — the GIL is released while waiting on I/O.
- **CPU-bound** work (math, image processing): threads **don't** speed it up → use **multiprocessing** (separate processes, each with its own GIL) or C extensions (NumPy releases the GIL).
- Python 3.13+ has an optional **free-threaded build** (`python3.13t`) without the GIL; 3.14 made it officially supported, but most deployments still use the default GIL build.

| Work type | Best tool |
|---|---|
| Many network/DB calls (I/O) | `asyncio` (best for thousands) or threads |
| Blocking I/O libraries (no async version) | `ThreadPoolExecutor` |
| CPU-heavy computation | `ProcessPoolExecutor` / `multiprocessing` |

### Threading

```python
import threading
import requests
from concurrent.futures import ThreadPoolExecutor, as_completed

urls = [f"https://httpbin.org/delay/1?i={i}" for i in range(10)]

def fetch(url):
    return requests.get(url, timeout=10).status_code

# 10 requests x 1s each → ~1s total with threads (vs ~10s sequential)
with ThreadPoolExecutor(max_workers=10) as pool:
    futures = {pool.submit(fetch, u): u for u in urls}
    for fut in as_completed(futures):
        print(futures[fut], fut.result())

# or simply
with ThreadPoolExecutor(max_workers=10) as pool:
    results = list(pool.map(fetch, urls))
```

### Race conditions & Lock

```python
counter = 0
lock = threading.Lock()

def increment():
    global counter
    for _ in range(100_000):
        with lock:               # without the lock, counter += 1 isn't atomic → wrong totals
            counter += 1

threads = [threading.Thread(target=increment) for _ in range(4)]
for t in threads: t.start()
for t in threads: t.join()
print(counter)                   # 400000
```

Other primitives: `RLock`, `Semaphore` (limit concurrency), `Event`, `Condition`, `queue.Queue` (thread-safe producer/consumer).

### Multiprocessing

```python
from concurrent.futures import ProcessPoolExecutor

def is_prime(n):
    if n < 2: return False
    return all(n % i for i in range(2, int(n ** 0.5) + 1))

if __name__ == "__main__":            # REQUIRED on macOS/Windows (spawn start method)
    numbers = range(10_000_000, 10_000_200)
    with ProcessPoolExecutor() as pool:          # uses all CPU cores
        results = list(pool.map(is_prime, numbers, chunksize=20))
```

Processes don't share memory — arguments/results are **pickled** and sent between processes (overhead). Share state with `multiprocessing.Queue`, `Manager`, or shared memory.

**Interview Qs**
- What is the GIL? Why does it exist? → Simplifies memory management (refcounting) and C-extension safety.
- Threads vs processes vs asyncio — when to use which?
- Does the GIL make code thread-safe? → No! Operations like `x += 1` are multiple bytecodes; you still need locks.

---

## 35. asyncio

**asyncio** = single-threaded **cooperative concurrency** with an **event loop**. While one coroutine waits on I/O (`await`), others run. Ideal for thousands of concurrent network operations (web servers like FastAPI, scrapers, websockets, bots).

### Basics

```python
import asyncio

async def fetch_user(user_id: int) -> dict:     # coroutine function
    await asyncio.sleep(1)                      # non-blocking wait (simulated I/O)
    return {"id": user_id}

async def main():
    user = await fetch_user(1)                   # sequential: 1s
    users = await asyncio.gather(                # concurrent: ~1s total for all three
        fetch_user(1), fetch_user(2), fetch_user(3)
    )
    print(users)

asyncio.run(main())                              # entry point — creates & runs the event loop
```

Calling `fetch_user(1)` without `await` only creates a coroutine object — it doesn't run.

### Example 1 — real HTTP calls with httpx + concurrency limit

```python
import asyncio
import httpx

async def fetch(client: httpx.AsyncClient, url: str, sem: asyncio.Semaphore) -> int:
    async with sem:                              # max N requests in flight
        r = await client.get(url, timeout=10)
        return r.status_code

async def main(urls: list[str]):
    sem = asyncio.Semaphore(10)
    async with httpx.AsyncClient() as client:    # reuse connections
        results = await asyncio.gather(
            *(fetch(client, u, sem) for u in urls),
            return_exceptions=True,              # one failure doesn't cancel the rest
        )
    for url, res in zip(urls, results):
        print(url, "ERROR" if isinstance(res, Exception) else res)
```

### Example 2 — TaskGroup (3.11+, structured concurrency) & timeouts

```python
async def main():
    async with asyncio.TaskGroup() as tg:        # if one task fails, others are cancelled
        t1 = tg.create_task(fetch_user(1))
        t2 = tg.create_task(fetch_user(2))
    print(t1.result(), t2.result())

    try:
        async with asyncio.timeout(2):           # 3.11+
            await slow_operation()
    except TimeoutError:
        print("timed out")

    result = await asyncio.wait_for(slow_operation(), timeout=2)   # older style
```

### Example 3 — producer/consumer with asyncio.Queue

```python
async def producer(q: asyncio.Queue):
    for i in range(10):
        await q.put(i)
    for _ in range(3):
        await q.put(None)                       # poison pills to stop workers

async def worker(name: str, q: asyncio.Queue):
    while (item := await q.get()) is not None:
        await asyncio.sleep(0.1)                # process
        print(name, "processed", item)
        q.task_done()

async def main():
    q = asyncio.Queue(maxsize=5)                # backpressure
    await asyncio.gather(producer(q), *(worker(f"w{i}", q) for i in range(3)))
```

### Don't block the event loop

```python
async def bad():
    time.sleep(5)            # ❌ blocks EVERYTHING
    requests.get(url)        # ❌ blocking library

async def good():
    await asyncio.sleep(5)                        # ✅
    await httpx.AsyncClient().get(url)            # ✅ async library
    await asyncio.to_thread(blocking_function)    # ✅ run blocking code in a thread
```

Async-friendly libraries: `httpx`/`aiohttp` (HTTP), `asyncpg`/SQLAlchemy async (Postgres), `motor` (Mongo), `redis.asyncio`, `aiofiles`.

### Key concepts

| Term | Meaning |
|---|---|
| Coroutine | `async def` function's result; runs when awaited/scheduled |
| Event loop | Scheduler that runs coroutines and I/O callbacks |
| `await` | Pause this coroutine until the awaitable finishes |
| Task | Coroutine scheduled to run concurrently (`asyncio.create_task`) |
| Future | Low-level placeholder for a result |
| `gather` | Run many awaitables concurrently, collect results |

**Interview Qs**
- Concurrency vs parallelism? → Concurrency = dealing with many things at once (interleaving); parallelism = doing many things at the same time (multiple cores).
- asyncio vs threading? → asyncio: single thread, explicit `await` switch points, very lightweight (thousands of tasks); threads: OS-managed, preemptive, work with blocking libraries.
- What happens if you call a blocking function inside async code?
- `gather` vs `TaskGroup`?

---

## 36. Testing with pytest

```python
# src/pricing.py
def apply_discount(price: float, percent: float) -> float:
    if not 0 <= percent <= 100:
        raise ValueError("percent must be 0-100")
    return round(price * (1 - percent / 100), 2)

# tests/test_pricing.py
import pytest
from pricing import apply_discount

def test_apply_discount():
    assert apply_discount(200, 10) == 180

def test_invalid_percent():
    with pytest.raises(ValueError, match="0-100"):
        apply_discount(100, 150)

@pytest.mark.parametrize("price,percent,expected", [
    (100, 0, 100),
    (100, 50, 50),
    (99.99, 10, 89.99),
])
def test_many(price, percent, expected):
    assert apply_discount(price, percent) == expected
```

```bash
pytest                    # discovers test_*.py
pytest -v -k discount     # verbose, filter by name
pytest -x                 # stop at first failure
pytest --cov=src          # coverage (pytest-cov)
```

### Fixtures (setup/teardown + dependency injection)

```python
@pytest.fixture
def user():
    return {"id": 1, "name": "Rohit"}

@pytest.fixture
def db():
    conn = create_test_db()
    yield conn               # test runs here
    conn.close()             # teardown

def test_save_user(db, user):
    save(db, user)
    assert get(db, 1)["name"] == "Rohit"
```

Scopes: `function` (default), `class`, `module`, `session`. Shared fixtures go in `conftest.py`. Built-ins: `tmp_path`, `monkeypatch`, `capsys`, `caplog`.

### Mocking

```python
from unittest.mock import patch, MagicMock

def test_weather(monkeypatch):
    monkeypatch.setenv("API_KEY", "test")

@patch("myapp.services.weather.httpx.get")        # patch where it's LOOKED UP
def test_get_temp(mock_get):
    mock_get.return_value = MagicMock(status_code=200, json=lambda: {"temp": 30})
    assert get_temp("Delhi") == 30
    mock_get.assert_called_once()
```

Async tests: `pytest-asyncio` (`@pytest.mark.asyncio`) or `anyio`.

---

## 37. Logging & Debugging

Use `logging`, not `print`, in real code: levels, timestamps, module names, handlers (console/file/remote), and can be turned up/down without code changes.

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s %(levelname)s %(name)s: %(message)s",
)
logger = logging.getLogger(__name__)      # one logger per module

logger.debug("details for devs")
logger.info("user %s logged in", user_id)  # lazy formatting — don't use f-strings in hot paths
logger.warning("disk 90%% full")
logger.error("payment failed for order %s", order_id)

try:
    1 / 0
except ZeroDivisionError:
    logger.exception("calculation failed")  # ERROR level + full traceback
```

Levels: `DEBUG < INFO < WARNING < ERROR < CRITICAL`. In production prefer **structured JSON logs** (`structlog`, `python-json-logger`) with request IDs.

### Debugging

```python
breakpoint()        # drops into pdb (3.7+)
# pdb commands: n (next), s (step into), c (continue), p var (print), l (list), q (quit), w (where)
```

Also: VS Code/PyCharm debuggers, `python -X importtime`, `traceback.print_exc()`, `rich` for pretty tracebacks.

---

## 38. Regular Expressions

```python
import re

re.search(r"\d+", "order 42 shipped").group()        # '42' (first match anywhere)
re.match(r"\d+", "42abc")                            # match at START only
re.fullmatch(r"\d{6}", "110001")                     # entire string must match
re.findall(r"\b\w+@\w+\.\w+\b", text)                # all matches → list
re.sub(r"\s+", " ", "too    many   spaces")          # replace
re.split(r"[,;]\s*", "a, b;c")                       # ['a', 'b', 'c']

m = re.search(r"(?P<year>\d{4})-(?P<month>\d{2})", "2026-09-24")
m.group("year"), m.groupdict()                       # '2026', {'year': '2026', 'month': '09'}

EMAIL = re.compile(r"[\w.+-]+@[\w-]+\.[\w.]+", re.IGNORECASE)   # compile once, reuse
bool(EMAIL.fullmatch("a@b.com"))                     # True
bool(EMAIL.fullmatch("a@b.com\n"))                   # False
```

**Validate with `fullmatch`, not `^…$` + `match`.** In Python, `$` also matches **before a trailing newline**, so `re.match(r"^\d+$", "123\n")` succeeds and `"a@b.com\n"` would pass an email check. (JavaScript's `$` doesn't do this.) `fullmatch` requires the entire string to match; `\Z` is the "true end of string" anchor if you need one inside a larger pattern.

Always use raw strings `r"..."` for patterns. Flags: `re.I`, `re.M`, `re.S`, `re.X` (verbose).

---

## 39. Code Style: PEP 8 & the Zen of Python

- **Indentation defines blocks** (4 spaces). No braces.
- Statements end at the newline (no semicolons needed).
- Comments with `#`; docstrings with triple quotes.

```python
def greet(name: str) -> str:
    """Return a greeting for the given name."""   # docstring
    if name:
        return f"Hello, {name}!"
    return "Hello, stranger!"

# Line continuation
total = (price * quantity
         + shipping
         - discount)
```

### PEP 8 (official style guide) — key rules

| Thing | Convention |
|---|---|
| variables, functions, modules | `snake_case` |
| classes, exceptions | `PascalCase` |
| constants | `UPPER_SNAKE_CASE` |
| "private" (internal) | `_leading_underscore` |
| name mangling | `__double_leading` |
| indentation | 4 spaces |
| line length | 79 (many teams use 88–120) |
| imports | top of file: stdlib → third-party → local, one per line |
| comparisons to None | `is None` / `is not None` |
| booleans | `if items:` not `if len(items) > 0:` |

Use **ruff** (linter + formatter) or **black** to enforce automatically.

**The Zen of Python** (`import this`): "Beautiful is better than ugly. Explicit is better than implicit. Simple is better than complex. Readability counts. Errors should never pass silently…"

---

## 40. Pythonic Idioms

```python
# Swap
a, b = b, a

# Truthiness
if items: ...                          # not: if len(items) > 0
if not name: ...

# enumerate / zip instead of range(len())
for i, item in enumerate(items): ...
for a, b in zip(list1, list2): ...

# Comprehensions instead of map/filter + lambda
squares = [x * x for x in nums if x > 0]

# dict.get / setdefault / defaultdict / Counter
count = counts.get(word, 0) + 1

# Unpacking
first, *middle, last = values
for name, (lat, lng) in cities.items(): ...

# Context managers for resources
with open(path) as f: ...

# join for strings
", ".join(names)

# any / all
if any(u.is_admin for u in users): ...

# Chained comparison
if 0 < x < 10: ...

# Conditional expression
label = "even" if n % 2 == 0 else "odd"

# EAFP
try:
    value = mapping[key]
except KeyError:
    value = default

# Walrus to avoid double computation
if (match := pattern.search(text)):
    print(match.group())

# f-strings
f"{user.name} has {len(orders)} orders"

# Merge dicts
config = defaults | overrides

# Sorting with keys
sorted(people, key=lambda p: (p.age, p.name))

# Don't compare to True/False/None with ==
if flag: ...          # not: if flag == True
if x is None: ...     # not: if x == None
```

---

## 41. Performance

- **Measure first**: `timeit`, `cProfile`, `py-spy`, `line_profiler`, `memray` (memory).
- **Choose the right data structure**: `set`/`dict` for membership (O(1)) instead of lists (O(n)); `deque` for queues.
- **Built-ins & comprehensions** are implemented in C and are faster than manual loops.
- **Avoid repeated work**: cache with `lru_cache`, hoist invariants out of loops.
- **Generators** for large data (memory).
- **String building**: `"".join()` not `+=` in loops.
- **Local variables** are faster than globals/attribute lookups in hot loops.
- **Vectorize** numeric work with NumPy/pandas/Polars.
- **I/O concurrency** with asyncio/threads; **CPU parallelism** with multiprocessing.
- Upgrade Python (3.11+ is much faster); consider PyPy, Cython or Rust extensions (PyO3) for hot spots.

```python
import timeit
timeit.timeit("x in s", setup="s = set(range(10_000)); x = 9_999", number=10_000)   # fast
timeit.timeit("x in l", setup="l = list(range(10_000)); x = 9_999", number=10_000)  # much slower

# python -m cProfile -s cumulative app.py
```

---

## 42. Production-Grade Python

### Project structure (src layout)

```
my-service/
├── pyproject.toml          # deps, tool config (ruff, mypy, pytest)
├── uv.lock                 # lockfile (commit it)
├── .env.example            # documented env vars (never commit .env)
├── Dockerfile
├── src/my_service/
│   ├── __init__.py
│   ├── main.py             # entry point
│   ├── config.py           # settings (pydantic-settings)
│   ├── logging.py
│   ├── domain/             # business logic (pure, testable)
│   ├── services/           # orchestration
│   ├── repositories/       # DB access
│   └── api/                # HTTP layer (FastAPI routers)
└── tests/
    ├── conftest.py
    ├── unit/
    └── integration/
```

### Configuration with validation

```python
# config.py
from pydantic_settings import BaseSettings, SettingsConfigDict
from pydantic import SecretStr, PostgresDsn

class Settings(BaseSettings):
    model_config = SettingsConfigDict(env_file=".env", env_prefix="APP_")
    env: str = "development"
    database_url: PostgresDsn
    jwt_secret: SecretStr              # hidden in logs/repr
    request_timeout: float = 10.0
    debug: bool = False                # "false"/"0"/"true" parsed correctly

settings = Settings()                  # fails fast at startup if required vars are missing
```

### Tooling

| Tool | Purpose |
|---|---|
| **uv** | env + dependency management + lockfile |
| **ruff** | linting + formatting (replaces flake8, isort, black) |
| **mypy / pyright** | static type checking |
| **pytest** (+ pytest-cov, pytest-asyncio) | tests |
| **pre-commit** | run ruff/mypy before each commit |
| **bandit / pip-audit** | security scanning |

```toml
[tool.ruff.lint]
select = ["E", "F", "I", "B", "UP", "SIM", "S"]   # pycodestyle, pyflakes, isort, bugbear, pyupgrade, simplify, bandit

[tool.mypy]
strict = true
```

### Production habits

1. **Type hints everywhere** + mypy/pyright in CI.
2. **Validate all external input** (Pydantic models for API bodies, env vars, JSON files, queue messages).
3. **Specific exceptions**, custom exception hierarchy, never swallow errors; log with context and traceback.
4. **Structured logging** (JSON) with request IDs; no `print`.
5. **Timeouts on every network call** (`httpx.get(url, timeout=10)`; `requests` has NO default timeout!).
6. **Retries with backoff** only for transient errors (`tenacity` library).
7. **Resource cleanup** via context managers (files, DB sessions, HTTP clients). Reuse HTTP clients/connection pools.
8. **Timezone-aware datetimes** in UTC; `Decimal` or integer paise/cents for money.
9. **Don't use mutable default args**; don't shadow built-ins.
10. **Secrets** from env/secret manager, `SecretStr`, never in code or logs; use `secrets` not `random` for tokens.
11. **Security**: parameterized SQL (never f-strings in queries), avoid `eval`/`exec`/`pickle` on untrusted data, `yaml.safe_load`, `subprocess.run([...])` without `shell=True`.
12. **Pin dependencies** with a lockfile; update regularly; scan with pip-audit.
13. **Tests**: unit tests for domain logic, integration tests for DB/API, fixtures in `conftest.py`.
14. **Graceful shutdown**: handle SIGTERM, close pools/clients (FastAPI lifespan).
15. **Keep functions small & pure** where possible; dependency injection for testability.
16. **Docstrings** for public functions (Google/NumPy style).

```python
# ❌ SQL injection
cursor.execute(f"SELECT * FROM users WHERE email = '{email}'")
# ✅ parameterized
cursor.execute("SELECT * FROM users WHERE email = %s", (email,))

# ❌ No timeout — can hang forever
requests.get(url)
# ✅
httpx.get(url, timeout=httpx.Timeout(10.0, connect=3.0))

# Retries with tenacity
from tenacity import retry, stop_after_attempt, wait_exponential_jitter, retry_if_exception_type

@retry(stop=stop_after_attempt(3), wait=wait_exponential_jitter(initial=0.5, max=5),
       retry=retry_if_exception_type(httpx.TransportError))
def call_payment_api(payload): ...
```

---

## 43. Packaging & Publishing a Python Library

Section 26 covered *using* packages. This section covers *making* one: a library other projects can `pip install`, with a command-line tool, type hints that editors and mypy understand, and a release process that doesn't leak secrets or break users. Everything below was built and installed locally with uv 0.12, hatchling 1.32 and pip on Python 3.13. Nothing was uploaded.

### 1. The vocabulary

| Term | Meaning |
|---|---|
| **Distribution package** | What you `pip install`: `acme-text-utils` on PyPI |
| **Import package** | What you `import`: `text_utils`. The two names can differ (`beautifulsoup4` → `import bs4`) |
| **Wheel** (`.whl`) | The built, ready-to-install archive. `py3-none-any` means pure Python and works everywhere. Installing a wheel just copies files |
| **sdist** (`.tar.gz`) | The source archive. Installers build a wheel from it when no matching wheel exists |
| **Build backend** | Turns your project into a wheel and sdist: **hatchling**, setuptools, flit-core, uv_build, pdm-backend, maturin (Rust extensions) |
| **Build frontend** | Runs the backend: `uv build`, `python -m build`, pip |
| **PyPI / TestPyPI** | The public registry, and its practice copy |

### 2. Project layout: use `src/`

```text
text-utils/
├── pyproject.toml
├── README.md
├── LICENSE
├── .gitignore               .env, .venv/, dist/
├── src/
│   └── text_utils/
│       ├── __init__.py
│       ├── core.py
│       ├── cli.py
│       └── py.typed         empty marker: "this package ships type hints"
└── tests/
    └── test_core.py
```

With the **`src` layout**, the project root isn't importable, so tests run against the **installed** package (`uv run pytest` installs it into the project venv first). A file you forgot to include in the build breaks the tests, not your users.

### 3. `pyproject.toml`

```toml
[build-system]
requires = ["hatchling>=1.27"]
build-backend = "hatchling.build"

[project]
name = "acme-text-utils"                    # the name on PyPI: pip install acme-text-utils
version = "1.0.0"
description = "Tiny text helpers: slugify, truncate, chunk"
readme = "README.md"
license = "MIT"                             # SPDX expression (PEP 639)
license-files = ["LICENSE"]
authors = [{ name = "Acme Engineering", email = "eng@acme.example" }]
requires-python = ">=3.10"
dependencies = []                           # a library: lower bounds only (">=2.28"), never exact pins
classifiers = [
  "Programming Language :: Python :: 3",
  "Typing :: Typed",
]

[project.scripts]
slugify = "text_utils.cli:main"             # installs a `slugify` command

[project.urls]
Homepage = "https://github.com/acme/text-utils"
Changelog = "https://github.com/acme/text-utils/blob/main/CHANGELOG.md"

[tool.hatch.build.targets.wheel]
packages = ["src/text_utils"]               # needed because the import name differs from the project name

[tool.hatch.build.targets.sdist]
include = ["src/", "tests/", "README.md", "LICENSE"]   # a whitelist: .env and other local files stay out

[dependency-groups]
dev = ["pytest>=8", "mypy>=1.11"]
```

| Part | Why |
|---|---|
| `[build-system]` | Always declare it. Without it, installers fall back to legacy setuptools behaviour: it builds, but not with the tool you think |
| `packages = [...]` | When the import name (`text_utils`) differs from the project name (`acme-text-utils`), hatchling can't guess: *"Unable to determine which files to ship inside the wheel"* |
| `license = "MIT"` + `license-files` | The modern SPDX form. The installed metadata then shows `License-Expression: MIT` |
| `requires-python` | Installers on older Pythons pick an older release instead of installing a broken one |
| **`dependencies`** | Libraries declare **ranges** (`"httpx>=0.27"`). An exact pin (`==0.27.0`) in a library makes it impossible to install alongside anything that needs a different version. Only **applications** pin, through a lockfile (`uv.lock`) |
| `[project.optional-dependencies]` | "Extras" users opt into: `pip install "acme-text-utils[cli]"` |
| `[project.scripts]` | Console commands. The installer creates a `slugify` executable that calls `text_utils.cli:main` and exits with its return value |
| `[dependency-groups]` | Dev-only tools (PEP 735). **Not** published, and not installed by your users |
| sdist `include` | A whitelist for the source archive (see the `.env` finding below) |

### 4. The code

```python
# src/text_utils/__init__.py
"""Tiny text helpers."""
from importlib.metadata import version

from .core import chunk, slugify, truncate

__all__ = ["__version__", "chunk", "slugify", "truncate"]
__version__ = version("acme-text-utils")    # single source of truth: the version in pyproject.toml
```

```python
# src/text_utils/core.py
import re
import unicodedata
from collections.abc import Sequence
from typing import TypeVar

T = TypeVar("T")


def _fold_latin(ch: str) -> str:
    """é → e, ﬁ → fi. Other scripts are left alone (Devanagari vowel signs are marks too)."""
    stripped = "".join(c for c in unicodedata.normalize("NFKD", ch) if not unicodedata.combining(c))
    return stripped if stripped and stripped.isascii() else ch


def slugify(text: str) -> str:
    """'Crème Brûlée: 10 Recipes!' → 'creme-brulee-10-recipes', 'नमस्ते दुनिया' → 'नमस्ते-दुनिया'"""
    folded = "".join(_fold_latin(ch) for ch in text.lower())
    kept = "".join(ch if ch.isalnum() or unicodedata.category(ch).startswith("M") else "-" for ch in folded)
    return re.sub(r"-{2,}", "-", kept).strip("-")


def truncate(text: str, max_len: int) -> str:
    """Shorten text to max_len characters, adding '…' when cut."""
    return text if len(text) <= max_len else text[: max(0, max_len - 1)] + "…"


def chunk(items: Sequence[T], size: int) -> list[list[T]]:
    """Split a sequence into lists of `size` items."""
    if size < 1:
        raise ValueError("size must be a positive integer")
    return [list(items[i : i + size]) for i in range(0, len(items), size)]
```

The common "strip accents" recipe removes **all** combining marks. That turns Hindi "नमस्ते दुनिया" into "नमसत-दनय", because Devanagari vowel signs are combining marks too. `_fold_latin` only simplifies characters that become plain ASCII, so accents on Latin letters go and other scripts stay intact. (Python's `\w` doesn't match Devanagari vowel signs either, which is why `slugify` checks `isalnum()` and the mark category instead of using `[\W_]+`.)

```python
# src/text_utils/cli.py
import argparse
import sys

from . import __version__, slugify


def main(argv: list[str] | None = None) -> int:
    parser = argparse.ArgumentParser(prog="slugify", description="Turn text into a URL slug.")
    parser.add_argument("text", nargs="+", help="the text to convert")
    parser.add_argument("--version", action="version", version=f"%(prog)s {__version__}")
    args = parser.parse_args(argv)
    print(slugify(" ".join(args.text)))
    return 0


if __name__ == "__main__":
    sys.exit(main())
```

`main(argv=None)` takes arguments as a parameter, so tests can call `main(["Hello", "World"])` without a subprocess.

### 5. Build and inspect

```bash
uv build                                   # or: python -m build
# Successfully built dist/acme_text_utils-1.0.0.tar.gz
# Successfully built dist/acme_text_utils-1.0.0-py3-none-any.whl
uvx twine check dist/*                     # validates metadata and that the README will render on PyPI
# Checking dist/acme_text_utils-1.0.0-py3-none-any.whl: PASSED
# Checking dist/acme_text_utils-1.0.0.tar.gz: PASSED
```

`uv build` builds the sdist first and then the wheel **from the sdist**, so a file missing from the sdist shows up as a build failure. Always look inside both archives:

```text
wheel:  text_utils/__init__.py  text_utils/cli.py  text_utils/core.py  text_utils/py.typed
        acme_text_utils-1.0.0.dist-info/{METADATA, WHEEL, entry_points.txt, RECORD, licenses/LICENSE}
sdist:  src/text_utils/…  tests/test_core.py  README.md  LICENSE  pyproject.toml  PKG-INFO
```

**The `.env` finding.** In a first build without `.gitignore` and without the sdist `include` list, the wheel was clean, but the **sdist contained `.env`** (with its secret). hatchling puts everything in the project folder into the sdist unless it's excluded. Both a `.gitignore` entry (hatchling honours it, even outside a git repo) and the `include` whitelist fixed it. Use the whitelist: it doesn't depend on someone remembering the ignore file.

### 6. Test the built wheel like a user

```bash
python3 -m venv /tmp/try && /tmp/try/bin/pip install dist/acme_text_utils-1.0.0-py3-none-any.whl
/tmp/try/bin/python -c "import text_utils as t; print(t.slugify('Crème Brûlée: 10 Recipes!'), t.__version__)"
# creme-brulee-10-recipes 1.0.0
/tmp/try/bin/slugify नमस्ते दुनिया 2026      # नमस्ते-दुनिया-2026
/tmp/try/bin/slugify --version             # slugify 1.0.0
```

**`py.typed` matters.** With the marker, mypy checks users' code against your hints (`bad: int = slugify("x")` → *Incompatible types in assignment*). Remove it and mypy ignores your package entirely: *Skipping analyzing "text_utils": module is installed, but missing library stubs or py.typed marker*. Ship it whenever the package has type hints, and add the `Typing :: Typed` classifier.

### 7. Versions: PEP 440, not semver

Python versions follow **PEP 440**. It's semver-like for the numbers, but pre-releases are written differently:

| Stage | PEP 440 | npm/semver equivalent |
|---|---|---|
| Development build | `1.0.dev1` | — |
| Alpha / beta / release candidate | `1.0a1`, `1.0b2`, `1.0rc1` | `1.0.0-alpha.1`, `-beta.2`, `-rc.1` |
| Final | `1.0` | `1.0.0` |
| Post-release (metadata or doc fix) | `1.0.post1` | — |

- **Ordering:** `1.0.dev1 < 1.0a1 < 1.0b2 < 1.0rc1 < 1.0 < 1.0.post1`. Tools normalise `1.0.0-rc.1` to `1.0.0rc1` and `v2.0` to `2.0`.
- **`~=` ("compatible release"):**
  - `~=1.4` means `>=1.4, <2.0` (1.9 ✓, 2.0 ✗).
  - `~=1.4.2` means `>=1.4.2, <1.5` (1.4.9 ✓, 1.5.0 ✗).
- **Pre-releases are opt-in.** With `1.0` and `1.1rc1` both available, `pip install demo-pkg` and `uv pip install demo-pkg` installed **1.0**. `pip install --pre demo-pkg` or `demo-pkg==1.1rc1` got the release candidate.
- **Bump versions with the tool:** `uv version --bump minor` (1.0.0 → 1.1.0), `uv version --bump patch --bump beta` (→ 1.0.1b1). Or derive versions from git tags with `hatch-vcs`.
- **Breaking changes need a major bump:** removing or renaming a public function, changing behaviour or defaults, raising `requires-python`, or adding a required dependency that conflicts with common ones. Say what's public with `__all__`, and prefix private helpers with `_` (like `_fold_latin`).

### 8. Publishing safely

1. **Rehearse on TestPyPI:** `uv publish --publish-url https://test.pypi.org/legacy/`, then install from it in a clean venv.
2. **Publish from CI with trusted publishing** (OIDC). PyPI trusts a specific GitHub workflow, so no API token is stored anywhere to be stolen. The official action also uploads signed attestations (PEP 740) linking each file to the commit that built it.
3. **Protect the release job** with a GitHub environment that requires approval, and enable 2FA on your PyPI account.
4. **Versions are permanent.** PyPI never accepts the same filename twice, even after deletion. For a bad release, **yank** it: installers skip yanked versions unless someone pins that exact version. Then publish a fix.

```yaml
# .github/workflows/release.yml: build once, publish with trusted publishing (no PYPI_TOKEN)
name: Release
on:
  push:
    tags: ["v*"]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: astral-sh/setup-uv@v6
      - run: uv build
      - run: uvx twine check dist/*
      - uses: actions/upload-artifact@v4
        with:
          name: dist
          path: dist/
  publish:
    needs: build
    runs-on: ubuntu-latest
    environment: pypi                  # add required reviewers in the repo settings
    permissions:
      id-token: write                  # trusted publishing: GitHub proves its identity to PyPI
    steps:
      - uses: actions/download-artifact@v4
        with:
          name: dist
          path: dist/
      - uses: pypa/gh-action-pypi-publish@release/v1
```

Register the publisher once on PyPI (project → Publishing: owner, repository, workflow file, environment). This workflow was syntax-checked, not run.

### 9. Checklist

- [ ] `[build-system]` declared; `src/` layout; `packages` set if the import name differs from the project name
- [ ] `license` (SPDX), `readme`, `requires-python`, URLs; `twine check` passes
- [ ] Libraries use dependency **ranges**; only applications pin (through a lockfile)
- [ ] sdist `include` whitelist; **both** archives inspected: no `.env`, no local files
- [ ] `py.typed` shipped; the built wheel tested in a fresh venv (import, CLI, mypy)
- [ ] PEP 440 versions, bumped by a tool; CHANGELOG; pre-releases for risky changes
- [ ] Published from CI with trusted publishing, after a TestPyPI rehearsal

### Interview Qs

1. What's the difference between a wheel and an sdist? → A wheel is prebuilt and installed by copying files; an sdist is source that has to be built first. Publish both.
2. Build backend vs build frontend? → The backend (hatchling, setuptools, uv_build, …) produces the archives; the frontend (uv, build, pip) calls it according to `[build-system]` (PEP 517/518).
3. Why use the `src` layout? → Tests import the installed package rather than the working folder, which catches packaging mistakes.
4. Why must libraries avoid exact pins? → Pins make dependency resolution impossible for users with other constraints. Libraries declare ranges; applications pin with lockfiles.
5. What does `py.typed` do? → It tells type checkers the package ships inline type hints (PEP 561). Without it, mypy skips the package.
6. How do you add a command-line tool to a package? → `[project.scripts] name = "package.module:function"`; the installer generates the executable.
7. How do you keep one version number? → Set it in `pyproject.toml` and read it at runtime with `importlib.metadata.version()` (or derive it from git tags).
8. What does `~=1.4.2` mean? → `>=1.4.2, <1.5`, a compatible release.
9. How are pre-releases written, and are they installed by default? → `1.0rc1` (PEP 440). Installers skip them unless you pass `--pre` or pin one.
10. How do you publish to PyPI securely? → From CI with trusted publishing (OIDC, no stored token), attestations, a protected environment, and 2FA.
11. How do you retract a broken release? → Yank it (installers skip it unless it's pinned exactly) and publish a fixed version. Version numbers can't be reused.

---

## 44. Data Structures & Algorithms in Python

Python is the most popular language for coding interviews because its standard library gives you most data structures for free. This section covers **complexities of built-ins**, the **Python tools** for each pattern, and tested implementations. (The same patterns explained in JS: `javascript.md` → Data Structures & Algorithms.)

### 1. Big-O of Python built-ins

| Operation | Complexity | Notes |
|---|---|---|
| `list[i]`, `list.append`, `list.pop()` | O(1) | amortized append |
| `list.insert(0, x)`, `list.pop(0)`, `x in list`, `list.remove` | **O(n)** | use `deque` for queues, `set` for membership |
| `list.sort()` / `sorted()` | O(n log n) | Timsort, stable |
| slicing `a[i:j]` | O(j − i) | copies |
| `dict`/`set` get, set, `in`, delete | O(1) avg | hash tables |
| `deque.append/appendleft/pop/popleft` | O(1) | double-ended queue |
| `heapq.heappush/heappop` | O(log n) | min-heap on a list |
| `heapq.heapify` | O(n) | |
| `bisect.bisect_left/insort` | O(log n) search / O(n) insert | on sorted lists |
| `str + str` in a loop | O(n²) total | use `"".join(parts)` |
| `min/max/sum/len(list)` | O(n) / O(n) / O(n) / O(1) | |

### 2. The toolbox

```python
from collections import deque, defaultdict, Counter, OrderedDict
from heapq import heappush, heappop, heapify, nlargest, nsmallest
from bisect import bisect_left, bisect_right, insort
from functools import cache, lru_cache
from itertools import accumulate, combinations, permutations, product, pairwise
from math import inf
import sys
sys.setrecursionlimit(10_000)      # default 1000 — raise for deep DFS (or go iterative)
```

---

### 3. Arrays & strings patterns

```python
# Two pointers — container with most water, O(n)
def max_area(heights: list[int]) -> int:
    l, r, best = 0, len(heights) - 1, 0
    while l < r:
        best = max(best, (r - l) * min(heights[l], heights[r]))
        if heights[l] < heights[r]:
            l += 1
        else:
            r -= 1
    return best

# Sliding window — smallest subarray with sum >= target, O(n)
def min_subarray_len(target: int, nums: list[int]) -> int:
    left = total = 0
    best = inf
    for right, n in enumerate(nums):
        total += n
        while total >= target:
            best = min(best, right - left + 1)
            total -= nums[left]
            left += 1
    return 0 if best == inf else best

# Sliding window with a Counter — longest substring with at most k distinct chars
def longest_k_distinct(s: str, k: int) -> int:
    counts, left, best = Counter(), 0, 0
    for right, ch in enumerate(s):
        counts[ch] += 1
        while len(counts) > k:
            counts[s[left]] -= 1
            if counts[s[left]] == 0:
                del counts[s[left]]
            left += 1
        best = max(best, right - left + 1)
    return best

# Prefix sums with itertools.accumulate
def range_sum_query(nums: list[int]):
    prefix = [0, *accumulate(nums)]
    return lambda i, j: prefix[j + 1] - prefix[i]          # sum of nums[i..j]
```

### 4. Binary search with `bisect`

```python
scores = [10, 20, 20, 30, 40]
bisect_left(scores, 20)     # 1 — first index where 20 could go (first >= 20)
bisect_right(scores, 20)    # 3 — after the last 20 (first > 20)
insort(scores, 25)          # keeps the list sorted

def count_in_range(sorted_nums, lo, hi):          # how many values in [lo, hi] — O(log n)
    return bisect_right(sorted_nums, hi) - bisect_left(sorted_nums, lo)

# Binary search on the ANSWER: minimum ship capacity to ship all packages within `days`
def ship_within_days(weights: list[int], days: int) -> int:
    def can_ship(capacity: int) -> bool:
        needed, load = 1, 0
        for w in weights:
            if load + w > capacity:
                needed += 1
                load = 0
            load += w
        return needed <= days
    lo, hi = max(weights), sum(weights)
    while lo < hi:
        mid = (lo + hi) // 2
        if can_ship(mid):
            hi = mid
        else:
            lo = mid + 1
    return lo
```

### 5. Stacks & queues

```python
# Stack = list. Monotonic stack: days until a warmer temperature
def daily_temperatures(temps: list[int]) -> list[int]:
    answer, stack = [0] * len(temps), []          # stack holds indexes of decreasing temps
    for i, t in enumerate(temps):
        while stack and temps[stack[-1]] < t:
            j = stack.pop()
            answer[j] = i - j
        stack.append(i)
    return answer

# Queue = deque (NOT list.pop(0), which is O(n))
q = deque([1, 2])
q.append(3); q.popleft()      # FIFO, both O(1)

# Sliding window maximum with a monotonic deque — O(n)
def max_sliding_window(nums: list[int], k: int) -> list[int]:
    dq, out = deque(), []                          # indexes, values decreasing
    for i, n in enumerate(nums):
        while dq and nums[dq[-1]] <= n:
            dq.pop()
        dq.append(i)
        if dq[0] <= i - k:
            dq.popleft()                           # drop index that left the window
        if i >= k - 1:
            out.append(nums[dq[0]])
    return out
```

### 6. Heaps (`heapq`) — priority queues

`heapq` is a **min-heap**. For a max-heap push negatives; for objects push tuples `(priority, tiebreaker, item)`.

```python
# Top-k frequent elements — O(n log k)
def top_k_frequent(nums: list[int], k: int) -> list[int]:
    return [n for n, _ in Counter(nums).most_common(k)]    # Counter uses a heap internally for k

# Kth largest element — keep a min-heap of size k
def kth_largest(nums: list[int], k: int) -> int:
    heap = nums[:k]
    heapify(heap)
    for n in nums[k:]:
        if n > heap[0]:
            heappop(heap); heappush(heap, n)
    return heap[0]

# Merge k sorted lists
def merge_k_sorted(lists: list[list[int]]) -> list[int]:
    heap = [(lst[0], i, 0) for i, lst in enumerate(lists) if lst]
    heapify(heap)
    out = []
    while heap:
        val, i, j = heappop(heap)
        out.append(val)
        if j + 1 < len(lists[i]):
            heappush(heap, (lists[i][j + 1], i, j + 1))
    return out

# Task scheduler by priority (tuples compare element by element)
tasks = []
heappush(tasks, (2, "write report"))
heappush(tasks, (1, "fix prod bug"))
heappop(tasks)            # (1, 'fix prod bug')
nlargest(2, [5, 1, 9, 3])  # [9, 5]
```

### 7. Linked lists (interview-only in Python)

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val, self.next = val, next

def build(values):
    head = None
    for v in reversed(values):
        head = ListNode(v, head)
    return head

def to_list(head):
    out = []
    while head:
        out.append(head.val); head = head.next
    return out

def reverse(head):
    prev = None
    while head:
        head.next, prev, head = prev, head, head.next      # tuple assignment does the pointer dance
    return prev

def remove_nth_from_end(head, n):
    dummy = ListNode(0, head)
    fast = slow = dummy
    for _ in range(n + 1):
        fast = fast.next
    while fast:
        fast, slow = fast.next, slow.next
    slow.next = slow.next.next
    return dummy.next
```

### 8. Trees

```python
class TreeNode:
    def __init__(self, val, left=None, right=None):
        self.val, self.left, self.right = val, left, right

#        4
#      2   6
#     1 3 5 7
root = TreeNode(4, TreeNode(2, TreeNode(1), TreeNode(3)), TreeNode(6, TreeNode(5), TreeNode(7)))

# Recursive DFS
def inorder(node):
    return inorder(node.left) + [node.val] + inorder(node.right) if node else []

# Iterative inorder with an explicit stack (no recursion limit issues)
def inorder_iter(node):
    out, stack = [], []
    while stack or node:
        while node:
            stack.append(node); node = node.left
        node = stack.pop()
        out.append(node.val)
        node = node.right
    return out

# BFS level order with deque
def level_order(root):
    if not root:
        return []
    levels, q = [], deque([root])
    while q:
        level = []
        for _ in range(len(q)):
            node = q.popleft()
            level.append(node.val)
            q.extend(child for child in (node.left, node.right) if child)
        levels.append(level)
    return levels

def max_depth(node):
    return 1 + max(max_depth(node.left), max_depth(node.right)) if node else 0

def is_valid_bst(node, lo=-inf, hi=inf):
    if not node:
        return True
    return lo < node.val < hi and is_valid_bst(node.left, lo, node.val) and is_valid_bst(node.right, node.val, hi)

# Diameter (longest path between any two nodes) — post-order with nonlocal
def diameter(root):
    best = 0
    def height(node):
        nonlocal best
        if not node:
            return 0
        l, r = height(node.left), height(node.right)
        best = max(best, l + r)
        return 1 + max(l, r)
    height(root)
    return best
```

### 9. Graphs

```python
# Adjacency list with defaultdict
def build_graph(edges, directed=False):
    graph = defaultdict(list)
    for u, v in edges:
        graph[u].append(v)
        if not directed:
            graph[v].append(u)
    return graph

# BFS shortest path (unweighted) — returns distance
def shortest_path_len(graph, start, goal):
    q, seen = deque([(start, 0)]), {start}
    while q:
        node, dist = q.popleft()
        if node == goal:
            return dist
        for nxt in graph[node]:
            if nxt not in seen:
                seen.add(nxt)
                q.append((nxt, dist + 1))
    return -1

# Grid BFS — shortest path in a maze (0 = open, 1 = wall)
def maze_shortest(grid):
    rows, cols = len(grid), len(grid[0])
    q, seen = deque([(0, 0, 0)]), {(0, 0)}
    while q:
        r, c, d = q.popleft()
        if (r, c) == (rows - 1, cols - 1):
            return d
        for dr, dc in ((1, 0), (-1, 0), (0, 1), (0, -1)):
            nr, nc = r + dr, c + dc
            if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == 0 and (nr, nc) not in seen:
                seen.add((nr, nc))
                q.append((nr, nc, d + 1))
    return -1

# Topological sort (Kahn) + cycle detection — course schedule
def course_order(n: int, prereqs: list[tuple[int, int]]) -> list[int]:
    graph, indegree = defaultdict(list), [0] * n
    for course, pre in prereqs:
        graph[pre].append(course)
        indegree[course] += 1
    q = deque(i for i in range(n) if indegree[i] == 0)
    order = []
    while q:
        node = q.popleft()
        order.append(node)
        for nxt in graph[node]:
            indegree[nxt] -= 1
            if indegree[nxt] == 0:
                q.append(nxt)
    return order if len(order) == n else []          # [] → cycle, impossible

# Dijkstra — shortest paths with non-negative weights, O((V + E) log V)
def dijkstra(graph: dict, start) -> dict:
    dist = {start: 0}
    heap = [(0, start)]
    while heap:
        d, node = heappop(heap)
        if d > dist.get(node, inf):
            continue                                   # stale heap entry
        for nxt, weight in graph.get(node, []):
            nd = d + weight
            if nd < dist.get(nxt, inf):
                dist[nxt] = nd
                heappush(heap, (nd, nxt))
    return dist

# Union-Find (Disjoint Set) — connected components, cycle detection in undirected graphs
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.size = [1] * n
    def find(self, x):
        while self.parent[x] != x:
            self.parent[x] = self.parent[self.parent[x]]   # path compression
            x = self.parent[x]
        return x
    def union(self, a, b) -> bool:
        ra, rb = self.find(a), self.find(b)
        if ra == rb:
            return False                                   # already connected → adding edge makes a cycle
        if self.size[ra] < self.size[rb]:
            ra, rb = rb, ra
        self.parent[rb] = ra
        self.size[ra] += self.size[rb]
        return True
```

### 10. Trie

```python
class Trie:
    def __init__(self):
        self.root = {}
    def insert(self, word: str) -> None:
        node = self.root
        for ch in word:
            node = node.setdefault(ch, {})
        node["$"] = True                                   # end-of-word marker
    def starts_with(self, prefix: str) -> list[str]:
        node = self.root
        for ch in prefix:
            if ch not in node:
                return []
            node = node[ch]
        out = []
        def dfs(n, path):
            if "$" in n:
                out.append(path)
            for ch, child in n.items():
                if ch != "$":
                    dfs(child, path + ch)
        dfs(node, prefix)
        return out
```

### 11. Backtracking

```python
# Combination sum: numbers can be reused, find all combos summing to target
def combination_sum(candidates: list[int], target: int) -> list[list[int]]:
    result = []
    def backtrack(start, remaining, path):
        if remaining == 0:
            result.append(path[:])
            return
        for i in range(start, len(candidates)):
            if candidates[i] <= remaining:
                path.append(candidates[i])
                backtrack(i, remaining - candidates[i], path)    # i (not i+1) → reuse allowed
                path.pop()
    backtrack(0, target, [])
    return result

# N-Queens count
def n_queens(n: int) -> int:
    cols, diag1, diag2 = set(), set(), set()
    def place(row):
        if row == n:
            return 1
        count = 0
        for c in range(n):
            if c in cols or row - c in diag1 or row + c in diag2:
                continue
            cols.add(c); diag1.add(row - c); diag2.add(row + c)
            count += place(row + 1)
            cols.remove(c); diag1.remove(row - c); diag2.remove(row + c)
        return count
    return place(0)

# Or let itertools do simple enumeration
list(combinations([1, 2, 3], 2))      # [(1,2), (1,3), (2,3)]
list(permutations("ab"))              # [('a','b'), ('b','a')]
```

### 12. Dynamic programming

```python
# Memoization with @cache — house robber (can't rob adjacent houses)
def rob(houses: list[int]) -> int:
    @cache
    def best(i: int) -> int:
        if i >= len(houses):
            return 0
        return max(houses[i] + best(i + 2), best(i + 1))
    return best(0)

# Tabulation — 0/1 knapsack (each item once), O(n × capacity), 1-D array iterated backwards
def knapsack(weights: list[int], values: list[int], capacity: int) -> int:
    dp = [0] * (capacity + 1)
    for w, v in zip(weights, values):
        for c in range(capacity, w - 1, -1):
            dp[c] = max(dp[c], dp[c - w] + v)
    return dp[capacity]

# Longest increasing subsequence in O(n log n) with bisect ("patience sorting")
def lis_length(nums: list[int]) -> int:
    tails = []                                        # tails[k] = smallest tail of an increasing subsequence of length k+1
    for n in nums:
        i = bisect_left(tails, n)
        if i == len(tails):
            tails.append(n)
        else:
            tails[i] = n
    return len(tails)

# Edit distance (Levenshtein) — 2-D DP, used in spell-checkers & fuzzy search
def edit_distance(a: str, b: str) -> int:
    prev = list(range(len(b) + 1))
    for i, ca in enumerate(a, 1):
        curr = [i]
        for j, cb in enumerate(b, 1):
            curr.append(min(prev[j] + 1,                # delete
                            curr[j - 1] + 1,            # insert
                            prev[j - 1] + (ca != cb)))  # replace (or match)
        prev = curr
    return prev[-1]

# Unique paths in a grid
def unique_paths(m: int, n: int) -> int:
    row = [1] * n
    for _ in range(1, m):
        for j in range(1, n):
            row[j] += row[j - 1]
    return row[-1]
```

### 13. Intervals, greedy & bits

```python
# Meeting rooms needed — sort starts & ends (or a heap of end times)
def min_meeting_rooms(intervals: list[tuple[int, int]]) -> int:
    ends, rooms = [], 0
    for start, end in sorted(intervals):
        while ends and ends[0] <= start:
            heappop(ends)                         # a room freed up
        heappush(ends, end)
        rooms = max(rooms, len(ends))
    return rooms

# Jump game — greedy farthest reach
def can_jump(nums: list[int]) -> bool:
    reach = 0
    for i, n in enumerate(nums):
        if i > reach:
            return False
        reach = max(reach, i + n)
    return True

# Bits: single number (XOR), count set bits, power of two
from functools import reduce
from operator import xor
single = reduce(xor, [4, 1, 2, 1, 2])     # 4
bin(13).count("1")                        # 3   (or (13).bit_count() in 3.10+)
is_pow2 = lambda n: n > 0 and n & (n - 1) == 0
```

### 14. Python-specific interview tips

- Use `collections` & `heapq` instead of hand-writing structures — interviewers expect it.
- `deque` for BFS, `heapq` for "top k / smallest / scheduling", `bisect` for sorted-array search, `Counter` for frequencies, `defaultdict(list)` for graphs/grouping, `@cache` for memoized recursion.
- Recursion depth is limited (~1000): use iteration/explicit stacks for deep trees/graphs, or raise `sys.setrecursionlimit` carefully.
- Tuples compare lexicographically → `(priority, counter, item)` in heaps; add a counter to avoid comparing non-comparable items.
- `sorted(key=...)` with tuples for multi-key sorts; `-x` for descending numeric keys.
- `float("inf")`/`math.inf` as initial min/max values.
- Avoid `list.pop(0)`, `x in list` inside loops, and string `+=` in loops.
- State complexity out loud; mention trade-offs (memory vs time).

### Interview Qs

1. What's the time complexity of `x in list` vs `x in set`? Of `list.pop(0)`?
2. Why use `deque` for BFS?
3. How do you make a max-heap with `heapq`? How do you store objects in a heap?
4. What does `bisect_left` vs `bisect_right` return?
5. How does `@cache` turn exponential recursion into polynomial time?
6. Explain the O(n log n) LIS algorithm.
7. What is Union-Find and when is it useful?
8. How does Dijkstra work and why can't it handle negative weights?
9. How do you avoid hitting Python's recursion limit?

---

## 45. Coding Questions

```python
# 1. Reverse a string / check palindrome
def is_palindrome(s: str) -> bool:
    cleaned = "".join(ch.lower() for ch in s if ch.isalnum())
    return cleaned == cleaned[::-1]

# 2. Anagram check
from collections import Counter
def is_anagram(a: str, b: str) -> bool:
    return Counter(a.replace(" ", "").lower()) == Counter(b.replace(" ", "").lower())

# 3. Two sum — O(n)
def two_sum(nums: list[int], target: int) -> tuple[int, int] | None:
    seen = {}
    for i, n in enumerate(nums):
        if target - n in seen:
            return seen[target - n], i
        seen[n] = i
    return None

# 4. First non-repeating character
def first_unique(s: str) -> str | None:
    counts = Counter(s)
    return next((ch for ch in s if counts[ch] == 1), None)

# 5. Flatten a nested list (any depth)
def flatten(items):
    for item in items:
        if isinstance(item, list):
            yield from flatten(item)
        else:
            yield item
list(flatten([1, [2, [3, [4]]], 5]))   # [1, 2, 3, 4, 5]

# 6. Fibonacci (memoized / iterative)
from functools import cache
@cache
def fib(n: int) -> int:
    return n if n < 2 else fib(n - 1) + fib(n - 2)

# 7. Group anagrams
from collections import defaultdict
def group_anagrams(words):
    groups = defaultdict(list)
    for w in words:
        groups["".join(sorted(w))].append(w)
    return list(groups.values())

# 8. Balanced brackets
def is_balanced(s: str) -> bool:
    pairs = {")": "(", "]": "[", "}": "{"}
    stack = []
    for ch in s:
        if ch in "([{":
            stack.append(ch)
        elif ch in pairs and (not stack or stack.pop() != pairs[ch]):
            return False
    return not stack

# 9. Most frequent element
def most_frequent(items):
    return Counter(items).most_common(1)[0][0]

# 10. Chunk a list
def chunks(lst, size):
    return [lst[i:i + size] for i in range(0, len(lst), size)]

# 11. LRU cache from scratch
from collections import OrderedDict
class LRUCache:
    def __init__(self, capacity: int):
        self.cap = capacity
        self.data: OrderedDict = OrderedDict()
    def get(self, key):
        if key not in self.data:
            return -1
        self.data.move_to_end(key)
        return self.data[key]
    def put(self, key, value):
        self.data[key] = value
        self.data.move_to_end(key)
        if len(self.data) > self.cap:
            self.data.popitem(last=False)

# 12. Merge two sorted lists
def merge_sorted(a, b):
    i = j = 0
    out = []
    while i < len(a) and j < len(b):
        if a[i] <= b[j]:
            out.append(a[i]); i += 1
        else:
            out.append(b[j]); j += 1
    return out + a[i:] + b[j:]

# 13. Word frequency from a file (top 10)
def top_words(path, n=10):
    with open(path, encoding="utf-8") as f:
        words = re.findall(r"[a-z']+", f.read().lower())
    return Counter(words).most_common(n)
```

---

## 46. Output-Based Questions

**Q1**
```python
def f(x, lst=[]):
    lst.append(x)
    return lst
print(f(1), f(2))
```
> `[1, 2] [1, 2]` — the same default list is shared (and both calls return the same object).

**Q2**
```python
a = [1, 2, 3]
b = a
b += [4]
print(a)
```
> `[1, 2, 3, 4]` — `+=` on a list mutates in place.

**Q3**
```python
a = (1, 2)
b = a
b += (3,)
print(a)
```
> `(1, 2)` — tuples are immutable, `+=` creates a new tuple.

**Q4**
```python
print([lambda: i for i in range(3)][0]())
```
> `2` — late binding.

**Q5**
```python
x = 10
def f():
    print(x)
    x = 5
f()
```
> `UnboundLocalError`.

**Q6**
```python
print(0.1 + 0.2 == 0.3, round(2.5), round(3.5), -7 // 2)
```
> `False 2 4 -4`

**Q7**
```python
print(bool([]), bool([0]), bool(""), bool(" "), bool(None))
```
> `False True False True False`

**Q8**
```python
d = {1: "a", True: "b", 1.0: "c"}
print(d)
```
> `{1: 'c'}` — `1 == True == 1.0` and they hash the same; the first key is kept, the last value wins.

**Q9**
```python
grid = [[0] * 2] * 2
grid[0][0] = 5
print(grid)
```
> `[[5, 0], [5, 0]]`

**Q10**
```python
s = "hello"
print(s[::-1], s[1:-1], s[-3:])
```
> `olleh ell llo`

**Q11**
```python
print("a" * 3 + "b" * 0, [1] * 3, 3 * "ab")
```
> `aaa [1, 1, 1] ababab`

**Q12**
```python
class A:
    x = 1
class B(A): pass
class C(A): pass
B.x = 2
A.x = 3
print(A.x, B.x, C.x)
```
> `3 2 3` — B has its own attribute now; C still looks up A.

**Q13**
```python
print(type(1 / 1), 5 // 2.0, 2 ** -1, True + True)
```
> `<class 'float'> 2.0 0.5 2`

**Q14**
```python
nums = [1, 2, 3, 4]
for n in nums:
    if n % 2 == 0:
        nums.remove(n)
print(nums)
```
> `[1, 3]` — happens to work here, but modifying while iterating skips elements in general (e.g. `[2, 4]` → `[4]`).

**Q15**
```python
try:
    print("try"); raise ValueError
except ValueError:
    print("except")
else:
    print("else")
finally:
    print("finally")
```
> `try except finally`

**Q16**
```python
def gen():
    yield 1
    return 2
g = gen()
print(next(g))
print(next(g, "done"))
```
> `1` then `done` (the return value goes into `StopIteration.value`).

**Q17**
```python
a = 256; b = 256
c = 1000; d = 1000
print(a is b, a == b, c == d)
```
> `True True True` (`c is d` would be implementation-dependent).

**Q18**
```python
print(sorted([3, 1, 2]), [3, 1, 2].sort())
```
> `[1, 2, 3] None`

---

## 47. Most Asked Interview Questions

### Basics

1. **Key features of Python?** → Interpreted, dynamic + strong typing, everything is an object, GC, huge stdlib, multi-paradigm.
2. **List vs tuple vs set vs dict?** → ordered/mutable, ordered/immutable, unique/unordered, key-value hash map.
3. **Mutable vs immutable types; why does it matter?**
4. **`is` vs `==`?**
5. **What are `*args` and `**kwargs`?**
6. **Mutable default argument problem.**
7. **Shallow vs deep copy.**
8. **What is pass-by-object-reference?**
9. **What are comprehensions? List comprehension vs generator expression?**
10. **`append` vs `extend`; `sort` vs `sorted`; `remove` vs `pop` vs `del`.**
11. **What is `None`?** → The singleton "no value" object; functions return it by default.
12. **What is PEP 8?**
13. **How is memory managed?** → Private heap, refcounting + cyclic GC, pymalloc allocator.
14. **What is `__init__`? Is it a constructor?** → An initializer; `__new__` creates the object.
15. **What is `self`?**
16. **What are namespaces & LEGB?**
17. **`global` vs `nonlocal`?**
18. **What does `if __name__ == "__main__"` do?**
19. **What are docstrings?**
20. **How are dicts implemented? Why must keys be hashable?**

### Intermediate

21. **What are decorators? Write a timing/retry decorator. Why `functools.wraps`?**
22. **What are closures? Late-binding issue?**
23. **Iterators vs generators; what does `yield` do? `yield from`?**
24. **What are context managers? Write one (class & contextlib).**
25. **Explain `@staticmethod` vs `@classmethod` vs instance methods.**
26. **What is `@property`?**
27. **Explain inheritance, `super()`, MRO, diamond problem.**
28. **Encapsulation in Python — private variables? Name mangling?**
29. **What are dunder methods? `__str__` vs `__repr__`? `__eq__` & `__hash__`?**
30. **What are dataclasses? dataclass vs Pydantic vs NamedTuple?**
31. **Abstract classes (`abc`) vs Protocols?**
32. **Exception handling: `try/except/else/finally`, custom exceptions, chaining.**
33. **EAFP vs LBYL.**
34. **What are lambda functions? Limitations?**
35. **`map`, `filter`, `reduce` vs comprehensions.**
36. **What are type hints? Are they enforced?**
37. **Module vs package; how does import work; circular imports?**
38. **What is `__slots__`?**
39. **What is monkey patching?** → Changing classes/modules at runtime (common in tests via `monkeypatch`/`patch`).
40. **What is the walrus operator?**

### Advanced

41. **What is the GIL? Its impact? Free-threaded Python?**
42. **Threading vs multiprocessing vs asyncio — when to use which?**
43. **How does asyncio work? What is the event loop? `gather` vs `TaskGroup`?**
44. **What happens if you call blocking code in an async function?**
45. **What are metaclasses? `__init_subclass__`?**
46. **Descriptors?** → Objects defining `__get__/__set__/__delete__`; power `property`, methods, `classmethod`.
47. **How does garbage collection handle reference cycles?**
48. **What is `functools.lru_cache` and how does it work?**
49. **How do you profile & optimize Python code?**
50. **How do you structure and ship a production Python service?** (Section 42)
51. **What's new in recent Python versions?** → 3.10 match-case & `X | Y` types; 3.11 speedups, `ExceptionGroup`, `TaskGroup`, `tomllib`; 3.12 generic syntax `def f[T]`, `type` aliases, better f-strings; 3.13 new REPL, experimental JIT & free-threading; 3.14 officially supported free-threading, template strings (t-strings), deferred evaluation of annotations.

---

**End of Python notes.** Next: `fastapi.md`.
