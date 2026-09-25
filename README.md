# Full-Stack Notes — JavaScript · TypeScript · React · Node.js · Python · FastAPI · DSA · SQL

Complete notes from absolute basics to production and interviews. Every topic has an explanation, 2–3 examples, best practices, and interview questions. Many code examples were executed/type-checked while writing; bugs those checks caught are collected in the **Gotchas Hall of Fame**.

## Files

| File | Covers | Sections | Lines |
|---|---|---|---|
| [JavaScript](javascript.md) | Language fundamentals → async → browser → tooling → testing → production, DSA, polyfills | 58 | 11,017 |
| [TypeScript](typescript.md) | Types from basics to advanced type-level programming, TS with React/Node, end-to-end type safety | 43 | 3,779 |
| [React](react.md) | Components & hooks → patterns & performance → state/data → Next.js → testing → production & machine coding | 56 | 7,709 |
| [Node.js](nodejs.md) | Runtime & event loop → Express & APIs → auth & security → databases → queues, observability, system design | 65 | 8,524 |
| [Python](python.md) | Absolute basics → OOP & functional features → stdlib, scripting, databases → concurrency → production, DSA | 47 | 5,425 |
| [FastAPI](fastapi.md) | Routing & Pydantic → DI, databases, auth → queues, integrations → testing, observability, security, deployment | 43 | 3,832 |
| [DSA in Python](dsa-python.md) | Data structures & algorithms from absolute zero in five levels (Basic → Easy → Moderate → Advanced → Interview Prep): Python basics, pattern printing and number theory first, then arrays, hashing, techniques, linked lists, trees, graphs, DP, string algorithms, segment trees, max flow, the algorithms inside real systems (Bloom filters, consistent hashing, B-trees, vector search) and recent breakthroughs, plus a checklist of what top companies ask. Every topic: simple explanation, diagram, tested Python, practice | 60 | 8,364 |
| [SQL & PostgreSQL](sql-postgresql.md) | SQL from zero in five levels (Basic → Easy → Moderate → Advanced → Interview Prep): tables and queries, joins, CTEs, design and normalisation, window functions, transactions and MVCC, indexes and query plans, JSONB, full-text search, pgvector for AI, security, Python (psycopg, SQLAlchemy), backups, replication, scaling, PostgreSQL 17/18, and classic interview problems. Every query run on PostgreSQL with real output | 34 | 5,291 |
| [Best Practices](best-practices.md) | Every good practice combined across the stack, the Gotchas Hall of Fame, and checklists | 32 | 1,733 |
| **Total** | | **438** | **55,674** |

## How every file is organized

1. **Basics first** — each file starts with getting-started material and builds up.
2. **Core → advanced** — internals, patterns and deep dives come after the fundamentals they depend on.
3. **Production** — testing, security, performance, observability, deployment and best practices.
4. **Interview section last** — DSA/coding questions, output questions, and *Most Asked Interview Questions*.

Conventions: ❌ = wrong/risky, ✅ = recommended · *(caught in these notes)* = a real bug found by testing the examples · code blocks are meant to run as written (imports included).

## Learning roadmap (basics → advanced)

### Phase 1 — Programming basics (pick JS or Python first)

