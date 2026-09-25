# SQL and PostgreSQL: From Absolute Basics to Production

SQL explained from zero, using PostgreSQL, in **levels**: **Basic** (tables, `SELECT`, changing data) → **Easy** (functions, grouping, joins, CTEs) → **Moderate** (design, constraints, window functions, transactions, indexes, query plans) → **Advanced** (JSONB, full-text search, pgvector for AI, security, Python, backups, replication, scaling, PostgreSQL 17 and 18) → **Interview Prep**. **Each part uses only what earlier parts taught.**

Every section has the same shape: a **picture** where it helps, **theory** in plain words, **SQL** you can run, and **practice** with hidden answers and links. Every query was run on PostgreSQL 16 against the sample shop database built up in these notes, in order, and every result under **Output** is the real `psql` output. (Features that need PostgreSQL 17 or 18 are marked and weren't run.)

Each part ends with a ✅ **checkpoint**. The DSA notes (`dsa-python.md`) explain the data structures behind databases (B-trees, hashing, LSM trees, vector search); the Python notes cover the language used in Section [28](#28-using-postgresql-from-python-psycopg-pooling-and-sqlalchemy).

## Table of Contents

**[Part 1 — Basic: Databases and Your First Queries](#part-1--basic-databases-and-your-first-queries)**

1. [How to Use These Notes (and Set Up PostgreSQL)](#1-how-to-use-these-notes-and-set-up-postgresql)
2. [What Is a Database? Tables, Rows, Columns and Keys](#2-what-is-a-database-tables-rows-columns-and-keys)
3. [Your First Table: CREATE TABLE, INSERT and SELECT](#3-your-first-table-create-table-insert-and-select)
4. [Data Types and NULL](#4-data-types-and-null)
5. [SELECT in Depth: Filtering, Sorting and Limiting](#5-select-in-depth-filtering-sorting-and-limiting)
6. [Changing Data: UPDATE, DELETE and RETURNING](#6-changing-data-update-delete-and-returning)

**[Part 2 — Easy: Asking Bigger Questions](#part-2--easy-asking-bigger-questions)**

7. [Functions and Expressions: Text, Numbers, Dates and CASE](#7-functions-and-expressions-text-numbers-dates-and-case)
8. [Aggregation: COUNT, SUM, GROUP BY and HAVING](#8-aggregation-count-sum-group-by-and-having)
9. [Joins: Combining Tables](#9-joins-combining-tables)
10. [Subqueries and CTEs (WITH), Including Recursive Queries](#10-subqueries-and-ctes-with-including-recursive-queries)
11. [Set Operations: UNION, INTERSECT and EXCEPT](#11-set-operations-union-intersect-and-except)

**[Part 3 — Moderate: Designing Databases](#part-3--moderate-designing-databases)**

12. [Keys and Constraints: Letting the Database Protect Your Data](#12-keys-and-constraints-letting-the-database-protect-your-data)
13. [Designing Tables: Relationships and Normalisation](#13-designing-tables-relationships-and-normalisation)
14. [Changing the Schema: ALTER TABLE and Migrations](#14-changing-the-schema-alter-table-and-migrations)
15. [Views and Materialized Views](#15-views-and-materialized-views)
16. [Window Functions: Rankings, Running Totals and Comparing Rows](#16-window-functions-rankings-running-totals-and-comparing-rows)

**[Part 4 — Moderate: Transactions and Performance](#part-4--moderate-transactions-and-performance)**

17. [Transactions, ACID and Concurrency](#17-transactions-acid-and-concurrency)
18. [Indexes: Making Lookups Fast](#18-indexes-making-lookups-fast)
19. [Reading Query Plans with EXPLAIN](#19-reading-query-plans-with-explain)
20. [Making Queries Fast: Common Performance Patterns](#20-making-queries-fast-common-performance-patterns)

**[Part 5 — Advanced: PostgreSQL Power Features](#part-5--advanced-postgresql-power-features)**

21. [JSON and JSONB: Documents Inside PostgreSQL](#21-json-and-jsonb-documents-inside-postgresql)
22. [Arrays, Enums, Ranges and Generated Columns](#22-arrays-enums-ranges-and-generated-columns)
23. [Full-Text Search](#23-full-text-search)
24. [Functions, Procedures and Triggers](#24-functions-procedures-and-triggers)
25. [Upserts, MERGE and Bulk Loading](#25-upserts-merge-and-bulk-loading)
26. [pgvector: Vector Search for AI Applications](#26-pgvector-vector-search-for-ai-applications)

**[Part 6 — Advanced: PostgreSQL in Production](#part-6--advanced-postgresql-in-production)**

27. [Security: Roles, Permissions, Row-Level Security and SQL Injection](#27-security-roles-permissions-row-level-security-and-sql-injection)
28. [Using PostgreSQL from Python: psycopg, Pooling and SQLAlchemy](#28-using-postgresql-from-python-psycopg-pooling-and-sqlalchemy)
29. [Running PostgreSQL: Backups, Replication, VACUUM, Partitioning and Monitoring](#29-running-postgresql-backups-replication-vacuum-partitioning-and-monitoring)
30. [Scaling PostgreSQL, and What's New in PostgreSQL 17 and 18](#30-scaling-postgresql-and-whats-new-in-postgresql-17-and-18)
31. [PostgreSQL vs MySQL vs SQLite vs SQL Server: Dialect Differences](#31-postgresql-vs-mysql-vs-sqlite-vs-sql-server-dialect-differences)

**[Part 7 — Interview Prep: Revision](#part-7--interview-prep-revision)**

32. [Classic SQL Interview Problems (with Solutions)](#32-classic-sql-interview-problems-with-solutions)
33. [SQL and PostgreSQL Cheat Sheet](#33-sql-and-postgresql-cheat-sheet)
34. [Most Asked SQL and Database Theory Questions](#34-most-asked-sql-and-database-theory-questions)

---

# Part 1 — Basic: Databases and Your First Queries

> **Goal:** Understand what a database is, create tables, and read and change data with SELECT, INSERT, UPDATE and DELETE.  
> **You need:** Nothing. (Basic Python helps later, but isn't needed here.)

---

## 1. How to Use These Notes (and Set Up PostgreSQL)

![The learning path](images/sql/00-roadmap.svg)

### Theory

> **In simple words:** a **database** is an organised, permanent place to keep data. **SQL** (Structured Query Language, said "S-Q-L" or "sequel") is the language you use to ask it questions and change what's in it. **PostgreSQL** ("Postgres") is the free, open-source database these notes use.

**Why learn SQL in 2026?** Almost every app you use stores its data in a SQL database: banking, shopping, social media, hospital records. Data analysts, backend developers, data engineers, and AI/ML engineers all write SQL every day. It's also one of the most stable skills in tech: SQL written 30 years ago still runs today. PostgreSQL has become developers' most-used database in recent Stack Overflow surveys, and it now also powers AI features through extensions like **pgvector** (Section [26](#26-pgvector-vector-search-for-ai-applications)).

**These notes climb level by level, like the DSA notes:**

| Part | Level | You learn |
|---|---|---|
| 1 | Basic | What a database is, tables, data types, `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
| 2 | Easy | Functions, grouping and aggregates, joins, subqueries and CTEs, set operations |
| 3 | Moderate | Designing databases: keys, constraints, relationships, normalisation, migrations, views, window functions |
| 4 | Moderate | Transactions, isolation and locking, indexes, reading query plans, making queries fast |
| 5 | Advanced | PostgreSQL power features: JSONB, arrays, full-text search, functions and triggers, upserts and bulk loading, pgvector for AI |
| 6 | Advanced | Production: security, using Postgres from Python, backups and replication, scaling, what's new in PostgreSQL 17 and 18 |
| 7 | Interview Prep | Classic SQL interview problems, a cheat sheet, theory questions |

Each part uses only what came before it. Each section has a **picture** (where one helps), **theory** in plain words, **SQL** you can run, and **practice**. Every query in this file was run on PostgreSQL 16, and the results shown under **Output** are the real output of `psql`. SQL is also standardised, so about 80% of what you learn here works the same in MySQL, SQLite, SQL Server and Oracle; Section [31](#31-postgresql-vs-mysql-vs-sqlite-vs-sql-server-dialect-differences) lists the differences.

**Set up (choose one):**

1. **Install PostgreSQL** from [postgresql.org/download](https://www.postgresql.org/download/). On macOS, [Postgres.app](https://postgresapp.com/) is the easiest; on Windows, the EDB installer; on Ubuntu, `sudo apt install postgresql`.
2. **Docker:** `docker run --name pg -e POSTGRES_PASSWORD=secret -p 5432:5432 -d postgres:18`, then `docker exec -it pg psql -U postgres`.
3. **In the browser, no install:** a free hosted Postgres (Neon, Supabase) or an online playground such as [DB Fiddle](https://www.db-fiddle.com/) (pick PostgreSQL).

**psql, the command-line client.** `psql -U postgres` opens a prompt where you type SQL (end each statement with `;`). Its own commands start with a backslash:

| Command | Does |
|---|---|
| `\l` | List databases |
| `\c shop` | Connect to the database `shop` |
| `\dt` | List tables |
| `\d customers` | Describe a table (columns, types, indexes) |
| `\x` | Toggle "expanded" display for wide rows |
| `\timing` | Show how long each query takes |
| `\pset null '(null)'` | Show missing values as `(null)` instead of blank space (the outputs in these notes use this) |
| `\?` / `\h SELECT` | Help for psql commands / for an SQL command |
| `\q` | Quit |

Graphical tools are fine too: **pgAdmin**, **DBeaver**, **DataGrip**, **TablePlus**, or the database panel in VS Code.

### Practice

1. Install PostgreSQL (or start the Docker container) and open `psql`.
2. Run `CREATE DATABASE shop;` then `\c shop`. Everything in these notes runs in that database, in order.
3. Bookmark two practice sites: [PostgreSQL Exercises](https://pgexercises.com/) (free, Postgres-specific) and [LeetCode's SQL 50 study plan](https://leetcode.com/studyplan/top-sql-50/).

---

## 2. What Is a Database? Tables, Rows, Columns and Keys

![A table has columns (fields) and rows (records); keys link tables](images/sql/01-table-anatomy.svg)

### Theory

> **In simple words:** a relational database stores data in **tables**, which look like spreadsheets. Each **row** is one thing (one customer), each **column** is one fact about it (their name, their city). Tables are linked by **keys**, like a customer's ID written on each of their orders.

**Why not just use a spreadsheet or a file?** A spreadsheet is great for one person and a few thousand rows. A database adds what real applications need:

| Need | A database gives you |
|---|---|
| Millions or billions of rows | Fast search with indexes (Section [18](#18-indexes-making-lookups-fast)) |
| Many users at the same time | Safe concurrent reads and writes (Section [17](#17-transactions-acid-and-concurrency)) |
| Never losing data | Durability: data survives crashes and power cuts |
| Correct data | Rules (constraints) the database enforces, like "every order must belong to a real customer" |
| Asking questions | SQL: describe **what** you want, and the database works out **how** to get it |

**The vocabulary:**

| Word | Meaning | Example |
|---|---|---|
| **Database** | A collection of related tables | `shop` |
| **Table** (relation) | One kind of thing | `customers` |
| **Row** (record, tuple) | One item | Asha, from Pune |
| **Column** (field, attribute) | One fact about each item, with a fixed **type** | `city`, of type text |
| **Primary key** | A column whose value is unique for every row, so it identifies the row | `customers.id` |
| **Foreign key** | A column that stores another table's primary key, linking the two | `orders.customer_id` |
| **Schema** | The design: which tables, columns, types and rules exist (also a named group of tables in Postgres) | |
| **Query** | A question or command written in SQL | `SELECT name FROM customers;` |
| **DBMS** | The software that runs the database | PostgreSQL, MySQL, SQLite |

**SQL is declarative.** In Python you say **how** (loop, check, append). In SQL you say **what** ("names of customers from Pune"), and the database's **query planner** chooses the steps, such as which index to use or which table to read first (Section [19](#19-reading-query-plans-with-explain)).

**SQL's four families of commands:**

- **DQL** (query): `SELECT`
- **DML** (change data): `INSERT`, `UPDATE`, `DELETE`
- **DDL** (define structure): `CREATE`, `ALTER`, `DROP`
- **DCL / TCL** (permissions and transactions): `GRANT`, `REVOKE`, `BEGIN`, `COMMIT`, `ROLLBACK`

**SQL vs NoSQL.** Relational (SQL) databases store related tables with a fixed schema and strong guarantees. "NoSQL" databases trade some of that for other strengths: document stores (MongoDB) keep JSON-like documents, key-value stores (Redis, DynamoDB) are extremely fast lookups, wide-column stores (Cassandra) spread writes across many machines, and graph databases (Neo4j) follow relationships. In 2026 the boundary is blurry: PostgreSQL stores JSON documents (Section [21](#21-json-and-jsonb-documents-inside-postgresql)), vectors (Section [26](#26-pgvector-vector-search-for-ai-applications)) and full-text indexes too, so many teams start with Postgres and add a specialised store only when they must.

**Why PostgreSQL?** It's free and open source (no licence costs), extremely reliable, follows the SQL standard closely, and has powerful extras: JSONB, full-text search, geographic data (PostGIS), vector search (pgvector) and hundreds of extensions. Every major cloud offers it as a managed service.

**Used in real software:** Instagram and Reddit were built on PostgreSQL; Supabase, Neon and many "backend-as-a-service" platforms are built on it; and every major cloud sells it as a managed service (Amazon RDS and Aurora, Google Cloud SQL and AlloyDB, Azure Database for PostgreSQL).

### Practice

Answer in your own words:

1. What is the difference between a primary key and a foreign key?
2. Why is it useful that SQL is declarative?
3. Name one situation where a key-value store like Redis would be a better fit than PostgreSQL.

<details>
<summary><b>Answer</b></summary>

1. A primary key uniquely identifies a row in its own table; a foreign key is a column holding another table's primary key, to link a row to a row in that table.
2. You describe the result you want, and the database picks an efficient way to compute it, which can change as data grows (for example, starting to use an index) without you rewriting the query.
3. A cache of session data or rate-limit counters that need extremely fast reads and writes and can be rebuilt if lost.

</details>

---

## 3. Your First Table: CREATE TABLE, INSERT and SELECT

![CREATE TABLE defines the columns; INSERT adds rows; SELECT reads them](images/sql/02-create-insert-select.svg)

### Theory

> **In simple words:** three commands get you started. `CREATE TABLE` draws the empty table with its column headings, `INSERT` adds rows, and `SELECT` reads them back.

**CREATE TABLE** names the table and lists each column with its **type** (Section [4](#4-data-types-and-null) covers types fully):

```text
CREATE TABLE customers (
    id        int GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name      text NOT NULL,
    city      text,
    email     text,
    signed_up date
);
```

- `int GENERATED ALWAYS AS IDENTITY` asks PostgreSQL to **number the rows for you**: 1, 2, 3, … (Older tutorials use `serial`, which does the same; identity columns are the modern, standard way.)
- `PRIMARY KEY` means "this column identifies each row": unique and never empty.
- `NOT NULL` means "this column must always have a value". Columns without it may be **NULL**: unknown or missing.

**INSERT** adds rows. List the columns you're filling, then the values in the same order. One `INSERT` can add many rows, separated by commas. `id` is left out because the database generates it.

**SELECT** reads rows: `SELECT name, city FROM customers;` returns those two columns for every row, and `SELECT *` means "all columns".

**The small rules of SQL syntax:**

- End each statement with a **semicolon** `;`.
- **Keywords aren't case-sensitive** (`select` = `SELECT`). Writing keywords in capitals is a common convention that makes queries easier to read.
- **Text values use single quotes:** `'Pune'`. Double quotes are for **names** of tables and columns that contain spaces or capitals (`"Order Date"`), which it's best to avoid by using lowercase names with underscores: `order_date`.
- Comments start with `--` (to the end of the line) or are wrapped in `/* ... */`.
- Unquoted names are folded to lowercase, so `Customers` and `customers` are the same table.

**Deleting a whole table** is `DROP TABLE customers;`. It's permanent, so `DROP TABLE IF EXISTS` is used in setup scripts to start fresh without an error when the table isn't there.

### SQL

```sql
DROP TABLE IF EXISTS customers;

CREATE TABLE customers (
    id        int GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name      text NOT NULL,
    city      text,
    email     text,
    signed_up date
);

INSERT INTO customers (name, city, email, signed_up) VALUES
    ('Asha',  'Pune',      'asha@example.com',  '2024-01-15'),
    ('Ravi',  'Mumbai',    'ravi@example.com',  '2024-02-03'),
    ('Meera', 'Pune',      'meera@example.com', '2024-03-22'),
    ('Arjun', 'Delhi',     NULL,                '2024-03-30'),
    ('Zoya',  'Mumbai',    'zoya@example.com',  '2024-06-11'),
    ('Kabir', 'Bengaluru', 'kabir@example.com', '2025-01-08'),
    ('Isha',  'Delhi',     'isha@example.com',  '2025-02-14'),
    ('Dev',   'Pune',      NULL,                '2025-05-01');

SELECT * FROM customers;
```

**Output:**

```text
 id | name  |   city    |       email       | signed_up
----+-------+-----------+-------------------+------------
  1 | Asha  | Pune      | asha@example.com  | 2024-01-15
  2 | Ravi  | Mumbai    | ravi@example.com  | 2024-02-03
  3 | Meera | Pune      | meera@example.com | 2024-03-22
  4 | Arjun | Delhi     | (null)            | 2024-03-30
  5 | Zoya  | Mumbai    | zoya@example.com  | 2024-06-11
  6 | Kabir | Bengaluru | kabir@example.com | 2025-01-08
  7 | Isha  | Delhi     | isha@example.com  | 2025-02-14
  8 | Dev   | Pune      | (null)            | 2025-05-01
(8 rows)
```

```sql
SELECT name, city FROM customers;   -- only two columns
```

**Output:**

```text
 name  |   city
-------+-----------
 Asha  | Pune
 Ravi  | Mumbai
 Meera | Pune
 Arjun | Delhi
 Zoya  | Mumbai
 Kabir | Bengaluru
 Isha  | Delhi
 Dev   | Pune
(8 rows)
```

Now a second table, used throughout the rest of these notes. `numeric(10, 2)` stores exact money amounts with 2 decimal places:

```sql
DROP TABLE IF EXISTS products;

CREATE TABLE products (
    id       int GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name     text NOT NULL,
    category text NOT NULL,
    price    numeric(10, 2) NOT NULL,
    stock    int NOT NULL DEFAULT 0
);

INSERT INTO products (name, category, price, stock) VALUES
    ('Notebook',     'stationery',  60.00,   120),
    ('Pen',          'stationery',  15.50,   500),
    ('Backpack',     'bags',        1200.00, 25),
    ('Water bottle', 'kitchen',     350.00,  60),
    ('Headphones',   'electronics', 2500.00, 15),
    ('Keyboard',     'electronics', 1800.00, 0),
    ('Mug',          'kitchen',     250.00,  80),
    ('Desk lamp',    'electronics', 900.00,  30),
    ('Stapler',      'stationery',  120.00,  40);

SELECT id, name, price FROM products;
```

**Output:**

```text
 id |     name     |  price
----+--------------+---------
  1 | Notebook     |   60.00
  2 | Pen          |   15.50
  3 | Backpack     | 1200.00
  4 | Water bottle |  350.00
  5 | Headphones   | 2500.00
  6 | Keyboard     | 1800.00
  7 | Mug          |  250.00
  8 | Desk lamp    |  900.00
  9 | Stapler      |  120.00
(9 rows)
```

**Common mistakes:**

- ❌ Double quotes around text values: `WHERE city = "Pune"` looks for a **column** called Pune. ✅ `'Pune'`.
- ❌ Forgetting the semicolon in `psql`, which then waits for more input (the prompt changes from `=#` to `-#`).
- ❌ Listing values in a different order from the columns in `INSERT`.

### Practice

1. Create a table `books` with an identity `id`, a required `title`, an `author` and a `year` (int).
2. Insert three books in one statement, one of them without an author.
3. Select only the titles.

<details>
<summary><b>Answer</b></summary>

```sql
CREATE TABLE books (
    id     int GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    title  text NOT NULL,
    author text,
    year   int
);

INSERT INTO books (title, author, year) VALUES
    ('Clean Code', 'Robert C. Martin', 2008),
    ('Designing Data-Intensive Applications', 'Martin Kleppmann', 2017),
    ('Anonymous Notes', NULL, 2024);

SELECT title FROM books;
DROP TABLE books;
```

**Output:**

```text
                 title
---------------------------------------
 Clean Code
 Designing Data-Intensive Applications
 Anonymous Notes
(3 rows)
```

</details>

---

## 4. Data Types and NULL

![Choosing a column type](images/sql/03-data-types.svg)

### Theory

> **In simple words:** every column has a **type** that says what kind of value it holds: whole numbers, money, text, dates, true/false. The type protects your data (you can't put "hello" in a price column) and lets the database store and compare values efficiently.

**The types you'll use 95% of the time:**

| Kind | Type | Use for | Notes |
|---|---|---|---|
| Whole numbers | `int` (±2.1 billion), `bigint` (±9.2 × 10¹⁸), `smallint` | Counts, quantities, IDs | Use `bigint` for IDs of tables that may grow huge |
| Exact decimals | `numeric(p, s)` | **Money**, anything that must add up exactly | `numeric(10, 2)`: up to 10 digits, 2 after the point |
| Approximate decimals | `real`, `double precision` | Measurements, science, ML features | Fast, but `0.1 + 0.2` isn't exactly `0.3` |
| Text | `text`, `varchar(n)` | Names, descriptions | In PostgreSQL `text` is just as fast as `varchar`; use `varchar(n)` only to enforce a maximum length |
| True/false | `boolean` | Flags like `is_active` | Values `true`, `false` (or NULL) |
| Date | `date` | Birthdays, order dates | `'2025-03-14'` (ISO format: year-month-day) |
| Date + time | `timestamptz` | **Any moment in time** (created_at, paid_at) | Stored in UTC, shown in your session's time zone |
| Duration | `interval` | "3 days", "2 hours 30 minutes" | `now() - interval '7 days'` |
| Unique IDs | `uuid` | Public IDs that can't be guessed or counted | `gen_random_uuid()`; PostgreSQL 18 adds time-ordered `uuidv7()` |
| Documents | `jsonb` | Flexible, nested data | Section [21](#21-json-and-jsonb-documents-inside-postgresql) |
| Lists | `int[]`, `text[]` | Tags, small lists | Section [22](#22-arrays-enums-ranges-and-generated-columns) |

**Two rules that prevent real bugs:**

1. **Money → `numeric`, never `real`/`double precision`.** Floating-point numbers store binary fractions, so 0.1 can't be stored exactly and tiny errors pile up in totals.
2. **Moments in time → `timestamptz`, not `timestamp`.** `timestamp` (without time zone) doesn't know **which** 10:00 it means. `timestamptz` stores an exact instant (internally in UTC) and converts it to each user's time zone when displayed.

**Casting** converts between types: `'42'::int` (PostgreSQL style) or `CAST('42' AS int)` (standard SQL). `pg_typeof(x)` tells you a value's type.

**NULL means "unknown" or "missing"**, and it behaves unlike any other value:

- `NULL = NULL` is not true; it's **NULL** ("unknown equals unknown?" is unknown). So never write `= NULL`; use **`IS NULL`** and **`IS NOT NULL`**.
- Most operations with NULL give NULL: `5 + NULL` is NULL.
- SQL uses **three-valued logic**: true, false and unknown. `WHERE` keeps only rows where the condition is **true**, so rows where it's unknown are silently dropped (a classic source of "missing rows").
- `COALESCE(a, b)` returns the first value that isn't NULL: `COALESCE(email, 'no email')`.
- `IS DISTINCT FROM` compares values treating NULLs as equal to each other: handy when either side may be NULL.

### SQL

```sql
SELECT 0.1::double precision + 0.2 AS float_sum,
       0.1::numeric + 0.2          AS exact_sum,
       '42'::int + 1               AS casted,
       pg_typeof(15.50)            AS type_of_literal;
```

**Output:**

```text
      float_sum      | exact_sum | casted | type_of_literal
---------------------+-----------+--------+-----------------
 0.30000000000000004 |       0.3 |     43 | numeric
(1 row)
```

```sql
SELECT NULL = NULL          AS equals_null,
       NULL IS NULL         AS is_null,
       5 + NULL             AS plus_null,
       COALESCE(NULL, 'fallback') AS coalesced,
       NULL IS DISTINCT FROM NULL AS distinct_nulls;
```

**Output:**

```text
 equals_null | is_null | plus_null | coalesced | distinct_nulls
-------------+---------+-----------+-----------+----------------
 (null)      | t       |    (null) | fallback  | f
(1 row)
```

```sql
-- the silent-drop trap: Arjun and Dev have no email
SELECT count(*) FROM customers WHERE email <> 'asha@example.com';
SELECT count(*) FROM customers WHERE email IS DISTINCT FROM 'asha@example.com';
```

**Output:**

```text
 count
-------
     5
(1 row)

 count
-------
     7
(1 row)
```

The first count is 5, not 7: for Arjun and Dev, `NULL <> 'asha@…'` is unknown, so `WHERE` drops them.

```sql
SELECT timestamptz '2025-03-14 10:00:00+05:30' AS stored_instant,
       (timestamptz '2025-03-14 10:00:00+05:30') AT TIME ZONE 'America/New_York' AS new_york_clock,
       date '2025-03-14' + 30 AS thirty_days_later,
       date '2025-12-25' - date '2025-03-14' AS days_between,
       interval '1 day 2 hours' * 3 AS tripled;
```

**Output:**

```text
     stored_instant     |   new_york_clock    | thirty_days_later | days_between |     tripled
------------------------+---------------------+-------------------+--------------+-----------------
 2025-03-14 04:30:00+00 | 2025-03-14 00:30:00 | 2025-04-13        |          286 | 3 days 06:00:00
(1 row)
```

The session time zone here is UTC, so the stored instant is shown as 04:30 UTC: the same moment as 10:00 in India (+05:30).

**Common mistakes:**

- ❌ `WHERE email = NULL` (always returns nothing). ✅ `WHERE email IS NULL`.
- ❌ Storing prices as `real` or `double precision`.
- ❌ Storing dates as text (`'14/03/2025'`), which breaks sorting, comparisons and date maths.
- ❌ `timestamp` without time zone for events that happen in real time.

### Practice

1. What does `SELECT NULL AND false, NULL OR true;` return, and why?
2. Pick types for: a phone number, a product's weight in kg, a user's date of birth, the moment a payment succeeded, a bank balance.

<details>
<summary><b>Answer</b></summary>

```sql
SELECT NULL AND false AS and_result, NULL OR true AS or_result;
```

**Output:**

```text
 and_result | or_result
------------+-----------
 f          | t
(1 row)
```

`false` whatever the unknown value is, and `true` whatever it is, so the result doesn't depend on the NULL. Types: phone number → `text` (it isn't a number you do maths on, and may start with + or 0); weight → `numeric(8, 3)` or `double precision`; date of birth → `date`; payment moment → `timestamptz`; bank balance → `numeric(14, 2)`.

</details>

---

## 5. SELECT in Depth: Filtering, Sorting and Limiting

![A query reads the table, filters rows with WHERE, sorts with ORDER BY and keeps the first rows with LIMIT](images/sql/04-select-pipeline.svg)

### Theory

> **In simple words:** `SELECT` answers questions. Pick the **columns** you want, say **which rows** (`WHERE`), what **order** (`ORDER BY`) and **how many** (`LIMIT`).

**The shape of a basic query:**

```text
SELECT   columns or expressions      -- what to show
FROM     table                       -- where the rows come from
WHERE    condition                   -- which rows to keep
ORDER BY column [ASC | DESC]         -- how to sort them
LIMIT    n OFFSET m;                 -- how many to return
```

**Filtering with WHERE:**

| Operator | Meaning | Example |
|---|---|---|
| `=`, `<>` (or `!=`), `<`, `>`, `<=`, `>=` | Compare | `price > 1000` |
| `AND`, `OR`, `NOT` | Combine conditions (`AND` is evaluated before `OR`; use brackets) | `city = 'Pune' AND signed_up >= '2025-01-01'` |
| `IN (...)` | Equals any value in a list | `city IN ('Pune', 'Delhi')` |
| `BETWEEN a AND b` | In a range, **both ends included** | `price BETWEEN 100 AND 1000` |
| `LIKE` / `ILIKE` | Text pattern: `%` = any characters, `_` = one character; `ILIKE` ignores case | `name LIKE 'A%'` |
| `IS NULL` / `IS NOT NULL` | Missing or present | `email IS NULL` |

**Sorting with ORDER BY:** `ASC` (smallest first, the default) or `DESC`. Sort by several columns to break ties: `ORDER BY city, name`. NULLs sort **last** in ascending order in PostgreSQL (`NULLS FIRST` / `NULLS LAST` changes that). **Without `ORDER BY`, the order of rows is not guaranteed**, even if it looks stable today.

**Limiting:** `LIMIT 3` returns at most 3 rows; `OFFSET 3` skips the first 3 (used for simple pagination; Section [20](#20-making-queries-fast-common-performance-patterns) explains why big offsets get slow).

**Other everyday tools:**

- **Expressions and aliases:** `SELECT name, price * 1.18 AS price_with_gst` computes a new column and names it with `AS`.
- **DISTINCT** removes duplicate rows from the result: `SELECT DISTINCT city FROM customers`.
- `FETCH FIRST 3 ROWS ONLY` is the standard-SQL spelling of `LIMIT 3`.

**The order SQL runs in is not the order you write it:** `FROM` → `WHERE` → `SELECT` → `DISTINCT` → `ORDER BY` → `LIMIT`. That's why an alias created in `SELECT` can be used in `ORDER BY` but **not** in `WHERE` (the filter runs before the alias exists). Section [8](#8-aggregation-count-sum-group-by-and-having) adds `GROUP BY` and `HAVING` to this list.

### SQL

```sql
SELECT name, city, signed_up
FROM customers
WHERE city IN ('Pune', 'Delhi') AND signed_up >= '2025-01-01'
ORDER BY signed_up;
```

**Output:**

```text
 name | city  | signed_up
------+-------+------------
 Isha | Delhi | 2025-02-14
 Dev  | Pune  | 2025-05-01
(2 rows)
```

```sql
SELECT name, price, round(price * 1.18, 2) AS price_with_gst
FROM products
WHERE price BETWEEN 200 AND 2000
ORDER BY price DESC
LIMIT 3;
```

**Output:**

```text
   name    |  price  | price_with_gst
-----------+---------+----------------
 Keyboard  | 1800.00 |        2124.00
 Backpack  | 1200.00 |        1416.00
 Desk lamp |  900.00 |        1062.00
(3 rows)
```

```sql
SELECT name FROM customers WHERE name ILIKE '%a' ORDER BY name;   -- ends with a or A
SELECT DISTINCT city FROM customers ORDER BY city;
SELECT name, email FROM customers WHERE email IS NULL;
```

**Output:**

```text
 name
-------
 Asha
 Isha
 Meera
 Zoya
(4 rows)

   city
-----------
 Bengaluru
 Delhi
 Mumbai
 Pune
(4 rows)

 name  | email
-------+--------
 Arjun | (null)
 Dev   | (null)
(2 rows)
```

```sql
-- AND binds tighter than OR: these two queries are different
SELECT name, category, price FROM products
WHERE category = 'kitchen' OR category = 'bags' AND price > 1000 ORDER BY name;

SELECT name, category, price FROM products
WHERE (category = 'kitchen' OR category = 'bags') AND price > 1000 ORDER BY name;
```

**Output:**

```text
     name     | category |  price
--------------+----------+---------
 Backpack     | bags     | 1200.00
 Mug          | kitchen  |  250.00
 Water bottle | kitchen  |  350.00
(3 rows)

   name   | category |  price
----------+----------+---------
 Backpack | bags     | 1200.00
(1 row)
```

The first query reads as "kitchen items, or bags over 1000", which is why the cheap kitchen items appear.

**Common mistakes:**

- ❌ Mixing `AND` and `OR` without brackets.
- ❌ Relying on row order without `ORDER BY`.
- ❌ `BETWEEN '2025-01-01' AND '2025-01-31'` on a **timestamp** column: it stops at midnight at the **start** of the 31st. ✅ Use `>= '2025-01-01' AND < '2025-02-01'`.
- ❌ Using a `SELECT` alias inside `WHERE`.

### Practice

On the `products` table:

1. Products in the `electronics` category that are in stock, cheapest first.
2. The two most expensive products.
3. Products whose name contains the letter `o` (any case).

<details>
<summary><b>Answer</b></summary>

```sql
SELECT name, price FROM products WHERE category = 'electronics' AND stock > 0 ORDER BY price;
SELECT name, price FROM products ORDER BY price DESC LIMIT 2;
SELECT name FROM products WHERE name ILIKE '%o%' ORDER BY name;
```

**Output:**

```text
    name    |  price
------------+---------
 Desk lamp  |  900.00
 Headphones | 2500.00
(2 rows)

    name    |  price
------------+---------
 Headphones | 2500.00
 Keyboard   | 1800.00
(2 rows)

     name
--------------
 Headphones
 Keyboard
 Notebook
 Water bottle
(4 rows)
```

</details>

| # | Practice problem | Level |
|---|---|---|
| 1 | [LeetCode 1757. Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/) | 🟢 Easy |
| 2 | [LeetCode 584. Find Customer Referee](https://leetcode.com/problems/find-customer-referee/) (the NULL trap) | 🟢 Easy |
| 3 | [LeetCode 595. Big Countries](https://leetcode.com/problems/big-countries/) | 🟢 Easy |
| 4 | [PostgreSQL Exercises: Basic](https://pgexercises.com/questions/basic/) | 🟢 Easy |

**Learn more:** [PostgreSQL docs: Queries](https://www.postgresql.org/docs/current/queries.html) · [SQLBolt (interactive lessons)](https://sqlbolt.com/)

---

## 6. Changing Data: UPDATE, DELETE and RETURNING

![UPDATE changes matching rows; DELETE removes them; without WHERE, every row is affected](images/sql/05-update-delete.svg)

### Theory

> **In simple words:** `UPDATE` changes values in rows that match a condition, and `DELETE` removes rows that match. The `WHERE` clause decides **which** rows. Forget it, and the change hits **every** row.

**UPDATE:**

```text
UPDATE products
SET    price = price * 0.9, stock = stock + 10     -- one or more columns
WHERE  category = 'kitchen';                       -- which rows
```

**DELETE:**

```text
DELETE FROM customers WHERE id = 8;
```

**RETURNING** (a PostgreSQL feature that SQLite and MariaDB also support) makes `INSERT`, `UPDATE` and `DELETE` return the affected rows, so you see exactly what changed, or get the new `id` of an inserted row without a second query.

**TRUNCATE** empties a whole table instantly (much faster than `DELETE` without `WHERE` on big tables), and `TRUNCATE ... RESTART IDENTITY` also resets the ID counter.

**Working safely (habits that save careers):**

1. **Write the `WHERE` first, as a `SELECT`.** Run `SELECT * FROM products WHERE category = 'kitchen'`, check the rows, then turn it into the `UPDATE`.
2. **Use a transaction** for anything risky: `BEGIN;` … check with `RETURNING` or a `SELECT` … then `COMMIT;` to keep it or `ROLLBACK;` to undo everything (Section [17](#17-transactions-acid-and-concurrency)).
3. Many teams prefer **soft deletes**: an `archived_at timestamptz` column set instead of deleting, so data can be restored and audited.

### SQL

```sql
UPDATE products
SET price = price * 0.9
WHERE category = 'kitchen'
RETURNING id, name, price;
```

**Output:**

```text
 id |     name     | price
----+--------------+--------
  4 | Water bottle | 315.00
  7 | Mug          | 225.00
(2 rows)
```

```sql
BEGIN;
DELETE FROM customers RETURNING name;        -- oops: no WHERE!
SELECT count(*) AS left_after_mistake FROM customers;
ROLLBACK;                                   -- undo everything since BEGIN
SELECT count(*) AS back_again FROM customers;
```

**Output:**

```text
 name
-------
 Asha
 Ravi
 Meera
 Arjun
 Zoya
 Kabir
 Isha
 Dev
(8 rows)

 left_after_mistake
--------------------
                  0
(1 row)

 back_again
------------
          8
(1 row)
```

```sql
INSERT INTO products (name, category, price, stock)
VALUES ('Sticky notes', 'stationery', 45.00, 200)
RETURNING id, name;
```

**Output:**

```text
 id |     name
----+--------------
 10 | Sticky notes
(1 row)
```

```sql
UPDATE products SET price = price / 0.9 WHERE category = 'kitchen';   -- restore the prices
DELETE FROM products WHERE name = 'Sticky notes';
SELECT name, price FROM products WHERE category = 'kitchen' ORDER BY name;
```

**Output:**

```text
     name     | price
--------------+--------
 Mug          | 250.00
 Water bottle | 350.00
(2 rows)
```

**Common mistakes:**

- ❌ `UPDATE`/`DELETE` without `WHERE` (it happens to experienced engineers too: use transactions and `RETURNING`).
- ❌ Updating a `numeric` price with a float calculation that doesn't round: store money with fixed decimals, and round deliberately (`round(x, 2)`).
- ❌ Deleting rows that other tables still point to. Foreign keys (Section [12](#12-keys-and-constraints-letting-the-database-protect-your-data)) stop you, or cascade, depending on how they're defined.

### Practice

1. Increase the stock of every `stationery` product by 50 and return the new stock values.
2. In a transaction, delete all customers from Mumbai, check the count, then roll back.

<details>
<summary><b>Answer</b></summary>

```sql
UPDATE products SET stock = stock + 50 WHERE category = 'stationery' RETURNING name, stock;
UPDATE products SET stock = stock - 50 WHERE category = 'stationery';   -- put it back

BEGIN;
DELETE FROM customers WHERE city = 'Mumbai';
SELECT count(*) FROM customers;
ROLLBACK;
```

**Output:**

```text
   name   | stock
----------+-------
 Notebook |   170
 Pen      |   550
 Stapler  |    90
(3 rows)

 count
-------
     6
(1 row)
```

</details>

---

### ✅ Part 1 checkpoint

Without looking, can you:

- [ ] Explain tables, rows, columns, primary keys and foreign keys?
- [ ] Create a table with sensible types, and insert several rows in one statement?
- [ ] Filter with `WHERE` using `IN`, `BETWEEN`, `ILIKE` and `IS NULL`, and explain why `= NULL` fails?
- [ ] Sort, limit and remove duplicates?
- [ ] Update and delete rows safely inside a transaction, using `RETURNING`?

---

# Part 2 — Easy: Asking Bigger Questions

> **Goal:** Transform values with functions, summarise with GROUP BY, combine tables with joins, and build queries in steps with subqueries and CTEs.  
> **You need:** Part 1.

---

## 7. Functions and Expressions: Text, Numbers, Dates and CASE

### Theory

> **In simple words:** functions transform values inside a query: tidy text, round numbers, pull the month out of a date, or turn values into labels with `CASE`. They work row by row, so each row gets its own result.

**Text functions:**

| Function | Example | Result |
|---|---|---|
| `upper(s)`, `lower(s)`, `initcap(s)` | `upper('pune')` | `PUNE` |
| `length(s)` | `length('Asha')` | 4 |
| `s1 \|\| s2`, `concat(...)`, `concat_ws(sep, ...)` | `'Hi ' \|\| name` | `Hi Asha` (`\|\|` gives NULL if any part is NULL; `concat` skips NULLs) |
| `substring(s from i for n)`, `left(s, n)`, `right(s, n)` | `left('Notebook', 4)` | `Note` |
| `replace(s, from, to)` | `replace('a-b', '-', '+')` | `a+b` |
| `split_part(s, sep, n)` | `split_part('asha@example.com', '@', 2)` | `example.com` |
| `trim(s)`, `ltrim`, `rtrim` | `trim('  hi ')` | `hi` |
| `position(sub in s)` | `position('@' in email)` | index of the first `@` (1-based) |

**Number functions:** `round(x, 2)`, `ceil(x)`, `floor(x)`, `abs(x)`, `x % y` (remainder), `power(x, y)`, `greatest(a, b, …)`, `least(a, b, …)`. Watch out for **integer division**: `7 / 2` is `3` when both are integers; write `7 / 2.0` or cast (`7::numeric / 2`).

**Date and time functions:**

| Function | Gives |
|---|---|
| `now()`, `current_date` | The current timestamp / date |
| `extract(year from d)`, `date_part('month', d)` | A part of a date as a number |
| `date_trunc('month', ts)` | The timestamp rounded **down** to the start of the month (perfect for grouping by month) |
| `age(d2, d1)` | The interval between two dates, in years/months/days |
| `to_char(ts, 'DD Mon YYYY')` | Formatted text |
| `d + interval '7 days'` | Date arithmetic |

**CASE: if/else inside SQL.**

```text
CASE
    WHEN price >= 2000 THEN 'premium'
    WHEN price >= 500  THEN 'mid'
    ELSE 'budget'
END
```

The first true `WHEN` wins; without `ELSE`, unmatched rows get NULL.

**Handling NULLs and zeros:** `COALESCE(x, default)` replaces NULL; `NULLIF(a, b)` returns NULL when a = b, which is the standard trick to avoid division by zero: `total / NULLIF(count, 0)` gives NULL instead of an error.

### SQL

```sql
SELECT name,
       upper(city) AS city_upper,
       coalesce(split_part(email, '@', 2), 'no email') AS email_domain,
       extract(year from signed_up) AS year_joined,
       to_char(signed_up, 'DD Mon YYYY') AS joined_on
FROM customers
ORDER BY id
LIMIT 4;
```

**Output:**

```text
 name  | city_upper | email_domain | year_joined |  joined_on
-------+------------+--------------+-------------+-------------
 Asha  | PUNE       | example.com  |        2024 | 15 Jan 2024
 Ravi  | MUMBAI     | example.com  |        2024 | 03 Feb 2024
 Meera | PUNE       | example.com  |        2024 | 22 Mar 2024
 Arjun | DELHI      | no email     |        2024 | 30 Mar 2024
(4 rows)
```

```sql
SELECT name, price,
       CASE
           WHEN price >= 2000 THEN 'premium'
           WHEN price >= 500  THEN 'mid'
           ELSE 'budget'
       END AS tier,
       CASE WHEN stock = 0 THEN 'sold out' ELSE stock || ' left' END AS availability
FROM products
ORDER BY price DESC;
```

**Output:**

```text
     name     |  price  |  tier   | availability
--------------+---------+---------+--------------
 Headphones   | 2500.00 | premium | 15 left
 Keyboard     | 1800.00 | mid     | sold out
 Backpack     | 1200.00 | mid     | 25 left
 Desk lamp    |  900.00 | mid     | 30 left
 Water bottle |  350.00 | budget  | 60 left
 Mug          |  250.00 | budget  | 80 left
 Stapler      |  120.00 | budget  | 40 left
 Notebook     |   60.00 | budget  | 120 left
 Pen          |   15.50 | budget  | 500 left
(9 rows)
```

```sql
SELECT 7 / 2 AS int_division, 7 / 2.0 AS real_division, 7 % 2 AS remainder,
       round(2 / 3.0, 3) AS rounded,
       10 / NULLIF(0, 0) AS safe_divide,
       date_trunc('month', timestamptz '2025-03-14 10:30+00') AS month_start,
       age(date '2025-03-14', date '2000-08-01') AS age_then;
```

**Output:**

```text
 int_division |   real_division    | remainder | rounded | safe_divide |      month_start       |        age_then
--------------+--------------------+-----------+---------+-------------+------------------------+-------------------------
            3 | 3.5000000000000000 |         1 |   0.667 |      (null) | 2025-03-01 00:00:00+00 | 24 years 7 mons 13 days
(1 row)
```

**Common mistakes:**

- ❌ Integer division giving 0 for percentages: `completed / total * 100`. ✅ `completed * 100.0 / total`.
- ❌ `'Hi ' || NULL` becomes NULL. Use `concat` or `coalesce`.
- ❌ Applying functions to a column in `WHERE` (`WHERE extract(year from signed_up) = 2025`) can stop an index from being used. ✅ Compare ranges: `signed_up >= '2025-01-01' AND signed_up < '2026-01-01'` (Section [20](#20-making-queries-fast-common-performance-patterns)).

### Practice

1. Show each product's name in capitals and its price rounded up to the next hundred.
2. Label each customer as `new` if they signed up in 2025, otherwise `existing`.

<details>
<summary><b>Answer</b></summary>

```sql
SELECT upper(name) AS name, ceil(price / 100) * 100 AS rounded_up
FROM products ORDER BY id LIMIT 3;

SELECT name, CASE WHEN signed_up >= '2025-01-01' THEN 'new' ELSE 'existing' END AS kind
FROM customers ORDER BY id;
```

**Output:**

```text
   name   | rounded_up
----------+------------
 NOTEBOOK |        100
 PEN      |        100
 BACKPACK |       1200
(3 rows)

 name  |   kind
-------+----------
 Asha  | existing
 Ravi  | existing
 Meera | existing
 Arjun | existing
 Zoya  | existing
 Kabir | new
 Isha  | new
 Dev   | new
(8 rows)
```

</details>

| # | Practice problem | Level |
|---|---|---|
| 1 | [LeetCode 1667. Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table/) | 🟢 Easy |
| 2 | [LeetCode 1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/) | 🟢 Easy |
| 3 | [LeetCode 1873. Calculate Special Bonus](https://leetcode.com/problems/calculate-special-bonus/) | 🟢 Easy |
| 4 | [LeetCode 1517. Find Users With Valid E-Mails](https://leetcode.com/problems/find-users-with-valid-e-mails/) (regular expressions) | 🟢 Easy |

**Learn more:** [PostgreSQL docs: Functions and Operators](https://www.postgresql.org/docs/current/functions.html)

---

## 8. Aggregation: COUNT, SUM, GROUP BY and HAVING

![GROUP BY splits rows into groups, then an aggregate turns each group into one row](images/sql/06-group-by.svg)

### Theory

> **In simple words:** aggregate functions **squash many rows into one number**: how many, the total, the average. `GROUP BY` first splits the rows into groups (per city, per category), so you get one number **per group**.

**Aggregate functions:**

| Function | Gives | NULLs |
|---|---|---|
| `count(*)` | Number of rows | Counts every row |
| `count(col)` | Number of rows where `col` isn't NULL | Skipped |
| `count(DISTINCT col)` | Number of different values | Skipped |
| `sum(col)`, `avg(col)` | Total, average | Skipped (avg of 10, NULL, 20 is 15) |
| `min(col)`, `max(col)` | Smallest, largest | Skipped |
| `string_agg(col, ', ')`, `array_agg(col)` | All values joined into one text / array | |
| `bool_and`, `bool_or` | Are all / any true? | |

**GROUP BY** makes one output row per distinct value (or combination of values) of the grouping columns. **Rule:** every column in `SELECT` must either be in `GROUP BY` or be inside an aggregate. (What would "the city" of a group of many customers be otherwise?)

**WHERE vs HAVING:**

- `WHERE` filters **rows before** grouping ("only delivered orders").
- `HAVING` filters **groups after** aggregating ("only cities with at least 2 customers"). It's the only place you can filter on an aggregate like `count(*) >= 2`.

**FILTER** computes several conditional aggregates in one pass: `count(*) FILTER (WHERE stock = 0)`.

**The full logical order of a query** (the order the database conceptually runs the clauses):

1. `FROM` (and joins) → 2. `WHERE` → 3. `GROUP BY` → 4. `HAVING` → 5. `SELECT` → 6. `DISTINCT` → 7. `ORDER BY` → 8. `LIMIT`.

**ROLLUP** adds subtotal and grand-total rows: `GROUP BY ROLLUP (category)` adds a final row where `category` is NULL, holding the total over all categories.

### SQL

```sql
SELECT count(*) AS customers, count(email) AS with_email,
       count(DISTINCT city) AS cities, min(signed_up) AS first_signup
FROM customers;
```

**Output:**

```text
 customers | with_email | cities | first_signup
-----------+------------+--------+--------------
         8 |          6 |      4 | 2024-01-15
(1 row)
```

```sql
SELECT city, count(*) AS customers, string_agg(name, ', ' ORDER BY name) AS names
FROM customers
GROUP BY city
ORDER BY customers DESC, city;
```

**Output:**

```text
   city    | customers |      names
-----------+-----------+------------------
 Pune      |         3 | Asha, Dev, Meera
 Delhi     |         2 | Arjun, Isha
 Mumbai    |         2 | Ravi, Zoya
 Bengaluru |         1 | Kabir
(4 rows)
```

```sql
SELECT category,
       count(*)                           AS products,
       round(avg(price), 2)               AS avg_price,
       sum(price * stock)                 AS stock_value,
       count(*) FILTER (WHERE stock = 0)  AS sold_out
FROM products
GROUP BY category
HAVING count(*) >= 2                      -- only categories with 2+ products
ORDER BY stock_value DESC;
```

**Output:**

```text
  category   | products | avg_price | stock_value | sold_out
-------------+----------+-----------+-------------+----------
 electronics |        3 |   1733.33 |    64500.00 |        1
 kitchen     |        2 |    300.00 |    41000.00 |        0
 stationery  |        3 |     65.17 |    19750.00 |        0
(3 rows)
```

```sql
SELECT coalesce(category, 'ALL') AS category, sum(stock) AS units
FROM products
GROUP BY ROLLUP (category)
ORDER BY category = 'ALL', category;     -- false sorts before true, so the total goes last
```

**Output:**

```text
  category   | units
-------------+-------
 bags        |    25
 electronics |    45
 kitchen     |   140
 stationery  |   660
 ALL         |   870
(5 rows)
```

(`category` is NULL on the rollup row, and `coalesce` labels it `ALL`.)

**Common mistakes:**

- ❌ Selecting a column that isn't grouped: `SELECT city, name, count(*) ... GROUP BY city` fails ("must appear in the GROUP BY clause").
- ❌ Filtering an aggregate in `WHERE` (`WHERE count(*) > 1`). ✅ Use `HAVING`.
- ❌ `count(col)` when you meant `count(*)`: it silently skips NULLs.
- ❌ `avg` on integers expecting a whole number: PostgreSQL returns `numeric`; round it for display.

### Practice

1. How many customers signed up in each year?
2. Which categories have an average price above 1,000?

<details>
<summary><b>Answer</b></summary>

```sql
SELECT extract(year from signed_up) AS year, count(*) AS signups
FROM customers GROUP BY year ORDER BY year;

SELECT category, round(avg(price), 2) AS avg_price
FROM products GROUP BY category HAVING avg(price) > 1000 ORDER BY category;
```

**Output:**

```text
 year | signups
------+---------
 2024 |       5
 2025 |       3
(2 rows)

  category   | avg_price
-------------+-----------
 bags        |   1200.00
 electronics |   1733.33
(2 rows)
```

(PostgreSQL allows `GROUP BY year`, the alias, as a convenience; standard SQL would repeat the expression.)

</details>

| # | Practice problem | Level |
|---|---|---|
| 1 | [LeetCode 2356. Number of Unique Subjects Taught by Each Teacher](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/) | 🟢 Easy |
| 2 | [LeetCode 596. Classes More Than 5 Students](https://leetcode.com/problems/classes-more-than-5-students/) | 🟢 Easy |
| 3 | [LeetCode 1729. Find Followers Count](https://leetcode.com/problems/find-followers-count/) | 🟢 Easy |
| 4 | [LeetCode 1193. Monthly Transactions I](https://leetcode.com/problems/monthly-transactions-i/) | 🟡 Medium |
| 5 | [PostgreSQL Exercises: Aggregation](https://pgexercises.com/questions/aggregates/) | 🟡 Medium |

---

## 9. Joins: Combining Tables

![INNER, LEFT, RIGHT and FULL joins: which rows each one keeps](images/sql/07-joins.svg)

### Theory

> **In simple words:** a join **matches rows from two tables** using a shared value (usually an ID), and glues each matching pair into one wider row. It's how you answer questions that need data from several tables, like "which customer placed each order?".

Data is split across tables on purpose (Section [13](#13-designing-tables-relationships-and-normalisation) explains why): an order row stores only `customer_id`, not the customer's name and city. A join brings them back together at query time.

**Let's add orders.** Each order belongs to a customer (`customer_id` **references** `customers.id`: a foreign key, covered fully in Section [12](#12-keys-and-constraints-letting-the-database-protect-your-data)), and each order has several **items** (products with quantities).

**The join types:**

| Join | Keeps | Use it for |
|---|---|---|
| `INNER JOIN` (or just `JOIN`) | Only rows that have a match on **both** sides | "Orders with their customer" |
| `LEFT JOIN` | **Every** row of the left table; right-side columns are NULL when there's no match | "All customers, with their orders if any" |
| `RIGHT JOIN` | Every row of the right table (a LEFT JOIN written backwards; rarely used) | |
| `FULL JOIN` | Every row from both sides, matched where possible | Comparing two lists |
| `CROSS JOIN` | Every combination (rows × rows) | Generating combinations: sizes × colours |
| Self join | A table joined to itself, with two aliases | "Each employee with their manager" |

**How to write one:**

```text
SELECT o.id, c.name
FROM orders AS o
JOIN customers AS c ON c.id = o.customer_id;
```

- **Aliases** (`o`, `c`) keep queries short, and are required when two columns share a name (both tables have `id`).
- `ON` gives the matching rule. `USING (col)` is a shortcut when both columns have the same name.
- Joins chain: `orders → order_items → products` answers "what was in each order?".

**Two patterns you'll use constantly:**

- **Anti-join ("rows with no match"):** `LEFT JOIN ... WHERE right.id IS NULL`, or `WHERE NOT EXISTS (...)` (Section [10](#10-subqueries-and-ctes-with-including-recursive-queries)). "Customers who never ordered."
- **Many-to-many through a junction table:** `orders` ↔ `products` are linked by `order_items`.

**The join trap: row multiplication.** A join returns one row **per matching pair**. Joining customers to orders gives a customer's row once **per order**, so summing a customer-level column after the join counts it several times. Aggregate at the right level (or aggregate first in a subquery, then join).

**Where you filter a LEFT JOIN matters.** A condition on the right table in `WHERE` removes the NULL rows and silently turns it into an INNER JOIN. Put such conditions in `ON` instead.

### SQL

```sql
DROP TABLE IF EXISTS order_items, orders;

CREATE TABLE orders (
    id          int GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    customer_id int NOT NULL REFERENCES customers (id),
    ordered_at  date NOT NULL,
    status      text NOT NULL
);

CREATE TABLE order_items (
    order_id   int REFERENCES orders (id),
    product_id int REFERENCES products (id),
    quantity   int NOT NULL,
    unit_price numeric(10, 2) NOT NULL,
    PRIMARY KEY (order_id, product_id)
);

INSERT INTO orders (customer_id, ordered_at, status) VALUES
    (1, '2025-01-05', 'delivered'), (2, '2025-01-06', 'delivered'),
    (1, '2025-02-10', 'delivered'), (3, '2025-02-11', 'cancelled'),
    (5, '2025-03-02', 'delivered'), (6, '2025-03-15', 'shipped'),
    (1, '2025-03-20', 'pending'),   (7, '2025-04-01', 'delivered'),
    (2, '2025-04-18', 'delivered'), (5, '2025-05-05', 'shipped');

INSERT INTO order_items VALUES
    (1, 1, 5, 60),   (1, 2, 10, 15.50), (2, 5, 1, 2500), (3, 3, 1, 1200),
    (3, 7, 2, 250),  (4, 6, 1, 1800),   (5, 4, 2, 350),  (5, 1, 3, 60),
    (6, 8, 1, 900),  (6, 2, 4, 15.50),  (7, 5, 1, 2500), (8, 7, 4, 250),
    (9, 1, 10, 60),  (9, 3, 1, 1200),   (10, 6, 1, 1800);

SELECT o.id, c.name, o.ordered_at, o.status
FROM orders AS o
JOIN customers AS c ON c.id = o.customer_id
ORDER BY o.id
LIMIT 5;
```

**Output:**

```text
 id | name  | ordered_at |  status
----+-------+------------+-----------
  1 | Asha  | 2025-01-05 | delivered
  2 | Ravi  | 2025-01-06 | delivered
  3 | Asha  | 2025-02-10 | delivered
  4 | Meera | 2025-02-11 | cancelled
  5 | Zoya  | 2025-03-02 | delivered
(5 rows)
```

```sql
-- LEFT JOIN keeps customers with no orders (their order columns are NULL)
SELECT c.name, count(o.id) AS orders
FROM customers AS c
LEFT JOIN orders AS o ON o.customer_id = c.id
GROUP BY c.id, c.name
ORDER BY orders DESC, c.name;
```

**Output:**

```text
 name  | orders
-------+--------
 Asha  |      3
 Ravi  |      2
 Zoya  |      2
 Isha  |      1
 Kabir |      1
 Meera |      1
 Arjun |      0
 Dev   |      0
(8 rows)
```

`count(o.id)` (not `count(*)`) gives 0 for customers without orders, because `o.id` is NULL for them.

```sql
-- three tables: what did each delivered order contain, and what was it worth?
SELECT o.id AS order_id, c.name AS customer,
       string_agg(p.name || ' ×' || oi.quantity, ', ' ORDER BY p.name) AS items,
       sum(oi.quantity * oi.unit_price) AS total
FROM orders o
JOIN customers c    ON c.id = o.customer_id
JOIN order_items oi ON oi.order_id = o.id
JOIN products p     ON p.id = oi.product_id
WHERE o.status = 'delivered'
GROUP BY o.id, c.name
ORDER BY o.id;
```

**Output:**

```text
 order_id | customer |            items             |  total
----------+----------+------------------------------+---------
        1 | Asha     | Notebook ×5, Pen ×10         |  455.00
        2 | Ravi     | Headphones ×1                | 2500.00
        3 | Asha     | Backpack ×1, Mug ×2          | 1700.00
        5 | Zoya     | Notebook ×3, Water bottle ×2 |  880.00
        8 | Isha     | Mug ×4                       | 1000.00
        9 | Ravi     | Backpack ×1, Notebook ×10    | 1800.00
(6 rows)
```

```sql
-- anti-join: customers who have never ordered
SELECT c.name
FROM customers c
LEFT JOIN orders o ON o.customer_id = c.id
WHERE o.id IS NULL
ORDER BY c.name;
```

**Output:**

```text
 name
-------
 Arjun
 Dev
(2 rows)
```

```sql
DROP TABLE IF EXISTS employees;
CREATE TABLE employees (
    id         int PRIMARY KEY,
    name       text NOT NULL,
    manager_id int REFERENCES employees (id),
    department text NOT NULL,
    salary     numeric(10, 2) NOT NULL
);
INSERT INTO employees VALUES
    (1, 'Anita',  NULL, 'Management',  300000), (2, 'Rahul', 1, 'Engineering', 180000),
    (3, 'Sneha',  1,    'Sales',       150000), (4, 'Vikram', 2, 'Engineering', 120000),
    (5, 'Priya',  2,    'Engineering', 120000), (6, 'Karan', 3, 'Sales',        90000),
    (7, 'Neha',   4,    'Engineering',  95000), (8, 'Rohan', 3, 'Sales',        85000);

-- self join: each employee with their manager's name
SELECT e.name AS employee, m.name AS manager
FROM employees e
LEFT JOIN employees m ON m.id = e.manager_id
ORDER BY e.id;
```

**Output:**

```text
 employee | manager
----------+---------
 Anita    | (null)
 Rahul    | Anita
 Sneha    | Anita
 Vikram   | Rahul
 Priya    | Rahul
 Karan    | Sneha
 Neha     | Vikram
 Rohan    | Sneha
(8 rows)
```

**Common mistakes:**

- ❌ Forgetting the `ON` condition (or joining on the wrong columns), which creates a huge cross join.
- ❌ Turning a LEFT JOIN into an INNER JOIN by filtering the right table in `WHERE`.
- ❌ Summing after a one-to-many join and double-counting.
- ❌ `count(*)` after a LEFT JOIN, which counts the NULL row as 1.

### Practice

1. List every product with the total quantity sold (0 for products never ordered).
2. Which customers have ordered a product from the `electronics` category?

<details>
<summary><b>Answer</b></summary>

```sql
SELECT p.name, coalesce(sum(oi.quantity), 0) AS sold
FROM products p
LEFT JOIN order_items oi ON oi.product_id = p.id
GROUP BY p.id, p.name
ORDER BY sold DESC, p.name;

SELECT DISTINCT c.name
FROM customers c
JOIN orders o       ON o.customer_id = c.id
JOIN order_items oi ON oi.order_id = o.id
JOIN products p     ON p.id = oi.product_id
WHERE p.category = 'electronics'
ORDER BY c.name;
```

**Output:**

```text
     name     | sold
--------------+------
 Notebook     |   18
 Pen          |   14
 Mug          |    6
 Backpack     |    2
 Headphones   |    2
 Keyboard     |    2
 Water bottle |    2
 Desk lamp    |    1
 Stapler      |    0
(9 rows)

 name
-------
 Asha
 Kabir
 Meera
 Ravi
 Zoya
(5 rows)
```

</details>

| # | Practice problem | Level |
|---|---|---|
| 1 | [LeetCode 1378. Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/) | 🟢 Easy |
| 2 | [LeetCode 1581. Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/) | 🟢 Easy |
| 3 | [LeetCode 197. Rising Temperature](https://leetcode.com/problems/rising-temperature/) (self join) | 🟢 Easy |
| 4 | [LeetCode 1280. Students and Examinations](https://leetcode.com/problems/students-and-examinations/) (cross join + left join) | 🟢 Easy |
| 5 | [LeetCode 570. Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/) | 🟡 Medium |
| 6 | [PostgreSQL Exercises: Joins](https://pgexercises.com/questions/joins/) | 🟡 Medium |

**Learn & visualise:** [PostgreSQL docs: Joins between tables](https://www.postgresql.org/docs/current/tutorial-join.html)

---

## 10. Subqueries and CTEs (WITH), Including Recursive Queries

![A CTE names a step; a recursive CTE repeats a step until no new rows appear](images/sql/08-cte.svg)

### Theory

> **In simple words:** a **subquery** is a query inside another query, used like a value, a list or a temporary table. A **CTE** (`WITH name AS (...)`) gives that inner query a **name**, so you can build a complex query step by step, like variables in a program.

**Where a subquery can go:**

| Kind | Returns | Example |
|---|---|---|
| **Scalar** | One value | `WHERE price > (SELECT avg(price) FROM products)` |
| **List** with `IN` | A column of values | `WHERE id IN (SELECT customer_id FROM orders)` |
| **EXISTS** | True if the subquery finds any row | `WHERE EXISTS (SELECT 1 FROM orders o WHERE o.customer_id = c.id)` |
| **Derived table** in `FROM` | A whole table | `FROM (SELECT ...) AS t` |

A **correlated** subquery refers to the outer row (`o.customer_id = c.id` above), so conceptually it runs once per outer row. PostgreSQL usually rewrites `EXISTS` into an efficient join for you.

**`NOT IN` has a NULL trap.** If the subquery's list contains even one NULL, `x NOT IN (list)` is never true (because `x <> NULL` is unknown), and you get **no rows**. `NOT EXISTS` doesn't have this problem, so prefer it.

**CTEs (common table expressions):**

```text
WITH order_totals AS (          -- step 1: a named result
    SELECT order_id, sum(quantity * unit_price) AS total
    FROM order_items GROUP BY order_id
)
SELECT ... FROM order_totals ...  -- step 2: use it like a table
```

Several CTEs can follow each other (`WITH a AS (...), b AS (... FROM a ...)`). They make long queries readable and testable one step at a time. (Since PostgreSQL 12, simple CTEs are inlined into the main query, so there's no performance penalty.)

**Recursive CTEs** repeat a step to walk **hierarchies** (org charts, folders, categories, comment threads) or generate sequences:

```text
WITH RECURSIVE chain AS (
    SELECT ... starting rows ...            -- the "anchor": where to start
    UNION ALL
    SELECT ... FROM table JOIN chain ...    -- the step: rows reachable from the previous ones
)
SELECT * FROM chain;
```

PostgreSQL runs the anchor, then repeats the step on the **newly added** rows until a step adds nothing. It's BFS over a graph, written in SQL.

**LATERAL** lets a subquery in `FROM` refer to columns of tables listed before it: "for each customer, their latest order". It's the SQL version of a loop with an inner query.

### SQL

```sql
-- scalar subquery: products priced above the average
SELECT name, price
FROM products
WHERE price > (SELECT avg(price) FROM products)
ORDER BY price DESC;
```

**Output:**

```text
    name    |  price
------------+---------
 Headphones | 2500.00
 Keyboard   | 1800.00
 Backpack   | 1200.00
 Desk lamp  |  900.00
(4 rows)
```

```sql
-- EXISTS vs the NOT IN trap
SELECT name FROM customers c
WHERE NOT EXISTS (SELECT 1 FROM orders o WHERE o.customer_id = c.id)
ORDER BY name;

SELECT count(*) AS not_in_with_a_null
FROM customers
WHERE id NOT IN (SELECT manager_id FROM employees);   -- manager_id contains a NULL
```

**Output:**

```text
 name
-------
 Arjun
 Dev
(2 rows)

 not_in_with_a_null
--------------------
                  0
(1 row)
```

The second query returns 0 even though most customer IDs aren't manager IDs: the NULL in the list makes every `NOT IN` unknown.

```sql
-- CTEs: build the answer in named steps
WITH order_totals AS (
    SELECT order_id, sum(quantity * unit_price) AS total
    FROM order_items
    GROUP BY order_id
),
customer_spend AS (
    SELECT o.customer_id, sum(t.total) AS spent, count(*) AS orders
    FROM orders o
    JOIN order_totals t ON t.order_id = o.id
    WHERE o.status <> 'cancelled'
    GROUP BY o.customer_id
)
SELECT c.name, s.orders, s.spent
FROM customer_spend s
JOIN customers c ON c.id = s.customer_id
ORDER BY s.spent DESC;
```

**Output:**

```text
 name  | orders |  spent
-------+--------+---------
 Asha  |      3 | 4655.00
 Ravi  |      2 | 4300.00
 Zoya  |      2 | 2680.00
 Isha  |      1 | 1000.00
 Kabir |      1 |  962.00
(5 rows)
```

```sql
-- recursive CTE: everyone who reports (directly or indirectly) to Rahul, with their level
WITH RECURSIVE team AS (
    SELECT id, name, 1 AS level FROM employees WHERE manager_id = 2      -- anchor: direct reports
    UNION ALL
    SELECT e.id, e.name, t.level + 1
    FROM employees e JOIN team t ON e.manager_id = t.id                  -- step: their reports
)
SELECT name, level FROM team ORDER BY level, name;
```

**Output:**

```text
  name  | level
--------+-------
 Priya  |     1
 Vikram |     1
 Neha   |     2
(3 rows)
```

```sql
-- LATERAL: each customer's most recent order
SELECT c.name, last.ordered_at, last.status
FROM customers c
CROSS JOIN LATERAL (
    SELECT ordered_at, status FROM orders o
    WHERE o.customer_id = c.id
    ORDER BY ordered_at DESC
    LIMIT 1
) AS last
ORDER BY c.name;

-- generate_series makes a sequence without any table
SELECT n, n * n AS square FROM generate_series(1, 5) AS n;
```

**Output:**

```text
 name  | ordered_at |  status
-------+------------+-----------
 Asha  | 2025-03-20 | pending
 Isha  | 2025-04-01 | delivered
 Kabir | 2025-03-15 | shipped
 Meera | 2025-02-11 | cancelled
 Ravi  | 2025-04-18 | delivered
 Zoya  | 2025-05-05 | shipped
(6 rows)

 n | square
---+--------
 1 |      1
 2 |      4
 3 |      9
 4 |     16
 5 |     25
(5 rows)
```

**Common mistakes:**

- ❌ `NOT IN` with a subquery that can return NULL. ✅ `NOT EXISTS`.
- ❌ A scalar subquery that returns more than one row (an error at run time).
- ❌ A recursive CTE on data with a **cycle** (A manages B manages A) loops forever. Stop it with a depth limit or a `CYCLE` clause (PostgreSQL 14+).

### Practice

1. Find products that have never been ordered, using `NOT EXISTS`.
2. With a CTE, find the average order value (non-cancelled orders only).

<details>
<summary><b>Answer</b></summary>

```sql
SELECT name FROM products p
WHERE NOT EXISTS (SELECT 1 FROM order_items oi WHERE oi.product_id = p.id)
ORDER BY name;

WITH totals AS (
    SELECT o.id, sum(oi.quantity * oi.unit_price) AS total
    FROM orders o JOIN order_items oi ON oi.order_id = o.id
    WHERE o.status <> 'cancelled'
    GROUP BY o.id
)
SELECT round(avg(total), 2) AS avg_order_value FROM totals;
```

**Output:**

```text
  name
---------
 Stapler
(1 row)

 avg_order_value
-----------------
         1510.78
(1 row)
```

</details>

| # | Practice problem | Level |
|---|---|---|
| 1 | [LeetCode 1978. Employees Whose Manager Left the Company](https://leetcode.com/problems/employees-whose-manager-left-the-company/) | 🟢 Easy |
| 2 | [LeetCode 1070. Product Sales Analysis III](https://leetcode.com/problems/product-sales-analysis-iii/) | 🟡 Medium |
| 3 | [LeetCode 585. Investments in 2016](https://leetcode.com/problems/investments-in-2016/) | 🟡 Medium |
| 4 | [LeetCode 1164. Product Price at a Given Date](https://leetcode.com/problems/product-price-at-a-given-date/) | 🟡 Medium |
| 5 | [PostgreSQL Exercises: Recursive queries](https://pgexercises.com/questions/recursive/) | 🟡 Medium |

**Learn more:** [PostgreSQL docs: WITH queries](https://www.postgresql.org/docs/current/queries-with.html)

---

## 11. Set Operations: UNION, INTERSECT and EXCEPT

### Theory

> **In simple words:** joins put tables **side by side** (more columns); set operations stack results **on top of each other** (more rows), or keep only the rows two results share, or only the rows one has and the other doesn't.

| Operation | Returns | Duplicates |
|---|---|---|
| `A UNION B` | Rows in A **or** B | Removed |
| `A UNION ALL B` | All rows of A, then all rows of B | **Kept** (and faster, since no de-duplication is needed) |
| `A INTERSECT B` | Rows in **both** A and B | Removed |
| `A EXCEPT B` | Rows in A that are **not** in B | Removed |

**Rules:** both queries must return the **same number of columns** with **compatible types**; the column names come from the first query; one `ORDER BY` at the very end sorts the combined result.

**UNION or UNION ALL?** Use `UNION ALL` unless you really need duplicates removed: removing them means sorting or hashing every row.

**Typical uses:** merging similar tables (this year's and last year's archive), building one list from different sources ("everyone to email: customers and employees"), and comparing lists ("customers who ordered in January but not in February").

### SQL

```sql
-- one contact list from two tables, with a label
SELECT name, 'customer' AS kind FROM customers WHERE city = 'Pune'
UNION ALL
SELECT name, 'employee' FROM employees WHERE department = 'Sales'
ORDER BY kind, name;
```

**Output:**

```text
 name  |   kind
-------+----------
 Asha  | customer
 Dev   | customer
 Meera | customer
 Karan | employee
 Rohan | employee
 Sneha | employee
(6 rows)
```

```sql
-- customers who ordered in January AND in April; in January but NOT in April
SELECT customer_id FROM orders WHERE ordered_at < '2025-02-01'
INTERSECT
SELECT customer_id FROM orders WHERE ordered_at >= '2025-04-01' AND ordered_at < '2025-05-01';

SELECT customer_id FROM orders WHERE ordered_at < '2025-02-01'
EXCEPT
SELECT customer_id FROM orders WHERE ordered_at >= '2025-04-01' AND ordered_at < '2025-05-01';
```

**Output:**

```text
 customer_id
-------------
           2
(1 row)

 customer_id
-------------
           1
(1 row)
```

**Common mistakes:**

- ❌ Different column counts or incompatible types in the two queries.
- ❌ `UNION` when duplicates are fine (slower for no reason).
- ❌ Putting `ORDER BY` inside the first query instead of at the end.

### Practice

1. List all cities that have customers, plus the city 'Chennai', with no duplicates.
2. Which product IDs exist in `products` but were never ordered? Use `EXCEPT`.

<details>
<summary><b>Answer</b></summary>

```sql
SELECT city FROM customers
UNION
SELECT 'Chennai'
ORDER BY city;

SELECT id FROM products
EXCEPT
SELECT product_id FROM order_items;
```

**Output:**

```text
   city
-----------
 Bengaluru
 Chennai
 Delhi
 Mumbai
 Pune
(5 rows)

 id
----
  9
(1 row)
```

</details>

| # | Practice problem | Level |
|---|---|---|
| 1 | [LeetCode 1965. Employees With Missing Information](https://leetcode.com/problems/employees-with-missing-information/) | 🟢 Easy |
| 2 | [LeetCode 1795. Rearrange Products Table](https://leetcode.com/problems/rearrange-products-table/) | 🟢 Easy |
| 3 | [LeetCode 1341. Movie Rating](https://leetcode.com/problems/movie-rating/) | 🟡 Medium |

---

### ✅ Part 2 checkpoint

Without looking, can you:

- [ ] Use text, number and date functions, `CASE`, `COALESCE` and `NULLIF`?
- [ ] Group rows and filter groups with `HAVING`, and explain the logical order of a query's clauses?
- [ ] Write INNER, LEFT and self joins across three tables, and find rows with no match?
- [ ] Explain the `NOT IN` + NULL trap and use `NOT EXISTS` instead?
- [ ] Break a long query into CTEs, and walk a hierarchy with a recursive CTE?
- [ ] Combine results with `UNION ALL`, `INTERSECT` and `EXCEPT`?

---

# Part 3 — Moderate: Designing Databases

> **Goal:** Design tables that keep data correct: keys, constraints, relationships, normalisation, schema changes, views, and window functions for analysis.  
> **You need:** Parts 1–2.

---

## 12. Keys and Constraints: Letting the Database Protect Your Data

![Constraints reject bad rows before they are stored](images/sql/09-constraints.svg)

### Theory

> **In simple words:** constraints are **rules the database enforces on every write**: "every product needs a name", "no two customers share an email", "every order must belong to a real customer", "stock can't be negative". Bad data is rejected at the door, whatever program sends it.

Application code has bugs, and many programs (web app, scripts, admin tools) may write to the same database. Constraints are the one place where the rules can't be bypassed.

| Constraint | Rule | Example |
|---|---|---|
| `NOT NULL` | A value is required | `name text NOT NULL` |
| `UNIQUE` | No two rows share the value (NULLs don't count as equal) | `email text UNIQUE` |
| `PRIMARY KEY` | `UNIQUE` + `NOT NULL`: the row's identity | `id int GENERATED ALWAYS AS IDENTITY PRIMARY KEY` |
| `FOREIGN KEY` / `REFERENCES` | The value must exist in another table's key | `customer_id int REFERENCES customers (id)` |
| `CHECK` | Any true/false rule on the row | `CHECK (price >= 0)` |
| `DEFAULT` | Value to use when none is given (not a rule, but defined the same way) | `created_at timestamptz DEFAULT now()` |

**Composite keys** cover several columns: `PRIMARY KEY (order_id, product_id)` in `order_items` means "each product appears once per order".

**Foreign keys and deletes.** What should happen to orders when their customer is deleted? You choose with `ON DELETE`:

| Option | Effect | Typical use |
|---|---|---|
| `NO ACTION` / `RESTRICT` (default) | Refuse to delete the customer while orders point to them | Most business data: don't lose history |
| `CASCADE` | Delete the orders too | Child rows that mean nothing alone (a post's comments, an order's items) |
| `SET NULL` | Set `customer_id` to NULL | Optional links ("assigned to" an employee who left) |

**Natural vs surrogate keys.** A **natural** key is a real-world value (an email, a passport number); a **surrogate** key is a meaningless generated number or UUID. Use a surrogate primary key (real-world values change: people change emails), and put `UNIQUE` on natural keys that must stay unique.

**Name your constraints** (`CONSTRAINT price_not_negative CHECK (price >= 0)`) so error messages and migrations are readable.

**Remember to index foreign keys.** PostgreSQL indexes primary keys and unique columns automatically, but **not** foreign-key columns. Queries like "orders of customer 5" and deletes on the parent table need an index on `orders.customer_id` (Section [18](#18-indexes-making-lookups-fast)).

### SQL

```sql
ALTER TABLE products ADD CONSTRAINT price_not_negative CHECK (price >= 0);
ALTER TABLE products ADD CONSTRAINT stock_not_negative CHECK (stock >= 0);
ALTER TABLE customers ADD CONSTRAINT customers_email_key UNIQUE (email);

UPDATE products SET stock = stock - 100 WHERE name = 'Headphones';           -- only 15 in stock
INSERT INTO customers (name, email) VALUES ('Asha Copy', 'asha@example.com'); -- duplicate email
INSERT INTO orders (customer_id, ordered_at, status) VALUES (999, '2025-06-01', 'pending');  -- no customer 999
INSERT INTO products (category, price) VALUES ('bags', 10);                  -- no name
```

**Output:**

```text
ERROR:  new row for relation "products" violates check constraint "stock_not_negative"
DETAIL:  Failing row contains (5, Headphones, electronics, 2500.00, -85).
ERROR:  duplicate key value violates unique constraint "customers_email_key"
DETAIL:  Key (email)=(asha@example.com) already exists.
ERROR:  insert or update on table "orders" violates foreign key constraint "orders_customer_id_fkey"
DETAIL:  Key (customer_id)=(999) is not present in table "customers".
ERROR:  null value in column "name" of relation "products" violates not-null constraint
DETAIL:  Failing row contains (11, null, bags, 10.00, 0).
```

Each bad write is rejected with a clear message, and the data stays correct.

```sql
-- ON DELETE in action, on two small tables
CREATE TABLE posts (id int PRIMARY KEY, title text NOT NULL);
CREATE TABLE comments (
    id      int PRIMARY KEY,
    post_id int NOT NULL REFERENCES posts (id) ON DELETE CASCADE,
    body    text NOT NULL
);
INSERT INTO posts VALUES (1, 'Hello'), (2, 'SQL tips');
INSERT INTO comments VALUES (10, 1, 'Nice!'), (11, 1, 'Thanks'), (12, 2, 'Useful');

DELETE FROM posts WHERE id = 1;          -- its comments go too
SELECT * FROM comments;

DELETE FROM customers WHERE id = 1;      -- orders use the default (NO ACTION): refused
DROP TABLE comments, posts;
```

**Output:**

```text
 id | post_id |  body
----+---------+--------
 12 |       2 | Useful
(1 row)

ERROR:  update or delete on table "customers" violates foreign key constraint "orders_customer_id_fkey" on table "orders"
DETAIL:  Key (id)=(1) is still referenced from table "orders".
```

**Common mistakes:**

- ❌ Enforcing rules only in application code ("the form checks it").
- ❌ `ON DELETE CASCADE` on important data: one delete can silently wipe thousands of rows.
- ❌ Using an email or username as the primary key.
- ❌ Forgetting to index foreign-key columns.

### Practice

1. Add a rule that an order's `status` can only be `pending`, `shipped`, `delivered` or `cancelled`, then try to insert `'lost'`.
2. Why is `UNIQUE (email)` allowed even though two customers have a NULL email?

<details>
<summary><b>Answer</b></summary>

```sql
ALTER TABLE orders ADD CONSTRAINT valid_status
    CHECK (status IN ('pending', 'shipped', 'delivered', 'cancelled'));
INSERT INTO orders (customer_id, ordered_at, status) VALUES (1, '2025-06-01', 'lost');
```

**Output:**

```text
ERROR:  new row for relation "orders" violates check constraint "valid_status"
DETAIL:  Failing row contains (12, 1, 2025-06-01, lost).
```

2: NULL means "unknown", and two unknowns aren't considered equal, so they don't violate `UNIQUE`. (PostgreSQL 15+ has `UNIQUE NULLS NOT DISTINCT` if you want at most one NULL.)

</details>

**Learn more:** [PostgreSQL docs: Constraints](https://www.postgresql.org/docs/current/ddl-constraints.html)

---

## 13. Designing Tables: Relationships and Normalisation

![One-to-many, many-to-many via a junction table, and one-to-one](images/sql/10-relationships.svg)

### Theory

> **In simple words:** good database design means **storing each fact exactly once**. If a customer's city is written on every one of their orders, changing their city means updating many rows, and missing one leaves the data contradicting itself. Normalisation is the set of rules for splitting data into tables so that can't happen.

**The three relationships between tables:**

| Relationship | Example | How to model it |
|---|---|---|
| **One-to-many** (1:N) | One customer has many orders | A foreign key on the "many" side: `orders.customer_id` |
| **Many-to-many** (N:M) | An order has many products; a product is in many orders | A **junction table** with two foreign keys: `order_items (order_id, product_id)`, which can also hold data about the pair (quantity, price) |
| **One-to-one** (1:1) | A user and their profile settings | A foreign key that is also `UNIQUE` (or the same primary key in both tables) |

**The problems normalisation prevents.** Imagine one wide table `orders_flat (order_id, customer_name, customer_city, product_name, product_price, quantity)`:

- **Update anomaly:** Asha moves to Mumbai; her city is stored in every row of every order, and missing one leaves two different cities for her.
- **Insert anomaly:** you can't record a new product until someone orders it.
- **Delete anomaly:** deleting the only order for a product also deletes everything you knew about the product.

**The normal forms, in plain words** (each builds on the previous one):

| Form | Rule | Breaks it |
|---|---|---|
| **1NF** | Each cell holds **one** value; no repeating groups | `phones = '98xxx, 99xxx'` in one cell, or columns `phone1, phone2, phone3` |
| **2NF** | Every non-key column depends on the **whole** key | In `order_items (order_id, product_id, product_name)`, the name depends only on `product_id` |
| **3NF** | Non-key columns depend **only** on the key, not on other non-key columns | In `customers (id, pincode, city)`, the city depends on the pincode |
| **BCNF** | A stricter 3NF: every determining column is a key | Rare edge cases |

A memorable summary of 3NF: every column must depend on "**the key, the whole key, and nothing but the key**".

**Denormalisation: breaking the rules on purpose.** Sometimes you **copy** data to make reads faster or to keep history:

- `order_items.unit_price` copies the product's price **at the time of the order**. That's not redundancy, it's a different fact (prices change; old orders must not).
- Analytics tables and data warehouses are often deliberately wide ("star schemas") because they're read far more than written.
- Cached counts like `posts.comment_count` save a count query, at the cost of keeping them in sync (triggers, Section [24](#24-functions-procedures-and-triggers)).

Normalise first; denormalise only for a measured reason.

**A design checklist:** give every table a surrogate primary key; name tables in the plural and columns in `snake_case`; use the right types (Section [4](#4-data-types-and-null)); add `NOT NULL`, `UNIQUE`, `CHECK` and foreign keys (Section [12](#12-keys-and-constraints-letting-the-database-protect-your-data)); add `created_at` and `updated_at timestamptz` columns; and draw an **ER diagram** (entities and relationships) before creating anything. Tools like dbdiagram.io or DBeaver draw them for you.

### SQL

```sql
-- the anomaly, live: a denormalised copy of orders with the customer's city repeated
CREATE TABLE orders_flat AS
SELECT o.id AS order_id, c.name AS customer, c.city AS customer_city, o.ordered_at
FROM orders o JOIN customers c ON c.id = o.customer_id;

UPDATE orders_flat SET customer_city = 'Mumbai' WHERE order_id = 1;   -- update only one of Asha's rows

SELECT customer, string_agg(DISTINCT customer_city, ' / ') AS cities
FROM orders_flat
GROUP BY customer
HAVING count(DISTINCT customer_city) > 1;

DROP TABLE orders_flat;
```

**Output:**

```text
 customer |    cities
----------+---------------
 Asha     | Mumbai / Pune
(1 row)
```

The flat table now claims Asha lives in two cities. In the normalised design, her city exists in exactly one row of `customers`, so this contradiction is impossible.

**Common mistakes:**

- ❌ Comma-separated lists in a column (`tags = 'sql,db,postgres'`), which break 1NF and make searching slow. ✅ A junction table (or, carefully, an array: Section [22](#22-arrays-enums-ranges-and-generated-columns)).
- ❌ Copying customer details into every order "for convenience".
- ❌ One giant table for everything, or the opposite: splitting into dozens of tiny tables nobody can query.

### Practice

Design tables for a **library**: books (a book can have several authors), authors, members, and loans (a member borrows a copy of a book on a date and returns it later). Write the `CREATE TABLE` statements.

<details>
<summary><b>Answer</b></summary>

```sql
CREATE TABLE authors (id int GENERATED ALWAYS AS IDENTITY PRIMARY KEY, name text NOT NULL);
CREATE TABLE books   (id int GENERATED ALWAYS AS IDENTITY PRIMARY KEY, title text NOT NULL, isbn text UNIQUE);
CREATE TABLE book_authors (                        -- many-to-many
    book_id   int REFERENCES books (id) ON DELETE CASCADE,
    author_id int REFERENCES authors (id),
    PRIMARY KEY (book_id, author_id)
);
CREATE TABLE members (id int GENERATED ALWAYS AS IDENTITY PRIMARY KEY, name text NOT NULL, email text UNIQUE);
CREATE TABLE loans (
    id          int GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    book_id     int NOT NULL REFERENCES books (id),
    member_id   int NOT NULL REFERENCES members (id),
    borrowed_on date NOT NULL DEFAULT current_date,
    returned_on date,
    CHECK (returned_on IS NULL OR returned_on >= borrowed_on)
);
DROP TABLE loans, members, book_authors, books, authors;
```

A real library would add a `copies` table (several physical copies per book) and have loans reference a copy.

</details>

| # | Practice problem | Level |
|---|---|---|
| 1 | [dbdiagram.io](https://dbdiagram.io/) — draw your library design as an ER diagram | 🟢 Easy |
| 2 | Redesign a spreadsheet you use (expenses, a class register) into normalised tables | 🟡 Medium |

---

## 14. Changing the Schema: ALTER TABLE and Migrations

### Theory

> **In simple words:** apps change, so tables must change too: new columns, renamed columns, new rules. `ALTER TABLE` does it, and **migrations** are numbered scripts that apply those changes in the same order on every copy of the database (your laptop, testing, production).

**The common ALTER TABLE commands:**

| Command | Does |
|---|---|
| `ADD COLUMN phone text` | Add a column (NULL in existing rows, or the `DEFAULT`) |
| `DROP COLUMN phone` | Remove a column and its data |
| `RENAME COLUMN a TO b`, `RENAME TO new_name` | Rename a column / the table |
| `ALTER COLUMN x TYPE bigint` | Change the type (may rewrite the whole table) |
| `ALTER COLUMN x SET NOT NULL` / `DROP NOT NULL` | Add/remove the NOT NULL rule |
| `ALTER COLUMN x SET DEFAULT ...` | Change the default for future rows |
| `ADD CONSTRAINT ...` / `DROP CONSTRAINT ...` | Add/remove rules (Section [12](#12-keys-and-constraints-letting-the-database-protect-your-data)) |

**Migrations in real projects.** Nobody types `ALTER TABLE` by hand on production. Each change is a file in version control (`0007_add_phone_to_customers.sql`), and a tool applies the ones not yet run and records which ran: **Alembic** (Python / SQLAlchemy), **Django migrations**, **Flyway** and **Liquibase** (Java), **Prisma Migrate** and **Drizzle** (TypeScript), or plain SQL files with a tool like **dbmate**. Migrations are reviewed like code and tested on a copy of production data.

**Changing a busy production table safely (zero-downtime migrations).** Some changes **lock** the table while they run, blocking the app. The safe patterns:

- **Adding a column** with no default, or with a constant default, is instant in PostgreSQL 11+.
- **Adding NOT NULL to an existing column:** add a `CHECK (col IS NOT NULL) NOT VALID` constraint, `VALIDATE` it (which doesn't block writes), then `SET NOT NULL`, which uses the validated check.
- **Creating an index:** `CREATE INDEX CONCURRENTLY` doesn't block writes (Section [18](#18-indexes-making-lookups-fast)).
- **Renaming or changing a column that the app uses: expand, then contract.** Add the new column → write to both → backfill old rows in small batches → switch reads to the new column → deploy → only then drop the old one. The app and the database must work together at every step.
- Set `lock_timeout` so a migration gives up instead of queueing behind a long transaction and blocking everyone.

### SQL

```sql
ALTER TABLE customers ADD COLUMN phone text;
ALTER TABLE customers ADD COLUMN is_active boolean NOT NULL DEFAULT true;
ALTER TABLE customers RENAME COLUMN signed_up TO signed_up_on;

UPDATE customers SET phone = '+91-90000-0000' || id WHERE city = 'Pune';

SELECT id, name, phone, is_active, signed_up_on FROM customers WHERE city = 'Pune' ORDER BY id;

ALTER TABLE customers DROP COLUMN phone;
ALTER TABLE customers RENAME COLUMN signed_up_on TO signed_up;
ALTER TABLE customers DROP COLUMN is_active;
```

**Output:**

```text
 id | name  |      phone      | is_active | signed_up_on
----+-------+-----------------+-----------+--------------
  1 | Asha  | +91-90000-00001 | t         | 2024-01-15
  3 | Meera | +91-90000-00003 | t         | 2024-03-22
  8 | Dev   | +91-90000-00008 | t         | 2025-05-01
(3 rows)
```

```sql
-- the safe way to make an existing column required
ALTER TABLE orders ADD CONSTRAINT ordered_at_present CHECK (ordered_at IS NOT NULL) NOT VALID;
ALTER TABLE orders VALIDATE CONSTRAINT ordered_at_present;     -- checks old rows without blocking writes
ALTER TABLE orders ALTER COLUMN ordered_at SET NOT NULL;       -- fast: uses the validated check
ALTER TABLE orders DROP CONSTRAINT ordered_at_present;
SELECT column_name, is_nullable FROM information_schema.columns
WHERE table_name = 'orders' ORDER BY ordinal_position;
```

**Output:**

```text
 column_name | is_nullable
-------------+-------------
 id          | NO
 customer_id | NO
 ordered_at  | NO
 status      | NO
(4 rows)
```

`information_schema` is the standard, read-only set of views describing every table and column; it's how tools inspect your database.

**Common mistakes:**

- ❌ Editing a migration that has already run somewhere. ✅ Write a new migration.
- ❌ Renaming or dropping a column in the same deploy that still uses it.
- ❌ Long-running backfills in one transaction on a huge table. ✅ Batches of a few thousand rows.
- ❌ Running migrations against production without a backup and a tested rollback plan.

### Practice

1. Add a `discount_percent int NOT NULL DEFAULT 0` column to `products` with a check that it's between 0 and 90, then remove it again.

<details>
<summary><b>Answer</b></summary>

```sql
ALTER TABLE products
    ADD COLUMN discount_percent int NOT NULL DEFAULT 0
    CHECK (discount_percent BETWEEN 0 AND 90);
UPDATE products SET discount_percent = 95 WHERE id = 1;     -- rejected
ALTER TABLE products DROP COLUMN discount_percent;
```

**Output:**

```text
ERROR:  new row for relation "products" violates check constraint "products_discount_percent_check"
DETAIL:  Failing row contains (1, Notebook, stationery, 60.00, 120, 95).
```

</details>

**Learn more:** [PostgreSQL docs: Modifying tables](https://www.postgresql.org/docs/current/ddl-alter.html) · [Alembic tutorial](https://alembic.sqlalchemy.org/en/latest/tutorial.html)

---

## 15. Views and Materialized Views

### Theory

> **In simple words:** a **view** is a saved query with a name that you can use like a table. A **materialized view** also saves the query's **result**, like a snapshot, so reading it is instant, but it must be refreshed to see new data.

**Views** (`CREATE VIEW name AS SELECT ...`):

- Hide complexity: a five-table join becomes `SELECT * FROM order_summary`.
- Give a stable interface: the tables underneath can change as long as the view keeps its columns.
- Control access: let a reporting user read a view that exposes only safe columns (Section [27](#27-security-roles-permissions-row-level-security-and-sql-injection)).
- Store **no data**: every read runs the underlying query, so results are always current, and costs are the same as the query itself.

**Materialized views** (`CREATE MATERIALIZED VIEW ...`):

- Store the result on disk, and can have their own indexes, so heavy aggregations become instant reads.
- Go stale: `REFRESH MATERIALIZED VIEW name;` recomputes them (from a scheduled job, say every 10 minutes). `REFRESH ... CONCURRENTLY` lets people keep reading during the refresh (it needs a unique index on the view).
- Are ideal for dashboards and reports where "a few minutes old" is fine.

| | View | Materialized view |
|---|---|---|
| Stores data | No | Yes |
| Always up to date | Yes | Only after a refresh |
| Read speed | Same as the query | Like reading a table |
| Good for | Simplifying and securing queries | Expensive reports and dashboards |

### SQL

```sql
CREATE VIEW order_summary AS
SELECT o.id AS order_id, c.name AS customer, o.status, o.ordered_at,
       sum(oi.quantity * oi.unit_price) AS total
FROM orders o
JOIN customers c    ON c.id = o.customer_id
JOIN order_items oi ON oi.order_id = o.id
GROUP BY o.id, c.name;

SELECT customer, count(*) AS orders, sum(total) AS spent
FROM order_summary
WHERE status <> 'cancelled'
GROUP BY customer
ORDER BY spent DESC
LIMIT 3;
```

**Output:**

```text
 customer | orders |  spent
----------+--------+---------
 Asha     |      3 | 4655.00
 Ravi     |      2 | 4300.00
 Zoya     |      2 | 2680.00
(3 rows)
```

```sql
CREATE MATERIALIZED VIEW monthly_sales AS
SELECT date_trunc('month', ordered_at)::date AS month, sum(total) AS revenue, count(*) AS orders
FROM order_summary
WHERE status <> 'cancelled'
GROUP BY 1;

SELECT * FROM monthly_sales ORDER BY month;

INSERT INTO orders (customer_id, ordered_at, status) VALUES (3, '2025-05-20', 'delivered');
INSERT INTO order_items VALUES (currval('orders_id_seq'), 5, 1, 2500);

SELECT revenue AS may_before_refresh FROM monthly_sales WHERE month = '2025-05-01';
REFRESH MATERIALIZED VIEW monthly_sales;
SELECT revenue AS may_after_refresh FROM monthly_sales WHERE month = '2025-05-01';
```

**Output:**

```text
   month    | revenue | orders
------------+---------+--------
 2025-01-01 | 2955.00 |      2
 2025-02-01 | 1700.00 |      1
 2025-03-01 | 4342.00 |      3
 2025-04-01 | 2800.00 |      2
 2025-05-01 | 1800.00 |      1
(5 rows)

 may_before_refresh
--------------------
            1800.00
(1 row)

 may_after_refresh
-------------------
           4300.00
(1 row)
```

`currval('orders_id_seq')` is the ID just generated for the new order in this session. (`GROUP BY 1` means "group by the first selected column".)

**Common mistakes:**

- ❌ Expecting a view to make a slow query fast. It's the same query; use indexes or a materialized view.
- ❌ Forgetting to schedule refreshes, so a dashboard shows old numbers.
- ❌ Stacking views on views on views until nobody can tell what a query really does.

### Practice

1. Create a view `product_sales` with each product's name and total units sold (0 if none), then read the top 3.

<details>
<summary><b>Answer</b></summary>

```sql
CREATE VIEW product_sales AS
SELECT p.name, coalesce(sum(oi.quantity), 0) AS units
FROM products p LEFT JOIN order_items oi ON oi.product_id = p.id
GROUP BY p.id, p.name;

SELECT * FROM product_sales ORDER BY units DESC, name LIMIT 3;
DROP VIEW product_sales;
```

**Output:**

```text
   name   | units
----------+-------
 Notebook |    18
 Pen      |    14
 Mug      |     6
(3 rows)
```

</details>

**Learn more:** [PostgreSQL docs: Materialized views](https://www.postgresql.org/docs/current/rules-materializedviews.html)

---

## 16. Window Functions: Rankings, Running Totals and Comparing Rows

![GROUP BY collapses each group into one row; a window function keeps every row and adds a value computed over its group](images/sql/11-window.svg)

### Theory

> **In simple words:** a window function looks at a **group of related rows** (the "window") to compute something for **each row**, **without** collapsing them the way `GROUP BY` does. "Rank each employee within their department", "running total of sales by day", "compare each order with the previous one".

**The syntax:**

```text
function(...) OVER (
    PARTITION BY dept        -- split rows into groups (optional; without it, the window is all rows)
    ORDER BY salary DESC     -- order inside each group (needed for rankings and running totals)
    ROWS BETWEEN ...         -- which neighbouring rows to include (optional "frame")
)
```

**The functions you'll use:**

| Function | Gives | Example use |
|---|---|---|
| `row_number()` | 1, 2, 3, … (no ties) | De-duplicate: keep row 1 per group |
| `rank()` | 1, 2, 2, 4 (ties share, then skip) | Competition rankings |
| `dense_rank()` | 1, 2, 2, 3 (ties share, no gaps) | "Second-highest salary" |
| `ntile(4)` | Which quarter (1–4) a row falls in | Quartiles, grouping customers into bands |
| `sum() / avg() / count() OVER (...)` | Aggregate over the window, on every row | Group totals next to details, running totals |
| `lag(col, n)` / `lead(col, n)` | The value n rows before / after | Day-over-day change |
| `first_value()` / `last_value()` | The first / last value in the window | "Top earner in the department" |

**Running totals and frames.** With `ORDER BY` inside `OVER`, `sum(x)` sums **from the first row up to the current one**: a running total. For a moving average over the last 3 rows, add a frame: `ROWS BETWEEN 2 PRECEDING AND CURRENT ROW`.

**Where window functions run.** After `WHERE`, `GROUP BY` and `HAVING`, just before `ORDER BY`. So you **can't** filter on them in `WHERE`: compute them in a CTE or subquery, then filter outside (the "top N per group" pattern below).

**`WINDOW w AS (...)`** names a window definition you can reuse across several functions in one query.

### SQL

```sql
SELECT name, department, salary,
       rank()       OVER (PARTITION BY department ORDER BY salary DESC) AS dept_rank,
       dense_rank() OVER (ORDER BY salary DESC)                         AS overall_dense_rank,
       round(salary * 100.0 / sum(salary) OVER (PARTITION BY department), 1) AS pct_of_dept
FROM employees
ORDER BY department, dept_rank;
```

**Output:**

```text
  name  | department  |  salary   | dept_rank | overall_dense_rank | pct_of_dept
--------+-------------+-----------+-----------+--------------------+-------------
 Rahul  | Engineering | 180000.00 |         1 |                  2 |        35.0
 Vikram | Engineering | 120000.00 |         2 |                  4 |        23.3
 Priya  | Engineering | 120000.00 |         2 |                  4 |        23.3
 Neha   | Engineering |  95000.00 |         4 |                  5 |        18.4
 Anita  | Management  | 300000.00 |         1 |                  1 |       100.0
 Sneha  | Sales       | 150000.00 |         1 |                  3 |        46.2
 Karan  | Sales       |  90000.00 |         2 |                  6 |        27.7
 Rohan  | Sales       |  85000.00 |         3 |                  7 |        26.2
(8 rows)
```

Vikram and Priya tie, so `rank()` gives them both 2 and then skips to 4; `dense_rank()` gives the next person 5 instead of 6 overall.

```sql
-- daily revenue with a running total and the change from the previous order day
WITH daily AS (
    SELECT ordered_at, sum(total) AS revenue
    FROM order_summary
    WHERE status <> 'cancelled'
    GROUP BY ordered_at
)
SELECT ordered_at, revenue,
       sum(revenue) OVER (ORDER BY ordered_at)                AS running_total,
       revenue - lag(revenue) OVER (ORDER BY ordered_at)      AS change_vs_previous,
       round(avg(revenue) OVER (ORDER BY ordered_at
                                ROWS BETWEEN 2 PRECEDING AND CURRENT ROW), 2) AS moving_avg_3
FROM daily
ORDER BY ordered_at;
```

**Output:**

```text
 ordered_at | revenue | running_total | change_vs_previous | moving_avg_3
------------+---------+---------------+--------------------+--------------
 2025-01-05 |  455.00 |        455.00 |             (null) |       455.00
 2025-01-06 | 2500.00 |       2955.00 |            2045.00 |      1477.50
 2025-02-10 | 1700.00 |       4655.00 |            -800.00 |      1551.67
 2025-03-02 |  880.00 |       5535.00 |            -820.00 |      1693.33
 2025-03-15 |  962.00 |       6497.00 |              82.00 |      1180.67
 2025-03-20 | 2500.00 |       8997.00 |            1538.00 |      1447.33
 2025-04-01 | 1000.00 |       9997.00 |           -1500.00 |      1487.33
 2025-04-18 | 1800.00 |      11797.00 |             800.00 |      1766.67
 2025-05-05 | 1800.00 |      13597.00 |               0.00 |      1533.33
 2025-05-20 | 2500.00 |      16097.00 |             700.00 |      2033.33
(10 rows)
```

```sql
-- top N per group: the highest-paid person in each department
WITH ranked AS (
    SELECT name, department, salary,
           row_number() OVER (PARTITION BY department ORDER BY salary DESC, name) AS rn
    FROM employees
)
SELECT department, name, salary FROM ranked WHERE rn = 1 ORDER BY department;
```

**Output:**

```text
 department  | name  |  salary
-------------+-------+-----------
 Engineering | Rahul | 180000.00
 Management  | Anita | 300000.00
 Sales       | Sneha | 150000.00
(3 rows)
```

**Common mistakes:**

- ❌ Filtering on a window function in `WHERE`. ✅ Wrap it in a CTE.
- ❌ `row_number()` when ties should share a place (use `rank` or `dense_rank`).
- ❌ Forgetting `ORDER BY` inside `OVER` for running totals (you get the group total on every row).
- ❌ `last_value()` surprises: the default frame ends at the current row. Add `ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING`.

### Practice

1. Number each customer's orders in date order (1 = their first order).
2. Find the second-highest salary using `dense_rank`.

<details>
<summary><b>Answer</b></summary>

```sql
SELECT c.name, o.ordered_at,
       row_number() OVER (PARTITION BY o.customer_id ORDER BY o.ordered_at) AS nth_order
FROM orders o JOIN customers c ON c.id = o.customer_id
WHERE c.name IN ('Asha', 'Ravi')
ORDER BY c.name, nth_order;

WITH r AS (SELECT salary, dense_rank() OVER (ORDER BY salary DESC) AS dr FROM employees)
SELECT DISTINCT salary AS second_highest FROM r WHERE dr = 2;
```

**Output:**

```text
 name | ordered_at | nth_order
------+------------+-----------
 Asha | 2025-01-05 |         1
 Asha | 2025-02-10 |         2
 Asha | 2025-03-20 |         3
 Ravi | 2025-01-06 |         1
 Ravi | 2025-04-18 |         2
(5 rows)

 second_highest
----------------
      180000.00
(1 row)
```

</details>

| # | Practice problem | Level |
|---|---|---|
| 1 | [LeetCode 176. Second Highest Salary](https://leetcode.com/problems/second-highest-salary/) | 🟡 Medium |
| 2 | [LeetCode 178. Rank Scores](https://leetcode.com/problems/rank-scores/) | 🟡 Medium |
| 3 | [LeetCode 180. Consecutive Numbers](https://leetcode.com/problems/consecutive-numbers/) | 🟡 Medium |
| 4 | [LeetCode 1321. Restaurant Growth](https://leetcode.com/problems/restaurant-growth/) (moving average) | 🟡 Medium |
| 5 | [LeetCode 185. Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries/) | 🔴 Hard |

---

### ✅ Part 3 checkpoint

Without looking, can you:

- [ ] Add primary keys, foreign keys (with a chosen `ON DELETE`), `UNIQUE`, `NOT NULL` and `CHECK` constraints?
- [ ] Model one-to-many and many-to-many relationships, and explain 1NF, 2NF and 3NF with examples?
- [ ] Change a table with `ALTER TABLE`, and describe a zero-downtime migration?
- [ ] Explain the difference between a view and a materialized view?
- [ ] Rank rows within groups, compute a running total, compare with the previous row, and get the top N per group?

**Learn more:** [PostgreSQL docs: Window functions tutorial](https://www.postgresql.org/docs/current/tutorial-window.html)

---

# Part 4 — Moderate: Transactions and Performance

> **Goal:** Keep data correct under concurrency, and make queries fast with indexes and query plans.  
> **You need:** Parts 1–3.

---

## 17. Transactions, ACID and Concurrency

![A transfer is all-or-nothing; MVCC lets readers see a consistent snapshot while a writer works](images/sql/12-transactions.svg)

### Theory

> **In simple words:** a **transaction** groups several changes into one **all-or-nothing** unit. Moving ₹500 from Asha to Ravi is two updates (subtract, add); a transaction guarantees you never end up with only one of them done, even if the server crashes halfway.

```text
BEGIN;
UPDATE accounts SET balance = balance - 500 WHERE owner = 'Asha';
UPDATE accounts SET balance = balance + 500 WHERE owner = 'Ravi';
COMMIT;        -- both changes become permanent together (or ROLLBACK to undo both)
```

**ACID: the four promises of a transaction.**

| Letter | Promise | In plain words |
|---|---|---|
| **A**tomicity | All or nothing | If anything fails, every change in the transaction is undone |
| **C**onsistency | Rules hold | Constraints are satisfied before and after (no negative balance if a `CHECK` forbids it) |
| **I**solation | Transactions don't trip over each other | Running at the same time gives sensible results (how sensible depends on the isolation level) |
| **D**urability | Committed means saved | After `COMMIT` returns, the change survives a crash (PostgreSQL writes it to the write-ahead log, the **WAL**, first) |

**Without `BEGIN`, every statement is its own transaction** ("autocommit"). **Savepoints** let you undo part of a transaction: `SAVEPOINT s1; ... ROLLBACK TO s1;`. If any statement fails inside a transaction, PostgreSQL marks the whole transaction as failed, and only `ROLLBACK` (or `ROLLBACK TO` a savepoint) gets you out.

**How PostgreSQL lets many people work at once: MVCC.** With **multi-version concurrency control**, an update doesn't overwrite a row in place; it writes a **new version** of it. Each transaction sees a consistent **snapshot** of the versions that were committed when it started (or when each statement started). So:

- **Readers never block writers, and writers never block readers.**
- Two writers updating the **same row** do wait for each other: the second waits until the first commits or rolls back.
- Old row versions pile up and are cleaned later by **VACUUM** (Section [29](#29-running-postgresql-backups-replication-vacuum-partitioning-and-monitoring)).

**Isolation levels** decide which "anomalies" you can see when transactions overlap:

| Level | Prevents | Still possible | PostgreSQL notes |
|---|---|---|---|
| Read Committed (**default**) | Dirty reads (seeing uncommitted data) | Non-repeatable reads, lost updates in read-modify-write code | Each **statement** sees a fresh snapshot |
| Repeatable Read | + non-repeatable reads, phantoms | Some rare "write skew" cases | The whole **transaction** sees one snapshot; conflicting updates fail with a serialization error |
| Serializable | Everything: results as if transactions ran one at a time | — | May abort transactions with a serialization error; the app must **retry** them |

**The lost-update problem.** Two requests both read `stock = 10`, both compute `10 - 1`, and both write `9`: one sale vanished. Fixes, from simplest:

1. Let the database do the arithmetic in one statement: `UPDATE products SET stock = stock - 1 WHERE id = 5 AND stock > 0` (atomic).
2. Lock the row while you work on it: `SELECT ... FOR UPDATE` inside a transaction.
3. **Optimistic locking:** keep a `version` column and update `WHERE id = 5 AND version = 7`; if 0 rows change, someone else won, so retry.
4. Use `SERIALIZABLE` and retry on errors.

**Job queues in Postgres: `FOR UPDATE SKIP LOCKED`.** Several workers each run `SELECT ... FROM jobs WHERE status = 'queued' ORDER BY id LIMIT 1 FOR UPDATE SKIP LOCKED`, and each gets a **different** job, because rows locked by other workers are skipped instead of waited on. Many real job systems work this way.

**Deadlocks.** Transaction A locks row 1 and wants row 2; B locks row 2 and wants row 1: both wait forever. PostgreSQL detects this after about a second and aborts one of them. Prevent it by always locking rows **in the same order** (for example, by ID), and keep transactions **short**.

### SQL

```sql
CREATE TABLE accounts (
    owner   text PRIMARY KEY,
    balance numeric(12, 2) NOT NULL CHECK (balance >= 0)
);
INSERT INTO accounts VALUES ('Asha', 1000), ('Ravi', 200);

-- a transfer that fails halfway is completely undone
BEGIN;
UPDATE accounts SET balance = balance + 5000 WHERE owner = 'Ravi';
UPDATE accounts SET balance = balance - 5000 WHERE owner = 'Asha';   -- violates the CHECK
COMMIT;                                                              -- becomes a ROLLBACK
SELECT * FROM accounts ORDER BY owner;
```

**Output:**

```text
ERROR:  new row for relation "accounts" violates check constraint "accounts_balance_check"
DETAIL:  Failing row contains (Asha, -4000.00).
 owner | balance
-------+---------
 Asha  | 1000.00
 Ravi  |  200.00
(2 rows)
```

Ravi did **not** keep the 5,000: the failed statement aborted the transaction, and `COMMIT` on an aborted transaction rolls everything back.

```sql
BEGIN;
UPDATE accounts SET balance = balance - 300 WHERE owner = 'Asha';
SAVEPOINT before_bonus;
UPDATE accounts SET balance = balance + 1000 WHERE owner = 'Ravi';   -- a mistake
ROLLBACK TO before_bonus;                                            -- undo just that part
UPDATE accounts SET balance = balance + 300 WHERE owner = 'Ravi';
COMMIT;
SELECT * FROM accounts ORDER BY owner;
```

**Output:**

```text
 owner | balance
-------+---------
 Asha  |  700.00
 Ravi  |  500.00
(2 rows)
```

```sql
-- a job queue: each worker claims a different job with SKIP LOCKED
CREATE TABLE jobs (id int PRIMARY KEY, task text, status text NOT NULL DEFAULT 'queued');
INSERT INTO jobs (id, task) VALUES (1, 'send email'), (2, 'resize image'), (3, 'build report');

BEGIN;
SELECT id, task FROM jobs WHERE status = 'queued'
ORDER BY id LIMIT 1
FOR UPDATE SKIP LOCKED;          -- worker 1 claims job 1; others would skip it
UPDATE jobs SET status = 'done' WHERE id = 1;
COMMIT;
SELECT * FROM jobs ORDER BY id;
DROP TABLE jobs;
```

**Output:**

```text
 id |    task
----+------------
  1 | send email
(1 row)

 id |     task     | status
----+--------------+--------
  1 | send email   | done
  2 | resize image | queued
  3 | build report | queued
(3 rows)
```

(With a second connection, a second worker running the same `SELECT` while the first transaction is open would get job 2 instead of waiting.)

<!-- no-run -->
```sql
-- setting an isolation level for one transaction
BEGIN ISOLATION LEVEL SERIALIZABLE;
-- ... reads and writes ...
COMMIT;   -- may fail with "could not serialize access": catch it in the app and retry
```

**Common mistakes:**

- ❌ Read-modify-write in application code (`read stock`, compute, `write stock`) without a lock or an atomic `UPDATE`.
- ❌ Long transactions (waiting for a user or an HTTP call while holding locks). They block others and stop VACUUM from cleaning up.
- ❌ Using `SERIALIZABLE` without retry logic.
- ❌ Locking rows in different orders in different code paths (deadlocks).

### Practice

1. Write the SQL that sells one unit of product 5 safely, without ever letting stock go below 0, in a single statement. How do you know if it failed?

<details>
<summary><b>Answer</b></summary>

```sql
UPDATE products SET stock = stock - 1
WHERE id = 5 AND stock > 0
RETURNING stock;
```

**Output:**

```text
 stock
-------
    14
(1 row)
```

If no row comes back (`UPDATE 0`), the product was out of stock. The check and the change happen atomically, so two buyers can't both take the last unit.

</details>

**Learn more:** [PostgreSQL docs: Transaction isolation](https://www.postgresql.org/docs/current/transaction-iso.html) · [PostgreSQL docs: Explicit locking](https://www.postgresql.org/docs/current/explicit-locking.html)

---

## 18. Indexes: Making Lookups Fast

![A B-tree index: sorted keys in a few wide levels, pointing to rows in the table](images/sql/13-btree-index.svg)

### Theory

> **In simple words:** an index is like the index at the back of a book. Without it, finding every mention of "Dijkstra" means reading every page (a **sequential scan**). With it, you look up the word and jump straight to the right pages. The price: the index takes space, and every insert or update must also update it.

**How the default index works: a B-tree.** `CREATE INDEX ON orders (customer_id)` builds a **B-tree**: the `customer_id` values sorted in a shallow tree of wide pages, each value pointing to the row's location in the table (the DSA notes explain B-trees in their real-systems section). Looking up one value touches 3–4 pages even in a table of millions of rows, and because the values are **sorted**, the same index also speeds up ranges (`>`, `<`, `BETWEEN`), `ORDER BY` and `min`/`max`.

**What gets indexed automatically:** primary keys and `UNIQUE` columns. **Not** foreign keys: add those yourself.

**Composite (multi-column) indexes: order matters.** An index on `(customer_id, ordered_at)` is sorted by customer first, then by date within each customer (like a phone book: surname, then first name). It helps:

- `WHERE customer_id = 5`
- `WHERE customer_id = 5 AND ordered_at >= '2025-01-01'`
- `WHERE customer_id = 5 ORDER BY ordered_at DESC`

but **not** `WHERE ordered_at >= '2025-01-01'` alone (like finding everyone named "Ravi" in a phone book sorted by surname). The rule of thumb: put **equality** columns first, then the **range or sort** column.

**Other useful kinds:**

| Index | For | Example |
|---|---|---|
| **Unique** | Enforcing uniqueness | `CREATE UNIQUE INDEX ON users (lower(email))` |
| **Partial** | Only some rows (smaller, faster) | `CREATE INDEX ON orders (ordered_at) WHERE status = 'pending'` |
| **Expression** | A computed value you search on | `CREATE INDEX ON customers (lower(email))` for `WHERE lower(email) = ...` |
| **Covering** (`INCLUDE`) | Answering a query from the index alone ("index-only scan") | `CREATE INDEX ON orders (customer_id) INCLUDE (status)` |
| **GIN** | Values **inside** a column: JSONB keys, array elements, full-text words | Sections [21](#21-json-and-jsonb-documents-inside-postgresql), [23](#23-full-text-search) |
| **GiST** | Geometric data, ranges, nearest-neighbour | PostGIS locations, `tsrange` overlaps |
| **BRIN** | Huge tables whose values follow physical order (time series) | A tiny index on `created_at` of an append-only log |
| **HNSW / IVFFlat** (pgvector) | Vector similarity | Section [26](#26-pgvector-vector-search-for-ai-applications) |

**When indexes don't help (or hurt):**

- Small tables: reading everything is faster than using the index.
- Conditions matching a big fraction of the rows (`WHERE status <> 'cancelled'` on 95% of the table): a sequential scan wins.
- Functions or casts on the column: `WHERE lower(email) = ...` can't use a plain index on `email` (use an expression index), and neither can `WHERE date(created_at) = ...`.
- `LIKE '%term'` (leading wildcard) can't use a B-tree (a trigram GIN index from the `pg_trgm` extension can).
- **Every index slows writes** and uses disk. Drop indexes nobody uses (`pg_stat_user_indexes` shows usage).

**Creating indexes on a live system:** `CREATE INDEX CONCURRENTLY` builds without blocking writes (slower, and can't run inside a transaction).

### SQL

```sql
-- a bigger table so the difference is visible: 200,000 page views
CREATE TABLE page_views (
    id          bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    user_id     int NOT NULL,
    url         text NOT NULL,
    viewed_at   timestamptz NOT NULL
);
INSERT INTO page_views (user_id, url, viewed_at)
SELECT (i % 5000) + 1,
       '/page/' || (i % 300),
       timestamptz '2025-01-01' + (i * interval '1 minute')
FROM generate_series(1, 200000) AS i;
ANALYZE page_views;                      -- update the planner's statistics

EXPLAIN (COSTS OFF) SELECT * FROM page_views WHERE user_id = 42;
```

**Output:**

```text
        QUERY PLAN
--------------------------
 Seq Scan on page_views
   Filter: (user_id = 42)
(2 rows)
```

```sql
CREATE INDEX page_views_user_time_idx ON page_views (user_id, viewed_at);

EXPLAIN (COSTS OFF) SELECT * FROM page_views WHERE user_id = 42;
EXPLAIN (COSTS OFF) SELECT * FROM page_views WHERE user_id = 42 ORDER BY viewed_at DESC LIMIT 5;
EXPLAIN (COSTS OFF) SELECT * FROM page_views WHERE viewed_at >= '2025-03-01' AND viewed_at < '2025-03-02';
```

**Output:**

```text
                     QUERY PLAN
-----------------------------------------------------
 Bitmap Heap Scan on page_views
   Recheck Cond: (user_id = 42)
   ->  Bitmap Index Scan on page_views_user_time_idx
         Index Cond: (user_id = 42)
(4 rows)

                               QUERY PLAN
------------------------------------------------------------------------
 Limit
   ->  Index Scan Backward using page_views_user_time_idx on page_views
         Index Cond: (user_id = 42)
(3 rows)

                                                                        QUERY PLAN
----------------------------------------------------------------------------------------------------------------------------------------------------------
 Gather
   Workers Planned: 1
   ->  Parallel Seq Scan on page_views
         Filter: ((viewed_at >= '2025-03-01 00:00:00+00'::timestamp with time zone) AND (viewed_at < '2025-03-02 00:00:00+00'::timestamp with time zone))
(4 rows)
```

The first two queries use the index (the second even reads it backwards to get the latest rows without sorting). The third filters only on the **second** column of the index, so PostgreSQL falls back to scanning the whole table.

```sql
CREATE INDEX page_views_time_idx ON page_views (viewed_at);
EXPLAIN (COSTS OFF) SELECT * FROM page_views WHERE viewed_at >= '2025-03-01' AND viewed_at < '2025-03-02';

-- a function on the column hides it from the index
EXPLAIN (COSTS OFF) SELECT count(*) FROM page_views WHERE date(viewed_at AT TIME ZONE 'UTC') = '2025-03-01';

SELECT pg_size_pretty(pg_relation_size('page_views')) AS table_size,
       pg_size_pretty(pg_relation_size('page_views_user_time_idx')) AS index_size;
```

**Output:**

```text
                                                                       QUERY PLAN
--------------------------------------------------------------------------------------------------------------------------------------------------------
 Index Scan using page_views_time_idx on page_views
   Index Cond: ((viewed_at >= '2025-03-01 00:00:00+00'::timestamp with time zone) AND (viewed_at < '2025-03-02 00:00:00+00'::timestamp with time zone))
(2 rows)

                                          QUERY PLAN
-----------------------------------------------------------------------------------------------
 Finalize Aggregate
   ->  Gather
         Workers Planned: 1
         ->  Partial Aggregate
               ->  Parallel Seq Scan on page_views
                     Filter: (date((viewed_at AT TIME ZONE 'UTC'::text)) = '2025-03-01'::date)
(6 rows)

 table_size | index_size
------------+------------
 11 MB      | 6184 kB
(1 row)
```

**Common mistakes:**

- ❌ No index on foreign-key columns used in joins and filters.
- ❌ A composite index in the wrong column order for your queries.
- ❌ Indexing every column "just in case" (slower writes, wasted space).
- ❌ Wrapping indexed columns in functions in `WHERE`.
- ❌ Building an index without `CONCURRENTLY` on a busy production table.

### Practice

1. Which index would you create for `SELECT * FROM orders WHERE status = 'pending' ORDER BY ordered_at LIMIT 20` if only 1% of orders are pending?
2. Why doesn't an index on `(user_id, viewed_at)` help `WHERE viewed_at > ...`?

<details>
<summary><b>Answer</b></summary>

1. A partial index: `CREATE INDEX ON orders (ordered_at) WHERE status = 'pending';` It's tiny (1% of rows), already sorted by date, and matches the query's condition.
2. The index is sorted by `user_id` first; rows with a given `viewed_at` are scattered across every user's section, so there's no single range to read.

</details>

| # | Practice problem | Level |
|---|---|---|
| 1 | [Use The Index, Luke!](https://use-the-index-luke.com/) — a free, excellent book on SQL indexing | 🟡 Medium |
| 2 | Run `EXPLAIN` on your own slow query and add the index it needs | 🟡 Medium |

**Learn more:** [PostgreSQL docs: Indexes](https://www.postgresql.org/docs/current/indexes.html)

---

## 19. Reading Query Plans with EXPLAIN

![A query plan is a tree: rows flow up from scans at the leaves, through joins and sorts, to the result at the top](images/sql/14-query-plan.svg)

### Theory

> **In simple words:** before running a query, PostgreSQL's **planner** picks a strategy: which index to use, which table to read first, how to join them. `EXPLAIN` shows you that strategy (the **plan**), and `EXPLAIN ANALYZE` actually runs the query and shows what really happened. It's the most important tool for fixing slow queries.

**How to read a plan.** It's a tree printed with indentation. Rows flow **upwards**: the most-indented lines (scans that read tables) run first, and each `->` node feeds the node above it.

**The scan nodes (how a table is read):**

| Node | Means | Good when |
|---|---|---|
| **Seq Scan** | Read the whole table, top to bottom | Small tables, or when most rows match |
| **Index Scan** | Walk the index, fetch each matching row | Few rows match, or rows are needed in index order |
| **Index Only Scan** | Answer from the index alone, never touching the table | All needed columns are in the index (and the table is vacuumed) |
| **Bitmap Index Scan → Bitmap Heap Scan** | Collect matching row locations from the index, then fetch them in physical order | A moderate number of matches; can combine several indexes |

**The join nodes (how two inputs are combined).** They're the algorithms from the DSA notes:

| Node | How | Best for |
|---|---|---|
| **Nested Loop** | For each row on one side, look up matches on the other (ideally via an index) | One side is small |
| **Hash Join** | Build a hash table from the smaller side, then probe it with each row of the other (DSA: hashing) | Big, unsorted inputs joined on `=` |
| **Merge Join** | Walk two inputs sorted on the join key side by side (DSA: two pointers, merge step) | Inputs already sorted (for example, via indexes) |

**Other common nodes:** `Sort`, `HashAggregate` / `GroupAggregate` (for `GROUP BY`), `Limit`, and `Gather` (combines the work of **parallel** workers).

**Costs and estimates.** Plain `EXPLAIN` shows `cost=startup..total rows=estimated_rows`. Costs are in arbitrary units, useful only for comparing plans. The row estimates come from **statistics** that `ANALYZE` collects (autovacuum runs it automatically). **If estimated rows and actual rows differ by a lot, the planner is working with bad information**; running `ANALYZE` (or increasing the statistics target for a column) is often the fix.

**Useful forms:**

- `EXPLAIN query` — the plan only, nothing runs.
- `EXPLAIN (ANALYZE, BUFFERS) query` — runs it: real time per node, real row counts, and how many pages were read from memory or disk. (Careful: `ANALYZE` really executes `INSERT`/`UPDATE`/`DELETE`; wrap those in `BEGIN ... ROLLBACK`.)
- The examples below add `COSTS OFF`, `TIMING OFF` and `SUMMARY OFF` only so the output is identical on every run.

**Reading checklist for a slow query:** find the node with the most time (or the most rows); look for a `Seq Scan` on a big table with a selective filter (missing index); look for estimate vs actual mismatches; look for `Sort` spilling to disk ("external merge", fix with an index or more `work_mem`); and check `loops=` on nested loops (a small cost times a million loops is a big cost).

**Tools:** [explain.dalibo.com](https://explain.dalibo.com/) and [explain.depesz.com](https://explain.depesz.com/) draw plans as readable diagrams.

### SQL

```sql
VACUUM ANALYZE page_views;     -- refresh statistics and the visibility map (enables index-only scans)

EXPLAIN (ANALYZE, COSTS OFF, TIMING OFF, SUMMARY OFF)
SELECT user_id, viewed_at FROM page_views WHERE user_id = 7 AND viewed_at < '2025-02-01';
```

**Output:**

```text
                                             QUERY PLAN
----------------------------------------------------------------------------------------------------
 Index Only Scan using page_views_user_time_idx on page_views (actual rows=9 loops=1)
   Index Cond: ((user_id = 7) AND (viewed_at < '2025-02-01 00:00:00+00'::timestamp with time zone))
   Heap Fetches: 0
(3 rows)
```

An **Index Only Scan**: both columns are in the `(user_id, viewed_at)` index, so the table itself is never read (`Heap Fetches: 0`).

```sql
EXPLAIN (COSTS OFF)
SELECT c.name, count(*)
FROM customers c
JOIN orders o ON o.customer_id = c.id
GROUP BY c.name;
```

**Output:**

```text
                QUERY PLAN
-------------------------------------------
 HashAggregate
   Group Key: c.name
   ->  Hash Join
         Hash Cond: (o.customer_id = c.id)
         ->  Seq Scan on orders o
         ->  Hash
               ->  Seq Scan on customers c
(7 rows)
```

Read it bottom-up: scan `orders`, build a hash table from `customers`, join by hashing, then group with another hash table.

<!-- no-check -->
```sql
-- estimates vs reality: the planner guesses well here because statistics are fresh
EXPLAIN (ANALYZE, TIMING OFF, SUMMARY OFF)
SELECT count(*) FROM page_views WHERE url = '/page/7';
```

**Output:**

```text
                                          QUERY PLAN
-----------------------------------------------------------------------------------------------
 Aggregate  (cost=3972.66..3972.67 rows=1 width=8) (actual rows=1 loops=1)
   ->  Seq Scan on page_views  (cost=0.00..3971.00 rows=664 width=0) (actual rows=667 loops=1)
         Filter: (url = '/page/7'::text)
         Rows Removed by Filter: 199333
(4 rows)
```

(Exact numbers vary from run to run, which is why this output isn't checked. Compare the `rows=` in the estimate with the actual `rows=`: close is good.)

**Common mistakes:**

- ❌ Guessing at performance instead of reading the plan.
- ❌ Running `EXPLAIN ANALYZE` on a `DELETE` outside a transaction (it really deletes).
- ❌ Judging a plan on a tiny development database: plans change with data size. Test with realistic volumes.
- ❌ Forgetting `ANALYZE` after bulk-loading data.

### Practice

1. Run `EXPLAIN` on a query that filters `page_views` by `url`. Which scan do you get? Create an index on `url` and compare.

<details>
<summary><b>Answer</b></summary>

```sql
EXPLAIN (COSTS OFF) SELECT count(*) FROM page_views WHERE url = '/page/7';
CREATE INDEX page_views_url_idx ON page_views (url);
EXPLAIN (COSTS OFF) SELECT count(*) FROM page_views WHERE url = '/page/7';
DROP INDEX page_views_url_idx;
```

**Output:**

```text
               QUERY PLAN
-----------------------------------------
 Aggregate
   ->  Seq Scan on page_views
         Filter: (url = '/page/7'::text)
(3 rows)

                          QUERY PLAN
--------------------------------------------------------------
 Aggregate
   ->  Index Only Scan using page_views_url_idx on page_views
         Index Cond: (url = '/page/7'::text)
(3 rows)
```

</details>

**Learn more:** [PostgreSQL docs: Using EXPLAIN](https://www.postgresql.org/docs/current/using-explain.html)

---

## 20. Making Queries Fast: Common Performance Patterns

### Theory

> **In simple words:** most slow database code comes from a handful of repeated mistakes: asking the database too many small questions, reading far more rows than needed, or hiding columns from indexes. Fix those and most apps are fast enough.

**1. The N+1 query problem.** Code loads 100 orders (1 query), then loops and loads each order's customer (100 more queries): 101 round trips. Each round trip costs network time, so this is slow even when every query is fast. ORMs (Section [28](#28-using-postgresql-from-python-psycopg-pooling-and-sqlalchemy)) cause it easily with "lazy loading". **Fix:** one query with a `JOIN`, or one query with `WHERE id = ANY(list_of_ids)`, or the ORM's eager-loading option.

**2. Pagination: keyset beats OFFSET.** `ORDER BY id LIMIT 20 OFFSET 100000` makes the database produce and throw away 100,000 rows before returning 20, and it gets slower on every page. **Keyset (cursor) pagination** remembers the last row seen and asks for the next ones: `WHERE id > :last_id ORDER BY id LIMIT 20`. With an index on the sort column it's equally fast on page 1 and page 10,000. (It also doesn't skip or repeat rows when new rows are inserted between page loads.)

**3. Make conditions "sargable"** (able to use an index): don't wrap the indexed column in functions or arithmetic.

| ❌ Can't use an index on the column | ✅ Can |
|---|---|
| `WHERE date(created_at) = '2025-03-01'` | `WHERE created_at >= '2025-03-01' AND created_at < '2025-03-02'` |
| `WHERE price * 1.18 > 1000` | `WHERE price > 1000 / 1.18` |
| `WHERE lower(email) = 'a@b.com'` | the same, **plus** an expression index on `lower(email)` |
| `WHERE name LIKE '%sha'` | `WHERE name LIKE 'Ash%'` (prefix), or a trigram index |

**4. Read only what you need.** `SELECT *` fetches every column (including large text and JSON), prevents index-only scans, and breaks code when columns are added. Name the columns.

**5. "Does any row exist?" → `EXISTS`, not `count(*)`.** `count(*)` must count every match; `EXISTS` stops at the first one.

**6. Batch writes.** Insert many rows with one multi-row `INSERT` or `COPY` (Section [25](#25-upserts-merge-and-bulk-loading)), not thousands of single-row inserts in separate transactions.

**7. Big `IN` lists and `OR` across different columns** can confuse the planner. `= ANY(array)` handles big lists well; `OR` across columns can be rewritten as `UNION` of two indexed queries.

**8. Find the slow queries first.** Enable the `pg_stat_statements` extension: it records every query shape with its total time, call count and mean time. Sort by total time and fix the top few: that's where the wins are. Also set `log_min_duration_statement` to log any query slower than, say, 500 ms.

**9. Outside the query:** keep connections pooled (PgBouncer, Section [28](#28-using-postgresql-from-python-psycopg-pooling-and-sqlalchemy)), cache results that don't change often (Redis, materialized views), add read replicas for read-heavy apps (Section [29](#29-running-postgresql-backups-replication-vacuum-partitioning-and-monitoring)), and keep tables vacuumed.

### SQL

```sql
-- OFFSET pagination reads and discards rows; keyset pagination jumps straight there
EXPLAIN (ANALYZE, COSTS OFF, TIMING OFF, SUMMARY OFF)
SELECT id, url FROM page_views ORDER BY id LIMIT 5 OFFSET 150000;

EXPLAIN (ANALYZE, COSTS OFF, TIMING OFF, SUMMARY OFF)
SELECT id, url FROM page_views WHERE id > 150000 ORDER BY id LIMIT 5;
```

**Output:**

```text
                                    QUERY PLAN
-----------------------------------------------------------------------------------
 Limit (actual rows=5 loops=1)
   ->  Index Scan using page_views_pkey on page_views (actual rows=150005 loops=1)
(2 rows)

                                  QUERY PLAN
------------------------------------------------------------------------------
 Limit (actual rows=5 loops=1)
   ->  Index Scan using page_views_pkey on page_views (actual rows=5 loops=1)
         Index Cond: (id > 150000)
(3 rows)
```

Look at the actual `rows=`: the OFFSET version pulls 150,005 rows through the index to return 5; the keyset version touches just 5.

<!-- no-check -->
```sql
-- EXISTS stops at the first match; count(*) visits them all
EXPLAIN (ANALYZE, COSTS OFF, TIMING OFF, SUMMARY OFF)
SELECT count(*) > 0 FROM page_views WHERE url = '/page/7';

EXPLAIN (ANALYZE, COSTS OFF, TIMING OFF, SUMMARY OFF)
SELECT EXISTS (SELECT 1 FROM page_views WHERE url = '/page/7');
```

**Output:**

```text
                       QUERY PLAN
--------------------------------------------------------
 Aggregate (actual rows=1 loops=1)
   ->  Seq Scan on page_views (actual rows=667 loops=1)
         Filter: (url = '/page/7'::text)
         Rows Removed by Filter: 199333
(4 rows)

                       QUERY PLAN
--------------------------------------------------------
 Result (actual rows=1 loops=1)
   InitPlan 1 (returns $0)
     ->  Seq Scan on page_views (actual rows=1 loops=1)
           Filter: (url = '/page/7'::text)
           Rows Removed by Filter: 6
(5 rows)
```

The `count` plan reads all 200,000 rows (`Rows Removed by Filter: 199333`); the `EXISTS` plan stops at the first match, after looking at just 7 rows. (Plans like these can change between runs and versions, so this output isn't checked automatically.)

```sql
-- one query instead of N+1: all the customers for a list of order IDs at once
SELECT o.id AS order_id, c.name
FROM orders o
JOIN customers c ON c.id = o.customer_id
WHERE o.id = ANY (ARRAY[1, 4, 7])
ORDER BY o.id;
```

**Output:**

```text
 order_id | name
----------+-------
        1 | Asha
        4 | Meera
        7 | Asha
(3 rows)
```

**Common mistakes:**

- ❌ Optimising without measuring (`pg_stat_statements` and `EXPLAIN ANALYZE` first).
- ❌ Deep `OFFSET` pagination in APIs and infinite scroll.
- ❌ Queries inside loops in application code.
- ❌ Adding indexes blindly instead of for specific, measured queries.

### Practice

1. Rewrite `SELECT * FROM page_views WHERE extract(month from viewed_at) = 3 AND extract(year from viewed_at) = 2025` so it can use the index on `viewed_at`.

<details>
<summary><b>Answer</b></summary>

```sql
EXPLAIN (COSTS OFF)
SELECT count(*) FROM page_views
WHERE viewed_at >= '2025-03-01' AND viewed_at < '2025-04-01';
```

**Output:**

```text
                                                                          QUERY PLAN
--------------------------------------------------------------------------------------------------------------------------------------------------------------
 Aggregate
   ->  Index Only Scan using page_views_time_idx on page_views
         Index Cond: ((viewed_at >= '2025-03-01 00:00:00+00'::timestamp with time zone) AND (viewed_at < '2025-04-01 00:00:00+00'::timestamp with time zone))
(3 rows)
```

A range on the raw column is "sargable": PostgreSQL answers the count straight from the `viewed_at` index. (When a range covers a large share of a table, the planner may still pick a sequential scan: it chooses based on how many rows match.)

</details>

---

### ✅ Part 4 checkpoint

Without looking, can you:

- [ ] Explain ACID and MVCC, and what happens to a transaction after one statement fails?
- [ ] Prevent lost updates with an atomic `UPDATE`, `SELECT ... FOR UPDATE` or optimistic locking?
- [ ] Choose the column order for a composite index, and name three situations where an index can't be used?
- [ ] Read a plan: Seq Scan vs Index Scan vs Index Only Scan, Nested Loop vs Hash Join?
- [ ] Fix N+1 queries and deep-OFFSET pagination?

**Learn more:** [pg_stat_statements](https://www.postgresql.org/docs/current/pgstatstatements.html) · [Use The Index, Luke!: Pagination](https://use-the-index-luke.com/no-offset)

---

# Part 5 — Advanced: PostgreSQL Power Features

> **Goal:** Use what makes PostgreSQL special: JSONB, arrays and ranges, full-text search, functions and triggers, upserts and bulk loading, and pgvector for AI.  
> **You need:** Parts 1–4.

---

## 21. JSON and JSONB: Documents Inside PostgreSQL

![A jsonb column holds a document; operators reach into it, and a GIN index makes searching it fast](images/sql/15-jsonb.svg)

### Theory

> **In simple words:** sometimes data doesn't fit fixed columns: each product has different attributes (a laptop has RAM, a shirt has a size), or you store an event payload from another system. A `jsonb` column stores a whole JSON document in one cell, and PostgreSQL can still search inside it quickly.

**`json` vs `jsonb`:** `json` stores the text exactly as given; **`jsonb`** stores a parsed, binary version: slightly slower to write, much faster to query, and it can be indexed. **Use `jsonb`.**

**Reading inside a document:**

| Operator | Returns | Example | Result |
|---|---|---|---|
| `->` | A JSON value (still jsonb) | `attrs -> 'dimensions'` | `{"w": 30, "h": 45}` |
| `->>` | **Text** | `attrs ->> 'color'` | `black` |
| `#>` / `#>>` | JSON / text at a path | `attrs #>> '{dimensions,w}'` | `30` |
| `@>` | Contains? | `attrs @> '{"color": "black"}'` | true/false |
| `?` | Has this key? | `attrs ? 'wireless'` | true/false |

Cast text results to use them as numbers: `(attrs ->> 'battery_hours')::int > 20`.

**Changing documents:** `jsonb_set(doc, '{path}', new_value)` replaces a value, `doc || '{"new": 1}'` merges keys in, and `doc - 'key'` removes a key.

**Building JSON from tables:** `jsonb_build_object('name', name, 'price', price)` and `jsonb_agg(...)` turn rows into JSON, handy for APIs returning nested data in one query.

**Indexing:** a **GIN** index on the column (`CREATE INDEX ON products_ext USING gin (attrs)`) makes `@>` and `?` searches fast. For one frequently-used key, an expression index is smaller: `CREATE INDEX ON products_ext ((attrs ->> 'color'))`.

**JSONB or columns?** Use real columns for data that every row has, that you filter, join or constrain often, or that needs types and foreign keys. Use `jsonb` for genuinely variable or sparse attributes, raw payloads from other systems, and user preferences. A table that's "all JSON" throws away most of what makes a relational database useful. (PostgreSQL 16 added SQL/JSON constructors like `JSON_OBJECT`; PostgreSQL 17 added `JSON_TABLE`, which turns JSON into rows and columns.)

### SQL

```sql
CREATE TABLE products_ext (
    id    int PRIMARY KEY,
    name  text NOT NULL,
    attrs jsonb NOT NULL DEFAULT '{}'
);
INSERT INTO products_ext VALUES
    (1, 'Headphones', '{"color": "black", "wireless": true, "battery_hours": 30, "tags": ["audio", "bluetooth"]}'),
    (2, 'Keyboard',   '{"color": "white", "wireless": false, "layout": "US", "dimensions": {"w": 44, "h": 13}}'),
    (3, 'Desk lamp',  '{"color": "black", "wattage": 9, "dimensions": {"w": 15, "h": 45}}');

SELECT name,
       attrs ->> 'color'                AS color,
       attrs #>> '{dimensions,h}'       AS height,
       (attrs ->> 'battery_hours')::int AS battery
FROM products_ext
ORDER BY id;
```

**Output:**

```text
    name    | color | height | battery
------------+-------+--------+---------
 Headphones | black | (null) |      30
 Keyboard   | white | 13     |  (null)
 Desk lamp  | black | 45     |  (null)
(3 rows)
```

```sql
SELECT name FROM products_ext WHERE attrs @> '{"color": "black"}' ORDER BY name;   -- containment
SELECT name FROM products_ext WHERE attrs ? 'dimensions' ORDER BY name;          -- has key
SELECT name FROM products_ext WHERE attrs -> 'tags' ? 'bluetooth';               -- array element
```

**Output:**

```text
    name
------------
 Desk lamp
 Headphones
(2 rows)

   name
-----------
 Desk lamp
 Keyboard
(2 rows)

    name
------------
 Headphones
(1 row)
```

```sql
UPDATE products_ext
SET attrs = jsonb_set(attrs, '{battery_hours}', '40') || '{"warranty_years": 2}'
WHERE id = 1
RETURNING attrs;

-- rows → JSON for an API response
SELECT jsonb_agg(jsonb_build_object('id', id, 'name', name) ORDER BY id) AS items
FROM products_ext;
```

**Output:**

```text
                                                     attrs
----------------------------------------------------------------------------------------------------------------
 {"tags": ["audio", "bluetooth"], "color": "black", "wireless": true, "battery_hours": 40, "warranty_years": 2}
(1 row)

                                              items
--------------------------------------------------------------------------------------------------
 [{"id": 1, "name": "Headphones"}, {"id": 2, "name": "Keyboard"}, {"id": 3, "name": "Desk lamp"}]
(1 row)
```

```sql
CREATE INDEX products_ext_attrs_gin ON products_ext USING gin (attrs);
SET enable_seqscan = off;                     -- only to demonstrate on this tiny table
EXPLAIN (COSTS OFF) SELECT name FROM products_ext WHERE attrs @> '{"color": "black"}';
RESET enable_seqscan;
```

**Output:**

```text
                         QUERY PLAN
------------------------------------------------------------
 Bitmap Heap Scan on products_ext
   Recheck Cond: (attrs @> '{"color": "black"}'::jsonb)
   ->  Bitmap Index Scan on products_ext_attrs_gin
         Index Cond: (attrs @> '{"color": "black"}'::jsonb)
(4 rows)
```

**Common mistakes:**

- ❌ Comparing `attrs -> 'color' = 'black'` (`->` returns JSON, not text). ✅ `attrs ->> 'color' = 'black'`.
- ❌ Putting everything in JSONB to "avoid migrations", then losing types, constraints and fast joins.
- ❌ Forgetting to cast before numeric comparisons.

### Practice

1. Find products whose `dimensions.w` is greater than 20.
2. Remove the `layout` key from the keyboard's attributes.

<details>
<summary><b>Answer</b></summary>

```sql
SELECT name FROM products_ext WHERE (attrs #>> '{dimensions,w}')::int > 20;
UPDATE products_ext SET attrs = attrs - 'layout' WHERE id = 2 RETURNING attrs;
```

**Output:**

```text
   name
----------
 Keyboard
(1 row)

                                  attrs
-------------------------------------------------------------------------
 {"color": "white", "wireless": false, "dimensions": {"h": 13, "w": 44}}
(1 row)
```

</details>

**Learn more:** [PostgreSQL docs: JSON types](https://www.postgresql.org/docs/current/datatype-json.html) · [JSON functions and operators](https://www.postgresql.org/docs/current/functions-json.html)

---

## 22. Arrays, Enums, Ranges and Generated Columns

### Theory

> **In simple words:** PostgreSQL has special column types for a few common shapes of data: a small **list** of values (arrays), a fixed **set of choices** (enums), a **span** from one value to another (ranges), and a column **calculated** from other columns (generated columns).

**Arrays** (`text[]`, `int[]`): a list in one cell.

- Literal: `ARRAY['sql', 'db']` or `'{sql,db}'`. Indexes start at **1**: `tags[1]`.
- `'sql' = ANY(tags)` (is it in the list?), `tags @> ARRAY['sql']` (contains all of these?), `array_length(tags, 1)`, `cardinality(tags)`.
- `unnest(tags)` turns an array into rows; `array_agg(x)` turns rows into an array.
- GIN indexes make `@>` searches fast.
- Good for small, simple lists that are read together (tags, roles). If you need to query or constrain individual items heavily, or they have their own attributes, use a separate table (Section [13](#13-designing-tables-relationships-and-normalisation)).

**Enums:** `CREATE TYPE order_status AS ENUM ('pending', 'shipped', 'delivered', 'cancelled');` makes a type that only accepts those values, stored compactly and sorted in the declared order. Adding a value later is easy (`ALTER TYPE ... ADD VALUE`); removing one is hard. Many teams prefer a `CHECK` constraint or a lookup table for flexibility.

**Ranges:** `int4range`, `numrange`, `daterange`, `tstzrange` store a span with inclusive `[` or exclusive `)` ends: `'[2025-03-01, 2025-03-05)'`. Operators: `@>` (contains a value), `&&` (overlaps). With an **exclusion constraint**, PostgreSQL can guarantee that no two bookings for the same room overlap, something that's very hard to get right in application code.

**Generated columns:** `total numeric GENERATED ALWAYS AS (quantity * unit_price) STORED` is computed by the database from other columns and can't be set by hand, so it can never be out of sync. (PostgreSQL 18 also supports `VIRTUAL` generated columns, computed on read, and makes them the default.)

### SQL

```sql
CREATE TABLE articles (
    id    int PRIMARY KEY,
    title text NOT NULL,
    tags  text[] NOT NULL DEFAULT '{}'
);
INSERT INTO articles VALUES
    (1, 'Intro to SQL',     ARRAY['sql', 'beginner']),
    (2, 'Postgres indexes', ARRAY['sql', 'postgres', 'performance']),
    (3, 'Python basics',    ARRAY['python', 'beginner']);

SELECT title, tags[1] AS first_tag, cardinality(tags) AS n_tags
FROM articles WHERE 'sql' = ANY (tags) ORDER BY id;

SELECT tag, count(*) FROM articles, unnest(tags) AS tag GROUP BY tag ORDER BY count(*) DESC, tag;
```

**Output:**

```text
      title       | first_tag | n_tags
------------------+-----------+--------
 Intro to SQL     | sql       |      2
 Postgres indexes | sql       |      3
(2 rows)

     tag     | count
-------------+-------
 beginner    |     2
 sql         |     2
 performance |     1
 postgres    |     1
 python      |     1
(5 rows)
```

```sql
CREATE TYPE mood AS ENUM ('sad', 'ok', 'happy');
SELECT 'happy'::mood > 'sad'::mood AS ordered;
SELECT 'ecstatic'::mood;
```

**Output:**

```text
 ordered
---------
 t
(1 row)

ERROR:  invalid input value for enum mood: "ecstatic"
LINE 1: SELECT 'ecstatic'::mood;
               ^
```

```sql
-- no two bookings of the same room may overlap
CREATE EXTENSION IF NOT EXISTS btree_gist;   -- lets GiST combine '=' on room with '&&' on dates
CREATE TABLE bookings (
    room   int NOT NULL,
    during daterange NOT NULL,
    EXCLUDE USING gist (room WITH =, during WITH &&)
);
INSERT INTO bookings VALUES (101, '[2025-03-01, 2025-03-05)');
INSERT INTO bookings VALUES (102, '[2025-03-02, 2025-03-04)');   -- another room: fine
INSERT INTO bookings VALUES (101, '[2025-03-05, 2025-03-07)');   -- starts as the first ends: fine
INSERT INTO bookings VALUES (101, '[2025-03-04, 2025-03-06)');   -- overlaps: rejected
SELECT room, during FROM bookings ORDER BY room, during;
```

**Output:**

```text
ERROR:  conflicting key value violates exclusion constraint "bookings_room_during_excl"
DETAIL:  Key (room, during)=(101, [2025-03-04,2025-03-06)) conflicts with existing key (room, during)=(101, [2025-03-01,2025-03-05)).
 room |         during
------+-------------------------
  101 | [2025-03-01,2025-03-05)
  101 | [2025-03-05,2025-03-07)
  102 | [2025-03-02,2025-03-04)
(3 rows)
```

```sql
CREATE TABLE line_items (
    id         int PRIMARY KEY,
    quantity   int NOT NULL,
    unit_price numeric(10, 2) NOT NULL,
    total      numeric(12, 2) GENERATED ALWAYS AS (quantity * unit_price) STORED
);
INSERT INTO line_items (id, quantity, unit_price) VALUES (1, 3, 60), (2, 2, 1200);
UPDATE line_items SET quantity = 5 WHERE id = 1;
SELECT * FROM line_items ORDER BY id;
DROP TABLE line_items, bookings, articles;
DROP TYPE mood;
```

**Output:**

```text
 id | quantity | unit_price |  total
----+----------+------------+---------
  1 |        5 |      60.00 |  300.00
  2 |        2 |    1200.00 | 2400.00
(2 rows)
```

**Common mistakes:**

- ❌ Arrays for data that's really a relationship (orders in a customer's `order_ids[]`).
- ❌ Forgetting that arrays are 1-based.
- ❌ Enforcing "no overlapping bookings" in app code, which races under concurrency. ✅ An exclusion constraint.

### Practice

1. Find articles tagged with **both** `sql` and `beginner`.

<details>
<summary><b>Answer</b></summary>

`WHERE tags @> ARRAY['sql', 'beginner']` (the array contains all of the given values). On the data above, that's only "Intro to SQL".

</details>

**Learn more:** [PostgreSQL docs: Arrays](https://www.postgresql.org/docs/current/arrays.html) · [Range types](https://www.postgresql.org/docs/current/rangetypes.html)

---

## 23. Full-Text Search

### Theory

> **In simple words:** `LIKE '%index%'` only finds exact letters, can't rank results, and is slow on big tables. **Full-text search** understands words: it knows "indexes", "indexing" and "indexed" share the root "index", ignores filler words like "the", ranks the best matches first, and uses an index.

**The two building blocks:**

- **`tsvector`**: a document reduced to its searchable words (**lexemes**), normalised and stemmed: `to_tsvector('english', 'The indexes are indexing')` → `'index':2,4`.
- **`tsquery`**: a search: `to_tsquery('english', 'index & fast')` (AND), `|` (OR), `!` (NOT), `<->` (followed by). For raw user input, **`websearch_to_tsquery`** accepts Google-style searches: `"exact phrase" -excluded or other`.
- `vector @@ query` is true when they match.

**Ranking and highlighting:** `ts_rank(vector, query)` scores how well a document matches; `ts_headline(...)` returns a snippet with the matches highlighted.

**Making it fast:** store the vector in a **generated column** (Section [22](#22-arrays-enums-ranges-and-generated-columns)) and add a **GIN** index on it. Give titles more weight than bodies with `setweight`.

**Postgres full-text search or a search engine?** Postgres is excellent for search inside an app (products, articles, tickets), with no extra system to run. Dedicated engines (Elasticsearch, OpenSearch, Meilisearch, Typesense) add typo tolerance, facets and heavy relevance tuning at large scale. The `pg_trgm` extension adds fuzzy "did you mean" matching to Postgres. AI apps increasingly combine keyword search like this with vector search (Section [26](#26-pgvector-vector-search-for-ai-applications)): **hybrid search**.

### SQL

```sql
CREATE TABLE docs (
    id     int PRIMARY KEY,
    title  text NOT NULL,
    body   text NOT NULL,
    search tsvector GENERATED ALWAYS AS (
        setweight(to_tsvector('english', title), 'A') ||
        setweight(to_tsvector('english', body), 'B')
    ) STORED
);
CREATE INDEX docs_search_idx ON docs USING gin (search);

INSERT INTO docs (id, title, body) VALUES
    (1, 'Indexing in PostgreSQL', 'B-tree indexes make lookups fast. Indexing every column slows down writes.'),
    (2, 'Joins explained',        'A hash join builds a hash table; indexes help nested loop joins.'),
    (3, 'Cooking rice',           'Rinse the rice, then simmer it gently for twelve minutes.');

SELECT to_tsvector('english', 'The indexes are indexing') AS vector;

SELECT id, title, round(ts_rank(search, q)::numeric, 3) AS rank
FROM docs, websearch_to_tsquery('english', 'index') AS q
WHERE search @@ q
ORDER BY rank DESC;
```

**Output:**

```text
   vector
-------------
 'index':2,4
(1 row)

 id |         title          | rank
----+------------------------+-------
  1 | Indexing in PostgreSQL | 0.696
  2 | Joins explained        | 0.243
(2 rows)
```

The document with "Indexing" in its **title** ranks higher, because titles got weight A.

```sql
SELECT id, ts_headline('english', body, websearch_to_tsquery('english', 'hash join'),
                       'StartSel=[, StopSel=]') AS snippet
FROM docs
WHERE search @@ websearch_to_tsquery('english', 'hash join');

SELECT id, title FROM docs WHERE search @@ websearch_to_tsquery('english', 'index -join') ORDER BY id;
DROP TABLE docs;
```

**Output:**

```text
 id |                                 snippet
----+--------------------------------------------------------------------------
  2 | A [hash] [join] builds a [hash] table; indexes help nested loop [joins].
(1 row)

 id |         title
----+------------------------
  1 | Indexing in PostgreSQL
(1 row)
```

**Common mistakes:**

- ❌ `ILIKE '%word%'` for search on large tables.
- ❌ Passing raw user input to `to_tsquery` (syntax errors on characters like `&` or `:`). ✅ `websearch_to_tsquery` or `plainto_tsquery`.
- ❌ Mixing language configurations (`'english'` in the index, `'simple'` in the query), so words never match.

### Practice

1. Search the documents for "rice minutes" and show a highlighted snippet.

<details>
<summary><b>Answer</b></summary>

`SELECT ts_headline('english', body, websearch_to_tsquery('english', 'rice minutes')) FROM docs WHERE search @@ websearch_to_tsquery('english', 'rice minutes');` finds document 3 and wraps "rice" and "minutes" in `<b>` tags by default.

</details>

**Learn more:** [PostgreSQL docs: Full text search](https://www.postgresql.org/docs/current/textsearch.html)

---

## 24. Functions, Procedures and Triggers

### Theory

> **In simple words:** you can store small programs **inside** the database. A **function** computes and returns a value, a **procedure** runs a series of steps, and a **trigger** runs a function **automatically** whenever rows are inserted, updated or deleted, like "always set `updated_at` when a row changes" or "record every change in an audit log".

**SQL functions** are the simplest: a query with parameters.

```text
CREATE FUNCTION price_with_gst(p numeric) RETURNS numeric
LANGUAGE sql IMMUTABLE
RETURN round(p * 1.18, 2);
```

`IMMUTABLE` promises the result depends only on the inputs (same input, same output), which lets PostgreSQL optimise calls and use the function in indexes.

**PL/pgSQL functions** add variables, `IF`, loops and error handling:

```text
CREATE FUNCTION f(...) RETURNS ... LANGUAGE plpgsql AS $$
DECLARE
    x int;
BEGIN
    ...
    RETURN ...;
END;
$$;
```

`$$ ... $$` is **dollar quoting**: a way to write a block of text without escaping every quote inside it.

**Procedures** (`CREATE PROCEDURE`, run with `CALL`) can commit transactions in the middle, which is useful for long batch jobs.

**Triggers** have two parts: a function that `RETURNS trigger`, and the `CREATE TRIGGER` statement that attaches it to a table. Inside the function, `NEW` is the row being written and `OLD` is the previous version; `TG_OP` says whether it's an `INSERT`, `UPDATE` or `DELETE`.

- `BEFORE` triggers can change `NEW` before it's saved (setting `updated_at`, normalising an email).
- `AFTER` triggers see the final row and suit side effects (audit logs, keeping a count in sync).

**When to use database logic, and when not.** Good uses: keeping data correct no matter which program writes it (timestamps, audit trails, derived values), and heavy set-based work close to the data. Be careful with: complex business logic (harder to test, version and debug than application code), triggers calling other triggers, and anything that surprises the next developer. Keep triggers small and document them.

### SQL

```sql
CREATE FUNCTION price_with_gst(p numeric) RETURNS numeric
LANGUAGE sql IMMUTABLE
RETURN round(p * 1.18, 2);

SELECT name, price, price_with_gst(price) FROM products WHERE category = 'bags';
```

**Output:**

```text
   name   |  price  | price_with_gst
----------+---------+----------------
 Backpack | 1200.00 |        1416.00
(1 row)
```

```sql
-- keep updated_at correct automatically, whoever updates the row
ALTER TABLE products ADD COLUMN updated_at timestamptz NOT NULL DEFAULT '2025-01-01';

CREATE FUNCTION set_updated_at() RETURNS trigger
LANGUAGE plpgsql AS $$
BEGIN
    NEW.updated_at := timestamptz '2025-06-01 12:00+00';   -- real code would use now()
    RETURN NEW;
END;
$$;

CREATE TRIGGER products_set_updated_at
BEFORE UPDATE ON products
FOR EACH ROW EXECUTE FUNCTION set_updated_at();

UPDATE products SET stock = stock + 5 WHERE name = 'Pen';
SELECT name, stock, updated_at FROM products WHERE name IN ('Pen', 'Mug') ORDER BY name;
```

**Output:**

```text
 name | stock |       updated_at
------+-------+------------------------
 Mug  |    80 | 2025-01-01 00:00:00+00
 Pen  |   505 | 2025-06-01 12:00:00+00
(2 rows)
```

(A fixed timestamp keeps this example's output the same on every run; use `now()` in real code.)

```sql
-- an audit trail: every price change is recorded
CREATE TABLE price_history (
    product_id int,
    old_price  numeric(10, 2),
    new_price  numeric(10, 2)
);

CREATE FUNCTION log_price_change() RETURNS trigger
LANGUAGE plpgsql AS $$
BEGIN
    IF NEW.price IS DISTINCT FROM OLD.price THEN
        INSERT INTO price_history VALUES (OLD.id, OLD.price, NEW.price);
    END IF;
    RETURN NULL;          -- the return value of an AFTER trigger is ignored
END;
$$;

CREATE TRIGGER products_log_price
AFTER UPDATE ON products
FOR EACH ROW EXECUTE FUNCTION log_price_change();

UPDATE products SET price = 280 WHERE name = 'Mug';
UPDATE products SET stock = stock + 1 WHERE name = 'Mug';     -- no price change: nothing logged
SELECT * FROM price_history;

UPDATE products SET price = 250 WHERE name = 'Mug';           -- put it back
DROP TRIGGER products_log_price ON products;
DROP TRIGGER products_set_updated_at ON products;
ALTER TABLE products DROP COLUMN updated_at;
```

**Output:**

```text
 product_id | old_price | new_price
------------+-----------+-----------
          7 |    250.00 |    280.00
(1 row)
```

**Common mistakes:**

- ❌ Business rules hidden in triggers that nobody knows about.
- ❌ Marking a function `IMMUTABLE` when it reads tables or the clock (wrong results from caching and indexes).
- ❌ Forgetting `RETURN NEW` in a `BEFORE` trigger (returning NULL silently skips the write).
- ❌ Trigger chains that update other tables that have their own triggers.

### Practice

1. Write a `BEFORE INSERT OR UPDATE` trigger on `customers` that stores emails in lowercase.

<details>
<summary><b>Answer</b></summary>

```sql
CREATE FUNCTION lowercase_email() RETURNS trigger LANGUAGE plpgsql AS $$
BEGIN
    NEW.email := lower(NEW.email);
    RETURN NEW;
END;
$$;
CREATE TRIGGER customers_lowercase_email
BEFORE INSERT OR UPDATE ON customers
FOR EACH ROW EXECUTE FUNCTION lowercase_email();

INSERT INTO customers (name, city, email, signed_up) VALUES ('Tara', 'Goa', 'Tara@Example.COM', '2025-06-01')
RETURNING name, email;
DELETE FROM customers WHERE name = 'Tara';
DROP TRIGGER customers_lowercase_email ON customers;
```

**Output:**

```text
 name |      email
------+------------------
 Tara | tara@example.com
(1 row)
```

</details>

**Learn more:** [PostgreSQL docs: PL/pgSQL](https://www.postgresql.org/docs/current/plpgsql.html) · [Triggers](https://www.postgresql.org/docs/current/triggers.html)

---

## 25. Upserts, MERGE and Bulk Loading

### Theory

> **In simple words:** an **upsert** means "insert this row, or if it already exists, update it", in one safe step. **Bulk loading** means getting thousands or millions of rows in fast, which needs different tools from inserting one row at a time.

**INSERT ... ON CONFLICT (PostgreSQL's upsert):**

```text
INSERT INTO stock_levels (sku, qty) VALUES ('PEN-01', 10)
ON CONFLICT (sku)                       -- a unique column or constraint
DO UPDATE SET qty = stock_levels.qty + EXCLUDED.qty;   -- EXCLUDED = the row we tried to insert
```

or `ON CONFLICT DO NOTHING` to skip duplicates. It's **atomic**: two requests racing to insert the same key can't both succeed or both fail. Doing it by hand ("SELECT; if missing INSERT else UPDATE") has exactly that race condition.

**MERGE** (standard SQL, PostgreSQL 15+) handles more complex "sync this source into that table" jobs: match rows, update the matched ones, insert the new ones, and optionally delete, in one statement. PostgreSQL 17 added `RETURNING` to `MERGE`.

**Bulk loading, from slowest to fastest:**

1. One `INSERT` per row, each in its own transaction (slowest: a disk flush per row).
2. Many single-row inserts inside **one transaction**.
3. **Multi-row `INSERT ... VALUES (...), (...), ...`** in batches of a few hundred to a few thousand rows.
4. **`COPY`**: streams rows from a CSV file or program (`COPY t FROM '/path/file.csv' CSV HEADER`, or `\copy` in psql for a file on your own computer). Usually 5–10× faster than inserts; Python drivers expose it too.

For huge one-off loads: create indexes and foreign keys **after** loading, and run `ANALYZE` at the end.

**`generate_series`** creates test data on the fly (as in Section [18](#18-indexes-making-lookups-fast)), and `COPY ... TO` exports query results as CSV.

### SQL

```sql
CREATE TABLE stock_levels (sku text PRIMARY KEY, qty int NOT NULL);
INSERT INTO stock_levels VALUES ('PEN-01', 10), ('MUG-01', 5);

INSERT INTO stock_levels (sku, qty) VALUES ('PEN-01', 7), ('LAMP-01', 3)
ON CONFLICT (sku) DO UPDATE SET qty = stock_levels.qty + EXCLUDED.qty
RETURNING sku, qty;

INSERT INTO stock_levels VALUES ('MUG-01', 100) ON CONFLICT DO NOTHING;   -- existing row untouched
SELECT * FROM stock_levels ORDER BY sku;
```

**Output:**

```text
   sku   | qty
---------+-----
 PEN-01  |  17
 LAMP-01 |   3
(2 rows)

   sku   | qty
---------+-----
 LAMP-01 |   3
 MUG-01  |   5
 PEN-01  |  17
(3 rows)
```

```sql
-- MERGE: sync a delivery into stock levels (add to existing SKUs, insert new ones, drop zeroed ones)
CREATE TABLE delivery (sku text, qty int);
INSERT INTO delivery VALUES ('MUG-01', 20), ('BAG-01', 4), ('LAMP-01', -3);

MERGE INTO stock_levels AS s
USING delivery AS d ON s.sku = d.sku
WHEN MATCHED AND s.qty + d.qty <= 0 THEN DELETE
WHEN MATCHED THEN UPDATE SET qty = s.qty + d.qty
WHEN NOT MATCHED THEN INSERT (sku, qty) VALUES (d.sku, d.qty);

SELECT * FROM stock_levels ORDER BY sku;
```

**Output:**

```text
  sku   | qty
--------+-----
 BAG-01 |   4
 MUG-01 |  25
 PEN-01 |  17
(3 rows)
```

```sql
-- COPY: stream rows in (here from inline data; normally from a CSV file) and back out as CSV
COPY stock_levels (sku, qty) FROM STDIN WITH (FORMAT csv);
CUP-01,12
BOX-01,8
\.
COPY (SELECT sku, qty FROM stock_levels ORDER BY sku) TO STDOUT WITH (FORMAT csv, HEADER);
DROP TABLE stock_levels, delivery;
```

**Output:**

```text
sku,qty
BAG-01,4
BOX-01,8
CUP-01,12
MUG-01,25
PEN-01,17
```

**Common mistakes:**

- ❌ "Check then insert" in application code (race conditions). ✅ `ON CONFLICT`.
- ❌ `ON CONFLICT` without a unique index or constraint on the conflict columns (it's an error).
- ❌ Loading millions of rows with row-by-row inserts and autocommit.
- ❌ `COPY FROM '/file'` reads a file on the **database server**; for a file on your laptop use psql's `\copy`.

### Practice

1. Write an upsert that records a user's last login time in `user_logins (user_id PRIMARY KEY, last_login timestamptz)`.

<details>
<summary><b>Answer</b></summary>

`INSERT INTO user_logins (user_id, last_login) VALUES (42, now()) ON CONFLICT (user_id) DO UPDATE SET last_login = EXCLUDED.last_login;`

</details>

**Learn more:** [PostgreSQL docs: INSERT ... ON CONFLICT](https://www.postgresql.org/docs/current/sql-insert.html#SQL-ON-CONFLICT) · [MERGE](https://www.postgresql.org/docs/current/sql-merge.html) · [COPY](https://www.postgresql.org/docs/current/sql-copy.html)

---

## 26. pgvector: Vector Search for AI Applications

![Documents become vectors; a query vector finds its nearest neighbours](images/sql/16-pgvector.svg)

### Theory

> **In simple words:** AI models can turn a piece of text (or an image) into an **embedding**: a list of numbers that captures its **meaning**, so texts that mean similar things get similar lists. **pgvector** is a PostgreSQL extension that stores these lists and finds the **most similar** ones fast. It's the "retrieval" part of most AI chatbots that answer questions about your own documents (RAG).

**The idea in three steps:**

1. **Embed** each document chunk with an embedding model (an API call or a local model; the AI notes cover this) and store the vector in a `vector(n)` column, where n is the model's dimension (often 384, 768, 1024, 1536 or 3072).
2. **Embed the user's question** with the same model.
3. **Find the nearest vectors** to the question's vector: `ORDER BY embedding <=> :question LIMIT 5`. Those chunks are the most relevant context to give the language model.

**Distance operators:**

| Operator | Distance | Use when |
|---|---|---|
| `<=>` | **Cosine distance** (1 − cosine similarity) | The usual choice for text embeddings |
| `<->` | Euclidean (L2) distance | Some image and older models |
| `<#>` | Negative inner product | Normalised vectors, for speed |

Smaller distance means more similar. Cosine similarity itself is `1 - (a <=> b)`.

**Indexes for speed (approximate nearest neighbour, ANN):** without an index, pgvector compares the query with every row (exact, fine for up to roughly 100k rows). For more:

- **HNSW** (`USING hnsw (embedding vector_cosine_ops)`): a layered graph (the DSA notes explain it in their real-systems section). Fast, accurate, no training step; uses more memory and builds slower. Tune recall with `SET hnsw.ef_search = 100`.
- **IVFFlat** (`USING ivfflat ... WITH (lists = 100)`): clusters the vectors and searches the nearest clusters. Builds faster and uses less memory, but must be built after data is loaded, and usually has lower recall.
- Approximate means "almost always the true nearest neighbours", traded for huge speed-ups. Check **recall** on your own data.

**Why vectors in Postgres (and not a separate vector database)?** Your documents, users, permissions and vectors live in one place: one backup, one transaction, and ordinary SQL filters like `WHERE tenant_id = 7 AND published`. Dedicated vector databases (Pinecone, Qdrant, Milvus, Weaviate) are worth it at very large scale or for specialised features. Newer pgvector versions add `halfvec` (half the storage) and binary quantization, and, since 0.8, **iterative index scans** that keep returning results when a `WHERE` filter removes many candidates.

**Hybrid search.** Vectors find meaning ("cheap laptop" ≈ "budget notebook computer"); keywords (Section [23](#23-full-text-search)) find exact terms (product codes, names). Production RAG systems usually run **both** and merge the rankings, commonly with **reciprocal rank fusion (RRF)**: each result scores `1 / (60 + its rank)` in each list, and the scores are added.

### SQL

```sql
CREATE EXTENSION IF NOT EXISTS vector;

-- 3-number "embeddings" so you can see what's happening; real ones have hundreds of numbers
CREATE TABLE kb (
    id        int PRIMARY KEY,
    content   text NOT NULL,
    embedding vector(3) NOT NULL
);
INSERT INTO kb VALUES
    (1, 'How to reset your password',        '[0.90, 0.10, 0.00]'),
    (2, 'Changing your account email',       '[0.70, 0.30, 0.05]'),
    (3, 'Refund policy for damaged items',   '[0.05, 0.90, 0.20]'),
    (4, 'How long does shipping take?',      '[0.00, 0.30, 0.95]'),
    (5, 'Track your order',                  '[0.10, 0.25, 0.90]');

-- the question "I forgot my login" embedded by the same (toy) model
SELECT id, content, round((1 - (embedding <=> '[0.85, 0.20, 0.05]'))::numeric, 3) AS cosine_similarity
FROM kb
ORDER BY embedding <=> '[0.85, 0.20, 0.05]'
LIMIT 2;
```

**Output:**

```text
 id |           content           | cosine_similarity
----+-----------------------------+-------------------
  1 | How to reset your password  |             0.991
  2 | Changing your account email |             0.985
(2 rows)
```

```sql
CREATE INDEX kb_embedding_hnsw ON kb USING hnsw (embedding vector_cosine_ops);
SET enable_seqscan = off;       -- only to show the index being used on this tiny table
EXPLAIN (COSTS OFF)
SELECT id FROM kb ORDER BY embedding <=> '[0.0, 0.3, 0.9]' LIMIT 2;
RESET enable_seqscan;
```

**Output:**

```text
                       QUERY PLAN
---------------------------------------------------------
 Limit
   ->  Index Scan using kb_embedding_hnsw on kb
         Order By: (embedding <=> '[0,0.3,0.9]'::vector)
(3 rows)
```

```sql
-- hybrid search with reciprocal rank fusion: vectors + keywords
WITH vec AS (
    SELECT id, row_number() OVER (ORDER BY embedding <=> '[0.05, 0.30, 0.90]') AS r
    FROM kb ORDER BY embedding <=> '[0.05, 0.30, 0.90]' LIMIT 3
),
kw AS (
    SELECT id, row_number() OVER (ORDER BY ts_rank(to_tsvector('english', content), q) DESC) AS r
    FROM kb, websearch_to_tsquery('english', 'order') q
    WHERE to_tsvector('english', content) @@ q
)
SELECT kb.id, kb.content,
       round((coalesce(1.0 / (60 + vec.r), 0) + coalesce(1.0 / (60 + kw.r), 0))::numeric, 4) AS rrf
FROM kb
LEFT JOIN vec ON vec.id = kb.id
LEFT JOIN kw  ON kw.id  = kb.id
WHERE vec.id IS NOT NULL OR kw.id IS NOT NULL
ORDER BY rrf DESC;
```

**Output:**

```text
 id |             content             |  rrf
----+---------------------------------+--------
  5 | Track your order                | 0.0325
  4 | How long does shipping take?    | 0.0164
  3 | Refund policy for damaged items | 0.0159
(3 rows)
```

"Track your order" wins: it's near the top of **both** lists.

<!-- no-run -->
```sql
-- a realistic table (dimension from your embedding model) and a filtered search
CREATE TABLE chunks (
    id         bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    doc_id     bigint NOT NULL,
    tenant_id  int NOT NULL,
    content    text NOT NULL,
    embedding  vector(1536) NOT NULL
);
CREATE INDEX ON chunks USING hnsw (embedding vector_cosine_ops);
CREATE INDEX ON chunks (tenant_id);

SELECT id, content
FROM chunks
WHERE tenant_id = $1                   -- only this customer's documents
ORDER BY embedding <=> $2              -- $2 = the question's embedding, passed from the app
LIMIT 5;
```

**Common mistakes:**

- ❌ Mixing embeddings from different models (or model versions) in one column: distances become meaningless. Re-embed everything when you change models.
- ❌ Comparing with `<->` when the index was built with `vector_cosine_ops` (the index is ignored).
- ❌ Expecting exact results from an ANN index, or not measuring recall.
- ❌ Heavy `WHERE` filters with an ANN index on old pgvector versions, which can return fewer than `LIMIT` rows.

### Practice

1. Which knowledge-base entry is most similar to the query vector `[0.1, 0.9, 0.1]`? Predict first, then run it.

<details>
<summary><b>Answer</b></summary>

```sql
SELECT content FROM kb ORDER BY embedding <=> '[0.1, 0.9, 0.1]' LIMIT 1;
```

**Output:**

```text
             content
---------------------------------
 Refund policy for damaged items
(1 row)
```

</details>

**Learn more:** [pgvector on GitHub](https://github.com/pgvector/pgvector) · [Supabase: vector columns guide](https://supabase.com/docs/guides/ai/vector-columns)

---

### ✅ Part 5 checkpoint

Without looking, can you:

- [ ] Query inside `jsonb` with `->`, `->>` and `@>`, and index it with GIN?
- [ ] Use arrays with `ANY` and `unnest`, and prevent overlapping bookings with an exclusion constraint?
- [ ] Build a ranked full-text search with a generated `tsvector` column and a GIN index?
- [ ] Write a trigger that maintains `updated_at` or an audit log?
- [ ] Upsert with `ON CONFLICT`, and bulk-load with `COPY`?
- [ ] Store embeddings in pgvector, find nearest neighbours, and explain HNSW and hybrid search?

---

# Part 6 — Advanced: PostgreSQL in Production

> **Goal:** Secure it, use it from Python, keep it running (backups, replication, VACUUM, partitioning), scale it, and know the other SQL dialects.  
> **You need:** Parts 1–5, and basic Python for one section.

---

## 27. Security: Roles, Permissions, Row-Level Security and SQL Injection

### Theory

> **In simple words:** give every program and person **only the access they need** (least privilege), let the database itself enforce **who can see which rows**, and **never build SQL by gluing user input into a string**, which is how SQL injection attacks steal or destroy data.

**Roles and privileges.** PostgreSQL has **roles** (a role with `LOGIN` is a user). Privileges are granted on objects:

```text
CREATE ROLE app_readonly LOGIN PASSWORD '...';
GRANT CONNECT ON DATABASE shop TO app_readonly;
GRANT USAGE ON SCHEMA public TO app_readonly;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO app_readonly;
REVOKE ... FROM ...;
```

A sensible setup: a **migration role** that owns the tables and can change the schema; an **application role** that can only `SELECT`, `INSERT`, `UPDATE` and `DELETE` on its tables (it can't `DROP` anything); a **read-only role** for analysts and dashboards; and nobody's app connecting as the superuser `postgres`.

**Row-Level Security (RLS)** makes the database filter rows per user automatically. In a multi-tenant SaaS app, a **policy** like "you can only see rows where `tenant_id` equals your tenant" means a bug in one query can't leak another customer's data. Supabase's security model is built on RLS.

**SQL injection: the classic attack.** If code builds a query by pasting user input into the text:

```text
query = "SELECT * FROM users WHERE email = '" + email + "'"
```

a user who types `' OR '1'='1` as their email turns it into `... WHERE email = '' OR '1'='1'`, which matches every user. Worse inputs can delete tables. **The fix is always parameterised queries** (placeholders), where the SQL text and the values travel separately and the value can never become SQL:

```text
cur.execute("SELECT * FROM users WHERE email = %s", (email,))   # psycopg (Section on Python)
```

ORMs and query builders parameterise for you. Never use string formatting (`f"...{x}"`) to put values into SQL. Identifiers (table or column names) can't be parameters; if they must be dynamic, choose them from a fixed allow-list or quote them with the driver's identifier-quoting helper.

**More essentials:**

- **Encrypt connections** (TLS: `sslmode=require` or `verify-full` in connection strings).
- **Keep secrets out of code**: passwords and connection strings come from environment variables or a secrets manager, never from Git.
- Use **SCRAM-SHA-256** password authentication (the default since PostgreSQL 14), and restrict which hosts can connect (`pg_hba.conf`, cloud firewalls).
- **Store passwords hashed** with Argon2 or bcrypt in the application, never in plain text or with fast hashes like MD5.
- **Audit and back up** (Section [29](#29-running-postgresql-backups-replication-vacuum-partitioning-and-monitoring)): security includes being able to recover.

### SQL

```sql
-- least privilege: a read-only role that can see two tables
CREATE ROLE analyst NOLOGIN;
GRANT SELECT ON customers, orders TO analyst;

SET ROLE analyst;                         -- act as that role
SELECT count(*) AS customers_visible FROM customers;
SELECT count(*) FROM products;            -- not granted
DELETE FROM customers WHERE id = 8;       -- not granted
RESET ROLE;
```

**Output:**

```text
 customers_visible
-------------------
                 8
(1 row)

ERROR:  permission denied for table products
ERROR:  permission denied for table customers
```

```sql
-- row-level security: each tenant sees only its own rows
CREATE TABLE notes (id int PRIMARY KEY, tenant text NOT NULL, body text NOT NULL);
INSERT INTO notes VALUES (1, 'acme', 'Acme roadmap'), (2, 'acme', 'Acme pricing'), (3, 'globex', 'Globex secrets');

CREATE ROLE app_user NOLOGIN;
GRANT SELECT ON notes TO app_user;
ALTER TABLE notes ENABLE ROW LEVEL SECURITY;
CREATE POLICY tenant_isolation ON notes
    USING (tenant = current_setting('app.tenant'));    -- the app sets this per request

SET ROLE app_user;
SET app.tenant = 'acme';
SELECT * FROM notes ORDER BY id;                        -- even without any WHERE clause
SET app.tenant = 'globex';
SELECT * FROM notes ORDER BY id;
RESET ROLE;
```

**Output:**

```text
 id | tenant |     body
----+--------+--------------
  1 | acme   | Acme roadmap
  2 | acme   | Acme pricing
(2 rows)

 id | tenant |      body
----+--------+----------------
  3 | globex | Globex secrets
(1 row)
```

```sql
-- what injection does: the attacker's "email" becomes part of the SQL
SELECT count(*) AS rows_leaked FROM customers WHERE email = '' OR '1'='1';
DROP TABLE notes;
DROP ROLE app_user;
REVOKE ALL ON customers, orders FROM analyst;
DROP ROLE analyst;
```

**Output:**

```text
 rows_leaked
-------------
           8
(1 row)
```

**Common mistakes:**

- ❌ Building SQL with string concatenation or f-strings.
- ❌ The app connecting as a superuser or table owner.
- ❌ Relying only on application code for tenant isolation in multi-tenant apps (add RLS, or at least test every query path).
- ❌ Secrets committed to Git, or databases exposed to the whole internet.

### Practice

1. Why can't a placeholder be used for a table name, and how do you handle a user choosing which column to sort by?

<details>
<summary><b>Answer</b></summary>

Placeholders carry **values**; the database must know the table and columns to plan the query, so identifiers must be part of the SQL text. For a user-chosen sort column, map the user's choice through an allow-list in code (`{"price": "price", "name": "name"}`) and reject anything else, never pasting raw input into the query.

</details>

**Learn more:** [PostgreSQL docs: Row security policies](https://www.postgresql.org/docs/current/ddl-rowsecurity.html) · [OWASP: SQL injection prevention](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)

---

## 28. Using PostgreSQL from Python: psycopg, Pooling and SQLAlchemy

### Theory

> **In simple words:** your application talks to PostgreSQL through a **driver** (a library that speaks Postgres's network protocol). In Python that's usually **psycopg** (version 3). On top of it you can write SQL directly, or use an **ORM** like **SQLAlchemy** that maps tables to Python classes.

**psycopg 3 essentials** (`pip install "psycopg[binary]"`):

- `psycopg.connect(dsn)` opens a connection; a **DSN** or URL says where the database is: `postgresql://user:password@host:5432/shop`. Read it from an environment variable, never hard-code it.
- `with conn.cursor() as cur: cur.execute(sql, params)` runs a query; `fetchone()`, `fetchall()` read results.
- **Always pass values as parameters** (`%s` placeholders + a tuple), never with f-strings (Section [27](#27-security-roles-permissions-row-level-security-and-sql-injection)).
- **Transactions:** psycopg starts a transaction automatically; `with psycopg.connect(...) as conn:` commits at the end of the block, or rolls back if an exception escapes. `with conn.transaction():` makes an explicit inner transaction.
- `row_factory=dict_row` returns rows as dicts instead of tuples.
- `executemany` for batches, and `cur.copy(...)` for fast `COPY` bulk loads (Section [25](#25-upserts-merge-and-bulk-loading)).

**Connection pooling.** Opening a connection is slow (a network handshake, authentication, and a new server process), and PostgreSQL handles hundreds, not tens of thousands, of connections. So applications keep a **pool** of open connections and lend them out per request: `psycopg_pool.ConnectionPool` inside one app, or **PgBouncer** in front of the database for many app instances (and for serverless functions, which otherwise open a connection per call).

**ORMs (SQLAlchemy 2.0, Django ORM, and in other languages Prisma, Drizzle, Hibernate).**

- ✅ Less boilerplate, Python classes instead of tuples, database-independent code, and integration with migrations (Alembic, Section [14](#14-changing-the-schema-alter-table-and-migrations)).
- ⚠️ They hide the SQL, which makes N+1 queries easy (Section [20](#20-making-queries-fast-common-performance-patterns)); use eager loading (`selectinload`, `joinedload`) and turn on SQL logging (`echo=True`) during development.
- Complex reporting queries are often clearer in plain SQL; ORMs let you run raw SQL when needed.

**Async.** For async frameworks like FastAPI, use an async driver: psycopg's `AsyncConnection`, or **asyncpg**, with SQLAlchemy's async engine.

**pandas** can read query results straight into a DataFrame with `pandas.read_sql(query, connection)`, which the data-science notes use.

### Python

These examples use the database in the `DATABASE_URL` environment variable (for example `postgresql://postgres:secret@localhost:5432/shop`).

```python
import os
import psycopg
from psycopg.rows import dict_row

DSN = os.environ.get("DATABASE_URL", "postgresql://localhost/shop")

with psycopg.connect(DSN) as conn:                    # commits at the end of the block
    with conn.cursor() as cur:
        cur.execute("DROP TABLE IF EXISTS py_products")
        cur.execute("""
            CREATE TABLE py_products (
                id    int GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
                name  text NOT NULL,
                price numeric(10, 2) NOT NULL
            )""")
        cur.executemany(
            "INSERT INTO py_products (name, price) VALUES (%s, %s)",
            [("Pen", 15.5), ("Mug", 250), ("Lamp", 900)],
        )
        max_price = 500                                # a value from the user: passed as a parameter
        cur.execute("SELECT name, price FROM py_products WHERE price < %s ORDER BY price", (max_price,))
        print(cur.fetchall())

with psycopg.connect(DSN, row_factory=dict_row) as conn:
    row = conn.execute("SELECT name, price FROM py_products WHERE name = %s", ("Lamp",)).fetchone()
    print(row)
```

**Output:**

```text
[('Pen', Decimal('15.50')), ('Mug', Decimal('250.00'))]
{'name': 'Lamp', 'price': Decimal('900.00')}
```

`numeric` values arrive as Python `Decimal`s, so money stays exact.

```python
# transactions: everything inside the block is rolled back if an exception escapes
try:
    with psycopg.connect(DSN) as conn:
        with conn.transaction():
            conn.execute("UPDATE py_products SET price = price * 2")
            raise RuntimeError("something went wrong halfway")
except RuntimeError as e:
    print("rolled back:", e)

with psycopg.connect(DSN) as conn:
    print(conn.execute("SELECT sum(price) FROM py_products").fetchone()[0])

    with conn.cursor().copy("COPY py_products (name, price) FROM STDIN") as copy:   # fast bulk load
        for i in range(1000):
            copy.write_row((f"item {i}", i))
    print(conn.execute("SELECT count(*) FROM py_products").fetchone()[0])
```

**Output:**

```text
rolled back: something went wrong halfway
1165.50
1003
```

```python
# SQLAlchemy 2.0 ORM: tables as classes, and eager loading to avoid N+1 queries
from sqlalchemy import ForeignKey, String, create_engine, select
from sqlalchemy.orm import DeclarativeBase, Mapped, Session, mapped_column, relationship, selectinload

class Base(DeclarativeBase):
    pass

class Author(Base):
    __tablename__ = "py_authors"
    id: Mapped[int] = mapped_column(primary_key=True)
    name: Mapped[str] = mapped_column(String(100))
    books: Mapped[list["Book"]] = relationship(back_populates="author")

class Book(Base):
    __tablename__ = "py_books"
    id: Mapped[int] = mapped_column(primary_key=True)
    title: Mapped[str]
    author_id: Mapped[int] = mapped_column(ForeignKey("py_authors.id"))
    author: Mapped[Author] = relationship(back_populates="books")

engine = create_engine(DSN.replace("postgresql://", "postgresql+psycopg://", 1))
Base.metadata.drop_all(engine)
Base.metadata.create_all(engine)                      # in real projects: Alembic migrations

with Session(engine) as session:
    kleppmann = Author(name="Martin Kleppmann", books=[Book(title="Designing Data-Intensive Applications")])
    martin = Author(name="Robert C. Martin", books=[Book(title="Clean Code"), Book(title="Clean Architecture")])
    session.add_all([kleppmann, martin])
    session.commit()

    stmt = select(Author).options(selectinload(Author.books)).order_by(Author.name)   # 2 queries, not N+1
    for author in session.scalars(stmt):
        print(author.name, "→", sorted(b.title for b in author.books))

Base.metadata.drop_all(engine)
with psycopg.connect(DSN) as conn:
    conn.execute("DROP TABLE py_products")
```

**Output:**

```text
Martin Kleppmann → ['Designing Data-Intensive Applications']
Robert C. Martin → ['Clean Architecture', 'Clean Code']
```

<!-- no-run -->
```python
# a connection pool (pip install psycopg-pool) and async access
from psycopg_pool import ConnectionPool

pool = ConnectionPool(DSN, min_size=2, max_size=10)
with pool.connection() as conn:                      # borrow, then automatically return
    conn.execute("SELECT 1")

import asyncio
async def main():
    async with await psycopg.AsyncConnection.connect(DSN) as aconn:
        cur = await aconn.execute("SELECT count(*) FROM customers")
        print(await cur.fetchone())
asyncio.run(main())
```

**Common mistakes:**

- ❌ f-strings to put values in SQL (injection).
- ❌ Opening a new connection per request without a pool.
- ❌ Forgetting to commit (psycopg's `with connect(...)` commits for you; a bare `conn` needs `conn.commit()`).
- ❌ Lazy-loading relationships in a loop (N+1).
- ❌ Converting `numeric` money to `float` in Python.

### Practice

1. Write a function `find_customers(city)` that returns a list of names for a city, safely parameterised.

<details>
<summary><b>Answer</b></summary>

<!-- no-run -->
```python
def find_customers(city):
    with psycopg.connect(DSN) as conn:
        rows = conn.execute("SELECT name FROM customers WHERE city = %s ORDER BY name", (city,)).fetchall()
    return [name for (name,) in rows]
```

</details>

**Learn more:** [psycopg 3 documentation](https://www.psycopg.org/psycopg3/docs/) · [SQLAlchemy 2.0 unified tutorial](https://docs.sqlalchemy.org/en/20/tutorial/) · [PgBouncer](https://www.pgbouncer.org/)

---

## 29. Running PostgreSQL: Backups, Replication, VACUUM, Partitioning and Monitoring

![A primary streams its write-ahead log to replicas; WAL archives plus base backups allow point-in-time recovery](images/sql/17-replication.svg)

### Theory

> **In simple words:** keeping a database healthy in production means four jobs: **back it up** (and practise restoring), **copy it live to other servers** (so a crash doesn't take you down and reads can be spread out), **clean up after updates** (VACUUM), and **watch it** (monitoring). Managed cloud services do much of this for you, but you still need to understand it.

**1. Backups: two kinds.**

| Kind | Tool | Gives | Good for |
|---|---|---|---|
| **Logical** | `pg_dump` / `pg_restore` | SQL or a compressed archive of one database | Small–medium databases, moving data between versions or servers |
| **Physical + WAL archiving** | `pg_basebackup`, pgBackRest, Barman, WAL-G | A copy of the data files plus a continuous stream of changes | **Point-in-time recovery (PITR)**: restore to "11:59:58, just before someone ran `DELETE` without `WHERE`" |

The **write-ahead log (WAL)** records every change before it's applied (that's how durability works, Section [17](#17-transactions-acid-and-concurrency)). Archiving the WAL lets you replay changes on top of a base backup up to any moment. **A backup you've never restored is not a backup:** test restores regularly. (PostgreSQL 17 added **incremental** base backups.)

**2. Replication and high availability.**

- **Streaming replication:** replicas continuously receive the primary's WAL and apply it, staying a fraction of a second behind. Replicas can serve **read-only** queries (read replicas).
- **Synchronous vs asynchronous:** asynchronous (the default) is fast but can lose the last moments of data if the primary dies; synchronous waits for a replica to confirm each commit.
- **Failover:** if the primary dies, promote a replica. Tools like **Patroni** automate this; managed services (Amazon RDS/Aurora, Google Cloud SQL/AlloyDB, Azure, Neon, Supabase, Crunchy Bridge) do it for you.
- **Logical replication** copies changes for chosen tables (to another database, a different major version, or an analytics system), and underpins zero-downtime major upgrades and **change data capture (CDC)** tools like Debezium that stream database changes into Kafka.
- Read replicas lag slightly: a user who just saved something may not see it if the next read goes to a replica ("read-your-writes"; route such reads to the primary).

**3. VACUUM and bloat.** Because of MVCC, updates and deletes leave **dead row versions** behind. **VACUUM** marks their space as reusable, keeps the visibility map current (for index-only scans), and prevents transaction-ID wraparound. **Autovacuum** runs it automatically; your job is not to block it: avoid long-running or idle-in-transaction sessions, and tune autovacuum for very busy tables. `VACUUM FULL` rewrites a table to shrink it but locks it completely; tools like `pg_repack` do it online.

**4. Partitioning: splitting one huge table into pieces.** A table partitioned by month (`PARTITION BY RANGE (created_at)`) stores each month separately. Queries that filter on the partition key only touch the relevant partitions (**partition pruning**), and dropping old data becomes `DROP TABLE` of one partition instead of a slow `DELETE`. Useful from tens or hundreds of millions of rows, for time-series and log-like data.

**5. Monitoring: the views to know.**

| View / tool | Tells you |
|---|---|
| `pg_stat_activity` | What every connection is doing right now (spot long-running and stuck queries) |
| `pg_stat_statements` | Which query shapes use the most time overall |
| `pg_stat_user_tables` | Sequential vs index scans, dead rows, last (auto)vacuum per table |
| `pg_stat_user_indexes` | Which indexes are actually used |
| `pg_locks` | Who is waiting for whom |
| Dashboards | pgwatch, Prometheus + postgres_exporter + Grafana, or your cloud's built-in monitoring |

**Upgrades:** minor versions (16.3 → 16.4) are bug and security fixes: apply them promptly. Major versions (16 → 17) come yearly and need `pg_upgrade` (fast, in place) or logical replication (near-zero downtime). Each major version is supported for 5 years.

### SQL

```sql
-- range partitioning by month, and partition pruning
CREATE TABLE events (
    id         bigint GENERATED ALWAYS AS IDENTITY,
    created_at timestamptz NOT NULL,
    kind       text NOT NULL
) PARTITION BY RANGE (created_at);

CREATE TABLE events_2025_01 PARTITION OF events FOR VALUES FROM ('2025-01-01') TO ('2025-02-01');
CREATE TABLE events_2025_02 PARTITION OF events FOR VALUES FROM ('2025-02-01') TO ('2025-03-01');
CREATE TABLE events_2025_03 PARTITION OF events FOR VALUES FROM ('2025-03-01') TO ('2025-04-01');

INSERT INTO events (created_at, kind)
SELECT timestamptz '2025-01-01' + i * interval '1 hour', CASE WHEN i % 3 = 0 THEN 'click' ELSE 'view' END
FROM generate_series(0, 2000) AS i;       -- 2001 hours ≈ Jan to mid-March

SELECT tableoid::regclass AS partition, count(*) FROM events GROUP BY 1 ORDER BY 1;

EXPLAIN (COSTS OFF) SELECT count(*) FROM events WHERE created_at >= '2025-02-10' AND created_at < '2025-02-20';
```

**Output:**

```text
   partition    | count
----------------+-------
 events_2025_01 |   744
 events_2025_02 |   672
 events_2025_03 |   585
(3 rows)

                                                                         QUERY PLAN
------------------------------------------------------------------------------------------------------------------------------------------------------------
 Aggregate
   ->  Seq Scan on events_2025_02 events
         Filter: ((created_at >= '2025-02-10 00:00:00+00'::timestamp with time zone) AND (created_at < '2025-02-20 00:00:00+00'::timestamp with time zone))
(3 rows)
```

Only `events_2025_02` is scanned: the other partitions were pruned. Retiring January's data is now `DROP TABLE events_2025_01;`, which is instant.

<!-- no-check -->
```sql
-- health checks you can run any time
SELECT count(*) FILTER (WHERE state = 'active') >= 1 AS someone_active
FROM pg_stat_activity;

SELECT relname, n_live_tup, n_dead_tup
FROM pg_stat_user_tables
WHERE relname IN ('customers', 'products')
ORDER BY relname;
DROP TABLE events;
```

**Output:**

```text
 someone_active
----------------
 t
(1 row)

  relname  | n_live_tup | n_dead_tup
-----------+------------+------------
 customers |          8 |          5
 products  |          9 |         16
(2 rows)
```

(The dead-row counts depend on how recently autovacuum ran, so this output isn't checked.)

<!-- no-run -->
```sql
-- from a shell (not psql): logical backup and restore of one database
-- pg_dump -Fc -d shop -f shop.dump
-- pg_restore -d shop_copy shop.dump

-- find queries running longer than 5 minutes, and cancel one
SELECT pid, now() - query_start AS runtime, state, left(query, 60) AS query
FROM pg_stat_activity
WHERE state <> 'idle' AND now() - query_start > interval '5 minutes';
SELECT pg_cancel_backend(12345);     -- polite: cancel the query (pg_terminate_backend ends the connection)
```

**Common mistakes:**

- ❌ Never testing a restore.
- ❌ Sessions left "idle in transaction", which hold locks and block VACUUM.
- ❌ Reading your own just-written data from a lagging replica.
- ❌ Partitioning small tables (it adds complexity with no benefit), or choosing a partition key that queries don't filter on.
- ❌ Running unsupported major versions.

### Practice

1. Your database was damaged at 14:05 by a bad migration. Which backup setup lets you restore to 14:04, and which doesn't?

<details>
<summary><b>Answer</b></summary>

Physical base backups **plus continuous WAL archiving** allow point-in-time recovery to 14:04. A nightly `pg_dump` only restores to the time of the last dump, losing every change since.

</details>

**Learn more:** [PostgreSQL docs: Backup and restore](https://www.postgresql.org/docs/current/backup.html) · [High availability and replication](https://www.postgresql.org/docs/current/high-availability.html) · [Routine vacuuming](https://www.postgresql.org/docs/current/routine-vacuuming.html) · [Table partitioning](https://www.postgresql.org/docs/current/ddl-partitioning.html)

---

## 30. Scaling PostgreSQL, and What's New in PostgreSQL 17 and 18

### Theory

> **In simple words:** a single well-tuned PostgreSQL server handles far more than most apps ever need. When it isn't enough, you scale in steps: fix queries, add caching, add read replicas, partition, and only then split data across servers (sharding).

**The scaling ladder (climb only as far as you must):**

1. **Fix the queries and indexes** (Sections [18](#18-indexes-making-lookups-fast)–[20](#20-making-queries-fast-common-performance-patterns)). This is usually the biggest win by far.
2. **Scale up:** a bigger machine (more RAM so the working set fits in memory, faster disks). Surprisingly far-reaching: single servers with hundreds of cores and terabytes of RAM exist.
3. **Pool connections** (PgBouncer) so thousands of clients share a few hundred connections.
4. **Cache** hot, rarely-changing data (Redis, materialized views, HTTP caches).
5. **Read replicas** for read-heavy traffic (Section [29](#29-running-postgresql-backups-replication-vacuum-partitioning-and-monitoring)).
6. **Partition** very large tables.
7. **Shard:** split data across several independent servers by a key (usually `tenant_id` or `user_id`). Extensions like **Citus** do this inside Postgres; otherwise the application routes queries. Cross-shard joins and transactions become hard, so choose the key carefully.
8. **Split by workload:** move analytics to a warehouse or columnar store (BigQuery, Snowflake, ClickHouse, DuckDB) fed by CDC or ETL, and keep Postgres for transactions (OLTP vs OLAP).

**Modern PostgreSQL platforms (2024–2026):** serverless and branching Postgres (**Neon**: databases that scale to zero, and branches of your database for each pull request, like Git), **Supabase** (Postgres plus auth, storage, realtime and RLS-based APIs), **Amazon Aurora** and **Google AlloyDB** (Postgres-compatible engines with custom storage), and distributed Postgres-compatible databases (CockroachDB, YugabyteDB) for global writes.

**What's new in PostgreSQL 17 (September 2024):**

- `JSON_TABLE` and more SQL/JSON functions (turn JSON into rows and columns).
- `MERGE ... RETURNING`, and `MERGE` on updatable views.
- **Incremental backups** with `pg_basebackup --incremental`.
- A new memory structure for VACUUM that uses far less memory and runs faster.
- Faster bulk loading with `COPY`, and `COPY ... ON_ERROR ignore` to skip bad rows.

**What's new in PostgreSQL 18 (September 2025):**

- An **asynchronous I/O** subsystem that speeds up sequential scans, bitmap scans and vacuum on many systems.
- **`uuidv7()`**: time-ordered UUIDs, which are much friendlier to B-tree indexes than random `gen_random_uuid()` values.
- **Virtual generated columns** (computed on read) become the default for generated columns.
- **Skip scan** for multi-column B-tree indexes: some queries that don't filter on the first index column can now use the index (softening the rule in Section [18](#18-indexes-making-lookups-fast)).
- `RETURNING` can show both the `OLD` and `NEW` values in `UPDATE`, `DELETE` and `MERGE`.
- **OAuth** authentication support, and planner statistics that survive a major-version upgrade, so performance is stable right after upgrading.

<!-- no-run -->
```sql
-- PostgreSQL 18 only
SELECT uuidv7();                                   -- time-ordered UUID
UPDATE products SET price = price * 1.1 WHERE id = 3
RETURNING old.price AS before, new.price AS after; -- both versions in one statement

-- PostgreSQL 17+: JSON_TABLE turns a JSON array into rows
SELECT * FROM JSON_TABLE(
    '[{"sku": "PEN-01", "qty": 3}, {"sku": "MUG-01", "qty": 1}]',
    '$[*]' COLUMNS (sku text PATH '$.sku', qty int PATH '$.qty')
) AS jt;
```

**Common mistakes:**

- ❌ Sharding (or switching databases) before exhausting indexes, pooling, caching and replicas.
- ❌ Picking a shard key that forces most queries to touch every shard.
- ❌ Running analytics on the production primary during peak hours.

### Practice

1. An app has 5,000 web server processes each opening its own connection, and the database is struggling. What's the first fix?

<details>
<summary><b>Answer</b></summary>

Put a connection pooler (PgBouncer, or the cloud provider's built-in pooler) between the app and the database, so thousands of clients share a small pool of real connections (a few hundred at most). Each Postgres connection is a separate process using memory, so thousands of them waste resources even when idle.

</details>

**Learn more:** [PostgreSQL 17 release notes](https://www.postgresql.org/docs/17/release-17.html) · [PostgreSQL 18 release notes](https://www.postgresql.org/docs/18/release-18.html) · [Citus](https://www.citusdata.com/)

---

## 31. PostgreSQL vs MySQL vs SQLite vs SQL Server: Dialect Differences

### Theory

> **In simple words:** all SQL databases share the same core (`SELECT`, joins, `GROUP BY`, transactions), so most of what you learned transfers directly. They differ in extras and small spellings. Here are the differences you'll actually meet.

**Which database is used where:**

| Database | Typical use | Notes |
|---|---|---|
| **PostgreSQL** | General-purpose apps, SaaS, geospatial, AI (pgvector) | Rich types and extensions, strict standards |
| **MySQL / MariaDB** | Web apps (WordPress, many classic stacks) | Very widely deployed; InnoDB storage engine |
| **SQLite** | Embedded in apps, phones, browsers, tests, small sites | A single file, no server; the most-deployed database in the world |
| **SQL Server** | Microsoft / .NET enterprises | T-SQL dialect |
| **Oracle** | Large enterprises, banks | PL/SQL dialect |
| **DuckDB** | Analytics on files (CSV, Parquet) on your laptop | "SQLite for analytics"; columnar, very fast |

**Spelling differences:**

| Task | PostgreSQL | MySQL | SQLite | SQL Server |
|---|---|---|---|---|
| First N rows | `LIMIT 10` | `LIMIT 10` | `LIMIT 10` | `SELECT TOP 10` / `OFFSET … FETCH` |
| Auto-increment ID | `GENERATED ALWAYS AS IDENTITY` | `AUTO_INCREMENT` | `INTEGER PRIMARY KEY` | `IDENTITY(1,1)` |
| String concatenation | `a \|\| b` | `CONCAT(a, b)` | `a \|\| b` | `a + b` / `CONCAT` |
| Case-insensitive match | `ILIKE` | `LIKE` (usually case-insensitive by collation) | `LIKE` (ASCII case-insensitive) | `LIKE` (by collation) |
| Upsert | `ON CONFLICT … DO UPDATE` | `ON DUPLICATE KEY UPDATE` | `ON CONFLICT … DO UPDATE` | `MERGE` |
| Return changed rows | `RETURNING` | — (MariaDB: `RETURNING`) | `RETURNING` | `OUTPUT` |
| Current time | `now()` | `NOW()` | `datetime('now')` | `GETDATE()` / `SYSDATETIME()` |
| Boolean type | `boolean` | `TINYINT(1)` / `BOOL` alias | integers 0/1 | `BIT` |
| Identifier quoting | `"name"` | `` `name` `` | `"name"` | `[name]` |

**Behaviour differences that bite:**

- **Types:** SQLite uses flexible typing (a column declared `INTEGER` can hold text unless the table is `STRICT`); PostgreSQL rejects wrong types.
- **Strictness:** older MySQL settings silently truncated bad data; modern MySQL defaults to strict mode, PostgreSQL has always been strict.
- **Transactional DDL:** in PostgreSQL, `CREATE`/`ALTER`/`DROP` can be rolled back inside a transaction; in MySQL most DDL commits immediately, so a failed migration can leave things half-done.
- **GROUP BY:** MySQL (with some settings) allows selecting non-grouped columns and picks an arbitrary value; PostgreSQL requires them to be grouped.

**Learn SQL portably:** stick to standard SQL where you can (`CASE`, `COALESCE`, `JOIN ... ON`, window functions, CTEs), and look up the dialect-specific spellings as needed.

### Practice

1. Rewrite `SELECT TOP 5 name FROM products ORDER BY price DESC` for PostgreSQL.

<details>
<summary><b>Answer</b></summary>

`SELECT name FROM products ORDER BY price DESC LIMIT 5;` (or the standard `FETCH FIRST 5 ROWS ONLY`, which PostgreSQL also supports).

</details>

---

### ✅ Part 6 checkpoint

Without looking, can you:

- [ ] Set up least-privilege roles, explain row-level security, and prevent SQL injection with parameters?
- [ ] Query PostgreSQL from Python with psycopg safely, use transactions, and avoid N+1 with an ORM?
- [ ] Explain logical vs physical backups, point-in-time recovery, streaming replication and failover?
- [ ] Explain why VACUUM exists, and partition a large table by time?
- [ ] Describe the scaling ladder, and name a few features new in PostgreSQL 17 and 18?

**Learn more:** [Modern SQL (standard features across databases)](https://modern-sql.com/) · [DB-Engines ranking](https://db-engines.com/en/ranking)

---

# Part 7 — Interview Prep: Revision

> **Goal:** Practise the classic interview problems and revise quickly.  
> **You need:** Parts 1–6.

---

## 32. Classic SQL Interview Problems (with Solutions)

### Theory

> **In simple words:** SQL interviews reuse about a dozen patterns. Recognise the pattern, and the query almost writes itself. Try each problem before opening its solution.

**How to approach any SQL question:**

1. **Restate the output:** what is one row of the result? ("one row per department", "one row per user who …").
2. **Find the grain of each table** (what one row means) and the join keys.
3. **Build it in CTEs**, one step at a time, checking each step's output.
4. **Check the edge cases:** NULLs, ties, customers with no orders, duplicates, empty results.
5. **Say the complexity out loud** if asked: which indexes would help?

| Pattern | Tool | Problems below |
|---|---|---|
| N-th highest / top N per group | `dense_rank()` / `row_number()` in a CTE | 1, 2 |
| Rows with no match | `LEFT JOIN … IS NULL` / `NOT EXISTS` | 3 |
| Compare with a related row | Self join | 4 |
| Duplicates | `GROUP BY … HAVING count(*) > 1`, `row_number()` | 5 |
| Consecutive runs ("gaps and islands") | `date - row_number()` trick | 6 |
| Change over time | `lag()` / `lead()` | 7 |
| Pivot rows into columns | `sum(...) FILTER (WHERE …)` | 8 |
| Median / percentiles | `percentile_cont(0.5) WITHIN GROUP (ORDER BY …)` | 9 |
| Share of total, retention | Window sums, conditional counts | 10 |

### SQL

**1. The second-highest salary** (return NULL if there isn't one).

<details>
<summary><b>Solution</b></summary>

```sql
SELECT (SELECT DISTINCT salary FROM employees ORDER BY salary DESC OFFSET 1 LIMIT 1) AS second_highest;
```

**Output:**

```text
 second_highest
----------------
      180000.00
(1 row)
```

Wrapping the query in `SELECT (...)` returns NULL instead of no rows when there's no second salary. `DISTINCT` handles ties at the top.

</details>

**2. The top 2 earners in each department** (include ties).

<details>
<summary><b>Solution</b></summary>

```sql
WITH ranked AS (
    SELECT department, name, salary,
           dense_rank() OVER (PARTITION BY department ORDER BY salary DESC) AS r
    FROM employees
)
SELECT department, name, salary FROM ranked WHERE r <= 2 ORDER BY department, salary DESC, name;
```

**Output:**

```text
 department  |  name  |  salary
-------------+--------+-----------
 Engineering | Rahul  | 180000.00
 Engineering | Priya  | 120000.00
 Engineering | Vikram | 120000.00
 Management  | Anita  | 300000.00
 Sales       | Sneha  | 150000.00
 Sales       | Karan  |  90000.00
(6 rows)
```

</details>

**3. Customers who placed no order in 2025.**

<details>
<summary><b>Solution</b></summary>

```sql
SELECT c.name
FROM customers c
WHERE NOT EXISTS (
    SELECT 1 FROM orders o
    WHERE o.customer_id = c.id AND o.ordered_at >= '2025-01-01' AND o.ordered_at < '2026-01-01'
)
ORDER BY c.name;
```

**Output:**

```text
 name
-------
 Arjun
 Dev
(2 rows)
```

</details>

**4. Employees who earn more than their manager.**

<details>
<summary><b>Solution</b></summary>

```sql
UPDATE employees SET salary = 160000 WHERE name = 'Karan';     -- make the example interesting

SELECT e.name AS employee, e.salary, m.name AS manager, m.salary AS manager_salary
FROM employees e
JOIN employees m ON m.id = e.manager_id
WHERE e.salary > m.salary;

UPDATE employees SET salary = 90000 WHERE name = 'Karan';      -- restore
```

**Output:**

```text
 employee |  salary   | manager | manager_salary
----------+-----------+---------+----------------
 Karan    | 160000.00 | Sneha   |      150000.00
(1 row)
```

</details>

**5. Find duplicate emails, then delete the duplicates, keeping the oldest row.**

<details>
<summary><b>Solution</b></summary>

```sql
CREATE TABLE signups (id int PRIMARY KEY, email text NOT NULL);
INSERT INTO signups VALUES (1, 'a@x.com'), (2, 'b@x.com'), (3, 'a@x.com'), (4, 'c@x.com'), (5, 'a@x.com'), (6, 'b@x.com');

SELECT email, count(*) FROM signups GROUP BY email HAVING count(*) > 1 ORDER BY email;

DELETE FROM signups
WHERE id IN (
    SELECT id FROM (
        SELECT id, row_number() OVER (PARTITION BY email ORDER BY id) AS rn FROM signups
    ) t
    WHERE rn > 1
);
SELECT * FROM signups ORDER BY id;
DROP TABLE signups;
```

**Output:**

```text
  email  | count
---------+-------
 a@x.com |     3
 b@x.com |     2
(2 rows)

 id |  email
----+---------
  1 | a@x.com
  2 | b@x.com
  4 | c@x.com
(3 rows)
```

</details>

**6. Users who logged in on 3 or more consecutive days** (gaps and islands).

<details>
<summary><b>Solution</b></summary>

```sql
CREATE TABLE logins (user_id int, day date, PRIMARY KEY (user_id, day));
INSERT INTO logins VALUES
    (1, '2025-03-01'), (1, '2025-03-02'), (1, '2025-03-03'), (1, '2025-03-05'),
    (2, '2025-03-01'), (2, '2025-03-03'), (2, '2025-03-04'),
    (3, '2025-03-10'), (3, '2025-03-11'), (3, '2025-03-12'), (3, '2025-03-13');

WITH grouped AS (
    SELECT user_id, day,
           day - (row_number() OVER (PARTITION BY user_id ORDER BY day))::int AS island
    FROM logins
)
SELECT user_id, min(day) AS streak_start, max(day) AS streak_end, count(*) AS days
FROM grouped
GROUP BY user_id, island
HAVING count(*) >= 3
ORDER BY user_id;
DROP TABLE logins;
```

**Output:**

```text
 user_id | streak_start | streak_end | days
---------+--------------+------------+------
       1 | 2025-03-01   | 2025-03-03 |    3
       3 | 2025-03-10   | 2025-03-13 |    4
(2 rows)
```

The trick: within a run of consecutive days, `day` and `row_number()` both go up by 1 each step, so `day − row_number` is the **same date** for the whole run (the island's ID). A gap changes it.

</details>

**7. Month-over-month revenue growth (%).**

<details>
<summary><b>Solution</b></summary>

```sql
WITH monthly AS (
    SELECT date_trunc('month', ordered_at)::date AS month, sum(total) AS revenue
    FROM order_summary WHERE status <> 'cancelled'
    GROUP BY 1
)
SELECT month, revenue,
       round(100.0 * (revenue - lag(revenue) OVER (ORDER BY month)) / lag(revenue) OVER (ORDER BY month), 1) AS growth_pct
FROM monthly
ORDER BY month;
```

**Output:**

```text
   month    | revenue | growth_pct
------------+---------+------------
 2025-01-01 | 2955.00 |     (null)
 2025-02-01 | 1700.00 |      -42.5
 2025-03-01 | 4342.00 |      155.4
 2025-04-01 | 2800.00 |      -35.5
 2025-05-01 | 4300.00 |       53.6
(5 rows)
```

</details>

**8. Pivot: units sold per category, one column per month.**

<details>
<summary><b>Solution</b></summary>

```sql
SELECT p.category,
       sum(oi.quantity) FILTER (WHERE o.ordered_at <  '2025-02-01')                                AS jan,
       sum(oi.quantity) FILTER (WHERE o.ordered_at >= '2025-02-01' AND o.ordered_at < '2025-03-01') AS feb,
       sum(oi.quantity) FILTER (WHERE o.ordered_at >= '2025-03-01' AND o.ordered_at < '2025-04-01') AS mar
FROM order_items oi
JOIN orders o   ON o.id = oi.order_id
JOIN products p ON p.id = oi.product_id
GROUP BY p.category
ORDER BY p.category;
```

**Output:**

```text
  category   |  jan   |  feb   |  mar
-------------+--------+--------+--------
 bags        | (null) |      1 | (null)
 electronics |      1 |      1 |      2
 kitchen     | (null) |      2 |      2
 stationery  |     15 | (null) |      7
(4 rows)
```

(NULL means nothing was sold that month; wrap each sum in `coalesce(..., 0)` to show 0.)

</details>

**9. The median order value.**

<details>
<summary><b>Solution</b></summary>

```sql
SELECT percentile_cont(0.5) WITHIN GROUP (ORDER BY total) AS median_order,
       round(avg(total), 2) AS mean_order
FROM order_summary
WHERE status <> 'cancelled';
```

**Output:**

```text
 median_order | mean_order
--------------+------------
         1750 |    1609.70
(1 row)
```

`percentile_cont` interpolates between the two middle values when there's an even count; `percentile_disc` returns an actual value from the data.

</details>

**10. What share of customers ordered more than once (repeat rate)?**

<details>
<summary><b>Solution</b></summary>

```sql
WITH per_customer AS (
    SELECT c.id, count(o.id) AS orders
    FROM customers c LEFT JOIN orders o ON o.customer_id = c.id AND o.status <> 'cancelled'
    GROUP BY c.id
)
SELECT count(*) AS customers,
       count(*) FILTER (WHERE orders >= 2) AS repeat_customers,
       round(100.0 * count(*) FILTER (WHERE orders >= 2) / count(*), 1) AS repeat_pct
FROM per_customer;
```

**Output:**

```text
 customers | repeat_customers | repeat_pct
-----------+------------------+------------
         8 |                3 |       37.5
(1 row)
```

</details>

### Practice

Work through [LeetCode's SQL 50 study plan](https://leetcode.com/studyplan/top-sql-50/) in order, then these harder ones:

| # | Problem | Level |
|---|---|---|
| 1 | [LeetCode 177. Nth Highest Salary](https://leetcode.com/problems/nth-highest-salary/) | 🟡 Medium |
| 2 | [LeetCode 626. Exchange Seats](https://leetcode.com/problems/exchange-seats/) | 🟡 Medium |
| 3 | [LeetCode 1204. Last Person to Fit in the Bus](https://leetcode.com/problems/last-person-to-fit-in-the-bus/) (running total) | 🟡 Medium |
| 4 | [LeetCode 550. Game Play Analysis IV](https://leetcode.com/problems/game-play-analysis-iv/) (retention) | 🟡 Medium |
| 5 | [LeetCode 601. Human Traffic of Stadium](https://leetcode.com/problems/human-traffic-of-stadium/) (gaps and islands) | 🔴 Hard |
| 6 | [LeetCode 262. Trips and Users](https://leetcode.com/problems/trips-and-users/) | 🔴 Hard |
| 7 | [HackerRank SQL track](https://www.hackerrank.com/domains/sql) | Mixed |
| 8 | [DataLemur](https://datalemur.com/) (real interview questions from tech companies) | Mixed |

---

## 33. SQL and PostgreSQL Cheat Sheet

**Query skeleton, and the order it runs in:**

```text
SELECT   [DISTINCT] cols, aggregates, window_fn() OVER (...)   -- 5
FROM     t1 JOIN t2 ON ...                                     -- 1
WHERE    row filters                                           -- 2
GROUP BY cols                                                  -- 3
HAVING   group filters                                         -- 4
ORDER BY cols [ASC|DESC] [NULLS FIRST|LAST]                    -- 6
LIMIT n OFFSET m;                                              -- 7
```

**Which tool for which question:**

| Question | Tool |
|---|---|
| "How many / total / average per X" | `GROUP BY` + aggregates; `HAVING` to filter groups |
| "Combine data from two tables" | `JOIN` (`LEFT JOIN` to keep unmatched rows) |
| "Rows with no match" | `NOT EXISTS` or `LEFT JOIN … WHERE b.id IS NULL` (avoid `NOT IN` with NULLs) |
| "Rank / top N per group / running total / previous row" | Window functions (`rank`, `row_number`, `sum() OVER`, `lag`) |
| "Break a big query into steps" | CTEs (`WITH`) |
| "Walk a hierarchy" | `WITH RECURSIVE` |
| "Insert or update" | `INSERT … ON CONFLICT … DO UPDATE` (or `MERGE`) |
| "Load lots of rows" | `COPY` / multi-row `INSERT` |
| "Search text by words" | `tsvector` + `websearch_to_tsquery` + GIN |
| "Search by meaning" | pgvector + HNSW; hybrid with full-text |
| "Flexible attributes" | `jsonb` + GIN |
| "No overlapping ranges" | Range types + exclusion constraint |
| "Slow query" | `EXPLAIN (ANALYZE, BUFFERS)`, then indexes, then rewrite |
| "Many workers taking jobs" | `SELECT … FOR UPDATE SKIP LOCKED` |

**Index cheat sheet:**

| Query shape | Index |
|---|---|
| `WHERE a = ?` | `(a)` |
| `WHERE a = ? AND b > ?` / `WHERE a = ? ORDER BY b` | `(a, b)` (equality first, then range/sort) |
| `WHERE lower(email) = ?` | `(lower(email))` expression index |
| `WHERE status = 'pending'` on a small subset | Partial index `WHERE status = 'pending'` |
| JSONB `@>`, array `@>`, full-text `@@` | GIN |
| Nearest vectors | HNSW (pgvector) |
| Huge append-only time series | BRIN on the timestamp |

**Types to reach for:** `bigint`/`int` identity IDs · `numeric(p,s)` for money · `text` for strings · `timestamptz` for moments · `date` for days · `boolean` · `jsonb` · `uuid` (`uuidv7()` on PG 18).

**psql:** `\l` `\c db` `\dt` `\d table` `\x` `\timing` `\pset null '(null)'` `\copy` `\q`.

**Safety habits:** write the `WHERE` as a `SELECT` first · `BEGIN; … RETURNING …; COMMIT/ROLLBACK` · parameterised queries only · least-privilege roles · tested backups · `CREATE INDEX CONCURRENTLY` in production.

---

## 34. Most Asked SQL and Database Theory Questions

1. **What's the difference between `WHERE` and `HAVING`?** → `WHERE` filters rows before grouping; `HAVING` filters groups after aggregation and can use aggregates like `count(*)`.
2. **INNER vs LEFT JOIN?** → INNER keeps only matching pairs; LEFT keeps every left row, with NULLs where the right side has no match.
3. **Why does `WHERE x = NULL` return nothing?** → Comparisons with NULL are unknown, not true. Use `IS NULL`. The same three-valued logic makes `NOT IN` with a NULL in the list return nothing.
4. **What is a primary key? A foreign key?** → A primary key uniquely identifies a row (unique + not null). A foreign key stores another table's key and guarantees the referenced row exists.
5. **Explain normalisation and 1NF/2NF/3NF.** → Storing each fact once to avoid update, insert and delete anomalies. 1NF: atomic values; 2NF: no dependency on part of a composite key; 3NF: no dependency between non-key columns.
6. **When would you denormalise?** → For read performance or history (copying the price into an order line), in analytics tables, or cached counters, accepting the cost of keeping copies in sync.
7. **What does ACID mean?** → Atomicity (all or nothing), Consistency (constraints hold), Isolation (concurrent transactions don't interfere, per isolation level), Durability (committed data survives crashes, via the WAL).
8. **What are isolation levels and anomalies?** → Read Committed (default in PostgreSQL), Repeatable Read, Serializable. Higher levels prevent non-repeatable reads, phantoms and write skew, at the cost of retries.
9. **What is MVCC?** → Multi-version concurrency control: updates create new row versions, and each transaction reads a consistent snapshot, so readers and writers don't block each other; VACUUM cleans up old versions.
10. **How does a B-tree index work, and when isn't it used?** → Sorted keys in a shallow tree of wide pages; lookups and ranges take a few page reads. It isn't used for small tables, low-selectivity conditions, functions on the column, leading-wildcard `LIKE`, or conditions on only a non-leading column of a composite index.
11. **Clustered vs non-clustered index?** → A clustered index stores the table rows in index order (SQL Server, MySQL InnoDB's primary key). PostgreSQL tables are heaps; all indexes are secondary (`CLUSTER` reorders once but isn't maintained).
12. **What is a covering index / index-only scan?** → An index containing every column a query needs (via `INCLUDE`), so the table isn't read.
13. **How do you find and fix a slow query?** → `pg_stat_statements` to find it, `EXPLAIN (ANALYZE, BUFFERS)` to see the plan, then fix: add or adjust indexes, make conditions sargable, fix row-estimate problems with `ANALYZE`, rewrite (EXISTS, keyset pagination), or reduce N+1 round trips.
14. **`UNION` vs `UNION ALL`?** → `UNION` removes duplicates (extra sort/hash work); `UNION ALL` keeps them and is faster.
15. **`rank` vs `dense_rank` vs `row_number`?** → For ties: 1,2,2,4 / 1,2,2,3 / 1,2,3,4.
16. **`DELETE` vs `TRUNCATE` vs `DROP`?** → Delete chosen rows (logged, can use WHERE, fires triggers) / empty the whole table quickly / remove the table itself.
17. **How do you prevent SQL injection?** → Parameterised queries (placeholders) always; allow-lists for dynamic identifiers; least-privilege database roles.
18. **What is a deadlock and how do you avoid one?** → Two transactions each waiting for a lock the other holds. PostgreSQL aborts one; avoid them by locking rows in a consistent order and keeping transactions short.
19. **Optimistic vs pessimistic locking?** → Pessimistic locks rows up front (`SELECT … FOR UPDATE`); optimistic checks a version number at write time and retries on conflict. Optimistic suits low-contention workloads.
20. **What is the N+1 query problem?** → Loading a list, then running one query per item. Fix with a join, `= ANY(ids)`, or ORM eager loading.
21. **Why is `OFFSET` pagination slow on deep pages?** → The database still produces and discards all skipped rows; keyset pagination (`WHERE id > last_id`) jumps straight to the next page.
22. **How does replication work, and what is replication lag?** → Replicas replay the primary's WAL; asynchronous replicas can be slightly behind, so a read right after a write may not see it.
23. **Vertical vs horizontal scaling; partitioning vs sharding?** → Bigger machine vs more machines. Partitioning splits a table into pieces on one server; sharding spreads data across servers.
24. **When would you use JSONB instead of columns?** → For variable, sparse or externally-defined attributes; use columns for data that's filtered, joined, constrained or present on every row.
25. **What is a vector database, and how does pgvector fit?** → A store that finds nearest neighbours among embeddings for semantic search and RAG; pgvector adds vector columns and ANN indexes (HNSW, IVFFlat) to PostgreSQL, so vectors live next to the rest of your data.

---
