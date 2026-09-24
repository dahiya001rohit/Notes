# Best Practices — Everything Combined

> One cheat sheet of good practices across **JavaScript, TypeScript, React, Node.js, Python and FastAPI**.
> Each rule is short, with ❌/✅ examples where useful. The detailed explanations live in the topic files (`javascript.md`, `typescript.md`, `react.md`, `nodejs.md`, `python.md`, `fastapi.md`).
> Ordered from basics (naming, functions) to production (security, deployment). Checklists at the end.

---

## Table of Contents

1. [Universal Principles](#1-universal-principles)
2. [Naming](#2-naming)
3. [Functions](#3-functions)
4. [Variables, Data & Immutability](#4-variables-data--immutability)
5. [Control Flow & Readability](#5-control-flow--readability)
6. [Comments & Documentation](#6-comments--documentation)
7. [Project Structure](#7-project-structure)
8. [Error Handling](#8-error-handling)
9. [Async & Concurrency](#9-async--concurrency)
10. [Validation & Handling Outside Data](#10-validation--handling-outside-data)
11. [Money, Dates, IDs & Text](#11-money-dates-ids--text)
12. [TypeScript Practices](#12-typescript-practices)
13. [React Practices](#13-react-practices)
14. [Node.js & Express Practices](#14-nodejs--express-practices)
15. [Python Practices](#15-python-practices)
16. [FastAPI Practices](#16-fastapi-practices)
17. [API Design](#17-api-design)
18. [Database Practices](#18-database-practices)
19. [Security](#19-security)
20. [Performance](#20-performance)
21. [Testing](#21-testing)
22. [Logging, Monitoring & Observability](#22-logging-monitoring--observability)
23. [Configuration & Secrets](#23-configuration--secrets)
24. [Accessibility](#24-accessibility)
25. [Dependencies](#25-dependencies)
26. [Git, Pull Requests & Code Review](#26-git-pull-requests--code-review)
27. [Git in Practice: Everyday Workflow, Fixing History & Recovery](#27-git-in-practice-everyday-workflow-fixing-history--recovery)
28. [CI/CD & Deployment](#28-cicd--deployment)
29. [Feature Flags & Safe Rollouts](#29-feature-flags--safe-rollouts)
30. [Incident Response, On-Call, Postmortems & Living Documentation](#30-incident-response-on-call-postmortems--living-documentation)
31. [Gotchas Hall of Fame](#31-gotchas-hall-of-fame)
32. [Checklists](#32-checklists)

---

## 1. Universal Principles

| Principle | Meaning in practice |
|---|---|
| **KISS** — Keep It Simple | The simplest solution that works. Clever code is expensive to read at 3 a.m. |
| **YAGNI** — You Aren't Gonna Need It | Don't build features, options or abstractions "for later". |
| **DRY** — Don't Repeat Yourself | One source of truth for each piece of *knowledge* — but don't merge code that only *looks* similar (wrong abstraction is worse than duplication). |
| **Single Responsibility** | Each function/module/class has one reason to change. |
| **Composition over inheritance** | Combine small pieces instead of deep class hierarchies. |
| **Explicit over implicit** | Clear names, explicit dependencies, no magic globals. |
| **Fail fast** | Validate early (startup config, inputs) and crash loudly on impossible states. |
| **Least privilege** | Every user, service, token and DB account gets only the access it needs. |
| **Separation of concerns** | UI ≠ business logic ≠ data access. |
| **Boy Scout rule** | Leave code a little cleaner than you found it (in small, safe steps). |
| **Make it work → make it right → make it fast** | Correctness first, clarity second, measured optimization last. |

**Readability is the #1 feature**: code is read 10× more than it's written.

---

## 2. Naming

- Names describe **intent**, not type or implementation: `activeUsers`, not `arr2` or `userListArray`.
- **Booleans** read as yes/no questions: `isLoading`, `hasAccess`, `canEdit`, `shouldRetry` (JS) / `is_active` (Python).
- **Functions** start with verbs: `getUser`, `fetchOrders`, `calculateTotal`, `validateEmail`, `sendInvoice`.
- **Event handlers**: `handleClick` inside the component, `onClick` for props.
- **Collections** are plural: `users`, `orderIds`; maps show the key: `usersById`, `priceBySku`.
- **Constants**: `MAX_RETRIES`, `DEFAULT_PAGE_SIZE`; units in names: `timeoutMs`, `amountPaise`, `sizeBytes`, `ttlSeconds`.
- Avoid abbreviations (`usr`, `cnt`, `tmp2`) except universally known ones (`id`, `url`, `api`, `i` in short loops).
- Be consistent: don't mix `fetch`/`get`/`retrieve` for the same idea.

| Language | Variables/functions | Classes/types/components | Constants | Files |
|---|---|---|---|---|
| JS/TS | `camelCase` | `PascalCase` | `UPPER_SNAKE` | `kebab-case.ts` or `PascalCase.tsx` for components |
| Python | `snake_case` | `PascalCase` | `UPPER_SNAKE` | `snake_case.py` |
| React hooks | `useSomething` | — | — | `useSomething.ts` |

```js
// ❌
const d = 86400000;
function proc(a) { return a.filter((x) => x.s === 1); }

// ✅
const MS_PER_DAY = 24 * 60 * 60 * 1000;
function getActiveUsers(users) { return users.filter((user) => user.status === STATUS.ACTIVE); }
```

---

## 3. Functions

- **Small and focused** — does one thing; if the name needs "and", split it.
- **Few parameters** (≤ 3); beyond that use an **options object** (JS) / keyword-only args (Python).
- **Avoid boolean flag parameters** — `createUser(data, true)` is unreadable; use options or two functions.
- **Pure when possible**: same input → same output, no hidden side effects. Push I/O to the edges ("functional core, imperative shell").
- **Don't mutate arguments** — return new data.
- **Return early** (guard clauses) instead of deep nesting.
- **Consistent return types** — don't return a user sometimes and `false` other times.
- **Default parameters** instead of `x = x || default` (which breaks for `0`/`""`).

```js
// ❌
function createUser(name, email, admin, sendMail, trialDays) {}
createUser("Rohit", "r@x.com", true, false, 30);

// ✅
function createUser({ name, email, isAdmin = false, sendWelcomeEmail = true, trialDays = 14 }) {}
createUser({ name: "Rohit", email: "r@x.com", isAdmin: true, sendWelcomeEmail: false, trialDays: 30 });
```

```python
# ✅ keyword-only args make call sites readable
def create_user(name: str, email: str, *, is_admin: bool = False, send_welcome_email: bool = True): ...
create_user("Rohit", "r@x.com", is_admin=True)
```

```python
# ❌ mutable default argument (shared between calls!)
def add_item(item, cart=[]): ...
# ✅
def add_item(item, cart=None):
    cart = [] if cart is None else cart
```

---

## 4. Variables, Data & Immutability

- JS: **`const` by default**, `let` when reassigning, **never `var`**.
- Keep variables in the **smallest scope** possible; declare close to first use.
- **No magic numbers/strings** — name them (`MAX_UPLOAD_MB`, `Status.PAID`).
- Prefer **immutable updates** for shared/state data (spread, `map`, `filter`, `toSorted`, `with`; Python tuples/frozen dataclasses).
- **Don't store derived data** — compute it (`fullName = first + last`, `count = items.length`).
- Use the right structure: **`Map`/`Set`/`dict`/`set`** for lookups (O(1)) instead of searching arrays/lists (O(n)).
- Use `===` (JS) and `is None` (Python); avoid loose equality.
- Use `??` for defaults when `0`/`""`/`false` are valid values; `||` only when any falsy value should fall back.

```js
// ❌ mutation leaks to every holder of the reference
function addTax(order) { order.total *= 1.18; return order; }
// ✅
const addTax = (order) => ({ ...order, total: Math.round(order.total * 1.18) });

// ❌ O(n²)
orders.map((o) => ({ ...o, user: users.find((u) => u.id === o.userId) }));
// ✅ O(n)
const usersById = new Map(users.map((u) => [u.id, u]));
orders.map((o) => ({ ...o, user: usersById.get(o.userId) }));
```

---

## 5. Control Flow & Readability

- **Guard clauses** over nested `if`s.
- **Positive, named conditions**: `const canCheckout = cart.items.length > 0 && user.isVerified;`.
- **Lookup tables** over long `if/else`/`switch` chains for value mappings.
- **Exhaustive handling** of every case (TS `never` check, Python `match` with `case _`, a `default` that throws).
- Avoid nested ternaries; one level is fine.
- One statement per line; always use braces in JS blocks.
- Keep line length reasonable (~100) and let the formatter decide the rest.

```js
// ❌
if (user) { if (user.active) { if (cart.items.length) { checkout(); } } }

// ✅
if (!user?.active) return;
if (cart.items.length === 0) return;
checkout();

// ✅ lookup table
const STATUS_LABEL = { pending: "Pending", shipped: "On the way", delivered: "Delivered" };
const label = STATUS_LABEL[order.status] ?? "Unknown";
```

---

## 6. Comments & Documentation

- Comments explain **why**, not **what** — the code already says what.
- Delete commented-out code (git remembers it).
- `TODO` comments include an owner/ticket: `// TODO(rohit, JIRA-123): remove after v2 migration`.
- Document **public APIs**: JSDoc/TSDoc (JS/TS), docstrings (Python), OpenAPI (HTTP APIs).
- Keep a **README**: what it is, how to run, env vars, scripts, architecture overview.
- Record big decisions in short **ADRs** (Architecture Decision Records): context → decision → consequences. Template, numbering script and keeping docs current: Section 30.

```js
// ❌ increment retry count
retries++;

// ✅ Razorpay sends amounts in paise; our DB stores paise too — no conversion needed
const amountPaise = payload.amount;
```

---

## 7. Project Structure

- Group by **feature/domain** as the project grows (`features/orders/`, `app/users/`), not only by type (`controllers/`, `models/`).
- Separate **layers**: routes/controllers (HTTP) → services (business logic) → repositories (data access).
- Keep **business logic pure and framework-independent** (testable without HTTP/DB).
- One module = one responsibility, small public API; avoid `utils.js` dumping grounds.
- Avoid **circular imports**.
- Keep config, logging, HTTP client and DB setup in dedicated modules (`config`, `logger`, `http`, `db`).
- App factory pattern (`createApp()`) so tests can build the app with different config.

```
src/
  features/orders/     # routes, service, repository, schemas, tests
  features/users/
  lib/                 # config, logger, http client, db
  shared/              # truly shared UI/components/utils
tests/
```

---

## 8. Error Handling

- **Never swallow errors** (`catch {}` / `except: pass`).
- Catch errors **where you can act** (retry, fallback, user message); otherwise let them bubble to a global handler.
- **Throw/raise error objects**, not strings; add context and keep the cause (`new Error(msg, { cause })` / `raise X from e`).
- Create a small **error hierarchy** (`AppError` → `NotFoundError`, `ValidationError`, `ConflictError`) mapped to HTTP status codes in **one** place.
- **Expected failures** (validation, not found) are normal results; **bugs** should crash loudly and be reported.
- **User-facing messages** are friendly and generic; **details go to logs** — never leak stack traces or SQL errors to clients.
- Always clean up (`finally`, `with`, `using`, `try/finally` for loading states).
- Global safety nets: `unhandledrejection`/`error` (browser), `process.on("unhandledRejection")` (Node), exception handlers (FastAPI), error boundaries (React).
- Catch **specific** exceptions in Python; never a bare `except:`.

```js
// ❌
try { await saveOrder(order); } catch (e) {}

// ✅
try {
  await saveOrder(order);
} catch (err) {
  throw new Error(`Failed to save order ${order.id}`, { cause: err });
}
```

```python
# ✅
try:
    user = repo.get(user_id)
except DatabaseError as e:
    raise ServiceUnavailable("Could not load user") from e
```

---

## 9. Async & Concurrency

- Every network call needs a **timeout** (`AbortSignal.timeout`, `httpx.Timeout`, DB statement timeouts).
- **Retry only transient errors** (network, 429, 5xx) with **exponential backoff + jitter**; never blindly retry POSTs without **idempotency keys**.
- **Cancel** work nobody needs (AbortController on unmount/new search; cancel tasks on shutdown).
- Guard against **race conditions**: latest-request-wins, disable double submits, DB constraints/locks for concurrent writes.
- Run independent work in **parallel** (`Promise.all`, `asyncio.gather`/`TaskGroup`), with **concurrency limits** for large batches.
- Always `await`/return promises — no floating promises (lint rule `no-floating-promises`). `forEach` doesn't await.
- **Never block the event loop**: no sync I/O or heavy CPU in Node request handlers / FastAPI `async def` routes — use workers, process pools or queues.
- Move slow/unreliable work (emails, reports, webhooks, image processing) to **background job queues** with retries.
- Clean up timers, intervals, listeners, subscriptions and connections.

```js
// ✅ timeout + retry transient only + idempotency for writes
await withRetry(() => fetch(url, {
  method: "POST",
  headers: { "Idempotency-Key": orderId },
  body: JSON.stringify(payload),
  signal: AbortSignal.timeout(8000),
}), { retries: 3, shouldRetry: isTransient });
```

---

## 10. Validation & Handling Outside Data

- **Validate at every boundary**: request bodies/params/queries, forms, API responses, webhooks, queue messages, files, env vars, localStorage, URL params.
- Use **schemas** as the single source of truth: **Zod** (TS/JS), **Pydantic** (Python/FastAPI) — derive types from them.
- **Whitelist** accepted fields (`extra="forbid"`, `whitelist: true`, Zod `.strict()`); never `Object.assign(user, req.body)` (**mass assignment**).
- Validate on the **server** even if the client validates (client validation is UX, server validation is security).
- Normalize input (trim strings, lowercase emails) at the boundary.
- Limit sizes: body size, file size, string length, array length, page size.

```ts
const CreateUser = z.object({
  name: z.string().trim().min(2).max(50),
  email: z.string().email().toLowerCase(),
}).strict();
const data = CreateUser.parse(req.body);     // typed + safe from here on
```

---

## 11. Money, Dates, IDs & Text

- **Money**: integers in the smallest unit (paise/cents) or `Decimal`; never floats. Store the currency. Round once, deliberately. Format with `Intl.NumberFormat` / locale-aware formatting only for display.
- **Dates**: store and transmit **UTC ISO 8601** timestamps; convert to the user's time zone only for display; use timezone-aware datetimes (Python `datetime.now(UTC)`); date-only values as `YYYY-MM-DD`; use date libraries (date-fns, Luxon, `zoneinfo`) for math.
- **IDs**: generate with `crypto.randomUUID()` / `uuid4()` (or UUIDv7/ULID for sortable IDs); keep large numeric IDs as strings in JSON (JS numbers lose precision above 2^53).
- **Text**: UTF-8 everywhere; `localeCompare`/`Intl.Collator` for human sorting; `Intl` for plurals/numbers/dates; never concatenate translated sentences.

```js
const totalPaise = items.reduce((s, i) => s + i.pricePaise * i.qty, 0);
new Intl.NumberFormat("en-IN", { style: "currency", currency: "INR" }).format(totalPaise / 100);
```

---

## 12. TypeScript Practices

- `strict: true` (+ `noUncheckedIndexedAccess`, `noImplicitOverride`, `verbatimModuleSyntax`); run **`tsc --noEmit` in CI** (bundlers don't type-check).
- **No `any`** — use `unknown` + narrowing, generics, or proper types; lint-enforce `no-explicit-any`.
- **Don't `as`-cast external data** — validate it (Zod) and infer the type.
- Annotate **function parameters and exported return types**; let inference handle locals.
- Model state with **discriminated unions** + exhaustive `switch` (`assertNever`).
- Prefer **union types / `as const` objects** over enums; use `import type`.
- `readonly` inputs; avoid non-null assertions (`!`) — narrow instead.
- Use `satisfies` for config objects; `@ts-expect-error` (with a reason) instead of `@ts-ignore`.
- Generate types from sources of truth (Prisma, OpenAPI, Zod) instead of hand-writing duplicates.
- Lint async bugs: `no-floating-promises`, `no-misused-promises`, `switch-exhaustiveness-check`.

```ts
type RequestState<T> =
  | { status: "idle" | "loading" }
  | { status: "success"; data: T }
  | { status: "error"; error: string };
```

---

## 13. React Practices

**Components**
- Small, focused, **pure** components; one component per file; `PascalCase` names.
- Never define components inside other components.
- Keep **state as local as possible**; lift only when shared; derive values instead of syncing state.
- Avoid **redundant/contradictory state** (one `status` instead of `isLoading` + `isError` + `isSuccess`).
- **Immutable state updates**; functional updates when the next state depends on the previous.
- Stable, unique **keys** (never `Math.random()`, index only for static lists).
- Composition (`children`, slots) over prop drilling; Context for low-frequency global values.

**Effects & data**
- **You might not need an effect**: derive during render, handle events in handlers, reset with `key`.
- Every effect with a subscription/timer/listener/request has a **cleanup**.
- Correct **dependency arrays** (eslint `react-hooks/exhaustive-deps`).
- **Server state** in TanStack Query (or framework loaders), not hand-rolled `useEffect` fetching.
- Put filters/pagination/tabs in the **URL**.

**UX & robustness**
- Handle **loading, error, empty and success** states for every async UI.
- **Error boundaries** per route/widget + error reporting.
- Disable buttons while submitting; prevent double submits.
- Forms: schema validation (React Hook Form + Zod), show server errors on fields, never lose user input on failure.

**Performance**
- Measure with the Profiler before optimizing; memoize (`memo`/`useMemo`/`useCallback`) where it matters (or use React Compiler).
- Code-split routes (`lazy`); virtualize long lists; optimize images; debounce search inputs.

**Security & a11y**
- Never `dangerouslySetInnerHTML` with unsanitized input; validate URLs in `href`.
- Semantic HTML, labels, keyboard support, focus management (see Accessibility).

```jsx
// ❌ derived state synced by an effect
const [fullName, setFullName] = useState("");
useEffect(() => setFullName(`${first} ${last}`), [first, last]);

// ✅ derive during render
const fullName = `${first} ${last}`;
```

---

## 14. Node.js & Express Practices

- **Never block the event loop**: no `*Sync` APIs in request handlers; offload CPU work to worker threads or queues.
- **Layered structure**: routes → controllers → services → repositories; export the `app` separately from `listen()` for tests.
- **Central error handler** + custom error classes; handle async errors (Express 5 does automatically; wrap in Express 4).
- **Validate** every request (Zod/Joi) at the route boundary.
- **Security middleware**: `helmet`, explicit CORS origins, body size limits, rate limiting (`express-rate-limit` with a Redis store), `app.disable("x-powered-by")`.
- **Config** from validated env vars; fail fast at startup.
- **Structured logging** (pino) with request IDs; no `console.log` in production code.
- **Timeouts** on outbound calls & DB queries; set `keepAliveTimeout` above the load balancer idle timeout.
- **Reuse** HTTP clients and DB pools; streams for large files.
- **Graceful shutdown** on SIGTERM (stop accepting, finish in-flight requests, close pools).
- Handle `unhandledRejection` / `uncaughtException`: log and exit, let the process manager restart.
- Use an **LTS** Node version; pin it (`.nvmrc`, `engines`, Docker image tag).
- Keep servers **stateless** (sessions in Redis, files in object storage) so you can scale horizontally.

```js
app.disable("x-powered-by");
app.use(helmet());
app.use(cors({ origin: ALLOWED_ORIGINS, credentials: true }));
app.use(express.json({ limit: "100kb" }));
app.use("/api", apiLimiter, routes);
app.use(notFoundHandler);
app.use(errorHandler);        // last
```

---

## 15. Python Practices

- Follow **PEP 8**; enforce with **ruff** (lint + format); type-check with **mypy/pyright**.
- **Type hints** on all functions; `X | None` instead of implicit `None`.
- **Virtual environments** + a lockfile (uv/poetry); `pyproject.toml` for config.
- **Pythonic idioms**: comprehensions, `enumerate`, `zip`, unpacking, context managers, `pathlib`, f-strings, `any/all`.
- **No mutable default arguments**; don't shadow built-ins (`list`, `id`, `type`).
- **Specific exceptions**; custom exception hierarchy; `raise ... from e`; `logger.exception()` in `except`.
- **`with`** for every resource (files, locks, DB sessions, HTTP clients).
- **dataclasses/Pydantic** for structured data instead of loose dicts.
- **Timezone-aware** datetimes (`datetime.now(UTC)`); `Decimal` for money.
- **`logging`** (structured in production), not `print`.
- Concurrency: **asyncio** for many I/O tasks, **threads** for blocking I/O libraries, **processes** for CPU-bound work; never block the event loop in async code.
- **Security**: parameterized SQL, no `eval`/`exec`/`pickle` on untrusted data, `yaml.safe_load`, `secrets` (not `random`) for tokens, `subprocess.run([...])` without `shell=True`.
- `requests` has **no default timeout** — always pass one (or use `httpx` with timeouts).
- Guard scripts with `if __name__ == "__main__":`.

```python
# ✅
with open(path, encoding="utf-8") as f:
    rows = [parse(line) for line in f if line.strip()]

response = httpx.get(url, timeout=httpx.Timeout(10.0, connect=3.0))
cursor.execute("SELECT * FROM users WHERE email = %s", (email,))
```

---

## 16. FastAPI Practices

- **Separate schemas**: `UserCreate`, `UserUpdate`, `UserOut` — always set `response_model` (never return ORM objects raw).
- `model_config = ConfigDict(extra="forbid")` on input models; `exclude_unset=True` for PATCH.
- **`Annotated` dependency aliases** (`DbSession`, `CurrentUser`, `Pagination`) to keep routes clean.
- **`async def` only with async libraries**; use plain `def` for blocking libraries (runs in a threadpool); never `time.sleep`/`requests` in `async def`.
- **Lifespan** for shared resources (HTTP clients, DB engines, Redis, ML models) — never create them per request.
- **Custom exception classes + handlers** for a consistent error format; don't raise `HTTPException` deep inside services.
- **Layers**: routers → services → repositories; business logic free of FastAPI imports.
- **Settings** with `pydantic-settings` (validated, `SecretStr`), injected via a dependency.
- **Alembic** migrations; never `create_all()` in production.
- **Auth**: OAuth2 + short-lived JWTs (explicit `algorithms=[...]`), Argon2/bcrypt, ownership checks in queries.
- **Background work**: `BackgroundTasks` only for tiny tasks; Celery/ARQ for real jobs.
- **Tests** with `TestClient`/`httpx` + `app.dependency_overrides`; real Postgres in CI.
- Disable/protect `/docs` in production for private APIs.

```python
@router.patch("/{note_id}", response_model=NoteOut)
async def update_note(note_id: int, data: NoteUpdate, user: CurrentUser, service: NoteServiceDep):
    return await service.update(user.id, note_id, data)     # ownership enforced in the service query
```

---

## 17. API Design

- **Resource-oriented REST**: plural nouns (`/orders`, `/orders/{id}/items`), HTTP verbs for actions, no verbs in URLs (`/getOrders` ❌).
- **Correct status codes**: 200/201/204, 400/401/403/404/409/422/429, 500/503.
- **Consistent error format** everywhere: `{ "error": { "code": "VALIDATION_ERROR", "message": "…", "details": [...] } }`.
- **Version** the API (`/v1`); deprecate before removing (mark deprecated, announce, sunset date).
- **Pagination** on every list endpoint (cursor for feeds/large tables), with max page size; filtering & sorting via query params (whitelisted fields).
- **Idempotency**: GET/PUT/DELETE idempotent; `Idempotency-Key` for POSTs that create payments/orders.
- **Document** with OpenAPI (generated from schemas); give examples.
- Consistent naming style in JSON (`camelCase` or `snake_case`, pick one); ISO 8601 UTC dates; money as integer minor units + currency; IDs as strings.
- Use **ETags/Cache-Control** for cacheable GETs; `Location` header on 201.
- **Backwards compatibility**: add fields freely; never rename/remove/change the meaning of fields without a new version.
- Rate limit and return `429` with `Retry-After`.

---

## 18. Database Practices

- **Migrations** for every schema change (reviewed, versioned); never edit production schemas by hand.
- **Zero-downtime changes**: expand → migrate data → contract; add NOT NULL columns in steps; `CREATE INDEX CONCURRENTLY` on big Postgres tables.
- **Indexes** for columns used in `WHERE`, `JOIN`, `ORDER BY`; check with `EXPLAIN ANALYZE`; don't over-index write-heavy tables.
- **Avoid N+1 queries** (eager loading / joins / batching).
- **Select only needed columns**; paginate; keep transactions short.
- **Transactions** for multi-step writes (transfers, orders + items); row locks / optimistic locking for concurrent updates.
- **Constraints in the DB** (unique, foreign keys, NOT NULL, CHECK) — the last line of defence against bad data and race conditions.
- **Parameterized queries** only (ORMs or bound parameters).
- **Connection pooling** with sensible limits; query timeouts.
- **Backups** tested by actually restoring; point-in-time recovery for production.
- Soft deletes / audit tables where history matters.
- Idempotent **seed scripts**; separate test databases.

---

## 19. Security

**Everywhere**
- Validate & sanitize all input; whitelist fields; limit sizes.
- Least privilege for users, services, DB accounts and cloud IAM.
- Secrets in env vars/secret managers — never in code, logs, frontend bundles or git; rotate on leak.
- Keep dependencies updated (`npm audit`, `pip-audit`, Dependabot/Renovate); commit lockfiles.
- HTTPS everywhere; HSTS.

**Frontend**
- Prevent **XSS**: render text (`textContent`, JSX), sanitize HTML (DOMPurify), Content-Security-Policy.
- Validate URLs (`http/https` only) before using in `href`/`src`; safe redirects (same-origin paths).
- Tokens in **HttpOnly, Secure, SameSite** cookies rather than localStorage when possible.
- Check `event.origin` for `postMessage`; load third-party scripts sparingly (SRI for CDN scripts).
- `NEXT_PUBLIC_*`/`VITE_*` env vars are public.

**Backend**
- **AuthN + AuthZ on every endpoint**; enforce ownership in queries (prevent **IDOR**).
- Passwords: Argon2/bcrypt; rate-limit login/OTP; MFA for sensitive accounts.
- JWTs: short-lived, explicit algorithms, refresh rotation, revocation strategy.
- **Injection**: parameterized SQL, no NoSQL operator injection (validate types), no shell interpolation.
- **CSRF** protection for cookie-based auth (SameSite + tokens/Origin checks).
- **SSRF** protection when fetching user-provided URLs.
- Webhooks: verify signatures on the raw body, reject stale timestamps, dedupe events.
- Security headers (`helmet`), CORS allowlist, no stack traces in responses.
- Log security events (logins, permission denials) without sensitive data.

---

## 20. Performance

- **Measure first** (Lighthouse, Web Vitals, DevTools Performance, profilers, APM), then optimize the biggest bottleneck.
- **Algorithms & data structures** beat micro-optimizations (Map/Set lookups, avoid O(n²)).
- **Frontend**: code-split, lazy-load, optimize images (modern formats, sizes, dimensions), preload the LCP resource, defer scripts, animate only `transform`/`opacity`, avoid layout thrashing, virtualize long lists, debounce/throttle frequent events, keep main-thread tasks < 50 ms.
- **Caching** at every layer: HTTP (`Cache-Control`, ETag), CDN, client cache (TanStack Query), server cache (Redis) — with deliberate invalidation.
- **Backend**: async I/O, connection reuse, DB indexes, avoid N+1, pagination, background jobs for slow work, horizontal scaling with stateless servers.
- **Payloads**: compress (Brotli/gzip), send only needed fields, paginate.
- Set **performance budgets** (bundle size, LCP, p95 latency) and enforce them in CI.

---

## 21. Testing

- **Testing trophy/pyramid**: many fast unit tests for pure logic, solid integration tests (components with mocked network, API routes with a real test DB), a few E2E tests for critical flows (login, checkout).
- Test **behaviour, not implementation** (Testing Library queries by role/label).
- Test **edge cases**: empty, zero, negative, max, null, unicode, time zones, concurrency, error paths.
- Add a **regression test** for every bug fix.
- Make code testable: pure functions, dependency injection, inject time/randomness.
- Mock at the **boundaries** (network via MSW/`respx`, external services), not your own internals.
- Tests are **independent and deterministic** (no shared state, fixed clocks, seeded data).
- Keep tests fast; run them in CI on every PR; track coverage as a signal, not a goal.

```js
test("applies 10% discount and rounds to paise", () => {
  expect(priceOrder([{ pricePaise: 999, qty: 3 }], { type: "percent", value: 10 }, 0).total).toBe(2697);
});
```

---

## 22. Logging, Monitoring & Observability

- **Structured logs** (JSON) with level, timestamp, message, **request/correlation ID**, user ID, route, duration.
- Log levels used correctly: `debug` (dev), `info` (business events), `warn` (recoverable issues), `error` (failures needing attention).
- **Never log** passwords, tokens, secrets, full card numbers or unnecessary PII (use redaction).
- **Error tracking** (Sentry) with releases and source maps.
- **Metrics**: request rate, error rate, latency (p50/p95/p99), saturation (CPU, memory, event loop lag, DB pool usage), business KPIs.
- **Tracing** across services (OpenTelemetry).
- **Health checks**: liveness (`/health`) and readiness (`/ready` — dependencies reachable).
- **Alerts** on symptoms users feel (error rate, latency), with runbooks; avoid noisy alerts.

---

## 23. Configuration & Secrets

- **12-factor**: config in environment variables, not code.
- **Validate config at startup** (Zod / pydantic-settings) and fail fast with a clear message.
- Commit `.env.example`, never `.env`.
- Parse types explicitly (`"false"` is truthy as a string).
- Separate config per environment (dev/staging/prod); same build artifact promoted across environments.
- Secrets from a **secret manager** in production; rotate regularly; different secrets per environment.
- **Feature flags** for risky changes (gradual rollout, instant kill switch); remove stale flags.

---

## 24. Accessibility

- **Semantic HTML** first: `<button>` for actions, `<a>` for navigation, headings in order, landmarks (`<nav>`, `<main>`).
- Every input has a **label**; errors are linked (`aria-describedby`) and announced (`role="alert"`).
- **Keyboard**: everything reachable and usable with Tab/Enter/Space/Escape; visible focus styles; logical focus order; focus management in modals (trap + restore).
- **Images**: meaningful `alt`; `alt=""` for decorative images.
- **Color contrast** (WCAG AA); never rely on color alone.
- Respect **`prefers-reduced-motion`**.
- ARIA only when native HTML can't express it (`aria-expanded`, `aria-live`, `role="dialog"`).
- Use accessible headless libraries (Radix, React Aria) for complex widgets; test with axe + keyboard + a screen reader.

---

## 25. Dependencies

- Before adding a package: can native JS/Python do it? Is it maintained? Size (bundlephobia)? License? Security history?
- **Commit lockfiles**; install with `npm ci` / `uv sync --frozen` in CI.
- Update regularly in small steps (Renovate/Dependabot); read changelogs for major versions.
- Remove unused dependencies (`knip`, `depcheck`, `deptry`).
- Pin runtime versions (Node LTS, Python version) in config and Docker images.
- Prefer ESM, tree-shakeable packages on the frontend.

---

## 26. Git, Pull Requests & Code Review

- **Small, focused commits and PRs** (easy to review and revert).
- **Conventional commits**: `feat:`, `fix:`, `refactor:`, `docs:`, `test:`, `chore:`, `perf:`.
- Descriptive branch names: `feat/checkout-coupons`, `fix/login-redirect`.
- PR description: **what, why, how to test**, screenshots for UI, risks/rollback plan.
- Never commit secrets, `.env`, build output or `node_modules`/`.venv`; use `.gitignore` and secret scanning.
- Rebase/merge regularly to avoid giant conflicts; keep `main` always deployable.
- Commands for all of this (rebasing, fixups, undo, reflog recovery, bisect, hooks): Section 27.

**Code review checklist**
- Correctness & edge cases; error handling; security (authZ, validation, injection, secrets); performance (N+1, loops, re-renders); readability & naming; tests added/updated; backwards compatibility (API, DB migrations); observability (logs/metrics); no leftover debug code.
- Review the code, not the person; explain *why*; distinguish blocking issues from nits.

---

## 27. Git in Practice: Everyday Workflow, Fixing History & Recovery

The previous section covers conventions. This one covers the commands behind them: keeping a branch up to date, cleaning up commits before review, undoing mistakes, and getting back work you thought was lost. The commands and behaviours below were checked against scratch repositories with Git 2.54 (external tools such as `git filter-repo` and `pre-commit` weren't run).

### The mental model

- A **commit** is a snapshot of the whole project plus a pointer to its parent commit(s). Commits never change; "editing history" creates **new** commits with new IDs.
- A **branch** is a movable label that points at a commit. `HEAD` is the branch (or commit) you're on. A **tag** is a label that doesn't move.
- Changes go through three places: the **working tree** (your files), the **staging area** or index (what the next commit will contain), and the **repository** (commits).
- **The golden rule:** never rewrite commits that other people already have (anything pushed to a shared branch). Rewriting your own unpushed or personal feature-branch commits is fine.

### One-time setup that prevents common pain

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global pull.rebase true            # replay local commits on pull instead of making merge bubbles
git config --global rebase.autoStash true       # stash/unstash uncommitted work around a rebase
git config --global rebase.autoSquash true      # fixup! commits are folded in automatically
git config --global rebase.updateRefs true      # rebasing stacked branches moves the branches above too
git config --global push.autoSetupRemote true   # the first `git push` sets the upstream
git config --global fetch.prune true            # drop remote-tracking branches deleted on the server
git config --global rerere.enabled true         # remember how you resolved a conflict and reuse it
git config --global merge.conflictStyle zdiff3  # conflict markers also show the common base version
git config --global diff.algorithm histogram    # more readable diffs
```

### The daily feature-branch loop

```bash
git switch main && git pull                  # start from the latest main
git switch -c feat/coupons                   # new branch (git switch/restore replace the overloaded checkout)

git add -p                                   # stage hunk by hunk: review exactly what goes in
git commit -m "feat(checkout): apply coupon codes at payment"

git fetch origin
git rebase origin/main                       # replay your commits on top of the latest main
git push --force-with-lease --force-if-includes    # a rebase rewrote your commits: force-push SAFELY
```

**Why `--force-with-lease --force-if-includes` and never `--force`.** `--force` overwrites whatever is on the server, including a teammate's commits pushed a minute ago. `--force-with-lease` refuses if the remote branch moved since you last *fetched*. But if anything fetched in the background (many editors auto-fetch), the lease is updated and the teammate's work is overwritten anyway. `--force-if-includes` (Git 2.30+) closes that hole by also checking that you've actually integrated the remote commits. Make it the default with an alias: `git config --global alias.pushf "push --force-with-lease --force-if-includes"`.

### Merge vs rebase vs squash

```
          A---B---C  feature                 merge:   A---B---C
         /                                            /         \
    D---E---F---G  main                     D---E---F---G-------M   (M = merge commit)

    rebase feature onto main:               D---E---F---G---A'---B'---C'   (new commits, linear history)
    squash merge (GitHub "Squash and merge"):   D---E---F---G---S          (S = A+B+C as one commit)
```

| | Merge | Rebase | Squash merge |
|---|---|---|---|
| History | True history with merge commits | Linear, rewritten (new SHAs) | One commit per PR on `main` |
| Safe on shared branches | Yes | **No**: only on your own branch | Done by the platform at merge time |
| Typical use | Merging long-lived branches, release branches | Updating your feature branch with `main` | Merging PRs into `main` |
| Downside | Noisy graph | Conflicts may repeat per commit (use `rerere`) | Loses individual commits (keep PRs small) |

A **fast-forward** happens when `main` hasn't moved since you branched: Git just moves the label forward and creates no merge commit.

### Undo cheat sheet

| I want to… | Command |
|---|---|
| Throw away unstaged edits to a file | `git restore app.js` |
| Unstage a file (keep the edits) | `git restore --staged app.js` |
| Fix the last commit's message or add a forgotten file | `git add forgotten.js && git commit --amend --no-edit` |
| Undo the last commit, keep its changes **staged** | `git reset --soft HEAD~1` |
| Undo the last commit, keep its changes **unstaged** | `git reset HEAD~1` (`--mixed` is the default) |
| Undo the last commit **and delete its changes** ⚠ | `git reset --hard HEAD~1` |
| Undo a commit that's already pushed/shared | `git revert <sha>` (adds a new commit that undoes it) |
| Undo a pushed merge | `git revert -m 1 <merge-sha>` (`-m 1` = keep the main-line parent) |
| Stop tracking a file but keep it on disk | `git rm --cached .env`, then add it to `.gitignore` |
| Get back commits "lost" by reset/rebase/amend | `git reflog`, then `git branch rescue <sha>` or `git reset --hard HEAD@{n}` |
| Recover a deleted branch | `git reflog` (or the SHA printed by `git branch -D`), then `git branch <name> <sha>` |

```bash
# reset modes, starting from a commit that changed app.js
git reset --soft HEAD~1 && git status --short    # M  app.js   (staged)
git reset HEAD~1        && git status --short    #  M app.js   (unstaged)
git reset --hard HEAD~1 && git status --short    # (nothing: the changes are gone from the working tree)
```

**Recovering "lost" work with the reflog.** The reflog records every position `HEAD` has been at, so commits are almost never truly lost. By default entries are kept for 90 days, but only **30 days** for commits no longer on any branch, which is exactly the "lost" case, so rescue work promptly:

```bash
git reset --hard HEAD~3          # oops: three commits "gone"
git reflog -5
# 1a2b3c4 HEAD@{0}: reset: moving to HEAD~3
# 9f8e7d6 HEAD@{1}: commit: feat: add invoice PDF       ← the tip before the reset
# …
git reset --hard HEAD@{1}        # back to where you were (or: git branch rescue 9f8e7d6)
```

Uncommitted changes are **not** in the reflog. `git reset --hard` and `git restore` on uncommitted edits can't be undone by Git, so commit or stash early. (A staged-but-never-committed file can sometimes be found with `git fsck --lost-found`.)

**Committed a secret?** Treat it as leaked the moment it's pushed: **rotate the key first**. Then remove it from history with `git filter-repo --invert-paths --path .env` (a separate tool; use it instead of the old `filter-branch`), force-push, and ask everyone to re-clone. Enable secret scanning / push protection (GitHub, `gitleaks` in pre-commit) so it doesn't happen again.

### Clean up commits before review: fixup + autosquash

Reviewers prefer a few meaningful commits to "wip", "fix typo" and "address review". Record fixes as **fixup commits** aimed at the commit they belong to, then fold them in:

```bash
git log --oneline
# c3 feat: coupon UI
# b2 feat: coupon API
git commit --fixup=b2                  # creates "fixup! feat: coupon API"
git rebase --autosquash main           # Git 2.44+: no editor needed; the fixup is folded into b2
```

**Interactive rebase** (`git rebase -i main`) opens a todo list where you can reorder lines and change each commit's action:

| Action | Effect |
|---|---|
| `pick` | Keep the commit |
| `reword` | Keep it, edit the message |
| `edit` | Stop so you can amend it (e.g. split it into two commits) |
| `squash` | Merge into the previous commit, combining the messages |
| `fixup` | Merge into the previous commit, discarding this message |
| `drop` | Remove the commit |

If a rebase goes wrong, `git rebase --abort` returns you to exactly where you started, and even after it finishes, the reflog still has the old commits.

### Resolving conflicts

```bash
git rebase origin/main            # or git merge origin/main
# CONFLICT (content): Merge conflict in src/price.js
git status                        # lists "both modified" files
# edit the files: keep the right code and delete the <<<<<<< ||||||| ======= >>>>>>> markers
git add src/price.js
git rebase --continue             # or: git merge --continue.  Bail out with --abort
```

With `merge.conflictStyle zdiff3`, each conflict shows three versions: yours, the **common ancestor** (between `|||||||` and `=======`), and theirs. Seeing the ancestor makes it clear what each side actually changed.

**"Ours" and "theirs" swap during a rebase.** In a merge, *ours* is your current branch and *theirs* is the branch being merged in. A rebase replays your commits **onto** the other branch, so *ours* is the branch you're rebasing onto (e.g. `main`) and *theirs* is **your** commit being replayed:

```bash
# during `git rebase main` on your feature branch:
git checkout --theirs src/price.js     # keeps YOUR feature-branch version
git checkout --ours src/price.js       # keeps MAIN's version
```

**Lockfile conflicts** (`package-lock.json`, `poetry.lock`, `uv.lock`): don't hand-merge them. Take the version from the branch you're updating from, then regenerate: `git checkout --ours package-lock.json && npm install` during a rebase onto main (that's main's version; `npm install` re-adds your dependencies), then `git add package-lock.json`.

### Stash and worktrees: switching context

```bash
git stash push -u -m "wip: coupon form"    # -u includes untracked files
git stash list                              # stash@{0}: On feat/coupons: wip: coupon form
git stash pop                               # re-apply and drop it (if the pop conflicts, the stash is KEPT)
git stash apply stash@{1}                   # re-apply without dropping
git stash branch fix/from-stash stash@{0}   # turn a stash into a branch
```

For an urgent hotfix while you're mid-feature, a **worktree** is often better than stashing. It's a second working directory on another branch that shares the same repository:

```bash
git worktree add ../shop-hotfix -b hotfix/price-rounding main
cd ../shop-hotfix        # fix, commit, push; your feature folder is untouched
git worktree remove ../shop-hotfix
```

### Cherry-pick: copy a commit to another branch

```bash
git switch release/1.4
git cherry-pick -x 9f8e7d6     # -x appends "(cherry picked from commit 9f8e7d6…)" to the message
git cherry-pick A^..B          # a range, A through B inclusive
```

Typical use: backporting a fix from `main` to a release branch. Prefer fixing on `main` first and cherry-picking **down**, so the fix can't be forgotten on `main`.

### Finding things in history

```bash
git log --oneline --graph --all                 # the whole picture
git log -S "applyCoupon" --oneline              # "pickaxe": commits that ADDED or REMOVED this text
git log -G "apply(Coupon|Discount)" --oneline   # commits whose changed lines match a regex (POSIX extended:
                                                #   \w and \d are NOT portable, e.g. on macOS; use [[:alnum:]_] and [0-9])
git log -p --follow -- src/price.js             # history of one file, across renames
git show 9f8e7d6:src/price.js                   # the file as it was at a commit
git blame -w -C -L 40,60 src/price.js           # who last touched lines 40–60 (-w ignore whitespace, -C detect moved code)

git log main..feature        # TWO dots: commits on feature that aren't on main (what the PR adds)
git diff main...feature      # THREE dots: changes on feature since it branched off (what the PR diff shows)
```

**Ignore formatting commits in `blame`.** After a mass reformat (Prettier, Black), `blame` would point every line at the formatting commit. List such commits in a file and tell Git to skip them (GitHub's blame view reads the same file automatically):

```bash
git rev-parse HEAD                               # the formatting commit: blame needs the FULL 40-character SHA
echo "4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f  # style: run prettier" >> .git-blame-ignore-revs
git config blame.ignoreRevsFile .git-blame-ignore-revs
```

### `git bisect`: find the commit that broke something

Bisect binary-searches history: 1,000 commits take about 10 steps. Let a script decide good or bad with `git bisect run`:

```bash
git bisect start
git bisect bad                    # the current commit is broken
git bisect good v1.3.0            # this release worked
git bisect run npm test -- price.test.js
# … "a1b2c3d is the first bad commit"
git bisect reset                  # go back to where you started
```

The script's exit code decides: **0** = good, **1–124** (and 126–127) = bad, **125** = "can't test this commit, skip it" (e.g. it doesn't build). If skipped commits sit right before the culprit, bisect can't tell them apart and reports *"The first bad commit could be any of: …"* with a short list, which is still far fewer than 1,000. Write a small script that checks only the one behaviour you care about; a whole test suite with unrelated flaky tests sends bisect the wrong way.

### Hooks: automate checks locally

Git runs scripts from `.git/hooks` at certain moments (`pre-commit`, `commit-msg`, `pre-push`). That folder isn't committed, so teams share hooks through a tool:

- **JavaScript:** husky + lint-staged (format and lint only the staged files, so it's fast).
- **Python:** the `pre-commit` framework (ruff, black, gitleaks …).
- **Anything:** a committed folder plus `git config core.hooksPath .githooks`.

```bash
npm install --save-dev husky lint-staged
npx husky init                                  # creates .husky/pre-commit and a "prepare" script
echo "npx lint-staged" > .husky/pre-commit
```

```json
{
  "lint-staged": {
    "*.{js,jsx,ts,tsx}": ["eslint --fix", "prettier --write"],
    "*.{json,md,css}": "prettier --write"
  }
}
```

```yaml
# .pre-commit-config.yaml (Python projects: pip install pre-commit && pre-commit install)
repos:
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.6.9
    hooks:
      - id: ruff
        args: [--fix]
      - id: ruff-format
  - repo: https://github.com/gitleaks/gitleaks
    rev: v8.21.2
    hooks:
      - id: gitleaks
```

A plain `commit-msg` hook that enforces Conventional Commits:

```bash
#!/bin/sh
# .githooks/commit-msg   (chmod +x, then: git config core.hooksPath .githooks)
pattern='^(feat|fix|docs|style|refactor|perf|test|build|ci|chore|revert)(\([a-z0-9-]+\))?!?: .{1,72}$'
if ! head -n 1 "$1" | grep -Eq "$pattern"; then
  echo "✖ Commit message must look like: feat(scope): short summary" >&2
  exit 1
fi
```

Hooks can be skipped with `--no-verify`, so **CI must run the same checks**. Keep hooks fast: formatting and linting in `pre-commit`, the unit tests in `pre-push` at most.

### Repository hygiene files

```gitattributes
# .gitattributes: normalise line endings (no more whole-file diffs from CRLF vs LF)
* text=auto eol=lf
*.cmd text eol=crlf
*.bat text eol=crlf
*.png binary
*.jpg binary
```

- Git patterns (`.gitignore`, `.gitattributes`) have **no brace expansion**: `*.{cmd,bat}` silently matches nothing. Write one line per extension. Check a rule with `git check-attr eol -- run.cmd` or `git check-ignore -v path`.
- Put OS and editor junk (`.DS_Store`, `.idea/`) in a **global** ignore file (`git config --global core.excludesFile ~/.gitignore_global`) rather than every project's `.gitignore`.
- Already committed `node_modules/` or `.env`? `git rm -r --cached node_modules`, add it to `.gitignore`, commit.
- Large binaries (videos, datasets, design files) belong in **Git LFS** or object storage, not in history. A big repo can be cloned faster with `git clone --filter=blob:none` (a partial clone that downloads file contents on demand).

### Branching strategies

| Strategy | Shape | Good for |
|---|---|---|
| **Trunk-based** | Short-lived branches (hours to a couple of days), merged to `main` behind **feature flags**; `main` is always deployable | Web apps with CI/CD. The DORA research ties it to high-performing teams |
| **GitHub flow** | Branch → PR → review → merge → deploy | Most teams, most of the time (trunk-based with PRs) |
| **Git flow** | `develop`, `release/*`, `hotfix/*` branches | Versioned releases with long support windows (mobile apps, libraries, on-premise software) |

Whatever the strategy: **protect `main`** (require a PR, at least one review and passing checks; block force-pushes), tag releases (`git tag -a v1.4.0 -m "Release 1.4.0" && git push origin v1.4.0`), and follow semantic versioning for anything others depend on.

### Commit messages that help future you

```
fix(checkout): round coupon discounts to whole paise

Discounts were computed with floats, so 10% of ₹199.90 came out as
19.990000000000002. Compute in integer paise and round once at the end.

Closes #482
```

- **Subject:** an imperative summary under 72 characters ("fix", not "fixed"), with a type and scope.
- **Body:** *why* the change was made and what the reader wouldn't guess from the diff.
- **Footer:** issue links and `BREAKING CHANGE: …`.

### Interview Qs

1. `git fetch` vs `git pull`? → `fetch` downloads commits and updates `origin/*` without touching your branch; `pull` = `fetch` + merge (or rebase with `pull.rebase`).
2. Merge vs rebase? → Merge preserves history with a merge commit. Rebase rewrites your commits onto a new base for a linear history. Never rebase shared commits.
3. `reset --soft` vs `--mixed` vs `--hard`? → They move the branch and keep the changes staged, keep them unstaged, or discard them.
4. `reset` vs `revert`? → `reset` moves the branch pointer (rewrites history, local work). `revert` adds a new commit that undoes one (safe for shared branches).
5. How do you recover a commit after `reset --hard` or a deleted branch? → `git reflog` to find the SHA, then `git branch <name> <sha>`.
6. What is a detached HEAD? → `HEAD` points at a commit rather than a branch. New commits there aren't on any branch; create one with `git switch -c <name>` before leaving.
7. `--force` vs `--force-with-lease` (and `--force-if-includes`)? → The lease refuses to overwrite remote commits you haven't seen; `--force-if-includes` also protects against background fetches.
8. What does `git cherry-pick` do? When would you use it? → It copies a commit onto the current branch, e.g. backporting a hotfix to a release branch.
9. How does `git bisect` work? → A binary search between a good and a bad commit; `git bisect run <script>` automates it using exit codes.
10. `main..feature` vs `main...feature`? → Two dots in `log`: commits on feature that aren't on main. Three dots in `diff`: changes since the merge base.
11. What do "ours" and "theirs" mean during a rebase? → They're swapped: *ours* is the branch you're rebasing onto, *theirs* is your commit.
12. How do you remove a secret that was committed? → Rotate it first, then `git filter-repo`, force-push, have everyone re-clone, and add secret scanning.
13. Squash merge vs merge commit? → One tidy commit per PR vs preserving every commit plus a merge commit.
14. What is a fast-forward merge? → The target branch hasn't diverged, so Git just moves its pointer forward.
15. Why can't hooks replace CI? → They're local and skippable (`--no-verify`), and not everyone has them installed.

---

## 28. CI/CD & Deployment

- **CI on every PR**: install (frozen lockfile) → lint → format check → type-check → tests → build → (bundle size / security scans).
- **Automate formatting and linting** (Prettier/ESLint, ruff) with pre-commit hooks (husky + lint-staged / pre-commit).
- **Build once, deploy the same artifact** to staging and production.
- **Migrations** run as a separate pipeline step before rolling out new app versions, and are backwards compatible.
- **Zero-downtime deploys**: rolling/blue-green/canary; health checks; graceful shutdown.
- **Docker**: small base images, multi-stage builds, non-root user, pinned versions, `.dockerignore`.
- **Rollback plan** for every release (previous image, feature flag off, roll-forward fix). Flags, progressive rollouts and deployment strategies: Section 29.
- **Environment parity**: dev/staging/prod as similar as possible (same DB engine, same versions).
- Monitor after each deploy (errors, latency, key business metrics).

---

## 29. Feature Flags & Safe Rollouts

A feature flag is an `if` whose condition you can change **without deploying**. It separates two things that are usually bundled together: **deploying** (putting code on servers) and **releasing** (letting users use it). You can merge unfinished work to `main` behind a flag, turn a feature on for staff, then for 1% of users, watch the metrics, and switch it off in seconds if something breaks.

### 1. Four kinds of flags

| Kind | Example | Lifetime | Owner |
|---|---|---|---|
| **Release flag** | `new-checkout`: finished code, gradually released | Days to weeks, then **deleted** | The team building it |
| **Experiment flag** | `checkout-button-copy`: A/B test variants | Until the experiment concludes | Product / data |
| **Ops flag / kill switch** | `recommendations`: turn off an expensive feature under load | Permanent | On-call / platform |
| **Permission flag** | `beta-reports` for customers on the Pro plan | Long-lived | Product |

A permission flag decides what a user **sees**. It is **not** access control: the server must still check permissions on every request. Hiding a button doesn't protect the API behind it.

### 2. Deterministic bucketing: the core algorithm

Percentage rollouts must be **sticky**: a user who sees the new checkout on one request must see it on every request, on every server, after every restart. Never use `Math.random()`. Hash a stable key into a bucket from 0 to 9,999 (0.01% granularity) and compare it with the rollout percentage:

```js
// flags/bucket.js: FNV-1a 32-bit over UTF-8 bytes, portable to any language
const encoder = new TextEncoder();

export function fnv1a32(text) {
  let hash = 0x811c9dc5;
  for (const byte of encoder.encode(text)) {
    hash ^= byte;
    hash = Math.imul(hash, 0x01000193) >>> 0;
  }
  return hash >>> 0;
}

// Salt with the flag key, so each flag picks a DIFFERENT, independent set of users
export function bucket(flagKey, unitId) {
  return fnv1a32(`${flagKey}:${unitId}`) % 10_000;          // 0 … 9999
}

export function inRollout(flagKey, unitId, percent) {
  return bucket(flagKey, unitId) < Math.round(percent * 100);  // 25 → buckets 0–2499
}
```

The properties this guarantees (all tested with 100,000 ids):

- **Sticky:** the same flag and user always give the same answer.
- **Monotonic:** raising a rollout from 10% to 25% only **adds** users; nobody who had the feature loses it.
- **Accurate:** 25% of users really land in the rollout, within a fraction of a percent.
- **Independent flags:** because the flag key is part of the hash, two 10% flags overlap on about 1% of users (10% × 10%), not the same 10%. **Without the salt, every flag hits the same users**, so the same unlucky users get every risky change, and experiments contaminate each other.
- **Portable:** the Python version below gives identical buckets, so a Node API and a Python worker agree on who's in.

```python
# flags/bucket.py: identical results to the JavaScript version
import math

def fnv1a32(text: str) -> int:
    h = 0x811C9DC5
    for byte in text.encode("utf-8"):
        h ^= byte
        h = (h * 0x01000193) & 0xFFFFFFFF
    return h

def bucket(flag_key: str, unit_id: str) -> int:
    return fnv1a32(f"{flag_key}:{unit_id}") % 10_000

def in_rollout(flag_key: str, unit_id: str, percent: float) -> bool:
    # floor(x + 0.5) = JavaScript's Math.round; Python's round() uses banker's rounding (round(1234.5) == 1234)
    return bucket(flag_key, unit_id) < math.floor(percent * 100 + 0.5)
```

**Choose the unit per flag:**

- **User id** for most features.
- **Organisation or tenant id** when everyone in a company must see the same thing (a new invoicing flow).
- **A stable anonymous id** (a first-party cookie) for logged-out traffic.

Bucketing a B2B feature by user makes colleagues see different screens, which is a support nightmare.

### 3. Evaluating a flag: rules in a fixed order

```js
// flags/evaluate.js
import { inRollout } from "./bucket.js";

// config example:
// {
//   "new-checkout": { enabled: true, rollout: 25, unit: "userId",
//                     allow: ["u_staff_1"], deny: ["u_vip_9"], segment: { country: ["IN"] } },
//   "recommendations": { enabled: true, rollout: 100 },    // kill switch: set enabled:false to shed load
// }
export function evaluate(config, flagKey, context, { fallback = false } = {}) {
  const flag = config?.[flagKey];
  if (!flag) return { on: fallback, reason: "unknown-flag" };           // safe default if config is missing
  if (!flag.enabled) return { on: false, reason: "disabled" };          // the kill switch wins over everything
  const unitId = context[flag.unit ?? "userId"];
  if (unitId != null && flag.deny?.includes(unitId)) return { on: false, reason: "deny-list" };
  if (unitId != null && flag.allow?.includes(unitId)) return { on: true, reason: "allow-list" };
  for (const [attribute, allowed] of Object.entries(flag.segment ?? {})) {
    if (!allowed.includes(context[attribute])) return { on: false, reason: "segment-miss" };
  }
  if (unitId == null) return { on: false, reason: "no-unit-id" };         // can't bucket → stay on the safe side
  return inRollout(flagKey, String(unitId), flag.rollout ?? 0)
    ? { on: true, reason: "rollout" }
    : { on: false, reason: "rollout-miss" };
}
```

- **The `reason` is gold for debugging** ("why does this customer see the old checkout?"). Log it with experiment exposures, and show it in an internal admin tool.
- **Fail safe:** when the flag config can't be loaded, evaluate against the **last known good** config, or fall back to the safe default. For a new feature that's *off*; name kill switches so that *on* means "feature working normally".
- **Evaluate locally:** load the config at startup, refresh it every ~30 s (or via a push stream), and evaluate in memory. Never make a network call per flag check.
- **Evaluate on the server, send results to the client:** the browser gets `{ newCheckout: true }` for **this** user, not the rules. Rules reveal staff ids, customer names and unreleased feature names.
- **Avoid flicker:** render the evaluated flags into the initial HTML or SSR response (or block the first render on them). Otherwise users see the old UI flash, then swap.

Hosted services and SDKs do all of this: LaunchDarkly, Unleash, GrowthBook, Flagsmith, ConfigCat. **OpenFeature** is a vendor-neutral API standard, so your code calls `client.getBooleanValue("new-checkout", false, context)` and the provider behind it can change.

### 4. A progressive rollout playbook

1. **Merge dark:** the code is deployed with the flag off everywhere. Both paths are tested in CI.
2. **Internal:** turn it on for staff through the allow list. Dogfood for a few days.
3. **1% → 5% → 25% → 50% → 100%.** At each step, compare the flagged group with everyone else on **guardrail metrics** (error rate, p95 latency, conversion, support tickets). Stay long enough to cover a full daily traffic cycle.
4. **Automate the brakes:** an alert on the guardrails pages the owner, or a rollout controller turns the flag off automatically when errors rise.
5. **Clean up:** after a week or two at 100% with no issues, delete the flag and the old code path.

**Deployment strategies** protect the deploy itself. Flags protect the release. Use both:

| Strategy | How | Protects against |
|---|---|---|
| **Rolling** | Replace instances a few at a time | Downtime during deploys |
| **Blue-green** | Run the new version beside the old one; switch the load balancer; switch back to roll back | Slow rollbacks: switching back takes seconds |
| **Canary** | Send a small % of *traffic* to the new version, compare metrics, then promote | A bad build reaching everyone |
| **Shadow / dark launch** | Mirror real traffic to the new code path and discard its results | Performance or correctness surprises, with zero user impact |
| **Feature flag** | New code runs everywhere; the flag decides who uses it | A bad *feature*, even when the build itself is fine |

Every strategy assumes the old and new versions can run **at the same time** against the same database. Schema changes must be backward compatible: expand, then migrate, then contract (`nodejs.md` → "Database Migrations & Seeding").

### 5. Kill switches for operations

Give expensive or fragile features an **ops flag** before you need one: recommendations, search suggestions, PDF generation, third-party widgets. During an incident, turning them off sheds load in seconds, without a deploy. This complements automatic load shedding and circuit breakers (`nodejs.md` → "Resilience: Timeouts, Retries, Circuit Breakers & Load Shedding"). Document the kill switches in the runbook, and **test them** in staging: a switch that has never been flipped may not work.

### 6. Experiments (A/B tests) done honestly

- Assign variants with the **same bucketing**, salted with the experiment key: bucket < 5,000 → A, otherwise → B.
- **Log an exposure event** when the user actually **sees** the variant, not when the flag is evaluated on some unrelated page. Otherwise both groups fill up with users the change never touched.
- Decide the **primary metric, guardrails and sample size before starting**. Don't stop the test the first time the dashboard looks good ("peeking" inflates false positives).
- Check for **sample ratio mismatch**. If a 50/50 test shows 52/48, something is broken (bots, caching, redirects), and the results can't be trusted.

### 7. Flag debt: remove flags on purpose

Every flag doubles the code paths it touches. Ten flags means up to 1,024 combinations nobody has tested. Keep a **registry** with an owner and an expiry date for every non-permanent flag, and let CI enforce it:

```js
// flags/registry.js
export const FLAG_REGISTRY = [
  { key: "new-checkout", kind: "release", owner: "payments-team", expires: "2026-11-30" },
  { key: "recommendations", kind: "ops", owner: "platform", expires: null },           // permanent kill switch
  { key: "checkout-button-copy", kind: "experiment", owner: "growth", expires: "2026-10-15" },
];

// CI step: fail the build when a temporary flag is past its expiry date
export function expiredFlags(registry, today = new Date().toISOString().slice(0, 10)) {
  return registry.filter((f) => f.kind !== "ops" && f.kind !== "permission" && f.expires !== null && f.expires < today)
    .map((f) => `${f.key} (owner: ${f.owner}, expired ${f.expires})`);
}
```

```js
// scripts/check-flags.js: run in CI
import { FLAG_REGISTRY, expiredFlags } from "../flags/registry.js";

const expired = expiredFlags(FLAG_REGISTRY);
if (expired.length > 0) {
  console.error(`Remove or extend these feature flags:\n  ${expired.join("\n  ")}`);
  process.exit(1);
}
```

More rules that keep flags manageable:

- **One flag per feature.** Don't nest flags inside flags.
- **Wrap the check in one place** (`isNewCheckoutEnabled(user)`), not scattered string lookups.
- **Unit tests set flags explicitly:** inject the evaluator or config, and test both the on and off paths while both exist.
- When a flag reaches 100%, **delete the old path in the same sprint**.

### Interview Qs

1. What problem do feature flags solve? → They separate deploy from release: merge and deploy dark, release gradually, and turn features off without a redeploy.
2. Name the kinds of flags. How do their lifetimes differ? → Release (short, then deleted), experiment (until concluded), ops/kill switch (permanent), permission (long-lived).
3. How do you implement a sticky percentage rollout? → Hash a stable unit id salted with the flag key into buckets and compare with the percentage. Never use `Math.random()`.
4. Why salt the hash with the flag key? → Without it, every flag selects the same users, so the same users get every risky change and experiments interfere with each other.
5. Why must raising a rollout percentage be monotonic? → So users who already have a feature don't lose it when you go from 10% to 25%.
6. Where should flags be evaluated, and what goes to the browser? → On the server, from locally cached config. The browser gets evaluated values for the current user, never the targeting rules.
7. How do you avoid UI flicker with client-side flags? → Bootstrap evaluated flags into the initial HTML or SSR, or block the first render until flags load.
8. Canary deploy vs feature flag rollout? → A canary tests a new *build* on a slice of traffic; a flag rolls out a *feature* inside an already-deployed build. Use both.
9. What's a kill switch? Why test it? → An ops flag that disables an expensive or fragile feature during incidents. An untested switch may fail exactly when needed.
10. What is flag debt and how do you control it? → Stale flags multiply code paths. Use a registry with owners and expiry dates, CI checks, and delete old paths soon after reaching 100%.
11. Is a permission flag a security control? → No. Hiding UI isn't authorization; the server must check permissions itself.
12. What is sample ratio mismatch in A/B tests? → Observed group sizes deviate from the planned split, which signals broken assignment or logging, so the results are invalid.

---

## 30. Incident Response, On-Call, Postmortems & Living Documentation

Every production system has incidents. What separates good teams is how quickly they **notice**, how calmly they **respond**, and whether they **learn**, so the same failure doesn't happen twice. The technical side (SLOs, burn-rate alerts, tracing a slow request) is in `nodejs.md` → "Observability Hands-On: Logs, Metrics, Traces, SLOs & Alerts". This section covers the human side: roles, communication, postmortems, on-call, runbooks, and the documentation that makes all of it possible.

### 1. Severity levels

Agree on levels **before** you need them, so nobody debates wording at 3 a.m.:

| Level | Meaning | Examples | Response |
|---|---|---|---|
| **SEV1** | Critical: most users can't use a core feature, data loss, security breach | Checkout down for everyone; leaked credentials | Page immediately, all hands, updates every 30 min, postmortem required |
| **SEV2** | Major: a core feature is degraded, or a key customer segment is affected | Payments slow for 20% of users; one region down | Page on-call, updates every 60 min, postmortem required |
| **SEV3** | Minor: limited impact, with a workaround | Report exports failing; one admin page broken | Fix within business hours, optional postmortem |
| **SEV4** | Cosmetic or internal only | Typo on a status page; a flaky internal job | A normal ticket |

**Declare early.** Downgrading a SEV2 to a SEV3 costs nothing; discovering an hour later that "someone was looking into it" was actually a SEV1 costs a lot.

### 2. Roles

| Role | Does | Doesn't |
|---|---|---|
| **Incident commander (IC)** | Coordinates: decides priorities, assigns work, calls for help, decides when it's over | Debug. The IC keeps the big picture while others dig |
| **Ops lead / subject experts** | Investigate and apply mitigations | Talk to customers or management mid-debug |
| **Comms lead** | Posts internal updates and status-page updates on a fixed cadence | Guess at root causes in public |
| **Scribe** | Keeps the timeline: what was seen, decided and done, with timestamps | Filter out "unimportant" steps |

In a small team one person holds several roles, but **say out loud who the IC is**. For bigger incidents, hand over the IC role explicitly ("I'm handing IC to Asha") instead of letting it drift.

### 3. The response loop

1. **Detect:** an alert, a customer report or a failed deploy check.
2. **Declare:** open an incident channel (`#inc-2026-09-24-checkout-errors`), name the IC, set a severity.
3. **Assess:** what's broken, for whom, since when? ("Checkout 5xx at 18% since 14:02 IST, all regions.")
4. **Mitigate first:** stop the bleeding **before** hunting for the root cause.
5. **Communicate:** updates on the promised cadence, even when the update is "no change".
6. **Resolve and watch:** confirm the metrics are back to normal, keep watching, then close.
7. **Learn:** a postmortem within about five working days.

**Mitigations to try first** (fast, reversible, and they buy time for the real fix):

| Symptom | First move |
|---|---|
| Started right after a deploy | **Roll back** (or turn off the feature flag) |
| One dependency failing | Kill switch / circuit breaker; serve stale data |
| Overloaded | Scale out, shed load, turn off expensive features |
| One region or node bad | Fail over; drain the bad instances |
| Bad data being written | Stop the writer (pause the job or queue) **before** fixing the data |

**Update template** (internal channel and status page):

```text
[SEV2] Checkout errors: update 2 (14:31 IST)
Impact: ~18% of checkout attempts fail with an error. Other pages work.
Status: Mitigating. We started rolling back release 1.8.2 at 14:30; the error rate is falling.
Next: confirm recovery and keep monitoring.
Next update: 15:30 IST or sooner if anything changes.
```

Customer-facing updates say what's affected and when you'll update next. They don't speculate about causes and don't blame vendors.

### 4. Measuring response

| Metric | From → to | Improves with |
|---|---|---|
| **Time to detect** | Impact starts → alert fires | Symptom-based alerts on SLOs |
| **Time to acknowledge** | Alert → a human responds | Healthy on-call, clear escalation |
| **Time to mitigate** | Impact starts → users stop being hurt | Rollbacks, feature flags, runbooks |
| **Time to resolve** | Impact starts → fully fixed | Good observability, clean code |

Use the **median** over a quarter; one long incident distorts the average.

```js
// incident-metrics.js: timestamps are ISO strings from your incident tracker
const minutesBetween = (from, to) => (Date.parse(to) - Date.parse(from)) / 60_000;

function median(values) {
  const sorted = [...values].sort((a, b) => a - b);
  const mid = Math.floor(sorted.length / 2);
  return sorted.length % 2 ? sorted[mid] : (sorted[mid - 1] + sorted[mid]) / 2;
}

export function responseMetrics(incidents) {
  const pick = (from, to) => median(incidents.filter((i) => i[from] && i[to]).map((i) => minutesBetween(i[from], i[to])));
  return {
    count: incidents.length,
    medianMinutesToDetect: pick("startedAt", "detectedAt"),
    medianMinutesToAcknowledge: pick("detectedAt", "acknowledgedAt"),
    medianMinutesToMitigate: pick("startedAt", "mitigatedAt"),
    medianMinutesToResolve: pick("startedAt", "resolvedAt"),
  };
}

const incidents = [
  { startedAt: "2026-09-01T14:02:00+05:30", detectedAt: "2026-09-01T14:06:00+05:30", acknowledgedAt: "2026-09-01T14:08:00+05:30", mitigatedAt: "2026-09-01T14:32:00+05:30", resolvedAt: "2026-09-01T16:02:00+05:30" },
  { startedAt: "2026-09-10T03:15:00+05:30", detectedAt: "2026-09-10T03:45:00+05:30", acknowledgedAt: "2026-09-10T03:55:00+05:30", mitigatedAt: "2026-09-10T04:15:00+05:30", resolvedAt: "2026-09-10T09:15:00+05:30" },
  { startedAt: "2026-09-20T10:00:00+05:30", detectedAt: "2026-09-20T10:02:00+05:30", acknowledgedAt: "2026-09-20T10:03:00+05:30", mitigatedAt: "2026-09-20T10:12:00+05:30", resolvedAt: "2026-09-20T11:00:00+05:30" },
];
responseMetrics(incidents);
// → { count: 3, medianMinutesToDetect: 4, medianMinutesToAcknowledge: 2, medianMinutesToMitigate: 30, medianMinutesToResolve: 120 }
```

The 3:15 a.m. IST incident (detected after 30 minutes, acknowledged after 10) is the one to study. Was the alert too slow, or was paging broken?

### 5. Blameless postmortems

A postmortem asks **how the system allowed the failure**, not who to blame. People who fear punishment hide mistakes, and hidden mistakes repeat. "Human error" is never the root cause: if one person's typo could take production down, the missing safeguard is the finding.

| ❌ Blameful | ✅ Blameless |
|---|---|
| "Ravi deployed a broken config." | "A config change reached production without validation; the pipeline has no schema check for config files." |
| "On-call ignored the alert." | "The alert fired 40 times last week with no impact, so it was indistinguishable from noise." |
| "Root cause: carelessness." | "Contributing factors: no staging parity for config, no canary, and the rollback script needed manual steps." |

**Postmortem template:**

```markdown
# Postmortem: Checkout errors after release 1.8.2 (SEV2, 2026-09-24)

**Status:** Action items in progress · **IC:** Asha · **Authors:** Asha, Ravi · **Reviewed:** 2026-09-29

## Summary
Between 14:02 and 14:32 IST, ~18% of checkout attempts failed. Release 1.8.2 lowered the payment
provider timeout from 10 s to 1 s; slow provider responses then failed instead of completing.

## Impact
- ~2,400 failed checkout attempts from ~1,400 customers; ~1,100 succeeded on retry, ~310 didn't complete a purchase
- Estimated lost revenue ₹4.1 lakh; 37 support tickets
- Error budget: 62% of the monthly checkout budget used

## Timeline (IST)
- 14:00 Release 1.8.2 deployed to 100% (no canary for config-only changes)
- 14:02 Checkout 5xx rate rises from 0.1% to 18%
- 14:06 Fast-burn alert pages on-call (Ravi)
- 14:15 SEV2 declared, Asha is IC; traces show provider calls timing out at 1 s
- 14:30 Rollback started; 14:32 error rate back to baseline
- 16:02 Resolved: the provider's p99 latency (1.8 s) was confirmed to be normal for them

## Contributing factors
1. The timeout value was chosen without looking at the provider's latency data.
2. Config-only changes skip the canary stage.
3. There was no alert on provider timeouts specifically; we only saw them as checkout 5xx.

## What went well
- Detected within 4 minutes by the SLO burn-rate alert; rollback took 2 minutes.

## Where we got lucky
- It happened in the afternoon; the night on-call rotation has no payments expert.

## Action items
| # | Action | Type | Owner | Due | Ticket |
|---|---|---|---|---|---|
| 1 | Set timeouts from measured p99 + margin; document it in the runbook | Prevent | Ravi | 2026-10-03 | PAY-812 |
| 2 | Send config changes through the same canary as code | Prevent | Platform | 2026-10-10 | PLAT-221 |
| 3 | Alert on payment-provider timeout rate | Detect | Asha | 2026-10-01 | PAY-813 |
| 4 | Make rollback a single command in the deploy tool | Mitigate | Platform | 2026-10-15 | PLAT-222 |
```

Rules that keep postmortems useful:

- Write one for every SEV1/SEV2, and for **near misses**: the incident that almost happened teaches the same lesson for free.
- Base it on the timeline and data, not memory. Review it in a meeting that's about the system, never about a person.
- Action items are **specific, owned, dated and tracked** like any other work. A postmortem whose action items never get done is theatre.
- Publish postmortems widely inside the company; other teams have the same weaknesses.

### 6. On-call that doesn't burn people out

- **Rotation:** weekly shifts with a primary and a secondary; follow-the-sun if you have teams in several time zones. Write handover notes (open issues, recent risky changes).
- **Page only for urgent, actionable, user-affecting problems.** Everything else becomes a ticket for business hours.
- **Target: a handful of pages per shift at most.** Google's SRE guidance is no more than about two incidents per 12-hour shift; beyond that, people can't investigate properly.
- **Review every page weekly:** Was it actionable? Did it have a runbook? Should it be tuned, turned into a ticket, or deleted?
- **Escalation policy:** if the primary doesn't acknowledge in 5–10 minutes, page the secondary, then the manager. Escalating is always acceptable and never a failure.
- **Care for people:** time off after a night of pages, on-call pay or compensation, and no hero culture.

**Enforce alert hygiene in CI.** Every paging alert must link to a runbook and name an owning team:

```python
# scripts/lint_alerts.py: fail CI when a paging alert has no runbook or owner (Prometheus rule files)
# pip install pyyaml; run: python scripts/lint_alerts.py alerts/*.yml
import sys
from pathlib import Path

import yaml

REQUIRED_ANNOTATIONS = ("summary", "runbook")


def problems_in(path: Path) -> list[str]:
    doc = yaml.safe_load(path.read_text(encoding="utf-8")) or {}
    problems = []
    for group in doc.get("groups", []):
        for rule in group.get("rules", []):
            name = rule.get("alert")
            if not name:
                continue                                   # recording rules don't page
            labels = rule.get("labels") or {}
            annotations = rule.get("annotations") or {}
            if labels.get("severity") not in {"page", "ticket"}:
                problems.append(f"{path}: {name}: severity must be 'page' or 'ticket'")
            if not labels.get("team"):
                problems.append(f"{path}: {name}: missing 'team' label (who gets paged?)")
            for key in REQUIRED_ANNOTATIONS:
                if not str(annotations.get(key, "")).strip():
                    problems.append(f"{path}: {name}: missing '{key}' annotation")
    return problems


if __name__ == "__main__":
    found = [p for arg in sys.argv[1:] for p in problems_in(Path(arg))]
    print("\n".join(found) or "All alerts have a severity, team, summary and runbook.")
    sys.exit(1 if found else 0)
```

### 7. Runbooks

A runbook turns "find the one person who knows" into steps anyone on-call can follow. Link it from the alert itself:

```markdown
# Runbook: CheckoutErrorBudgetFastBurn

**What it means:** checkout requests are failing fast enough to burn the monthly error budget in ~2 days.
**User impact:** customers can't pay. Treat as SEV2 unless the error rate is below 1%.

## Check
1. Dashboard "Checkout RED": which routes, since when, all regions or one?
2. Recent deploys: `deploy-tool history checkout --since 2h`
3. Traces filtered by `route=/checkout status=5xx`: which span fails?

## Mitigate
- Started after a deploy → `deploy-tool rollback checkout` (takes ~2 min)
- Payment provider timing out → turn off the flag `payments-provider-b`, which routes to provider A
- Overload → `kubectl scale deploy/checkout --replicas=12`

## Verify
- Error rate below 0.5% for 15 minutes on the dashboard, then close the page.

## Escalate
- Payments team (#team-payments, secondary on-call via the pager) if not mitigated in 20 minutes.
```

Keep runbooks **in the repository** next to the code (reviewed in PRs, versioned). Practise them in **game days**: break something on purpose in staging and have someone who didn't write the runbook follow it. When a step keeps being repeated, turn it into a script, and eventually into automatic remediation.

### 8. Architecture Decision Records (ADRs)

An ADR is a short document recording **one significant decision**, why it was made and what it costs. Six months later, "why on earth did we use X?" has an answer. Keep them numbered in the repo (`docs/adr/`), and never rewrite an accepted ADR: write a new one that **supersedes** it.

```markdown
# 7. Use PostgreSQL full-text search instead of Elasticsearch

- **Status:** Accepted
- **Date:** 2026-09-24
- **Deciders:** Asha, Ravi, Platform team

## Context
Product search must handle typos and rank results by relevance. We have ~200,000 products and
one PostgreSQL database. The team has no Elasticsearch experience, and a second datastore would
need syncing (outbox + indexer) and on-call coverage.

## Decision
Use PostgreSQL full-text search (`tsvector` + GIN) with a `pg_trgm` fuzzy fallback.

## Alternatives considered
- **Elasticsearch/OpenSearch:** best relevance tuning and facets; rejected for operational cost at our size.
- **Meilisearch:** great typo tolerance and easy to run; revisit if autocomplete quality falls short.

## Consequences
- ✅ One datastore, results always consistent with the data, no sync pipeline.
- ⚠️ Typo tolerance for short words is weaker; similarity thresholds need tuning.
- 🔁 Revisit when the catalogue exceeds ~5 million rows, or search p95 exceeds 200 ms.
```

A small script keeps the numbering and format consistent:

```js
// scripts/new-adr.js: node scripts/new-adr.js "Use PostgreSQL full-text search"
import { mkdirSync, readdirSync, writeFileSync } from "node:fs";
import { join } from "node:path";
import { fileURLToPath } from "node:url";

const slugify = (s) => s.normalize("NFKD").replace(/(\p{Script=Latin})\p{M}+/gu, "$1").normalize("NFC")
  .toLowerCase().replace(/[^\p{L}\p{M}\p{N}]+/gu, "-").replace(/^-+|-+$/g, "");

export function createAdr(title, { dir = "docs/adr", today = new Date().toISOString().slice(0, 10) } = {}) {
  if (!title?.trim()) throw new Error('Usage: node scripts/new-adr.js "Decision title"');
  mkdirSync(dir, { recursive: true });
  const numbers = readdirSync(dir).map((f) => Number.parseInt(f, 10)).filter(Number.isInteger);
  const next = Math.max(0, ...numbers) + 1;
  const file = join(dir, `${String(next).padStart(4, "0")}-${slugify(title) || "decision"}.md`);
  const body = `# ${next}. ${title.trim()}\n\n- **Status:** Proposed\n- **Date:** ${today}\n- **Deciders:** \n\n` +
    "## Context\n\n## Decision\n\n## Alternatives considered\n\n## Consequences\n";
  writeFileSync(file, body, { flag: "wx" });          // "wx": never overwrite an existing ADR
  return file;
}

if (process.argv[1] === fileURLToPath(import.meta.url)) {          // run directly, not imported
  try {
    console.log(`Created ${createAdr(process.argv.slice(2).join(" "))}`);
  } catch (err) {
    console.error(err.message);                                      // a usage message, not a stack trace
    process.exitCode = 1;
  }
}
```

Write an ADR when a decision is expensive to reverse, affects several teams, or will be questioned later: a database, a framework, an API style, a build-versus-buy choice. Don't write one for every library upgrade.

### 9. Documentation that stays current

Docs rot when they live far from the code and nobody owns them. What works:

- **Docs as code:** Markdown in the repository, changed **in the same PR** as the behaviour it describes, and reviewed like code. Add "docs updated?" to the PR template.
- **Generate reference docs** instead of hand-writing them: OpenAPI from the API (FastAPI does it automatically), TypeDoc/JSDoc, docstrings, database schema diagrams from migrations.
- **Four kinds of docs** (the Diátaxis framework): **tutorials** (learning), **how-to guides** (tasks), **reference** (facts), **explanation** (why). Mixing them produces pages that serve nobody.
- **Diagrams as code** (Mermaid, PlantUML, C4 model) live in the repo and change in PRs; screenshots of whiteboards don't get updated.
- **Owners and dates:** every runbook and design doc names an owning team and a "last reviewed" date; `CODEOWNERS` routes doc changes to them.
- **Automate the rot checks:** CI link checking, and a quarterly sweep that deletes or updates docs nobody has opened.
- **The onboarding test:** a new hire follows the README from a clean laptop. Every place they get stuck is a bug in the docs, so fix it in their first PR.

**A README that answers the first questions:** what the service does and who owns it; how to run it locally (one command); environment variables (with `.env.example`); how to test and deploy; architecture overview and diagram; links to runbooks, dashboards, ADRs and API docs.

### Interview Qs

1. What happens in the first 10 minutes of an incident? → Declare it, name an incident commander, assess impact and scope, and start mitigating (roll back, flag off, fail over) before investigating the root cause.
2. Why mitigate before finding the root cause? → Users are being hurt now. A reversible mitigation (rollback, flag, failover) stops the damage and buys time to understand the problem properly.
3. What does an incident commander do? → Coordinates, sets priorities, assigns people, owns communication cadence and closure. They deliberately don't debug.
4. What makes a postmortem blameless? Why does it matter? → It focuses on system conditions and missing safeguards instead of individuals. Blame makes people hide information, so failures repeat.
5. Why is "human error" not a root cause? → The system allowed one mistake to cause an outage. The missing validation, canary or guardrail is the real finding.
6. What should a postmortem contain? → Summary, quantified impact, timeline, contributing factors, what went well, where you got lucky, and owned, dated action items.
7. Time to detect vs acknowledge vs mitigate vs resolve? What improves each? → Alerts, on-call health, rollbacks and flags, and debuggability and code quality, respectively.
8. How do you keep on-call sustainable? → Page only for urgent, actionable, user-affecting issues, review every page, have runbooks and escalation, keep the page load low, and compensate people.
9. What's in a good runbook? → What the alert means, user impact, diagnosis steps, mitigations with exact commands, how to verify recovery, and who to escalate to.
10. What is an ADR? When do you write one? → A short record of a significant, hard-to-reverse decision: context, decision, alternatives, consequences. Supersede it rather than edit it.
11. How do you keep documentation from rotting? → Docs as code in the same PRs, generated reference docs, owners and review dates, link checks, and the onboarding test.

---

## 31. Gotchas Hall of Fame

Subtle bugs that look fine in code review and break in production. Entries marked **(caught in these notes)** are real bugs that turned up while testing the examples in these notes.

### JavaScript & the browser

**1. `Intl` output contains invisible non-breaking spaces** (caught in these notes)
```js
new Intl.NumberFormat("de-DE", { style: "currency", currency: "EUR" }).format(1234567.5) === "1.234.567,50 €";  // false!
// The space before € is U+00A0. ✅ In tests: normalize whitespace, or compare with another Intl call.
const norm = (s) => s.replace(/\s/g, " ");
```

**2. `forEach` doesn't wait for async callbacks**
```js
items.forEach(async (i) => await save(i));   // ❌ returns immediately; errors become unhandled rejections
for (const i of items) await save(i);        // ✅ sequential
await Promise.all(items.map(save));          // ✅ parallel
```

**3. `["1", "2", "3"].map(parseInt)` → `[1, NaN, NaN]`** — `map` passes `(value, index)`, so `parseInt("2", 1)`. ✅ `map(Number)` or `map((s) => parseInt(s, 10))`.

**4. `sort()` sorts numbers as strings** — `[10, 1, 5].sort()` → `[1, 10, 5]`. ✅ `sort((a, b) => a - b)`; and `sort` **mutates** (use `toSorted`).

**5. `new Date("2026-09-24")` is UTC midnight** — in the US it displays as **Sep 23**. Date-only strings parse as UTC, date-time strings without `Z` as local time. ✅ Store dates as `"YYYY-MM-DD"` strings for birthdays/deadlines; use explicit time zones for display.

**6. `fetch` doesn't reject on HTTP errors** — a 404/500 resolves normally. ✅ Always check `res.ok`.

**7. `0` renders in JSX** — `{items.length && <List />}` shows `0` for empty lists. ✅ `{items.length > 0 && …}`.

**8. `||` swallows valid falsy values** — `pageSize || 20` turns `0` into `20`. ✅ `??`.

**9. Logging a live object** — the console shows the object as it is *when expanded*, not when logged. ✅ Log `structuredClone(obj)` / JSON when state changes quickly.

**10. Base62/limit math off by one** (caught in these notes) — "7 base-62 characters cover IDs up to 3.5 trillion" is true, but `3_500_000_000_000` still has only 7 characters because 62⁷ ≈ 3.52 trillion. ✅ Test boundary values (`62⁷ − 1`, `62⁷`) in code instead of reasoning about them.

**11. A global regex in `test()` skips items** — `/^a/g` remembers `lastIndex`, so `words.filter((w) => re.test(w))` skips the word after each match. ✅ No `g` flag for `test()`; `g` is for finding many matches in one string.

**12. An HTML `pattern` that silently stops validating** — browsers compile `pattern` with the `v` flag, where `[\w.+-]` is a syntax error, and an invalid pattern is ignored (every value passes). ✅ Escape `-` and other class syntax characters: `[\w.+\-]`. Validate on the server anyway.

**13. `[\p{L}\p{N}]+` shreds Hindi words** (caught in these notes) — Devanagari vowel signs are combining marks (`\p{M}`), so a tokenizer without them turns "दिल्ली" into `["द","ल","ल"]`. ✅ `/[\p{L}\p{M}\p{N}]+/gu` for words in any script.

**14. Percentage rollouts that hash only the user id** (caught in these notes) — every flag at 10% selects the *same* 10% of users (measured: 100% overlap), so the same people get every risky change and A/B tests contaminate each other. ✅ Hash `flagKey + ":" + userId` (salted flags overlap ≈ 1% at 10% × 10%).

### React

**15. Ignoring an event in a reducer doesn't stop the side effect** (caught in these notes)
```jsx
async function handlePay() {
  send({ type: "SUBMIT" });     // the state machine ignores this while "submitting"…
  await pay();                  // ❌ …but pay() still runs a second time on a double click
}
// ✅ guard the side effect itself
if (!machine[state.status].SUBMIT) return;
```

**16. Components named like DOM globals** (caught in these notes) — a component called `Comment`, `Image`, `Option` or `Text` collides with the browser's built-in types/constructors in type checking and is confusing to read. ✅ `CommentItem`, `ProductImage`.

**17. Creating the debounced function during render** — `const d = debounce(fn, 300)` inside a component creates a new timer every render, so nothing is debounced. ✅ `useMemo`/`useRef`, or debounce the *value*.

**18. Stale closures in intervals** — `setInterval(() => setCount(count + 1), 1000)` with `[]` deps stays at 1. ✅ `setCount((c) => c + 1)`.

**19. Objects/arrays in effect dependencies** — a new `{}` every render re-runs the effect every render (possibly forever). ✅ Depend on primitives or memoize.

**20. React's `autoFocus` does nothing inside a `<dialog>` opened with `showModal()`** (caught in these notes) — React doesn't render the `autofocus` attribute; it calls `.focus()` on mount, while the dialog is still closed, so `showModal()` focuses the first focusable element instead (e.g. "Delete" rather than "Cancel"). ✅ Focus a `[data-autofocus]` element right after `showModal()`, or put the safe button first.

**21. Unstyled buttons fail WCAG 2.2 target size** (caught in these notes) — browser-default buttons and inputs are about 21px tall; axe's `target-size` rule (2.5.8, 24×24 px) flags them in a real browser, and jsdom-based tests can't see it. ✅ `button, input, select, [role=tab], [role=menuitem], [role=option] { min-height: 24px; min-width: 24px; }` and run axe in Playwright too.

### Node.js & Express

**22. Random 502s behind a load balancer** — Node's default `keepAliveTimeout` (5 s) is shorter than the load balancer's idle timeout (e.g. 60 s), so Node closes sockets the LB is about to reuse. ✅ `server.keepAliveTimeout = 65_000; server.headersTimeout = 66_000;`.

**23. There is no `req.signal` in Express** (caught in these notes) — to cancel upstream work when the client disconnects:
```js
const clientGone = new AbortController();
res.on("close", () => { if (!res.writableFinished) clientGone.abort(); });
```

**24. Express 4 doesn't catch rejected promises** — an `async` handler that throws hangs the request (or crashes on unhandled rejection). ✅ Express 5, or an `asyncHandler` wrapper.

**25. `express.json()` before the webhook route** — the raw body is gone, so signature verification always fails. ✅ `express.raw({ type: "application/json" })` on the webhook route.

**26. `sync` APIs in handlers** — `fs.readFileSync` / `crypto.pbkdf2Sync` in a request blocks every other request. ✅ async APIs or worker threads.

**27. ReDoS** — a regex with nested quantifiers such as `^(\w+\s?)*$` doubles its running time per input character (≈0.3 s at 26 characters, hours at 40) and blocks the event loop for everyone. ✅ Cap input length, avoid nested/overlapping quantifiers, escape user input with `RegExp.escape`, lint with `eslint-plugin-regexp`, or use RE2.

**28. Node's `fetch` has no overall timeout** — undici gives up only after 5 minutes without headers (or between body chunks), so one slow partner API ties up requests, sockets and memory. ✅ `fetch(url, { signal: AbortSignal.timeout(2_000) })` on every call, plus a circuit breaker for dependencies that fail repeatedly.

**29. Retries that make outages worse** — retrying every error (including 400/404 and non-idempotent POSTs), with no jitter, at several layers, turns a blip into a retry storm (3 layers × 3 retries = 27 calls). ✅ Retry only transient errors on idempotent requests, with full jitter, at one layer, honouring `Retry-After`.

**30. Compression middleware silently buffers Server-Sent Events** (caught in these notes) — with `app.use(compression())`, every event arrived only when the stream ended (measured). ✅ Send `Cache-Control: no-cache, no-transform` on `text/event-stream` responses (the middleware skips them), and `X-Accel-Buffering: no` for nginx.

**31. A newline inside an SSE `data:` line drops the rest of the message** — `res.write("data: " + text + "\n\n")` with multi-line text: the client treats the extra lines as unknown fields. ✅ Split the payload into one `data:` line per line (or JSON-encode it).

**32. A dual package with one top-level `types`** (caught in these notes) — `"types": "./dist/index.d.ts"` above `import`/`require` gives CommonJS users ESM typings: attw reports "Masquerading as ESM" and `module: node16` projects get TS1471 on `require`. ✅ Nested conditions: `import: { types: .d.ts, default: .js }`, `require: { types: .d.cts, default: .cjs }`.

**33. No `files` field → `.env` on the npm registry** — `npm pack --dry-run` without a whitelist listed `.env`, `src/` and tests; npm doesn't exclude `.env`. ✅ `"files": ["dist"]` and check `npm pack --dry-run` in CI.

**34. `^0.2.3` doesn't accept `0.3.0`** — below 1.0, caret ranges treat the *minor* number as breaking (and `^0.0.3` pins exactly). ✅ Release 1.0.0 once the API is used by others; bump minor for breaking changes while in 0.x.

### Python

**35. `defaultdict` + `+=` creates the key even when the right-hand side fails** (caught in these notes)
```python
totals = defaultdict(Decimal)
try:
    totals[region] += Decimal("abc")     # ❌ totals[region] = 0 is created BEFORE Decimal() raises
except InvalidOperation:
    pass
# ✅ parse first, then touch the dict
amount = Decimal(raw); totals[region] += amount
```

**36. Type hints are evaluated at definition time (before Python 3.14)** (caught in these notes) — `def f(p: Path)` without `from pathlib import Path` raises `NameError` when the module loads, even if `f` is never called. ✅ Import what you annotate (or `from __future__ import annotations`).

**37. Mutable default arguments** — `def add(item, cart=[])` shares one list across calls. ✅ `cart=None` then `cart = [] if cart is None else cart`.

**38. Late-binding closures** — `[lambda: i for i in range(3)]` all return `2`. ✅ `lambda i=i: i`.

**39. `requests` has no default timeout** — a hung server hangs your script forever. ✅ Always pass `timeout=` (or use `httpx`, which defaults to 5 s).

**40. Modifying a list while iterating it** skips elements. ✅ Build a new list (`[x for x in xs if keep(x)]`).

**41. `^…$` validation accepts a trailing newline** (caught in these notes) — in Python `$` also matches before a final `\n`, so `re.match(r"^\d+$", "123\n")` succeeds. ✅ `re.fullmatch(...)` (or `\Z`).

**42. `round()` is banker's rounding** (caught in these notes) — `round(1234.5) == 1234`, while JavaScript's `Math.round(1234.5) === 1235`, so a Node API and a Python worker disagreed on who is inside a 12.345% rollout. ✅ `math.floor(x + 0.5)` to match JS, or `Decimal.quantize(..., ROUND_HALF_UP)` for money.

**43. The sdist ships your `.env`** (caught in these notes) — with no `.gitignore` or include list, hatchling put `.env` (and every other local file) into the `.tar.gz` while the wheel looked clean. ✅ `[tool.hatch.build.targets.sdist] include = [...]` whitelist, and inspect **both** archives before publishing.

**44. No `py.typed` → mypy ignores your library** — users get *"module is installed, but missing library stubs or py.typed marker"* and none of your type hints are checked. ✅ Ship an empty `py.typed` in the package (and the `Typing :: Typed` classifier).

**45. "Strip all accents" slugify garbles Hindi** (caught in these notes) — removing every combining mark (`\p{M}` in JS, `unicodedata.combining` in Python) deletes Devanagari vowel signs: "नमस्ते दुनिया" → "नमसत-दनय". Python's `\w` doesn't match those signs either. ✅ Fold only characters that become plain ASCII (é → e) and keep marks elsewhere.

### FastAPI & SQLAlchemy

**46. `ContextVar` set in a sync (`def`) generator dependency** (caught in these notes) — FastAPI runs its setup and teardown in different threadpool contexts, so `var.reset(token)` after `yield` fails ("Token was created in a different Context"). ✅ Pass the value explicitly (e.g. `Session(info={"tenant_id": …})`) or use an `async def` dependency.

**47. `sqlite://` (in-memory) + a connection pool = empty database per connection** (caught in these notes) — "no such table" in tests. ✅ `poolclass=StaticPool` (or a file database / real Postgres in tests).

**48. Results without `ORDER BY` have no guaranteed order** (caught in these notes) — the same query returned rows in index order instead of insertion order. ✅ Always `ORDER BY` for lists, pagination and tests.

**49. `session.get(Model, id)` may skip the database** — it returns the object from the identity map if already loaded, bypassing query-level filters (e.g. tenant criteria). ✅ Use `select(...).where(...)` for scoped lookups, or check ownership explicitly.

**50. Blocking calls inside `async def`** — `requests.get` / `time.sleep` in an `async def` route freezes every request on that worker. ✅ async libraries, or a plain `def` route (runs in a threadpool).

**51. Auto-committing after `yield` in the DB dependency** — the commit can run after the response is sent, so a failed commit returns 200 for unsaved data. ✅ Commit explicitly in the service before returning.

**52. `TestClient` hangs on an endless stream** (caught in these notes) — reading one event from a live SSE feed and `break`ing still blocks forever, because the client waits for the app to finish. ✅ Test endless streams against a real `uvicorn` server in a thread with `httpx.stream(...)`; use `TestClient` only for streams that end.

### SQL & databases

**53. `NOT IN` with a NULL returns nothing** — `WHERE id NOT IN (SELECT department_id FROM employees)` returns zero rows as soon as one `department_id` is NULL. ✅ `NOT EXISTS`.

**54. A `WHERE` on the right table turns a `LEFT JOIN` into an `INNER JOIN`** — rows with no match silently vanish from the report. ✅ Put right-table conditions in `ON`.

**55. Lost updates from read-modify-write** — two requests read a balance of 100 and both write 70, so one withdrawal disappears (reproduced with two concurrent Postgres sessions in nodejs.md). ✅ `UPDATE … SET balance = balance - 30 WHERE balance >= 30`, `SELECT … FOR UPDATE`, or a version column.

**56. `created_at::date = …` on a `timestamptz`** — the index isn't used (Seq Scan), the day depends on the session's `TimeZone`, and Postgres rejects an expression index on it (not IMMUTABLE). ✅ Half-open range: `created_at >= start AND created_at < end`.

**57. Joining two child tables multiplies rows** — `SUM(o.total)` is inflated once `payments` is joined too (fan-out). ✅ Aggregate each child table in its own CTE, then join the totals.

**58. `ts_headline` output is not safe HTML** (caught in these notes) — it drops `<script>` but passes `<img src=x onerror=alert(1)>` through untouched. ✅ Private marker characters as StartSel/StopSel, HTML-escape the snippet, then replace the markers with `<mark>`.

**59. `pg_trgm` default thresholds miss real typos** — `word_similarity` for "labtop", "iphnoe", "headfones" is 0.40–0.50, under the 0.6 default, so `<%` finds nothing. ✅ Tune `pg_trgm.word_similarity_threshold` (≈0.35 here) against your data.

**60. Autocomplete with the `english` config misses partial words** — stored "running" is the stem `run`, so `runni:*` matches nothing. ✅ Prefix/autocomplete queries on `to_tsvector('simple', …)`.

### Shell, CI & tooling

**61. Commands on separate lines keep running after a failure** (caught in these notes) — a failed test followed by a deploy/splice step on the next line still deploys. ✅ Chain with `&&`, or start scripts with `set -euo pipefail`.

**62. zsh: a glob with no matches is an error** (caught in these notes) — `rm *.tmp` in an empty folder aborts the command chain (bash would pass the literal pattern instead). ✅ `rm -f -- *.tmp(N)` in zsh, `find . -name '*.tmp' -delete`, or do file handling in a script.

**63. "No errors" from a check that never ran** (caught in these notes) — a `grep … || echo "no errors"` printed success because the files to check were never created. ✅ Assert that the thing you're checking exists (count files/tests) before trusting a green result.

**64. Bundlers don't type-check** — Vite/esbuild/SWC strip TypeScript types; a build can succeed with type errors. ✅ `tsc --noEmit` in CI.

**65. zsh doesn't word-split variables** (caught in these notes) — `PSQL="psql -h localhost"; $PSQL -c "…"` works in bash but in zsh looks for a command literally named `psql -h localhost`. ✅ Use an array (`psql_cmd=(psql -h localhost); "${psql_cmd[@]}" -c "…"`), a shell function, or run the script with `bash`.

**66. `.gitattributes`/`.gitignore` patterns have no brace expansion** (caught in these notes) — `*.{cmd,bat} text eol=crlf` matches nothing, so Windows scripts silently get LF endings. ✅ One line per extension; verify with `git check-attr eol -- run.cmd`.

**67. `--force-with-lease` + a background fetch = overwritten teammate commits** — editors that auto-fetch update the lease, so the "safe" force-push replaces a colleague's pushed work (reproduced in these notes). ✅ `git push --force-with-lease --force-if-includes` (alias it).

**68. `git log -G '\w+'` finds nothing on macOS** (caught in these notes) — `-G` uses POSIX extended regex, where `\w`/`\d` aren't portable. ✅ `[[:alnum:]_]`, `[0-9]`.

**69. Paging alerts with no owner or runbook** (caught in these notes) — the burn-rate alert example in `nodejs.md` had `severity: page` but no `team` label, so nobody knew who gets woken up. ✅ Lint alert rules in CI: every paging alert needs a `team` label plus `summary` and `runbook` annotations.

**70. Turborepo "FULL TURBO" with no build output** (caught in these notes) — without `outputs` in `turbo.json`, a cache hit restores nothing: `dist/` stayed missing while turbo reported success. ✅ `"outputs": ["dist/**", "tsconfig.tsbuildinfo"]`.

**71. `tsc -b` "up to date" with no `dist/`** (caught in these notes) — deleting `dist/` but keeping `tsconfig.tsbuildinfo` makes incremental builds skip emitting. ✅ `tsc -b --clean`, and cache/delete the `.tsbuildinfo` together with `dist/`.

**72. npm workspaces hide phantom dependencies** — hoisting let an app import a package only another workspace declared (worked with npm, `ERR_MODULE_NOT_FOUND` with pnpm). ✅ pnpm's strict `node_modules`, and declare every import in its own `package.json`.







---

## 32. Checklists

### Before opening a PR

- [ ] Code is formatted, lint-clean and type-checks
- [ ] Names are clear; functions are small; no dead/commented-out code or debug logs
- [ ] Inputs validated; errors handled (no swallowed errors); user-facing messages are friendly
- [ ] Async code has timeouts, cleanup and no floating promises
- [ ] Security: authZ/ownership checks, no secrets, no injection, safe HTML/URLs
- [ ] Tests added/updated (happy path, edge cases, error paths, regression test for bugs)
- [ ] Loading/empty/error states handled in UI; accessibility basics checked
- [ ] Migrations are backwards compatible; API changes are non-breaking or versioned
- [ ] PR description explains what, why and how to test

### Before a production release

- [ ] Config validated; secrets in the secret manager; feature flags ready for risky features
- [ ] DB migrations reviewed, tested on a copy of production-like data, backups verified
- [ ] Monitoring, alerts and dashboards in place; source maps uploaded; logs structured
- [ ] Performance budget checked (bundle size, Web Vitals, p95 latency)
- [ ] Rate limits, CORS, security headers, HTTPS configured
- [ ] Health/readiness checks and graceful shutdown work
- [ ] Rollback plan documented
- [ ] Post-deploy verification steps defined

### New project setup

- [ ] Language version pinned (Node LTS / Python), lockfile committed
- [ ] TypeScript strict / mypy strict; ESLint + Prettier / ruff; pre-commit hooks
- [ ] Folder structure by feature with layers; app factory; config module with validation
- [ ] Logger with request IDs; error handling + consistent error format
- [ ] Test runner + first tests; CI pipeline
- [ ] `.env.example`, README, `.gitignore`, Dockerfile
- [ ] Dependency update bot and security scanning enabled

---

**This file is the summary. For the "why" and full examples, see the topic notes.**