- **JavaScript:** [Getting Started: What is JavaScript & Your First Program](javascript.md#1-getting-started-what-is-javascript--your-first-program) · [var, let, const](javascript.md#2-var-let-const) · [Data Types](javascript.md#3-data-types) · [Operators, Control Flow & Loops](javascript.md#4-operators-control-flow--loops) · [Functions (all types)](javascript.md#6-functions) · [Arrays & Array Methods (+ polyfills)](javascript.md#20-arrays--array-methods) · [Strings](javascript.md#21-strings) · [Objects in Depth](javascript.md#14-objects-in-depth)
- **Python:** [Getting Started: What is Python & Your First Program](python.md#1-getting-started-what-is-python--your-first-program) · [Variables](python.md#2-variables) · [Data Types & Type Conversion](python.md#3-data-types--type-conversion) · [Control Flow & match-case](python.md#10-control-flow--match-case) · [Loops, range, enumerate, zip](python.md#11-loops-range-enumerate-zip) · [Functions & Arguments](python.md#13-functions--arguments) · [Lists](python.md#6-lists) · [Dictionaries](python.md#9-dictionaries)

### DSA track — study alongside the other phases

- **DSA in Python** (Basic → Easy → Moderate → Advanced → Interview Prep; go in order, each part ends with a checkpoint): [How to Use These Notes](dsa-python.md#1-how-to-use-these-notes) · [Loops and Dry Runs](dsa-python.md#3-loops-and-dry-runs) · [Pattern Printing I: Squares and Triangles](dsa-python.md#4-pattern-printing-i-squares-and-triangles) · [Working with Digits](dsa-python.md#7-working-with-digits) · [Divisors and Prime Numbers](dsa-python.md#8-divisors-and-prime-numbers) · [Big-O: How Fast Is My Code?](dsa-python.md#13-big-o-how-fast-is-my-code) · [Recursion Basics](dsa-python.md#14-recursion-basics) · [Arrays and Python Lists](dsa-python.md#15-arrays-and-python-lists) · [Hashing: Dictionaries and Sets](dsa-python.md#19-hashing-dictionaries-and-sets) · [Two Pointers](dsa-python.md#22-two-pointers) · [Sliding Window](dsa-python.md#23-sliding-window) · [Classic Array Algorithms: Kadane, Majority Vote, Dutch Flag and More](dsa-python.md#25-classic-array-algorithms-kadane-majority-vote-dutch-flag-and-more) · [Linked Lists](dsa-python.md#31-linked-lists) · [Binary Tree Interview Problems](dsa-python.md#37-binary-tree-interview-problems) · [Graphs: Representation, BFS and DFS](dsa-python.md#41-graphs-representation-bfs-and-dfs) · [Dynamic Programming](dsa-python.md#49-dynamic-programming) · [Algorithms Behind Real Systems: Consistent Hashing, Rate Limiters, B-Trees, LSM Trees and Vector Search](dsa-python.md#56-algorithms-behind-real-systems-consistent-hashing-rate-limiters-b-trees-lsm-trees-and-vector-search) · [Interview Topic Checklist: What Top Companies Ask](dsa-python.md#58-interview-topic-checklist-what-top-companies-ask)

### Databases track — SQL & PostgreSQL (start after Phase 1)

- **SQL & PostgreSQL** (go in order; every query shows real psql output): [What Is a Database? Tables, Rows, Columns and Keys](sql-postgresql.md#2-what-is-a-database-tables-rows-columns-and-keys) · [SELECT in Depth: Filtering, Sorting and Limiting](sql-postgresql.md#5-select-in-depth-filtering-sorting-and-limiting) · [Aggregation: COUNT, SUM, GROUP BY and HAVING](sql-postgresql.md#8-aggregation-count-sum-group-by-and-having) · [Joins: Combining Tables](sql-postgresql.md#9-joins-combining-tables) · [Subqueries and CTEs (WITH), Including Recursive Queries](sql-postgresql.md#10-subqueries-and-ctes-with-including-recursive-queries) · [Designing Tables: Relationships and Normalisation](sql-postgresql.md#13-designing-tables-relationships-and-normalisation) · [Window Functions: Rankings, Running Totals and Comparing Rows](sql-postgresql.md#16-window-functions-rankings-running-totals-and-comparing-rows) · [Transactions, ACID and Concurrency](sql-postgresql.md#17-transactions-acid-and-concurrency) · [Indexes: Making Lookups Fast](sql-postgresql.md#18-indexes-making-lookups-fast) · [Reading Query Plans with EXPLAIN](sql-postgresql.md#19-reading-query-plans-with-explain) · [pgvector: Vector Search for AI Applications](sql-postgresql.md#26-pgvector-vector-search-for-ai-applications)

### Phase 2 — How JavaScript really works

- **JavaScript:** [Scope, Lexical Scope, Scope Chain](javascript.md#7-scope-lexical-scope-scope-chain) · [Hoisting & Temporal Dead Zone](javascript.md#8-hoisting--temporal-dead-zone) · [Execution Context & Call Stack](javascript.md#10-execution-context--call-stack) · [Closures](javascript.md#11-closures) · [The `this` Keyword](javascript.md#12-the-this-keyword) · [Prototypes & Inheritance](javascript.md#17-prototypes--prototypal-inheritance) · [Classes](javascript.md#18-classes) · [OOP in JavaScript (Object-Oriented Programming)](javascript.md#19-oop-in-javascript-object-oriented-programming) · [Event Loop](javascript.md#25-event-loop) · [Promises (+ polyfills)](javascript.md#27-promises) · [Async / Await](javascript.md#28-async--await) · [Error Handling](javascript.md#33-error-handling) · [Modules (CommonJS vs ESM)](javascript.md#31-modules) · [Regular Expressions](javascript.md#47-regular-expressions)

### Phase 3 — The browser & frontend fundamentals

- **JavaScript:** [DOM & Events (Bubbling, Capturing, Delegation)](javascript.md#35-dom--events) · [Browser Storage & Cookies](javascript.md#36-browser-storage--cookies) · [Web APIs (fetch, AbortController, Workers, rAF, Observers)](javascript.md#42-web-apis) · [Networking for Frontend: What Happens When You Type a URL](javascript.md#48-networking-for-frontend-what-happens-when-you-type-a-url) · [Performance Concepts](javascript.md#49-performance-concepts) · [Security Basics (XSS, CSRF, CORS)](javascript.md#50-security-basics) · [Debounce & Throttle](javascript.md#24-debounce--throttle)

### Phase 4 — TypeScript

- **TypeScript:** [What is TypeScript](typescript.md#1-what-is-typescript) · [Basic Types](typescript.md#3-basic-types) · [any, unknown, never, void](typescript.md#4-any-unknown-never-void) · [Objects: type aliases & interfaces](typescript.md#7-object-types) · [Union & Intersection Types](typescript.md#9-union--intersection-types) · [Type Narrowing & Type Guards](typescript.md#11-type-narrowing--type-guards) · [Discriminated Unions & Exhaustiveness](typescript.md#12-discriminated-unions) · [Generics](typescript.md#16-generics) · [Utility Types (all built-ins + implementations)](typescript.md#22-utility-types) · [TypeScript with React](typescript.md#33-typescript-with-react) · [Runtime Validation with Zod](typescript.md#36-runtime-validation-with-zod)

### Phase 5 — React

- **React:** [What is React](react.md#1-what-is-react) · [JSX](react.md#2-jsx) · [Components](react.md#3-components) · [Props](react.md#4-props) · [State & useState](react.md#5-state--usestate) · [Lists & Keys](react.md#8-lists--keys) · [Forms: Controlled vs Uncontrolled](react.md#9-forms-controlled-vs-uncontrolled) · [useEffect](react.md#12-useeffect) · [useRef](react.md#13-useref) · [useContext & Context API](react.md#14-usecontext--context-api) · [Custom Hooks](react.md#25-custom-hooks) · [Rendering: when & why components re-render](react.md#10-rendering--re-rendering) · [Performance Optimization](react.md#32-performance-optimization) · [React Router](react.md#35-react-router) · [Data Fetching: fetch, TanStack Query](react.md#38-data-fetching) · [Testing React](react.md#45-testing-react)

### Phase 6 — Backend with Node.js

- **Node.js:** [What is Node.js](nodejs.md#1-what-is-nodejs) · [Modules: CommonJS, ESM, require resolution](nodejs.md#2-modules) · [The Node.js Event Loop (phases)](nodejs.md#10-the-nodejs-event-loop) · [Streams](nodejs.md#14-streams) · [Express.js basics](nodejs.md#16-expressjs) · [Middleware](nodejs.md#18-middleware) · [REST API Design](nodejs.md#20-rest-api-design) · [Request Validation](nodejs.md#22-validation) · [Authentication: Sessions, Cookies, JWT, OAuth](nodejs.md#24-authentication) · [Databases: SQL, PostgreSQL, Prisma](nodejs.md#31-sql--prisma) · [SQL Deep Dive: Joins, Window Functions, Query Plans & Locking](nodejs.md#33-sql-deep-dive-joins-window-functions-query-plans--locking) · [Search with PostgreSQL: Full-Text, Fuzzy Matching & Autocomplete](nodejs.md#34-search-with-postgresql-full-text-fuzzy-matching--autocomplete) · [Database Migrations & Seeding](nodejs.md#35-database-migrations--seeding) · [Testing (Jest/Vitest, Supertest, node:test)](nodejs.md#52-testing)

### Phase 7 — Backend with Python & FastAPI

- **Python:** [OOP: Classes & Objects](python.md#19-oop-classes--objects) · [Decorators](python.md#17-decorators) · [Iterators & Generators](python.md#18-iterators--generators) · [Exceptions & Error Handling](python.md#23-exceptions--error-handling) · [Type Hints & typing](python.md#31-type-hints--typing) · [asyncio](python.md#35-asyncio) · [Testing with pytest](python.md#36-testing-with-pytest)
- **FastAPI:** [What is FastAPI](fastapi.md#1-what-is-fastapi) · [Request Body with Pydantic](fastapi.md#6-request-body-with-pydantic) · [Dependency Injection](fastapi.md#11-dependency-injection) · [async def vs def](fastapi.md#13-async-def-vs-def) · [Databases: SQLAlchemy 2.0](fastapi.md#15-databases-sqlalchemy-20) · [Authentication: OAuth2 + JWT](fastapi.md#19-authentication-oauth2--jwt) · [Testing FastAPI](fastapi.md#32-testing-fastapi)

### Phase 8 — Production engineering

- **JavaScript:** [Testing JavaScript (Vitest / Jest)](javascript.md#53-testing-javascript-vitest--jest) · [Production-Grade JavaScript](javascript.md#54-production-grade-javascript) · [Code Smells & Refactoring Catalog](javascript.md#55-code-smells--refactoring-catalog)
- **React:** [Production React Patterns](react.md#51-production-react-patterns) · [Accessibility (a11y)](react.md#47-accessibility-a11y)
- **Node.js:** [Security Best Practices](nodejs.md#40-security) · [OWASP API Security Top 10 (2023) with Examples](nodejs.md#41-owasp-api-security-top-10-2023-with-examples) · [Observability Hands-On: Logs, Metrics, Traces, SLOs & Alerts](nodejs.md#44-observability-hands-on-logs-metrics-traces-slos--alerts) · [BullMQ in Depth](nodejs.md#51-bullmq-in-depth) · [Graceful Shutdown](nodejs.md#54-graceful-shutdown) · [Streaming Responses & Server-Sent Events in Depth](nodejs.md#49-streaming-responses--server-sent-events-in-depth) · [Deployment: Docker, PM2, CI/CD, Nginx](nodejs.md#58-deployment)
- **TypeScript:** [Production TypeScript Best Practices](typescript.md#40-production-typescript-best-practices)
- **Python:** [Production-Grade Python](python.md#42-production-grade-python) · [Packaging & Publishing a Python Library](python.md#43-packaging--publishing-a-python-library)
- **FastAPI:** [Server-Sent Events & Streaming Answers in FastAPI](fastapi.md#27-server-sent-events--streaming-answers-in-fastapi) · [Production Checklist & Best Practices](fastapi.md#41-production-checklist)
- **Best Practices:** [Git in Practice: Everyday Workflow, Fixing History & Recovery](best-practices.md#27-git-in-practice-everyday-workflow-fixing-history--recovery) · [Feature Flags & Safe Rollouts](best-practices.md#29-feature-flags--safe-rollouts) · [Incident Response, On-Call, Postmortems & Living Documentation](best-practices.md#30-incident-response-on-call-postmortems--living-documentation) · [Gotchas Hall of Fame](best-practices.md#31-gotchas-hall-of-fame) · [Checklists](best-practices.md#32-checklists)

### Phase 9 — Senior topics

- **Node.js:** [System Design Basics for Backend Interviews](nodejs.md#63-system-design-basics-for-backend-interviews) · [Microservices, API Gateway, Message Brokers](nodejs.md#55-microservices) · [Resilience: Timeouts, Retries, Circuit Breakers & Load Shedding](nodejs.md#56-resilience-timeouts-retries-circuit-breakers--load-shedding) · [Building & Publishing an npm Package](nodejs.md#60-building--publishing-an-npm-package) · [Monorepos: pnpm Workspaces, Turborepo & Shared Packages](nodejs.md#61-monorepos-pnpm-workspaces-turborepo--shared-packages)
- **React:** [How Hooks Work Under the Hood (+ Children & cloneElement APIs)](react.md#24-how-hooks-work-under-the-hood--children--cloneelement-apis) · [Next.js App Router Deep Dive (+ Animations)](react.md#44-nextjs-app-router-deep-dive--animations)
- **TypeScript:** [Typing React Components: Advanced Patterns](typescript.md#34-typing-react-components-advanced-patterns) · [Advanced TypeScript Features](typescript.md#39-advanced-typescript-features) · [End-to-End Type Safety: Shared Schemas, tRPC & OpenAPI Codegen](typescript.md#37-end-to-end-type-safety-shared-schemas-trpc--openapi-codegen)
- **Python:** [Advanced Python: Attribute Access, Descriptors, Metaclasses & Weak References](python.md#33-advanced-python-attribute-access-descriptors-metaclasses--weak-references)

## Interview revision plan

Go through these in order in the last week before an interview; for each topic, explain it out loud and write the code without looking.

### Core concepts (explain out loud)

- **JavaScript:** [Closures](javascript.md#11-closures) · [Event Loop](javascript.md#25-event-loop) · [The `this` Keyword](javascript.md#12-the-this-keyword) · [Prototypes & Inheritance](javascript.md#17-prototypes--prototypal-inheritance)
- **React:** [Rendering: when & why components re-render](react.md#10-rendering--re-rendering) · [Rules of Hooks](react.md#23-rules-of-hooks) · [Virtual DOM, Reconciliation, Diffing & Fiber](react.md#11-virtual-dom-reconciliation--fiber)
- **Node.js:** [The Node.js Event Loop (phases)](nodejs.md#10-the-nodejs-event-loop) · [Streams](nodejs.md#14-streams)

### Write from memory

- **JavaScript:** [Polyfill Collection](javascript.md#52-polyfill-collection) · [Debounce & Throttle](javascript.md#24-debounce--throttle) · [Promises (+ polyfills)](javascript.md#27-promises)
- **Python:** [Decorators](python.md#17-decorators) · [Iterators & Generators](python.md#18-iterators--generators)

### Predict the output

- **JavaScript:** [Output-Based Questions](javascript.md#57-output-based-questions)
- **React:** [Output / Behaviour Questions](react.md#55-output--behaviour-questions)
- **Node.js:** [Output-Based Questions](nodejs.md#64-output-based-questions)
- **Python:** [Output-Based Questions](python.md#46-output-based-questions)

### Coding & machine coding

- **JavaScript:** [Data Structures & Algorithms in JavaScript](javascript.md#56-data-structures--algorithms-in-javascript)
- **Node.js:** [SQL Deep Dive: Joins, Window Functions, Query Plans & Locking](nodejs.md#33-sql-deep-dive-joins-window-functions-query-plans--locking)
- **Python:** [Data Structures & Algorithms in Python](python.md#44-data-structures--algorithms-in-python) · [Coding Questions (with solutions)](python.md#45-coding-questions)
- **DSA in Python:** [Interview Topic Checklist: What Top Companies Ask](dsa-python.md#58-interview-topic-checklist-what-top-companies-ask) · [Pattern Cheat Sheet: Which Technique When?](dsa-python.md#59-pattern-cheat-sheet-which-technique-when) · [Most Asked DSA Theory Questions](dsa-python.md#60-most-asked-dsa-theory-questions)
- **React:** [Machine Coding Questions (with solutions)](react.md#53-machine-coding-questions) · [Machine Coding II (Carousel, Kanban, Data Table, Wizard, Toasts, Comments)](react.md#54-machine-coding-ii-carousel-kanban-data-table-wizard-toasts-comments)
- **TypeScript:** [Type Challenges](typescript.md#42-type-challenges)
- **SQL & PostgreSQL:** [Classic SQL Interview Problems (with Solutions)](sql-postgresql.md#32-classic-sql-interview-problems-with-solutions) · [SQL and PostgreSQL Cheat Sheet](sql-postgresql.md#33-sql-and-postgresql-cheat-sheet) · [Most Asked SQL and Database Theory Questions](sql-postgresql.md#34-most-asked-sql-and-database-theory-questions)

### System design & production

- **Node.js:** [System Design Basics for Backend Interviews](nodejs.md#63-system-design-basics-for-backend-interviews)
- **Best Practices:** [Gotchas Hall of Fame](best-practices.md#31-gotchas-hall-of-fame)

### Most-asked questions (final pass)

- **JavaScript:** [Most Asked Interview Questions](javascript.md#58-most-asked-interview-questions)
- **TypeScript:** [Most Asked Interview Questions](typescript.md#43-most-asked-interview-questions)
- **React:** [Most Asked Interview Questions](react.md#56-most-asked-interview-questions)
- **Node.js:** [Most Asked Interview Questions](nodejs.md#65-most-asked-interview-questions)
- **Python:** [Most Asked Interview Questions](python.md#47-most-asked-interview-questions)
- **FastAPI:** [Most Asked Interview Questions](fastapi.md#43-most-asked-interview-questions)

## Full index

<details>
<summary><b>JavaScript</b> — 58 sections</summary>

1. [Getting Started: What is JavaScript & Your First Program](javascript.md#1-getting-started-what-is-javascript--your-first-program)
2. [var, let, const](javascript.md#2-var-let-const)
3. [Data Types](javascript.md#3-data-types)
4. [Operators, Control Flow & Loops](javascript.md#4-operators-control-flow--loops)
5. [Type Coercion, == vs ===](javascript.md#5-type-coercion--vs-)
6. [Functions (all types)](javascript.md#6-functions)
7. [Scope, Lexical Scope, Scope Chain](javascript.md#7-scope-lexical-scope-scope-chain)
8. [Hoisting & Temporal Dead Zone](javascript.md#8-hoisting--temporal-dead-zone)
9. [How JavaScript Runs](javascript.md#9-how-javascript-runs)
10. [Execution Context & Call Stack](javascript.md#10-execution-context--call-stack)
11. [Closures](javascript.md#11-closures)
12. [The `this` Keyword](javascript.md#12-the-this-keyword)
13. [call, apply, bind (+ polyfills)](javascript.md#13-call-apply-bind)
14. [Objects in Depth](javascript.md#14-objects-in-depth)
15. [Copying: Shallow vs Deep](javascript.md#15-shallow-vs-deep-copy)
16. [Destructuring, Spread, Rest](javascript.md#16-destructuring-spread-rest)
17. [Prototypes & Inheritance](javascript.md#17-prototypes--prototypal-inheritance)
18. [Classes](javascript.md#18-classes)
19. [OOP in JavaScript (Object-Oriented Programming)](javascript.md#19-oop-in-javascript-object-oriented-programming)
20. [Arrays & Array Methods (+ polyfills)](javascript.md#20-arrays--array-methods)
21. [Strings](javascript.md#21-strings)
22. [Higher-Order Functions, Currying, Composition](javascript.md#22-higher-order-functions-currying-composition)
23. [Functional Programming in Depth](javascript.md#23-functional-programming-in-depth)
24. [Debounce & Throttle](javascript.md#24-debounce--throttle)
25. [Event Loop](javascript.md#25-event-loop)
26. [Callbacks & Callback Hell](javascript.md#26-callbacks--callback-hell)
27. [Promises (+ polyfills)](javascript.md#27-promises)
28. [Async / Await](javascript.md#28-async--await)
29. [Iterators & Generators](javascript.md#29-iterators--generators)
30. [Symbol, Map, Set, WeakMap, WeakSet, WeakRef](javascript.md#30-symbol-map-set-weakmap-weakset)
31. [Modules (CommonJS vs ESM)](javascript.md#31-modules)
32. [Build Tooling: Transpilers, Bundlers & the JS Toolchain](javascript.md#32-build-tooling-transpilers-bundlers--the-js-toolchain)
33. [Error Handling](javascript.md#33-error-handling)
34. [Debugging JavaScript](javascript.md#34-debugging-javascript)
35. [DOM & Events (Bubbling, Capturing, Delegation)](javascript.md#35-dom--events)
36. [Browser Storage & Cookies](javascript.md#36-browser-storage--cookies)
37. [Memory Management & Garbage Collection](javascript.md#37-memory-management--garbage-collection)
38. [Strict Mode](javascript.md#38-strict-mode)
39. [Proxy & Reflect](javascript.md#39-proxy--reflect)
40. [Getters, Setters, Property Descriptors](javascript.md#40-getters-setters-property-descriptors)
41. [Design Patterns](javascript.md#41-design-patterns)
42. [Web APIs (fetch, AbortController, Workers, rAF, Observers)](javascript.md#42-web-apis)
43. [Binary Data & Files in the Browser](javascript.md#43-binary-data--files-in-the-browser)
44. [Browser Internals: Rendering Pipeline, Web Components & Service Workers (PWA)](javascript.md#44-browser-internals-rendering-pipeline-web-components--service-workers-pwa)
45. [Date, Math, Number, Intl](javascript.md#45-date-math-number-intl)
46. [Dates & Time Zones in Depth](javascript.md#46-dates--time-zones-in-depth)
47. [Regular Expressions](javascript.md#47-regular-expressions)
48. [Networking for Frontend: What Happens When You Type a URL](javascript.md#48-networking-for-frontend-what-happens-when-you-type-a-url)
49. [Performance Concepts](javascript.md#49-performance-concepts)
50. [Security Basics (XSS, CSRF, CORS)](javascript.md#50-security-basics)
51. [Modern JS (ES6 → ES2025)](javascript.md#51-modern-js-features)
52. [Polyfill Collection](javascript.md#52-polyfill-collection)
53. [Testing JavaScript (Vitest / Jest)](javascript.md#53-testing-javascript-vitest--jest)
54. [Production-Grade JavaScript](javascript.md#54-production-grade-javascript)
55. [Code Smells & Refactoring Catalog](javascript.md#55-code-smells--refactoring-catalog)
56. [Data Structures & Algorithms in JavaScript](javascript.md#56-data-structures--algorithms-in-javascript)
57. [Output-Based Questions](javascript.md#57-output-based-questions)
58. [Most Asked Interview Questions](javascript.md#58-most-asked-interview-questions)

</details>

<details>
<summary><b>TypeScript</b> — 43 sections</summary>

1. [What is TypeScript](typescript.md#1-what-is-typescript)
2. [Setup & Compilation](typescript.md#2-setup--compilation)
3. [Basic Types](typescript.md#3-basic-types)
4. [any, unknown, never, void](typescript.md#4-any-unknown-never-void)
5. [Type Inference & Annotations](typescript.md#5-type-inference--annotations)
6. [Arrays & Tuples](typescript.md#6-arrays--tuples)
7. [Objects: type aliases & interfaces](typescript.md#7-object-types)
8. [type vs interface](typescript.md#8-type-vs-interface)
9. [Union & Intersection Types](typescript.md#9-union--intersection-types)
10. [Literal Types & `as const`](typescript.md#10-literal-types--as-const)
11. [Type Narrowing & Type Guards](typescript.md#11-type-narrowing--type-guards)
12. [Discriminated Unions & Exhaustiveness](typescript.md#12-discriminated-unions)
13. [Functions](typescript.md#13-functions)
14. [Function Overloads](typescript.md#14-function-overloads)
15. [Enums](typescript.md#15-enums)
16. [Generics](typescript.md#16-generics)
17. [Generic Constraints & Defaults](typescript.md#17-generic-constraints--defaults)
18. [keyof, typeof, Indexed Access Types](typescript.md#18-keyof-typeof-indexed-access)
19. [Mapped Types](typescript.md#19-mapped-types)
20. [Conditional Types & `infer`](typescript.md#20-conditional-types--infer)
21. [Template Literal Types](typescript.md#21-template-literal-types)
22. [Utility Types (all built-ins + implementations)](typescript.md#22-utility-types)
23. [Type Assertions, Non-null `!`, `satisfies`](typescript.md#23-type-assertions-non-null--satisfies)
24. [Classes in TS](typescript.md#24-classes)
25. [Abstract Classes & Interfaces with Classes](typescript.md#25-abstract-classes)
26. [Index Signatures & Record](typescript.md#26-index-signatures)
27. [Readonly & Immutability](typescript.md#27-readonly--immutability)
28. [Modules, Namespaces, Declaration Files (.d.ts)](typescript.md#28-modules-namespaces-declaration-files)
29. [Declaration Merging & Module Augmentation](typescript.md#29-declaration-merging--module-augmentation)
30. [Decorators](typescript.md#30-decorators)
31. [tsconfig.json explained](typescript.md#31-tsconfigjson)
32. [Structural Typing, Variance, Excess Property Checks](typescript.md#32-structural-typing)
33. [TypeScript with React](typescript.md#33-typescript-with-react)
34. [Typing React Components: Advanced Patterns](typescript.md#34-typing-react-components-advanced-patterns)
35. [TypeScript with Node & Express](typescript.md#35-typescript-with-node--express)
36. [Runtime Validation with Zod](typescript.md#36-runtime-validation-with-zod)
37. [End-to-End Type Safety: Shared Schemas, tRPC & OpenAPI Codegen](typescript.md#37-end-to-end-type-safety-shared-schemas-trpc--openapi-codegen)
38. [Branded Types & Other Patterns](typescript.md#38-patterns)
39. [Advanced TypeScript Features](typescript.md#39-advanced-typescript-features)
40. [Production TypeScript Best Practices](typescript.md#40-production-typescript-best-practices)
41. [Common Errors & Fixes](typescript.md#41-common-errors--fixes)
42. [Type Challenges](typescript.md#42-type-challenges)
43. [Most Asked Interview Questions](typescript.md#43-most-asked-interview-questions)

</details>

<details>
<summary><b>React</b> — 56 sections</summary>

1. [What is React](react.md#1-what-is-react)
2. [JSX](react.md#2-jsx)
3. [Components](react.md#3-components)
4. [Props](react.md#4-props)
5. [State & useState](react.md#5-state--usestate)
6. [Event Handling (Synthetic Events)](react.md#6-event-handling)
7. [Conditional Rendering](react.md#7-conditional-rendering)
8. [Lists & Keys](react.md#8-lists--keys)
9. [Forms: Controlled vs Uncontrolled](react.md#9-forms-controlled-vs-uncontrolled)
10. [Rendering: when & why components re-render](react.md#10-rendering--re-rendering)
11. [Virtual DOM, Reconciliation, Diffing & Fiber](react.md#11-virtual-dom-reconciliation--fiber)
12. [useEffect](react.md#12-useeffect)
13. [useRef](react.md#13-useref)
14. [useContext & Context API](react.md#14-usecontext--context-api)
15. [useReducer](react.md#15-usereducer)
16. [useMemo](react.md#16-usememo)
17. [useCallback](react.md#17-usecallback)
18. [React.memo](react.md#18-reactmemo)
19. [useLayoutEffect & useInsertionEffect](react.md#19-uselayouteffect--useinsertioneffect)
20. [useImperativeHandle & forwardRef](react.md#20-useimperativehandle--forwardref)
21. [useId, useTransition, useDeferredValue, useSyncExternalStore, useDebugValue](react.md#21-more-hooks)
22. [React 19: Actions, use, useActionState, useOptimistic, useFormStatus](react.md#22-react-19-features)
23. [Rules of Hooks](react.md#23-rules-of-hooks)
24. [How Hooks Work Under the Hood (+ Children & cloneElement APIs)](react.md#24-how-hooks-work-under-the-hood--children--cloneelement-apis)
25. [Custom Hooks](react.md#25-custom-hooks)
26. [Lifting State Up & Prop Drilling](react.md#26-lifting-state-up--prop-drilling)
27. [Component Lifecycle (Class Components)](react.md#27-component-lifecycle-class-components)
28. [Fragments & Portals](react.md#28-fragments--portals)
29. [Error Boundaries](react.md#29-error-boundaries)
30. [Code Splitting: lazy & Suspense](react.md#30-code-splitting-lazy--suspense)
31. [Advanced Patterns: HOC, Render Props, Compound Components, Controlled Props](react.md#31-advanced-patterns)
32. [Performance Optimization](react.md#32-performance-optimization)
33. [React 18: Concurrent Rendering & Automatic Batching](react.md#33-react-18-concurrent-features)
34. [Strict Mode](react.md#34-strict-mode)
35. [React Router](react.md#35-react-router)
36. [State Management: Redux Toolkit, Zustand, Context](react.md#36-state-management)
37. [State Management II: Choosing a Tool, Jotai, Redux-Saga & State Machines](react.md#37-state-management-ii-choosing-a-tool-jotai-redux-saga--state-machines)
38. [Data Fetching: fetch, TanStack Query](react.md#38-data-fetching)
39. [Styling in React](react.md#39-styling)
40. [Internationalization (i18n), Theming & Dark Mode, Design Tokens](react.md#40-internationalization-i18n-theming--dark-mode-design-tokens)
41. [Rendering Strategies: CSR, SSR, SSG, ISR, RSC](react.md#41-rendering-strategies-csr-ssr-ssg-isr)
42. [Server Components & Next.js Basics](react.md#42-server-components--nextjs-basics)
43. [Hydration](react.md#43-hydration)
44. [Next.js App Router Deep Dive (+ Animations)](react.md#44-nextjs-app-router-deep-dive--animations)
45. [Testing React](react.md#45-testing-react)
46. [Testing React in Depth: Providers, MSW, Async UI, Router, Query & Playwright](react.md#46-testing-react-in-depth-providers-msw-async-ui-router-query--playwright)
47. [Accessibility (a11y)](react.md#47-accessibility-a11y)
48. [Security in React](react.md#48-security-in-react)
49. [Folder Structure & Best Practices](react.md#49-folder-structure--best-practices)
50. [Common Mistakes / Anti-patterns](react.md#50-common-mistakes)
51. [Production React Patterns](react.md#51-production-react-patterns)
52. [Real-time & Rich Interactions: WebSockets, Uploads with Progress, Drag & Drop](react.md#52-real-time--rich-interactions-websockets-uploads-with-progress-drag--drop)
53. [Machine Coding Questions (with solutions)](react.md#53-machine-coding-questions)
54. [Machine Coding II (Carousel, Kanban, Data Table, Wizard, Toasts, Comments)](react.md#54-machine-coding-ii-carousel-kanban-data-table-wizard-toasts-comments)
55. [Output / Behaviour Questions](react.md#55-output--behaviour-questions)
56. [Most Asked Interview Questions](react.md#56-most-asked-interview-questions)

</details>

<details>
<summary><b>Node.js</b> — 65 sections</summary>

1. [What is Node.js](nodejs.md#1-what-is-nodejs)
2. [Modules: CommonJS, ESM, require resolution](nodejs.md#2-modules)
3. [npm, package.json, semver, package-lock](nodejs.md#3-npm--packagejson)
4. [Globals & the process object](nodejs.md#4-globals--process)
5. [Environment Variables & Config](nodejs.md#5-environment-variables)
6. [fs — File System](nodejs.md#6-fs-module)
7. [path, os, url, util, crypto](nodejs.md#7-path-os-url-util-crypto)
8. [Events & EventEmitter](nodejs.md#8-events--eventemitter)
9. [Node Architecture: V8, libuv, Thread Pool](nodejs.md#9-node-architecture)
10. [The Node.js Event Loop (phases)](nodejs.md#10-the-nodejs-event-loop)
11. [process.nextTick vs setImmediate vs setTimeout vs Promises](nodejs.md#11-nexttick-vs-setimmediate-vs-settimeout)
12. [Blocking vs Non-blocking](nodejs.md#12-blocking-vs-non-blocking)
13. [Buffers](nodejs.md#13-buffers)
14. [Streams](nodejs.md#14-streams)
15. [http module — building a server from scratch](nodejs.md#15-http-module)
16. [Express.js basics](nodejs.md#16-expressjs)
17. [Routing](nodejs.md#17-routing)
18. [Middleware](nodejs.md#18-middleware)
19. [Error Handling (Express & process level)](nodejs.md#19-error-handling)
20. [REST API Design](nodejs.md#20-rest-api-design)
21. [Node Networking in Depth: TCP, Keep-Alive, HTTP Caching, Compression & Timeouts](nodejs.md#21-node-networking-in-depth-tcp-keep-alive-http-caching-compression--timeouts)
22. [Request Validation](nodejs.md#22-validation)
23. [API Documentation with OpenAPI (Swagger)](nodejs.md#23-api-documentation-with-openapi-swagger)
24. [Authentication: Sessions, Cookies, JWT, OAuth](nodejs.md#24-authentication)
25. [Authorization: RBAC](nodejs.md#25-authorization)
26. [Password Hashing (bcrypt/argon2)](nodejs.md#26-password-hashing)
27. [Advanced Authentication: OAuth PKCE, MFA (TOTP), Passkeys & Account Security](nodejs.md#27-advanced-authentication-oauth-pkce-mfa-totp-passkeys--account-security)
28. [CORS](nodejs.md#28-cors)
29. [Beyond Express: NestJS & Fastify](nodejs.md#29-beyond-express-nestjs--fastify)
30. [Databases: MongoDB & Mongoose](nodejs.md#30-mongodb--mongoose)
31. [Databases: SQL, PostgreSQL, Prisma](nodejs.md#31-sql--prisma)
32. [SQL vs NoSQL, Indexing, Transactions](nodejs.md#32-sql-vs-nosql-indexing-transactions)
33. [SQL Deep Dive: Joins, Window Functions, Query Plans & Locking](nodejs.md#33-sql-deep-dive-joins-window-functions-query-plans--locking)
34. [Search with PostgreSQL: Full-Text, Fuzzy Matching & Autocomplete](nodejs.md#34-search-with-postgresql-full-text-fuzzy-matching--autocomplete)
35. [Database Migrations & Seeding](nodejs.md#35-database-migrations--seeding)
36. [Data Import Pipelines: Stream CSV → Validate → Batch Insert → Report](nodejs.md#36-data-import-pipelines-stream-csv--validate--batch-insert--report)
37. [File Uploads (multer)](nodejs.md#37-file-uploads)
38. [Caching with Redis](nodejs.md#38-caching-with-redis)
39. [Rate Limiting](nodejs.md#39-rate-limiting)
40. [Security Best Practices](nodejs.md#40-security)
41. [OWASP API Security Top 10 (2023) with Examples](nodejs.md#41-owasp-api-security-top-10-2023-with-examples)
42. [Webhooks & Payment Integration](nodejs.md#42-webhooks--payment-integration)
43. [Logging & Monitoring](nodejs.md#43-logging--monitoring)
44. [Observability Hands-On: Logs, Metrics, Traces, SLOs & Alerts](nodejs.md#44-observability-hands-on-logs-metrics-traces-slos--alerts)
45. [child_process](nodejs.md#45-child_process)
46. [Worker Threads](nodejs.md#46-worker-threads)
47. [Cluster Module & Scaling](nodejs.md#47-cluster--scaling)
48. [WebSockets & Real-time (Socket.IO, SSE)](nodejs.md#48-websockets--real-time)
49. [Streaming Responses & Server-Sent Events in Depth](nodejs.md#49-streaming-responses--server-sent-events-in-depth)
50. [Job Queues & Background Work](nodejs.md#50-job-queues)
51. [BullMQ in Depth](nodejs.md#51-bullmq-in-depth)
52. [Testing (Jest/Vitest, Supertest, node:test)](nodejs.md#52-testing)
53. [Performance & Debugging, Memory Leaks](nodejs.md#53-performance--debugging)
54. [Graceful Shutdown](nodejs.md#54-graceful-shutdown)
55. [Microservices, API Gateway, Message Brokers](nodejs.md#55-microservices)
56. [Resilience: Timeouts, Retries, Circuit Breakers & Load Shedding](nodejs.md#56-resilience-timeouts-retries-circuit-breakers--load-shedding)
57. [GraphQL basics](nodejs.md#57-graphql-basics)
58. [Deployment: Docker, PM2, CI/CD, Nginx](nodejs.md#58-deployment)
59. [Project Structure (MVC / layered)](nodejs.md#59-project-structure)
60. [Building & Publishing an npm Package](nodejs.md#60-building--publishing-an-npm-package)
61. [Monorepos: pnpm Workspaces, Turborepo & Shared Packages](nodejs.md#61-monorepos-pnpm-workspaces-turborepo--shared-packages)
62. [Modern Node Features](nodejs.md#62-modern-node-features)
63. [System Design Basics for Backend Interviews](nodejs.md#63-system-design-basics-for-backend-interviews)
64. [Output-Based Questions](nodejs.md#64-output-based-questions)
65. [Most Asked Interview Questions](nodejs.md#65-most-asked-interview-questions)

</details>

<details>
<summary><b>Python</b> — 47 sections</summary>

1. [Getting Started: What is Python & Your First Program](python.md#1-getting-started-what-is-python--your-first-program)
2. [Variables](python.md#2-variables)
3. [Data Types & Type Conversion](python.md#3-data-types--type-conversion)
4. [Operators](python.md#4-operators)
5. [Strings](python.md#5-strings)
6. [Lists](python.md#6-lists)
7. [Tuples](python.md#7-tuples)
8. [Sets](python.md#8-sets)
9. [Dictionaries](python.md#9-dictionaries)
10. [Control Flow & match-case](python.md#10-control-flow--match-case)
11. [Loops, range, enumerate, zip](python.md#11-loops-range-enumerate-zip)
12. [Comprehensions](python.md#12-comprehensions)
13. [Functions & Arguments](python.md#13-functions--arguments)
14. [Lambda, map, filter, reduce, sorted](python.md#14-lambda-map-filter-reduce-sorted)
15. [Scope: LEGB, global, nonlocal](python.md#15-scope-legb-global-nonlocal)
16. [Closures](python.md#16-closures)
17. [Decorators](python.md#17-decorators)
18. [Iterators & Generators](python.md#18-iterators--generators)
19. [OOP: Classes & Objects](python.md#19-oop-classes--objects)
20. [OOP: 4 Pillars, Inheritance & MRO](python.md#20-oop-4-pillars-inheritance--mro)
21. [Dunder (Magic) Methods](python.md#21-dunder-magic-methods)
22. [Dataclasses, Enums, NamedTuple, __slots__](python.md#22-dataclasses-enums-namedtuple-__slots__)
23. [Exceptions & Error Handling](python.md#23-exceptions--error-handling)
24. [Context Managers](python.md#24-context-managers)
25. [Modules & Packages](python.md#25-modules--packages)
26. [Installing Packages: pip, venv, uv & pyproject.toml](python.md#26-installing-packages-pip-venv-uv--pyprojecttoml)
27. [File Handling, pathlib, JSON, CSV](python.md#27-file-handling-pathlib-json-csv)
28. [Databases Without an ORM (sqlite3, psycopg 3)](python.md#28-databases-without-an-orm-sqlite3-psycopg-3)
29. [Standard Library Essentials](python.md#29-standard-library-essentials)
30. [Scripting & Automation](python.md#30-scripting--automation)
31. [Type Hints & typing](python.md#31-type-hints--typing)
32. [How Python Runs: Bytecode, Memory & Internals](python.md#32-how-python-runs-bytecode-memory--internals)
33. [Advanced Python: Attribute Access, Descriptors, Metaclasses & Weak References](python.md#33-advanced-python-attribute-access-descriptors-metaclasses--weak-references)
34. [Concurrency: GIL, Threads, Processes](python.md#34-concurrency-gil-threads-processes)
35. [asyncio](python.md#35-asyncio)
36. [Testing with pytest](python.md#36-testing-with-pytest)
37. [Logging & Debugging](python.md#37-logging--debugging)
38. [Regular Expressions](python.md#38-regular-expressions)
39. [Code Style: PEP 8 & the Zen of Python](python.md#39-code-style-pep-8--the-zen-of-python)
40. [Pythonic Idioms](python.md#40-pythonic-idioms)
41. [Performance](python.md#41-performance)
42. [Production-Grade Python](python.md#42-production-grade-python)
43. [Packaging & Publishing a Python Library](python.md#43-packaging--publishing-a-python-library)
44. [Data Structures & Algorithms in Python](python.md#44-data-structures--algorithms-in-python)
45. [Coding Questions (with solutions)](python.md#45-coding-questions)
46. [Output-Based Questions](python.md#46-output-based-questions)
47. [Most Asked Interview Questions](python.md#47-most-asked-interview-questions)

</details>

<details>
<summary><b>FastAPI</b> — 43 sections</summary>

1. [What is FastAPI](fastapi.md#1-what-is-fastapi)
2. [Setup & First App](fastapi.md#2-setup--first-app)
3. [Path Operations & HTTP Methods](fastapi.md#3-path-operations--http-methods)
4. [Path Parameters](fastapi.md#4-path-parameters)
5. [Query Parameters](fastapi.md#5-query-parameters)
6. [Request Body with Pydantic](fastapi.md#6-request-body-with-pydantic)
7. [Pydantic v2 Deep Dive](fastapi.md#7-pydantic-v2-deep-dive)
8. [Response Models & Status Codes](fastapi.md#8-response-models--status-codes)
9. [Headers, Cookies, Forms & File Uploads](fastapi.md#9-headers-cookies-forms--file-uploads)
10. [Error Handling](fastapi.md#10-error-handling)
11. [Dependency Injection](fastapi.md#11-dependency-injection)
12. [APIRouter & Project Structure](fastapi.md#12-apirouter--project-structure)
13. [async def vs def](fastapi.md#13-async-def-vs-def)
14. [Settings & Configuration](fastapi.md#14-settings--configuration)
15. [Databases: SQLAlchemy 2.0](fastapi.md#15-databases-sqlalchemy-20)
16. [Async SQLAlchemy](fastapi.md#16-async-sqlalchemy)
17. [Migrations with Alembic](fastapi.md#17-migrations-with-alembic)
18. [Other Databases: SQLModel & MongoDB (Beanie)](fastapi.md#18-other-databases-sqlmodel--mongodb-beanie)
19. [Authentication: OAuth2 + JWT](fastapi.md#19-authentication-oauth2--jwt)
20. [Authorization: Roles, Scopes, Ownership](fastapi.md#20-authorization-roles-scopes-ownership)
21. [Multi-Tenancy & API Versioning](fastapi.md#21-multi-tenancy--api-versioning)
22. [Middleware & CORS](fastapi.md#22-middleware--cors)
23. [Lifespan Events (startup/shutdown)](fastapi.md#23-lifespan-events)
24. [Background Tasks & Job Queues](fastapi.md#24-background-tasks--job-queues)
25. [Task Queues in Depth: Celery & ARQ](fastapi.md#25-task-queues-in-depth-celery--arq)
26. [WebSockets & Streaming](fastapi.md#26-websockets--streaming)
27. [Server-Sent Events & Streaming Answers in FastAPI](fastapi.md#27-server-sent-events--streaming-answers-in-fastapi)
28. [Pagination, Filtering & Sorting](fastapi.md#28-pagination-filtering--sorting)
29. [Caching & Rate Limiting](fastapi.md#29-caching--rate-limiting)
30. [Calling External APIs (httpx)](fastapi.md#30-calling-external-apis)
31. [Integrations: Webhooks, Payments, Email & S3 Uploads](fastapi.md#31-integrations-webhooks-payments-email--s3-uploads)
32. [Testing FastAPI](fastapi.md#32-testing-fastapi)
33. [OpenAPI Docs Customization](fastapi.md#33-openapi-docs-customization)
34. [Logging, Monitoring & Request IDs](fastapi.md#34-logging-monitoring--request-ids)
35. [Observability Hands-On in FastAPI (Metrics, Tracing, Error Tracking)](fastapi.md#35-observability-hands-on-in-fastapi-metrics-tracing-error-tracking)
36. [Security Best Practices](fastapi.md#36-security-best-practices)
37. [OWASP API Top 10 in FastAPI](fastapi.md#37-owasp-api-top-10-in-fastapi)
38. [Performance](fastapi.md#38-performance)
39. [Deployment: Uvicorn, Gunicorn, Docker](fastapi.md#39-deployment)
40. [Complete CRUD Example (layered)](fastapi.md#40-complete-crud-example)
41. [Production Checklist & Best Practices](fastapi.md#41-production-checklist)
42. [FastAPI vs Flask vs Django vs Express](fastapi.md#42-fastapi-vs-flask-vs-django-vs-express)
43. [Most Asked Interview Questions](fastapi.md#43-most-asked-interview-questions)

</details>

<details>
<summary><b>DSA in Python</b> — 60 sections in 11 parts</summary>

**Part 1 — Basic: Programming Fundamentals**

1. [How to Use These Notes](dsa-python.md#1-how-to-use-these-notes)
2. [Python Basics: Values, Variables, Decisions and Functions](dsa-python.md#2-python-basics-values-variables-decisions-and-functions)
3. [Loops and Dry Runs](dsa-python.md#3-loops-and-dry-runs)
4. [Pattern Printing I: Squares and Triangles](dsa-python.md#4-pattern-printing-i-squares-and-triangles)
5. [Pattern Printing II: Pyramids, Diamonds and Hollow Shapes](dsa-python.md#5-pattern-printing-ii-pyramids-diamonds-and-hollow-shapes)
6. [Pattern Printing III: Number and Letter Patterns](dsa-python.md#6-pattern-printing-iii-number-and-letter-patterns)

**Part 2 — Basic: Maths for Programmers**

7. [Working with Digits](dsa-python.md#7-working-with-digits)
8. [Divisors and Prime Numbers](dsa-python.md#8-divisors-and-prime-numbers)
9. [GCD, LCM and Euclid's Algorithm](dsa-python.md#9-gcd-lcm-and-euclids-algorithm)
10. [Sieve of Eratosthenes and Prime Factorisation](dsa-python.md#10-sieve-of-eratosthenes-and-prime-factorisation)
11. [Maths Toolbox: Series, Factorials, Fibonacci, Powers and Modulo](dsa-python.md#11-maths-toolbox-series-factorials-fibonacci-powers-and-modulo)
12. [Number Systems: Decimal and Binary](dsa-python.md#12-number-systems-decimal-and-binary)

**Part 3 — Easy: Core Data Structures and Algorithms**

13. [Big-O: How Fast Is My Code?](dsa-python.md#13-big-o-how-fast-is-my-code)
14. [Recursion Basics](dsa-python.md#14-recursion-basics)
15. [Arrays and Python Lists](dsa-python.md#15-arrays-and-python-lists)
16. [Strings](dsa-python.md#16-strings)
17. [Basic Sorting: Selection, Bubble and Insertion Sort](dsa-python.md#17-basic-sorting-selection-bubble-and-insertion-sort)
18. [Searching: Linear Search and Binary Search](dsa-python.md#18-searching-linear-search-and-binary-search)
19. [Hashing: Dictionaries and Sets](dsa-python.md#19-hashing-dictionaries-and-sets)
20. [Python's Cost Model: What Each Operation Costs](dsa-python.md#20-pythons-cost-model-what-each-operation-costs)

**Part 4 — Moderate: Problem-Solving Techniques**

21. [How to Attack a New Problem](dsa-python.md#21-how-to-attack-a-new-problem)
22. [Two Pointers](dsa-python.md#22-two-pointers)
23. [Sliding Window](dsa-python.md#23-sliding-window)
24. [Prefix Sums](dsa-python.md#24-prefix-sums)
25. [Classic Array Algorithms: Kadane, Majority Vote, Dutch Flag and More](dsa-python.md#25-classic-array-algorithms-kadane-majority-vote-dutch-flag-and-more)
26. [Matrices: 2D Array Problems](dsa-python.md#26-matrices-2d-array-problems)
27. [Intervals: Merge, Insert and Overlap](dsa-python.md#27-intervals-merge-insert-and-overlap)
28. [Binary Search on the Answer](dsa-python.md#28-binary-search-on-the-answer)
29. [Merge Sort and Quick Sort](dsa-python.md#29-merge-sort-and-quick-sort)

**Part 5 — Moderate: Linked Lists, Stacks, Queues and Design**

30. [Classes, Objects and Nodes](dsa-python.md#30-classes-objects-and-nodes)
31. [Linked Lists](dsa-python.md#31-linked-lists)
32. [Linked List Interview Problems](dsa-python.md#32-linked-list-interview-problems)
33. [Stacks](dsa-python.md#33-stacks)
34. [Queues and Deques](dsa-python.md#34-queues-and-deques)
35. [Design Problems: Min Stack, Queue from Stacks, LRU Cache](dsa-python.md#35-design-problems-min-stack-queue-from-stacks-lru-cache)

**Part 6 — Moderate: Trees and Heaps**

36. [Binary Trees and Traversals](dsa-python.md#36-binary-trees-and-traversals)
37. [Binary Tree Interview Problems](dsa-python.md#37-binary-tree-interview-problems)
38. [Binary Search Trees](dsa-python.md#38-binary-search-trees)
39. [Heaps and Priority Queues](dsa-python.md#39-heaps-and-priority-queues)
40. [Tries (Prefix Trees)](dsa-python.md#40-tries-prefix-trees)

**Part 7 — Advanced: Graphs**

41. [Graphs: Representation, BFS and DFS](dsa-python.md#41-graphs-representation-bfs-and-dfs)
42. [Graph Problems: Cycles, Bipartite Graphs and Multi-Source BFS](dsa-python.md#42-graph-problems-cycles-bipartite-graphs-and-multi-source-bfs)
43. [Shortest Paths: Dijkstra](dsa-python.md#43-shortest-paths-dijkstra)
44. [Topological Sort](dsa-python.md#44-topological-sort)
45. [Union-Find (Disjoint Set Union)](dsa-python.md#45-union-find-disjoint-set-union)
46. [Minimum Spanning Trees, Bellman-Ford and Floyd-Warshall](dsa-python.md#46-minimum-spanning-trees-bellman-ford-and-floyd-warshall)

**Part 8 — Advanced: Algorithm Design**

47. [Backtracking](dsa-python.md#47-backtracking)
48. [Greedy Algorithms](dsa-python.md#48-greedy-algorithms)
49. [Dynamic Programming](dsa-python.md#49-dynamic-programming)
50. [Dynamic Programming II: Knapsack, Subsequences, Strings and Intervals](dsa-python.md#50-dynamic-programming-ii-knapsack-subsequences-strings-and-intervals)
51. [Bit Manipulation](dsa-python.md#51-bit-manipulation)

**Part 9 — Advanced: Specialised Topics**

52. [String Algorithms: Palindromes, KMP and Rabin-Karp](dsa-python.md#52-string-algorithms-palindromes-kmp-and-rabin-karp)
53. [Range Queries with Updates: Fenwick Trees and Segment Trees](dsa-python.md#53-range-queries-with-updates-fenwick-trees-and-segment-trees)
54. [Advanced Graphs: Bridges, Strongly Connected Components and Max Flow](dsa-python.md#54-advanced-graphs-bridges-strongly-connected-components-and-max-flow)

**Part 10 — Advanced: Algorithms in the Real World (2026)**

55. [Randomised and Streaming Algorithms: Shuffling, Sampling, Bloom Filters and Sketches](dsa-python.md#55-randomised-and-streaming-algorithms-shuffling-sampling-bloom-filters-and-sketches)
56. [Algorithms Behind Real Systems: Consistent Hashing, Rate Limiters, B-Trees, LSM Trees and Vector Search](dsa-python.md#56-algorithms-behind-real-systems-consistent-hashing-rate-limiters-b-trees-lsm-trees-and-vector-search)
57. [What's New: Recent Breakthroughs and Modern Practice (2022–2026)](dsa-python.md#57-whats-new-recent-breakthroughs-and-modern-practice-20222026)

**Part 11 — Interview Prep: Revision**

58. [Interview Topic Checklist: What Top Companies Ask](dsa-python.md#58-interview-topic-checklist-what-top-companies-ask)
59. [Pattern Cheat Sheet: Which Technique When?](dsa-python.md#59-pattern-cheat-sheet-which-technique-when)
60. [Most Asked DSA Theory Questions](dsa-python.md#60-most-asked-dsa-theory-questions)

</details>

<details>
<summary><b>SQL & PostgreSQL</b> — 34 sections in 7 parts</summary>


**Part 1 — Basic: Databases and Your First Queries**

1. [How to Use These Notes (and Set Up PostgreSQL)](sql-postgresql.md#1-how-to-use-these-notes-and-set-up-postgresql)
2. [What Is a Database? Tables, Rows, Columns and Keys](sql-postgresql.md#2-what-is-a-database-tables-rows-columns-and-keys)
3. [Your First Table: CREATE TABLE, INSERT and SELECT](sql-postgresql.md#3-your-first-table-create-table-insert-and-select)
4. [Data Types and NULL](sql-postgresql.md#4-data-types-and-null)
5. [SELECT in Depth: Filtering, Sorting and Limiting](sql-postgresql.md#5-select-in-depth-filtering-sorting-and-limiting)
6. [Changing Data: UPDATE, DELETE and RETURNING](sql-postgresql.md#6-changing-data-update-delete-and-returning)

**Part 2 — Easy: Asking Bigger Questions**

7. [Functions and Expressions: Text, Numbers, Dates and CASE](sql-postgresql.md#7-functions-and-expressions-text-numbers-dates-and-case)
8. [Aggregation: COUNT, SUM, GROUP BY and HAVING](sql-postgresql.md#8-aggregation-count-sum-group-by-and-having)
9. [Joins: Combining Tables](sql-postgresql.md#9-joins-combining-tables)
10. [Subqueries and CTEs (WITH), Including Recursive Queries](sql-postgresql.md#10-subqueries-and-ctes-with-including-recursive-queries)
11. [Set Operations: UNION, INTERSECT and EXCEPT](sql-postgresql.md#11-set-operations-union-intersect-and-except)

**Part 3 — Moderate: Designing Databases**

12. [Keys and Constraints: Letting the Database Protect Your Data](sql-postgresql.md#12-keys-and-constraints-letting-the-database-protect-your-data)
13. [Designing Tables: Relationships and Normalisation](sql-postgresql.md#13-designing-tables-relationships-and-normalisation)
14. [Changing the Schema: ALTER TABLE and Migrations](sql-postgresql.md#14-changing-the-schema-alter-table-and-migrations)
15. [Views and Materialized Views](sql-postgresql.md#15-views-and-materialized-views)
16. [Window Functions: Rankings, Running Totals and Comparing Rows](sql-postgresql.md#16-window-functions-rankings-running-totals-and-comparing-rows)

**Part 4 — Moderate: Transactions and Performance**

17. [Transactions, ACID and Concurrency](sql-postgresql.md#17-transactions-acid-and-concurrency)
18. [Indexes: Making Lookups Fast](sql-postgresql.md#18-indexes-making-lookups-fast)
19. [Reading Query Plans with EXPLAIN](sql-postgresql.md#19-reading-query-plans-with-explain)
20. [Making Queries Fast: Common Performance Patterns](sql-postgresql.md#20-making-queries-fast-common-performance-patterns)

**Part 5 — Advanced: PostgreSQL Power Features**

21. [JSON and JSONB: Documents Inside PostgreSQL](sql-postgresql.md#21-json-and-jsonb-documents-inside-postgresql)
22. [Arrays, Enums, Ranges and Generated Columns](sql-postgresql.md#22-arrays-enums-ranges-and-generated-columns)
23. [Full-Text Search](sql-postgresql.md#23-full-text-search)
24. [Functions, Procedures and Triggers](sql-postgresql.md#24-functions-procedures-and-triggers)
25. [Upserts, MERGE and Bulk Loading](sql-postgresql.md#25-upserts-merge-and-bulk-loading)
26. [pgvector: Vector Search for AI Applications](sql-postgresql.md#26-pgvector-vector-search-for-ai-applications)

**Part 6 — Advanced: PostgreSQL in Production**

27. [Security: Roles, Permissions, Row-Level Security and SQL Injection](sql-postgresql.md#27-security-roles-permissions-row-level-security-and-sql-injection)
28. [Using PostgreSQL from Python: psycopg, Pooling and SQLAlchemy](sql-postgresql.md#28-using-postgresql-from-python-psycopg-pooling-and-sqlalchemy)
29. [Running PostgreSQL: Backups, Replication, VACUUM, Partitioning and Monitoring](sql-postgresql.md#29-running-postgresql-backups-replication-vacuum-partitioning-and-monitoring)
30. [Scaling PostgreSQL, and What's New in PostgreSQL 17 and 18](sql-postgresql.md#30-scaling-postgresql-and-whats-new-in-postgresql-17-and-18)
31. [PostgreSQL vs MySQL vs SQLite vs SQL Server: Dialect Differences](sql-postgresql.md#31-postgresql-vs-mysql-vs-sqlite-vs-sql-server-dialect-differences)

**Part 7 — Interview Prep: Revision**

32. [Classic SQL Interview Problems (with Solutions)](sql-postgresql.md#32-classic-sql-interview-problems-with-solutions)
33. [SQL and PostgreSQL Cheat Sheet](sql-postgresql.md#33-sql-and-postgresql-cheat-sheet)
34. [Most Asked SQL and Database Theory Questions](sql-postgresql.md#34-most-asked-sql-and-database-theory-questions)

</details>

<details>
<summary><b>Best Practices</b> — 32 sections</summary>

1. [Universal Principles](best-practices.md#1-universal-principles)
2. [Naming](best-practices.md#2-naming)
3. [Functions](best-practices.md#3-functions)
4. [Variables, Data & Immutability](best-practices.md#4-variables-data--immutability)
5. [Control Flow & Readability](best-practices.md#5-control-flow--readability)
6. [Comments & Documentation](best-practices.md#6-comments--documentation)
7. [Project Structure](best-practices.md#7-project-structure)
8. [Error Handling](best-practices.md#8-error-handling)
9. [Async & Concurrency](best-practices.md#9-async--concurrency)
10. [Validation & Handling Outside Data](best-practices.md#10-validation--handling-outside-data)
11. [Money, Dates, IDs & Text](best-practices.md#11-money-dates-ids--text)
12. [TypeScript Practices](best-practices.md#12-typescript-practices)
13. [React Practices](best-practices.md#13-react-practices)
14. [Node.js & Express Practices](best-practices.md#14-nodejs--express-practices)
15. [Python Practices](best-practices.md#15-python-practices)
16. [FastAPI Practices](best-practices.md#16-fastapi-practices)
17. [API Design](best-practices.md#17-api-design)
18. [Database Practices](best-practices.md#18-database-practices)
19. [Security](best-practices.md#19-security)
20. [Performance](best-practices.md#20-performance)
21. [Testing](best-practices.md#21-testing)
22. [Logging, Monitoring & Observability](best-practices.md#22-logging-monitoring--observability)
23. [Configuration & Secrets](best-practices.md#23-configuration--secrets)
24. [Accessibility](best-practices.md#24-accessibility)
25. [Dependencies](best-practices.md#25-dependencies)
26. [Git, Pull Requests & Code Review](best-practices.md#26-git-pull-requests--code-review)
27. [Git in Practice: Everyday Workflow, Fixing History & Recovery](best-practices.md#27-git-in-practice-everyday-workflow-fixing-history--recovery)
28. [CI/CD & Deployment](best-practices.md#28-cicd--deployment)
29. [Feature Flags & Safe Rollouts](best-practices.md#29-feature-flags--safe-rollouts)
30. [Incident Response, On-Call, Postmortems & Living Documentation](best-practices.md#30-incident-response-on-call-postmortems--living-documentation)
31. [Gotchas Hall of Fame](best-practices.md#31-gotchas-hall-of-fame)
32. [Checklists](best-practices.md#32-checklists)

</details>

---

_This README is generated from the files' tables of contents — section links always point to the current sections._
