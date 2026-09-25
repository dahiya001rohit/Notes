# Full-Stack & AI Notes — JavaScript · TypeScript · React · Node.js · Python · FastAPI · DSA · SQL · Data Science · ML · Deep Learning · LLMs · RAG & Agents

Complete notes from absolute basics to production and interviews. Every topic has an explanation, 2–3 examples, best practices, and interview questions. Many code examples were executed/type-checked while writing; bugs those checks caught are collected in the **Gotchas Hall of Fame**.

## Files

| File | Covers | Sections | Lines |
|---|---|---|---|
| [JavaScript](javascript.md) | JavaScript from absolute zero in five levels (Basic → Easy → Moderate → Advanced → Interview Prep): variables, types, operators, decisions, loops, strings, arrays, objects and functions; array methods, destructuring, scope, closures, this, coercion and errors; objects, prototypes, classes, Map/Set, generators, the event loop, promises, async/await, modules, regex and Intl; the DOM, events, storage, fetch, CORS, rendering and web security; functional patterns, debounce/throttle, Proxy, design patterns, memory, performance and ES2020–ES2026; tooling, testing, debugging and production code; polyfills, DSA and output questions. Every example runs on Node.js 24 or headless Chromium with real output | 51 | 7,114 |
| [TypeScript](typescript.md) | Types from basics to advanced type-level programming, TS with React/Node, end-to-end type safety | 43 | 3,779 |
| [React](react.md) | Components & hooks → patterns & performance → state/data → Next.js → testing → production & machine coding | 56 | 7,709 |
| [Node.js](nodejs.md) | Runtime & event loop → Express & APIs → auth & security → databases → queues, observability, system design | 65 | 8,524 |
| [Python](python.md) | Python from absolute zero in five levels (Basic → Easy → Moderate → Advanced → Interview Prep): variables, numbers, strings, decisions and loops; lists, dicts, sets, comprehensions and functions; errors, files, modules and uv, the standard library, classes, dataclasses and type hints; decorators, generators, context managers, regex, Pythonic style, pytest and logging; internals, descriptors, threads, processes, free-threading, asyncio, performance, databases and scripting; production tooling, packaging and what's new in 3.12–3.14. Every example runs on Python 3.14 with real output | 44 | 6,977 |
| [FastAPI](fastapi.md) | Production APIs with FastAPI from zero in five levels (Basic → Easy → Moderate → Advanced → Interview Prep): HTTP and REST, routes, parameters and Pydantic bodies; response models, errors, forms/files and routers; dependency injection, async, settings and lifespan, SQLAlchemy 2.0, JWT auth and authorisation, CORS, testing; pagination, background jobs, WebSockets, SSE streaming for LLMs, webhooks, caching and rate limits; API design, OWASP API Top 10, observability, deployment and serving ML/LLM models. Every response shown was produced by the app (FastAPI 0.141, Python 3.14) | 33 | 4,853 |
| [DSA in Python](dsa-python.md) | Data structures & algorithms from absolute zero in five levels (Basic → Easy → Moderate → Advanced → Interview Prep): Python basics, pattern printing and number theory first, then arrays, hashing, techniques, linked lists, trees, graphs, DP, string algorithms, segment trees, max flow, the algorithms inside real systems (Bloom filters, consistent hashing, B-trees, vector search) and recent breakthroughs, plus a checklist of what top companies ask. Every topic: simple explanation, diagram, tested Python, practice | 60 | 8,364 |
| [SQL & PostgreSQL](sql-postgresql.md) | SQL from zero in five levels (Basic → Easy → Moderate → Advanced → Interview Prep): tables and queries, joins, CTEs, design and normalisation, window functions, transactions and MVCC, indexes and query plans, JSONB, full-text search, pgvector for AI, security, Python (psycopg, SQLAlchemy), backups, replication, scaling, PostgreSQL 17/18, and classic interview problems. Every query run on PostgreSQL with real output | 34 | 5,291 |
| [Data Science](data-science.md) | The Python data toolkit from zero in five levels (Basic → Easy → Moderate → Advanced → Interview Prep): NumPy arrays and broadcasting, pandas 3 (loading, selecting, cleaning, groupby, merge, pivot, time series), Arrow, Polars and DuckDB for bigger data, Matplotlib and Seaborn charts, statistics (distributions, confidence intervals, hypothesis tests, A/B testing), a full EDA and feature preparation for ML, plus pandas interview problems. Every example run with real output and real chart images | 27 | 3,755 |
| [Machine Learning](machine-learning.md) | Machine learning from zero to production in five levels (Basic → Easy → Moderate → Advanced → Interview Prep): the maths explained simply (vectors, gradient descent, loss functions), linear and logistic regression, honest evaluation and metrics, scikit-learn pipelines, cross-validation and tuning (Optuna), regularisation, trees, random forests, XGBoost and LightGBM, SVMs, clustering, PCA/t-SNE, anomalies, forecasting, recommenders, text classification, SHAP, leakage and fairness, serving (ONNX, FastAPI), MLflow, drift monitoring and ML system design. Every example run with real output and charts | 32 | 4,538 |
| [Deep Learning](deep-learning.md) | Deep learning from zero in five levels (Basic → Easy → Moderate → Advanced → Interview Prep): neurons and backpropagation built from scratch in NumPy, PyTorch tensors, autograd and the training loop, training recipes (AdamW, schedules, normalisation, dropout), CNNs, embeddings and RNNs, attention and transformers, a tiny GPT built from scratch, Hugging Face, fine-tuning with Trainer, LoRA/QLoRA with PEFT, autoencoders and diffusion, mixed precision, FSDP, quantisation, distillation, mixture of experts and scaling laws. Every example run on CPU with real output | 20 | 3,009 |
| [LLM Engineering](llm-engineering.md) | Building applications with large language models, from zero, in five levels (Basic → Easy → Moderate → Advanced → Interview Prep): how LLMs work and are trained, tokens and cost, the Claude API from Python (messages, streaming, errors, refusals), prompt engineering, structured outputs, tool use, embeddings and vector search, prompt caching and batching, images and PDFs, evaluation and LLM-as-judge, hallucinations and prompt injection, fine-tuning (SFT, DPO, LoRA), reasoning models, open-weight models and vLLM, LLMOps and LLM system design. Local examples run with real output; API code checked against the official SDK | 21 | 3,167 |
| [RAG and AI Agents](rag-and-agents.md) | Retrieval-augmented generation and agentic AI, from zero, in five levels (Basic → Easy → Moderate → Advanced → Interview Prep): RAG from scratch, loading and chunking, BM25 and vector search, hybrid search, reranking and query rewriting, RAG evaluation, vectorless RAG (full-text, text-to-SQL, tree navigation, agentic search, long context), contextual retrieval, parent documents and GraphRAG, production RAG (freshness, permissions, injection), LangChain, LangGraph, the agent loop, tools, memory and context engineering, agents with LangGraph, multi-agent systems, MCP, agent evaluation and security, and system design. Examples run locally with real output; API code checked against the official SDKs | 21 | 3,936 |
| [Best Practices](best-practices.md) | Every good practice combined across the stack, the Gotchas Hall of Fame, and checklists | 32 | 1,733 |
| **Total** | | **539** | **72,749** |

## How every file is organized

1. **Basics first** — each file starts with getting-started material and builds up.
2. **Core → advanced** — internals, patterns and deep dives come after the fundamentals they depend on.
3. **Production** — testing, security, performance, observability, deployment and best practices.
4. **Interview section last** — DSA/coding questions, output questions, and *Most Asked Interview Questions*.

Conventions: ❌ = wrong/risky, ✅ = recommended · *(caught in these notes)* = a real bug found by testing the examples · code blocks are meant to run as written (imports included).

## AI/ML Engineer roadmap

The AI/ML files form one path, from "I know some Python" to building and shipping ML models, LLM apps, RAG systems and agents. Each file goes **Basic → Easy → Moderate → Advanced → Interview Prep**, never uses an idea before teaching it, and ends every part with a ✅ checkpoint. Do the stages in order; inside a stage, do the parts in order.

