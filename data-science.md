# Data Science with Python: From Absolute Basics to Interviews

The data toolkit every data analyst, data scientist and AI/ML engineer uses, explained from zero, in **five levels**: **Basic** (Python for data, the shapes data comes in, NumPy arrays) → **Easy** (pandas tables: loading, selecting, filtering, new columns) → **Moderate** (cleaning, grouping, merging, reshaping, dates and time series, bigger data with Arrow, Polars and DuckDB, charts with Matplotlib, Seaborn and Plotly) → **Advanced** (statistics from probability to A/B tests and regression, a complete EDA, feature engineering, data pipelines, communicating results) → **Interview Prep**. **Each part uses only what earlier parts taught**, so read in order.

**Nothing is left for you to look up.** Every technical word is explained in plain language the first time it appears (look for the **Words to know** box at the top of a section), and Section [70](#70-glossary-every-term-in-these-notes) collects every term in one alphabetical glossary with a link back to where it's taught.

Every section has the same shape:

1. **Picture:** a diagram or a real chart of the idea.
2. **Theory:** what it is, an everyday picture, how it works step by step (often traced by hand in a table), when to use it, when *not* to, common mistakes, and where it's used in real software.
3. **Python:** short working programs. Every example was run with **Python 3.13, NumPy 2.5, pandas 3.0, Matplotlib 3.11, Seaborn 0.13, SciPy 1.18, statsmodels, Polars, DuckDB and Plotly**: results under **Output** are real, and every chart image was produced by the code next to it.
4. **Practice:** exercises with hidden answers, plus graded problems (🟢 Easy, 🟡 Medium, 🔴 Hard, all free) from LeetCode's pandas track and Deep-ML's NumPy, probability and statistics problems, and links to read and watch.

Each part ends with a ✅ **checkpoint**. Before this file you need basic Python (`dsa-python.md` Parts 1–3 or `python.md` Parts 1–2; Section [3](#3-python-refresher-for-data-work-lists-dicts-comprehensions-and-functions) recaps what's used here). After it, continue with `machine-learning.md`. The SQL notes (`sql-postgresql.md`) teach the database side of the same work.

## Table of Contents

**[Part 1 — Basic: Getting Started with Data](#part-1--basic-getting-started-with-data)**

1. [How to Use These Notes (and What Data Scientists Do)](#1-how-to-use-these-notes-and-what-data-scientists-do)
2. [Setting Up: Python, Virtual Environments, uv and Jupyter Notebooks](#2-setting-up-python-virtual-environments-uv-and-jupyter-notebooks)
3. [Python Refresher for Data Work: Lists, Dicts, Comprehensions and Functions](#3-python-refresher-for-data-work-lists-dicts-comprehensions-and-functions)
4. [What Data Looks Like: Types of Data, Tables and Tidy Data](#4-what-data-looks-like-types-of-data-tables-and-tidy-data)
5. [Reading Files with Plain Python: Text, CSV and JSON](#5-reading-files-with-plain-python-text-csv-and-json)

**[Part 2 — Basic: NumPy, Fast Arrays of Numbers](#part-2--basic-numpy-fast-arrays-of-numbers)**

6. [Why NumPy? Arrays vs Lists, and How Arrays Sit in Memory](#6-why-numpy-arrays-vs-lists-and-how-arrays-sit-in-memory)
7. [Creating Arrays: array, arange, linspace, zeros, ones and full](#7-creating-arrays-array-arange-linspace-zeros-ones-and-full)
8. [Shape, Dimensions and dtypes](#8-shape-dimensions-and-dtypes)
9. [Indexing and Slicing (1D and 2D), Views vs Copies](#9-indexing-and-slicing-1d-and-2d-views-vs-copies)
10. [Boolean Masks, Fancy Indexing and np.where](#10-boolean-masks-fancy-indexing-and-npwhere)
11. [Vectorised Maths and Universal Functions](#11-vectorised-maths-and-universal-functions)
12. [Aggregations and the axis Argument](#12-aggregations-and-the-axis-argument)
13. [Broadcasting: Maths Between Arrays of Different Shapes](#13-broadcasting-maths-between-arrays-of-different-shapes)
14. [Reshaping, Stacking, Splitting and Sorting](#14-reshaping-stacking-splitting-and-sorting)
15. [Random Numbers and Simulation](#15-random-numbers-and-simulation)
16. [Linear Algebra Basics: Dot Products, Matrix Multiplication and Solving Equations](#16-linear-algebra-basics-dot-products-matrix-multiplication-and-solving-equations)

**[Part 3 — Easy: pandas Basics, Working with Tables](#part-3--easy-pandas-basics-working-with-tables)**

17. [pandas Series: Labelled 1D Data](#17-pandas-series-labelled-1d-data)
18. [DataFrames: Creating, Inspecting and Understanding a Table](#18-dataframes-creating-inspecting-and-understanding-a-table)
19. [Reading and Writing Files: CSV, Excel, JSON and Parquet](#19-reading-and-writing-files-csv-excel-json-and-parquet)
20. [Reading from Databases and Web APIs](#20-reading-from-databases-and-web-apis)
21. [Selecting Data: Columns, [], loc and iloc](#21-selecting-data-columns--loc-and-iloc)
22. [Filtering Rows: Conditions, isin, between and query](#22-filtering-rows-conditions-isin-between-and-query)
23. [Sorting, Ranking and Top-N](#23-sorting-ranking-and-top-n)
24. [Adding and Changing Columns: Arithmetic, assign, map, apply and np.select](#24-adding-and-changing-columns-arithmetic-assign-map-apply-and-npselect)
25. [Method Chaining and Copy-on-Write (pandas 3)](#25-method-chaining-and-copy-on-write-pandas-3)

**[Part 4 — Moderate: Cleaning Data](#part-4--moderate-cleaning-data)**

26. [Missing Values: Finding, Dropping and Filling](#26-missing-values-finding-dropping-and-filling)
27. [Duplicates, Data Types and Type Conversion](#27-duplicates-data-types-and-type-conversion)
28. [Text Data: The .str Accessor and Regular Expressions](#28-text-data-the-str-accessor-and-regular-expressions)
29. [Categorical Data and Binning (cut and qcut)](#29-categorical-data-and-binning-cut-and-qcut)
30. [Outliers and Data Validation](#30-outliers-and-data-validation)

**[Part 5 — Moderate: Analysing Data](#part-5--moderate-analysing-data)**

31. [Grouping I: groupby, agg and Split-Apply-Combine](#31-grouping-i-groupby-agg-and-split-apply-combine)
32. [Grouping II: transform, filter, apply and Group-Wise Ranking](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking)
33. [Combining Tables I: merge and Join Types](#33-combining-tables-i-merge-and-join-types)
34. [Combining Tables II: concat, Validation and Merge Pitfalls](#34-combining-tables-ii-concat-validation-and-merge-pitfalls)
35. [Reshaping: pivot_table, melt, crosstab and explode](#35-reshaping-pivot_table-melt-crosstab-and-explode)
36. [MultiIndex, stack and unstack](#36-multiindex-stack-and-unstack)
37. [Dates and Times: Parsing, .dt, Time Zones and Periods](#37-dates-and-times-parsing-dt-time-zones-and-periods)
38. [Time Series: resample, rolling, shift and Window Functions](#38-time-series-resample-rolling-shift-and-window-functions)

**[Part 6 — Moderate: Bigger and Faster Data](#part-6--moderate-bigger-and-faster-data)**

39. [Performance: Vectorise, Avoid Loops and Measure](#39-performance-vectorise-avoid-loops-and-measure)
40. [Memory: dtypes, Categoricals, Chunking and Apache Arrow](#40-memory-dtypes-categoricals-chunking-and-apache-arrow)
41. [Polars: Fast DataFrames with Lazy Queries](#41-polars-fast-dataframes-with-lazy-queries)
42. [DuckDB: SQL on DataFrames and Files](#42-duckdb-sql-on-dataframes-and-files)

**[Part 7 — Moderate: Charts with Matplotlib, Seaborn and Plotly](#part-7--moderate-charts-with-matplotlib-seaborn-and-plotly)**

43. [Your First Charts with Matplotlib](#43-your-first-charts-with-matplotlib)
44. [Matplotlib Anatomy: Figures, Axes and Subplots](#44-matplotlib-anatomy-figures-axes-and-subplots)
45. [Styling, Annotation and Saving Charts](#45-styling-annotation-and-saving-charts)
46. [Seaborn I: Distributions](#46-seaborn-i-distributions)
47. [Seaborn II: Relationships, Categories and Facets](#47-seaborn-ii-relationships-categories-and-facets)
48. [Heatmaps, Pair Plots and Correlation Charts](#48-heatmaps-pair-plots-and-correlation-charts)
49. [Interactive Charts with Plotly](#49-interactive-charts-with-plotly)
50. [Choosing the Right Chart (and Not Misleading)](#50-choosing-the-right-chart-and-not-misleading)

**[Part 8 — Advanced: Statistics](#part-8--advanced-statistics)**

51. [Describing Data: Centre, Spread and Shape](#51-describing-data-centre-spread-and-shape)
52. [Correlation, Covariance and Causation](#52-correlation-covariance-and-causation)
53. [Probability Basics: Events, Conditional Probability and Bayes' Rule](#53-probability-basics-events-conditional-probability-and-bayes-rule)
54. [Probability Distributions: Normal, Binomial, Poisson and More](#54-probability-distributions-normal-binomial-poisson-and-more)
55. [Sampling, the Central Limit Theorem and Standard Error](#55-sampling-the-central-limit-theorem-and-standard-error)
56. [Confidence Intervals and the Bootstrap](#56-confidence-intervals-and-the-bootstrap)
57. [Hypothesis Testing: p-values, t-tests, Chi-Square and Non-Parametric Tests](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests)
58. [A/B Testing End to End: Design, Power, Sample Size and Pitfalls](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls)
59. [Regression for Analysis: statsmodels, Coefficients and Confidence](#59-regression-for-analysis-statsmodels-coefficients-and-confidence)

**[Part 9 — Advanced: Data Science in Practice](#part-9--advanced-data-science-in-practice)**

60. [A Complete Exploratory Data Analysis (EDA)](#60-a-complete-exploratory-data-analysis-eda)
61. [Feature Engineering: Preparing Data for Machine Learning](#61-feature-engineering-preparing-data-for-machine-learning)
62. [Data Pipelines and Data Quality in Production](#62-data-pipelines-and-data-quality-in-production)
63. [Communicating Results: Reports, Dashboards and Data Storytelling](#63-communicating-results-reports-dashboards-and-data-storytelling)
64. [What's New: Modern Data Tooling (2023–2026)](#64-whats-new-modern-data-tooling-20232026)

**[Part 10 — Interview Prep: Revision](#part-10--interview-prep-revision)**

65. [Interview Topic Checklist: What Companies Ask](#65-interview-topic-checklist-what-companies-ask)
66. [Interview Problems: pandas, NumPy and SQL-Style Questions](#66-interview-problems-pandas-numpy-and-sql-style-questions)
67. [Statistics, Probability and Product Interview Problems](#67-statistics-probability-and-product-interview-problems)
68. [Cheat Sheet: Which Tool or Method When?](#68-cheat-sheet-which-tool-or-method-when)
69. [Most Asked Data Science Theory Questions](#69-most-asked-data-science-theory-questions)
70. [Glossary: Every Term in These Notes](#70-glossary-every-term-in-these-notes)

---

# Part 1 — Basic: Getting Started with Data

> **Goal:** Know what data science is, set up your tools, refresh the Python you'll use every day, recognise the kinds of data you'll meet, and load a file with plain Python, so you understand what the libraries in later parts do for you.  
> **You need:** Basic Python: variables, `if`, loops and functions (`dsa-python.md` Parts 1–3 or `python.md` Parts 1–2).

---

## 1. How to Use These Notes (and What Data Scientists Do)

![The learning path through these notes](images/data-science/00-roadmap.svg)

### Theory

> **In simple words:** data science means **turning raw data into answers you can trust**. You collect data, clean it, explore it, summarise it, draw it, test ideas with statistics, and explain what you found so someone can make a decision.

**Words to know:**

- **Data:** recorded facts. A list of orders, sensor readings, survey answers, web clicks.
- **Dataset:** one collection of data about one subject, usually a table (or a few related tables).
- **Library (or package):** code someone else wrote that you install and reuse. NumPy, pandas and Matplotlib are libraries.
- **Analysis:** working out what the data says: totals, averages, trends, differences between groups.
- **Statistics:** the maths of drawing conclusions from data that contains randomness, and of saying how sure you are.
- **Machine learning (ML):** letting a program learn a rule from examples instead of writing the rule by hand (the `machine-learning.md` notes).
- **Model:** a simplified mathematical description of how something works, fitted to data: a straight line through points, or a trained ML program that maps inputs to predictions.
- **Algorithm:** an exact, step-by-step procedure for solving a problem (sorting a list, fitting a line).
- **scikit-learn / PyTorch:** the main Python libraries for classic machine learning and for deep learning (neural networks), taught in `machine-learning.md` and `deep-learning.md`.
- **LLM (large language model):** an AI model trained on huge amounts of text that can read and write language (Claude, GPT, Gemini); `llm-engineering.md` covers them.
- **Spark (Apache Spark):** a system that spreads data processing across many computers (a **cluster**) for data too big for one machine.
- **Kaggle / LeetCode / Deep-ML:** free practice websites: Kaggle for datasets, competitions and short courses; LeetCode for coding problems (including pandas and SQL tracks); Deep-ML for maths, statistics and ML coding problems.

**Everyday picture.** A shop owner keeps every receipt in a shoebox. Data science is everything between "a shoebox of receipts" and "we should stock more umbrellas in Mumbai in June": sorting the receipts, throwing out the torn ones, adding them up by city and month, drawing a chart, and checking that the June jump isn't just luck.

**The data workflow** (you'll repeat this loop in every project):

| Step | What you do | Where in these notes |
|---|---|---|
| 1. **Ask** | Turn a vague wish ("sales are weird") into a clear question ("did average order value fall in March, and in which cities?") | Section [60](#60-a-complete-exploratory-data-analysis-eda) |
| 2. **Get** | Load files (CSV, Excel, Parquet), query databases (SQL), call web APIs | Parts 1 and 3 |
| 3. **Clean** | Fix missing values, wrong types, duplicates and typos. Often **most** of the work | Part 4 |
| 4. **Explore** | Summaries, groupings and charts to find patterns and problems (**EDA**, *exploratory data analysis*) | Parts 5–7 |
| 5. **Test / model** | Check whether a difference is real (statistics), or predict something (ML) | Part 8, then `machine-learning.md` |
| 6. **Communicate** | A chart, a table, a short report, a dashboard, a decision | Sections [50](#50-choosing-the-right-chart-and-not-misleading), [63](#63-communicating-results-reports-dashboards-and-data-storytelling) |

**Who does this work:**

| Role | Mostly does | Main tools |
|---|---|---|
| **Data analyst** | Answers business questions with SQL, spreadsheets, pandas and dashboards | SQL, pandas, charts |
| **Data scientist** | Analysis plus statistics, experiments (A/B tests) and predictive models | pandas, statistics, scikit-learn |
| **Data engineer** | Builds the pipelines that move and clean data reliably at scale | SQL, Python, Spark, orchestration tools |
| **ML / AI engineer** | Builds and ships models and AI features | pandas, scikit-learn, PyTorch, LLM APIs |

All four use what this file teaches.

**These notes climb level by level.** Each part uses only what earlier parts taught. If a section ever uses a word or a tool that wasn't explained earlier, treat it as a mistake in the notes.

| Part | Level | What you learn | Afterwards you can… |
|---|---|---|---|
| 1 | Basic | What data science is, setup, Python for data, kinds of data, loading files by hand | Load a CSV with plain Python and say what kind of data each column holds |
| 2 | Basic | NumPy: arrays, dtypes, indexing, masks, vectorised maths, axes, broadcasting, reshaping, random numbers, linear algebra | Do fast maths on whole arrays without loops |
| 3 | Easy | pandas basics: Series, DataFrames, files, databases, APIs, selecting, filtering, sorting, new columns, method chaining | Load any table and pull out exactly the rows and columns you need |
| 4 | Moderate | Cleaning: missing values, duplicates, types, text, categories, outliers, validation | Turn a messy file into a clean, trustworthy table |
| 5 | Moderate | Analysis: groupby, merge, reshape, MultiIndex, dates, time series | Answer "per group", "per month" and "compared with" questions |
| 6 | Moderate | Speed and size: vectorising, memory, Arrow, Polars, DuckDB | Work with data bigger than a few hundred megabytes |
| 7 | Moderate | Charts: Matplotlib, Seaborn, Plotly, choosing the right chart | Draw clear, honest charts |
| 8 | Advanced | Statistics: describing data, correlation, probability, distributions, sampling, confidence intervals, hypothesis tests, A/B tests, regression | Say whether a difference is real and how sure you are |
| 9 | Advanced | Practice: a full EDA, feature engineering, pipelines and data quality, communicating results, modern tooling | Run a complete project and present it |
| 10 | Interview Prep | What companies ask, interview problems, a cheat sheet, theory questions, the glossary | Revise quickly and check your coverage |

**How to study each section:**

1. **Picture:** look at the diagram first; it shows the whole idea at once.
2. **Theory:** read it slowly. Trace the worked examples with a pen before reading the code.
3. **Python:** **type the code yourself** instead of copy-pasting, run it, then change one number and predict the new result *before* running again. Results are shown under **Output**.
4. **Practice:** try each exercise before opening its **Answer**. The LeetCode tables (from Part 3 on) are real interview-style problems that accept pandas solutions.

**Each part ends with a checkpoint:** a list of things you should be able to do without looking. If you can't, redo that part's exercises before moving on.

**Conventions:** ❌ = wrong or risky, ✅ = recommended. `# →` in a code comment means "this gives". Long numbers are written with underscores (`1_000_000`), which Python also accepts.

### Practice

1. Write down one question you'd like to answer with data from your own life (your spending, a sports team, your city's weather). Keep it: you'll practise on it throughout these notes.
2. For that question, write which of the six workflow steps you think will be hardest, and why.

**Learn more:** [Kaggle Learn: free short data courses](https://www.kaggle.com/learn) · [Python Data Science Handbook (free online book)](https://jakevdp.github.io/PythonDataScienceHandbook/)

---

## 2. Setting Up: Python, Virtual Environments, uv and Jupyter Notebooks

![A notebook is a list of cells that all talk to one running Python process, the kernel](images/data-science/02-notebook.svg)

### Theory

> **In simple words:** you need Python, the data libraries, and a comfortable place to run code bit by bit. A **notebook** lets you run one small piece of code, look at the result, and then decide what to try next, which is exactly how exploring data feels.

**Words to know:**

- **Package manager:** a tool that downloads and installs libraries for you (`pip`, `uv`, `conda`).
- **Virtual environment ("venv"):** a private folder of installed libraries for **one** project, so two projects can use different versions without breaking each other.
- **Notebook (`.ipynb` file):** a document made of **cells**. A **code cell** holds Python; a **Markdown cell** holds notes. Each code cell's result is shown right under it and saved in the file.
- **Kernel:** the running Python process behind a notebook. Every cell you run sends its code to the kernel, and the kernel **remembers** every variable until you restart it.
- **Jupyter / JupyterLab:** the free program that opens notebooks in your browser.
- **IDE (integrated development environment):** an editor with built-in running and debugging, such as **VS Code**, which also opens notebooks.
- **Import:** loading a library into your program with `import name`.
- **Alias:** a short nickname for an imported library, like `import pandas as pd`.
- **uv:** a fast, modern Python package and project manager (installs libraries, creates venvs, records exact versions in a lock file).
- **Google Colab:** Google's free browser-based notebook service with the data libraries pre-installed.
- **Git:** the standard version-control tool: it records every change to your files so you can review, share and undo them.

**Everyday picture.** A notebook is a lab bench with a notepad: you try something, write down what happened, and try the next thing. The kernel is the person doing the experiments; they remember everything done so far, even if you tore the page out of the notepad.

**Three ways to get started (pick one):**

| Option | Steps | Good for |
|---|---|---|
| **Google Colab** | Open [colab.research.google.com](https://colab.research.google.com), sign in, "New notebook". NumPy, pandas, Matplotlib, Seaborn, SciPy and scikit-learn are already installed | The fastest start; nothing to install |
| **uv** (fast, modern) | Install uv from [docs.astral.sh/uv](https://docs.astral.sh/uv/), then in a project folder: `uv init`, `uv add numpy pandas matplotlib seaborn scipy statsmodels pyarrow polars duckdb plotly jupyterlab`, then `uv run jupyter lab` | Your own computer; reproducible projects |
| **pip + venv** (built in) | `python -m venv .venv`, activate it (`source .venv/bin/activate` on macOS/Linux, `.venv\Scripts\activate` on Windows), then `pip install numpy pandas ...` | When you can't install uv |

`uv init` creates a `pyproject.toml` file listing your project's libraries, and `uv add` installs them into a venv **and** records them, so anyone can recreate the exact setup later with `uv sync`. That's the modern habit; the `python.md` notes explain packaging in depth.

**Notebook habits that save hours:**

- **Run cells top to bottom.** The kernel keeps variables from cells you've deleted or edited, so a notebook can "work" for you and fail for everyone else. Before sharing, use **Restart kernel and run all**.
- **The last line of a cell is displayed automatically.** A DataFrame shows as a formatted table; you only need `print` for earlier lines.
- **Magic commands** start with `%` and talk to the notebook itself, not Python: `%timeit expr` times a line, `%who` lists variables, `%pip install x` installs into the running kernel.
- **Notebooks are for exploring; `.py` files are for repeating.** When code needs to run every day (a pipeline, an app), move it into functions in a `.py` file.

**Standard import names** (everyone uses these, so code examples online look the same):

```text
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

**When notebooks are the wrong tool:** long-running jobs, code other programs import, anything that needs tests or code review line by line. Notebooks also store outputs inside the file, which makes `git` diffs noisy; tools like `jupytext` or `nbstripout` help when you must version them.

**Common mistakes:**

- ❌ Installing with `pip install` into the system Python, then wondering why the notebook can't find the library. ✅ One venv per project, and point the notebook at it (in VS Code: "Select Kernel").
- ❌ Running cells out of order and trusting the result. ✅ Restart and run all before you believe or share anything.
- ❌ `from pandas import *`. ✅ `import pandas as pd`, so you always know where a name came from.

**Used in real software:** notebooks are where most data analysis and model prototyping starts at companies of every size; Colab, Kaggle, Databricks, Hex, Deepnote and VS Code all run the same `.ipynb` format.

### Python

Run this in your first notebook cell. It prints the version of each library, which is the first thing to check when an example behaves differently for you:

```python
import sys
import numpy as np
import pandas as pd
import matplotlib
import scipy

print("Python", sys.version.split()[0])
print("NumPy", np.__version__, "| pandas", pd.__version__)
print("Matplotlib", matplotlib.__version__, "| SciPy", scipy.__version__)
```

**Output:**

```text
Python 3.13.2
NumPy 2.5.3 | pandas 3.0.6
Matplotlib 3.11.2 | SciPy 1.18.1
```

Your numbers may be a little different; anything at or above these versions runs every example in these notes.

### Practice

1. Set up one of the three options and run the version cell above.
2. In a notebook, run `x = 5` in one cell, delete that cell, then run `print(x)` in a new cell. What happens, and why? Then restart the kernel and run `print(x)` again.

<details>
<summary><b>Answer</b></summary>

The first `print(x)` prints `5`: deleting a cell doesn't delete the variable, because the **kernel** still remembers it. After a restart the kernel's memory is empty, so you get `NameError: name 'x' is not defined`. This is why "restart and run all" is the only honest test of a notebook.

</details>

**Learn more:** [uv documentation](https://docs.astral.sh/uv/) · [JupyterLab: getting started](https://jupyterlab.readthedocs.io/en/latest/getting_started/overview.html) · [VS Code: Jupyter notebooks](https://code.visualstudio.com/docs/datascience/jupyter-notebooks)

---

## 3. Python Refresher for Data Work: Lists, Dicts, Comprehensions and Functions

![A list comprehension: for each item, optionally filter it, then transform it](images/data-science/03-comprehension.svg)

### Theory

> **In simple words:** before the libraries, plain Python already holds data well: a **list** keeps things in order, a **dict** looks things up by name, and a **list of dicts** is a table. This section recaps exactly the Python features the rest of the notes rely on.

**Words to know:**

- **List:** an ordered, changeable collection: `[3, 1, 4]`. Get items by **position** (index), starting from 0.
- **Tuple:** like a list but **can't be changed** after creation: `(3, 1)`. Used for fixed groups like `(row, column)`.
- **Dict (dictionary):** a collection of **key → value** pairs: `{"city": "Pune", "qty": 5}`. Get a value by its key.
- **Set:** an unordered collection with **no duplicates**: `{"Pune", "Delhi"}`. Fast "is this in it?" checks.
- **Comprehension:** a one-line way to build a list, dict or set from another collection.
- **Function:** a named, reusable block of code that takes **arguments** (inputs) and **returns** a result.
- **Lambda:** a tiny function without a name, written in one expression: `lambda x: x * 2`.
- **Record:** one row of data, such as one order. A list of dicts is a list of records.
- **f-string:** a string with `f` in front that fills in values: `f"{name} spent {total:.2f}"` (`:.2f` = 2 decimal places).
- **Loop:** code that repeats for each item (`for x in items:`) or while a condition holds (`while ...:`).
- **Standard library / module:** the collection of modules that come with Python (`csv`, `json`, `collections`, `math`); a **module** is one importable file of code.

**Everyday picture.** A list is a numbered queue of people; a dict is a phone book (look up by name, not by position); a list of dicts is a stack of filled-in forms, one form per order, each with the same labelled boxes.

**The features you'll use constantly:**

| Feature | Example | Result |
|---|---|---|
| Index / slice a list | `nums[0]`, `nums[-1]`, `nums[1:3]` | first, last, items 1 and 2 |
| Dict lookup with a default | `prices.get("pen", 0)` | the price, or 0 if missing |
| Loop over a dict | `for key, value in d.items():` | each pair in turn |
| `enumerate` | `for i, x in enumerate(items):` | position and item together |
| `zip` | `for name, score in zip(names, scores):` | pairs items from two lists |
| `sorted` with a key | `sorted(rows, key=lambda r: r["qty"], reverse=True)` | rows by quantity, biggest first |
| List comprehension | `[x * 2 for x in nums if x > 0]` | doubled positives |
| Dict comprehension | `{name: len(name) for name in names}` | name → length |
| `sum`, `min`, `max`, `len` | `sum(r["qty"] for r in rows)` | total quantity |
| Unpacking | `first, *rest = [1, 2, 3]` | `first = 1`, `rest = [2, 3]` |

**How a comprehension runs**, traced by hand for `[x * x for x in [3, -1, 4] if x > 0]`:

| `x` | `x > 0`? | Added to the result |
|---|---|---|
| 3 | yes | 9 |
| -1 | no | (skipped) |
| 4 | yes | 16 |

Result: `[9, 16]`. Read it as "**x times x**, **for** each x in the list, **if** x is positive".

**`collections.Counter` and `defaultdict`** (from Python's standard library) count and group without boilerplate: `Counter(cities)` counts each city; `defaultdict(list)` creates an empty list the first time you use a key. pandas does the same things on whole tables, but you'll still use these in quick scripts and interviews.

**When plain Python is enough:** a few thousand rows, a one-off script, or data that isn't a table (nested JSON from an API). **When it isn't:** maths over millions of numbers (Part 2, NumPy) and table operations like grouping and joining (Part 3 on, pandas). Plain-Python loops are roughly 10–100× slower for those.

**Common mistakes:**

- ❌ `d["missing"]` raises `KeyError`. ✅ `d.get("missing", default)` when a key might be absent.
- ❌ Changing a list while looping over it. ✅ Build a new list with a comprehension.
- ❌ A comprehension so long it needs a comment to explain. ✅ Use a normal loop; readability wins.
- ❌ Copying with `b = a` and being surprised that changing `b` changes `a` (both names point to the same list). ✅ `b = a.copy()` or `list(a)`.

**Used in real software:** API responses arrive as lists of dicts (JSON); configuration is a dict; every pandas DataFrame can be built from, and turned back into, a list of dicts (`pd.DataFrame(records)` and `df.to_dict("records")`).

### Python

```python
orders = [
    {"customer": "Asha", "city": "Pune", "qty": 5, "price": 60},
    {"customer": "Ravi", "city": "Mumbai", "qty": 1, "price": 2500},
    {"customer": "Asha", "city": "Pune", "qty": 1, "price": 1200},
    {"customer": "Zoya", "city": "Mumbai", "qty": 2, "price": 350},
]

revenues = [o["qty"] * o["price"] for o in orders]
print(revenues, sum(revenues))

big = [o["customer"] for o in orders if o["qty"] * o["price"] >= 1000]
print(big)

by_revenue = sorted(orders, key=lambda o: o["qty"] * o["price"], reverse=True)
print([o["customer"] for o in by_revenue])
```

**Output:**

```text
[300, 2500, 1200, 700] 4700
['Ravi', 'Asha']
['Ravi', 'Asha', 'Zoya', 'Asha']
```

```python
from collections import Counter, defaultdict

print(Counter(o["city"] for o in orders))          # how many orders per city

city_total = defaultdict(int)                      # missing keys start at 0
for o in orders:
    city_total[o["city"]] += o["qty"] * o["price"]
print(dict(city_total))

def average(values):
    """Return the mean of a list of numbers, or None for an empty list."""
    return sum(values) / len(values) if values else None

for city, total in city_total.items():
    n = sum(1 for o in orders if o["city"] == city)
    print(f"{city:<7} total {total:>5}  average order {average([o['qty'] * o['price'] for o in orders if o['city'] == city]):8.2f}  ({n} orders)")
```

**Output:**

```text
Counter({'Pune': 2, 'Mumbai': 2})
{'Pune': 1500, 'Mumbai': 3200}
Pune    total  1500  average order   750.00  (2 orders)
Mumbai  total  3200  average order  1600.00  (2 orders)
```

This "group by city and add up" is exactly what pandas does in one line in Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine). Seeing it by hand first makes that line easy to understand.

### Practice

1. Using `orders`, build a dict mapping each customer to the **number of items** (`qty`) they bought in total.
2. Build a list of `(customer, revenue)` tuples for orders from Mumbai only, sorted by revenue from smallest to largest.

<details>
<summary><b>Answer</b></summary>

```python
items = defaultdict(int)
for o in orders:
    items[o["customer"]] += o["qty"]
print(dict(items))

mumbai = sorted(((o["customer"], o["qty"] * o["price"]) for o in orders if o["city"] == "Mumbai"),
                key=lambda pair: pair[1])
print(mumbai)
```

**Output:**

```text
{'Asha': 6, 'Ravi': 1, 'Zoya': 2}
[('Zoya', 700), ('Ravi', 2500)]
```

</details>

**Learn more:** [Python tutorial: data structures](https://docs.python.org/3/tutorial/datastructures.html) · [Python docs: collections](https://docs.python.org/3/library/collections.html)

---

## 4. What Data Looks Like: Types of Data, Tables and Tidy Data

![Kinds of data: numerical (continuous or discrete) and categorical (nominal or ordinal), plus dates, text and booleans](images/data-science/04-data-types.svg)

### Theory

> **In simple words:** before you calculate anything, look at **what kind** of values each column holds. You can average temperatures but not postcodes; you can sort T-shirt sizes but not colours. The kind of data decides which summaries, charts and models make sense.

**Words to know:**

- **Observation (row, record, sample):** one thing you measured: one order, one patient, one day.
- **Variable (column, field, feature):** one property measured for every observation: price, city, date. (In statistics "variable" means a column, not a Python variable.)
- **Value:** one cell: the price of one order.
- **Numerical (quantitative) data:** numbers where maths makes sense.
  - **Continuous:** can take any value in a range (height 172.4 cm, temperature, price).
  - **Discrete:** countable whole numbers (number of children, items in a basket).
- **Categorical (qualitative) data:** labels that put observations into groups.
  - **Nominal:** groups with **no order** (city, colour, payment method).
  - **Ordinal:** groups **with an order** but no meaningful distance (S < M < L; "poor < fair < good"). The gap from S to M isn't "the same" as M to L.
- **Boolean (binary):** two values: yes/no, true/false, clicked/didn't.
- **Date / time (temporal):** a moment or a period; has order **and** distance (days between).
- **Text (unstructured):** free-form words: reviews, emails.
- **Identifier (ID):** a code that names something (order ID, phone number, postcode). Looks numeric, but **isn't a quantity**: averaging order IDs is meaningless.
- **Structured data:** data in rows and columns with fixed meanings. **Unstructured:** text, images, audio. **Semi-structured:** JSON and XML, which have labels but flexible nesting.
- **Schema:** the description of a table: each column's name and type.
- **Tidy data:** a table where **each variable is a column, each observation is a row, and each value is a single cell**.
- **Wide vs long format:** wide puts repeated measurements side by side as columns (`jan`, `feb`, `mar`); long stacks them as rows (`month`, `sales`). Tidy data is usually long.

**Everyday picture.** A school register is tidy: one row per student, one column per thing you know about them (name, class, height). A teacher's handwritten sheet with "Term 1 / Term 2 / Term 3" marks side by side is **wide**: easy to read, but awkward to ask "average mark per term".

**What you can do with each kind:**

| Kind | Example | Meaningful summary | Typical chart |
|---|---|---|---|
| Continuous | price, height | mean, median, spread | histogram, box plot |
| Discrete | items in basket | mean, median, counts per value | bar chart of counts |
| Nominal | city | counts, most common value (mode) | bar chart |
| Ordinal | size S/M/L, rating 1–5 | counts, median, mode | ordered bar chart |
| Boolean | clicked? | proportion that are true | bar chart, single number |
| Date / time | order date | min/max, counts per period, trends | line chart |
| Identifier | order ID | count of distinct values only | none |

**The three tidy-data rules,** with a common untidy layout and its fix:

| Untidy (wide): one row per store, months as columns | | | |
|---|---|---|---|
| **store** | **jan** | **feb** | **mar** |
| Pune | 120 | 135 | 150 |
| Delhi | 90 | 80 | 110 |

| Tidy (long): one row per store per month | | |
|---|---|---|
| **store** | **month** | **sales** |
| Pune | jan | 120 |
| Pune | feb | 135 |
| … | … | … |

In the tidy version, "month" is a real column, so "total sales per month" is one group-by, and adding April means adding rows, not changing the table's shape. Section [35](#35-reshaping-pivot_table-melt-crosstab-and-explode) converts between the two with `melt` and `pivot`.

**Other common untidy patterns:** two values in one cell (`"Pune, MH"`), one variable split across columns (`male_18_24`, `female_18_24`), and several kinds of observation in one table (customers and orders mixed together).

**When wide is fine:** a final report for humans, and the input to many ML models (one row per customer, one column per feature) is "wide" on purpose. Tidy is the best shape for **analysis**; reshape at the end for presentation.

**Common mistakes:**

- ❌ Averaging codes: a mean postcode or a mean customer ID. ✅ Treat IDs as text/categories.
- ❌ Storing ordinal labels as plain text, then sorting gives `L, M, S, XL` (alphabetical). ✅ Use an **ordered category** (Section [29](#29-categorical-data-and-binning-cut-and-qcut)).
- ❌ Encoding categories as numbers (1 = Pune, 2 = Delhi) and letting a model think Delhi is "twice" Pune. ✅ Keep them categorical; encode properly for ML (Section [61](#61-feature-engineering-preparing-data-for-machine-learning)).

**Used in real software:** database schemas, Parquet files and pandas all store a **type per column** for exactly these reasons; BI dashboards (Tableau, Power BI, Looker) ask whether each field is a "dimension" (categorical, for grouping) or a "measure" (numerical, for adding up).

### Python

Python can check the kind of each value for you. Here a small function classifies each column of a list of records:

```python
from datetime import date

rows = [
    {"order_id": 1001, "date": date(2025, 1, 5), "city": "Pune", "size": "M", "qty": 2, "price": 349.0, "gift": False},
    {"order_id": 1002, "date": date(2025, 1, 6), "city": "Delhi", "size": "L", "qty": 1, "price": 1299.5, "gift": True},
    {"order_id": 1003, "date": date(2025, 1, 6), "city": "Pune", "size": "S", "qty": 3, "price": 99.0, "gift": False},
]

def kind(column, values):
    if column.endswith("_id"):
        return "identifier"
    v = values[0]
    if isinstance(v, bool):              # check bool first: in Python, True is also an int
        return "boolean"
    if isinstance(v, date):
        return "date"
    if isinstance(v, int):
        return "numerical (discrete)"
    if isinstance(v, float):
        return "numerical (continuous)"
    return f"categorical ({len(set(values))} distinct values)"

for col in rows[0]:
    print(f"{col:<9} {kind(col, [r[col] for r in rows])}")
```

**Output:**

```text
order_id  identifier
date      date
city      categorical (2 distinct values)
size      categorical (3 distinct values)
qty       numerical (discrete)
price     numerical (continuous)
gift      boolean
```

Notice `size` is reported as plain categorical; only **you** know it's ordinal (S < M < L). Data never tells you its meaning: you have to bring that knowledge.

Turning wide data into tidy data by hand shows what `melt` (Section [35](#35-reshaping-pivot_table-melt-crosstab-and-explode)) will do for you:

```python
wide = {"Pune": {"jan": 120, "feb": 135, "mar": 150},
        "Delhi": {"jan": 90, "feb": 80, "mar": 110}}

tidy = [{"store": store, "month": month, "sales": sales}
        for store, months in wide.items()
        for month, sales in months.items()]
for row in tidy:
    print(row)

per_month = {}
for row in tidy:
    per_month[row["month"]] = per_month.get(row["month"], 0) + row["sales"]
print(per_month)
```

**Output:**

```text
{'store': 'Pune', 'month': 'jan', 'sales': 120}
{'store': 'Pune', 'month': 'feb', 'sales': 135}
{'store': 'Pune', 'month': 'mar', 'sales': 150}
{'store': 'Delhi', 'month': 'jan', 'sales': 90}
{'store': 'Delhi', 'month': 'feb', 'sales': 80}
{'store': 'Delhi', 'month': 'mar', 'sales': 110}
{'jan': 210, 'feb': 215, 'mar': 260}
```

### Practice

1. For each column, say its kind: `customer_email`, `age`, `star_rating (1–5)`, `delivery_minutes`, `is_member`, `signup_date`, `country`, `phone_number`.
2. A table has columns `student, maths_2024, maths_2025, physics_2024, physics_2025`. What are the variables really, and what would the tidy columns be?

<details>
<summary><b>Answer</b></summary>

1. `customer_email`: identifier (text) · `age`: numerical, discrete if whole years (continuous in principle) · `star_rating`: ordinal categorical · `delivery_minutes`: numerical continuous · `is_member`: boolean · `signup_date`: date · `country`: nominal categorical · `phone_number`: identifier (never do maths on it, and store it as text so leading zeros and `+` survive).
2. The column names hide two variables, **subject** and **year**. Tidy columns: `student, subject, year, mark`, one row per student per subject per year.

</details>

**Learn more:** [Hadley Wickham: Tidy Data (the original paper, very readable)](https://vita.had.co.nz/papers/tidy-data.pdf) · [Khan Academy: types of statistical data](https://www.khanacademy.org/math/statistics-probability/analyzing-categorical-data)

---

## 5. Reading Files with Plain Python: Text, CSV and JSON

![A CSV file is lines of text; the csv module splits each line on commas into a dict keyed by the header](images/data-science/05-csv-to-records.svg)

### Theory

> **In simple words:** most data arrives as a **file**. A CSV file is just text: one line per row, values separated by commas. JSON is text too, shaped like Python dicts and lists. Loading them by hand once shows you what pandas automates, and why it saves so much work.

**Words to know:**

- **File path:** where a file lives, like `data/orders.csv` (relative to the current folder) or `/Users/asha/data/orders.csv` (absolute).
- **CSV (comma-separated values):** a text file where each line is a row and commas separate the values. The first line is usually the **header** (the column names).
- **Delimiter (separator):** the character between values: comma, semicolon (common in Europe), or tab (a **TSV** file).
- **Quoting:** a value containing the delimiter is wrapped in quotes: `"Pune, MH"`.
- **Encoding:** how characters are stored as bytes. **UTF-8** handles every language and is the standard; old Excel files may use `cp1252` or `latin-1`.
- **JSON (JavaScript Object Notation):** text with `{"key": value}` objects and `[...]` arrays, the standard format of web APIs. It maps directly onto Python dicts and lists.
- **Parsing:** turning text into structured values (the text `"60"` into the number `60`).
- **Context manager (`with`):** `with open(path) as f:` opens a file and **guarantees it is closed** afterwards, even if an error happens.
- **Serialisation:** turning in-memory objects into text or bytes to save or send (`json.dumps`); the reverse is **deserialisation** (`json.loads`).

**Everyday picture.** A CSV file is a table typed on a typewriter with commas between the columns. A program reading it has to split each line at the commas, remember which column is which from the first line, and work out that `"60"` is a number, which is easy until someone types a comma inside a city name.

**How reading a CSV works, step by step:**

1. Open the file as text with the right encoding.
2. Read the first line and split it into column names.
3. For every other line, split on the delimiter (respecting quotes) and pair each value with its column name.
4. Convert each value from text to the right type (number, date, boolean).
5. Decide what to do with empty values.

Python's built-in `csv` module does steps 2–3, including quotes. **It does not do step 4**: every value comes back as a string. That's the first thing pandas does for you (Section [19](#19-reading-and-writing-files-csv-excel-json-and-parquet)), along with steps 1 and 5.

**Traced by hand** for the line `3,"Pune, MH",1200` under the header `order_id,city,price`:

| Step | Result |
|---|---|
| Split, respecting quotes | `["3", "Pune, MH", "1200"]` |
| Pair with the header | `{"order_id": "3", "city": "Pune, MH", "price": "1200"}` |
| Convert types (your job with `csv`) | `{"order_id": 3, "city": "Pune, MH", "price": 1200.0}` |

A naive `line.split(",")` would give **four** pieces here, splitting the city in two: that's why you use the `csv` module, never `split`.

**When plain Python is the right tool:** reading a config file, a small JSON response, or a file too irregular for a table. **When it isn't:** anything you'll filter, group, join or chart. Use pandas.

**Common mistakes:**

- ❌ `line.split(",")` on CSV data (breaks on quoted commas). ✅ The `csv` module or pandas.
- ❌ Forgetting that every CSV value is a string: `"10" > "9"` is `False` (text compares character by character). ✅ Convert types right after reading.
- ❌ Opening files without `encoding="utf-8"` and getting garbled names on another computer. ✅ Always pass the encoding.
- ❌ `open()` without `with`, leaving files open. ✅ `with open(...) as f:`.

**Used in real software:** CSV is the universal export format (banks, spreadsheets, government open data); JSON is how almost every web API sends data, and how many log systems store events (one JSON object per line, called **JSON Lines**).

### Python

To keep every example self-contained, these notes create small files in a temporary folder first. With real data, you'd skip that and open your own file.

```python
import csv, json, os, tempfile

folder = tempfile.mkdtemp()                       # a fresh temporary folder
path = os.path.join(folder, "orders.csv")
with open(path, "w", encoding="utf-8") as f:
    f.write('order_id,city,product,qty,price\n'
            '1,Pune,Notebook,5,60\n'
            '2,Mumbai,Headphones,1,2500\n'
            '3,"Pune, MH",Backpack,1,1200\n')

with open(path, encoding="utf-8") as f:
    rows = list(csv.DictReader(f))                # header → keys, one dict per line
print(rows[2])
print(type(rows[0]["qty"]), "10" > "9")           # everything is text!

for r in rows:                                    # step 4: convert types yourself
    r["order_id"], r["qty"], r["price"] = int(r["order_id"]), int(r["qty"]), float(r["price"])
print(sum(r["qty"] * r["price"] for r in rows))
```

**Output:**

```text
{'order_id': '3', 'city': 'Pune, MH', 'product': 'Backpack', 'qty': '1', 'price': '1200'}
<class 'str'> False
4000.0
```

```python
api_text = '{"store": "Pune", "open": true, "orders": [{"id": 1, "total": 300}, {"id": 2, "total": null}]}'
data = json.loads(api_text)                       # JSON text → Python dicts and lists
print(data["orders"][0], data["open"], data["orders"][1]["total"])

totals = [o["total"] for o in data["orders"] if o["total"] is not None]
print(totals)

out_path = os.path.join(folder, "summary.json")
with open(out_path, "w", encoding="utf-8") as f:
    json.dump({"store": data["store"], "known_total": sum(totals)}, f, indent=2)
print(open(out_path, encoding="utf-8").read())
```

**Output:**

```text
{'id': 1, 'total': 300} True None
[300]
{
  "store": "Pune",
  "known_total": 300
}
```

JSON's `true`, `false` and `null` become Python's `True`, `False` and `None`. A missing value (`null`/`None`) has to be handled before you add things up, a problem pandas handles with `NaN` (Section [26](#26-missing-values-finding-dropping-and-filling)).

### Practice

1. Write a CSV with the header `name,score` and three rows (one score left empty). Read it with `csv.DictReader` and print the average of the scores that are present.
2. Given `'[{"city": "Pune", "temp": 31.5}, {"city": "Delhi", "temp": 38.0}]'`, load it and print the hottest city.

<details>
<summary><b>Answer</b></summary>

```python
p = os.path.join(folder, "scores.csv")
with open(p, "w", encoding="utf-8") as f:
    f.write("name,score\nAsha,82\nRavi,\nZoya,91\n")
with open(p, encoding="utf-8") as f:
    scores = [float(r["score"]) for r in csv.DictReader(f) if r["score"] != ""]
print(sum(scores) / len(scores))

cities = json.loads('[{"city": "Pune", "temp": 31.5}, {"city": "Delhi", "temp": 38.0}]')
print(max(cities, key=lambda c: c["temp"])["city"])
```

**Output:**

```text
86.5
Delhi
```

</details>

**Learn more:** [Python docs: csv](https://docs.python.org/3/library/csv.html) · [Python docs: json](https://docs.python.org/3/library/json.html) · [JSON Lines format](https://jsonlines.org/)

---

### ✅ Part 1 checkpoint

Without looking, can you:

- [ ] List the six steps of the data workflow and say which one usually takes longest?
- [ ] Create a virtual environment (or open Colab), start a notebook, and explain what the kernel remembers?
- [ ] Write a list comprehension with a filter, sort a list of dicts by a key, and count with `Counter`?
- [ ] Classify a column as continuous, discrete, nominal, ordinal, boolean, date, text or identifier?
- [ ] State the three tidy-data rules and turn a wide table into a long one?
- [ ] Read a CSV with the `csv` module and explain why every value comes back as a string?

Plain Python handled 4 rows easily. Part 2 introduces **NumPy**, which does the same maths on millions of numbers at once.

---

# Part 2 — Basic: NumPy, Fast Arrays of Numbers

> **Goal:** Create, select, calculate with, summarise and reshape NumPy arrays, generate random data, and do the linear algebra that machine learning is built on. NumPy is the foundation under pandas, scikit-learn and PyTorch.  
> **You need:** Part 1.

---

## 6. Why NumPy? Arrays vs Lists, and How Arrays Sit in Memory

![A Python list holds pointers to separate objects; a NumPy array holds raw numbers side by side in one block](images/data-science/01-ndarray.svg)

### Theory

> **In simple words:** a NumPy **array** is like a Python list of numbers, but **every number has the same type and they sit side by side in one block of memory**. That lets NumPy run maths on millions of numbers in fast compiled code, written as one line, with no Python loop.

**Words to know:**

- **NumPy (Numerical Python):** the library for fast arrays of numbers. Imported as `np`.
- **Array (ndarray, "n-dimensional array"):** NumPy's container: a grid of values that all have the **same type**.
- **Element:** one value inside an array.
- **Memory:** where a running program keeps its data (RAM). A **contiguous block** means the values are stored one after another with no gaps.
- **Pointer (reference):** an address that says where some other object lives in memory.
- **Compiled code (C):** code translated ahead of time into machine instructions. It runs far faster than Python, which is **interpreted** (read and executed line by line, checking types on every step).
- **Vectorisation:** writing an operation on a whole array (`a * 2`) so NumPy loops in compiled code instead of you looping in Python.
- **Overhead:** extra work that isn't the actual calculation, like Python checking the type of every number in a loop.
- **CPU / GPU:** the computer's main processor / a graphics processor with thousands of small cores, which does the same arithmetic on many numbers at once (ideal for deep learning).
- **SIMD (single instruction, multiple data):** CPU instructions that apply one operation to several numbers in a single step.
- **Unicode:** the standard numbering of every character in every language (UTF-8 is a way to store it as bytes).

**Everyday picture.** A Python list is a row of **lockers holding claim tickets**: each ticket tells you which warehouse shelf the real item is on, and every item comes with its own label saying what it is. A NumPy array is an **egg carton**: the eggs themselves sit side by side, all the same kind, so you can process the whole carton in one go.

**Why that makes arrays fast, step by step** (computing `x * 2` for a million numbers):

| | Python list + loop | NumPy array |
|---|---|---|
| Where the numbers are | Scattered objects, each with a type label and reference count | One contiguous block of raw 8-byte numbers |
| Per element, the program must | Follow the pointer, check the type, look up `*` for that type, create a new number object | Multiply two raw numbers |
| Who runs the loop | The Python interpreter (slow) | Compiled C code (fast), often using the CPU's **SIMD** instructions, which multiply several numbers in one step |
| Memory for 1 million integers | About 36 MB (8-byte pointer + 28-byte object each) | 8 MB |
| Typical speed | 1× | 10–100× faster |

**The trade-off:** every element must have the same type, and the size is fixed when the array is created. Adding one element means making a new, bigger array. Lists are better for collections that grow one item at a time or mix types; arrays are better for maths.

**When to use NumPy:** any maths on many numbers: statistics, images (an image *is* an array of pixel numbers), simulations, the inputs and weights of ML models. **When not to:** a handful of values, mixed types (use a dict, or a pandas DataFrame, which is built on NumPy arrays, one per column), or a collection you grow item by item.

**Common mistakes:**

- ❌ Writing a Python `for` loop over an array's elements. ✅ Use a vectorised expression; the rest of Part 2 shows how.
- ❌ Growing an array in a loop with `np.append` (it copies the whole array every time: slow, O(n²) in total). ✅ Collect values in a list and convert once with `np.array(lst)`, or create `np.zeros(n)` first and fill it.
- ❌ Timing tiny arrays and concluding NumPy is slow. ✅ For 5 numbers the call overhead dominates; NumPy wins as sizes grow.

**Used in real software:** pandas stores each column as a NumPy array; scikit-learn models take arrays as input; images in OpenCV and Pillow convert to arrays; PyTorch tensors are NumPy-like arrays that can also live on a GPU.

### Python

```python
import sys, time
import numpy as np

nums = list(range(1_000_000))
arr = np.arange(1_000_000)                     # the same numbers as an array

list_bytes = sys.getsizeof(nums) + sum(sys.getsizeof(x) for x in nums)
print(f"list  ≈ {list_bytes / 1e6:.0f} MB")
print(f"array = {arr.nbytes / 1e6:.0f} MB, each element {arr.itemsize} bytes, dtype {arr.dtype}")

t0 = time.perf_counter(); doubled_list = [x * 2 for x in nums]; t1 = time.perf_counter()
doubled_arr = arr * 2;                                            t2 = time.perf_counter()
print("same answer:", doubled_list[-1] == doubled_arr[-1])
print(f"NumPy was about {(t1 - t0) / (t2 - t1):.0f}× faster")
```

**Output:**

```text
list  ≈ 36 MB
array = 8 MB, each element 8 bytes, dtype int64
same answer: True
NumPy was about 6× faster
```

The exact speed-up depends on your computer; the size difference doesn't. (`sys.getsizeof` reports the bytes one Python object uses; `nbytes` is the size of an array's data block.)

```python
small = np.array([3, 1, 4])
print(type(small), small * 2, small + small, small ** 2)
print([3, 1, 4] * 2)                             # a LIST repeats instead!
```

**Output:**

```text
<class 'numpy.ndarray'> [6 2 8] [6 2 8] [ 9  1 16]
[3, 1, 4, 3, 1, 4]
```

The last line is the most important lesson of this section: `*` means "repeat" for lists but "multiply every element" for arrays.

### Practice

1. Create an array of the numbers 0 to 9 and print each one multiplied by 10, without a loop.
2. Why can't an array hold `[1, "two", 3.0]` as numbers? What do you think `np.array([1, "two", 3.0])` produces? Run it to check.

<details>
<summary><b>Answer</b></summary>

```python
print(np.arange(10) * 10)
mixed = np.array([1, "two", 3.0])
print(mixed, mixed.dtype)
```

**Output:**

```text
[ 0 10 20 30 40 50 60 70 80 90]
['1' 'two' '3.0'] <U32
```

All elements of an array share one type, so NumPy picks a type that fits everything: here a string type (`<U21` means "Unicode text up to 21 characters"). The numbers became text and you can no longer do maths with them.

</details>

**Learn more:** [NumPy: the absolute basics for beginners](https://numpy.org/doc/stable/user/absolute_beginners.html) · [Jake VanderPlas: why Python is slow (and how NumPy helps)](https://jakevdp.github.io/PythonDataScienceHandbook/02.01-understanding-data-types.html)

---

## 7. Creating Arrays: array, arange, linspace, zeros, ones and full

![arange steps by a fixed size and stops before the end; linspace places a fixed number of points including both ends](images/data-science/07-arange-linspace.svg)

### Theory

> **In simple words:** you make arrays from lists you already have (`np.array`), from number ranges (`np.arange`, `np.linspace`), or pre-filled with a constant (`np.zeros`, `np.ones`, `np.full`) when you'll fill them in later.

**Words to know:**

- **Range:** a sequence of numbers from a start up to (but usually not including) a stop, moving by a **step**.
- **Evenly spaced:** neighbouring values are the same distance apart.
- **Identity matrix:** a square grid with 1s on the diagonal (top-left to bottom-right) and 0s elsewhere. Multiplying by it changes nothing, like multiplying a number by 1.
- **Pre-allocate:** create an array of the final size first, then fill it.
- **Floating-point (float):** a number with a fractional part, stored approximately in binary. `0.1 + 0.2` is `0.30000000000000004`, because 0.1 can't be stored exactly.

**Everyday picture.** `arange` is walking along a road placing a cone every 2 metres until you reach the 10 m mark (no cone *at* 10). `linspace` is "put exactly 5 cones from the start line to the finish line, evenly", so the end gets a cone and the spacing is worked out for you.

**The creation functions:**

| Code | Makes | Result |
|---|---|---|
| `np.array([1, 2, 3])` | From a list; a list of lists makes a 2D array | `[1 2 3]` |
| `np.arange(5)` | 0 up to 5, **not including** 5 | `[0 1 2 3 4]` |
| `np.arange(2, 11, 3)` | start 2, stop 11, step 3 | `[2 5 8]` |
| `np.linspace(0, 1, 5)` | 5 points from 0 to 1, **including** 1 | `[0. 0.25 0.5 0.75 1.]` |
| `np.zeros(3)`, `np.zeros((2, 3))` | Filled with 0.0 (a shape is a tuple) | 3 zeros; 2 × 3 zeros |
| `np.ones((2, 2))` | Filled with 1.0 | 2 × 2 ones |
| `np.full((2, 3), 7)` | Filled with any value | 2 × 3 sevens |
| `np.eye(3)` | 3 × 3 identity matrix | 1s on the diagonal |
| `np.zeros_like(a)`, `np.ones_like(a)` | Same shape and type as `a` | |
| `np.empty(n)` | Uninitialised (whatever bytes were in memory): fast, but you **must** overwrite every value | |

**How `linspace` works out its spacing:** step = (stop − start) / (num − 1). For `np.linspace(0, 1, 5)`: (1 − 0) / 4 = 0.25, so 0, 0.25, 0.5, 0.75, 1.

**`arange` vs `linspace` for decimals.** `np.arange(0, 1, 0.1)` steps by a float that can't be stored exactly, so whether the last value sneaks in can surprise you. When you know **how many** points you want (very common for charts), use `linspace`. Use `arange` for whole-number steps.

**When to use which:** `array` for data you already have; `arange` for indices and integer sequences; `linspace` for smooth x-values (plotting a curve) and grids; `zeros`/`full` when you'll fill values in a loop or by index.

**Common mistakes:**

- ❌ `np.zeros(2, 3)`: the second argument is the **type**, not a size, so this raises an error. ✅ `np.zeros((2, 3))`, shape as one tuple.
- ❌ `np.array([[1, 2], [3]])`: rows of different lengths can't form a grid, so NumPy raises an error. ✅ Make every row the same length (or fill gaps with `np.nan`).
- ❌ Forgetting that `arange` excludes the stop value, just like Python's `range`.

**Used in real software:** `linspace` builds the x-axis of every smooth curve you'll plot; `zeros` pre-allocates result arrays in simulations; `eye` appears in linear algebra and in "one-hot" encodings for ML (Section [61](#61-feature-engineering-preparing-data-for-machine-learning)).

### Python

```python
import numpy as np

print(np.array([[1, 2, 3], [4, 5, 6]]))
print(np.arange(5), np.arange(2, 11, 3), np.arange(10, 0, -3))
print(np.linspace(0, 1, 5))
print(np.linspace(0, 10, 4))          # step = (10 - 0) / 3
print(np.zeros((2, 3)))
print(np.full((2, 3), 7), np.eye(3), sep="\n")
```

**Output:**

```text
[[1 2 3]
 [4 5 6]]
[0 1 2 3 4] [2 5 8] [10  7  4  1]
[0.   0.25 0.5  0.75 1.  ]
[ 0.          3.33333333  6.66666667 10.        ]
[[0. 0. 0.]
 [0. 0. 0.]]
[[7 7 7]
 [7 7 7]]
[[1. 0. 0.]
 [0. 1. 0.]
 [0. 0. 1.]]
```

```python
print(np.arange(0, 1, 0.1))           # floats: 10 values, stop excluded
print(0.1 + 0.2, 0.1 + 0.2 == 0.3)    # why float steps are risky
print(np.isclose(0.1 + 0.2, 0.3))     # compare floats with a tolerance instead

squares = np.zeros(5, dtype=int)      # pre-allocate, then fill
for i in range(5):
    squares[i] = i * i
print(squares, np.arange(5) ** 2)     # ...though the vectorised line is better
```

**Output:**

```text
[0.  0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9]
0.30000000000000004 False
True
[ 0  1  4  9 16] [ 0  1  4  9 16]
```

`np.isclose(a, b)` checks whether two floats are equal **within a tiny tolerance**: the right way to compare decimals.

### Practice

1. Create the even numbers from 10 to 30 inclusive.
2. Create 7 evenly spaced numbers from −3 to 3, and a 3 × 3 array of `-1`s.
3. What does `np.arange(1, 2, 0.25)` return? Work it out by hand, then run it.

<details>
<summary><b>Answer</b></summary>

```python
print(np.arange(10, 31, 2))
print(np.linspace(-3, 3, 7), np.full((3, 3), -1), sep="\n")
print(np.arange(1, 2, 0.25))
```

**Output:**

```text
[10 12 14 16 18 20 22 24 26 28 30]
[-3. -2. -1.  0.  1.  2.  3.]
[[-1 -1 -1]
 [-1 -1 -1]
 [-1 -1 -1]]
[1.   1.25 1.5  1.75]
```

`0.25` is stored exactly in binary, so here `arange` behaves: 1, 1.25, 1.5, 1.75 (2 is excluded).

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [35. Convert Vector to Diagonal Matrix](https://www.deep-ml.com/problems/35) | 🟢 Easy |

**Learn more:** [NumPy: array creation](https://numpy.org/doc/stable/user/basics.creation.html)

---

## 8. Shape, Dimensions and dtypes

![An array's shape gives its size along each axis; axis 0 runs down the rows, axis 1 across the columns](images/data-science/08-shape-axes.svg)

### Theory

> **In simple words:** every array knows its **shape** (how many items along each direction), its number of **dimensions**, and its **dtype** (the one type all its elements share). Checking `.shape` and `.dtype` is the first thing to do whenever an array surprises you.

**Words to know:**

- **Dimension / axis:** a direction you can move along. A list of numbers has 1 axis; a table has 2 (rows and columns); a colour image has 3 (height, width, colour channel).
- **Shape:** a tuple with the size along each axis: `(3, 4)` means 3 rows and 4 columns.
- **Scalar:** a single number (0 dimensions). **Vector:** 1 dimension. **Matrix:** 2 dimensions. **Tensor:** the general word for any number of dimensions (used by PyTorch and TensorFlow).
- **dtype (data type):** the element type: `int64` (whole numbers using 64 bits = 8 bytes), `float64`, `float32`, `bool`, `uint8` (unsigned 8-bit: 0–255) and so on.
- **Bit / byte:** a bit is a single 0 or 1; a byte is 8 bits.
- **Precision:** how many digits a number type keeps. `float64` keeps about 15–16 significant digits; `float32` about 7.
- **Overflow:** when a result is too big for its type and wraps around to a wrong value (an `int8` can hold only −128 to 127).
- **Upcasting:** NumPy converting to a more general type so every element fits (mixing ints and floats gives floats).
- **Casting:** converting an array to another type with `astype`.

**Everyday picture.** The shape is the size printed on a box of chocolates: "3 rows × 4 columns". The dtype is the rule "every chocolate in this box is the same size": you can't drop a watermelon into one slot.

**Attributes of an array `a`:**

| Attribute | Meaning | For a 3 × 4 int64 array |
|---|---|---|
| `a.ndim` | Number of axes | `2` |
| `a.shape` | Size along each axis | `(3, 4)` |
| `a.size` | Total number of elements (product of the shape) | `12` |
| `a.dtype` | The element type | `int64` |
| `a.itemsize` | Bytes per element | `8` |
| `a.nbytes` | Total bytes = size × itemsize | `96` |

**Common dtypes and their ranges:**

| dtype | Holds | Bytes | Typical use |
|---|---|---|---|
| `bool` | `True` / `False` | 1 | masks (Section [10](#10-boolean-masks-fancy-indexing-and-npwhere)) |
| `int8` / `uint8` | −128…127 / 0…255 | 1 | image pixels (`uint8`) |
| `int32` / `int64` | about ±2.1 billion / ±9.2 × 10¹⁸ | 4 / 8 | counts, IDs; `int64` is the default |
| `float32` | ~7 significant digits | 4 | deep learning (half the memory) |
| `float64` | ~15 significant digits | 8 | the default for decimals |
| `<U10` | text up to 10 characters | 40 | avoid for data: pandas handles text better |

**Upcasting, traced:** `np.array([1, 2, 3.5])`: the elements are int, int, float. One type must fit all, so NumPy picks `float64` and stores `1.0, 2.0, 3.5`. Adding a bool to an int array gives int; adding a string makes everything text.

**Casting with `astype`:** `a.astype(np.float32)` makes a converted **copy**. Float → int **truncates** (chops off the decimals, towards zero): `2.9 → 2`, `-2.9 → -2`. Round first (`np.round`) if you mean rounding.

**When to care about dtypes:** memory (a 1-billion-element `float64` array is 8 GB; `float32` halves it), speed (smaller types move through memory faster), and correctness (overflow in small integer types, precision loss in `float32` money sums). **Rule of thumb:** keep the defaults (`int64`, `float64`) until memory matters.

**Common mistakes:**

- ❌ Storing pixel maths in `uint8`: `200 + 100` wraps around to `44`. ✅ Convert to a bigger type first: `img.astype(np.int16)`.
- ❌ Using `float32` for money or anything needing many digits. ✅ `float64`, or whole numbers of the smallest unit (paise, cents) as integers.
- ❌ Confusing `a.size` (elements) with `len(a)` (the length of the **first** axis only: 3 for a 3 × 4 array).

**Used in real software:** image libraries load photos as `uint8` arrays of shape `(height, width, 3)`; deep-learning frameworks default to `float32` (or the even smaller `float16`/`bfloat16` on GPUs) to fit bigger models; pandas chooses a dtype per column on load (Section [27](#27-duplicates-data-types-and-type-conversion)).

### Python

```python
import numpy as np

m = np.arange(12).reshape(3, 4)        # 12 numbers arranged as 3 rows × 4 columns
print(m)
print("ndim", m.ndim, "| shape", m.shape, "| size", m.size, "| len", len(m))
print("dtype", m.dtype, "| itemsize", m.itemsize, "| nbytes", m.nbytes)

image = np.zeros((480, 640, 3), dtype=np.uint8)   # a black 640 × 480 colour image
print(image.ndim, image.shape, f"{image.nbytes / 1e6:.2f} MB")
print(np.float64(3.5).ndim, np.array(3.5).shape)  # a scalar: 0 dimensions, shape ()
```

**Output:**

```text
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
ndim 2 | shape (3, 4) | size 12 | len 3
dtype int64 | itemsize 8 | nbytes 96
3 (480, 640, 3) 0.92 MB
0 ()
```

(`reshape` rearranges numbers into a new shape; Section [14](#14-reshaping-stacking-splitting-and-sorting) covers it fully.)

```python
print(np.array([1, 2, 3.5]).dtype, np.array([True, 2]).dtype, np.array([1, "a"]).dtype)

prices = np.array([2.9, -2.9, 7.5])
print(prices.astype(int), np.round(prices).astype(int))   # truncate vs round first

pixels = np.array([200, 250], dtype=np.uint8)
print(pixels + np.uint8(100))                              # wraps around: overflow!
print(pixels.astype(np.int16) + 100)                       # safe in a bigger type

print(np.iinfo(np.int8).min, np.iinfo(np.int8).max, np.iinfo(np.int64).max)
print(np.finfo(np.float32).precision, np.finfo(np.float64).precision)   # about how many decimal digits each keeps
```

**Output:**

```text
float64 int64 <U21
[ 2 -2  7] [ 3 -3  8]
[44 94]
[300 350]
-128 127 9223372036854775807
6 15
```

`np.iinfo` and `np.finfo` tell you the limits of an integer or float type. `np.round` rounds halves to the nearest **even** number (7.5 → 8, but 6.5 → 6), a rule called **banker's rounding** that avoids bias when you round many values.

### Practice

1. Create a 4 × 5 array of ones. Print its shape, size and total bytes. Then convert it to `float32` and print the bytes again.
2. Predict the dtype of `np.array([1, 2]) / 2` and of `np.array([1, 2]) // 2`, then check.

<details>
<summary><b>Answer</b></summary>

```python
ones = np.ones((4, 5))
print(ones.shape, ones.size, ones.nbytes, ones.astype(np.float32).nbytes)
print((np.array([1, 2]) / 2).dtype, (np.array([1, 2]) // 2).dtype)
```

**Output:**

```text
(4, 5) 20 160 80
float64 int64
```

`/` is true division, which always gives floats; `//` is floor division, which keeps integers.

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [3. Reshape Matrix](https://www.deep-ml.com/problems/3) | 🟢 Easy |
| 2 | [2. Transpose of a Matrix](https://www.deep-ml.com/problems/2) | 🟢 Easy |

**Learn more:** [NumPy: data types](https://numpy.org/doc/stable/user/basics.types.html) · [What every programmer should know about floating point](https://floating-point-gui.de/)

---

## 9. Indexing and Slicing (1D and 2D), Views vs Copies

![Indexing a 2D array: one position per axis; slices pick ranges of rows and columns](images/data-science/09-slicing.svg)

### Theory

> **In simple words:** you pick parts of an array like a list (`a[2]`, `a[1:4]`), but with **one position per axis** separated by commas: `m[row, col]`. Slices don't copy the data: they're **windows** onto the original, so changing a slice changes the original too.

**Words to know:**

- **Index:** a position number, starting at 0. Negative indices count from the end: `-1` is the last element.
- **Slice:** a range of positions written `start:stop:step`. `stop` is **excluded**. Leave a part out to mean "from the beginning", "to the end" or "step 1".
- **`:` on its own:** "everything along this axis".
- **View:** a new array object that **shares memory** with the original. Changing one changes the other.
- **Copy:** a new array with its **own** memory. Independent of the original.

**Everyday picture.** A slice is a **window cut in a cardboard mask** laid over a spreadsheet: you see only part of the sheet, but if you write through the window, you're writing on the sheet itself. `.copy()` is photocopying that part, so your scribbles stay on the photocopy.

**Indexing patterns,** using `m = np.arange(1, 13).reshape(3, 4)`:

```text
m = [[ 1  2  3  4]      row 0
     [ 5  6  7  8]      row 1
     [ 9 10 11 12]]     row 2
      col 0 1 2 3
```

| Code | Means | Result |
|---|---|---|
| `m[1, 2]` | row 1, column 2 | `7` |
| `m[-1, -1]` | last row, last column | `12` |
| `m[0]` or `m[0, :]` | the whole of row 0 | `[1 2 3 4]` |
| `m[:, 1]` | every row, column 1 | `[ 2  6 10]` |
| `m[:2, 1:3]` | rows 0–1, columns 1–2 | `[[2 3] [6 7]]` |
| `m[::2]` | every 2nd row | rows 0 and 2 |
| `m[:, ::-1]` | every row, columns reversed | each row backwards |

**Tracing `m[:2, 1:3]` by hand:** rows `:2` means rows 0 and 1 (stop 2 excluded); columns `1:3` means columns 1 and 2. Row 0 gives `2, 3`; row 1 gives `6, 7`. Result shape `(2, 2)`.

**Getting a row vs a one-row matrix:** `m[0]` has shape `(4,)` (1D); `m[0:1]` has shape `(1, 4)` (still 2D). An integer index **removes** that axis; a slice **keeps** it.

**Views vs copies:**

| Operation | Returns | Shares memory? |
|---|---|---|
| Basic slicing `a[1:4]`, `m[:, 0]` | view | ✅ yes |
| `a.reshape(...)`, `a.T` (usually) | view | ✅ yes |
| Boolean or list indexing `a[a > 0]`, `a[[0, 2]]` (Section [10](#10-boolean-masks-fancy-indexing-and-npwhere)) | copy | ❌ no |
| `a.copy()` | copy | ❌ no |

`np.shares_memory(a, b)` tells you for sure. Views make slicing instant even on huge arrays, which is why NumPy does it.

**When to `.copy()`:** whenever you take a slice and plan to modify it **without** affecting the original, or keep a small piece of a huge array (a view keeps the whole big array alive in memory).

**Common mistakes:**

- ❌ Modifying a slice and being surprised the original changed. ✅ `.copy()` first.
- ❌ `m[0][1]` instead of `m[0, 1]`. It works, but first builds a temporary row; with slices (`m[:, 0][1:]` vs `m[1:, 0]`) the two styles can differ.
- ❌ Off-by-one: `a[1:3]` has **2** elements (positions 1 and 2).

**Used in real software:** cropping an image is a slice (`img[100:300, 50:250]`); selecting a feature column for a model is `X[:, j]`; splitting time-ordered data into train and test sets is a slice (`data[:800]`, `data[800:]`).

### Python

```python
import numpy as np

m = np.arange(1, 13).reshape(3, 4)
print(m[1, 2], m[-1, -1])
print(m[0], m[:, 1], m[:2, 1:3], sep="\n")
print(m[0].shape, m[0:1].shape)                    # integer drops an axis; slice keeps it
print(m[::2], m[:, ::-1], sep="\n")
```

**Output:**

```text
7 12
[1 2 3 4]
[ 2  6 10]
[[2 3]
 [6 7]]
(4,) (1, 4)
[[ 1  2  3  4]
 [ 9 10 11 12]]
[[ 4  3  2  1]
 [ 8  7  6  5]
 [12 11 10  9]]
```

```python
scores = np.array([45, 82, 67, 91, 38, 74])
window = scores[:3]                    # a VIEW
window[0] = 100
print(scores, np.shares_memory(scores, window))

safe = scores[:3].copy()               # a COPY
safe[0] = -1
print(scores[0], safe[0], np.shares_memory(scores, safe))

img = np.arange(36).reshape(6, 6)      # pretend this is an image
crop = img[1:4, 2:5]                   # rows 1-3, columns 2-4
print(crop)
```

**Output:**

```text
[100  82  67  91  38  74] True
100 -1 False
[[ 8  9 10]
 [14 15 16]
 [20 21 22]]
```

### Practice

1. From `m = np.arange(1, 13).reshape(3, 4)`, take: the last column, the bottom-right 2 × 2 block, and the middle row reversed.
2. Without running it, what does `np.arange(10)[2:8:3]` give? Then check.

<details>
<summary><b>Answer</b></summary>

```python
print(m[:, -1], m[-2:, -2:], m[1, ::-1], sep="\n")
print(np.arange(10)[2:8:3])
```

**Output:**

```text
[ 4  8 12]
[[ 7  8]
 [11 12]]
[8 7 6 5]
[2 5]
```

`2:8:3` starts at 2, steps by 3 (2, 5) and stops before 8.

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [2. Transpose of a Matrix](https://www.deep-ml.com/problems/2) | 🟢 Easy |
| 2 | [5. Scalar Multiplication of a Matrix](https://www.deep-ml.com/problems/5) | 🟢 Easy |

**Learn more:** [NumPy: indexing on ndarrays](https://numpy.org/doc/stable/user/basics.indexing.html) · [NumPy: copies and views](https://numpy.org/doc/stable/user/basics.copies.html)

---

## 10. Boolean Masks, Fancy Indexing and np.where

![A condition makes a mask of True/False; indexing with the mask keeps only the True positions](images/data-science/10-boolean-mask.svg)

### Theory

> **In simple words:** a comparison like `scores >= 50` gives an array of `True`/`False`, one per element: a **mask**. Using the mask inside `[ ]` keeps only the `True` elements. It's the NumPy way to say "give me the values that pass this test", with no loop.

**Words to know:**

- **Boolean:** a `True`/`False` value (named after the mathematician George Boole).
- **Mask (boolean mask):** an array of booleans with the same shape as the data, used to pick elements.
- **Element-wise logical operators:** `&` (and), `|` (or), `~` (not), applied to each pair of booleans.
- **Operator precedence:** the order Python evaluates operators. `&` binds **tighter** than `>`, so each comparison needs its own brackets.
- **Fancy indexing:** indexing with a list (or array) of positions: `a[[0, 3, 5]]`.
- **`np.where(condition, x, y)`:** builds a new array taking `x` where the condition is true and `y` where it's false.

**Everyday picture.** A mask is a **stencil**: holes where you want to see the data, solid card everywhere else. Lay it over the array and only the values under the holes come through.

**How masking works, traced by hand:**

| `scores` | 45 | 82 | 67 | 91 | 38 | 74 |
|---|---|---|---|---|---|---|
| `scores >= 50` | False | True | True | True | False | True |
| `scores[scores >= 50]` | | 82 | 67 | 91 | | 74 |

Result: `[82 67 91 74]`. The result is always **1D** and a **copy**.

**Combining conditions:** `(a > 1) & (a < 5)`. The brackets are **required**: without them, Python reads `a > 1 & a < 5` as `a > (1 & a) < 5`. Python's `and`/`or`/`not` don't work on arrays (they need one single True/False and raise `ValueError: The truth value of an array ... is ambiguous`).

**Useful mask tricks:**

| Code | Gives |
|---|---|
| `mask.sum()` | how many are `True` (True counts as 1) |
| `mask.mean()` | the **fraction** that are `True` |
| `mask.any()`, `mask.all()` | is at least one / every element `True`? |
| `np.flatnonzero(mask)` | the **positions** of the `True` elements |
| `a[mask] = 0` | change only the matching elements (in place) |
| `np.isin(a, [1, 5])` | is each element one of these values? |

**`np.where` traced:** `np.where(scores >= 50, "pass", "fail")` walks the mask: `False → "fail"`, `True → "pass"`, … giving `['fail' 'pass' 'pass' 'pass' 'fail' 'pass']`. It's NumPy's version of an `if/else` per element (and of `CASE WHEN` in SQL). For more than two outcomes, use `np.select(conditions, choices, default)`.

**When to use:** filtering, counting things that meet a rule, cleaning (replace negatives, cap outliers), creating labels. **When not to:** if you need the *positions* of a handful of matches in a huge array repeatedly, sort once and use binary search (`np.searchsorted`), covered in `dsa-python.md` Section 18.

**Common mistakes:**

- ❌ `a[a > 1 and a < 5]` → `ValueError`. ✅ `a[(a > 1) & (a < 5)]`.
- ❌ `a[a > 1 & a < 5]` (missing brackets: a different, wrong calculation). ✅ Bracket every comparison.
- ❌ Expecting `a[mask]` to keep the 2D shape. It returns a 1D array of the matching values. ✅ Use `np.where(mask, a, 0)` to keep the shape.
- ❌ `a[mask].fill(0)` hoping to change `a` (it fills a temporary copy). ✅ `a[mask] = 0`.

**Used in real software:** every pandas filter (`df[df["price"] > 100]`) is a boolean mask underneath (Section [22](#22-filtering-rows-conditions-isin-between-and-query)); image editing uses masks to select regions; ML code uses `np.where(prob >= 0.5, 1, 0)` to turn probabilities into class labels.

### Python

```python
import numpy as np

scores = np.array([45, 82, 67, 91, 38, 74])
passed = scores >= 50
print(passed)
print(scores[passed], scores[(scores > 60) & (scores < 90)], scores[~passed])
print("passed:", passed.sum(), "of", passed.size, f"({passed.mean():.0%})")
print("positions of top scores:", np.flatnonzero(scores > 80))
print(scores[[0, -1, 2]])                              # fancy indexing: a chosen list of positions
```

**Output:**

```text
[False  True  True  True False  True]
[82 67 91 74] [82 67 74] [45 38]
passed: 4 of 6 (67%)
positions of top scores: [1 3]
[45 74 67]
```

```python
print(np.where(scores >= 50, "pass", "fail"))
grade = np.select([scores >= 85, scores >= 60, scores >= 50], ["A", "B", "C"], default="F")
print(grade)

temps = np.array([12.5, -3.0, 7.1, -0.5, 40.2])
temps[temps < 0] = 0                                 # replace in place
print(temps, np.where(temps > 35, 35, temps))        # cap at 35 (a new array)

m = np.arange(1, 13).reshape(3, 4)
print(m[m % 2 == 0])                                 # 2D in, 1D out
print(np.where(m % 2 == 0, m, 0))                    # keeps the shape
```

**Output:**

```text
['fail' 'pass' 'pass' 'pass' 'fail' 'pass']
['F' 'B' 'B' 'A' 'F' 'B']
[12.5  0.   7.1  0.  40.2] [12.5  0.   7.1  0.  35. ]
[ 2  4  6  8 10 12]
[[ 0  2  0  4]
 [ 0  6  0  8]
 [ 0 10  0 12]]
```

### Practice

1. From `x = np.random.default_rng(1).integers(0, 100, 20)`, keep the even numbers greater than 50, and print how many there are.
2. Replace every value of `x` below 10 with 10 and above 90 with 90 (this is called **clipping**; check your answer against `np.clip(x, 10, 90)`).

<details>
<summary><b>Answer</b></summary>

```python
x = np.random.default_rng(1).integers(0, 100, 20)
picked = x[(x % 2 == 0) & (x > 50)]
print(x, picked, len(picked), sep="\n")

y = x.copy()
y[y < 10] = 10
y[y > 90] = 90
print(np.array_equal(y, np.clip(x, 10, 90)))
```

**Output:**

```text
[47 51 75 95  3 14 82 94 24 31 86 42 27 82 25 40 64 54  8  2]
[82 94 86 82 64 54]
6
True
```

(`np.random.default_rng(1)` makes repeatable random numbers; Section [15](#15-random-numbers-and-simulation) explains it.)

</details>

| # | Problem (LeetCode, solve with a mask in pandas later too) | Difficulty |
|---|---|---|
| 1 | [595. Big Countries](https://leetcode.com/problems/big-countries/) | 🟢 Easy |
| 2 | [1757. Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/) | 🟢 Easy |

(These two are table problems; solve them now with NumPy-style thinking, then again in pandas after Section [22](#22-filtering-rows-conditions-isin-between-and-query).)

**Learn more:** [NumPy: boolean array indexing](https://numpy.org/doc/stable/user/basics.indexing.html#boolean-array-indexing) · [NumPy: np.where](https://numpy.org/doc/stable/reference/generated/numpy.where.html)

---

## 11. Vectorised Maths and Universal Functions

![An element-wise operation lines up two arrays and applies the operation to each pair at once](images/data-science/11-elementwise.svg)

### Theory

> **In simple words:** in NumPy, `+ - * /` and functions like `np.sqrt` work on **whole arrays**, element by element, and return a new array. You write the maths once, as if for one number, and it happens for every element at compiled speed. That style is called **vectorisation**.

**Words to know:**

- **Element-wise:** applied to each element (or each matching pair of elements) separately.
- **ufunc (universal function):** a NumPy function that works element-wise on arrays of any shape: `np.sqrt`, `np.exp`, `np.log`, `np.abs`, `np.maximum`, …
- **Exponential `exp(x)`:** e (≈ 2.718) raised to the power x. Grows extremely fast; used in growth models, softmax and probabilities.
- **Logarithm `log(x)`:** the inverse of `exp`: the power you'd raise e to, to get x. `np.log` is the **natural** log (base e); `np.log10` is base 10; `np.log1p(x)` computes `log(1 + x)` accurately for small x.
- **NaN (Not a Number):** a special float meaning "missing" or "undefined" (like 0/0). **inf:** infinity (like 1/0).
- **Scalar operation:** combining an array with a single number: `prices * 1.18` multiplies every element.
- **Activation function / ReLU:** in neural networks, a function applied after each layer's arithmetic; **ReLU** (rectified linear unit) is `max(0, x)`: negatives become 0.
- **Numba:** a library that compiles Python functions with loops into fast machine code (Section [39](#39-performance-vectorise-avoid-loops-and-measure)).

**Everyday picture.** Vectorised maths is a **cashier scanning a whole trolley in one sweep** instead of asking each item its price one by one. You describe what to do with one item; the machine does it for all.

**Operators and ufuncs:**

| Category | Operators / functions |
|---|---|
| Arithmetic | `+ - * / // % **`, `np.add`, `np.multiply`, … |
| Comparison (give booleans) | `== != < <= > >=` |
| Powers and roots | `np.sqrt`, `np.square`, `np.power(a, 3)`, `np.cbrt` |
| Exponents and logs | `np.exp`, `np.log`, `np.log10`, `np.log2`, `np.log1p` |
| Rounding | `np.round(a, 2)`, `np.floor`, `np.ceil`, `np.trunc` |
| Sign and size | `np.abs`, `np.sign`, `np.clip(a, lo, hi)` |
| Two arrays | `np.maximum(a, b)`, `np.minimum(a, b)` (element-wise max/min, **not** the overall max) |
| Trigonometry | `np.sin`, `np.cos`, `np.deg2rad` |
| Missing-safe checks | `np.isnan`, `np.isinf`, `np.isfinite` |

**Element-wise, traced:** `np.array([1, 2, 3]) * np.array([10, 20, 30])` pairs position 0 with 0, 1 with 1, 2 with 2: `[1×10, 2×20, 3×30] = [10 40 90]`. The arrays must have the **same shape** (or shapes that **broadcast**, Section [13](#13-broadcasting-maths-between-arrays-of-different-shapes)).

**Special values:** `np.log(0)` is `-inf`, `np.log(-1)` and `0/0` are `nan`, `1/0` is `inf`. NumPy gives a **warning**, not an error, and carries on, so check with `np.isfinite` after risky maths.

**When to use:** almost always: any calculation applied to every element. **When it gets hard:** logic that depends on the previous result (a running balance with rules, say). Try a built-in first (`np.cumsum`, `np.maximum.accumulate`); if nothing fits, a plain loop (or the `numba` library, which compiles Python loops) is acceptable.

**Common mistakes:**

- ❌ `math.sqrt(arr)`: the `math` module only takes single numbers (`TypeError`). ✅ `np.sqrt(arr)`.
- ❌ `max(a, b)` for element-wise maximum (Python's `max` compares whole arrays and errors). ✅ `np.maximum(a, b)`.
- ❌ Ignoring `RuntimeWarning: divide by zero`. ✅ Guard with `np.where(b != 0, a / b, 0)` or check `np.isfinite`.

**Used in real software:** price and tax calculations on whole columns; feature transforms before ML (`np.log1p(income)` to tame big values); activation functions in neural networks (`np.maximum(0, x)` is the **ReLU** function used in deep learning).

### Python

```python
import numpy as np

prices = np.array([60.0, 15.5, 1200.0, 350.0])
qty = np.array([5, 10, 1, 2])
revenue = prices * qty                                  # element-wise
print(revenue, revenue.sum())
print(np.round(prices * 1.18, 2))                       # add 18% tax to every price
print(np.sqrt([4, 9, 16]), np.exp([0, 1]).round(3), np.log([1, np.e, 100]).round(3))
print(np.maximum(prices, 100), np.clip(prices, 50, 500))
```

**Output:**

```text
[ 300.  155. 1200.  700.] 2355.0
[  70.8    18.29 1416.    413.  ]
[2. 3. 4.] [1.    2.718] [0.    1.    4.605]
[ 100.  100. 1200.  350.] [ 60.  50. 500. 350.]
```

```python
income = np.array([0, 9_000, 25_000, 120_000, 4_500_000])
print(np.log1p(income).round(2))                        # big gaps shrink: useful before ML

x = np.array([-2.0, -0.5, 0.0, 1.5])
print(np.maximum(0, x))                                  # ReLU, the deep-learning activation

with np.errstate(divide="ignore", invalid="ignore"):    # silence the warnings for this demo
    ratio = np.array([1.0, 0.0, -1.0]) / np.array([0.0, 0.0, 2.0])
print(ratio, np.isfinite(ratio))
```

**Output:**

```text
[ 0.    9.11 10.13 11.7  15.32]
[0.  0.  0.  1.5]
[ inf  nan -0.5] [False False  True]
```

`np.errstate` temporarily changes how NumPy reports floating-point problems; outside a demo, you'd rather check results than hide warnings.

### Practice

1. Convert Celsius temperatures `[0, 25, 37, 100]` to Fahrenheit (`F = C × 9/5 + 32`) without a loop.
2. Given `a = np.array([3, 8, 1])` and `b = np.array([5, 2, 9])`, compute the element-wise larger value, and the **percentage change** from `a` to `b` rounded to 1 decimal.

<details>
<summary><b>Answer</b></summary>

```python
c = np.array([0, 25, 37, 100])
print(c * 9 / 5 + 32)
a, b = np.array([3, 8, 1]), np.array([5, 2, 9])
print(np.maximum(a, b), np.round((b - a) / a * 100, 1))
```

**Output:**

```text
[ 32.   77.   98.6 212. ]
[5 8 9] [ 66.7 -75.  800. ]
```

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [121. Vector Element-wise Sum](https://www.deep-ml.com/problems/121) | 🟢 Easy |
| 2 | [5. Scalar Multiplication of a Matrix](https://www.deep-ml.com/problems/5) | 🟢 Easy |
| 3 | [112. Min-Max Scaling of Feature Values](https://www.deep-ml.com/problems/112) | 🟢 Easy |

**Learn more:** [NumPy: universal functions (ufunc)](https://numpy.org/doc/stable/reference/ufuncs.html)

---

## 12. Aggregations and the axis Argument

![axis=0 squashes the rows and gives one result per column; axis=1 squashes the columns and gives one result per row](images/data-science/12-axis.svg)

### Theory

> **In simple words:** an **aggregation** squashes many numbers into one: the total, the average, the biggest. On a table, the `axis` argument says **which direction to squash**: down the columns (`axis=0`, one answer per column) or across the rows (`axis=1`, one answer per row).

**Words to know:**

- **Aggregation (aggregate function, reduction):** a function that turns many values into fewer: `sum`, `mean`, `max`, …
- **Mean:** the average: add everything up and divide by how many there are.
- **Median:** the middle value after sorting (half are below, half above). Section [51](#51-describing-data-centre-spread-and-shape) explains when it beats the mean.
- **Standard deviation (std):** a measure of how spread out values are around the mean (Section [51](#51-describing-data-centre-spread-and-shape)). **Variance** is the std squared.
- **Percentile / quantile:** the value below which a given percentage of the data falls. The 90th percentile is bigger than 90% of the values.
- **argmax / argmin:** the **position** of the biggest / smallest value, not the value itself.
- **Cumulative sum (cumsum):** a running total: each element is the sum of everything up to it.
- **Latency:** how long something takes to respond (a web request, a database query).
- **p50 / p95 / p99:** the 50th, 95th and 99th percentiles, usually of latency: "p99 = 800 ms" means 99% of requests finish within 800 ms.

**Everyday picture.** A sales table has stores as rows and months as columns. "Total per month" means pressing each **column** down into one number: `axis=0`. "Total per store" means squashing each **row** sideways: `axis=1`. **The axis you name is the one that disappears.**

**Traced by hand,** with `sales` = rows are stores, columns are months:

```text
              Jan  Feb  Mar      sum(axis=1)  (per store)
store A  [[   10,  20,  30],     → 60
store B   [    5,  15,  25],     → 45
store C   [    8,  12,  40]]     → 60
sum(axis=0)  23   47   95        (per month)       sum() → 165
```

Shapes: `sales` is `(3, 3)`; `sales.sum(axis=0)` has shape `(3,)` (the row axis vanished); `sales.sum()` is a single number.

**The aggregation functions** (all accept `axis=`):

| Function | Gives | Function | Gives |
|---|---|---|---|
| `sum` | total | `min`, `max` | smallest, largest |
| `mean` | average | `argmin`, `argmax` | position of smallest, largest |
| `median` | middle value | `std`, `var` | spread |
| `percentile(a, 90)` | 90th percentile | `quantile(a, 0.9)` | the same, as a fraction |
| `cumsum`, `cumprod` | running total / product (shape unchanged) | `ptp` | range = max − min |
| `any`, `all` | for booleans | `count_nonzero` | how many non-zero / True |

**`keepdims=True`** keeps the squashed axis with size 1 (`(3, 3)` → `(3, 1)`) so the result lines up with the original for broadcasting, e.g. dividing each row by its own total (Section [13](#13-broadcasting-maths-between-arrays-of-different-shapes)).

**Missing values:** any `nan` makes `sum`, `mean`, `max` return `nan`. Use the **nan-safe** versions: `np.nansum`, `np.nanmean`, `np.nanmax`, `np.nanmedian`, …

**`std` and `ddof`:** NumPy's `std` divides by `n` by default (`ddof=0`, the **population** formula). pandas divides by `n − 1` (`ddof=1`, the **sample** formula). Section [51](#51-describing-data-centre-spread-and-shape) explains why; for now, know that the two libraries give slightly different numbers on small data unless you set `ddof`.

**When to use which axis:** features are usually **columns**, so per-feature statistics (means for scaling, say) use `axis=0`. Per-sample statistics (a student's average across subjects) use `axis=1`.

**Common mistakes:**

- ❌ Mixing up `axis=0` and `axis=1`. ✅ Say "the axis I name disappears"; check the result's shape.
- ❌ `argmax` when you wanted the value. ✅ `a.max()` for the value, `a.argmax()` for its position.
- ❌ `mean` on data with `nan`. ✅ `np.nanmean`.
- ❌ Comparing NumPy `std` with pandas `std` and thinking one is buggy. ✅ It's `ddof`.

**Used in real software:** dashboards (totals per region per month); ML preprocessing (`X.mean(axis=0)` and `X.std(axis=0)` per feature for scaling); image processing (`img.mean(axis=2)` turns a colour image into greyscale); latency monitoring (the 95th and 99th percentile response time, known as **p95** and **p99**).

### Python

```python
import numpy as np

sales = np.array([[10, 20, 30],      # rows = stores A, B, C; columns = Jan, Feb, Mar
                  [ 5, 15, 25],
                  [ 8, 12, 40]])
print(sales.sum(), sales.sum(axis=0), sales.sum(axis=1))
print(sales.mean(axis=0).round(2), sales.max(axis=1), sales.argmax(axis=1))
print(sales.cumsum(axis=1))                       # running total across months, per store
print(sales.sum(axis=1, keepdims=True).shape)
share = sales / sales.sum(axis=1, keepdims=True)  # each month's share of its store's total
print(share.round(2))
```

**Output:**

```text
165 [23 47 95] [60 45 60]
[ 7.67 15.67 31.67] [30 25 40] [2 2 2]
[[10 30 60]
 [ 5 20 45]
 [ 8 20 60]]
(3, 1)
[[0.17 0.33 0.5 ]
 [0.11 0.33 0.56]
 [0.13 0.2  0.67]]
```

```python
latency_ms = np.random.default_rng(0).lognormal(mean=4, sigma=0.5, size=10_000)
print(f"median {np.median(latency_ms):.0f} ms, p95 {np.percentile(latency_ms, 95):.0f} ms, "
      f"p99 {np.percentile(latency_ms, 99):.0f} ms, max {latency_ms.max():.0f} ms")

data = np.array([2.0, np.nan, 4.0, 6.0])
print(data.mean(), np.nanmean(data), np.nanmax(data))
x = np.array([2, 4, 4, 4, 5, 5, 7, 9])
print(x.std(), x.std(ddof=1).round(4))            # population vs sample formula
```

**Output:**

```text
median 54 ms, p95 124 ms, p99 173 ms, max 311 ms
nan 4.0 6.0
2.0 2.1381
```

The latency example uses a **log-normal** distribution (a common shape for response times: most are fast, a few are very slow); Section [54](#54-probability-distributions-normal-binomial-poisson-and-more) explains it. Notice p99 is far above the median: that long tail is why engineers track percentiles, not averages.

### Practice

1. Exam scores `s` have shape (5 students, 3 subjects). Find each student's average, each subject's top score, and **which student** got the top score in each subject.
2. For `sales` above, which month had the highest total across all stores? Answer with the month's name, using `argmax`.

<details>
<summary><b>Answer</b></summary>

```python
s = np.random.default_rng(7).integers(40, 100, size=(5, 3))
print(s)
print(s.mean(axis=1).round(1), s.max(axis=0), s.argmax(axis=0))
months = np.array(["Jan", "Feb", "Mar"])
print(months[sales.sum(axis=0).argmax()])
```

**Output:**

```text
[[96 77 81]
 [93 74 86]
 [90 53 43]
 [58 57 92]
 [94 40 69]]
[84.7 84.3 62.  69.  67.7] [96 77 92] [0 0 3]
Mar
```

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [4. Calculate Mean by Row or Column](https://www.deep-ml.com/problems/4) | 🟢 Easy |
| 2 | [78. Descriptive Statistics Calculator](https://www.deep-ml.com/problems/78) | 🟢 Easy |
| 3 | [293. Calculate P50/P95/P99 Latency Percentiles](https://www.deep-ml.com/problems/293) | 🟢 Easy |

**Learn more:** [NumPy: statistics routines](https://numpy.org/doc/stable/reference/routines.statistics.html)

---

## 13. Broadcasting: Maths Between Arrays of Different Shapes

![Broadcasting stretches a smaller array across a bigger one without copying it](images/data-science/02-broadcasting.svg)

### Theory

> **In simple words:** broadcasting is the rule that lets NumPy combine arrays of **different shapes**, like adding one row of numbers to every row of a table. The smaller array is "stretched" to match the bigger one, without actually copying it.

**Words to know:**

- **Broadcasting:** NumPy's rules for matching up arrays of different shapes in element-wise operations.
- **Compatible shapes:** shapes that broadcasting can line up.
- **Trailing dimensions:** the axes at the **end** (right side) of a shape. Broadcasting compares shapes starting from the right.
- **`None` / `np.newaxis` in an index:** inserts a new axis of size 1: `a[:, None]` turns shape `(3,)` into `(3, 1)`.
- **Standardise (z-score):** subtract the mean and divide by the standard deviation, so a column has mean 0 and standard deviation 1.
- **Outer operation:** combining **every** element of one array with **every** element of another, giving a grid.
- **Clustering (k-means):** grouping similar points together without labels; **k-means** repeatedly assigns each point to its nearest of k centres and moves each centre to the mean of its points (`machine-learning.md`).

**Everyday picture.** A teacher adds 5 bonus marks to every student's Maths, 3 to Physics and 2 to Chemistry. She doesn't write the bonus row out for each student: she has **one** bonus row and applies it down the whole mark sheet. That's broadcasting a `(3,)` row across a `(students, 3)` table.

**The rule, step by step:**

1. Write the two shapes one under the other, **right-aligned**.
2. If one shape is shorter, pad it on the **left** with 1s.
3. Compare each column of sizes. They're compatible if they're **equal** or **one of them is 1**.
4. A size-1 axis is stretched to match the other. The result takes the larger size on each axis.
5. If any pair is unequal and neither is 1 → `ValueError: operands could not be broadcast together`.

**Traced by hand:**

| A | B | Right-aligned (padded) | Result |
|---|---|---|---|
| `(3, 4)` | `(4,)` | `3 4` vs `1 4` → 3 vs 1 ✅, 4 vs 4 ✅ | `(3, 4)`: the row is added to each row |
| `(3, 4)` | `(3, 1)` | 3 vs 3 ✅, 4 vs 1 ✅ | `(3, 4)`: the column is added to each column |
| `(3, 1)` | `(1, 4)` | 3 vs 1 ✅, 1 vs 4 ✅ | `(3, 4)`: every pair (an outer operation) |
| `(3, 4)` | `(3,)` | `3 4` vs `1 3` → 4 vs 3 ❌ | error: make it `(3, 1)` with `b[:, None]` |
| `(2, 3, 4)` | `(3, 4)` | 2 vs 1 ✅, 3 vs 3 ✅, 4 vs 4 ✅ | `(2, 3, 4)` |

**The classic use, standardising columns:** `(X - X.mean(axis=0)) / X.std(axis=0)`. `X` is `(n, features)`; `X.mean(axis=0)` is `(features,)`; broadcasting subtracts each column's own mean from every row of that column at once. ML models often need this (the `machine-learning.md` notes use scikit-learn's `StandardScaler`, which does exactly this).

**Per-row operations need `keepdims` or `None`:** to divide each row by its own total, the totals must be shaped `(rows, 1)`, not `(rows,)`: `X / X.sum(axis=1, keepdims=True)`.

**Why no copy?** NumPy fakes the stretching by reading the same memory again (a "stride" of 0 along that axis), so broadcasting a 1-row array across a million rows uses no extra memory for the row.

**When to use:** per-column or per-row adjustments, pairwise distances, grids of combinations. **When to be careful:** an accidental broadcast (e.g. `(n,)` vs `(n, 1)`) silently builds an `n × n` result instead of an error. Print shapes when unsure.

**Common mistakes:**

- ❌ `X - X.mean(axis=1)` for per-row centring: shapes `(n, k)` and `(n,)` don't align (or align wrongly when `n == k`). ✅ `X - X.mean(axis=1, keepdims=True)`.
- ❌ Subtracting a column vector `(n, 1)` from a 1D array `(n,)` and getting an `(n, n)` matrix. ✅ Make shapes match first; assert `result.shape`.
- ❌ Thinking broadcasting copies data. It doesn't, so it's cheap; the **result** is still full size, though.

**Used in real software:** feature scaling in every ML pipeline; adding a bias vector to each row in a neural-network layer (`X @ W + b`, Section [16](#16-linear-algebra-basics-dot-products-matrix-multiplication-and-solving-equations)); computing distances from every point to every cluster centre in k-means (`machine-learning.md`).

### Python

```python
import numpy as np

marks = np.array([[70, 65, 80],      # rows = students; columns = Maths, Physics, Chemistry
                  [55, 72, 60],
                  [90, 85, 88]])
bonus = np.array([5, 3, 2])          # shape (3,): one bonus per subject
print(marks + bonus)                 # (3, 3) + (3,) → added to every row

curve = np.array([[10], [0], [-5]])  # shape (3, 1): one adjustment per student
print(marks + curve)                 # added across each row

print(np.arange(1, 4)[:, None] * np.arange(1, 5))   # (3,1) × (4,) → a 3 × 4 times table
```

**Output:**

```text
[[75 68 82]
 [60 75 62]
 [95 88 90]]
[[80 75 90]
 [55 72 60]
 [85 80 83]]
[[ 1  2  3  4]
 [ 2  4  6  8]
 [ 3  6  9 12]]
```

```python
body = np.array([[170, 65], [182, 80], [158, 52]], dtype=float)   # columns: height cm, weight kg
z = (body - body.mean(axis=0)) / body.std(axis=0)
print(z.round(2))
print(z.mean(axis=0).round(10) + 0.0, z.std(axis=0))                # each column: mean 0, std 1
# (+ 0.0 turns a "-0." rounding leftover into a plain 0.)

row_share = marks / marks.sum(axis=1, keepdims=True)
print(row_share.round(2), row_share.sum(axis=1))

points = np.array([[0, 0], [3, 4], [6, 8]])
centres = np.array([[0, 0], [6, 8]])
d = np.sqrt(((points[:, None, :] - centres[None, :, :]) ** 2).sum(axis=2))   # (3,1,2) - (1,2,2) → (3,2,2)
print(d)                                                                     # distance from each point to each centre
```

**Output:**

```text
[[ 0.   -0.06]
 [ 1.22  1.25]
 [-1.22 -1.19]]
[0. 0.] [1. 1.]
[[0.33 0.3  0.37]
 [0.29 0.39 0.32]
 [0.34 0.32 0.33]] [1. 1. 1.]
[[ 0. 10.]
 [ 5.  5.]
 [10.  0.]]
```

The last example is the heart of the k-means clustering algorithm: `d[i, j]` is the distance from point `i` to centre `j`, computed for all pairs at once.

```python
marks + np.array([1, 2])             # (3, 3) + (2,): 3 vs 2, neither is 1
```

**Output:**

```text
Traceback (most recent call last):
  ...
ValueError: operands could not be broadcast together with shapes (3,3) (2,)
```

### Practice

1. Subtract each **student's** average (row mean) from their marks, so each row then averages 0.
2. Predict the result shapes, then check: `(5, 1) + (1, 6)`, `(4, 3) * (3,)`, `(2, 1, 3) + (4, 1)`.

<details>
<summary><b>Answer</b></summary>

```python
centred = marks - marks.mean(axis=1, keepdims=True)
print(centred.round(2), centred.mean(axis=1).round(10) + 0.0)
print((np.ones((5, 1)) + np.ones((1, 6))).shape,
      (np.ones((4, 3)) * np.ones(3)).shape,
      (np.ones((2, 1, 3)) + np.ones((4, 1))).shape)
```

**Output:**

```text
[[-1.67 -6.67  8.33]
 [-7.33  9.67 -2.33]
 [ 2.33 -2.67  0.33]] [0. 0. 0.]
(5, 6) (4, 3) (2, 4, 3)
```

The last one: right-align `2 1 3` and `_ 4 1` → pad to `1 4 1` → sizes 2 vs 1, 1 vs 4, 3 vs 1 → `(2, 4, 3)`.

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [112. Min-Max Scaling of Feature Values](https://www.deep-ml.com/problems/112) | 🟢 Easy |
| 2 | [10. Calculate Covariance Matrix](https://www.deep-ml.com/problems/10) | 🟢 Easy |

**Learn more:** [NumPy: broadcasting](https://numpy.org/doc/stable/user/basics.broadcasting.html)

---

## 14. Reshaping, Stacking, Splitting and Sorting

![reshape fills the new shape row by row in the original reading order; the numbers never change, only their arrangement](images/data-science/14-reshape.svg)

### Theory

> **In simple words:** the same 12 numbers can be one row of 12, or 3 rows of 4, or 2 × 2 × 3 blocks. **Reshaping** changes the arrangement without changing the numbers. **Stacking** glues arrays together, **splitting** cuts them apart, and **sorting** puts values in order.

**Words to know:**

- **Reshape:** give an array a new shape with the **same total size**.
- **Row-major (C) order:** the reading order NumPy uses by default: along each row left to right, then the next row, like reading a book.
- **Flatten / ravel:** turn any array into 1D.
- **Transpose (`.T`):** swap rows and columns: element `[i, j]` moves to `[j, i]`.
- **Concatenate:** join arrays end to end along an **existing** axis. **Stack:** join them along a **new** axis.
- **Split:** cut one array into several.
- **Sort:** arrange in order. **argsort:** the **positions** that would sort the array (used to sort one array by another).
- **Unique:** the distinct values, optionally with how often each appears.

**Everyday picture.** 12 eggs can sit in one long row or in a 3 × 4 carton: same eggs, same order when you read them left to right, top to bottom. Reshaping is moving eggs between cartons in that reading order.

**Reshape, traced:** `np.arange(6).reshape(2, 3)` reads 0 1 2 3 4 5 in order and fills row 0 first: `[[0 1 2], [3 4 5]]`. `-1` means "work this size out": `reshape(-1, 2)` on 6 elements gives `(3, 2)`. The total must match: 6 elements can't become `(4, 2)`.

**The shape-changing tools:**

| Code | Does | Shape example |
|---|---|---|
| `a.reshape(3, 4)` | new shape, same data (a view when possible) | `(12,)` → `(3, 4)` |
| `a.reshape(-1)`, `a.ravel()` | flatten to 1D (`ravel` returns a view when possible) | `(3, 4)` → `(12,)` |
| `a.flatten()` | flatten, always a **copy** | `(3, 4)` → `(12,)` |
| `a.T` | transpose | `(3, 4)` → `(4, 3)` |
| `a[:, None]`, `np.expand_dims(a, 1)` | add an axis of size 1 | `(3,)` → `(3, 1)` |
| `np.squeeze(a)` | remove axes of size 1 | `(1, 3, 1)` → `(3,)` |

**Joining and cutting:**

| Code | Does | `(2, 3)` and `(2, 3)` give |
|---|---|---|
| `np.concatenate([a, b], axis=0)` / `np.vstack` | one under the other | `(4, 3)` |
| `np.concatenate([a, b], axis=1)` / `np.hstack` | side by side | `(2, 6)` |
| `np.stack([a, b])` | along a **new** first axis | `(2, 2, 3)` |
| `np.split(a, 3, axis=1)` | into 3 equal pieces | three `(2, 1)` arrays |
| `np.array_split(a, 4)` | into 4 pieces, sizes may differ | |

**Sorting:**

| Code | Does |
|---|---|
| `np.sort(a)` | a sorted **copy** (ascending) |
| `a.sort()` | sorts **in place** |
| `np.sort(a)[::-1]` | descending |
| `np.argsort(a)` | positions that would sort `a`; `names[np.argsort(scores)]` sorts names by score |
| `np.sort(m, axis=1)` | sort each row separately |
| `np.unique(a, return_counts=True)` | distinct values and their counts |
| `np.partition(a, k)` | puts the k-th smallest in position k, smaller ones before it (unsorted), in O(n): fast top-k |

**`argsort`, traced:** `scores = [70, 95, 60]` → sorted order is 60 (position 2), 70 (position 0), 95 (position 1), so `argsort` gives `[2, 0, 1]`. Then `names[[2, 0, 1]]` lists names from lowest to highest score.

**When to use:** reshape when a library expects a particular shape (scikit-learn wants 2D `X` of shape `(samples, features)`, so one feature `x` becomes `x.reshape(-1, 1)`); stack to combine batches; `argsort` whenever you sort one thing by another.

**Common mistakes:**

- ❌ Using `reshape` to transpose. `reshape(4, 3)` of a `(3, 4)` array **re-reads** the numbers in order; it doesn't swap rows and columns. ✅ `.T`.
- ❌ `np.concatenate([a, b])` with mismatched sizes on the other axis. ✅ All axes except the joining one must match.
- ❌ Calling `np.sort` on two arrays separately and expecting rows to stay paired. ✅ `order = np.argsort(key)`, then index both with `order`.

**Used in real software:** `x.reshape(-1, 1)` appears in nearly every beginner scikit-learn example; images are reshaped between `(height, width, channels)` and `(channels, height, width)` for different libraries; batches of training data are `np.stack`ed; recommendation systems use `argpartition` to grab the top-k items fast.

### Python

```python
import numpy as np

a = np.arange(12)
print(a.reshape(3, 4), a.reshape(-1, 6).shape, sep="\n")
m = a.reshape(3, 4)
print(m.T)                                    # transpose: (3, 4) → (4, 3)
print(m.reshape(4, 3))                        # NOT the same as .T: just re-reads the numbers
print(np.array([1, 2, 3])[:, None].shape, np.squeeze(np.zeros((1, 3, 1))).shape)
```

**Output:**

```text
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
(2, 6)
[[ 0  4  8]
 [ 1  5  9]
 [ 2  6 10]
 [ 3  7 11]]
[[ 0  1  2]
 [ 3  4  5]
 [ 6  7  8]
 [ 9 10 11]]
(3, 1) (3,)
```

```python
x = np.array([[1, 2, 3], [4, 5, 6]])
y = np.array([[7, 8, 9], [10, 11, 12]])
print(np.vstack([x, y]).shape, np.hstack([x, y]).shape, np.stack([x, y]).shape)
left, right = np.split(np.hstack([x, y]), 2, axis=1)
print(np.array_equal(left, x), np.array_equal(right, y))

scores = np.array([70, 95, 60, 88])
names = np.array(["Asha", "Ravi", "Zoya", "Meera"])
order = np.argsort(scores)
print(order, names[order], names[order[::-1]][:2])        # lowest → highest; top 2
print(np.unique(["Pune", "Delhi", "Pune", "Goa", "Pune"], return_counts=True))
print(np.sort(np.array([[3, 1, 2], [9, 7, 8]]), axis=1))
print(np.partition(np.array([9, 1, 8, 2, 7, 3]), 2)[:2])  # the 2 smallest (any order)
```

**Output:**

```text
(4, 3) (2, 6) (2, 2, 3)
True True
[2 0 3 1] ['Zoya' 'Asha' 'Meera' 'Ravi'] ['Ravi' 'Meera']
(array(['Delhi', 'Goa', 'Pune'], dtype='<U5'), array([1, 1, 3]))
[[1 2 3]
 [7 8 9]]
[1 2]
```

### Practice

1. Turn `np.arange(24)` into shape `(2, 3, 4)`, then into `(6, 4)`, then back to 1D.
2. You have `heights = np.array([165, 180, 158])` and `names = np.array(["A", "B", "C"])`. Print the names from tallest to shortest.

<details>
<summary><b>Answer</b></summary>

```python
t = np.arange(24).reshape(2, 3, 4)
print(t.shape, t.reshape(6, 4).shape, t.ravel().shape)
heights, names = np.array([165, 180, 158]), np.array(["A", "B", "C"])
print(names[np.argsort(heights)[::-1]])
```

**Output:**

```text
(2, 3, 4) (6, 4) (24,)
['B' 'A' 'C']
```

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [3. Reshape Matrix](https://www.deep-ml.com/problems/3) | 🟢 Easy |
| 2 | [2. Transpose of a Matrix](https://www.deep-ml.com/problems/2) | 🟢 Easy |

**Learn more:** [NumPy: array manipulation routines](https://numpy.org/doc/stable/reference/routines.array-manipulation.html) · [NumPy: sorting and searching](https://numpy.org/doc/stable/reference/routines.sort.html)

---

## 15. Random Numbers and Simulation

![Rolling two dice 100,000 times: the simulated frequencies match the exact probabilities](images/data-science/dice-simulation.png)

### Theory

> **In simple words:** a computer can generate numbers that **look** random. With them you can **simulate**: roll a million dice, shuffle a deck, or invent realistic test data, and then count what happened. Fixing a **seed** makes the "random" numbers the same every run, so your results can be repeated.

**Words to know:**

- **Pseudo-random numbers:** numbers made by a deterministic formula that only **looks** random. Good enough for data science; not for passwords (use Python's `secrets` module for those).
- **Seed:** the starting number for the formula. Same seed → same sequence of numbers.
- **Generator:** NumPy's random-number object, created by `np.random.default_rng(seed)`.
- **Reproducible:** someone else running your code gets exactly your results.
- **Uniform distribution:** every value in a range is equally likely (a fair die).
- **Normal (Gaussian) distribution:** the bell curve: values cluster around a mean and get rarer further away (heights, measurement errors). Defined by its **mean** (centre) and **standard deviation** (width).
- **Sampling with / without replacement:** with replacement, an item can be picked again (rolling a die); without, each item is picked at most once (dealing cards).
- **Simulation (Monte Carlo method):** estimating something by generating many random trials and counting outcomes. Named after the Monte Carlo casino.
- **Law of large numbers:** the more trials you run, the closer the observed fraction gets to the true probability.
- **A/B test:** an experiment that randomly splits users between two versions and compares a metric (Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls)).

**Everyday picture.** A seed is like the starting position of a shuffled deck in a magic trick: the deck *looks* shuffled, but if you start from the same arrangement and do the same moves, you get the same cards in the same order every time.

**The modern API** (use this, not the old `np.random.rand` functions):

| Code | Gives |
|---|---|
| `rng = np.random.default_rng(42)` | a Generator with seed 42 |
| `rng.random(5)` | 5 uniform floats in [0, 1) (0 included, 1 excluded) |
| `rng.integers(1, 7, size=10)` | 10 integers from 1 to 6 (**high is excluded**) |
| `rng.uniform(10, 20, 5)` | uniform floats between 10 and 20 |
| `rng.normal(loc=170, scale=10, size=1000)` | normal values, mean 170, standard deviation 10 |
| `rng.choice(["a", "b", "c"], size=5, p=[0.5, 0.3, 0.2])` | picks with given probabilities |
| `rng.choice(10, size=3, replace=False)` | 3 different items (without replacement) |
| `rng.permutation(a)` / `rng.shuffle(a)` | shuffled copy / shuffle in place |
| `rng.binomial(n=10, p=0.5, size=5)`, `rng.poisson(3, 5)`, `rng.exponential(2, 5)` | other distributions (Section [54](#54-probability-distributions-normal-binomial-poisson-and-more)) |

**Why `default_rng` and not `np.random.seed`?** The old functions share one global state: any library calling them changes your sequence. A Generator is your own object; pass it to functions that need randomness. It also uses a better algorithm (PCG64).

**How a simulation estimates a probability, step by step** (chance that two dice sum to 7):

1. Roll die A 100,000 times and die B 100,000 times (two arrays of 1–6).
2. Add them element-wise: 100,000 sums.
3. Make a mask `sums == 7` and take its mean: the fraction of 7s.
4. Compare with the exact answer: 6 of the 36 equally likely pairs sum to 7, so 6/36 ≈ 0.1667.

**When to use simulation:** when the maths is hard but the process is easy to describe (queues, risk, games, "what if" scenarios), to check a formula you derived, and to create **synthetic data** to test code. **When not to:** when an exact formula is easy (then use it), or when you need security (use `secrets`).

**Common mistakes:**

- ❌ No seed in experiments, so results change every run and can't be debugged. ✅ Seed once at the top and pass the `rng` around.
- ❌ `rng.integers(1, 6)` for a die (that gives 1–5). ✅ `rng.integers(1, 7)`.
- ❌ Re-creating `default_rng(42)` inside a loop, which gives the **same** numbers every iteration. ✅ Create it once.
- ❌ Trusting a simulation with few trials. ✅ More trials → less noise (the noise shrinks like 1/√trials, Section [55](#55-sampling-the-central-limit-theorem-and-standard-error)).

**Used in real software:** shuffling and splitting data before training a model; random initial weights in neural networks; A/B test assignment; risk models in finance (simulate thousands of possible futures); load testing with synthetic users.

### Python

```python
import numpy as np

rng = np.random.default_rng(42)
print(rng.integers(1, 7, size=10))                     # 10 dice rolls
print(rng.normal(loc=170, scale=10, size=3).round(1))  # 3 heights
print(rng.choice(["cash", "card", "UPI"], size=6, p=[0.2, 0.3, 0.5]))
print(rng.permutation(np.arange(1, 9)))                # shuffled 1..8

print(np.random.default_rng(7).random(3).round(3), np.random.default_rng(7).random(3).round(3))   # same seed, same numbers
```

**Output:**

```text
[1 5 4 3 3 6 1 5 2 1]
[157.  171.3 166.8]
['cash' 'card' 'card' 'UPI' 'UPI' 'UPI']
[2 1 5 8 6 7 3 4]
[0.625 0.897 0.776] [0.625 0.897 0.776]
```

```python
import matplotlib.pyplot as plt

rng = np.random.default_rng(0)
n = 100_000
sums = rng.integers(1, 7, n) + rng.integers(1, 7, n)
print(f"P(sum = 7) ≈ {(sums == 7).mean():.4f}   exact 6/36 = {6/36:.4f}")

values, counts = np.unique(sums, return_counts=True)
exact = np.array([6 - abs(7 - s) for s in values]) / 36   # ways to make each sum, out of 36
for v, c, e in zip(values, counts, exact):
    print(f"{v:2d}: simulated {c / n:.4f}  exact {e:.4f}")

fig, ax = plt.subplots(figsize=(7, 3.2), layout="constrained")
ax.bar(values, counts / n, color="#93c5fd", label="simulated (100,000 rolls)")
ax.plot(values, exact, "o-", color="#dc2626", label="exact probability")
ax.set(xlabel="sum of two dice", ylabel="probability", xticks=values, title="Simulation matches the maths")
ax.legend()
fig.savefig("dice-simulation.png", dpi=100)
plt.close(fig)
```

**Output:**

```text
P(sum = 7) ≈ 0.1667   exact 6/36 = 0.1667
 2: simulated 0.0286  exact 0.0278
 3: simulated 0.0540  exact 0.0556
 4: simulated 0.0832  exact 0.0833
 5: simulated 0.1117  exact 0.1111
 6: simulated 0.1389  exact 0.1389
 7: simulated 0.1667  exact 0.1667
 8: simulated 0.1410  exact 0.1389
 9: simulated 0.1095  exact 0.1111
10: simulated 0.0832  exact 0.0833
11: simulated 0.0556  exact 0.0556
12: simulated 0.0276  exact 0.0278
```

(The chart code uses Matplotlib, taught in Part 7; for now just run it.)

```python
for trials in (10, 100, 10_000, 1_000_000):          # law of large numbers
    heads = np.random.default_rng(2).integers(0, 2, trials).mean()
    print(f"{trials:>9,} flips → fraction of heads {heads:.4f}")

# Monte Carlo estimate of π: throw darts at a square; the fraction landing inside the quarter circle ≈ π/4
pts = np.random.default_rng(3).random((1_000_000, 2))
inside = (pts ** 2).sum(axis=1) <= 1
print("π ≈", 4 * inside.mean())
```

**Output:**

```text
       10 flips → fraction of heads 0.3000
      100 flips → fraction of heads 0.5100
   10,000 flips → fraction of heads 0.4955
1,000,000 flips → fraction of heads 0.5005
π ≈ 3.140468
```

### Practice

1. Simulate 10,000 families with 3 children each (each child a boy or girl with probability 0.5). Estimate the probability of exactly 2 girls. (Exact answer: 3/8 = 0.375.)
2. A playlist has 20 songs. Shuffle it and print the first 5 song numbers, so that the same shuffle appears every time you run it.

<details>
<summary><b>Answer</b></summary>

```python
rng = np.random.default_rng(11)
girls = rng.integers(0, 2, size=(10_000, 3)).sum(axis=1)   # each row is a family
print((girls == 2).mean())
print(np.random.default_rng(5).permutation(np.arange(1, 21))[:5])
```

**Output:**

```text
0.3729
[10 19  4  8  2]
```

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [184. Empirical Probability Mass Function (PMF)](https://www.deep-ml.com/problems/184) | 🟢 Easy |
| 2 | [179. Expected Value and Variance of an n-Sided Die](https://www.deep-ml.com/problems/179) | 🟢 Easy |
| 3 | [246. Birthday Problem Probability](https://www.deep-ml.com/problems/246) | 🟡 Medium |
| 4 | [182. Central Limit Theorem Simulation](https://www.deep-ml.com/problems/182) | 🟡 Medium |

**Learn more:** [NumPy: random Generator](https://numpy.org/doc/stable/reference/random/generator.html) · [Seeing Theory: chance events (interactive)](https://seeing-theory.brown.edu/basic-probability/index.html)

---

## 16. Linear Algebra Basics: Dot Products, Matrix Multiplication and Solving Equations

![Matrix multiplication: entry (i, j) of A @ B is row i of A dotted with column j of B](images/data-science/16-matmul.svg)

### Theory

> **In simple words:** linear algebra is the maths of **vectors** (lists of numbers) and **matrices** (tables of numbers). Its core move is the **dot product**: multiply matching pairs and add them up. Matrix multiplication is many dot products at once, and it's the single most important calculation in machine learning.

**Words to know:**

- **Vector:** an ordered list of numbers, like `[height, weight]`. Can be drawn as an arrow from the origin.
- **Matrix:** a rectangular grid of numbers with `m` rows and `n` columns, shape `(m, n)`.
- **Dot product (`a @ b` for vectors):** `a₁b₁ + a₂b₂ + … + aₙbₙ`. A single number measuring how much two vectors point the same way.
- **Norm (length, magnitude):** a vector's length, √(a₁² + a₂² + …). `np.linalg.norm(a)`.
- **Cosine similarity:** the dot product divided by both lengths: 1 = same direction, 0 = unrelated (perpendicular), −1 = opposite. Used to compare text **embeddings** in AI search.
- **Matrix multiplication (`A @ B`):** entry `(i, j)` of the result is row `i` of `A` dotted with column `j` of `B`. Needs `A`'s column count to equal `B`'s row count.
- **Linear equation system:** several equations like `2x + y = 5`, `x + 3y = 10`, solved together.
- **Inverse (A⁻¹):** the matrix that "undoes" `A`: `A⁻¹ @ A` is the identity matrix. Not every matrix has one.
- **Determinant:** a single number computed from a square matrix; if it's 0, the matrix has no inverse (the equations have no single solution).
- **Eigenvector / eigenvalue:** a direction that a matrix only stretches (doesn't rotate), and the stretch factor. Used by PCA (`machine-learning.md`).
- **Embedding:** a list of numbers (a vector) that represents the meaning of a word, sentence, image or product, so that similar things get similar vectors.
- **Neural network:** a model built from layers of simple units, each computing weighted sums (matrix multiplications) followed by an activation function (`deep-learning.md`).

**Everyday picture.** A shopping list `[2 kg rice, 3 L milk]` dotted with a price list `[60, 50]` gives the bill: 2×60 + 3×50 = 270. Matrix multiplication is pricing **several** shopping lists (rows of one matrix) against **several** shops' price lists (columns of another) all at once.

**Dot product, traced:** `[1, 2, 3] @ [4, 5, 6]` = 1×4 + 2×5 + 3×6 = 4 + 10 + 18 = **32**.

**Matrix multiplication, traced** for `A = [[2, 1], [1, 3]]` and `B = [[1, 0], [2, 1]]`:

| Entry | Row of A | Column of B | Dot product |
|---|---|---|---|
| (0, 0) | [2, 1] | [1, 2] | 2×1 + 1×2 = **4** |
| (0, 1) | [2, 1] | [0, 1] | 2×0 + 1×1 = **1** |
| (1, 0) | [1, 3] | [1, 2] | 1×1 + 3×2 = **7** |
| (1, 1) | [1, 3] | [0, 1] | 1×0 + 3×1 = **3** |

So `A @ B = [[4, 1], [7, 3]]`. **The shape rule:** `(m, n) @ (n, p) → (m, p)`; the inner sizes must match and disappear. Order matters: `A @ B` is usually not `B @ A`.

**`*` vs `@`:** `A * B` multiplies **matching positions** (element-wise): `[[2, 0], [2, 3]]` here. `A @ B` is matrix multiplication. Mixing them up is one of the most common bugs in numerical code.

**Solving equations:** `2x + y = 5` and `x + 3y = 10` is `A @ [x, y] = b` with `A = [[2, 1], [1, 3]]` and `b = [5, 10]`. `np.linalg.solve(A, b)` returns `[1, 3]` (check: 2×1 + 3 = 5 ✓, 1 + 3×3 = 10 ✓). Prefer `solve` to `inv(A) @ b`: it's faster and more accurate.

**Why ML engineers care:**

| ML idea | The linear algebra |
|---|---|
| A dataset | a matrix `X` of shape `(samples, features)` |
| Linear regression's prediction | `X @ w + b` (one dot product per row) |
| A neural-network layer | `inputs @ weights + bias`, then an activation |
| Comparing documents, images, songs | cosine similarity of embedding vectors |
| PCA (compressing features) | eigenvectors of the covariance matrix, via `np.linalg.eigh` or SVD |
| Least-squares fitting | `np.linalg.lstsq(X, y)` |

**The `np.linalg` toolbox:** `norm`, `solve`, `inv`, `det`, `eig` / `eigh` (eigen decomposition; `eigh` for symmetric matrices), `svd` (singular value decomposition: splits any matrix into rotation × stretch × rotation), `lstsq` (best fit when there are more equations than unknowns), `matrix_rank`.

**Common mistakes:**

- ❌ `A * B` when you meant `A @ B`.
- ❌ Shape mismatch in `@`. ✅ Write the shapes down: `(m, n) @ (n, p)`; print `.shape` often.
- ❌ `np.linalg.inv(A) @ b`. ✅ `np.linalg.solve(A, b)`.
- ❌ Comparing vectors of very different lengths with the raw dot product. ✅ Normalise (cosine similarity) when only direction matters.

**Used in real software:** every neural network (GPUs are, at heart, very fast matrix-multiplication machines); search engines and RAG systems ranking documents by cosine similarity of embeddings (`rag-and-agents.md`); recommender systems (user vectors dotted with item vectors); 3D graphics (rotation matrices).

### Python

```python
import numpy as np

u, v = np.array([1, 2, 3]), np.array([4, 5, 6])
print(u @ v, np.dot(u, v), (u * v).sum())                # three ways to the same dot product: 32
print(np.linalg.norm(u).round(4), np.sqrt((u ** 2).sum()).round(4))
cos = (u @ v) / (np.linalg.norm(u) * np.linalg.norm(v))
print(round(float(cos), 4))

def cosine(a, b):
    return float(a @ b / (np.linalg.norm(a) * np.linalg.norm(b)))

cat, kitten, car = np.array([0.9, 0.8, 0.1]), np.array([0.85, 0.75, 0.2]), np.array([0.1, 0.2, 0.95])
print(f"cat~kitten {cosine(cat, kitten):.3f}   cat~car {cosine(cat, car):.3f}")   # toy "embeddings"
```

**Output:**

```text
32 32 32
3.7417 3.7417
0.9746
cat~kitten 0.996   cat~car 0.293
```

```python
A = np.array([[2, 1], [1, 3]])
B = np.array([[1, 0], [2, 1]])
print(A @ B, B @ A, A * B, sep="\n")                     # @ is not commutative; * is element-wise

print(np.linalg.solve(A, np.array([5, 10])))             # 2x + y = 5, x + 3y = 10
print(np.linalg.det(A).round(6), (np.linalg.inv(A) @ A).round(10) + 0.0)   # det 5 ≠ 0, so an inverse exists

X = np.array([[1.0, 0.5, 2.0], [0.0, 1.0, 1.0], [2.0, 2.0, 0.0], [1.0, 1.0, 1.0]])   # 4 samples × 3 features
W = np.array([[0.1, -0.2], [0.4, 0.3], [-0.5, 0.2]])                                # 3 inputs → 2 outputs
b = np.array([0.01, 0.02])
out = X @ W + b                                          # one neural-network layer (before activation)
print(out.round(2), out.shape)
```

**Output:**

```text
[[4 1]
 [7 3]]
[[2 1]
 [5 5]]
[[2 0]
 [2 3]]
[1. 3.]
5.0 [[1. 0.]
 [0. 1.]]
[[-0.69  0.37]
 [-0.09  0.52]
 [ 1.01  0.22]
 [ 0.01  0.32]] (4, 2)
```

```python
# Least squares: the best straight line y ≈ w*x + c through noisy points
x = np.array([1, 2, 3, 4, 5], dtype=float)
y = np.array([2.1, 3.9, 6.2, 7.8, 10.1])
design = np.column_stack([x, np.ones_like(x)])           # columns: x, 1  (shape (5, 2))
(w, c), *_ = np.linalg.lstsq(design, y)
print(f"y ≈ {w:.3f}·x + {c:.3f}")

S = np.array([[2.0, 1.0], [1.0, 2.0]])                   # a symmetric matrix
vals, vecs = np.linalg.eigh(S)
print(vals, vecs.round(3), sep="\n")
print(np.allclose(S @ vecs[:, 1], vals[1] * vecs[:, 1])) # S only stretches its eigenvector
```

**Output:**

```text
y ≈ 1.990·x + 0.050
[1. 3.]
[[-0.707  0.707]
 [ 0.707  0.707]]
True
```

`(inv(A) @ A).round(10)` hides tiny floating-point leftovers such as `-5.55e-17` (that is −0.0000000000000000555): computed results are rarely *exactly* 0 or 1, which is why `np.allclose` exists. `np.column_stack` builds a matrix from 1D columns. The eigenvector check shows the definition in action: multiplying by `S` gives the same direction, scaled by the eigenvalue 3.

### Practice

1. Compute the cosine similarity between `[1, 0, 1]` and `[0, 1, 1]` by hand, then check with NumPy.
2. Solve `x + y + z = 6`, `2y + 5z = −4`, `2x + 5y − z = 27`.
3. What shape is `(10, 4) @ (4, 3) @ (3, 1)`? Check with `np.ones`.

<details>
<summary><b>Answer</b></summary>

```python
p, q = np.array([1, 0, 1]), np.array([0, 1, 1])
print(round(cosine(p, q), 3))                            # dot 1, lengths √2 and √2 → 1/2
A3 = np.array([[1, 1, 1], [0, 2, 5], [2, 5, -1]])
print(np.linalg.solve(A3, np.array([6, -4, 27])))
print((np.ones((10, 4)) @ np.ones((4, 3)) @ np.ones((3, 1))).shape)
```

**Output:**

```text
0.5
[ 5.  3. -2.]
(10, 1)
```

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [83. Dot Product Calculator](https://www.deep-ml.com/problems/83) | 🟢 Easy |
| 2 | [1. Matrix-Vector Dot Product](https://www.deep-ml.com/problems/1) | 🟢 Easy |
| 3 | [76. Calculate Cosine Similarity Between Vectors](https://www.deep-ml.com/problems/76) | 🟢 Easy |
| 4 | [8. Calculate 2x2 Matrix Inverse](https://www.deep-ml.com/problems/8) | 🟢 Easy |
| 5 | [195. Matrix Determinant & Trace](https://www.deep-ml.com/problems/195) | 🟢 Easy |
| 6 | [9. Matrix times Matrix](https://www.deep-ml.com/problems/9) | 🟡 Medium |
| 7 | [6. Calculate Eigenvalues of a Matrix](https://www.deep-ml.com/problems/6) | 🟡 Medium |
| 8 | [58. Gaussian Elimination for Solving Linear Systems](https://www.deep-ml.com/problems/58) | 🟡 Medium |
| 9 | [12. Singular Value Decomposition (SVD) of 2x2 Matrix](https://www.deep-ml.com/problems/12) | 🔴 Hard |

**Learn more:** [3Blue1Brown: Essence of linear algebra (videos)](https://www.3blue1brown.com/topics/linear-algebra) · [NumPy: linear algebra](https://numpy.org/doc/stable/reference/routines.linalg.html)

---

### ✅ Part 2 checkpoint

Without looking, can you:

- [ ] Explain why a NumPy array is faster and smaller than a list of the same numbers?
- [ ] Create arrays with `array`, `arange`, `linspace`, `zeros` and `full`, and say when `linspace` beats `arange`?
- [ ] Read an array's `shape`, `ndim`, `size` and `dtype`, and predict upcasting and overflow?
- [ ] Index rows, columns and blocks of a 2D array, and say which operations return views and which return copies?
- [ ] Filter with a boolean mask using `&`, `|` and `~`, and build labels with `np.where` and `np.select`?
- [ ] Aggregate along `axis=0` and `axis=1` and say what shape you'll get?
- [ ] Decide whether two shapes broadcast, and standardise the columns of a matrix in one line?
- [ ] Reshape, transpose, stack and sort one array by another with `argsort`?
- [ ] Use a seeded `default_rng` to simulate a probability and compare it with the exact answer?
- [ ] Compute a dot product and a matrix product by hand, and explain the difference between `*` and `@`?

NumPy handles numbers brilliantly, but real data is a **table** with names, dates and text in labelled columns. Part 3 introduces **pandas**, which builds labelled tables on top of NumPy arrays.

---

# Part 3 — Easy: pandas Basics, Working with Tables

> **Goal:** Load any table into pandas, inspect it, pull out exactly the rows and columns you need, sort it, add new columns, and write clean multi-step pipelines.  
> **You need:** Parts 1–2.

**About the LeetCode problems from here on.** LeetCode's pandas track gives you each table as a DataFrame argument to a function, and you `return` a DataFrame. For example:

```text
import pandas as pd

def big_countries(world: pd.DataFrame) -> pd.DataFrame:
    return world.loc[(world["area"] >= 3_000_000) | (world["population"] >= 25_000_000),
                     ["name", "population", "area"]]
```

Choose **Pandas** in the language menu. Read the expected output carefully: column names and order matter.

---

## 17. pandas Series: Labelled 1D Data

![A Series is a NumPy array of values plus an index of labels; operations line up by label](images/data-science/17-series.svg)

### Theory

> **In simple words:** a **Series** is a NumPy array with a **label on every value**. You can get values by label (`s["Pune"]`) or position, and when you combine two Series, pandas **lines them up by label**, not by position.

**Words to know:**

- **pandas:** the library for labelled tables in Python (the name comes from "panel data"). Imported as `pd`.
- **Series:** one column of data: values of one type, plus an **index**.
- **Index:** the labels for the rows. By default 0, 1, 2, …; can be names, dates, IDs.
- **Label:** one entry of the index, like `"Pune"` or a date.
- **Alignment:** matching values by label before combining them. Labels missing on one side give `NaN`.
- **`NaN` / missing value:** pandas' marker for "no value here". (`NA`/`<NA>` is a newer missing marker used by some types; Section [26](#26-missing-values-finding-dropping-and-filling) covers both.)
- **Vectorised (again):** Series maths works on all values at once, like NumPy.
- **Method:** a function attached to an object, called with a dot: `s.mean()`.

**Everyday picture.** A NumPy array is a row of **unlabelled jars**; a Series is the same jars with **name tags**. When you combine two shelves of tagged jars, you pour "sugar" into "sugar", even if the shelves list them in a different order. A jar with no partner on the other shelf ends up empty (`NaN`).

**Alignment, traced by hand:**

| Label | `s1` | `s2` | `s1 + s2` |
|---|---|---|---|
| Delhi | 90 | (missing) | NaN |
| Mumbai | 120 | 30 | 150 |
| Pune | 100 | 20 | 120 |
| Goa | (missing) | 10 | NaN |

Even if `s2` lists Pune first, the Pune values meet each other. That's different from NumPy, which pairs by **position**. Use `s1.add(s2, fill_value=0)` to treat missing labels as 0 instead of producing NaN.

**Getting values:**

| Code | Picks |
|---|---|
| `s["Pune"]`, `s.loc["Pune"]` | by label |
| `s.iloc[0]` | by position (first value) |
| `s[s > 100]` | by a boolean mask, as in NumPy |
| `s.index`, `s.values` / `s.to_numpy()` | the labels; the underlying array |

**Everyday Series methods:** `sum`, `mean`, `median`, `min`, `max`, `idxmax` (the **label** of the max; `argmax` gives the position), `value_counts()` (how often each value appears), `unique()`, `nunique()`, `sort_values()`, `sort_index()`, `head(n)`, `round(n)`, `describe()`, `isna()`, `astype(type)`.

**When to use a Series:** whenever one column is enough, a lookup table (label → value), or a result like "revenue per city". You'll mostly get Series by picking a column from a DataFrame (next section).

**Common mistakes:**

- ❌ Expecting position-based pairing like NumPy and getting NaN from label mismatches. ✅ Check indexes, or use `.to_numpy()` when you truly want positional maths.
- ❌ `s[0]` to mean "the first value". In pandas 3, square brackets with an integer always look for the **label** `0`, so on a text-labelled Series it raises `KeyError` (older pandas silently fell back to position). ✅ Be explicit: `s.iloc[0]` for position, `s.loc[label]` for label.
- ❌ Confusing `idxmax` (the label) with `argmax` (the position).

**Used in real software:** time series (a Series indexed by dates: stock prices, daily users); lookup tables used with `.map` (Section [24](#24-adding-and-changing-columns-arithmetic-assign-map-apply-and-npselect)); every DataFrame column you'll ever touch.

### Python

```python
import pandas as pd

sales = pd.Series([100, 120, 90], index=["Pune", "Mumbai", "Delhi"], name="sales")
print(sales)
print(sales["Mumbai"], sales.iloc[0], sales[sales > 95].index.tolist())
print(sales.mean().round(2), sales.idxmax(), sales.sort_values(ascending=False).index.tolist())

returns = pd.Series({"Pune": 20, "Mumbai": 30, "Goa": 10})    # a dict becomes label → value
print(sales - returns)                                       # aligned by label: Delhi and Goa → NaN
print(sales.sub(returns, fill_value=0))                      # treat missing as 0
```

**Output:**

```text
Pune      100
Mumbai    120
Delhi      90
Name: sales, dtype: int64
120 100 ['Pune', 'Mumbai']
103.33 Mumbai ['Mumbai', 'Pune', 'Delhi']
Delhi      NaN
Goa        NaN
Mumbai    90.0
Pune      80.0
dtype: float64
Delhi     90.0
Goa      -10.0
Mumbai    90.0
Pune      80.0
dtype: float64
```

```python
colours = pd.Series(["red", "blue", "red", "green", "red", "blue"])
print(colours.value_counts())
print(colours.nunique(), colours.unique().tolist())
print((colours == "red").mean())                            # fraction that are red
print(pd.Series([3.14159, 2.71828]).round(2).tolist(), colours.str.upper().tolist()[:3])
```

**Output:**

```text
red      3
blue     2
green    1
Name: count, dtype: int64
3 ['red', 'blue', 'green']
0.5
[3.14, 2.72] ['RED', 'BLUE', 'RED']
```

`.str` applies text methods to every value (Section [28](#28-text-data-the-str-accessor-and-regular-expressions)). `value_counts` returns a Series whose index is the distinct values, sorted by count.

### Practice

1. Make a Series of 5 students' marks indexed by name. Print the top scorer's name, the average, and the names of everyone above the average.
2. Two shops' stock: `a = pd.Series({"pen": 10, "ink": 5})`, `b = pd.Series({"ink": 3, "pad": 7})`. Compute total stock per item, with missing items counting as 0.

<details>
<summary><b>Answer</b></summary>

```python
marks = pd.Series([72, 88, 95, 60, 81], index=["Asha", "Ravi", "Zoya", "Kabir", "Meera"])
print(marks.idxmax(), marks.mean(), marks[marks > marks.mean()].index.tolist())
a, b = pd.Series({"pen": 10, "ink": 5}), pd.Series({"ink": 3, "pad": 7})
print(a.add(b, fill_value=0))
```

**Output:**

```text
Zoya 79.2 ['Ravi', 'Zoya', 'Meera']
ink     8.0
pad     7.0
pen    10.0
dtype: float64
```

</details>

**Learn more:** [pandas: intro to data structures (Series)](https://pandas.pydata.org/docs/user_guide/dsintro.html#series)

---

## 18. DataFrames: Creating, Inspecting and Understanding a Table

![A DataFrame is a table of columns (Series) sharing one row index](images/data-science/03-dataframe.svg)

### Theory

> **In simple words:** a **DataFrame** is pandas' table: rows and named columns, like a spreadsheet or a SQL table, controlled from code. Every column is a Series (one type per column), and all columns share the same row index.

**Words to know:**

- **DataFrame:** a 2D labelled table: rows × columns.
- **Columns:** the column labels (`df.columns`). **Index:** the row labels (`df.index`).
- **dtype per column:** each column has its own type. pandas 3's main types: `int64`, `float64`, `bool`, `str` (text), `datetime64` (dates and times), `category` (repeated labels, Section [29](#29-categorical-data-and-binning-cut-and-qcut)).
- **`str` dtype (pandas 3):** the new default type for text columns. Older pandas stored text in the catch-all `object` type; you'll still see `object` for mixed or unusual values.
- **Summary statistics:** numbers that describe a column: count, mean, standard deviation, min, quartiles, max.
- **Quartiles (25%, 50%, 75%):** the values that cut sorted data into four equal parts. The 50% quartile is the median.
- **Non-null count:** how many values in a column are not missing.
- **Streamlit:** a Python library that turns a script into an interactive web app with charts and filters (Section [63](#63-communicating-results-reports-dashboards-and-data-storytelling)).

**Everyday picture.** A DataFrame is a spreadsheet where every column has a **fixed type** (no mixing a date into the price column) and where both rows and columns have names you can use in code.

**Ways to create a DataFrame:**

| From | Code |
|---|---|
| A dict of columns | `pd.DataFrame({"name": [...], "price": [...]})` |
| A list of dicts (records, e.g. from JSON) | `pd.DataFrame([{"name": "Pen", "price": 15}, ...])` |
| A list of lists + column names | `pd.DataFrame(rows, columns=["name", "price"])` |
| A NumPy array | `pd.DataFrame(arr, columns=[...])` |
| A file or database | `pd.read_csv(...)`, `pd.read_parquet(...)`, `pd.read_sql(...)` (Sections [19](#19-reading-and-writing-files-csv-excel-json-and-parquet)–[20](#20-reading-from-databases-and-web-apis)) |

**The first five minutes with any DataFrame** (do this every time, before any analysis):

| Code | Tells you | Look for |
|---|---|---|
| `df.shape` | (rows, columns) | is the size what you expected? |
| `df.head()`, `df.tail(3)`, `df.sample(5)` | some rows | does it look like the data you think it is? |
| `df.info()` | each column's type, non-null count, memory | numbers stored as text; unexpected missing values |
| `df.describe()` | summary statistics of numeric columns | impossible values (negative prices, age 200) |
| `df.describe(include="str")` | count, distinct values, most common value of text columns | typos (`Pune` vs `pune`) |
| `df["col"].value_counts()` | frequency of each value | rare or misspelled categories |
| `df.isna().sum()` | missing values per column | columns that are mostly empty |
| `df.duplicated().sum()` | fully duplicated rows | accidental double loading |

**Index basics:** `df.set_index("order_id")` makes a column the row labels (fast lookups with `.loc`); `df.reset_index()` moves the index back into a normal column. Many operations (groupby results, Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine)) put keys into the index, so you'll use `reset_index` often.

**Renaming and tidying the layout:** `df.rename(columns={"qty": "quantity"})`, `df.columns = [...]`, `df[["b", "a"]]` to reorder, `df.drop(columns=["tmp"])` to remove.

**When a DataFrame is the right tool:** almost any tabular data that fits in memory (up to a few GB comfortably). **When it isn't:** data far bigger than memory (Part 6: chunking, Polars, DuckDB), or deeply nested data that isn't a table.

**Common mistakes:**

- ❌ Starting analysis before looking at `info()` and `describe()`. ✅ Always do the five-minute check.
- ❌ Forgetting that most methods **return a new DataFrame**: `df.rename(...)` alone changes nothing. ✅ `df = df.rename(...)`.
- ❌ Building a DataFrame row by row in a loop with `pd.concat` (very slow). ✅ Collect a list of dicts, then make the DataFrame once.

**Used in real software:** pandas DataFrames are the standard input to scikit-learn, Seaborn, statsmodels and many dashboards; tools like Streamlit display them directly; most data APIs and notebooks hand you one.

### Python

The rest of these notes use this small shop dataset, the **orders** table, so you can focus on the method, not the data:

```python
import io
import pandas as pd

csv_text = """order_id,date,customer,city,product,category,qty,price
1,2025-01-05,Asha,Pune,Notebook,stationery,5,60
2,2025-01-06,Ravi,Mumbai,Headphones,electronics,1,2500
3,2025-02-10,Asha,Pune,Backpack,bags,1,1200
4,2025-02-11,Meera,Pune,Keyboard,electronics,1,1800
5,2025-03-02,Zoya,Mumbai,Water bottle,kitchen,2,350
6,2025-03-15,Kabir,Bengaluru,Desk lamp,electronics,1,900
7,2025-03-20,Asha,Pune,Headphones,electronics,1,2500
8,2025-04-01,Isha,Delhi,Mug,kitchen,4,250
9,2025-04-18,Ravi,Mumbai,Notebook,stationery,10,60
10,2025-05-05,Zoya,Mumbai,Keyboard,electronics,1,1800
"""
orders = pd.read_csv(io.StringIO(csv_text), parse_dates=["date"])
print(orders.shape)
print(orders.head(3))
orders.info()
```

**Output:**

```text
(10, 8)
   order_id       date customer    city     product     category  qty  price
0         1 2025-01-05     Asha    Pune    Notebook   stationery    5     60
1         2 2025-01-06     Ravi  Mumbai  Headphones  electronics    1   2500
2         3 2025-02-10     Asha    Pune    Backpack         bags    1   1200
<class 'pandas.DataFrame'>
RangeIndex: 10 entries, 0 to 9
Data columns (total 8 columns):
 #   Column    Non-Null Count  Dtype         
---  ------    --------------  -----         
 0   order_id  10 non-null     int64         
 1   date      10 non-null     datetime64[us]
 2   customer  10 non-null     str           
 3   city      10 non-null     str           
 4   product   10 non-null     str           
 5   category  10 non-null     str           
 6   qty       10 non-null     int64         
 7   price     10 non-null     int64         
dtypes: datetime64[us](1), int64(3), str(4)
memory usage: 1.0 KB
```

**Display tip:** pandas hides middle columns with `...` when a table is wider than its display setting. These notes print with `pd.set_option("display.width", 120)` and `pd.set_option("display.max_columns", 20)`; run those two lines once at the top of your notebook to see the same output.

`io.StringIO(text)` makes a string behave like a file, so the example needs no download; with a real file you'd write `pd.read_csv("orders.csv", parse_dates=["date"])`. In `info()`, `datetime64[us]` means dates stored to the microsecond.

```python
print(orders.describe().round(1))
print(orders.describe(include="str"))
print(orders["city"].value_counts())
print(orders.isna().sum().sum(), orders.duplicated().sum())        # no missing values, no duplicate rows
```

**Output:**

```text
       order_id                 date   qty   price
count      10.0                   10  10.0    10.0
mean        5.5  2025-03-04 04:48:00   2.7  1142.0
min         1.0  2025-01-05 00:00:00   1.0    60.0
25%         3.2  2025-02-10 06:00:00   1.0   275.0
50%         5.5  2025-03-08 12:00:00   1.0  1050.0
75%         7.8  2025-03-29 00:00:00   3.5  1800.0
max        10.0  2025-05-05 00:00:00  10.0  2500.0
std         3.0                  NaN   2.9   965.0
       customer  city   product     category
count        10    10        10           10
unique        6     4         7            4
top        Asha  Pune  Notebook  electronics
freq          3     4         2            5
city
Pune         4
Mumbai       4
Bengaluru    1
Delhi        1
Name: count, dtype: int64
0 0
```

In the text summary, `top` is the most common value and `freq` how often it appears. `describe()` on numbers shows `qty` is mostly 1 with a maximum of 10: worth a look later.

```python
products = pd.DataFrame([{"product": "Pen", "price": 15.5, "stock": 500},
                         {"product": "Mug", "price": 250.0, "stock": 80}])     # from records
print(products, products.dtypes, sep="\n")

by_id = orders.set_index("order_id")
print(by_id.loc[7, ["customer", "product"]].tolist())
print(by_id.reset_index().columns.tolist()[:3])
print(orders.rename(columns={"qty": "quantity"}).columns.tolist())
```

**Output:**

```text
  product  price  stock
0     Pen   15.5    500
1     Mug  250.0     80
product        str
price      float64
stock        int64
dtype: object
['Asha', 'Headphones']
['order_id', 'date', 'customer']
['order_id', 'date', 'customer', 'city', 'product', 'category', 'quantity', 'price']
```

### Practice

1. Build a DataFrame of 4 students with `name`, `maths` and `science`. Print its shape, its dtypes and the average of each subject.
2. On `orders`, answer with one line each: how many distinct customers are there? Which product appears most often?

<details>
<summary><b>Answer</b></summary>

```python
students = pd.DataFrame({"name": ["Asha", "Ravi", "Meera", "Arjun"],
                         "maths": [88, 72, 95, 60], "science": [79, 85, 91, 70]})
print(students.shape, students.dtypes.astype(str).to_dict(), students[["maths", "science"]].mean().to_dict())
print(orders["customer"].nunique(), orders["product"].value_counts().idxmax())
```

**Output:**

```text
(4, 3) {'name': 'str', 'maths': 'int64', 'science': 'int64'} {'maths': 78.75, 'science': 81.25}
6 Notebook
```

`value_counts()` sorts by count, and ties keep the order of first appearance, so `Notebook` (first seen in row 0) wins the tie with `Headphones` and `Keyboard`.

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [2877. Create a DataFrame from List](https://leetcode.com/problems/create-a-dataframe-from-list/) | 🟢 Easy |
| 2 | [2878. Get the Size of a DataFrame](https://leetcode.com/problems/get-the-size-of-a-dataframe/) | 🟢 Easy |
| 3 | [2879. Display the First Three Rows](https://leetcode.com/problems/display-the-first-three-rows/) | 🟢 Easy |
| 4 | [2885. Rename Columns](https://leetcode.com/problems/rename-columns/) | 🟢 Easy |

**Learn more:** [pandas: 10 minutes to pandas](https://pandas.pydata.org/docs/user_guide/10min.html) · [Kaggle Learn: pandas (free course)](https://www.kaggle.com/learn/pandas)

---

## 19. Reading and Writing Files: CSV, Excel, JSON and Parquet

![Row-based CSV versus column-based Parquet: Parquet stores each column together, compressed and with its type](images/data-science/19-csv-vs-parquet.svg)

### Theory

> **In simple words:** pandas has a `read_…` function for every common file format that turns it into a DataFrame, and a matching `to_…` method to write one out. CSV is universal but slow and forgets types; **Parquet** is the modern format for analytics: small, fast, and it remembers every column's type.

**Words to know:**

- **Excel file (`.xlsx`):** a spreadsheet file; can have several **sheets** (tabs). pandas reads it with the `openpyxl` library.
- **Parquet:** a **columnar** file format: values of each column are stored together, compressed, with the column's type. Created for big-data systems (Hadoop, Spark) and now standard everywhere.
- **Columnar vs row-based:** a row-based file (CSV) stores row 1, then row 2, …; a columnar file stores all of column 1, then all of column 2, … Reading three columns of a columnar file skips the rest of the file.
- **Compression:** storing data in fewer bytes by encoding patterns (a column of "Pune, Pune, Pune" compresses extremely well).
- **Schema:** the column names and types, which Parquet stores inside the file.
- **Feather / Arrow IPC:** another fast binary format, good for passing data between programs; Parquet is better for storage.
- **Chunk:** a piece of a big file read at a time.
- **`NA` markers:** strings that mean "missing", like `""`, `"NA"`, `"n/a"`, `"-"`.
- **Hadoop:** an older open-source system for storing and processing big data across many computers; Parquet was created in its ecosystem.
- **Cloud object storage (S3):** pay-as-you-go online file storage (Amazon S3, Google Cloud Storage, Azure Blob) where data lakes keep their files.

**Everyday picture.** A CSV is a **handwritten ledger**: anyone can read it, but you have to re-read every line to add up one column, and "01234" might be copied as 1234. Parquet is a **filing cabinet with one drawer per column**, each drawer labelled with its type and packed tight: to total the prices, open one drawer.

**Formats at a glance:**

| Format | Read | Write | Strengths | Weaknesses |
|---|---|---|---|---|
| CSV | `pd.read_csv` | `df.to_csv(path, index=False)` | universal, human-readable | slow, big, **loses types** (dates, leading zeros) |
| Excel | `pd.read_excel(path, sheet_name=...)` | `df.to_excel(path, index=False)` | business users live in it | slow, row limit ~1M, formatting surprises |
| JSON | `pd.read_json(path)` (`lines=True` for JSON Lines) | `df.to_json(path, orient="records")` | APIs, logs, nested data | verbose; nesting needs flattening (Section [20](#20-reading-from-databases-and-web-apis)) |
| **Parquet** | `pd.read_parquet(path, columns=[...])` | `df.to_parquet(path)` | small, fast, typed, read only some columns | binary (not human-readable) |
| Feather | `pd.read_feather` | `df.to_feather` | very fast round-trips | less common for long-term storage |
| Pickle | `pd.read_pickle` | `df.to_pickle` | exact Python objects | **unsafe** to load from untrusted sources; Python-only |

**The `read_csv` options you'll actually use:**

| Option | Does |
|---|---|
| `sep=";"` | a different delimiter (`"\t"` for TSV) |
| `usecols=["a", "b"]` | load only these columns (saves time and memory) |
| `dtype={"zip": "str"}` | force a type (keeps leading zeros) |
| `parse_dates=["date"]` | turn text into real dates |
| `na_values=["-", "n/a"]` | extra markers for missing values |
| `nrows=1000` | peek at the start of a huge file |
| `skiprows=2`, `header=None`, `names=[...]` | files with junk lines or no header |
| `chunksize=100_000` | read in pieces (Section [40](#40-memory-dtypes-categoricals-chunking-and-apache-arrow)) |
| `encoding="utf-8"` (or `"latin-1"`) | text encoding |
| `thousands=","`, `decimal=","` | numbers like `1,200` or European `3,5` |

**Why Parquet wins for analysis, step by step:** (1) types are stored, so no re-parsing and no lost zeros; (2) each column is compressed separately, often 5–10× smaller than CSV; (3) `columns=[...]` reads only what you need; (4) every big-data tool (Spark, DuckDB, Polars, BigQuery, Snowflake) reads it. **Habit:** receive a CSV once, clean it, save it as Parquet, and work from the Parquet.

**When to use which:** CSV to exchange with people and tools that only speak CSV; Excel for business users; JSON for APIs and logs; Parquet for everything you store for analysis.

**Common mistakes:**

- ❌ `to_csv(path)` without `index=False`, then a mystery `Unnamed: 0` column appears on reading back.
- ❌ Forgetting `parse_dates`, so dates stay as text and sort wrongly ("10/1" before "9/1").
- ❌ IDs like ZIP or phone codes read as numbers, losing leading zeros. ✅ `dtype={"zip": "str"}`.
- ❌ Loading a 10 GB CSV to use three columns. ✅ `usecols`, chunks, or convert to Parquet once.
- ❌ `read_pickle` on a file from the internet (it can run arbitrary code). ✅ Parquet.

**Used in real software:** data lakes on S3 or Google Cloud Storage are mostly Parquet files; Kaggle datasets usually ship as CSV; analytics engineers export Parquet from warehouses; logging systems write JSON Lines.

### Python

```python
import io, os, tempfile
import pandas as pd

csv_text = """order_id,date,customer,city,product,category,qty,price
1,2025-01-05,Asha,Pune,Notebook,stationery,5,60
2,2025-01-06,Ravi,Mumbai,Headphones,electronics,1,2500
3,2025-02-10,Asha,Pune,Backpack,bags,1,1200
4,2025-02-11,Meera,Pune,Keyboard,electronics,1,1800
5,2025-03-02,Zoya,Mumbai,Water bottle,kitchen,2,350
"""
orders = pd.read_csv(io.StringIO(csv_text), parse_dates=["date"])

folder = tempfile.mkdtemp()
csv_path, pq_path = os.path.join(folder, "orders.csv"), os.path.join(folder, "orders.parquet")
orders.to_csv(csv_path, index=False)
orders.to_parquet(pq_path)

print(pd.read_csv(csv_path).dtypes["date"], "<- CSV forgot the date type")
print(pd.read_parquet(pq_path).dtypes["date"], "<- Parquet remembered it")
print(pd.read_parquet(pq_path, columns=["customer", "price"]).head(2))
print(pd.read_csv(csv_path, usecols=["city", "qty"], nrows=2))
```

**Output:**

```text
str <- CSV forgot the date type
datetime64[us] <- Parquet remembered it
  customer  price
0     Asha     60
1     Ravi   2500
     city  qty
0    Pune    5
1  Mumbai    1
```

```python
messy = """id;zip;amount;note
1;01234;1.200,50;ok
2;-;3,75;n/a
"""
df = pd.read_csv(io.StringIO(messy), sep=";", dtype={"zip": "str"}, na_values=["-", "n/a"],
                 thousands=".", decimal=",")
print(df, df.dtypes, sep="\n")

big = pd.concat([orders] * 2000, ignore_index=True)        # 10,000 rows to compare sizes
big.to_csv(csv_path, index=False); big.to_parquet(pq_path)
print(f"CSV {os.path.getsize(csv_path) / 1e3:.0f} KB vs Parquet {os.path.getsize(pq_path) / 1e3:.0f} KB")

json_path = os.path.join(folder, "orders.jsonl")
orders.head(2).to_json(json_path, orient="records", lines=True, date_format="iso")
print(open(json_path).read())
print(pd.read_json(json_path, lines=True).shape)
```

**Output:**

```text
   id    zip   amount note
0   1  01234  1200.50   ok
1   2    NaN     3.75  NaN
id          int64
zip           str
amount    float64
note          str
dtype: object
CSV 502 KB vs Parquet 7 KB
{"order_id":1,"date":"2025-01-05T00:00:00.000","customer":"Asha","city":"Pune","product":"Notebook","category":"stationery","qty":5,"price":60}
{"order_id":2,"date":"2025-01-06T00:00:00.000","customer":"Ravi","city":"Mumbai","product":"Headphones","category":"electronics","qty":1,"price":2500}

(2, 8)
```

This copy-pasted table compresses unusually well because the same 5 rows repeat; real data is typically 5–10× smaller as Parquet. The European-style file used `;` between values, `.` for thousands and `,` for decimals; the right options read `1.200,50` as 1200.5 and kept the ZIP code's leading zero. (`pd.concat([orders] * 2000)` stacks 2,000 copies to make a bigger table; Section [34](#34-combining-tables-ii-concat-validation-and-merge-pitfalls) covers `concat`.)

### Practice

1. Read the orders CSV text with only the `customer` and `qty` columns. How many rows and columns did you load, and what's the total quantity?
2. A file uses tabs between values and writes missing values as `?`. Write the `read_csv` call.

<details>
<summary><b>Answer</b></summary>

```python
small = pd.read_csv(io.StringIO(csv_text), usecols=["customer", "qty"])
print(small.shape, small["qty"].sum())
```

**Output:**

```text
(5, 2) 10
```

2. `pd.read_csv(path, sep="\t", na_values=["?"])`.

</details>

**Learn more:** [pandas: IO tools](https://pandas.pydata.org/docs/user_guide/io.html) · [Apache Parquet: overview](https://parquet.apache.org/docs/overview/)

---

## 20. Reading from Databases and Web APIs

![Push filtering and aggregation into SQL; load only the small result into pandas](images/data-science/20-sql-to-pandas.svg)

### Theory

> **In simple words:** a lot of data lives in **databases** (ask with SQL) or behind **web APIs** (ask over HTTP and get JSON back). pandas can run a SQL query and give you the result as a DataFrame, and can flatten nested JSON into a table.

**Words to know:**

- **Database:** a program that stores tables and answers questions about them (PostgreSQL, MySQL, SQLite, BigQuery, Snowflake).
- **SQL (Structured Query Language):** the language for asking databases questions: `SELECT city, SUM(price) FROM orders GROUP BY city`. Taught in `sql-postgresql.md`.
- **SQLite:** a small database stored in a single file (or in memory), built into Python as the `sqlite3` module. Perfect for examples and small apps.
- **Connection:** an open link to a database that queries go through.
- **SQLAlchemy:** the standard Python library for connecting to many databases with one interface; pandas uses it for anything other than SQLite.
- **Connection string (URL):** text describing how to reach a database: `postgresql+psycopg://user:password@host:5432/dbname`.
- **Parameterised query:** a query with placeholders (`?` or `:name`) filled in safely by the driver, instead of pasting values into the SQL text. Prevents **SQL injection** (an attacker sneaking SQL in through a value).
- **API (application programming interface):** a defined way for programs to talk to each other. A **web API** answers HTTP requests, usually with JSON.
- **HTTP request:** asking a web server for something (`GET` to read, `POST` to send). The `requests` or `httpx` library makes them from Python.
- **Endpoint:** one URL of an API, like `https://api.example.com/orders`.
- **Pagination:** an API returning results in pages; you keep asking for the next page until there are none.
- **Rate limit:** the maximum number of requests an API allows per period.
- **Nested JSON:** JSON with objects inside objects (`{"customer": {"name": ..., "city": ...}}`). **Flattening** turns nested fields into columns like `customer.name`.
- **Server:** a program (or computer) that waits for requests and answers them: a database server, a web server.

**Everyday picture.** Querying a database is **phoning a librarian**: describe exactly what you need ("total sales per city for 2025") and they bring back one sheet, rather than the whole library. An API is **ordering from a menu by post**: you send a request in a fixed format and get back a parcel (JSON) you must unpack.

**Rule of thumb: let the database do the heavy lifting.** Filtering, joining and aggregating millions of rows is what databases are built for. Bring the **result** into pandas for the last mile (charts, statistics, modelling).

| Bad | Good |
|---|---|
| `pd.read_sql("SELECT * FROM orders", con)` then filter in pandas | `pd.read_sql("SELECT city, SUM(qty*price) AS revenue FROM orders WHERE date >= '2025-01-01' GROUP BY city", con)` |

**pandas' SQL functions:**

| Code | Does |
|---|---|
| `pd.read_sql(query, con, params=...)` | run a query → DataFrame |
| `pd.read_sql_table("orders", engine)` | a whole table (SQLAlchemy only) |
| `df.to_sql("name", con, if_exists="replace", index=False)` | write a DataFrame as a table |
| `chunksize=50_000` in `read_sql` | stream a big result in pieces |

For PostgreSQL: `from sqlalchemy import create_engine; engine = create_engine("postgresql+psycopg://...")`, then pass `engine` as `con`. Keep passwords in environment variables, never in notebooks.

**Reading a web API, step by step:**

1. Send a request: `r = requests.get(url, params={"page": 1}, timeout=10)`.
2. Check it worked: `r.raise_for_status()` raises an error for a failed status (404 not found, 500 server error, 429 too many requests).
3. Parse the JSON: `data = r.json()`.
4. Flatten into a table: `pd.json_normalize(data["results"])`.
5. Repeat for every page; collect the pages in a list; `pd.concat` once at the end.
6. Save the raw responses (JSON Lines) so you don't have to call the API again while you work.

**`pd.json_normalize`** turns a list of nested dicts into a flat DataFrame: nested keys become `parent.child` columns; `record_path` explodes a nested list into one row per item, and `meta` copies parent fields onto each of those rows.

**Common mistakes:**

- ❌ Building SQL with f-strings from user input (`f"... WHERE name = '{name}'"`): SQL injection. ✅ `params=`.
- ❌ `SELECT *` on a huge table "just to look". ✅ `LIMIT 100`, or aggregate in SQL.
- ❌ Calling an API in a loop with no `timeout` and no pause, getting blocked by the rate limit. ✅ Timeouts, retries with backoff, and caching raw responses.
- ❌ Hard-coding API keys and database passwords in code you share. ✅ Environment variables or a secrets manager.

**Used in real software:** analysts pull from data warehouses (Snowflake, BigQuery, Redshift, PostgreSQL) with `read_sql`; data pipelines call payment, CRM and analytics APIs nightly and store the flattened results as Parquet.

### Python

```python
import io, sqlite3
import pandas as pd

csv_text = """order_id,date,customer,city,product,category,qty,price
1,2025-01-05,Asha,Pune,Notebook,stationery,5,60
2,2025-01-06,Ravi,Mumbai,Headphones,electronics,1,2500
3,2025-02-10,Asha,Pune,Backpack,bags,1,1200
4,2025-02-11,Meera,Pune,Keyboard,electronics,1,1800
5,2025-03-02,Zoya,Mumbai,Water bottle,kitchen,2,350
6,2025-03-15,Kabir,Bengaluru,Desk lamp,electronics,1,900
7,2025-03-20,Asha,Pune,Headphones,electronics,1,2500
8,2025-04-01,Isha,Delhi,Mug,kitchen,4,250
9,2025-04-18,Ravi,Mumbai,Notebook,stationery,10,60
10,2025-05-05,Zoya,Mumbai,Keyboard,electronics,1,1800
"""
orders = pd.read_csv(io.StringIO(csv_text))

con = sqlite3.connect(":memory:")                     # a throwaway database in memory
orders.to_sql("orders", con, index=False)

query = """
SELECT city, COUNT(*) AS n_orders, SUM(qty * price) AS revenue
FROM orders
WHERE category = :cat
GROUP BY city
ORDER BY revenue DESC
"""
print(pd.read_sql(query, con, params={"cat": "electronics"}))   # :cat filled in safely
```

**Output:**

```text
        city  n_orders  revenue
0       Pune         2     4300
1     Mumbai         2     4300
2  Bengaluru         1      900
```

```python
api_response = {                                     # what r.json() might return from a shop API
    "page": 1, "next_page": None,
    "results": [
        {"id": 1, "customer": {"name": "Asha", "city": "Pune"}, "items": [{"sku": "NB", "qty": 5}, {"sku": "PN", "qty": 2}]},
        {"id": 2, "customer": {"name": "Ravi", "city": "Mumbai"}, "items": [{"sku": "HP", "qty": 1}]},
    ],
}
flat = pd.json_normalize(api_response["results"])                 # nested dicts → dotted columns
print(flat.drop(columns="items"))
items = pd.json_normalize(api_response["results"], record_path="items", meta=["id", ["customer", "name"]])
print(items)                                                      # one row per item, parent fields copied
```

**Output:**

```text
   id customer.name customer.city
0   1          Asha          Pune
1   2          Ravi        Mumbai
  sku  qty id customer.name
0  NB    5  1          Asha
1  PN    2  1          Asha
2  HP    1  2          Ravi
```

Calling a real API looks like this (not run here, because it needs the internet and a real URL):

```python
import requests

def fetch_all(url, token):
    pages, page = [], 1
    while page is not None:
        r = requests.get(url, params={"page": page}, headers={"Authorization": f"Bearer {token}"}, timeout=10)
        r.raise_for_status()                       # stop on 4xx/5xx errors
        body = r.json()
        pages.append(pd.json_normalize(body["results"]))
        page = body["next_page"]                   # None when there are no more pages
    return pd.concat(pages, ignore_index=True)
```

### Practice

1. Using the in-memory database, write a query that returns each customer's number of orders and total quantity, only for customers with at least 2 orders. Load it into pandas.
2. Flatten `[{"user": {"id": 7, "plan": "pro"}, "spend": 120}, {"user": {"id": 9, "plan": "free"}, "spend": 0}]` into a table with columns `user.id`, `user.plan`, `spend`.

<details>
<summary><b>Answer</b></summary>

```python
q = """SELECT customer, COUNT(*) AS n, SUM(qty) AS total_qty
       FROM orders GROUP BY customer HAVING COUNT(*) >= 2 ORDER BY n DESC, customer"""
print(pd.read_sql(q, con))
print(pd.json_normalize([{"user": {"id": 7, "plan": "pro"}, "spend": 120},
                         {"user": {"id": 9, "plan": "free"}, "spend": 0}]))
```

**Output:**

```text
  customer  n  total_qty
0     Asha  3          7
1     Ravi  2         11
2     Zoya  2          3
   spend  user.id user.plan
0    120        7       pro
1      0        9      free
```

</details>

**Learn more:** [pandas: read_sql](https://pandas.pydata.org/docs/reference/api/pandas.read_sql.html) · [pandas: json_normalize](https://pandas.pydata.org/docs/reference/api/pandas.json_normalize.html) · [Requests: quickstart](https://requests.readthedocs.io/en/latest/user/quickstart/)

---

## 21. Selecting Data: Columns, [], loc and iloc

![loc selects by label (end included); iloc selects by position (end excluded)](images/data-science/21-loc-iloc.svg)

### Theory

> **In simple words:** pick **columns** with `df["col"]` or `df[["a", "b"]]`. Pick **rows and columns together** with `.loc[rows, cols]` using **labels** (names), or `.iloc[rows, cols]` using **positions** (numbers). It's NumPy indexing, but with names.

**Words to know:**

- **Selection:** choosing part of a table: some columns, some rows, or both.
- **`.loc` (label-based):** select by row labels and column names. Slices **include** the end label.
- **`.iloc` (integer-location-based):** select by position numbers. Slices **exclude** the end, like Python.
- **Projection:** choosing columns (SQL's `SELECT a, b`).
- **Scalar access:** getting one single value; `.at[label, col]` and `.iat[i, j]` are the fast versions.

**Everyday picture.** `.loc` is finding seats in a theatre **by their printed labels** ("row K, seats 5 to 8", and seat 8 is included because you named it). `.iloc` is counting **positions** from the front ("the 1st to the 4th seat", stopping before the 4th, programmer-style).

**The selection table:**

| Code | Returns | Selects |
|---|---|---|
| `df["price"]` | Series | one column |
| `df[["product", "price"]]` | DataFrame | several columns, in this order |
| `df.loc[3]` | Series | the row whose **label** is 3 |
| `df.loc[2:4]` | DataFrame | rows labelled 2, 3, **and 4** |
| `df.loc[2:4, "customer":"product"]` | DataFrame | label ranges for rows and columns (both ends included) |
| `df.loc[[1, 5], ["city", "qty"]]` | DataFrame | lists of labels |
| `df.iloc[0]` | Series | the first row (by position) |
| `df.iloc[:3, 1:4]` | DataFrame | first 3 rows, columns at positions 1–3 |
| `df.iloc[-1, -1]` | scalar | bottom-right value |
| `df.at[3, "price"]`, `df.iat[0, 0]` | scalar | one value, fastest |
| `df.select_dtypes("number")` | DataFrame | all numeric columns |
| `df.filter(like="date")` | DataFrame | columns whose name contains "date" |

**Series or DataFrame?** One label in → Series (`df["a"]`); a **list** of labels in → DataFrame (`df[["a"]]`). Many functions want one or the other, so this matters.

**Why `loc` includes the end:** labels aren't necessarily numbers or in order ("from `customer` to `product`" naturally means including `product`). With the default 0, 1, 2, … index, `df.loc[0:2]` and `df.iloc[0:2]` look similar but return 3 and 2 rows respectively.

**Changing values safely:** select with `.loc` on the left of `=`: `df.loc[df["qty"] > 5, "bulk"] = True`. Never chain two selections when assigning (`df[df["qty"] > 5]["bulk"] = True` changes a temporary copy; in pandas 3 it never touches `df`, Section [25](#25-method-chaining-and-copy-on-write-pandas-3)).

**When to use which:** `df[...]` for columns; `.loc` for almost everything else (readable, uses names); `.iloc` when position really matters ("the first 5 rows", "the last column"), for example after sorting.

**Common mistakes:**

- ❌ `df["a", "b"]` (looks for a single column named by the tuple `("a", "b")`). ✅ `df[["a", "b"]]`.
- ❌ `df.loc[0:2]` vs `df.iloc[0:2]` off-by-one confusion. ✅ Remember: loc includes, iloc excludes.
- ❌ After sorting or filtering, using `.loc[0]` expecting "the first row" (label 0 may be anywhere or gone). ✅ `.iloc[0]`.
- ❌ Relying on `df.price` (attribute access). It breaks for names with spaces or names like `count`. ✅ `df["price"]`.

**Used in real software:** `X = df[feature_columns]` and `y = df["target"]` start nearly every ML script; `.iloc[:split]` and `.iloc[split:]` split time-ordered data into training and test parts.

### Python

```python
import io
import pandas as pd

csv_text = """order_id,date,customer,city,product,category,qty,price
1,2025-01-05,Asha,Pune,Notebook,stationery,5,60
2,2025-01-06,Ravi,Mumbai,Headphones,electronics,1,2500
3,2025-02-10,Asha,Pune,Backpack,bags,1,1200
4,2025-02-11,Meera,Pune,Keyboard,electronics,1,1800
5,2025-03-02,Zoya,Mumbai,Water bottle,kitchen,2,350
6,2025-03-15,Kabir,Bengaluru,Desk lamp,electronics,1,900
"""
orders = pd.read_csv(io.StringIO(csv_text), parse_dates=["date"])

print(type(orders["price"]).__name__, type(orders[["price"]]).__name__)
print(orders[["customer", "product", "price"]].head(2))
print(orders.loc[2:4, "customer":"product"])              # labels: 2, 3 AND 4; customer..product
print(orders.iloc[2:4, 2:5])                              # positions: 2, 3; columns 2, 3, 4
print(orders.at[3, "price"], orders.iat[0, 2], orders.iloc[-1, -1])
```

**Output:**

```text
Series DataFrame
  customer     product  price
0     Asha    Notebook     60
1     Ravi  Headphones   2500
  customer    city       product
2     Asha    Pune      Backpack
3    Meera    Pune      Keyboard
4     Zoya  Mumbai  Water bottle
  customer  city   product
2     Asha  Pune  Backpack
3    Meera  Pune  Keyboard
1800 Asha 900
```

```python
print(orders.select_dtypes("number").columns.tolist())
print(orders.filter(like="c").columns.tolist())           # names containing "c"

by_product = orders.set_index("product")
print(by_product.loc["Keyboard", "customer"], by_product.loc["Keyboard", "price"])
print(by_product.loc[["Notebook", "Desk lamp"], "price"])

orders.loc[orders["qty"] >= 2, "note"] = "multi"          # set values for matching rows
print(orders[["product", "qty", "note"]])
```

**Output:**

```text
['order_id', 'qty', 'price']
['customer', 'city', 'product', 'category', 'price']
Meera 1800
product
Notebook      60
Desk lamp    900
Name: price, dtype: int64
        product  qty   note
0      Notebook    5  multi
1    Headphones    1    NaN
2      Backpack    1    NaN
3      Keyboard    1    NaN
4  Water bottle    2  multi
5     Desk lamp    1    NaN
```

The new `note` column gets `NaN` where no value was set. `orders.filter(like="c")` matches column **names**; to filter rows, see the next section.

### Practice

1. From `orders`, select the `city` and `price` of rows at positions 1 to 3 (inclusive) using `.iloc`, and then the same rows using `.loc`.
2. Make `order_id` the index, then get the customer of order 5 with `.at`.

<details>
<summary><b>Answer</b></summary>

```python
print(orders.iloc[1:4][["city", "price"]])
print(orders.loc[1:3, ["city", "price"]])
print(orders.set_index("order_id").at[5, "customer"])
```

**Output:**

```text
     city  price
1  Mumbai   2500
2    Pune   1200
3    Pune   1800
     city  price
1  Mumbai   2500
2    Pune   1200
3    Pune   1800
Zoya
```

`.iloc[1:4]` needs stop 4 to include position 3; `.loc[1:3]` includes label 3. With the default index the labels equal the positions, so both give the same rows.

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [2880. Select Data](https://leetcode.com/problems/select-data/) | 🟢 Easy |
| 2 | [2879. Display the First Three Rows](https://leetcode.com/problems/display-the-first-three-rows/) | 🟢 Easy |

**Learn more:** [pandas: indexing and selecting data](https://pandas.pydata.org/docs/user_guide/indexing.html)

---

## 22. Filtering Rows: Conditions, isin, between and query

![A boolean condition on a column becomes a mask; df[mask] keeps the matching rows](images/data-science/22-filter.svg)

### Theory

> **In simple words:** filtering means **keeping only the rows that match a rule**: orders from Pune, prices over 1,000, dates in March. You write the rule as a condition on columns; it becomes a True/False mask (exactly like NumPy), and `df[mask]` keeps the True rows. It's SQL's `WHERE`.

**Words to know:**

- **Filter / predicate:** a rule each row either passes or fails.
- **Mask:** the Series of True/False the rule produces, one per row.
- **`isin`:** "is the value one of these?" (SQL `IN`).
- **`between(a, b)`:** "a ≤ value ≤ b" (both ends included by default; SQL `BETWEEN`).
- **`query`:** filtering with a readable text expression: `df.query("price > 1000 and city == 'Pune'")`.
- **`@variable` in `query`:** refers to a Python variable from inside the query string.
- **Cohort:** a group of users who share a starting point, such as everyone who signed up in March.

**Everyday picture.** Filtering is a **bouncer with a guest list**: each row walks up, the bouncer checks the rule, and only the rows that pass get in. The table's columns don't change; only the number of rows does.

**Filtering, traced:** `orders[(orders["city"] == "Pune") & (orders["price"] > 100)]`

| Row | city | price | `city == "Pune"` | `price > 100` | `&` → kept? |
|---|---|---|---|---|---|
| 0 | Pune | 60 | True | False | ❌ |
| 1 | Mumbai | 2500 | False | True | ❌ |
| 2 | Pune | 1200 | True | True | ✅ |
| 3 | Pune | 1800 | True | True | ✅ |

**The filtering toolbox:**

| Rule | Code | SQL |
|---|---|---|
| comparison | `df[df["qty"] >= 2]` | `WHERE qty >= 2` |
| and / or / not | `(c1) & (c2)`, `(c1) \| (c2)`, `~(c1)` | `AND`, `OR`, `NOT` |
| in a list | `df[df["city"].isin(["Pune", "Goa"])]` | `IN (...)` |
| range | `df[df["price"].between(500, 2000)]` | `BETWEEN` |
| text contains | `df[df["product"].str.contains("book", case=False)]` | `ILIKE '%book%'` |
| starts with | `df[df["product"].str.startswith("Key")]` | `LIKE 'Key%'` |
| missing / present | `df[df["note"].isna()]`, `.notna()` | `IS NULL` / `IS NOT NULL` |
| dates | `df[df["date"] >= "2025-03-01"]` | `WHERE date >= ...` |
| readable string | `df.query("qty >= 2 and city != 'Delhi'")` | |
| a variable in query | `limit = 1000; df.query("price > @limit")` | |

**Filter rows and choose columns in one step:** `df.loc[mask, ["customer", "price"]]`.

**After filtering,** the index keeps the original labels (2, 3, 6, …). Add `.reset_index(drop=True)` if you want 0, 1, 2 again.

**When to use `query`:** long conditions read better as text, and it accepts `and`/`or`. **When to avoid it:** column names with spaces (need backticks `` `order id` ``), or when you're building the condition from code (masks are easier to combine).

**Common mistakes:**

- ❌ `and`/`or` between masks → `ValueError`. ✅ `&`/`|`, with brackets around each comparison.
- ❌ `df[df["city"] == "Pune" | df["city"] == "Goa"]` (precedence bug). ✅ `df[df["city"].isin(["Pune", "Goa"])]`.
- ❌ Comparing with `== None` or `== np.nan` (never True: NaN isn't equal to anything, even itself). ✅ `.isna()`.
- ❌ `str.contains` on a column with missing values (NaN in the mask → error). ✅ `.str.contains("x", na=False)`.

**Used in real software:** every "filter" dropdown in a dashboard; selecting a cohort ("users who signed up in March") for analysis; removing test accounts and internal traffic before computing metrics.

### Python

```python
import io
import pandas as pd

csv_text = """order_id,date,customer,city,product,category,qty,price
1,2025-01-05,Asha,Pune,Notebook,stationery,5,60
2,2025-01-06,Ravi,Mumbai,Headphones,electronics,1,2500
3,2025-02-10,Asha,Pune,Backpack,bags,1,1200
4,2025-02-11,Meera,Pune,Keyboard,electronics,1,1800
5,2025-03-02,Zoya,Mumbai,Water bottle,kitchen,2,350
6,2025-03-15,Kabir,Bengaluru,Desk lamp,electronics,1,900
7,2025-03-20,Asha,Pune,Headphones,electronics,1,2500
8,2025-04-01,Isha,Delhi,Mug,kitchen,4,250
9,2025-04-18,Ravi,Mumbai,Notebook,stationery,10,60
10,2025-05-05,Zoya,Mumbai,Keyboard,electronics,1,1800
"""
orders = pd.read_csv(io.StringIO(csv_text), parse_dates=["date"])

pune_big = orders[(orders["city"] == "Pune") & (orders["price"] > 100)]
print(pune_big[["order_id", "product", "price"]])
print(orders.loc[orders["category"].isin(["kitchen", "bags"]), ["product", "qty"]])
print(orders.loc[orders["price"].between(500, 2000), "product"].tolist())
print(orders.loc[orders["product"].str.contains("book", case=False), "order_id"].tolist())
```

**Output:**

```text
   order_id     product  price
2         3    Backpack   1200
3         4    Keyboard   1800
6         7  Headphones   2500
        product  qty
2      Backpack    1
4  Water bottle    2
7           Mug    4
['Backpack', 'Keyboard', 'Desk lamp', 'Keyboard']
[1, 9]
```

```python
march = orders[(orders["date"] >= "2025-03-01") & (orders["date"] < "2025-04-01")]
print(march[["date", "product"]])

limit = 1000
print(orders.query("price > @limit and city != 'Mumbai'")[["customer", "price"]])
print(orders[~orders["city"].isin(["Pune", "Mumbai"])].reset_index(drop=True)[["city", "product"]])
print(f"{(orders['qty'] > 1).mean():.0%} of orders have more than one item")
```

**Output:**

```text
        date       product
4 2025-03-02  Water bottle
5 2025-03-15     Desk lamp
6 2025-03-20    Headphones
  customer  price
2     Asha   1200
3    Meera   1800
6     Asha   2500
        city    product
0  Bengaluru  Desk lamp
1      Delhi        Mug
40% of orders have more than one item
```

### Practice

1. Find electronics orders with exactly one item, showing customer and price.
2. Find orders **not** from Pune placed in the first quarter (January–March 2025), using `query`.
3. Which customers ever bought something priced 2,000 or more? (Each name once.)

<details>
<summary><b>Answer</b></summary>

```python
print(orders.loc[(orders["category"] == "electronics") & (orders["qty"] == 1), ["customer", "price"]])
print(orders.query("city != 'Pune' and date < '2025-04-01'")[["order_id", "city", "date"]])
print(orders.loc[orders["price"] >= 2000, "customer"].unique().tolist())
```

**Output:**

```text
  customer  price
1     Ravi   2500
3    Meera   1800
5    Kabir    900
6     Asha   2500
9     Zoya   1800
   order_id       city       date
1         2     Mumbai 2025-01-06
4         5     Mumbai 2025-03-02
5         6  Bengaluru 2025-03-15
['Ravi', 'Asha']
```

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [595. Big Countries](https://leetcode.com/problems/big-countries/) | 🟢 Easy |
| 2 | [1757. Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/) | 🟢 Easy |
| 3 | [584. Find Customer Referee](https://leetcode.com/problems/find-customer-referee/) | 🟢 Easy |
| 4 | [183. Customers Who Never Order](https://leetcode.com/problems/customers-who-never-order/) | 🟢 Easy |
| 5 | [1148. Article Views I](https://leetcode.com/problems/article-views-i/) | 🟢 Easy |
| 6 | [1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/) | 🟢 Easy |
| 7 | [620. Not Boring Movies](https://leetcode.com/problems/not-boring-movies/) | 🟢 Easy |

Hints: 584 has missing referees (a NaN is "not equal to 2", but `!=` alone drops it); 183 is `~isin`; 1683 uses `.str.len()`.

**Learn more:** [pandas: boolean indexing](https://pandas.pydata.org/docs/user_guide/indexing.html#boolean-indexing) · [pandas: DataFrame.query](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.query.html)

---

## 23. Sorting, Ranking and Top-N

![rank: method="min" gives ties the lowest rank and skips; "dense" gives ties the same rank without gaps](images/data-science/23-rank.svg)

### Theory

> **In simple words:** sorting puts rows in order by one or more columns; **ranking** gives each row its place number (1st, 2nd, …); **top-N** keeps the N biggest or smallest. Interviews love ranking questions ("second highest salary"), and the tricky part is always **ties**.

**Words to know:**

- **Sort key:** the column(s) you sort by. With several keys, the second breaks ties in the first.
- **Ascending / descending:** smallest first / largest first.
- **Stable sort:** rows with equal keys keep their original order. Needed when you sort in several passes.
- **Rank:** a row's position in sorted order. **Tie:** two rows with the same value.
- **Ranking methods for ties:** `"first"` (by order of appearance), `"min"` (all tied rows get the lowest rank, then a gap: 1, 2, 2, 4 — "Olympic" ranking, SQL `RANK()`), `"dense"` (tied rows share a rank, no gap: 1, 2, 2, 3 — SQL `DENSE_RANK()`), `"average"` (the default: tied rows get the mean of their positions: 2.5).
- **Percentile rank:** rank as a fraction from 0 to 1 (`pct=True`).
- **Top-N:** the N largest (or smallest) rows.

**Everyday picture.** A race: two runners cross the line together in second place. Olympic style (`min`) gives them both silver and nobody gets bronze (next is 4th). A school sports day (`dense`) gives them both 2nd and the next runner gets 3rd.

**Ranking methods traced** for scores `[90, 85, 85, 70]` (descending):

| score | first | min | dense | average |
|---|---|---|---|---|
| 90 | 1 | 1 | 1 | 1.0 |
| 85 | 2 | 2 | 2 | 2.5 |
| 85 | 3 | 2 | 2 | 2.5 |
| 70 | 4 | 4 | 3 | 4.0 |

**The tools:**

| Code | Does |
|---|---|
| `df.sort_values("price")` | ascending by price |
| `df.sort_values("price", ascending=False)` | descending |
| `df.sort_values(["city", "price"], ascending=[True, False])` | city A→Z, then price high→low within each city |
| `df.sort_values("x", na_position="first")` | where missing values go (default: last) |
| `df.sort_index()` | by the row labels |
| `df.nlargest(3, "price")`, `df.nsmallest(3, "price")` | top/bottom 3 (faster than sorting everything) |
| `df["price"].rank(ascending=False, method="dense")` | rank values |
| `df.groupby("city")["price"].rank(...)` | rank **within each group** (Section [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking)) |

**"Second highest value", the interview classic:** take the **distinct** values, sort descending, and take the second, being careful when there **is** no second (return missing, not an error). `dense` rank == 2 does the same.

**When to sort:** before showing results to people, before `.iloc[0]` ("the first after sorting"), before time-based operations (Section [38](#38-time-series-resample-rolling-shift-and-window-functions)). **When not to:** just to find the max (use `max`/`idxmax`) or top-N (use `nlargest`), which are faster than a full sort.

**Common mistakes:**

- ❌ Forgetting that `sort_values` returns a new DataFrame. ✅ `df = df.sort_values(...)`.
- ❌ Picking "second highest" with `.iloc[1]` on non-distinct values (if the top value appears twice, you get the top value again). ✅ `drop_duplicates()` or dense rank.
- ❌ The default rank method `average` giving `2.5` when you expected whole numbers. ✅ Choose `method` deliberately.
- ❌ Sorting text with mixed case: `"apple"` sorts after `"Zebra"` (uppercase first). ✅ `key=lambda s: s.str.lower()`.

**Used in real software:** leaderboards (dense rank), search results (sort by relevance score), "top 10 products this week" reports, percentile ranks for grading and credit scores.

### Python

```python
import pandas as pd

emp = pd.DataFrame({"name": ["Asha", "Ravi", "Zoya", "Kabir", "Meera", "Isha"],
                    "dept": ["IT", "IT", "Sales", "Sales", "IT", "Sales"],
                    "salary": [90, 85, 85, 70, 95, 70]})

print(emp.sort_values("salary", ascending=False).head(3))
print(emp.sort_values(["dept", "salary"], ascending=[True, False]))

for method in ["first", "min", "dense", "average"]:
    emp[method] = emp["salary"].rank(ascending=False, method=method)
print(emp)
```

**Output:**

```text
    name dept  salary
4  Meera   IT      95
0   Asha   IT      90
1   Ravi   IT      85
    name   dept  salary
4  Meera     IT      95
0   Asha     IT      90
1   Ravi     IT      85
2   Zoya  Sales      85
3  Kabir  Sales      70
5   Isha  Sales      70
    name   dept  salary  first  min  dense  average
0   Asha     IT      90    2.0  2.0    2.0      2.0
1   Ravi     IT      85    3.0  3.0    3.0      3.5
2   Zoya  Sales      85    4.0  3.0    3.0      3.5
3  Kabir  Sales      70    5.0  5.0    4.0      5.5
4  Meera     IT      95    1.0  1.0    1.0      1.0
5   Isha  Sales      70    6.0  5.0    4.0      5.5
```

```python
emp = emp[["name", "dept", "salary"]]
print(emp.nlargest(2, "salary"), emp.nsmallest(2, "salary", keep="all"), sep="\n")

def second_highest(s):
    distinct = s.drop_duplicates().sort_values(ascending=False)
    return distinct.iloc[1] if len(distinct) >= 2 else None

print(second_highest(emp["salary"]), second_highest(pd.Series([100, 100])))
print(emp.loc[emp["salary"].rank(method="dense", ascending=False) == 2, "name"].tolist())

emp["pct_rank"] = emp["salary"].rank(pct=True).round(2)
print(emp.sort_values("pct_rank"))
names = pd.Series(["banana", "Cherry", "apple"])
print(names.sort_values().tolist(), names.sort_values(key=lambda s: s.str.lower()).tolist())
```

**Output:**

```text
    name dept  salary
4  Meera   IT      95
0   Asha   IT      90
    name   dept  salary
3  Kabir  Sales      70
5   Isha  Sales      70
90 None
['Asha']
    name   dept  salary  pct_rank
3  Kabir  Sales      70      0.25
5   Isha  Sales      70      0.25
1   Ravi     IT      85      0.58
2   Zoya  Sales      85      0.58
0   Asha     IT      90      0.83
4  Meera     IT      95      1.00
['Cherry', 'apple', 'banana'] ['apple', 'banana', 'Cherry']
```

`keep="all"` makes `nsmallest` keep every row tied at the cut-off (Kabir and Isha both earn 70).

### Practice

1. Rank employees by salary **within each department** using dense ranking (hint: `emp.groupby("dept")["salary"].rank(...)`).
2. Return the third-highest **distinct** salary, or `None` if there isn't one.

<details>
<summary><b>Answer</b></summary>

```python
emp["dept_rank"] = emp.groupby("dept")["salary"].rank(method="dense", ascending=False).astype(int)
print(emp.sort_values(["dept", "dept_rank"]))

def nth_highest(s, n):
    distinct = s.drop_duplicates().nlargest(n)
    return distinct.iloc[-1] if len(distinct) == n else None

print(nth_highest(emp["salary"], 3), nth_highest(emp["salary"], 9))
```

**Output:**

```text
    name   dept  salary  pct_rank  dept_rank
4  Meera     IT      95      1.00          1
0   Asha     IT      90      0.83          2
1   Ravi     IT      85      0.58          3
2   Zoya  Sales      85      0.58          1
3  Kabir  Sales      70      0.25          2
5   Isha  Sales      70      0.25          2
85 None
```

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [176. Second Highest Salary](https://leetcode.com/problems/second-highest-salary/) | 🟡 Medium |
| 2 | [177. Nth Highest Salary](https://leetcode.com/problems/nth-highest-salary/) | 🟡 Medium |
| 3 | [178. Rank Scores](https://leetcode.com/problems/rank-scores/) | 🟡 Medium |
| 4 | [586. Customer Placing the Largest Number of Orders](https://leetcode.com/problems/customer-placing-the-largest-number-of-orders/) | 🟢 Easy |

**Learn more:** [pandas: sort_values](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html) · [pandas: Series.rank](https://pandas.pydata.org/docs/reference/api/pandas.Series.rank.html)

---

## 24. Adding and Changing Columns: Arithmetic, assign, map, apply and np.select

![Ways to make a new column, from fastest (vectorised arithmetic) to slowest (row-wise apply)](images/data-science/24-new-columns.svg)

### Theory

> **In simple words:** most analysis needs **new columns** made from existing ones: revenue = quantity × price, a month from a date, a region from a city, a label from a rule. Use whole-column operations whenever possible; use `apply` (a Python function per value or per row) only when nothing vectorised exists.

**Words to know:**

- **Derived column (feature):** a column calculated from others.
- **`assign`:** returns a **new** DataFrame with columns added; ideal for chains (Section [25](#25-method-chaining-and-copy-on-write-pandas-3)).
- **`map`:** replaces each value of a Series using a dict (or function): a lookup table.
- **`apply`:** runs a Python function on each value (Series) or each row/column (DataFrame). Flexible but slow: it's a hidden Python loop.
- **`np.where` / `np.select`:** vectorised if/else for columns (Section [10](#10-boolean-masks-fancy-indexing-and-npwhere)).
- **`.dt` accessor:** date parts of a datetime column: `.dt.year`, `.dt.month`, `.dt.day_name()`.
- **Lambda:** a one-line unnamed function (Section [3](#3-python-refresher-for-data-work-lists-dicts-comprehensions-and-functions)); in `assign`, `lambda d: ...` receives the DataFrame as it is at that step.

**Everyday picture.** A spreadsheet formula `=C2*D2` dragged down a whole column is vectorised arithmetic. `apply` is asking an assistant to read every row and work it out by hand: fine for 100 rows, painful for a million.

**Ways to create a column, fastest first:**

| Approach | Example | Speed |
|---|---|---|
| Vectorised arithmetic | `df["revenue"] = df["qty"] * df["price"]` | ⚡ fastest |
| `.dt` / `.str` accessors | `df["month"] = df["date"].dt.month` | ⚡ fast |
| `np.where` / `np.select` | `np.where(df["qty"] > 3, "bulk", "single")` | ⚡ fast |
| `.map(dict)` | `df["region"] = df["city"].map({"Pune": "West"})` | ⚡ fast |
| `pd.cut` | numbers → labelled ranges (Section [29](#29-categorical-data-and-binning-cut-and-qcut)) | ⚡ fast |
| `Series.apply(func)` | a Python function on each value | 🐢 slow on big data |
| `df.apply(func, axis=1)` | a function on each **row** | 🐌 slowest; avoid on big data |

**`np.select` for several rules** (checked in order, the first match wins):

```text
conditions = [df["price"] >= 2000, df["price"] >= 500]
choices    = ["premium", "mid"]
df["tier"] = np.select(conditions, choices, default="budget")
```

Traced for prices `[60, 2500, 1200]`: 60 matches neither → `"budget"`; 2500 matches the first → `"premium"`; 1200 fails the first, matches the second → `"mid"`.

**`map` vs `replace`:** `map` turns values **not in the dict into NaN** (good: you notice unmapped values); `replace` leaves them unchanged.

**Assigning:**

| Code | Effect |
|---|---|
| `df["new"] = ...` | adds or overwrites a column **in place** |
| `df = df.assign(new=...)` | returns a new DataFrame (chain-friendly) |
| `df.insert(1, "new", values)` | add at a specific position |
| `df.loc[mask, "col"] = value` | change only some rows |
| `df["col"] = df["col"].astype("int32")` | change a column's type |

**When `apply` is fine:** small data, or logic with no vectorised equivalent (calling a parsing library on each value). **When it isn't:** arithmetic, comparisons, string methods, date parts: all have fast versions.

**Common mistakes:**

- ❌ `df.apply(lambda r: r["qty"] * r["price"], axis=1)` for simple maths (often 100–1000× slower).
- ❌ `map` with a dict that misses some keys, creating silent NaNs. ✅ Check `.isna().sum()` afterwards.
- ❌ Using Python's `if` on a column (`if df["qty"] > 3:` → `ValueError`). ✅ `np.where`.
- ❌ Integer division surprises: `df["a"] / df["b"]` always gives floats; `//` floors.

**Used in real software:** feature engineering for ML (ratios, flags, date parts, Section [61](#61-feature-engineering-preparing-data-for-machine-learning)); business metrics (revenue, margin, discount); data labelling rules ("high value customer").

### Python

```python
import io
import numpy as np
import pandas as pd

csv_text = """order_id,date,customer,city,product,category,qty,price
1,2025-01-05,Asha,Pune,Notebook,stationery,5,60
2,2025-01-06,Ravi,Mumbai,Headphones,electronics,1,2500
3,2025-02-10,Asha,Pune,Backpack,bags,1,1200
4,2025-02-11,Meera,Pune,Keyboard,electronics,1,1800
5,2025-03-02,Zoya,Mumbai,Water bottle,kitchen,2,350
6,2025-03-15,Kabir,Bengaluru,Desk lamp,electronics,1,900
"""
orders = pd.read_csv(io.StringIO(csv_text), parse_dates=["date"])

orders["revenue"] = orders["qty"] * orders["price"]
orders["month"] = orders["date"].dt.month_name().str[:3]
orders["weekday"] = orders["date"].dt.day_name()
orders["region"] = orders["city"].map({"Pune": "West", "Mumbai": "West", "Bengaluru": "South"})
orders["tier"] = np.select([orders["price"] >= 2000, orders["price"] >= 500], ["premium", "mid"], default="budget")
orders["size"] = np.where(orders["qty"] >= 2, "multi", "single")
print(orders[["product", "revenue", "month", "weekday", "region", "tier", "size"]])
```

**Output:**

```text
        product  revenue month   weekday region     tier    size
0      Notebook      300   Jan    Sunday   West   budget   multi
1    Headphones     2500   Jan    Monday   West  premium  single
2      Backpack     1200   Feb    Monday   West      mid  single
3      Keyboard     1800   Feb   Tuesday   West      mid  single
4  Water bottle      700   Mar    Sunday   West   budget   multi
5     Desk lamp      900   Mar  Saturday  South      mid  single
```

```python
import time

big = pd.DataFrame({"qty": np.random.default_rng(0).integers(1, 10, 200_000),
                    "price": np.random.default_rng(1).uniform(10, 3000, 200_000)})
t0 = time.perf_counter(); fast = big["qty"] * big["price"]; t1 = time.perf_counter()
slow = big.apply(lambda row: row["qty"] * row["price"], axis=1); t2 = time.perf_counter()
print("same answer:", np.allclose(fast, slow))
print(f"row-wise apply was about {(t2 - t1) / (t1 - t0):,.0f}× slower")

df = pd.DataFrame({"city": ["Pune", "Goa", "Delhi"]})
print(df["city"].map({"Pune": "West", "Delhi": "North"}).tolist())        # Goa → NaN: you notice
print(df["city"].replace({"Pune": "West", "Delhi": "North"}).tolist())    # Goa unchanged
```

**Output:**

```text
same answer: True
row-wise apply was about 2,591× slower
['West', nan, 'North']
['West', 'Goa', 'North']
```

### Practice

1. Add a column `discounted`: 10% off the price for electronics, full price otherwise.
2. Add `is_weekend` (True for Saturday or Sunday orders) using `.dt.dayofweek` (Monday = 0, Sunday = 6).
3. Add `price_band` with `np.select`: under 100 → "low", 100–999 → "medium", 1000+ → "high".

<details>
<summary><b>Answer</b></summary>

```python
orders["discounted"] = np.where(orders["category"] == "electronics", orders["price"] * 0.9, orders["price"])
orders["is_weekend"] = orders["date"].dt.dayofweek >= 5
orders["price_band"] = np.select([orders["price"] < 100, orders["price"] < 1000], ["low", "medium"], default="high")
print(orders[["product", "price", "discounted", "weekday", "is_weekend", "price_band"]])
```

**Output:**

```text
        product  price  discounted   weekday  is_weekend price_band
0      Notebook     60        60.0    Sunday        True        low
1    Headphones   2500      2250.0    Monday       False       high
2      Backpack   1200      1200.0    Monday       False       high
3      Keyboard   1800      1620.0   Tuesday       False       high
4  Water bottle    350       350.0    Sunday        True     medium
5     Desk lamp    900       810.0  Saturday        True     medium
```

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [2881. Create a New Column](https://leetcode.com/problems/create-a-new-column/) | 🟢 Easy |
| 2 | [2884. Modify Columns](https://leetcode.com/problems/modify-columns/) | 🟢 Easy |
| 3 | [2886. Change Data Type](https://leetcode.com/problems/change-data-type/) | 🟢 Easy |
| 4 | [1873. Calculate Special Bonus](https://leetcode.com/problems/calculate-special-bonus/) | 🟢 Easy |
| 5 | [610. Triangle Judgement](https://leetcode.com/problems/triangle-judgement/) | 🟢 Easy |
| 6 | [627. Swap Sex of Employees](https://leetcode.com/problems/swap-sex-of-employees/) | 🟢 Easy |

**Learn more:** [pandas: DataFrame.assign](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.assign.html) · [pandas: Series.map](https://pandas.pydata.org/docs/reference/api/pandas.Series.map.html)

---

## 25. Method Chaining and Copy-on-Write (pandas 3)

![A method chain: each step takes a DataFrame and returns a new one, read top to bottom like a recipe](images/data-science/25-chain.svg)

### Theory

> **In simple words:** most pandas methods return a **new** DataFrame, so you can chain them: load → clean → add columns → filter → sort, written top to bottom like a recipe. pandas 3's **copy-on-write** rule guarantees that a result never secretly shares changes with the table it came from.

**Words to know:**

- **Method chaining:** calling methods one after another on each result: `df.dropna().sort_values("x").head()`.
- **Pipeline:** a sequence of processing steps where each step's output feeds the next.
- **`pipe(func)`:** puts your own function into a chain: `df.pipe(clean_names)` is `clean_names(df)`.
- **Immutable style:** never changing an object in place; always creating a new one. Easier to reason about and to test.
- **`inplace=True`:** an old option that modifies the object instead of returning a new one. Discouraged; it doesn't even save memory in most cases.
- **Copy-on-write (CoW):** pandas 3's rule: any DataFrame or Series derived from another **behaves as an independent copy**. Data is actually copied only when one side is modified (that's the "on write"), so it's still fast.
- **Chained assignment:** assigning through two selections in a row, like `df[mask]["col"] = 5`. Under copy-on-write it **never** changes `df`.
- **`SettingWithCopyWarning`:** the confusing warning older pandas gave for chained assignment. Gone in pandas 3, because the behaviour is now always the same.

**Everyday picture.** A method chain is a **recipe card**: "take the orders, remove cancelled ones, add revenue, keep March, sort by revenue". Copy-on-write means each step works on its **own photocopy** of the page, so scribbling on step 3's copy never smudges the original.

**The same analysis, two styles:**

```text
# step by step: many intermediate names, easy to run cells out of order
df = orders.copy()
df["revenue"] = df["qty"] * df["price"]
df = df[df["revenue"] > 1000]
df = df.sort_values("revenue", ascending=False)

# one chain: reads top to bottom, no leftovers
result = (orders
          .assign(revenue=lambda d: d["qty"] * d["price"])
          .query("revenue > 1000")
          .sort_values("revenue", ascending=False))
```

The outer **brackets** let a chain span several lines. Inside `assign`, `lambda d:` receives the DataFrame **as it is at that step**, so you can use columns created earlier in the same chain.

**Copy-on-write in practice (the three rules):**

1. **Assign results back:** `df = df.dropna()`. Methods don't change `df` itself.
2. **Change values with one `.loc`:** `df.loc[df["qty"] > 5, "bulk"] = True`. Never `df[df["qty"] > 5]["bulk"] = True`.
3. **A subset is independent:** `sub = df[df["city"] == "Pune"]; sub["x"] = 1` changes only `sub`, never `df`.

**Debugging a chain:** comment out the last steps, or insert `.pipe(lambda d: print(d.shape) or d)` to print the shape mid-chain (`print` returns `None`, so `or d` passes the DataFrame on).

**When to chain:** repeatable transformations (cleaning, feature building) and anything you'll turn into a function. **When not to:** while exploring step by step in a notebook, where looking at each intermediate result is the point. Very long chains (15+ steps) are better split into named functions joined with `pipe`.

**Common mistakes:**

- ❌ `df[df["x"] > 0]["y"] = 1` (chained assignment: does nothing to `df` in pandas 3). ✅ `df.loc[df["x"] > 0, "y"] = 1`.
- ❌ `df.sort_values("x", inplace=True)` inside a chain (returns `None`, breaking the chain). ✅ Drop `inplace`.
- ❌ Referring to the **original** DataFrame inside `assign` (`orders["qty"]`) instead of the current step (`d["qty"]`) after rows were filtered: the indexes no longer match. ✅ Use `lambda d:`.

**Used in real software:** data-cleaning functions in production pipelines are typically chains wrapped in functions, then unit-tested; Polars (Section [41](#41-polars-fast-dataframes-with-lazy-queries)) is built entirely around chained expressions.

### Python

```python
import io
import pandas as pd

csv_text = """order_id,date,customer,city,product,category,qty,price
1,2025-01-05,Asha,Pune,Notebook,stationery,5,60
2,2025-01-06,Ravi,Mumbai,Headphones,electronics,1,2500
3,2025-02-10,Asha,Pune,Backpack,bags,1,1200
4,2025-02-11,Meera,Pune,Keyboard,electronics,1,1800
5,2025-03-02,Zoya,Mumbai,Water bottle,kitchen,2,350
6,2025-03-15,Kabir,Bengaluru,Desk lamp,electronics,1,900
7,2025-03-20,Asha,Pune,Headphones,electronics,1,2500
8,2025-04-01,Isha,Delhi,Mug,kitchen,4,250
"""

def clean_names(df):
    return df.rename(columns=str.upper)

result = (pd.read_csv(io.StringIO(csv_text), parse_dates=["date"])
          .assign(revenue=lambda d: d["qty"] * d["price"],
                  month=lambda d: d["date"].dt.month)
          .query("revenue >= 900")
          .pipe(lambda d: print("after filter:", d.shape) or d)     # peek mid-chain
          .sort_values(["month", "revenue"], ascending=[True, False])
          .loc[:, ["month", "customer", "product", "revenue"]]
          .pipe(clean_names)
          .reset_index(drop=True))
print(result)
```

**Output:**

```text
after filter: (6, 10)
   MONTH CUSTOMER     PRODUCT  REVENUE
0      1     Ravi  Headphones     2500
1      2    Meera    Keyboard     1800
2      2     Asha    Backpack     1200
3      3     Asha  Headphones     2500
4      3    Kabir   Desk lamp      900
5      4     Isha         Mug     1000
```

```python
orders = pd.read_csv(io.StringIO(csv_text))

pune = orders[orders["city"] == "Pune"]
pune["qty"] = 0                                       # changes only `pune` (copy-on-write)
print(orders["qty"].tolist(), pune["qty"].tolist())

orders[orders["qty"] > 1]["qty"] = 99                 # chained assignment: does nothing to orders
print(orders["qty"].tolist())

orders.loc[orders["qty"] > 1, "qty"] = 99             # the right way
print(orders["qty"].tolist())
```

**Output:**

```text
[5, 1, 1, 1, 2, 1, 1, 4] [0, 0, 0, 0]
[5, 1, 1, 1, 2, 1, 1, 4]
[99, 1, 1, 1, 99, 1, 1, 99]
```

### Practice

1. Rewrite as one chain: load the CSV, keep electronics, add `revenue`, keep the columns `customer`, `product`, `revenue`, sort by revenue descending.
2. Why does `orders.dropna()` on its own line not remove missing values from `orders`?

<details>
<summary><b>Answer</b></summary>

```python
out = (pd.read_csv(io.StringIO(csv_text))
       .query("category == 'electronics'")
       .assign(revenue=lambda d: d["qty"] * d["price"])
       [["customer", "product", "revenue"]]
       .sort_values("revenue", ascending=False))
print(out)
```

**Output:**

```text
  customer     product  revenue
1     Ravi  Headphones     2500
6     Asha  Headphones     2500
3    Meera    Keyboard     1800
5    Kabir   Desk lamp      900
```

2. `dropna()` returns a **new** DataFrame and leaves `orders` unchanged; you must assign it: `orders = orders.dropna()`.

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [2891. Method Chaining](https://leetcode.com/problems/method-chaining/) | 🟢 Easy |
| 2 | [2887. Fill Missing Data](https://leetcode.com/problems/fill-missing-data/) | 🟢 Easy |

**Learn more:** [pandas: copy-on-write](https://pandas.pydata.org/docs/user_guide/copy_on_write.html) · [Tom Augspurger: Modern pandas, method chaining](https://tomaugspurger.net/posts/method-chaining/)

---

### ✅ Part 3 checkpoint

Without looking, can you:

- [ ] Explain how two Series with different labels are added, and how `fill_value` changes it?
- [ ] Create a DataFrame three ways and run the five-minute check (`shape`, `head`, `info`, `describe`, `value_counts`, `isna().sum()`)?
- [ ] Read and write CSV, Parquet and JSON Lines, and say why Parquet is better for analysis?
- [ ] Run a parameterised SQL query into pandas and flatten nested JSON with `json_normalize`?
- [ ] Select with `[]`, `.loc` and `.iloc`, and say which includes the end of a slice?
- [ ] Filter with `&`, `|`, `~`, `isin`, `between`, `str.contains` and `query`?
- [ ] Sort by several keys, and rank with `min` and `dense`, explaining ties?
- [ ] Create columns with arithmetic, `.dt`, `map`, `np.where` and `np.select`, and say why `apply` is slow?
- [ ] Write a method chain with `assign` and `pipe`, and explain copy-on-write's three rules?

You can now load and shape clean tables. Real data is rarely clean: Part 4 is about **cleaning**.

---

# Part 4 — Moderate: Cleaning Data

> **Goal:** Turn a messy file into a clean, trustworthy table: handle missing values deliberately, remove duplicates, fix types, clean text, organise categories, and catch impossible values before they reach a chart or a model.  
> **You need:** Part 3.

Cleaning is often **most** of a data project, and it's where many wrong conclusions start. Every section in this part follows the same habit: **look → decide → fix → check → write down why**.

---

## 26. Missing Values: Finding, Dropping and Filling

![Three choices for a missing value: drop the row, fill it with something sensible, or keep it missing and flag it](images/data-science/26-missing.svg)

### Theory

> **In simple words:** real data has blanks: a customer skipped a question, a sensor failed, a field didn't exist last year. pandas marks them as **missing** (`NaN`). You must decide, column by column, whether to **drop** those rows, **fill** the blanks, or **keep** them as missing, and the right choice depends on **why** they're missing.

**Words to know:**

- **Missing value:** a cell with no data. pandas shows it as `NaN` (Not a Number, for numbers and text), `NaT` (Not a Time, for dates) or `<NA>` (for the newer "nullable" types).
- **`None`:** Python's "nothing" value; pandas converts it to a missing marker inside columns.
- **Nullable dtypes:** types like `Int64` (capital I), `boolean` and `Float64` that can hold `<NA>` without changing type. A normal `int64` column can't hold NaN, so one missing value turns it into `float64`.
- **Impute / imputation:** filling missing values with estimates.
- **Forward fill (`ffill`):** fill a gap with the last known value above it. **Backward fill (`bfill`):** with the next value below.
- **Interpolation:** estimating a gap from the values on both sides (a straight line between them, for example).
- **Missing indicator:** an extra True/False column recording that a value **was** missing, so the information isn't lost after filling.
- **Why values go missing (MCAR, MAR, MNAR):** statisticians' three cases, in plain words:
  - **MCAR (missing completely at random):** pure bad luck, unrelated to anything (a sensor glitch). Dropping rows is safe, just wasteful.
  - **MAR (missing at random):** missingness depends on **other columns you have** (older customers skip the "app rating" question more). Fill using those columns.
  - **MNAR (missing not at random):** missingness depends on the **missing value itself** (people with high incomes hide their income). Dangerous: no simple fix; flag it and say so.

**Everyday picture.** A class register with blanks. If a student was absent because the bus broke down (random), you can ignore that day. If the students who skipped the test were the ones who hadn't studied, then "average score of those who took it" makes the class look better than it is. **The reason for the blanks changes the right answer.**

**The decision, step by step:**

1. **Count** missing values per column: `df.isna().sum()` and as a share: `df.isna().mean()`.
2. **Look** at the rows with missing values: is there a pattern (a date, a source, a city)?
3. **Decide per column:**

| Situation | Action | Code |
|---|---|---|
| A few rows, can't be recovered, missing at random | drop those rows | `df.dropna(subset=["price"])` |
| A column that's mostly empty and not needed | drop the column | `df.drop(columns=["fax"])` |
| "Missing" really means zero / none (no discount recorded) | fill with that value | `df["discount"].fillna(0)` |
| A category | fill with `"Unknown"` (a real category) | `df["city"].fillna("Unknown")` |
| A skewed number (income, price) | fill with the **median** (not swayed by extremes), plus an indicator | `df["income"].fillna(df["income"].median())` |
| Time series (temperature, stock level) | carry the last value forward, or interpolate | `df["temp"].ffill()`, `.interpolate()` |
| Depends on a group (price by category) | fill with the group's median (Section [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking)) | `groupby(...).transform("median")` |
| The missingness itself is informative (MNAR) | keep missing and add an indicator column | `df["income_missing"] = df["income"].isna()` |

4. **Check** after: `df.isna().sum()` again, and compare key statistics before and after.
5. **Write down** what you did and why.

**`dropna` options:** `subset=[...]` (only look at these columns), `how="all"` (drop only rows where every value is missing), `thresh=3` (keep rows with at least 3 non-missing values), `axis=1` (drop columns instead of rows).

**Why filling with the mean is risky:** it pretends you know more than you do. Every filled row gets the same average value, which **shrinks the spread** of the column, weakens correlations, and can hide that the missing rows were different. For ML, impute **after** splitting into train and test sets, using only the training data's statistics (`machine-learning.md` explains why: otherwise information "leaks" from the test set).

**NaN behaves strangely:** `np.nan == np.nan` is **False** (missing isn't equal to anything, not even missing). Always test with `isna()`. Sums skip NaN by default (`skipna=True`), so `df["x"].sum()` quietly ignores blanks, and `count()` counts only non-missing values.

**Common mistakes:**

- ❌ `df.dropna()` with no `subset`, silently deleting half your rows because of one unimportant column. ✅ Check `df.isna().sum()` first; drop on the columns that matter.
- ❌ Filling everything with 0. A missing price is not a free product.
- ❌ `df[df["x"] == np.nan]` (always empty). ✅ `df[df["x"].isna()]`.
- ❌ Forgetting that `fillna` returns a new object. ✅ `df["x"] = df["x"].fillna(...)`.
- ❌ Not noticing that a column became `float64` because of one NaN (IDs printed as `1001.0`). ✅ Use `Int64`.

**Used in real software:** survey analysis (non-response), IoT and monitoring (sensor gaps filled with `ffill` or interpolation), finance (missing prices on holidays carried forward), ML pipelines (scikit-learn's `SimpleImputer` with `add_indicator=True`).

### Python

```python
import io
import numpy as np
import pandas as pd

csv_text = """id,date,city,age,income,rating,discount
1,2025-01-01,Pune,34,52000,4,
2,2025-01-02,,41,,5,10
3,2025-01-03,Mumbai,,61000,,
4,2025-01-04,Delhi,29,48000,3,5
5,,Pune,55,250000,,
6,2025-01-06,Mumbai,38,,4,
"""
df = pd.read_csv(io.StringIO(csv_text), parse_dates=["date"])
print(df)
print(df.isna().sum())
print(df.isna().mean().round(2).sort_values(ascending=False))     # share missing per column
print(np.nan == np.nan, pd.isna(np.nan), df["income"].sum(), df["income"].count())
```

**Output:**

```text
   id       date    city   age    income  rating  discount
0   1 2025-01-01    Pune  34.0   52000.0     4.0       NaN
1   2 2025-01-02     NaN  41.0       NaN     5.0      10.0
2   3 2025-01-03  Mumbai   NaN   61000.0     NaN       NaN
3   4 2025-01-04   Delhi  29.0   48000.0     3.0       5.0
4   5        NaT    Pune  55.0  250000.0     NaN       NaN
5   6 2025-01-06  Mumbai  38.0       NaN     4.0       NaN
id          0
date        1
city        1
age         1
income      2
rating      2
discount    4
dtype: int64
discount    0.67
income      0.33
rating      0.33
date        0.17
city        0.17
age         0.17
id          0.00
dtype: float64
False True 411000.0 4
```

```python
print(len(df.dropna()), len(df.dropna(subset=["city", "date"])), len(df.dropna(thresh=6)))

clean = df.assign(
    city=df["city"].fillna("Unknown"),
    discount=df["discount"].fillna(0),                                  # missing really means "no discount"
    income_missing=df["income"].isna(),                                 # keep the information
    income=df["income"].fillna(df["income"].median()),                  # median: not pulled up by 250,000
    rating=df["rating"].astype("Int64"),                                # nullable integer keeps <NA>
)
print(clean)
print(f"income mean {df['income'].mean():.0f}  median {df['income'].median():.0f}")
```

**Output:**

```text
1 4 2
   id       date     city   age    income  rating  discount  income_missing
0   1 2025-01-01     Pune  34.0   52000.0       4       0.0           False
1   2 2025-01-02  Unknown  41.0   56500.0       5      10.0            True
2   3 2025-01-03   Mumbai   NaN   61000.0    <NA>       0.0           False
3   4 2025-01-04    Delhi  29.0   48000.0       3       5.0           False
4   5        NaT     Pune  55.0  250000.0    <NA>       0.0           False
5   6 2025-01-06   Mumbai  38.0   56500.0       4       0.0            True
income mean 102750  median 56500
```

The one very high income (250,000) pulls the mean far above the typical value, which is why the median is the safer fill here. Notice `rating` shows `<NA>` and stays a whole-number column instead of turning into floats.

```python
temps = pd.Series([21.0, np.nan, np.nan, 24.0, np.nan, 23.0],
                  index=pd.date_range("2025-06-01", periods=6, freq="h"))
print(pd.DataFrame({"raw": temps, "ffill": temps.ffill(), "bfill": temps.bfill(),
                    "interpolate": temps.interpolate()}))

s = pd.Series([10, 20, 30, 40])
print(s.std().round(2), s.where(s != 20).fillna(s.mean()).std().round(2))   # mean-filling shrinks the spread
```

**Output:**

```text
                      raw  ffill  bfill  interpolate
2025-06-01 00:00:00  21.0   21.0   21.0         21.0
2025-06-01 01:00:00   NaN   21.0   24.0         22.0
2025-06-01 02:00:00   NaN   21.0   24.0         23.0
2025-06-01 03:00:00  24.0   24.0   24.0         24.0
2025-06-01 04:00:00   NaN   24.0   23.0         23.5
2025-06-01 05:00:00  23.0   23.0   23.0         23.0
12.91 12.5
```

`pd.date_range` makes evenly spaced timestamps (here one per hour, `freq="h"`; Section [37](#37-dates-and-times-parsing-dt-time-zones-and-periods)). `s.where(cond)` keeps values where the condition is true and makes the rest missing: an easy way to create a gap for a demo.

### Practice

1. In `df`, which rows are missing **both** `income` and `rating`? Which column has the highest share of missing values?
2. Fill missing `age` with the median age and add an `age_missing` column. What is the median?

<details>
<summary><b>Answer</b></summary>

```python
print(df[df["income"].isna() & df["rating"].isna()]["id"].tolist(), df.isna().mean().idxmax())
filled = df.assign(age_missing=df["age"].isna(), age=df["age"].fillna(df["age"].median()))
print(df["age"].median(), filled[["id", "age", "age_missing"]].to_dict("list"))
```

**Output:**

```text
[] discount
38.0 {'id': [1, 2, 3, 4, 5, 6], 'age': [34.0, 41.0, 38.0, 29.0, 55.0, 38.0], 'age_missing': [False, False, True, False, False, False]}
```

No row is missing both; `discount` is missing most often. (`to_dict("list")` prints each column as a list, handy for compact output.)

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [2883. Drop Missing Data](https://leetcode.com/problems/drop-missing-data/) | 🟢 Easy |
| 2 | [2887. Fill Missing Data](https://leetcode.com/problems/fill-missing-data/) | 🟢 Easy |
| 3 | [1965. Employees With Missing Information](https://leetcode.com/problems/employees-with-missing-information/) | 🟢 Easy |
| 4 | [577. Employee Bonus](https://leetcode.com/problems/employee-bonus/) | 🟢 Easy |

**Learn more:** [pandas: working with missing data](https://pandas.pydata.org/docs/user_guide/missing_data.html) · [Kaggle Learn: Data Cleaning](https://www.kaggle.com/learn/data-cleaning)

---

## 27. Duplicates, Data Types and Type Conversion

![Wrong types hide in plain sight: numbers stored as text, dates as strings, IDs as floats; convert them with errors="coerce" and inspect what failed](images/data-science/27-types.svg)

### Theory

> **In simple words:** two silent problems ruin analyses: the **same record counted twice** (duplicates), and **values stored as the wrong type** ("1,200" as text, so it can't be added; dates as strings, so they sort wrongly). Find duplicates with `duplicated`, and convert types with `to_numeric`, `to_datetime` and `astype`.

**Words to know:**

- **Duplicate row:** a row identical to another, in all columns or in the columns that should be unique.
- **Key / unique identifier:** the column(s) that should identify each row exactly once (`order_id`). A duplicate key is a red flag even if other columns differ.
- **`keep`:** which copy `drop_duplicates` keeps: `"first"`, `"last"`, or `False` (drop all copies).
- **Type conversion (casting):** changing a column's type.
- **Coerce:** force conversion and turn anything that fails into missing (`errors="coerce"`), instead of crashing.
- **Downcasting:** converting to a smaller type (`int64` → `int32`) to save memory.
- **Timestamp:** a date and time. **Epoch time:** seconds since 1 January 1970 (UTC), a common way APIs send times.
- **Locale formats:** country-specific ways of writing numbers and dates (`1.200,50` in Germany; `03/04/2025` is 3 April in India, March 4 in the USA).

**Everyday picture.** Duplicates are a guest who signed the wedding guestbook twice: the headcount is wrong, and nobody notices unless they look. Wrong types are prices written as words on the receipts: you can read them, but your calculator can't add "one thousand two hundred".

**Duplicates, step by step:**

1. Exact duplicates: `df.duplicated().sum()`.
2. Key duplicates: `df.duplicated(subset=["order_id"]).sum()`; look at them with `df[df.duplicated("order_id", keep=False)]` (`keep=False` marks **every** copy).
3. Decide: exact copies (double-loaded file) → drop. Same key, different values (an order updated later) → keep the latest (`sort_values("updated_at").drop_duplicates("order_id", keep="last")`) or investigate.
4. Check: the key is now unique: `df["order_id"].is_unique`.

**Type conversions:**

| Problem | Fix |
|---|---|
| Numbers as text with symbols: `"₹1,200"` | `pd.to_numeric(s.str.replace(r"[₹,]", "", regex=True), errors="coerce")` |
| Dates as text | `pd.to_datetime(s, format="%Y-%m-%d", errors="coerce")` |
| Day-first dates (`03/04/2025` = 3 April) | `pd.to_datetime(s, dayfirst=True)` or an explicit `format="%d/%m/%Y"` |
| Epoch seconds | `pd.to_datetime(s, unit="s")` |
| IDs read as floats (`1001.0`) | `s.astype("Int64")` (nullable) or `astype("str")` |
| "yes"/"no" text | `s.map({"yes": True, "no": False})` |
| Repeated labels | `s.astype("category")` (Section [29](#29-categorical-data-and-binning-cut-and-qcut)) |
| Let pandas pick the best nullable types | `df.convert_dtypes()` |

**The `errors="coerce"` habit:** convert, then **look at what became missing** that wasn't missing before. Those are your bad values: maybe a typo to fix, maybe a format you didn't expect.

**Date format codes** (used by `format=` and `strftime`): `%Y` 4-digit year, `%m` month, `%d` day, `%H` hour (24h), `%M` minute, `%S` second, `%b` short month name (`Jan`). Giving an explicit format is faster and avoids guessing wrong.

**When to convert:** right after loading, before any analysis. **When not to:** don't convert identifiers (phone numbers, ZIP codes, account numbers) to numbers: they're labels, and maths on them is meaningless; you'd also lose leading zeros.

**Common mistakes:**

- ❌ `astype(float)` on dirty text → crash on the first bad value. ✅ `pd.to_numeric(..., errors="coerce")`, then inspect.
- ❌ Letting pandas guess an ambiguous date format. ✅ `format=` or `dayfirst=True`.
- ❌ Dropping duplicates on all columns when the real key is `order_id` (rows with a changed timestamp survive). ✅ `subset=`.
- ❌ Assuming duplicates are errors: two identical small orders on one day can be real. ✅ Check the key and the business meaning.

**Used in real software:** data pipelines enforce unique keys (primary keys in databases); event tracking deduplicates repeated events from mobile apps retrying when offline; finance systems reconcile amounts parsed from text exports.

### Python

```python
import io
import pandas as pd

messy = pd.read_csv(io.StringIO("""order_id,customer,amount,paid,order_date,updated_at
1,Asha,"₹1,200",yes,2025-01-05,1736100000
2,Ravi,₹2500,no,2025-01-06,1736200000
2,Ravi,₹2500,no,2025-01-06,1736200000
3,Meera,pending,yes,2025-02-11,1736300000
4,Arjun,₹900,yes,not a date,1736400000
4,Arjun,₹950,yes,2025-02-20,1736500000
"""))
print(messy.dtypes)
print("exact duplicates:", messy.duplicated().sum(), "| duplicate keys:", messy.duplicated("order_id").sum())
print(messy[messy.duplicated("order_id", keep=False)][["order_id", "amount", "updated_at"]])
```

**Output:**

```text
order_id      int64
customer        str
amount          str
paid            str
order_date      str
updated_at    int64
dtype: object
exact duplicates: 1 | duplicate keys: 2
   order_id amount  updated_at
1         2  ₹2500  1736200000
2         2  ₹2500  1736200000
4         4   ₹900  1736400000
5         4   ₹950  1736500000
```

```python
df = (messy
      .drop_duplicates()                                                   # exact copies
      .assign(updated_at=lambda d: pd.to_datetime(d["updated_at"], unit="s"))
      .sort_values("updated_at")
      .drop_duplicates("order_id", keep="last"))                           # latest version of each order
print(df["order_id"].is_unique)

amount_text = df["amount"]
df["amount"] = pd.to_numeric(amount_text.str.replace(r"[₹,]", "", regex=True), errors="coerce")
df["order_date"] = pd.to_datetime(df["order_date"], format="%Y-%m-%d", errors="coerce")
df["paid"] = df["paid"].map({"yes": True, "no": False})

newly_missing = df["amount"].isna() & amount_text.notna()
print("could not parse:", amount_text[newly_missing].tolist())
print(df)
print(df.dtypes)
```

**Output:**

```text
True
could not parse: ['pending']
   order_id customer  amount   paid order_date          updated_at
0         1     Asha  1200.0   True 2025-01-05 2025-01-05 18:00:00
1         2     Ravi  2500.0  False 2025-01-06 2025-01-06 21:46:40
3         3    Meera     NaN   True 2025-02-11 2025-01-08 01:33:20
5         4    Arjun   950.0   True 2025-02-20 2025-01-10 09:06:40
order_id               int64
customer                 str
amount               float64
paid                    bool
order_date    datetime64[us]
updated_at     datetime64[s]
dtype: object
```

`r"[₹,]"` is a **regular expression** meaning "the character ₹ or a comma" (Section [28](#28-text-data-the-str-accessor-and-regular-expressions)); `regex=True` tells `replace` to treat it that way. `read_csv` already turns common markers like `n/a`, `NA` and empty cells into missing values on its own, so only truly unexpected text (here `pending`) shows up as a failure. Order 4's two versions collapsed to the later one (₹950), and the impossible date `not a date` became `NaT` instead of crashing.

```python
print(pd.to_datetime("03/04/2025", dayfirst=True).date(), pd.to_datetime("03/04/2025", format="%m/%d/%Y").date())
ids = pd.Series([1001, None, 1003])
print(ids.tolist(), ids.astype("Int64").tolist())
print(pd.DataFrame({"a": [1, None], "b": ["x", None], "c": [True, None]}).convert_dtypes().dtypes)
```

**Output:**

```text
2025-04-03 2025-03-04
[1001.0, nan, 1003.0] [1001, <NA>, 1003]
a      Int64
b     string
c    boolean
dtype: object
```

### Practice

1. `s = pd.Series(["12", "7.5", "eight", "", "1e3"])`: convert to numbers, and list the values that failed.
2. A table of logins has columns `user_id, login_time`. How do you keep only each user's **most recent** login?

<details>
<summary><b>Answer</b></summary>

```python
s = pd.Series(["12", "7.5", "eight", "", "1e3"])
nums = pd.to_numeric(s, errors="coerce")
print(nums.tolist(), s[nums.isna()].tolist())

logins = pd.DataFrame({"user_id": [1, 2, 1, 2, 3],
                       "login_time": pd.to_datetime(["2025-01-01", "2025-01-02", "2025-01-05", "2025-01-03", "2025-01-04"])})
print(logins.sort_values("login_time").drop_duplicates("user_id", keep="last").sort_values("user_id"))
```

**Output:**

```text
[12.0, 7.5, nan, nan, 1000.0] ['eight', '']
   user_id login_time
2        1 2025-01-05
3        2 2025-01-03
4        3 2025-01-04
```

`"1e3"` is scientific notation for 1,000, which `to_numeric` understands. (Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine)'s `groupby("user_id")["login_time"].max()` gives the same latest times.)

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [2882. Drop Duplicate Rows](https://leetcode.com/problems/drop-duplicate-rows/) | 🟢 Easy |
| 2 | [182. Duplicate Emails](https://leetcode.com/problems/duplicate-emails/) | 🟢 Easy |
| 3 | [196. Delete Duplicate Emails](https://leetcode.com/problems/delete-duplicate-emails/) | 🟢 Easy |
| 4 | [2886. Change Data Type](https://leetcode.com/problems/change-data-type/) | 🟢 Easy |
| 5 | [1890. The Latest Login in 2020](https://leetcode.com/problems/the-latest-login-in-2020/) | 🟢 Easy |

**Learn more:** [pandas: drop_duplicates](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop_duplicates.html) · [pandas: to_datetime](https://pandas.pydata.org/docs/reference/api/pandas.to_datetime.html) · [Python: strftime format codes](https://docs.python.org/3/library/datetime.html#format-codes)

---

## 28. Text Data: The .str Accessor and Regular Expressions

![A regular expression is a pattern: \d+ means one or more digits; ( ) captures the part you want to extract](images/data-science/28-regex.svg)

### Theory

> **In simple words:** text columns are messy: extra spaces, mixed capitals, three spellings of one city, numbers buried inside sentences. The `.str` accessor applies string methods to a **whole column** at once, and **regular expressions** let you describe patterns ("a 6-digit number", "an email address") to find, check, extract or replace them.

**Words to know:**

- **String:** text. **Substring:** a piece of a string.
- **`.str` accessor:** gives every Python string method (and more) to a pandas text column: `df["city"].str.lower()`.
- **Whitespace:** spaces, tabs and newlines. `strip` removes it from both ends.
- **Normalise text:** make variants identical (same case, no stray spaces, one spelling).
- **Regular expression (regex):** a mini-language for text patterns. Python's built-in `re` module and pandas `.str` methods understand it.
- **Character class:** a set of allowed characters in brackets: `[aeiou]`, `[0-9]`, `[A-Za-z]`.
- **Quantifier:** how many times something repeats: `+` (1 or more), `*` (0 or more), `?` (0 or 1), `{6}` (exactly 6), `{2,4}` (2 to 4).
- **Anchor:** a position, not a character: `^` (start of the string), `$` (end).
- **Capture group:** brackets `( )` around the part you want to **extract**. A **named group** `(?P<name>...)` becomes a column name.
- **Escape:** a backslash makes a special character literal: `\.` means a real dot (a bare `.` means "any character").
- **Raw string (`r"..."`):** a Python string where backslashes are kept as typed. Always write regexes as raw strings.
- **PII (personally identifiable information):** data that can identify a person (name, email, phone, address, ID numbers); it must be protected and often removed before sharing.

**Everyday picture.** A regular expression is a **template with blanks**, like a form that says "6 digits here" or "letters, then @, then letters, a dot, letters". Instead of checking each value by eye, you hold the template against every value at once.

**Regex building blocks:**

| Pattern | Matches | Example |
|---|---|---|
| `\d` | one digit 0–9 | `\d\d` matches `"42"` |
| `\w` | a "word" character (letter, digit, `_`) | `\w+` matches `"pune_01"` |
| `\s` | whitespace | `\s+` matches runs of spaces |
| `.` | any character (except newline) | `a.c` matches `"abc"`, `"a-c"` |
| `[A-Z]`, `[^0-9]` | one from a set / **not** in a set | `[^0-9]` matches `"x"` |
| `+`, `*`, `?`, `{n}`, `{n,m}` | repetition | `\d{6}` = exactly 6 digits |
| `^`, `$` | start, end | `^\d{6}$` = the **whole** value is 6 digits |
| `a\|b` | either | `cat\|dog` |
| `( )`, `(?P<name> )` | capture group | `(\d+)\s*kg` captures the number before "kg" |
| `\.`, `\$`, `\(` | literal special characters | `\.com$` = ends with ".com" |

**Regex traced** on `"Order #A-1042 shipped 3 items"` with `r"#([A-Z])-(\d+)"`: find `#` → capture one capital letter (`A`) → a literal `-` → capture one or more digits (`1042`). Result: groups `("A", "1042")`. The text before and after is ignored, because `extract` searches anywhere unless you anchor with `^`/`$`.

**The `.str` methods you'll use most:**

| Task | Code |
|---|---|
| Tidy | `.str.strip()`, `.str.lower()`, `.str.title()`, `.str.upper()` |
| Replace | `.str.replace("Bombay", "Mumbai")`, `.str.replace(r"\s+", " ", regex=True)` |
| Test | `.str.contains("x", case=False, na=False)`, `.str.startswith("A")`, `.str.fullmatch(r"\d{6}")` |
| Measure | `.str.len()`, `.str.count("a")` |
| Cut | `.str[:3]`, `.str.slice(0, 3)` |
| Split | `.str.split(",")` (lists), `.str.split(",", expand=True)` (columns), `.str.split(",").str[0]` |
| Extract | `.str.extract(r"(\d+)")` (first match, one column per group), `.str.extractall(...)` (every match) |
| Find all | `.str.findall(r"#\w+")` (lists of all matches, e.g. hashtags) |
| Join | `df["a"] + " " + df["b"]`, `.str.cat(sep=", ")` |
| Remove accents / unify Unicode | `.str.normalize("NFKD")` |

**`contains` vs `match` vs `fullmatch`:** `contains` finds the pattern **anywhere**; `match` only at the **start**; `fullmatch` requires the **whole** value to match (best for validation: "is this a valid PIN code?").

**A text-cleaning recipe:**

1. `strip` spaces, unify case.
2. Collapse internal whitespace: `.str.replace(r"\s+", " ", regex=True)`.
3. Map known variants to one spelling with a dict: `.replace({"Bombay": "Mumbai", "Bengaluru": "Bangalore"})`.
4. Check what's left: `value_counts()`; look at rare values, they're usually typos.
5. For fuzzy matches ("Mumbaai"), use a similarity library like `rapidfuzz` and review the suggestions by hand.

**When regex is the right tool:** structured patterns: codes, phone numbers, emails, dates in text, numbers with units. **When it isn't:** parsing HTML or JSON (use a parser), or understanding meaning ("is this review positive?"): that's NLP (`machine-learning.md`, `llm-engineering.md`).

**Common mistakes:**

- ❌ Forgetting `regex=True` in `.str.replace` when you meant a pattern (in pandas 3 the default is a **literal** replace). ✅ Pass `regex=True`, or `regex=False` when your text contains special characters like `.` or `$`.
- ❌ An unescaped `.` matching any character (`"a.b"` also matches `"axb"`). ✅ `\.`.
- ❌ `contains` for validation (`"12345678"` contains 6 digits). ✅ `fullmatch(r"\d{6}")`.
- ❌ Regex strings without `r` (`"\d"` happens to work, `"\b"` silently becomes a backspace character). ✅ Always `r"..."`.
- ❌ NaN in a text column breaking a filter. ✅ `na=False`.

**Used in real software:** log parsing (extract status codes and durations), cleaning product catalogues, validating form input (emails, phone numbers, PIN codes), extracting hashtags and mentions, detecting PII (personal data like card numbers) before sharing data.

### Python

```python
import pandas as pd

cities = pd.Series(["  pune", "PUNE ", "Bombay", "mumbai", "Bengaluru", "new   delhi", None])
clean = (cities.str.strip()
               .str.replace(r"\s+", " ", regex=True)
               .str.title()
               .replace({"Bombay": "Mumbai"}))
print(clean.tolist())
print(cities.nunique(), clean.nunique(), clean.value_counts(dropna=False).to_dict())
```

**Output:**

```text
['Pune', 'Pune', 'Mumbai', 'Mumbai', 'Bengaluru', 'New Delhi', nan]
6 4 {'Pune': 2, 'Mumbai': 2, 'Bengaluru': 1, 'New Delhi': 1, nan: 1}
```

```python
notes = pd.Series(["Order #A-1042 shipped 3 items", "order #B-77: 12 items", "no order code", None])
print(notes.str.extract(r"#(?P<series>[A-Z])-(?P<number>\d+)"))
print(notes.str.extract(r"(\d+)\s*items")[0].astype("Int64").tolist())
print(notes.str.contains("order", case=False, na=False).tolist())

tweets = pd.Series(["Loving #python and #pandas", "no tags here", "#data rocks"])
print(tweets.str.findall(r"#\w+").tolist(), tweets.str.len().tolist())

full = pd.Series(["Asha Rao", "Ravi Kumar Singh"])
print(full.str.split(" ", n=1, expand=True).set_axis(["first", "rest"], axis=1))
```

**Output:**

```text
  series number
0      A   1042
1      B     77
2    NaN    NaN
3    NaN    NaN
[3, 12, <NA>, <NA>]
[True, True, True, False]
[['#python', '#pandas'], [], ['#data']] [26, 12, 11]
  first         rest
0  Asha          Rao
1  Ravi  Kumar Singh
```

`expand=True` turns the pieces into columns; `n=1` splits only at the first space; `set_axis` names the new columns.

```python
emails = pd.Series(["asha@shop.in", "ravi@@shop.in", "zoya.k@mail.co.uk", "kabir@shop", "MEERA@SHOP.IN"])
pattern = r"[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}"
print(pd.DataFrame({"email": emails, "valid": emails.str.fullmatch(pattern)}))

pins = pd.Series(["411001", "4110011", "41100A", "560034"])
print(pins.str.contains(r"\d{6}").tolist(), pins.str.fullmatch(r"\d{6}").tolist())   # contains is not validation
```

**Output:**

```text
               email  valid
0       asha@shop.in   True
1      ravi@@shop.in  False
2  zoya.k@mail.co.uk   True
3         kabir@shop  False
4      MEERA@SHOP.IN   True
[True, True, False, True] [True, False, False, True]
```

The email pattern reads: one or more allowed characters, `@`, a domain, a literal dot, and at least two letters at the end. Real email validation is famously messy; patterns like this catch obvious typos, and the only true test is sending a confirmation email.

### Practice

1. From `pd.Series(["Weight: 72 kg", "weight 65kg", "n/a", "80 KG"])`, extract the weights as numbers.
2. Clean `pd.Series([" asha  RAO ", "ravi kumar", "ZOYA"])` into title case with single spaces, then make a column of initials (`"AR"`, `"RK"`, `"Z"`).

<details>
<summary><b>Answer</b></summary>

```python
w = pd.Series(["Weight: 72 kg", "weight 65kg", "n/a", "80 KG"])
print(w.str.extract(r"(\d+)\s*kg", flags=2)[0].astype("Int64").tolist())   # flags=2 is re.IGNORECASE

names = pd.Series([" asha  RAO ", "ravi kumar", "ZOYA"]).str.strip().str.replace(r"\s+", " ", regex=True).str.title()
print(names.tolist(), names.str.split().apply(lambda parts: "".join(p[0] for p in parts)).tolist())
```

**Output:**

```text
[72, 65, <NA>, 80]
['Asha Rao', 'Ravi Kumar', 'Zoya'] ['AR', 'RK', 'Z']
```

`flags=2` is the number behind `re.IGNORECASE`; writing `import re` and `flags=re.IGNORECASE` is clearer. The initials step uses `apply` because each name has a different number of parts; it's fine for small data.

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [1667. Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table/) | 🟢 Easy |
| 2 | [1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/) | 🟢 Easy |
| 3 | [1527. Patients With a Condition](https://leetcode.com/problems/patients-with-a-condition/) | 🟢 Easy |
| 4 | [1517. Find Users With Valid E-Mails](https://leetcode.com/problems/find-users-with-valid-e-mails/) | 🟢 Easy |
| 5 | [3436. Find Valid Emails](https://leetcode.com/problems/find-valid-emails/) | 🟢 Easy |
| 6 | [3465. Find Products with Valid Serial Numbers](https://leetcode.com/problems/find-products-with-valid-serial-numbers/) | 🟢 Easy |
| 7 | [3475. DNA Pattern Recognition](https://leetcode.com/problems/dna-pattern-recognition/) | 🟡 Medium |
| 8 | [3374. First Letter Capitalization II](https://leetcode.com/problems/first-letter-capitalization-ii/) | 🔴 Hard |
| 9 | [3451. Find Invalid IP Addresses](https://leetcode.com/problems/find-invalid-ip-addresses/) | 🔴 Hard |

**Learn more:** [pandas: working with text data](https://pandas.pydata.org/docs/user_guide/text.html) · [Python: regular expression HOWTO](https://docs.python.org/3/howto/regex.html) · [regex101 (test patterns interactively)](https://regex101.com/)

---

## 29. Categorical Data and Binning (cut and qcut)

![cut splits by value ranges you choose; qcut splits so each bin has the same number of rows](images/data-science/29-cut-qcut.svg)

### Theory

> **In simple words:** a **category** column holds a small set of repeated labels (city, size, plan). pandas' `category` type stores each label once and keeps a number per row, which saves memory and lets you give labels an **order** (S < M < L). **Binning** turns numbers into categories: ages into age bands, prices into tiers.

**Words to know:**

- **Category dtype:** pandas' type for repeated labels. Internally: a list of the distinct labels (the **categories**) and a small integer **code** per row pointing into it.
- **Cardinality:** how many distinct values a column has. Low cardinality (a few cities) suits `category`; high cardinality (customer emails) doesn't.
- **Ordered categorical:** categories with a meaningful order, so sorting and comparisons (`size > "M"`) work.
- **Binning (discretisation, bucketing):** grouping numbers into ranges called **bins**.
- **Bin edges:** the boundary values. `(0, 500]` means "above 0, up to and including 500": a **round** bracket excludes the edge, a **square** bracket includes it.
- **`cut`:** bins by edges **you choose** (or equal-width ranges).
- **`qcut`:** bins by **quantiles**, so each bin holds about the same number of rows (quartiles = 4 bins, deciles = 10).
- **Rare categories:** labels that appear only a few times; often grouped into "Other".

**Everyday picture.** A coat-check counter: instead of writing each guest's full coat description on every ticket, the counter keeps one shelf per coat type and hands out **numbered tickets**. That's a category column: labels stored once, small codes per row. Binning is sorting exam scores into grades: A for 85+, B for 70–84, and so on.

**How a category column is stored,** for `["Pune", "Delhi", "Pune", "Pune", "Goa"]`:

| Categories (stored once) | Codes (one small integer per row) |
|---|---|
| 0 → Delhi, 1 → Goa, 2 → Pune | `[2, 0, 2, 2, 1]` |

A million rows of city names become a million 1-byte codes plus a few labels: often **10–50× less memory** than text.

**`cut` vs `qcut`, traced** on prices `[60, 250, 350, 900, 1200, 1800, 2500, 2500]`:

| Method | Bins | Rows per bin |
|---|---|---|
| `pd.cut(p, [0, 500, 2000, inf], labels=["budget", "mid", "premium"])` | (0, 500], (500, 2000], (2000, ∞) | 3, 3, 2 |
| `pd.qcut(p, 4)` (quartiles) | edges at the 0/25/50/75/100% quantiles | 2, 2, 2, 2 |

Use `cut` when the edges have **meaning** (tax slabs, age bands, business tiers). Use `qcut` to split customers into equal-sized groups ("top 25% spenders").

**Category operations:**

| Code | Does |
|---|---|
| `s.astype("category")` | convert |
| `pd.Categorical(s, categories=["S", "M", "L"], ordered=True)` | ordered categories |
| `s.cat.categories`, `s.cat.codes` | the labels; the codes |
| `s.cat.rename_categories({...})`, `s.cat.add_categories([...])` | edit labels |
| `s.value_counts(normalize=True)` | share of each category |
| `s.where(s.map(s.value_counts()) >= 10, "Other")` | group rare labels into "Other" |

**When to use `category`:** low-cardinality text columns in big tables (memory, speed), ordinal data (sizes, ratings, education level), and ML preparation (many libraries understand pandas categories). **When not to:** columns with mostly unique values, or text you'll keep editing freely (adding a new value to a category column requires adding the category first).

**Common mistakes:**

- ❌ Sorting ordinal text alphabetically (`L, M, S, XL`). ✅ An ordered categorical.
- ❌ `groupby` on a category column showing empty groups for categories with no rows. ✅ `observed=True` (the default in pandas 3).
- ❌ Bins that don't cover all values: values outside the edges become NaN silently. ✅ Use `-np.inf`/`np.inf` as outer edges, and check `isna()`.
- ❌ Binning a number before a model when the raw number works better: binning throws information away. Bin for **reporting**; let models see the number.

**Used in real software:** age bands and income bands in reports; customer segmentation into deciles of spend; T-shirt sizes and subscription tiers in e-commerce; memory savings in large analytics tables (Section [40](#40-memory-dtypes-categoricals-chunking-and-apache-arrow)).

### Python

```python
import numpy as np
import pandas as pd

rng = np.random.default_rng(0)
cities = pd.Series(rng.choice(["Pune", "Mumbai", "Delhi", "Goa"], size=1_000_000))
as_cat = cities.astype("category")
print(f"str: {cities.memory_usage(deep=True) / 1e6:.1f} MB   category: {as_cat.memory_usage(deep=True) / 1e6:.1f} MB")
print(as_cat.cat.categories.tolist(), as_cat.cat.codes[:5].tolist(), cities[:5].tolist())

sizes = pd.Series(["M", "S", "XL", "L", "M"])
print(sizes.sort_values().tolist())                                     # alphabetical: wrong order
ordered = pd.Categorical(sizes, categories=["S", "M", "L", "XL"], ordered=True)
print(pd.Series(ordered).sort_values().tolist(), (pd.Series(ordered) > "M").tolist())
```

**Output:**

```text
str: 12.5 MB   category: 1.0 MB
['Delhi', 'Goa', 'Mumbai', 'Pune'] [1, 0, 0, 2, 2] ['Goa', 'Delhi', 'Delhi', 'Mumbai', 'Mumbai']
['L', 'M', 'M', 'S', 'XL']
['S', 'M', 'M', 'L', 'XL'] [False, False, True, True, False]
```

`memory_usage(deep=True)` counts the real bytes, including the text itself.

```python
prices = pd.Series([60, 250, 350, 900, 1200, 1800, 2500, 2500])
tiers = pd.cut(prices, bins=[0, 500, 2000, np.inf], labels=["budget", "mid", "premium"])
quart = pd.qcut(prices, q=4, labels=["Q1", "Q2", "Q3", "Q4"])
print(pd.DataFrame({"price": prices, "tier": tiers, "quartile": quart}))
print(tiers.value_counts(sort=False).to_dict(), quart.value_counts(sort=False).to_dict())
print(pd.cut(prices, bins=3).cat.categories.tolist())                    # 3 equal-WIDTH ranges

plans = pd.Series(["free"] * 6 + ["pro"] * 3 + ["team", "edu"])
counts = plans.map(plans.value_counts())
print(plans.where(counts >= 2, "Other").value_counts().to_dict())       # rare labels → "Other"
```

**Output:**

```text
   price     tier quartile
0     60   budget       Q1
1    250   budget       Q1
2    350   budget       Q2
3    900      mid       Q2
4   1200      mid       Q3
5   1800      mid       Q3
6   2500  premium       Q4
7   2500  premium       Q4
{'budget': 3, 'mid': 3, 'premium': 2} {'Q1': 2, 'Q2': 2, 'Q3': 2, 'Q4': 2}
[Interval(57.56, 873.333, closed='right'), Interval(873.333, 1686.667, closed='right'), Interval(1686.667, 2500.0, closed='right')]
{'free': 6, 'pro': 3, 'Other': 2}
```

`pd.cut(prices, bins=3)` makes 3 ranges of equal width between the minimum and maximum (the edges extend a tiny bit, 0.1%, so the minimum is included).

### Practice

1. Bin ages `[5, 17, 18, 34, 35, 64, 65, 90]` into `child` (0–17), `adult` (18–64) and `senior` (65+). Check that 17 and 18 fall in different bins.
2. Split 1,000 random spend values into deciles (10 equal groups) and confirm each has 100 rows.

<details>
<summary><b>Answer</b></summary>

```python
ages = pd.Series([5, 17, 18, 34, 35, 64, 65, 90])
print(pd.cut(ages, bins=[-np.inf, 17, 64, np.inf], labels=["child", "adult", "senior"]).tolist())
spend = pd.Series(np.random.default_rng(1).exponential(500, 1000))
print(pd.qcut(spend, 10, labels=False).value_counts().unique())
```

**Output:**

```text
['child', 'child', 'adult', 'adult', 'adult', 'adult', 'senior', 'senior']
[100]
```

The edges `(−∞, 17]`, `(17, 64]`, `(64, ∞)` put 17 in `child` and 18 in `adult`. `labels=False` returns bin numbers 0–9 instead of interval labels.

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [1907. Count Salary Categories](https://leetcode.com/problems/count-salary-categories/) | 🟡 Medium |
| 2 | [1873. Calculate Special Bonus](https://leetcode.com/problems/calculate-special-bonus/) | 🟢 Easy |

**Learn more:** [pandas: categorical data](https://pandas.pydata.org/docs/user_guide/categorical.html) · [pandas: cut](https://pandas.pydata.org/docs/reference/api/pandas.cut.html) · [pandas: qcut](https://pandas.pydata.org/docs/reference/api/pandas.qcut.html)

---

## 30. Outliers and Data Validation

![The IQR rule: values beyond 1.5 × IQR outside the middle 50% are flagged as possible outliers](images/data-science/30-iqr.svg)

### Theory

> **In simple words:** an **outlier** is a value far from the rest: a ₹2,50,000 order in a shop of ₹500 orders, an age of 200. Some are **errors** (typos, unit mix-ups), some are **real and important** (a fraud, a VIP customer). Find them with simple rules, then **investigate before deciding**. **Validation** means writing down the rules your data must obey and checking them automatically, every time.

**Words to know:**

- **Outlier:** an observation far from most others.
- **Quartiles (Q1, Q3):** the values below which 25% and 75% of the data fall.
- **IQR (interquartile range):** Q3 − Q1, the width of the middle 50% of the data.
- **IQR rule (Tukey's fences):** flag values below Q1 − 1.5 × IQR or above Q3 + 1.5 × IQR. This is what a box plot's whiskers show (Section [46](#46-seaborn-i-distributions)).
- **z-score:** how many standard deviations a value is from the mean: z = (x − mean) / std. |z| > 3 is a common outlier flag for bell-shaped data.
- **Robust:** not easily distorted by extreme values. The median and IQR are robust; the mean and standard deviation are not.
- **Winsorising (capping, clipping):** replacing extreme values with a chosen limit (e.g. the 1st and 99th percentiles) instead of deleting them.
- **Log transform:** taking `log` of a skewed positive column so huge values are pulled closer to the rest.
- **Data validation:** automatically checking data against rules: types, ranges, allowed values, uniqueness, relationships between columns.
- **Schema (data contract):** the agreed rules for a table: column names, types and checks.
- **pandera:** a Python library for declaring DataFrame schemas and validating them.
- **Assertion:** a check in code that stops the program if something that must be true isn't: `assert df["qty"].ge(1).all()`.

**Everyday picture.** A teacher marking exams sees one score of 310 out of 100. It's not "an unusually good student": it's a typo, probably 31. Another student scored 100 when everyone else scored 40–70: that's real, and the most interesting result in the class. **Flag, look, then decide**: never delete automatically.

**Finding outliers with the IQR rule, traced** on order values `[300, 350, 400, 420, 450, 480, 500, 520, 2500]`:

| Step | Value |
|---|---|
| Q1 (25th percentile) | 400 |
| Q3 (75th percentile) | 500 |
| IQR = Q3 − Q1 | 100 |
| Lower fence = Q1 − 1.5 × IQR | 250 |
| Upper fence = Q3 + 1.5 × IQR | 650 |
| Flagged | 2500 |

**Why not just the z-score?** The extreme value itself inflates the mean and standard deviation, which can **hide** it (with few data points, one huge value may only reach z ≈ 2.7). The IQR rule uses quartiles, which one extreme value barely moves. Use z-scores for large, roughly bell-shaped data; the IQR rule or **domain rules** otherwise.

**Domain rules beat statistics.** You know things the data doesn't: quantities are ≥ 1, ages are 0–120, delivery can't happen before the order, a discount can't exceed the price. Write them down and check them.

**What to do with an outlier:**

| Cause | Action |
|---|---|
| Data entry or unit error (age 200, price in paise instead of rupees) | fix if you can tell the right value; otherwise make it missing |
| Test or internal data (orders from staff accounts) | remove, with a documented rule |
| Real but extreme (a bulk corporate order) | **keep**; analyse with robust statistics (median), report it separately, or log-transform for charts and models |
| Real and the point of the analysis (fraud, failures) | keep, and study it |

**Validation, step by step:**

1. Write the rules: types, allowed ranges, allowed categories, uniqueness, not-null, cross-column checks.
2. Encode them (plain assertions, or a pandera schema).
3. Run them **every time** data is loaded, in notebooks and pipelines.
4. Fail loudly with a clear message listing the bad rows; don't silently "fix" in the check.

**When to validate:** at every boundary: after loading raw data, after cleaning, before saving or training a model. **Tools:** plain `assert` for notebooks; **pandera** for DataFrame schemas in code; **Great Expectations** or **dbt tests** (Section [62](#62-data-pipelines-and-data-quality-in-production)) in production pipelines.

**Common mistakes:**

- ❌ Deleting every value outside 3 standard deviations. You may delete your most important customers.
- ❌ Computing outlier fences on one group and applying them to everything (prices differ by category). ✅ Fences per group when groups differ.
- ❌ Validation that prints a warning nobody reads. ✅ Make it fail.
- ❌ Fixing outliers without recording what changed. ✅ Keep the original column, or log the changes.

**Used in real software:** fraud detection (outliers are the target), monitoring alerts (a metric outside its normal band), data pipelines that refuse to publish a table failing its checks (data contracts), sensor systems rejecting physically impossible readings.

### Python

```python
import numpy as np
import pandas as pd

values = pd.Series([300, 350, 400, 420, 450, 480, 500, 520, 2500])
q1, q3 = values.quantile([0.25, 0.75])
iqr = q3 - q1
low, high = q1 - 1.5 * iqr, q3 + 1.5 * iqr
print(f"Q1={q1} Q3={q3} IQR={iqr} fences=({low}, {high})")
print("IQR flags:", values[(values < low) | (values > high)].tolist())

z = (values - values.mean()) / values.std()
print("z-scores:", z.round(2).tolist())
print("|z| > 3 flags:", values[z.abs() > 3].tolist(), "<- the outlier hides itself")
print("capped:", values.clip(upper=values.quantile(0.9)).round(1).tolist())
print("log10:", np.log10(values).round(2).tolist())
```

**Output:**

```text
Q1=400.0 Q3=500.0 IQR=100.0 fences=(250.0, 650.0)
IQR flags: [2500]
z-scores: [-0.52, -0.44, -0.37, -0.34, -0.3, -0.26, -0.23, -0.2, 2.65]
|z| > 3 flags: [] <- the outlier hides itself
capped: [300.0, 350.0, 400.0, 420.0, 450.0, 480.0, 500.0, 520.0, 916.0]
log10: [2.48, 2.54, 2.6, 2.62, 2.65, 2.68, 2.7, 2.72, 3.4]
```

```python
orders = pd.DataFrame({
    "order_id": [1, 2, 3, 4, 5, 5],
    "qty": [2, 0, 1, 3, 1, 1],
    "price": [350.0, 1200.0, -50.0, 900.0, 250.0, 250.0],
    "city": ["Pune", "Mumbai", "Delhi", "Paris", "Goa", "Goa"],
    "ordered": pd.to_datetime(["2025-01-05", "2025-01-06", "2025-01-07", "2025-01-08", "2025-01-09", "2025-01-09"]),
    "delivered": pd.to_datetime(["2025-01-07", "2025-01-05", "2025-01-09", "2025-01-10", "2025-01-12", "2025-01-12"]),
})

rules = {
    "qty is at least 1": orders["qty"] >= 1,
    "price is positive": orders["price"] > 0,
    "city is known": orders["city"].isin(["Pune", "Mumbai", "Delhi", "Goa", "Bengaluru"]),
    "delivered after ordered": orders["delivered"] >= orders["ordered"],
    "order_id is unique": ~orders["order_id"].duplicated(keep=False),
}
report = pd.DataFrame(rules)
print(report.all())                                   # which rules hold for every row
print(orders[~report.all(axis=1)][["order_id", "qty", "price", "city"]])   # rows breaking any rule
```

**Output:**

```text
qty is at least 1          False
price is positive          False
city is known              False
delivered after ordered    False
order_id is unique         False
dtype: bool
   order_id  qty   price    city
1         2    0  1200.0  Mumbai
2         3    1   -50.0   Delhi
3         4    3   900.0   Paris
4         5    1   250.0     Goa
5         5    1   250.0     Goa
```

Each rule is a boolean Series (one True/False per row); putting them in a DataFrame gives a pass/fail grid. `report.all()` checks each rule down the rows; `report.all(axis=1)` checks each row across the rules.

```python
import pandera.pandas as pa

schema = pa.DataFrameSchema(
    {
        "order_id": pa.Column(int, unique=True),
        "qty": pa.Column(int, pa.Check.ge(1)),
        "price": pa.Column(float, pa.Check.gt(0)),
        "city": pa.Column(str, pa.Check.isin(["Pune", "Mumbai", "Delhi", "Goa", "Bengaluru"])),
    },
)
try:
    schema.validate(orders, lazy=True)                  # lazy=True: collect ALL failures, not just the first
except pa.errors.SchemaErrors as err:
    print(err.failure_cases[["column", "check", "failure_case", "index"]].to_string())
```

**Output:**

```text
     column                                                  check failure_case  index
0  order_id                                       field_uniqueness            5      4
1  order_id                                       field_uniqueness            5      5
2       qty                            greater_than_or_equal_to(1)            0      1
3     price                                        greater_than(0)        -50.0      2
4      city  isin(['Pune', 'Mumbai', 'Delhi', 'Goa', 'Bengaluru'])        Paris      3
```

pandera lists every failing value with its column, the rule it broke and its row. In a pipeline, that exception stops bad data from going any further.

### Practice

1. Using the IQR rule **per city**, flag outliers in `pd.DataFrame({"city": ["A"]*6 + ["B"]*6, "value": [10, 11, 12, 13, 12, 40, 100, 105, 98, 102, 101, 300]})`. Why would one global fence be wrong here?
2. Add a validation rule to the `rules` dict: "price × qty is at most 10,000".

<details>
<summary><b>Answer</b></summary>

```python
d = pd.DataFrame({"city": ["A"] * 6 + ["B"] * 6, "value": [10, 11, 12, 13, 12, 40, 100, 105, 98, 102, 101, 300]})

def iqr_flags(s):
    q1, q3 = s.quantile([0.25, 0.75])
    return (s < q1 - 1.5 * (q3 - q1)) | (s > q3 + 1.5 * (q3 - q1))

d["flag"] = d.groupby("city")["value"].transform(iqr_flags)
print(d[d["flag"]])
print("global flags:", d.loc[iqr_flags(d["value"]), "value"].tolist())

rules["order value at most 10,000"] = orders["price"] * orders["qty"] <= 10_000
print(pd.DataFrame(rules).all().tail(1))
```

**Output:**

```text
   city  value  flag
5     A     40  True
11    B    300  True
global flags: [300]
order value at most 10,000    True
dtype: bool
```

Per city, 40 (city A) and 300 (city B) are flagged. A single global fence mixes two very different scales, so it misses 40 completely: compared with city B's values, 40 doesn't look extreme. (`groupby(...).transform(func)` runs the function on each city's values and lines the results back up with the rows; Section [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking) explains it.)

</details>

| # | Problem | Difficulty |
|---|---|---|
| 1 | [LeetCode 1795. Rearrange Products Table](https://leetcode.com/problems/rearrange-products-table/) (missing values + reshaping) | 🟢 Easy |
| 2 | [Deep-ML 78. Descriptive Statistics Calculator](https://www.deep-ml.com/problems/78) | 🟢 Easy |

**Learn more:** [pandera: DataFrame schemas](https://pandera.readthedocs.io/en/stable/dataframe_schemas.html) · [NIST: what are outliers?](https://www.itl.nist.gov/div898/handbook/prc/section1/prc16.htm)

---

### ✅ Part 4 checkpoint

Without looking, can you:

- [ ] Count missing values per column and choose between dropping, filling and flagging, with a reason?
- [ ] Explain MCAR, MAR and MNAR with an everyday example, and why mean-filling shrinks the spread?
- [ ] Find exact and key duplicates, and keep the latest version of each record?
- [ ] Convert messy text to numbers and dates with `errors="coerce"`, and list what failed to convert?
- [ ] Clean a text column with `.str` methods and write a regex that extracts a number?
- [ ] Explain the difference between `contains`, `match` and `fullmatch`?
- [ ] Use an ordered categorical, and bin numbers with `cut` and `qcut`?
- [ ] Flag outliers with the IQR rule, say why z-scores can miss them, and decide what to do with each?
- [ ] Write validation rules and make them fail loudly?

Your table is clean. Part 5 asks it questions: **per group**, **combined with other tables**, **over time**.

---

# Part 5 — Moderate: Analysing Data

> **Goal:** Answer the questions analysts get every day: totals and averages **per group**, values **compared with** their group, information **combined from several tables**, tables **reshaped** for reports, and patterns **over time**.  
> **You need:** Parts 3–4. Knowing SQL's `GROUP BY` and `JOIN` (`sql-postgresql.md`) helps but isn't required: each idea is explained from scratch with its SQL equivalent alongside.

---

## 31. Grouping I: groupby, agg and Split-Apply-Combine

![groupby splits rows into groups, applies a function to each group, and combines the results](images/data-science/04-groupby.svg)

### Theory

> **In simple words:** `groupby` answers "**per** something" questions: total sales **per city**, average price **per category**, orders **per customer per month**. It works in three steps called **split–apply–combine**: **split** the rows into groups by a key, **apply** a calculation to each group, and **combine** the answers into a new, smaller table. It's pandas' version of SQL's `GROUP BY`.

**Words to know:**

- **Grouping key:** the column(s) whose values define the groups (`city`).
- **Group:** all rows sharing one key value (all Pune orders).
- **Aggregate / aggregation function:** a function that turns a group's many values into one: `sum`, `mean`, `count`, `max`, …
- **Split–apply–combine:** the three-step pattern above, named by Hadley Wickham.
- **Named aggregation:** `agg(new_name=("column", "function"))`: choose the output column names yourself.
- **`size` vs `count`:** `size` counts **rows** in each group; `count` counts **non-missing values** in a column.
- **`nunique`:** the number of distinct values per group.
- **Multi-key grouping:** grouping by several columns at once (`["city", "category"]`): one group per combination that exists.
- **`as_index=False` / `reset_index()`:** keep the keys as ordinary columns instead of moving them into the index.
- **Funnel:** the sequence of steps users go through (view → cart → purchase); **funnel analysis** measures how many make it from each step to the next.

**Everyday picture.** A teacher has a pile of answer sheets from three classes. **Split:** sort the pile into three stacks by class. **Apply:** for each stack, work out the average mark. **Combine:** write a little table with one line per class. `groupby` does exactly this, for any column and any calculation.

**Traced by hand:** `orders.groupby("city")["revenue"].sum()` on

| city | revenue |
|---|---|
| Pune | 300 |
| Mumbai | 2500 |
| Pune | 1200 |
| Delhi | 1000 |
| Mumbai | 700 |

1. **Split** → Pune: [300, 1200] · Mumbai: [2500, 700] · Delhi: [1000]
2. **Apply** `sum` → Pune: 1500 · Mumbai: 3200 · Delhi: 1000
3. **Combine** → a Series indexed by city (sorted by key): Delhi 1000, Mumbai 3200, Pune 1500.

**The patterns you'll use daily:**

| Code | Answers | SQL |
|---|---|---|
| `df.groupby("city")["revenue"].sum()` | total per city | `SELECT city, SUM(revenue) ... GROUP BY city` |
| `df.groupby("city").size()` | rows per city | `COUNT(*)` |
| `df.groupby("city")["customer"].nunique()` | distinct customers per city | `COUNT(DISTINCT customer)` |
| `df.groupby(["city", "category"])["revenue"].mean()` | average per (city, category) | `GROUP BY city, category` |
| `df.groupby("city").agg(orders=("order_id", "count"), revenue=("revenue", "sum"))` | several named results | several aggregates with `AS` |
| `df.groupby("city")["revenue"].agg(["sum", "mean", "max"])` | several functions on one column | |
| `df.groupby("city", as_index=False)["revenue"].sum()` | the same, with `city` as a column | |
| `df.groupby(df["date"].dt.month)["revenue"].sum()` | group by a computed key | `GROUP BY EXTRACT(MONTH FROM date)` |

**Aggregation functions:** `sum`, `mean`, `median`, `min`, `max`, `count`, `size`, `nunique`, `std`, `var`, `first`, `last`, `idxmax` / `idxmin` (the row label of the max/min), `quantile(0.9)`, and any function you write (`lambda s: s.max() - s.min()`), which is slower than built-ins.

**Filtering groups ("HAVING"):** aggregate first, then filter the result: `per_city = df.groupby("city")["revenue"].sum(); per_city[per_city > 2000]`. (To keep the **original rows** of the qualifying groups instead, use `groupby(...).filter`, Section [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking).)

**Sorting results:** the result is sorted by key; for "top groups", add `.sort_values(ascending=False)`.

**Missing keys:** rows whose key is NaN are **dropped** from the groups by default. Use `dropna=False` to keep them as their own group.

**When to use:** any summary by category, time period or segment. **When not to:** if you need each row **plus** its group's number side by side, that's `transform` (next section); a `groupby` + `merge` back also works but is longer.

**Common mistakes:**

- ❌ Forgetting `reset_index()` and then failing to merge or save because `city` is the index, not a column.
- ❌ Using `count` when you meant `size` (they differ when values are missing).
- ❌ Writing a Python loop (`for city in df["city"].unique(): ...`) instead of one `groupby`.
- ❌ Averaging averages: the mean of per-store means isn't the overall mean when stores have different numbers of orders. ✅ Compute totals and counts, then divide.
- ❌ Silently losing rows with a missing key. ✅ `dropna=False` when missing keys matter.

**Used in real software:** every business dashboard (revenue per region per month), cohort and funnel analysis, feature engineering for ML (a customer's order count and average spend, Section [61](#61-feature-engineering-preparing-data-for-machine-learning)), monitoring (errors per service per minute).

### Python

```python
import io
import pandas as pd

csv_text = """order_id,date,customer,city,product,category,qty,price
1,2025-01-05,Asha,Pune,Notebook,stationery,5,60
2,2025-01-06,Ravi,Mumbai,Headphones,electronics,1,2500
3,2025-02-10,Asha,Pune,Backpack,bags,1,1200
4,2025-02-11,Meera,Pune,Keyboard,electronics,1,1800
5,2025-03-02,Zoya,Mumbai,Water bottle,kitchen,2,350
6,2025-03-15,Kabir,Bengaluru,Desk lamp,electronics,1,900
7,2025-03-20,Asha,Pune,Headphones,electronics,1,2500
8,2025-04-01,Isha,Delhi,Mug,kitchen,4,250
9,2025-04-18,Ravi,Mumbai,Notebook,stationery,10,60
10,2025-05-05,Zoya,Mumbai,Keyboard,electronics,1,1800
"""
orders = pd.read_csv(io.StringIO(csv_text), parse_dates=["date"])
orders["revenue"] = orders["qty"] * orders["price"]

print(orders.groupby("city")["revenue"].sum().sort_values(ascending=False))
print(orders.groupby("city").size().to_dict(), orders.groupby("city")["customer"].nunique().to_dict())
print(orders.groupby(["city", "category"])["revenue"].sum().head(4))
```

**Output:**

```text
city
Pune         5800
Mumbai       5600
Delhi        1000
Bengaluru     900
Name: revenue, dtype: int64
{'Bengaluru': 1, 'Delhi': 1, 'Mumbai': 4, 'Pune': 4} {'Bengaluru': 1, 'Delhi': 1, 'Mumbai': 2, 'Pune': 2}
city       category   
Bengaluru  electronics     900
Delhi      kitchen        1000
Mumbai     electronics    4300
           kitchen         700
Name: revenue, dtype: int64
```

```python
summary = (orders.groupby("city")
           .agg(orders=("order_id", "count"),
                customers=("customer", "nunique"),
                revenue=("revenue", "sum"),
                avg_order=("revenue", "mean"),
                biggest=("revenue", "max"))
           .round(1)
           .sort_values("revenue", ascending=False)
           .reset_index())
print(summary)

per_month = orders.groupby(orders["date"].dt.to_period("M"))["revenue"].sum()   # a computed key
print(per_month)

per_city = orders.groupby("city")["revenue"].sum()
print(per_city[per_city > 2000].index.tolist())                                  # like SQL HAVING
print(orders.groupby("category")["revenue"].agg(["sum", "mean", "max"]).round(0))
```

**Output:**

```text
        city  orders  customers  revenue  avg_order  biggest
0       Pune       4          2     5800     1450.0     2500
1     Mumbai       4          2     5600     1400.0     2500
2      Delhi       1          1     1000     1000.0     1000
3  Bengaluru       1          1      900      900.0      900
date
2025-01    2800
2025-02    3000
2025-03    4100
2025-04    1600
2025-05    1800
Freq: M, Name: revenue, dtype: int64
['Mumbai', 'Pune']
              sum    mean   max
category                       
bags         1200  1200.0  1200
electronics  9500  1900.0  2500
kitchen      1700   850.0  1000
stationery    900   450.0   600
```

`dt.to_period("M")` turns each date into its year-month (`2025-01`), a natural key for monthly totals (Section [37](#37-dates-and-times-parsing-dt-time-zones-and-periods)).

```python
store = pd.DataFrame({"store": ["A", "A", "A", "A", "B"], "sale": [10, 10, 10, 10, 100]})
means = store.groupby("store")["sale"].mean()
print("mean of means:", means.mean(), " true overall mean:", store["sale"].mean())   # don't average averages

with_gap = pd.DataFrame({"city": ["Pune", None, "Pune"], "v": [1, 2, 3]})
print(with_gap.groupby("city")["v"].sum().to_dict(), with_gap.groupby("city", dropna=False)["v"].sum().to_dict())
```

**Output:**

```text
mean of means: 55.0  true overall mean: 28.0
{'Pune': 4} {'Pune': 4, nan: 2}
```

### Practice

1. For each customer: number of orders, total revenue and the most expensive item price, sorted by revenue (highest first).
2. Which category has the highest **average** quantity per order?
3. Keep only cities with at least 3 orders (answer: a list of city names).

<details>
<summary><b>Answer</b></summary>

```python
per_customer = (orders.groupby("customer")
                .agg(orders=("order_id", "count"), revenue=("revenue", "sum"), top_price=("price", "max"))
                .sort_values("revenue", ascending=False))
print(per_customer)
print(orders.groupby("category")["qty"].mean().idxmax())
counts = orders.groupby("city").size()
print(counts[counts >= 3].index.tolist())
```

**Output:**

```text
          orders  revenue  top_price
customer                            
Asha           3     4000       2500
Ravi           2     3100       2500
Zoya           2     2500       1800
Meera          1     1800       1800
Isha           1     1000        250
Kabir          1      900        900
stationery
['Mumbai', 'Pune']
```

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [1741. Find Total Time Spent by Each Employee](https://leetcode.com/problems/find-total-time-spent-by-each-employee/) | 🟢 Easy |
| 2 | [511. Game Play Analysis I](https://leetcode.com/problems/game-play-analysis-i/) | 🟢 Easy |
| 3 | [2356. Number of Unique Subjects Taught by Each Teacher](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/) | 🟢 Easy |
| 4 | [596. Classes With at Least 5 Students](https://leetcode.com/problems/classes-with-at-least-5-students/) | 🟢 Easy |
| 5 | [1693. Daily Leads and Partners](https://leetcode.com/problems/daily-leads-and-partners/) | 🟢 Easy |
| 6 | [1484. Group Sold Products By The Date](https://leetcode.com/problems/group-sold-products-by-the-date/) | 🟢 Easy |
| 7 | [1050. Actors and Directors Who Cooperated At Least Three Times](https://leetcode.com/problems/actors-and-directors-who-cooperated-at-least-three-times/) | 🟢 Easy |
| 8 | [1211. Queries Quality and Percentage](https://leetcode.com/problems/queries-quality-and-percentage/) | 🟢 Easy |
| 9 | [619. Biggest Single Number](https://leetcode.com/problems/biggest-single-number/) | 🟢 Easy |
| 10 | [1193. Monthly Transactions I](https://leetcode.com/problems/monthly-transactions-i/) | 🟡 Medium |

**Learn more:** [pandas: group by (split-apply-combine)](https://pandas.pydata.org/docs/user_guide/groupby.html) · [Kaggle Learn: Grouping and sorting](https://www.kaggle.com/code/residentmario/grouping-and-sorting)

---

## 32. Grouping II: transform, filter, apply and Group-Wise Ranking

![agg returns one row per group; transform returns one value per original row, so group numbers sit next to each row](images/data-science/32-transform.svg)

### Theory

> **In simple words:** `agg` shrinks each group to **one row**. Often you instead want each **row** next to a number about **its group**: an order's share of its city's revenue, a student's rank within their class, a missing price filled with its category's median. That's `transform`. `filter` keeps or drops **whole groups**, and `apply` is the flexible fallback for anything else.

**Words to know:**

- **`transform`:** runs a function per group and returns a result **the same length as the original**, lined up row by row.
- **Window function (SQL):** a calculation across related rows that keeps every row: `SUM(revenue) OVER (PARTITION BY city)`. `transform` is pandas' version.
- **Partition:** SQL's word for "group" in a window function.
- **`filter` (on groups):** keep the rows of groups that pass a test (like SQL `HAVING`, but you get the original rows back).
- **`apply` (on groups):** run any function on each group's sub-table; results are glued together. Most flexible, slowest.
- **Cumulative within groups:** `cumsum`, `cumcount` (0, 1, 2… within each group), `cummax` per group.
- **`shift` within groups:** the previous (or next) row's value **inside the same group**: last order's date for the same customer.
- **Top-N per group:** the N largest rows inside every group.

**Everyday picture.** After the teacher works out each class's average (`agg`), she writes that class average **at the top of every student's answer sheet** in that class, so each student can see how they compare (`transform`). Then the head teacher says "only show me classes with more than 30 students" (`filter`).

**`agg` vs `transform`, traced** on Pune [300, 1200], Mumbai [2500, 700]:

| Row | city | revenue | `transform("sum")` | share = revenue / city total |
|---|---|---|---|---|
| 0 | Pune | 300 | 1500 | 0.20 |
| 1 | Mumbai | 2500 | 3200 | 0.78 |
| 2 | Pune | 1200 | 1500 | 0.80 |
| 3 | Mumbai | 700 | 3200 | 0.22 |

`agg("sum")` would give just 2 rows (Pune 1500, Mumbai 3200). `transform("sum")` gives 4: each row's own city total.

**The toolbox:**

| Need | Code | SQL |
|---|---|---|
| group total on every row | `g["revenue"].transform("sum")` | `SUM(...) OVER (PARTITION BY city)` |
| difference from group average | `df["x"] - g["x"].transform("mean")` | |
| fill missing with group median | `df["price"].fillna(g["price"].transform("median"))` | |
| standardise within group | `g["x"].transform(lambda s: (s - s.mean()) / s.std())` | |
| rank within group | `g["revenue"].rank(ascending=False, method="dense")` | `DENSE_RANK() OVER (PARTITION BY ... ORDER BY ...)` |
| running total within group | `g["revenue"].cumsum()` (after sorting by date) | `SUM(...) OVER (PARTITION BY ... ORDER BY date)` |
| row number within group | `g.cumcount() + 1` | `ROW_NUMBER()` |
| previous row in group | `g["date"].shift(1)` | `LAG(date) OVER (...)` |
| top N per group | `df.sort_values("revenue", ascending=False).groupby("city").head(2)` | `ROW_NUMBER() <= 2` |
| keep groups passing a test | `df.groupby("city").filter(lambda d: len(d) >= 3)` | `HAVING` (but keeping rows) |
| first / last row per group | `g.head(1)`, `g.tail(1)`, `g.nth(0)` | |
| anything else | `g.apply(func)` | |

(Here `g = df.groupby("city")`.)

**Order matters for "running" and "previous" calculations:** sort by the time column **before** `cumsum`, `shift` or `cumcount`, otherwise "previous" means "previous in file order".

**When to use `apply`:** only when no built-in or `transform` fits (fitting a small model per group, complex multi-column logic). It calls Python once per group, so it's fine for hundreds of groups and slow for millions.

**Common mistakes:**

- ❌ `groupby().agg()` then `merge` back to the rows when `transform` does it in one step.
- ❌ `shift`/`cumsum` without sorting by date first.
- ❌ `apply` for something `transform("mean")` or `rank` already does (10–100× slower).
- ❌ Top-N per group with `nlargest` on the whole table (that's top-N **overall**). ✅ Sort, then `groupby(...).head(n)`.

**Used in real software:** "% of category sales" columns in reports; z-scores within a segment for anomaly detection; customer journeys (time since previous order, order number 1, 2, 3…); leaderboards per region; ML features such as "price relative to the category average".

### Python

```python
import io
import pandas as pd

csv_text = """order_id,date,customer,city,product,category,qty,price
1,2025-01-05,Asha,Pune,Notebook,stationery,5,60
2,2025-01-06,Ravi,Mumbai,Headphones,electronics,1,2500
3,2025-02-10,Asha,Pune,Backpack,bags,1,1200
4,2025-02-11,Meera,Pune,Keyboard,electronics,1,1800
5,2025-03-02,Zoya,Mumbai,Water bottle,kitchen,2,350
6,2025-03-15,Kabir,Bengaluru,Desk lamp,electronics,1,900
7,2025-03-20,Asha,Pune,Headphones,electronics,1,2500
8,2025-04-01,Isha,Delhi,Mug,kitchen,4,250
9,2025-04-18,Ravi,Mumbai,Notebook,stationery,10,60
10,2025-05-05,Zoya,Mumbai,Keyboard,electronics,1,1800
"""
orders = pd.read_csv(io.StringIO(csv_text), parse_dates=["date"]).sort_values("date")
orders["revenue"] = orders["qty"] * orders["price"]
g = orders.groupby("city")

orders["city_total"] = g["revenue"].transform("sum")
orders["share_pct"] = (100 * orders["revenue"] / orders["city_total"]).round(1)
orders["vs_city_avg"] = (orders["revenue"] - g["revenue"].transform("mean")).round(0)
orders["rank_in_city"] = g["revenue"].rank(ascending=False, method="dense").astype(int)
print(orders[["city", "customer", "revenue", "city_total", "share_pct", "vs_city_avg", "rank_in_city"]])
```

**Output:**

```text
        city customer  revenue  city_total  share_pct  vs_city_avg  rank_in_city
0       Pune     Asha      300        5800        5.2      -1150.0             4
1     Mumbai     Ravi     2500        5600       44.6       1100.0             1
2       Pune     Asha     1200        5800       20.7       -250.0             3
3       Pune    Meera     1800        5800       31.0        350.0             2
4     Mumbai     Zoya      700        5600       12.5       -700.0             3
5  Bengaluru    Kabir      900         900      100.0          0.0             1
6       Pune     Asha     2500        5800       43.1       1050.0             1
7      Delhi     Isha     1000        1000      100.0          0.0             1
8     Mumbai     Ravi      600        5600       10.7       -800.0             4
9     Mumbai     Zoya     1800        5600       32.1        400.0             2
```

```python
c = orders.groupby("customer")
orders["order_no"] = c.cumcount() + 1                                   # 1st, 2nd, 3rd order of each customer
orders["prev_date"] = c["date"].shift(1)
orders["days_since_prev"] = (orders["date"] - orders["prev_date"]).dt.days
orders["running_spend"] = c["revenue"].cumsum()
print(orders.loc[orders["customer"].isin(["Asha", "Ravi"]),
                 ["customer", "date", "order_no", "days_since_prev", "running_spend"]])

top2 = orders.sort_values("revenue", ascending=False).groupby("city").head(2)
print(top2.sort_values(["city", "revenue"], ascending=[True, False])[["city", "product", "revenue"]])
print(orders.groupby("city").filter(lambda d: len(d) >= 3)["city"].unique().tolist())
```

**Output:**

```text
  customer       date  order_no  days_since_prev  running_spend
0     Asha 2025-01-05         1              NaN            300
1     Ravi 2025-01-06         1              NaN           2500
2     Asha 2025-02-10         2             36.0           1500
6     Asha 2025-03-20         3             38.0           4000
8     Ravi 2025-04-18         2            102.0           3100
        city     product  revenue
5  Bengaluru   Desk lamp      900
7      Delhi         Mug     1000
1     Mumbai  Headphones     2500
9     Mumbai    Keyboard     1800
6       Pune  Headphones     2500
3       Pune    Keyboard     1800
['Pune', 'Mumbai']
```

`days_since_prev` is `NaN` for each customer's first order: there's no previous one. `cumcount()` numbers rows 0, 1, 2… within each group.

```python
prices = pd.DataFrame({"category": ["pen", "pen", "pen", "bag", "bag", "bag"],
                       "price": [10, None, 14, 900, 1100, None]})
prices["filled"] = prices["price"].fillna(prices.groupby("category")["price"].transform("median"))
print(prices)

spread = orders.groupby("category").apply(lambda d: d["revenue"].max() - d["revenue"].min(), include_groups=False)
print(spread.to_dict())                                                  # apply: any custom calculation
```

**Output:**

```text
  category   price  filled
0      pen    10.0    10.0
1      pen     NaN    12.0
2      pen    14.0    14.0
3      bag   900.0   900.0
4      bag  1100.0  1100.0
5      bag     NaN  1000.0
{'bags': 0, 'electronics': 1600, 'kitchen': 300, 'stationery': 300}
```

`include_groups=False` tells `apply` not to pass the grouping column into your function (pandas 3 requires you to be explicit). Filling each missing price with its own category's median (12 for pens, 1000 for bags) is far better than one global median, which would price a pen at 455.

### Practice

1. For each order, compute its revenue as a percentage of that **customer's** total revenue.
2. Find each city's single most expensive order (one row per city).
3. Flag orders whose revenue is more than 25% above their category's average.

<details>
<summary><b>Answer</b></summary>

```python
orders["pct_of_customer"] = (100 * orders["revenue"] / orders.groupby("customer")["revenue"].transform("sum")).round(1)
print(orders[["customer", "product", "revenue", "pct_of_customer"]].head(4))
print(orders.loc[orders.groupby("city")["revenue"].idxmax(), ["city", "product", "revenue"]])
orders["big_for_category"] = orders["revenue"] > 1.25 * orders.groupby("category")["revenue"].transform("mean")
print(orders.loc[orders["big_for_category"], ["product", "category", "revenue"]])
```

**Output:**

```text
  customer     product  revenue  pct_of_customer
0     Asha    Notebook      300              7.5
1     Ravi  Headphones     2500             80.6
2     Asha    Backpack     1200             30.0
3    Meera    Keyboard     1800            100.0
        city     product  revenue
5  Bengaluru   Desk lamp      900
7      Delhi         Mug     1000
1     Mumbai  Headphones     2500
6       Pune  Headphones     2500
      product     category  revenue
1  Headphones  electronics     2500
6  Headphones  electronics     2500
8    Notebook   stationery      600
```

`idxmax` gives the row label of each group's maximum; `.loc` then fetches those rows.

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [184. Department Highest Salary](https://leetcode.com/problems/department-highest-salary/) | 🟡 Medium |
| 2 | [1070. Product Sales Analysis III](https://leetcode.com/problems/product-sales-analysis-iii/) | 🟡 Medium |
| 3 | [1174. Immediate Food Delivery II](https://leetcode.com/problems/immediate-food-delivery-ii/) | 🟡 Medium |
| 4 | [550. Game Play Analysis IV](https://leetcode.com/problems/game-play-analysis-iv/) | 🟡 Medium |
| 5 | [3421. Find Students Who Improved](https://leetcode.com/problems/find-students-who-improved/) | 🟡 Medium |
| 6 | [185. Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries/) | 🔴 Hard |

**Learn more:** [pandas: transformation](https://pandas.pydata.org/docs/user_guide/groupby.html#transformation) · [pandas: filtration](https://pandas.pydata.org/docs/user_guide/groupby.html#filtration)

---

## 33. Combining Tables I: merge and Join Types

![merge: which rows survive an inner, left and outer join](images/data-science/05-merge.svg)

### Theory

> **In simple words:** real data is spread across several tables: orders in one, customers in another, products in a third. A **merge** (a **join** in SQL) lines up rows from two tables that share a **key** (like `customer_id`) and puts their columns side by side. The **join type** decides what happens to rows that have **no partner** on the other side.

**Words to know:**

- **Merge / join:** combining two tables side by side by matching key values.
- **Key (join key):** the column(s) used to match rows: `customer_id`.
- **Left table / right table:** the first and second table in `pd.merge(left, right)`.
- **Inner join:** keep only rows whose key appears in **both** tables.
- **Left join:** keep **every** row of the left table; fill missing partners with NaN.
- **Right join:** the mirror: every row of the right table.
- **Outer (full) join:** keep every row from **both** tables.
- **Cross join:** every row of the left with every row of the right (all combinations).
- **Anti-join:** rows in the left table with **no** match in the right ("customers who never ordered").
- **Semi-join:** rows in the left table that **do** have a match, without adding the right table's columns.
- **Self-join:** joining a table to itself (employees to their managers, who are also employees).
- **Cardinality / relationship:** how many rows can match on each side: one-to-one (1:1), one-to-many (1:m), many-to-one (m:1), many-to-many (m:m).
- **Indicator:** a column (`_merge`) saying where each row came from: `left_only`, `right_only` or `both`.
- **Suffixes:** endings added to columns with the same name in both tables (`_x`, `_y` by default).

**Everyday picture.** A wedding: the **guest list** (left) and the **RSVP replies** (right), matched by name. **Inner:** only guests who replied. **Left:** every guest, with a blank where no reply came. **Outer:** everyone on either list, including people who replied but weren't on the guest list (!). **Anti-join:** guests who never replied, the ones you need to phone.

**Join types, traced** on orders (left: customer IDs 10, 11, 99) and customers (right: 10 Asha, 11 Ravi, 13 Arjun):

| how | Rows kept | Result keys |
|---|---|---|
| `inner` | matches only | 10, 11 |
| `left` | all orders | 10, 11, 99 (name NaN) |
| `right` | all customers | 10, 11, 13 (order NaN) |
| `outer` | everything | 10, 11, 99, 13 |

**The merge call:**

| Code | Does | SQL |
|---|---|---|
| `pd.merge(orders, customers, on="customer_id")` | inner join on a shared column name | `JOIN ... USING (customer_id)` |
| `orders.merge(customers, on="customer_id", how="left")` | left join | `LEFT JOIN` |
| `merge(left_on="cust", right_on="id")` | keys with different names | `ON o.cust = c.id` |
| `merge(on=["city", "date"])` | several key columns | `ON a.city = b.city AND a.date = b.date` |
| `merge(how="cross")` | all combinations | `CROSS JOIN` |
| `merge(..., indicator=True)` | adds `_merge` | |
| `merge(..., suffixes=("_order", "_cust"))` | names clashing columns | aliases |
| `left.join(right)` | merge on the **index** (shortcut) | |

**Anti-join recipe:** `m = left.merge(right, on="key", how="left", indicator=True); m[m["_merge"] == "left_only"]`. A shorter version when you need only the left rows: `left[~left["key"].isin(right["key"])]`.

**Self-join recipe:** `emp.merge(emp, left_on="manager_id", right_on="id", suffixes=("", "_mgr"))` puts each employee's manager's columns next to them.

**How many rows will I get?** With a **one-to-many** join (one customer, many orders), the result has one row per order. With **many-to-many** (duplicate keys on both sides), rows **multiply**: 3 matching rows × 4 matching rows = 12 rows. That's the most common merge bug; Section [34](#34-combining-tables-ii-concat-validation-and-merge-pitfalls) shows how to prevent it with `validate=`.

**When to use which join:** `left` is the everyday default ("keep all my orders, add customer details"); `inner` when unmatched rows are meaningless; `outer` + `indicator` to **reconcile** two sources ("which records are in one system but not the other?"); anti-join for "never did X" questions.

**Common mistakes:**

- ❌ Joining on keys with different types (`int` vs `str` IDs): nothing matches, or pandas raises an error. ✅ Make the key types equal first.
- ❌ An inner join silently dropping rows with no match. ✅ Use `how="left"` and check `isna()` on the right-hand columns, or `indicator=True`.
- ❌ Duplicate keys on the "one" side multiplying rows. ✅ `validate="many_to_one"`.
- ❌ Joining on names or emails with different capitalisation or spaces. ✅ Clean the keys first (Section [28](#28-text-data-the-str-accessor-and-regular-expressions)).

**Used in real software:** every analytics query joins fact tables (orders, events) to dimension tables (customers, products, dates); reconciliation between a payments provider and the internal ledger is an outer join with an indicator; feature tables for ML are built by left-joining features onto a list of customers.

### Python

```python
import pandas as pd

orders = pd.DataFrame({"order_id": [1, 2, 3, 4], "customer_id": [10, 11, 10, 99], "amount": [300, 2500, 1200, 450]})
customers = pd.DataFrame({"customer_id": [10, 11, 13], "name": ["Asha", "Ravi", "Arjun"], "city": ["Pune", "Mumbai", "Delhi"]})

for how in ["inner", "left", "right", "outer"]:
    m = orders.merge(customers, on="customer_id", how=how)
    print(f"--- {how}: {len(m)} rows")
    print(m)
```

**Output:**

```text
--- inner: 3 rows
   order_id  customer_id  amount  name    city
0         1           10     300  Asha    Pune
1         2           11    2500  Ravi  Mumbai
2         3           10    1200  Asha    Pune
--- left: 4 rows
   order_id  customer_id  amount  name    city
0         1           10     300  Asha    Pune
1         2           11    2500  Ravi  Mumbai
2         3           10    1200  Asha    Pune
3         4           99     450   NaN     NaN
--- right: 4 rows
   order_id  customer_id  amount   name    city
0       1.0           10   300.0   Asha    Pune
1       3.0           10  1200.0   Asha    Pune
2       2.0           11  2500.0   Ravi  Mumbai
3       NaN           13     NaN  Arjun   Delhi
--- outer: 5 rows
   order_id  customer_id  amount   name    city
0       1.0           10   300.0   Asha    Pune
1       3.0           10  1200.0   Asha    Pune
2       2.0           11  2500.0   Ravi  Mumbai
3       NaN           13     NaN  Arjun   Delhi
4       4.0           99   450.0    NaN     NaN
```

```python
m = orders.merge(customers, on="customer_id", how="outer", indicator=True)
print(m["_merge"].value_counts().to_dict())
print("orders with an unknown customer:", m.loc[m["_merge"] == "left_only", "order_id"].astype(int).tolist())
print("customers who never ordered:", customers.loc[~customers["customer_id"].isin(orders["customer_id"]), "name"].tolist())

per_customer = (orders.merge(customers, on="customer_id", how="left")
                .groupby("name", dropna=False)["amount"].sum())
print(per_customer)
```

**Output:**

```text
{'both': 3, 'left_only': 1, 'right_only': 1}
orders with an unknown customer: [4]
customers who never ordered: ['Arjun']
name
Asha    1500
Ravi    2500
NaN      450
Name: amount, dtype: int64
```

The order from customer 99 shows up under `NaN` because that customer isn't in the customers table: a data-quality problem a left join exposes and an inner join would hide.

```python
emp = pd.DataFrame({"id": [1, 2, 3, 4], "name": ["Meera", "Asha", "Ravi", "Zoya"],
                    "salary": [150, 90, 160, 70], "manager_id": [None, 1, 1, 2]})
pairs = emp.merge(emp, left_on="manager_id", right_on="id", suffixes=("", "_mgr"))      # self-join
print(pairs[["name", "salary", "name_mgr", "salary_mgr"]])
print("earn more than their manager:", pairs.loc[pairs["salary"] > pairs["salary_mgr"], "name"].tolist())

sizes = pd.DataFrame({"size": ["S", "M"]})
colours = pd.DataFrame({"colour": ["red", "blue", "green"]})
print(len(sizes.merge(colours, how="cross")), "combinations")                          # cross join: 2 × 3
```

**Output:**

```text
   name  salary name_mgr  salary_mgr
0  Asha      90    Meera         150
1  Ravi     160    Meera         150
2  Zoya      70     Asha          90
earn more than their manager: ['Ravi']
6 combinations
```

### Practice

1. Add each order's customer **city** to `orders`, keeping every order. How many orders have no city?
2. Which customers have **no** orders? Solve it once with `merge(..., indicator=True)` and once with `isin`.
3. Make every (student, subject) combination for students `["A", "B"]` and subjects `["Maths", "Art", "PE"]`.

<details>
<summary><b>Answer</b></summary>

```python
with_city = orders.merge(customers[["customer_id", "city"]], on="customer_id", how="left")
print(with_city, with_city["city"].isna().sum(), sep="\n")

ind = customers.merge(orders, on="customer_id", how="left", indicator=True)
print(ind.loc[ind["_merge"] == "left_only", "name"].tolist(),
      customers.loc[~customers["customer_id"].isin(orders["customer_id"]), "name"].tolist())

print(pd.DataFrame({"student": ["A", "B"]}).merge(pd.DataFrame({"subject": ["Maths", "Art", "PE"]}), how="cross"))
```

**Output:**

```text
   order_id  customer_id  amount    city
0         1           10     300    Pune
1         2           11    2500  Mumbai
2         3           10    1200    Pune
3         4           99     450     NaN
1
['Arjun'] ['Arjun']
  student subject
0       A   Maths
1       A     Art
2       A      PE
3       B   Maths
4       B     Art
5       B      PE
```

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [175. Combine Two Tables](https://leetcode.com/problems/combine-two-tables/) | 🟢 Easy |
| 2 | [1378. Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/) | 🟢 Easy |
| 3 | [1068. Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/) | 🟢 Easy |
| 4 | [181. Employees Earning More Than Their Managers](https://leetcode.com/problems/employees-earning-more-than-their-managers/) | 🟢 Easy |
| 5 | [1581. Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/) | 🟢 Easy |
| 6 | [607. Sales Person](https://leetcode.com/problems/sales-person/) | 🟢 Easy |
| 7 | [1280. Students and Examinations](https://leetcode.com/problems/students-and-examinations/) | 🟢 Easy |
| 8 | [1251. Average Selling Price](https://leetcode.com/problems/average-selling-price/) | 🟢 Easy |
| 9 | [1633. Percentage of Users Attended a Contest](https://leetcode.com/problems/percentage-of-users-attended-a-contest/) | 🟢 Easy |
| 10 | [570. Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/) | 🟡 Medium |
| 11 | [1934. Confirmation Rate](https://leetcode.com/problems/confirmation-rate/) | 🟡 Medium |
| 12 | [1158. Market Analysis I](https://leetcode.com/problems/market-analysis-i/) | 🟡 Medium |
| 13 | [1045. Customers Who Bought All Products](https://leetcode.com/problems/customers-who-bought-all-products/) | 🟡 Medium |
| 14 | [262. Trips and Users](https://leetcode.com/problems/trips-and-users/) | 🔴 Hard |

**Learn more:** [pandas: merge, join, concatenate and compare](https://pandas.pydata.org/docs/user_guide/merging.html) · [Visual explanation of SQL joins](https://joins.spathon.com/)

---

## 34. Combining Tables II: concat, Validation and Merge Pitfalls

![concat stacks tables: axis=0 adds rows (same columns), axis=1 adds columns (same index)](images/data-science/34-concat.svg)

### Theory

> **In simple words:** `merge` puts tables **side by side** by matching keys. `concat` **stacks** tables: January's file on top of February's (more rows), or extra columns glued alongside (more columns). This section also covers the merge traps that silently corrupt results, and the one-word guard against the worst of them: `validate=`.

**Words to know:**

- **Concatenate:** join end to end. `pd.concat([a, b])` stacks rows; `axis=1` places them side by side by index.
- **Union (SQL `UNION ALL`):** stacking rows from tables with the same columns; `UNION` also removes duplicates.
- **`ignore_index=True`:** renumber rows 0, 1, 2… after stacking (otherwise index labels repeat).
- **`keys=`:** label which source each stacked piece came from.
- **Row explosion (fan-out):** a merge producing far more rows than expected because keys repeat on both sides.
- **`validate=`:** tells `merge` the relationship you expect (`"one_to_one"`, `"one_to_many"`, `"many_to_one"`, `"many_to_many"`); it raises an error if the data breaks it.
- **As-of merge (`merge_asof`):** match each row to the **most recent** row on or before it in time (the exchange rate in effect on the order date).
- **Reconciliation:** comparing two sources of the same facts to find differences.

**Everyday picture.** `concat` is stapling this month's attendance sheet under last month's: same columns, more rows. A bad merge is like matching wedding guests to tables using **first names only**: three Rahuls and two tables with a "Rahul" seat gives six seatings, and the caterer orders six meals.

**Row explosion, traced:** prices has **two** rows for `pen` (an old price and a new one), and orders has **three** `pen` orders. Merging on `product` gives 3 × 2 = **6** pen rows instead of 3, and total revenue is double-counted. `validate="many_to_one"` catches it immediately: "right keys are not unique".

**`concat` options:**

| Code | Does |
|---|---|
| `pd.concat([jan, feb], ignore_index=True)` | stack rows, renumber |
| `pd.concat([jan, feb], keys=["jan", "feb"])` | stack, labelling each source in the index |
| `pd.concat(frames, join="inner")` | keep only columns present in **all** frames (default `"outer"` keeps all, filling NaN) |
| `pd.concat([a, b], axis=1)` | side by side, aligned on the index |
| `pd.concat(list_of_frames)` | the fast way to combine many pieces: collect in a list, concat **once** |

**`merge_asof`, the time-aware join:** for each order, find the latest exchange rate published at or before the order time. Both tables must be **sorted** by the time key. Options: `by="currency"` (match within groups), `direction="backward"` (default) / `"forward"` / `"nearest"`, `tolerance=pd.Timedelta("1D")`.

**A merge checklist (do this every time):**

1. **Key types match:** `left["id"].dtype == right["id"].dtype`.
2. **Keys are clean:** stripped, same case, no stray NaN.
3. **Relationship is what you think:** `validate="many_to_one"` (or `"one_to_one"`).
4. **Row count is right:** compare `len(result)` with `len(left)` for a left join on a unique right key; they must be equal.
5. **Unmatched rows are understood:** `indicator=True`, then look at `left_only` / `right_only`.
6. **Totals survive:** a sum before the merge equals the same sum after (when it should).

**When to use which:** `concat` for the same kind of table split across files or periods; `merge` for different tables linked by keys; `merge_asof` for "the latest value as of this time".

**Common mistakes:**

- ❌ `pd.concat` inside a loop (`df = pd.concat([df, new])` each time): quadratic slowdown. ✅ Append to a list, concat once.
- ❌ Stacking frames whose columns are named slightly differently (`Qty` vs `qty`): you get two half-empty columns. ✅ Standardise names first.
- ❌ Merging with duplicate keys on the side you believe is unique. ✅ `validate=`.
- ❌ Forgetting `ignore_index=True`, then `.loc[0]` returns several rows.

**Used in real software:** monthly files combined into one table; logs from several servers stacked; currency conversion and "price at time of order" with `merge_asof`; finance reconciliation and data migrations checked with outer joins and indicators.

### Python

```python
import pandas as pd

jan = pd.DataFrame({"order_id": [1, 2], "product": ["pen", "mug"], "qty": [3, 1]})
feb = pd.DataFrame({"order_id": [3, 4], "product": ["pen", "lamp"], "qty": [2, 1], "coupon": ["NEW10", None]})
both = pd.concat([jan, feb], ignore_index=True)
print(both)
print(pd.concat([jan, feb], keys=["jan", "feb"]).loc["feb", ["order_id", "product"]])
print(pd.concat([jan, feb], join="inner").columns.tolist())
```

**Output:**

```text
   order_id product  qty coupon
0         1     pen    3    NaN
1         2     mug    1    NaN
2         3     pen    2  NEW10
3         4    lamp    1    NaN
   order_id product
0         3     pen
1         4    lamp
['order_id', 'product', 'qty']
```

```python
orders = pd.DataFrame({"order_id": [1, 2, 3], "product": ["pen", "pen", "pen"], "qty": [3, 2, 5]})
prices = pd.DataFrame({"product": ["pen", "pen"], "price": [10, 12], "valid_from": ["2025-01-01", "2025-03-01"]})

bad = orders.merge(prices, on="product")
print(len(orders), "orders became", len(bad), "rows; revenue", (bad["qty"] * bad["price"]).sum())
try:
    orders.merge(prices, on="product", validate="many_to_one")
except pd.errors.MergeError as e:
    print("MergeError:", str(e).splitlines()[0])
```

**Output:**

```text
3 orders became 6 rows; revenue 220
MergeError: Merge keys are not unique in right dataset; not a many-to-one merge
```

```python
orders = pd.DataFrame({"time": pd.to_datetime(["2025-01-10", "2025-02-15", "2025-03-05"]),
                       "currency": ["USD", "USD", "EUR"], "amount": [100, 100, 100]})
rates = pd.DataFrame({"time": pd.to_datetime(["2025-01-01", "2025-02-01", "2025-03-01", "2025-01-01"]),
                      "currency": ["USD", "USD", "USD", "EUR"], "inr": [83.0, 84.5, 86.0, 90.0]})
fx = pd.merge_asof(orders.sort_values("time"), rates.sort_values("time"), on="time", by="currency")
fx["amount_inr"] = fx["amount"] * fx["inr"]
print(fx)
```

**Output:**

```text
        time currency  amount   inr  amount_inr
0 2025-01-10      USD     100  83.0      8300.0
1 2025-02-15      USD     100  84.5      8450.0
2 2025-03-05      EUR     100  90.0      9000.0
```

The 15 February USD order used the 1 February rate (84.5), the latest one known at the time; the March EUR order used the EUR rate from 1 January, because that's the newest EUR rate available.

### Practice

1. You receive 12 monthly DataFrames in a list called `months`. Write the one line that combines them with a fresh index.
2. A left join of 1,000 orders to a customers table returns 1,037 rows. What happened, and how do you find the culprits?

<details>
<summary><b>Answer</b></summary>

1. `all_orders = pd.concat(months, ignore_index=True)`.
2. Some customer IDs appear more than once in the customers table, so those orders matched several customer rows (fan-out). Find them with `customers[customers["customer_id"].duplicated(keep=False)]`, fix or deduplicate, and add `validate="many_to_one"` to the merge so it can't happen silently again.

```python
customers = pd.DataFrame({"customer_id": [1, 2, 2, 3], "name": ["A", "B", "B (old)", "C"]})
print(customers[customers["customer_id"].duplicated(keep=False)])
```

**Output:**

```text
   customer_id     name
1            2        B
2            2  B (old)
```

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [2888. Reshape Data: Concatenate](https://leetcode.com/problems/reshape-data-concatenate/) | 🟢 Easy |
| 2 | [1084. Sales Analysis III](https://leetcode.com/problems/sales-analysis-iii/) | 🟢 Easy |
| 3 | [1978. Employees Whose Manager Left the Company](https://leetcode.com/problems/employees-whose-manager-left-the-company/) | 🟢 Easy |
| 4 | [602. Friend Requests II: Who Has the Most Friends](https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends/) | 🟡 Medium |
| 5 | [1164. Product Price at a Given Date](https://leetcode.com/problems/product-price-at-a-given-date/) | 🟡 Medium |

**Learn more:** [pandas: concat](https://pandas.pydata.org/docs/reference/api/pandas.concat.html) · [pandas: merge_asof](https://pandas.pydata.org/docs/reference/api/pandas.merge_asof.html)

---

## 35. Reshaping: pivot_table, melt, crosstab and explode

![pivot_table turns long data wide; melt turns wide data long](images/data-science/06-reshape.svg)

### Theory

> **In simple words:** the same numbers can be laid out **long** (one row per observation: city, month, revenue) or **wide** (one row per city, one column per month). Analysis, groupby and charts prefer long; reports and spreadsheets prefer wide. `pivot_table` goes long → wide, `melt` goes wide → long, `crosstab` counts combinations, and `explode` turns list-valued cells into rows.

**Words to know:**

- **Long (tidy) format:** one row per observation (Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data)).
- **Wide format:** one row per entity, with repeated measurements spread across columns.
- **Pivot:** rotate values from a column into column **headers**. **Pivot table:** a pivot that also **aggregates** duplicates (sum, mean…), like Excel's pivot tables.
- **Melt (unpivot):** turn column headers back into values in a column.
- **`index` / `columns` / `values`:** in `pivot_table`: what becomes rows, what becomes columns, and which numbers fill the cells.
- **`aggfunc`:** how to combine several values landing in the same cell (default `"mean"`).
- **Margins:** total rows and columns (`margins=True` adds "All").
- **Crosstab (contingency table):** a table of **counts** of each combination of two categorical columns.
- **Explode:** give each item of a list-valued cell its own row.
- **Retention:** the share of users who come back (are still active) some time after they started; a **cohort retention table** shows it per signup cohort and period.

**Everyday picture.** A long table is a **receipt roll**: every sale on its own line. A wide table is the **summary card on the manager's desk**: cities down the side, months across the top. Same information; pivoting prints the summary card from the roll, melting tears it back into lines.

**`pivot_table`, traced:** long rows (Pune, Jan, 300), (Pune, Jan, 200), (Pune, Feb, 3000), (Mumbai, Jan, 2500) with `index="city", columns="month", values="revenue", aggfunc="sum"`:

| city | Feb | Jan |
|---|---|---|
| Mumbai | NaN | 2500 |
| Pune | 3000 | 500 |

The two Pune-January rows landed in one cell and were **summed**; Mumbai had no February row, so that cell is NaN (`fill_value=0` makes it 0).

**`pivot` vs `pivot_table`:** `pivot` only reshapes and **fails** if two rows land in the same cell ("Index contains duplicate entries"). `pivot_table` aggregates them. Use `pivot_table` unless you know each cell has exactly one value.

**The tools:**

| Code | Does |
|---|---|
| `df.pivot_table(index="city", columns="month", values="revenue", aggfunc="sum", fill_value=0, margins=True)` | long → wide with totals |
| `df.pivot(index="id", columns="metric", values="value")` | reshape only (no duplicates allowed) |
| `wide.melt(id_vars="city", var_name="month", value_name="revenue")` | wide → long |
| `pd.crosstab(df["city"], df["category"])` | counts of combinations |
| `pd.crosstab(a, b, normalize="index")` | row percentages (each row sums to 1) |
| `df.explode("tags")` | one row per list item |
| `df.groupby(["city", "month"])["revenue"].sum().unstack()` | the groupby route to wide (Section [36](#36-multiindex-stack-and-unstack)) |

**When to use:** `pivot_table` for report tables and heatmaps; `melt` to tidy spreadsheet-style data before analysis or Seaborn charts (which want long data); `crosstab` to compare two categories (and for chi-square tests, Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests)); `explode` for tags, list-valued API fields, and "split this comma-separated cell".

**Common mistakes:**

- ❌ `pivot` on data with duplicates → `ValueError`. ✅ `pivot_table` with an explicit `aggfunc`.
- ❌ Forgetting the default `aggfunc="mean"` and getting averages when you wanted totals. ✅ Always pass `aggfunc`.
- ❌ Months as column headers sorted alphabetically (Apr, Feb, Jan…). ✅ Use month numbers or ordered categories, or reorder columns.
- ❌ Keeping data wide for analysis and writing one line of code per month column. ✅ Melt it first.

**Used in real software:** Excel-style pivot reports, cohort retention tables (signup month × months since signup), heatmaps of activity by weekday × hour, survey analysis (crosstabs), turning "tags" fields into rows for counting.

### Python

```python
import io
import pandas as pd

csv_text = """order_id,date,customer,city,product,category,qty,price
1,2025-01-05,Asha,Pune,Notebook,stationery,5,60
2,2025-01-06,Ravi,Mumbai,Headphones,electronics,1,2500
3,2025-02-10,Asha,Pune,Backpack,bags,1,1200
4,2025-02-11,Meera,Pune,Keyboard,electronics,1,1800
5,2025-03-02,Zoya,Mumbai,Water bottle,kitchen,2,350
6,2025-03-15,Kabir,Bengaluru,Desk lamp,electronics,1,900
7,2025-03-20,Asha,Pune,Headphones,electronics,1,2500
8,2025-04-01,Isha,Delhi,Mug,kitchen,4,250
9,2025-04-18,Ravi,Mumbai,Notebook,stationery,10,60
10,2025-05-05,Zoya,Mumbai,Keyboard,electronics,1,1800
"""
orders = pd.read_csv(io.StringIO(csv_text), parse_dates=["date"])
orders["revenue"] = orders["qty"] * orders["price"]
orders["month"] = orders["date"].dt.month

wide = orders.pivot_table(index="city", columns="month", values="revenue", aggfunc="sum", fill_value=0, margins=True)
print(wide)
```

**Output:**

```text
month         1     2     3     4     5    All
city                                          
Bengaluru     0     0   900     0     0    900
Delhi         0     0     0  1000     0   1000
Mumbai     2500     0   700   600  1800   5600
Pune        300  3000  2500     0     0   5800
All        2800  3000  4100  1600  1800  13300
```

```python
report = pd.DataFrame({"city": ["Pune", "Mumbai"], "jan": [300, 2500], "feb": [3000, 0], "mar": [2500, 700]})
long = report.melt(id_vars="city", var_name="month", value_name="revenue")
print(long)
print(long.groupby("month", sort=False)["revenue"].sum().to_dict())     # easy once it's long

print(pd.crosstab(orders["city"], orders["category"]))
print(pd.crosstab(orders["city"], orders["category"], normalize="index").round(2))
```

**Output:**

```text
     city month  revenue
0    Pune   jan      300
1  Mumbai   jan     2500
2    Pune   feb     3000
3  Mumbai   feb        0
4    Pune   mar     2500
5  Mumbai   mar      700
{'jan': 2800, 'feb': 3000, 'mar': 3200}
category   bags  electronics  kitchen  stationery
city                                             
Bengaluru     0            1        0           0
Delhi         0            0        1           0
Mumbai        0            2        1           1
Pune          1            2        0           1
category   bags  electronics  kitchen  stationery
city                                             
Bengaluru  0.00          1.0     0.00        0.00
Delhi      0.00          0.0     1.00        0.00
Mumbai     0.00          0.5     0.25        0.25
Pune       0.25          0.5     0.00        0.25
```

```python
posts = pd.DataFrame({"post": [1, 2, 3], "tags": ["python,pandas", "sql", "python,ml,pandas"]})
tags = posts.assign(tag=posts["tags"].str.split(",")).explode("tag")
print(tags[["post", "tag"]])
print(tags["tag"].value_counts().to_dict())

metrics = pd.DataFrame({"id": [1, 1, 2, 2], "metric": ["height", "weight", "height", "weight"], "value": [170, 65, 182, 80]})
print(metrics.pivot(index="id", columns="metric", values="value"))
```

**Output:**

```text
   post     tag
0     1  python
0     1  pandas
1     2     sql
2     3  python
2     3      ml
2     3  pandas
{'python': 2, 'pandas': 2, 'sql': 1, 'ml': 1}
metric  height  weight
id                    
1          170      65
2          182      80
```

### Practice

1. Make a table with categories as rows, months as columns and **total quantity** in the cells, missing cells as 0.
2. Melt `pd.DataFrame({"student": ["A", "B"], "maths": [80, 70], "art": [90, 60]})` into `student, subject, mark`, then find each subject's average.

<details>
<summary><b>Answer</b></summary>

```python
print(orders.pivot_table(index="category", columns="month", values="qty", aggfunc="sum", fill_value=0))
marks = pd.DataFrame({"student": ["A", "B"], "maths": [80, 70], "art": [90, 60]}).melt(
    id_vars="student", var_name="subject", value_name="mark")
print(marks, marks.groupby("subject")["mark"].mean().to_dict(), sep="\n")
```

**Output:**

```text
month        1  2  3   4  5
category                   
bags         0  1  0   0  0
electronics  1  1  2   0  1
kitchen      0  0  2   4  0
stationery   5  0  0  10  0
  student subject  mark
0       A   maths    80
1       B   maths    70
2       A     art    90
3       B     art    60
{'art': 75.0, 'maths': 75.0}
```

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [2889. Reshape Data: Pivot](https://leetcode.com/problems/reshape-data-pivot/) | 🟢 Easy |
| 2 | [2890. Reshape Data: Melt](https://leetcode.com/problems/reshape-data-melt/) | 🟢 Easy |
| 3 | [1179. Reformat Department Table](https://leetcode.com/problems/reformat-department-table/) | 🟢 Easy |
| 4 | [1795. Rearrange Products Table](https://leetcode.com/problems/rearrange-products-table/) | 🟢 Easy |
| 5 | [1661. Average Time of Process per Machine](https://leetcode.com/problems/average-time-of-process-per-machine/) | 🟢 Easy |

**Learn more:** [pandas: reshaping and pivot tables](https://pandas.pydata.org/docs/user_guide/reshaping.html)

---

## 36. MultiIndex, stack and unstack

![A MultiIndex has several levels of row labels; unstack moves an inner level into the columns, stack moves it back](images/data-science/36-multiindex.svg)

### Theory

> **In simple words:** group by two keys and pandas puts **both** keys in the row labels: a **MultiIndex** (city, then category inside each city). `unstack` moves one level of those labels up into the columns (making a wide table); `stack` moves it back down. Knowing this explains many "why does my result look like that?" moments.

**Words to know:**

- **MultiIndex (hierarchical index):** an index with several **levels**, like (city, category).
- **Level:** one layer of a MultiIndex, referred to by position (0, 1) or name (`"city"`).
- **Outer / inner level:** the first / later levels. Rows are grouped by the outer level.
- **`unstack(level)`:** pivot an index level into the column headers (long → wide).
- **`stack()`:** pivot the column headers into the innermost index level (wide → long).
- **Cross-section (`xs`):** select all rows with a given value on one level.
- **Flatten:** turn a MultiIndex into ordinary columns (`reset_index()`), or join multi-level column names into one string.

**Everyday picture.** A filing cabinet: the **drawer** is the city (outer level) and the **folders inside** are categories (inner level). `unstack` pulls the folders out and lays them across the desk as columns; `stack` files them back into the drawer.

**What a MultiIndex looks like:**

```text
city    category
Mumbai  electronics    4300
        kitchen         700
        stationery      600
Pune    bags           1200
        electronics    4300
```

The blank under `Mumbai` means "still Mumbai": the outer label is printed once per block.

**Working with it:**

| Code | Does |
|---|---|
| `s.loc["Pune"]` | everything for Pune (drops the outer level) |
| `s.loc[("Pune", "electronics")]` | one value (a tuple of labels) |
| `s.xs("electronics", level="category")` | electronics in every city |
| `s.unstack()` / `s.unstack("city")` | move the inner (or named) level into the columns |
| `s.unstack(fill_value=0)` | fill missing combinations |
| `df.stack()` | columns → innermost index level |
| `s.reset_index()` | all levels back into ordinary columns (often the simplest fix) |
| `s.swaplevel().sort_index()` | category first, then city |
| `s.groupby(level="city").sum()` | aggregate over one level |

**Multi-level columns** appear after `agg` with several functions (`("revenue", "sum")`, `("revenue", "mean")`). Flatten them with `df.columns = ["_".join(c) for c in df.columns]`, or avoid them with named aggregation (Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine)).

**When to keep a MultiIndex:** quick exploration, `unstack`ing for a report, time series per entity (store, date). **When to flatten:** before saving to CSV/Parquet, merging, or handing the data to other tools: most of them expect plain columns.

**Common mistakes:**

- ❌ Fighting a MultiIndex with complicated `.loc` calls when `reset_index()` would make life easy.
- ❌ Slicing a MultiIndex that isn't sorted (`PerformanceWarning`, or errors). ✅ `sort_index()` first.
- ❌ Saving multi-level column names to CSV and getting two header rows. ✅ Flatten first.

**Used in real software:** panel data (many entities × many dates) in finance and economics; results of multi-key groupby in every analysis; `unstack` to produce heatmap-ready matrices.

### Python

```python
import io
import pandas as pd

csv_text = """order_id,date,customer,city,product,category,qty,price
1,2025-01-05,Asha,Pune,Notebook,stationery,5,60
2,2025-01-06,Ravi,Mumbai,Headphones,electronics,1,2500
3,2025-02-10,Asha,Pune,Backpack,bags,1,1200
4,2025-02-11,Meera,Pune,Keyboard,electronics,1,1800
5,2025-03-02,Zoya,Mumbai,Water bottle,kitchen,2,350
7,2025-03-20,Asha,Pune,Headphones,electronics,1,2500
9,2025-04-18,Ravi,Mumbai,Notebook,stationery,10,60
10,2025-05-05,Zoya,Mumbai,Keyboard,electronics,1,1800
"""
orders = pd.read_csv(io.StringIO(csv_text))
orders["revenue"] = orders["qty"] * orders["price"]

s = orders.groupby(["city", "category"])["revenue"].sum()
print(s)
print(s.index.nlevels, s.index.names, s.loc["Pune"].to_dict(), s.loc[("Mumbai", "kitchen")])
print(s.xs("electronics", level="category").to_dict())
```

**Output:**

```text
city    category   
Mumbai  electronics    4300
        kitchen         700
        stationery      600
Pune    bags           1200
        electronics    4300
        stationery      300
Name: revenue, dtype: int64
2 ['city', 'category'] {'bags': 1200, 'electronics': 4300, 'stationery': 300} 700
{'Mumbai': 4300, 'Pune': 4300}
```

```python
wide = s.unstack(fill_value=0)                    # inner level (category) → columns
print(wide)
print(wide.stack().head(3))                       # and back
print(s.unstack("city", fill_value=0))            # choose which level moves
print(s.groupby(level="city").sum().to_dict())

stats = orders.groupby("city").agg({"revenue": ["sum", "mean"], "qty": ["sum"]})
print(stats.columns.tolist())
stats.columns = ["_".join(col) for col in stats.columns]
print(stats.reset_index())
```

**Output:**

```text
category  bags  electronics  kitchen  stationery
city                                            
Mumbai       0         4300      700         600
Pune      1200         4300        0         300
city    category   
Mumbai  bags              0
        electronics    4300
        kitchen         700
dtype: int64
city         Mumbai  Pune
category                 
bags              0  1200
electronics    4300  4300
kitchen         700     0
stationery      600   300
{'Mumbai': 5600, 'Pune': 5800}
[('revenue', 'sum'), ('revenue', 'mean'), ('qty', 'sum')]
     city  revenue_sum  revenue_mean  qty_sum
0  Mumbai         5600        1400.0       14
1    Pune         5800        1450.0        8
```

### Practice

1. From `s`, get the revenue of every category in Mumbai as a dict, then the total revenue per category across all cities.
2. Group `orders` by `customer` and `category`, sum `qty`, and `unstack` so each customer is a row.

<details>
<summary><b>Answer</b></summary>

```python
print(s.loc["Mumbai"].to_dict(), s.groupby(level="category").sum().to_dict())
print(orders.groupby(["customer", "category"])["qty"].sum().unstack(fill_value=0))
```

**Output:**

```text
{'electronics': 4300, 'kitchen': 700, 'stationery': 600} {'bags': 1200, 'electronics': 8600, 'kitchen': 700, 'stationery': 900}
category  bags  electronics  kitchen  stationery
customer                                        
Asha         1            1        0           5
Meera        0            1        0           0
Ravi         0            1        0          10
Zoya         0            1        2           0
```

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [1179. Reformat Department Table](https://leetcode.com/problems/reformat-department-table/) (try it with `unstack`) | 🟢 Easy |

**Learn more:** [pandas: MultiIndex / advanced indexing](https://pandas.pydata.org/docs/user_guide/advanced.html)

---

## 37. Dates and Times: Parsing, .dt, Time Zones and Periods

![A timestamp is a point in time; a period is a whole span (a day, a month); a timedelta is a duration](images/data-science/37-time-types.svg)

### Theory

> **In simple words:** dates are deceptively hard: formats differ by country, months have different lengths, clocks change, and the same moment is a different local time in Mumbai and London. pandas has proper types for **points in time** (timestamps), **durations** (timedeltas) and **spans** (periods), plus the `.dt` accessor to pull out parts like month and weekday.

**Words to know:**

- **Timestamp (`datetime64`):** a specific moment: 2025-03-14 09:30:00.
- **Timedelta:** a duration: 3 days, 2 hours. `date2 - date1` gives a timedelta.
- **Period:** a whole span with a frequency: the month 2025-03, the day 2025-03-14, the quarter 2025Q1.
- **Frequency / offset alias:** a code for a time step: `"D"` day, `"h"` hour, `"min"` minute, `"W"` week, `"MS"` month start, `"ME"` month end, `"QE"` quarter end, `"YE"` year end, `"B"` business day.
- **Time zone:** a region's rule for local time: `Asia/Kolkata` (UTC+5:30), `Europe/London` (UTC+0 or +1 in summer).
- **UTC (Coordinated Universal Time):** the world's reference time, with no daylight saving. Store times in UTC; convert for display.
- **Naive vs aware:** a **naive** timestamp has no time zone (ambiguous); an **aware** one knows its zone.
- **Daylight saving time (DST):** moving clocks forward in spring and back in autumn in some countries; creates missing and repeated local hours.
- **ISO 8601:** the international date format `2025-03-14T09:30:00+05:30`. Unambiguous; use it for storing and exchanging dates.
- **Business day:** Monday–Friday (holidays can be added).

**Everyday picture.** A timestamp is a **photo with the exact time printed on it**. A timedelta is a **stopwatch reading**. A period is a **page of a calendar**: "March 2025" covers the whole month. Time zones are the **clocks on a hotel lobby wall**: one moment, different local readings.

**What you can get from a datetime column (`s.dt`):**

| Code | Gives (for 2025-03-14 09:30, a Friday) |
|---|---|
| `.dt.year`, `.dt.month`, `.dt.day` | 2025, 3, 14 |
| `.dt.hour`, `.dt.minute` | 9, 30 |
| `.dt.dayofweek` | 4 (Monday = 0) |
| `.dt.day_name()`, `.dt.month_name()` | "Friday", "March" |
| `.dt.quarter`, `.dt.isocalendar().week` | 1, 11 |
| `.dt.date`, `.dt.normalize()` | the date part; midnight of that day |
| `.dt.to_period("M")` | Period 2025-03 |
| `.dt.floor("h")`, `.dt.ceil("D")` | round down/up to the hour/day |
| `.dt.is_month_end`, `.dt.days_in_month` | False, 31 |
| `.dt.strftime("%d %b %Y")` | "14 Mar 2025" (text, for display only) |

**Date arithmetic:**

| Code | Result |
|---|---|
| `ts + pd.Timedelta(days=7)` | one week later |
| `(end - start).dt.days` | whole days between |
| `(end - start).dt.total_seconds() / 3600` | hours between |
| `ts + pd.DateOffset(months=1)` | same day next month (handles month lengths) |
| `ts + pd.offsets.MonthEnd(0)` | the end of this month |
| `ts + pd.offsets.BDay(3)` | three business days later |
| `pd.date_range("2025-01-01", periods=5, freq="D")` | a sequence of dates |
| `pd.bdate_range(start, end)` | business days only |

**Time zones, step by step:**

1. Parse the raw times.
2. If they're **naive**, declare what zone they were recorded in: `s.dt.tz_localize("Asia/Kolkata")`.
3. Convert to UTC for storage and comparison: `s.dt.tz_convert("UTC")`.
4. Convert to the viewer's zone for display: `s.dt.tz_convert("Europe/London")`.
5. Strings with an offset (`"…+05:30"`) parse as aware directly; `pd.to_datetime(..., utc=True)` converts everything to UTC in one go.

**Timestamps vs periods:** use timestamps for events ("the order was placed at 09:30"); use periods for buckets ("revenue in March"). `to_period("M")` is the cleanest monthly grouping key, and `pd.Period("2025-03").start_time` / `.end_time` give its edges.

**When dates go wrong:** ambiguous formats (`03/04/2025`), mixing naive and aware times (pandas refuses to compare them), daylight-saving gaps, and "end of month" logic (`+ 30 days` from 31 January is 2 March).

**Common mistakes:**

- ❌ Keeping dates as strings: `"2025-10-01" < "2025-9-30"` is `True` as text (`"1"` < `"9"`). ✅ `pd.to_datetime` right after loading.
- ❌ Storing local times without a zone. ✅ Store UTC (aware), display local.
- ❌ `+ pd.Timedelta(days=30)` for "next month". ✅ `pd.DateOffset(months=1)`.
- ❌ Filtering "everything on 31 March" with `== "2025-03-31"` on timestamps that have times (only midnight matches). ✅ `s.dt.normalize() == "2025-03-31"` or a range.
- ❌ Using `strftime` output for sorting or maths (it's text).

**Used in real software:** every event log and analytics table (event time in UTC); billing and subscriptions (month-end logic, `DateOffset`); delivery promises (business days); global apps showing each user their local time; finance (trading days, quarter ends).

### Python

```python
import pandas as pd

ts = pd.Series(pd.to_datetime(["2025-03-14 09:30", "2025-01-31 23:15", "2025-12-25 18:00"]))
parts = pd.DataFrame({"ts": ts, "year": ts.dt.year, "month": ts.dt.month, "weekday": ts.dt.day_name(),
                      "dow": ts.dt.dayofweek, "quarter": ts.dt.quarter, "period": ts.dt.to_period("M"),
                      "hour_floor": ts.dt.floor("h"), "label": ts.dt.strftime("%d %b %Y")})
print(parts)
```

**Output:**

```text
                   ts  year  month   weekday  dow  quarter   period          hour_floor        label
0 2025-03-14 09:30:00  2025      3    Friday    4        1  2025-03 2025-03-14 09:00:00  14 Mar 2025
1 2025-01-31 23:15:00  2025      1    Friday    4        1  2025-01 2025-01-31 23:00:00  31 Jan 2025
2 2025-12-25 18:00:00  2025     12  Thursday    3        4  2025-12 2025-12-25 18:00:00  25 Dec 2025
```

```python
start = pd.Timestamp("2025-01-31")
print(start + pd.Timedelta(days=30), start + pd.DateOffset(months=1), start + pd.offsets.MonthEnd(1))
print(pd.Timestamp("2025-03-14") + pd.offsets.BDay(3))                  # Friday + 3 business days
print(pd.date_range("2025-01-01", periods=4, freq="MS").strftime("%Y-%m-%d").tolist())

placed = pd.Series(pd.to_datetime(["2025-03-01 10:00", "2025-03-03 16:30"]))
delivered = pd.Series(pd.to_datetime(["2025-03-04 09:00", "2025-03-03 20:00"]))
took = delivered - placed
print(took.tolist(), (took.dt.total_seconds() / 3600).round(1).tolist())
print("2025-10-01" < "2025-9-30", pd.Timestamp("2025-10-01") < pd.Timestamp("2025-09-30"))
```

**Output:**

```text
2025-03-02 00:00:00 2025-02-28 00:00:00 2025-02-28 00:00:00
2025-03-19 00:00:00
['2025-01-01', '2025-02-01', '2025-03-01', '2025-04-01']
[Timedelta('2 days 23:00:00'), Timedelta('0 days 03:30:00')] [71.0, 3.5]
True False
```

`+ 30 days` from 31 January lands on 2 March; `DateOffset(months=1)` gives 28 February, and `MonthEnd(1)` moves to the end of the month.

```python
local = pd.Series(pd.to_datetime(["2025-03-14 09:30", "2025-03-14 23:45"])).dt.tz_localize("Asia/Kolkata")
print(pd.DataFrame({"india": local, "utc": local.dt.tz_convert("UTC"), "new_york": local.dt.tz_convert("America/New_York")}))

mixed = pd.to_datetime(["2025-03-14T09:30:00+05:30", "2025-03-14T04:00:00Z"], utc=True)
print(mixed, mixed[0] == mixed[1])                      # the same moment written two ways

march = pd.Period("2025-03", freq="M")
print(march.start_time, march.end_time.floor("s"), march.days_in_month)
```

**Output:**

```text
                      india                       utc                  new_york
0 2025-03-14 09:30:00+05:30 2025-03-14 04:00:00+00:00 2025-03-14 00:00:00-04:00
1 2025-03-14 23:45:00+05:30 2025-03-14 18:15:00+00:00 2025-03-14 14:15:00-04:00
DatetimeIndex(['2025-03-14 04:00:00+00:00', '2025-03-14 04:00:00+00:00'], dtype='datetime64[us, UTC]', freq=None) True
2025-03-01 00:00:00 2025-03-31 23:59:59 31
```

The two strings in `mixed` describe **the same instant** (09:30 in India is 04:00 UTC), and once converted to UTC pandas agrees they're equal.

### Practice

1. For `orders` dates `["2025-01-05", "2025-02-10", "2025-03-15"]`, compute each date's weekday name and the number of days until the end of its month.
2. A user in London clicked at `2025-07-01 08:00` local time. What time was that in UTC and in India?

<details>
<summary><b>Answer</b></summary>

```python
d = pd.Series(pd.to_datetime(["2025-01-05", "2025-02-10", "2025-03-15"]))
print(d.dt.day_name().tolist(), ((d + pd.offsets.MonthEnd(0)) - d).dt.days.tolist())
click = pd.Timestamp("2025-07-01 08:00", tz="Europe/London")
print(click.tz_convert("UTC"), click.tz_convert("Asia/Kolkata"))
```

**Output:**

```text
['Sunday', 'Monday', 'Saturday'] [26, 18, 16]
2025-07-01 07:00:00+00:00 2025-07-01 12:30:00+05:30
```

`MonthEnd(0)` rolls forward to the month end (or stays if already there). In July the UK is on summer time (UTC+1), so 08:00 London is 07:00 UTC and 12:30 in India.

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [1141. User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/) | 🟢 Easy |
| 2 | [1327. List the Products Ordered in a Period](https://leetcode.com/problems/list-the-products-ordered-in-a-period/) | 🟢 Easy |
| 3 | [1890. The Latest Login in 2020](https://leetcode.com/problems/the-latest-login-in-2020/) | 🟢 Easy |
| 4 | [1193. Monthly Transactions I](https://leetcode.com/problems/monthly-transactions-i/) | 🟡 Medium |

**Learn more:** [pandas: time series / date functionality](https://pandas.pydata.org/docs/user_guide/timeseries.html) · [pandas: offset aliases](https://pandas.pydata.org/docs/user_guide/timeseries.html#offset-aliases)

---

## 38. Time Series: resample, rolling, shift and Window Functions

![Daily sales with a 7-day rolling average: the rolling window smooths out the weekly pattern and noise](images/data-science/rolling-average.png)

### Theory

> **In simple words:** a **time series** is a measurement taken over time: daily sales, hourly temperature, monthly users. Four tools answer almost every time-series question: **resample** (change the time step: daily → monthly), **rolling** (a moving window: the average of the last 7 days), **shift** (compare with the previous period) and **cumulative/expanding** totals.

**Words to know:**

- **Time series:** values indexed by time, in order.
- **DatetimeIndex:** an index made of timestamps; needed for `resample` and time-based `rolling`.
- **Resample:** regroup by a new time frequency. **Downsampling** = coarser (days → months, needs aggregation). **Upsampling** = finer (months → days, needs filling).
- **Rolling window (moving window):** for each point, look at the last N values (or the last N days) and compute something, like a **moving average**.
- **Expanding window:** from the start up to each point (running total, running max).
- **Exponentially weighted (EWM):** a moving average where recent values count more, fading smoothly into the past.
- **Shift / lag:** move values down by N steps so each row sees the value from N periods ago. **Lead:** the opposite.
- **diff / pct_change:** change from the previous value, absolute / as a fraction.
- **Seasonality:** a pattern that repeats at a fixed period (weekends, December). **Trend:** a long-term rise or fall. **Noise:** random ups and downs.
- **Year-over-year (YoY):** comparing with the same period last year, which removes seasonality.

**Everyday picture.** Daily step counts jump around: lazy Sundays, busy Mondays. A **7-day rolling average** is asking "what's my typical day this week?", which hides the Sunday dip. **Resample to months** is reading the monthly summary on your fitness app. **Shift** is "compared with yesterday". **Cumulative sum** is "total steps since New Year".

**Rolling mean, traced** with a 3-day window on `[10, 20, 30, 40, 50]`:

| day | value | window | rolling mean |
|---|---|---|---|
| 1 | 10 | [10] | NaN (fewer than 3 values) |
| 2 | 20 | [10, 20] | NaN |
| 3 | 30 | [10, 20, 30] | 20 |
| 4 | 40 | [20, 30, 40] | 30 |
| 5 | 50 | [30, 40, 50] | 40 |

`min_periods=1` would give 10 and 15 for the first two days instead of NaN.

**The toolbox (with a DatetimeIndex):**

| Need | Code | SQL window equivalent |
|---|---|---|
| monthly totals | `s.resample("MS").sum()` | `GROUP BY date_trunc('month', ...)` |
| weekly averages | `s.resample("W").mean()` | |
| 7-day moving average | `s.rolling(7).mean()` or `s.rolling("7D").mean()` | `AVG(...) OVER (ORDER BY d ROWS 6 PRECEDING)` |
| centred moving average | `s.rolling(7, center=True).mean()` | |
| running total | `s.cumsum()` / `s.expanding().sum()` | `SUM(...) OVER (ORDER BY d)` |
| previous value | `s.shift(1)` | `LAG(...)` |
| next value | `s.shift(-1)` | `LEAD(...)` |
| day-over-day change | `s.diff()`, `s.pct_change()` | |
| same day last week | `s.shift(7)` (daily data) | |
| smooth, recent-weighted | `s.ewm(span=7).mean()` | |
| upsample + fill | `s.resample("D").ffill()` / `.interpolate()` | |

**`rolling(7)` vs `rolling("7D")`:** a number means "the last 7 **rows**"; a time string means "the last 7 **days of time**", which is correct even when some days are missing from the data. With gaps, prefer the time-based window.

**Missing days:** a shop with no sales on a day often has **no row** for that day. Resampling to `"D"` creates the missing days (as NaN or 0 with `.sum()`); do that before rolling, or the 7-row window silently covers more than 7 days.

**When to use what:** resample for reports at a different granularity; rolling to see the trend through noise; shift/diff/pct_change for growth and "consecutive" questions; YoY (`shift(12)` on monthly data) to compare across seasons.

**Common mistakes:**

- ❌ Rolling or shifting **unsorted** data. ✅ `sort_index()` (or `sort_values("date")`) first.
- ❌ Rolling over rows when days are missing. ✅ `rolling("7D")` or resample to daily first.
- ❌ Using a centred window for forecasting or features (it peeks into the future). ✅ Trailing windows for anything predictive.
- ❌ `pct_change` when the previous value is 0 (gives `inf`).
- ❌ Comparing December with November and calling it growth (seasonality). ✅ Compare with last December.

**Used in real software:** dashboards with 7-day averages (COVID case charts made this famous), finance (moving averages, returns with `pct_change`), monitoring (error rate over the last 5 minutes), retention and growth metrics (week-over-week), ML features for forecasting (lags and rolling statistics, `machine-learning.md`).

### Python

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

rng = np.random.default_rng(42)
days = pd.date_range("2025-01-01", "2025-04-30", freq="D")
weekly = np.where(days.dayofweek >= 5, 40, 0)                  # weekends sell more
trend = np.linspace(100, 160, len(days))                       # slow growth
sales = pd.Series((trend + weekly + rng.normal(0, 12, len(days))).round(), index=days, name="sales")

print(sales.head(8))
print(sales.resample("MS").sum())
print(sales.resample("W").mean().head(3).round(1))
```

**Output:**

```text
2025-01-01    104.0
2025-01-02     88.0
2025-01-03    110.0
2025-01-04    153.0
2025-01-05    119.0
2025-01-06     87.0
2025-01-07    105.0
2025-01-08    100.0
Freq: D, Name: sales, dtype: float64
2025-01-01    3688.0
2025-02-01    3753.0
2025-03-01    4631.0
2025-04-01    4804.0
Freq: MS, Name: sales, dtype: float64
2025-01-05    114.8
2025-01-12    114.4
2025-01-19    120.9
Freq: W-SUN, Name: sales, dtype: float64
```

```python
df = sales.to_frame()
df["ma7"] = sales.rolling(7).mean().round(1)
df["prev_day"] = sales.shift(1)
df["change"] = sales.diff()
df["pct"] = (sales.pct_change() * 100).round(1)
df["same_day_last_week"] = sales.shift(7)
df["running_total"] = sales.cumsum()
print(df.iloc[5:10])

monthly = sales.resample("MS").sum()
print(pd.DataFrame({"total": monthly, "growth_pct": (monthly.pct_change() * 100).round(1)}))

fig, ax = plt.subplots(figsize=(9, 3.4), layout="constrained")
ax.plot(sales.index, sales, color="#94a3b8", linewidth=1, label="daily sales")
ax.plot(df.index, df["ma7"], color="#2563eb", linewidth=2.5, label="7-day rolling average")
ax.set(title="Rolling averages reveal the trend under weekly swings", ylabel="units")
ax.xaxis.set_major_locator(plt.matplotlib.dates.MonthLocator())         # one tick per month...
ax.xaxis.set_major_formatter(plt.matplotlib.dates.DateFormatter("%b"))   # ...labelled with its name
ax.legend(loc="upper left")
fig.savefig("rolling-average.png", dpi=100)
plt.close(fig)
```

**Output:**

```text
            sales    ma7  prev_day  change   pct  same_day_last_week  running_total
2025-01-06   87.0    NaN     119.0   -32.0 -26.9                 NaN          661.0
2025-01-07  105.0  109.4      87.0    18.0  20.7                 NaN          766.0
2025-01-08  100.0  108.9     105.0    -5.0  -4.8               104.0          866.0
2025-01-09  104.0  111.1     100.0     4.0   4.0                88.0          970.0
2025-01-10   94.0  108.9     104.0   -10.0  -9.6               110.0         1064.0
             total  growth_pct
2025-01-01  3688.0         NaN
2025-02-01  3753.0         1.8
2025-03-01  4631.0        23.4
2025-04-01  4804.0         3.7
```

(The chart code uses Matplotlib, taught in Part 7.)

```python
gappy = pd.Series([10, 20, 30, 40], index=pd.to_datetime(["2025-01-01", "2025-01-02", "2025-01-08", "2025-01-09"]))
print(pd.DataFrame({"value": gappy, "last_3_rows": gappy.rolling(3).sum(), "last_3_days": gappy.rolling("3D").sum()}))

temps = pd.DataFrame({"day": pd.date_range("2025-01-01", periods=6), "temp": [20, 22, 21, 25, 26, 24]})
temps["warmer_than_yesterday"] = temps["temp"] > temps["temp"].shift(1)
print(temps)
run = (temps["warmer_than_yesterday"] != temps["warmer_than_yesterday"].shift()).cumsum()
print("longest warming streak:", temps.groupby(run)["warmer_than_yesterday"].sum().max(), "days")
```

**Output:**

```text
            value  last_3_rows  last_3_days
2025-01-01     10          NaN         10.0
2025-01-02     20          NaN         30.0
2025-01-08     30         60.0         30.0
2025-01-09     40         90.0         70.0
         day  temp  warmer_than_yesterday
0 2025-01-01    20                  False
1 2025-01-02    22                   True
2 2025-01-03    21                  False
3 2025-01-04    25                   True
4 2025-01-05    26                   True
5 2025-01-06    24                  False
longest warming streak: 2 days
```

The gappy example shows the difference: on 8 January, "last 3 rows" reaches back to 1 January (a week ago), while "last 3 days" correctly includes only 8 January. The streak trick numbers each run of equal values (`!= shift()` marks where a run changes, `cumsum` counts the changes), then counts the Trues in each run: a common interview pattern for "consecutive days".

### Practice

1. From `sales`, find the best and worst **week** (by total) and the date each week ends.
2. Add a column marking days where sales were above their own 7-day rolling average by more than 20%.

<details>
<summary><b>Answer</b></summary>

```python
weekly_total = sales.resample("W").sum()
print(weekly_total.idxmax().date(), weekly_total.max(), weekly_total.idxmin().date(), weekly_total.min())
spike = sales > 1.2 * sales.rolling(7).mean()
print(spike.sum(), sales[spike].index[:3].strftime("%Y-%m-%d").tolist())
```

**Output:**

```text
2025-04-27 1160.0 2025-05-04 495.0
16 ['2025-01-11', '2025-01-12', '2025-01-19']
```

The weekly totals of the first and last partial weeks (fewer than 7 days) are naturally smaller: check the date range before calling one the "worst week".

</details>

| # | LeetCode problem | Difficulty |
|---|---|---|
| 1 | [197. Rising Temperature](https://leetcode.com/problems/rising-temperature/) | 🟢 Easy |
| 2 | [180. Consecutive Numbers](https://leetcode.com/problems/consecutive-numbers/) | 🟡 Medium |
| 3 | [1321. Restaurant Growth](https://leetcode.com/problems/restaurant-growth/) | 🟡 Medium |
| 4 | [1204. Last Person to Fit in the Bus](https://leetcode.com/problems/last-person-to-fit-in-the-bus/) | 🟡 Medium |
| 5 | [626. Exchange Seats](https://leetcode.com/problems/exchange-seats/) | 🟡 Medium |
| 6 | [3220. Odd and Even Transactions](https://leetcode.com/problems/odd-and-even-transactions/) | 🟡 Medium |
| 7 | [601. Human Traffic of Stadium](https://leetcode.com/problems/human-traffic-of-stadium/) | 🔴 Hard |

**Learn more:** [pandas: resampling](https://pandas.pydata.org/docs/user_guide/timeseries.html#resampling) · [pandas: windowing operations](https://pandas.pydata.org/docs/user_guide/window.html)

---

### ✅ Part 5 checkpoint

Without looking, can you:

- [ ] Explain split–apply–combine and write a named aggregation with `agg`?
- [ ] Say when to use `agg`, `transform`, `filter` and `apply`, and compute each row's share of its group?
- [ ] Number each customer's orders and compute days since their previous order?
- [ ] Predict the rows kept by inner, left, right and outer joins, and write an anti-join and a self-join?
- [ ] Explain row explosion and prevent it with `validate=`; use `merge_asof` for "latest value as of"?
- [ ] Pivot long → wide with totals, melt wide → long, and count combinations with `crosstab`?
- [ ] `unstack` a two-key groupby and flatten multi-level columns?
- [ ] Do date arithmetic correctly (month ends, business days) and convert between time zones?
- [ ] Resample, compute a rolling average, and compare with the previous period and the same period last week?

Your toolkit now answers most business questions. Part 6 makes it **fast** and lets it handle **big** data.

---

# Part 6 — Moderate: Bigger and Faster Data

> **Goal:** Make pandas code fast, fit bigger data into memory, and know when to switch to the modern tools built for size: **Apache Arrow**, **Polars** and **DuckDB**.  
> **You need:** Parts 2–5. The Big-O idea from `dsa-python.md` Section 13 ("how does the work grow as the data grows?") helps here.

---

## 39. Performance: Vectorise, Avoid Loops and Measure

![The speed ladder: built-in vectorised operations are hundreds of times faster than Python loops over rows](images/data-science/39-speed-ladder.svg)

### Theory

> **In simple words:** pandas is fast when **it** does the looping (in compiled code) and slow when **you** loop in Python. So: express work as whole-column operations, look things up with joins or sets instead of nested loops, and **measure** before and after any "optimisation", because guesses about speed are usually wrong.

**Words to know:**

- **Performance:** how fast code runs and how much memory it uses.
- **Bottleneck:** the slowest part, which limits the whole program. Speeding up anything else barely helps.
- **Profiling:** measuring where time is actually spent.
- **`%timeit` / `timeit`:** runs a line many times and reports the typical time (in a notebook, `%timeit expr`; in a script, the `timeit` module).
- **`time.perf_counter()`:** a precise clock for timing a block of code once.
- **Vectorised operation:** one call that processes a whole column in compiled code (Section [11](#11-vectorised-maths-and-universal-functions)).
- **Row iteration:** `iterrows`, `itertuples` or `apply(axis=1)`: Python code run once per row.
- **Big-O:** how the work grows with the input size n: O(n) doubles when n doubles; O(n²) quadruples.
- **Hash lookup:** checking membership in a set or dict in roughly constant time, O(1), however big it is.
- **JIT (just-in-time) compiler:** a tool like **Numba** that compiles a Python function to machine code the first time it runs.

**Everyday picture.** Sorting post by hand, one letter at a time, versus feeding the whole bag into a sorting machine. The machine has a start-up cost (the call overhead), so for 3 letters your hands are fine; for 30,000 the machine wins by miles.

**The speed ladder** (fastest first; typical numbers for a million rows):

| Approach | Example | Relative speed |
|---|---|---|
| Built-in vectorised method | `df["a"] * df["b"]`, `.sum()`, `.str.lower()` | 1× (the baseline: milliseconds) |
| NumPy on the underlying arrays | `np.where(...)`, `df["a"].to_numpy()` | about the same |
| `groupby` / `merge` / `map` | built-in, compiled | fast |
| `Series.apply(func)` | Python per value | 10–100× slower |
| `itertuples()` loop | Python per row, light | 50–200× slower |
| `iterrows()` / `apply(axis=1)` | Python per row, builds a Series each time | 500–5,000× slower |

**Big-O traps in data code:**

| Slow pattern | Why | Fast replacement |
|---|---|---|
| `for each order: find its customer in a list` | O(n × m) | `merge` (hash join, about O(n + m)) |
| `if x in some_list` inside a loop | list search is O(m) each time | `set(some_list)` → O(1) lookups; `isin` |
| `df = pd.concat([df, row])` in a loop | copies everything each time: O(n²) | collect a list, concat once |
| `df.loc[i, "col"] = ...` in a loop | per-cell overhead | compute the whole column at once |
| repeated `df[df["id"] == x]` | scans every row each time | `groupby` once, or set the index |

**How to optimise, step by step:**

1. **Make it correct first**, with a small test case to compare against.
2. **Measure** the whole thing: is it actually too slow?
3. **Find the bottleneck** (time each step; in notebooks `%%time` on a cell, or `%prun` / `line_profiler` for detail).
4. **Fix the bottleneck**: vectorise it, replace loops with `merge`/`groupby`/`isin`, reduce the data early (filter rows and columns first).
5. **Measure again** and check the result is still identical (`pd.testing.assert_frame_equal`).
6. Still too slow? Shrink memory (Section [40](#40-memory-dtypes-categoricals-chunking-and-apache-arrow)), or move to Polars or DuckDB (Sections [41](#41-polars-fast-dataframes-with-lazy-queries)–[42](#42-duckdb-sql-on-dataframes-and-files)).

**When a loop is fine:** a few thousand rows; logic that depends on the previous row's **result** and has no built-in (try `cumsum`/`shift` first; if not, Numba compiles the loop).

**Common mistakes:**

- ❌ Optimising before measuring (the slow part is rarely where you think).
- ❌ `iterrows` for arithmetic. ✅ Column maths.
- ❌ Timing once, with a cold cache, and trusting the number. ✅ `%timeit` repeats the run.
- ❌ "Optimising" and changing the answer. ✅ Compare outputs before and after.

**Used in real software:** data teams routinely turn hour-long notebook loops into seconds-long vectorised code; production pipelines profile jobs and fix the slowest step; the same thinking (move work into compiled, batched operations) is why GPUs and databases are fast.

### Python

```python
import time
import numpy as np
import pandas as pd

rng = np.random.default_rng(0)
n = 200_000
df = pd.DataFrame({"qty": rng.integers(1, 10, n), "price": rng.uniform(10, 3000, n).round(2),
                   "city": rng.choice(["Pune", "Mumbai", "Delhi", "Goa"], n)})

def timed(label, func, repeat=3):
    best = min(_time_once(func) for _ in range(repeat))
    print(f"{label:<28} {best * 1000:9.1f} ms")
    return best

def _time_once(func):
    t0 = time.perf_counter(); func(); return time.perf_counter() - t0

base = timed("vectorised  qty * price", lambda: df["qty"] * df["price"])
timed("numpy arrays", lambda: df["qty"].to_numpy() * df["price"].to_numpy())
timed("list comprehension + zip", lambda: [q * p for q, p in zip(df["qty"], df["price"])])
timed("itertuples loop", lambda: [r.qty * r.price for r in df.itertuples()])
slow = timed("apply(axis=1)", lambda: df.apply(lambda r: r["qty"] * r["price"], axis=1), repeat=1)
print(f"apply(axis=1) was about {slow / base:,.0f}× slower than the vectorised line")
```

**Output:**

```text
vectorised  qty * price            0.1 ms
numpy arrays                       0.1 ms
list comprehension + zip          15.8 ms
itertuples loop                  100.3 ms
apply(axis=1)                    411.7 ms
apply(axis=1) was about 3,201× slower than the vectorised line
```

`time.perf_counter()` reads a precise clock; taking the best of a few runs reduces noise from other programs. Your exact numbers will differ; the ordering won't.

```python
vip_list = list(rng.integers(0, 1_000_000, 5_000))
ids = pd.Series(rng.integers(0, 1_000_000, 20_000))

t0 = time.perf_counter(); slow = [i in vip_list for i in ids]; t1 = time.perf_counter()
vip_set = set(vip_list)
fast = [i in vip_set for i in ids]; t2 = time.perf_counter()
vec = ids.isin(vip_list); t3 = time.perf_counter()
print(f"list lookups {t1 - t0:.3f}s · set lookups {t2 - t1:.4f}s · isin {t3 - t2:.4f}s · same: {slow == fast == vec.tolist()}")

rows = [{"a": i, "b": i * 2} for i in range(5_000)]
t0 = time.perf_counter()
grown = pd.DataFrame(columns=["a", "b"])
for r in rows[:1_000]:                                      # only 1,000: the slow way is really slow
    grown = pd.concat([grown, pd.DataFrame([r])], ignore_index=True)
t1 = time.perf_counter()
once = pd.DataFrame(rows); t2 = time.perf_counter()
print(f"concat in a loop (1,000 rows): {t1 - t0:.2f}s · build once (5,000 rows): {t2 - t1:.4f}s")
```

**Output:**

```text
list lookups 1.807s · set lookups 0.0010s · isin 0.0007s · same: True
concat in a loop (1,000 rows): 0.07s · build once (5,000 rows): 0.0013s
```

```python
from numba import njit

prices = rng.uniform(90, 110, 1_000_000)

def max_drawdown_py(p):                       # worst fall from a previous peak: depends on the running peak
    peak, worst = p[0], 0.0
    for x in p:
        peak = max(peak, x)
        worst = min(worst, (x - peak) / peak)
    return worst

max_drawdown_jit = njit(max_drawdown_py)      # same code, compiled by Numba
max_drawdown_jit(prices[:10])                 # first call compiles (not timed)

t0 = time.perf_counter(); a = max_drawdown_py(prices); t1 = time.perf_counter()
b = max_drawdown_jit(prices); t2 = time.perf_counter()
peak = np.maximum.accumulate(prices); c = ((prices - peak) / peak).min(); t3 = time.perf_counter()
print(f"python {t1 - t0:.3f}s · numba {t2 - t1:.4f}s · numpy {t3 - t2:.4f}s · equal: {np.isclose(a, b) and np.isclose(b, c)}")
```

**Output:**

```text
python 0.092s · numba 0.0007s · numpy 0.0037s · equal: True
```

**Max drawdown** (the worst drop from a previous high, a standard risk measure in finance) depends on a running peak, so it looks like it needs a loop. Numba compiles that loop; NumPy's `maximum.accumulate` (a running maximum) solves it without one. Look for a built-in first; reach for Numba when none exists.

### Practice

1. Replace this loop with one vectorised line: `out = []; for q, p in zip(df["qty"], df["price"]): out.append("big" if q * p > 5000 else "small")`.
2. You must flag 10 million transactions whose `card_id` is in a blocklist of 100,000 cards. Which approach, and why?

<details>
<summary><b>Answer</b></summary>

```python
labels = np.where(df["qty"] * df["price"] > 5000, "big", "small")
print(pd.Series(labels).value_counts().to_dict())
```

**Output:**

```text
{'big': 110303, 'small': 89697}
```

2. `transactions["card_id"].isin(blocklist)`: it builds a hash table of the blocklist once and checks each transaction in roughly constant time, so the total work is about O(n + m). A Python loop testing `card in blocklist_list` would be O(n × m) = 10¹² comparisons.

</details>

**Learn more:** [pandas: enhancing performance](https://pandas.pydata.org/docs/user_guide/enhancingperf.html) · [Numba: 5-minute guide](https://numba.readthedocs.io/en/stable/user/5minguide.html)

---

## 40. Memory: dtypes, Categoricals, Chunking and Apache Arrow

![Shrinking a table: smaller number types, categories for repeated text, Arrow strings, and reading only the columns you need](images/data-science/40-memory.svg)

### Theory

> **In simple words:** pandas keeps the whole table in **RAM** (memory). When a file is too big, shrink each column to the smallest type that fits, store repeated text as categories, read only the columns and rows you need, or process the file in **chunks**. **Apache Arrow** is the modern columnar memory format that makes text cheaper and lets pandas, Polars, DuckDB and Spark share data without copying.

**Words to know:**

- **RAM:** the computer's working memory. A laptop has 8–32 GB; if your data (plus the copies operations make) doesn't fit, the program crashes or slows to a crawl as the system **swaps** to disk.
- **Footprint:** how much memory an object uses. `df.memory_usage(deep=True)` measures it.
- **Downcast:** convert to a smaller numeric type (`int64` → `int16`, `float64` → `float32`) when values fit.
- **Chunking:** reading and processing a file in pieces of, say, 100,000 rows, keeping only small running results.
- **Streaming / out-of-core:** processing data bigger than memory by never holding all of it at once.
- **Apache Arrow:** a standard **columnar in-memory** format (and the `pyarrow` library). Columns are stored contiguously, strings efficiently, missing values as a compact bitmap.
- **Zero-copy:** handing data between tools without copying it, possible when both use Arrow.
- **Backend (`dtype_backend="pyarrow"`):** telling pandas to store columns as Arrow arrays instead of NumPy arrays.

**Everyday picture.** Packing for a flight with a strict weight limit: roll clothes tightly (smaller types), pack one toiletry bag instead of a bottle per day (categories for repeated values), leave behind what you won't use (read only some columns), and if it still doesn't fit, ship boxes ahead one at a time (chunks).

**Where the memory goes**, for a table of 1 million orders:

| Column | Default type | Bytes per row | Better type | Bytes per row |
|---|---|---|---|---|
| `qty` (1–20) | `int64` | 8 | `int8` | 1 |
| `price` | `float64` | 8 | `float32` (if precision allows) | 4 |
| `city` (4 values) | `str` | ~55 (Python strings) / ~12 (Arrow strings) | `category` | ~1 |
| `order_id` | `int64` | 8 | `int32` (if < 2.1 billion) | 4 |

**Rule of thumb:** pandas often needs **5–10× the file size** in RAM during analysis (operations create temporary copies). A 2 GB CSV can need 10+ GB.

**The memory toolkit:**

| Technique | Code |
|---|---|
| Measure | `df.memory_usage(deep=True).sum()`, `df.info(memory_usage="deep")` |
| Read fewer columns | `pd.read_csv(path, usecols=[...])`, `pd.read_parquet(path, columns=[...])` |
| Choose types when reading | `pd.read_csv(path, dtype={"qty": "int8", "city": "category"})` |
| Downcast numbers | `pd.to_numeric(s, downcast="integer")`, `s.astype("float32")` |
| Repeated text → category | `s.astype("category")` (Section [29](#29-categorical-data-and-binning-cut-and-qcut)) |
| Arrow-backed columns | `pd.read_csv(path, dtype_backend="pyarrow")`, `pd.read_parquet(path, dtype_backend="pyarrow")` |
| Process in chunks | `for chunk in pd.read_csv(path, chunksize=100_000): ...` |
| Filter early | read Parquet with `filters=[("city", "==", "Pune")]` so non-matching row groups are skipped |
| Free memory | `del df` (and avoid keeping many intermediate copies) |

**Chunked processing, step by step** (total revenue per city from a 50 GB CSV):

1. Open the file with `chunksize=1_000_000`.
2. For each chunk: compute `qty * price`, then `groupby("city").sum()`, giving a tiny result.
3. Keep a list of those tiny results.
4. At the end, `pd.concat(results).groupby(level=0).sum()` combines them.

This works for anything that can be **combined from parts**: sums, counts, min/max. Means need sums and counts kept separately (Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine)'s "don't average averages"). Medians and exact distinct counts can't be combined this simply.

**pandas + Arrow in 2026:** pandas 3's default `str` type is already backed by Arrow when `pyarrow` is installed, which is why text columns use far less memory than the old `object` type. Polars and DuckDB use Arrow natively, so converting between them and pandas is cheap.

**When to stop squeezing pandas:** when data is several times bigger than RAM, when you need many full passes over it, or when a query is mostly filtering and aggregating. Then DuckDB (SQL, out-of-core) or Polars (lazy, streaming) is simpler and faster than hand-written chunking.

**Common mistakes:**

- ❌ `float16` or `int8` without checking ranges: silent overflow or precision loss. ✅ Check `min`/`max` first; `downcast=` checks for you.
- ❌ `memory_usage()` without `deep=True` (it doesn't count the text itself).
- ❌ Chunking and then computing a mean of chunk means. ✅ Keep sums and counts.
- ❌ Loading everything "just in case". ✅ Only the columns and rows you need.

**Used in real software:** analysts squeezing month-long logs onto a laptop; ETL jobs that stream files in chunks; data platforms passing Arrow tables between Python, Spark, DuckDB and databases (Arrow Flight, ADBC); Parquet readers skipping irrelevant row groups.

### Python

```python
import os, tempfile
import numpy as np
import pandas as pd

rng = np.random.default_rng(1)
n = 1_000_000
df = pd.DataFrame({
    "order_id": np.arange(n),
    "qty": rng.integers(1, 20, n),
    "price": rng.uniform(10, 3000, n).round(2),
    "city": rng.choice(["Pune", "Mumbai", "Delhi", "Goa"], n),
})
def mb(frame):
    return round(frame.memory_usage(deep=True).sum() / 1e6, 1)

print("default:", mb(df), "MB")
print(df.memory_usage(deep=True).div(1e6).round(1).to_dict())

small = df.assign(order_id=pd.to_numeric(df["order_id"], downcast="integer"),
                  qty=pd.to_numeric(df["qty"], downcast="integer"),
                  price=df["price"].astype("float32"),
                  city=df["city"].astype("category"))
print("shrunk:", mb(small), "MB", small.dtypes.astype(str).to_dict())
print("max price error from float32:", float((small["price"] - df["price"]).abs().max().round(5)))
```

**Output:**

```text
default: 36.5 MB
{'Index': 0.0, 'order_id': 8.0, 'qty': 8.0, 'price': 8.0, 'city': 12.5}
shrunk: 10.0 MB {'order_id': 'int32', 'qty': 'int8', 'price': 'float32', 'city': 'category'}
max price error from float32: 0.00012
```

`downcast="integer"` picks the smallest integer type that holds every value (`int32` for IDs up to a million, `int8` for 1–19). `float32` keeps about 7 significant digits, so prices around 3,000 lose a tiny fraction of a paisa: fine for analysis, not for accounting.

```python
folder = tempfile.mkdtemp()
path = os.path.join(folder, "orders.csv")
df.to_csv(path, index=False)
print(f"CSV on disk: {os.path.getsize(path) / 1e6:.0f} MB")

totals = []
for chunk in pd.read_csv(path, chunksize=250_000, dtype={"city": "category"}):
    chunk["revenue"] = chunk["qty"] * chunk["price"]
    totals.append(chunk.groupby("city", observed=True)["revenue"].agg(["sum", "count"]))
combined = pd.concat(totals).groupby(level=0).sum()
combined["mean"] = combined["sum"] / combined["count"]               # combine sums and counts, not means
combined["sum"] = combined["sum"].round().astype("int64")
print(combined.round(1))
print("matches the in-memory answer:",
      np.allclose(combined["mean"].sort_index(), (df["qty"] * df["price"]).groupby(df["city"]).mean().sort_index()))
```

**Output:**

```text
CSV on disk: 22 MB
               sum   count     mean
city                               
Delhi   3753520188  249544  15041.5
Goa     3760307329  250298  15023.3
Mumbai  3773641550  250135  15086.4
Pune    3766985104  250023  15066.6
matches the in-memory answer: True
```

```python
arrow_df = pd.read_csv(path, dtype_backend="pyarrow", engine="pyarrow")
print(arrow_df.dtypes.astype(str).to_dict(), "|", mb(arrow_df), "MB")

pq = os.path.join(folder, "orders.parquet")
df.to_parquet(pq, row_group_size=100_000)
pune = pd.read_parquet(pq, columns=["city", "price"], filters=[("city", "==", "Pune")])
print(len(pune), pune["city"].unique().tolist())
```

**Output:**

```text
{'order_id': 'int64[pyarrow]', 'qty': 'int64[pyarrow]', 'price': 'double[pyarrow]', 'city': 'string[pyarrow]'} | 32.5 MB
250023 ['Pune']
```

`engine="pyarrow"` uses Arrow's multi-threaded CSV reader (much faster on big files); `dtype_backend="pyarrow"` keeps the result in Arrow types (shown as `...[pyarrow]`). The Parquet read loaded two columns and only Pune rows.

### Practice

1. A column `rating` holds whole numbers 1–5 in `int64`. What type should it be, and how much memory does that save per million rows?
2. Compute the **maximum** price per city from the CSV in chunks. Why is max easier to combine than median?

<details>
<summary><b>Answer</b></summary>

1. `int8` (or a `category` if you treat ratings as labels): 1 byte instead of 8, saving about 7 MB per million rows.

```python
parts = [c.groupby("city")["price"].max() for c in pd.read_csv(path, chunksize=250_000, usecols=["city", "price"])]
print(pd.concat(parts).groupby(level=0).max().to_dict())
```

**Output:**

```text
{'Delhi': 2999.99, 'Goa': 3000.0, 'Mumbai': 2999.99, 'Pune': 2999.96}
```

The max of the chunk maxima **is** the overall max. A median needs to see all values at once (the middle of the whole column isn't the middle of chunk middles), so it needs a different approach: an approximate algorithm, or DuckDB/Polars, which handle it for you.

</details>

**Learn more:** [pandas: scaling to large datasets](https://pandas.pydata.org/docs/user_guide/scale.html) · [pandas: PyArrow functionality](https://pandas.pydata.org/docs/user_guide/pyarrow.html) · [Apache Arrow: overview](https://arrow.apache.org/overview/)

---

## 41. Polars: Fast DataFrames with Lazy Queries

![Lazy Polars: build a query plan, let the optimiser push filters and column selection down to the file, then run it in parallel](images/data-science/41-polars-lazy.svg)

### Theory

> **In simple words:** **Polars** is a newer DataFrame library written in Rust. It uses all your CPU cores, stores data in Arrow format, and has a **lazy** mode: you describe the whole query first, Polars **optimises** it (reads only the needed columns, filters early) and then runs it. On big data it's often 5–20× faster than pandas and uses less memory.

**Words to know:**

- **Polars:** a fast DataFrame library (imported as `pl`), built on Arrow, with a Python API.
- **Rust:** a fast, memory-safe compiled programming language, used to write Polars' engine.
- **Expression:** a description of a column calculation, like `pl.col("qty") * pl.col("price")`. Expressions are combined and run by Polars' engine, not by Python.
- **Context:** where an expression is used: `select` (choose/compute columns), `with_columns` (add columns), `filter` (rows), `group_by(...).agg(...)` (summaries).
- **Eager vs lazy:** **eager** runs each step immediately (like pandas). **Lazy** builds a **query plan** and runs it only when you call `.collect()`.
- **Query optimiser:** the part that rewrites a plan to do less work. **Predicate pushdown:** applying filters as early as possible (even inside the file reader). **Projection pushdown:** reading only the columns the query uses.
- **Parallelism / multi-threading:** using several CPU cores at once.
- **Streaming engine:** processing data in batches so results can be computed on data bigger than RAM.
- **`scan_*` vs `read_*`:** `scan_parquet`/`scan_csv` start a **lazy** query on a file; `read_*` loads it eagerly.

**Everyday picture.** pandas is a cook who starts chopping the moment each instruction is read. Lazy Polars reads the **whole recipe first**, notices you only need the onions from the bag of vegetables and that half the dishes are cancelled, and only then starts cooking, with four helpers at once.

**pandas vs Polars, side by side:**

| Task | pandas | Polars |
|---|---|---|
| read | `pd.read_parquet(p)` | `pl.read_parquet(p)` (eager), `pl.scan_parquet(p)` (lazy) |
| new column | `df.assign(rev=df.qty * df.price)` | `df.with_columns((pl.col("qty") * pl.col("price")).alias("rev"))` |
| filter | `df[df["city"] == "Pune"]` | `df.filter(pl.col("city") == "Pune")` |
| select | `df[["a", "b"]]` | `df.select("a", "b")` |
| group | `df.groupby("city").agg(total=("rev", "sum"))` | `df.group_by("city").agg(pl.col("rev").sum().alias("total"))` |
| sort | `df.sort_values("rev", ascending=False)` | `df.sort("rev", descending=True)` |
| window | `df.groupby("city")["rev"].transform("sum")` | `pl.col("rev").sum().over("city")` |
| join | `a.merge(b, on="id", how="left")` | `a.join(b, on="id", how="left")` |
| to/from pandas | | `pl.from_pandas(pdf)`, `df.to_pandas()` |

**Key differences in thinking:**

1. **No index.** Rows are just rows; there's nothing like `.loc` with labels. (Fewer surprises.)
2. **Expressions everywhere.** You describe what you want with `pl.col(...)`; Polars decides how to run it in parallel.
3. **Strict types.** Columns don't silently change type; missing values are `null` for every type.
4. **Lazy by choice.** For files, start with `scan_*`, chain steps, and `collect()` once at the end. `explain()` shows the optimised plan.

**When to use Polars:** data from a few hundred MB to tens of GB on one machine; pipelines you'll rerun often; when pandas is too slow or runs out of memory. **When to stay with pandas:** small data, code that relies on the index, or libraries that expect pandas (many plotting and stats tools; though `.to_pandas()` at the end is cheap).

**Common mistakes:**

- ❌ Writing Python loops or `map_elements` (Polars' `apply`) over rows: you lose all the speed. ✅ Expressions.
- ❌ Calling `.collect()` after every step in lazy mode (defeats the optimiser). ✅ Collect once.
- ❌ Expecting pandas-style index behaviour (`reset_index`, label alignment). ✅ Use explicit joins and columns.
- ❌ Copying pandas method names (`groupby` → it's `group_by`; `sort_values` → `sort`).

**Used in real software:** data engineering pipelines replacing slow pandas jobs; feature engineering for ML on large tables; analytics on single big machines instead of clusters; the Polars Cloud and GPU engines for scaling further.

### Python

```python
import os, tempfile
import numpy as np
import pandas as pd
import polars as pl

rng = np.random.default_rng(2)
n = 2_000_000
pdf = pd.DataFrame({"order_id": np.arange(n), "city": rng.choice(["Pune", "Mumbai", "Delhi", "Goa"], n),
                    "category": rng.choice(["electronics", "kitchen", "books"], n),
                    "qty": rng.integers(1, 10, n), "price": rng.uniform(10, 3000, n).round(2)})
folder = tempfile.mkdtemp()
path = os.path.join(folder, "orders.parquet")
pdf.to_parquet(path)

df = pl.read_parquet(path)                       # eager
print(df.head(3))
out = (df.with_columns((pl.col("qty") * pl.col("price")).alias("revenue"))
         .filter(pl.col("category") == "electronics")
         .group_by("city")
         .agg(pl.col("revenue").sum().round(0).cast(pl.Int64).alias("total"),
              pl.len().alias("orders"),
              pl.col("revenue").mean().round(1).alias("avg"))
         .sort("total", descending=True))
print(out)
```

**Output:**

```text
shape: (3, 5)
┌──────────┬────────┬─────────────┬─────┬────────┐
│ order_id ┆ city   ┆ category    ┆ qty ┆ price  │
│ ---      ┆ ---    ┆ ---         ┆ --- ┆ ---    │
│ i64      ┆ str    ┆ str         ┆ i64 ┆ f64    │
╞══════════╪════════╪═════════════╪═════╪════════╡
│ 0        ┆ Goa    ┆ electronics ┆ 3   ┆ 786.78 │
│ 1        ┆ Mumbai ┆ electronics ┆ 2   ┆ 986.05 │
│ 2        ┆ Pune   ┆ electronics ┆ 8   ┆ 167.61 │
└──────────┴────────┴─────────────┴─────┴────────┘
shape: (4, 4)
┌────────┬────────────┬────────┬────────┐
│ city   ┆ total      ┆ orders ┆ avg    │
│ ---    ┆ ---        ┆ ---    ┆ ---    │
│ str    ┆ i64        ┆ u32    ┆ f64    │
╞════════╪════════════╪════════╪════════╡
│ Pune   ┆ 1256821098 ┆ 166640 ┆ 7542.1 │
│ Delhi  ┆ 1256269117 ┆ 166672 ┆ 7537.4 │
│ Mumbai ┆ 1249885023 ┆ 166417 ┆ 7510.6 │
│ Goa    ┆ 1247897143 ┆ 166008 ┆ 7517.1 │
└────────┴────────────┴────────┴────────┘
```

`pl.len()` counts rows per group. Polars prints the shape and each column's type under its name.

```python
query = (pl.scan_parquet(path)                   # lazy: nothing is read yet
           .filter(pl.col("city") == "Pune")
           .with_columns((pl.col("qty") * pl.col("price")).alias("revenue"))
           .group_by("category")
           .agg(pl.col("revenue").sum().round(0).cast(pl.Int64).alias("total"))
           .sort("category"))
print(query.explain())                           # the optimised plan
print(query.collect())
```

**Output:**

```text
SORT BY [col("category")]
  AGGREGATE[maintain_order: false]
    [col("revenue").sum().round().strict_cast(Int64).alias("total")] BY [col("category")]
    FROM
    simple π 2/2 ["category", "revenue"]
       WITH_COLUMNS:
       [(col("qty").cast(Float64) * col("price")).alias("revenue")] 
        simple π 3/3 ["category", "qty", "price"]
          Parquet SCAN [/var/folders/63/sbjzw15506j9pfmwfgdf45t40000gn/T/tmp9h288f6m/orders.parquet]
          PROJECT 4/5 COLUMNS
          SELECTION: col("city") == "Pune"
          ESTIMATED ROWS: 2000000
shape: (3, 2)
┌─────────────┬────────────┐
│ category    ┆ total      │
│ ---         ┆ ---        │
│ str         ┆ i64        │
╞═════════════╪════════════╡
│ books       ┆ 1256703633 │
│ electronics ┆ 1256821098 │
│ kitchen     ┆ 1248605154 │
└─────────────┴────────────┘
```

In the plan, look for the file scan line: it lists only the columns the query needs (`PROJECT 4/5 COLUMNS` or similar) and carries the `city == "Pune"` filter (the **selection** or **predicate**), so the reader skips data before it ever reaches Python.

```python
import time

t0 = time.perf_counter()
p_res = (pdf.assign(revenue=pdf["qty"] * pdf["price"]).groupby(["city", "category"])["revenue"].sum())
t1 = time.perf_counter()
l_res = (pl.scan_parquet(path).with_columns((pl.col("qty") * pl.col("price")).alias("revenue"))
           .group_by("city", "category").agg(pl.col("revenue").sum()).collect())
t2 = time.perf_counter()
print(f"pandas {t1 - t0:.3f}s · polars (incl. reading the file) {t2 - t1:.3f}s")

ranked = df.with_columns((pl.col("qty") * pl.col("price")).alias("revenue")).with_columns(
    pl.col("revenue").sum().over("city").round(0).cast(pl.Int64).alias("city_total"),
    pl.col("revenue").rank("dense", descending=True).over("city").alias("rank_in_city"))
print(ranked.filter(pl.col("rank_in_city") == 1).select("city", "order_id", "revenue", "city_total").sort("city"))
print(type(ranked.head(2).to_pandas()).__name__)
```

**Output:**

```text
pandas 0.071s · polars (incl. reading the file) 0.025s
shape: (4, 4)
┌────────┬──────────┬──────────┬────────────┐
│ city   ┆ order_id ┆ revenue  ┆ city_total │
│ ---    ┆ ---      ┆ ---      ┆ ---        │
│ str    ┆ i64      ┆ f64      ┆ i64        │
╞════════╪══════════╪══════════╪════════════╡
│ Delhi  ┆ 361799   ┆ 26999.91 ┆ 3771202552 │
│ Goa    ┆ 1546598  ┆ 26999.82 ┆ 3764643744 │
│ Mumbai ┆ 760350   ┆ 26999.82 ┆ 3766631336 │
│ Pune   ┆ 1727651  ┆ 26999.19 ┆ 3762129885 │
└────────┴──────────┴──────────┴────────────┘
DataFrame
```

`.over("city")` is Polars' window function: the same idea as pandas' `transform` and SQL's `PARTITION BY` (Section [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking)). Timings depend on your machine; Polars' advantage grows with data size and CPU cores.

### Practice

1. With lazy Polars on the Parquet file: for each category, the number of orders with `qty >= 5` and their average price, sorted by count.
2. Add a column with each order's price minus its category's average price (a window expression).

<details>
<summary><b>Answer</b></summary>

```python
print(pl.scan_parquet(path).filter(pl.col("qty") >= 5).group_by("category")
        .agg(pl.len().alias("n"), pl.col("price").mean().round(1).alias("avg_price"))
        .sort("n", descending=True).collect())
print(df.with_columns((pl.col("price") - pl.col("price").mean().over("category")).round(1).alias("vs_cat"))
        .select("category", "price", "vs_cat").head(3))
```

**Output:**

```text
shape: (3, 3)
┌─────────────┬────────┬───────────┐
│ category    ┆ n      ┆ avg_price │
│ ---         ┆ ---    ┆ ---       │
│ str         ┆ u32    ┆ f64       │
╞═════════════╪════════╪═══════════╡
│ books       ┆ 371146 ┆ 1507.9    │
│ kitchen     ┆ 370167 ┆ 1506.6    │
│ electronics ┆ 369665 ┆ 1506.8    │
└─────────────┴────────┴───────────┘
shape: (3, 3)
┌─────────────┬────────┬─────────┐
│ category    ┆ price  ┆ vs_cat  │
│ ---         ┆ ---    ┆ ---     │
│ str         ┆ f64    ┆ f64     │
╞═════════════╪════════╪═════════╡
│ electronics ┆ 786.78 ┆ -719.8  │
│ electronics ┆ 986.05 ┆ -520.5  │
│ electronics ┆ 167.61 ┆ -1339.0 │
└─────────────┴────────┴─────────┘
```

</details>

**Learn more:** [Polars user guide](https://docs.pola.rs/user-guide/) · [Polars: coming from pandas](https://docs.pola.rs/user-guide/migration/pandas/)

---

## 42. DuckDB: SQL on DataFrames and Files

![DuckDB runs SQL directly on pandas/Polars DataFrames and on Parquet/CSV files, inside your Python process](images/data-science/42-duckdb.svg)

### Theory

> **In simple words:** **DuckDB** is a database that runs **inside your Python program**, with no server to install. It runs fast analytical SQL directly on pandas or Polars DataFrames and on CSV and Parquet files (even ones bigger than memory, or on cloud storage), and gives the result back as a DataFrame. If you know SQL, it's often the quickest way to analyse big files.

**Words to know:**

- **DuckDB:** an **in-process** analytical database (often called "SQLite for analytics").
- **In-process / embedded:** the database runs as a library inside your program, not as a separate server you connect to over a network.
- **OLAP vs OLTP:** **analytical** workloads (scan millions of rows, aggregate: "revenue per month") vs **transactional** ones (many small reads and writes: "update this order"). DuckDB is OLAP; PostgreSQL is mainly OLTP (`sql-postgresql.md`).
- **Columnar, vectorised engine:** processes columns in batches of values at a time, like NumPy, which suits aggregation.
- **Replacement scan:** DuckDB's trick of letting SQL refer to a Python DataFrame variable by name (`FROM orders` finds the `orders` DataFrame).
- **Window function (SQL):** `OVER (PARTITION BY ... ORDER BY ...)` calculations that keep every row (ranks, running totals).
- **CTE (common table expression):** a named sub-query written with `WITH name AS (...)`, making long SQL readable.
- **Spilling to disk:** writing temporary data to disk when memory runs out, so queries on data bigger than RAM still finish.
- **AOV (average order value):** total revenue divided by the number of orders.

**Everyday picture.** Instead of carrying all your files to the library (a database server) to ask the librarian a question, the librarian comes to **your desk**, reads your files where they are, answers, and leaves.

**What DuckDB can query directly:**

| Source | SQL |
|---|---|
| a pandas or Polars DataFrame variable | `SELECT * FROM orders` |
| a Parquet file (or many) | `SELECT * FROM 'data/*.parquet'` |
| a CSV file | `SELECT * FROM read_csv('orders.csv')` |
| files on S3 / HTTP (with the `httpfs` extension) | `SELECT * FROM 's3://bucket/orders/*.parquet'` |
| a DuckDB database file | `duckdb.connect("analytics.duckdb")` |

**Results come back as:** `.df()` (pandas), `.pl()` (Polars), `.fetchall()` (Python tuples), `.arrow()` (Arrow table).

**Why it's fast:** columnar storage, vectorised execution, all CPU cores, reading only needed columns and row groups from Parquet, and spilling to disk instead of crashing when memory runs out.

**pandas vs DuckDB, the same question:**

```text
# pandas
(orders.assign(revenue=orders.qty * orders.price)
       .groupby("city")["revenue"].sum().sort_values(ascending=False))

# DuckDB
duckdb.sql("SELECT city, SUM(qty * price) AS revenue FROM orders GROUP BY city ORDER BY revenue DESC").df()
```

**When to use DuckDB:** big files (GBs, or more than RAM), SQL-shaped questions (joins, group-bys, window functions), querying many Parquet files at once, and when you or your team think in SQL. **When to use pandas/Polars instead:** step-by-step exploratory manipulation, complex Python logic per row, or tight integration with plotting and ML code. They mix freely: SQL for the heavy aggregation, pandas for the last mile.

**Common mistakes:**

- ❌ Loading a huge Parquet file into pandas just to aggregate it. ✅ Aggregate with DuckDB, load the small result.
- ❌ Building SQL strings with f-strings from user input. ✅ Parameters: `duckdb.execute("... WHERE city = ?", ["Pune"])`.
- ❌ Using DuckDB as a multi-user transactional database for an app. ✅ That's PostgreSQL's job; DuckDB is for analytics.

**Used in real software:** analysts querying data-lake Parquet files from a laptop; dbt projects running on DuckDB locally; embedded analytics inside applications; MotherDuck (a cloud service built on DuckDB); a fast engine inside notebooks for anything SQL-shaped.

### Python

```python
import os, tempfile
import duckdb
import numpy as np
import pandas as pd

rng = np.random.default_rng(3)
n = 1_000_000
orders = pd.DataFrame({"order_id": np.arange(n), "customer_id": rng.integers(1, 50_000, n),
                       "city": rng.choice(["Pune", "Mumbai", "Delhi", "Goa"], n),
                       "qty": rng.integers(1, 10, n), "price": rng.uniform(10, 3000, n).round(2),
                       "day": pd.Timestamp("2025-01-01") + pd.to_timedelta(rng.integers(0, 120, n), unit="D")})

result = duckdb.sql("""
    SELECT city, COUNT(*) AS orders, CAST(SUM(qty * price) AS BIGINT) AS revenue
    FROM orders                       -- the pandas DataFrame above, found by name
    GROUP BY city
    ORDER BY revenue DESC
""").df()
print(result)
```

**Output:**

```text
     city  orders     revenue
0    Pune  250320  1884591009
1     Goa  250094  1881515791
2   Delhi  249828  1880764778
3  Mumbai  249758  1879773011
```

```python
folder = tempfile.mkdtemp()
for m in range(1, 5):                                  # one Parquet file per month, like a data lake
    part = orders[orders["day"].dt.month == m]
    part.to_parquet(os.path.join(folder, f"orders_2025_{m:02d}.parquet"))

glob = os.path.join(folder, "*.parquet")
monthly = duckdb.sql(f"""
    SELECT date_trunc('month', day) AS month, CAST(SUM(qty * price) AS BIGINT) AS revenue
    FROM '{glob}'
    GROUP BY month ORDER BY month
""").df()
print(monthly)

top = duckdb.sql(f"""
    WITH per_customer AS (
        SELECT city, customer_id, SUM(qty * price) AS spend
        FROM '{glob}' GROUP BY city, customer_id
    )
    SELECT city, customer_id, ROUND(spend) AS spend,
           RANK() OVER (PARTITION BY city ORDER BY spend DESC) AS rank_in_city
    FROM per_customer
    QUALIFY rank_in_city <= 2
    ORDER BY city, rank_in_city
""").df()
print(top)
```

**Output:**

```text
       month     revenue
0 2025-01-01  1930998971
1 2025-02-01  1760012751
2 2025-03-01  1936563272
3 2025-04-01  1899069595
     city  customer_id     spend  rank_in_city
0   Delhi        19405  170928.0             1
1   Delhi         8402  163646.0             2
2     Goa         5925  169485.0             1
3     Goa        16127  163836.0             2
4  Mumbai        38749  166939.0             1
5  Mumbai        36254  152903.0             2
6    Pune        27195  181097.0             1
7    Pune         3353  162022.0             2
```

The file path here is built by the notes themselves, so an f-string is safe; anything that comes from a user goes through parameters. `QUALIFY` filters on a window function's result (DuckDB supports it; in PostgreSQL you'd wrap the query in a sub-query instead). `date_trunc('month', day)` rounds each date down to the first of its month.

```python
con = duckdb.connect()                                  # an in-memory database
print(con.execute("SELECT city, AVG(price) AS avg_price FROM orders WHERE city = ? GROUP BY city",
                  ["Pune"]).df().round(2))

big_spenders = con.execute(f"SELECT customer_id, SUM(qty * price) AS spend FROM '{glob}' GROUP BY 1 HAVING spend > 150000").pl()
print(type(big_spenders).__name__, big_spenders.shape)
print(duckdb.sql(f"SELECT COUNT(*) AS n FROM '{glob}'").fetchall())
```

**Output:**

```text
   city  avg_price
0  Pune    1506.16
DataFrame (24019, 2)
[(1000000,)]
```

`?` is a **parameter placeholder**: DuckDB inserts `"Pune"` safely. `.pl()` returns a Polars DataFrame, `.fetchall()` plain Python tuples.

### Practice

1. With DuckDB on the `orders` DataFrame: the average order value per city per month, only for (city, month) pairs with an average above 7,550.
2. Using a window function, add each order's running total of revenue per customer, ordered by day, and show customer 1's first 5 rows.

<details>
<summary><b>Answer</b></summary>

```python
print(duckdb.sql("""
    SELECT city, date_trunc('month', day) AS month, ROUND(AVG(qty * price), 1) AS aov
    FROM orders GROUP BY ALL HAVING AVG(qty * price) > 7550 ORDER BY city, month
""").df())
print(duckdb.sql("""
    SELECT customer_id, day, ROUND(qty * price, 2) AS revenue,
           ROUND(SUM(qty * price) OVER (PARTITION BY customer_id ORDER BY day, order_id), 2) AS running
    FROM orders WHERE customer_id = 1 ORDER BY day, order_id LIMIT 5
""").df())
```

**Output:**

```text
     city      month     aov
0  Mumbai 2025-04-01  7552.8
1    Pune 2025-02-01  7576.6
2    Pune 2025-04-01  7556.0
   customer_id        day   revenue   running
0            1 2025-01-03  20839.44  20839.44
1            1 2025-02-05   3561.75  24401.19
2            1 2025-02-06  16086.78  40487.97
3            1 2025-02-14   1170.02  41657.99
4            1 2025-02-19   4458.72  46116.71
```

`CAST(x AS BIGINT)` makes a sum a whole number (no scientific notation like `1.88e+09` in printouts). `GROUP BY ALL` groups by every non-aggregated column in the `SELECT`, a DuckDB convenience. **AOV** means average order value.

</details>

| # | LeetCode problem (solve in SQL with DuckDB, or in pandas) | Difficulty |
|---|---|---|
| 1 | [1321. Restaurant Growth](https://leetcode.com/problems/restaurant-growth/) | 🟡 Medium |
| 2 | [585. Investments in 2016](https://leetcode.com/problems/investments-in-2016/) | 🟡 Medium |
| 3 | [1341. Movie Rating](https://leetcode.com/problems/movie-rating/) | 🟡 Medium |
| 4 | [1393. Capital Gain/Loss](https://leetcode.com/problems/capital-gainloss/) | 🟡 Medium |

**Learn more:** [DuckDB: Python API](https://duckdb.org/docs/stable/clients/python/overview) · [DuckDB: why DuckDB](https://duckdb.org/why_duckdb)

---

### ✅ Part 6 checkpoint

Without looking, can you:

- [ ] Rank five ways of computing a new column from fastest to slowest, and time them?
- [ ] Replace a nested-loop lookup with a `merge`, a set or `isin`, and explain the Big-O difference?
- [ ] Measure a DataFrame's real memory, and shrink it with downcasting and categories?
- [ ] Process a file in chunks and combine the pieces correctly (sums and counts, not means of means)?
- [ ] Explain what Apache Arrow is and why pandas, Polars and DuckDB all use it?
- [ ] Write a lazy Polars query with `filter`, `with_columns`, `group_by` and `over`, and read its plan?
- [ ] Query a DataFrame and a folder of Parquet files with DuckDB SQL, including a window function?

Numbers and tables are only half the story: people understand **pictures**. Part 7 is about charts.

---

# Part 7 — Moderate: Charts with Matplotlib, Seaborn and Plotly

> **Goal:** Draw clear, honest charts: the four basic chart types, multi-panel layouts, annotations, statistical charts with Seaborn, interactive charts with Plotly, and the judgement to pick the right chart for a question.  
> **You need:** Parts 2–5. Every chart image in this part was produced by the code next to it.

---

## 43. Your First Charts with Matplotlib

![The parts of a Matplotlib figure: the figure, axes, title, labels, ticks and legend](images/data-science/07-figure-anatomy.svg)

### Theory

> **In simple words:** a chart shows in one second what a table takes a minute to read. **Matplotlib** is Python's main charting library; Seaborn and pandas' `.plot()` are built on it. You create a **figure** (the whole picture), put one or more **axes** (individual charts) on it, draw on the axes, then save or show the figure.

**Words to know:**

- **Matplotlib:** the foundational Python plotting library. `matplotlib.pyplot`, imported as `plt`, is its main interface.
- **Figure (`fig`):** the whole image or window; it can hold several charts.
- **Axes (`ax`):** **one chart**, with its own x-axis, y-axis, title and data. (Plural-looking but singular. An Axes contains two **axis** objects, the x-axis and y-axis.)
- **Plot / draw:** add marks (lines, bars, points) to an axes.
- **Series (in charts):** one set of values drawn together, like one line. Not the same as a pandas Series, though one often becomes the other.
- **Legend:** the key explaining which colour or marker is which series.
- **Tick / tick label:** the small marks along an axis and their numbers or names.
- **Distribution:** how the values of one variable are spread out: where most of them are, how wide the spread is, whether there's a long tail.
- **Bin:** one bar's range in a histogram (e.g. order values from 500 to 600).
- **DPI (dots per inch):** image resolution when saving. 100 for screens, 150–300 for print and slides.
- **Scatter plot:** a chart with one dot per observation, placed by two numeric values (x and y), for seeing relationships.

**Everyday picture.** The figure is a sheet of paper; each axes is a framed graph you draw on that sheet. You can have one big graph on the sheet, or a 2 × 2 grid of small ones.

**The recommended style** creates both at once and calls methods on `ax`:

```text
fig, ax = plt.subplots(figsize=(6, 4))     # width, height in inches
ax.plot(x, y)                              # draw
ax.set_title("..."); ax.set_xlabel("..."); ax.set_ylabel("...")
fig.savefig("chart.png", dpi=150, bbox_inches="tight")
plt.show()                                 # scripts: open a window (notebooks show charts automatically)
```

You'll also see `plt.plot(...)`, `plt.title(...)` in tutorials. That **pyplot style** draws on "the current chart" and is fine for a quick look; the `ax` style is clearer as soon as there's more than one chart, so these notes use it.

**The four charts you'll use most:**

| Chart | Method | Shows | Example |
|---|---|---|---|
| **Line** | `ax.plot(x, y)` | a trend over an **ordered** x (usually time) | daily sales |
| **Bar** | `ax.bar(labels, values)` (`ax.barh` for horizontal) | comparing amounts between categories | revenue per city |
| **Scatter** | `ax.scatter(x, y)` | the relationship between two numbers | price vs units sold |
| **Histogram** | `ax.hist(values, bins=30)` | the distribution of one number | spread of order values |

**How a histogram is built, traced:** values `[3, 7, 8, 12, 13, 14, 21]` with bins of width 5 starting at 0: [0, 5) has 1 value, [5, 10) has 2, [10, 15) has 3, [15, 20) has 0, [20, 25) has 1. Bar heights: 1, 2, 3, 0, 1. Too few bins hide the shape; too many make noise. Try a few.

**Making a chart readable:** a title that states the **point**; axis labels **with units**; a legend when there's more than one series (`label="..."` on each draw call, then `ax.legend()`); nothing decorative.

**pandas shortcut:** `df.plot(x="date", y="units", ax=ax)`, `s.plot.bar(ax=ax)`, `df["price"].plot.hist(bins=20)` call Matplotlib for you. Handy for quick looks.

**When to use Matplotlib directly:** full control, custom layouts, publication-quality figures. **When something else is quicker:** Seaborn for statistical charts from DataFrames (Sections [46](#46-seaborn-i-distributions)–[48](#48-heatmaps-pair-plots-and-correlation-charts)); Plotly for interactive charts (Section [49](#49-interactive-charts-with-plotly)).

**Common mistakes:**

- ❌ No axis labels or units.
- ❌ A line chart for categories with no order (cities). ✅ A bar chart.
- ❌ Overlapping labels. ✅ `layout="constrained"` in `plt.subplots` (or `fig.tight_layout()`).
- ❌ Making hundreds of figures in a loop without `plt.close(fig)`, which eats memory.

**Used in real software:** scientific papers, reports and model diagnostics (loss curves in `deep-learning.md`, ROC curves in `machine-learning.md`); Matplotlib renders charts inside many other tools.

### Python

```python
import matplotlib.pyplot as plt
import numpy as np

days = np.arange(1, 31)
units = 100 + 2 * days + np.random.default_rng(1).normal(0, 8, 30).round()

fig, ax = plt.subplots(figsize=(6, 3.5))
ax.plot(days, units, marker="o", markersize=3, label="units sold")
ax.plot(days, 100 + 2 * days, linestyle="--", color="gray", label="trend")
ax.set_title("Sales are rising by about 2 units a day")
ax.set_xlabel("Day of month")
ax.set_ylabel("Units sold")
ax.legend()
fig.savefig("first-line-chart.png", dpi=100, bbox_inches="tight")
plt.close(fig)
print(type(fig).__name__, type(ax).__name__)
```

**Output:**

```text
Figure Axes
```

![A line chart of units sold over 30 days, with a dashed trend line](images/data-science/first-line-chart.png)

```python
rng = np.random.default_rng(3)
cities = ["Pune", "Mumbai", "Delhi", "Bengaluru"]
revenue = [5800, 5600, 1000, 900]
price = rng.uniform(50, 3000, 80)
units_sold = (400 - 0.1 * price + rng.normal(0, 30, 80)).clip(0)
order_values = rng.lognormal(mean=6.5, sigma=0.6, size=500)

fig, axes = plt.subplots(2, 2, figsize=(9, 6.5), layout="constrained")   # a 2 × 2 grid; axes is a 2D array
axes[0, 0].plot(days, units)
axes[0, 0].set_title("Line: trend over time")
axes[0, 1].bar(cities, revenue, color="tab:orange")
axes[0, 1].set_title("Bar: compare categories")
axes[1, 0].scatter(price, units_sold, alpha=0.6)
axes[1, 0].set(title="Scatter: relationship", xlabel="Price (₹)", ylabel="Units sold")
counts, edges, _ = axes[1, 1].hist(order_values, bins=30, color="tab:green", edgecolor="white")
axes[1, 1].set(title="Histogram: distribution", xlabel="Order value (₹)")
fig.savefig("four-basic-charts.png", dpi=100)
plt.close(fig)
print(axes.shape, f"tallest bin: {int(counts.max())} orders between ₹{edges[counts.argmax()]:.0f} and ₹{edges[counts.argmax() + 1]:.0f}")
```

**Output:**

```text
(2, 2) tallest bin: 73 orders between ₹588 and ₹712
```

![A 2 by 2 grid: line, bar, scatter and histogram charts](images/data-science/four-basic-charts.png)

`ax.hist` returns the bar heights, the bin edges and the drawn bars, so you can read the numbers behind the picture. `ax.set(title=..., xlabel=...)` sets several properties at once.

### Practice

1. Draw a horizontal bar chart of `revenue` per city, sorted so the biggest bar is on top, with the revenue written at the end of each bar.
2. Draw a histogram of `order_values` with 10 bins and another with 100. Which shows the shape better?

<details>
<summary><b>Answer</b></summary>

```python
order = np.argsort(revenue)                    # smallest first: barh draws from the bottom up
names = [cities[i] for i in order]
vals = [revenue[i] for i in order]
fig, ax = plt.subplots(figsize=(5, 3), layout="constrained")
ax.barh(names, vals)
for i, v in enumerate(vals):
    ax.text(v + 50, i, f"₹{v:,}", va="center")
ax.set(xlabel="Revenue (₹)", title="Pune and Mumbai lead revenue", xlim=(0, 7000))
plt.close(fig)

fig, (a1, a2) = plt.subplots(1, 2, figsize=(8, 3), layout="constrained")
a1.hist(order_values, bins=10); a2.hist(order_values, bins=100)
plt.close(fig)
print(names, "| 10 bins: smooth but blocky; 100 bins: noisy. Around 30 suits 500 values.")
```

**Output:**

```text
['Bengaluru', 'Delhi', 'Mumbai', 'Pune'] | 10 bins: smooth but blocky; 100 bins: noisy. Around 30 suits 500 values.
```

`va="center"` vertically centres each label on its bar.

</details>

**Learn more:** [Matplotlib: quick start guide](https://matplotlib.org/stable/users/explain/quick_start.html) · [Matplotlib: plot types gallery](https://matplotlib.org/stable/plot_types/index.html)

---

## 44. Matplotlib Anatomy: Figures, Axes and Subplots

![A mosaic layout: a highlighted bar chart with a second y-axis, a correlation matrix and a log-scale line chart](images/data-science/mosaic-layout.png)

### Theory

> **In simple words:** a figure can hold many charts arranged in a grid or any uneven layout. Knowing how the pieces nest (figure → axes → axis → ticks) lets you control every detail, and putting related charts side by side (**small multiples**) is one of the most effective ways to compare.

**Words to know:**

- **Artist:** Matplotlib's name for anything drawn: lines, text, bars, even the axes. Everything visible is an artist with properties you can set.
- **Subplot:** one axes inside a grid of axes.
- **Grid layout:** `plt.subplots(nrows, ncols)` returns a figure and an **array** of axes.
- **Shared axes (`sharex` / `sharey`):** charts that use the same scale, so they're directly comparable.
- **Constrained layout:** Matplotlib's automatic spacing engine that stops titles and labels overlapping.
- **Mosaic:** a layout described by a picture-like string, e.g. `"AAB;CCB"`.
- **Twin axes (`twinx`):** a second y-axis on the right, sharing the x-axis.
- **Log scale:** an axis where equal steps mean equal **multiples** (1, 10, 100, 1000), for data spanning many orders of magnitude.
- **Small multiples (facets):** the same chart repeated for each group, on shared scales.

**Everyday picture.** A newspaper page: the page is the figure; each article's graphic is an axes; some graphics span two columns (a mosaic); a few share the same vertical scale so readers can compare them at a glance.

**The object tree:**

```text
Figure                      fig        the whole image
└── Axes                    ax         one chart (many per figure)
    ├── Axis (x and y)      ax.xaxis   scale, ticks, tick labels, label
    ├── Lines, bars, text   artists you add with ax.plot / ax.bar / ax.text
    ├── Title, legend
    └── Spines              ax.spines  the four border lines
```

**Layouts:**

| Code | Gives |
|---|---|
| `fig, ax = plt.subplots()` | one chart |
| `fig, axes = plt.subplots(2, 3)` | a 2 × 3 array: `axes[row, col]` |
| `fig, (a, b) = plt.subplots(1, 2, sharey=True)` | two charts side by side, same y-scale |
| `plt.subplots(..., layout="constrained")` | automatic spacing (use it always) |
| `fig.subplot_mosaic("AAB;CCB")` | named, uneven layout: `axd["A"]` spans two columns, `axd["B"]` spans two rows |
| `ax.twinx()` | second y-axis (use sparingly) |
| `ax.inset_axes([x, y, w, h])` | a small chart inside a chart (a zoomed detail) |
| `for ax in axes.flat:` | loop over every chart in a grid |

**Small multiples beat one crowded chart:** five overlapping lines in one chart are hard to read; five small charts with `sharex=True, sharey=True` let each line be seen and compared. Seaborn's `col=`/`row=` does this automatically (Section [47](#47-seaborn-ii-relationships-categories-and-facets)).

**On twin axes:** two y-scales let you place any two lines anywhere relative to each other, so a reader may see a relationship that's an artefact of the chosen scales. Prefer two stacked charts with `sharex=True`; use `twinx` only when the two measures are tightly linked and clearly labelled.

**Common mistakes:**

- ❌ `axes[0]` on a 2D grid (that's a whole row). ✅ `axes[0, 1]`, or `axes.flat`.
- ❌ Comparing charts on different y-scales without noticing. ✅ `sharey=True`.
- ❌ Dual y-axes that make unrelated series look correlated.
- ❌ Fiddling with `subplots_adjust` by hand. ✅ `layout="constrained"`.

**Used in real software:** dashboards (one figure, many panels), model diagnostics (training and validation curves side by side), scientific figures with labelled panels (a), (b), (c).

### Python

```python
import matplotlib.pyplot as plt
import numpy as np

rng = np.random.default_rng(5)
fig, axd = plt.subplot_mosaic("AAB;CCB", figsize=(9, 5), layout="constrained")
months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun"]
orders = np.array([120, 135, 160, 150, 190, 230])
avg_value = np.array([840, 820, 870, 910, 880, 950])

axd["A"].bar(months, orders, color="lightgray")
axd["A"].bar(months[-1], orders[-1], color="tab:red")               # highlight the one bar that matters
axd["A"].set_title("Orders: June was the best month")
right = axd["A"].twinx()                                             # second y-axis, different units
right.plot(months, avg_value, color="tab:blue", marker="o")
right.set_ylabel("Avg order value (₹)", color="tab:blue")

corr = np.corrcoef(rng.normal(size=(5, 50)))
im = axd["B"].imshow(corr, cmap="RdBu", vmin=-1, vmax=1)            # diverging colours centred on 0
axd["B"].set_title("Correlation matrix")
fig.colorbar(im, ax=axd["B"], shrink=0.7)

users = np.array([50, 400, 3_000, 25_000, 180_000, 1_400_000])
axd["C"].plot(months, users, marker="o")
axd["C"].set_yscale("log")                                           # equal steps = equal multiples
axd["C"].set_title("Users (log scale): roughly 8× growth each month")
fig.savefig("mosaic-layout.png", dpi=100)
plt.close(fig)
print(sorted(axd), (users[1:] / users[:-1]).round(1))
```

**Output:**

```text
['A', 'B', 'C'] [8.  7.5 8.3 7.2 7.8]
```

`imshow` draws a grid of numbers as coloured squares; `colorbar` adds the colour key. On the log scale, the steady ~8× monthly growth becomes a straight line, which a normal scale would hide behind one huge final jump.

```python
cities = ["Pune", "Mumbai", "Delhi", "Goa"]
monthly = {c: 100 + rng.normal(0, 10, 12).cumsum() + k * 15 for k, c in enumerate(cities)}

fig, axes = plt.subplots(1, 4, figsize=(11, 2.6), sharey=True, layout="constrained")
for ax, city in zip(axes.flat, cities):
    for other in cities:                                  # all cities in grey for context...
        ax.plot(range(1, 13), monthly[other], color="lightgray", linewidth=1)
    ax.plot(range(1, 13), monthly[city], color="tab:blue", linewidth=2.2)   # ...and this one highlighted
    ax.set(title=city, xticks=[1, 4, 7, 10], xlabel="month")
    ax.spines[["top", "right"]].set_visible(False)
fig.suptitle("Small multiples: each city against the others")
fig.savefig("small-multiples.png", dpi=100)
plt.close(fig)
print(len(axes), "panels sharing one y-scale")
```

**Output:**

```text
4 panels sharing one y-scale
```

![Four small line charts, one per city, each highlighting that city in blue over the others in grey](images/data-science/small-multiples.png)

`fig.suptitle` puts one title over the whole figure; `ax.spines[...]` hides the top and right border lines.

### Practice

1. Make a 2 × 3 grid of histograms of 6 different random normal samples (means 0 to 5), sharing the x-axis, each titled with its mean.
2. Why might `sharey=False` in the small-multiples chart mislead a reader?

<details>
<summary><b>Answer</b></summary>

```python
fig, axes = plt.subplots(2, 3, figsize=(9, 5), sharex=True, layout="constrained")
for mean, ax in enumerate(axes.flat):
    ax.hist(rng.normal(mean, 1, 300), bins=20)
    ax.set_title(f"mean {mean}")
plt.close(fig)
print(axes.shape, axes.flat[5].get_title())
```

**Output:**

```text
(2, 3) mean 5
```

2. Each panel would pick its own y-range, so a city with tiny changes would look as dramatic as one with huge changes; the reader compares heights that mean different things.

</details>

**Learn more:** [Matplotlib: arranging multiple axes](https://matplotlib.org/stable/users/explain/axes/arranging_axes.html) · [Matplotlib: subplot_mosaic](https://matplotlib.org/stable/users/explain/axes/mosaic.html)

---

## 45. Styling, Annotation and Saving Charts

![A line chart with a forecast band, a target line, a shaded festival week and an arrow annotation](images/data-science/annotated-forecast.png)

### Theory

> **In simple words:** the difference between an OK chart and a great one is a few deliberate touches: colour used for **meaning**, a note pointing at the interesting part, numbers formatted for humans (₹20k, 35%), clutter removed, and the file saved at the right quality.

**Words to know:**

- **Colormap (cmap):** a mapping from numbers to colours, used for heatmaps and colour scales.
- **Sequential colormap:** light-to-dark for values from low to high (`viridis`, `Blues`).
- **Diverging colormap:** two colours meeting at a neutral middle, for values above and below a centre like 0 (`RdBu`, `coolwarm`).
- **Qualitative (categorical) palette:** distinct colours for unordered groups (`tab10`).
- **Perceptually uniform:** equal steps in value look like equal steps in colour (`viridis` is; the old rainbow `jet` isn't).
- **Colour-blind safe:** distinguishable for people with colour-vision deficiency (about 1 in 12 men). Avoid red–green pairs.
- **Annotation:** text or an arrow pointing at a specific point.
- **Reference line / band:** a horizontal or vertical line (`axhline`) or shaded region (`axvspan`) marking a target or a period.
- **Tick formatter:** a rule turning tick values into labels (`₹20k`, `35%`).
- **Raster vs vector:** **raster** images (PNG, JPG) are grids of pixels; **vector** images (SVG, PDF) store shapes and stay sharp at any size.
- **Style sheet / rcParams:** global default settings for fonts, colours and sizes.

**Everyday picture.** A tour guide doesn't just stand in front of a painting; they **point** at the detail you should notice. Annotations are your pointing finger; grey-for-context, colour-for-focus is your spotlight.

**Colour, step by step:**

1. Start everything in **grey**.
2. Colour only what carries the message (one series, one bar).
3. For numbers on a scale, use a **sequential** colormap; for numbers around a midpoint, a **diverging** one centred on that midpoint (`vmin=-1, vmax=1`).
4. Check it works in greyscale and for colour-blind readers (`cividis`, `viridis`, blue/orange pairs).

**Annotation tools:**

| Code | Does |
|---|---|
| `ax.annotate("text", xy=(x, y), xytext=(x2, y2), arrowprops=dict(arrowstyle="->"))` | label with an arrow |
| `ax.text(x, y, "text")` | plain text at a data position |
| `ax.axhline(30000, ls="--")`, `ax.axvline(...)` | a target or threshold line |
| `ax.axvspan(start, end, alpha=0.15)` | shade a period |
| `ax.fill_between(x, low, high, alpha=0.2)` | a band (forecast range, confidence interval) |

**Axes and ticks:**

| Code | Does |
|---|---|
| `ax.set_xlim(...)`, `ax.set_ylim(0, None)` | control the visible range |
| `ax.set_yscale("log")` | log scale |
| `ax.yaxis.set_major_formatter(StrMethodFormatter("₹{x:,.0f}"))` | currency with thousands separators |
| `ax.yaxis.set_major_formatter(PercentFormatter(1.0))` | 0.35 → 35% |
| `ax.yaxis.set_major_formatter(lambda v, pos: f"₹{v / 1000:.0f}k")` | any custom format |
| `ax.spines[["top", "right"]].set_visible(False)` | remove unneeded borders |
| `ax.grid(axis="y", alpha=0.3)` | light gridlines on one axis |

**Styles and saving:**

- `plt.style.use("seaborn-v0_8-whitegrid")` (or `"ggplot"`, `"fivethirtyeight"`) changes every later chart; `plt.rcParams["font.size"] = 11` sets a default.
- Save **PNG** at `dpi=150`–`300` for documents and slides; **SVG** or **PDF** for print and the web (vector, sharp at any zoom).
- `bbox_inches="tight"` trims extra white space.

**When to annotate:** whenever there's one thing the reader must notice (an event, a threshold, a peak). **When not to:** don't label every point; three annotations is usually the most a chart can take.

**Common mistakes:**

- ❌ Rainbow (`jet`) colormaps and red–green pairs. ✅ `viridis`, `cividis`, blue–orange.
- ❌ A sequential colormap for data centred on zero (correlations, profit/loss). ✅ Diverging, with symmetric limits.
- ❌ Saving at the default resolution for a printed report. ✅ `dpi=200` or SVG.
- ❌ Every chart in a different style. ✅ Set the style once at the top.

**Used in real software:** news graphics (The Economist, the FT, the New York Times all annotate heavily), executive reports, forecast charts with uncertainty bands, monitoring dashboards with threshold lines.

### Python

```python
import matplotlib.pyplot as plt
import numpy as np
from matplotlib.ticker import StrMethodFormatter

rng = np.random.default_rng(5)
days = np.arange(1, 91)
sales = 20000 + 150 * days + rng.normal(0, 2500, 90)
sales[60:67] += 15000                                       # a one-week festival sale
forecast_days = np.arange(91, 121)
forecast = 20000 + 150 * forecast_days
spread = np.linspace(2000, 8000, 30)                        # uncertainty grows further ahead

fig, ax = plt.subplots(figsize=(8, 4), layout="constrained")
ax.plot(days, sales, color="tab:blue", label="Actual")
ax.plot(forecast_days, forecast, color="tab:blue", ls="--", label="Forecast")
ax.fill_between(forecast_days, forecast - spread, forecast + spread, color="tab:blue", alpha=0.2, label="Likely range")
ax.axhline(30000, color="gray", ls=":", lw=1)
ax.text(2, 30500, "Target ₹30k/day", color="gray")
ax.axvspan(61, 67, color="tab:orange", alpha=0.15)
ax.annotate("Festival sale", xy=(67, sales[63]), xytext=(78, 44000), arrowprops=dict(arrowstyle="->", color="black"))
ax.yaxis.set_major_formatter(StrMethodFormatter("₹{x:,.0f}"))
ax.spines[["top", "right"]].set_visible(False)
ax.set(title="Daily revenue: steady growth, one festival spike", xlabel="Day", ylabel="Revenue")
ax.legend(loc="upper left", frameon=False)
fig.savefig("annotated-forecast.png", dpi=100)
plt.close(fig)
print("peak day:", int(days[np.argmax(sales)]), "| first day above target:", int(days[np.argmax(sales > 30000)]))
```

**Output:**

```text
peak day: 65 | first day above target: 51
```

```python
grid = np.linspace(-1, 1, 200).reshape(1, -1)
fig, axes = plt.subplots(4, 1, figsize=(7, 3.2), layout="constrained")
for ax, (cmap, kind) in zip(axes, [("viridis", "sequential (good)"), ("cividis", "sequential, colour-blind safe"),
                                    ("RdBu", "diverging: centred on 0"), ("jet", "rainbow: avoid")]):
    ax.imshow(grid, cmap=cmap, aspect="auto")
    ax.set_yticks([]); ax.set_xticks([])
    ax.set_ylabel(cmap, rotation=0, ha="right", va="center")
    ax.set_title(kind, fontsize=9, loc="left")
fig.savefig("colormaps.png", dpi=100)
plt.close(fig)
print("saved 4 colormaps")
```

**Output:**

```text
saved 4 colormaps
```

![Four colour scales: viridis, cividis, RdBu diverging around a white middle, and the rainbow jet map with its false bands](images/data-science/colormaps.png)

Look at `jet`: bright yellow and cyan bands appear where the data changes smoothly, inventing boundaries that aren't there.

### Practice

1. Plot `sales` again, shade weekend days (where `day % 7` is 5 or 6), and format the y-axis in thousands (`₹20k`).
2. Save the same figure as PNG at 200 dpi and as SVG. Which file is bigger, and which stays sharp when zoomed?

<details>
<summary><b>Answer</b></summary>

```python
import os, tempfile

fig, ax = plt.subplots(figsize=(8, 3), layout="constrained")
ax.plot(days, sales)
weekend = days[(days % 7 == 5) | (days % 7 == 6)]
for d in weekend:
    ax.axvspan(d - 0.5, d + 0.5, color="gray", alpha=0.15, lw=0)
ax.yaxis.set_major_formatter(lambda y, pos: f"₹{y / 1000:.0f}k")   # (value, position) → label
folder = tempfile.mkdtemp()
fig.savefig(os.path.join(folder, "s.png"), dpi=200); fig.savefig(os.path.join(folder, "s.svg"))
plt.close(fig)
print(len(weekend), "weekend days;", {f: os.path.getsize(os.path.join(folder, f)) // 1000 for f in ["s.png", "s.svg"]}, "KB")
```

**Output:**

```text
26 weekend days; {'s.png': 72, 's.svg': 20} KB
```

Here the SVG is smaller: it stores only 26 rectangles and one 90-point line, while the 200-dpi PNG stores every pixel. The SVG also stays sharp at any zoom. A scatter with 100,000 points flips this: the SVG must describe every dot and becomes far bigger than the PNG.

</details>

**Learn more:** [Matplotlib: choosing colormaps](https://matplotlib.org/stable/users/explain/colors/colormaps.html) · [Matplotlib: annotations](https://matplotlib.org/stable/users/explain/text/annotations.html) · [ColorBrewer: colour-blind-safe palettes](https://colorbrewer2.org/)

---

## 46. Seaborn I: Distributions

![Four ways to show a distribution: histogram with density curve, box plot, violin plot and ECDF](images/data-science/seaborn-distributions.png)

### Theory

> **In simple words:** **Seaborn** is built on Matplotlib and speaks **DataFrames**: you pass a table and column names, and it groups, colours and labels for you. This section covers the charts that answer "**how are the values spread out?**": histograms, density curves, box plots, violin plots and ECDFs, and how to compare them across groups.

**Words to know:**

- **Seaborn:** a statistical plotting library built on Matplotlib, imported as `sns`.
- **`hue`:** a column whose values set the colour, splitting one chart into groups.
- **KDE (kernel density estimate):** a smooth curve estimating the shape of a distribution, made by placing a small bump on every data point and adding the bumps up.
- **Bandwidth:** how wide each KDE bump is. Too narrow → wiggly; too wide → over-smoothed.
- **Density:** a scale where the area under the curve is 1, so groups of different sizes can be compared by shape.
- **Box plot (box-and-whisker):** the box spans the middle 50% (Q1 to Q3, the **IQR**); the line is the **median**; whiskers reach the furthest points within 1.5 × IQR; dots beyond are possible outliers (Section [30](#30-outliers-and-data-validation)).
- **Violin plot:** a box plot's cousin showing the full density shape, mirrored.
- **Strip / swarm plot:** every individual point, jittered or packed so they don't overlap.
- **ECDF (empirical cumulative distribution function):** for each value x, the fraction of data ≤ x. Reads off percentiles directly; needs no binning.
- **Skew:** a lopsided distribution. **Right-skewed** has a long tail to the right (incomes, order values). **Modality:** the number of peaks (**bimodal** = two peaks, often two groups mixed together).

**Everyday picture.** A box plot is a **class photo arranged by height**: the box is the middle half of the class, the line is the middle student, and the whiskers reach the tallest and shortest "normal" students; anyone far beyond is a dot. A violin plot is the same photo seen as a silhouette, showing where students bunch up.

**Choosing a distribution chart:**

| Chart | Function | Best for | Watch out |
|---|---|---|---|
| histogram | `sns.histplot` | the overall shape | bin width changes the story |
| KDE | `sns.kdeplot` | smooth comparison of groups | invents values beyond the data's range; bandwidth matters |
| box plot | `sns.boxplot` | comparing many groups compactly | hides two-peak shapes |
| violin | `sns.violinplot` | shape + comparison | harder for general audiences |
| strip / swarm | `sns.stripplot`, `sns.swarmplot` | small data: show every point | unreadable for thousands of points |
| ECDF | `sns.ecdfplot` | precise percentiles, many groups | less intuitive at first |

**Comparing groups of different sizes:** raw-count histograms make the bigger group look taller. Use `stat="density", common_norm=False` so each group's area is 1 and you compare **shapes**.

**Reading a skewed distribution:** in right-skewed data the **mean is above the median** (the tail pulls it up). Say "the typical order is ₹X (median)" rather than quoting the mean.

**When to use:** at the start of every analysis, for every important numeric column (Section [60](#60-a-complete-exploratory-data-analysis-eda)); whenever you'd report an average, look at the distribution behind it first.

**Common mistakes:**

- ❌ Reporting only the mean of a skewed column.
- ❌ One histogram with default bins and concluding "no pattern". ✅ Try a few bin widths, or an ECDF.
- ❌ A box plot of bimodal data (it hides the two peaks). ✅ Violin, strip plot or histogram.
- ❌ Comparing groups by raw counts. ✅ `stat="density", common_norm=False`.

**Used in real software:** latency distributions in monitoring (p50/p95/p99 read straight off an ECDF), A/B test result plots, model residual checks, salary and price reports.

### Python

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns

rng = np.random.default_rng(11)
n = 400
shop = pd.DataFrame({
    "city": rng.choice(["Pune", "Mumbai", "Delhi", "Bengaluru"], n, p=[0.3, 0.3, 0.2, 0.2]),
    "channel": rng.choice(["app", "web"], n, p=[0.6, 0.4]),
    "items": rng.integers(1, 8, n),
})
shop["order_value"] = (shop["items"] * rng.uniform(150, 450, n) * np.where(shop["channel"] == "app", 1.15, 1.0)).round()
shop["delivery_days"] = (rng.gamma(2, 1.2, n) + np.where(shop["city"] == "Delhi", 1.0, 0.0)).round(1)
shop["rating"] = (5 - 0.4 * shop["delivery_days"] + rng.normal(0, 0.5, n)).clip(1, 5).round(1)
print(shop.head(3))
print(shop["order_value"].agg(["mean", "median", "skew"]).round(2).to_dict())

sns.set_theme(style="whitegrid")
fig, axes = plt.subplots(2, 2, figsize=(10, 7), layout="constrained")
sns.histplot(data=shop, x="order_value", hue="channel", kde=True, stat="density", common_norm=False, ax=axes[0, 0])
axes[0, 0].set_title("Histogram + KDE: app orders tend to be larger")
sns.boxplot(data=shop, x="city", y="delivery_days", ax=axes[0, 1])
axes[0, 1].set_title("Box plot: Delhi deliveries take longer")
sns.violinplot(data=shop, x="channel", y="order_value", inner="quart", ax=axes[1, 0])
axes[1, 0].set_title("Violin: full shape, quartiles inside")
sns.ecdfplot(data=shop, x="delivery_days", hue="city", ax=axes[1, 1])
axes[1, 1].axhline(0.9, color="gray", ls=":")
axes[1, 1].set_title("ECDF: read percentiles off the curve (dotted = 90%)")
fig.savefig("seaborn-distributions.png", dpi=100)
plt.close(fig)
print(shop.groupby("city")["delivery_days"].quantile(0.9).round(1).to_dict())
```

**Output:**

```text
     city channel  items  order_value  delivery_days  rating
0    Pune     app      7       3221.0            1.3     4.4
1  Mumbai     web      1        157.0            4.1     3.9
2   Delhi     app      4        771.0            1.6     3.4
{'mean': 1298.92, 'median': 1218.0, 'skew': 0.66}
{'Bengaluru': 4.6, 'Delhi': 5.4, 'Mumbai': 5.0, 'Pune': 4.9}
```

The `skew` statistic is positive (a right tail), and the mean sits above the median, as expected. Look at the violins: they reach **below zero**, although no order is negative. That's the KDE smoothing beyond the data, the "invents values" warning in the table above; `cut=0` stops the curve at the smallest and largest real values. The last line reads the 90th-percentile delivery time per city: the same numbers where each ECDF curve crosses the dotted 0.9 line.

```python
bimodal = pd.Series(np.concatenate([rng.normal(30, 4, 300), rng.normal(60, 5, 300)]), name="minutes")
fig, axes = plt.subplots(1, 3, figsize=(10, 2.8), layout="constrained")
sns.boxplot(x=bimodal, ax=axes[0]); axes[0].set_title("box plot: hides two peaks")
sns.histplot(x=bimodal, bins=30, ax=axes[1]); axes[1].set_title("histogram: two groups!")
sns.kdeplot(x=bimodal, bw_adjust=0.3, ax=axes[2], label="bw 0.3")
sns.kdeplot(x=bimodal, bw_adjust=3, ax=axes[2], label="bw 3")
axes[2].legend(); axes[2].set_title("KDE bandwidth matters")
fig.savefig("bimodal.png", dpi=100)
plt.close(fig)
print(f"mean {bimodal.mean():.1f} min, but almost nobody takes ~45 min: "
      f"{((bimodal > 40) & (bimodal < 50)).mean():.1%} of trips")
```

**Output:**

```text
mean 45.2 min, but almost nobody takes ~45 min: 1.7% of trips
```

![A box plot that hides two peaks, a histogram that reveals them, and two KDE curves with different bandwidths](images/data-science/bimodal.png)

Commute times mixing walkers (~30 min) and bus riders (~60 min): the mean, 45 minutes, describes almost nobody. `bw_adjust` scales the KDE bandwidth: 3 smooths the two peaks into one hill.

### Practice

1. Draw a box plot of `rating` by `city`, ordered from the lowest to the highest median rating.
2. Using the ECDF idea without a chart, what fraction of orders were delivered within 2 days?

<details>
<summary><b>Answer</b></summary>

```python
order = shop.groupby("city")["rating"].median().sort_values().index.tolist()
fig, ax = plt.subplots(figsize=(6, 3), layout="constrained")
sns.boxplot(data=shop, x="city", y="rating", order=order, ax=ax)
plt.close(fig)
print(order, f"{(shop['delivery_days'] <= 2).mean():.1%}")
```

**Output:**

```text
['Delhi', 'Bengaluru', 'Mumbai', 'Pune'] 42.2%
```

</details>

**Learn more:** [Seaborn: visualizing distributions](https://seaborn.pydata.org/tutorial/distributions.html) · [Claus Wilke: visualizing distributions](https://clauswilke.com/dataviz/histograms-density-plots.html)

---

## 47. Seaborn II: Relationships, Categories and Facets

![A bar plot with confidence intervals, a regression plot, a line plot with a band, and a count plot](images/data-science/seaborn-four.png)

### Theory

> **In simple words:** the next questions after "how is it spread?" are "**how do groups compare?**" and "**how do two variables move together?**". Seaborn answers both by mapping columns to visual roles (`x`, `y`, `hue`, `size`, `style`) and can split any chart into a grid of small charts with `col=` and `row=` (**facets**).

**Words to know:**

- **Mapping / encoding:** linking a column to a visual property (position, colour, size, shape).
- **Long (tidy) data:** Seaborn's preferred input (Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data)): one row per observation.
- **Estimator:** the summary a categorical chart draws (`barplot` and `pointplot` use the **mean** by default).
- **Confidence interval (CI):** a range showing how uncertain an estimate is. Seaborn's default error bar is a **95% CI** of the mean (Section [56](#56-confidence-intervals-and-the-bootstrap) explains it fully); a short bar means a precise estimate.
- **Regression line:** the best-fitting straight line through a scatter (`regplot` draws it with a CI band).
- **Overplotting:** so many points that they hide each other; fix with transparency (`alpha`), smaller points, or a 2D histogram.
- **Facet grid:** a grid of small charts, one per value of a column (`col="channel"`).
- **Axes-level vs figure-level functions:** axes-level (`scatterplot`, `boxplot`, …) draw on one `ax` you pass; figure-level (`relplot`, `catplot`, `displot`, `lmplot`) create their own figure and support facets.

**Everyday picture.** A school sports-day results board: a bar per house showing the average points, with a little line showing "we're fairly sure the true average is within this range". Facets are the same board printed once per age group, side by side.

**The function families:**

| Question | Axes-level (one chart, `ax=`) | Figure-level (facets with `col=` / `row=`) |
|---|---|---|
| distributions (Section [46](#46-seaborn-i-distributions)) | `histplot`, `kdeplot`, `ecdfplot` | `displot` |
| comparing groups | `barplot`, `pointplot`, `countplot`, `boxplot`, `violinplot`, `stripplot` | `catplot` |
| two numbers | `scatterplot`, `lineplot`, `regplot` | `relplot`, `lmplot` |
| many variables (Section [48](#48-heatmaps-pair-plots-and-correlation-charts)) | `heatmap` | `pairplot`, `jointplot` |

**Mapping arguments:**

| Argument | Visual role |
|---|---|
| `data=df` | the DataFrame |
| `x=`, `y=` | columns on each axis |
| `hue=` | colour |
| `size=`, `style=` | marker size / shape (scatter, line) |
| `col=`, `row=` | facets (figure-level only) |
| `order=`, `hue_order=` | category order |
| `estimator="sum"`, `errorbar=None` / `("ci", 95)` / `"sd"` | what bars show and what the error bar means |

**Bar plots show a mean, not a total:** `sns.barplot(data=df, x="city", y="order_value")` draws the **average** order value per city. For totals, pass `estimator="sum"` or aggregate first and use plain `ax.bar`. For counts of rows, `sns.countplot`.

**`lineplot` aggregates too:** with several y-values per x, it draws the mean with a 95% CI band. Great for "average rating by delivery day".

**When to use facets:** comparing the same relationship across a few groups (2–6 panels). **When not to:** dozens of groups (use a heatmap or a sorted bar chart instead).

**Common mistakes:**

- ❌ Reading a `barplot` height as a total.
- ❌ Passing wide data. ✅ `melt` first (Section [35](#35-reshaping-pivot_table-melt-crosstab-and-explode)).
- ❌ `ax=` with figure-level functions (`relplot`, `catplot`): they make their own figure. ✅ Use axes-level functions in your own layouts.
- ❌ Assuming a regression line means causation (Section [52](#52-correlation-covariance-and-causation)).

**Used in real software:** experiment readouts (mean metric per variant with CIs), product analytics (conversion by segment), research papers, and EDA notebooks everywhere.

### Python

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns

rng = np.random.default_rng(11)
n = 400
shop = pd.DataFrame({
    "city": rng.choice(["Pune", "Mumbai", "Delhi", "Bengaluru"], n, p=[0.3, 0.3, 0.2, 0.2]),
    "channel": rng.choice(["app", "web"], n, p=[0.6, 0.4]),
    "items": rng.integers(1, 8, n),
})
shop["order_value"] = (shop["items"] * rng.uniform(150, 450, n) * np.where(shop["channel"] == "app", 1.15, 1.0)).round()
shop["delivery_days"] = (rng.gamma(2, 1.2, n) + np.where(shop["city"] == "Delhi", 1.0, 0.0)).round(1)
shop["rating"] = (5 - 0.4 * shop["delivery_days"] + rng.normal(0, 0.5, n)).clip(1, 5).round(1)

sns.set_theme(style="whitegrid")
fig, axes = plt.subplots(2, 2, figsize=(10, 7.5), layout="constrained")
sns.barplot(data=shop, x="city", y="order_value", hue="channel", ax=axes[0, 0])
axes[0, 0].set_title("barplot: MEAN order value, 95% CI")
sns.regplot(data=shop, x="delivery_days", y="rating", scatter_kws={"alpha": 0.3}, ax=axes[0, 1])
axes[0, 1].set_title("regplot: slower delivery → lower ratings")
sns.lineplot(data=shop, x="items", y="order_value", hue="channel", ax=axes[1, 0])
axes[1, 0].set_title("lineplot: mean per x, with CI band")
sns.countplot(data=shop, x="city", hue="channel", ax=axes[1, 1])
axes[1, 1].set_title("countplot: number of orders")
fig.savefig("seaborn-four.png", dpi=100)
plt.close(fig)
print(shop.groupby(["city", "channel"])["order_value"].mean().unstack().round(0))
```

**Output:**

```text
channel       app     web
city                     
Bengaluru  1392.0  1172.0
Delhi      1365.0  1340.0
Mumbai     1211.0  1197.0
Pune       1467.0  1162.0
```

The printed table holds exactly the bar heights in the top-left chart: Seaborn computed these means for you.

```python
grid = sns.relplot(data=shop, x="items", y="order_value", col="channel", hue="city",
                   height=3.2, aspect=1.1, alpha=0.7)              # one panel per channel (facets)
grid.set_titles("{col_name} orders")
grid.savefig("seaborn-facets.png", dpi=100)
plt.close(grid.figure)

g2 = sns.catplot(data=shop, x="city", y="rating", col="channel", kind="point", height=3, aspect=1.2)
plt.close(g2.figure)
print(type(grid).__name__, grid.axes.shape, g2.axes.shape)
```

**Output:**

```text
FacetGrid (1, 2) (1, 2)
```

![Two side-by-side scatter plots of items versus order value, one for app orders and one for web orders, coloured by city](images/data-science/seaborn-facets.png)

`relplot` and `catplot` return a **FacetGrid**: a figure plus an array of axes (`grid.axes`), one per panel. `kind="point"` draws each group's mean as a dot with its CI, joined by lines.

### Practice

1. Show the **total** (not mean) order value per city as bars, sorted from highest to lowest.
2. Facet a `regplot`-style chart by city: `sns.lmplot(data=shop, x="delivery_days", y="rating", col="city", col_wrap=2)`. Does the slope look similar everywhere?

<details>
<summary><b>Answer</b></summary>

```python
totals = shop.groupby("city")["order_value"].sum().sort_values(ascending=False)
fig, ax = plt.subplots(figsize=(6, 3), layout="constrained")
sns.barplot(x=totals.index, y=totals.values, ax=ax)                # already aggregated: one value per bar
plt.close(fig)
lm = sns.lmplot(data=shop, x="delivery_days", y="rating", col="city", col_wrap=2, height=2.5)
plt.close(lm.figure)
slopes = shop.groupby("city").apply(lambda d: np.polyfit(d["delivery_days"], d["rating"], 1)[0], include_groups=False)
print(totals.astype(int).to_dict(), slopes.round(2).to_dict())
```

**Output:**

```text
{'Pune': 178011, 'Mumbai': 145834, 'Delhi': 104524, 'Bengaluru': 91201} {'Bengaluru': -0.35, 'Delhi': -0.36, 'Mumbai': -0.39, 'Pune': -0.37}
```

`np.polyfit(x, y, 1)` fits a straight line and returns `[slope, intercept]`. The slopes are similar (about −0.3 to −0.4 rating points per extra day) in every city.

</details>

**Learn more:** [Seaborn: statistical relationships](https://seaborn.pydata.org/tutorial/relational.html) · [Seaborn: categorical data](https://seaborn.pydata.org/tutorial/categorical.html)

---

## 48. Heatmaps, Pair Plots and Correlation Charts

![A correlation heatmap with values in each cell, and a weekday-by-hour heatmap of orders](images/data-science/heatmaps.png)

### Theory

> **In simple words:** when you have many variables, look at **all pairs at once**. A **correlation heatmap** colours a grid of numbers so strong relationships jump out; a **pair plot** draws a scatter for every pair of columns; a **pivot heatmap** shows a 2D pattern like orders by weekday × hour.

**Words to know:**

- **Heatmap:** a grid where each cell's colour shows its value.
- **Correlation (Pearson's r):** a number from −1 to +1 measuring how strongly two numeric variables move together in a straight line: +1 perfectly together, −1 perfectly opposite, 0 no straight-line relationship (Section [52](#52-correlation-covariance-and-causation)).
- **Correlation matrix:** the table of correlations for every pair of columns; symmetric, with 1s on the diagonal.
- **Pair plot (scatter-plot matrix):** a grid with a scatter plot for every pair of variables and each variable's distribution on the diagonal.
- **Joint plot:** one scatter with the two distributions in the margins.
- **Mask:** hiding part of a heatmap (e.g. the duplicate upper triangle).
- **Annotate (`annot=True`):** write each cell's number inside it.
- **Hexbin / 2D histogram:** counts in a grid of cells, for scatters with too many points.

**Everyday picture.** A heatmap is a **seating chart coloured by noise level**: in one look you spot the loud corner. A pair plot is a **contact sheet** of photos: every pair of variables photographed together on one page.

**Reading a correlation heatmap, step by step:**

1. Check the colour scale: diverging, centred on 0, from −1 to +1.
2. Ignore the diagonal (every variable correlates 1 with itself) and one triangle (it's a mirror).
3. Look for the darkest cells: strong positive or negative relationships.
4. Treat |r| > 0.7 between two **features** as a warning of redundancy (they carry similar information).
5. Remember: correlation measures **straight-line** relationships only and says nothing about cause.

**The tools:**

| Code | Draws |
|---|---|
| `sns.heatmap(df.corr(numeric_only=True), annot=True, cmap="RdBu", vmin=-1, vmax=1, center=0)` | correlation heatmap |
| `mask=np.triu(np.ones_like(corr, dtype=bool), k=1)` | hide the upper triangle (keep the diagonal) |
| `sns.heatmap(pivot_table, annot=True, fmt="d", cmap="Blues")` | any 2D table (weekday × hour) |
| `sns.pairplot(df, hue="group", corner=True)` | scatter-plot matrix |
| `sns.jointplot(data=df, x=..., y=..., kind="hex")` | scatter + margins (hexbin for many points) |
| `sns.clustermap(corr)` | heatmap with similar rows/columns grouped together |

**When to use:** at the start of an EDA (which variables relate?), before ML (redundant features, possible leakage when a feature correlates suspiciously well with the target), and for time patterns (weekday × hour).

**Common mistakes:**

- ❌ A sequential colormap for correlations (−0.8 looks "light"). ✅ Diverging, `vmin=-1, vmax=1`.
- ❌ Pair plots of 30 columns (900 tiny panels). ✅ Pick 4–6 columns.
- ❌ Concluding "no relationship" from r ≈ 0 (a U-shape has r ≈ 0). ✅ Look at the scatter.
- ❌ Correlating ID columns or codes. ✅ `numeric_only=True` and drop IDs first.

**Used in real software:** feature selection in ML, website heatmaps of activity by time, finance (correlation between assets for diversification), biology (gene-expression clustermaps).

### Python

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns

rng = np.random.default_rng(11)
n = 400
shop = pd.DataFrame({"items": rng.integers(1, 8, n), "channel": rng.choice(["app", "web"], n, p=[0.6, 0.4])})
shop["order_value"] = (shop["items"] * rng.uniform(150, 450, n) * np.where(shop["channel"] == "app", 1.15, 1.0)).round()
shop["delivery_days"] = rng.gamma(2, 1.2, n).round(1)
shop["rating"] = (5 - 0.4 * shop["delivery_days"] + rng.normal(0, 0.5, n)).clip(1, 5).round(1)
shop["discount_pct"] = rng.uniform(0, 30, n).round()
corr = shop.corr(numeric_only=True).round(2) + 0.0     # + 0.0 turns -0.00 into 0.00
print(corr)

events = pd.DataFrame({"ts": pd.Timestamp("2025-03-03") + pd.to_timedelta(rng.integers(0, 28 * 24 * 60, 5000), unit="min")})
hours = events["ts"].dt.hour
keep = rng.random(len(events)) < np.where((hours >= 18) & (hours <= 22), 1.0, 0.35)   # evenings are busier
events = events[keep]
table = pd.crosstab(events["ts"].dt.day_name().str[:3], events["ts"].dt.hour).reindex(["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"])

sns.set_theme(style="white")
fig, axes = plt.subplots(1, 2, figsize=(13, 4.5), layout="constrained", width_ratios=[1, 1.6])
mask = np.triu(np.ones_like(corr, dtype=bool), k=1)                       # hide the mirror half (k=1 keeps the diagonal)
sns.heatmap(corr, mask=mask, annot=True, cmap="RdBu", vmin=-1, vmax=1, center=0, ax=axes[0])
axes[0].set_title("Correlations (lower triangle)")
axes[0].tick_params(axis="x", rotation=45)
sns.heatmap(table, cmap="Blues", ax=axes[1], cbar_kws={"label": "orders"})
axes[1].set(title="Orders by weekday and hour: evenings are busiest", xlabel="hour of day", ylabel="")
fig.savefig("heatmaps.png", dpi=100)
plt.close(fig)
print(table.sum().idxmax(), "is the busiest hour")
```

**Output:**

```text
               items  order_value  delivery_days  rating  discount_pct
items           1.00         0.85           0.00   -0.01         -0.01
order_value     0.85         1.00           0.01    0.00         -0.07
delivery_days   0.00         0.01           1.00   -0.81          0.05
rating         -0.01         0.00          -0.81    1.00         -0.10
discount_pct   -0.01        -0.07           0.05   -0.10          1.00
18 is the busiest hour
```

`items` and `order_value` correlate strongly (more items, bigger orders), `delivery_days` and `rating` strongly negatively, and `discount_pct` with nothing, as it was generated at random. `width_ratios` makes the second panel wider.

```python
g = sns.pairplot(shop, vars=["items", "order_value", "delivery_days", "rating"], hue="channel",
                 corner=True, plot_kws={"alpha": 0.4, "s": 15}, height=2)
g.savefig("pairplot.png", dpi=90)
plt.close(g.figure)

x = rng.uniform(-3, 3, 300)
u_shape = x ** 2 + rng.normal(0, 0.5, 300)
print("r for a U-shape:", round(float(np.corrcoef(x, u_shape)[0, 1]), 3), "(near 0, yet y depends strongly on x)")
```

**Output:**

```text
r for a U-shape: 0.092 (near 0, yet y depends strongly on x)
```

![A corner pair plot of four shop variables coloured by channel, with distributions on the diagonal](images/data-science/pairplot.png)

`corner=True` draws only the lower triangle; `vars=` picks the columns. The U-shape demo is the classic warning: correlation only measures **straight-line** relationships.

### Practice

1. Which pair of shop variables has the strongest negative correlation, and what is r? Find it from `corr` with code, not by eye.
2. Make a heatmap of the **average rating** for each (`items`, `channel`) combination.

<details>
<summary><b>Answer</b></summary>

```python
pairs = corr.where(~np.eye(len(corr), dtype=bool)).stack()        # drop the diagonal, list every pair
print(pairs.idxmin(), pairs.min())
avg = shop.pivot_table(index="items", columns="channel", values="rating", aggfunc="mean").round(2)
fig, ax = plt.subplots(figsize=(4, 4), layout="constrained")
sns.heatmap(avg, annot=True, cmap="viridis", ax=ax)
plt.close(fig)
print(avg.head(3))
```

**Output:**

```text
('delivery_days', 'rating') -0.81
channel   app   web
items              
1        4.15  4.15
2        3.97  4.12
3        3.95  3.99
```

</details>

**Learn more:** [Seaborn: heatmap](https://seaborn.pydata.org/generated/seaborn.heatmap.html) · [Seaborn: pairplot](https://seaborn.pydata.org/generated/seaborn.pairplot.html)

---

## 49. Interactive Charts with Plotly

![A Plotly chart of monthly revenue per city, exported as a static image (the HTML version supports hover, zoom and toggling cities)](images/data-science/plotly-lines.png)

### Theory

> **In simple words:** static charts are pictures; **interactive** charts let the reader hover to see exact values, zoom into a period, and click a legend entry to hide a series. **Plotly Express** makes them in one line from a DataFrame, and saves them as a standalone HTML file anyone can open in a browser.

**Words to know:**

- **Interactive chart:** a chart that responds to the mouse: hover tooltips, zoom, pan, toggling series.
- **Plotly:** a charting library that draws in the web browser (JavaScript underneath). **Plotly Express** (`px`) is its quick, DataFrame-first interface.
- **Tooltip (hover label):** the box that appears when you point at a mark.
- **HTML export:** saving a chart as a web page that works offline (`fig.write_html`).
- **Static export:** saving a PNG/SVG of the current view (`fig.write_image`, uses the `kaleido` package).
- **Animation frame:** a column whose values become the frames of an animation (`animation_frame="year"`).
- **Dashboard / data app:** an interactive web page with charts and controls (filters, dropdowns): **Streamlit**, **Dash**, **Gradio**, **Panel**.
- **BI tool (business intelligence):** point-and-click dashboard software used across companies: Power BI, Tableau, Looker, Metabase, Apache Superset.
- **Lakh / crore:** Indian number words: 1 lakh = 100,000; 1 crore = 10,000,000 (100 lakh).

**Everyday picture.** A static chart is a **printed map**; an interactive chart is **Google Maps**: same information, but you can zoom into your street and tap a pin for details.

**Plotly Express in one table** (same mapping idea as Seaborn):

| Chart | Code |
|---|---|
| line | `px.line(df, x="month", y="revenue", color="city", markers=True)` |
| scatter | `px.scatter(df, x="price", y="units", color="category", size="stock", hover_data=["name"])` |
| bar | `px.bar(df, x="city", y="revenue", color="channel", barmode="group")` |
| histogram / box | `px.histogram(df, x="value", nbins=30)`, `px.box(df, x="city", y="value")` |
| facets | `facet_col="channel"` on any of the above |
| maps | `px.choropleth(...)`, `px.scatter_map(...)` |
| animation | `animation_frame="year"` |

**Customising and sharing:** `fig.update_layout(title=..., yaxis_title=..., template="plotly_white")`, `fig.update_traces(...)`; `fig.write_html("chart.html")` for sharing; `fig.show()` in notebooks.

**Static vs interactive vs dashboard:**

| Use | Pick |
|---|---|
| report, paper, slide, email | static (Matplotlib/Seaborn, or Plotly's `write_image`) |
| exploring a dense dataset yourself; sharing a chart people will poke at | interactive HTML (Plotly) |
| a live view with filters that updates as data changes | a data app (Streamlit/Dash) or a BI tool |

**When not to use interactivity:** when there's one message to deliver. Hover-to-discover hides the point; annotate a static chart instead (Section [45](#45-styling-annotation-and-saving-charts)).

**Common mistakes:**

- ❌ Putting the insight behind a hover tooltip. ✅ Put it in the title.
- ❌ Plotting a million points in the browser (slow). ✅ Aggregate first, or use `render_mode="webgl"` / Datashader.
- ❌ Emailing a notebook full of interactive charts. ✅ `write_html` or a static image.

**Used in real software:** internal analytics apps built with Streamlit or Dash; product dashboards; data journalism; model monitoring pages.

### Python

```python
import numpy as np
import pandas as pd
import plotly.express as px

rng = np.random.default_rng(4)
months = pd.period_range("2025-01", "2025-12", freq="M").to_timestamp()
rows = []
for k, city in enumerate(["Pune", "Mumbai", "Delhi", "Bengaluru"]):
    base = 50 + 12 * k
    rows += [{"month": m, "city": city, "revenue_lakh": round(base + 2.5 * i + rng.normal(0, 4), 1)} for i, m in enumerate(months)]
df = pd.DataFrame(rows)

fig = px.line(df, x="month", y="revenue_lakh", color="city", markers=True,
              title="Monthly revenue by city (₹ lakh): all four cities growing",
              labels={"revenue_lakh": "revenue (₹ lakh)", "month": ""}, template="plotly_white")
fig.update_layout(legend_title_text="")
import os, tempfile
fig.write_html(os.path.join(tempfile.mkdtemp(), "revenue.html"), include_plotlyjs="cdn")   # an interactive web page
fig.write_image("plotly-lines.png", width=900, height=420)       # a static snapshot
print(len(fig.data), "lines;", df.groupby("city")["revenue_lakh"].last().to_dict())
```

**Output:**

```text
4 lines; {'Bengaluru': 113.0, 'Delhi': 105.5, 'Mumbai': 89.1, 'Pune': 83.8}
```

`len(fig.data)` counts the **traces** (Plotly's word for series): one per city. A **lakh** is 100,000 (Indian numbering). `include_plotlyjs="cdn"` keeps the HTML file small by loading Plotly's JavaScript from the internet; `include_plotlyjs=True` embeds it so the file works offline (about 4 MB).

```python
scatter = px.scatter(df, x="month", y="revenue_lakh", color="city", facet_col="city", facet_col_wrap=2,
                     trendline=None, hover_data={"revenue_lakh": ":.1f"}, height=450)
scatter.update_yaxes(matches=None)                               # let each panel have its own y-range
print(type(scatter).__name__, len(scatter.data), "traces in", len({t.xaxis for t in scatter.data}), "panels")
```

**Output:**

```text
Figure 4 traces in 4 panels
```

### Practice

1. Make a Plotly bar chart of total yearly revenue per city, sorted from highest to lowest, with the value shown on each bar (`text_auto=True`).
2. When would you send a Plotly HTML file instead of a PNG?

<details>
<summary><b>Answer</b></summary>

```python
totals = df.groupby("city", as_index=False)["revenue_lakh"].sum().sort_values("revenue_lakh", ascending=False)
bar = px.bar(totals, x="city", y="revenue_lakh", text_auto=".0f", title="Yearly revenue (₹ lakh)")
print(totals.round(1).to_dict("records"))
```

**Output:**

```text
[{'city': 'Bengaluru', 'revenue_lakh': 1187.1}, {'city': 'Delhi', 'revenue_lakh': 1044.7}, {'city': 'Mumbai', 'revenue_lakh': 903.0}, {'city': 'Pune', 'revenue_lakh': 764.3}]
```

2. When readers need to explore (look up exact values for any month, zoom, compare two cities by hiding the others), and they'll open it in a browser. For a report or a slide with one message, a static PNG with a clear title is better.

</details>

**Learn more:** [Plotly Express](https://plotly.com/python/plotly-express/) · [Streamlit: get started](https://docs.streamlit.io/get-started)

---

## 50. Choosing the Right Chart (and Not Misleading)

![Bad versus better: a truncated bar chart against a zero-based one, and a seven-slice pie against a sorted, labelled bar chart](images/data-science/good-vs-bad-charts.png)

### Theory

> **In simple words:** start from the **question**, not the chart type. "How did sales change?" needs a line. "Which city sells most?" needs sorted bars. "Are price and sales related?" needs a scatter. A good chart makes **one point** obvious, and an honest chart doesn't exaggerate it.

**Words to know:**

- **Data-ink:** the ink (pixels) that shows data, as opposed to decoration. Maximise it (Edward Tufte's idea).
- **Chartjunk:** decoration that adds nothing: 3D effects, shadows, heavy gridlines, clip art.
- **Truncated axis:** an axis that doesn't start at zero. Fine for lines (which show change), misleading for bars (whose **length** is the value).
- **Pre-attentive attributes:** properties the eye notices before you think: colour, size, position. Use them for the message.
- **Direct labelling:** writing labels next to lines or bars instead of in a legend.
- **Cherry-picking:** choosing a date range or subset that supports a story while hiding the rest.
- **Choropleth:** a map with regions coloured by value.

**Everyday picture.** A chart is a **sentence**: it should say one thing clearly. "Revenue by city" is a label, not a sentence; "Mumbai overtook Pune in May" is a sentence, and it tells you which chart to draw.

**Question → chart:**

| Your question is about… | Use | Avoid |
|---|---|---|
| change **over time** | line chart (bars for a few periods) | pie charts, unordered bars |
| **comparing** categories | bar chart, **sorted**, horizontal if labels are long | pie with many slices, 3D bars |
| **parts of a whole** | stacked bar, or a pie/donut with **2–4** slices | pie with 7+ slices |
| **distribution** of one number | histogram, box plot, violin, ECDF (Section [46](#46-seaborn-i-distributions)) | a bar of the mean alone (hides the spread) |
| **relationship** between two numbers | scatter (+ trend line; transparency for many points) | line chart of unordered points |
| **many variables** | heatmap, pair plot, small multiples | one overloaded chart |
| **geography** | choropleth map | a table of 30 regions |
| a single key number | the number, big, with context ("₹5.8L, +12% vs last month") | a chart |

**Rules for honest, clear charts:**

1. **Bars start at zero.** Bar length is the value; cutting the axis at 95 makes a 2% difference look like 5×. (Line charts may zoom in.)
2. **One message per chart**, stated in the title.
3. **Sort** categories by value unless they have a natural order (months, sizes).
4. **Label directly** where you can.
5. **Colour for meaning:** grey for context, one strong colour for the highlight; colour-blind-safe palettes.
6. **Remove clutter:** 3D, heavy gridlines, borders, shadows, needless decimals.
7. **Show uncertainty** when it matters: error bars, bands, the raw points.
8. **Same scale for comparisons:** shared y-axes for side-by-side charts.
9. **Show the full context:** a sensible date range, the baseline, the denominator ("12 complaints" means something different out of 100 or 100,000 orders).

**How charts mislead (spot them in other people's work):** truncated bar axes, dual y-axes with tuned scales, cherry-picked date ranges, area or 3D effects exaggerating differences, cumulative charts that always go up, percentages without base sizes, and maps where big empty regions dominate.

**Common mistakes:**

- ❌ Choosing a chart because it looks impressive (3D pies, radar charts, word clouds).
- ❌ Default titles like "Figure 1" or the column name.
- ❌ Ten colours for ten categories. ✅ Highlight one or two; grey the rest.

**Used in real software:** every dashboard and report; the BBC, the FT and The Economist publish their chart style guides, which follow these same rules.

### Python

```python
import matplotlib.pyplot as plt

teams = ["Team A", "Team B"]
scores = [96.1, 98.3]
shares = {"Pune": 29, "Mumbai": 27, "Delhi": 14, "Bengaluru": 12, "Chennai": 8, "Kolkata": 6, "Other": 4}

fig, axes = plt.subplots(2, 2, figsize=(9, 7), layout="constrained")
axes[0, 0].bar(teams, scores, color=["gray", "tab:red"])
axes[0, 0].set_ylim(95.5, 98.5)
axes[0, 0].set_title("BAD: axis starts at 95.5,\nso B's bar is 5× taller")
axes[0, 1].bar(teams, scores, color=["gray", "tab:red"])
axes[0, 1].set_ylim(0, 100)
axes[0, 1].set_title("BETTER: axis starts at 0,\nB is about 2% better")

axes[1, 0].pie(shares.values(), labels=shares.keys(), startangle=90)
axes[1, 0].set_title("BAD: seven slices are hard to compare")
names = sorted(shares, key=shares.get)
colors = ["tab:blue" if c == "Pune" else "lightgray" for c in names]
axes[1, 1].barh(names, [shares[c] for c in names], color=colors)
for i, c in enumerate(names):
    axes[1, 1].text(shares[c] + 0.5, i, f"{shares[c]}%", va="center")
axes[1, 1].spines[["top", "right"]].set_visible(False)
axes[1, 1].set_title("BETTER: sorted, labelled bars;\nPune has the largest share")
fig.savefig("good-vs-bad-charts.png", dpi=100)
plt.close(fig)
visible_ratio = (scores[1] - 95.5) / (scores[0] - 95.5)
print(f"real difference: {100 * (scores[1] - scores[0]) / scores[0]:.1f}% · bar heights in the bad chart differ {visible_ratio:.1f}×")
```

**Output:**

```text
real difference: 2.3% · bar heights in the bad chart differ 4.7×
```

### Practice

1. Which chart for each question? (a) How are delivery times spread out? (b) Did weekly active users grow this year? (c) Do customers who order more often rate us higher? (d) What share of revenue comes from app vs web?
2. A slide shows "complaints rose from 40 to 80" as two bars starting at 35. List two things wrong and how you'd redraw it.

<details>
<summary><b>Answer</b></summary>

1. (a) Histogram or box plot (by city if comparing). (b) Line chart over weeks. (c) Scatter of order frequency vs rating with a trend line. (d) One stacked bar or a two-slice donut; or just state the two percentages.
2. The truncated axis makes 80 look 9× bigger than 40 (45 vs 5 above the baseline) when it's 2×; and raw counts hide the denominator: if orders also doubled, the complaint **rate** didn't change. Redraw as bars from zero of complaints **per 1,000 orders**, or a line of the rate over time.

</details>

**Learn more:** [Claus Wilke: Fundamentals of Data Visualization (free book)](https://clauswilke.com/dataviz/) · [From Data to Viz: chart chooser](https://www.data-to-viz.com/) · [BBC Visual and Data Journalism cookbook](https://bbc.github.io/rcookbook/)

---

### ✅ Part 7 checkpoint

Without looking, can you:

- [ ] Create a figure with `plt.subplots`, draw line, bar, scatter and histogram charts, and label and save them?
- [ ] Explain figure vs axes vs axis, build a grid or mosaic layout, and make small multiples with shared scales?
- [ ] Annotate a point, shade a period, format axis labels as currency or percentages, and pick sequential vs diverging colormaps?
- [ ] Compare distributions across groups with histograms (density), box plots, violins and ECDFs, and explain why a box plot can hide two peaks?
- [ ] Say what a Seaborn `barplot` shows by default and how to show totals; facet a chart with `col=`?
- [ ] Draw and read a correlation heatmap and a pair plot, and say why r ≈ 0 doesn't mean "unrelated"?
- [ ] Make an interactive Plotly chart and save it as HTML and PNG?
- [ ] Choose the right chart for a question, and spot five ways charts mislead?

Charts show patterns; **statistics** tells you whether a pattern is real or just luck. That's Part 8.

---

# Part 8 — Advanced: Statistics

> **Goal:** Summarise data honestly, reason with probability, understand why samples vary, put error bars on estimates, test whether a difference is real, run an A/B test from design to decision, and read a regression table.  
> **You need:** Parts 2–7. No maths beyond school algebra: every formula is explained in words, traced by hand, and checked with a simulation.

Statistics answers one question over and over: **"is this pattern real, or could it be luck?"** Every section builds one piece of the answer.

---

## 51. Describing Data: Centre, Spread and Shape

![Right-skewed data: the mode is below the median, which is below the mean; the box plot summarises the same data](images/data-science/08-describing-data.svg)

### Theory

> **In simple words:** **descriptive statistics** summarise a column of numbers in a few values: where the **middle** is (mean, median, mode), how **spread out** the values are (standard deviation, IQR), and what **shape** the distribution has (symmetric or skewed, one peak or two). Choosing the right summary is the difference between "the typical customer" and "a number that describes nobody".

**Words to know:**

- **Descriptive statistics:** numbers that summarise data you have. (**Inferential statistics**, Sections [55](#55-sampling-the-central-limit-theorem-and-standard-error)–[59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence), uses a sample to say something about a bigger population.)
- **Central tendency:** where the middle of the data is.
  - **Mean (average, x̄):** add everything, divide by the count.
  - **Median:** the middle value after sorting (the average of the two middle values when the count is even).
  - **Mode:** the most frequent value.
- **Dispersion (spread):** how far values are from the middle.
  - **Range:** max − min.
  - **Variance:** the average squared distance from the mean.
  - **Standard deviation (std, s or σ):** the square root of the variance, in the **same units** as the data. Roughly "how far a typical value is from the mean".
  - **IQR (interquartile range):** Q3 − Q1, the width of the middle 50%.
  - **Coefficient of variation (CV):** std ÷ mean, spread relative to size (compare the spread of elephants' and mice's weights).
- **Percentile / quantile:** the value below which a given share of data falls (Section [12](#12-aggregations-and-the-axis-argument)).
- **Skewness:** lopsidedness. **Right (positive) skew:** a long tail of big values (incomes, prices, waiting times). **Left (negative) skew:** a long tail of small values (exam scores on an easy test).
- **Kurtosis:** how heavy the tails are: how often extreme values appear compared with a bell curve.
- **Robust statistic:** one that extreme values barely move (median, IQR) as opposed to one they distort (mean, std).
- **Population vs sample; `ddof`:** dividing the variance by `n − 1` instead of `n` (**Bessel's correction**) corrects for using the sample's own mean, which sits closer to the sample's values than the true mean does. pandas uses `n − 1` by default (`ddof=1`); NumPy uses `n` (`ddof=0`).

**Everyday picture.** Ten people in a café earn ₹30k–₹50k a month. A billionaire walks in. The **mean** income jumps to crores; the **median** barely moves. The median still describes "a typical person in the café"; the mean now describes nobody.

**Traced by hand** for salaries (₹ thousands) `[30, 35, 40, 45, 1000]`:

| Statistic | Working | Value |
|---|---|---|
| mean | (30 + 35 + 40 + 45 + 1000) / 5 | **230** |
| median | middle of the sorted list | **40** |
| variance (sample) | squared distances from 230: 40000, 38025, 36100, 34225, 592900; sum 741250; ÷ (5 − 1) | 185312.5 |
| std | √185312.5 | **430.5** |
| Q1, Q3 (pandas' default method) | 25th and 75th percentiles | 35, 45 |
| IQR | 45 − 35 | **10** |

The std (430) is bigger than most of the data, because one value dominates it; the IQR (10) describes the four ordinary salaries. **When mean ≫ median, the data is right-skewed.**

**Which summary to report:**

| Data shape | Centre | Spread |
|---|---|---|
| roughly symmetric, no extreme outliers (heights, test scores) | mean | standard deviation |
| skewed or with outliers (income, price, time, counts) | median | IQR or percentiles (p10/p90) |
| categories | mode (most common) | number of categories, share of the top one |
| anything important | **show the distribution** (Section [46](#46-seaborn-i-distributions)) | |

**Reading a standard deviation:** for bell-shaped data, about **68%** of values lie within 1 std of the mean and **95%** within 2 (Section [54](#54-probability-distributions-normal-binomial-poisson-and-more)). "Mean 50, std 10" → most values between 40 and 60, nearly all between 30 and 70. For skewed data this rule doesn't hold: use percentiles.

**Shape in numbers:** skewness near 0 means symmetric; above about +1 strongly right-skewed. A **log transform** (`np.log1p`) often makes right-skewed data roughly symmetric, which helps charts and some models.

**When averages lie:** averaging percentages or ratios across groups of different sizes (weight by size instead); averaging skewed values; the **mean of means** (Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine)).

**Common mistakes:**

- ❌ Reporting the mean of salaries, house prices or delivery times. ✅ Median (plus percentiles).
- ❌ "Mean ± 2 std" ranges for skewed data (they can go negative for prices). ✅ Percentiles.
- ❌ Comparing pandas' `std()` with NumPy's `np.std()` and finding a mismatch. ✅ `ddof`.
- ❌ Summarising without looking: two very different datasets can share the same mean and std (Section [52](#52-correlation-covariance-and-causation)'s Anscombe's quartet).

**Used in real software:** dashboards (median delivery time, p95 latency), salary reports (medians and percentile bands), quality control (mean and std of a manufacturing measurement), `df.describe()` in every notebook.

### Python

```python
import numpy as np
import pandas as pd
from scipy import stats

salaries = pd.Series([30, 35, 40, 45, 1000], name="salary_k")
print(f"mean {salaries.mean():.1f}  median {salaries.median():.1f}  std {salaries.std():.1f}  "
      f"IQR {salaries.quantile(0.75) - salaries.quantile(0.25):.1f}")
print("without the outlier:", salaries[salaries < 500].agg(["mean", "median", "std"]).round(1).to_dict())
print("numpy std (ddof=0):", round(float(np.std(salaries)), 1), " pandas std (ddof=1):", round(salaries.std(), 1))
```

**Output:**

```text
mean 230.0  median 40.0  std 430.5  IQR 10.0
without the outlier: {'mean': 37.5, 'median': 37.5, 'std': 6.5}
numpy std (ddof=0): 385.0  pandas std (ddof=1): 430.5
```

```python
rng = np.random.default_rng(0)
orders = pd.Series(rng.lognormal(mean=6.5, sigma=0.7, size=5_000).round(), name="order_value")   # right-skewed
heights = pd.Series(rng.normal(165, 8, 5_000).round(1), name="height_cm")                          # symmetric

def summary(s):
    q = s.quantile([0.1, 0.25, 0.5, 0.75, 0.9])
    return pd.Series({"mean": s.mean(), "median": q[0.5], "std": s.std(), "IQR": q[0.75] - q[0.25],
                      "p10": q[0.1], "p90": q[0.9], "skew": s.skew(), "CV": s.std() / s.mean()}).round(2)

print(pd.DataFrame({"orders": summary(orders), "heights": summary(heights), "log(orders)": summary(np.log(orders))}))
within_1sd = ((heights - heights.mean()).abs() <= heights.std()).mean()
print(f"heights within 1 std: {within_1sd:.1%} | orders within mean ± 2 std goes as low as {orders.mean() - 2 * orders.std():.0f}")
print("mode of a category:", pd.Series(["M", "L", "M", "S", "M", "L"]).mode().tolist())
```

**Output:**

```text
         orders  heights  log(orders)
mean     844.90   165.14         6.50
median   652.50   165.20         6.48
std      652.06     8.01         0.70
IQR      657.25    10.80         0.95
p10      276.00   154.90         5.62
p90     1645.10   175.10         7.41
skew       2.23    -0.09         0.02
CV         0.77     0.05         0.11
heights within 1 std: 69.0% | orders within mean ± 2 std goes as low as -459
mode of a category: ['M']
```

The order values are strongly right-skewed (skew ≈ 2, mean well above the median); their log is nearly symmetric (skew ≈ 0). Heights follow the 68% rule. For the skewed orders, "mean − 2 std" is **negative**: a range that includes impossible values is a sign you picked the wrong summary.

### Practice

1. For `[2, 3, 3, 4, 5, 6, 30]`, compute by hand the mean, median and mode; then check with pandas. Which would you report as "typical", and why?
2. Two delivery services both average 3 days; service A has std 0.5 days, B has std 2.5 days. Which would you choose, and what extra number would you ask for?

<details>
<summary><b>Answer</b></summary>

```python
v = pd.Series([2, 3, 3, 4, 5, 6, 30])
print(round(v.mean(), 2), v.median(), v.mode().tolist(), round(v.skew(), 2))
```

**Output:**

```text
7.57 4.0 [3] 2.55
```

1. Mean 53/7 ≈ 7.57, median 4, mode 3. The median: one value (30) drags the mean above six of the seven numbers.
2. A: same average but far more predictable. Ask for a high percentile, e.g. "what share arrive within 4 days?" or the p90/p95 delivery time, because that's what customers notice.

</details>

| # | Problem | Difficulty |
|---|---|---|
| 1 | [Deep-ML 78. Descriptive Statistics Calculator](https://www.deep-ml.com/problems/78) | 🟢 Easy |
| 2 | [Deep-ML 293. Calculate P50/P95/P99 Latency Percentiles](https://www.deep-ml.com/problems/293) | 🟢 Easy |
| 3 | [LeetCode 1251. Average Selling Price](https://leetcode.com/problems/average-selling-price/) (a weighted average) | 🟢 Easy |

**Learn more:** [OpenIntro Statistics (free textbook), chapter 2](https://www.openintro.org/book/os/) · [Seeing Theory: basic probability and statistics (interactive)](https://seeing-theory.brown.edu/)

---

## 52. Correlation, Covariance and Causation

![Anscombe's quartet: four datasets with the same means, variances and correlation (0.82) that look completely different](images/data-science/anscombe.png)

### Theory

> **In simple words:** **correlation** measures how strongly two numbers move together in a straight line, from −1 to +1. It's useful and easily misread: it says nothing about curves, it can be created by a third hidden factor, and it never, by itself, tells you that one thing **causes** the other.

**Words to know:**

- **Covariance:** the average of (x − mean of x) × (y − mean of y). Positive when x and y tend to be above their means together; its size depends on the units, so it's hard to read directly.
- **Pearson correlation (r):** covariance divided by both standard deviations, so it's unit-free and always between −1 and +1. Measures **linear** (straight-line) association.
- **Spearman correlation (ρ, "rho"):** Pearson's r computed on the **ranks** of the values. Measures **monotonic** association (always going up, or always down, even if curved) and resists outliers.
- **r² (coefficient of determination):** for a straight-line fit, the share of y's variance explained by x. r = 0.5 → r² = 0.25 (25%).
- **Causation:** changing x actually **changes** y.
- **Confounder (lurking variable):** a third factor that drives both x and y, creating a correlation between them (summer drives both ice-cream sales and drownings).
- **Spurious correlation:** a correlation with no meaningful connection (two unrelated trends that both rise over time).
- **Reverse causation:** y causes x, not the other way round.
- **Simpson's paradox:** a trend that appears in every group **reverses** when the groups are combined, because the groups differ in size or mix.
- **Randomised controlled experiment:** the gold standard for causation: assign the treatment **at random**, so confounders are balanced between groups (Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls)).

**Everyday picture.** Towns with more fire engines at a fire have more damage. Fire engines don't cause damage; **big fires** cause both more engines and more damage. That's a confounder. Banning fire engines would not reduce damage.

**Pearson's r, traced by hand** for x = `[1, 2, 3, 4, 5]`, y = `[2, 4, 5, 4, 5]` (means 3 and 4):

| x − 3 | y − 4 | product | (x − 3)² | (y − 4)² |
|---|---|---|---|---|
| −2 | −2 | 4 | 4 | 4 |
| −1 | 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 | 1 |
| 1 | 0 | 0 | 1 | 0 |
| 2 | 1 | 2 | 4 | 1 |
| | **sum** | **6** | **10** | **6** |

r = 6 / √(10 × 6) = 6 / 7.75 = **0.77**: a fairly strong positive linear relationship.

**How strong is "strong"?** Rough guide for |r|: below 0.1 negligible, 0.1–0.3 weak, 0.3–0.5 moderate, above 0.5 strong. Context matters: in social science 0.3 can be important; in physics 0.9 can be disappointing.

**Pearson vs Spearman:**

| Data | Pearson r | Spearman ρ |
|---|---|---|
| straight-line relationship | ✅ | ✅ |
| curved but always increasing (y = x³) | understates it | ✅ near 1 |
| one extreme outlier | can be wrecked | ✅ robust |
| U-shape | ≈ 0 | ≈ 0 (neither catches it: **look at the scatter**) |

**From correlation to causation, the questions to ask:**

1. Could a **confounder** drive both? (Season, income, age, company size…)
2. Could it be **reverse causation**? (Do happy employees get promoted, or do promotions make employees happy?)
3. Is it **selection**? (Only successful startups get studied.)
4. Could it be **chance**? (Test enough pairs of variables and some will correlate.)
5. Can you run an **experiment**? If you randomly assign x, a remaining difference in y is causal.

**Simpson's paradox in one table:** a treatment works better in both small and large kidney stones, but looks worse overall, because doctors gave it mostly to the hard (large-stone) cases. Always check whether a combined comparison mixes groups of different difficulty.

**When to use correlation:** a first screen of which variables move together (Section [48](#48-heatmaps-pair-plots-and-correlation-charts)), checking for redundant features before ML, describing a relationship you've already looked at. **When not to:** as evidence of cause, or without a scatter plot.

**Common mistakes:**

- ❌ "r = 0, so x and y are unrelated" (U-shapes, cycles).
- ❌ Computing correlation on time series that both trend upwards (they'll correlate strongly regardless). ✅ Correlate the **changes** (`diff()`), not the levels.
- ❌ Reading r as a slope ("r = 0.5 means y rises half as fast"). It's strength, not steepness.
- ❌ Claiming causation from observational data. ✅ "is associated with".

**Used in real software:** feature screening in ML, portfolio diversification (assets with low correlation), product analytics (which behaviours go with retention: then test causally with an experiment), epidemiology.

### Python

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from scipy import stats

x, y = np.array([1, 2, 3, 4, 5]), np.array([2, 4, 5, 4, 5])
cov = ((x - x.mean()) * (y - y.mean())).sum() / (len(x) - 1)
r = cov / (x.std(ddof=1) * y.std(ddof=1))
print(f"covariance {cov:.2f}  r by hand {r:.3f}  numpy {np.corrcoef(x, y)[0, 1]:.3f}  scipy {stats.pearsonr(x, y)[0]:.3f}")

z = np.arange(1, 21)
cubic = z ** 3
with_outlier = np.append(z, 21)
y_out = np.append(z * 2.0, -100)                            # one wild point
print("y = x³:      pearson", round(stats.pearsonr(z, cubic)[0], 3), " spearman", round(stats.spearmanr(z, cubic)[0], 3))
print("1 outlier:   pearson", round(stats.pearsonr(with_outlier, y_out)[0], 3), " spearman", round(stats.spearmanr(with_outlier, y_out)[0], 3))
```

**Output:**

```text
covariance 1.50  r by hand 0.775  numpy 0.775  scipy 0.775
y = x³:      pearson 0.922  spearman 1.0
1 outlier:   pearson 0.034  spearman 0.727
```

`np.corrcoef` returns a 2 × 2 matrix (each variable with itself and with the other), so `[0, 1]` picks the cross-correlation.

```python
anscombe = {   # Anscombe's quartet (1973): four datasets built to share the same summary statistics
    "I":   ([10, 8, 13, 9, 11, 14, 6, 4, 12, 7, 5], [8.04, 6.95, 7.58, 8.81, 8.33, 9.96, 7.24, 4.26, 10.84, 4.82, 5.68]),
    "II":  ([10, 8, 13, 9, 11, 14, 6, 4, 12, 7, 5], [9.14, 8.14, 8.74, 8.77, 9.26, 8.10, 6.13, 3.10, 9.13, 7.26, 4.74]),
    "III": ([10, 8, 13, 9, 11, 14, 6, 4, 12, 7, 5], [7.46, 6.77, 12.74, 7.11, 7.81, 8.84, 6.08, 5.39, 8.15, 6.42, 5.73]),
    "IV":  ([8, 8, 8, 8, 8, 8, 8, 19, 8, 8, 8], [6.58, 5.76, 7.71, 8.84, 8.47, 7.04, 5.25, 12.50, 5.56, 7.91, 6.89]),
}
fig, axes = plt.subplots(1, 4, figsize=(12, 3), sharex=True, sharey=True, layout="constrained")
for ax, (name, (ax_x, ax_y)) in zip(axes, anscombe.items()):
    ax_x, ax_y = np.array(ax_x), np.array(ax_y)
    slope, intercept = np.polyfit(ax_x, ax_y, 1)
    ax.scatter(ax_x, ax_y, color="tab:blue")
    ax.plot([3, 20], [intercept + slope * 3, intercept + slope * 20], color="tab:red", lw=1.5)
    ax.set_title(f"{name}: r = {np.corrcoef(ax_x, ax_y)[0, 1]:.2f}")
    print(f"{name:>3}: mean x {ax_x.mean():.1f}, mean y {ax_y.mean():.2f}, var y {ax_y.var(ddof=1):.2f}, r {np.corrcoef(ax_x, ax_y)[0, 1]:.3f}, line y = {intercept:.2f} + {slope:.2f}x")
fig.suptitle("Same statistics, different stories: always plot your data")
fig.savefig("anscombe.png", dpi=100)
plt.close(fig)
```

**Output:**

```text
  I: mean x 9.0, mean y 7.50, var y 4.13, r 0.816, line y = 3.00 + 0.50x
 II: mean x 9.0, mean y 7.50, var y 4.13, r 0.816, line y = 3.00 + 0.50x
III: mean x 9.0, mean y 7.50, var y 4.12, r 0.816, line y = 3.00 + 0.50x
 IV: mean x 9.0, mean y 7.50, var y 4.12, r 0.817, line y = 3.00 + 0.50x
```

```python
rng = np.random.default_rng(1)
temp = rng.uniform(15, 40, 365)                                       # the confounder: daily temperature
ice_cream = 50 + 8 * temp + rng.normal(0, 25, 365)
swims = 2 + 0.3 * temp + rng.normal(0, 2, 365)
print("ice cream ~ swimming:", round(np.corrcoef(ice_cream, swims)[0, 1], 2))
resid_ice = ice_cream - np.polyval(np.polyfit(temp, ice_cream, 1), temp)    # remove temperature's effect
resid_swim = swims - np.polyval(np.polyfit(temp, swims, 1), temp)
print("after removing temperature:", round(np.corrcoef(resid_ice, resid_swim)[0, 1], 2))

stones = pd.DataFrame({"treatment": ["A", "A", "B", "B"], "stone": ["small", "large", "small", "large"],
                       "success": [81, 192, 234, 55], "patients": [87, 263, 270, 80]})   # the classic kidney-stone study
by_group = stones.assign(rate=lambda d: (d["success"] / d["patients"]).round(3)).pivot(index="stone", columns="treatment", values="rate")
overall = stones.groupby("treatment")[["success", "patients"]].sum().eval("success / patients").round(3)
print(by_group, "overall:", overall.to_dict(), sep="\n")
```

**Output:**

```text
ice cream ~ swimming: 0.67
after removing temperature: 0.03
treatment      A      B
stone                  
large      0.730  0.688
small      0.931  0.867
overall:
{'A': 0.78, 'B': 0.826}
```

The ice-cream/swimming correlation is strong, but it disappears once temperature's effect is removed: **partial correlation** in action. In the kidney-stone data, treatment A wins in **both** groups but loses overall, because A was given mostly to the harder, large-stone cases: Simpson's paradox. (`np.polyfit(x, y, 1)` fits a straight line; `np.polyval` evaluates it; `DataFrame.eval` computes an expression from column names.)

### Practice

1. Two time series both rise over 10 years: `a = np.arange(10) + noise_a`, `b = 2 * np.arange(10) + noise_b` with independent noise. Show that the levels correlate strongly but the year-to-year **changes** don't.
2. Studies find people who drink more coffee live longer. Name a possible confounder, a possible reverse-causation story, and the study design that would settle it.

<details>
<summary><b>Answer</b></summary>

```python
rng2 = np.random.default_rng(7)
a = np.arange(10) + rng2.normal(0, 1, 10)
b = 2 * np.arange(10) + rng2.normal(0, 2, 10)
print(round(np.corrcoef(a, b)[0, 1], 2), round(np.corrcoef(np.diff(a), np.diff(b))[0, 1], 2))
```

**Output:**

```text
0.95 0.26
```

2. Confounder: wealth or general health (healthier, richer people may drink more coffee and live longer). Reverse causation: people who are already ill may stop drinking coffee. Settle it: a randomised experiment (assign coffee at random), or at least careful adjustment for confounders in a large study.

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [10. Calculate Covariance Matrix](https://www.deep-ml.com/problems/10) | 🟢 Easy |
| 2 | [95. Calculate the Phi Coefficient](https://www.deep-ml.com/problems/95) | 🟢 Easy |
| 3 | [37. Calculate Correlation Matrix](https://www.deep-ml.com/problems/37) | 🟡 Medium |

**Learn more:** [Spurious correlations (Tyler Vigen)](https://www.tylervigen.com/spurious-correlations) · [Seeing Theory: regression analysis](https://seeing-theory.brown.edu/regression-analysis/index.html)

---

## 53. Probability Basics: Events, Conditional Probability and Bayes' Rule

![Bayes' rule as a tree of 10,000 people: only about 16% of positive tests come from people who have the disease](images/data-science/53-bayes-tree.svg)

### Theory

> **In simple words:** **probability** is a number from 0 (impossible) to 1 (certain) describing how likely something is. **Conditional probability** is the chance of something **given** you already know something else. **Bayes' rule** turns "how likely is the evidence if the claim is true?" into "how likely is the claim given the evidence?", and it's the reason a positive test for a rare disease usually means you **don't** have it.

**Words to know:**

- **Experiment / trial:** something with an uncertain outcome (rolling a die, a visitor arriving).
- **Outcome:** one possible result. **Sample space:** all possible outcomes.
- **Event:** a set of outcomes we care about ("the roll is even").
- **P(A):** the probability of event A.
- **Complement (not A):** P(not A) = 1 − P(A).
- **Union (A or B):** P(A or B) = P(A) + P(B) − P(A and B) (subtract the overlap once).
- **Intersection / joint probability (A and B):** both happen.
- **Mutually exclusive:** A and B can't both happen (P(A and B) = 0).
- **Independent:** knowing A tells you nothing about B: P(A and B) = P(A) × P(B).
- **Conditional probability P(A | B):** the probability of A **given** B happened = P(A and B) / P(B). Read "|" as "given".
- **Law of total probability:** P(B) = P(B | A) P(A) + P(B | not A) P(not A): add up the ways B can happen.
- **Bayes' rule:** P(A | B) = P(B | A) × P(A) / P(B).
- **Prior:** what you believed before the evidence (P(A)). **Likelihood:** how probable the evidence is under the claim (P(B | A)). **Posterior:** the updated belief (P(A | B)).
- **Base rate:** how common something is in the population (the prior). Ignoring it is the **base-rate fallacy**.
- **Sensitivity (true positive rate):** P(test positive | sick). **Specificity (true negative rate):** P(test negative | healthy). **False positive rate:** 1 − specificity.
- **Expected value:** the long-run average outcome: Σ value × probability.
- **Classifier:** a model that assigns each item to a category (fraud / not fraud, spam / not spam).

**Everyday picture.** A smoke alarm that beeps at every burnt toast. Most beeps aren't fires, not because the alarm is bad, but because **fires are rare and toast is common**. Bayes' rule is the arithmetic of that intuition.

**Bayes, traced with counts** (counts are far easier than formulas). A disease affects **1%** of people. The test catches **95%** of sick people (sensitivity) and wrongly flags **5%** of healthy people. You test positive. How likely are you sick? Imagine 10,000 people:

| | Sick (1%) | Healthy (99%) | Total |
|---|---|---|---|
| people | 100 | 9,900 | 10,000 |
| test positive | 95 (95% of 100) | 495 (5% of 9,900) | **590** |
| test negative | 5 | 9,405 | 9,410 |

P(sick | positive) = 95 / 590 = **16%**. Most positives are healthy people, because there are so many more healthy people to make mistakes on. A second, independent positive test changes the prior from 1% to 16%, and then P(sick) jumps to about **78%**.

**The same with the formula:** P(sick | +) = P(+ | sick) × P(sick) / P(+) = 0.95 × 0.01 / (0.95 × 0.01 + 0.05 × 0.99) = 0.0095 / 0.059 = 0.161.

**Rules you'll use:**

| Rule | Formula | Example |
|---|---|---|
| complement | P(not A) = 1 − P(A) | P(at least one six in 4 rolls) = 1 − (5/6)⁴ = 0.518 |
| independent "and" | P(A and B) = P(A) P(B) | two heads: 0.5 × 0.5 |
| "or" | P(A) + P(B) − P(A and B) | |
| conditional | P(A \| B) = P(A and B) / P(B) | |
| total probability | P(B) = Σ P(B \| Aᵢ) P(Aᵢ) | P(+) above: 0.95 × 0.01 + 0.05 × 0.99 |
| Bayes | P(A \| B) = P(B \| A) P(A) / P(B) | the disease test |
| expected value | E[X] = Σ x · P(x) | a fair die: (1+2+…+6)/6 = 3.5 |

**"At least one" problems:** compute "none" and subtract from 1. The **birthday problem**: with 23 people, P(at least two share a birthday) = 1 − (365/365 × 364/365 × … × 343/365) ≈ **51%**, far higher than intuition says, because there are 253 **pairs**.

**When probability thinking matters in data work:** reading any test, classifier or alert (Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests); precision and recall in `machine-learning.md`), fraud and anomaly alerts on rare events, A/B tests, risk estimates, and Naive Bayes classifiers.

**Common mistakes:**

- ❌ Confusing P(positive | sick) with P(sick | positive) ("the test is 95% accurate, so I'm 95% likely sick"). This is the **prosecutor's fallacy**.
- ❌ Ignoring the base rate when events are rare (fraud, disease, defects).
- ❌ Multiplying probabilities of events that aren't independent (two alarms triggered by the same cause).
- ❌ The **gambler's fallacy**: after five reds, black is "due". Independent spins have no memory.

**Used in real software:** spam filters (Naive Bayes), medical diagnosis, fraud alert triage, recommendation ranking, A/B testing platforms using Bayesian methods, risk scoring in insurance and lending.

### Python

```python
import numpy as np
from math import comb, prod

def posterior(prior, sensitivity, false_positive_rate):
    p_positive = sensitivity * prior + false_positive_rate * (1 - prior)      # law of total probability
    return sensitivity * prior / p_positive                                   # Bayes' rule

p1 = posterior(0.01, 0.95, 0.05)
print(f"after one positive: {p1:.1%}   after a second independent positive: {posterior(p1, 0.95, 0.05):.1%}")
for prior in (0.001, 0.01, 0.1, 0.5):
    print(f"prior {prior:>5.1%} → posterior {posterior(prior, 0.95, 0.05):.1%}")
```

**Output:**

```text
after one positive: 16.1%   after a second independent positive: 78.5%
prior  0.1% → posterior 1.9%
prior  1.0% → posterior 16.1%
prior 10.0% → posterior 67.9%
prior 50.0% → posterior 95.0%
```

The same test means very different things depending on how common the disease is: the **prior** matters as much as the test.

```python
rng = np.random.default_rng(0)
n = 1_000_000
sick = rng.random(n) < 0.01
positive = np.where(sick, rng.random(n) < 0.95, rng.random(n) < 0.05)
print(f"simulated P(sick | positive) = {sick[positive].mean():.3f}")          # matches the formula

print("P(at least one six in 4 rolls):", round(1 - (5 / 6) ** 4, 4))
same_bday = 1 - prod((365 - k) / 365 for k in range(23))
print(f"birthday problem, 23 people: {same_bday:.3f}  (pairs: {comb(23, 2)})")
print("expected value of a die:", np.mean(np.arange(1, 7)), "| simulated:", rng.integers(1, 7, 100_000).mean().round(3))
```

**Output:**

```text
simulated P(sick | positive) = 0.161
P(at least one six in 4 rolls): 0.5177
birthday problem, 23 people: 0.507  (pairs: 253)
expected value of a die: 3.5 | simulated: 3.511
```

`math.comb(n, k)` counts the ways to choose k items from n ("n choose k"); `math.prod` multiplies a sequence.

### Practice

1. 2% of transactions are fraud. A model flags 90% of frauds and 3% of genuine transactions. What fraction of flagged transactions are actually fraud? Solve with counts out of 10,000, then with the function.
2. You roll two dice. What's P(sum = 8 | the first die shows an even number)? Reason by listing outcomes, then simulate.

<details>
<summary><b>Answer</b></summary>

1. Of 10,000: 200 fraud → 180 flagged; 9,800 genuine → 294 flagged. 180 / 474 ≈ **38%**.

```python
print(round(posterior(0.02, 0.90, 0.03), 3))
d1, d2 = rng.integers(1, 7, 200_000), rng.integers(1, 7, 200_000)
even = d1 % 2 == 0
print(round(((d1 + d2 == 8) & even).sum() / even.sum(), 3), "exact:", round(3 / 18, 3))
```

**Output:**

```text
0.38
0.166 exact: 0.167
```

2. First die even: 18 equally likely outcomes. Sum 8 among them: (2,6), (4,4), (6,2) → 3/18 = 1/6 ≈ 0.167.

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [168. Calculate Conditional Probability from Data](https://www.deep-ml.com/problems/168) | 🟢 Easy |
| 2 | [179. Expected Value and Variance of an n-Sided Die](https://www.deep-ml.com/problems/179) | 🟢 Easy |
| 3 | [180. Conditional Probability from Joint Distribution](https://www.deep-ml.com/problems/180) | 🟡 Medium |
| 4 | [244. Compute Total Probability using Law of Total Probability](https://www.deep-ml.com/problems/244) | 🟡 Medium |
| 5 | [246. Birthday Problem Probability](https://www.deep-ml.com/problems/246) | 🟡 Medium |

**Learn more:** [3Blue1Brown: Bayes' theorem (video)](https://www.youtube.com/watch?v=HZGCoVF3YvM) · [Seeing Theory: compound probability](https://seeing-theory.brown.edu/compound-probability/index.html)

---

## 54. Probability Distributions: Normal, Binomial, Poisson and More

![The six distributions you meet most: uniform, normal, binomial, Poisson, exponential and log-normal](images/data-science/distributions.png)

### Theory

> **In simple words:** a **probability distribution** describes all the values something can take and how likely each is. A handful of distributions describe most real data: the **normal** bell curve for measurements, the **binomial** for "how many successes in n tries", the **Poisson** for "how many events in a period", the **exponential** for waiting times, and the **log-normal** for positive, right-skewed amounts like incomes and prices.

**Words to know:**

- **Random variable:** a quantity whose value depends on chance (the number of clicks today).
- **Discrete vs continuous:** countable values (0, 1, 2 clicks) vs any value in a range (a delivery time of 2.37 days).
- **PMF (probability mass function):** for discrete variables, P(X = k) for each k.
- **PDF (probability density function):** for continuous variables, a curve whose **area** over a range is the probability of landing in that range. (The height at one point is a density, not a probability; P(X = exactly 2.37) is 0.)
- **CDF (cumulative distribution function):** P(X ≤ x). Works for both kinds; it's the theoretical version of the ECDF (Section [46](#46-seaborn-i-distributions)).
- **Parameters:** the numbers that pin down a distribution's exact shape (the normal's mean μ "mu" and standard deviation σ "sigma").
- **Expected value (mean) and variance of a distribution:** its long-run average and spread.
- **z-score:** (x − μ) / σ: how many standard deviations from the mean. The **standard normal** has μ = 0, σ = 1.
- **Tail:** the far ends of a distribution. "Heavy-tailed" = extreme values are more common than a normal curve predicts.
- **`scipy.stats`:** SciPy's module with every common distribution: `.pmf`/`.pdf`, `.cdf`, `.ppf` (inverse CDF: the value at a given percentile), `.rvs` (random samples), `.mean()`, `.std()`.

**Everyday picture.** A distribution is the **shape a pile of sand makes** when you pour many grains (outcomes) through a funnel: always the same kind of shape for the same process, even though each grain lands somewhere unpredictable.

**The distributions you'll meet most:**

| Distribution | Type | Describes | Parameters | Mean / variance | Example |
|---|---|---|---|---|---|
| **Uniform** | continuous | every value in [a, b] equally likely | a, b | (a+b)/2 | a random number generator |
| **Bernoulli** | discrete | one yes/no trial | p | p / p(1−p) | did this visitor buy? |
| **Binomial** | discrete | number of successes in n independent trials | n, p | np / np(1−p) | buyers among 1,000 visitors |
| **Poisson** | discrete | number of events in a fixed interval, at a steady average rate | λ ("lambda") | λ / λ | orders per minute, typos per page |
| **Normal (Gaussian)** | continuous | sums of many small effects; measurement errors | μ, σ | μ / σ² | heights, sensor noise, sample means |
| **Exponential** | continuous | time between Poisson events | rate λ (scale 1/λ) | 1/λ / 1/λ² | time until the next customer |
| **Log-normal** | continuous | positive values whose **log** is normal; right-skewed | μ, σ of the log | | incomes, order values, response times |
| **Student's t** | continuous | like the normal, heavier tails; used with small samples | degrees of freedom | | t-tests (Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests)) |
| **Chi-square (χ²)** | continuous | sums of squared normal values | degrees of freedom | | chi-square tests |

**The normal distribution's 68–95–99.7 rule:** about **68%** of values lie within 1σ of the mean, **95%** within 2σ (more exactly 1.96σ), and **99.7%** within 3σ. A value 3σ away happens about 3 times in 1,000.

**Binomial, traced by hand:** a coin with p = 0.5 flipped n = 4 times. P(exactly 2 heads) = (number of ways to choose which 2 flips are heads) × 0.5² × 0.5² = C(4, 2) × 0.0625 = 6 × 0.0625 = **0.375**. In general P(k) = C(n, k) pᵏ (1 − p)ⁿ⁻ᵏ.

**Poisson, traced:** a shop averages λ = 3 orders per minute. P(0 orders in a minute) = e⁻³ ≈ **0.05**. In general P(k) = λᵏ e⁻λ / k!. If it averages 3 per minute, the **waiting time** between orders is exponential with mean 1/3 minute.

**Why the normal is everywhere:** anything that's a **sum or average of many independent small effects** tends to be normal (the Central Limit Theorem, Section [55](#55-sampling-the-central-limit-theorem-and-standard-error)). Things that are **products** of many effects (growth, compounding) tend to be log-normal.

**Choosing a distribution for your data:** counts of successes out of a fixed number → binomial; counts of events with no fixed maximum → Poisson; waiting times → exponential; positive and skewed → log-normal; measurements and averages → normal. Then **check** with a histogram or a Q–Q plot (`scipy.stats.probplot`), which draws your data's quantiles against the theoretical ones: a straight line means a good fit.

**Common mistakes:**

- ❌ Assuming everything is normal: money, time and counts usually aren't.
- ❌ Reading a PDF's height as a probability (it can exceed 1). ✅ Probabilities are areas: use the CDF.
- ❌ Using a Poisson model when events cluster (a viral post brings bursts of signups): the variance will be much larger than the mean (**overdispersion**).
- ❌ Using 2 instead of 1.96 when precision matters (or vice versa when it doesn't).

**Used in real software:** capacity planning (Poisson arrivals, exponential service times), quality control (normal limits, "six sigma"), click-through modelling (binomial), finance (log-normal prices, heavy-tailed risk), synthetic test data, and every statistical test.

### Python

```python
import numpy as np
from scipy import stats

print("Binomial n=4, p=0.5:", stats.binom.pmf(range(5), 4, 0.5).round(4).tolist())
print("P(at most 520 buyers of 1,000 at p=0.5):", round(stats.binom.cdf(520, 1000, 0.5), 4))
print("Poisson λ=3, P(0..5):", stats.poisson.pmf(range(6), 3).round(3).tolist())
print("P(more than 6 orders in a minute):", round(stats.poisson.sf(6, 3), 4))     # sf = 1 - cdf ("survival function")

norm = stats.norm(loc=170, scale=10)                         # heights: mean 170 cm, std 10
print("P(height < 185):", round(norm.cdf(185), 4), "| 90th percentile:", round(norm.ppf(0.9), 1))
print("within 1, 2, 3 σ:", [round(float(stats.norm.cdf(k) - stats.norm.cdf(-k)), 4) for k in (1, 2, 3)])
print("z for the middle 95%:", round(stats.norm.ppf(0.975), 3))
print("exponential wait, mean 1/3 min, P(wait > 1 min):", round(stats.expon(scale=1 / 3).sf(1), 4))
```

**Output:**

```text
Binomial n=4, p=0.5: [0.0625, 0.25, 0.375, 0.25, 0.0625]
P(at most 520 buyers of 1,000 at p=0.5): 0.9026
Poisson λ=3, P(0..5): [0.05, 0.149, 0.224, 0.224, 0.168, 0.101]
P(more than 6 orders in a minute): 0.0335
P(height < 185): 0.9332 | 90th percentile: 182.8
within 1, 2, 3 σ: [0.6827, 0.9545, 0.9973]
z for the middle 95%: 1.96
exponential wait, mean 1/3 min, P(wait > 1 min): 0.0498
```

`ppf` is the **inverse** of `cdf`: `cdf(185)` answers "what share is below 185?", `ppf(0.9)` answers "below what height are 90% of people?". `ppf(0.975) = 1.96` is where the famous 1.96 comes from.

```python
import matplotlib.pyplot as plt

rng = np.random.default_rng(3)
samples = {
    "Uniform(0, 1)": rng.uniform(0, 1, 20_000),
    "Normal(170, 10)": rng.normal(170, 10, 20_000),
    "Binomial(n=20, p=0.3)": rng.binomial(20, 0.3, 20_000),
    "Poisson(λ=3)": rng.poisson(3, 20_000),
    "Exponential(mean 2)": rng.exponential(2, 20_000),
    "Log-normal(6.5, 0.7)": rng.lognormal(6.5, 0.7, 20_000),
}
fig, axes = plt.subplots(2, 3, figsize=(11, 6), layout="constrained")
for ax, (name, data) in zip(axes.flat, samples.items()):
    discrete = np.issubdtype(data.dtype, np.integer)
    if discrete:
        vals, counts = np.unique(data, return_counts=True)
        ax.bar(vals, counts / len(data), color="tab:blue", width=0.8)
    else:
        ax.hist(data, bins=60, density=True, color="tab:blue", alpha=0.8)
    ax.set_title(name)
    print(f"{name:<22} mean {data.mean():8.2f}  std {data.std():7.2f}  skew {stats.skew(data):5.2f}")
fig.suptitle("Simulated distributions (20,000 draws each)")
fig.savefig("distributions.png", dpi=100)
plt.close(fig)
```

**Output:**

```text
Uniform(0, 1)          mean     0.50  std    0.29  skew -0.00
Normal(170, 10)        mean   170.05  std    9.99  skew -0.01
Binomial(n=20, p=0.3)  mean     5.97  std    2.05  skew  0.20
Poisson(λ=3)           mean     3.03  std    1.74  skew  0.59
Exponential(mean 2)    mean     2.02  std    2.00  skew  2.01
Log-normal(6.5, 0.7)   mean   850.61  std  671.24  skew  2.63
```

The Poisson's mean and variance are both about 3 (std √3 ≈ 1.73), and the exponential's mean equals its std: quick checks that data follows these distributions.

### Practice

1. A web page converts 4% of visitors. Out of 500 visitors, what's the probability of 30 or more buyers? Use `binom.sf(29, ...)` and check by simulation.
2. Exam scores are normal with mean 65 and std 12. What score do you need to be in the top 10%? What fraction score below 40?

<details>
<summary><b>Answer</b></summary>

```python
print(round(stats.binom.sf(29, 500, 0.04), 4), (rng.binomial(500, 0.04, 200_000) >= 30).mean().round(4))
exam = stats.norm(65, 12)
print(round(exam.ppf(0.9), 1), round(exam.cdf(40), 4))
```

**Output:**

```text
0.0196 0.0197
80.4 0.0186
```

`sf(29)` = P(X > 29) = P(X ≥ 30). The expected number of buyers is 500 × 0.04 = 20, so 30 or more is unusual (about 1.6%).

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [81. Poisson Distribution Probability Calculator](https://www.deep-ml.com/problems/81) | 🟢 Easy |
| 2 | [79. Binomial Distribution Probability](https://www.deep-ml.com/problems/79) | 🟡 Medium |
| 3 | [80. Normal Distribution PDF Calculator](https://www.deep-ml.com/problems/80) | 🟡 Medium |
| 4 | [176. Chi-square Probability Distribution](https://www.deep-ml.com/problems/176) | 🟡 Medium |
| 5 | [245. Hypergeometric Distribution PMF](https://www.deep-ml.com/problems/245) | 🟡 Medium |
| 6 | [247. Negative Binomial Distribution Probability](https://www.deep-ml.com/problems/247) | 🟡 Medium |

**Learn more:** [SciPy: statistical functions (scipy.stats)](https://docs.scipy.org/doc/scipy/reference/stats.html) · [Seeing Theory: probability distributions](https://seeing-theory.brown.edu/probability-distributions/index.html)

---

## 55. Sampling, the Central Limit Theorem and Standard Error

![The central limit theorem: averages of samples from a skewed distribution form a bell curve that narrows as the sample size grows](images/data-science/central-limit-theorem.png)

### Theory

> **In simple words:** you almost never measure everyone; you measure a **sample** and use it to estimate the truth about the **population**. Different samples give different answers. The **Central Limit Theorem** says the **average** of a sample is approximately normally distributed around the true value, and the **standard error** tells you how far off a sample average typically is. It shrinks with the square root of the sample size.

**Words to know:**

- **Population:** everyone or everything you want to know about (all customers, all future orders).
- **Sample:** the part you actually measured.
- **Parameter vs statistic:** a fixed (usually unknown) number describing the population, like the true mean μ, vs a number computed from the sample, like the sample mean x̄, used to **estimate** it.
- **Estimator:** a formula that turns a sample into an estimate (the sample mean estimates μ).
- **Random sample:** every member of the population has a known, fair chance of being chosen.
- **Sampling bias:** a sampling method that systematically over- or under-represents some groups (surveying only app users about the website).
- **Sampling distribution:** the distribution of a statistic (such as the mean) over many hypothetical repeated samples.
- **Law of large numbers:** as the sample grows, the sample mean gets closer to the true mean (Section [15](#15-random-numbers-and-simulation)).
- **Central Limit Theorem (CLT):** for large enough samples (often n ≥ 30, more for very skewed data), the sample mean is approximately **normal**, centred on the true mean, **whatever shape** the original data has.
- **Standard error (SE):** the standard deviation of the sampling distribution: how much a statistic typically varies between samples. For a mean, SE = σ / √n (estimated with the sample's std, s / √n).
- **Stratified sampling:** sampling separately within groups (cities, plans) so each is represented.

**Everyday picture.** To check if a pot of soup is salty enough, you taste **one spoonful**: a sample. One spoonful from a well-stirred pot (random sample) tells you about the whole pot (population). A spoonful skimmed off the top of an unstirred pot (biased sample) misleads you, and no amount of extra spoonfuls from the top fixes it.

**Standard error, traced:** order values have std σ = ₹800.

| Sample size n | SE = 800 / √n | The sample mean is typically within… |
|---|---|---|
| 16 | 800 / 4 = 200 | ±₹200 of the truth |
| 100 | 800 / 10 = 80 | ±₹80 |
| 400 | 800 / 20 = 40 | ±₹40 |
| 10,000 | 800 / 100 = 8 | ±₹8 |

**To halve the error, you need four times the data.** That square root is why precise estimates get expensive, and why A/B tests on small effects need huge samples (Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls)).

**Std vs SE, the most confused pair in statistics:**

| | Standard deviation (s) | Standard error (SE) |
|---|---|---|
| describes | spread of **individual values** | uncertainty of an **estimate** (like the mean) |
| with more data | stays about the same | shrinks like 1/√n |
| question it answers | "how different are customers from each other?" | "how precisely do I know the average customer?" |

**The CLT, step by step** (what the chart above simulates):

1. Start with a skewed population (order values: most small, a few huge).
2. Draw a sample of n orders and compute its mean. Repeat thousands of times.
3. Plot those means: they form a **bell curve**, centred on the true mean.
4. With bigger n, the bell gets **narrower** (its std is the SE, σ/√n) and more symmetric.

This is why so many statistical tests assume normality: they're usually about **means**, and means are approximately normal even when the data isn't.

**When the CLT is weak:** tiny samples from very skewed or heavy-tailed data (a few huge outliers can dominate a mean of 30 values); statistics other than means (medians, maxima behave differently: use the bootstrap, Section [56](#56-confidence-intervals-and-the-bootstrap)); dependent data (repeated measurements of the same customers, time series).

**Sampling in practice:**

| Method | How | Use when |
|---|---|---|
| simple random | `df.sample(n=1000, random_state=0)` | a quick representative sample |
| stratified | `df.groupby("city").sample(frac=0.1, random_state=0)` | keep each group's share (or oversample small groups) |
| systematic | every k-th row | data arriving in a stream (beware hidden patterns) |
| cluster | pick whole groups (stores), then everyone in them | when reaching individuals is expensive |

**Common mistakes:**

- ❌ Reporting the std when you mean the SE (or the reverse) in error bars. ✅ Always say which.
- ❌ Believing a huge biased sample beats a small random one. More data doesn't fix bias.
- ❌ Assuming n = 30 is always "enough" for skewed data.
- ❌ Treating repeated measurements of the same user as independent samples (they underestimate the SE).

**Used in real software:** opinion polls (± margin of error), A/B testing platforms, quality inspection (sample 50 items per batch), sampling huge logs for quick analysis, monitoring dashboards showing averages with error bands.

### Python

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

rng = np.random.default_rng(42)
population = rng.exponential(scale=800, size=1_000_000)        # skewed "order values", true mean ≈ 800
mu, sigma = population.mean(), population.std()
print(f"population: mean {mu:.1f}, std {sigma:.1f}, skew {pd.Series(population).skew():.2f}")

fig, axes = plt.subplots(1, 4, figsize=(13, 3), layout="constrained")
axes[0].hist(population[:20_000], bins=60, color="lightgray")
axes[0].set_title("population (skewed)")
for ax, n in zip(axes[1:], [5, 30, 200]):
    means = rng.choice(population, size=(5_000, n)).mean(axis=1)      # 5,000 samples of size n
    ax.hist(means, bins=50, color="tab:blue", density=True)
    ax.axvline(mu, color="tab:red", lw=1.5)
    ax.set_title(f"means of samples, n = {n}")
    print(f"n={n:>3}: mean of means {means.mean():7.1f} | std of means {means.std():6.1f} | theory σ/√n {sigma / np.sqrt(n):6.1f} | skew {pd.Series(means).skew():.2f}")
fig.savefig("central-limit-theorem.png", dpi=100)
plt.close(fig)
```

**Output:**

```text
population: mean 799.8, std 799.8, skew 2.00
n=  5: mean of means   800.3 | std of means  360.1 | theory σ/√n  357.7 | skew 0.99
n= 30: mean of means   800.0 | std of means  145.9 | theory σ/√n  146.0 | skew 0.40
n=200: mean of means   799.8 | std of means   56.3 | theory σ/√n   56.6 | skew 0.18
```

The spread of the sample means matches σ/√n almost exactly, and their skew falls towards 0 (a symmetric bell) as n grows. With n = 5 the bell is still lopsided: the CLT needs larger samples for skewed data.

```python
customers = pd.DataFrame({"city": rng.choice(["Pune", "Mumbai", "Goa"], 10_000, p=[0.45, 0.5, 0.05]),
                          "spend": rng.exponential(800, 10_000)})
simple = customers.sample(n=200, random_state=1)
strat = customers.groupby("city").sample(frac=0.02, random_state=1)
print("population shares:", customers["city"].value_counts(normalize=True).round(3).to_dict())
print("simple sample:    ", simple["city"].value_counts(normalize=True).round(3).to_dict())
print("stratified sample:", strat["city"].value_counts(normalize=True).round(3).to_dict())

sample = customers["spend"].sample(400, random_state=2)
print(f"one sample of 400: mean {sample.mean():.1f}, std {sample.std():.1f}, SE {sample.std() / np.sqrt(len(sample)):.1f} "
      f"(pandas .sem(): {sample.sem():.1f})")
```

**Output:**

```text
population shares: {'Mumbai': 0.504, 'Pune': 0.444, 'Goa': 0.052}
simple sample:     {'Mumbai': 0.545, 'Pune': 0.415, 'Goa': 0.04}
stratified sample: {'Mumbai': 0.505, 'Pune': 0.445, 'Goa': 0.05}
one sample of 400: mean 811.2, std 803.3, SE 40.2 (pandas .sem(): 40.2)
```

`groupby(...).sample(frac=0.02)` takes 2% of **each** city, so small groups like Goa keep their share exactly; a simple random sample of 200 can over- or under-represent them by chance. `Series.sem()` is pandas' built-in **standard error of the mean**.

### Practice

1. A survey of 100 users finds mean session length 12 minutes with std 9. What's the SE? How many users would you need to get the SE down to 0.3 minutes?
2. Simulate: draw 10,000 samples of size 50 from `rng.uniform(0, 10, ...)` and check that the std of their means ≈ σ/√50 (the std of a uniform on [0, 10] is 10/√12).

<details>
<summary><b>Answer</b></summary>

1. SE = 9 / √100 = 0.9 min. For 0.3: √n = 9 / 0.3 = 30 → n = **900** (3× smaller error needs 9× the data).

```python
means = rng.uniform(0, 10, size=(10_000, 50)).mean(axis=1)
print(round(means.std(), 4), round(10 / np.sqrt(12) / np.sqrt(50), 4))
```

**Output:**

```text
0.4077 0.4082
```

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [181. Sampling Distribution of the Mean](https://www.deep-ml.com/problems/181) | 🟢 Easy |
| 2 | [182. Central Limit Theorem Simulation](https://www.deep-ml.com/problems/182) | 🟡 Medium |

**Learn more:** [Seeing Theory: the central limit theorem](https://seeing-theory.brown.edu/probability-distributions/index.html#section3) · [OpenIntro Statistics, chapter 5 (foundations for inference)](https://www.openintro.org/book/os/)

---

## 56. Confidence Intervals and the Bootstrap

![100 confidence intervals from 100 samples: about 95 of them contain the true mean (red line), and about 5 miss it](images/data-science/ci-coverage.png)

### Theory

> **In simple words:** an estimate without an error bar is half an answer. A **95% confidence interval** is a range built from your sample by a method that captures the true value **95% of the time**. The **bootstrap** builds such intervals for almost any statistic (median, ratio, percentile) by resampling your own data thousands of times: no formula needed.

**Words to know:**

- **Point estimate:** a single best guess (the sample mean, ₹812).
- **Interval estimate / confidence interval (CI):** a range of plausible values (₹770 to ₹854).
- **Confidence level:** the long-run success rate of the method (95%, 90%, 99%).
- **Margin of error:** half the width of the interval (± ₹42).
- **Critical value:** the multiplier for the SE: 1.96 for 95% with the normal distribution; slightly bigger from the **t distribution** for small samples.
- **t distribution:** like the normal but with heavier tails, accounting for the extra uncertainty of estimating σ from a small sample; nearly identical to the normal for n above ~30. **Degrees of freedom (df)** = n − 1 for a mean.
- **Bootstrap:** estimating a statistic's uncertainty by repeatedly **resampling the data with replacement** and recomputing the statistic.
- **Resample with replacement:** draw n values from your n values, where each draw can pick a value already picked (some values appear twice, some not at all).
- **Percentile bootstrap interval:** the 2.5th and 97.5th percentiles of the bootstrapped statistics.
- **Wilson interval:** a better CI for proportions (rates) than the simple formula, especially for small samples or rates near 0% or 100%.

**Everyday picture.** A weather forecast says "28°C, give or take 2". The give-or-take is the confidence interval. The bootstrap is like estimating how much a recipe's taste varies by **remaking it many times from the same box of ingredients**, picking ingredients at random each time.

**A CI for a mean, traced:** n = 100 orders, sample mean ₹812, sample std ₹420.

1. SE = 420 / √100 = 42.
2. Critical value for 95% with 99 degrees of freedom ≈ 1.984 (from `stats.t.ppf(0.975, 99)`; 1.96 with the normal).
3. Margin = 1.984 × 42 ≈ 83.3.
4. CI = 812 ± 83.3 = **₹728.7 to ₹895.3**.

**What "95% confidence" means (and doesn't):**

- ✅ "If we repeated the sampling many times, 95% of the intervals built this way would contain the true mean." (The chart above shows exactly this.)
- ✅ Informally: "the data are consistent with a true mean anywhere from ₹729 to ₹895".
- ❌ "There's a 95% probability the true mean is in **this** interval." (The true mean is fixed; this interval either contains it or not. That probability statement needs Bayesian methods.)
- ❌ "95% of orders are between ₹729 and ₹895." (That's about individual values, the std's job, not the mean's.)

**A CI for a proportion:** 46 buyers out of 1,000 visitors: p̂ = 0.046, SE = √(p̂(1 − p̂)/n) = √(0.046 × 0.954 / 1000) ≈ 0.0066, so 95% CI ≈ 0.046 ± 1.96 × 0.0066 = 3.3% to 5.9%. For small counts use the **Wilson** interval (`statsmodels.stats.proportion.proportion_confint(method="wilson")`).

**The bootstrap, step by step** (CI for the **median** order value, which has no simple formula):

1. Take your sample of n values.
2. Draw n values **with replacement** from it: a bootstrap sample.
3. Compute the median of that bootstrap sample.
4. Repeat steps 2–3 several thousand times.
5. The 2.5th and 97.5th percentiles of those medians form a 95% CI.

It works because your sample is the best picture you have of the population; resampling it imitates "drawing new samples". It needs a reasonably large, representative sample, and it struggles with extremes (the maximum) and dependent data.

**When to use what:**

| Statistic | CI method |
|---|---|
| mean, n not tiny | t interval (`scipy.stats.t.interval`, or `scipy.stats.ttest_1samp(...).confidence_interval()`) |
| proportion / rate | Wilson interval |
| median, percentile, ratio, correlation, anything else | bootstrap (`scipy.stats.bootstrap`) |
| difference between two groups | the same idea on the difference (Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests)) |

**Common mistakes:**

- ❌ Reporting a mean or a rate with no interval.
- ❌ Overlapping CIs → "no difference". Two 95% CIs can overlap a little while the difference is still significant. ✅ Compute a CI for the **difference**.
- ❌ The normal-approximation interval for a rate of 2 out of 40 (it can go below 0%). ✅ Wilson.
- ❌ Bootstrapping 10 data points and trusting the result.

**Used in real software:** poll margins of error, A/B test dashboards (CI on the lift), model evaluation (a CI on accuracy from a finite test set), forecast ranges, scientific reporting.

### Python

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import stats

rng = np.random.default_rng(7)
orders = rng.gamma(shape=3.5, scale=230, size=100)              # one sample of 100 order values
m, s, n = orders.mean(), orders.std(ddof=1), len(orders)
se = s / np.sqrt(n)
t_crit = stats.t.ppf(0.975, df=n - 1)
print(f"mean {m:.1f}, std {s:.1f}, SE {se:.1f}, t critical {t_crit:.3f}")
print(f"95% CI by hand: {m - t_crit * se:.1f} to {m + t_crit * se:.1f}")
print("scipy:", np.round(stats.t.interval(0.95, df=n - 1, loc=m, scale=se), 1))
print("normal vs t critical values for n = 5, 30, 1000:", round(stats.norm.ppf(0.975), 3),
      [round(float(stats.t.ppf(0.975, k - 1)), 3) for k in (5, 30, 1000)])
```

**Output:**

```text
mean 731.0, std 359.5, SE 35.9, t critical 1.984
95% CI by hand: 659.7 to 802.4
scipy: [659.7 802.4]
normal vs t critical values for n = 5, 30, 1000: 1.96 [2.776, 2.045, 1.962]
```

```python
true_mean = 3.5 * 230                                            # the gamma distribution's mean: shape × scale
hits, intervals = 0, []
for i in range(100):
    smp = rng.gamma(3.5, 230, 100)
    lo, hi = stats.t.interval(0.95, df=99, loc=smp.mean(), scale=smp.std(ddof=1) / 10)
    intervals.append((lo, hi)); hits += lo <= true_mean <= hi

fig, ax = plt.subplots(figsize=(9, 4), layout="constrained")
for i, (lo, hi) in enumerate(intervals):
    ax.plot([i, i], [lo, hi], color="tab:blue" if lo <= true_mean <= hi else "tab:red", lw=1.6)
ax.axhline(true_mean, color="black", lw=1)
ax.set(title=f"{hits} of 100 intervals contain the true mean ({true_mean:.0f})", xlabel="sample number", ylabel="95% CI for the mean")
fig.savefig("ci-coverage.png", dpi=100)
plt.close(fig)
print(f"{hits} of 100 intervals caught the true mean")
```

**Output:**

```text
92 of 100 intervals caught the true mean
```

```python
def bootstrap_ci(data, stat=np.median, reps=10_000, level=0.95, seed=0):
    r = np.random.default_rng(seed)
    boot = np.array([stat(r.choice(data, size=len(data), replace=True)) for _ in range(reps)])
    alpha = (1 - level) / 2
    return np.quantile(boot, [alpha, 1 - alpha])

print("median:", round(float(np.median(orders)), 1), "bootstrap 95% CI:", bootstrap_ci(orders).round(1))
res = stats.bootstrap((orders,), np.median, n_resamples=10_000, method="percentile", random_state=0)
print("scipy.stats.bootstrap:", np.round([res.confidence_interval.low, res.confidence_interval.high], 1))
print("p90 bootstrap CI:", bootstrap_ci(orders, stat=lambda d: np.percentile(d, 90)).round(1))

from statsmodels.stats.proportion import proportion_confint
for buyers, visitors in [(46, 1000), (2, 40)]:
    p = buyers / visitors
    normal = (p - 1.96 * np.sqrt(p * (1 - p) / visitors), p + 1.96 * np.sqrt(p * (1 - p) / visitors))
    wilson = proportion_confint(buyers, visitors, method="wilson")
    print(f"{buyers}/{visitors}: normal ({normal[0]:.3f}, {normal[1]:.3f})  wilson ({wilson[0]:.3f}, {wilson[1]:.3f})")
```

**Output:**

```text
median: 681.8 bootstrap 95% CI: [611.6 743.5]
scipy.stats.bootstrap: [611.6 745.3]
p90 bootstrap CI: [1045.5 1304.8]
46/1000: normal (0.033, 0.059)  wilson (0.035, 0.061)
2/40: normal (-0.018, 0.118)  wilson (0.014, 0.165)
```

For 2 buyers out of 40, the simple normal formula gives a **negative** lower bound (an impossible rate); the Wilson interval stays within 0–1 and is more accurate.

### Practice

1. From `orders`, compute a 90% and a 99% t-interval for the mean. Which is wider, and why?
2. Bootstrap a 95% CI for the **ratio** of mean order value in two groups: `a = rng.gamma(3.5, 230, 120)`, `b = rng.gamma(3.5, 250, 150)` (resample each group separately).

<details>
<summary><b>Answer</b></summary>

```python
for level in (0.90, 0.99):
    print(level, np.round(stats.t.interval(level, df=n - 1, loc=m, scale=se), 1))

a, b = rng.gamma(3.5, 230, 120), rng.gamma(3.5, 250, 150)
r2 = np.random.default_rng(1)
ratios = [r2.choice(b, len(b)).mean() / r2.choice(a, len(a)).mean() for _ in range(5_000)]
print(round(b.mean() / a.mean(), 3), np.quantile(ratios, [0.025, 0.975]).round(3))
```

**Output:**

```text
0.9 [671.4 790.7]
0.99 [636.6 825.5]
1.124 [0.996 1.272]
```

1. The 99% interval is wider: to be right more often, the method must cast a wider net.
2. If the interval contains 1.0, the data are consistent with no difference in mean order value.

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [212. Confidence Interval for Population Mean](https://www.deep-ml.com/problems/212) | 🟡 Medium |
| 2 | [213. Bayesian Inference for Beta-Binomial Model](https://www.deep-ml.com/problems/213) | 🟡 Medium |

**Learn more:** [SciPy: bootstrap](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.bootstrap.html) · [Seeing Theory: frequentist inference](https://seeing-theory.brown.edu/frequentist-inference/index.html)

---

## 57. Hypothesis Testing: p-values, t-tests, Chi-Square and Non-Parametric Tests

![A p-value is the area in the tails of the null distribution beyond the observed result](images/data-science/p-value.png)

### Theory

> **In simple words:** a **hypothesis test** asks: "if there were really **no** difference, how surprising would my data be?" That surprise is measured by the **p-value**. A small p-value means the data would be unusual under "no difference", so you have evidence that a difference exists. It does **not** tell you how big or important the difference is.

**Words to know:**

- **Null hypothesis (H₀):** the "nothing is going on" claim: no difference between groups, no relationship.
- **Alternative hypothesis (H₁ or Hₐ):** what you're looking for evidence of: the groups differ.
- **Test statistic:** a number summarising how far the data are from H₀ (a t value, a χ² value, a z value).
- **Null distribution:** the distribution the test statistic would have if H₀ were true.
- **p-value:** the probability, **assuming H₀ is true**, of getting a result at least as extreme as the one observed.
- **Significance level (α, "alpha"):** the cut-off decided in advance, usually 0.05. If p < α, "reject H₀" (the result is **statistically significant**).
- **Two-sided vs one-sided test:** two-sided looks for a difference in either direction (the usual default); one-sided only in one, chosen **before** seeing data.
- **Type I error (false positive):** rejecting a true H₀; its probability is α.
- **Type II error (false negative):** missing a real effect; its probability is β. **Power** = 1 − β (Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls)).
- **Effect size:** how big the difference is, in units (₹42) or standardised (**Cohen's d** = difference ÷ pooled std; 0.2 small, 0.5 medium, 0.8 large).
- **Parametric test:** assumes a distribution shape (t-test: roughly normal means). **Non-parametric test:** makes fewer assumptions, often using ranks (Mann–Whitney U).
- **Permutation test:** shuffle the group labels many times to build the null distribution directly by simulation.
- **Multiple comparisons:** running many tests; some will be "significant" by chance (about 1 in 20 at α = 0.05) unless you correct (**Bonferroni**: use α / number of tests; or control the **false discovery rate** with Benjamini–Hochberg).

**Everyday picture.** A courtroom. H₀ is "innocent". The p-value is "how likely is evidence this strong if the defendant were innocent?". If very unlikely, you convict (reject H₀). "Not guilty" doesn't mean "proven innocent": a large p-value means **not enough evidence**, not "no effect".

**The steps of a test:**

1. State H₀ and H₁, and choose α (0.05) **before** looking at the result.
2. Choose the test that fits the data and question (table below).
3. Compute the test statistic and the p-value.
4. Decide: p < α → reject H₀; otherwise, "no significant difference found".
5. Report the **effect size with a confidence interval**, not just the p-value.

**A p-value by simulation, traced (a permutation test):** group A's mean is ₹50 higher than group B's. Shuffle the A/B labels randomly 10,000 times and record the difference each time. If only 120 of the 10,000 shuffled differences are as large as ₹50 (in either direction), the p-value ≈ 120 / 10,000 = **0.012**: under "labels don't matter", a ₹50 gap is rare.

**Which test?**

| Question | Data | Test | Python |
|---|---|---|---|
| do two groups' means differ? | numbers, independent groups | **Welch's t-test** | `stats.ttest_ind(a, b, equal_var=False)` |
| same people before vs after? | paired numbers | paired t-test | `stats.ttest_rel(before, after)` |
| does a mean differ from a target? | numbers | one-sample t-test | `stats.ttest_1samp(x, 100)` |
| do two groups differ, data skewed / ordinal / outliers? | numbers or ranks | **Mann–Whitney U** | `stats.mannwhitneyu(a, b)` |
| paired, non-normal | | Wilcoxon signed-rank | `stats.wilcoxon(before, after)` |
| do two rates differ? | counts of yes/no | two-proportion z-test / chi-square | `proportions_ztest(...)`, `stats.chi2_contingency(table)` |
| are two categorical variables related? | contingency table | **chi-square test of independence** | `stats.chi2_contingency(table)` |
| small counts (any cell < 5) | 2 × 2 table | Fisher's exact test | `stats.fisher_exact(table)` |
| do three or more groups' means differ? | numbers | one-way **ANOVA** / Kruskal–Wallis | `stats.f_oneway(a, b, c)`, `stats.kruskal(...)` |
| does data follow a distribution? | numbers | Shapiro–Wilk, Kolmogorov–Smirnov | `stats.shapiro(x)`, `stats.ks_2samp(a, b)` |
| any statistic, few assumptions | anything | permutation test | `stats.permutation_test(...)` |

**Welch's t-test, traced:** group A: n = 50, mean 12.0, std 3.0; group B: n = 50, mean 10.5, std 3.5. Difference = 1.5. SE of the difference = √(3²/50 + 3.5²/50) = √(0.18 + 0.245) = 0.652. t = 1.5 / 0.652 = **2.30**. With about 96 degrees of freedom, a t of 2.30 has a two-sided p ≈ **0.024**: significant at 0.05. (Welch's version doesn't assume equal spreads; use it by default.)

**Chi-square, traced:** do app and web users differ in whether they buy? Expected counts under "no relationship" = row total × column total ÷ grand total. The statistic adds up (observed − expected)² / expected over all cells; big values mean the table is far from independence.

**What p-values do NOT mean:**

| ❌ Myth | ✅ Reality |
|---|---|
| p = 0.03 → 3% chance H₀ is true | it's P(data this extreme \| H₀), not P(H₀ \| data) |
| p = 0.001 → a big, important effect | huge samples make tiny effects significant; look at the effect size |
| p = 0.2 → there's no effect | there may be one you lacked the data (power) to detect |
| p = 0.049 and p = 0.051 are opposites | they're nearly the same evidence; 0.05 is a convention |

**Statistical vs practical significance:** with a million users, a 0.01% lift in conversion can be "significant" and still worthless. Always pair the p-value with the effect size and its CI, and ask whether that size matters to the business.

**Common mistakes:**

- ❌ Testing many metrics or segments and reporting the one with p < 0.05 (**p-hacking**). ✅ Pre-register the primary metric; correct for multiple tests.
- ❌ Using Student's t-test (`equal_var=True`) with unequal group sizes and spreads. ✅ Welch.
- ❌ A t-test on heavily skewed data with small samples. ✅ Mann–Whitney or bootstrap / permutation.
- ❌ Treating "not significant" as "no difference". ✅ Look at the CI: if it's wide, you simply don't know.

**Used in real software:** A/B testing platforms (Optimizely, Statsig, Eppo, GrowthBook), clinical trials, manufacturing quality control, validating ML models (is the new model really better?), checking survey results.

### Python

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import stats

rng = np.random.default_rng(25)
a = rng.normal(12.0, 3.0, 50)                 # e.g. minutes on site with the new design
b = rng.normal(10.5, 3.5, 50)                 # old design
res = stats.ttest_ind(a, b, equal_var=False)  # Welch's t-test
diff = a.mean() - b.mean()
pooled_sd = np.sqrt((a.var(ddof=1) + b.var(ddof=1)) / 2)
print(f"difference {diff:.2f} min | t = {res.statistic:.2f} | p = {res.pvalue:.4f} | Cohen's d = {diff / pooled_sd:.2f}")
ci = res.confidence_interval(0.95)
print(f"95% CI for the difference: {ci.low:.2f} to {ci.high:.2f}")

observed = diff
pooled = np.concatenate([a, b])
r = np.random.default_rng(0)
perm = np.empty(10_000)
for i in range(10_000):
    shuffled = r.permutation(pooled)
    perm[i] = shuffled[:50].mean() - shuffled[50:].mean()
p_perm = (np.abs(perm) >= abs(observed)).mean()
print(f"permutation test p ≈ {p_perm:.4f}")

fig, ax = plt.subplots(figsize=(8, 3.4), layout="constrained")
bins = np.linspace(perm.min(), perm.max(), 61)                 # the same bins for both layers
ax.hist(perm, bins=bins, color="lightgray", label="differences if labels don't matter (H₀)")
ax.hist(perm[np.abs(perm) >= abs(observed)], bins=bins, color="tab:red", label="as extreme as observed → p-value")
ax.axvline(observed, color="tab:red", lw=2)
ax.set(title=f"Observed difference {observed:.2f}: p ≈ {p_perm:.3f}", xlabel="difference in means (minutes)", ylabel="shuffles")
ax.legend(loc="upper left", fontsize=8, frameon=False)
fig.savefig("p-value.png", dpi=100)
plt.close(fig)
```

**Output:**

```text
difference 1.53 min | t = 2.37 | p = 0.0198 | Cohen's d = 0.47
95% CI for the difference: 0.25 to 2.81
permutation test p ≈ 0.0199
```

`res.confidence_interval()` gives the CI for the difference in means directly. The permutation test needs no normality assumption and agrees closely with the t-test here.

```python
import pandas as pd

table = pd.DataFrame({"bought": [180, 95], "did_not": [1820, 1405]}, index=["app", "web"])
chi2, p, dof, expected = stats.chi2_contingency(table)
print(table, f"chi2 = {chi2:.2f}, dof = {dof}, p = {p:.4f}", "expected counts if no relationship:",
      pd.DataFrame(expected.round(1), index=table.index, columns=table.columns), sep="\n")

skew_rng = np.random.default_rng(29)
skewed_a = skew_rng.lognormal(6.0, 1.0, 40)                  # skewed data, e.g. spend per user
skewed_b = skew_rng.lognormal(6.4, 1.0, 40)
print("t-test p:", round(stats.ttest_ind(skewed_a, skewed_b, equal_var=False).pvalue, 4),
      "| Mann-Whitney p:", round(stats.mannwhitneyu(skewed_a, skewed_b).pvalue, 4))
g = np.random.default_rng(1)
print("ANOVA p for three similar groups:", round(stats.f_oneway(g.normal(5, 1, 30), g.normal(5, 1, 30), g.normal(5.1, 1, 30)).pvalue, 3))
```

**Output:**

```text
     bought  did_not
app     180     1820
web      95     1405
chi2 = 8.05, dof = 1, p = 0.0045
expected counts if no relationship:
     bought  did_not
app   157.1   1842.9
web   117.9   1382.1
t-test p: 0.4518 | Mann-Whitney p: 0.0172
ANOVA p for three similar groups: 0.948
```

The chi-square test finds that app and web users buy at different rates (9.0% vs 6.3%). On the skewed spend data, the t-test misses a difference that the rank-based Mann–Whitney test detects: a few huge values inflate the variance the t-test relies on, while ranks ignore how extreme they are. The ANOVA correctly finds nothing among three nearly identical groups.

```python
false_alarms = 0
for _ in range(1_000):                                # 1,000 A/A tests: both groups from the SAME distribution
    x, y = rng.normal(0, 1, 100), rng.normal(0, 1, 100)
    false_alarms += stats.ttest_ind(x, y).pvalue < 0.05
print(f"{false_alarms / 10:.1f}% of no-difference tests were 'significant' (expected ≈ 5%)")

pvals = np.array([0.001, 0.008, 0.039, 0.041, 0.042, 0.06, 0.074, 0.205])
from statsmodels.stats.multitest import multipletests
for method in ["bonferroni", "fdr_bh"]:
    reject, adj, _, _ = multipletests(pvals, alpha=0.05, method=method)
    print(f"{method:<10} significant: {reject.sum()} of {len(pvals)}  adjusted p: {adj.round(3).tolist()}")
```

**Output:**

```text
4.3% of no-difference tests were 'significant' (expected ≈ 5%)
bonferroni significant: 1 of 8  adjusted p: [0.008, 0.064, 0.312, 0.328, 0.336, 0.48, 0.592, 1.0]
fdr_bh     significant: 2 of 8  adjusted p: [0.008, 0.032, 0.067, 0.067, 0.067, 0.08, 0.085, 0.205]
```

An **A/A test** compares two identical groups: about 5% come out "significant" at α = 0.05, which is exactly what a 5% false-positive rate means. Testing 8 metrics at once, 5 look significant raw; Bonferroni (each p must beat 0.05 / 8 = 0.00625) keeps only 1, and the gentler Benjamini–Hochberg (`fdr_bh`, which controls the share of false discoveries) keeps 2.

### Practice

1. Twelve people's typing speed before and after a training course: before `[52, 48, 61, 55, 47, 58, 50, 63, 45, 57, 54, 49]`, after = before + `[3, 5, -1, 4, 6, 2, 3, 1, 5, 4, 0, 6]`. Which test, and is the improvement significant?
2. A test gives p = 0.0001 for a 0.2% difference in conversion with 5 million users per group. What do you tell the product manager?

<details>
<summary><b>Answer</b></summary>

```python
before = np.array([52, 48, 61, 55, 47, 58, 50, 63, 45, 57, 54, 49])
after = before + np.array([3, 5, -1, 4, 6, 2, 3, 1, 5, 4, 0, 6])
r1 = stats.ttest_rel(after, before)
print(f"mean gain {np.mean(after - before):.2f} wpm, t = {r1.statistic:.2f}, p = {r1.pvalue:.5f}")
print("Wilcoxon p:", round(stats.wilcoxon(after, before).pvalue, 4))
```

**Output:**

```text
mean gain 3.17 wpm, t = 4.79, p = 0.00056
Wilcoxon p: 0.0029
```

1. A **paired** t-test (the same 12 people measured twice), or Wilcoxon if you doubt normality. The gain is clearly significant.
2. "The difference is almost certainly real, but tiny: 0.2% of conversions. Whether it's worth shipping depends on its value versus the cost of the change." Statistical significance isn't business significance.

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [211. Two-Sample T-Test Implementation](https://www.deep-ml.com/problems/211) | 🔴 Hard |
| 2 | [176. Chi-square Probability Distribution](https://www.deep-ml.com/problems/176) | 🟡 Medium |

**Learn more:** [SciPy: hypothesis tests](https://docs.scipy.org/doc/scipy/reference/stats.html#hypothesis-tests-and-related-functions) · [ASA statement on p-values (short and readable)](https://www.amstat.org/asa/files/pdfs/p-valuestatements.pdf) · [StatQuest: p-values (video)](https://www.youtube.com/watch?v=vemZtEM63GY)

---

## 58. A/B Testing End to End: Design, Power, Sample Size and Pitfalls

![Power curves: with a 4% baseline conversion, detecting a +0.5 point lift needs about 25,000 users per group for 80% power](images/data-science/power-curve.png)

### Theory

> **In simple words:** an **A/B test** (online controlled experiment) shows the current version (**A**, control) to a random half of users and the new version (**B**, treatment) to the other half, then compares a metric. Because users are assigned **at random**, any difference beyond chance is **caused** by the change. Most of the work is **before** the test (choosing the metric and sample size) and in avoiding the classic traps.

**Words to know:**

- **Control / treatment (variant):** the current experience / the new one.
- **Randomisation unit:** what you randomise: users (most common), sessions, or whole cities.
- **Primary metric (OEC, overall evaluation criterion):** the one metric that decides the test (conversion rate, revenue per user).
- **Guardrail metrics:** metrics that must **not** get worse (page load time, refunds, unsubscribes).
- **Baseline:** the control's current metric value (4% conversion).
- **MDE (minimum detectable effect):** the smallest change worth detecting (+0.5 percentage points).
- **Absolute vs relative lift:** 4.0% → 4.5% is +0.5 points absolute, +12.5% relative.
- **Power (1 − β):** the probability of detecting the MDE if it's real; usually 80%.
- **Sample size calculation (power analysis):** working out how many users you need for a given baseline, MDE, α and power.
- **Peeking:** checking results repeatedly and stopping as soon as p < 0.05. Inflates false positives dramatically.
- **Sequential testing:** methods designed for looking at results early without inflating errors.
- **SRM (sample ratio mismatch):** the groups' sizes differ from the planned split (e.g. 50.8% / 49.2% on a huge test): a sign of a bug in assignment or logging. Checked with a chi-square test.
- **Novelty effect:** users react to anything new at first, then settle down. **Primacy effect:** users resist change at first.
- **Network effects / interference:** one user's treatment affects another's (marketplaces, social apps), breaking the "independent groups" assumption.
- **CUPED:** a variance-reduction technique using each user's pre-experiment behaviour to make tests more sensitive.
- **Conversion rate:** the share of users who complete a goal action (orders ÷ visitors).

**Everyday picture.** A farmer testing a new fertiliser plants half the field with it, **chosen by coin flips**, not "the sunny half". Coin flips mean sun, soil and water are balanced between halves on average, so a difference in harvest is due to the fertiliser. Choosing "the sunny half" would make any comparison meaningless.

**The A/B testing process:**

1. **Hypothesis:** "Showing delivery dates on product pages will increase conversion."
2. **Metric:** primary = conversion rate (orders ÷ visitors); guardrails = page speed, refund rate.
3. **Design:** randomise by user, 50/50 split, α = 0.05, power = 80%, MDE = +0.5 points on a 4% baseline.
4. **Sample size:** compute it (below) and the **duration** (sample size ÷ daily traffic, rounded up to **whole weeks** to cover weekday/weekend cycles).
5. **Run:** don't peek-and-stop; monitor only for bugs and guardrail disasters; check **SRM** early.
6. **Analyse:** the pre-planned test on the primary metric; effect size with a CI; guardrails; segments only as exploration.
7. **Decide:** ship, iterate or drop, considering practical significance and costs.
8. **Document** the result, including failures (they prevent repeated mistakes).

**Sample size, traced** (two proportions, 4.0% → 4.5%, α = 0.05 two-sided, power 80%): a common approximation is n per group ≈ (z₁₋α/₂ + z₁₋β)² × [p₁(1 − p₁) + p₂(1 − p₂)] / (p₂ − p₁)² = (1.96 + 0.84)² × (0.0384 + 0.0430) / 0.000025 = 7.84 × 0.0814 / 0.000025 ≈ **25,500 users per group**. Halving the MDE to +0.25 points needs about **4×** as many. With 5,000 visitors a day split in two, 25,500 per group takes about 11 days → run **2 full weeks**.

**Why peeking breaks the test:** each look is another chance for noise to cross p < 0.05. Checking daily for 20 days and stopping at the first "significant" result can push the false-positive rate from 5% to 25% or more. Decide the sample size up front, or use a **sequential** method built for peeking.

**Analysis checklist:**

| Check | How |
|---|---|
| SRM | chi-square of observed group sizes vs the planned split; p < 0.001 → investigate before trusting anything |
| primary metric | two-proportion z-test (rates) or Welch t-test (means), with a CI on the lift |
| guardrails | the same tests; a significant harm blocks the launch |
| segments | explore (new vs returning, mobile vs desktop) but treat as hypotheses for the next test |
| novelty | compare week 1 with week 2 |

**When not to A/B test:** too little traffic to reach the needed sample size in reasonable time; obvious bug fixes; changes with strong network effects (use cluster or switchback designs); decisions that can't be reversed. Alternatives: qualitative research, before/after with care, quasi-experiments.

**Common mistakes:**

- ❌ Peeking and stopping at the first p < 0.05.
- ❌ No sample-size calculation, then calling an under-powered test "no effect".
- ❌ Randomising by page view instead of user (the same person sees both versions).
- ❌ Changing the metric after seeing results; slicing 30 segments until one is significant.
- ❌ Ignoring SRM: a broken split invalidates the whole test.
- ❌ Running for 3 days (misses weekly cycles; over-weights the novelty effect).

**Used in real software:** every major tech company runs thousands of experiments a year (Microsoft, Google, Amazon, Netflix, Booking, Uber); platforms such as Optimizely, Statsig, Eppo, GrowthBook and LaunchDarkly implement exactly this workflow.

### Python

```python
import numpy as np
from statsmodels.stats.power import NormalIndPower
from statsmodels.stats.proportion import proportion_effectsize, proportions_ztest, confint_proportions_2indep
from scipy import stats

baseline, target = 0.040, 0.045
effect = proportion_effectsize(target, baseline)              # Cohen's h, a standardised difference for rates
n = NormalIndPower().solve_power(effect_size=effect, alpha=0.05, power=0.8, alternative="two-sided")
print(f"Cohen's h {effect:.4f} → {np.ceil(n):,.0f} users per group")
for mde in (0.0025, 0.005, 0.01):
    h = proportion_effectsize(baseline + mde, baseline)
    print(f"MDE +{mde:.2%} points → {np.ceil(NormalIndPower().solve_power(h, alpha=0.05, power=0.8)):>9,.0f} per group")
print("days at 5,000 visitors/day:", int(np.ceil(2 * n / 5000)))
```

**Output:**

```text
Cohen's h 0.0248 → 25,531 users per group
MDE +0.25% points →    99,310 per group
MDE +0.50% points →    25,531 per group
MDE +1.00% points →     6,726 per group
days at 5,000 visitors/day: 11
```

`proportion_effectsize` converts two rates into **Cohen's h**, the standardised effect size that power calculations for proportions use; `solve_power` finds whichever input you leave out (here the sample size). It agrees with the hand formula above to within a few users.

```python
rng = np.random.default_rng(2)
n_a, n_b = 25_620, 25_480                                     # users actually assigned
conv_a = rng.binomial(n_a, 0.040)
conv_b = rng.binomial(n_b, 0.0455)
print(f"A: {conv_a}/{n_a} = {conv_a / n_a:.3%}   B: {conv_b}/{n_b} = {conv_b / n_b:.3%}")

srm_p = stats.chisquare([n_a, n_b], f_exp=[(n_a + n_b) / 2] * 2).pvalue
print(f"SRM check p = {srm_p:.3f} ({'OK' if srm_p > 0.001 else 'INVESTIGATE'})")

z, p = proportions_ztest([conv_b, conv_a], [n_b, n_a])
lo, hi = confint_proportions_2indep(conv_b, n_b, conv_a, n_a, method="wald")
lift = conv_b / n_b - conv_a / n_a
print(f"lift {lift:+.3%} points ({lift / (conv_a / n_a):+.1%} relative), z = {z:.2f}, p = {p:.4f}, 95% CI ({lo:+.3%}, {hi:+.3%})")
```

**Output:**

```text
A: 1028/25620 = 4.012%   B: 1144/25480 = 4.490%
SRM check p = 0.536 (OK)
lift +0.477% points (+11.9% relative), z = 2.67, p = 0.0075, 95% CI (+0.127%, +0.827%)
```

```python
def run_with_peeking(rng, days=20, per_day=1000, p=0.04):
    a = b = conv_a = conv_b = 0
    for _ in range(days):
        a += per_day; b += per_day
        conv_a += rng.binomial(per_day, p); conv_b += rng.binomial(per_day, p)    # NO real difference
        if proportions_ztest([conv_b, conv_a], [b, a])[1] < 0.05:
            return True                                       # stopped early on a "win"
    return False

r = np.random.default_rng(1)
peek_rate = np.mean([run_with_peeking(r) for _ in range(1_000)])
print(f"false-positive rate with daily peeking: {peek_rate:.1%} (should be 5%)")
```

**Output:**

```text
false-positive rate with daily peeking: 25.1% (should be 5%)
```

With no real difference at all, stopping at the first daily p < 0.05 "finds" a winner far more often than 5% of the time.

```python
import matplotlib.pyplot as plt

sizes = np.linspace(1_000, 60_000, 100)
fig, ax = plt.subplots(figsize=(8, 3.6), layout="constrained")
for mde, color in [(0.0025, "tab:red"), (0.005, "tab:blue"), (0.01, "tab:green")]:
    h = proportion_effectsize(baseline + mde, baseline)
    power = NormalIndPower().power(h, nobs1=sizes, alpha=0.05)
    ax.plot(sizes, power, color=color, label=f"lift +{mde:.2%} points")
ax.axhline(0.8, color="gray", ls="--", lw=1)
ax.text(1_500, 0.82, "80% power", color="gray")
ax.set(title="Power vs users per group (baseline 4% conversion, α = 0.05)", xlabel="users per group", ylabel="power")
ax.legend(loc="lower right")
fig.savefig("power-curve.png", dpi=100)
plt.close(fig)
print("power with 10,000 per group for +0.5 points:", round(float(NormalIndPower().power(effect, nobs1=10_000, alpha=0.05)), 2))
```

**Output:**

```text
power with 10,000 per group for +0.5 points: 0.42
```

With only 10,000 users per group, a real +0.5-point lift would be detected less than half the time: an under-powered test that "finds nothing" tells you very little.

### Practice

1. Baseline revenue per user is ₹220 with std ₹600. How many users per group to detect a ₹15 increase with 80% power? (Hint: Cohen's d = 15 / 600; use `TTestIndPower().solve_power`.)
2. A test assigned 50,912 users to A and 49,088 to B on a planned 50/50 split. Run the SRM check. What do you do?

<details>
<summary><b>Answer</b></summary>

```python
from statsmodels.stats.power import TTestIndPower
print(f"{np.ceil(TTestIndPower().solve_power(effect_size=15 / 600, alpha=0.05, power=0.8)):,.0f} per group")
print(f"SRM p = {stats.chisquare([50_912, 49_088]).pvalue:.1e}")
```

**Output:**

```text
25,118 per group
SRM p = 8.0e-09
```

1. About 25,000 users per group: revenue is noisy (std ≫ mean), so small lifts need large samples. Variance-reduction methods such as CUPED help.
2. The p-value is tiny: the split is broken. Don't analyse the metric; find the cause first (a redirect dropping users in one variant, bot filtering, logging differences).

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [296. Calculate Statistical Power for Experiment Design](https://www.deep-ml.com/problems/296) | 🟡 Medium |
| 2 | [211. Two-Sample T-Test Implementation](https://www.deep-ml.com/problems/211) | 🔴 Hard |

**Learn more:** [Kohavi, Tang and Xu: Trustworthy Online Controlled Experiments (book site)](https://experimentguide.com/) · [Evan Miller: how not to run an A/B test](https://www.evanmiller.org/how-not-to-run-an-ab-test.html) · [Evan Miller: sample size calculator](https://www.evanmiller.org/ab-testing/sample-size.html)

---

## 59. Regression for Analysis: statsmodels, Coefficients and Confidence

![A fitted regression line with its 95% confidence band for the mean and the wider prediction band for individual orders](images/data-science/regression-bands.png)

### Theory

> **In simple words:** **linear regression** fits a straight line (or a flat surface, with several inputs) through data: y ≈ intercept + slope × x. In **analysis**, the goal is to **understand**: how much does y change per unit of x, holding other things equal, and how sure are we? **statsmodels** prints a regression table answering exactly that, with confidence intervals and p-values for every coefficient. (Using regression to **predict** is covered in `machine-learning.md`.)

**Words to know:**

- **Regression:** modelling how an outcome depends on one or more inputs.
- **Dependent variable (outcome, response, y):** what you're explaining (sales).
- **Independent variables (predictors, features, x):** what you explain it with (price, ad spend).
- **Coefficient (β, "beta"):** how much y changes when that x rises by 1, **holding the other x's constant**.
- **Intercept:** the predicted y when every x is 0 (often not meaningful on its own).
- **Residual:** actual y − predicted y for one row: what the model missed.
- **OLS (ordinary least squares):** the standard method: choose coefficients that minimise the **sum of squared residuals**.
- **R² (R-squared):** the share of y's variance the model explains (0 to 1). **Adjusted R²** penalises adding useless predictors.
- **Standard error of a coefficient:** how uncertain the coefficient is; its 95% CI is roughly coefficient ± 2 SE.
- **Dummy (indicator) variable:** a 0/1 column for a category (is_weekend). With k categories, use k − 1 dummies; the left-out one is the **reference** that others are compared with.
- **Interaction:** the effect of x₁ depends on x₂ (ads work better on weekends): modelled with x₁ × x₂.
- **Multicollinearity:** predictors so correlated with each other that their separate effects can't be pinned down (huge SEs). Checked with the **VIF** (variance inflation factor).
- **Confounding (again):** a regression can "control for" confounders **you include**; it can't fix ones you didn't measure.
- **Logistic regression:** the version for yes/no outcomes; coefficients are in **log-odds** (exponentiate them to get **odds ratios**).
- **Formula interface:** writing a model as text: `"sales ~ price + ads + C(city)"` (`C()` marks a categorical column).

**Everyday picture.** A sales manager asks: "If we spend ₹1,000 more on ads, how many more units do we sell, taking into account that we also discount on weekends?" Regression separates the tangled effects of ads, discounts and weekends, like listening to one instrument in a band.

**Simple regression, traced by hand** for x = `[1, 2, 3, 4, 5]`, y = `[2, 4, 5, 4, 5]` (from Section [52](#52-correlation-covariance-and-causation): Σ(x − x̄)(y − ȳ) = 6 and Σ(x − x̄)² = 10):

- slope = 6 / 10 = **0.6**
- intercept = ȳ − slope × x̄ = 4 − 0.6 × 3 = **2.2**
- line: y ≈ 2.2 + 0.6x. At x = 4, predicted 4.6; actual 4; residual −0.6.

**Reading a regression table:**

| Column | Meaning | How to read it |
|---|---|---|
| `coef` | the estimated effect | "+3.1 units per ₹1,000 of ads, others held constant" |
| `std err` | its uncertainty | smaller = more precise |
| `t`, `P>\|t\|` | test of "coef = 0" | p < 0.05: evidence of a non-zero effect |
| `[0.025  0.975]` | 95% CI for the coef | the range of plausible effects |
| `R-squared` | variance explained | context-dependent; 0.3 can be useful for noisy behaviour |
| `No. Observations` | rows used | check nothing was silently dropped |

**Confidence band vs prediction band (the picture above):** the **confidence band** is the uncertainty in the **average** y at each x (narrow with lots of data); the **prediction band** is where **individual** new observations will fall (always wider, because individuals vary around the average).

**Assumptions to check:** a roughly linear relationship (plot it); residuals with constant spread and no pattern (plot residuals vs fitted values); independent observations; no extreme points dominating the fit. Violations don't always ruin the analysis, but they change how much you can trust the p-values; **robust standard errors** (`cov_type="HC3"`) help when the spread isn't constant.

**When to use regression for analysis:** estimating the effect of one factor while adjusting for others; quantifying relationships with uncertainty; marketing mix models; analysing experiments with covariates. **When not to:** to prove causation from observational data with unmeasured confounders; with strongly non-linear relationships (transform variables or use ML models).

**Common mistakes:**

- ❌ Reading a coefficient as causal without an experiment or a strong design.
- ❌ Forgetting "holding the others constant" when interpreting.
- ❌ Including every category as a dummy plus the intercept (the **dummy variable trap**: perfectly collinear). ✅ k − 1 dummies; the formula interface does it for you.
- ❌ Extrapolating far beyond the range of the data.
- ❌ Judging a model only by R².

**Used in real software:** marketing mix modelling (how much each channel drives sales), pricing studies (price elasticity), economics and social science, analysing A/B tests with pre-period covariates (the idea behind CUPED), and as the baseline every ML model must beat.

### Python

```python
import numpy as np
import pandas as pd
import statsmodels.formula.api as smf

x, y = np.array([1, 2, 3, 4, 5]), np.array([2, 4, 5, 4, 5])
slope = ((x - x.mean()) * (y - y.mean())).sum() / ((x - x.mean()) ** 2).sum()
print(f"by hand: y = {y.mean() - slope * x.mean():.2f} + {slope:.2f}x | numpy polyfit: {np.polyfit(x, y, 1).round(2)}")

rng = np.random.default_rng(8)
n = 300
df = pd.DataFrame({"ads_k": rng.uniform(0, 20, n).round(1),           # ad spend, ₹ thousands
                   "price": rng.uniform(80, 120, n).round(),
                   "weekend": rng.integers(0, 2, n),
                   "city": rng.choice(["Pune", "Mumbai", "Delhi"], n)})
city_effect = df["city"].map({"Pune": 0, "Mumbai": 15, "Delhi": -10})
df["units"] = (200 + 3.0 * df["ads_k"] - 1.2 * df["price"] + 25 * df["weekend"] + city_effect
               + rng.normal(0, 12, n)).round()

model = smf.ols("units ~ ads_k + price + weekend + C(city)", data=df).fit()
print(model.summary().tables[1])
print(f"R² = {model.rsquared:.3f}, adjusted R² = {model.rsquared_adj:.3f}, n = {int(model.nobs)}")
```

**Output:**

```text
by hand: y = 2.20 + 0.60x | numpy polyfit: [0.6 2.2]
=====================================================================================
                        coef    std err          t      P>|t|      [0.025      0.975]
-------------------------------------------------------------------------------------
Intercept           186.5535      6.613     28.209      0.000     173.538     199.569
C(city)[T.Mumbai]    24.3672      1.636     14.893      0.000      21.147      27.587
C(city)[T.Pune]      12.1280      1.590      7.627      0.000       8.998      15.258
ads_k                 3.1732      0.117     27.140      0.000       2.943       3.403
price                -1.1933      0.063    -18.901      0.000      -1.318      -1.069
weekend              24.5570      1.322     18.574      0.000      21.955      27.159
=====================================================================================
R² = 0.865, adjusted R² = 0.862, n = 300
```

The data were generated with known effects (+3.0 per ₹1k of ads, −1.2 per rupee of price, +25 on weekends, Mumbai +15 and Delhi −10 versus Pune), and the regression recovers each one within its confidence interval. `C(city)` created two dummies. The **reference** category is the first alphabetically, **Delhi**, so `C(city)[T.Mumbai]` means "Mumbai compared with Delhi" (the true gap is 15 − (−10) = +25) and `C(city)[T.Pune]` means "Pune compared with Delhi" (+10).

```python
import matplotlib.pyplot as plt

simple = smf.ols("units ~ ads_k", data=df).fit()
grid = pd.DataFrame({"ads_k": np.linspace(0, 20, 50)})
pred = simple.get_prediction(grid).summary_frame(alpha=0.05)
print(pred[["mean", "mean_ci_lower", "mean_ci_upper", "obs_ci_lower", "obs_ci_upper"]].iloc[[0, 25, 49]].round(1))

fig, ax = plt.subplots(figsize=(8, 3.8), layout="constrained")
ax.scatter(df["ads_k"], df["units"], s=10, alpha=0.4, color="gray")
ax.plot(grid["ads_k"], pred["mean"], color="tab:blue", lw=2, label="fitted line")
ax.fill_between(grid["ads_k"], pred["mean_ci_lower"], pred["mean_ci_upper"], color="tab:blue", alpha=0.35, label="95% CI for the mean")
ax.fill_between(grid["ads_k"], pred["obs_ci_lower"], pred["obs_ci_upper"], color="tab:blue", alpha=0.1, label="95% prediction interval")
ax.set(title="Units vs ad spend: confidence band (mean) vs prediction band (individual days)", xlabel="ad spend (₹ thousands)", ylabel="units")
ax.legend(loc="upper left", fontsize=8)
fig.savefig("regression-bands.png", dpi=100)
plt.close(fig)

robust = smf.ols("units ~ ads_k + price + weekend + C(city)", data=df).fit(cov_type="HC3")
print("ads_k SE, classic vs robust:", round(model.bse["ads_k"], 4), round(robust.bse["ads_k"], 4))
```

**Output:**

```text
     mean  mean_ci_lower  mean_ci_upper  obs_ci_lower  obs_ci_upper
0    90.2           84.7           95.7          42.6         137.7
25  124.6          121.9          127.4          77.3         171.9
49  157.7          152.1          163.3         110.2         205.3
ads_k SE, classic vs robust: 0.1169 0.1167
```

`get_prediction(...).summary_frame()` returns the fitted mean, its confidence interval (`mean_ci_*`) and the prediction interval for new observations (`obs_ci_*`). The prediction band is far wider: individual days vary much more than the average does.

```python
df["converted"] = (rng.random(n) < 1 / (1 + np.exp(-(-3 + 0.15 * df["ads_k"] + 0.8 * df["weekend"])))).astype(int)
logit = smf.logit("converted ~ ads_k + weekend", data=df).fit(disp=0)
odds = pd.DataFrame({"coef (log-odds)": logit.params, "odds ratio": np.exp(logit.params),
                     "p": logit.pvalues}).round(3)
print(odds)
```

**Output:**

```text
           coef (log-odds)  odds ratio      p
Intercept           -2.305       0.100  0.000
ads_k                0.102       1.107  0.000
weekend              0.360       1.434  0.187
```

In logistic regression, `exp(coef)` is an **odds ratio**: each extra ₹1k of ads multiplies the odds of converting by about 1.1. The weekend estimate (odds × 1.4) is **not** significant (p ≈ 0.19), although the data were generated with a real weekend effect (odds × e^0.8 ≈ 2.2): with only 300 rows and few conversions, the test lacks power. A non-significant result is "not enough evidence", not "no effect". (`disp=0` hides the fitting progress messages.)

### Practice

1. Refit the model without `price`. Does the `ads_k` coefficient change much? Why (or why not)? (Hint: are ads and price correlated in this data?)
2. Add an interaction `ads_k:weekend` and interpret its coefficient.

<details>
<summary><b>Answer</b></summary>

```python
no_price = smf.ols("units ~ ads_k + weekend + C(city)", data=df).fit()
print(round(model.params["ads_k"], 3), round(no_price.params["ads_k"], 3), round(df[["ads_k", "price"]].corr().iloc[0, 1], 3))
inter = smf.ols("units ~ ads_k * weekend + price + C(city)", data=df).fit()
print(inter.params[["ads_k", "weekend", "ads_k:weekend"]].round(3).to_dict(), round(inter.pvalues["ads_k:weekend"], 3))
```

**Output:**

```text
3.173 3.209 -0.012
{'ads_k': 3.158, 'weekend': 24.29, 'ads_k:weekend': 0.027} 0.909
```

1. Barely: price and ad spend were generated independently (correlation ≈ 0), so leaving price out doesn't bias the ads effect, it just adds noise. If they were correlated (say, ads ran mostly during discounts), dropping price **would** bias the ads coefficient: that's confounding.
2. `ads_k * weekend` expands to `ads_k + weekend + ads_k:weekend`. The interaction is small and not significant: the data were generated with the same ads effect on weekdays and weekends.

</details>

| # | Problem (Deep-ML) | Difficulty |
|---|---|---|
| 1 | [14. Linear Regression Using Normal Equation](https://www.deep-ml.com/problems/14) | 🟢 Easy |
| 2 | [15. Linear Regression Using Gradient Descent](https://www.deep-ml.com/problems/15) | 🟢 Easy |

**Learn more:** [statsmodels: regression with formulas](https://www.statsmodels.org/stable/example_formulas.html) · [OpenIntro Statistics, chapters 8–9 (regression)](https://www.openintro.org/book/os/) · [StatQuest: linear regression (video)](https://www.youtube.com/watch?v=nk2CQITm_eo)

---

### ✅ Part 8 checkpoint

Without looking, can you:

- [ ] Choose between mean/std and median/IQR for a column, and explain why with an example?
- [ ] Compute Pearson's r by hand for five points, and explain confounding, reverse causation and Simpson's paradox?
- [ ] Solve the disease-test problem with counts out of 10,000 and with Bayes' rule?
- [ ] Name the distribution for conversions, orders per minute, waiting times, heights and incomes, and use `cdf`/`ppf`?
- [ ] Explain the CLT, the difference between std and SE, and why 4× the data halves the error?
- [ ] Build a t-interval for a mean, a Wilson interval for a rate and a bootstrap interval for a median, and say what "95% confidence" means?
- [ ] Pick the right test for a question, compute a p-value by permutation, and list four things a p-value is not?
- [ ] Design an A/B test with a sample-size calculation, check SRM, and explain why peeking inflates false positives?
- [ ] Read a regression table: coefficients, CIs, p-values, R², dummies, and confidence vs prediction bands?

You now have every tool. Part 9 puts them together on complete, realistic projects.

---

# Part 9 — Advanced: Data Science in Practice

> **Goal:** Put everything together: run a complete exploratory analysis and write up the findings, turn raw tables into model-ready features without leakage, build a small but production-shaped data pipeline with quality checks, communicate results so people act on them, and know the modern tooling landscape.  
> **You need:** Parts 1–8.

---

## 60. A Complete Exploratory Data Analysis (EDA)

![Pair plot of proline, flavanoids and colour intensity, coloured by cultivar: three fairly separate clusters](images/data-science/eda-pairplot.png)

### Theory

> **In simple words:** **EDA** is getting to know a dataset **before** drawing conclusions or training models: what's in it, what's wrong with it, and what patterns stand out. It combines everything so far: pandas to inspect and summarise, charts to see, and statistics to check that patterns aren't just noise. It ends with **written findings**, not just charts.

**Words to know:**

- **EDA (exploratory data analysis):** open-ended investigation of a dataset to understand it, find problems and form hypotheses.
- **Data dictionary:** a document describing every column: meaning, unit, type, allowed values, source.
- **Univariate / bivariate / multivariate analysis:** looking at one column alone / two together / many at once.
- **Target (label, outcome):** the column you want to predict or explain.
- **Class balance:** how evenly the target's categories are represented.
- **Hypothesis (in EDA):** a pattern you've noticed and want to test properly later.
- **ANOVA F-score (as a screening tool):** how different a numeric column's averages are across groups, relative to the spread inside groups. High F = the column separates the groups well (Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests)).
- **Profiling report:** an automatically generated overview of every column (tools such as `ydata-profiling`, `skimpy`).

**Everyday picture.** A doctor's first appointment with a new patient: take the history (context), check vital signs (structure, quality), examine each system (each column), look at how things interact (relationships), and only then write a diagnosis and plan. Skipping straight to treatment (modelling) is how mistakes happen.

**The EDA checklist** (reuse it on every dataset):

| Step | Questions | Tools |
|---|---|---|
| 1. Context | What does a row represent? What does each column mean? What question are we answering? Who's missing from this data? | data dictionary, talk to the data owner |
| 2. Structure | How many rows and columns? Are the types right? | `shape`, `dtypes`, `head`, `info` |
| 3. Quality | Missing values? Duplicates? Impossible values? Inconsistent categories? | `isna`, `duplicated`, `describe`, `value_counts` (Part 4) |
| 4. Univariate | What does each column look like? Skewed? Outliers? Rare categories? | histograms, box plots, `describe`, `skew` |
| 5. Target | How is the target distributed? Balanced classes? | `value_counts(normalize=True)`, histogram |
| 6. Bivariate | Which columns relate to the target and to each other? | grouped means, box plots by group, correlations, scatter |
| 7. Multivariate | Do patterns hold within subgroups? Clusters? Redundant features? | heatmaps, pair plots, facets |
| 8. Findings | What's true, what's broken, what to do next? | a short written list |

**Good findings are:** specific ("cultivar A has ~2× the proline of B and C"), quantified, tied to the question, and paired with a next step. Separate **facts** (what the data shows) from **hypotheses** (what might explain it).

**The dataset here:** the classic **wine** dataset bundled with scikit-learn (no download needed): 178 wines from three grape cultivars grown in the same region of Italy, with 13 chemical measurements each. The question: **which measurements tell the three cultivars apart?** (`machine-learning.md` then trains a classifier on it.)

**When to stop exploring:** when you can answer the question, or you've written down the hypotheses to test next. Exploration without a question expands forever.

**Common mistakes:**

- ❌ Jumping straight to modelling.
- ❌ Dozens of charts, no question, no written conclusions.
- ❌ In ML projects, exploring the **test** set too. Split first; explore only the training part, so your decisions aren't shaped by the data you'll evaluate on.
- ❌ Reporting a pattern from the full data that disappears within subgroups (Simpson's paradox, Section [52](#52-correlation-covariance-and-causation)).

**Used in real software:** the first week of every data-science project; Kaggle competition notebooks; data-quality reviews before a dashboard goes live; model-monitoring investigations when performance drops.

### Python

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
from scipy import stats
from sklearn.datasets import load_wine

wine = load_wine(as_frame=True).frame
wine = wine.rename(columns={"od280/od315_of_diluted_wines": "od280", "target": "cultivar"})
wine["cultivar"] = wine["cultivar"].map({0: "A", 1: "B", 2: "C"}).astype("category")

print(wine.shape)
print("missing values:", int(wine.isna().sum().sum()), "| duplicate rows:", int(wine.duplicated().sum()))
print(wine["cultivar"].value_counts(normalize=True).sort_index().round(3).to_dict())
print(wine.describe().T[["mean", "std", "min", "max"]].round(2))
```

**Output:**

```text
(178, 14)
missing values: 0 | duplicate rows: 0
{'A': 0.331, 'B': 0.399, 'C': 0.27}
                        mean     std     min      max
alcohol                13.00    0.81   11.03    14.83
malic_acid              2.34    1.12    0.74     5.80
ash                     2.37    0.27    1.36     3.23
alcalinity_of_ash      19.49    3.34   10.60    30.00
magnesium              99.74   14.28   70.00   162.00
total_phenols           2.30    0.63    0.98     3.88
flavanoids              2.03    1.00    0.34     5.08
nonflavanoid_phenols    0.36    0.12    0.13     0.66
proanthocyanins         1.59    0.57    0.41     3.58
color_intensity         5.06    2.32    1.28    13.00
hue                     0.96    0.23    0.48     1.71
od280                   2.61    0.71    1.27     4.00
proline               746.89  314.91  278.00  1680.00
```

The data is clean (no missing values or duplicates), and the classes are reasonably balanced (33% / 40% / 27%). Note the very different **scales**: `magnesium` around 100, `hue` around 1, `proline` up to 1,680. That matters for many ML models (Section [61](#61-feature-engineering-preparing-data-for-machine-learning)).

```python
numeric = wine.columns.drop("cultivar")
print("most skewed:", wine[numeric].skew().sort_values(ascending=False).round(2).head(3).to_dict())

f_scores = {col: stats.f_oneway(*[g[col] for _, g in wine.groupby("cultivar", observed=True)]).statistic
            for col in numeric}                                   # ANOVA F: how different are the group means?
ranking = pd.Series(f_scores).sort_values(ascending=False).round(0)
print(ranking.head(5).to_dict())
print(wine.groupby("cultivar", observed=True)[["flavanoids", "proline", "od280", "alcohol", "color_intensity"]].mean().round(2))
```

**Output:**

```text
most skewed: {'magnesium': 1.1, 'malic_acid': 1.04, 'color_intensity': 0.87}
{'flavanoids': 234.0, 'proline': 208.0, 'od280': 190.0, 'alcohol': 135.0, 'color_intensity': 121.0}
          flavanoids  proline  od280  alcohol  color_intensity
cultivar                                                      
A               2.98  1115.71   3.16    13.74             5.53
B               2.08   519.51   2.79    12.28             3.09
C               0.78   629.90   1.68    13.15             7.40
```

The ANOVA F-score ranks each measurement by how strongly the three cultivars' means differ relative to the spread inside each group. `flavanoids`, `proline`, `od280` and `alcohol` separate the cultivars best.

```python
sns.set_theme(style="whitegrid")
fig, axes = plt.subplots(1, 3, figsize=(11, 3.4), layout="constrained")
for ax, col in zip(axes, ["proline", "flavanoids", "color_intensity"]):
    sns.boxplot(data=wine, x="cultivar", y=col, hue="cultivar", legend=False, ax=ax)
    ax.set_title(f"{col} by cultivar")
fig.savefig("eda-boxplots.png", dpi=100)
plt.close(fig)

fig, ax = plt.subplots(figsize=(7, 5.5), layout="constrained")
top = ranking.index[:7].tolist()
sns.heatmap(wine[top].corr().round(2), annot=True, cmap="RdBu", vmin=-1, vmax=1, ax=ax)
ax.set_title("Correlations among the most useful measurements")
fig.savefig("eda-heatmap.png", dpi=100)
plt.close(fig)

grid = sns.pairplot(wine, vars=["proline", "flavanoids", "color_intensity"], hue="cultivar", height=2.2, corner=True)
grid.savefig("eda-pairplot.png", dpi=90)
plt.close(grid.figure)
print("flavanoids ~ total_phenols r =", round(wine["flavanoids"].corr(wine["total_phenols"]), 2))
```

**Output:**

```text
flavanoids ~ total_phenols r = 0.86
```

![Box plots of proline, flavanoids and colour intensity for each of the three cultivars](images/data-science/eda-boxplots.png)

![Correlation heatmap of the seven most useful measurements](images/data-science/eda-heatmap.png)

**Findings (what you'd write in the notebook):**

1. **Clean data:** 178 rows, 13 numeric features, no missing values or duplicates; classes 59 / 71 / 48, no severe imbalance.
2. **Cultivar A** has high `proline` (≈1,116 vs ≈520–630). **Cultivar C** has low `flavanoids` (≈0.78) and high `color_intensity` (≈7.4). Two or three measurements already separate the groups well (the pair plot shows three fairly distinct clusters).
3. **Redundancy:** `flavanoids`, `total_phenols` and `od280` are strongly correlated (r ≈ 0.7–0.86); a model may need only one or two of them.
4. **Scales differ by three orders of magnitude** (`proline` vs `hue`): scale features before distance-based models.
5. **Next steps:** train a simple classifier on these features with a proper train/test split (`machine-learning.md`); check whether 2–3 features are enough.

### Practice

1. Which cultivar has the highest average `color_intensity`, and by how much does it exceed the lowest?
2. Is `alcohol` normally distributed within cultivar B? Use `stats.shapiro` and a histogram, and say what the p-value means here.

<details>
<summary><b>Answer</b></summary>

```python
ci = wine.groupby("cultivar", observed=True)["color_intensity"].mean().round(2)
print(ci.idxmax(), ci.max(), "vs lowest", ci.idxmin(), ci.min())
b_alcohol = wine.loc[wine["cultivar"] == "B", "alcohol"]
print("Shapiro-Wilk p =", round(stats.shapiro(b_alcohol).pvalue, 3))
```

**Output:**

```text
C 7.4 vs lowest B 3.09
Shapiro-Wilk p = 0.114
```

2. Shapiro–Wilk's null hypothesis is "the data come from a normal distribution". A large p-value means no evidence against normality (not proof of it); a small one means the shape departs noticeably from a bell curve. Always look at the histogram too: with big samples the test flags tiny, harmless departures.

</details>

| # | Problem | Difficulty |
|---|---|---|
| 1 | [Kaggle: Titanic, a classic first EDA dataset](https://www.kaggle.com/competitions/titanic) | 🟢 Easy |
| 2 | [Kaggle: House Prices, EDA plus feature engineering](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques) | 🟡 Medium |
| 3 | [LeetCode 1158. Market Analysis I](https://leetcode.com/problems/market-analysis-i/) | 🟡 Medium |

**Learn more:** [Kaggle Learn: data visualization](https://www.kaggle.com/learn/data-visualization) · [UCI: wine dataset description](https://archive.ics.uci.edu/dataset/109/wine) · [ydata-profiling](https://docs.profiling.ydata.ai/)

---

## 61. Feature Engineering: Preparing Data for Machine Learning

![Split first: statistics such as medians, scales and category lists are learned from the training rows only, then applied to both sets](images/data-science/61-split-first.svg)

### Theory

> **In simple words:** a machine-learning model learns from a table of **features** (inputs, called **X**) to predict a **target** (the answer, called **y**). Models only understand **numbers**, most can't handle missing values, and many are thrown off by very different scales. **Feature engineering** turns raw columns (and raw tables like order logs) into good numeric inputs, and it often improves results more than choosing a fancier model.

**Words to know:**

- **Feature (predictor, input, X):** a column the model uses. **Target (label, y):** what it predicts.
- **Training set / test set:** rows the model learns from / rows kept aside to measure performance honestly.
- **Data leakage:** information from the test set (or from the future) sneaking into training, making the model look better than it will be in real use.
- **Fit / transform:** **fit** = learn numbers from data (a median, a mean, a category list); **transform** = apply them. Fit on training rows only; transform both.
- **Encoding:** turning categories into numbers.
  - **One-hot encoding:** one 0/1 column per category.
  - **Ordinal encoding:** ordered integers for ordered categories.
  - **Frequency encoding:** each category replaced by how common it is.
  - **Target encoding:** each category replaced by the average target for that category (with smoothing).
- **Smoothing (target encoding):** pulling small categories' averages towards the overall average, because averages of a few rows are noisy.
- **Scaling:** putting numeric features on comparable ranges. **Standardisation** = (x − mean) / std; **min–max** = (x − min) / (max − min); **robust** = (x − median) / IQR.
- **Aggregate features:** summaries of a customer's history (order count, average spend, days since last order), built with `groupby` from an event table.
- **Interaction feature:** a combination of two features (price × quantity, ratio of two counts).
- **Cardinality:** the number of distinct values (high cardinality = thousands of product IDs).
- **Feature store:** a system that computes, stores and serves features consistently for training and live predictions.
- **Churn:** customers leaving (cancelling, or no longer buying); **churn rate** = the share who leave in a period.
- **RFM:** **R**ecency (time since the last purchase), **F**requency (how often), **M**onetary (how much): three classic customer features.

**Everyday picture.** Cooking for a judge who only tastes **purées**: you must peel, chop and blend every ingredient (encode, scale, fill gaps) the **same way** for the practice dish (training) and the competition dish (test). And you can't taste the competition dish while preparing the recipe (leakage).

**The golden rule: split first, then learn anything from the data.** Any value computed **across rows** (a median for filling gaps, a mean and std for scaling, the list of categories, a target average) must be learned from training rows only and then applied to the test rows. Values computed **within one row** (price × qty, day of week) can be done any time.

**Turning categories into numbers:**

| Method | How | Use when | Watch out |
|---|---|---|---|
| **One-hot** | one 0/1 column per category (`pd.get_dummies`, `OneHotEncoder`) | unordered, up to a few dozen categories | many columns; unseen categories at prediction time |
| **Ordinal** | small=0, medium=1, large=2 | ordered categories | never for unordered ones |
| **Frequency** | category → its share of rows | many categories | different categories with equal frequency collide |
| **Target (mean) encoding** | category → smoothed average target | many categories with a strong link to the target | **leaks** unless computed out-of-fold on training data |

**Smoothed target encoding, traced:** overall churn rate 20%. City X has 4 customers, 3 churned (raw 75%). With smoothing strength m = 10: encoded = (3 + 10 × 0.20) / (4 + 10) = 5 / 14 = **35.7%**. The tiny group's extreme rate is pulled towards the average; a city with 1,000 customers would barely move.

**Numeric transformations:**

| Problem | Fix |
|---|---|
| right-skewed (income, price, counts) | `np.log1p(x)` |
| different scales, model uses distances or gradients (k-NN, SVM, linear models, neural networks) | standardise (or min–max); **tree models don't need scaling** |
| outliers distort scaling | robust scaling, or clip at percentiles |
| missing values | fill (median / most frequent / "Unknown") **plus** a 0/1 "was missing" column |
| non-linear effect of age, hour | bins (Section [29](#29-categorical-data-and-binning-cut-and-qcut)), or let a tree model handle it |
| cyclical time (hour 23 is next to hour 0) | sine and cosine of the angle: `sin(2π·hour/24)`, `cos(2π·hour/24)` |

**Feature ideas that usually help:**

- **Date parts:** day of week, month, hour, is_weekend, is_holiday, days since signup, days since last purchase. A raw timestamp alone is rarely useful.
- **Ratios and differences:** price per item, revenue per visit, discount as % of price, change vs last month.
- **Aggregates over history (RFM):** **R**ecency (days since last order), **F**requency (orders in the last 90 days), **M**onetary (spend in the last 90 days). Compute them **as of** the prediction date, using only earlier events.
- **Text:** length, word counts, keyword flags (embeddings from `llm-engineering.md` are far richer).
- **Drop:** IDs, near-constant columns, and anything not known at prediction time (a "refund_issued" column when predicting refunds).

**Point-in-time correctness:** when building features from event logs, each training example must only use events **before** its own prediction date. Using a customer's full history (including after the date you're "predicting") is time-travel leakage, one of the most common reasons models fail after launch.

**Common mistakes:**

- ❌ Scaling or filling on the **whole** dataset before splitting.
- ❌ One-hot encoding train and test separately, so a city missing from test gives them **different columns**. ✅ Fix the column list from training (`reindex`), or `OneHotEncoder(handle_unknown="ignore")`.
- ❌ Ordinal-encoding unordered categories.
- ❌ Target encoding without smoothing or out-of-fold computation (the model memorises the target).
- ❌ Features from the future (aggregates that include events after the prediction date).

**Used in real software:** churn models (RFM features), fraud detection (transaction velocity: number of transactions in the last hour), recommendation (user and item aggregates), credit scoring; production systems use feature stores (Feast, Tecton, Databricks) to compute features identically for training and serving. `machine-learning.md` does all of this with scikit-learn pipelines.

### Python

```python
import numpy as np
import pandas as pd

rng = np.random.default_rng(3)
n = 10
customers = pd.DataFrame({
    "customer_id": range(101, 101 + n),
    "city": rng.choice(["Pune", "Mumbai", "Delhi"], n),
    "plan": rng.choice(["basic", "plus", "premium"], n),
    "monthly_spend": rng.lognormal(7, 0.8, n).round(),
    "signup": pd.to_datetime("2024-01-01") + pd.to_timedelta(rng.integers(0, 400, n), unit="D"),
    "age": [25, 31, np.nan, 45, 38, np.nan, 29, 52, 41, 34],
    "churned": rng.integers(0, 2, n),                    # the target: did the customer leave?
})
train = customers.sample(frac=0.7, random_state=0)      # split FIRST
test = customers.drop(train.index)
print(len(train), "train rows,", len(test), "test rows")

def fit_stats(df):                                       # learn every cross-row number from TRAIN only
    log_spend = np.log1p(df["monthly_spend"])
    return {"age_median": df["age"].median(), "spend_mean": log_spend.mean(), "spend_std": log_spend.std(),
            "city_columns": [f"city_{c}" for c in sorted(df["city"].unique())]}

def transform(df, st):
    out = pd.DataFrame(index=df.index)
    out["age_missing"] = df["age"].isna().astype(int)
    out["age"] = df["age"].fillna(st["age_median"])
    out["log_spend_z"] = (np.log1p(df["monthly_spend"]) - st["spend_mean"]) / st["spend_std"]
    out["plan_level"] = df["plan"].map({"basic": 0, "plus": 1, "premium": 2})          # ordered categories
    out["days_since_signup"] = (pd.Timestamp("2025-06-01") - df["signup"]).dt.days
    out["signup_weekend"] = (df["signup"].dt.dayofweek >= 5).astype(int)
    city = pd.get_dummies(df["city"], prefix="city", dtype=int)
    return out.join(city.reindex(columns=st["city_columns"], fill_value=0))           # same columns every time

st = fit_stats(train)
X_train, y_train = transform(train, st), train["churned"]
X_test, y_test = transform(test, st), test["churned"]
print(X_train.round(2).to_string())
print("same columns in test:", X_test.columns.equals(X_train.columns))
```

**Output:**

```text
7 train rows, 3 test rows
   age_missing   age  log_spend_z  plan_level  days_since_signup  signup_weekend  city_Delhi  city_Mumbai  city_Pune
2            1  36.0        -0.28           1                487               0           0            0          1
8            0  41.0         1.64           0                500               0           0            0          1
4            0  38.0        -1.48           0                140               1           0            0          1
9            0  34.0        -0.16           0                161               1           0            0          1
1            0  31.0        -0.39           1                517               0           0            0          1
6            0  29.0         0.90           2                462               1           1            0          0
7            0  52.0        -0.22           2                392               1           0            1          0
same columns in test: True
```

The test rows went through exactly the same steps, using only numbers learned from the training rows, and ended up with exactly the same columns, which is what a model needs. `to_string()` prints every column without truncation.

```python
orders = pd.DataFrame({
    "customer_id": rng.choice([101, 102, 103], 15),
    "date": pd.to_datetime("2025-01-01") + pd.to_timedelta(rng.integers(0, 180, 15), unit="D"),
    "amount": rng.integers(200, 3000, 15),
})
as_of = pd.Timestamp("2025-05-01")                                   # the prediction date
past = orders[orders["date"] < as_of]                                # point-in-time: only earlier events
rfm = past.groupby("customer_id").agg(
    recency_days=("date", lambda d: (as_of - d.max()).days),
    frequency_90d=("date", lambda d: (d >= as_of - pd.Timedelta(days=90)).sum()),
    monetary_90d=("amount", lambda a: a[past.loc[a.index, "date"] >= as_of - pd.Timedelta(days=90)].sum()),
)
print(rfm)
print("orders after the as-of date that must NOT be used:", int((orders["date"] >= as_of).sum()))

hours = np.array([0, 6, 12, 18, 23])
print(pd.DataFrame({"hour": hours, "sin": np.sin(2 * np.pi * hours / 24).round(2) + 0.0,
                    "cos": np.cos(2 * np.pi * hours / 24).round(2) + 0.0}).to_string(index=False))
```

**Output:**

```text
             recency_days  frequency_90d  monetary_90d
customer_id                                           
101                     3              1          2659
102                    43              5          6424
103                     2              1          2037
orders after the as-of date that must NOT be used: 7
 hour   sin   cos
    0  0.00  1.00
    6  1.00  0.00
   12  0.00 -1.00
   18 -1.00  0.00
   23 -0.26  0.97
```

The sine/cosine pair places hours on a circle: 23:00 and 00:00 get nearly identical values, whereas the raw numbers 23 and 0 look far apart to a model.

```python
churn = pd.DataFrame({"city": ["X"] * 4 + ["Y"] * 50 + ["Z"] * 46,
                      "churned": [1, 1, 1, 0] + [1] * 10 + [0] * 40 + [1] * 9 + [0] * 37})

def target_encode(train_df, col, target, m=10):
    prior = train_df[target].mean()
    g = train_df.groupby(col)[target].agg(["sum", "count"])
    return ((g["sum"] + m * prior) / (g["count"] + m)).rename("encoded")

enc = target_encode(churn, "city", "churned")
summary = churn.groupby("city")["churned"].agg(raw_rate="mean", n="size").join(enc).round(3)
print(f"overall rate {churn['churned'].mean():.3f}", summary, sep="\n")
```

**Output:**

```text
overall rate 0.220
      raw_rate   n  encoded
city                       
X        0.750   4    0.371
Y        0.200  50    0.203
Z        0.196  46    0.200
```

City X's raw rate (75% from 4 customers) is pulled down to about 36%; the big cities barely move. In a real project you'd compute these encodings **out-of-fold** (for each training row, using only the other folds' rows; `machine-learning.md` explains folds) so no row's own target leaks into its feature.

### Practice

1. Add a feature `spend_per_day` (monthly spend ÷ days since signup) to `X_train`. Can this feature cause leakage?
2. Why does computing `rfm` from **all** orders (ignoring `as_of`) make a churn model look better in testing than in production?

<details>
<summary><b>Answer</b></summary>

```python
X_train["spend_per_day"] = (train["monthly_spend"] / X_train["days_since_signup"]).round(2)
print(X_train["spend_per_day"].head(3))
```

**Output:**

```text
2    1.80
8    4.72
4    3.36
Name: spend_per_day, dtype: float64
```

1. It uses only each customer's own row, so it can't leak information between rows; computing it before or after the split gives the same values. Leakage comes from values computed **across rows** (means, medians, scaling factors, category lists, target averages) or from the future.
2. Customers who churned stop ordering, so "days since last order" computed with **future** data perfectly reveals who churned. At prediction time those future orders don't exist yet: the feature is unavailable, and the model's real accuracy is far lower.

</details>

| # | Problem | Difficulty |
|---|---|---|
| 1 | [Deep-ML 112. Min-Max Scaling of Feature Values](https://www.deep-ml.com/problems/112) | 🟢 Easy |
| 2 | [Deep-ML 84. Phi Transformation for Polynomial Features](https://www.deep-ml.com/problems/84) | 🟢 Easy |
| 3 | [Kaggle Learn: Feature Engineering (course)](https://www.kaggle.com/learn/feature-engineering) | 🟡 Medium |

**Learn more:** [Kaggle Learn: data leakage](https://www.kaggle.com/code/alexisbcook/data-leakage) · [scikit-learn: preprocessing data](https://scikit-learn.org/stable/modules/preprocessing.html) · [Feature Engineering and Selection (free book, Kuhn & Johnson)](https://www.feat.engineering/)

---

## 62. Data Pipelines and Data Quality in Production

![A batch pipeline: extract raw data, transform it, validate it, and load it as partitioned Parquet; a failed check stops bad data before it reaches dashboards](images/data-science/62-pipeline.svg)

### Theory

> **In simple words:** a notebook analysis runs once; a **pipeline** runs every day, unattended, and other people depend on its output. That changes the rules: every step must be a function, re-running must be safe, data must be **validated** before anyone sees it, and problems must stop the pipeline loudly instead of quietly publishing wrong numbers.

**Words to know:**

- **Data pipeline:** an automated sequence of steps that moves and transforms data from sources to destinations.
- **ETL / ELT:** **E**xtract, **T**ransform, **L**oad (transform before storing) vs **E**xtract, **L**oad, **T**ransform (store raw data first, transform inside the warehouse with SQL; the modern default).
- **Batch vs streaming:** processing data in scheduled chunks (every night) vs continuously as events arrive (Kafka, Flink).
- **Data warehouse / data lake / lakehouse:** a database built for analytics (Snowflake, BigQuery, Redshift) / cheap storage of raw files (Parquet on S3) / a lake with warehouse features (Delta Lake, Apache Iceberg, DuckLake).
- **Orchestrator:** software that schedules pipeline steps, runs them in the right order, retries failures and alerts people: **Airflow**, **Dagster**, **Prefect**.
- **DAG (directed acyclic graph):** the dependency graph of pipeline steps (B runs after A; no loops).
- **dbt (data build tool):** writes warehouse transformations as SQL `SELECT` files with tests and documentation; the standard for ELT.
- **Idempotent:** running a step twice gives the same result as running it once (re-running yesterday's job doesn't duplicate yesterday's rows).
- **Partitioning:** splitting stored data into folders by a key (one folder per day or month), so queries and re-runs touch only the parts they need.
- **Backfill:** re-running a pipeline for past dates (after a bug fix or a new column).
- **Data quality dimensions:** **completeness** (nothing missing), **validity** (values follow the rules), **uniqueness** (no duplicates), **consistency** (agrees across tables), **accuracy** (matches reality), **timeliness / freshness** (up to date).
- **Data contract:** an agreement between the team producing data and the teams using it: schema, meaning, quality rules and freshness.
- **Observability (data):** monitoring pipelines and tables over time: row counts, null rates, freshness, distribution shifts.
- **Lineage:** which upstream tables and steps each output depends on.
- **Cron:** the classic Unix tool for running a command on a schedule ("every day at 06:00").
- **Kafka / Flink:** popular streaming tools: Apache Kafka carries streams of events between systems; Apache Flink processes those streams continuously.

**Everyday picture.** A restaurant kitchen. A home cook (notebook) makes one meal, tasting as they go. A restaurant (pipeline) serves the same dish hundreds of times a day: fixed recipes (functions), checks at each station (validation), a head chef who stops the line when something's wrong (failing loudly), and a rule that re-cooking an order replaces it rather than sending two plates (idempotency).

**A batch pipeline, step by step:**

1. **Extract:** read new raw data for a date (files, an API, a database) and keep an untouched copy.
2. **Transform:** clean, join and aggregate with pure functions (input DataFrame → output DataFrame).
3. **Validate:** check schema, rules, row counts and freshness. **Fail** if a check fails.
4. **Load:** write the output for that date, **replacing** that date's partition (idempotent).
5. **Log and monitor:** record row counts, durations and check results; alert on failure.

**Notebook habits vs pipeline habits:**

| Notebook | Pipeline |
|---|---|
| cells run in any order | functions with clear inputs and outputs |
| hard-coded file paths and dates | parameters (`run_date`), config files |
| look at the output to check it | automated checks that fail the run |
| append results | overwrite the partition (idempotent) |
| print | structured logging |
| "it worked on my laptop" | pinned dependencies (`uv.lock`), tests, scheduled runs |

**What to monitor on every table:** row count (vs yesterday and vs the same weekday last week), null rate per column, duplicate keys, freshness (the latest timestamp), and the distribution of key metrics. A sudden drop to zero rows, or a 3× jump, is usually a bug upstream.

**When you need a full orchestrator:** several pipelines with dependencies, retries, backfills and alerts. A single nightly script can start as a scheduled job (cron, GitHub Actions); move to Airflow, Dagster or Prefect when coordination gets hard.

**Common mistakes:**

- ❌ Appending on every run, so a retry duplicates a day's data. ✅ Overwrite the date's partition.
- ❌ Silent fallbacks (`fillna(0)` on a column that is suddenly all missing). ✅ Validate and fail.
- ❌ Logic only in notebooks, with no tests. ✅ Functions plus a few unit tests on small DataFrames.
- ❌ Timezone-naive timestamps, so "yesterday" means different things on different servers (Section [37](#37-dates-and-times-parsing-dt-time-zones-and-periods)).
- ❌ No owner: nobody notices when a source changes its format. ✅ Data contracts and alerts.

**Used in real software:** every company with dashboards runs pipelines like this: orchestrated by Airflow, Dagster or Prefect, transforming with dbt or Spark, storing in Snowflake, BigQuery, Databricks or Parquet lakes, and checked with tools such as dbt tests, Great Expectations, Soda or pandera.

### Python

```python
import logging, os, tempfile
import numpy as np
import pandas as pd
import pandera.pandas as pa

logging.basicConfig(level=logging.INFO, format="%(levelname)s %(message)s", force=True)
log = logging.getLogger("orders_pipeline")
import sys; logging.getLogger().handlers[0].setStream(sys.stdout)       # show logs in these notes' output

LAKE = tempfile.mkdtemp()                                                 # stands in for S3 / a data lake

def extract(run_date: str) -> pd.DataFrame:
    """Pretend to read the day's raw orders from a source system."""
    rng = np.random.default_rng(int(run_date.replace("-", "")))          # a repeatable seed per date
    n = 500
    return pd.DataFrame({"order_id": np.arange(n) + int(run_date.replace("-", "")) * 1000,
                         "ts": pd.Timestamp(run_date, tz="UTC") + pd.to_timedelta(rng.integers(0, 86_400, n), unit="s"),
                         "city": rng.choice(["Pune", "Mumbai", "Delhi"], n),
                         "qty": rng.integers(1, 5, n), "price": rng.uniform(50, 3000, n).round(2)})

def transform(raw: pd.DataFrame) -> pd.DataFrame:
    return (raw.assign(revenue=lambda d: d["qty"] * d["price"],
                       order_date=lambda d: d["ts"].dt.strftime("%Y-%m-%d"))
               .groupby(["order_date", "city"], as_index=False)
               .agg(orders=("order_id", "nunique"), revenue=("revenue", "sum")))

schema = pa.DataFrameSchema({
    "order_date": pa.Column(str),
    "city": pa.Column(str, pa.Check.isin(["Pune", "Mumbai", "Delhi", "Bengaluru"])),
    "orders": pa.Column(int, pa.Check.gt(0)),
    "revenue": pa.Column(float, pa.Check.ge(0)),
}, unique=["order_date", "city"])

def load(df: pd.DataFrame, run_date: str) -> str:
    folder = os.path.join(LAKE, "daily_city_revenue", f"order_date={run_date}")
    os.makedirs(folder, exist_ok=True)
    path = os.path.join(folder, "part-0.parquet")
    df.drop(columns="order_date").to_parquet(path, index=False)          # overwrite = idempotent
    return path

def run(run_date: str) -> None:
    raw = extract(run_date)
    log.info("extracted %d rows for %s", len(raw), run_date)
    out = schema.validate(transform(raw))                                 # raises (stops the run) if a rule fails
    if len(out) == 0:
        raise ValueError("no output rows: refusing to publish an empty day")
    log.info("loaded %d rows to %s", len(out), os.path.relpath(load(out, run_date), LAKE))

for day in ["2025-03-01", "2025-03-02", "2025-03-02"]:                    # note: 03-02 runs twice (a retry)
    run(day)
```

**Output:**

```text
INFO extracted 500 rows for 2025-03-01
INFO loaded 3 rows to daily_city_revenue/order_date=2025-03-01/part-0.parquet
INFO extracted 500 rows for 2025-03-02
INFO loaded 3 rows to daily_city_revenue/order_date=2025-03-02/part-0.parquet
INFO extracted 500 rows for 2025-03-02
INFO loaded 3 rows to daily_city_revenue/order_date=2025-03-02/part-0.parquet
```

`logging` records what happened with a level (INFO, WARNING, ERROR) instead of loose `print`s; in production, logs go to a central system. The two lines setting up the handler make the log messages appear in these notes. The folder name `order_date=2025-03-02` is **Hive-style partitioning**: readers understand it as a column.

```python
table = pd.read_parquet(os.path.join(LAKE, "daily_city_revenue")).astype({"order_date": "str"})   # partition names come back as a category
print(table.groupby("order_date").agg(rows=("city", "size"), orders=("orders", "sum")))   # the retry didn't duplicate

def quality_report(df: pd.DataFrame, key: list[str]) -> pd.Series:
    return pd.Series({"rows": len(df), "duplicate_keys": int(df.duplicated(key).sum()),
                      "max_null_rate": float(df.isna().mean().max()),
                      "latest_partition": str(df["order_date"].max())})
print(quality_report(table, ["order_date", "city"]))

bad = transform(extract("2025-03-03")).assign(revenue=lambda d: d["revenue"] * np.where(d["city"] == "Delhi", -1, 1))
try:
    schema.validate(bad)
except pa.errors.SchemaError as err:
    print("ERROR validation failed, nothing published:", str(err).splitlines()[0])   # in production: log.error(...) and alert
```

**Output:**

```text
            rows  orders
order_date              
2025-03-01     3     500
2025-03-02     3     500
rows                         6
duplicate_keys               0
max_null_rate              0.0
latest_partition    2025-03-02
dtype: object
ERROR validation failed, nothing published: Column 'revenue' failed element-wise validator number 0: greater_than_or_equal_to(0) failure cases: -619974.61
```

Reading the folder back, pandas turns the `order_date=...` folder names into a column; it arrives as an unordered category, so `astype` makes it text again for sorting and `max`. The 2 March partition appears **once** despite the retry. The bad batch with negative revenue is stopped before it's loaded.

### Practice

1. Add a check to `run` that fails if a day's total revenue is less than half of the previous day's (a simple anomaly guard). What could cause a false alarm?
2. Why is `df.to_parquet(path)` into a fixed per-date folder idempotent, while appending rows to one big file isn't?

<details>
<summary><b>Answer</b></summary>

```python
def revenue_guard(today: pd.DataFrame, yesterday: pd.DataFrame, min_ratio=0.5):
    ratio = today["revenue"].sum() / yesterday["revenue"].sum()
    if ratio < min_ratio:
        raise ValueError(f"revenue fell to {ratio:.0%} of yesterday's")
    return ratio

d1, d2 = transform(extract("2025-03-01")), transform(extract("2025-03-02"))
print(f"ratio {revenue_guard(d2, d1):.2f}")
```

**Output:**

```text
ratio 1.02
```

1. False alarms: real seasonality (a Sunday after a big Saturday, a holiday), a legitimate outage, or a partial day if the pipeline ran early. Compare with the same weekday last week, and alert a human instead of failing outright for borderline cases.
2. Writing a date's output to its own folder **replaces** whatever was there, so running twice leaves exactly one copy. Appending adds the rows again on every retry, doubling that day's numbers.

</details>

**Learn more:** [dbt: what is dbt?](https://docs.getdbt.com/docs/introduction) · [Dagster: concepts](https://docs.dagster.io/getting-started/concepts) · [Apache Airflow: tutorial](https://airflow.apache.org/docs/apache-airflow/stable/tutorial/fundamentals.html) · [Joe Reis & Matt Housley: Fundamentals of Data Engineering](https://www.oreilly.com/library/view/fundamentals-of-data/9781098108298/)

---

## 63. Communicating Results: Reports, Dashboards and Data Storytelling

![A one-page analysis: answer first, then the evidence, the recommendation and the caveats](images/data-science/63-report.svg)

### Theory

> **In simple words:** an analysis only matters if someone **acts** on it. Lead with the **answer**, support it with two or three pieces of evidence, say what you **recommend** and how sure you are, and put everything else in an appendix. Dashboards are for monitoring things people check repeatedly; one-off questions deserve a short written answer.

**Words to know:**

- **Stakeholder:** a person who uses or is affected by your analysis (a product manager, a marketing lead).
- **Pyramid principle (answer first):** start with the conclusion, then the supporting points, then the details (Barbara Minto's method, used by consulting firms).
- **Executive summary (TL;DR):** the 2–4 sentences someone reads if they read nothing else.
- **KPI (key performance indicator):** a metric that tracks a goal (weekly active users, conversion rate, revenue per user).
- **North-star metric:** the single metric that best captures the value a product delivers.
- **Metric definition:** the exact formula, filters and time window (e.g. "active = at least one session in the last 7 days, excluding staff accounts").
- **Dashboard:** a page of charts and numbers that updates automatically, for **monitoring**.
- **Self-serve analytics:** tools that let non-analysts explore data themselves (BI tools, semantic layers).
- **Semantic layer / metrics layer:** one shared, central definition of each metric so every dashboard computes "revenue" the same way.
- **Data storytelling:** presenting data as a narrative: context → tension (what changed or what's wrong) → resolution (what to do).
- **Caveats / limitations:** what the analysis can't tell you and why.
- **Quarto:** an open-source tool that turns notebooks and Markdown into reports, websites and slides.

**Everyday picture.** A doctor doesn't hand you your blood-test spreadsheet; they say "You're healthy, but your cholesterol is a bit high; cut down on fried food and we'll recheck in six months." That's the whole structure: answer, evidence, recommendation, caveat, next step.

**The one-page analysis template:**

1. **Question:** what was asked, in one line.
2. **Answer:** the conclusion in 1–3 sentences, with the key number and its uncertainty.
3. **Evidence:** 2–3 findings, each with one chart or table.
4. **Recommendation:** what to do, and the expected impact.
5. **Caveats:** data limitations, assumptions, what would change the conclusion.
6. **Appendix:** method, definitions, extra charts, a link to the code.

**Writing numbers people understand:**

| ❌ Hard to read | ✅ Clear |
|---|---|
| conversion went from 0.0412 to 0.0461 | conversion rose from 4.1% to 4.6% (+0.5 points, +12% relative) |
| p = 0.0075 | the lift is very unlikely to be chance (95% CI: +0.1 to +0.8 points) |
| revenue = 18,734,221.56 | revenue ₹1.87 crore (≈ ₹18.7 million) |
| 1 in 1,000 users | 0.1% of users (about 2,400 people this month) |

**Dashboards that work:**

- One audience and one purpose per dashboard ("weekly sales health for regional managers").
- The 3–5 most important numbers at the top, each with a comparison (vs last week, vs target).
- Trends as lines; breakdowns as sorted bars; filters for the dimensions people actually use.
- Every metric's **definition** one click away; the **data freshness** ("updated 06:00 UTC") always visible.
- Fewer charts, better chosen (Section [50](#50-choosing-the-right-chart-and-not-misleading)).

**Tools:** written reports in notebooks or docs (Quarto and Jupyter can render notebooks to HTML or PDF); BI tools (Power BI, Tableau, Looker, Metabase, Superset); Python data apps (Streamlit, Dash) when you need custom interactivity; slides when presenting live.

**Common mistakes:**

- ❌ Walking through the analysis chronologically ("first I loaded the data…"). ✅ Answer first.
- ❌ Twenty charts. ✅ Three that support the answer.
- ❌ Precision theatre (7 decimal places) and jargon ("heteroscedasticity").
- ❌ Hiding uncertainty or caveats, then losing trust when reality differs.
- ❌ Dashboards that nobody owns and whose metrics silently drift from their definitions.

**Used in real software:** weekly business reviews, experiment readouts, board decks, product dashboards, incident post-mortems; companies standardise metric definitions in semantic layers (dbt Semantic Layer, Looker's LookML, Cube).

### Python

```python
import numpy as np
import pandas as pd

rng = np.random.default_rng(12)
weeks = pd.date_range("2025-08-04", periods=8, freq="W-MON")
kpi = pd.DataFrame({"week": weeks,
                    "active_users": (52_000 * 1.02 ** np.arange(8) + rng.normal(0, 600, 8)).round(),
                    "orders": (9_800 * 1.03 ** np.arange(8) + rng.normal(0, 150, 8)).round()})
kpi["conversion"] = kpi["orders"] / kpi["active_users"]

last, prev = kpi.iloc[-1], kpi.iloc[-2]
def change(col):
    return f"{last[col]:,.0f} ({(last[col] / prev[col] - 1):+.1%} vs last week)"

summary = f"""**Answer:** orders keep growing faster than users, so conversion is rising.

- Active users: {change("active_users")}
- Orders: {change("orders")}
- Conversion: {last["conversion"]:.1%} ({(last["conversion"] - kpi["conversion"].iloc[0]) * 100:+.1f} points over 8 weeks)

**Recommendation:** keep the new checkout flow; test free delivery thresholds next.
**Caveat:** 8 weeks include a festival period; compare with last year before forecasting."""
print(summary)
```

**Output:**

```text
**Answer:** orders keep growing faster than users, so conversion is rising.

- Active users: 58,939 (+1.3% vs last week)
- Orders: 12,319 (+6.5% vs last week)
- Conversion: 20.9% (+2.1 points over 8 weeks)

**Recommendation:** keep the new checkout flow; test free delivery thresholds next.
**Caveat:** 8 weeks include a festival period; compare with last year before forecasting.
```

```python
table = kpi.assign(week=kpi["week"].dt.strftime("%d %b"),
                   active_users=kpi["active_users"].map("{:,.0f}".format),
                   orders=kpi["orders"].map("{:,.0f}".format),
                   conversion=kpi["conversion"].map("{:.1%}".format)).tail(4)
print(table.to_markdown(index=False))          # paste straight into a doc, a wiki or a pull request
```

**Output:**

```text
| week   |   active_users |   orders | conversion   |
|:-------|---------------:|---------:|:-------------|
| 01 Sep |         57,258 |   10,743 | 18.8%        |
| 08 Sep |         56,689 |   11,383 | 20.1%        |
| 15 Sep |         58,184 |   11,566 | 19.9%        |
| 22 Sep |         58,939 |   12,319 | 20.9%        |
```

`to_markdown` (it needs the small `tabulate` library) produces a table you can paste into any Markdown document; formatting numbers as strings first (`"{:,.0f}".format`) controls exactly how they appear.

A minimal **Streamlit** dashboard looks like this (save as `app.py`, run with `streamlit run app.py`; not run here because it starts a web server):

```python
import pandas as pd
import streamlit as st

st.title("Weekly sales health")
df = pd.read_parquet("daily_city_revenue")                 # the pipeline's output (Section 62)
city = st.selectbox("City", sorted(df["city"].unique()))
view = df[df["city"] == city]
st.metric("Revenue (last day)", f"₹{view['revenue'].iloc[-1]:,.0f}")
st.line_chart(view, x="order_date", y="revenue")
st.caption("Revenue = qty × price, excluding cancelled orders. Updated daily at 06:00 UTC.")
```

### Practice

1. Rewrite as a two-sentence executive summary: "We ran a test for 14 days with 51,100 users. Group B converted at 4.49% vs 4.01% for A (p = 0.0075, 95% CI +0.13 to +0.83 points). Page load times were unchanged. The test overlapped a sale weekend."
2. A manager asks for "a dashboard of everything". What three questions do you ask first?

<details>
<summary><b>Answer</b></summary>

1. "The new design increased conversion from 4.0% to 4.5% (+12%, very unlikely to be chance), with no slowdown in page loads; we recommend shipping it. Because the test overlapped a sale weekend, we'll confirm the lift holds over the next two normal weeks."
2. Who will use it, and how often? Which decisions will it drive (what would they do differently if a number moved)? Which 3–5 metrics matter most, and how exactly are they defined?

</details>

**Learn more:** [Storytelling with Data (Cole Nussbaumer Knaflic)](https://www.storytellingwithdata.com/) · [Streamlit: get started](https://docs.streamlit.io/get-started) · [Quarto: publish notebooks and reports](https://quarto.org/)

---

## 64. What's New: Modern Data Tooling (2023–2026)

![The modern Python data stack: Arrow-based DataFrames and engines, columnar files and table formats, and AI assistants on top](images/data-science/64-modern-stack.svg)

### Theory

> **In simple words:** the Python data world changed a lot between 2023 and 2026. pandas moved to Arrow-backed text and copy-on-write; Polars and DuckDB became mainstream for speed; `uv` made environments fast and reproducible; open **table formats** turned folders of Parquet files into reliable tables; and AI assistants now help write and explain analysis code. The fundamentals in these notes are the same; the tools around them are faster.

**Words to know:**

- **Apache Arrow:** the shared columnar memory format behind modern data tools (Section [40](#40-memory-dtypes-categoricals-chunking-and-apache-arrow)).
- **DataFrame library:** pandas, Polars, and others with a table API.
- **Query engine:** software that plans and runs queries efficiently (DuckDB, Polars' engine, DataFusion, Spark).
- **Table format:** a layer over Parquet files that adds transactions, schema changes and "time travel" (reading old versions): **Apache Iceberg**, **Delta Lake**, **DuckLake**.
- **Dataframe-agnostic code:** code written once that runs on pandas, Polars and others (**Narwhals**, **Ibis**).
- **Reactive notebook:** a notebook where changing a cell automatically re-runs the cells that depend on it, so state can't get out of sync (**marimo**).
- **Free-threaded Python:** Python builds without the **GIL** (global interpreter lock, which lets only one thread run Python code at a time), so threads can use several CPU cores.
- **AI coding assistant:** an LLM-based tool that writes, explains and debugs code (Claude, GitHub Copilot, Jupyter AI, assistants built into IDEs).

**Everyday picture.** A kitchen renovation: the new oven heats faster and the new fridge holds more, so dinner is quicker, but the recipes and the cooking skills are the same. New data tools are the appliances; asking a clear question, cleaning carefully and checking your numbers are the cooking.

**What changed, with dates (verified against release records):**

| Year | Change | Why it matters |
|---|---|---|
| Apr 2023 | **pandas 2.0**: optional Arrow-backed dtypes | the start of pandas' move to Arrow |
| Jun 2024 | **NumPy 2.0**: cleaned-up API and type promotion rules | some old code needed small fixes |
| Jun 2024 | **DuckDB 1.0**: stable file format and API | in-process SQL became a safe default for analytics |
| Jul 2024 | **Polars 1.0**: stable API | Polars became a mainstream pandas alternative |
| 2024 | **uv** (released February 2024) grows into a full project manager | environments in seconds; `uv.lock` for reproducibility |
| Oct 2024 / Oct 2025 | Python 3.13 adds an experimental free-threaded build; Python 3.14 makes it officially supported | multi-core threading becomes possible for Python code |
| 2024–2025 | Apache Iceberg and Delta Lake become the common lakehouse formats; DuckDB announces **DuckLake** (2025) | reliable tables on cheap object storage |
| Jan 2026 | **pandas 3.0**: a dedicated `str` dtype (Arrow-backed when available) and **copy-on-write** by default | faster text, far fewer copy/view bugs (Section [25](#25-method-chaining-and-copy-on-write-pandas-3)) |
| Oct 2026 | **Polars 2.0** | the engine and API keep maturing |
| 2023–2026 | LLM assistants become a normal part of data work | faster code writing; new need to verify results |

**How to work with AI assistants on data (2026 practice):**

1. **Give context:** the DataFrame's `dtypes`, a few rows (`head().to_markdown()`), the question, and your library versions.
2. **Ask for code, then run it yourself.** Treat generated code like a colleague's pull request: read it, test it on a small case you can check by hand.
3. **Verify every number** an assistant states about your data by computing it. LLMs can produce plausible but wrong statistics and invented column names.
4. **Never paste sensitive data** (personal data, credentials, confidential numbers) into tools your organisation hasn't approved.
5. **Use it to learn:** "explain this regression table", "why does this merge produce more rows?" are excellent uses; the explanations in these notes are your check.

**Choosing tools in 2026 (a practical default):**

| Need | Default choice |
|---|---|
| everyday analysis up to a few GB | pandas 3 (+ pyarrow) |
| big files, speed, lazy pipelines | Polars |
| SQL-shaped questions on files, or data bigger than RAM | DuckDB |
| a team's shared tables at scale | a warehouse (BigQuery, Snowflake, Databricks) or Iceberg/Delta tables, transformed with dbt |
| charts | Matplotlib/Seaborn (static), Plotly (interactive) |
| environments | uv |
| notebooks | Jupyter (VS Code or JupyterLab); marimo for reproducible, app-like notebooks |

**What did NOT change:** asking a clear question, cleaning data carefully, looking at distributions before averages, splitting before learning, quantifying uncertainty, and communicating answer-first. Tools come and go; those skills transfer.

**Common mistakes:**

- ❌ Rewriting working pandas code in a new library for fashion. ✅ Switch when you hit a real limit (speed, memory).
- ❌ Copying old tutorials (pre-2024) without noticing changed behaviour (copy-on-write, `str` dtype, NumPy 2 promotion).
- ❌ Trusting AI-generated numbers or code without running and checking them.

**Used in real software:** most new data platforms combine Parquet/Iceberg storage, DuckDB or Polars for single-machine work, a warehouse for shared data, dbt for transformations, and AI assistants in the editor.

### Python

```python
import importlib

for name in ["numpy", "pandas", "pyarrow", "polars", "duckdb", "matplotlib", "seaborn", "scipy", "statsmodels", "plotly"]:
    module = importlib.import_module(name)
    print(f"{name:<12} {module.__version__}")
```

**Output:**

```text
numpy        2.5.3
pandas       3.0.6
pyarrow      25.0.1
polars       2.0.0
duckdb       1.5.6
matplotlib   3.11.2
seaborn      0.13.2
scipy        1.18.1
statsmodels  0.15.0
plotly       7.1.0
```

```python
import pandas as pd

s = pd.Series(["a", "b", None])
print("default text dtype:", s.dtype, "| storage:", getattr(s.dtype, "storage", "n/a"))
df = pd.DataFrame({"x": [1, 2, 3]})
view = df["x"]
view.iloc[0] = 100                                # copy-on-write: df is NOT changed
print("df after editing a derived Series:", df["x"].tolist())
```

**Output:**

```text
default text dtype: str | storage: pyarrow
df after editing a derived Series: [1, 2, 3]
```

The first line confirms pandas 3's `str` dtype, stored with Arrow (`pyarrow`). The second shows copy-on-write: changing a Series taken from a DataFrame leaves the DataFrame untouched (in pandas 1.x this would have changed `df` too).

### Practice

1. Check your own versions with the first code block. If your pandas is below 3.0, which two behaviours from this section will differ?
2. Write the prompt you'd give an AI assistant to help find why a monthly revenue total doesn't match the finance team's number. What would you include, and what would you leave out?

<details>
<summary><b>Answer</b></summary>

1. Text columns will show `object` (or `string` if you opt in) instead of `str`, and without copy-on-write a modified subset may change the original (with `SettingWithCopyWarning`); enable it on pandas 2.x with `pd.options.mode.copy_on_write = True`.
2. Include: both totals, the exact metric definitions (gross vs net, refunds, taxes, time zone of "month"), your code, `df.dtypes` and a few anonymised rows, and the library versions. Ask for a list of likely causes and checks to run. Leave out: customer names, emails, payment details and any confidential figures your company doesn't allow in that tool.

</details>

**Learn more:** [pandas 3.0 release notes](https://pandas.pydata.org/docs/whatsnew/index.html) · [Polars: user guide](https://docs.pola.rs/) · [DuckDB: documentation](https://duckdb.org/docs/) · [uv](https://docs.astral.sh/uv/) · [marimo](https://marimo.io/) · [Narwhals](https://narwhals-dev.github.io/narwhals/)

---

### ✅ Part 9 checkpoint

Without looking, can you:

- [ ] Run the eight-step EDA checklist on a new dataset and write five specific, quantified findings?
- [ ] Prepare train and test features without leakage, encode categories correctly, and explain smoothed target encoding?
- [ ] Build point-in-time RFM features from an event table?
- [ ] Write a pipeline as extract/transform/validate/load functions that's idempotent and fails loudly on bad data?
- [ ] Name the six data-quality dimensions and what to monitor on every table?
- [ ] Write a one-page, answer-first summary with evidence, a recommendation and caveats?
- [ ] Explain what changed in pandas 3 and when to choose pandas, Polars or DuckDB?

Part 10 is revision: what companies ask, practice problems, a cheat sheet, the most-asked questions, and the glossary of every term.

---

# Part 10 — Interview Prep: Revision

> **Goal:** Know what data interviews test, practise the classic pandas, NumPy, statistics and product questions with worked solutions, revise with one cheat sheet, and look up any term in the glossary.  
> **You need:** Parts 1–9.

---

## 65. Interview Topic Checklist: What Companies Ask

### Theory

Data analyst, data scientist and analytics/ML engineer interviews at product companies (and the many that interview the same way) usually combine four kinds of round:

| Round | What happens | Tested in these notes |
|---|---|---|
| **SQL / pandas coding** | 2–4 problems on small tables: filtering, grouping, joins, window functions, ranking, dates | Parts 3–6; Section [66](#66-interview-problems-pandas-numpy-and-sql-style-questions) |
| **Statistics and probability** | explain p-values, CIs, CLT; small probability puzzles; A/B test design | Part 8; Section [67](#67-statistics-probability-and-product-interview-problems) |
| **Product sense / metrics** | "how would you measure success of feature X?", "DAU dropped 10%: investigate" | Sections [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls), [63](#63-communicating-results-reports-dashboards-and-data-storytelling), [67](#67-statistics-probability-and-product-interview-problems) |
| **Take-home or case study** | EDA on a dataset, a short written report, sometimes a simple model | Sections [60](#60-a-complete-exploratory-data-analysis-eda)–[63](#63-communicating-results-reports-dashboards-and-data-storytelling) |

ML-focused roles add a machine-learning round (`machine-learning.md`); engineering-heavy roles add Python/DSA (`dsa-python.md`) and pipeline design (Section [62](#62-data-pipelines-and-data-quality-in-production)).

**How to read the priority column:** ⭐⭐⭐ appears in almost every loop; ⭐⭐ is common; ⭐ is occasional but separates strong candidates.

| Topic | Priority | Study | Must-do problems |
|---|---|---|---|
| Filtering and selecting | ⭐⭐⭐ | [21](#21-selecting-data-columns--loc-and-iloc), [22](#22-filtering-rows-conditions-isin-between-and-query) | [595. Big Countries](https://leetcode.com/problems/big-countries/) · [1757. Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/) · [183. Customers Who Never Order](https://leetcode.com/problems/customers-who-never-order/) · [1148. Article Views I](https://leetcode.com/problems/article-views-i/) |
| Missing values and duplicates | ⭐⭐⭐ | [26](#26-missing-values-finding-dropping-and-filling), [27](#27-duplicates-data-types-and-type-conversion) | [584. Find Customer Referee](https://leetcode.com/problems/find-customer-referee/) · [196. Delete Duplicate Emails](https://leetcode.com/problems/delete-duplicate-emails/) · [1965. Employees With Missing Information](https://leetcode.com/problems/employees-with-missing-information/) |
| Text and regex | ⭐⭐ | [28](#28-text-data-the-str-accessor-and-regular-expressions) | [1667. Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table/) · [1527. Patients With a Condition](https://leetcode.com/problems/patients-with-a-condition/) · [1517. Find Users With Valid E-Mails](https://leetcode.com/problems/find-users-with-valid-e-mails/) |
| Group and aggregate | ⭐⭐⭐ | [31](#31-grouping-i-groupby-agg-and-split-apply-combine) | [1741. Find Total Time Spent by Each Employee](https://leetcode.com/problems/find-total-time-spent-by-each-employee/) · [596. Classes With at Least 5 Students](https://leetcode.com/problems/classes-with-at-least-5-students/) · [1484. Group Sold Products By The Date](https://leetcode.com/problems/group-sold-products-by-the-date/) · [1193. Monthly Transactions I](https://leetcode.com/problems/monthly-transactions-i/) |
| Ranking, Nth highest, top N per group | ⭐⭐⭐ | [23](#23-sorting-ranking-and-top-n), [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking) | [176. Second Highest Salary](https://leetcode.com/problems/second-highest-salary/) · [177. Nth Highest Salary](https://leetcode.com/problems/nth-highest-salary/) · [178. Rank Scores](https://leetcode.com/problems/rank-scores/) · [184. Department Highest Salary](https://leetcode.com/problems/department-highest-salary/) · [185. Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries/) |
| Joins (incl. anti- and self-joins) | ⭐⭐⭐ | [33](#33-combining-tables-i-merge-and-join-types), [34](#34-combining-tables-ii-concat-validation-and-merge-pitfalls) | [175. Combine Two Tables](https://leetcode.com/problems/combine-two-tables/) · [181. Employees Earning More Than Their Managers](https://leetcode.com/problems/employees-earning-more-than-their-managers/) · [1280. Students and Examinations](https://leetcode.com/problems/students-and-examinations/) · [570. Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/) · [1934. Confirmation Rate](https://leetcode.com/problems/confirmation-rate/) |
| Window functions (running totals, lag, streaks) | ⭐⭐⭐ | [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking), [38](#38-time-series-resample-rolling-shift-and-window-functions) | [197. Rising Temperature](https://leetcode.com/problems/rising-temperature/) · [180. Consecutive Numbers](https://leetcode.com/problems/consecutive-numbers/) · [1321. Restaurant Growth](https://leetcode.com/problems/restaurant-growth/) · [1204. Last Person to Fit in the Bus](https://leetcode.com/problems/last-person-to-fit-in-the-bus/) · [601. Human Traffic of Stadium](https://leetcode.com/problems/human-traffic-of-stadium/) |
| Dates and retention | ⭐⭐ | [37](#37-dates-and-times-parsing-dt-time-zones-and-periods), [38](#38-time-series-resample-rolling-shift-and-window-functions) | [550. Game Play Analysis IV](https://leetcode.com/problems/game-play-analysis-iv/) · [1141. User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/) · [1174. Immediate Food Delivery II](https://leetcode.com/problems/immediate-food-delivery-ii/) |
| Pivot and reshape | ⭐⭐ | [35](#35-reshaping-pivot_table-melt-crosstab-and-explode) | [1179. Reformat Department Table](https://leetcode.com/problems/reformat-department-table/) · [1795. Rearrange Products Table](https://leetcode.com/problems/rearrange-products-table/) · [2889. Reshape Data: Pivot](https://leetcode.com/problems/reshape-data-pivot/) |
| Hard multi-step SQL/pandas | ⭐ | Parts 5–6 | [262. Trips and Users](https://leetcode.com/problems/trips-and-users/) · [1045. Customers Who Bought All Products](https://leetcode.com/problems/customers-who-bought-all-products/) · [3554. Find Category Recommendation Pairs](https://leetcode.com/problems/find-category-recommendation-pairs/) |
| NumPy and linear algebra | ⭐⭐ | Part 2 | [Deep-ML 1. Matrix-Vector Dot Product](https://www.deep-ml.com/problems/1) · [Deep-ML 4. Calculate Mean by Row or Column](https://www.deep-ml.com/problems/4) · [Deep-ML 76. Cosine Similarity](https://www.deep-ml.com/problems/76) |
| Descriptive statistics | ⭐⭐⭐ | [51](#51-describing-data-centre-spread-and-shape), [52](#52-correlation-covariance-and-causation) | [Deep-ML 78. Descriptive Statistics Calculator](https://www.deep-ml.com/problems/78) · [Deep-ML 10. Covariance Matrix](https://www.deep-ml.com/problems/10) |
| Probability and Bayes | ⭐⭐⭐ | [53](#53-probability-basics-events-conditional-probability-and-bayes-rule), [54](#54-probability-distributions-normal-binomial-poisson-and-more) | [Deep-ML 168. Conditional Probability from Data](https://www.deep-ml.com/problems/168) · [Deep-ML 79. Binomial Distribution Probability](https://www.deep-ml.com/problems/79) · [Deep-ML 246. Birthday Problem](https://www.deep-ml.com/problems/246) |
| Sampling, CIs and the bootstrap | ⭐⭐ | [55](#55-sampling-the-central-limit-theorem-and-standard-error), [56](#56-confidence-intervals-and-the-bootstrap) | [Deep-ML 212. Confidence Interval for Population Mean](https://www.deep-ml.com/problems/212) · [Deep-ML 182. CLT Simulation](https://www.deep-ml.com/problems/182) |
| Hypothesis tests and A/B testing | ⭐⭐⭐ | [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests), [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls) | [Deep-ML 211. Two-Sample T-Test](https://www.deep-ml.com/problems/211) · [Deep-ML 296. Statistical Power](https://www.deep-ml.com/problems/296) |
| Regression | ⭐⭐ | [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence) | [Deep-ML 14. Linear Regression Using Normal Equation](https://www.deep-ml.com/problems/14) |
| Charts and communication | ⭐⭐ | Part 7, [63](#63-communicating-results-reports-dashboards-and-data-storytelling) | redraw a misleading chart; write a 3-sentence summary of any analysis above |
| EDA / take-home | ⭐⭐ | [60](#60-a-complete-exploratory-data-analysis-eda), [61](#61-feature-engineering-preparing-data-for-machine-learning) | [Kaggle: Titanic](https://www.kaggle.com/competitions/titanic) · [Kaggle: House Prices](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques) |

**A study plan:** LeetCode's free [Introduction to Pandas](https://leetcode.com/studyplan/introduction-to-pandas/) and [30 Days of Pandas](https://leetcode.com/studyplan/30-days-of-pandas/) study plans cover the coding round; solve each problem in **both** pandas and SQL (`sql-postgresql.md`), because many companies let you choose.

**Beyond the problems, interviewers check that you:**

1. **Clarify before coding:** what's a row? Are there duplicates, NULLs, ties? What should happen with ties?
2. **Say the plan first**, then code it step by step, checking the row count after joins and filters.
3. **Handle edge cases out loud:** empty results, ties, missing values, time zones.
4. **Explain statistics in plain words** (p-value, CI, power) without jargon, and give the business meaning.
5. **Structure open questions:** clarify the goal → define metrics → list hypotheses → say what data you'd check → decide.
6. **Communicate trade-offs:** speed vs accuracy, a quick answer now vs a thorough one later.

---

## 66. Interview Problems: pandas, NumPy and SQL-Style Questions

### Theory

> **In simple words:** the coding round reuses about a dozen patterns. Learn to recognise each from the question's wording, write it in pandas, and know its SQL twin. Every problem below is solved and run.

**Words to know:**

- **DAU / WAU / MAU:** daily / weekly / monthly active users: the number of distinct users active in a day, week or month.
- **Stickiness:** DAU ÷ MAU: how many of the month's users come back on a typical day (20% means users are active about 6 days a month).
- **Gaps and islands:** the classic problem of finding runs of consecutive values (consecutive login days) separated by gaps.
- **Basket analysis:** finding products that are bought together in the same order.
- **Product sense:** the ability to reason about what a product's users need and how to measure whether a feature helps them.

**Pattern → pandas tool → SQL twin:**

| Pattern ("the question says…") | pandas | SQL |
|---|---|---|
| top N per group | sort + `groupby().head(N)`, or `rank` | `ROW_NUMBER() OVER (PARTITION BY … ORDER BY …) <= N` |
| N-th highest (distinct) | `drop_duplicates` + `nlargest(N).iloc[-1]`, or dense rank | `DENSE_RANK()` / `LIMIT 1 OFFSET N-1` |
| share of total, running total | `transform("sum")`, `groupby().cumsum()` | `SUM() OVER (PARTITION BY …)` |
| growth vs previous period | `resample` / `groupby` + `pct_change()`, `shift()` | `LAG()` |
| latest record per key | sort + `drop_duplicates(keep="last")` | `ROW_NUMBER() … = 1` |
| rows with no match ("never") | `merge(indicator=True)` or `~isin` | `LEFT JOIN … WHERE right.id IS NULL` / `NOT EXISTS` |
| consecutive streaks (gaps and islands) | `diff() != 1` → `cumsum()` labels runs | `day - ROW_NUMBER()` trick |
| retention / cohorts | first date per user → months since → `pivot_table(nunique)` | `GROUP BY cohort, period` |
| funnel conversion | per-user flags → step counts → ratios | conditional `COUNT(DISTINCT …)` |
| pairs bought together | self-merge on order ID | self-join |

**How to do well:** say your plan before coding; check the row count after each step; handle ties and missing values out loud; prefer vectorised pandas over loops; state complexity if asked (sorting O(n log n), `groupby` about O(n)).

### Python

```python
import numpy as np
import pandas as pd

sales = pd.DataFrame({
    "order_id": range(1, 13),
    "user": ["u1", "u2", "u1", "u3", "u2", "u1", "u4", "u3", "u2", "u1", "u4", "u2"],
    "date": pd.to_datetime(["2025-01-03", "2025-01-10", "2025-01-20", "2025-02-02", "2025-02-05", "2025-02-17",
                            "2025-02-21", "2025-03-01", "2025-03-04", "2025-03-09", "2025-03-15", "2025-03-28"]),
    "category": ["books", "tech", "tech", "books", "books", "tech", "home", "tech", "home", "books", "home", "tech"],
    "amount": [300, 2500, 1800, 450, 300, 2200, 900, 1500, 650, 500, 1200, 2500],
})

# 1. Top 2 orders by amount in each category (ties broken by date)
top2 = sales.sort_values(["category", "amount", "date"], ascending=[True, False, True]).groupby("category").head(2)
print(top2[["category", "order_id", "amount"]])

# 2. Second-highest distinct order amount (None if there isn't one)
distinct = sales["amount"].drop_duplicates().nlargest(2)
print(distinct.iloc[-1] if len(distinct) == 2 else None)

# 3. Each order's share of its user's total spend, and each user's running total
sales = sales.sort_values("date")
sales["user_share"] = (sales["amount"] / sales.groupby("user")["amount"].transform("sum")).round(2)
sales["running"] = sales.groupby("user")["amount"].cumsum()
print(sales.loc[sales["user"] == "u1", ["date", "amount", "user_share", "running"]])
```

**Output:**

```text
   category  order_id  amount
9     books        10     500
3     books         4     450
10     home        11    1200
6      home         7     900
1      tech         2    2500
11     tech        12    2500
2200
        date  amount  user_share  running
0 2025-01-03     300        0.06      300
2 2025-01-20    1800        0.38     2100
5 2025-02-17    2200        0.46     4300
9 2025-03-09     500        0.10     4800
```

```python
# 4. Month-over-month revenue growth
monthly = sales.set_index("date")["amount"].resample("MS").sum()
print(pd.DataFrame({"revenue": monthly, "growth_pct": (100 * monthly.pct_change()).round(1)}))

# 5. Each user's latest order only
latest = sales.sort_values("date").drop_duplicates("user", keep="last")
print(latest[["user", "order_id", "date"]].sort_values("user"))

# 6. Users who never bought a "home" item (anti-join)
home_buyers = sales.loc[sales["category"] == "home", "user"].unique()
print(sorted(set(sales["user"]) - set(home_buyers)))

# 7. For each category, the user who spent most in it
spend = sales.groupby(["category", "user"], as_index=False)["amount"].sum()
print(spend.loc[spend.groupby("category")["amount"].idxmax()])
```

**Output:**

```text
            revenue  growth_pct
date                           
2025-01-01     4600         NaN
2025-02-01     3850       -16.3
2025-03-01     6350        64.9
   user  order_id       date
9    u1        10 2025-03-09
11   u2        12 2025-03-28
7    u3         8 2025-03-01
10   u4        11 2025-03-15
['u1', 'u3']
  category user  amount
0    books   u1     800
4     home   u4    2100
6     tech   u2    5000
```

```python
# 8. Longest streak of consecutive login days per user (gaps and islands)
logins = pd.DataFrame({"user": ["a"] * 6 + ["b"] * 4,
                       "day": pd.to_datetime(["2025-05-01", "2025-05-02", "2025-05-03", "2025-05-05", "2025-05-06", "2025-05-07",
                                              "2025-05-01", "2025-05-03", "2025-05-04", "2025-05-10"])})
logins = logins.drop_duplicates().sort_values(["user", "day"])
new_run = logins.groupby("user")["day"].diff().dt.days.ne(1)          # True where a new streak starts
logins["run_id"] = new_run.cumsum()
print(logins.groupby(["user", "run_id"]).size().groupby("user").max().to_dict())

# 9. Monthly retention cohorts: of users who first bought in month M, how many bought k months later?
sales["month"] = sales["date"].dt.to_period("M")
sales["cohort"] = sales.groupby("user")["month"].transform("min")
sales["months_since"] = (sales["month"] - sales["cohort"]).apply(lambda d: d.n)
print(sales.pivot_table(index="cohort", columns="months_since", values="user", aggfunc="nunique", fill_value=0))

# 10. Funnel: view → cart → purchase conversion
events = pd.DataFrame({"user": ["a", "a", "a", "b", "b", "c", "d", "d", "d", "e"],
                       "event": ["view", "cart", "purchase", "view", "cart", "view", "view", "cart", "purchase", "view"]})
steps = ["view", "cart", "purchase"]
reached = events.pivot_table(index="user", columns="event", aggfunc="size", fill_value=0)[steps].gt(0)
counts = reached.sum()
print(pd.DataFrame({"users": counts, "from_previous": (counts / counts.shift()).round(2),
                    "from_start": (counts / counts.iloc[0]).round(2)}))
```

**Output:**

```text
{'a': 3, 'b': 2}
months_since  0  1  2
cohort               
2025-01       2  2  2
2025-02       2  2  0
          users  from_previous  from_start
event                                     
view          5            NaN         1.0
cart          3           0.60         0.6
purchase      2           0.67         0.4
```

`(month − cohort)` on periods gives a "month offset" object; `.n` reads its number of months. In the funnel, `aggfunc="size"` counts events per user and step; `.gt(0)` turns counts into "reached this step".

```python
# 11. Products bought together most often (self-merge on order)
baskets = pd.DataFrame({"order": [1, 1, 1, 2, 2, 3, 3, 3, 4, 4],
                        "item": ["tea", "milk", "sugar", "tea", "milk", "milk", "bread", "tea", "bread", "milk"]})
pairs = baskets.merge(baskets, on="order")
pairs = pairs[pairs["item_x"] < pairs["item_y"]]                       # each unordered pair once
print(pairs.groupby(["item_x", "item_y"]).size().sort_values(ascending=False).head(3))

# 12. DAU/MAU "stickiness": average daily active users ÷ monthly active users
rng = np.random.default_rng(0)
acts = pd.DataFrame({"user": rng.integers(1, 300, 4000),
                     "day": pd.Timestamp("2025-06-01") + pd.to_timedelta(rng.integers(0, 30, 4000), unit="D")})
dau = acts.groupby("day")["user"].nunique().mean()
mau = acts["user"].nunique()
print(f"average DAU {dau:.0f}, MAU {mau}, stickiness {dau / mau:.0%}")
```

**Output:**

```text
item_x  item_y
milk    tea       3
bread   milk      2
        tea       1
dtype: int64
average DAU 107, MAU 299, stickiness 36%
```

```python
# 13. NumPy: standardise each column, then find which column is furthest above average in each row
X = np.array([[1.0, 200, 3], [2.0, 180, 9], [3.0, 220, 6]])
Z = (X - X.mean(axis=0)) / X.std(axis=0)
print(Z.round(2) + 0.0, Z.argmax(axis=1), sep="\n")

# 14. NumPy: moving average of window 3 without a loop (two ways)
x = np.array([3, 5, 7, 6, 8, 12, 10])
c = np.cumsum(np.insert(x, 0, 0))
print(np.convolve(x, np.ones(3) / 3, mode="valid").round(2), ((c[3:] - c[:-3]) / 3).round(2))

# 15. NumPy: one-hot encode integer labels, and pairwise distances without loops
labels = np.array([2, 0, 1, 2])
print(np.eye(3, dtype=int)[labels])
P = np.array([[0, 0], [3, 4], [6, 8]])
print(np.sqrt(((P[:, None, :] - P[None, :, :]) ** 2).sum(axis=2)))
```

**Output:**

```text
[[-1.22  0.   -1.22]
 [ 0.   -1.22  1.22]
 [ 1.22  1.22  0.  ]]
[1 2 0]
[ 5.    6.    7.    8.67 10.  ] [ 5.    6.    7.    8.67 10.  ]
[[0 0 1]
 [1 0 0]
 [0 1 0]
 [0 0 1]]
[[ 0.  5. 10.]
 [ 5.  0.  5.]
 [10.  5.  0.]]
```

The cumulative-sum trick computes every window sum as a difference of two running totals: O(n) whatever the window size. `np.eye(3)[labels]` picks rows of the identity matrix, giving one-hot vectors.

**Common mistakes:**

- ❌ Ignoring ties ("top 2" with a tie for second place: say which rule you use).
- ❌ `groupby().head(N)` without sorting first (it takes the first N rows **as they appear**).
- ❌ Loops over rows in an interview when a `groupby` exists.
- ❌ Not checking the row count after a merge (silent fan-out).

### Practice

1. Using `sales`, find users whose spend **increased** every month they were active (compare each month's total with their previous active month).
2. Write the pandas for: "the percentage of users who bought again within 30 days of their first order".

<details>
<summary><b>Answer</b></summary>

```python
m = sales.groupby(["user", "month"])["amount"].sum().reset_index()
m["prev"] = m.groupby("user")["amount"].shift()
growing = m.groupby("user").apply(lambda d: bool((d["amount"].iloc[1:] > d["prev"].iloc[1:]).all()) and len(d) > 1,
                                  include_groups=False)
print(growing[growing].index.tolist())

first = sales.groupby("user")["date"].transform("min")
repeat = sales[(sales["date"] > first) & (sales["date"] <= first + pd.Timedelta(days=30))]["user"].nunique()
print(f"{repeat / sales['user'].nunique():.0%} of users bought again within 30 days")
```

**Output:**

```text
['u3', 'u4']
100% of users bought again within 30 days
```

</details>

**Learn more:** [LeetCode: 30 Days of Pandas](https://leetcode.com/studyplan/30-days-of-pandas/) · [StrataScratch: pandas interview questions](https://www.stratascratch.com/blog/python-pandas-interview-questions-for-data-science/)

---

## 67. Statistics, Probability and Product Interview Problems

### Theory

> **In simple words:** statistics rounds test whether you can reason with uncertainty out loud: small probability puzzles, explaining a concept to a non-expert, designing and reading an experiment, and diagnosing a metric change. Each problem below has a worked answer; cover the answer, solve it, then compare.

**A framework for open-ended metric questions** ("DAU dropped 10% yesterday"):

1. **Clarify:** which metric exactly, compared with what (yesterday? last Tuesday?), how sudden, which platforms?
2. **Check the data first:** a logging change, a pipeline delay, a bot filter, a time-zone shift?
3. **Segment:** platform, country, app version, new vs returning users, acquisition channel. Is the drop everywhere or in one place?
4. **Internal causes:** a release, an experiment, an outage, a pricing change.
5. **External causes:** holidays, competitors, news, seasonality.
6. **Conclude and recommend:** the most likely cause, the evidence, the next check.

### Worked problems

**1. Coin flips.** A fair coin is flipped 10 times. What's P(exactly 7 heads)? P(at least one head)?

<details>
<summary><b>Answer</b></summary>

P(7 heads) = C(10, 7) / 2¹⁰ = 120 / 1024 ≈ **0.117**. P(at least one head) = 1 − P(no heads) = 1 − 1/1024 ≈ **0.999**.

```python
from math import comb
from scipy import stats
print(round(comb(10, 7) / 2**10, 4), round(stats.binom.pmf(7, 10, 0.5), 4), round(1 - 0.5**10, 4))
```

**Output:**

```text
0.1172 0.1172 0.999
```

</details>

**2. Two children.** A family has two children, at least one of whom is a girl. What's the probability both are girls?

<details>
<summary><b>Answer</b></summary>

Equally likely families: GG, GB, BG, BB. "At least one girl" leaves GG, GB, BG, so P(both girls) = **1/3**, not 1/2. (If you're told "the **older** child is a girl", the answer becomes 1/2: the condition changes what's known.)

```python
import numpy as np
rng = np.random.default_rng(1)
kids = rng.integers(0, 2, size=(200_000, 2))          # 1 = girl
at_least_one = kids.sum(axis=1) >= 1
print(round((kids[at_least_one].sum(axis=1) == 2).mean(), 3))
```

**Output:**

```text
0.335
```

</details>

**3. Expected value.** A game costs ₹10. Roll a die: win ₹30 on a 6, ₹10 on a 5, nothing otherwise. Should you play?

<details>
<summary><b>Answer</b></summary>

Expected winnings = 30 × 1/6 + 10 × 1/6 = 40/6 ≈ ₹6.67 per game; minus the ₹10 cost gives **−₹3.33 per game**. Don't play (unless you value the fun at more than ₹3.33).

</details>

**4. Fraud alert (Bayes).** 0.5% of transactions are fraud. A model flags 98% of frauds and 2% of good transactions. What share of flagged transactions are fraud?

<details>
<summary><b>Answer</b></summary>

Per 100,000 transactions: 500 fraud → 490 flagged; 99,500 good → 1,990 flagged. Precision = 490 / 2,480 ≈ **19.8%**. Most alerts are false alarms because fraud is rare, so the operations team needs a second-stage review or a stricter threshold (`machine-learning.md` covers precision/recall trade-offs).

</details>

**5. Explain a p-value to a product manager.** One or two sentences.

<details>
<summary><b>Answer</b></summary>

"If the new design really made no difference, a gap this big would show up by chance only about 1% of the time (p = 0.01). So we're fairly confident the difference is real; the confidence interval tells us how big it probably is."

</details>

**6. Sample size.** Baseline conversion 10%. You want to detect a lift to 11% with 80% power at α = 0.05. Roughly how many users per group?

<details>
<summary><b>Answer</b></summary>

n ≈ (1.96 + 0.84)² × (0.10 × 0.90 + 0.11 × 0.89) / 0.01² = 7.84 × 0.1879 / 0.0001 ≈ **14,700 per group**.

```python
from statsmodels.stats.power import NormalIndPower
from statsmodels.stats.proportion import proportion_effectsize
print(round(NormalIndPower().solve_power(proportion_effectsize(0.11, 0.10), alpha=0.05, power=0.8)))
```

**Output:**

```text
14744
```

</details>

**7. The A/B test "won" on day 3.** A colleague wants to stop the test because p = 0.03 after three days of a planned two weeks. What do you say?

<details>
<summary><b>Answer</b></summary>

Don't stop: checking early and stopping at the first p < 0.05 inflates false positives (Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls)'s simulation showed about 25% instead of 5%). Three days also miss weekly cycles and may reflect a novelty effect. Run the planned two weeks, or use a sequential method designed for early looks.

</details>

**8. Simpson's paradox.** Treatment A has a higher success rate than B for both mild and severe cases, but a lower rate overall. How?

<details>
<summary><b>Answer</b></summary>

A was given mostly to severe cases (which succeed less often), B mostly to mild ones. Overall rates mix different case difficulties. Compare within severity groups (or adjust for severity); Section [52](#52-correlation-covariance-and-causation) has the real kidney-stone numbers.

</details>

**9. Mean vs median salary.** A company's mean salary rose 8% but the median fell 2%. What happened?

<details>
<summary><b>Answer</b></summary>

The top earners got large raises (or a few highly paid people were hired), pulling the mean up, while typical employees saw small or negative changes (or many junior hires joined at lower salaries). Report the median for "typical" pay and look at the distribution (percentiles) before drawing conclusions.

</details>

**10. Measuring a new feature.** How would you measure the success of a "save for later" button in a shopping app?

<details>
<summary><b>Answer</b></summary>

Goal: help users who aren't ready to buy come back and buy later. **Primary metric:** purchase conversion within 14 days among users who saw the button (A/B test: button vs no button). **Secondary:** usage rate of the button, return visits, items purchased from the saved list. **Guardrails:** immediate conversion (it shouldn't cannibalise "buy now"), page load time. Run for at least two full weeks; segment new vs returning users.

</details>

**11. DAU dropped 10% yesterday.** Walk through your investigation.

<details>
<summary><b>Answer</b></summary>

Use the framework above: confirm the number (is yesterday's data complete? did a pipeline or logging change ship?); compare with the same weekday last week and holidays; segment by platform, app version, country and acquisition channel (a drop only on Android version 5.2 points to a bad release; a drop in one country to a local outage or holiday); check releases, experiments, outages and marketing changes; then report the most likely cause with evidence and the next step.

</details>

**12. Correlation from a dashboard.** Users who use feature X retain 2× better. Should we push everyone to use X?

<details>
<summary><b>Answer</b></summary>

Not on this evidence: engaged users are likely to both use X **and** retain (a confounder: engagement), so the correlation may not be causal. Test it: randomly prompt half of new users to try X and compare retention. If the prompted group retains better, pushing X helps.

</details>

**Learn more:** [Ace the Data Science Interview (Huo & Singh, book site)](https://www.acethedatascienceinterview.com/) · [Seeing Theory](https://seeing-theory.brown.edu/) · [Evan Miller: A/B testing tools](https://www.evanmiller.org/ab-testing/)

---

## 68. Cheat Sheet: Which Tool or Method When?

**Clue in the question → tool:**

| Clue | Use |
|---|---|
| "per", "for each", "by" | `groupby(...).agg(...)` (Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine)) |
| "compared with its group", "share of", "rank within" | `transform`, `rank` per group (Section [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking)) |
| "never", "without", "missing from" | anti-join: `merge(indicator=True)` / `~isin` |
| "previous", "since last", "consecutive" | sort + `shift`, `diff`, run-labelling with `cumsum` |
| "last 7 days", "moving average" | `rolling("7D")` (Section [38](#38-time-series-resample-rolling-shift-and-window-functions)) |
| "monthly", "weekly" | `resample` or `dt.to_period` |
| "as of that date", "price at the time" | `merge_asof` (Section [34](#34-combining-tables-ii-concat-validation-and-merge-pitfalls)) |
| "one row per X, columns per Y" | `pivot_table` / `unstack` |
| "typical value" | median (skewed) or mean (symmetric) |
| "is the difference real?" | CI for the difference + an appropriate test (Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests)) |
| "how many users do we need?" | power analysis (Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls)) |
| "effect of X holding Y constant" | regression (Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence)) |
| file bigger than memory | DuckDB or lazy Polars (Sections [41](#41-polars-fast-dataframes-with-lazy-queries)–[42](#42-duckdb-sql-on-dataframes-and-files)) |

**NumPy:**

| Task | Code |
|---|---|
| create | `np.array(lst)`, `np.zeros((r, c))`, `np.arange(a, b, step)`, `np.linspace(a, b, n)`, `rng = np.random.default_rng(42)` |
| inspect | `a.shape`, `a.ndim`, `a.dtype`, `a.size`, `a.nbytes` |
| select | `a[i, j]`, `a[:, 0]`, `a[a > 0]`, `a[[0, 2]]`, `np.where(cond, x, y)`, `np.select(conds, choices)` |
| maths | `a + b`, `a * 2`, `np.sqrt(a)`, `np.log1p(a)`, `a @ b`, `np.clip(a, lo, hi)` |
| summarise | `a.sum(axis=0)` (per column), `a.mean(axis=1)` (per row), `a.argmax()`, `np.percentile(a, 90)`, `np.nanmean(a)` |
| reshape | `a.reshape(3, -1)`, `a.T`, `a[:, None]`, `np.concatenate`, `np.stack`, `np.argsort` |
| linear algebra | `np.linalg.norm`, `np.linalg.solve(A, b)`, `np.linalg.eigh`, `np.linalg.lstsq` |
| floats | `np.isclose(x, y)`, `np.allclose(a, b)` |

**pandas:**

| Task | Code |
|---|---|
| read / write | `pd.read_csv(p, parse_dates=[...], usecols=[...], dtype={...})`, `pd.read_parquet(p, columns=[...])`, `pd.read_sql(q, con, params=...)`, `df.to_parquet(p)`, `df.to_csv(p, index=False)` |
| inspect | `df.shape`, `df.head()`, `df.info()`, `df.describe()`, `df["c"].value_counts()`, `df.isna().sum()`, `df.duplicated().sum()` |
| select | `df["c"]`, `df[["a", "b"]]`, `df.loc[mask, cols]`, `df.iloc[:5, :3]`, `df.query("a > 1 and b == 'x'")` |
| change | `df["new"] = ...`, `df.assign(new=lambda d: ...)`, `df.loc[mask, "c"] = v`, `df.rename(columns={...})`, `np.select(...)`, `s.map(dict)` |
| clean | `df.dropna(subset=[...])`, `s.fillna(v)`, `df.drop_duplicates(subset=[...], keep="last")`, `pd.to_numeric(s, errors="coerce")`, `pd.to_datetime(s, format=..., errors="coerce")`, `s.str.strip().str.lower()`, `s.str.extract(r"(\d+)")` |
| categories | `s.astype("category")`, `pd.cut(s, bins, labels=...)`, `pd.qcut(s, 4)` |
| sort / rank | `df.sort_values(["a", "b"], ascending=[True, False])`, `df.nlargest(5, "c")`, `s.rank(method="dense", ascending=False)` |
| group | `df.groupby("k")["v"].sum()`, `.agg(total=("v", "sum"), n=("id", "count"))`, `.transform("mean")`, `.filter(lambda g: ...)`, `.cumcount()`, `.shift()` |
| combine | `a.merge(b, on="k", how="left", validate="many_to_one", indicator=True)`, `pd.concat(frames, ignore_index=True)`, `pd.merge_asof(...)` |
| reshape | `df.pivot_table(index=, columns=, values=, aggfunc=, fill_value=0)`, `df.melt(id_vars=)`, `pd.crosstab(a, b)`, `df.explode("c")`, `s.unstack()` |
| time | `s.dt.month`, `s.dt.tz_convert("UTC")`, `df.set_index("date").resample("MS").sum()`, `s.rolling("7D").mean()`, `s.shift(1)`, `s.pct_change()`, `pd.DateOffset(months=1)` |
| memory | `df.memory_usage(deep=True)`, `pd.to_numeric(s, downcast="integer")`, `dtype_backend="pyarrow"`, `chunksize=` |

**Charts:**

| Task | Code |
|---|---|
| figure | `fig, ax = plt.subplots(figsize=(8, 4), layout="constrained")`; grids `plt.subplots(2, 2, sharey=True)`; `fig.subplot_mosaic("AAB;CCB")` |
| draw | `ax.plot`, `ax.bar` / `ax.barh`, `ax.scatter`, `ax.hist`, `ax.imshow`, `ax.fill_between`, `ax.axhline`, `ax.annotate` |
| label / save | `ax.set(title=, xlabel=, ylabel=)`, `ax.legend()`, `fig.savefig("c.png", dpi=200, bbox_inches="tight")` |
| Seaborn | `sns.histplot(data=df, x=, hue=, stat="density", common_norm=False)`, `sns.boxplot`, `sns.violinplot`, `sns.ecdfplot`, `sns.barplot(estimator=...)`, `sns.regplot`, `sns.heatmap(df.corr(), annot=True, cmap="RdBu", vmin=-1, vmax=1)`, `sns.relplot(..., col=)`, `sns.pairplot(df, hue=, corner=True)` |
| Plotly | `px.line(df, x=, y=, color=)`, `fig.write_html(path)`, `fig.write_image(path)` |

**Statistics:**

| Question | Tool |
|---|---|
| centre / spread | median & IQR (skewed), mean & std (symmetric); always look at the distribution |
| outliers | IQR fences or \|z\| > 3; investigate before removing |
| relationship | `df.corr()` (Pearson), `method="spearman"`; always a scatter plot |
| probability of a count | `stats.binom`, `stats.poisson` (`pmf`, `cdf`, `sf`) |
| uncertainty of a mean | SE = s/√n; t-interval; bootstrap for medians/ratios; Wilson for rates |
| two means | `stats.ttest_ind(a, b, equal_var=False)`; paired: `ttest_rel`; skewed: `mannwhitneyu` |
| two rates / two categories | `proportions_ztest`, `stats.chi2_contingency(table)`; small counts: `fisher_exact` |
| 3+ groups | `stats.f_oneway`, `stats.kruskal` |
| many tests | `multipletests(p, method="fdr_bh")` |
| A/B sample size | `NormalIndPower().solve_power(proportion_effectsize(p2, p1), alpha=0.05, power=0.8)` |
| effects with controls | `smf.ols("y ~ x1 + x2 + C(cat)", data=df).fit().summary()` |

**Tool choice:** pandas (up to a few GB, the whole ecosystem) · Polars (faster, lazy, bigger) · DuckDB (SQL on files and DataFrames, bigger than RAM) · Spark or a warehouse (terabytes, shared data) · PostgreSQL (application data).

**Habits:** look before you summarise · split before learning anything from data · check row counts after every merge, and use `validate=` · store dates as dates, times in UTC · Parquet over CSV · seed your random generators · report effect sizes with CIs, not just p-values · label every chart axis with units · write findings down, answer first.

---

## 69. Most Asked Data Science Theory Questions

**Data handling**

1. **Why is NumPy faster than Python lists?** → Arrays store raw numbers of one type in one contiguous block, and operations run as compiled loops (vectorisation) instead of the interpreter handling one object at a time (Section [6](#6-why-numpy-arrays-vs-lists-and-how-arrays-sit-in-memory)).
2. **What is broadcasting?** → NumPy's rule for combining arrays of different shapes: compare shapes from the right; sizes must match or be 1, and size-1 axes are stretched. Example: a `(3, 4)` table minus a `(4,)` row of column means.
3. **View vs copy in NumPy?** → Slices are views (shared memory); boolean and fancy indexing return copies. Use `.copy()` for independence.
4. **Series vs DataFrame?** → A Series is one labelled column of one type; a DataFrame is a table of Series sharing a row index.
5. **`loc` vs `iloc`?** → `loc` selects by label (slices include the end); `iloc` by position (slices exclude the end).
6. **What changed in pandas 3.0?** → Copy-on-write is always on (derived objects behave as copies; chained assignment never modifies the original, so use `df.loc[...] = ...`), and text columns get a dedicated `str` dtype (Arrow-backed when PyArrow is installed) instead of `object`.
7. **`apply` vs vectorised operations?** → Vectorised column operations run in compiled code; `apply` calls Python per value or row and can be 100–1000× slower.
8. **`merge` vs `join` vs `concat`?** → `merge` combines on key columns (SQL join); `join` merges on the index; `concat` stacks along rows or columns without matching keys.
9. **Inner vs left vs outer join?** → Inner keeps matches only; left keeps every left row (NaN where unmatched); outer keeps everything from both sides.
10. **What causes row explosion in a merge, and how do you prevent it?** → Duplicate keys on both sides multiply rows; check key uniqueness and pass `validate="many_to_one"` (or `one_to_one`).
11. **`groupby` + `agg` vs `transform`?** → `agg` returns one row per group; `transform` returns values aligned with the original rows (a SQL window function).
12. **Wide vs long data?** → Wide spreads one variable across columns; long (tidy) has one row per observation. `melt` goes wide → long, `pivot_table` long → wide.
13. **How do you handle missing data?** → Understand why it's missing (MCAR/MAR/MNAR), then drop, fill (median, mode, "Unknown", forward-fill, model-based) and/or add a missing indicator; fit fill values on training data only.
14. **How would you process a 50 GB CSV on a laptop?** → Don't load it whole: convert to Parquet in chunks, read only needed columns, use small dtypes and categories, or query it with DuckDB or lazy Polars.
15. **What is Apache Arrow and why does it matter?** → A standard columnar in-memory format; pandas, Polars, DuckDB and Spark share data through it without copying, and it stores text efficiently.

**Statistics and probability**

16. **Mean vs median?** → Median for skewed data or with outliers (income, prices, latency); mean for roughly symmetric data or when totals matter.
17. **Standard deviation vs standard error?** → Std measures the spread of individual values; SE = s/√n measures how much a sample mean would vary between samples.
18. **Explain the central limit theorem.** → Means of reasonably large random samples are approximately normal, whatever the data's shape; it justifies normal-based CIs and tests for means.
19. **What is a p-value?** → The probability of a result at least as extreme as the observed one, assuming the null hypothesis is true. Not the probability the null is true, and not the size of the effect.
20. **Type I vs Type II error, and power?** → Type I = false positive (probability α); Type II = false negative (β); power = 1 − β, rising with sample size and effect size.
21. **What is a 95% confidence interval?** → A range from a method that captures the true value in 95% of repeated samples; it shows an estimate's precision.
22. **When would you use the bootstrap?** → For CIs of statistics without simple formulas (median, percentiles, ratios) or when assumptions are doubtful: resample the data with replacement many times and take percentiles of the recomputed statistic.
23. **t-test vs Mann–Whitney vs chi-square?** → t-test (Welch) compares means of numeric data; Mann–Whitney compares distributions via ranks (skewed data, outliers); chi-square tests whether categorical variables (or rates) are related.
24. **What is the multiple comparisons problem?** → Many tests make some false positives likely; correct with Bonferroni or Benjamini–Hochberg (FDR).
25. **Correlation vs causation?** → Correlation measures co-movement; causation needs an experiment or careful causal methods, because confounders and reverse causation create correlation.
26. **Pearson vs Spearman?** → Pearson measures linear association and is outlier-sensitive; Spearman uses ranks and captures any monotonic association.
27. **What is Simpson's paradox?** → A trend in every group reverses when groups are combined, because group sizes or mixes differ; check important segments.
28. **Bayes' rule, and why do rare-event tests give many false positives?** → P(A|B) = P(B|A)·P(A)/P(B). When the condition is rare, a small false-positive rate on the huge negative group outnumbers the true positives.
29. **Which distribution for clicks, orders per minute, waiting times, heights, incomes?** → Binomial, Poisson, exponential, normal, log-normal.
30. **What does a regression coefficient mean?** → The expected change in y for a one-unit increase in that x, holding the other predictors constant; its CI shows the uncertainty. It isn't causal without a strong design.
31. **Confidence vs prediction interval in regression?** → The confidence interval covers the **average** y at a given x; the prediction interval covers an **individual** new observation and is always wider.

**Experiments**

32. **How do you design an A/B test?** → Hypothesis and primary metric, guardrails, α, power and MDE → sample size → randomise by user → run full weeks without peeking → check SRM → report the effect with its CI.
33. **Why is peeking a problem?** → Every look is another chance for noise to cross the threshold; stopping at the first p < 0.05 inflates false positives well above α. Use a fixed horizon or sequential testing.
34. **What is a sample ratio mismatch?** → Group sizes that differ significantly from the planned split; a sign of an assignment or logging bug that invalidates the test until explained.
35. **What are novelty and primacy effects?** → Users react to any change at first (curiosity, or resistance), so early results can mislead; run long enough and compare early vs late weeks.
36. **Statistical vs practical significance?** → A tiny, worthless effect can be significant with huge samples; judge the effect size and its CI against business value.

**Practice and production**

37. **What is data leakage?** → Training information unavailable at prediction time (test-set statistics in preprocessing, target-derived or future features), making models look better than they are.
38. **One-hot vs ordinal vs target encoding?** → One-hot for unordered categories with few values; ordinal for ordered ones; target encoding (smoothed, out-of-fold) for many categories.
39. **Why scale features?** → Distance- and gradient-based models are dominated by large-scale features otherwise; tree models don't need scaling.
40. **How do you detect outliers, and should you remove them?** → IQR fences, z-scores, plots, domain rules; investigate first, remove only clear errors, and use robust methods for real extreme values.
41. **What makes a pipeline production-ready?** → Functions with clear inputs/outputs, parameters instead of hard-coding, idempotent loads (overwrite partitions), validation that fails loudly, logging and monitoring, tests, and an orchestrator for scheduling and retries.
42. **What are the data-quality dimensions?** → Completeness, validity, uniqueness, consistency, accuracy and timeliness (freshness).
43. **How do you choose a chart?** → From the question: line for change over time, sorted bars for comparisons, histogram/box/ECDF for distributions, scatter for relationships, heatmap for many correlations; bars start at zero; the message goes in the title.
44. **How do you present an analysis to executives?** → Answer first (with the key number and its uncertainty), 2–3 pieces of evidence, a recommendation, caveats; details in an appendix.
45. **pandas, Polars or DuckDB?** → pandas for everyday work up to a few GB and the widest ecosystem; Polars for speed and lazy pipelines; DuckDB for SQL-shaped questions and data bigger than RAM.

---

## 70. Glossary: Every Term in These Notes

Every technical term from the **Words to know** boxes, A to Z, with a plain definition and a link to the section that teaches it (the first link is where it's introduced). Terms are listed by their main word; symbols and code names (like `.str` or `ddof`) are sorted by their first letter.


### A

- **A/B test:** an experiment that randomly splits users between two versions and compares a metric (Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls)). *(Section [15](#15-random-numbers-and-simulation))*
- **Absolute vs relative lift:** 4.0% → 4.5% is +0.5 points absolute, +12.5% relative. *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **Activation function / ReLU:** in neural networks, a function applied after each layer's arithmetic; **ReLU** (rectified linear unit) is `max(0, x)`: negatives become 0. *(Section [11](#11-vectorised-maths-and-universal-functions))*
- **`aggfunc`:** how to combine several values landing in the same cell (default `"mean"`). *(Section [35](#35-reshaping-pivot_table-melt-crosstab-and-explode))*
- **Aggregate / aggregation function:** a function that turns a group's many values into one: `sum`, `mean`, `count`, `max`, … *(Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine))*
- **Aggregate features:** summaries of a customer's history (order count, average spend, days since last order), built with `groupby` from an event table. *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Aggregation (aggregate function, reduction):** a function that turns many values into fewer: `sum`, `mean`, `max`, … *(Section [12](#12-aggregations-and-the-axis-argument))*
- **AI coding assistant:** an LLM-based tool that writes, explains and debugs code (Claude, GitHub Copilot, Jupyter AI, assistants built into IDEs). *(Section [64](#64-whats-new-modern-data-tooling-20232026))*
- **Algorithm:** an exact, step-by-step procedure for solving a problem (sorting a list, fitting a line). *(Section [1](#1-how-to-use-these-notes-and-what-data-scientists-do))*
- **Alias:** a short nickname for an imported library, like `import pandas as pd`. *(Section [2](#2-setting-up-python-virtual-environments-uv-and-jupyter-notebooks))*
- **Alignment:** matching values by label before combining them. Labels missing on one side give `NaN`. *(Section [17](#17-pandas-series-labelled-1d-data))*
- **Alternative hypothesis (H₁ or Hₐ):** what you're looking for evidence of: the groups differ. *(Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests))*
- **Analysis:** working out what the data says: totals, averages, trends, differences between groups. *(Section [1](#1-how-to-use-these-notes-and-what-data-scientists-do))*
- **Anchor:** a position, not a character: `^` (start of the string), `$` (end). *(Section [28](#28-text-data-the-str-accessor-and-regular-expressions))*
- **Animation frame:** a column whose values become the frames of an animation (`animation_frame="year"`). *(Section [49](#49-interactive-charts-with-plotly))*
- **Annotate (`annot=True`):** write each cell's number inside it. *(Section [48](#48-heatmaps-pair-plots-and-correlation-charts))*
- **Annotation:** text or an arrow pointing at a specific point. *(Section [45](#45-styling-annotation-and-saving-charts))*
- **ANOVA F-score (as a screening tool):** how different a numeric column's averages are across groups, relative to the spread inside groups. High F = the column separates the groups well (Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests)). *(Section [60](#60-a-complete-exploratory-data-analysis-eda))*
- **Anti-join:** rows in the left table with **no** match in the right ("customers who never ordered"). *(Section [33](#33-combining-tables-i-merge-and-join-types))*
- **AOV (average order value):** total revenue divided by the number of orders. *(Section [42](#42-duckdb-sql-on-dataframes-and-files))*
- **Apache Arrow:** a standard **columnar in-memory** format (and the `pyarrow` library). Columns are stored contiguously, strings efficiently, missing values as a compact bitmap. *(Section [40](#40-memory-dtypes-categoricals-chunking-and-apache-arrow), [64](#64-whats-new-modern-data-tooling-20232026))*
- **API (application programming interface):** a defined way for programs to talk to each other. A **web API** answers HTTP requests, usually with JSON. *(Section [20](#20-reading-from-databases-and-web-apis))*
- **`apply`:** runs a Python function on each value (Series) or each row/column (DataFrame). Flexible but slow: it's a hidden Python loop. *(Section [24](#24-adding-and-changing-columns-arithmetic-assign-map-apply-and-npselect))*
- **`apply` (on groups):** run any function on each group's sub-table; results are glued together. Most flexible, slowest. *(Section [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking))*
- **argmax / argmin:** the **position** of the biggest / smallest value, not the value itself. *(Section [12](#12-aggregations-and-the-axis-argument))*
- **Array (ndarray, "n-dimensional array"):** NumPy's container: a grid of values that all have the **same type**. *(Section [6](#6-why-numpy-arrays-vs-lists-and-how-arrays-sit-in-memory))*
- **Artist:** Matplotlib's name for anything drawn: lines, text, bars, even the axes. Everything visible is an artist with properties you can set. *(Section [44](#44-matplotlib-anatomy-figures-axes-and-subplots))*
- **As-of merge (`merge_asof`):** match each row to the **most recent** row on or before it in time (the exchange rate in effect on the order date). *(Section [34](#34-combining-tables-ii-concat-validation-and-merge-pitfalls))*
- **`as_index=False` / `reset_index()`:** keep the keys as ordinary columns instead of moving them into the index. *(Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine))*
- **Ascending / descending:** smallest first / largest first. *(Section [23](#23-sorting-ranking-and-top-n))*
- **Assertion:** a check in code that stops the program if something that must be true isn't: `assert df["qty"].ge(1).all()`. *(Section [30](#30-outliers-and-data-validation))*
- **`assign`:** returns a **new** DataFrame with columns added; ideal for chains (Section [25](#25-method-chaining-and-copy-on-write-pandas-3)). *(Section [24](#24-adding-and-changing-columns-arithmetic-assign-map-apply-and-npselect))*
- **Axes (`ax`):** **one chart**, with its own x-axis, y-axis, title and data. (Plural-looking but singular. An Axes contains two **axis** objects, the x-axis and y-axis.) *(Section [43](#43-your-first-charts-with-matplotlib))*
- **Axes-level vs figure-level functions:** axes-level (`scatterplot`, `boxplot`, …) draw on one `ax` you pass; figure-level (`relplot`, `catplot`, `displot`, `lmplot`) create their own figure and support facets. *(Section [47](#47-seaborn-ii-relationships-categories-and-facets))*

### B

- **Backend (`dtype_backend="pyarrow"`):** telling pandas to store columns as Arrow arrays instead of NumPy arrays. *(Section [40](#40-memory-dtypes-categoricals-chunking-and-apache-arrow))*
- **Backfill:** re-running a pipeline for past dates (after a bug fix or a new column). *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Bandwidth:** how wide each KDE bump is. Too narrow → wiggly; too wide → over-smoothed. *(Section [46](#46-seaborn-i-distributions))*
- **Base rate:** how common something is in the population (the prior). Ignoring it is the **base-rate fallacy**. *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **Baseline:** the control's current metric value (4% conversion). *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **Basket analysis:** finding products that are bought together in the same order. *(Section [66](#66-interview-problems-pandas-numpy-and-sql-style-questions))*
- **Batch vs streaming:** processing data in scheduled chunks (every night) vs continuously as events arrive (Kafka, Flink). *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Bayes' rule:** P(A | B) = P(B | A) × P(A) / P(B). *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **`between(a, b)`:** "a ≤ value ≤ b" (both ends included by default; SQL `BETWEEN`). *(Section [22](#22-filtering-rows-conditions-isin-between-and-query))*
- **BI tool (business intelligence):** point-and-click dashboard software used across companies: Power BI, Tableau, Looker, Metabase, Apache Superset. *(Section [49](#49-interactive-charts-with-plotly))*
- **Big-O:** how the work grows with the input size n: O(n) doubles when n doubles; O(n²) quadruples. *(Section [39](#39-performance-vectorise-avoid-loops-and-measure))*
- **Bin:** one bar's range in a histogram (e.g. order values from 500 to 600). *(Section [43](#43-your-first-charts-with-matplotlib))*
- **Bin edges:** the boundary values. `(0, 500]` means "above 0, up to and including 500": a **round** bracket excludes the edge, a **square** bracket includes it. *(Section [29](#29-categorical-data-and-binning-cut-and-qcut))*
- **Binning (discretisation, bucketing):** grouping numbers into ranges called **bins**. *(Section [29](#29-categorical-data-and-binning-cut-and-qcut))*
- **Bit / byte:** a bit is a single 0 or 1; a byte is 8 bits. *(Section [8](#8-shape-dimensions-and-dtypes))*
- **Boolean:** a `True`/`False` value (named after the mathematician George Boole). *(Section [10](#10-boolean-masks-fancy-indexing-and-npwhere))*
- **Boolean (binary):** two values: yes/no, true/false, clicked/didn't. *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **Bootstrap:** estimating a statistic's uncertainty by repeatedly **resampling the data with replacement** and recomputing the statistic. *(Section [56](#56-confidence-intervals-and-the-bootstrap))*
- **Bottleneck:** the slowest part, which limits the whole program. Speeding up anything else barely helps. *(Section [39](#39-performance-vectorise-avoid-loops-and-measure))*
- **Box plot (box-and-whisker):** the box spans the middle 50% (Q1 to Q3, the **IQR**); the line is the **median**; whiskers reach the furthest points within 1.5 × IQR; dots beyond are possible outliers (Section [30](#30-outliers-and-data-validation)). *(Section [46](#46-seaborn-i-distributions))*
- **Broadcasting:** NumPy's rules for matching up arrays of different shapes in element-wise operations. *(Section [13](#13-broadcasting-maths-between-arrays-of-different-shapes))*
- **Business day:** Monday–Friday (holidays can be added). *(Section [37](#37-dates-and-times-parsing-dt-time-zones-and-periods))*

### C

- **Capture group:** brackets `( )` around the part you want to **extract**. A **named group** `(?P<name>...)` becomes a column name. *(Section [28](#28-text-data-the-str-accessor-and-regular-expressions))*
- **Cardinality:** how many distinct values a column has. Low cardinality (a few cities) suits `category`; high cardinality (customer emails) doesn't. *(Section [29](#29-categorical-data-and-binning-cut-and-qcut), [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Cardinality / relationship:** how many rows can match on each side: one-to-one (1:1), one-to-many (1:m), many-to-one (m:1), many-to-many (m:m). *(Section [33](#33-combining-tables-i-merge-and-join-types))*
- **Casting:** converting an array to another type with `astype`. *(Section [8](#8-shape-dimensions-and-dtypes))*
- **Categorical (qualitative) data:** labels that put observations into groups. *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **Category dtype:** pandas' type for repeated labels. Internally: a list of the distinct labels (the **categories**) and a small integer **code** per row pointing into it. *(Section [29](#29-categorical-data-and-binning-cut-and-qcut))*
- **Causation:** changing x actually **changes** y. *(Section [52](#52-correlation-covariance-and-causation))*
- **Caveats / limitations:** what the analysis can't tell you and why. *(Section [63](#63-communicating-results-reports-dashboards-and-data-storytelling))*
- **CDF (cumulative distribution function):** P(X ≤ x). Works for both kinds; it's the theoretical version of the ECDF (Section [46](#46-seaborn-i-distributions)). *(Section [54](#54-probability-distributions-normal-binomial-poisson-and-more))*
- **Central Limit Theorem (CLT):** for large enough samples (often n ≥ 30, more for very skewed data), the sample mean is approximately **normal**, centred on the true mean, **whatever shape** the original data has. *(Section [55](#55-sampling-the-central-limit-theorem-and-standard-error))*
- **Central tendency:** where the middle of the data is. *(Section [51](#51-describing-data-centre-spread-and-shape))*
- **Chained assignment:** assigning through two selections in a row, like `df[mask]["col"] = 5`. Under copy-on-write it **never** changes `df`. *(Section [25](#25-method-chaining-and-copy-on-write-pandas-3))*
- **Character class:** a set of allowed characters in brackets: `[aeiou]`, `[0-9]`, `[A-Za-z]`. *(Section [28](#28-text-data-the-str-accessor-and-regular-expressions))*
- **Chartjunk:** decoration that adds nothing: 3D effects, shadows, heavy gridlines, clip art. *(Section [50](#50-choosing-the-right-chart-and-not-misleading))*
- **Cherry-picking:** choosing a date range or subset that supports a story while hiding the rest. *(Section [50](#50-choosing-the-right-chart-and-not-misleading))*
- **Choropleth:** a map with regions coloured by value. *(Section [50](#50-choosing-the-right-chart-and-not-misleading))*
- **Chunk:** a piece of a big file read at a time. *(Section [19](#19-reading-and-writing-files-csv-excel-json-and-parquet))*
- **Chunking:** reading and processing a file in pieces of, say, 100,000 rows, keeping only small running results. *(Section [40](#40-memory-dtypes-categoricals-chunking-and-apache-arrow))*
- **Churn:** customers leaving (cancelling, or no longer buying); **churn rate** = the share who leave in a period. *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Class balance:** how evenly the target's categories are represented. *(Section [60](#60-a-complete-exploratory-data-analysis-eda))*
- **Classifier:** a model that assigns each item to a category (fraud / not fraud, spam / not spam). *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **Cloud object storage (S3):** pay-as-you-go online file storage (Amazon S3, Google Cloud Storage, Azure Blob) where data lakes keep their files. *(Section [19](#19-reading-and-writing-files-csv-excel-json-and-parquet))*
- **Clustering (k-means):** grouping similar points together without labels; **k-means** repeatedly assigns each point to its nearest of k centres and moves each centre to the mean of its points (`machine-learning.md`). *(Section [13](#13-broadcasting-maths-between-arrays-of-different-shapes))*
- **Coefficient (β, "beta"):** how much y changes when that x rises by 1, **holding the other x's constant**. *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*
- **Coefficient of variation (CV):** std ÷ mean, spread relative to size (compare the spread of elephants' and mice's weights). *(Section [51](#51-describing-data-centre-spread-and-shape))*
- **Coerce:** force conversion and turn anything that fails into missing (`errors="coerce"`), instead of crashing. *(Section [27](#27-duplicates-data-types-and-type-conversion))*
- **Cohort:** a group of users who share a starting point, such as everyone who signed up in March. *(Section [22](#22-filtering-rows-conditions-isin-between-and-query))*
- **Colormap (cmap):** a mapping from numbers to colours, used for heatmaps and colour scales. *(Section [45](#45-styling-annotation-and-saving-charts))*
- **Colour-blind safe:** distinguishable for people with colour-vision deficiency (about 1 in 12 men). Avoid red–green pairs. *(Section [45](#45-styling-annotation-and-saving-charts))*
- **Columnar vs row-based:** a row-based file (CSV) stores row 1, then row 2, …; a columnar file stores all of column 1, then all of column 2, … Reading three columns of a columnar file skips the rest of the file. *(Section [19](#19-reading-and-writing-files-csv-excel-json-and-parquet))*
- **Columnar, vectorised engine:** processes columns in batches of values at a time, like NumPy, which suits aggregation. *(Section [42](#42-duckdb-sql-on-dataframes-and-files))*
- **Columns:** the column labels (`df.columns`). **Index:** the row labels (`df.index`). *(Section [18](#18-dataframes-creating-inspecting-and-understanding-a-table))*
- **Compatible shapes:** shapes that broadcasting can line up. *(Section [13](#13-broadcasting-maths-between-arrays-of-different-shapes))*
- **Compiled code (C):** code translated ahead of time into machine instructions. It runs far faster than Python, which is **interpreted** (read and executed line by line, checking types on every step). *(Section [6](#6-why-numpy-arrays-vs-lists-and-how-arrays-sit-in-memory))*
- **Complement (not A):** P(not A) = 1 − P(A). *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **Comprehension:** a one-line way to build a list, dict or set from another collection. *(Section [3](#3-python-refresher-for-data-work-lists-dicts-comprehensions-and-functions))*
- **Compression:** storing data in fewer bytes by encoding patterns (a column of "Pune, Pune, Pune" compresses extremely well). *(Section [19](#19-reading-and-writing-files-csv-excel-json-and-parquet))*
- **Concatenate:** join arrays end to end along an **existing** axis. **Stack:** join them along a **new** axis. *(Section [14](#14-reshaping-stacking-splitting-and-sorting), [34](#34-combining-tables-ii-concat-validation-and-merge-pitfalls))*
- **Conditional probability P(A | B):** the probability of A **given** B happened = P(A and B) / P(B). Read "|" as "given". *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **Confidence interval (CI):** a range showing how uncertain an estimate is. Seaborn's default error bar is a **95% CI** of the mean (Section [56](#56-confidence-intervals-and-the-bootstrap) explains it fully); a short bar means a precise estimate. *(Section [47](#47-seaborn-ii-relationships-categories-and-facets))*
- **Confidence level:** the long-run success rate of the method (95%, 90%, 99%). *(Section [56](#56-confidence-intervals-and-the-bootstrap))*
- **Confounder (lurking variable):** a third factor that drives both x and y, creating a correlation between them (summer drives both ice-cream sales and drownings). *(Section [52](#52-correlation-covariance-and-causation))*
- **Confounding (again):** a regression can "control for" confounders **you include**; it can't fix ones you didn't measure. *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*
- **Connection:** an open link to a database that queries go through. *(Section [20](#20-reading-from-databases-and-web-apis))*
- **Connection string (URL):** text describing how to reach a database: `postgresql+psycopg://user:password@host:5432/dbname`. *(Section [20](#20-reading-from-databases-and-web-apis))*
- **Constrained layout:** Matplotlib's automatic spacing engine that stops titles and labels overlapping. *(Section [44](#44-matplotlib-anatomy-figures-axes-and-subplots))*
- **Context:** where an expression is used: `select` (choose/compute columns), `with_columns` (add columns), `filter` (rows), `group_by(...).agg(...)` (summaries). *(Section [41](#41-polars-fast-dataframes-with-lazy-queries))*
- **Context manager (`with`):** `with open(path) as f:` opens a file and **guarantees it is closed** afterwards, even if an error happens. *(Section [5](#5-reading-files-with-plain-python-text-csv-and-json))*
- **Continuous:** can take any value in a range (height 172.4 cm, temperature, price). *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **Control / treatment (variant):** the current experience / the new one. *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **Conversion rate:** the share of users who complete a goal action (orders ÷ visitors). *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **Copy:** a new array with its **own** memory. Independent of the original. *(Section [9](#9-indexing-and-slicing-1d-and-2d-views-vs-copies))*
- **Copy-on-write (CoW):** pandas 3's rule: any DataFrame or Series derived from another **behaves as an independent copy**. Data is actually copied only when one side is modified (that's the "on write"), so it's still fast. *(Section [25](#25-method-chaining-and-copy-on-write-pandas-3))*
- **Correlation (Pearson's r):** a number from −1 to +1 measuring how strongly two numeric variables move together in a straight line: +1 perfectly together, −1 perfectly opposite, 0 no straight-line relationship (Section [52](#52-correlation-covariance-and-causation)). *(Section [48](#48-heatmaps-pair-plots-and-correlation-charts))*
- **Correlation matrix:** the table of correlations for every pair of columns; symmetric, with 1s on the diagonal. *(Section [48](#48-heatmaps-pair-plots-and-correlation-charts))*
- **Cosine similarity:** the dot product divided by both lengths: 1 = same direction, 0 = unrelated (perpendicular), −1 = opposite. Used to compare text **embeddings** in AI search. *(Section [16](#16-linear-algebra-basics-dot-products-matrix-multiplication-and-solving-equations))*
- **Covariance:** the average of (x − mean of x) × (y − mean of y). Positive when x and y tend to be above their means together; its size depends on the units, so it's hard to read directly. *(Section [52](#52-correlation-covariance-and-causation))*
- **CPU / GPU:** the computer's main processor / a graphics processor with thousands of small cores, which does the same arithmetic on many numbers at once (ideal for deep learning). *(Section [6](#6-why-numpy-arrays-vs-lists-and-how-arrays-sit-in-memory))*
- **Critical value:** the multiplier for the SE: 1.96 for 95% with the normal distribution; slightly bigger from the **t distribution** for small samples. *(Section [56](#56-confidence-intervals-and-the-bootstrap))*
- **Cron:** the classic Unix tool for running a command on a schedule ("every day at 06:00"). *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Cross join:** every row of the left with every row of the right (all combinations). *(Section [33](#33-combining-tables-i-merge-and-join-types))*
- **Cross-section (`xs`):** select all rows with a given value on one level. *(Section [36](#36-multiindex-stack-and-unstack))*
- **Crosstab (contingency table):** a table of **counts** of each combination of two categorical columns. *(Section [35](#35-reshaping-pivot_table-melt-crosstab-and-explode))*
- **CSV (comma-separated values):** a text file where each line is a row and commas separate the values. The first line is usually the **header** (the column names). *(Section [5](#5-reading-files-with-plain-python-text-csv-and-json))*
- **CTE (common table expression):** a named sub-query written with `WITH name AS (...)`, making long SQL readable. *(Section [42](#42-duckdb-sql-on-dataframes-and-files))*
- **Cumulative sum (cumsum):** a running total: each element is the sum of everything up to it. *(Section [12](#12-aggregations-and-the-axis-argument))*
- **Cumulative within groups:** `cumsum`, `cumcount` (0, 1, 2… within each group), `cummax` per group. *(Section [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking))*
- **CUPED:** a variance-reduction technique using each user's pre-experiment behaviour to make tests more sensitive. *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **`cut`:** bins by edges **you choose** (or equal-width ranges). *(Section [29](#29-categorical-data-and-binning-cut-and-qcut))*

### D

- **DAG (directed acyclic graph):** the dependency graph of pipeline steps (B runs after A; no loops). *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Dashboard:** a page of charts and numbers that updates automatically, for **monitoring**. *(Section [63](#63-communicating-results-reports-dashboards-and-data-storytelling))*
- **Dashboard / data app:** an interactive web page with charts and controls (filters, dropdowns): **Streamlit**, **Dash**, **Gradio**, **Panel**. *(Section [49](#49-interactive-charts-with-plotly))*
- **Data:** recorded facts. A list of orders, sensor readings, survey answers, web clicks. *(Section [1](#1-how-to-use-these-notes-and-what-data-scientists-do))*
- **Data contract:** an agreement between the team producing data and the teams using it: schema, meaning, quality rules and freshness. *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Data dictionary:** a document describing every column: meaning, unit, type, allowed values, source. *(Section [60](#60-a-complete-exploratory-data-analysis-eda))*
- **Data leakage:** information from the test set (or from the future) sneaking into training, making the model look better than it will be in real use. *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Data pipeline:** an automated sequence of steps that moves and transforms data from sources to destinations. *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Data quality dimensions:** **completeness** (nothing missing), **validity** (values follow the rules), **uniqueness** (no duplicates), **consistency** (agrees across tables), **accuracy** (matches reality), **timeliness / freshness** (up to date). *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Data storytelling:** presenting data as a narrative: context → tension (what changed or what's wrong) → resolution (what to do). *(Section [63](#63-communicating-results-reports-dashboards-and-data-storytelling))*
- **Data validation:** automatically checking data against rules: types, ranges, allowed values, uniqueness, relationships between columns. *(Section [30](#30-outliers-and-data-validation))*
- **Data warehouse / data lake / lakehouse:** a database built for analytics (Snowflake, BigQuery, Redshift) / cheap storage of raw files (Parquet on S3) / a lake with warehouse features (Delta Lake, Apache Iceberg, DuckLake). *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Data-ink:** the ink (pixels) that shows data, as opposed to decoration. Maximise it (Edward Tufte's idea). *(Section [50](#50-choosing-the-right-chart-and-not-misleading))*
- **Database:** a program that stores tables and answers questions about them (PostgreSQL, MySQL, SQLite, BigQuery, Snowflake). *(Section [20](#20-reading-from-databases-and-web-apis))*
- **DataFrame:** a 2D labelled table: rows × columns. *(Section [18](#18-dataframes-creating-inspecting-and-understanding-a-table))*
- **DataFrame library:** pandas, Polars, and others with a table API. *(Section [64](#64-whats-new-modern-data-tooling-20232026))*
- **Dataframe-agnostic code:** code written once that runs on pandas, Polars and others (**Narwhals**, **Ibis**). *(Section [64](#64-whats-new-modern-data-tooling-20232026))*
- **Dataset:** one collection of data about one subject, usually a table (or a few related tables). *(Section [1](#1-how-to-use-these-notes-and-what-data-scientists-do))*
- **Date / time (temporal):** a moment or a period; has order **and** distance (days between). *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **DatetimeIndex:** an index made of timestamps; needed for `resample` and time-based `rolling`. *(Section [38](#38-time-series-resample-rolling-shift-and-window-functions))*
- **DAU / WAU / MAU:** daily / weekly / monthly active users: the number of distinct users active in a day, week or month. *(Section [66](#66-interview-problems-pandas-numpy-and-sql-style-questions))*
- **Daylight saving time (DST):** moving clocks forward in spring and back in autumn in some countries; creates missing and repeated local hours. *(Section [37](#37-dates-and-times-parsing-dt-time-zones-and-periods))*
- **dbt (data build tool):** writes warehouse transformations as SQL `SELECT` files with tests and documentation; the standard for ELT. *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Delimiter (separator):** the character between values: comma, semicolon (common in Europe), or tab (a **TSV** file). *(Section [5](#5-reading-files-with-plain-python-text-csv-and-json))*
- **Density:** a scale where the area under the curve is 1, so groups of different sizes can be compared by shape. *(Section [46](#46-seaborn-i-distributions))*
- **Dependent variable (outcome, response, y):** what you're explaining (sales). *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*
- **Derived column (feature):** a column calculated from others. *(Section [24](#24-adding-and-changing-columns-arithmetic-assign-map-apply-and-npselect))*
- **Descriptive statistics:** numbers that summarise data you have. (**Inferential statistics**, Sections [55](#55-sampling-the-central-limit-theorem-and-standard-error)–[59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence), uses a sample to say something about a bigger population.) *(Section [51](#51-describing-data-centre-spread-and-shape))*
- **Determinant:** a single number computed from a square matrix; if it's 0, the matrix has no inverse (the equations have no single solution). *(Section [16](#16-linear-algebra-basics-dot-products-matrix-multiplication-and-solving-equations))*
- **Dict (dictionary):** a collection of **key → value** pairs: `{"city": "Pune", "qty": 5}`. Get a value by its key. *(Section [3](#3-python-refresher-for-data-work-lists-dicts-comprehensions-and-functions))*
- **diff / pct_change:** change from the previous value, absolute / as a fraction. *(Section [38](#38-time-series-resample-rolling-shift-and-window-functions))*
- **Dimension / axis:** a direction you can move along. A list of numbers has 1 axis; a table has 2 (rows and columns); a colour image has 3 (height, width, colour channel). *(Section [8](#8-shape-dimensions-and-dtypes))*
- **Direct labelling:** writing labels next to lines or bars instead of in a legend. *(Section [50](#50-choosing-the-right-chart-and-not-misleading))*
- **Discrete:** countable whole numbers (number of children, items in a basket). *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **Discrete vs continuous:** countable values (0, 1, 2 clicks) vs any value in a range (a delivery time of 2.37 days). *(Section [54](#54-probability-distributions-normal-binomial-poisson-and-more))*
- **Dispersion (spread):** how far values are from the middle. *(Section [51](#51-describing-data-centre-spread-and-shape))*
- **Distribution:** how the values of one variable are spread out: where most of them are, how wide the spread is, whether there's a long tail. *(Section [43](#43-your-first-charts-with-matplotlib))*
- **Diverging colormap:** two colours meeting at a neutral middle, for values above and below a centre like 0 (`RdBu`, `coolwarm`). *(Section [45](#45-styling-annotation-and-saving-charts))*
- **Dot product (`a @ b` for vectors):** `a₁b₁ + a₂b₂ + … + aₙbₙ`. A single number measuring how much two vectors point the same way. *(Section [16](#16-linear-algebra-basics-dot-products-matrix-multiplication-and-solving-equations))*
- **Downcast:** convert to a smaller numeric type (`int64` → `int16`, `float64` → `float32`) when values fit. *(Section [40](#40-memory-dtypes-categoricals-chunking-and-apache-arrow))*
- **Downcasting:** converting to a smaller type (`int64` → `int32`) to save memory. *(Section [27](#27-duplicates-data-types-and-type-conversion))*
- **DPI (dots per inch):** image resolution when saving. 100 for screens, 150–300 for print and slides. *(Section [43](#43-your-first-charts-with-matplotlib))*
- **`.dt` accessor:** date parts of a datetime column: `.dt.year`, `.dt.month`, `.dt.day_name()`. *(Section [24](#24-adding-and-changing-columns-arithmetic-assign-map-apply-and-npselect))*
- **dtype (data type):** the element type: `int64` (whole numbers using 64 bits = 8 bytes), `float64`, `float32`, `bool`, `uint8` (unsigned 8-bit: 0–255) and so on. *(Section [8](#8-shape-dimensions-and-dtypes))*
- **dtype per column:** each column has its own type. pandas 3's main types: `int64`, `float64`, `bool`, `str` (text), `datetime64` (dates and times), `category` (repeated labels, Section [29](#29-categorical-data-and-binning-cut-and-qcut)). *(Section [18](#18-dataframes-creating-inspecting-and-understanding-a-table))*
- **DuckDB:** an **in-process** analytical database (often called "SQLite for analytics"). *(Section [42](#42-duckdb-sql-on-dataframes-and-files))*
- **Dummy (indicator) variable:** a 0/1 column for a category (is_weekend). With k categories, use k − 1 dummies; the left-out one is the **reference** that others are compared with. *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*
- **Duplicate row:** a row identical to another, in all columns or in the columns that should be unique. *(Section [27](#27-duplicates-data-types-and-type-conversion))*

### E

- **Eager vs lazy:** **eager** runs each step immediately (like pandas). **Lazy** builds a **query plan** and runs it only when you call `.collect()`. *(Section [41](#41-polars-fast-dataframes-with-lazy-queries))*
- **ECDF (empirical cumulative distribution function):** for each value x, the fraction of data ≤ x. Reads off percentiles directly; needs no binning. *(Section [46](#46-seaborn-i-distributions))*
- **EDA (exploratory data analysis):** open-ended investigation of a dataset to understand it, find problems and form hypotheses. *(Section [60](#60-a-complete-exploratory-data-analysis-eda))*
- **Effect size:** how big the difference is, in units (₹42) or standardised (**Cohen's d** = difference ÷ pooled std; 0.2 small, 0.5 medium, 0.8 large). *(Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests))*
- **Eigenvector / eigenvalue:** a direction that a matrix only stretches (doesn't rotate), and the stretch factor. Used by PCA (`machine-learning.md`). *(Section [16](#16-linear-algebra-basics-dot-products-matrix-multiplication-and-solving-equations))*
- **Element:** one value inside an array. *(Section [6](#6-why-numpy-arrays-vs-lists-and-how-arrays-sit-in-memory))*
- **Element-wise:** applied to each element (or each matching pair of elements) separately. *(Section [11](#11-vectorised-maths-and-universal-functions))*
- **Element-wise logical operators:** `&` (and), `|` (or), `~` (not), applied to each pair of booleans. *(Section [10](#10-boolean-masks-fancy-indexing-and-npwhere))*
- **Embedding:** a list of numbers (a vector) that represents the meaning of a word, sentence, image or product, so that similar things get similar vectors. *(Section [16](#16-linear-algebra-basics-dot-products-matrix-multiplication-and-solving-equations))*
- **Encoding:** how characters are stored as bytes. **UTF-8** handles every language and is the standard; old Excel files may use `cp1252` or `latin-1`. *(Section [5](#5-reading-files-with-plain-python-text-csv-and-json), [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Endpoint:** one URL of an API, like `https://api.example.com/orders`. *(Section [20](#20-reading-from-databases-and-web-apis))*
- **Escape:** a backslash makes a special character literal: `\.` means a real dot (a bare `.` means "any character"). *(Section [28](#28-text-data-the-str-accessor-and-regular-expressions))*
- **Estimator:** the summary a categorical chart draws (`barplot` and `pointplot` use the **mean** by default). *(Section [47](#47-seaborn-ii-relationships-categories-and-facets), [55](#55-sampling-the-central-limit-theorem-and-standard-error))*
- **ETL / ELT:** **E**xtract, **T**ransform, **L**oad (transform before storing) vs **E**xtract, **L**oad, **T**ransform (store raw data first, transform inside the warehouse with SQL; the modern default). *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Evenly spaced:** neighbouring values are the same distance apart. *(Section [7](#7-creating-arrays-array-arange-linspace-zeros-ones-and-full))*
- **Event:** a set of outcomes we care about ("the roll is even"). *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **Excel file (`.xlsx`):** a spreadsheet file; can have several **sheets** (tabs). pandas reads it with the `openpyxl` library. *(Section [19](#19-reading-and-writing-files-csv-excel-json-and-parquet))*
- **Executive summary (TL;DR):** the 2–4 sentences someone reads if they read nothing else. *(Section [63](#63-communicating-results-reports-dashboards-and-data-storytelling))*
- **Expanding window:** from the start up to each point (running total, running max). *(Section [38](#38-time-series-resample-rolling-shift-and-window-functions))*
- **Expected value:** the long-run average outcome: Σ value × probability. *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **Expected value (mean) and variance of a distribution:** its long-run average and spread. *(Section [54](#54-probability-distributions-normal-binomial-poisson-and-more))*
- **Experiment / trial:** something with an uncertain outcome (rolling a die, a visitor arriving). *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **Explode:** give each item of a list-valued cell its own row. *(Section [35](#35-reshaping-pivot_table-melt-crosstab-and-explode))*
- **Exponential `exp(x)`:** e (≈ 2.718) raised to the power x. Grows extremely fast; used in growth models, softmax and probabilities. *(Section [11](#11-vectorised-maths-and-universal-functions))*
- **Exponentially weighted (EWM):** a moving average where recent values count more, fading smoothly into the past. *(Section [38](#38-time-series-resample-rolling-shift-and-window-functions))*
- **Expression:** a description of a column calculation, like `pl.col("qty") * pl.col("price")`. Expressions are combined and run by Polars' engine, not by Python. *(Section [41](#41-polars-fast-dataframes-with-lazy-queries))*

### F

- **f-string:** a string with `f` in front that fills in values: `f"{name} spent {total:.2f}"` (`:.2f` = 2 decimal places). *(Section [3](#3-python-refresher-for-data-work-lists-dicts-comprehensions-and-functions))*
- **Facet grid:** a grid of small charts, one per value of a column (`col="channel"`). *(Section [47](#47-seaborn-ii-relationships-categories-and-facets))*
- **Fancy indexing:** indexing with a list (or array) of positions: `a[[0, 3, 5]]`. *(Section [10](#10-boolean-masks-fancy-indexing-and-npwhere))*
- **Feather / Arrow IPC:** another fast binary format, good for passing data between programs; Parquet is better for storage. *(Section [19](#19-reading-and-writing-files-csv-excel-json-and-parquet))*
- **Feature (predictor, input, X):** a column the model uses. **Target (label, y):** what it predicts. *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Feature store:** a system that computes, stores and serves features consistently for training and live predictions. *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Figure (`fig`):** the whole image or window; it can hold several charts. *(Section [43](#43-your-first-charts-with-matplotlib))*
- **File path:** where a file lives, like `data/orders.csv` (relative to the current folder) or `/Users/asha/data/orders.csv` (absolute). *(Section [5](#5-reading-files-with-plain-python-text-csv-and-json))*
- **`filter` (on groups):** keep the rows of groups that pass a test (like SQL `HAVING`, but you get the original rows back). *(Section [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking))*
- **Filter / predicate:** a rule each row either passes or fails. *(Section [22](#22-filtering-rows-conditions-isin-between-and-query))*
- **Fit / transform:** **fit** = learn numbers from data (a median, a mean, a category list); **transform** = apply them. Fit on training rows only; transform both. *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Flatten:** turn a MultiIndex into ordinary columns (`reset_index()`), or join multi-level column names into one string. *(Section [36](#36-multiindex-stack-and-unstack))*
- **Flatten / ravel:** turn any array into 1D. *(Section [14](#14-reshaping-stacking-splitting-and-sorting))*
- **Floating-point (float):** a number with a fractional part, stored approximately in binary. `0.1 + 0.2` is `0.30000000000000004`, because 0.1 can't be stored exactly. *(Section [7](#7-creating-arrays-array-arange-linspace-zeros-ones-and-full))*
- **Footprint:** how much memory an object uses. `df.memory_usage(deep=True)` measures it. *(Section [40](#40-memory-dtypes-categoricals-chunking-and-apache-arrow))*
- **Formula interface:** writing a model as text: `"sales ~ price + ads + C(city)"` (`C()` marks a categorical column). *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*
- **Forward fill (`ffill`):** fill a gap with the last known value above it. **Backward fill (`bfill`):** with the next value below. *(Section [26](#26-missing-values-finding-dropping-and-filling))*
- **Free-threaded Python:** Python builds without the **GIL** (global interpreter lock, which lets only one thread run Python code at a time), so threads can use several CPU cores. *(Section [64](#64-whats-new-modern-data-tooling-20232026))*
- **Frequency / offset alias:** a code for a time step: `"D"` day, `"h"` hour, `"min"` minute, `"W"` week, `"MS"` month start, `"ME"` month end, `"QE"` quarter end, `"YE"` year end, `"B"` business day. *(Section [37](#37-dates-and-times-parsing-dt-time-zones-and-periods))*
- **Frequency encoding:** each category replaced by how common it is. *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Function:** a named, reusable block of code that takes **arguments** (inputs) and **returns** a result. *(Section [3](#3-python-refresher-for-data-work-lists-dicts-comprehensions-and-functions))*
- **Funnel:** the sequence of steps users go through (view → cart → purchase); **funnel analysis** measures how many make it from each step to the next. *(Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine))*

### G

- **Gaps and islands:** the classic problem of finding runs of consecutive values (consecutive login days) separated by gaps. *(Section [66](#66-interview-problems-pandas-numpy-and-sql-style-questions))*
- **Generator:** NumPy's random-number object, created by `np.random.default_rng(seed)`. *(Section [15](#15-random-numbers-and-simulation))*
- **Git:** the standard version-control tool: it records every change to your files so you can review, share and undo them. *(Section [2](#2-setting-up-python-virtual-environments-uv-and-jupyter-notebooks))*
- **Google Colab:** Google's free browser-based notebook service with the data libraries pre-installed. *(Section [2](#2-setting-up-python-virtual-environments-uv-and-jupyter-notebooks))*
- **Grid layout:** `plt.subplots(nrows, ncols)` returns a figure and an **array** of axes. *(Section [44](#44-matplotlib-anatomy-figures-axes-and-subplots))*
- **Group:** all rows sharing one key value (all Pune orders). *(Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine))*
- **Grouping key:** the column(s) whose values define the groups (`city`). *(Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine))*
- **Guardrail metrics:** metrics that must **not** get worse (page load time, refunds, unsubscribes). *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*

### H

- **Hadoop:** an older open-source system for storing and processing big data across many computers; Parquet was created in its ecosystem. *(Section [19](#19-reading-and-writing-files-csv-excel-json-and-parquet))*
- **Hash lookup:** checking membership in a set or dict in roughly constant time, O(1), however big it is. *(Section [39](#39-performance-vectorise-avoid-loops-and-measure))*
- **Heatmap:** a grid where each cell's colour shows its value. *(Section [48](#48-heatmaps-pair-plots-and-correlation-charts))*
- **Hexbin / 2D histogram:** counts in a grid of cells, for scatters with too many points. *(Section [48](#48-heatmaps-pair-plots-and-correlation-charts))*
- **HTML export:** saving a chart as a web page that works offline (`fig.write_html`). *(Section [49](#49-interactive-charts-with-plotly))*
- **HTTP request:** asking a web server for something (`GET` to read, `POST` to send). The `requests` or `httpx` library makes them from Python. *(Section [20](#20-reading-from-databases-and-web-apis))*
- **`hue`:** a column whose values set the colour, splitting one chart into groups. *(Section [46](#46-seaborn-i-distributions))*
- **Hypothesis (in EDA):** a pattern you've noticed and want to test properly later. *(Section [60](#60-a-complete-exploratory-data-analysis-eda))*

### I

- **IDE (integrated development environment):** an editor with built-in running and debugging, such as **VS Code**, which also opens notebooks. *(Section [2](#2-setting-up-python-virtual-environments-uv-and-jupyter-notebooks))*
- **Idempotent:** running a step twice gives the same result as running it once (re-running yesterday's job doesn't duplicate yesterday's rows). *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Identifier (ID):** a code that names something (order ID, phone number, postcode). Looks numeric, but **isn't a quantity**: averaging order IDs is meaningless. *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **Identity matrix:** a square grid with 1s on the diagonal (top-left to bottom-right) and 0s elsewhere. Multiplying by it changes nothing, like multiplying a number by 1. *(Section [7](#7-creating-arrays-array-arange-linspace-zeros-ones-and-full))*
- **`ignore_index=True`:** renumber rows 0, 1, 2… after stacking (otherwise index labels repeat). *(Section [34](#34-combining-tables-ii-concat-validation-and-merge-pitfalls))*
- **`.iloc` (integer-location-based):** select by position numbers. Slices **exclude** the end, like Python. *(Section [21](#21-selecting-data-columns--loc-and-iloc))*
- **Immutable style:** never changing an object in place; always creating a new one. Easier to reason about and to test. *(Section [25](#25-method-chaining-and-copy-on-write-pandas-3))*
- **Import:** loading a library into your program with `import name`. *(Section [2](#2-setting-up-python-virtual-environments-uv-and-jupyter-notebooks))*
- **Impute / imputation:** filling missing values with estimates. *(Section [26](#26-missing-values-finding-dropping-and-filling))*
- **In-process / embedded:** the database runs as a library inside your program, not as a separate server you connect to over a network. *(Section [42](#42-duckdb-sql-on-dataframes-and-files))*
- **Independent:** knowing A tells you nothing about B: P(A and B) = P(A) × P(B). *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **Independent variables (predictors, features, x):** what you explain it with (price, ad spend). *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*
- **Index:** a position number, starting at 0. Negative indices count from the end: `-1` is the last element. *(Section [9](#9-indexing-and-slicing-1d-and-2d-views-vs-copies), [17](#17-pandas-series-labelled-1d-data))*
- **`index` / `columns` / `values`:** in `pivot_table`: what becomes rows, what becomes columns, and which numbers fill the cells. *(Section [35](#35-reshaping-pivot_table-melt-crosstab-and-explode))*
- **Indicator:** a column (`_merge`) saying where each row came from: `left_only`, `right_only` or `both`. *(Section [33](#33-combining-tables-i-merge-and-join-types))*
- **Inner join:** keep only rows whose key appears in **both** tables. *(Section [33](#33-combining-tables-i-merge-and-join-types))*
- **`inplace=True`:** an old option that modifies the object instead of returning a new one. Discouraged; it doesn't even save memory in most cases. *(Section [25](#25-method-chaining-and-copy-on-write-pandas-3))*
- **Interaction:** the effect of x₁ depends on x₂ (ads work better on weekends): modelled with x₁ × x₂. *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*
- **Interaction feature:** a combination of two features (price × quantity, ratio of two counts). *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Interactive chart:** a chart that responds to the mouse: hover tooltips, zoom, pan, toggling series. *(Section [49](#49-interactive-charts-with-plotly))*
- **Intercept:** the predicted y when every x is 0 (often not meaningful on its own). *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*
- **Interpolation:** estimating a gap from the values on both sides (a straight line between them, for example). *(Section [26](#26-missing-values-finding-dropping-and-filling))*
- **Intersection / joint probability (A and B):** both happen. *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **Interval estimate / confidence interval (CI):** a range of plausible values (₹770 to ₹854). *(Section [56](#56-confidence-intervals-and-the-bootstrap))*
- **Inverse (A⁻¹):** the matrix that "undoes" `A`: `A⁻¹ @ A` is the identity matrix. Not every matrix has one. *(Section [16](#16-linear-algebra-basics-dot-products-matrix-multiplication-and-solving-equations))*
- **IQR (interquartile range):** Q3 − Q1, the width of the middle 50% of the data. *(Section [30](#30-outliers-and-data-validation), [51](#51-describing-data-centre-spread-and-shape))*
- **IQR rule (Tukey's fences):** flag values below Q1 − 1.5 × IQR or above Q3 + 1.5 × IQR. This is what a box plot's whiskers show (Section [46](#46-seaborn-i-distributions)). *(Section [30](#30-outliers-and-data-validation))*
- **`isin`:** "is the value one of these?" (SQL `IN`). *(Section [22](#22-filtering-rows-conditions-isin-between-and-query))*
- **ISO 8601:** the international date format `2025-03-14T09:30:00+05:30`. Unambiguous; use it for storing and exchanging dates. *(Section [37](#37-dates-and-times-parsing-dt-time-zones-and-periods))*

### J

- **JIT (just-in-time) compiler:** a tool like **Numba** that compiles a Python function to machine code the first time it runs. *(Section [39](#39-performance-vectorise-avoid-loops-and-measure))*
- **Joint plot:** one scatter with the two distributions in the margins. *(Section [48](#48-heatmaps-pair-plots-and-correlation-charts))*
- **JSON (JavaScript Object Notation):** text with `{"key": value}` objects and `[...]` arrays, the standard format of web APIs. It maps directly onto Python dicts and lists. *(Section [5](#5-reading-files-with-plain-python-text-csv-and-json))*
- **Jupyter / JupyterLab:** the free program that opens notebooks in your browser. *(Section [2](#2-setting-up-python-virtual-environments-uv-and-jupyter-notebooks))*

### K

- **Kafka / Flink:** popular streaming tools: Apache Kafka carries streams of events between systems; Apache Flink processes those streams continuously. *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Kaggle / LeetCode / Deep-ML:** free practice websites: Kaggle for datasets, competitions and short courses; LeetCode for coding problems (including pandas and SQL tracks); Deep-ML for maths, statistics and ML coding problems. *(Section [1](#1-how-to-use-these-notes-and-what-data-scientists-do))*
- **KDE (kernel density estimate):** a smooth curve estimating the shape of a distribution, made by placing a small bump on every data point and adding the bumps up. *(Section [46](#46-seaborn-i-distributions))*
- **`keep`:** which copy `drop_duplicates` keeps: `"first"`, `"last"`, or `False` (drop all copies). *(Section [27](#27-duplicates-data-types-and-type-conversion))*
- **Kernel:** the running Python process behind a notebook. Every cell you run sends its code to the kernel, and the kernel **remembers** every variable until you restart it. *(Section [2](#2-setting-up-python-virtual-environments-uv-and-jupyter-notebooks))*
- **Key (join key):** the column(s) used to match rows: `customer_id`. *(Section [33](#33-combining-tables-i-merge-and-join-types))*
- **Key / unique identifier:** the column(s) that should identify each row exactly once (`order_id`). A duplicate key is a red flag even if other columns differ. *(Section [27](#27-duplicates-data-types-and-type-conversion))*
- **`keys=`:** label which source each stacked piece came from. *(Section [34](#34-combining-tables-ii-concat-validation-and-merge-pitfalls))*
- **KPI (key performance indicator):** a metric that tracks a goal (weekly active users, conversion rate, revenue per user). *(Section [63](#63-communicating-results-reports-dashboards-and-data-storytelling))*
- **Kurtosis:** how heavy the tails are: how often extreme values appear compared with a bell curve. *(Section [51](#51-describing-data-centre-spread-and-shape))*

### L

- **Label:** one entry of the index, like `"Pune"` or a date. *(Section [17](#17-pandas-series-labelled-1d-data))*
- **Lakh / crore:** Indian number words: 1 lakh = 100,000; 1 crore = 10,000,000 (100 lakh). *(Section [49](#49-interactive-charts-with-plotly))*
- **Lambda:** a tiny function without a name, written in one expression: `lambda x: x * 2`. *(Section [3](#3-python-refresher-for-data-work-lists-dicts-comprehensions-and-functions), [24](#24-adding-and-changing-columns-arithmetic-assign-map-apply-and-npselect))*
- **Latency:** how long something takes to respond (a web request, a database query). *(Section [12](#12-aggregations-and-the-axis-argument))*
- **Law of large numbers:** the more trials you run, the closer the observed fraction gets to the true probability. *(Section [15](#15-random-numbers-and-simulation), [55](#55-sampling-the-central-limit-theorem-and-standard-error))*
- **Law of total probability:** P(B) = P(B | A) P(A) + P(B | not A) P(not A): add up the ways B can happen. *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **Left join:** keep **every** row of the left table; fill missing partners with NaN. *(Section [33](#33-combining-tables-i-merge-and-join-types))*
- **Left table / right table:** the first and second table in `pd.merge(left, right)`. *(Section [33](#33-combining-tables-i-merge-and-join-types))*
- **Legend:** the key explaining which colour or marker is which series. *(Section [43](#43-your-first-charts-with-matplotlib))*
- **Level:** one layer of a MultiIndex, referred to by position (0, 1) or name (`"city"`). *(Section [36](#36-multiindex-stack-and-unstack))*
- **Library (or package):** code someone else wrote that you install and reuse. NumPy, pandas and Matplotlib are libraries. *(Section [1](#1-how-to-use-these-notes-and-what-data-scientists-do))*
- **Lineage:** which upstream tables and steps each output depends on. *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Linear equation system:** several equations like `2x + y = 5`, `x + 3y = 10`, solved together. *(Section [16](#16-linear-algebra-basics-dot-products-matrix-multiplication-and-solving-equations))*
- **List:** an ordered, changeable collection: `[3, 1, 4]`. Get items by **position** (index), starting from 0. *(Section [3](#3-python-refresher-for-data-work-lists-dicts-comprehensions-and-functions))*
- **LLM (large language model):** an AI model trained on huge amounts of text that can read and write language (Claude, GPT, Gemini); `llm-engineering.md` covers them. *(Section [1](#1-how-to-use-these-notes-and-what-data-scientists-do))*
- **`.loc` (label-based):** select by row labels and column names. Slices **include** the end label. *(Section [21](#21-selecting-data-columns--loc-and-iloc))*
- **Locale formats:** country-specific ways of writing numbers and dates (`1.200,50` in Germany; `03/04/2025` is 3 April in India, March 4 in the USA). *(Section [27](#27-duplicates-data-types-and-type-conversion))*
- **Log scale:** an axis where equal steps mean equal **multiples** (1, 10, 100, 1000), for data spanning many orders of magnitude. *(Section [44](#44-matplotlib-anatomy-figures-axes-and-subplots))*
- **Log transform:** taking `log` of a skewed positive column so huge values are pulled closer to the rest. *(Section [30](#30-outliers-and-data-validation))*
- **Logarithm `log(x)`:** the inverse of `exp`: the power you'd raise e to, to get x. `np.log` is the **natural** log (base e); `np.log10` is base 10; `np.log1p(x)` computes `log(1 + x)` accurately for small x. *(Section [11](#11-vectorised-maths-and-universal-functions))*
- **Logistic regression:** the version for yes/no outcomes; coefficients are in **log-odds** (exponentiate them to get **odds ratios**). *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*
- **Long (tidy) data:** Seaborn's preferred input (Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data)): one row per observation. *(Section [47](#47-seaborn-ii-relationships-categories-and-facets))*
- **Long (tidy) format:** one row per observation (Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data)). *(Section [35](#35-reshaping-pivot_table-melt-crosstab-and-explode))*
- **Loop:** code that repeats for each item (`for x in items:`) or while a condition holds (`while ...:`). *(Section [3](#3-python-refresher-for-data-work-lists-dicts-comprehensions-and-functions))*

### M

- **Machine learning (ML):** letting a program learn a rule from examples instead of writing the rule by hand (the `machine-learning.md` notes). *(Section [1](#1-how-to-use-these-notes-and-what-data-scientists-do))*
- **`map`:** replaces each value of a Series using a dict (or function): a lookup table. *(Section [24](#24-adding-and-changing-columns-arithmetic-assign-map-apply-and-npselect))*
- **Mapping / encoding:** linking a column to a visual property (position, colour, size, shape). *(Section [47](#47-seaborn-ii-relationships-categories-and-facets))*
- **MAR (missing at random):** missingness depends on **other columns you have** (older customers skip the "app rating" question more). Fill using those columns. *(Section [26](#26-missing-values-finding-dropping-and-filling))*
- **Margin of error:** half the width of the interval (± ₹42). *(Section [56](#56-confidence-intervals-and-the-bootstrap))*
- **Margins:** total rows and columns (`margins=True` adds "All"). *(Section [35](#35-reshaping-pivot_table-melt-crosstab-and-explode))*
- **Mask:** the Series of True/False the rule produces, one per row. *(Section [22](#22-filtering-rows-conditions-isin-between-and-query), [48](#48-heatmaps-pair-plots-and-correlation-charts))*
- **Mask (boolean mask):** an array of booleans with the same shape as the data, used to pick elements. *(Section [10](#10-boolean-masks-fancy-indexing-and-npwhere))*
- **Matplotlib:** the foundational Python plotting library. `matplotlib.pyplot`, imported as `plt`, is its main interface. *(Section [43](#43-your-first-charts-with-matplotlib))*
- **Matrix:** a rectangular grid of numbers with `m` rows and `n` columns, shape `(m, n)`. *(Section [16](#16-linear-algebra-basics-dot-products-matrix-multiplication-and-solving-equations))*
- **Matrix multiplication (`A @ B`):** entry `(i, j)` of the result is row `i` of `A` dotted with column `j` of `B`. Needs `A`'s column count to equal `B`'s row count. *(Section [16](#16-linear-algebra-basics-dot-products-matrix-multiplication-and-solving-equations))*
- **MCAR (missing completely at random):** pure bad luck, unrelated to anything (a sensor glitch). Dropping rows is safe, just wasteful. *(Section [26](#26-missing-values-finding-dropping-and-filling))*
- **MDE (minimum detectable effect):** the smallest change worth detecting (+0.5 percentage points). *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **Mean:** the average: add everything up and divide by how many there are. *(Section [12](#12-aggregations-and-the-axis-argument))*
- **Mean (average, x̄):** add everything, divide by the count. *(Section [51](#51-describing-data-centre-spread-and-shape))*
- **Median:** the middle value after sorting (half are below, half above). Section [51](#51-describing-data-centre-spread-and-shape) explains when it beats the mean. *(Section [12](#12-aggregations-and-the-axis-argument), [51](#51-describing-data-centre-spread-and-shape))*
- **Melt (unpivot):** turn column headers back into values in a column. *(Section [35](#35-reshaping-pivot_table-melt-crosstab-and-explode))*
- **Memory:** where a running program keeps its data (RAM). A **contiguous block** means the values are stored one after another with no gaps. *(Section [6](#6-why-numpy-arrays-vs-lists-and-how-arrays-sit-in-memory))*
- **Merge / join:** combining two tables side by side by matching key values. *(Section [33](#33-combining-tables-i-merge-and-join-types))*
- **Method:** a function attached to an object, called with a dot: `s.mean()`. *(Section [17](#17-pandas-series-labelled-1d-data))*
- **Method chaining:** calling methods one after another on each result: `df.dropna().sort_values("x").head()`. *(Section [25](#25-method-chaining-and-copy-on-write-pandas-3))*
- **Metric definition:** the exact formula, filters and time window (e.g. "active = at least one session in the last 7 days, excluding staff accounts"). *(Section [63](#63-communicating-results-reports-dashboards-and-data-storytelling))*
- **Missing indicator:** an extra True/False column recording that a value **was** missing, so the information isn't lost after filling. *(Section [26](#26-missing-values-finding-dropping-and-filling))*
- **Missing value:** a cell with no data. pandas shows it as `NaN` (Not a Number, for numbers and text), `NaT` (Not a Time, for dates) or `<NA>` (for the newer "nullable" types). *(Section [26](#26-missing-values-finding-dropping-and-filling))*
- **MNAR (missing not at random):** missingness depends on the **missing value itself** (people with high incomes hide their income). Dangerous: no simple fix; flag it and say so. *(Section [26](#26-missing-values-finding-dropping-and-filling))*
- **Mode:** the most frequent value. *(Section [51](#51-describing-data-centre-spread-and-shape))*
- **Model:** a simplified mathematical description of how something works, fitted to data: a straight line through points, or a trained ML program that maps inputs to predictions. *(Section [1](#1-how-to-use-these-notes-and-what-data-scientists-do))*
- **Mosaic:** a layout described by a picture-like string, e.g. `"AAB;CCB"`. *(Section [44](#44-matplotlib-anatomy-figures-axes-and-subplots))*
- **Multi-key grouping:** grouping by several columns at once (`["city", "category"]`): one group per combination that exists. *(Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine))*
- **Multicollinearity:** predictors so correlated with each other that their separate effects can't be pinned down (huge SEs). Checked with the **VIF** (variance inflation factor). *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*
- **MultiIndex (hierarchical index):** an index with several **levels**, like (city, category). *(Section [36](#36-multiindex-stack-and-unstack))*
- **Multiple comparisons:** running many tests; some will be "significant" by chance (about 1 in 20 at α = 0.05) unless you correct (**Bonferroni**: use α / number of tests; or control the **false discovery rate** with Benjamini–Hochberg). *(Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests))*
- **Mutually exclusive:** A and B can't both happen (P(A and B) = 0). *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*

### N

- **`NA` markers:** strings that mean "missing", like `""`, `"NA"`, `"n/a"`, `"-"`. *(Section [19](#19-reading-and-writing-files-csv-excel-json-and-parquet))*
- **Naive vs aware:** a **naive** timestamp has no time zone (ambiguous); an **aware** one knows its zone. *(Section [37](#37-dates-and-times-parsing-dt-time-zones-and-periods))*
- **Named aggregation:** `agg(new_name=("column", "function"))`: choose the output column names yourself. *(Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine))*
- **NaN (Not a Number):** a special float meaning "missing" or "undefined" (like 0/0). **inf:** infinity (like 1/0). *(Section [11](#11-vectorised-maths-and-universal-functions))*
- **`NaN` / missing value:** pandas' marker for "no value here". (`NA`/`<NA>` is a newer missing marker used by some types; Section [26](#26-missing-values-finding-dropping-and-filling) covers both.) *(Section [17](#17-pandas-series-labelled-1d-data))*
- **Nested JSON:** JSON with objects inside objects (`{"customer": {"name": ..., "city": ...}}`). **Flattening** turns nested fields into columns like `customer.name`. *(Section [20](#20-reading-from-databases-and-web-apis))*
- **Network effects / interference:** one user's treatment affects another's (marketplaces, social apps), breaking the "independent groups" assumption. *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **Neural network:** a model built from layers of simple units, each computing weighted sums (matrix multiplications) followed by an activation function (`deep-learning.md`). *(Section [16](#16-linear-algebra-basics-dot-products-matrix-multiplication-and-solving-equations))*
- **Nominal:** groups with **no order** (city, colour, payment method). *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **Non-null count:** how many values in a column are not missing. *(Section [18](#18-dataframes-creating-inspecting-and-understanding-a-table))*
- **`None`:** Python's "nothing" value; pandas converts it to a missing marker inside columns. *(Section [26](#26-missing-values-finding-dropping-and-filling))*
- **`None` / `np.newaxis` in an index:** inserts a new axis of size 1: `a[:, None]` turns shape `(3,)` into `(3, 1)`. *(Section [13](#13-broadcasting-maths-between-arrays-of-different-shapes))*
- **Norm (length, magnitude):** a vector's length, √(a₁² + a₂² + …). `np.linalg.norm(a)`. *(Section [16](#16-linear-algebra-basics-dot-products-matrix-multiplication-and-solving-equations))*
- **Normal (Gaussian) distribution:** the bell curve: values cluster around a mean and get rarer further away (heights, measurement errors). Defined by its **mean** (centre) and **standard deviation** (width). *(Section [15](#15-random-numbers-and-simulation))*
- **Normalise text:** make variants identical (same case, no stray spaces, one spelling). *(Section [28](#28-text-data-the-str-accessor-and-regular-expressions))*
- **North-star metric:** the single metric that best captures the value a product delivers. *(Section [63](#63-communicating-results-reports-dashboards-and-data-storytelling))*
- **Notebook (`.ipynb` file):** a document made of **cells**. A **code cell** holds Python; a **Markdown cell** holds notes. Each code cell's result is shown right under it and saved in the file. *(Section [2](#2-setting-up-python-virtual-environments-uv-and-jupyter-notebooks))*
- **Novelty effect:** users react to anything new at first, then settle down. **Primacy effect:** users resist change at first. *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **`np.where` / `np.select`:** vectorised if/else for columns (Section [10](#10-boolean-masks-fancy-indexing-and-npwhere)). *(Section [24](#24-adding-and-changing-columns-arithmetic-assign-map-apply-and-npselect))*
- **`np.where(condition, x, y)`:** builds a new array taking `x` where the condition is true and `y` where it's false. *(Section [10](#10-boolean-masks-fancy-indexing-and-npwhere))*
- **Null distribution:** the distribution the test statistic would have if H₀ were true. *(Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests))*
- **Null hypothesis (H₀):** the "nothing is going on" claim: no difference between groups, no relationship. *(Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests))*
- **Nullable dtypes:** types like `Int64` (capital I), `boolean` and `Float64` that can hold `<NA>` without changing type. A normal `int64` column can't hold NaN, so one missing value turns it into `float64`. *(Section [26](#26-missing-values-finding-dropping-and-filling))*
- **Numba:** a library that compiles Python functions with loops into fast machine code (Section [39](#39-performance-vectorise-avoid-loops-and-measure)). *(Section [11](#11-vectorised-maths-and-universal-functions))*
- **Numerical (quantitative) data:** numbers where maths makes sense. *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **NumPy (Numerical Python):** the library for fast arrays of numbers. Imported as `np`. *(Section [6](#6-why-numpy-arrays-vs-lists-and-how-arrays-sit-in-memory))*
- **`nunique`:** the number of distinct values per group. *(Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine))*

### O

- **Observability (data):** monitoring pipelines and tables over time: row counts, null rates, freshness, distribution shifts. *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Observation (row, record, sample):** one thing you measured: one order, one patient, one day. *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **OLAP vs OLTP:** **analytical** workloads (scan millions of rows, aggregate: "revenue per month") vs **transactional** ones (many small reads and writes: "update this order"). DuckDB is OLAP; PostgreSQL is mainly OLTP (`sql-postgresql.md`). *(Section [42](#42-duckdb-sql-on-dataframes-and-files))*
- **OLS (ordinary least squares):** the standard method: choose coefficients that minimise the **sum of squared residuals**. *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*
- **`:` on its own:** "everything along this axis". *(Section [9](#9-indexing-and-slicing-1d-and-2d-views-vs-copies))*
- **One-hot encoding:** one 0/1 column per category. *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Operator precedence:** the order Python evaluates operators. `&` binds **tighter** than `>`, so each comparison needs its own brackets. *(Section [10](#10-boolean-masks-fancy-indexing-and-npwhere))*
- **Orchestrator:** software that schedules pipeline steps, runs them in the right order, retries failures and alerts people: **Airflow**, **Dagster**, **Prefect**. *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **Ordered categorical:** categories with a meaningful order, so sorting and comparisons (`size > "M"`) work. *(Section [29](#29-categorical-data-and-binning-cut-and-qcut))*
- **Ordinal:** groups **with an order** but no meaningful distance (S < M < L; "poor < fair < good"). The gap from S to M isn't "the same" as M to L. *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **Ordinal encoding:** ordered integers for ordered categories. *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Outcome:** one possible result. **Sample space:** all possible outcomes. *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **Outer (full) join:** keep every row from **both** tables. *(Section [33](#33-combining-tables-i-merge-and-join-types))*
- **Outer / inner level:** the first / later levels. Rows are grouped by the outer level. *(Section [36](#36-multiindex-stack-and-unstack))*
- **Outer operation:** combining **every** element of one array with **every** element of another, giving a grid. *(Section [13](#13-broadcasting-maths-between-arrays-of-different-shapes))*
- **Outlier:** an observation far from most others. *(Section [30](#30-outliers-and-data-validation))*
- **Overflow:** when a result is too big for its type and wraps around to a wrong value (an `int8` can hold only −128 to 127). *(Section [8](#8-shape-dimensions-and-dtypes))*
- **Overhead:** extra work that isn't the actual calculation, like Python checking the type of every number in a loop. *(Section [6](#6-why-numpy-arrays-vs-lists-and-how-arrays-sit-in-memory))*
- **Overplotting:** so many points that they hide each other; fix with transparency (`alpha`), smaller points, or a 2D histogram. *(Section [47](#47-seaborn-ii-relationships-categories-and-facets))*

### P

- **P(A):** the probability of event A. *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **p-value:** the probability, **assuming H₀ is true**, of getting a result at least as extreme as the one observed. *(Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests))*
- **p50 / p95 / p99:** the 50th, 95th and 99th percentiles, usually of latency: "p99 = 800 ms" means 99% of requests finish within 800 ms. *(Section [12](#12-aggregations-and-the-axis-argument))*
- **Package manager:** a tool that downloads and installs libraries for you (`pip`, `uv`, `conda`). *(Section [2](#2-setting-up-python-virtual-environments-uv-and-jupyter-notebooks))*
- **Pagination:** an API returning results in pages; you keep asking for the next page until there are none. *(Section [20](#20-reading-from-databases-and-web-apis))*
- **Pair plot (scatter-plot matrix):** a grid with a scatter plot for every pair of variables and each variable's distribution on the diagonal. *(Section [48](#48-heatmaps-pair-plots-and-correlation-charts))*
- **pandas:** the library for labelled tables in Python (the name comes from "panel data"). Imported as `pd`. *(Section [17](#17-pandas-series-labelled-1d-data))*
- **pandera:** a Python library for declaring DataFrame schemas and validating them. *(Section [30](#30-outliers-and-data-validation))*
- **Parallelism / multi-threading:** using several CPU cores at once. *(Section [41](#41-polars-fast-dataframes-with-lazy-queries))*
- **Parameter vs statistic:** a fixed (usually unknown) number describing the population, like the true mean μ, vs a number computed from the sample, like the sample mean x̄, used to **estimate** it. *(Section [55](#55-sampling-the-central-limit-theorem-and-standard-error))*
- **Parameterised query:** a query with placeholders (`?` or `:name`) filled in safely by the driver, instead of pasting values into the SQL text. Prevents **SQL injection** (an attacker sneaking SQL in through a value). *(Section [20](#20-reading-from-databases-and-web-apis))*
- **Parameters:** the numbers that pin down a distribution's exact shape (the normal's mean μ "mu" and standard deviation σ "sigma"). *(Section [54](#54-probability-distributions-normal-binomial-poisson-and-more))*
- **Parametric test:** assumes a distribution shape (t-test: roughly normal means). **Non-parametric test:** makes fewer assumptions, often using ranks (Mann–Whitney U). *(Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests))*
- **Parquet:** a **columnar** file format: values of each column are stored together, compressed, with the column's type. Created for big-data systems (Hadoop, Spark) and now standard everywhere. *(Section [19](#19-reading-and-writing-files-csv-excel-json-and-parquet))*
- **Parsing:** turning text into structured values (the text `"60"` into the number `60`). *(Section [5](#5-reading-files-with-plain-python-text-csv-and-json))*
- **Partition:** SQL's word for "group" in a window function. *(Section [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking))*
- **Partitioning:** splitting stored data into folders by a key (one folder per day or month), so queries and re-runs touch only the parts they need. *(Section [62](#62-data-pipelines-and-data-quality-in-production))*
- **PDF (probability density function):** for continuous variables, a curve whose **area** over a range is the probability of landing in that range. (The height at one point is a density, not a probability; P(X = exactly 2.37) is 0.) *(Section [54](#54-probability-distributions-normal-binomial-poisson-and-more))*
- **Pearson correlation (r):** covariance divided by both standard deviations, so it's unit-free and always between −1 and +1. Measures **linear** (straight-line) association. *(Section [52](#52-correlation-covariance-and-causation))*
- **Peeking:** checking results repeatedly and stopping as soon as p < 0.05. Inflates false positives dramatically. *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **Percentile / quantile:** the value below which a given percentage of the data falls. The 90th percentile is bigger than 90% of the values. *(Section [12](#12-aggregations-and-the-axis-argument), [51](#51-describing-data-centre-spread-and-shape))*
- **Percentile bootstrap interval:** the 2.5th and 97.5th percentiles of the bootstrapped statistics. *(Section [56](#56-confidence-intervals-and-the-bootstrap))*
- **Percentile rank:** rank as a fraction from 0 to 1 (`pct=True`). *(Section [23](#23-sorting-ranking-and-top-n))*
- **Perceptually uniform:** equal steps in value look like equal steps in colour (`viridis` is; the old rainbow `jet` isn't). *(Section [45](#45-styling-annotation-and-saving-charts))*
- **Performance:** how fast code runs and how much memory it uses. *(Section [39](#39-performance-vectorise-avoid-loops-and-measure))*
- **Period:** a whole span with a frequency: the month 2025-03, the day 2025-03-14, the quarter 2025Q1. *(Section [37](#37-dates-and-times-parsing-dt-time-zones-and-periods))*
- **Permutation test:** shuffle the group labels many times to build the null distribution directly by simulation. *(Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests))*
- **PII (personally identifiable information):** data that can identify a person (name, email, phone, address, ID numbers); it must be protected and often removed before sharing. *(Section [28](#28-text-data-the-str-accessor-and-regular-expressions))*
- **`pipe(func)`:** puts your own function into a chain: `df.pipe(clean_names)` is `clean_names(df)`. *(Section [25](#25-method-chaining-and-copy-on-write-pandas-3))*
- **Pipeline:** a sequence of processing steps where each step's output feeds the next. *(Section [25](#25-method-chaining-and-copy-on-write-pandas-3))*
- **Pivot:** rotate values from a column into column **headers**. **Pivot table:** a pivot that also **aggregates** duplicates (sum, mean…), like Excel's pivot tables. *(Section [35](#35-reshaping-pivot_table-melt-crosstab-and-explode))*
- **Plot / draw:** add marks (lines, bars, points) to an axes. *(Section [43](#43-your-first-charts-with-matplotlib))*
- **Plotly:** a charting library that draws in the web browser (JavaScript underneath). **Plotly Express** (`px`) is its quick, DataFrame-first interface. *(Section [49](#49-interactive-charts-with-plotly))*
- **PMF (probability mass function):** for discrete variables, P(X = k) for each k. *(Section [54](#54-probability-distributions-normal-binomial-poisson-and-more))*
- **Point estimate:** a single best guess (the sample mean, ₹812). *(Section [56](#56-confidence-intervals-and-the-bootstrap))*
- **Pointer (reference):** an address that says where some other object lives in memory. *(Section [6](#6-why-numpy-arrays-vs-lists-and-how-arrays-sit-in-memory))*
- **Polars:** a fast DataFrame library (imported as `pl`), built on Arrow, with a Python API. *(Section [41](#41-polars-fast-dataframes-with-lazy-queries))*
- **Population:** everyone or everything you want to know about (all customers, all future orders). *(Section [55](#55-sampling-the-central-limit-theorem-and-standard-error))*
- **Population vs sample; `ddof`:** dividing the variance by `n − 1` instead of `n` (**Bessel's correction**) corrects for using the sample's own mean, which sits closer to the sample's values than the true mean does. pandas uses `n − 1` by default (`ddof=1`); NumPy uses `n` (`ddof=0`). *(Section [51](#51-describing-data-centre-spread-and-shape))*
- **Power (1 − β):** the probability of detecting the MDE if it's real; usually 80%. *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **Pre-allocate:** create an array of the final size first, then fill it. *(Section [7](#7-creating-arrays-array-arange-linspace-zeros-ones-and-full))*
- **Pre-attentive attributes:** properties the eye notices before you think: colour, size, position. Use them for the message. *(Section [50](#50-choosing-the-right-chart-and-not-misleading))*
- **Precision:** how many digits a number type keeps. `float64` keeps about 15–16 significant digits; `float32` about 7. *(Section [8](#8-shape-dimensions-and-dtypes))*
- **Primary metric (OEC, overall evaluation criterion):** the one metric that decides the test (conversion rate, revenue per user). *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **Prior:** what you believed before the evidence (P(A)). **Likelihood:** how probable the evidence is under the claim (P(B | A)). **Posterior:** the updated belief (P(A | B)). *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **Product sense:** the ability to reason about what a product's users need and how to measure whether a feature helps them. *(Section [66](#66-interview-problems-pandas-numpy-and-sql-style-questions))*
- **Profiling:** measuring where time is actually spent. *(Section [39](#39-performance-vectorise-avoid-loops-and-measure))*
- **Profiling report:** an automatically generated overview of every column (tools such as `ydata-profiling`, `skimpy`). *(Section [60](#60-a-complete-exploratory-data-analysis-eda))*
- **Projection:** choosing columns (SQL's `SELECT a, b`). *(Section [21](#21-selecting-data-columns--loc-and-iloc))*
- **Pseudo-random numbers:** numbers made by a deterministic formula that only **looks** random. Good enough for data science; not for passwords (use Python's `secrets` module for those). *(Section [15](#15-random-numbers-and-simulation))*
- **Pyramid principle (answer first):** start with the conclusion, then the supporting points, then the details (Barbara Minto's method, used by consulting firms). *(Section [63](#63-communicating-results-reports-dashboards-and-data-storytelling))*

### Q

- **`qcut`:** bins by **quantiles**, so each bin holds about the same number of rows (quartiles = 4 bins, deciles = 10). *(Section [29](#29-categorical-data-and-binning-cut-and-qcut))*
- **Qualitative (categorical) palette:** distinct colours for unordered groups (`tab10`). *(Section [45](#45-styling-annotation-and-saving-charts))*
- **Quantifier:** how many times something repeats: `+` (1 or more), `*` (0 or more), `?` (0 or 1), `{6}` (exactly 6), `{2,4}` (2 to 4). *(Section [28](#28-text-data-the-str-accessor-and-regular-expressions))*
- **Quartiles (25%, 50%, 75%):** the values that cut sorted data into four equal parts. The 50% quartile is the median. *(Section [18](#18-dataframes-creating-inspecting-and-understanding-a-table))*
- **Quartiles (Q1, Q3):** the values below which 25% and 75% of the data fall. *(Section [30](#30-outliers-and-data-validation))*
- **Quarto:** an open-source tool that turns notebooks and Markdown into reports, websites and slides. *(Section [63](#63-communicating-results-reports-dashboards-and-data-storytelling))*
- **`query`:** filtering with a readable text expression: `df.query("price > 1000 and city == 'Pune'")`. *(Section [22](#22-filtering-rows-conditions-isin-between-and-query))*
- **Query engine:** software that plans and runs queries efficiently (DuckDB, Polars' engine, DataFusion, Spark). *(Section [64](#64-whats-new-modern-data-tooling-20232026))*
- **Query optimiser:** the part that rewrites a plan to do less work. **Predicate pushdown:** applying filters as early as possible (even inside the file reader). **Projection pushdown:** reading only the columns the query uses. *(Section [41](#41-polars-fast-dataframes-with-lazy-queries))*
- **Quoting:** a value containing the delimiter is wrapped in quotes: `"Pune, MH"`. *(Section [5](#5-reading-files-with-plain-python-text-csv-and-json))*

### R

- **RAM:** the computer's working memory. A laptop has 8–32 GB; if your data (plus the copies operations make) doesn't fit, the program crashes or slows to a crawl as the system **swaps** to disk. *(Section [40](#40-memory-dtypes-categoricals-chunking-and-apache-arrow))*
- **Random sample:** every member of the population has a known, fair chance of being chosen. *(Section [55](#55-sampling-the-central-limit-theorem-and-standard-error))*
- **Random variable:** a quantity whose value depends on chance (the number of clicks today). *(Section [54](#54-probability-distributions-normal-binomial-poisson-and-more))*
- **Randomisation unit:** what you randomise: users (most common), sessions, or whole cities. *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **Randomised controlled experiment:** the gold standard for causation: assign the treatment **at random**, so confounders are balanced between groups (Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls)). *(Section [52](#52-correlation-covariance-and-causation))*
- **Range:** a sequence of numbers from a start up to (but usually not including) a stop, moving by a **step**. *(Section [7](#7-creating-arrays-array-arange-linspace-zeros-ones-and-full), [51](#51-describing-data-centre-spread-and-shape))*
- **Rank:** a row's position in sorted order. **Tie:** two rows with the same value. *(Section [23](#23-sorting-ranking-and-top-n))*
- **Ranking methods for ties:** `"first"` (by order of appearance), `"min"` (all tied rows get the lowest rank, then a gap: 1, 2, 2, 4 — "Olympic" ranking, SQL `RANK()`), `"dense"` (tied rows share a rank, no gap: 1, 2, 2, 3 — SQL `DENSE_RANK()`), `"average"` (the default: tied rows get the mean of their positions: 2.5). *(Section [23](#23-sorting-ranking-and-top-n))*
- **Rare categories:** labels that appear only a few times; often grouped into "Other". *(Section [29](#29-categorical-data-and-binning-cut-and-qcut))*
- **Raster vs vector:** **raster** images (PNG, JPG) are grids of pixels; **vector** images (SVG, PDF) store shapes and stay sharp at any size. *(Section [45](#45-styling-annotation-and-saving-charts))*
- **Rate limit:** the maximum number of requests an API allows per period. *(Section [20](#20-reading-from-databases-and-web-apis))*
- **Raw string (`r"..."`):** a Python string where backslashes are kept as typed. Always write regexes as raw strings. *(Section [28](#28-text-data-the-str-accessor-and-regular-expressions))*
- **Reactive notebook:** a notebook where changing a cell automatically re-runs the cells that depend on it, so state can't get out of sync (**marimo**). *(Section [64](#64-whats-new-modern-data-tooling-20232026))*
- **Reconciliation:** comparing two sources of the same facts to find differences. *(Section [34](#34-combining-tables-ii-concat-validation-and-merge-pitfalls))*
- **Record:** one row of data, such as one order. A list of dicts is a list of records. *(Section [3](#3-python-refresher-for-data-work-lists-dicts-comprehensions-and-functions))*
- **Reference line / band:** a horizontal or vertical line (`axhline`) or shaded region (`axvspan`) marking a target or a period. *(Section [45](#45-styling-annotation-and-saving-charts))*
- **Regression:** modelling how an outcome depends on one or more inputs. *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*
- **Regression line:** the best-fitting straight line through a scatter (`regplot` draws it with a CI band). *(Section [47](#47-seaborn-ii-relationships-categories-and-facets))*
- **Regular expression (regex):** a mini-language for text patterns. Python's built-in `re` module and pandas `.str` methods understand it. *(Section [28](#28-text-data-the-str-accessor-and-regular-expressions))*
- **Replacement scan:** DuckDB's trick of letting SQL refer to a Python DataFrame variable by name (`FROM orders` finds the `orders` DataFrame). *(Section [42](#42-duckdb-sql-on-dataframes-and-files))*
- **Reproducible:** someone else running your code gets exactly your results. *(Section [15](#15-random-numbers-and-simulation))*
- **Resample:** regroup by a new time frequency. **Downsampling** = coarser (days → months, needs aggregation). **Upsampling** = finer (months → days, needs filling). *(Section [38](#38-time-series-resample-rolling-shift-and-window-functions))*
- **Resample with replacement:** draw n values from your n values, where each draw can pick a value already picked (some values appear twice, some not at all). *(Section [56](#56-confidence-intervals-and-the-bootstrap))*
- **Reshape:** give an array a new shape with the **same total size**. *(Section [14](#14-reshaping-stacking-splitting-and-sorting))*
- **Residual:** actual y − predicted y for one row: what the model missed. *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*
- **Retention:** the share of users who come back (are still active) some time after they started; a **cohort retention table** shows it per signup cohort and period. *(Section [35](#35-reshaping-pivot_table-melt-crosstab-and-explode))*
- **Reverse causation:** y causes x, not the other way round. *(Section [52](#52-correlation-covariance-and-causation))*
- **RFM:** **R**ecency (time since the last purchase), **F**requency (how often), **M**onetary (how much): three classic customer features. *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Right join:** the mirror: every row of the right table. *(Section [33](#33-combining-tables-i-merge-and-join-types))*
- **Robust:** not easily distorted by extreme values. The median and IQR are robust; the mean and standard deviation are not. *(Section [30](#30-outliers-and-data-validation))*
- **Robust statistic:** one that extreme values barely move (median, IQR) as opposed to one they distort (mean, std). *(Section [51](#51-describing-data-centre-spread-and-shape))*
- **Rolling window (moving window):** for each point, look at the last N values (or the last N days) and compute something, like a **moving average**. *(Section [38](#38-time-series-resample-rolling-shift-and-window-functions))*
- **Row explosion (fan-out):** a merge producing far more rows than expected because keys repeat on both sides. *(Section [34](#34-combining-tables-ii-concat-validation-and-merge-pitfalls))*
- **Row iteration:** `iterrows`, `itertuples` or `apply(axis=1)`: Python code run once per row. *(Section [39](#39-performance-vectorise-avoid-loops-and-measure))*
- **Row-major (C) order:** the reading order NumPy uses by default: along each row left to right, then the next row, like reading a book. *(Section [14](#14-reshaping-stacking-splitting-and-sorting))*
- **Rust:** a fast, memory-safe compiled programming language, used to write Polars' engine. *(Section [41](#41-polars-fast-dataframes-with-lazy-queries))*
- **r² (coefficient of determination):** for a straight-line fit, the share of y's variance explained by x. r = 0.5 → r² = 0.25 (25%). *(Section [52](#52-correlation-covariance-and-causation))*
- **R² (R-squared):** the share of y's variance the model explains (0 to 1). **Adjusted R²** penalises adding useless predictors. *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*

### S

- **Sample:** the part you actually measured. *(Section [55](#55-sampling-the-central-limit-theorem-and-standard-error))*
- **Sample size calculation (power analysis):** working out how many users you need for a given baseline, MDE, α and power. *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **Sampling bias:** a sampling method that systematically over- or under-represents some groups (surveying only app users about the website). *(Section [55](#55-sampling-the-central-limit-theorem-and-standard-error))*
- **Sampling distribution:** the distribution of a statistic (such as the mean) over many hypothetical repeated samples. *(Section [55](#55-sampling-the-central-limit-theorem-and-standard-error))*
- **Sampling with / without replacement:** with replacement, an item can be picked again (rolling a die); without, each item is picked at most once (dealing cards). *(Section [15](#15-random-numbers-and-simulation))*
- **Scalar:** a single number (0 dimensions). **Vector:** 1 dimension. **Matrix:** 2 dimensions. **Tensor:** the general word for any number of dimensions (used by PyTorch and TensorFlow). *(Section [8](#8-shape-dimensions-and-dtypes))*
- **Scalar access:** getting one single value; `.at[label, col]` and `.iat[i, j]` are the fast versions. *(Section [21](#21-selecting-data-columns--loc-and-iloc))*
- **Scalar operation:** combining an array with a single number: `prices * 1.18` multiplies every element. *(Section [11](#11-vectorised-maths-and-universal-functions))*
- **Scaling:** putting numeric features on comparable ranges. **Standardisation** = (x − mean) / std; **min–max** = (x − min) / (max − min); **robust** = (x − median) / IQR. *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **`scan_*` vs `read_*`:** `scan_parquet`/`scan_csv` start a **lazy** query on a file; `read_*` loads it eagerly. *(Section [41](#41-polars-fast-dataframes-with-lazy-queries))*
- **Scatter plot:** a chart with one dot per observation, placed by two numeric values (x and y), for seeing relationships. *(Section [43](#43-your-first-charts-with-matplotlib))*
- **Schema:** the description of a table: each column's name and type. *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data), [19](#19-reading-and-writing-files-csv-excel-json-and-parquet))*
- **Schema (data contract):** the agreed rules for a table: column names, types and checks. *(Section [30](#30-outliers-and-data-validation))*
- **scikit-learn / PyTorch:** the main Python libraries for classic machine learning and for deep learning (neural networks), taught in `machine-learning.md` and `deep-learning.md`. *(Section [1](#1-how-to-use-these-notes-and-what-data-scientists-do))*
- **`scipy.stats`:** SciPy's module with every common distribution: `.pmf`/`.pdf`, `.cdf`, `.ppf` (inverse CDF: the value at a given percentile), `.rvs` (random samples), `.mean()`, `.std()`. *(Section [54](#54-probability-distributions-normal-binomial-poisson-and-more))*
- **Seaborn:** a statistical plotting library built on Matplotlib, imported as `sns`. *(Section [46](#46-seaborn-i-distributions))*
- **Seasonality:** a pattern that repeats at a fixed period (weekends, December). **Trend:** a long-term rise or fall. **Noise:** random ups and downs. *(Section [38](#38-time-series-resample-rolling-shift-and-window-functions))*
- **Seed:** the starting number for the formula. Same seed → same sequence of numbers. *(Section [15](#15-random-numbers-and-simulation))*
- **Selection:** choosing part of a table: some columns, some rows, or both. *(Section [21](#21-selecting-data-columns--loc-and-iloc))*
- **Self-join:** joining a table to itself (employees to their managers, who are also employees). *(Section [33](#33-combining-tables-i-merge-and-join-types))*
- **Self-serve analytics:** tools that let non-analysts explore data themselves (BI tools, semantic layers). *(Section [63](#63-communicating-results-reports-dashboards-and-data-storytelling))*
- **Semantic layer / metrics layer:** one shared, central definition of each metric so every dashboard computes "revenue" the same way. *(Section [63](#63-communicating-results-reports-dashboards-and-data-storytelling))*
- **Semi-join:** rows in the left table that **do** have a match, without adding the right table's columns. *(Section [33](#33-combining-tables-i-merge-and-join-types))*
- **Sensitivity (true positive rate):** P(test positive | sick). **Specificity (true negative rate):** P(test negative | healthy). **False positive rate:** 1 − specificity. *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **Sequential colormap:** light-to-dark for values from low to high (`viridis`, `Blues`). *(Section [45](#45-styling-annotation-and-saving-charts))*
- **Sequential testing:** methods designed for looking at results early without inflating errors. *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **Serialisation:** turning in-memory objects into text or bytes to save or send (`json.dumps`); the reverse is **deserialisation** (`json.loads`). *(Section [5](#5-reading-files-with-plain-python-text-csv-and-json))*
- **Series:** one column of data: values of one type, plus an **index**. *(Section [17](#17-pandas-series-labelled-1d-data))*
- **Series (in charts):** one set of values drawn together, like one line. Not the same as a pandas Series, though one often becomes the other. *(Section [43](#43-your-first-charts-with-matplotlib))*
- **Server:** a program (or computer) that waits for requests and answers them: a database server, a web server. *(Section [20](#20-reading-from-databases-and-web-apis))*
- **Set:** an unordered collection with **no duplicates**: `{"Pune", "Delhi"}`. Fast "is this in it?" checks. *(Section [3](#3-python-refresher-for-data-work-lists-dicts-comprehensions-and-functions))*
- **`SettingWithCopyWarning`:** the confusing warning older pandas gave for chained assignment. Gone in pandas 3, because the behaviour is now always the same. *(Section [25](#25-method-chaining-and-copy-on-write-pandas-3))*
- **Shape:** a tuple with the size along each axis: `(3, 4)` means 3 rows and 4 columns. *(Section [8](#8-shape-dimensions-and-dtypes))*
- **Shared axes (`sharex` / `sharey`):** charts that use the same scale, so they're directly comparable. *(Section [44](#44-matplotlib-anatomy-figures-axes-and-subplots))*
- **Shift / lag:** move values down by N steps so each row sees the value from N periods ago. **Lead:** the opposite. *(Section [38](#38-time-series-resample-rolling-shift-and-window-functions))*
- **`shift` within groups:** the previous (or next) row's value **inside the same group**: last order's date for the same customer. *(Section [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking))*
- **Significance level (α, "alpha"):** the cut-off decided in advance, usually 0.05. If p < α, "reject H₀" (the result is **statistically significant**). *(Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests))*
- **SIMD (single instruction, multiple data):** CPU instructions that apply one operation to several numbers in a single step. *(Section [6](#6-why-numpy-arrays-vs-lists-and-how-arrays-sit-in-memory))*
- **Simpson's paradox:** a trend that appears in every group **reverses** when the groups are combined, because the groups differ in size or mix. *(Section [52](#52-correlation-covariance-and-causation))*
- **Simulation (Monte Carlo method):** estimating something by generating many random trials and counting outcomes. Named after the Monte Carlo casino. *(Section [15](#15-random-numbers-and-simulation))*
- **`size` vs `count`:** `size` counts **rows** in each group; `count` counts **non-missing values** in a column. *(Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine))*
- **Skew:** a lopsided distribution. **Right-skewed** has a long tail to the right (incomes, order values). **Modality:** the number of peaks (**bimodal** = two peaks, often two groups mixed together). *(Section [46](#46-seaborn-i-distributions))*
- **Skewness:** lopsidedness. **Right (positive) skew:** a long tail of big values (incomes, prices, waiting times). **Left (negative) skew:** a long tail of small values (exam scores on an easy test). *(Section [51](#51-describing-data-centre-spread-and-shape))*
- **Slice:** a range of positions written `start:stop:step`. `stop` is **excluded**. Leave a part out to mean "from the beginning", "to the end" or "step 1". *(Section [9](#9-indexing-and-slicing-1d-and-2d-views-vs-copies))*
- **Small multiples (facets):** the same chart repeated for each group, on shared scales. *(Section [44](#44-matplotlib-anatomy-figures-axes-and-subplots))*
- **Smoothing (target encoding):** pulling small categories' averages towards the overall average, because averages of a few rows are noisy. *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Sort:** arrange in order. **argsort:** the **positions** that would sort the array (used to sort one array by another). *(Section [14](#14-reshaping-stacking-splitting-and-sorting))*
- **Sort key:** the column(s) you sort by. With several keys, the second breaks ties in the first. *(Section [23](#23-sorting-ranking-and-top-n))*
- **Spark (Apache Spark):** a system that spreads data processing across many computers (a **cluster**) for data too big for one machine. *(Section [1](#1-how-to-use-these-notes-and-what-data-scientists-do))*
- **Spearman correlation (ρ, "rho"):** Pearson's r computed on the **ranks** of the values. Measures **monotonic** association (always going up, or always down, even if curved) and resists outliers. *(Section [52](#52-correlation-covariance-and-causation))*
- **Spilling to disk:** writing temporary data to disk when memory runs out, so queries on data bigger than RAM still finish. *(Section [42](#42-duckdb-sql-on-dataframes-and-files))*
- **Split:** cut one array into several. *(Section [14](#14-reshaping-stacking-splitting-and-sorting))*
- **Split–apply–combine:** the three-step pattern above, named by Hadley Wickham. *(Section [31](#31-grouping-i-groupby-agg-and-split-apply-combine))*
- **Spurious correlation:** a correlation with no meaningful connection (two unrelated trends that both rise over time). *(Section [52](#52-correlation-covariance-and-causation))*
- **SQL (Structured Query Language):** the language for asking databases questions: `SELECT city, SUM(price) FROM orders GROUP BY city`. Taught in `sql-postgresql.md`. *(Section [20](#20-reading-from-databases-and-web-apis))*
- **SQLAlchemy:** the standard Python library for connecting to many databases with one interface; pandas uses it for anything other than SQLite. *(Section [20](#20-reading-from-databases-and-web-apis))*
- **SQLite:** a small database stored in a single file (or in memory), built into Python as the `sqlite3` module. Perfect for examples and small apps. *(Section [20](#20-reading-from-databases-and-web-apis))*
- **SRM (sample ratio mismatch):** the groups' sizes differ from the planned split (e.g. 50.8% / 49.2% on a huge test): a sign of a bug in assignment or logging. Checked with a chi-square test. *(Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls))*
- **Stable sort:** rows with equal keys keep their original order. Needed when you sort in several passes. *(Section [23](#23-sorting-ranking-and-top-n))*
- **`stack()`:** pivot the column headers into the innermost index level (wide → long). *(Section [36](#36-multiindex-stack-and-unstack))*
- **Stakeholder:** a person who uses or is affected by your analysis (a product manager, a marketing lead). *(Section [63](#63-communicating-results-reports-dashboards-and-data-storytelling))*
- **Standard deviation (std):** a measure of how spread out values are around the mean (Section [51](#51-describing-data-centre-spread-and-shape)). **Variance** is the std squared. *(Section [12](#12-aggregations-and-the-axis-argument))*
- **Standard deviation (std, s or σ):** the square root of the variance, in the **same units** as the data. Roughly "how far a typical value is from the mean". *(Section [51](#51-describing-data-centre-spread-and-shape))*
- **Standard error (SE):** the standard deviation of the sampling distribution: how much a statistic typically varies between samples. For a mean, SE = σ / √n (estimated with the sample's std, s / √n). *(Section [55](#55-sampling-the-central-limit-theorem-and-standard-error))*
- **Standard error of a coefficient:** how uncertain the coefficient is; its 95% CI is roughly coefficient ± 2 SE. *(Section [59](#59-regression-for-analysis-statsmodels-coefficients-and-confidence))*
- **Standard library / module:** the collection of modules that come with Python (`csv`, `json`, `collections`, `math`); a **module** is one importable file of code. *(Section [3](#3-python-refresher-for-data-work-lists-dicts-comprehensions-and-functions))*
- **Standardise (z-score):** subtract the mean and divide by the standard deviation, so a column has mean 0 and standard deviation 1. *(Section [13](#13-broadcasting-maths-between-arrays-of-different-shapes))*
- **Static export:** saving a PNG/SVG of the current view (`fig.write_image`, uses the `kaleido` package). *(Section [49](#49-interactive-charts-with-plotly))*
- **Statistics:** the maths of drawing conclusions from data that contains randomness, and of saying how sure you are. *(Section [1](#1-how-to-use-these-notes-and-what-data-scientists-do))*
- **Stickiness:** DAU ÷ MAU: how many of the month's users come back on a typical day (20% means users are active about 6 days a month). *(Section [66](#66-interview-problems-pandas-numpy-and-sql-style-questions))*
- **`.str` accessor:** gives every Python string method (and more) to a pandas text column: `df["city"].str.lower()`. *(Section [28](#28-text-data-the-str-accessor-and-regular-expressions))*
- **`str` dtype (pandas 3):** the new default type for text columns. Older pandas stored text in the catch-all `object` type; you'll still see `object` for mixed or unusual values. *(Section [18](#18-dataframes-creating-inspecting-and-understanding-a-table))*
- **Stratified sampling:** sampling separately within groups (cities, plans) so each is represented. *(Section [55](#55-sampling-the-central-limit-theorem-and-standard-error))*
- **Streaming / out-of-core:** processing data bigger than memory by never holding all of it at once. *(Section [40](#40-memory-dtypes-categoricals-chunking-and-apache-arrow))*
- **Streaming engine:** processing data in batches so results can be computed on data bigger than RAM. *(Section [41](#41-polars-fast-dataframes-with-lazy-queries))*
- **Streamlit:** a Python library that turns a script into an interactive web app with charts and filters (Section [63](#63-communicating-results-reports-dashboards-and-data-storytelling)). *(Section [18](#18-dataframes-creating-inspecting-and-understanding-a-table))*
- **String:** text. **Substring:** a piece of a string. *(Section [28](#28-text-data-the-str-accessor-and-regular-expressions))*
- **Strip / swarm plot:** every individual point, jittered or packed so they don't overlap. *(Section [46](#46-seaborn-i-distributions))*
- **Structured data:** data in rows and columns with fixed meanings. **Unstructured:** text, images, audio. **Semi-structured:** JSON and XML, which have labels but flexible nesting. *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **Style sheet / rcParams:** global default settings for fonts, colours and sizes. *(Section [45](#45-styling-annotation-and-saving-charts))*
- **Subplot:** one axes inside a grid of axes. *(Section [44](#44-matplotlib-anatomy-figures-axes-and-subplots))*
- **Suffixes:** endings added to columns with the same name in both tables (`_x`, `_y` by default). *(Section [33](#33-combining-tables-i-merge-and-join-types))*
- **Summary statistics:** numbers that describe a column: count, mean, standard deviation, min, quartiles, max. *(Section [18](#18-dataframes-creating-inspecting-and-understanding-a-table))*

### T

- **t distribution:** like the normal but with heavier tails, accounting for the extra uncertainty of estimating σ from a small sample; nearly identical to the normal for n above ~30. **Degrees of freedom (df)** = n − 1 for a mean. *(Section [56](#56-confidence-intervals-and-the-bootstrap))*
- **Table format:** a layer over Parquet files that adds transactions, schema changes and "time travel" (reading old versions): **Apache Iceberg**, **Delta Lake**, **DuckLake**. *(Section [64](#64-whats-new-modern-data-tooling-20232026))*
- **Tail:** the far ends of a distribution. "Heavy-tailed" = extreme values are more common than a normal curve predicts. *(Section [54](#54-probability-distributions-normal-binomial-poisson-and-more))*
- **Target (label, outcome):** the column you want to predict or explain. *(Section [60](#60-a-complete-exploratory-data-analysis-eda))*
- **Target encoding:** each category replaced by the average target for that category (with smoothing). *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **Test statistic:** a number summarising how far the data are from H₀ (a t value, a χ² value, a z value). *(Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests))*
- **Text (unstructured):** free-form words: reviews, emails. *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **Tick / tick label:** the small marks along an axis and their numbers or names. *(Section [43](#43-your-first-charts-with-matplotlib))*
- **Tick formatter:** a rule turning tick values into labels (`₹20k`, `35%`). *(Section [45](#45-styling-annotation-and-saving-charts))*
- **Tidy data:** a table where **each variable is a column, each observation is a row, and each value is a single cell**. *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **Time series:** values indexed by time, in order. *(Section [38](#38-time-series-resample-rolling-shift-and-window-functions))*
- **Time zone:** a region's rule for local time: `Asia/Kolkata` (UTC+5:30), `Europe/London` (UTC+0 or +1 in summer). *(Section [37](#37-dates-and-times-parsing-dt-time-zones-and-periods))*
- **`time.perf_counter()`:** a precise clock for timing a block of code once. *(Section [39](#39-performance-vectorise-avoid-loops-and-measure))*
- **Timedelta:** a duration: 3 days, 2 hours. `date2 - date1` gives a timedelta. *(Section [37](#37-dates-and-times-parsing-dt-time-zones-and-periods))*
- **`%timeit` / `timeit`:** runs a line many times and reports the typical time (in a notebook, `%timeit expr`; in a script, the `timeit` module). *(Section [39](#39-performance-vectorise-avoid-loops-and-measure))*
- **Timestamp:** a date and time. **Epoch time:** seconds since 1 January 1970 (UTC), a common way APIs send times. *(Section [27](#27-duplicates-data-types-and-type-conversion))*
- **Timestamp (`datetime64`):** a specific moment: 2025-03-14 09:30:00. *(Section [37](#37-dates-and-times-parsing-dt-time-zones-and-periods))*
- **Tooltip (hover label):** the box that appears when you point at a mark. *(Section [49](#49-interactive-charts-with-plotly))*
- **Top-N:** the N largest (or smallest) rows. *(Section [23](#23-sorting-ranking-and-top-n))*
- **Top-N per group:** the N largest rows inside every group. *(Section [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking))*
- **Trailing dimensions:** the axes at the **end** (right side) of a shape. Broadcasting compares shapes starting from the right. *(Section [13](#13-broadcasting-maths-between-arrays-of-different-shapes))*
- **Training set / test set:** rows the model learns from / rows kept aside to measure performance honestly. *(Section [61](#61-feature-engineering-preparing-data-for-machine-learning))*
- **`transform`:** runs a function per group and returns a result **the same length as the original**, lined up row by row. *(Section [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking))*
- **Transpose (`.T`):** swap rows and columns: element `[i, j]` moves to `[j, i]`. *(Section [14](#14-reshaping-stacking-splitting-and-sorting))*
- **Truncated axis:** an axis that doesn't start at zero. Fine for lines (which show change), misleading for bars (whose **length** is the value). *(Section [50](#50-choosing-the-right-chart-and-not-misleading))*
- **Tuple:** like a list but **can't be changed** after creation: `(3, 1)`. Used for fixed groups like `(row, column)`. *(Section [3](#3-python-refresher-for-data-work-lists-dicts-comprehensions-and-functions))*
- **Twin axes (`twinx`):** a second y-axis on the right, sharing the x-axis. *(Section [44](#44-matplotlib-anatomy-figures-axes-and-subplots))*
- **Two-sided vs one-sided test:** two-sided looks for a difference in either direction (the usual default); one-sided only in one, chosen **before** seeing data. *(Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests))*
- **Type conversion (casting):** changing a column's type. *(Section [27](#27-duplicates-data-types-and-type-conversion))*
- **Type I error (false positive):** rejecting a true H₀; its probability is α. *(Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests))*
- **Type II error (false negative):** missing a real effect; its probability is β. **Power** = 1 − β (Section [58](#58-ab-testing-end-to-end-design-power-sample-size-and-pitfalls)). *(Section [57](#57-hypothesis-testing-p-values-t-tests-chi-square-and-non-parametric-tests))*

### U

- **ufunc (universal function):** a NumPy function that works element-wise on arrays of any shape: `np.sqrt`, `np.exp`, `np.log`, `np.abs`, `np.maximum`, … *(Section [11](#11-vectorised-maths-and-universal-functions))*
- **Unicode:** the standard numbering of every character in every language (UTF-8 is a way to store it as bytes). *(Section [6](#6-why-numpy-arrays-vs-lists-and-how-arrays-sit-in-memory))*
- **Uniform distribution:** every value in a range is equally likely (a fair die). *(Section [15](#15-random-numbers-and-simulation))*
- **Union (A or B):** P(A or B) = P(A) + P(B) − P(A and B) (subtract the overlap once). *(Section [53](#53-probability-basics-events-conditional-probability-and-bayes-rule))*
- **Union (SQL `UNION ALL`):** stacking rows from tables with the same columns; `UNION` also removes duplicates. *(Section [34](#34-combining-tables-ii-concat-validation-and-merge-pitfalls))*
- **Unique:** the distinct values, optionally with how often each appears. *(Section [14](#14-reshaping-stacking-splitting-and-sorting))*
- **Univariate / bivariate / multivariate analysis:** looking at one column alone / two together / many at once. *(Section [60](#60-a-complete-exploratory-data-analysis-eda))*
- **`unstack(level)`:** pivot an index level into the column headers (long → wide). *(Section [36](#36-multiindex-stack-and-unstack))*
- **Upcasting:** NumPy converting to a more general type so every element fits (mixing ints and floats gives floats). *(Section [8](#8-shape-dimensions-and-dtypes))*
- **UTC (Coordinated Universal Time):** the world's reference time, with no daylight saving. Store times in UTC; convert for display. *(Section [37](#37-dates-and-times-parsing-dt-time-zones-and-periods))*
- **uv:** a fast, modern Python package and project manager (installs libraries, creates venvs, records exact versions in a lock file). *(Section [2](#2-setting-up-python-virtual-environments-uv-and-jupyter-notebooks))*

### V

- **`validate=`:** tells `merge` the relationship you expect (`"one_to_one"`, `"one_to_many"`, `"many_to_one"`, `"many_to_many"`); it raises an error if the data breaks it. *(Section [34](#34-combining-tables-ii-concat-validation-and-merge-pitfalls))*
- **Value:** one cell: the price of one order. *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **Variable (column, field, feature):** one property measured for every observation: price, city, date. (In statistics "variable" means a column, not a Python variable.) *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **`@variable` in `query`:** refers to a Python variable from inside the query string. *(Section [22](#22-filtering-rows-conditions-isin-between-and-query))*
- **Variance:** the average squared distance from the mean. *(Section [51](#51-describing-data-centre-spread-and-shape))*
- **Vector:** an ordered list of numbers, like `[height, weight]`. Can be drawn as an arrow from the origin. *(Section [16](#16-linear-algebra-basics-dot-products-matrix-multiplication-and-solving-equations))*
- **Vectorisation:** writing an operation on a whole array (`a * 2`) so NumPy loops in compiled code instead of you looping in Python. *(Section [6](#6-why-numpy-arrays-vs-lists-and-how-arrays-sit-in-memory))*
- **Vectorised (again):** Series maths works on all values at once, like NumPy. *(Section [17](#17-pandas-series-labelled-1d-data))*
- **Vectorised operation:** one call that processes a whole column in compiled code (Section [11](#11-vectorised-maths-and-universal-functions)). *(Section [39](#39-performance-vectorise-avoid-loops-and-measure))*
- **View:** a new array object that **shares memory** with the original. Changing one changes the other. *(Section [9](#9-indexing-and-slicing-1d-and-2d-views-vs-copies))*
- **Violin plot:** a box plot's cousin showing the full density shape, mirrored. *(Section [46](#46-seaborn-i-distributions))*
- **Virtual environment ("venv"):** a private folder of installed libraries for **one** project, so two projects can use different versions without breaking each other. *(Section [2](#2-setting-up-python-virtual-environments-uv-and-jupyter-notebooks))*

### W

- **Whitespace:** spaces, tabs and newlines. `strip` removes it from both ends. *(Section [28](#28-text-data-the-str-accessor-and-regular-expressions))*
- **Why values go missing (MCAR, MAR, MNAR):** statisticians' three cases, in plain words: *(Section [26](#26-missing-values-finding-dropping-and-filling))*
- **Wide format:** one row per entity, with repeated measurements spread across columns. *(Section [35](#35-reshaping-pivot_table-melt-crosstab-and-explode))*
- **Wide vs long format:** wide puts repeated measurements side by side as columns (`jan`, `feb`, `mar`); long stacks them as rows (`month`, `sales`). Tidy data is usually long. *(Section [4](#4-what-data-looks-like-types-of-data-tables-and-tidy-data))*
- **Wilson interval:** a better CI for proportions (rates) than the simple formula, especially for small samples or rates near 0% or 100%. *(Section [56](#56-confidence-intervals-and-the-bootstrap))*
- **Window function (SQL):** a calculation across related rows that keeps every row: `SUM(revenue) OVER (PARTITION BY city)`. `transform` is pandas' version. *(Section [32](#32-grouping-ii-transform-filter-apply-and-group-wise-ranking), [42](#42-duckdb-sql-on-dataframes-and-files))*
- **Winsorising (capping, clipping):** replacing extreme values with a chosen limit (e.g. the 1st and 99th percentiles) instead of deleting them. *(Section [30](#30-outliers-and-data-validation))*

### Y

- **Year-over-year (YoY):** comparing with the same period last year, which removes seasonality. *(Section [38](#38-time-series-resample-rolling-shift-and-window-functions))*

### Z

- **z-score:** how many standard deviations a value is from the mean: z = (x − mean) / std. |z| > 3 is a common outlier flag for bell-shaped data. *(Section [30](#30-outliers-and-data-validation), [54](#54-probability-distributions-normal-binomial-poisson-and-more))*
- **Zero-copy:** handing data between tools without copying it, possible when both use Arrow. *(Section [40](#40-memory-dtypes-categoricals-chunking-and-apache-arrow))*

---
