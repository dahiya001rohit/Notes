# DSA in Python: Theory, Pictures, Code & Practice

Data structures and algorithms explained from the basics, in Python only. Every topic follows the same order:

1. **Picture:** a diagram of the idea.
2. **Theory:** what it is, how it works, its complexity, and when to use it.
3. **Python:** a short working example. Every example in this file was run, and each `# →` value is the real output.
4. **Practice:** LeetCode problems from easy to hard (all free; titles and difficulty checked against LeetCode's problem list), plus GeeksforGeeks and VisuAlgo links to read and watch.

Topics go from basic to advanced; study them in order. Interview coding questions and output questions are in `python.md` → "Data Structures & Algorithms in Python" and "Coding Questions (with solutions)".

## Table of Contents

1. [How to Study DSA](#1-how-to-study-dsa)
2. [Big-O: Time and Space Complexity](#2-big-o-time-and-space-complexity)
3. [Python's Cost Model](#3-pythons-cost-model)
4. [Arrays and Python Lists](#4-arrays-and-python-lists)
5. [Strings](#5-strings)
6. [Hash Tables: dict and set](#6-hash-tables-dict-and-set)
7. [Linked Lists](#7-linked-lists)
8. [Stacks](#8-stacks)
9. [Queues and Deques](#9-queues-and-deques)
10. [Recursion](#10-recursion)
11. [Two Pointers](#11-two-pointers)
12. [Sliding Window](#12-sliding-window)
13. [Prefix Sums](#13-prefix-sums)
14. [Binary Search](#14-binary-search)
15. [Sorting](#15-sorting)
16. [Binary Trees and Traversals](#16-binary-trees-and-traversals)
17. [Binary Search Trees](#17-binary-search-trees)
18. [Heaps and Priority Queues](#18-heaps-and-priority-queues)
19. [Tries (Prefix Trees)](#19-tries-prefix-trees)
20. [Graphs: Representation, BFS and DFS](#20-graphs-representation-bfs-and-dfs)
21. [Shortest Paths: Dijkstra](#21-shortest-paths-dijkstra)
22. [Topological Sort](#22-topological-sort)
23. [Union-Find (Disjoint Set Union)](#23-union-find-disjoint-set-union)
24. [Backtracking](#24-backtracking)
25. [Greedy Algorithms](#25-greedy-algorithms)
26. [Dynamic Programming](#26-dynamic-programming)
27. [Bit Manipulation](#27-bit-manipulation)
28. [Pattern Cheat Sheet: Which Technique When?](#28-pattern-cheat-sheet-which-technique-when)
29. [Most Asked DSA Theory Questions](#29-most-asked-dsa-theory-questions)

---

## 1. How to Study DSA

![DSA learning path](images/dsa/00-roadmap.svg)

### Theory

A **data structure** is a way of organising data so certain operations are fast: a dict finds a key instantly, a heap always knows the smallest item. An **algorithm** is a step-by-step method for solving a problem, like binary search or BFS. DSA is about choosing the structure and algorithm that make the important operations cheap.

**A method for solving any problem:**

1. **Understand:** restate the problem, and ask about the input size, edge cases (empty, duplicates, negatives) and what to return.
2. **Examples:** work 2–3 small cases by hand, including an edge case.
3. **Brute force first:** the simplest correct idea, and its complexity.
4. **Optimise:** find the repeated work. Is there a pattern (sorted → binary search or two pointers; "all subsets" → backtracking; overlapping subproblems → DP)?
5. **Code** it cleanly, then **test**: trace your examples through the code and check the edge cases.

**Constraints tell you the target complexity** (roughly 10⁸ simple operations per second, less in Python):

| Input size n | Target complexity | Typical approach |
|---|---|---|
| n ≤ 10 | O(n!) or O(2ⁿ) | Backtracking, brute force |
| n ≤ 20 | O(2ⁿ) | Subsets, bitmask DP |
| n ≤ 500 | O(n³) | Triple loops, interval DP |
| n ≤ 5,000 | O(n²) | Nested loops, 2D DP |
| n ≤ 10⁶ | O(n log n) or O(n) | Sorting, heaps, hashing, two pointers |
| n ≥ 10⁸ | O(log n) or O(1) | Binary search, maths |

### Python

```python
# The "brute force → optimise" loop on a classic: does any pair sum to target?
def has_pair_brute(nums, target):          # O(n²): try every pair
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] + nums[j] == target:
                return True
    return False

def has_pair_fast(nums, target):           # O(n): remember what we've seen
    seen = set()
    for x in nums:
        if target - x in seen:
            return True
        seen.add(x)
    return False

has_pair_brute([3, 8, 1, 5], 9)   # → True
has_pair_fast([3, 8, 1, 5], 9)    # → True
has_pair_fast([3, 8, 1, 5], 100)  # → False
```

### Practice

Start with the structured lists: [NeetCode practice](https://neetcode.io/practice) (problems grouped by pattern), [HackerRank Data Structures](https://www.hackerrank.com/domains/data-structures) and [Algorithms](https://www.hackerrank.com/domains/algorithms) tracks, and the [CSES Problem Set](https://cses.fi/problemset/) for classic algorithm drills. Each topic below links to specific LeetCode problems, easy first.

---

## 2. Big-O: Time and Space Complexity

![Growth of complexity classes](images/dsa/01-big-o-growth.svg)

### Theory

**Big-O** describes how the work (time) or memory (space) of an algorithm **grows** as the input grows. It ignores constant factors and small terms, because for large inputs only the growth rate matters.

| Class | Name | Example |
|---|---|---|
| O(1) | Constant | dict lookup, list index |
| O(log n) | Logarithmic | binary search (halve each step) |
| O(n) | Linear | one loop over the input |
| O(n log n) | Linearithmic | merge sort, Python's `sorted()` |
| O(n²) | Quadratic | two nested loops over the input |
| O(2ⁿ) | Exponential | all subsets |
| O(n!) | Factorial | all orderings (permutations) |

**Rules for working it out:**

- **Drop constants and smaller terms:** O(3n + 10) → O(n); O(n² + n) → O(n²).
- **Sequential steps add:** a loop, then another loop → O(n + m).
- **Nested steps multiply:** a loop inside a loop → O(n × m).
- **Halving each step** gives O(log n); doing that for each of n items gives O(n log n).
- **Recursion:** (number of calls) × (work per call). Fibonacci without memoisation makes ~2ⁿ calls.
- **Space** counts extra memory: new lists, dicts, and the **recursion stack** (depth d → O(d)).

**Best, average and worst case.** Quicksort is O(n log n) on average but O(n²) in the worst case. Interviews usually mean the worst case unless you say otherwise.

**Amortised O(1)** means an operation is occasionally expensive, but the average over a long sequence is constant: `list.append` sometimes copies the whole list, yet n appends cost O(n) in total.

### Python

```python
def count_steps(n):
    steps = {"constant": 0, "linear": 0, "log": 0, "quadratic": 0}
    steps["constant"] += 1                     # O(1)
    for _ in range(n):                         # O(n)
        steps["linear"] += 1
    i = n
    while i > 1:                               # O(log n): i halves every time
        i //= 2
        steps["log"] += 1
    for _ in range(n):                         # O(n²)
        for _ in range(n):
            steps["quadratic"] += 1
    return steps

count_steps(16)   # → {"constant": 1, "linear": 16, "log": 4, "quadratic": 256}
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/) | 🟢 Easy |
| 2 | [231. Power of Two](https://leetcode.com/problems/power-of-two/) | 🟢 Easy |
| 3 | [69. Sqrt(x)](https://leetcode.com/problems/sqrtx/) | 🟢 Easy |

**Learn & visualise:** [GeeksforGeeks: Analysis of Algorithms](https://www.geeksforgeeks.org/dsa/analysis-of-algorithms/) · [Big-O Cheat Sheet](https://www.bigocheatsheet.com/)

---

## 3. Python's Cost Model

![Python list costs](images/dsa/02-list-costs.svg)

### Theory

The same idea costs very different amounts depending on the structure you use. Know these by heart:

| Operation | list | dict / set | collections.deque | heapq (list) |
|---|---|---|---|---|
| Index `a[i]` | O(1) | — | O(n) | — |
| Append / add at end | O(1)* | O(1)* | O(1) | push O(log n) |
| Pop from end | O(1) | — | O(1) | pop min O(log n) |
| Insert / pop at front | **O(n)** | — | **O(1)** | — |
| `x in …` | **O(n)** | **O(1)** average | O(n) | O(n) |
| Delete by key/value | O(n) | O(1) average | O(n) | — |
| Sort | O(n log n) | — | — | heapify O(n) |
| Slice `a[i:j]` | O(j − i) (copies) | — | — | — |

\* amortised. Strings are immutable, so `s += piece` in a loop can copy the whole string each time: collect pieces in a list and `"".join()` once.

**The most common Python performance bugs in interviews:**

- `if x in some_list` inside a loop → O(n²). Convert to a `set` first.
- `queue.pop(0)` on a list → O(n) per pop. Use `collections.deque.popleft()`.
- Slicing inside recursion (`nums[1:]`) copies the list every call. Pass indices instead.
- `sorted()` inside a loop. Sort once, outside.

### Python

```python
from collections import deque

data = list(range(10_000))
lookup = set(data)                # O(n) once, then O(1) membership checks
9_999 in lookup                   # → True

queue = deque([1, 2, 3])
queue.append(4)                   # add at the back: O(1)
queue.popleft()                   # → 1   (O(1); list.pop(0) would be O(n))
list(queue)                       # → [2, 3, 4]

parts = []
for word in ["data", "structures", "in", "python"]:
    parts.append(word.upper())
"-".join(parts)                   # → "DATA-STRUCTURES-IN-PYTHON"
```

---

## 4. Arrays and Python Lists

![Array memory layout](images/dsa/03-array-memory.svg)

### Theory

An **array** stores items in **contiguous memory**, so the address of item `i` is `start + i × size`. That's why indexing is O(1). A Python `list` is a **dynamic array** of references: when it's full, it allocates a bigger block and copies everything over. Because the capacity grows by a factor, `append` is **amortised O(1)**.

| Operation | Cost | Why |
|---|---|---|
| Read/write `a[i]` | O(1) | Address arithmetic |
| Append / pop at the end | O(1) amortised | Spare capacity at the end |
| Insert/delete in the middle or front | O(n) | Everything after it shifts |
| Search for a value | O(n) | Must check each item (O(log n) if sorted, using binary search) |

**Common array techniques:** in-place swaps, reversing a range, the two-pointer write index for "remove/compact" problems, and extra arrays for "product except self"-style questions.

### Python

```python
def remove_duplicates_sorted(nums):
    """Compact a sorted list in place; return the count of unique values (O(n) time, O(1) space)."""
    write = 0
    for read in range(len(nums)):
        if read == 0 or nums[read] != nums[read - 1]:
            nums[write] = nums[read]
            write += 1
    return write

nums = [1, 1, 2, 3, 3, 3, 4]
k = remove_duplicates_sorted(nums)
(k, nums[:k])                                  # → (4, [1, 2, 3, 4])

def rotate_right(nums, k):
    """Rotate in place by reversing three ranges: O(n) time, O(1) space."""
    def reverse(lo, hi):
        while lo < hi:
            nums[lo], nums[hi] = nums[hi], nums[lo]
            lo, hi = lo + 1, hi - 1
    n = len(nums)
    k %= n
    reverse(0, n - 1)
    reverse(0, k - 1)
    reverse(k, n - 1)
    return nums

rotate_right([1, 2, 3, 4, 5, 6, 7], 3)         # → [5, 6, 7, 1, 2, 3, 4]
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [1929. Concatenation of Array](https://leetcode.com/problems/concatenation-of-array/) | 🟢 Easy |
| 2 | [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) | 🟢 Easy |
| 3 | [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/) | 🟢 Easy |
| 4 | [189. Rotate Array](https://leetcode.com/problems/rotate-array/) | 🟡 Medium |
| 5 | [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/) | 🟡 Medium |

**Learn & visualise:** [GeeksforGeeks: Arrays](https://www.geeksforgeeks.org/dsa/array-data-structure-guide/) · [VisuAlgo: Array](https://visualgo.net/en/array)

---

## 5. Strings

![String indexing](images/dsa/04-string-index.svg)

### Theory

A Python `str` is an **immutable** sequence of Unicode characters. Indexing and slicing work like lists, but every "modification" creates a new string.

- `len(s)`, indexing and comparing characters are O(1); slicing `s[i:j]` copies, O(j − i).
- Building a string with `+=` in a loop can be O(n²). Use `"".join(list_of_parts)`.
- **Counting characters** is the core of anagram and "permutation in string" problems: use `collections.Counter`, or a list of 26 counts for lowercase letters.
- **Palindromes** use two pointers from both ends.
- `ord("a")` is 97 and `chr(97)` is `"a"`, so `ord(c) - ord("a")` maps letters to 0–25.

### Python

```python
from collections import Counter

def is_anagram(a, b):                    # O(n)
    return Counter(a) == Counter(b)

def is_palindrome(s):                    # ignore case and non-alphanumerics, O(n)
    lo, hi = 0, len(s) - 1
    while lo < hi:
        if not s[lo].isalnum():
            lo += 1
        elif not s[hi].isalnum():
            hi -= 1
        elif s[lo].lower() != s[hi].lower():
            return False
        else:
            lo, hi = lo + 1, hi - 1
    return True

def compress(s):                         # "aaabcc" → "a3b1c2", built with join
    out, i = [], 0
    while i < len(s):
        j = i
        while j < len(s) and s[j] == s[i]:
            j += 1
        out.append(f"{s[i]}{j - i}")
        i = j
    return "".join(out)

is_anagram("listen", "silent")                    # → True
is_palindrome("A man, a plan, a canal: Panama")   # → True
compress("aaabcc")                                # → "a3b1c2"
"python"[1:4], "python"[::-1]                     # → ("yth", "nohtyp")
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [344. Reverse String](https://leetcode.com/problems/reverse-string/) | 🟢 Easy |
| 2 | [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/) | 🟢 Easy |
| 3 | [14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/) | 🟢 Easy |
| 4 | [151. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/) | 🟡 Medium |
| 5 | [443. String Compression](https://leetcode.com/problems/string-compression/) | 🟡 Medium |

**Learn & visualise:** [GeeksforGeeks: Strings](https://www.geeksforgeeks.org/dsa/string-data-structure/)

---

## 6. Hash Tables: dict and set

![Hash table](images/dsa/05-hash-table.svg)

### Theory

A **hash table** turns a key into an array index with a **hash function**: `index = hash(key) % capacity`. Looking up, inserting and deleting are **O(1) on average**, which is why "use a dict/set" is the answer to so many optimisation questions.

- **Collisions:** two keys can map to the same slot. Tables resolve them by chaining or probing (CPython uses open addressing). Too many collisions degrade lookups towards O(n), so tables **resize** as they fill.
- **Keys must be hashable:** immutable types like `int`, `str` and `tuple` work; `list`, `dict` and `set` don't (use `tuple(lst)` or `frozenset`).
- A `set` is a hash table without values: great for "seen before?" and de-duplication.
- `dict` preserves **insertion order** (Python 3.7+).

**Patterns:** complement lookup (two-sum), frequency counting (`Counter`), grouping by a canonical key (anagrams grouped by sorted letters), and "seen" sets for cycle or duplicate detection.

### Python

```python
from collections import Counter, defaultdict

def two_sum(nums, target):                 # O(n): value → index of what we've seen
    seen = {}
    for i, x in enumerate(nums):
        if target - x in seen:
            return [seen[target - x], i]
        seen[x] = i
    return []

def group_anagrams(words):                 # O(n · k log k): sorted letters are the key
    groups = defaultdict(list)
    for w in words:
        groups["".join(sorted(w))].append(w)
    return sorted(sorted(g) for g in groups.values())

two_sum([2, 7, 11, 15], 9)                               # → [0, 1]
group_anagrams(["eat", "tea", "tan", "ate", "nat", "bat"])  # → [["ate", "eat", "tea"], ["bat"], ["nat", "tan"]]
Counter("mississippi").most_common(2)                    # → [("i", 4), ("s", 4)]
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [1. Two Sum](https://leetcode.com/problems/two-sum/) | 🟢 Easy |
| 2 | [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/) | 🟢 Easy |
| 3 | [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/) | 🟡 Medium |
| 4 | [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) | 🟡 Medium |
| 5 | [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/) | 🟡 Medium |

**Learn & visualise:** [GeeksforGeeks: Hashing](https://www.geeksforgeeks.org/dsa/hashing-data-structure/) · [VisuAlgo: Hash Table](https://visualgo.net/en/hashtable)

---

## 7. Linked Lists

![Linked list](images/dsa/06-linked-list.svg)

### Theory

A **linked list** is a chain of nodes where each node holds a value and a reference to the **next** node (a **doubly** linked list also points back to the previous one). Unlike arrays, nodes aren't contiguous.

| Operation | Linked list | Array (list) |
|---|---|---|
| Access k-th item | O(k) | O(1) |
| Insert/delete at the head | O(1) | O(n) |
| Insert/delete after a known node | O(1) | O(n) |
| Extra memory | A reference per node | Compact |

**Key techniques:**

- **Dummy (sentinel) head** node, to avoid special-casing the first node.
- **Fast and slow pointers:** the middle of the list, and cycle detection (Floyd: if they ever meet, there's a cycle).
- **In-place reversal** with `prev`, `curr` and `nxt`.
- **Two lists:** merge by always taking the smaller head.

Python has no built-in linked list (`collections.deque` is implemented as blocks internally). Interviews make you build nodes by hand, as below.

### Python

```python
class ListNode:
    def __init__(self, val, next=None):
        self.val, self.next = val, next

def build(values):
    dummy = ListNode(0)
    tail = dummy
    for v in values:
        tail.next = ListNode(v)
        tail = tail.next
    return dummy.next

def to_list(head):
    out = []
    while head:
        out.append(head.val)
        head = head.next
    return out

def reverse(head):                        # O(n) time, O(1) space
    prev = None
    while head:
        nxt = head.next
        head.next = prev
        prev, head = head, nxt
    return prev

def middle(head):                         # slow moves 1, fast moves 2
    slow = fast = head
    while fast and fast.next:
        slow, fast = slow.next, fast.next.next
    return slow.val

def has_cycle(head):                      # Floyd's tortoise and hare
    slow = fast = head
    while fast and fast.next:
        slow, fast = slow.next, fast.next.next
        if slow is fast:
            return True
    return False

to_list(reverse(build([3, 7, 1, 9])))     # → [9, 1, 7, 3]
middle(build([1, 2, 3, 4, 5]))            # → 3
looped = build([1, 2, 3])
looped.next.next.next = looped            # 3 → back to 1
has_cycle(looped), has_cycle(build([1, 2]))   # → (True, False)
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) | 🟢 Easy |
| 2 | [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/) | 🟢 Easy |
| 3 | [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) | 🟢 Easy |
| 4 | [876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/) | 🟢 Easy |
| 5 | [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) | 🟡 Medium |
| 6 | [146. LRU Cache](https://leetcode.com/problems/lru-cache/) | 🟡 Medium |

**Learn & visualise:** [GeeksforGeeks: Linked List](https://www.geeksforgeeks.org/dsa/linked-list-data-structure/) · [VisuAlgo: Linked List](https://visualgo.net/en/list)

---

## 8. Stacks

![Stack](images/dsa/07-stack.svg)

### Theory

A **stack** is **Last In, First Out**: you only touch the top. `push`, `pop` and `peek` are O(1). In Python, a list used only at its end is a perfect stack (`append`, `pop`, `stack[-1]`).

**When to reach for a stack:**

- **Matching pairs:** brackets, tags, undo/redo.
- **Expression evaluation:** postfix (RPN), or the two-stack infix algorithm.
- **Monotonic stack:** keep the stack increasing or decreasing to answer "next greater/smaller element" questions in O(n) total. Each item is pushed and popped at most once.
- **DFS** without recursion, and anything recursive (the call stack is a stack).

### Python

```python
def valid_brackets(s):
    pairs = {")": "(", "]": "[", "}": "{"}
    stack = []
    for ch in s:
        if ch in "([{":
            stack.append(ch)
        elif not stack or stack.pop() != pairs[ch]:
            return False
    return not stack

def next_greater(nums):
    """For each item, the next bigger item to its right (-1 if none). Monotonic stack: O(n)."""
    result = [-1] * len(nums)
    stack = []                                  # indexes whose answer isn't known yet
    for i, x in enumerate(nums):
        while stack and nums[stack[-1]] < x:
            result[stack.pop()] = x
        stack.append(i)
    return result

valid_brackets("{[()()]}"), valid_brackets("([)]")   # → (True, False)
next_greater([2, 1, 5, 3, 6])                        # → [5, 5, 6, 6, -1]
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) | 🟢 Easy |
| 2 | [155. Min Stack](https://leetcode.com/problems/min-stack/) | 🟡 Medium |
| 3 | [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/) | 🟡 Medium |
| 4 | [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/) | 🟡 Medium |
| 5 | [84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/) | 🔴 Hard |

**Learn & visualise:** [GeeksforGeeks: Stack](https://www.geeksforgeeks.org/dsa/stack-data-structure/) · [VisuAlgo: Stack (list page)](https://visualgo.net/en/list)

---

## 9. Queues and Deques

![Queue and deque](images/dsa/08-queue.svg)

### Theory

A **queue** is **First In, First Out**: add at the back, remove from the front, like a line at a ticket counter. A **deque** (double-ended queue) adds and removes at **both** ends in O(1).

- Use `collections.deque`: `append` and `popleft` are both O(1). **Never** `list.pop(0)`, which shifts every element.
- Queues power **BFS** (level-by-level exploration), task scheduling, rate limiters and buffers.
- A **monotonic deque** keeps a sliding window's maximum at the front, giving O(n) for "max of every window".
- `queue.Queue` is the thread-safe version for producer/consumer code, not for algorithms.

### Python

```python
from collections import deque

def recent_calls(times, window=3000):
    """Count requests in the last `window` ms at each call (LeetCode 933 idea)."""
    q, counts = deque(), []
    for t in times:
        q.append(t)
        while q[0] < t - window:
            q.popleft()                    # drop calls that fell out of the window
        counts.append(len(q))
    return counts

def window_max(nums, k):
    """Max of every window of size k with a decreasing deque of indexes: O(n)."""
    dq, out = deque(), []
    for i, x in enumerate(nums):
        while dq and nums[dq[-1]] <= x:
            dq.pop()                       # smaller items can never be a max again
        dq.append(i)
        if dq[0] <= i - k:
            dq.popleft()                   # front index left the window
        if i >= k - 1:
            out.append(nums[dq[0]])
    return out

recent_calls([1, 100, 3001, 3002])           # → [1, 2, 3, 3]
window_max([1, 3, -1, -3, 5, 3, 6, 7], 3)    # → [3, 3, 5, 5, 6, 7]
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/) | 🟢 Easy |
| 2 | [933. Number of Recent Calls](https://leetcode.com/problems/number-of-recent-calls/) | 🟢 Easy |
| 3 | [622. Design Circular Queue](https://leetcode.com/problems/design-circular-queue/) | 🟡 Medium |
| 4 | [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/) | 🔴 Hard |

**Learn & visualise:** [GeeksforGeeks: Queue](https://www.geeksforgeeks.org/dsa/queue-data-structure/) · [VisuAlgo: Queue & Deque (list page)](https://visualgo.net/en/list)

---
## 10. Recursion

![Recursion call stack](images/dsa/09-recursion.svg)

### Theory

A **recursive** function solves a problem by calling itself on a **smaller** version of the same problem. Every recursive function needs:

1. A **base case** that stops the recursion (the smallest input, answered directly).
2. A **recursive case** that moves **towards** the base case.
3. **Trust** that the smaller call returns the right answer (the "leap of faith"), then combine it.

- Each call waits on the **call stack**, so space is O(depth). Python's default limit is about 1,000 frames (`RecursionError`). Deep recursion, like a 10⁵-node linked list, should become a loop.
- **Recursion trees** show the cost: fib(n) branches twice per call, giving O(2ⁿ) calls, many of them repeated, which is where DP comes in (Section 26).
- Recursion is natural for **trees, graphs (DFS), divide and conquer, and backtracking**.

### Python

```python
def factorial(n):
    if n <= 1:                    # base case
        return 1
    return n * factorial(n - 1)   # smaller problem

def power(x, n):
    """Fast exponentiation: x^n in O(log n) by halving n."""
    if n == 0:
        return 1
    if n < 0:
        return 1 / power(x, -n)
    half = power(x, n // 2)
    return half * half if n % 2 == 0 else half * half * x

def sum_digits(n):
    return n if n < 10 else n % 10 + sum_digits(n // 10)

factorial(5)          # → 120
power(2, 10)          # → 1024
power(2, -2)          # → 0.25
sum_digits(9045)      # → 18
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/) | 🟢 Easy |
| 2 | [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) | 🟢 Easy |
| 3 | [50. Pow(x, n)](https://leetcode.com/problems/powx-n/) | 🟡 Medium |
| 4 | [779. K-th Symbol in Grammar](https://leetcode.com/problems/k-th-symbol-in-grammar/) | 🟡 Medium |

**Learn & visualise:** [GeeksforGeeks: Recursion](https://www.geeksforgeeks.org/dsa/recursion-algorithms/) · [VisuAlgo: Recursion Tree](https://visualgo.net/en/recursion)

---

## 11. Two Pointers

![Two pointers](images/dsa/10-two-pointers.svg)

### Theory

**Two pointers** walk through a sequence together, usually from **both ends inwards** or both **forwards at different speeds**. Each move discards possibilities for good, turning an O(n²) pair search into O(n).

| Variant | Use it for |
|---|---|
| Opposite ends (L → ← R) on **sorted** data | Pair or triplet sums, container with most water, palindromes |
| Same direction (slow/fast, read/write) | Remove duplicates in place, move zeroes, partitioning |
| Two sequences | Merge two sorted lists, "is subsequence" |

**Why it's correct (opposite ends, sorted):** if `nums[L] + nums[R]` is too big, every pair using `R` with anything ≥ `L` is also too big, so `R` can be dropped.

### Python

```python
def pair_with_sum(sorted_nums, target):
    lo, hi = 0, len(sorted_nums) - 1
    while lo < hi:
        total = sorted_nums[lo] + sorted_nums[hi]
        if total == target:
            return (lo, hi)
        if total < target:
            lo += 1          # need a bigger sum
        else:
            hi -= 1          # need a smaller sum
    return None

def three_sum(nums):
    """All unique triplets summing to 0: sort, then two pointers for each first item. O(n²)."""
    nums.sort()
    out = []
    for i in range(len(nums) - 2):
        if i > 0 and nums[i] == nums[i - 1]:
            continue                                   # skip duplicate first numbers
        lo, hi = i + 1, len(nums) - 1
        while lo < hi:
            s = nums[i] + nums[lo] + nums[hi]
            if s < 0:
                lo += 1
            elif s > 0:
                hi -= 1
            else:
                out.append([nums[i], nums[lo], nums[hi]])
                lo += 1
                while lo < hi and nums[lo] == nums[lo - 1]:
                    lo += 1                            # skip duplicate second numbers
    return out

pair_with_sum([1, 2, 4, 6, 8, 11], 10)   # → (1, 4)
three_sum([-1, 0, 1, 2, -1, -4])         # → [[-1, -1, 2], [-1, 0, 1]]
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) | 🟢 Easy |
| 2 | [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) | 🟡 Medium |
| 3 | [15. 3Sum](https://leetcode.com/problems/3sum/) | 🟡 Medium |
| 4 | [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/) | 🟡 Medium |
| 5 | [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/) | 🔴 Hard |

**Learn & visualise:** [GeeksforGeeks: Two Pointers](https://www.geeksforgeeks.org/dsa/two-pointers-technique/)

---

## 12. Sliding Window

![Sliding window](images/dsa/11-sliding-window.svg)

### Theory

A **sliding window** is a range `[left, right]` that moves across a sequence. Instead of recomputing each window from scratch, **update** the answer as elements enter on the right and leave on the left: O(n) instead of O(n·k).

- **Fixed size k:** add `nums[right]`, remove `nums[right - k]`.
- **Variable size:** expand `right` every step; **shrink `left` while the window is invalid** (too big a sum, a repeated character…). Record the answer when the window is valid.
- The window state is usually a running sum, a `Counter`/dict of characters, or a deque (for window max/min).

Clues: "subarray/substring", "contiguous", "longest/shortest/max … such that …".

### Python

```python
def max_sum_k(nums, k):                       # fixed window
    window = sum(nums[:k])
    best = window
    for right in range(k, len(nums)):
        window += nums[right] - nums[right - k]
        best = max(best, window)
    return best

def longest_unique_substring(s):              # variable window
    last_seen, left, best = {}, 0, 0
    for right, ch in enumerate(s):
        if ch in last_seen and last_seen[ch] >= left:
            left = last_seen[ch] + 1          # shrink past the previous copy
        last_seen[ch] = right
        best = max(best, right - left + 1)
    return best

def min_len_subarray(target, nums):           # shortest window with sum ≥ target
    left, total, best = 0, 0, float("inf")
    for right, x in enumerate(nums):
        total += x
        while total >= target:
            best = min(best, right - left + 1)
            total -= nums[left]
            left += 1
    return 0 if best == float("inf") else best

max_sum_k([2, 1, 5, 1, 3, 2], 3)             # → 9
longest_unique_substring("abcabcbb")         # → 3
min_len_subarray(7, [2, 3, 1, 2, 4, 3])      # → 2
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [643. Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/) | 🟢 Easy |
| 2 | [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) | 🟢 Easy |
| 3 | [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) | 🟡 Medium |
| 4 | [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/) | 🟡 Medium |
| 5 | [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/) | 🟡 Medium |
| 6 | [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/) | 🔴 Hard |

**Learn & visualise:** [GeeksforGeeks: Sliding Window](https://www.geeksforgeeks.org/dsa/window-sliding-technique/)

---

## 13. Prefix Sums

![Prefix sums](images/dsa/12-prefix-sum.svg)

### Theory

A **prefix sum** array stores running totals: `P[0] = 0`, `P[i] = nums[0] + … + nums[i-1]`. Then **any range sum** is one subtraction:

> sum(nums[i..j]) = P[j + 1] − P[i]

- Build in O(n), answer each range query in O(1). Ideal when there are many queries on data that doesn't change.
- **Prefix sum + hash map** counts subarrays with sum k in O(n). A subarray ending at `j` sums to k when some earlier prefix equals `P[j+1] − k`. This works with negative numbers, where a sliding window fails.
- **2D prefix sums** give any rectangle's sum in O(1) (image processing, grid queries).
- The same idea works with XOR, products (careful with zeros) and counts.

### Python

```python
from collections import defaultdict
from itertools import accumulate

def prefix_sums(nums):
    return [0, *accumulate(nums)]

def range_sum(P, i, j):                       # inclusive i..j
    return P[j + 1] - P[i]

def count_subarrays_with_sum(nums, k):
    seen = defaultdict(int)
    seen[0] = 1                                # the empty prefix
    total = count = 0
    for x in nums:
        total += x
        count += seen[total - k]               # earlier prefixes that complete a sum of k
        seen[total] += 1
    return count

P = prefix_sums([3, 1, 4, 1, 5, 9])
P                                              # → [0, 3, 4, 8, 9, 14, 23]
range_sum(P, 2, 4)                             # → 10
count_subarrays_with_sum([1, 2, 3, -2, 2], 3)  # → 4
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [1480. Running Sum of 1d Array](https://leetcode.com/problems/running-sum-of-1d-array/) | 🟢 Easy |
| 2 | [303. Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/) | 🟢 Easy |
| 3 | [724. Find Pivot Index](https://leetcode.com/problems/find-pivot-index/) | 🟢 Easy |
| 4 | [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) | 🟡 Medium |
| 5 | [304. Range Sum Query 2D - Immutable](https://leetcode.com/problems/range-sum-query-2d-immutable/) | 🟡 Medium |

**Learn & visualise:** [GeeksforGeeks: Prefix Sum](https://www.geeksforgeeks.org/dsa/prefix-sum-array-implementation-applications-competitive-programming/)

---

## 14. Binary Search

![Binary search](images/dsa/13-binary-search.svg)

### Theory

**Binary search** finds a target in **sorted** data by comparing with the middle element and discarding half of the range each step: **O(log n)**. A million items take at most 20 steps.

The real power is **binary search on the answer**: whenever you can ask a yes/no question that is **monotonic** (false, false, …, true, true), you can binary-search for the first `true`. Examples: "the smallest speed that finishes in h hours", "the first bad version", "the minimum capacity that ships in d days".

**Getting the boundaries right** (the classic bug source):

- Use one consistent template. The **half-open** `[lo, hi)` template below never loops forever.
- `mid = (lo + hi) // 2`. Python ints don't overflow, but other languages need `lo + (hi - lo) // 2`.
- The standard library does it for you: `bisect_left(a, x)` is the first index where `a[i] >= x`, and `bisect_right(a, x)` the first where `a[i] > x`.

### Python

```python
from bisect import bisect_left, bisect_right

def lower_bound(a, x):
    """First index i with a[i] >= x (len(a) if none): the [lo, hi) template."""
    lo, hi = 0, len(a)
    while lo < hi:
        mid = (lo + hi) // 2
        if a[mid] < x:
            lo = mid + 1
        else:
            hi = mid
    return lo

def search(a, x):
    i = lower_bound(a, x)
    return i if i < len(a) and a[i] == x else -1

def min_eating_speed(piles, hours):
    """Binary search on the answer: the smallest speed k that finishes within `hours`."""
    def can_finish(k):
        return sum((p + k - 1) // k for p in piles) <= hours   # monotonic in k
    lo, hi = 1, max(piles)
    while lo < hi:
        mid = (lo + hi) // 2
        if can_finish(mid):
            hi = mid
        else:
            lo = mid + 1
    return lo

a = [2, 5, 8, 12, 16, 23, 38, 56, 72, 91]
search(a, 23), search(a, 7)                  # → (5, -1)
lower_bound([1, 2, 2, 2, 3], 2)              # → 1
bisect_left([1, 2, 2, 2, 3], 2), bisect_right([1, 2, 2, 2, 3], 2)   # → (1, 4)
min_eating_speed([3, 6, 7, 11], 8)           # → 4
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [704. Binary Search](https://leetcode.com/problems/binary-search/) | 🟢 Easy |
| 2 | [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/) | 🟢 Easy |
| 3 | [278. First Bad Version](https://leetcode.com/problems/first-bad-version/) | 🟢 Easy |
| 4 | [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) | 🟡 Medium |
| 5 | [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) | 🟡 Medium |
| 6 | [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/) | 🔴 Hard |

**Learn & visualise:** [GeeksforGeeks: Binary Search](https://www.geeksforgeeks.org/dsa/binary-search/)

---

## 15. Sorting

![Merge sort](images/dsa/14-merge-sort.svg)

### Theory

| Algorithm | Best | Average | Worst | Extra space | Stable | Notes |
|---|---|---|---|---|---|---|
| Bubble / insertion | O(n) | O(n²) | O(n²) | O(1) | Yes | Insertion sort is fast on small or nearly-sorted data |
| Selection | O(n²) | O(n²) | O(n²) | O(1) | No | Fewest swaps |
| **Merge sort** | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes | Divide and conquer; good for linked lists |
| **Quick sort** | O(n log n) | O(n log n) | O(n²) | O(log n) | No | Fast in practice; a random pivot avoids the worst case |
| Heap sort | O(n log n) | O(n log n) | O(n log n) | O(1) | No | Guaranteed O(n log n) in place |
| Counting / radix | O(n + k) | O(n + k) | O(n + k) | O(n + k) | Yes | Small integer ranges only (not comparison-based) |

- **Comparison sorts can't beat O(n log n)** in the worst case (a decision-tree lower bound).
- **Stable** means equal keys keep their original order. It matters when sorting by one field after another.
- **Python's `sorted()` / `list.sort()` use Timsort** (a merge/insertion hybrid). It's stable, O(n log n) worst case, and O(n) on already-sorted runs. In real code, always use it with `key=`; implement sorts yourself only to learn or when an interview asks.

### Python

```python
def merge_sort(a):
    if len(a) <= 1:
        return a
    mid = len(a) // 2
    left, right = merge_sort(a[:mid]), merge_sort(a[mid:])
    merged, i, j = [], 0, 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:              # <= keeps it stable
            merged.append(left[i]); i += 1
        else:
            merged.append(right[j]); j += 1
    return merged + left[i:] + right[j:]

def quick_sort(a):
    if len(a) <= 1:
        return a
    pivot = a[len(a) // 2]
    return (quick_sort([x for x in a if x < pivot]) + [x for x in a if x == pivot]
            + quick_sort([x for x in a if x > pivot]))

people = [("Asha", 31), ("Ravi", 25), ("Meera", 31), ("Arjun", 25)]
merge_sort([5, 2, 4, 6, 1, 3])                          # → [1, 2, 3, 4, 5, 6]
quick_sort([9, 3, 7, 3, 1])                             # → [1, 3, 3, 7, 9]
sorted(people, key=lambda p: p[1])                      # → [("Ravi", 25), ("Arjun", 25), ("Asha", 31), ("Meera", 31)]
sorted(people, key=lambda p: (-p[1], p[0]))             # → [("Asha", 31), ("Meera", 31), ("Arjun", 25), ("Ravi", 25)]
```

The third result shows **stability**: Ravi stays before Arjun because he came first in the input.

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/) | 🟢 Easy |
| 2 | [75. Sort Colors](https://leetcode.com/problems/sort-colors/) | 🟡 Medium |
| 3 | [912. Sort an Array](https://leetcode.com/problems/sort-an-array/) | 🟡 Medium |
| 4 | [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/) | 🟡 Medium |
| 5 | [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) | 🟡 Medium |

**Learn & visualise:** [GeeksforGeeks: Sorting](https://www.geeksforgeeks.org/dsa/sorting-algorithms/) · [VisuAlgo: Sorting (animated)](https://visualgo.net/en/sorting)

---

## 16. Binary Trees and Traversals

![Binary tree](images/dsa/15-binary-tree.svg)

### Theory

A **tree** is a hierarchy of nodes with no cycles. In a **binary tree** each node has at most two children (left and right).

- **Terms:** root, parent/child, leaf (no children), **depth** (edges from the root), **height** (longest path down to a leaf), subtree.
- A tree with n nodes has n − 1 edges. A **balanced** tree has height O(log n); a skewed one has height O(n).
- **DFS traversals** (recursion, or an explicit stack):
  - **pre-order** (node, left, right): copying a tree, serialising it;
  - **in-order** (left, node, right): sorted order in a BST;
  - **post-order** (left, right, node): deleting a tree, computing heights and sizes bottom-up.
- **BFS / level order** (a queue): the shortest path in edges, level averages, the right-side view.
- Most tree problems are "solve for the left subtree, solve for the right, combine": O(n) time, O(h) stack space.

### Python

```python
from collections import deque

class TreeNode:
    def __init__(self, val, left=None, right=None):
        self.val, self.left, self.right = val, left, right

#        1
#       / \
#      2   3
#     / \   \
#    4   5   6
root = TreeNode(1, TreeNode(2, TreeNode(4), TreeNode(5)), TreeNode(3, None, TreeNode(6)))

def preorder(n):  return [n.val, *preorder(n.left), *preorder(n.right)] if n else []
def inorder(n):   return [*inorder(n.left), n.val, *inorder(n.right)] if n else []
def postorder(n): return [*postorder(n.left), *postorder(n.right), n.val] if n else []

def level_order(root):
    levels, q = [], deque([root] if root else [])
    while q:
        level = []
        for _ in range(len(q)):                 # exactly one level per iteration
            node = q.popleft()
            level.append(node.val)
            q.extend(child for child in (node.left, node.right) if child)
        levels.append(level)
    return levels

def height(n):
    return 0 if n is None else 1 + max(height(n.left), height(n.right))

preorder(root), inorder(root), postorder(root)   # → ([1, 2, 4, 5, 3, 6], [4, 2, 5, 1, 3, 6], [4, 5, 2, 6, 3, 1])
level_order(root)                                 # → [[1], [2, 3], [4, 5, 6]]
height(root)                                      # → 3
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/) | 🟢 Easy |
| 2 | [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/) | 🟢 Easy |
| 3 | [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/) | 🟢 Easy |
| 4 | [543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/) | 🟢 Easy |
| 5 | [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) | 🟡 Medium |
| 6 | [124. Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/) | 🔴 Hard |

**Learn & visualise:** [GeeksforGeeks: Binary Tree](https://www.geeksforgeeks.org/dsa/binary-tree-data-structure/) · [VisuAlgo: BST & traversals](https://visualgo.net/en/bst)

---

## 17. Binary Search Trees

![Binary search tree](images/dsa/16-bst.svg)

### Theory

A **binary search tree (BST)** keeps an ordering rule at **every** node: everything in the left subtree is smaller, and everything in the right subtree is larger. So:

- Search, insert and delete follow **one root-to-leaf path**: O(h), which is O(log n) when balanced.
- An **in-order traversal returns the values sorted**. That's the key to "k-th smallest" and "validate BST" problems.
- Inserting already-sorted data creates a **skewed** tree (a linked list), O(n) per operation. **Self-balancing** trees (AVL, red-black) keep h = O(log n); they're used by Java's `TreeMap` and C++'s `std::map`. Python's standard library has none: use `bisect` on a sorted list, or the `sortedcontainers` package.
- **Validating** needs the full valid range (low, high) passed down, not just a comparison with the direct children.

### Python

```python
class Node:
    def __init__(self, val):
        self.val, self.left, self.right = val, None, None

def insert(root, val):
    if root is None:
        return Node(val)
    if val < root.val:
        root.left = insert(root.left, val)
    else:
        root.right = insert(root.right, val)
    return root

def contains(root, val):
    while root:
        if val == root.val:
            return True
        root = root.left if val < root.val else root.right
    return False

def is_valid(root, low=float("-inf"), high=float("inf")):
    if root is None:
        return True
    return low < root.val < high and is_valid(root.left, low, root.val) and is_valid(root.right, root.val, high)

def kth_smallest(root, k):
    stack = []
    while True:                                 # iterative in-order traversal
        while root:
            stack.append(root)
            root = root.left
        root = stack.pop()
        k -= 1
        if k == 0:
            return root.val
        root = root.right

root = None
for v in [8, 3, 10, 1, 6, 14, 4, 7, 13]:
    root = insert(root, v)
contains(root, 7), contains(root, 5)            # → (True, False)
is_valid(root), kth_smallest(root, 3)           # → (True, 4)
bad = Node(5); bad.left = Node(1); bad.right = Node(6); bad.right.left = Node(3)   # 3 is right of 5
is_valid(bad)                                   # → False
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [700. Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/) | 🟢 Easy |
| 2 | [701. Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/) | 🟡 Medium |
| 3 | [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) | 🟡 Medium |
| 4 | [230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) | 🟡 Medium |
| 5 | [235. Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) | 🟡 Medium |

**Learn & visualise:** [GeeksforGeeks: Binary Search Tree](https://www.geeksforgeeks.org/dsa/binary-search-tree-data-structure/) · [VisuAlgo: BST / AVL](https://visualgo.net/en/bst)

---

## 18. Heaps and Priority Queues

![Heap](images/dsa/17-heap.svg)

### Theory

A **binary heap** is a complete binary tree where every parent is ≤ its children (**min-heap**). The minimum is always at the root, and the whole tree lives in a plain list: the children of `i` are at `2i+1` and `2i+2`, and its parent is at `(i-1)//2`.

| Operation | Cost |
|---|---|
| Peek min `h[0]` | O(1) |
| Push / pop | O(log n) (sift up / sift down) |
| Build from a list (`heapify`) | O(n) |

- Python's `heapq` is a **min-heap** on a list. For a max-heap, push negated values (`-x`) or tuples like `(-priority, item)`.
- **Top-k pattern:** keep a heap of size k. The k largest of n items cost O(n log k), better than sorting when k ≪ n.
- **Merge k sorted lists**, the **running median** (two heaps), **Dijkstra**, and schedulers are all heap problems.
- Tuples compare element by element. Add a tie-breaker counter so items that aren't comparable never get compared: `(priority, counter, item)`.

### Python

```python
import heapq

nums = [5, 1, 8, 3, 9, 2]
heapq.nsmallest(3, nums), heapq.nlargest(2, nums)    # → ([1, 2, 3], [9, 8])

def kth_largest(nums, k):                   # heap of size k: O(n log k)
    heap = []
    for x in nums:
        heapq.heappush(heap, x)
        if len(heap) > k:
            heapq.heappop(heap)             # drop the smallest; k largest remain
    return heap[0]

def merge_sorted(lists):
    """Merge k sorted lists in O(N log k)."""
    heap = [(lst[0], i, 0) for i, lst in enumerate(lists) if lst]
    heapq.heapify(heap)
    out = []
    while heap:
        val, i, j = heapq.heappop(heap)
        out.append(val)
        if j + 1 < len(lists[i]):
            heapq.heappush(heap, (lists[i][j + 1], i, j + 1))
    return out

max_heap = []
for x in [3, 7, 1]:
    heapq.heappush(max_heap, -x)            # negate for a max-heap
kth_largest([3, 2, 1, 5, 6, 4], 2)          # → 5
merge_sorted([[1, 4, 7], [2, 5], [3, 6, 9]])  # → [1, 2, 3, 4, 5, 6, 7, 9]
-heapq.heappop(max_heap)                    # → 7
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [1046. Last Stone Weight](https://leetcode.com/problems/last-stone-weight/) | 🟢 Easy |
| 2 | [703. Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/) | 🟢 Easy |
| 3 | [973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/) | 🟡 Medium |
| 4 | [621. Task Scheduler](https://leetcode.com/problems/task-scheduler/) | 🟡 Medium |
| 5 | [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/) | 🔴 Hard |
| 6 | [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/) | 🔴 Hard |

**Learn & visualise:** [GeeksforGeeks: Heap](https://www.geeksforgeeks.org/dsa/heap-data-structure/) · [VisuAlgo: Binary Heap](https://visualgo.net/en/heap)

---

## 19. Tries (Prefix Trees)

![Trie](images/dsa/18-trie.svg)

### Theory

A **trie** stores strings character by character along paths from the root, so words with the same prefix **share** nodes. Each node has children (one per next character) and an **end-of-word** flag.

- Insert and search cost **O(L)**, where L is the word length, however many words are stored.
- `starts_with(prefix)` is also O(L). This is what hash sets can't do efficiently.
- Uses: autocomplete, spell-checkers, word games (Boggle / "word search II"), IP routing (longest prefix match).
- Memory-heavy: one node per character. Use a dict of children (flexible) or a list of 26 (fast, lowercase only).

### Python

```python
class Trie:
    def __init__(self):
        self.root = {}

    def insert(self, word):
        node = self.root
        for ch in word:
            node = node.setdefault(ch, {})
        node["$"] = True                          # end-of-word marker

    def _walk(self, prefix):
        node = self.root
        for ch in prefix:
            if ch not in node:
                return None
            node = node[ch]
        return node

    def search(self, word):
        node = self._walk(word)
        return node is not None and "$" in node

    def starts_with(self, prefix):
        return self._walk(prefix) is not None

    def words_with_prefix(self, prefix):
        node, out = self._walk(prefix), []
        def dfs(n, path):
            if "$" in n:
                out.append(prefix + path)
            for ch in sorted(k for k in n if k != "$"):
                dfs(n[ch], path + ch)
        if node is not None:
            dfs(node, "")
        return out

t = Trie()
for w in ["cat", "car", "cart", "dog"]:
    t.insert(w)
t.search("car"), t.search("ca"), t.starts_with("ca")   # → (True, False, True)
t.words_with_prefix("ca")                              # → ["car", "cart", "cat"]
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/) | 🟢 Easy |
| 2 | [208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/) | 🟡 Medium |
| 3 | [211. Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/) | 🟡 Medium |
| 4 | [212. Word Search II](https://leetcode.com/problems/word-search-ii/) | 🔴 Hard |

**Learn & visualise:** [GeeksforGeeks: Trie](https://www.geeksforgeeks.org/dsa/trie-insert-and-search/)

---
## 20. Graphs: Representation, BFS and DFS

![Graph and adjacency list](images/dsa/19-graph.svg)

### Theory

A **graph** is a set of **vertices** (nodes) connected by **edges**. Edges can be **directed** (one-way: follows, prerequisites) or **undirected** (two-way: friendships, roads), and **weighted** (distance, cost) or unweighted. Trees are graphs without cycles; grids are graphs where each cell connects to its neighbours.

| Representation | Space | Check edge u–v | List neighbours | Use when |
|---|---|---|---|---|
| **Adjacency list** (`dict[node, list]`) | O(V + E) | O(degree) | O(degree) | Almost always (sparse graphs) |
| Adjacency matrix | O(V²) | O(1) | O(V) | Dense graphs, small V |
| Edge list | O(E) | O(E) | O(E) | Kruskal's MST, input format |

**Traversals** visit every reachable node once, in O(V + E), with a **visited** set so cycles don't cause infinite loops:

- **BFS** (a queue) explores level by level, so it finds the **shortest path in unweighted graphs** (and grids).
- **DFS** (recursion or a stack) goes deep first. Use it for connectivity, counting components/islands, cycle detection and topological sort.
- **Grid problems:** neighbours are the 4 directions `(±1, 0), (0, ±1)`; mark cells visited as you go.

### Python

```python
from collections import deque

edges = [(0, 1), (0, 2), (1, 3), (2, 3), (2, 4), (3, 5), (4, 5)]
graph = {v: [] for v in range(6)}
for a, b in edges:                                 # undirected: add both directions
    graph[a].append(b)
    graph[b].append(a)

def bfs_order(graph, start):
    seen, order, q = {start}, [], deque([start])
    while q:
        node = q.popleft()
        order.append(node)
        for nxt in graph[node]:
            if nxt not in seen:
                seen.add(nxt)                      # mark when ENQUEUED, not when popped
                q.append(nxt)
    return order

def shortest_path_length(graph, start, goal):     # BFS = shortest in unweighted graphs
    dist, q = {start: 0}, deque([start])
    while q:
        node = q.popleft()
        if node == goal:
            return dist[node]
        for nxt in graph[node]:
            if nxt not in dist:
                dist[nxt] = dist[node] + 1
                q.append(nxt)
    return -1

def count_islands(grid):                          # DFS flood fill on a grid
    rows, cols, seen = len(grid), len(grid[0]), set()
    def dfs(r, c):
        if not (0 <= r < rows and 0 <= c < cols) or grid[r][c] == "0" or (r, c) in seen:
            return
        seen.add((r, c))
        for dr, dc in ((1, 0), (-1, 0), (0, 1), (0, -1)):
            dfs(r + dr, c + dc)
    islands = 0
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == "1" and (r, c) not in seen:
                dfs(r, c)
                islands += 1
    return islands

bfs_order(graph, 0)                          # → [0, 1, 2, 3, 4, 5]
shortest_path_length(graph, 0, 5)            # → 3
count_islands(["11000", "11000", "00100", "00011"])   # → 3
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [1971. Find if Path Exists in Graph](https://leetcode.com/problems/find-if-path-exists-in-graph/) | 🟢 Easy |
| 2 | [200. Number of Islands](https://leetcode.com/problems/number-of-islands/) | 🟡 Medium |
| 3 | [133. Clone Graph](https://leetcode.com/problems/clone-graph/) | 🟡 Medium |
| 4 | [994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/) | 🟡 Medium |
| 5 | [417. Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/) | 🟡 Medium |
| 6 | [127. Word Ladder](https://leetcode.com/problems/word-ladder/) | 🔴 Hard |

**Learn & visualise:** [GeeksforGeeks: Graph Algorithms](https://www.geeksforgeeks.org/dsa/graph-data-structure-and-algorithms/) · [VisuAlgo: Graph representations](https://visualgo.net/en/graphds) · [VisuAlgo: BFS & DFS](https://visualgo.net/en/dfsbfs)

---

## 21. Shortest Paths: Dijkstra

![Dijkstra](images/dsa/20-dijkstra.svg)

### Theory

| Graph | Algorithm | Time |
|---|---|---|
| Unweighted | **BFS** | O(V + E) |
| Weights 0 or 1 | 0-1 BFS (a deque) | O(V + E) |
| Non-negative weights | **Dijkstra** (a min-heap) | O((V + E) log V) |
| Negative weights (no negative cycle) | Bellman-Ford | O(V · E) |
| All pairs, small V | Floyd-Warshall | O(V³) |

**Dijkstra's idea:** repeatedly take the unfinished node with the **smallest known distance**. With non-negative weights, that distance can't improve later, so it's final. Then **relax** its edges (`dist[v] = min(dist[v], dist[u] + w)`).

- Use a heap of `(distance, node)`. Skip stale entries whose distance is larger than the recorded best (the "lazy deletion" trick).
- **A negative edge breaks it**: a node marked final could later be reached more cheaply.
- To rebuild the actual path, store `parent[v] = u` whenever you improve `dist[v]`.

### Python

```python
import heapq

def dijkstra(graph, source):
    dist = {source: 0}
    heap = [(0, source)]
    while heap:
        d, u = heapq.heappop(heap)
        if d > dist[u]:
            continue                             # stale entry
        for v, w in graph.get(u, []):
            nd = d + w
            if nd < dist.get(v, float("inf")):
                dist[v] = nd
                heapq.heappush(heap, (nd, v))
    return dist

graph = {
    "A": [("B", 4), ("C", 1)], "C": [("B", 2), ("E", 8)],
    "B": [("D", 5), ("E", 6)], "D": [("F", 2)], "E": [("F", 3)],
}
dict(sorted(dijkstra(graph, "A").items()))   # → {"A": 0, "B": 3, "C": 1, "D": 8, "E": 9, "F": 10}
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [743. Network Delay Time](https://leetcode.com/problems/network-delay-time/) | 🟡 Medium |
| 2 | [1631. Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort/) | 🟡 Medium |
| 3 | [787. Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/) | 🟡 Medium |
| 4 | [1091. Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/) | 🟡 Medium |

**Learn & visualise:** [GeeksforGeeks: Dijkstra](https://www.geeksforgeeks.org/dsa/dijkstras-shortest-path-algorithm-greedy-algo-7/) · [VisuAlgo: Shortest paths](https://visualgo.net/en/sssp)

---

## 22. Topological Sort

![Topological sort](images/dsa/21-topological-sort.svg)

### Theory

A **topological order** lists the nodes of a **directed acyclic graph (DAG)** so every edge u → v has u before v: prerequisites first. Build systems, course planners, spreadsheet recalculation and package managers all do this.

- **Kahn's algorithm (BFS):** count each node's incoming edges (**in-degree**); start with all zero-in-degree nodes; when you output a node, decrement its neighbours and enqueue any that reach zero.
- If fewer than V nodes come out, there's a **cycle** (no valid order). That's exactly how "can I finish all courses?" is answered.
- DFS alternative: add a node to the order **after** visiting all its descendants, then reverse.
- O(V + E). Many orders can be valid.

### Python

```python
from collections import deque

def topo_sort(n, prerequisites):
    """prerequisites: (course, needs) pairs. Returns an order, or [] if there's a cycle."""
    graph = [[] for _ in range(n)]
    indegree = [0] * n
    for course, needs in prerequisites:
        graph[needs].append(course)
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
    return order if len(order) == n else []

# 0 Intro, 1 Python, 2 Maths, 3 DSA, 4 ML
topo_sort(5, [(1, 0), (2, 0), (3, 1), (3, 2), (4, 3), (4, 2)])   # → [0, 1, 2, 3, 4]
topo_sort(2, [(0, 1), (1, 0)])                                   # → []
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [207. Course Schedule](https://leetcode.com/problems/course-schedule/) | 🟡 Medium |
| 2 | [210. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/) | 🟡 Medium |
| 3 | [802. Find Eventual Safe States](https://leetcode.com/problems/find-eventual-safe-states/) | 🟡 Medium |
| 4 | [2115. Find All Possible Recipes from Given Supplies](https://leetcode.com/problems/find-all-possible-recipes-from-given-supplies/) | 🟡 Medium |
| 5 | [1462. Course Schedule IV](https://leetcode.com/problems/course-schedule-iv/) | 🟡 Medium |

**Learn & visualise:** [GeeksforGeeks: Topological Sort](https://www.geeksforgeeks.org/dsa/topological-sorting/) · [VisuAlgo: DFS/BFS (topo sort mode)](https://visualgo.net/en/dfsbfs)

---

## 23. Union-Find (Disjoint Set Union)

![Union-find](images/dsa/22-union-find.svg)

### Theory

**Union-Find** tracks which items belong to the same group while groups keep merging. Each group is a tree, and its **root** is the group's representative.

- `find(x)` follows parents up to the root. `union(a, b)` links one root under the other.
- **Path compression** (point nodes straight at the root during `find`) plus **union by size/rank** (attach the smaller tree under the larger) make both operations nearly O(1): O(α(n)), where α is the inverse Ackermann function, below 5 for any practical n.
- Uses: connected components, **detecting a cycle** in an undirected graph (union of two already-connected nodes), Kruskal's minimum spanning tree, and merging accounts or friend circles.
- Better than BFS/DFS when edges arrive **one at a time** and you query connectivity in between.

### Python

```python
class DSU:
    def __init__(self, n):
        self.parent = list(range(n))
        self.size = [1] * n
        self.groups = n

    def find(self, x):
        while self.parent[x] != x:
            self.parent[x] = self.parent[self.parent[x]]   # path halving (a form of compression)
            x = self.parent[x]
        return x

    def union(self, a, b):
        ra, rb = self.find(a), self.find(b)
        if ra == rb:
            return False                                  # already connected → this edge makes a cycle
        if self.size[ra] < self.size[rb]:
            ra, rb = rb, ra
        self.parent[rb] = ra                              # attach smaller tree under larger
        self.size[ra] += self.size[rb]
        self.groups -= 1
        return True

d = DSU(6)
d.union(1, 2), d.union(1, 3), d.union(4, 5)   # → (True, True, True)
d.find(3) == d.find(1), d.find(5) == d.find(1)   # → (True, False)
d.union(3, 5), d.find(5) == d.find(2)          # → (True, True)
d.union(2, 4), d.groups                        # → (False, 2)
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [547. Number of Provinces](https://leetcode.com/problems/number-of-provinces/) | 🟡 Medium |
| 2 | [684. Redundant Connection](https://leetcode.com/problems/redundant-connection/) | 🟡 Medium |
| 3 | [721. Accounts Merge](https://leetcode.com/problems/accounts-merge/) | 🟡 Medium |
| 4 | [1319. Number of Operations to Make Network Connected](https://leetcode.com/problems/number-of-operations-to-make-network-connected/) | 🟡 Medium |

**Learn & visualise:** [GeeksforGeeks: Disjoint Set](https://www.geeksforgeeks.org/dsa/introduction-to-disjoint-set-data-structure-or-union-find-algorithm/) · [VisuAlgo: Union-Find](https://visualgo.net/en/ufds)

---

## 24. Backtracking

![Backtracking decision tree](images/dsa/23-backtracking.svg)

### Theory

**Backtracking** builds a solution one choice at a time and **undoes** the last choice (backtracks) to try the next option. It explores a **decision tree** depth-first.

The template has three parts: **choose → explore → un-choose**.

```text
def backtrack(state):
    if state is a complete solution: record it; return
    for choice in options(state):
        if choice is valid:
            make choice
            backtrack(next state)
            undo choice
```

- Sizes explode: 2ⁿ subsets, n! permutations. **Pruning** (skipping branches that can't lead to a valid answer) is what makes it practical.
- Typical problems: subsets, permutations, combinations or combination sum, N-Queens, Sudoku, word search, and generating valid parentheses.
- Append a **copy** of the current path (`path[:]`), because the list keeps changing.
- To avoid duplicate results with repeated inputs: sort first, and skip equal neighbours at the same depth.

### Python

```python
def subsets(nums):
    out, path = [], []
    def backtrack(i):
        if i == len(nums):
            out.append(path[:])                 # copy!
            return
        path.append(nums[i]); backtrack(i + 1); path.pop()   # include nums[i]
        backtrack(i + 1)                                     # skip nums[i]
    backtrack(0)
    return out

def permutations(nums):
    out, path, used = [], [], [False] * len(nums)
    def backtrack():
        if len(path) == len(nums):
            out.append(path[:])
            return
        for i, x in enumerate(nums):
            if not used[i]:
                used[i] = True; path.append(x)
                backtrack()
                path.pop(); used[i] = False
    backtrack()
    return out

def combination_sum(candidates, target):
    out, path = [], []
    candidates.sort()
    def backtrack(start, remaining):
        if remaining == 0:
            out.append(path[:])
            return
        for i in range(start, len(candidates)):
            if candidates[i] > remaining:
                break                            # prune: sorted, so the rest are too big
            path.append(candidates[i])
            backtrack(i, remaining - candidates[i])   # i, not i + 1: reuse allowed
            path.pop()
    backtrack(0, target)
    return out

subsets([1, 2, 3])                    # → [[1, 2, 3], [1, 2], [1, 3], [1], [2, 3], [2], [3], []]
len(permutations([1, 2, 3, 4]))       # → 24
combination_sum([2, 3, 6, 7], 7)      # → [[2, 2, 3], [7]]
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [78. Subsets](https://leetcode.com/problems/subsets/) | 🟡 Medium |
| 2 | [46. Permutations](https://leetcode.com/problems/permutations/) | 🟡 Medium |
| 3 | [39. Combination Sum](https://leetcode.com/problems/combination-sum/) | 🟡 Medium |
| 4 | [17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/) | 🟡 Medium |
| 5 | [79. Word Search](https://leetcode.com/problems/word-search/) | 🟡 Medium |
| 6 | [51. N-Queens](https://leetcode.com/problems/n-queens/) | 🔴 Hard |

**Learn & visualise:** [GeeksforGeeks: Backtracking](https://www.geeksforgeeks.org/dsa/backtracking-algorithms/)

---

## 25. Greedy Algorithms

![Greedy interval scheduling](images/dsa/24-greedy.svg)

### Theory

A **greedy** algorithm makes the **locally best** choice at each step and never reconsiders it. When it works, it's simple and fast, often just "sort, then one pass". The catch is that it **only works when you can prove** the local choice is always safe:

- **Exchange argument:** any optimal solution can be changed to include the greedy choice without getting worse.
- Greedy works for interval scheduling (earliest **end** first), Huffman coding, Dijkstra, Kruskal/Prim, jump game, gas station, and making change with standard coin systems.
- Greedy **fails** for 0/1 knapsack and for coin change with unusual coins: coins [1, 3, 4] for amount 6 greedily gives 4+1+1 (3 coins), but 3+3 needs 2. Those need DP.
- If you can't find a proof or a counterexample quickly, test greedy against a brute force on small inputs.

### Python

```python
def max_meetings(intervals):
    """Most non-overlapping meetings: sort by END time, take each that starts after the last end."""
    count, last_end = 0, float("-inf")
    for start, end in sorted(intervals, key=lambda m: m[1]):
        if start >= last_end:
            count += 1
            last_end = end
    return count

def can_jump(nums):
    """Jump game: track the farthest index reachable so far."""
    farthest = 0
    for i, jump in enumerate(nums):
        if i > farthest:
            return False
        farthest = max(farthest, i + jump)
    return True

def greedy_coins(coins, amount):
    count = 0
    for c in sorted(coins, reverse=True):
        count += amount // c
        amount %= c
    return count if amount == 0 else -1

max_meetings([(1, 4), (3, 5), (0, 6), (5, 7), (3, 9), (6, 10), (8, 11)])   # → 3
can_jump([2, 3, 1, 1, 4]), can_jump([3, 2, 1, 0, 4])                      # → (True, False)
greedy_coins([1, 3, 4], 6)                                                 # → 3
```

The last line is the **counterexample**: greedy uses 3 coins (4+1+1), but the optimum is 2 (3+3). Section 26 solves it correctly with DP.

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [455. Assign Cookies](https://leetcode.com/problems/assign-cookies/) | 🟢 Easy |
| 2 | [55. Jump Game](https://leetcode.com/problems/jump-game/) | 🟡 Medium |
| 3 | [134. Gas Station](https://leetcode.com/problems/gas-station/) | 🟡 Medium |
| 4 | [435. Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/) | 🟡 Medium |
| 5 | [763. Partition Labels](https://leetcode.com/problems/partition-labels/) | 🟡 Medium |

**Learn & visualise:** [GeeksforGeeks: Greedy](https://www.geeksforgeeks.org/dsa/greedy-algorithms/)

---

## 26. Dynamic Programming

![Dynamic programming](images/dsa/25-dynamic-programming.svg)

### Theory

**Dynamic programming (DP)** solves problems with:

1. **Overlapping subproblems:** the same smaller question is asked again and again (fib(2) in the picture).
2. **Optimal substructure:** the best answer is built from the best answers to the subproblems.

It solves each subproblem **once** and stores the result.

| Style | How | Pros |
|---|---|---|
| **Top-down (memoisation)** | Plain recursion + a cache (`@functools.cache`) | Easiest to write from the recurrence; only solves the states it needs |
| **Bottom-up (tabulation)** | Fill a table from the base cases up | No recursion limit; easy to shrink memory |

**The recipe that works for almost every DP problem:**

1. **State:** what does `dp[i]` (or `dp[i][j]`) mean? Say it in words: "the fewest coins to make amount i".
2. **Transition:** how does a state follow from smaller ones? For coins: `dp[a] = min(dp[a − c] + 1)` over each coin c.
3. **Base cases:** `dp[0] = 0`.
4. **Order:** compute the smaller states first. **Answer:** which state holds it?
5. **Optimise space:** if row i needs only row i − 1, keep two rows (or one).

Common families: 1D (climbing stairs, house robber, coin change), 2D grids (unique paths, minimum path sum), two strings (LCS, edit distance), knapsack, and intervals.

![2D DP grid](images/dsa/26-dp-grid.svg)

### Python

```python
from functools import cache

@cache
def climb(n):                          # top-down: ways to climb n stairs taking 1 or 2 steps
    return 1 if n <= 1 else climb(n - 1) + climb(n - 2)

def coin_change(coins, amount):        # bottom-up: fewest coins (fixes the greedy counterexample)
    INF = amount + 1
    dp = [0] + [INF] * amount
    for a in range(1, amount + 1):
        for c in coins:
            if c <= a:
                dp[a] = min(dp[a], dp[a - c] + 1)
    return dp[amount] if dp[amount] != INF else -1

def unique_paths(rows, cols):          # 2D table, kept as one row: O(cols) space
    row = [1] * cols
    for _ in range(1, rows):
        for c in range(1, cols):
            row[c] += row[c - 1]       # above (old row[c]) + left (new row[c-1])
    return row[-1]

def lcs(a, b):                         # longest common subsequence: the classic two-string DP
    dp = [[0] * (len(b) + 1) for _ in range(len(a) + 1)]
    for i in range(1, len(a) + 1):
        for j in range(1, len(b) + 1):
            if a[i - 1] == b[j - 1]:
                dp[i][j] = dp[i - 1][j - 1] + 1
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
    return dp[-1][-1]

def rob(houses):                       # house robber: take this house + best two back, or skip it
    take_prev, best = 0, 0
    for money in houses:
        take_prev, best = best, max(best, take_prev + money)
    return best

climb(10)                              # → 89
coin_change([1, 3, 4], 6)              # → 2
coin_change([2], 3)                    # → -1
unique_paths(3, 5)                     # → 15
lcs("abcde", "ace")                    # → 3
rob([2, 7, 9, 3, 1])                   # → 12
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/) | 🟢 Easy |
| 2 | [198. House Robber](https://leetcode.com/problems/house-robber/) | 🟡 Medium |
| 3 | [322. Coin Change](https://leetcode.com/problems/coin-change/) | 🟡 Medium |
| 4 | [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/) | 🟡 Medium |
| 5 | [62. Unique Paths](https://leetcode.com/problems/unique-paths/) | 🟡 Medium |
| 6 | [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/) | 🟡 Medium |
| 7 | [72. Edit Distance](https://leetcode.com/problems/edit-distance/) | 🟡 Medium |

**Learn & visualise:** [GeeksforGeeks: Dynamic Programming](https://www.geeksforgeeks.org/dsa/dynamic-programming/) · [VisuAlgo: Recursion tree → DP](https://visualgo.net/en/recursion)

---

## 27. Bit Manipulation

![Bits](images/dsa/27-bits.svg)

### Theory

Integers are stored in **binary**, and bitwise operators work on every bit at once in O(1):

| Operator | Meaning | Common use |
|---|---|---|
| `a & b` | AND | Test or clear bits; `x & 1` checks for odd |
| `a \| b` | OR | Set bits |
| `a ^ b` | XOR | Toggle bits; `x ^ x = 0`, so pairs cancel |
| `~x` | NOT | In Python, `~x == -x - 1` |
| `x << k`, `x >> k` | Shift | Multiply or divide by 2ᵏ |

- **Tricks:**
  - `x & (x - 1)` clears the lowest set bit (count bits, or test for a power of two: `x > 0 and x & (x - 1) == 0`);
  - `x & -x` isolates the lowest set bit;
  - XOR everything to find the single unpaired number.
- **Bitmasks** represent subsets of up to ~20 items as integers: bit i set means item i is in the subset. That enables bitmask DP, and it's another way to enumerate subsets.
- Python ints have **unlimited precision** (no overflow), and negatives behave as if infinitely sign-extended. Mask with `& 0xFFFFFFFF` to mimic 32-bit behaviour.

### Python

```python
def count_bits(x):
    count = 0
    while x:
        x &= x - 1                 # drop the lowest set bit
        count += 1
    return count

def single_number(nums):           # every number appears twice except one
    result = 0
    for x in nums:
        result ^= x
    return result

def is_power_of_two(x):
    return x > 0 and x & (x - 1) == 0

def subsets_by_mask(items):
    n = len(items)
    return [[items[i] for i in range(n) if mask >> i & 1] for mask in range(1 << n)]

bin(13), count_bits(13), (13).bit_count()        # → ("0b1101", 3, 3)
single_number([4, 1, 2, 1, 2])                   # → 4
is_power_of_two(64), is_power_of_two(96)         # → (True, False)
subsets_by_mask(["a", "b", "c"])                 # → [[], ["a"], ["b"], ["a", "b"], ["c"], ["a", "c"], ["b", "c"], ["a", "b", "c"]]
12 & 10, 12 | 10, 12 ^ 10, 13 << 1, 13 >> 1      # → (8, 14, 6, 26, 6)
```

### Practice

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/) | 🟢 Easy |
| 2 | [136. Single Number](https://leetcode.com/problems/single-number/) | 🟢 Easy |
| 3 | [338. Counting Bits](https://leetcode.com/problems/counting-bits/) | 🟢 Easy |
| 4 | [268. Missing Number](https://leetcode.com/problems/missing-number/) | 🟢 Easy |
| 5 | [190. Reverse Bits](https://leetcode.com/problems/reverse-bits/) | 🟢 Easy |
| 6 | [371. Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/) | 🟡 Medium |

**Learn & visualise:** [GeeksforGeeks: Bitwise Algorithms](https://www.geeksforgeeks.org/dsa/bitwise-algorithms/) · [VisuAlgo: Bitmask](https://visualgo.net/en/bitmask)

---

## 28. Pattern Cheat Sheet: Which Technique When?

Read the problem for **clues**, then match them to a technique:

| Clue in the problem | Try |
|---|---|
| "Sorted array", "find a pair/triplet" | Two pointers, binary search |
| "Contiguous subarray/substring", "longest/shortest … such that" | Sliding window (positives) or prefix sums + hash map (negatives) |
| "How many times…", "have we seen…", "group by…" | Hash map / set / `Counter` |
| "Minimum X that works", "maximise the minimum" | Binary search on the answer |
| "Next greater/smaller", "matching brackets" | Stack / monotonic stack |
| "Top k", "k-th largest", "merge k sorted", "running median" | Heap |
| "Shortest path", "minimum steps" (unweighted, grid) | BFS |
| Weighted shortest path | Dijkstra |
| "All combinations/permutations/subsets", "place N queens" | Backtracking |
| "Order with dependencies", "can all tasks finish" | Topological sort |
| "Connected groups", "merge accounts", edges arriving over time | Union-Find (or BFS/DFS) |
| "Prefix", "autocomplete", "words from a dictionary" | Trie |
| "Number of ways", "min/max cost", choices that overlap | Dynamic programming |
| "Pick the best locally" + a provable exchange argument | Greedy |
| "Appears once while others appear twice", subsets of ≤ 20 | Bit manipulation |

**Complexity summary of the core structures:**

| Structure | Access | Search | Insert | Delete | Notes |
|---|---|---|---|---|---|
| Array / list | O(1) | O(n) | O(1) end, O(n) middle | O(1) end, O(n) middle | Cache-friendly |
| Hash map / set | — | O(1) avg | O(1) avg | O(1) avg | O(n) worst case |
| Linked list | O(n) | O(n) | O(1) at a known node | O(1) at a known node | |
| Stack / queue / deque | top/ends O(1) | O(n) | O(1) | O(1) | |
| Balanced BST | O(log n) | O(log n) | O(log n) | O(log n) | Ordered iteration |
| Binary heap | min O(1) | O(n) | O(log n) | pop O(log n) | |
| Trie | — | O(L) | O(L) | O(L) | L = word length |

**A study plan that works:**

1. Learn a topic's theory here, and watch it animate on VisuAlgo.
2. Solve its **Easy** problems without hints, then the **Medium** ones (give each 30–45 minutes before reading a solution).
3. After reading a solution, **re-solve it from scratch** two days later. Spaced repetition beats volume.
4. Keep a log: problem, pattern, the key insight in one line, and mistakes made.
5. Once each pattern feels familiar, mix topics randomly (NeetCode lists or LeetCode's random problems), because interviews don't tell you the pattern.

**Where to practise:**

- **LeetCode**: the main interview platform (the problems linked under each topic above).
- [NeetCode](https://neetcode.io/practice): curated lists by pattern, with video explanations.
- [GeeksforGeeks DSA](https://www.geeksforgeeks.org/dsa/dsa-tutorial-learn-data-structures-and-algorithms/): theory articles and practice.
- [HackerRank](https://www.hackerrank.com/domains/data-structures): structured tracks.
- [CSES](https://cses.fi/problemset/): 300+ classic algorithm problems.
- [VisuAlgo](https://visualgo.net/en): animations of every structure here.
- [Python Tutor](https://pythontutor.com/): step through your code and see the memory.

---

## 29. Most Asked DSA Theory Questions

1. **Array vs linked list?** → Arrays have O(1) indexing and are cache-friendly, but inserting in the middle is O(n). Linked lists insert in O(1) at a known node but need O(n) to reach the k-th item.
2. **How does a hash table achieve O(1)? When does it degrade?** → Hashing maps keys straight to slots. With many collisions (a bad hash, or adversarial keys) lookups approach O(n); resizing keeps the load factor low.
3. **Why must dict keys be immutable in Python?** → The hash must never change while the key is stored, or the entry would be lost in the wrong slot.
4. **Stack vs queue? Real uses?** → LIFO (undo, call stack, DFS, brackets) vs FIFO (BFS, scheduling, buffering).
5. **What is amortised complexity? Example?** → The average cost per operation over a sequence. `list.append` is O(1) amortised despite occasional O(n) resizes.
6. **When does binary search apply beyond sorted arrays?** → Whenever a yes/no condition is monotonic: binary search on the answer (minimum speed, capacity, time).
7. **Merge sort vs quick sort?** → Merge: guaranteed O(n log n), stable, O(n) extra space. Quick: faster in practice and in-place, but O(n²) worst case (avoid with random pivots), not stable.
8. **What is a stable sort? Is Python's sort stable?** → Equal keys keep their input order. Yes, Timsort is stable.
9. **BFS vs DFS? When would you choose each?** → BFS: shortest path in unweighted graphs, level order, O(width) memory. DFS: connectivity, cycles, topological sort, backtracking, O(depth) memory.
10. **Why can't Dijkstra handle negative edges?** → It finalises the closest node on the assumption that no later path can be cheaper; a negative edge breaks that assumption. Use Bellman-Ford.
11. **What properties must a problem have for DP?** → Overlapping subproblems and optimal substructure.
12. **Memoisation vs tabulation?** → Top-down recursion with a cache vs bottom-up table filling. Same complexity; tabulation avoids recursion limits and makes it easy to reduce space.
13. **Greedy vs DP: how do you choose?** → Greedy needs a proof that the local choice is always safe (exchange argument). If the choices interact (knapsack, odd coin systems), use DP.
14. **What is a heap? How is it stored?** → A complete binary tree with the heap-order property, stored in an array (children at 2i+1 and 2i+2). O(1) peek, O(log n) push and pop, O(n) build.
15. **How does union-find stay nearly O(1)?** → Path compression and union by size/rank give O(α(n)) amortised.
16. **How do you detect a cycle in a directed graph vs an undirected graph?** → Directed: DFS with an "in the current path" colour, or Kahn's algorithm outputting fewer than V nodes. Undirected: union-find (union of already-connected nodes), or DFS that ignores the edge back to the parent.
17. **What is the time complexity of recursion like fib(n)? How do you fix it?** → O(2ⁿ) calls because subproblems repeat. Memoise, or tabulate, for O(n).
18. **What's a trie good for that a hash set isn't?** → Prefix queries (autocomplete, `starts_with`) in O(length of prefix).
19. **How do you choose a data structure for a problem?** → List the operations the problem needs most often (lookup, min, order, prefix…) and pick the structure that makes those cheapest.
20. **Space complexity of a recursive DFS on a tree?** → O(h), the height: O(log n) if balanced, O(n) if skewed.

---