| Stage | Study | You're ready to move on when you can… | Build this (portfolio project) |
|---|---|---|---|
| 0. Foundations | [Python](python.md) (basics → OOP → stdlib), [SQL & PostgreSQL](sql-postgresql.md) Parts 1–2, [DSA in Python](dsa-python.md) alongside | Write scripts with functions, classes and files; query and join tables | A CLI tool that loads a CSV into PostgreSQL and answers questions with SQL |
| 1. Data | [Data Science](data-science.md): NumPy, pandas, Matplotlib, Seaborn, statistics | Clean, reshape and chart a messy dataset; run an A/B test | A full EDA notebook on a public dataset, with a written summary |
| 2. Machine learning | [Machine Learning](machine-learning.md) Parts 1–5: maths, scikit-learn, boosting, clustering, explainability | Build a leak-free pipeline, tune it with cross-validation, pick the right metric, explain predictions | A churn or price model with a proper validation report and SHAP explanations |
| 3. Deep learning | [Deep Learning](deep-learning.md): backprop, PyTorch, CNNs, transformers, Hugging Face, LoRA | Train and debug a PyTorch model; fine-tune a pretrained transformer | Fine-tune a small transformer (LoRA) on a text-classification task |
| 4. LLM engineering | [LLM Engineering](llm-engineering.md) Parts 1–4: APIs, prompting, structured outputs, tools, embeddings, evaluation, guardrails | Call a model reliably, get validated JSON, use tools, measure quality with an eval set | An LLM feature (e.g. ticket triage) with structured output and an evaluation harness |
| 5. RAG and agents | [RAG and AI Agents](rag-and-agents.md) Parts 1–5: retrieval, vectorless RAG, LangChain, LangGraph, agents | Build hybrid retrieval, measure recall and faithfulness, build an agent with tools, memory and approvals | A "chat with our docs" app with citations, plus an agent that can act through two tools |
| 6. Production | [ML](machine-learning.md#part-6--advanced-mlops-and-ml-system-design) Part 6 (serving, MLOps, monitoring), [LLM](llm-engineering.md#part-5--advanced-reasoning-open-models-llmops-and-system-design) Part 5 (open models, LLMOps), [RAG](rag-and-agents.md#part-6--advanced-mcp-agent-safety-and-system-design) Part 6 (MCP, agent security, system design), [FastAPI](fastapi.md), [SQL](sql-postgresql.md) Parts 4–6 | Serve a model behind an API, track experiments, monitor drift, trace LLM calls, secure an agent | Deploy one of the projects above with an API, tracing, evals in CI and a cost estimate |
| 7. Interviews | The **Interview Prep** part of every file: coding problems, cheat sheets and most-asked questions, plus DSA | Explain any topic above in plain words and answer a system-design question with numbers | Mock system designs: ML ([framework](machine-learning.md#29-ml-system-design-a-framework-and-a-worked-example)), LLM ([framework](llm-engineering.md#18-llm-system-design-a-framework-and-a-worked-example)), RAG/agents ([framework](rag-and-agents.md#18-rag-and-agent-system-design-a-worked-example)) |

**Where each topic lives** (the tools and topics most asked for AI/ML engineer roles):

| Topic | Start here | Then |
|---|---|---|
| NumPy | [NumPy arrays](data-science.md#2-numpy-arrays-creating-and-inspecting) | [broadcasting](data-science.md#4-vectorised-maths-aggregations-and-broadcasting) · [linear algebra](data-science.md#5-reshaping-stacking-and-linear-algebra-basics) |
| pandas | [Series and DataFrames](data-science.md#6-pandas-series-and-dataframes) | [cleaning](data-science.md#9-cleaning-data-missing-values-duplicates-types-and-text) · [groupby](data-science.md#11-grouping-and-summarising-groupby-and-agg) · [merge](data-science.md#12-combining-tables-merge-join-and-concat) · [time series](data-science.md#14-dates-and-time-series-resample-rolling-and-shift) · [Arrow, Polars, DuckDB](data-science.md#15-bigger-and-faster-memory-arrow-polars-and-duckdb) |
| Matplotlib | [first charts](data-science.md#16-your-first-charts-with-matplotlib) | [layouts and styling](data-science.md#17-matplotlib-in-depth-layouts-styling-and-annotations) · [choosing charts](data-science.md#19-choosing-the-right-chart-and-not-misleading) |
| Seaborn | [statistical charts](data-science.md#18-statistical-charts-with-seaborn) | [EDA](data-science.md#23-a-complete-exploratory-data-analysis-eda) |
| Statistics | [describing data](data-science.md#20-describing-data-averages-spread-outliers-and-correlation) | [distributions and CIs](data-science.md#21-probability-distributions-sampling-and-confidence-intervals) · [A/B testing](data-science.md#22-hypothesis-tests-and-ab-testing) |
| Maths for ML | [vectors and matrices](machine-learning.md#3-maths-for-ml-1-vectors-matrices-and-the-dot-product) | [gradient descent](machine-learning.md#4-maths-for-ml-2-slopes-gradients-and-gradient-descent) · [probabilities and losses](machine-learning.md#5-maths-for-ml-3-probabilities-sigmoid-softmax-and-loss-functions) |
| scikit-learn | [first model](machine-learning.md#6-your-first-model-linear-regression) | [pipelines](machine-learning.md#11-scikit-learn-properly-estimators-pipelines-and-columntransformer) · [cross-validation](machine-learning.md#12-cross-validation-and-hyperparameter-tuning) · [boosting](machine-learning.md#15-ensembles-random-forests-and-gradient-boosting-xgboost-lightgbm-catboost) · [clustering](machine-learning.md#17-clustering-k-means-dbscan-and-hierarchical-clustering) |
| Model evaluation and trust | [classifier metrics](machine-learning.md#9-measuring-classifiers-confusion-matrix-precision-recall-roc-and-pr-curves) | [SHAP](machine-learning.md#23-explaining-models-feature-importance-partial-dependence-and-shap) · [debugging and leakage](machine-learning.md#24-debugging-models-learning-curves-error-analysis-and-leakage) · [fairness](machine-learning.md#25-fairness-privacy-and-responsible-ml) |
| MLOps | [serving models](machine-learning.md#26-saving-and-serving-models-joblib-skops-onnx-and-a-fastapi-endpoint) | [experiment tracking and pipelines](machine-learning.md#27-mlops-experiment-tracking-reproducibility-and-ml-pipelines) · [monitoring and drift](machine-learning.md#28-monitoring-models-in-production-data-drift-concept-drift-and-retraining) |
| Deep learning and PyTorch | [neurons](deep-learning.md#2-neurons-layers-and-activation-functions) · [backprop](deep-learning.md#3-how-networks-learn-backpropagation-from-scratch) | [PyTorch basics](deep-learning.md#4-pytorch-basics-tensors-devices-and-autograd) · [training loop](deep-learning.md#5-your-first-pytorch-model-modules-dataloaders-and-the-training-loop) · [training recipes](deep-learning.md#6-training-recipes-optimisers-learning-rate-schedules-normalisation-and-regularisation) |
| CNNs, RNNs, transformers | [CNNs](deep-learning.md#8-convolutional-neural-networks-cnns-for-images) · [RNNs](deep-learning.md#9-embeddings-and-sequence-models-rnn-lstm-gru) | [attention and transformers](deep-learning.md#10-attention-and-transformers) · [tiny GPT](deep-learning.md#11-build-a-tiny-gpt-from-scratch) |
| Hugging Face | [Hub, Transformers, pipelines](deep-learning.md#12-hugging-face-the-hub-transformers-tokenizers-and-pipelines) | [Trainer fine-tuning](deep-learning.md#13-transfer-learning-and-fine-tuning-with-the-trainer-api) · [LoRA and QLoRA](deep-learning.md#14-parameter-efficient-fine-tuning-lora-and-qlora) |
| Generative AI (images) | [autoencoders, GANs, diffusion](deep-learning.md#15-generative-models-autoencoders-gans-and-diffusion) | [multimodal models](deep-learning.md#17-modern-architectures-and-scaling-mixture-of-experts-state-space-models-and-multimodal-models) |
| LLMs: how they work | [next-token prediction and training](llm-engineering.md#2-how-llms-work-next-token-prediction-pre-training-and-post-training) | [tokens and cost](llm-engineering.md#3-tokens-context-windows-and-cost) · [reasoning models](llm-engineering.md#15-reasoning-models-thinking-effort-and-test-time-compute) |
| LLM APIs and prompting | [first API call](llm-engineering.md#4-your-first-llm-api-call-messages-system-prompts-and-conversations) | [prompt engineering](llm-engineering.md#6-prompt-engineering-clear-instructions-examples-structure-and-chaining) · [structured outputs](llm-engineering.md#7-structured-outputs-getting-reliable-json-with-schemas) · [tool use](llm-engineering.md#8-tool-use-function-calling-letting-the-model-call-your-code) |
| Embeddings and vector search | [embeddings](llm-engineering.md#9-embeddings-and-semantic-search) | [pgvector](sql-postgresql.md#26-pgvector-vector-search-for-ai-applications) · [BM25 vs vectors](rag-and-agents.md#4-keyword-search-bm25-and-vector-search) |
| Fine-tuning LLMs | [SFT, DPO, RL, distillation](llm-engineering.md#14-fine-tuning-llms-sft-preference-tuning-dpo-rl-and-distillation) | [open-weight models and vLLM](llm-engineering.md#16-open-weight-models-and-self-hosting-ollama-vllm-quantisation-and-gpu-sizing) |
| LLM evaluation and safety | [evals and LLM-as-judge](llm-engineering.md#12-evaluating-llm-applications-test-sets-metrics-and-llm-as-judge) | [hallucinations and prompt injection](llm-engineering.md#13-hallucinations-prompt-injection-and-guardrails) · [LLMOps](llm-engineering.md#17-llmops-tracing-monitoring-caching-budgets-and-prompt-versioning) |
| RAG | [RAG from scratch](rag-and-agents.md#2-what-is-rag-retrieval-augmented-generation-from-scratch) · [chunking](rag-and-agents.md#3-loading-and-chunking-documents) | [hybrid and reranking](rag-and-agents.md#5-hybrid-search-reranking-and-query-rewriting) · [evaluating RAG](rag-and-agents.md#6-evaluating-rag-retrieval-metrics-faithfulness-and-failure-modes) · [advanced RAG](rag-and-agents.md#8-advanced-rag-contextual-retrieval-parent-documents-graphrag-and-multi-hop) · [production RAG](rag-and-agents.md#9-production-rag-ingestion-freshness-permissions-security-and-cost) |
| Vectorless RAG | [full-text, SQL, tree navigation, agentic search](rag-and-agents.md#7-vectorless-rag-retrieval-without-embeddings) | [Postgres full-text search](sql-postgresql.md#23-full-text-search) |
| LangChain | [models, prompts, chains, retrievers](rag-and-agents.md#10-langchain-models-prompts-chains-and-retrievers) | [create_agent and middleware](rag-and-agents.md#14-building-agents-with-langchain-and-langgraph) |
| LangGraph | [stateful graphs, checkpoints, interrupts](rag-and-agents.md#11-langgraph-stateful-workflows-as-graphs) | [agents in LangGraph](rag-and-agents.md#14-building-agents-with-langchain-and-langgraph) · [multi-agent](rag-and-agents.md#15-multi-agent-systems-supervisors-handoffs-and-parallel-sub-agents) |
| Agentic AI | [workflows vs agents](rag-and-agents.md#12-ai-agents-workflows-vs-agents-and-the-agent-loop) | [tools, memory, context engineering](rag-and-agents.md#13-designing-agents-tools-memory-planning-and-context-engineering) · [multi-agent systems](rag-and-agents.md#15-multi-agent-systems-supervisors-handoffs-and-parallel-sub-agents) · [evaluating and securing agents](rag-and-agents.md#17-evaluating-securing-and-running-agents-in-production) |
| MCP | [Model Context Protocol](rag-and-agents.md#16-model-context-protocol-mcp-connecting-agents-to-tools-and-data) | [agent security](rag-and-agents.md#17-evaluating-securing-and-running-agents-in-production) |
| SQL and PostgreSQL | [first queries](sql-postgresql.md#3-your-first-table-create-table-insert-and-select) | [joins](sql-postgresql.md#9-joins-combining-tables) · [window functions](sql-postgresql.md#16-window-functions-rankings-running-totals-and-comparing-rows) · [indexes](sql-postgresql.md#18-indexes-making-lookups-fast) · [from Python](sql-postgresql.md#28-using-postgresql-from-python-psycopg-pooling-and-sqlalchemy) |

## Learning roadmap (basics → advanced)

### Phase 1 — Programming basics (pick JS or Python first)

- **JavaScript:** [Getting Started: What JavaScript Is and Your First Program](javascript.md#1-getting-started-what-javascript-is-and-your-first-program) · [Variables: let, const and var](javascript.md#2-variables-let-const-and-var) · [Data Types: Primitives, Objects, null and undefined](javascript.md#3-data-types-primitives-objects-null-and-undefined) · [Operators: Arithmetic, Comparison, Logical, ?? and ?.](javascript.md#4-operators-arithmetic-comparison-logical--and-) · [Functions: Declarations, Expressions, Arrows and Parameters](javascript.md#10-functions-declarations-expressions-arrows-and-parameters) · [Array Methods: map, filter, reduce, find and Friends](javascript.md#11-array-methods-map-filter-reduce-find-and-friends) · [Strings and Template Literals](javascript.md#7-strings-and-template-literals) · [Objects in Depth: Copying, Property Descriptors, Getters/Setters and Immutability](javascript.md#18-objects-in-depth-copying-property-descriptors-getterssetters-and-immutability)
- **Python:** [Getting Started: What Python Is and Your First Program](python.md#1-getting-started-what-python-is-and-your-first-program) · [Variables: Names for Values](python.md#2-variables-names-for-values) · [Numbers, Operators and Type Conversion](python.md#3-numbers-operators-and-type-conversion) · [Making Decisions: if, elif, else and match](python.md#5-making-decisions-if-elif-else-and-match) · [Loops: while, for and range](python.md#6-loops-while-for-and-range) · [Functions: Reusable Blocks of Code](python.md#12-functions-reusable-blocks-of-code) · [Lists: Ordered, Changeable Collections](python.md#7-lists-ordered-changeable-collections) · [Dictionaries: Looking Things Up by Key](python.md#9-dictionaries-looking-things-up-by-key)

### DSA track — study alongside the other phases

- **DSA in Python** (Basic → Easy → Moderate → Advanced → Interview Prep; go in order, each part ends with a checkpoint): [How to Use These Notes](dsa-python.md#1-how-to-use-these-notes) · [Loops and Dry Runs](dsa-python.md#3-loops-and-dry-runs) · [Pattern Printing I: Squares and Triangles](dsa-python.md#4-pattern-printing-i-squares-and-triangles) · [Working with Digits](dsa-python.md#7-working-with-digits) · [Divisors and Prime Numbers](dsa-python.md#8-divisors-and-prime-numbers) · [Big-O: How Fast Is My Code?](dsa-python.md#13-big-o-how-fast-is-my-code) · [Recursion Basics](dsa-python.md#14-recursion-basics) · [Arrays and Python Lists](dsa-python.md#15-arrays-and-python-lists) · [Hashing: Dictionaries and Sets](dsa-python.md#19-hashing-dictionaries-and-sets) · [Two Pointers](dsa-python.md#22-two-pointers) · [Sliding Window](dsa-python.md#23-sliding-window) · [Classic Array Algorithms: Kadane, Majority Vote, Dutch Flag and More](dsa-python.md#25-classic-array-algorithms-kadane-majority-vote-dutch-flag-and-more) · [Linked Lists](dsa-python.md#31-linked-lists) · [Binary Tree Interview Problems](dsa-python.md#37-binary-tree-interview-problems) · [Graphs: Representation, BFS and DFS](dsa-python.md#41-graphs-representation-bfs-and-dfs) · [Dynamic Programming](dsa-python.md#49-dynamic-programming) · [Algorithms Behind Real Systems: Consistent Hashing, Rate Limiters, B-Trees, LSM Trees and Vector Search](dsa-python.md#56-algorithms-behind-real-systems-consistent-hashing-rate-limiters-b-trees-lsm-trees-and-vector-search) · [Interview Topic Checklist: What Top Companies Ask](dsa-python.md#58-interview-topic-checklist-what-top-companies-ask)

### Databases track — SQL & PostgreSQL (start after Phase 1)

- **SQL & PostgreSQL** (go in order; every query shows real psql output): [What Is a Database? Tables, Rows, Columns and Keys](sql-postgresql.md#2-what-is-a-database-tables-rows-columns-and-keys) · [SELECT in Depth: Filtering, Sorting and Limiting](sql-postgresql.md#5-select-in-depth-filtering-sorting-and-limiting) · [Aggregation: COUNT, SUM, GROUP BY and HAVING](sql-postgresql.md#8-aggregation-count-sum-group-by-and-having) · [Joins: Combining Tables](sql-postgresql.md#9-joins-combining-tables) · [Subqueries and CTEs (WITH), Including Recursive Queries](sql-postgresql.md#10-subqueries-and-ctes-with-including-recursive-queries) · [Designing Tables: Relationships and Normalisation](sql-postgresql.md#13-designing-tables-relationships-and-normalisation) · [Window Functions: Rankings, Running Totals and Comparing Rows](sql-postgresql.md#16-window-functions-rankings-running-totals-and-comparing-rows) · [Transactions, ACID and Concurrency](sql-postgresql.md#17-transactions-acid-and-concurrency) · [Indexes: Making Lookups Fast](sql-postgresql.md#18-indexes-making-lookups-fast) · [Reading Query Plans with EXPLAIN](sql-postgresql.md#19-reading-query-plans-with-explain) · [pgvector: Vector Search for AI Applications](sql-postgresql.md#26-pgvector-vector-search-for-ai-applications)

### AI/ML track — 1. Data science (start after Phase 1)

- **Data Science** (NumPy → pandas → charts → statistics; every example runs): [NumPy Arrays: Creating and Inspecting](data-science.md#2-numpy-arrays-creating-and-inspecting) · [pandas Series and DataFrames](data-science.md#6-pandas-series-and-dataframes) · [Cleaning Data: Missing Values, Duplicates, Types and Text](data-science.md#9-cleaning-data-missing-values-duplicates-types-and-text) · [Grouping and Summarising: groupby and agg](data-science.md#11-grouping-and-summarising-groupby-and-agg) · [Combining Tables: merge, join and concat](data-science.md#12-combining-tables-merge-join-and-concat) · [Your First Charts with Matplotlib](data-science.md#16-your-first-charts-with-matplotlib) · [Statistical Charts with Seaborn](data-science.md#18-statistical-charts-with-seaborn) · [Describing Data: Averages, Spread, Outliers and Correlation](data-science.md#20-describing-data-averages-spread-outliers-and-correlation) · [Hypothesis Tests and A/B Testing](data-science.md#22-hypothesis-tests-and-ab-testing) · [A Complete Exploratory Data Analysis (EDA)](data-science.md#23-a-complete-exploratory-data-analysis-eda) · [Preparing Data for Machine Learning: Feature Engineering Basics](data-science.md#24-preparing-data-for-machine-learning-feature-engineering-basics)

### AI/ML track — 2. Machine learning (after data science)

- **Machine Learning** (maths → first models → scikit-learn → trust → MLOps; every example runs): [What Is Machine Learning?](machine-learning.md#2-what-is-machine-learning) · [Maths for ML 2: Slopes, Gradients and Gradient Descent](machine-learning.md#4-maths-for-ml-2-slopes-gradients-and-gradient-descent) · [Your First Model: Linear Regression](machine-learning.md#6-your-first-model-linear-regression) · [Train/Test Splits, Overfitting and Underfitting](machine-learning.md#7-traintest-splits-overfitting-and-underfitting) · [Measuring Classifiers: Confusion Matrix, Precision, Recall, ROC and PR Curves](machine-learning.md#9-measuring-classifiers-confusion-matrix-precision-recall-roc-and-pr-curves) · [scikit-learn Properly: Estimators, Pipelines and ColumnTransformer](machine-learning.md#11-scikit-learn-properly-estimators-pipelines-and-columntransformer) · [Cross-Validation and Hyperparameter Tuning](machine-learning.md#12-cross-validation-and-hyperparameter-tuning) · [Ensembles: Random Forests and Gradient Boosting (XGBoost, LightGBM, CatBoost)](machine-learning.md#15-ensembles-random-forests-and-gradient-boosting-xgboost-lightgbm-catboost) · [Explaining Models: Feature Importance, Partial Dependence and SHAP](machine-learning.md#23-explaining-models-feature-importance-partial-dependence-and-shap) · [Saving and Serving Models: joblib, skops, ONNX and a FastAPI Endpoint](machine-learning.md#26-saving-and-serving-models-joblib-skops-onnx-and-a-fastapi-endpoint) · [ML System Design: A Framework and a Worked Example](machine-learning.md#29-ml-system-design-a-framework-and-a-worked-example)

### AI/ML track — 3. Deep learning (after machine learning)

- **Deep Learning** (neurons → PyTorch → transformers → Hugging Face and LoRA → scale; every example runs): [Neurons, Layers and Activation Functions](deep-learning.md#2-neurons-layers-and-activation-functions) · [How Networks Learn: Backpropagation from Scratch](deep-learning.md#3-how-networks-learn-backpropagation-from-scratch) · [Your First PyTorch Model: Modules, DataLoaders and the Training Loop](deep-learning.md#5-your-first-pytorch-model-modules-dataloaders-and-the-training-loop) · [Training Recipes: Optimisers, Learning-Rate Schedules, Normalisation and Regularisation](deep-learning.md#6-training-recipes-optimisers-learning-rate-schedules-normalisation-and-regularisation) · [Convolutional Neural Networks (CNNs) for Images](deep-learning.md#8-convolutional-neural-networks-cnns-for-images) · [Attention and Transformers](deep-learning.md#10-attention-and-transformers) · [Build a Tiny GPT from Scratch](deep-learning.md#11-build-a-tiny-gpt-from-scratch) · [Hugging Face: The Hub, Transformers, Tokenizers and Pipelines](deep-learning.md#12-hugging-face-the-hub-transformers-tokenizers-and-pipelines) · [Parameter-Efficient Fine-Tuning: LoRA and QLoRA](deep-learning.md#14-parameter-efficient-fine-tuning-lora-and-qlora) · [Making Models Fast and Small: Mixed Precision, Distributed Training, Quantisation and Distillation](deep-learning.md#16-making-models-fast-and-small-mixed-precision-distributed-training-quantisation-and-distillation)

### AI/ML track — 4. LLM engineering (after deep learning)

- **LLM Engineering** (APIs → prompts → tools → evals → production; API code checked against the SDK): [How LLMs Work: Next-Token Prediction, Pre-Training and Post-Training](llm-engineering.md#2-how-llms-work-next-token-prediction-pre-training-and-post-training) · [Tokens, Context Windows and Cost](llm-engineering.md#3-tokens-context-windows-and-cost) · [Your First LLM API Call: Messages, System Prompts and Conversations](llm-engineering.md#4-your-first-llm-api-call-messages-system-prompts-and-conversations) · [Prompt Engineering: Clear Instructions, Examples, Structure and Chaining](llm-engineering.md#6-prompt-engineering-clear-instructions-examples-structure-and-chaining) · [Structured Outputs: Getting Reliable JSON with Schemas](llm-engineering.md#7-structured-outputs-getting-reliable-json-with-schemas) · [Tool Use (Function Calling): Letting the Model Call Your Code](llm-engineering.md#8-tool-use-function-calling-letting-the-model-call-your-code) · [Embeddings and Semantic Search](llm-engineering.md#9-embeddings-and-semantic-search) · [Evaluating LLM Applications: Test Sets, Metrics and LLM-as-Judge](llm-engineering.md#12-evaluating-llm-applications-test-sets-metrics-and-llm-as-judge) · [Hallucinations, Prompt Injection and Guardrails](llm-engineering.md#13-hallucinations-prompt-injection-and-guardrails) · [LLM System Design: A Framework and a Worked Example](llm-engineering.md#18-llm-system-design-a-framework-and-a-worked-example)

### AI/ML track — 5. RAG and agents (after LLM engineering)

- **RAG and AI Agents** (retrieval → vectorless → LangChain/LangGraph → agents → MCP): [What Is RAG? Retrieval-Augmented Generation from Scratch](rag-and-agents.md#2-what-is-rag-retrieval-augmented-generation-from-scratch) · [Loading and Chunking Documents](rag-and-agents.md#3-loading-and-chunking-documents) · [Hybrid Search, Reranking and Query Rewriting](rag-and-agents.md#5-hybrid-search-reranking-and-query-rewriting) · [Evaluating RAG: Retrieval Metrics, Faithfulness and Failure Modes](rag-and-agents.md#6-evaluating-rag-retrieval-metrics-faithfulness-and-failure-modes) · [Vectorless RAG: Retrieval Without Embeddings](rag-and-agents.md#7-vectorless-rag-retrieval-without-embeddings) · [LangGraph: Stateful Workflows as Graphs](rag-and-agents.md#11-langgraph-stateful-workflows-as-graphs) · [AI Agents: Workflows vs Agents and the Agent Loop](rag-and-agents.md#12-ai-agents-workflows-vs-agents-and-the-agent-loop) · [Building Agents with LangChain and LangGraph](rag-and-agents.md#14-building-agents-with-langchain-and-langgraph) · [Model Context Protocol (MCP): Connecting Agents to Tools and Data](rag-and-agents.md#16-model-context-protocol-mcp-connecting-agents-to-tools-and-data) · [RAG and Agent System Design: A Worked Example](rag-and-agents.md#18-rag-and-agent-system-design-a-worked-example)

### Phase 2 — How JavaScript really works

- **JavaScript:** [Scope, Hoisting and the Temporal Dead Zone](javascript.md#13-scope-hoisting-and-the-temporal-dead-zone) · [How JavaScript Runs: Call Stack, Event Loop, Tasks and Microtasks](javascript.md#23-how-javascript-runs-call-stack-event-loop-tasks-and-microtasks) · [Closures](javascript.md#14-closures) · [The this Keyword, call, apply and bind](javascript.md#15-the-this-keyword-call-apply-and-bind) · [Prototypes and Prototypal Inheritance](javascript.md#19-prototypes-and-prototypal-inheritance) · [Classes: Fields, Private Members, Static, Inheritance and OOP](javascript.md#20-classes-fields-private-members-static-inheritance-and-oop) · [Callbacks and Promises](javascript.md#24-callbacks-and-promises) · [async/await: Asynchronous Code That Reads Like Normal Code](javascript.md#25-asyncawait-asynchronous-code-that-reads-like-normal-code) · [Error Handling: try, catch, throw and Custom Errors](javascript.md#17-error-handling-try-catch-throw-and-custom-errors) · [Modules: import, export, ESM vs CommonJS](javascript.md#26-modules-import-export-esm-vs-commonjs) · [Regular Expressions](javascript.md#27-regular-expressions)

### Phase 3 — The browser & frontend fundamentals

- **JavaScript:** [The DOM and Events](javascript.md#29-the-dom-and-events) · [Browser Storage: localStorage, sessionStorage, Cookies and IndexedDB](javascript.md#30-browser-storage-localstorage-sessionstorage-cookies-and-indexeddb) · [Web APIs: fetch, AbortController, URL, Observers and Workers](javascript.md#31-web-apis-fetch-abortcontroller-url-observers-and-workers) · [Networking for Frontend Developers: From URL to Page, HTTP, Caching and CORS](javascript.md#34-networking-for-frontend-developers-from-url-to-page-http-caching-and-cors) · [Performance: How V8 Runs Your Code and How to Make It Fast](javascript.md#41-performance-how-v8-runs-your-code-and-how-to-make-it-fast) · [Frontend Security: XSS, CSRF, CSP, Prototype Pollution and the Supply Chain](javascript.md#35-frontend-security-xss-csrf-csp-prototype-pollution-and-the-supply-chain) · [Debounce and Throttle](javascript.md#37-debounce-and-throttle)

### Phase 4 — TypeScript

- **TypeScript:** [What is TypeScript](typescript.md#1-what-is-typescript) · [Basic Types](typescript.md#3-basic-types) · [any, unknown, never, void](typescript.md#4-any-unknown-never-void) · [Objects: type aliases & interfaces](typescript.md#7-object-types) · [Union & Intersection Types](typescript.md#9-union--intersection-types) · [Type Narrowing & Type Guards](typescript.md#11-type-narrowing--type-guards) · [Discriminated Unions & Exhaustiveness](typescript.md#12-discriminated-unions) · [Generics](typescript.md#16-generics) · [Utility Types (all built-ins + implementations)](typescript.md#22-utility-types) · [TypeScript with React](typescript.md#33-typescript-with-react) · [Runtime Validation with Zod](typescript.md#36-runtime-validation-with-zod)

### Phase 5 — React

- **React:** [What is React](react.md#1-what-is-react) · [JSX](react.md#2-jsx) · [Components](react.md#3-components) · [Props](react.md#4-props) · [State & useState](react.md#5-state--usestate) · [Lists & Keys](react.md#8-lists--keys) · [Forms: Controlled vs Uncontrolled](react.md#9-forms-controlled-vs-uncontrolled) · [useEffect](react.md#12-useeffect) · [useRef](react.md#13-useref) · [useContext & Context API](react.md#14-usecontext--context-api) · [Custom Hooks](react.md#25-custom-hooks) · [Rendering: when & why components re-render](react.md#10-rendering--re-rendering) · [Performance Optimization](react.md#32-performance-optimization) · [React Router](react.md#35-react-router) · [Data Fetching: fetch, TanStack Query](react.md#38-data-fetching) · [Testing React](react.md#45-testing-react)

### Phase 6 — Backend with Node.js

- **Node.js:** [What is Node.js](nodejs.md#1-what-is-nodejs) · [Modules: CommonJS, ESM, require resolution](nodejs.md#2-modules) · [The Node.js Event Loop (phases)](nodejs.md#10-the-nodejs-event-loop) · [Streams](nodejs.md#14-streams) · [Express.js basics](nodejs.md#16-expressjs) · [Middleware](nodejs.md#18-middleware) · [REST API Design](nodejs.md#20-rest-api-design) · [Request Validation](nodejs.md#22-validation) · [Authentication: Sessions, Cookies, JWT, OAuth](nodejs.md#24-authentication) · [Databases: SQL, PostgreSQL, Prisma](nodejs.md#31-sql--prisma) · [SQL Deep Dive: Joins, Window Functions, Query Plans & Locking](nodejs.md#33-sql-deep-dive-joins-window-functions-query-plans--locking) · [Search with PostgreSQL: Full-Text, Fuzzy Matching & Autocomplete](nodejs.md#34-search-with-postgresql-full-text-fuzzy-matching--autocomplete) · [Database Migrations & Seeding](nodejs.md#35-database-migrations--seeding) · [Testing (Jest/Vitest, Supertest, node:test)](nodejs.md#52-testing)

### Phase 7 — Backend with Python & FastAPI

- **Python:** [Classes and Objects](python.md#18-classes-and-objects) · [Closures and Decorators](python.md#23-closures-and-decorators) · [Iterators and Generators: Producing Values Lazily](python.md#24-iterators-and-generators-producing-values-lazily) · [Errors and Exceptions: try, except, raise](python.md#14-errors-and-exceptions-try-except-raise) · [Type Hints and Static Type Checking](python.md#22-type-hints-and-static-type-checking) · [asyncio: async and await](python.md#33-asyncio-async-and-await) · [Testing with pytest](python.md#28-testing-with-pytest)
- **FastAPI:** [How to Use These Notes: APIs, HTTP and What FastAPI Is](fastapi.md#1-how-to-use-these-notes-apis-http-and-what-fastapi-is) · [Request Bodies with Pydantic Models](fastapi.md#5-request-bodies-with-pydantic-models) · [Dependency Injection with Depends](fastapi.md#11-dependency-injection-with-depends) · [async def vs def: Concurrency in FastAPI](fastapi.md#12-async-def-vs-def-concurrency-in-fastapi) · [Databases with SQLAlchemy 2.0: Models, Sessions and CRUD](fastapi.md#14-databases-with-sqlalchemy-20-models-sessions-and-crud) · [Authentication: Password Hashing, JWT and OAuth2](fastapi.md#16-authentication-password-hashing-jwt-and-oauth2) · [Testing FastAPI Apps](fastapi.md#19-testing-fastapi-apps)

### Phase 8 — Production engineering

- **JavaScript:** [Testing JavaScript: Unit, Integration and End-to-End](javascript.md#44-testing-javascript-unit-integration-and-end-to-end) · [Production-Grade JavaScript: Code Quality, Refactoring and Reliability](javascript.md#46-production-grade-javascript-code-quality-refactoring-and-reliability)
- **React:** [Production React Patterns](react.md#51-production-react-patterns) · [Accessibility (a11y)](react.md#47-accessibility-a11y)
- **Node.js:** [Security Best Practices](nodejs.md#40-security) · [OWASP API Security Top 10 (2023) with Examples](nodejs.md#41-owasp-api-security-top-10-2023-with-examples) · [Observability Hands-On: Logs, Metrics, Traces, SLOs & Alerts](nodejs.md#44-observability-hands-on-logs-metrics-traces-slos--alerts) · [BullMQ in Depth](nodejs.md#51-bullmq-in-depth) · [Graceful Shutdown](nodejs.md#54-graceful-shutdown) · [Streaming Responses & Server-Sent Events in Depth](nodejs.md#49-streaming-responses--server-sent-events-in-depth) · [Deployment: Docker, PM2, CI/CD, Nginx](nodejs.md#58-deployment)
- **TypeScript:** [Production TypeScript Best Practices](typescript.md#40-production-typescript-best-practices)
- **Python:** [Production-Grade Python: Project Layout, Configuration, Tooling and CI](python.md#37-production-grade-python-project-layout-configuration-tooling-and-ci) · [Packaging and Publishing a Library](python.md#38-packaging-and-publishing-a-library)
- **FastAPI:** [Streaming Responses and Server-Sent Events (LLM Token Streaming)](fastapi.md#23-streaming-responses-and-server-sent-events-llm-token-streaming) · [FastAPI Cheat Sheet](fastapi.md#32-fastapi-cheat-sheet)
- **Best Practices:** [Git in Practice: Everyday Workflow, Fixing History & Recovery](best-practices.md#27-git-in-practice-everyday-workflow-fixing-history--recovery) · [Feature Flags & Safe Rollouts](best-practices.md#29-feature-flags--safe-rollouts) · [Incident Response, On-Call, Postmortems & Living Documentation](best-practices.md#30-incident-response-on-call-postmortems--living-documentation) · [Gotchas Hall of Fame](best-practices.md#31-gotchas-hall-of-fame) · [Checklists](best-practices.md#32-checklists)

### Phase 9 — Senior topics

- **Node.js:** [System Design Basics for Backend Interviews](nodejs.md#63-system-design-basics-for-backend-interviews) · [Microservices, API Gateway, Message Brokers](nodejs.md#55-microservices) · [Resilience: Timeouts, Retries, Circuit Breakers & Load Shedding](nodejs.md#56-resilience-timeouts-retries-circuit-breakers--load-shedding) · [Building & Publishing an npm Package](nodejs.md#60-building--publishing-an-npm-package) · [Monorepos: pnpm Workspaces, Turborepo & Shared Packages](nodejs.md#61-monorepos-pnpm-workspaces-turborepo--shared-packages)
- **React:** [How Hooks Work Under the Hood (+ Children & cloneElement APIs)](react.md#24-how-hooks-work-under-the-hood--children--cloneelement-apis) · [Next.js App Router Deep Dive (+ Animations)](react.md#44-nextjs-app-router-deep-dive--animations)
- **TypeScript:** [Typing React Components: Advanced Patterns](typescript.md#34-typing-react-components-advanced-patterns) · [Advanced TypeScript Features](typescript.md#39-advanced-typescript-features) · [End-to-End Type Safety: Shared Schemas, tRPC & OpenAPI Codegen](typescript.md#37-end-to-end-type-safety-shared-schemas-trpc--openapi-codegen)
- **Python:** [Advanced Classes: Attribute Lookup, Descriptors, Class Hooks and Metaclasses](python.md#31-advanced-classes-attribute-lookup-descriptors-class-hooks-and-metaclasses)

## Interview revision plan

Go through these in order in the last week before an interview; for each topic, explain it out loud and write the code without looking.

### Core concepts (explain out loud)

- **JavaScript:** [Closures](javascript.md#14-closures) · [How JavaScript Runs: Call Stack, Event Loop, Tasks and Microtasks](javascript.md#23-how-javascript-runs-call-stack-event-loop-tasks-and-microtasks) · [The this Keyword, call, apply and bind](javascript.md#15-the-this-keyword-call-apply-and-bind) · [Prototypes and Prototypal Inheritance](javascript.md#19-prototypes-and-prototypal-inheritance)
- **React:** [Rendering: when & why components re-render](react.md#10-rendering--re-rendering) · [Rules of Hooks](react.md#23-rules-of-hooks) · [Virtual DOM, Reconciliation, Diffing & Fiber](react.md#11-virtual-dom-reconciliation--fiber)
- **Node.js:** [The Node.js Event Loop (phases)](nodejs.md#10-the-nodejs-event-loop) · [Streams](nodejs.md#14-streams)

### Write from memory

- **JavaScript:** [Polyfills and "Implement It Yourself" Questions](javascript.md#47-polyfills-and-implement-it-yourself-questions) · [Debounce and Throttle](javascript.md#37-debounce-and-throttle) · [Callbacks and Promises](javascript.md#24-callbacks-and-promises)
- **Python:** [Closures and Decorators](python.md#23-closures-and-decorators) · [Iterators and Generators: Producing Values Lazily](python.md#24-iterators-and-generators-producing-values-lazily)

### Predict the output

- **JavaScript:** [Output-Based Questions (Predict the Output)](javascript.md#49-output-based-questions-predict-the-output)
- **React:** [Output / Behaviour Questions](react.md#55-output--behaviour-questions)
- **Node.js:** [Output-Based Questions](nodejs.md#64-output-based-questions)
- **Python:** [Output-Based Questions (Predict the Output)](python.md#42-output-based-questions-predict-the-output)

### Coding & machine coding

- **JavaScript:** [DSA in JavaScript: Toolbox and Classic Coding Questions](javascript.md#48-dsa-in-javascript-toolbox-and-classic-coding-questions)
- **Node.js:** [SQL Deep Dive: Joins, Window Functions, Query Plans & Locking](nodejs.md#33-sql-deep-dive-joins-window-functions-query-plans--locking)
- **Python:** [Python's Toolbox for Data Structures and Algorithms](python.md#40-pythons-toolbox-for-data-structures-and-algorithms) · [Interview Coding: Classic Python Problems](python.md#41-interview-coding-classic-python-problems)
- **DSA in Python:** [Interview Topic Checklist: What Top Companies Ask](dsa-python.md#58-interview-topic-checklist-what-top-companies-ask) · [Pattern Cheat Sheet: Which Technique When?](dsa-python.md#59-pattern-cheat-sheet-which-technique-when) · [Most Asked DSA Theory Questions](dsa-python.md#60-most-asked-dsa-theory-questions)
- **React:** [Machine Coding Questions (with solutions)](react.md#53-machine-coding-questions) · [Machine Coding II (Carousel, Kanban, Data Table, Wizard, Toasts, Comments)](react.md#54-machine-coding-ii-carousel-kanban-data-table-wizard-toasts-comments)
- **TypeScript:** [Type Challenges](typescript.md#42-type-challenges)
- **SQL & PostgreSQL:** [Classic SQL Interview Problems (with Solutions)](sql-postgresql.md#32-classic-sql-interview-problems-with-solutions) · [SQL and PostgreSQL Cheat Sheet](sql-postgresql.md#33-sql-and-postgresql-cheat-sheet) · [Most Asked SQL and Database Theory Questions](sql-postgresql.md#34-most-asked-sql-and-database-theory-questions)
- **Data Science:** [Interview Problems: pandas and NumPy](data-science.md#25-interview-problems-pandas-and-numpy) · [Data Science Cheat Sheet](data-science.md#26-data-science-cheat-sheet) · [Most Asked Data Science Theory Questions](data-science.md#27-most-asked-data-science-theory-questions)
- **Machine Learning:** [Interview Coding: ML Algorithms from Scratch in NumPy](machine-learning.md#30-interview-coding-ml-algorithms-from-scratch-in-numpy) · [Machine Learning Cheat Sheet](machine-learning.md#31-machine-learning-cheat-sheet) · [Most Asked Machine Learning Theory Questions](machine-learning.md#32-most-asked-machine-learning-theory-questions)
- **Deep Learning:** [Interview Coding: Deep-Learning Building Blocks](deep-learning.md#18-interview-coding-deep-learning-building-blocks) · [Deep Learning Cheat Sheet](deep-learning.md#19-deep-learning-cheat-sheet) · [Most Asked Deep Learning Theory Questions](deep-learning.md#20-most-asked-deep-learning-theory-questions)
- **LLM Engineering:** [Interview Coding: LLM Engineering Problems](llm-engineering.md#19-interview-coding-llm-engineering-problems) · [LLM Engineering Cheat Sheet](llm-engineering.md#20-llm-engineering-cheat-sheet) · [Most Asked LLM Engineering Theory Questions](llm-engineering.md#21-most-asked-llm-engineering-theory-questions)
- **RAG and AI Agents:** [Interview Coding: RAG and Agent Problems](rag-and-agents.md#19-interview-coding-rag-and-agent-problems) · [RAG and Agents Cheat Sheet](rag-and-agents.md#20-rag-and-agents-cheat-sheet) · [Most Asked RAG and Agent Theory Questions](rag-and-agents.md#21-most-asked-rag-and-agent-theory-questions)

### System design & production

- **Node.js:** [System Design Basics for Backend Interviews](nodejs.md#63-system-design-basics-for-backend-interviews)
- **Best Practices:** [Gotchas Hall of Fame](best-practices.md#31-gotchas-hall-of-fame)

### Most-asked questions (final pass)

- **JavaScript:** [Most Asked JavaScript Interview Questions](javascript.md#51-most-asked-javascript-interview-questions)
- **TypeScript:** [Most Asked Interview Questions](typescript.md#43-most-asked-interview-questions)
- **React:** [Most Asked Interview Questions](react.md#56-most-asked-interview-questions)
- **Node.js:** [Most Asked Interview Questions](nodejs.md#65-most-asked-interview-questions)
- **Python:** [Most Asked Python Interview Questions](python.md#44-most-asked-python-interview-questions)
- **FastAPI:** [Most Asked FastAPI and Backend Interview Questions](fastapi.md#33-most-asked-fastapi-and-backend-interview-questions)

## Full index

<details>
<summary><b>JavaScript</b> — 51 sections in 7 parts</summary>


**Part 1 — Basic: First Steps**

1. [Getting Started: What JavaScript Is and Your First Program](javascript.md#1-getting-started-what-javascript-is-and-your-first-program)
2. [Variables: let, const and var](javascript.md#2-variables-let-const-and-var)
3. [Data Types: Primitives, Objects, null and undefined](javascript.md#3-data-types-primitives-objects-null-and-undefined)
4. [Operators: Arithmetic, Comparison, Logical, ?? and ?.](javascript.md#4-operators-arithmetic-comparison-logical--and-)
5. [Decisions: if, else, switch and the Ternary Operator](javascript.md#5-decisions-if-else-switch-and-the-ternary-operator)
6. [Loops: for, while, for...of and for...in](javascript.md#6-loops-for-while-forof-and-forin)
7. [Strings and Template Literals](javascript.md#7-strings-and-template-literals)
8. [Arrays: Ordered Lists](javascript.md#8-arrays-ordered-lists)
9. [Objects: Grouping Data with Keys](javascript.md#9-objects-grouping-data-with-keys)
10. [Functions: Declarations, Expressions, Arrows and Parameters](javascript.md#10-functions-declarations-expressions-arrows-and-parameters)

**Part 2 — Easy: The Core Language**

11. [Array Methods: map, filter, reduce, find and Friends](javascript.md#11-array-methods-map-filter-reduce-find-and-friends)
12. [Destructuring, Spread and Rest](javascript.md#12-destructuring-spread-and-rest)
13. [Scope, Hoisting and the Temporal Dead Zone](javascript.md#13-scope-hoisting-and-the-temporal-dead-zone)
14. [Closures](javascript.md#14-closures)
15. [The this Keyword, call, apply and bind](javascript.md#15-the-this-keyword-call-apply-and-bind)
16. [Type Conversion, Coercion and == vs ===](javascript.md#16-type-conversion-coercion-and--vs-)
17. [Error Handling: try, catch, throw and Custom Errors](javascript.md#17-error-handling-try-catch-throw-and-custom-errors)

**Part 3 — Moderate: Objects, Async and Modules**

18. [Objects in Depth: Copying, Property Descriptors, Getters/Setters and Immutability](javascript.md#18-objects-in-depth-copying-property-descriptors-getterssetters-and-immutability)
19. [Prototypes and Prototypal Inheritance](javascript.md#19-prototypes-and-prototypal-inheritance)
20. [Classes: Fields, Private Members, Static, Inheritance and OOP](javascript.md#20-classes-fields-private-members-static-inheritance-and-oop)
21. [Map, Set, WeakMap, WeakSet and Symbol](javascript.md#21-map-set-weakmap-weakset-and-symbol)
22. [Iterators, Generators and Iterator Helpers](javascript.md#22-iterators-generators-and-iterator-helpers)
23. [How JavaScript Runs: Call Stack, Event Loop, Tasks and Microtasks](javascript.md#23-how-javascript-runs-call-stack-event-loop-tasks-and-microtasks)
24. [Callbacks and Promises](javascript.md#24-callbacks-and-promises)
25. [async/await: Asynchronous Code That Reads Like Normal Code](javascript.md#25-asyncawait-asynchronous-code-that-reads-like-normal-code)
26. [Modules: import, export, ESM vs CommonJS](javascript.md#26-modules-import-export-esm-vs-commonjs)
27. [Regular Expressions](javascript.md#27-regular-expressions)
28. [Dates, Time Zones, Numbers and Intl](javascript.md#28-dates-time-zones-numbers-and-intl)

**Part 4 — Moderate: JavaScript in the Browser**

29. [The DOM and Events](javascript.md#29-the-dom-and-events)
30. [Browser Storage: localStorage, sessionStorage, Cookies and IndexedDB](javascript.md#30-browser-storage-localstorage-sessionstorage-cookies-and-indexeddb)
31. [Web APIs: fetch, AbortController, URL, Observers and Workers](javascript.md#31-web-apis-fetch-abortcontroller-url-observers-and-workers)
32. [Files, Blobs, Binary Data and Streams](javascript.md#32-files-blobs-binary-data-and-streams)
33. [How Browsers Render Pages: Critical Path, Reflow, Web Components and Service Workers](javascript.md#33-how-browsers-render-pages-critical-path-reflow-web-components-and-service-workers)
34. [Networking for Frontend Developers: From URL to Page, HTTP, Caching and CORS](javascript.md#34-networking-for-frontend-developers-from-url-to-page-http-caching-and-cors)
35. [Frontend Security: XSS, CSRF, CSP, Prototype Pollution and the Supply Chain](javascript.md#35-frontend-security-xss-csrf-csp-prototype-pollution-and-the-supply-chain)

**Part 5 — Advanced: Patterns and Performance**

36. [Functional Programming: Pure Functions, Immutability, Currying and Composition](javascript.md#36-functional-programming-pure-functions-immutability-currying-and-composition)
37. [Debounce and Throttle](javascript.md#37-debounce-and-throttle)
38. [Proxy and Reflect](javascript.md#38-proxy-and-reflect)
39. [Design Patterns in JavaScript](javascript.md#39-design-patterns-in-javascript)
40. [Memory Management, Garbage Collection and Leaks](javascript.md#40-memory-management-garbage-collection-and-leaks)
41. [Performance: How V8 Runs Your Code and How to Make It Fast](javascript.md#41-performance-how-v8-runs-your-code-and-how-to-make-it-fast)
42. [Modern JavaScript: What's New in ES2020–ES2026](javascript.md#42-modern-javascript-whats-new-in-es2020es2026)

**Part 6 — Advanced: Tooling, Testing and Production**

43. [Tooling: npm, Package Managers, Bundlers, Linters and TypeScript](javascript.md#43-tooling-npm-package-managers-bundlers-linters-and-typescript)
44. [Testing JavaScript: Unit, Integration and End-to-End](javascript.md#44-testing-javascript-unit-integration-and-end-to-end)
45. [Debugging JavaScript](javascript.md#45-debugging-javascript)
46. [Production-Grade JavaScript: Code Quality, Refactoring and Reliability](javascript.md#46-production-grade-javascript-code-quality-refactoring-and-reliability)

**Part 7 — Interview Prep: Revision**

47. [Polyfills and "Implement It Yourself" Questions](javascript.md#47-polyfills-and-implement-it-yourself-questions)
48. [DSA in JavaScript: Toolbox and Classic Coding Questions](javascript.md#48-dsa-in-javascript-toolbox-and-classic-coding-questions)
49. [Output-Based Questions (Predict the Output)](javascript.md#49-output-based-questions-predict-the-output)
50. [JavaScript Cheat Sheet](javascript.md#50-javascript-cheat-sheet)
51. [Most Asked JavaScript Interview Questions](javascript.md#51-most-asked-javascript-interview-questions)

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
<summary><b>Python</b> — 44 sections in 7 parts</summary>


**Part 1 — Basic: First Steps**

1. [Getting Started: What Python Is and Your First Program](python.md#1-getting-started-what-python-is-and-your-first-program)
2. [Variables: Names for Values](python.md#2-variables-names-for-values)
3. [Numbers, Operators and Type Conversion](python.md#3-numbers-operators-and-type-conversion)
4. [Strings: Working with Text](python.md#4-strings-working-with-text)
5. [Making Decisions: if, elif, else and match](python.md#5-making-decisions-if-elif-else-and-match)
6. [Loops: while, for and range](python.md#6-loops-while-for-and-range)

**Part 2 — Easy: Collections and Functions**

7. [Lists: Ordered, Changeable Collections](python.md#7-lists-ordered-changeable-collections)
8. [Tuples and Unpacking](python.md#8-tuples-and-unpacking)
9. [Dictionaries: Looking Things Up by Key](python.md#9-dictionaries-looking-things-up-by-key)
10. [Sets: Unique Items and Fast Membership](python.md#10-sets-unique-items-and-fast-membership)
11. [Looping Helpers and Comprehensions](python.md#11-looping-helpers-and-comprehensions)
12. [Functions: Reusable Blocks of Code](python.md#12-functions-reusable-blocks-of-code)
13. [Scope, Lambda and Functional Tools (map, filter, sorted, reduce)](python.md#13-scope-lambda-and-functional-tools-map-filter-sorted-reduce)

**Part 3 — Moderate: Writing Real Programs**

14. [Errors and Exceptions: try, except, raise](python.md#14-errors-and-exceptions-try-except-raise)
15. [Files and Data Formats: pathlib, Text Files, JSON and CSV](python.md#15-files-and-data-formats-pathlib-text-files-json-and-csv)
16. [Modules, Packages, Virtual Environments and uv](python.md#16-modules-packages-virtual-environments-and-uv)
17. [The Standard Library Essentials](python.md#17-the-standard-library-essentials)
18. [Classes and Objects](python.md#18-classes-and-objects)
19. [Inheritance, Composition, Abstract Classes and Protocols](python.md#19-inheritance-composition-abstract-classes-and-protocols)
20. [Special (Dunder) Methods: Making Objects Feel Built-In](python.md#20-special-dunder-methods-making-objects-feel-built-in)
21. [Dataclasses, Enums and __slots__](python.md#21-dataclasses-enums-and-__slots__)
22. [Type Hints and Static Type Checking](python.md#22-type-hints-and-static-type-checking)

**Part 4 — Moderate: Pythonic Techniques, Testing and Logging**

23. [Closures and Decorators](python.md#23-closures-and-decorators)
24. [Iterators and Generators: Producing Values Lazily](python.md#24-iterators-and-generators-producing-values-lazily)
25. [Context Managers: with, Setup and Clean-Up](python.md#25-context-managers-with-setup-and-clean-up)
26. [Regular Expressions](python.md#26-regular-expressions)
27. [Pythonic Code: Idioms, PEP 8 and Linters](python.md#27-pythonic-code-idioms-pep-8-and-linters)
28. [Testing with pytest](python.md#28-testing-with-pytest)
29. [Logging and Debugging](python.md#29-logging-and-debugging)

**Part 5 — Advanced: Internals, Concurrency, Performance and Real-World Tools**

30. [How Python Runs: Bytecode, Memory and Garbage Collection](python.md#30-how-python-runs-bytecode-memory-and-garbage-collection)
31. [Advanced Classes: Attribute Lookup, Descriptors, Class Hooks and Metaclasses](python.md#31-advanced-classes-attribute-lookup-descriptors-class-hooks-and-metaclasses)
32. [Concurrency: Threads, Processes, the GIL and Free-Threaded Python](python.md#32-concurrency-threads-processes-the-gil-and-free-threaded-python)
33. [asyncio: async and await](python.md#33-asyncio-async-and-await)
34. [Performance: Measuring and Speeding Up Python](python.md#34-performance-measuring-and-speeding-up-python)
35. [Working with Databases: sqlite3, psycopg and SQLAlchemy](python.md#35-working-with-databases-sqlite3-psycopg-and-sqlalchemy)
36. [Scripting and Automation: CLIs, subprocess, Files and Scheduling](python.md#36-scripting-and-automation-clis-subprocess-files-and-scheduling)

**Part 6 — Advanced: Production Python**

37. [Production-Grade Python: Project Layout, Configuration, Tooling and CI](python.md#37-production-grade-python-project-layout-configuration-tooling-and-ci)
38. [Packaging and Publishing a Library](python.md#38-packaging-and-publishing-a-library)
39. [What's New in Python 3.12, 3.13 and 3.14](python.md#39-whats-new-in-python-312-313-and-314)

**Part 7 — Interview Prep: Revision**

40. [Python's Toolbox for Data Structures and Algorithms](python.md#40-pythons-toolbox-for-data-structures-and-algorithms)
41. [Interview Coding: Classic Python Problems](python.md#41-interview-coding-classic-python-problems)
42. [Output-Based Questions (Predict the Output)](python.md#42-output-based-questions-predict-the-output)
43. [Python Cheat Sheet](python.md#43-python-cheat-sheet)
44. [Most Asked Python Interview Questions](python.md#44-most-asked-python-interview-questions)

</details>

<details>
<summary><b>FastAPI</b> — 33 sections in 6 parts</summary>


**Part 1 — Basic: How APIs Work and Your First Endpoints**

1. [How to Use These Notes: APIs, HTTP and What FastAPI Is](fastapi.md#1-how-to-use-these-notes-apis-http-and-what-fastapi-is)
2. [Your First FastAPI App](fastapi.md#2-your-first-fastapi-app)
3. [Path Operations: Routes and HTTP Methods](fastapi.md#3-path-operations-routes-and-http-methods)
4. [Path and Query Parameters with Validation](fastapi.md#4-path-and-query-parameters-with-validation)
5. [Request Bodies with Pydantic Models](fastapi.md#5-request-bodies-with-pydantic-models)

**Part 2 — Easy: Data, Responses and Structure**

6. [Pydantic v2 in Depth: Validation, Serialisation and Custom Rules](fastapi.md#6-pydantic-v2-in-depth-validation-serialisation-and-custom-rules)
7. [Response Models, Status Codes and Response Types](fastapi.md#7-response-models-status-codes-and-response-types)
8. [Error Handling: HTTPException, Custom Errors and Consistent Error Responses](fastapi.md#8-error-handling-httpexception-custom-errors-and-consistent-error-responses)
9. [Headers, Cookies, Forms and File Uploads](fastapi.md#9-headers-cookies-forms-and-file-uploads)
10. [APIRouter and Project Structure](fastapi.md#10-apirouter-and-project-structure)

**Part 3 — Moderate: Building a Real API**

11. [Dependency Injection with Depends](fastapi.md#11-dependency-injection-with-depends)
12. [async def vs def: Concurrency in FastAPI](fastapi.md#12-async-def-vs-def-concurrency-in-fastapi)
13. [Settings, Lifespan Events and Shared Resources](fastapi.md#13-settings-lifespan-events-and-shared-resources)
14. [Databases with SQLAlchemy 2.0: Models, Sessions and CRUD](fastapi.md#14-databases-with-sqlalchemy-20-models-sessions-and-crud)
15. [Async Databases, Transactions, Repositories and Migrations](fastapi.md#15-async-databases-transactions-repositories-and-migrations)
16. [Authentication: Password Hashing, JWT and OAuth2](fastapi.md#16-authentication-password-hashing-jwt-and-oauth2)
17. [Authorisation: Roles, Permissions, Ownership and Multi-Tenancy](fastapi.md#17-authorisation-roles-permissions-ownership-and-multi-tenancy)
18. [Middleware and CORS](fastapi.md#18-middleware-and-cors)
19. [Testing FastAPI Apps](fastapi.md#19-testing-fastapi-apps)

**Part 4 — Moderate: API Features**

20. [Pagination, Filtering and Sorting](fastapi.md#20-pagination-filtering-and-sorting)
21. [Background Tasks and Job Queues](fastapi.md#21-background-tasks-and-job-queues)
22. [WebSockets: Real-Time, Two-Way Connections](fastapi.md#22-websockets-real-time-two-way-connections)
23. [Streaming Responses and Server-Sent Events (LLM Token Streaming)](fastapi.md#23-streaming-responses-and-server-sent-events-llm-token-streaming)
24. [Calling Other APIs and Receiving Webhooks](fastapi.md#24-calling-other-apis-and-receiving-webhooks)
25. [Caching and Rate Limiting](fastapi.md#25-caching-and-rate-limiting)

**Part 5 — Advanced: Design, Security and Production**

26. [API Design: Naming, Versioning, Idempotency and Consistency](fastapi.md#26-api-design-naming-versioning-idempotency-and-consistency)
27. [API Security: The OWASP API Top 10 in FastAPI](fastapi.md#27-api-security-the-owasp-api-top-10-in-fastapi)
28. [Observability: Structured Logs, Request IDs, Metrics and Tracing](fastapi.md#28-observability-structured-logs-request-ids-metrics-and-tracing)
29. [Performance and Deployment: Workers, Docker, Proxies and Scaling](fastapi.md#29-performance-and-deployment-workers-docker-proxies-and-scaling)
30. [Serving ML Models and LLM Features with FastAPI](fastapi.md#30-serving-ml-models-and-llm-features-with-fastapi)

**Part 6 — Interview Prep: Revision**

31. [Interview Coding: Build a Small API](fastapi.md#31-interview-coding-build-a-small-api)
32. [FastAPI Cheat Sheet](fastapi.md#32-fastapi-cheat-sheet)
33. [Most Asked FastAPI and Backend Interview Questions](fastapi.md#33-most-asked-fastapi-and-backend-interview-questions)

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
<summary><b>Data Science</b> — 27 sections in 6 parts</summary>


**Part 1 — Basic: NumPy, Fast Arrays of Numbers**

1. [How to Use These Notes (and Set Up Your Data Toolkit)](data-science.md#1-how-to-use-these-notes-and-set-up-your-data-toolkit)
2. [NumPy Arrays: Creating and Inspecting](data-science.md#2-numpy-arrays-creating-and-inspecting)
3. [NumPy Indexing, Slicing and Boolean Masks](data-science.md#3-numpy-indexing-slicing-and-boolean-masks)
4. [Vectorised Maths, Aggregations and Broadcasting](data-science.md#4-vectorised-maths-aggregations-and-broadcasting)
5. [Reshaping, Stacking and Linear Algebra Basics](data-science.md#5-reshaping-stacking-and-linear-algebra-basics)

**Part 2 — Easy: pandas, Working with Tables**

6. [pandas Series and DataFrames](data-science.md#6-pandas-series-and-dataframes)
7. [Reading and Writing Data: CSV, Excel, JSON, Parquet and SQL](data-science.md#7-reading-and-writing-data-csv-excel-json-parquet-and-sql)
8. [Selecting and Filtering: [], loc, iloc and query](data-science.md#8-selecting-and-filtering--loc-iloc-and-query)
9. [Cleaning Data: Missing Values, Duplicates, Types and Text](data-science.md#9-cleaning-data-missing-values-duplicates-types-and-text)
10. [Transforming Data: New Columns, apply, map, binning and assign](data-science.md#10-transforming-data-new-columns-apply-map-binning-and-assign)

**Part 3 — Moderate: Analysing Data with pandas**

11. [Grouping and Summarising: groupby and agg](data-science.md#11-grouping-and-summarising-groupby-and-agg)
12. [Combining Tables: merge, join and concat](data-science.md#12-combining-tables-merge-join-and-concat)
13. [Reshaping: pivot_table, melt, crosstab and explode](data-science.md#13-reshaping-pivot_table-melt-crosstab-and-explode)
14. [Dates and Time Series: resample, rolling and shift](data-science.md#14-dates-and-time-series-resample-rolling-and-shift)
15. [Bigger and Faster: Memory, Arrow, Polars and DuckDB](data-science.md#15-bigger-and-faster-memory-arrow-polars-and-duckdb)

**Part 4 — Moderate: Charts with Matplotlib and Seaborn**

16. [Your First Charts with Matplotlib](data-science.md#16-your-first-charts-with-matplotlib)
17. [Matplotlib in Depth: Layouts, Styling and Annotations](data-science.md#17-matplotlib-in-depth-layouts-styling-and-annotations)
18. [Statistical Charts with Seaborn](data-science.md#18-statistical-charts-with-seaborn)
19. [Choosing the Right Chart (and Not Misleading)](data-science.md#19-choosing-the-right-chart-and-not-misleading)

**Part 5 — Advanced: Statistics and Getting Data Ready for ML**

20. [Describing Data: Averages, Spread, Outliers and Correlation](data-science.md#20-describing-data-averages-spread-outliers-and-correlation)
21. [Probability, Distributions, Sampling and Confidence Intervals](data-science.md#21-probability-distributions-sampling-and-confidence-intervals)
22. [Hypothesis Tests and A/B Testing](data-science.md#22-hypothesis-tests-and-ab-testing)
23. [A Complete Exploratory Data Analysis (EDA)](data-science.md#23-a-complete-exploratory-data-analysis-eda)
24. [Preparing Data for Machine Learning: Feature Engineering Basics](data-science.md#24-preparing-data-for-machine-learning-feature-engineering-basics)

**Part 6 — Interview Prep: Revision**

25. [Interview Problems: pandas and NumPy](data-science.md#25-interview-problems-pandas-and-numpy)
26. [Data Science Cheat Sheet](data-science.md#26-data-science-cheat-sheet)
27. [Most Asked Data Science Theory Questions](data-science.md#27-most-asked-data-science-theory-questions)

</details>

<details>
<summary><b>Machine Learning</b> — 32 sections in 7 parts</summary>


**Part 1 — Basic: What ML Is, and the Maths It Uses**

1. [How to Use These Notes (and What an ML Engineer Does)](machine-learning.md#1-how-to-use-these-notes-and-what-an-ml-engineer-does)
2. [What Is Machine Learning?](machine-learning.md#2-what-is-machine-learning)
3. [Maths for ML 1: Vectors, Matrices and the Dot Product](machine-learning.md#3-maths-for-ml-1-vectors-matrices-and-the-dot-product)
4. [Maths for ML 2: Slopes, Gradients and Gradient Descent](machine-learning.md#4-maths-for-ml-2-slopes-gradients-and-gradient-descent)
5. [Maths for ML 3: Probabilities, Sigmoid, Softmax and Loss Functions](machine-learning.md#5-maths-for-ml-3-probabilities-sigmoid-softmax-and-loss-functions)

**Part 2 — Easy: Your First Models**

6. [Your First Model: Linear Regression](machine-learning.md#6-your-first-model-linear-regression)
7. [Train/Test Splits, Overfitting and Underfitting](machine-learning.md#7-traintest-splits-overfitting-and-underfitting)
8. [Classification with Logistic Regression](machine-learning.md#8-classification-with-logistic-regression)
9. [Measuring Classifiers: Confusion Matrix, Precision, Recall, ROC and PR Curves](machine-learning.md#9-measuring-classifiers-confusion-matrix-precision-recall-roc-and-pr-curves)
10. [k-Nearest Neighbours, Distances and Feature Scaling](machine-learning.md#10-k-nearest-neighbours-distances-and-feature-scaling)

**Part 3 — Moderate: The scikit-learn Toolkit and Strong Models**

11. [scikit-learn Properly: Estimators, Pipelines and ColumnTransformer](machine-learning.md#11-scikit-learn-properly-estimators-pipelines-and-columntransformer)
12. [Cross-Validation and Hyperparameter Tuning](machine-learning.md#12-cross-validation-and-hyperparameter-tuning)
13. [Regularisation: Ridge, Lasso and Elastic Net](machine-learning.md#13-regularisation-ridge-lasso-and-elastic-net)
14. [Decision Trees](machine-learning.md#14-decision-trees)
15. [Ensembles: Random Forests and Gradient Boosting (XGBoost, LightGBM, CatBoost)](machine-learning.md#15-ensembles-random-forests-and-gradient-boosting-xgboost-lightgbm-catboost)
16. [More Classic Models: Support Vector Machines and Naive Bayes](machine-learning.md#16-more-classic-models-support-vector-machines-and-naive-bayes)

**Part 4 — Moderate: Unsupervised Learning and Special Problems**

17. [Clustering: k-Means, DBSCAN and Hierarchical Clustering](machine-learning.md#17-clustering-k-means-dbscan-and-hierarchical-clustering)
18. [Dimensionality Reduction: PCA, t-SNE and UMAP](machine-learning.md#18-dimensionality-reduction-pca-t-sne-and-umap)
19. [Rare Events: Imbalanced Classes and Anomaly Detection](machine-learning.md#19-rare-events-imbalanced-classes-and-anomaly-detection)
20. [Time-Series Forecasting with Machine Learning](machine-learning.md#20-time-series-forecasting-with-machine-learning)
21. [Recommender Systems](machine-learning.md#21-recommender-systems)
22. [Classic Text Classification: Bag of Words and TF-IDF](machine-learning.md#22-classic-text-classification-bag-of-words-and-tf-idf)

**Part 5 — Advanced: Models You Can Trust**

23. [Explaining Models: Feature Importance, Partial Dependence and SHAP](machine-learning.md#23-explaining-models-feature-importance-partial-dependence-and-shap)
24. [Debugging Models: Learning Curves, Error Analysis and Leakage](machine-learning.md#24-debugging-models-learning-curves-error-analysis-and-leakage)
25. [Fairness, Privacy and Responsible ML](machine-learning.md#25-fairness-privacy-and-responsible-ml)

**Part 6 — Advanced: MLOps and ML System Design**

26. [Saving and Serving Models: joblib, skops, ONNX and a FastAPI Endpoint](machine-learning.md#26-saving-and-serving-models-joblib-skops-onnx-and-a-fastapi-endpoint)
27. [MLOps: Experiment Tracking, Reproducibility and ML Pipelines](machine-learning.md#27-mlops-experiment-tracking-reproducibility-and-ml-pipelines)
28. [Monitoring Models in Production: Data Drift, Concept Drift and Retraining](machine-learning.md#28-monitoring-models-in-production-data-drift-concept-drift-and-retraining)
29. [ML System Design: A Framework and a Worked Example](machine-learning.md#29-ml-system-design-a-framework-and-a-worked-example)

**Part 7 — Interview Prep: Revision**

30. [Interview Coding: ML Algorithms from Scratch in NumPy](machine-learning.md#30-interview-coding-ml-algorithms-from-scratch-in-numpy)
31. [Machine Learning Cheat Sheet](machine-learning.md#31-machine-learning-cheat-sheet)
32. [Most Asked Machine Learning Theory Questions](machine-learning.md#32-most-asked-machine-learning-theory-questions)

</details>

<details>
<summary><b>Deep Learning</b> — 20 sections in 6 parts</summary>


**Part 1 — Basic: How Neural Networks Work**

1. [How to Use These Notes (and What Deep Learning Is For)](deep-learning.md#1-how-to-use-these-notes-and-what-deep-learning-is-for)
2. [Neurons, Layers and Activation Functions](deep-learning.md#2-neurons-layers-and-activation-functions)
3. [How Networks Learn: Backpropagation from Scratch](deep-learning.md#3-how-networks-learn-backpropagation-from-scratch)
4. [PyTorch Basics: Tensors, Devices and Autograd](deep-learning.md#4-pytorch-basics-tensors-devices-and-autograd)

**Part 2 — Easy: Training Networks in PyTorch**

5. [Your First PyTorch Model: Modules, DataLoaders and the Training Loop](deep-learning.md#5-your-first-pytorch-model-modules-dataloaders-and-the-training-loop)
6. [Training Recipes: Optimisers, Learning-Rate Schedules, Normalisation and Regularisation](deep-learning.md#6-training-recipes-optimisers-learning-rate-schedules-normalisation-and-regularisation)
7. [Real Data Pipelines: Custom Datasets, Augmentation, Padding and Checkpoints](deep-learning.md#7-real-data-pipelines-custom-datasets-augmentation-padding-and-checkpoints)

**Part 3 — Moderate: Architectures: CNNs, RNNs and Transformers**

8. [Convolutional Neural Networks (CNNs) for Images](deep-learning.md#8-convolutional-neural-networks-cnns-for-images)
9. [Embeddings and Sequence Models (RNN, LSTM, GRU)](deep-learning.md#9-embeddings-and-sequence-models-rnn-lstm-gru)
10. [Attention and Transformers](deep-learning.md#10-attention-and-transformers)
11. [Build a Tiny GPT from Scratch](deep-learning.md#11-build-a-tiny-gpt-from-scratch)

**Part 4 — Moderate: Hugging Face, Fine-Tuning and Generative Models**

12. [Hugging Face: The Hub, Transformers, Tokenizers and Pipelines](deep-learning.md#12-hugging-face-the-hub-transformers-tokenizers-and-pipelines)
13. [Transfer Learning and Fine-Tuning with the Trainer API](deep-learning.md#13-transfer-learning-and-fine-tuning-with-the-trainer-api)
14. [Parameter-Efficient Fine-Tuning: LoRA and QLoRA](deep-learning.md#14-parameter-efficient-fine-tuning-lora-and-qlora)
15. [Generative Models: Autoencoders, GANs and Diffusion](deep-learning.md#15-generative-models-autoencoders-gans-and-diffusion)

**Part 5 — Advanced: Efficiency, Scale and Modern Architectures**

16. [Making Models Fast and Small: Mixed Precision, Distributed Training, Quantisation and Distillation](deep-learning.md#16-making-models-fast-and-small-mixed-precision-distributed-training-quantisation-and-distillation)
17. [Modern Architectures and Scaling: Mixture of Experts, State-Space Models and Multimodal Models](deep-learning.md#17-modern-architectures-and-scaling-mixture-of-experts-state-space-models-and-multimodal-models)

**Part 6 — Interview Prep: Revision**

18. [Interview Coding: Deep-Learning Building Blocks](deep-learning.md#18-interview-coding-deep-learning-building-blocks)
19. [Deep Learning Cheat Sheet](deep-learning.md#19-deep-learning-cheat-sheet)
20. [Most Asked Deep Learning Theory Questions](deep-learning.md#20-most-asked-deep-learning-theory-questions)

</details>

<details>
<summary><b>LLM Engineering</b> — 21 sections in 6 parts</summary>


**Part 1 — Basic: How LLMs Work**

1. [How to Use These Notes (and What an AI Engineer Does)](llm-engineering.md#1-how-to-use-these-notes-and-what-an-ai-engineer-does)
2. [How LLMs Work: Next-Token Prediction, Pre-Training and Post-Training](llm-engineering.md#2-how-llms-work-next-token-prediction-pre-training-and-post-training)
3. [Tokens, Context Windows and Cost](llm-engineering.md#3-tokens-context-windows-and-cost)

**Part 2 — Easy: Calling LLMs from Python**

4. [Your First LLM API Call: Messages, System Prompts and Conversations](llm-engineering.md#4-your-first-llm-api-call-messages-system-prompts-and-conversations)
5. [Streaming, Concurrency, Errors, Retries and Refusals](llm-engineering.md#5-streaming-concurrency-errors-retries-and-refusals)
6. [Prompt Engineering: Clear Instructions, Examples, Structure and Chaining](llm-engineering.md#6-prompt-engineering-clear-instructions-examples-structure-and-chaining)
7. [Structured Outputs: Getting Reliable JSON with Schemas](llm-engineering.md#7-structured-outputs-getting-reliable-json-with-schemas)

**Part 3 — Moderate: Building LLM Features**

8. [Tool Use (Function Calling): Letting the Model Call Your Code](llm-engineering.md#8-tool-use-function-calling-letting-the-model-call-your-code)
9. [Embeddings and Semantic Search](llm-engineering.md#9-embeddings-and-semantic-search)
10. [Controlling Cost and Latency: Prompt Caching, Batching, Routing and Effort](llm-engineering.md#10-controlling-cost-and-latency-prompt-caching-batching-routing-and-effort)
11. [Images, PDFs and Documents: Multimodal Inputs and Citations](llm-engineering.md#11-images-pdfs-and-documents-multimodal-inputs-and-citations)

**Part 4 — Moderate: Quality, Safety and Fine-Tuning**

12. [Evaluating LLM Applications: Test Sets, Metrics and LLM-as-Judge](llm-engineering.md#12-evaluating-llm-applications-test-sets-metrics-and-llm-as-judge)
13. [Hallucinations, Prompt Injection and Guardrails](llm-engineering.md#13-hallucinations-prompt-injection-and-guardrails)
14. [Fine-Tuning LLMs: SFT, Preference Tuning (DPO), RL and Distillation](llm-engineering.md#14-fine-tuning-llms-sft-preference-tuning-dpo-rl-and-distillation)

**Part 5 — Advanced: Reasoning, Open Models, LLMOps and System Design**

15. [Reasoning Models: Thinking, Effort and Test-Time Compute](llm-engineering.md#15-reasoning-models-thinking-effort-and-test-time-compute)
16. [Open-Weight Models and Self-Hosting: Ollama, vLLM, Quantisation and GPU Sizing](llm-engineering.md#16-open-weight-models-and-self-hosting-ollama-vllm-quantisation-and-gpu-sizing)
17. [LLMOps: Tracing, Monitoring, Caching, Budgets and Prompt Versioning](llm-engineering.md#17-llmops-tracing-monitoring-caching-budgets-and-prompt-versioning)
18. [LLM System Design: A Framework and a Worked Example](llm-engineering.md#18-llm-system-design-a-framework-and-a-worked-example)

**Part 6 — Interview Prep: Revision**

19. [Interview Coding: LLM Engineering Problems](llm-engineering.md#19-interview-coding-llm-engineering-problems)
20. [LLM Engineering Cheat Sheet](llm-engineering.md#20-llm-engineering-cheat-sheet)
21. [Most Asked LLM Engineering Theory Questions](llm-engineering.md#21-most-asked-llm-engineering-theory-questions)

</details>

<details>
<summary><b>RAG and AI Agents</b> — 21 sections in 7 parts</summary>


**Part 1 — Basic: RAG Foundations**

1. [How to Use These Notes (and What You Will Build)](rag-and-agents.md#1-how-to-use-these-notes-and-what-you-will-build)
2. [What Is RAG? Retrieval-Augmented Generation from Scratch](rag-and-agents.md#2-what-is-rag-retrieval-augmented-generation-from-scratch)
3. [Loading and Chunking Documents](rag-and-agents.md#3-loading-and-chunking-documents)

**Part 2 — Easy: Retrieval Quality**

4. [Keyword Search (BM25) and Vector Search](rag-and-agents.md#4-keyword-search-bm25-and-vector-search)
5. [Hybrid Search, Reranking and Query Rewriting](rag-and-agents.md#5-hybrid-search-reranking-and-query-rewriting)
6. [Evaluating RAG: Retrieval Metrics, Faithfulness and Failure Modes](rag-and-agents.md#6-evaluating-rag-retrieval-metrics-faithfulness-and-failure-modes)

**Part 3 — Moderate: Beyond Basic RAG**

7. [Vectorless RAG: Retrieval Without Embeddings](rag-and-agents.md#7-vectorless-rag-retrieval-without-embeddings)
8. [Advanced RAG: Contextual Retrieval, Parent Documents, GraphRAG and Multi-Hop](rag-and-agents.md#8-advanced-rag-contextual-retrieval-parent-documents-graphrag-and-multi-hop)
9. [Production RAG: Ingestion, Freshness, Permissions, Security and Cost](rag-and-agents.md#9-production-rag-ingestion-freshness-permissions-security-and-cost)

**Part 4 — Moderate: LangChain and LangGraph**

10. [LangChain: Models, Prompts, Chains and Retrievers](rag-and-agents.md#10-langchain-models-prompts-chains-and-retrievers)
11. [LangGraph: Stateful Workflows as Graphs](rag-and-agents.md#11-langgraph-stateful-workflows-as-graphs)

**Part 5 — Advanced: AI Agents**

12. [AI Agents: Workflows vs Agents and the Agent Loop](rag-and-agents.md#12-ai-agents-workflows-vs-agents-and-the-agent-loop)
13. [Designing Agents: Tools, Memory, Planning and Context Engineering](rag-and-agents.md#13-designing-agents-tools-memory-planning-and-context-engineering)
14. [Building Agents with LangChain and LangGraph](rag-and-agents.md#14-building-agents-with-langchain-and-langgraph)
15. [Multi-Agent Systems: Supervisors, Handoffs and Parallel Sub-Agents](rag-and-agents.md#15-multi-agent-systems-supervisors-handoffs-and-parallel-sub-agents)

**Part 6 — Advanced: MCP, Agent Safety and System Design**

16. [Model Context Protocol (MCP): Connecting Agents to Tools and Data](rag-and-agents.md#16-model-context-protocol-mcp-connecting-agents-to-tools-and-data)
17. [Evaluating, Securing and Running Agents in Production](rag-and-agents.md#17-evaluating-securing-and-running-agents-in-production)
18. [RAG and Agent System Design: A Worked Example](rag-and-agents.md#18-rag-and-agent-system-design-a-worked-example)

**Part 7 — Interview Prep: Revision**

19. [Interview Coding: RAG and Agent Problems](rag-and-agents.md#19-interview-coding-rag-and-agent-problems)
20. [RAG and Agents Cheat Sheet](rag-and-agents.md#20-rag-and-agents-cheat-sheet)
21. [Most Asked RAG and Agent Theory Questions](rag-and-agents.md#21-most-asked-rag-and-agent-theory-questions)

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
