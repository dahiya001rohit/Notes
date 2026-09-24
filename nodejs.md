# Node.js — Complete Notes

> Every major Node.js concept, each with an explanation, 2–3 examples and interview questions.
> Covers internals (V8, libuv, event loop), core modules, streams, Express, REST, auth, databases, security, scaling, testing and deployment.
> The **Most Asked Interview Questions** are at the end.

---

## Table of Contents

1. [What is Node.js](#1-what-is-nodejs)
2. [Modules: CommonJS, ESM, require resolution](#2-modules)
3. [npm, package.json, semver, package-lock](#3-npm--packagejson)
4. [Globals & the process object](#4-globals--process)
5. [Environment Variables & Config](#5-environment-variables)
6. [fs — File System](#6-fs-module)
7. [path, os, url, util, crypto](#7-path-os-url-util-crypto)
8. [Events & EventEmitter](#8-events--eventemitter)
9. [Node Architecture: V8, libuv, Thread Pool](#9-node-architecture)
10. [The Node.js Event Loop (phases)](#10-the-nodejs-event-loop)
11. [process.nextTick vs setImmediate vs setTimeout vs Promises](#11-nexttick-vs-setimmediate-vs-settimeout)
12. [Blocking vs Non-blocking](#12-blocking-vs-non-blocking)
13. [Buffers](#13-buffers)
14. [Streams](#14-streams)
15. [http module — building a server from scratch](#15-http-module)
16. [Express.js basics](#16-expressjs)
17. [Routing](#17-routing)
18. [Middleware](#18-middleware)
19. [Error Handling (Express & process level)](#19-error-handling)
20. [REST API Design](#20-rest-api-design)
21. [Node Networking in Depth: TCP, Keep-Alive, HTTP Caching, Compression & Timeouts](#21-node-networking-in-depth-tcp-keep-alive-http-caching-compression--timeouts)
22. [Request Validation](#22-validation)
23. [API Documentation with OpenAPI (Swagger)](#23-api-documentation-with-openapi-swagger)
24. [Authentication: Sessions, Cookies, JWT, OAuth](#24-authentication)
25. [Authorization: RBAC](#25-authorization)
26. [Password Hashing (bcrypt/argon2)](#26-password-hashing)
27. [Advanced Authentication: OAuth PKCE, MFA (TOTP), Passkeys & Account Security](#27-advanced-authentication-oauth-pkce-mfa-totp-passkeys--account-security)
28. [CORS](#28-cors)
29. [Beyond Express: NestJS & Fastify](#29-beyond-express-nestjs--fastify)
30. [Databases: MongoDB & Mongoose](#30-mongodb--mongoose)
31. [Databases: SQL, PostgreSQL, Prisma](#31-sql--prisma)
32. [SQL vs NoSQL, Indexing, Transactions](#32-sql-vs-nosql-indexing-transactions)
33. [SQL Deep Dive: Joins, Window Functions, Query Plans & Locking](#33-sql-deep-dive-joins-window-functions-query-plans--locking)
34. [Search with PostgreSQL: Full-Text, Fuzzy Matching & Autocomplete](#34-search-with-postgresql-full-text-fuzzy-matching--autocomplete)
35. [Database Migrations & Seeding](#35-database-migrations--seeding)
36. [Data Import Pipelines: Stream CSV → Validate → Batch Insert → Report](#36-data-import-pipelines-stream-csv--validate--batch-insert--report)
37. [File Uploads (multer)](#37-file-uploads)
38. [Caching with Redis](#38-caching-with-redis)
39. [Rate Limiting](#39-rate-limiting)
40. [Security Best Practices](#40-security)
41. [OWASP API Security Top 10 (2023) with Examples](#41-owasp-api-security-top-10-2023-with-examples)
42. [Webhooks & Payment Integration](#42-webhooks--payment-integration)
43. [Logging & Monitoring](#43-logging--monitoring)
44. [Observability Hands-On: Logs, Metrics, Traces, SLOs & Alerts](#44-observability-hands-on-logs-metrics-traces-slos--alerts)
45. [child_process](#45-child_process)
46. [Worker Threads](#46-worker-threads)
47. [Cluster Module & Scaling](#47-cluster--scaling)
48. [WebSockets & Real-time (Socket.IO, SSE)](#48-websockets--real-time)
49. [Streaming Responses & Server-Sent Events in Depth](#49-streaming-responses--server-sent-events-in-depth)
50. [Job Queues & Background Work](#50-job-queues)
51. [BullMQ in Depth](#51-bullmq-in-depth)
52. [Testing (Jest/Vitest, Supertest, node:test)](#52-testing)
53. [Performance & Debugging, Memory Leaks](#53-performance--debugging)
54. [Graceful Shutdown](#54-graceful-shutdown)
55. [Microservices, API Gateway, Message Brokers](#55-microservices)
56. [Resilience: Timeouts, Retries, Circuit Breakers & Load Shedding](#56-resilience-timeouts-retries-circuit-breakers--load-shedding)
57. [GraphQL basics](#57-graphql-basics)
58. [Deployment: Docker, PM2, CI/CD, Nginx](#58-deployment)
59. [Project Structure (MVC / layered)](#59-project-structure)
60. [Building & Publishing an npm Package](#60-building--publishing-an-npm-package)
61. [Monorepos: pnpm Workspaces, Turborepo & Shared Packages](#61-monorepos-pnpm-workspaces-turborepo--shared-packages)
62. [Modern Node Features](#62-modern-node-features)
63. [System Design Basics for Backend Interviews](#63-system-design-basics-for-backend-interviews)
64. [Output-Based Questions](#64-output-based-questions)
65. [Most Asked Interview Questions](#65-most-asked-interview-questions)

---

## 1. What is Node.js

**Node.js** is an open-source, cross-platform **JavaScript runtime** built on Chrome's **V8 engine** that lets you run JS outside the browser (servers, CLIs, scripts, tooling).

Key characteristics:
- **Event-driven, non-blocking I/O** — handles many connections concurrently with a single main thread.
- **Single-threaded** event loop for JS; I/O runs in the background (OS async APIs + libuv thread pool).
- **npm** — the largest package ecosystem.
- Same language on frontend & backend.

### What is Node good / bad at?

| Good for | Not ideal for |
|---|---|
| I/O-heavy apps: APIs, real-time chat, streaming, proxies | CPU-heavy work (video encoding, heavy ML) on the main thread |
| Microservices, BFFs, serverless | Unless offloaded to worker threads / other services |
| CLIs & tooling (Vite, ESLint, Webpack) | |

### Browser JS vs Node JS

| Browser | Node |
|---|---|
| `window`, `document`, DOM | No DOM; `global`/`globalThis`, `process` |
| Sandboxed, no file system | Full OS access: fs, network, processes |
| ES modules natively | CommonJS (default) + ESM |
| You don't control the version | You choose the Node version |
| Web APIs (fetch, localStorage) | Node APIs (fs, http, crypto); also fetch since v18 |

### Your first Node script

```js
// hello.js
console.log("Hello from Node!");
const name = process.argv[2] ?? "World";   // command-line argument
console.log(`Hi ${name}`);
```

```bash
node --version          # check Node is installed (install from nodejs.org or with nvm)
node hello.js Rohit     # → Hello from Node! / Hi Rohit
node                    # interactive REPL, .exit to quit
```

Anything that's plain JavaScript (variables, functions, arrays, promises) works exactly as in the browser — only browser APIs like `document` and `window` are missing, and Node adds its own (`fs`, `http`, `process`…).

### Hello server

```js
// server.js
const http = require("node:http");
http.createServer((req, res) => {
  res.writeHead(200, { "Content-Type": "text/plain" });
  res.end("Hello from Node");
}).listen(3000, () => console.log("http://localhost:3000"));
```

```bash
node server.js
node --watch server.js     # auto-restart on change (Node 18.11+)
node --env-file=.env app.js # load .env without dotenv (Node 20.6+)
```

**Interview Qs**
- Is Node a language/framework? → Neither; it's a runtime.
- Is Node single-threaded? → JS execution is single-threaded; libuv uses a thread pool and the OS for I/O. Worker threads allow multi-threaded JS.
- Why is Node fast for I/O? → Non-blocking I/O + event loop; no thread per request.

---

## 2. Modules

### CommonJS (CJS) — default for `.js` unless `"type": "module"`

```js
// math.js
const add = (a, b) => a + b;
const PI = 3.14;
module.exports = { add, PI };
// exports.add = add;   ✅ adds a property
// exports = { add };   ❌ breaks the link with module.exports

// app.js
const { add, PI } = require("./math");
const math = require("./math");
```

### The module wrapper

Every CJS file is wrapped in a function — that's where `require`, `module`, `exports`, `__filename`, `__dirname` come from, and why top-level variables are private:

```js
(function (exports, require, module, __filename, __dirname) {
  // your module code
});
```

### require resolution order

1. **Core modules** (`fs`, `http`, or `node:fs`).
2. **Relative/absolute paths** (`./`, `../`, `/`): tries exact file, then `.js`, `.json`, `.node`, then directory `index.js` / `package.json "main"`.
3. **node_modules**: looks in `./node_modules`, then parent directories up to root.

### Caching

Modules are **cached** after the first `require` — the code runs once, and every `require` gets the same object (singleton behaviour).

```js
// counter.js
let count = 0;
module.exports = { inc: () => ++count };

// a.js
const c1 = require("./counter");
const c2 = require("./counter");
c1.inc(); c2.inc();
console.log(c1 === c2, c1.inc()); // true 3
delete require.cache[require.resolve("./counter")]; // force reload
```

### ES Modules in Node

Enable with `"type": "module"` in package.json, or use `.mjs` extension.

```js
// math.mjs
export const add = (a, b) => a + b;
export default function mul(a, b) { return a * b; }

// app.mjs
import mul, { add } from "./math.mjs";  // file extension REQUIRED in ESM
import fs from "node:fs/promises";
import data from "./data.json" with { type: "json" };

// __dirname in ESM
import { fileURLToPath } from "node:url";
import path from "node:path";
const __dirname = path.dirname(fileURLToPath(import.meta.url));
// Node 20.11+: import.meta.dirname, import.meta.filename

// top-level await
const config = JSON.parse(await fs.readFile("./config.json", "utf8"));
```

### Interop

- ESM can `import` CJS (default import = `module.exports`).
- CJS can `require()` ESM synchronously in Node 22+ (if no top-level await); otherwise use `await import()`.

### CJS vs ESM

| CommonJS | ESM |
|---|---|
| `require` / `module.exports` | `import` / `export` |
| Sync, runtime, dynamic | Static, async loading, analyzable |
| Can require conditionally anywhere | Static imports at top; `import()` for dynamic |
| Value copy of exports | Live bindings |
| `__dirname`, `__filename` | `import.meta.dirname` / `import.meta.url` |
| Extensions optional | Extensions required |
| No top-level await | Top-level await |

### Circular dependencies

```js
// a.js
exports.loaded = false;
const b = require("./b");
console.log("in a, b.loaded =", b.loaded);
exports.loaded = true;

// b.js
exports.loaded = false;
const a = require("./a");            // gets a's PARTIAL exports
console.log("in b, a.loaded =", a.loaded); // false
exports.loaded = true;
```

Avoid circular deps; refactor shared code into a third module.

**Interview Qs**
- `module.exports` vs `exports`? → `exports` is a reference to `module.exports`; reassigning `exports` breaks it. `require` returns `module.exports`.
- How does require work? → Resolve → load → wrap → execute → cache → return `module.exports`.
- Are modules singletons? → Yes, due to caching (per resolved path).

---

## 3. npm & package.json

### package.json key fields

```json
{
  "name": "my-api",
  "version": "1.2.3",
  "type": "module",
  "main": "dist/index.js",
  "exports": { ".": "./dist/index.js" },
  "engines": { "node": ">=20" },
  "scripts": {
    "dev": "node --watch src/index.js",
    "start": "node src/index.js",
    "test": "vitest",
    "build": "tsc",
    "prestart": "echo runs before start"
  },
  "dependencies": { "express": "^5.1.0" },
  "devDependencies": { "vitest": "^3.0.0" },
  "peerDependencies": { "react": ">=18" },
  "optionalDependencies": {}
}
```

- **dependencies** — needed at runtime.
- **devDependencies** — only for development/build/test (`npm i -D`). Skipped with `npm ci --omit=dev`.
- **peerDependencies** — the host project must provide it (plugins/libraries).

### Semantic versioning (MAJOR.MINOR.PATCH)

- MAJOR — breaking changes. MINOR — new features, backward compatible. PATCH — bug fixes.
- `^1.2.3` → `>=1.2.3 <2.0.0` (default).
- `~1.2.3` → `>=1.2.3 <1.3.0`.
- `1.2.3` → exact.
- `*` / `latest` → any.

### package-lock.json

Locks the **exact** versions of the entire dependency tree → reproducible installs. Commit it. `npm ci` installs exactly from the lockfile (faster, used in CI, fails if out of sync).

### Common commands

```bash
npm init -y
npm install express            # npm i express
npm i -D nodemon
npm i -g pm2
npm uninstall lodash
npm update
npm outdated
npm audit / npm audit fix
npm run dev
npx create-vite                # run a package binary without installing globally
npm ls express                 # dependency tree
npm version patch              # bump version + git tag
npm publish
npm link                       # symlink local package for development
```

Alternatives: **pnpm** (content-addressable store, disk efficient, strict), **yarn**, **bun**.

Publishing a library properly (`exports`, ESM + CommonJS, types, the `files` whitelist, semver, safe publishing from CI): Section 60.

**Interview Qs**
- npm vs npx? → npm manages packages; npx executes a package binary (downloads temporarily if needed).
- `npm install` vs `npm ci`? → install may update lockfile; ci installs exactly from lockfile after deleting node_modules.
- What is `node_modules/.bin`? → Local binaries available to npm scripts.

---

## 4. Globals & process

Node globals: `globalThis`/`global`, `process`, `Buffer`, `console`, `setTimeout/setInterval/setImmediate`, `queueMicrotask`, `structuredClone`, `fetch`, `URL`, `AbortController`, `TextEncoder`, `crypto` (web crypto). In CJS modules also `require`, `module`, `exports`, `__dirname`, `__filename` (module-scoped, not truly global).

### process

```js
process.argv;          // ["node path", "script path", ...args]
process.env.NODE_ENV;  // environment variables (always strings)
process.pid;
process.platform;      // "darwin", "linux", "win32"
process.cwd();         // current working directory
process.memoryUsage(); // { rss, heapTotal, heapUsed, external }
process.uptime();
process.hrtime.bigint(); // high-resolution time
process.exitCode = 1;  // preferred over process.exit() — lets pending I/O finish
process.exit(0);       // immediate exit

process.on("exit", (code) => console.log("exiting with", code)); // sync only
process.on("uncaughtException", (err) => { console.error(err); process.exit(1); });
process.on("unhandledRejection", (reason) => { console.error(reason); process.exit(1); });
process.on("SIGINT", () => { /* Ctrl+C */ });
process.on("SIGTERM", () => { /* docker/k8s stop */ });

process.stdout.write("no newline");
process.stdin.on("data", (chunk) => console.log("you typed", chunk.toString()));
```

### Example — simple CLI with args

```js
// node greet.js --name Rohit --loud
import { parseArgs } from "node:util";
const { values } = parseArgs({
  options: { name: { type: "string", short: "n" }, loud: { type: "boolean" } },
});
const msg = `Hello ${values.name ?? "world"}`;
console.log(values.loud ? msg.toUpperCase() : msg);
```

### Example — readline

```js
import readline from "node:readline/promises";
const rl = readline.createInterface({ input: process.stdin, output: process.stdout });
const name = await rl.question("Your name? ");
console.log(`Hi ${name}`);
rl.close();
```

---

## 5. Environment Variables

Keep config (ports, DB URLs, secrets) out of code — **12-factor app** principle.

```bash
# .env  (never commit! add to .gitignore; commit .env.example instead)
PORT=4000
DATABASE_URL=postgres://user:pass@localhost:5432/app
JWT_SECRET=supersecret
NODE_ENV=development
```

```js
// Option 1: Node 20.6+
// node --env-file=.env app.js
// Option 2: dotenv
import "dotenv/config";

const PORT = Number(process.env.PORT) || 3000;
```

### Validate config at startup (fail fast)

```js
import { z } from "zod";
const Env = z.object({
  NODE_ENV: z.enum(["development", "test", "production"]).default("development"),
  PORT: z.coerce.number().default(3000),
  DATABASE_URL: z.string().url(),
  JWT_SECRET: z.string().min(32),
});
export const env = Env.parse(process.env); // throws with a clear message if missing
```

`NODE_ENV=production` enables optimizations in many libraries (Express caches views, less verbose errors).

---

## 6. fs Module

Three API styles: **callback**, **promise** (`fs/promises`), **sync**.

### Example 1 — read/write

```js
import fs from "node:fs/promises";

await fs.writeFile("notes.txt", "Hello\n");            // create/overwrite
await fs.appendFile("notes.txt", "More text\n");
const content = await fs.readFile("notes.txt", "utf8"); // without encoding -> Buffer
await fs.rename("notes.txt", "notes-old.txt");
await fs.unlink("notes-old.txt");                       // delete file
await fs.copyFile("a.txt", "b.txt");
```

```js
// callback style (error-first)
const fsCb = require("node:fs");
fsCb.readFile("a.txt", "utf8", (err, data) => {
  if (err) return console.error(err.code); // ENOENT = file not found
  console.log(data);
});

// sync — ok for startup/scripts
const cfg = JSON.parse(fsCb.readFileSync("config.json", "utf8"));
```

### Example 2 — directories & stats

```js
await fs.mkdir("logs/2026/09", { recursive: true });
const entries = await fs.readdir(".", { withFileTypes: true });
for (const e of entries) console.log(e.name, e.isDirectory() ? "dir" : "file");
await fs.rm("logs", { recursive: true, force: true });

const stat = await fs.stat("package.json");
stat.size; stat.isFile(); stat.mtime;

try {
  await fs.access("maybe.txt");       // exists & accessible?
} catch { console.log("not found"); }

// recursive listing (Node 20+)
const all = await fs.readdir("src", { recursive: true });
```

### Example 3 — watch a file & JSON "database"

```js
import { watch } from "node:fs/promises";
for await (const event of watch("./config.json")) console.log(event.eventType, event.filename);
```

```js
const DB = "./db.json";
async function readDb() {
  try { return JSON.parse(await fs.readFile(DB, "utf8")); }
  catch (e) { if (e.code === "ENOENT") return { users: [] }; throw e; }
}
async function addUser(user) {
  const db = await readDb();
  db.users.push(user);
  await fs.writeFile(DB, JSON.stringify(db, null, 2));
}
```

Large files → use **streams** (Section 14), not `readFile` (loads everything into memory).

**Interview Qs**
- readFile vs createReadStream? → readFile buffers whole file in memory; streams process in chunks.
- Why avoid sync fs in servers? → Blocks the event loop for every request.

---

## 7. path, os, url, util, crypto

### path

```js
import path from "node:path";
path.join("/users", "rohit", "../docs", "a.txt"); // "/users/docs/a.txt"
path.resolve("src", "index.js");                    // absolute path from cwd
path.basename("/a/b/file.txt");                     // "file.txt"
path.basename("/a/b/file.txt", ".txt");             // "file"
path.extname("photo.jpeg");                         // ".jpeg"
path.dirname("/a/b/file.txt");                      // "/a/b"
path.parse("/home/u/file.txt");                     // { root, dir, base, ext, name }
path.sep;                                           // "/" or "\\"
path.normalize("/a//b/../c");                        // "/a/c"
```

Always use `path.join` instead of string concatenation for cross-platform paths.

### os

```js
import os from "node:os";
os.cpus().length;   // number of cores (used for clustering)
os.totalmem(); os.freemem();
os.platform(); os.hostname(); os.homedir(); os.tmpdir(); os.uptime();
os.EOL;             // line ending
os.availableParallelism(); // Node 18.14+
```

### url

```js
const u = new URL("https://api.site.com:8080/users?page=2&sort=name#top");
u.hostname; u.port; u.pathname; u.hash;
u.searchParams.get("page");     // "2"
u.searchParams.append("limit", "10");
u.toString();
```

### util

```js
import util from "node:util";
const sleep = util.promisify(setTimeout);
const readFileP = util.promisify(require("fs").readFile);
util.inspect({ deep: { nested: { obj: 1 } } }, { depth: null, colors: true });
util.types.isPromise(p);
util.format("%s is %d years", "Rohit", 25);
util.styleText("green", "OK"); // Node 20.12+
```

### crypto

```js
import crypto from "node:crypto";

crypto.randomUUID();                                   // "9b1d..."
crypto.randomBytes(32).toString("hex");                // secure random token
crypto.createHash("sha256").update("hello").digest("hex");
crypto.createHmac("sha256", "secret").update("payload").digest("hex"); // webhook signatures
crypto.timingSafeEqual(Buffer.from(a), Buffer.from(b));// constant-time compare

// Password hashing with scrypt (built-in)
const salt = crypto.randomBytes(16).toString("hex");
const hash = crypto.scryptSync("password", salt, 64).toString("hex");

// Symmetric encryption AES-256-GCM
function encrypt(text, key) {
  const iv = crypto.randomBytes(12);
  const cipher = crypto.createCipheriv("aes-256-gcm", key, iv);
  const enc = Buffer.concat([cipher.update(text, "utf8"), cipher.final()]);
  return { iv, enc, tag: cipher.getAuthTag() };
}
function decrypt({ iv, enc, tag }, key) {
  const d = crypto.createDecipheriv("aes-256-gcm", key, iv);
  d.setAuthTag(tag);
  return Buffer.concat([d.update(enc), d.final()]).toString("utf8");
}
const key = crypto.randomBytes(32);
decrypt(encrypt("secret msg", key), key); // "secret msg"
```

**Hashing vs Encryption**: hashing is one-way (passwords, integrity); encryption is two-way with a key (data you need back).

---

## 8. Events & EventEmitter

Much of Node's core is built on `EventEmitter` (streams, http server, process). It implements the **observer pattern**.

### Example 1 — basic

```js
import { EventEmitter } from "node:events";
const emitter = new EventEmitter();

emitter.on("greet", (name) => console.log(`Hello ${name}`));
emitter.once("greet", () => console.log("only first time"));
emitter.emit("greet", "Rohit"); // Hello Rohit, only first time
emitter.emit("greet", "Dev");   // Hello Dev
```

Listeners run **synchronously** in the order registered.

### Example 2 — extending EventEmitter

```js
class OrderService extends EventEmitter {
  placeOrder(order) {
    // ...save order
    this.emit("order:placed", order);
  }
}
const orders = new OrderService();
orders.on("order:placed", (o) => sendEmail(o.userEmail));
orders.on("order:placed", (o) => updateInventory(o.items));
orders.on("order:placed", (o) => analytics.track("order", o.id));
orders.placeOrder({ id: 1, userEmail: "a@b.com", items: [] });
// decoupled: OrderService doesn't know about email/inventory/analytics
```

### Example 3 — error event, removing listeners, async iteration

```js
emitter.on("error", (err) => console.error("handled:", err.message));
emitter.emit("error", new Error("boom")); // without an 'error' listener this THROWS and can crash the process

const handler = () => {};
emitter.on("tick", handler);
emitter.off("tick", handler);          // removeListener
emitter.removeAllListeners("tick");
emitter.listenerCount("tick");
emitter.setMaxListeners(20);           // default 10 -> "MaxListenersExceededWarning" hints a leak

import { once, on } from "node:events";
const [value] = await once(emitter, "ready");   // promise for a single event
for await (const [data] of on(emitter, "data")) { /* async iterator */ }
```

**Interview Qs**
- Are listeners sync or async? → Sync, in registration order.
- What happens if 'error' is emitted without a listener? → Throws, likely crashing the process.
- EventEmitter vs callbacks vs promises? → Emitters for multiple events over time; promises for a single future value.

---

## 9. Node Architecture

```
┌─────────────────────────────────────────────┐
│             Your JavaScript code            │
├─────────────────────────────────────────────┤
│   Node.js core APIs (fs, http, crypto ...)  │  ← JS
├─────────────────────────────────────────────┤
│   Node.js bindings (C++)                    │
├──────────────────────┬──────────────────────┤
│  V8 (JS engine)      │  libuv (C library)   │
│  - compiles & runs JS│  - event loop        │
│  - heap, GC          │  - thread pool (4)   │
│                      │  - async I/O via OS  │
└──────────────────────┴──────────────────────┘
   + c-ares (DNS), llhttp (HTTP parser), OpenSSL, zlib
```

### V8

Google's JS engine (C++). Compiles JS to machine code (JIT: Ignition interpreter + TurboFan optimizing compiler), manages the heap and garbage collection.

### libuv

C library that provides:
- The **event loop**.
- **Async I/O**: uses OS mechanisms (epoll on Linux, kqueue on macOS, IOCP on Windows) for network sockets — no threads needed.
- A **thread pool** (default **4** threads, `UV_THREADPOOL_SIZE` up to 1024) for operations that don't have async OS APIs:
  - File system (`fs.*`)
  - DNS lookup (`dns.lookup`)
  - Crypto (`pbkdf2`, `scrypt`, `randomBytes`)
  - Compression (`zlib`)

### Example — seeing the thread pool

```js
const crypto = require("node:crypto");
const start = Date.now();
for (let i = 1; i <= 6; i++) {
  crypto.pbkdf2("pw", "salt", 100000, 64, "sha512", () => {
    console.log(`hash ${i}: ${Date.now() - start}ms`);
  });
}
// With 4 threads: hashes 1-4 finish ~together, 5-6 take ~2x longer.
// process.env.UV_THREADPOOL_SIZE = 6 (set before any pool usage) -> all 6 finish together
```

### Example — network I/O doesn't use the pool

```js
const https = require("node:https");
for (let i = 0; i < 10; i++) {
  https.get("https://example.com", () => console.log("done", i)); // handled by OS async, not the 4 threads
}
```

**Interview Qs**
- Role of libuv? → Event loop, thread pool, cross-platform async I/O.
- Which operations use the thread pool? → fs, dns.lookup, crypto (some), zlib.
- Default thread pool size? → 4.

---

## 10. The Node.js Event Loop

When Node starts it: initializes the event loop → runs your script (sync code, schedules timers, registers callbacks) → enters the loop. The loop runs as long as there is pending work (active handles/requests).

### Phases (each has a FIFO queue of callbacks)

```
   ┌───────────────────────────┐
┌─>│           timers          │  setTimeout, setInterval callbacks
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │     pending callbacks     │  some system I/O callbacks deferred from last loop (e.g. TCP errors)
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │       idle, prepare       │  internal
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │           poll            │  retrieve new I/O events; run I/O callbacks (fs, network)
│  └─────────────┬─────────────┘  (may block here waiting for I/O if nothing else scheduled)
│  ┌─────────────┴─────────────┐
│  │           check           │  setImmediate callbacks
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
└──┤      close callbacks      │  socket.on('close'), etc.
   └───────────────────────────┘
```

**Between every callback** (Node 11+), Node drains:
1. the **`process.nextTick` queue**, then
2. the **Promise microtask queue**.

### Example 1 — ordering

```js
console.log("1: sync");
setTimeout(() => console.log("5: timeout"), 0);
setImmediate(() => console.log("6: immediate"));
Promise.resolve().then(() => console.log("4: promise"));
process.nextTick(() => console.log("3: nextTick"));
console.log("2: sync");

// 1: sync
// 2: sync
// 3: nextTick
// 4: promise
// 5: timeout   <- timeout vs immediate order is NOT guaranteed in the main module
// 6: immediate
```

### Example 2 — inside an I/O callback, setImmediate always runs first

```js
const fs = require("node:fs");
fs.readFile(__filename, () => {
  setTimeout(() => console.log("timeout"), 0);
  setImmediate(() => console.log("immediate"));
});
// immediate
// timeout
// (after poll phase comes check phase, then the loop goes back to timers)
```

### Example 3 — microtasks between callbacks

```js
setTimeout(() => {
  console.log("timeout 1");
  Promise.resolve().then(() => console.log("promise in timeout 1"));
  process.nextTick(() => console.log("nextTick in timeout 1"));
}, 0);
setTimeout(() => console.log("timeout 2"), 0);

// timeout 1
// nextTick in timeout 1
// promise in timeout 1
// timeout 2
```

**Interview Qs**
- Explain the Node event loop phases. (above)
- Where do promises run? → Microtask queue, drained after each callback (after nextTick queue).
- Why is `setTimeout(0)` vs `setImmediate` order non-deterministic in main module? → Depends on whether 1ms has elapsed when the loop enters the timers phase (process performance).

---

## 11. nextTick vs setImmediate vs setTimeout

| API | Queue | When |
|---|---|---|
| `process.nextTick(fn)` | nextTick queue | Right after the current operation, **before** promises and before the loop continues |
| `Promise.then / queueMicrotask` | microtask queue | After nextTick queue |
| `setTimeout(fn, 0)` | timers phase | Next loop iteration's timers phase (≥1ms) |
| `setImmediate(fn)` | check phase | After the poll phase of the current iteration |

Naming is confusing: `nextTick` fires more *immediately* than `setImmediate`.

### nextTick starvation

```js
function recurse() { process.nextTick(recurse); }
recurse(); // I/O and timers never run — event loop starved
// setImmediate recursion doesn't starve I/O (runs once per loop)
```

### Use case for nextTick — emit after the constructor returns

```js
const EventEmitter = require("node:events");
class Server extends EventEmitter {
  constructor() {
    super();
    // this.emit("ready") here would fire before anyone could listen
    process.nextTick(() => this.emit("ready"));
  }
}
const s = new Server();
s.on("ready", () => console.log("ready!")); // works
```

### Use case — consistent async API (don't release Zalgo)

```js
function getData(cache, key, cb) {
  if (cache.has(key)) {
    return process.nextTick(cb, null, cache.get(key)); // always async
  }
  fetchFromDb(key, cb);
}
```

---

## 12. Blocking vs Non-blocking

- **Blocking**: JS execution waits for the operation to finish (sync APIs, CPU loops).
- **Non-blocking**: operation starts, JS continues; result comes via callback/promise.

```js
const fs = require("node:fs");

// Blocking
const data = fs.readFileSync("big.txt", "utf8");
console.log(data.length);
console.log("after"); // waits for the read

// Non-blocking
fs.readFile("big.txt", "utf8", (err, d) => console.log(d.length));
console.log("after"); // prints first
```

### CPU-bound work blocks everything

```js
const http = require("node:http");
http.createServer((req, res) => {
  if (req.url === "/slow") {
    let sum = 0;
    for (let i = 0; i < 5e9; i++) sum += i; // blocks ALL requests for seconds
    return res.end(String(sum));
  }
  res.end("fast");
}).listen(3000);
// while /slow is computing, /fast also hangs
```

Fixes: worker threads, child processes, chunking work (`setImmediate` between chunks), moving to a job queue/another service.

```js
// Chunking to keep the loop responsive
function sumChunked(n, cb) {
  let i = 0, sum = 0;
  (function step() {
    const end = Math.min(i + 1e7, n);
    for (; i < end; i++) sum += i;
    if (i < n) setImmediate(step);
    else cb(sum);
  })();
}
```

**Rule**: never use `*Sync` APIs inside request handlers (OK at startup/CLI scripts).

---

## 13. Buffers

A **Buffer** is a fixed-size chunk of raw **binary memory** outside the V8 heap (a subclass of `Uint8Array`). Used for files, network packets, images, crypto.

```js
const b1 = Buffer.from("Hello");                // from string (utf8)
const b2 = Buffer.alloc(10);                     // zero-filled, safe
const b3 = Buffer.allocUnsafe(10);               // faster, may contain old memory
const b4 = Buffer.from([72, 105]);               // from bytes

b1.toString();            // "Hello"
b1.toString("base64");    // "SGVsbG8="
b1.toString("hex");       // "48656c6c6f"
Buffer.from("SGVsbG8=", "base64").toString(); // "Hello"
b1.length;                // bytes, not characters
Buffer.byteLength("₹");   // 3 bytes in utf8
b1[0];                    // 72
Buffer.concat([b1, Buffer.from(" World")]).toString();
b1.slice(0, 2); b1.subarray(0, 2); // views (share memory!)
b1.equals(Buffer.from("Hello"));
```

```js
// Encode credentials for Basic auth
const auth = "Basic " + Buffer.from(`${user}:${pass}`).toString("base64");
```

**Interview Qs**
- Why Buffers? → JS strings are UTF-16 text; binary data (files, TCP) needs raw bytes.
- `alloc` vs `allocUnsafe`? → alloc zero-fills (safe); allocUnsafe is faster but may leak old data.

---

## 14. Streams

**Streams** process data **piece by piece (chunks)** instead of loading it all into memory. Great for large files, HTTP bodies, video, compression.

### Types

| Type | Example |
|---|---|
| **Readable** | `fs.createReadStream`, `http.IncomingMessage` (req), `process.stdin` |
| **Writable** | `fs.createWriteStream`, `http.ServerResponse` (res), `process.stdout` |
| **Duplex** (read + write, independent) | TCP socket |
| **Transform** (duplex that modifies data) | `zlib.createGzip()`, `crypto` ciphers |

All streams are EventEmitters. Readable events: `data`, `end`, `error`, `close`. Writable: `drain`, `finish`, `error`.

### Example 1 — serve a big file without memory blowup

```js
import http from "node:http";
import fs from "node:fs";

http.createServer((req, res) => {
  // ❌ fs.readFile("4GB.mp4") -> loads everything into memory
  // ✅ stream it
  const stream = fs.createReadStream("big-video.mp4");
  res.writeHead(200, { "Content-Type": "video/mp4" });
  stream.pipe(res);
  stream.on("error", () => { res.statusCode = 500; res.end("error"); });
}).listen(3000);
```

### Example 2 — pipeline with compression (proper error handling)

```js
import { pipeline } from "node:stream/promises";
import fs from "node:fs";
import zlib from "node:zlib";

await pipeline(
  fs.createReadStream("access.log"),
  zlib.createGzip(),
  fs.createWriteStream("access.log.gz")
);
console.log("compressed");
// pipeline handles errors and destroys all streams; .pipe() doesn't forward errors.
```

### Example 3 — custom Transform stream

```js
import { Transform } from "node:stream";

const upperCase = new Transform({
  transform(chunk, encoding, callback) {
    callback(null, chunk.toString().toUpperCase());
  },
});
process.stdin.pipe(upperCase).pipe(process.stdout);
```

```js
// CSV line counter with readline over a stream
import readline from "node:readline";
const rl = readline.createInterface({ input: fs.createReadStream("huge.csv") });
let lines = 0;
for await (const line of rl) lines++;
console.log(lines);
```

### Custom Readable & Writable

```js
import { Readable, Writable } from "node:stream";

const numbers = Readable.from([1, 2, 3, 4]); // from any iterable/async iterable

class Counter extends Readable {
  #n = 0;
  _read() {
    this.#n++;
    this.push(this.#n > 5 ? null : String(this.#n)); // null = end
  }
}

const logger = new Writable({
  write(chunk, enc, cb) {
    console.log("got:", chunk.toString());
    cb();
  },
});
new Counter().pipe(logger);
```

### Backpressure

When the writable is slower than the readable, data buffers up in memory. `write()` returns `false` when the internal buffer exceeds `highWaterMark` → you should pause until `'drain'`. **`pipe()` and `pipeline()` handle backpressure automatically.**

```js
function writeMany(writer, data) {
  let i = 0;
  (function write() {
    let ok = true;
    while (i < data.length && ok) {
      ok = writer.write(data[i++]);
    }
    if (i < data.length) writer.once("drain", write); // wait for buffer to empty
    else writer.end();
  })();
}
```

### Modes

- **Flowing** — data events fire automatically (`on('data')`, `pipe`).
- **Paused** — you call `read()` manually.
- `objectMode: true` — chunks are JS objects instead of Buffers.

**Interview Qs**
- What are streams and why use them? → Memory efficiency + time efficiency (start processing before all data arrives).
- Types of streams? (table)
- What is backpressure? (above)
- `pipe` vs `pipeline`? → pipeline propagates errors and cleans up.

---

## 15. http Module

```js
import http from "node:http";

const users = [{ id: 1, name: "Rohit" }];

const server = http.createServer(async (req, res) => {
  const url = new URL(req.url, `http://${req.headers.host}`);
  res.setHeader("Content-Type", "application/json");

  if (req.method === "GET" && url.pathname === "/users") {
    return res.end(JSON.stringify(users));
  }

  if (req.method === "POST" && url.pathname === "/users") {
    let body = "";
    for await (const chunk of req) body += chunk; // req is a readable stream
    try {
      const user = { id: users.length + 1, ...JSON.parse(body) };
      users.push(user);
      res.statusCode = 201;
      return res.end(JSON.stringify(user));
    } catch {
      res.statusCode = 400;
      return res.end(JSON.stringify({ error: "Invalid JSON" }));
    }
  }

  const match = url.pathname.match(/^\/users\/(\d+)$/);
  if (req.method === "GET" && match) {
    const user = users.find((u) => u.id === Number(match[1]));
    res.statusCode = user ? 200 : 404;
    return res.end(JSON.stringify(user ?? { error: "Not found" }));
  }

  res.statusCode = 404;
  res.end(JSON.stringify({ error: "Route not found" }));
});

server.listen(3000, () => console.log("listening on 3000"));
```

This is why frameworks exist: routing, body parsing, error handling, middleware get tedious.

### Making HTTP requests from Node

```js
// Built-in fetch (Node 18+)
const res = await fetch("https://api.github.com/users/octocat", {
  headers: { "User-Agent": "node" },
  signal: AbortSignal.timeout(5000),
});
const data = await res.json();

// axios is also common
```

### HTTP basics to know

- **Methods**: GET (read), POST (create), PUT (replace), PATCH (partial update), DELETE, HEAD, OPTIONS.
- **Status codes**: 200 OK, 201 Created, 204 No Content, 301/302 redirect, 304 Not Modified, 400 Bad Request, 401 Unauthorized (not authenticated), 403 Forbidden (not allowed), 404 Not Found, 409 Conflict, 422 Unprocessable Entity, 429 Too Many Requests, 500 Internal Server Error, 502 Bad Gateway, 503 Service Unavailable, 504 Gateway Timeout.
- **Headers**: Content-Type, Authorization, Cache-Control, ETag, Set-Cookie, Accept.
- HTTP/1.1 keep-alive, HTTP/2 multiplexing, HTTPS = HTTP over TLS.

---

## 16. Express.js

**Express** is a minimal, unopinionated web framework for Node: routing, middleware, request/response helpers. (Express 5 is current: native async error handling, path-to-regexp v8.)

### Example 1 — basic CRUD API

```js
import express from "express";
const app = express();

app.use(express.json());                        // parse JSON bodies
app.use(express.urlencoded({ extended: true })); // parse form bodies

let todos = [{ id: 1, title: "Learn Node", done: false }];

app.get("/api/todos", (req, res) => {
  const { done } = req.query;                    // ?done=true
  const result = done === undefined ? todos : todos.filter((t) => String(t.done) === done);
  res.json(result);
});

app.get("/api/todos/:id", (req, res) => {
  const todo = todos.find((t) => t.id === Number(req.params.id));
  if (!todo) return res.status(404).json({ error: "Not found" });
  res.json(todo);
});

app.post("/api/todos", (req, res) => {
  const { title } = req.body;
  if (!title) return res.status(400).json({ error: "title is required" });
  const todo = { id: Date.now(), title, done: false };
  todos.push(todo);
  res.status(201).json(todo);
});

app.patch("/api/todos/:id", (req, res) => {
  const todo = todos.find((t) => t.id === Number(req.params.id));
  if (!todo) return res.status(404).json({ error: "Not found" });
  Object.assign(todo, req.body);
  res.json(todo);
});

app.delete("/api/todos/:id", (req, res) => {
  todos = todos.filter((t) => t.id !== Number(req.params.id));
  res.sendStatus(204);
});

app.listen(3000, () => console.log("Server on 3000"));
```

### Request object (`req`)

```js
req.params     // route params  /users/:id
req.query      // query string  ?page=2
req.body       // parsed body (needs express.json())
req.headers    // req.get("Authorization")
req.cookies    // needs cookie-parser
req.method, req.path, req.originalUrl, req.ip, req.hostname, req.protocol
```

### Response object (`res`)

```js
res.status(201).json({ ok: true });
res.send("text or buffer or object");
res.sendStatus(204);
res.set("X-Custom", "1");
res.cookie("token", t, { httpOnly: true, secure: true, sameSite: "strict", maxAge: 86400000 });
res.clearCookie("token");
res.redirect(301, "/new-url");
res.sendFile(path.join(__dirname, "public/index.html"));
res.download("/files/report.pdf");
res.render("view", { data }); // with a template engine (EJS, Pug)
res.locals.user = user;        // pass data between middleware / to views
```

### Example 2 — static files & template engine

```js
app.use(express.static("public"));             // serves public/style.css at /style.css
app.use("/assets", express.static("uploads"));

app.set("view engine", "ejs");
app.get("/", (req, res) => res.render("home", { name: "Rohit" }));
```

### Example 3 — app structure with routers

```js
// routes/user.routes.js
import { Router } from "express";
import * as userController from "../controllers/user.controller.js";
import { auth } from "../middleware/auth.js";

const router = Router();
router.get("/", userController.list);
router.get("/:id", userController.getById);
router.post("/", auth, userController.create);
export default router;

// app.js
import userRoutes from "./routes/user.routes.js";
app.use("/api/users", userRoutes);
```

**Interview Qs**
- Why Express over raw http? → Routing, middleware, body parsing, helpers, ecosystem.
- `res.send` vs `res.json`? → json always serializes to JSON and sets the header; send handles strings/buffers/objects.
- `app.use` vs `app.get`? → use mounts middleware for all methods (prefix match); get handles only GET with exact path matching.
- Alternatives? → Fastify (faster, schema-based), NestJS (opinionated, Angular-like, DI, TypeScript), Koa, Hono.

---

## 17. Routing

### Route parameters & patterns

```js
app.get("/users/:userId/posts/:postId", (req, res) => {
  res.json(req.params); // { userId: "1", postId: "42" }  (always strings)
});

app.get("/files/*path", (req, res) => res.send(req.params.path)); // Express 5 wildcard syntax
app.get("/users/:id{/:tab}", handler);                           // Express 5 optional segment
```

### Chaining with app.route

```js
app.route("/books")
  .get((req, res) => res.json(books))
  .post((req, res) => res.status(201).json(req.body));
```

### router.param — preload resources

```js
router.param("id", async (req, res, next, id) => {
  const user = await User.findById(id);
  if (!user) return res.status(404).json({ error: "User not found" });
  req.user = user;
  next();
});
router.get("/:id", (req, res) => res.json(req.user));
```

### API versioning

```js
app.use("/api/v1", v1Router);
app.use("/api/v2", v2Router);
```

### Query parsing & pagination

```js
app.get("/products", async (req, res) => {
  const page = Math.max(1, parseInt(req.query.page) || 1);
  const limit = Math.min(100, parseInt(req.query.limit) || 20);
  const sort = req.query.sort === "price" ? { price: 1 } : { createdAt: -1 };
  const [items, total] = await Promise.all([
    Product.find().sort(sort).skip((page - 1) * limit).limit(limit),
    Product.countDocuments(),
  ]);
  res.json({ items, page, limit, total, totalPages: Math.ceil(total / limit) });
});
```

**Offset vs cursor pagination**: offset (`skip/limit`) is simple but slow on large offsets and unstable with inserts; cursor (`?after=<lastId>`) is fast and consistent — used for infinite feeds.

---

## 18. Middleware

A **middleware** is a function `(req, res, next)` that runs in the request-response cycle. It can:
- execute code,
- modify `req`/`res`,
- end the cycle (send a response),
- call `next()` to pass control to the next middleware,
- call `next(err)` to jump to error-handling middleware.

Order matters — middleware runs in the order it's registered.

```
Request → [logger] → [json parser] → [auth] → [route handler] → Response
                                        ↘ next(err) → [error handler]
```

### Types

1. **Application-level** — `app.use(fn)`, `app.get(path, fn)`.
2. **Router-level** — `router.use(fn)`.
3. **Built-in** — `express.json()`, `express.urlencoded()`, `express.static()`.
4. **Third-party** — `cors`, `helmet`, `morgan`, `cookie-parser`, `compression`, `express-rate-limit`.
5. **Error-handling** — 4 args `(err, req, res, next)`.

### Example 1 — logger

```js
function logger(req, res, next) {
  const start = Date.now();
  res.on("finish", () => {
    console.log(`${req.method} ${req.originalUrl} ${res.statusCode} ${Date.now() - start}ms`);
  });
  next();
}
app.use(logger);
```

### Example 2 — auth middleware

```js
import jwt from "jsonwebtoken";

export function auth(req, res, next) {
  const header = req.headers.authorization;
  if (!header?.startsWith("Bearer ")) return res.status(401).json({ error: "No token" });
  try {
    req.user = jwt.verify(header.slice(7), process.env.JWT_SECRET);
    next();
  } catch {
    res.status(401).json({ error: "Invalid or expired token" });
  }
}

app.get("/api/profile", auth, (req, res) => res.json({ user: req.user }));
```

### Example 3 — configurable middleware (factory) & async wrapper

```js
const requireRole = (...roles) => (req, res, next) => {
  if (!roles.includes(req.user?.role)) return res.status(403).json({ error: "Forbidden" });
  next();
};
app.delete("/api/users/:id", auth, requireRole("admin"), deleteUser);

// Express 4: async errors are NOT caught automatically -> wrapper
const asyncHandler = (fn) => (req, res, next) => Promise.resolve(fn(req, res, next)).catch(next);
app.get("/api/items", asyncHandler(async (req, res) => {
  res.json(await Item.find());
}));
// Express 5: rejected promises from handlers are forwarded to next(err) automatically.
```

### Common third-party stack

```js
import cors from "cors";
import helmet from "helmet";
import morgan from "morgan";
import cookieParser from "cookie-parser";
import compression from "compression";

app.use(helmet());                   // security headers
app.use(cors({ origin: "https://myapp.com", credentials: true }));
app.use(compression());              // gzip responses
app.use(morgan("dev"));              // request logs
app.use(express.json({ limit: "1mb" }));
app.use(cookieParser());
```

**Interview Qs**
- What is middleware? What is `next`?
- What happens if you don't call `next()` or send a response? → Request hangs until timeout.
- How does Express identify error middleware? → By 4 parameters.
- Order of middleware matters — example? → `express.json()` must come before routes that read `req.body`; error handler must be last.

---

## 19. Error Handling

### Express error handling

```js
// Custom error class
class AppError extends Error {
  constructor(message, statusCode = 500, details) {
    super(message);
    this.statusCode = statusCode;
    this.details = details;
    this.isOperational = true; // expected error vs programming bug
  }
}

// In routes
app.get("/api/users/:id", async (req, res, next) => {
  const user = await User.findById(req.params.id);
  if (!user) throw new AppError("User not found", 404); // Express 5 catches it
  res.json(user);
});

// 404 handler (after all routes)
app.use((req, res, next) => next(new AppError(`Route ${req.originalUrl} not found`, 404)));

// Central error handler (last)
app.use((err, req, res, next) => {
  const status = err.statusCode || 500;
  if (status >= 500) console.error(err); // log bugs
  res.status(status).json({
    error: status >= 500 && process.env.NODE_ENV === "production" ? "Internal Server Error" : err.message,
    ...(err.details && { details: err.details }),
    ...(process.env.NODE_ENV !== "production" && { stack: err.stack }),
  });
});
```

### Operational vs programmer errors

| Operational (expected) | Programmer (bugs) |
|---|---|
| Invalid input, 404, DB timeout, network failure | `undefined is not a function`, wrong logic |
| Handle & respond gracefully | Log, crash and restart (process manager) |

### Process-level errors

```js
process.on("unhandledRejection", (reason) => {
  console.error("Unhandled Rejection:", reason);
  // Node 15+ crashes by default on unhandled rejections
  shutdown(1);
});

process.on("uncaughtException", (err) => {
  console.error("Uncaught Exception:", err);
  process.exit(1); // state may be corrupt — restart via PM2/Docker/k8s
});
```

### Error patterns in async code

```js
// Callback: error-first
fs.readFile(p, (err, data) => { if (err) return handle(err); });

// Promise
doWork().then(ok).catch(handle);

// async/await
try { await doWork(); } catch (e) { handle(e); }

// Event emitter
stream.on("error", handle);
```

---

## 20. REST API Design

**REST** (Representational State Transfer) is an architectural style for APIs over HTTP.

### Principles

1. **Client–server** separation.
2. **Stateless** — each request contains everything needed (e.g. token); server keeps no session between requests.
3. **Cacheable** responses (Cache-Control, ETag).
4. **Uniform interface** — resources identified by URIs, manipulated via representations (JSON), standard methods.
5. **Layered system** (proxies, load balancers, CDNs).
6. Code on demand (optional).

### Resource naming conventions

| Action | Method & Path | Status |
|---|---|---|
| List | `GET /api/v1/users` | 200 |
| Get one | `GET /api/v1/users/42` | 200 / 404 |
| Create | `POST /api/v1/users` | 201 + Location header |
| Replace | `PUT /api/v1/users/42` | 200 / 204 |
| Partial update | `PATCH /api/v1/users/42` | 200 |
| Delete | `DELETE /api/v1/users/42` | 204 |
| Nested | `GET /api/v1/users/42/orders` | 200 |
| Filter/sort/paginate | `GET /api/v1/products?category=phones&sort=-price&page=2&limit=20` | 200 |

- Use **nouns, plural**, lowercase, hyphens: `/order-items` (not `/getOrders`).
- Consistent error format: `{ "error": { "code": "VALIDATION_ERROR", "message": "...", "details": [...] } }`.
- Version your API (`/v1`).

### Idempotency

An operation is **idempotent** if doing it multiple times has the same effect as once.

| Method | Safe (no side effects) | Idempotent |
|---|---|---|
| GET, HEAD, OPTIONS | ✅ | ✅ |
| PUT | ❌ | ✅ |
| DELETE | ❌ | ✅ |
| PATCH | ❌ | ❌ (can be) |
| POST | ❌ | ❌ |

For payments, use an **Idempotency-Key** header to make POST retries safe.

### PUT vs PATCH

```
PUT   /users/1  { "name": "A", "email": "a@x.com" }  -> replaces the whole resource
PATCH /users/1  { "name": "A" }                       -> updates only name
```

### REST vs GraphQL vs gRPC

| REST | GraphQL | gRPC |
|---|---|---|
| Multiple endpoints | Single endpoint, client picks fields | RPC over HTTP/2 with Protobuf |
| Over/under-fetching possible | No over-fetching | Very fast, binary, streaming |
| HTTP caching easy | Caching harder | Service-to-service |

---

## 21. Node Networking in Depth: TCP, Keep-Alive, HTTP Caching, Compression & Timeouts

The networking details that separate "works on my machine" from "survives production traffic": connection reuse, timeouts, caching headers, compression and proxies.

### 1. TCP with the `net` module

HTTP, WebSockets, database drivers and Redis clients all sit on **TCP**. The `net` module gives you raw TCP sockets.

```js
// tcp-server.js — a line-based echo/chat server
import net from "node:net";

const clients = new Set();

const server = net.createServer((socket) => {
  clients.add(socket);
  socket.setEncoding("utf8");
  socket.write("Welcome! Type messages and press Enter.\n");

  let buffer = "";
  socket.on("data", (chunk) => {
    buffer += chunk;
    let newline;
    while ((newline = buffer.indexOf("\n")) !== -1) {      // frame messages by newline
      const message = buffer.slice(0, newline).trim();
      buffer = buffer.slice(newline + 1);
      for (const c of clients) if (c !== socket) c.write(`> ${message}\n`);
    }
  });
  socket.on("end", () => clients.delete(socket));
  socket.on("error", () => clients.delete(socket));          // ALWAYS handle socket errors (ECONNRESET)
});

server.listen(4000, () => console.log("TCP server on :4000"));   // try: nc localhost 4000
```

**TCP is a byte stream, not a message stream**: one `write("hello")` can arrive as two `data` events ("he", "llo"), and two writes can arrive merged. Every protocol needs **framing** — delimiters (`\n`), length prefixes, or a format like HTTP that defines message boundaries.

```js
// tcp-client.js
const client = net.createConnection({ host: "localhost", port: 4000 }, () => client.write("hi\n"));
client.on("data", (d) => process.stdout.write(d));
```

UDP (`node:dgram`) is connectionless and unreliable — used for DNS, metrics (StatsD), games, video.

### 2. DNS in Node

```js
import dns from "node:dns/promises";
await dns.lookup("example.com");          // uses the OS resolver (getaddrinfo) → runs on the libuv THREAD POOL
await dns.resolve4("example.com");        // queries DNS servers directly (c-ares) → no thread pool
```

Many slow outbound DNS lookups can saturate the 4-thread pool and slow down `fs`/`crypto` too. Reusing connections (keep-alive) avoids repeated lookups; some apps add DNS caching.

### 3. Outbound HTTP: reuse connections (keep-alive)

Every new HTTPS connection costs a DNS lookup + TCP handshake + TLS handshake (often 50–300 ms to a remote API). **Keep-alive** reuses open connections for many requests.

- Node's built-in **`fetch`** (powered by **undici**) pools and reuses connections by default.
- Since **Node 19**, `http.globalAgent`/`https.globalAgent` also use keep-alive by default.
- Libraries like axios use the Node agents → configure them for heavy traffic.

```js
// Tune a connection pool for a high-traffic upstream API (undici)
import { Agent, setGlobalDispatcher } from "undici";

setGlobalDispatcher(new Agent({
  connections: 100,            // max sockets per origin
  keepAliveTimeout: 10_000,    // keep idle sockets 10s
  connect: { timeout: 5_000 }, // TCP/TLS connect timeout
}));

// axios / http-based clients
import https from "node:https";
import axios from "axios";
const api = axios.create({
  baseURL: "https://api.partner.com",
  timeout: 8000,
  httpsAgent: new https.Agent({ keepAlive: true, maxSockets: 50 }),
});
```

**Create clients once and reuse them** (module-level or DI) — creating a new client/agent per request throws away the pool.

### 4. Timeouts — the most important production setting

Without timeouts, one slow dependency makes requests pile up until memory, sockets or the event loop are exhausted.

#### Client side (your server calling others)

```js
// fetch: overall deadline
const res = await fetch("https://api.partner.com/rates", { signal: AbortSignal.timeout(5000) });

// inside a route: cancel the upstream call if the client disconnects OR after 5s
const clientGone = new AbortController();
res.on("close", () => { if (!res.writableFinished) clientGone.abort(); });   // closed before we finished
const signal = AbortSignal.any([clientGone.signal, AbortSignal.timeout(5000)]);
const upstream = await fetch("https://api.partner.com/report", { signal });

// Timeout budgets: if YOUR endpoint must answer in 3s, dependencies must time out sooner (e.g. 1.5s)
```

Different timeouts: **connect** (reach the server), **response/headers** (first byte), **overall/idle** (whole request or silence between chunks). Also set **DB query timeouts** (`statement_timeout` in Postgres, `maxTimeMS` in Mongo) and pool acquire timeouts.

#### Server side (Node's HTTP server)

```js
const server = app.listen(3000);

server.requestTimeout = 30_000;     // max time to receive the whole request (Node default 300s)
server.headersTimeout = 66_000;     // max time to receive request headers
server.keepAliveTimeout = 65_000;   // how long an idle keep-alive socket stays open (default 5s)
```

**Load balancer gotcha**: if the load balancer's idle timeout (e.g. AWS ALB = 60s) is **longer** than Node's `keepAliveTimeout` (default 5s), Node may close a socket the LB is about to reuse → random **502 Bad Gateway** errors. Set `keepAliveTimeout` **above** the LB idle timeout (e.g. 65s) and `headersTimeout` slightly above that.

Per-request timeout in Express:

```js
app.use((req, res, next) => {
  res.setTimeout(10_000, () => {
    if (!res.headersSent) res.status(503).json({ error: "Request timed out" });
  });
  next();
});
```

### 5. HTTP caching in Express (ETag, 304, Cache-Control)

(See the JS notes "Networking for Frontend" for Cache-Control directives in general.)

#### ETags & 304 Not Modified — built in

Express automatically adds a (weak) **ETag** to `res.send`/`res.json` responses and answers **`304 Not Modified`** (no body) when the client sends a matching `If-None-Match`.

```
GET /api/products        → 200, ETag: W/"1a2b-xyz", body (20 KB)
GET /api/products        → If-None-Match: W/"1a2b-xyz"
                         ← 304 Not Modified (0 bytes body) — saves bandwidth
```

The body is still **generated** on the server (the ETag is a hash of it). For expensive responses, check freshness **before** doing the work:

```js
app.get("/api/products/:id", async (req, res) => {
  const meta = await db.product.findUnique({ where: { id: req.params.id }, select: { id: true, updatedAt: true } });
  if (!meta) return res.sendStatus(404);

  const etag = `"${meta.id}-${meta.updatedAt.getTime()}"`;      // cheap version-based ETag
  res.set({ ETag: etag, "Cache-Control": "private, no-cache" });  // browser may store, must revalidate
  if (req.fresh) return res.sendStatus(304);                      // req.fresh compares If-None-Match / If-Modified-Since

  const product = await loadFullProductWithRelations(req.params.id);  // expensive work only when needed
  res.json(product);
});
```

#### Cache-Control per route

```js
// Hashed static assets: cache forever
app.use("/assets", express.static("dist/assets", { maxAge: "1y", immutable: true }));

// SPA HTML: always revalidate so new deploys are picked up
app.get("*", (req, res) => {
  res.set("Cache-Control", "no-cache");
  res.sendFile(path.join(__dirname, "dist/index.html"));
});

// Public, shared data: CDN caches for 60s, serves stale for 5 min while refreshing
app.get("/api/categories", async (req, res) => {
  res.set("Cache-Control", "public, max-age=60, s-maxage=300, stale-while-revalidate=600");
  res.json(await getCategories());
});

// User-specific or sensitive data: never cache in shared caches
app.get("/api/me", auth, (req, res) => {
  res.set("Cache-Control", "private, no-store");
  res.json(req.user);
});
```

- Add `Vary: Accept-Encoding` (compression middleware does it) and `Vary: Origin` when CORS responses differ by origin.
- **Never** let CDNs cache responses that depend on cookies/Authorization unless the cache key includes them.

### 6. Compression

```js
import compression from "compression";

app.use(compression({
  threshold: 1024,                                  // don't bother for tiny responses
  filter: (req, res) => {
    if (req.headers["x-no-compression"]) return false;
    if (res.getHeader("Content-Type")?.toString().includes("text/event-stream")) return false; // SSE
    return compression.filter(req, res);            // default: compressible types only
  },
}));
```

- Compress text (HTML, CSS, JS, JSON, SVG); **not** images/video/zip/woff2 (already compressed).
- **Brotli** is smaller than gzip for text; recent `compression` versions support it, and CDNs/Nginx do it natively.
- In production, compression is usually done at the **reverse proxy / CDN** (saves Node CPU). Do it in one place, not both.
- Streaming/SSE responses: compression buffers output — disable it for those routes or flush explicitly.

### 7. Streaming HTTP responses

```js
// Stream a large CSV export — constant memory, backpressure handled by pipeline
import { pipeline } from "node:stream/promises";
import { Readable } from "node:stream";

app.get("/api/export.csv", auth, async (req, res) => {
  res.set({ "Content-Type": "text/csv", "Content-Disposition": 'attachment; filename="orders.csv"' });
  async function* rows() {
    yield "id,total,status\n";
    for await (const order of db.order.streamAll({ userId: req.user.id })) {   // cursor/batches from DB
      yield `${order.id},${order.total},${order.status}\n`;
    }
  }
  await pipeline(Readable.from(rows()), res);
});
```

### 8. Behind proxies & load balancers

```js
app.set("trust proxy", 1);     // trust ONE hop (your LB) → req.ip, req.protocol, req.secure use X-Forwarded-* headers
```

- Without it: `req.ip` is the load balancer's IP (rate limiting breaks), `req.secure` is false (secure cookies fail).
- Don't set `trust proxy: true` blindly when there's no proxy — clients could spoof `X-Forwarded-For`.
- TLS is usually terminated at the LB/proxy; HTTP/2 and HTTP/3 are usually handled there too (Node has `node:http2`, but most apps speak HTTP/1.1 to the proxy).

### 9. Closing connections on shutdown

```js
process.on("SIGTERM", () => {
  server.close(() => process.exit(0));   // stop accepting; wait for in-flight requests
  server.closeIdleConnections();         // close idle keep-alive sockets now (Node 18.2+)
  setTimeout(() => {
    server.closeAllConnections();        // force-close anything still open
    process.exit(1);
  }, 10_000).unref();
});
```

Without closing idle keep-alive sockets, `server.close()` can wait until they time out.

### 10. Other networking topics worth knowing

- **HTTPS server**: `https.createServer({ key, cert }, app)` — usually unnecessary behind a TLS-terminating proxy.
- **Ports**: < 1024 need root; run Node on 3000/8080 behind Nginx/LB on 80/443.
- **CORS** is a browser rule, not a network one (see CORS section).
- **Error codes**: `ECONNREFUSED` (nothing listening), `ECONNRESET` (peer closed abruptly), `ETIMEDOUT`, `ENOTFOUND` (DNS), `EADDRINUSE` (port taken), `EPIPE` (writing to a closed socket).
- **SSRF protection** when fetching user-provided URLs: allowlist hosts, block private IP ranges (`10.x`, `172.16–31.x`, `192.168.x`, `127.x`, `169.254.169.254` cloud metadata), and re-check after DNS resolution and redirects.

### Production checklist

- [ ] Timeouts on every outbound call, DB query and pool acquire
- [ ] Server `keepAliveTimeout` > load balancer idle timeout; `headersTimeout` > `keepAliveTimeout`
- [ ] Reused HTTP clients/agents with keep-alive and sane pool sizes
- [ ] Cache-Control set deliberately per route (immutable assets, no-cache HTML, private/no-store for user data)
- [ ] ETag / 304 for cacheable GETs; version-based ETags for expensive resources
- [ ] Compression in exactly one layer (proxy/CDN preferred), disabled for SSE
- [ ] `trust proxy` configured to the real number of proxies
- [ ] Graceful shutdown closes idle connections
- [ ] Socket `error` handlers on raw sockets; SSRF checks on user-supplied URLs

### Interview Qs

1. Why is TCP called a stream protocol? What is message framing?
2. `dns.lookup` vs `dns.resolve` — why can DNS affect `fs` performance in Node?
3. What is HTTP keep-alive and why does it matter for calling other services?
4. What timeouts should a Node service configure? What happens without them?
5. Why do you get random 502s behind a load balancer? → `keepAliveTimeout` shorter than the LB idle timeout.
6. How do ETags and 304 responses work in Express? Does a 304 save server CPU?
7. How would you set Cache-Control for static assets, HTML, public API data and private data?
8. Where should compression happen? What shouldn't be compressed?
9. What does `app.set("trust proxy")` do and why is it needed?
10. What is SSRF and how do you prevent it?

---

## 22. Validation

Never trust client input. Validate at the API boundary (body, params, query, headers).

### Zod

```js
import { z } from "zod";

const createUserSchema = z.object({
  name: z.string().trim().min(2).max(50),
  email: z.string().email().toLowerCase(),
  password: z.string().min(8).regex(/[A-Z]/, "Needs an uppercase letter"),
  age: z.number().int().min(13).optional(),
  role: z.enum(["user", "admin"]).default("user"),
});

const validate = (schema, source = "body") => (req, res, next) => {
  const result = schema.safeParse(req[source]);
  if (!result.success) {
    return res.status(400).json({ error: "Validation failed", details: result.error.flatten().fieldErrors });
  }
  req[source] = result.data; // sanitized, typed, with defaults
  next();
};

app.post("/api/users", validate(createUserSchema), createUser);
```

Other options: Joi, express-validator, Yup, class-validator (NestJS), AJV (JSON Schema, used by Fastify).

---

## 23. API Documentation with OpenAPI (Swagger)

An API without docs is an API nobody can use correctly. **OpenAPI** (formerly Swagger) is the standard, machine-readable format for describing REST APIs: endpoints, parameters, request/response bodies, auth and errors.

From one OpenAPI file you get:
- **Interactive docs** (Swagger UI, Redoc, Scalar) where people can try requests.
- **Generated typed clients** for the frontend (`openapi-typescript`, `orval`, `@hey-api/openapi-ts`) → frontend & backend types stay in sync.
- **Mock servers** (Prism), **contract tests**, and imports into Postman/Insomnia/Bruno.

### What an OpenAPI document looks like

```yaml
openapi: 3.1.0
info:
  title: Shop API
  version: 1.2.0
servers:
  - url: https://api.shop.com/v1
paths:
  /products/{id}:
    get:
      summary: Get a product
      tags: [products]
      parameters:
        - name: id
          in: path
          required: true
          schema: { type: string }
      responses:
        "200":
          description: The product
          content:
            application/json:
              schema: { $ref: "#/components/schemas/Product" }
        "404":
          $ref: "#/components/responses/NotFound"
      security:
        - bearerAuth: []
components:
  schemas:
    Product:
      type: object
      required: [id, name, price]
      properties:
        id: { type: string }
        name: { type: string }
        price: { type: integer, description: "Price in paise" }
  responses:
    NotFound:
      description: Resource not found
  securitySchemes:
    bearerAuth: { type: http, scheme: bearer, bearerFormat: JWT }
```

### Design-first vs code-first

| Design-first | Code-first |
|---|---|
| Write the OpenAPI spec first, review it, then implement | Generate the spec from code (schemas/annotations) |
| Great for public APIs & multiple teams agreeing on a contract | Docs can't drift from code; less duplication |
| Tools: Stoplight, Swagger Editor, Redocly | Tools: zod-to-openapi, tsoa, NestJS Swagger, Fastify schemas, FastAPI (built in) |

### Example 1 — Code-first from Zod schemas (single source of truth)

The same Zod schema validates requests **and** documents them.

```js
import express from "express";
import { z } from "zod";
import { extendZodWithOpenApi, OpenAPIRegistry, OpenApiGeneratorV31 } from "@asteasolutions/zod-to-openapi";
import swaggerUi from "swagger-ui-express";

extendZodWithOpenApi(z);
const registry = new OpenAPIRegistry();

const ProductSchema = registry.register("Product", z.object({
  id: z.string().openapi({ example: "p_123" }),
  name: z.string().min(1),
  price: z.number().int().positive().openapi({ description: "Price in paise" }),
}));
const CreateProduct = ProductSchema.omit({ id: true });

registry.registerComponent("securitySchemes", "bearerAuth", { type: "http", scheme: "bearer", bearerFormat: "JWT" });

registry.registerPath({
  method: "post",
  path: "/products",
  tags: ["products"],
  security: [{ bearerAuth: [] }],
  request: { body: { content: { "application/json": { schema: CreateProduct } } } },
  responses: {
    201: { description: "Created", content: { "application/json": { schema: ProductSchema } } },
    400: { description: "Validation error" },
  },
});

const spec = new OpenApiGeneratorV31(registry.definitions).generateDocument({
  openapi: "3.1.0",
  info: { title: "Shop API", version: "1.0.0" },
  servers: [{ url: "/api/v1" }],
});

const app = express();
app.get("/openapi.json", (req, res) => res.json(spec));
app.use("/docs", swaggerUi.serve, swaggerUi.setup(spec));

// The route validates with the SAME schema
app.post("/api/v1/products", express.json(), validate(CreateProduct), createProduct);
```

### Example 2 — JSDoc annotations (swagger-jsdoc)

```js
import swaggerJsdoc from "swagger-jsdoc";

/**
 * @openapi
 * /users/{id}:
 *   get:
 *     summary: Get a user by ID
 *     tags: [users]
 *     parameters:
 *       - in: path
 *         name: id
 *         required: true
 *         schema: { type: string }
 *     responses:
 *       200: { description: The user }
 *       404: { description: Not found }
 */
router.get("/users/:id", getUser);

const spec = swaggerJsdoc({
  definition: { openapi: "3.1.0", info: { title: "API", version: "1.0.0" } },
  apis: ["./src/routes/*.js"],
});
```

Easy to add to an existing app, but comments can drift from the real code — prefer schema-driven generation.

### Example 3 — Generating a typed frontend client

```bash
npx openapi-typescript http://localhost:3000/openapi.json -o src/api/schema.d.ts
```

```ts
import createClient from "openapi-fetch";
import type { paths } from "./api/schema";

const api = createClient<paths>({ baseUrl: "/api/v1" });
const { data, error } = await api.GET("/products/{id}", { params: { path: { id: "p_123" } } });
// data is typed as Product; typos in paths/params are compile errors
```

### API documentation best practices

- Document **every** endpoint: purpose, auth, params, request body, **all** response codes including errors, with **examples**.
- One consistent **error format** documented as a shared component.
- Describe units and formats (`price` in paise, dates ISO 8601 UTC, IDs as strings).
- Group with **tags**; give stable `operationId`s (used as generated client method names).
- Version the API (`/v1`) and mark old endpoints `deprecated: true` with a sunset date before removing.
- Keep docs **generated from code** or **validated in CI** (lint the spec with Spectral/Redocly; contract tests).
- Protect or disable docs in production for private APIs.
- Add a **changelog** for consumers.

### Interview Qs

- What is OpenAPI/Swagger and why use it?
- Design-first vs code-first?
- How do you keep docs in sync with code? → Generate from validation schemas, lint spec in CI, contract tests.
- How can the frontend benefit from an OpenAPI spec? → Generated typed clients, mocks.
- How do you deprecate an endpoint safely? → Mark deprecated, announce, monitor usage, versioned replacement, sunset date.

---

## 24. Authentication

**Authentication** = who are you? **Authorization** = what are you allowed to do?

### 1. Session-based (stateful)

1. User logs in → server creates a session (stored in memory/Redis/DB) → sends session ID in an `HttpOnly` cookie.
2. Browser sends the cookie automatically → server looks up the session.

```js
import session from "express-session";
import { RedisStore } from "connect-redis";

app.use(session({
  store: new RedisStore({ client: redisClient }),
  secret: process.env.SESSION_SECRET,
  resave: false,
  saveUninitialized: false,
  cookie: { httpOnly: true, secure: true, sameSite: "lax", maxAge: 1000 * 60 * 60 * 24 },
}));

app.post("/login", async (req, res) => {
  const user = await verifyCredentials(req.body.email, req.body.password);
  if (!user) return res.status(401).json({ error: "Invalid credentials" });
  req.session.regenerate(() => {        // prevent session fixation
    req.session.userId = user.id;
    res.json({ ok: true });
  });
});
app.post("/logout", (req, res) => req.session.destroy(() => res.clearCookie("connect.sid").json({ ok: true })));
```

### 2. JWT (JSON Web Token) — stateless

A JWT has 3 base64url parts: `header.payload.signature`.

```
header:    { "alg": "HS256", "typ": "JWT" }
payload:   { "sub": "42", "role": "admin", "iat": 1727150000, "exp": 1727150900 }
signature: HMACSHA256(base64(header) + "." + base64(payload), secret)
```

- Payload is **encoded, not encrypted** — anyone can read it. Never put secrets/passwords in it.
- The signature proves it wasn't tampered with.
- Server doesn't store it → scales easily; but **revoking** before expiry is hard (use short expiry + refresh tokens + denylist).

### Access + Refresh token flow

```js
import jwt from "jsonwebtoken";
import bcrypt from "bcrypt";

const signAccess = (user) =>
  jwt.sign({ sub: user.id, role: user.role }, process.env.JWT_SECRET, { expiresIn: "15m" });
const signRefresh = (user) =>
  jwt.sign({ sub: user.id, tokenVersion: user.tokenVersion }, process.env.REFRESH_SECRET, { expiresIn: "7d" });

app.post("/auth/login", async (req, res) => {
  const { email, password } = req.body;
  const user = await User.findOne({ email }).select("+password");
  if (!user || !(await bcrypt.compare(password, user.password))) {
    return res.status(401).json({ error: "Invalid email or password" }); // don't reveal which one
  }
  res.cookie("refreshToken", signRefresh(user), {
    httpOnly: true, secure: true, sameSite: "strict", path: "/auth/refresh", maxAge: 7 * 24 * 3600 * 1000,
  });
  res.json({ accessToken: signAccess(user) });
});

app.post("/auth/refresh", async (req, res) => {
  try {
    const payload = jwt.verify(req.cookies.refreshToken, process.env.REFRESH_SECRET);
    const user = await User.findById(payload.sub);
    if (!user || user.tokenVersion !== payload.tokenVersion) throw new Error("revoked");
    res.cookie("refreshToken", signRefresh(user), { httpOnly: true, secure: true, sameSite: "strict", path: "/auth/refresh" }); // rotate
    res.json({ accessToken: signAccess(user) });
  } catch {
    res.status(401).json({ error: "Please log in again" });
  }
});

app.post("/auth/logout-all", auth, async (req, res) => {
  await User.updateOne({ _id: req.user.sub }, { $inc: { tokenVersion: 1 } }); // invalidates all refresh tokens
  res.clearCookie("refreshToken", { path: "/auth/refresh" }).sendStatus(204);
});
```

### Session vs JWT

| Session | JWT |
|---|---|
| Stateful (server stores session) | Stateless (token holds claims) |
| Easy to revoke | Hard to revoke before expiry |
| Needs shared store (Redis) to scale | Scales horizontally easily |
| Cookie-based (CSRF protection needed) | Usually `Authorization: Bearer` header (or cookie) |
| Good for traditional web apps | Good for APIs, mobile, microservices |

### Where to store tokens on the client

- **HttpOnly Secure SameSite cookie** — not readable by JS (XSS-safe), needs CSRF protection.
- **Memory** (access token) + HttpOnly cookie (refresh token) — common SPA pattern.
- **localStorage** — easy but exposed to XSS.

### 3. OAuth 2.0 / OpenID Connect

**OAuth 2.0** is an **authorization** framework: lets an app access resources on another service on the user's behalf ("Login with Google" uses **OIDC** on top of OAuth for authentication).

Authorization Code flow (+ PKCE):
1. App redirects user to Google with `client_id`, `redirect_uri`, `scope`, `state`, `code_challenge`.
2. User logs in & consents → Google redirects back with a `code`.
3. Server exchanges `code` (+ `client_secret` / `code_verifier`) for tokens (access token, ID token).
4. Server reads the ID token (user info), creates its own session/JWT.

Libraries: Passport.js, Auth.js (NextAuth), better-auth, Lucia, or hosted (Auth0, Clerk, Supabase Auth, Firebase Auth).

### Other methods

API keys (server-to-server), Basic auth, MFA/TOTP (`otplib`), magic links, passkeys/WebAuthn.

**Interview Qs**
- What is JWT, its structure, pros/cons?
- How do you invalidate a JWT? → Short expiry, refresh token rotation, token version / denylist in Redis.
- Authentication vs authorization.
- Where would you store JWT in the browser and why?
- 401 vs 403.

---

## 25. Authorization

### Role-Based Access Control (RBAC)

```js
const permissions = {
  admin: ["user:read", "user:write", "user:delete", "post:*"],
  editor: ["post:read", "post:write"],
  user: ["post:read"],
};

const can = (role, perm) =>
  permissions[role]?.some((p) => p === perm || (p.endsWith(":*") && perm.startsWith(p.slice(0, -1))));

const authorize = (perm) => (req, res, next) =>
  can(req.user.role, perm) ? next() : res.status(403).json({ error: "Forbidden" });

app.delete("/api/users/:id", auth, authorize("user:delete"), deleteUser);
```

### Resource ownership (ABAC-style check)

```js
app.patch("/api/posts/:id", auth, async (req, res) => {
  const post = await Post.findById(req.params.id);
  if (!post) return res.status(404).end();
  if (post.authorId.toString() !== req.user.sub && req.user.role !== "admin") {
    return res.status(403).json({ error: "Not your post" }); // prevents IDOR
  }
  Object.assign(post, req.body);
  await post.save();
  res.json(post);
});
```

**IDOR** (Insecure Direct Object Reference) — accessing someone else's resource by changing an ID in the URL. Always check ownership.

---

## 26. Password Hashing

Never store plain-text passwords. Never use fast hashes (MD5/SHA-256) for passwords. Use slow, salted algorithms: **bcrypt**, **argon2** (recommended), **scrypt**.

- **Salt** — random value added per password so identical passwords have different hashes (defeats rainbow tables). bcrypt stores it inside the hash.
- **Cost factor / rounds** — makes brute force slow.

```js
import bcrypt from "bcrypt";

const hash = await bcrypt.hash("MyP@ssw0rd", 12);   // 12 salt rounds
// $2b$12$<22-char-salt><31-char-hash>
const ok = await bcrypt.compare("MyP@ssw0rd", hash); // true
```

```js
// Mongoose pre-save hook
userSchema.pre("save", async function () {
  if (!this.isModified("password")) return;
  this.password = await bcrypt.hash(this.password, 12);
});
userSchema.methods.comparePassword = function (plain) {
  return bcrypt.compare(plain, this.password);
};
```

```js
// argon2
import argon2 from "argon2";
const h = await argon2.hash("pw");
await argon2.verify(h, "pw");
```

### Password reset flow

1. User submits email → generate random token (`crypto.randomBytes(32)`), store **hashed** token + expiry (15 min).
2. Email a link with the raw token.
3. On submit: hash the incoming token, find the matching unexpired record, set new password, invalidate token and existing sessions.
4. Always respond "If that email exists, we sent a link" (prevents user enumeration).

---

## 27. Advanced Authentication: OAuth PKCE, MFA (TOTP), Passkeys & Account Security

Builds on Authentication (sessions/JWT), Authorization and Password Hashing. In production, prefer a well-tested library or provider (Auth.js, better-auth, Passport, Clerk, Auth0, Cognito, Keycloak) — but you must understand these flows to configure them safely and to answer interview questions.

### 1. "Login with Google" — OAuth 2.0 Authorization Code flow + PKCE (OpenID Connect)

**OAuth 2.0** = delegated authorization. **OpenID Connect (OIDC)** = identity layer on top that returns an **ID token** (a signed JWT saying who the user is). **PKCE** (Proof Key for Code Exchange) stops a stolen authorization `code` from being redeemed by anyone except the app that started the login. PKCE is required for SPAs/mobile apps and recommended for all clients.

```
Browser → GET /auth/google
Server: create state + nonce + code_verifier; store them (short-lived, HttpOnly cookie or session)
        redirect → accounts.google.com/o/oauth2/v2/auth?client_id&redirect_uri&response_type=code
                   &scope=openid email profile&state&nonce&code_challenge=S256(code_verifier)&code_challenge_method=S256
User logs in & consents → Google redirects → /auth/google/callback?code=…&state=…
Server: check state matches → POST token endpoint {code, code_verifier, client_id, client_secret, redirect_uri}
        → { id_token, access_token } → VERIFY id_token (signature via JWKS, iss, aud, exp, nonce)
        → find or create local user → create YOUR session → redirect to the app
```

```js
import crypto from "node:crypto";
import { createRemoteJWKSet, jwtVerify } from "jose";

const base64url = (buf) => Buffer.from(buf).toString("base64url");
const randomToken = (bytes = 32) => base64url(crypto.randomBytes(bytes));
export const pkceChallenge = (verifier) => base64url(crypto.createHash("sha256").update(verifier).digest());

const GOOGLE = {
  authorize: "https://accounts.google.com/o/oauth2/v2/auth",
  token: "https://oauth2.googleapis.com/token",
  issuer: "https://accounts.google.com",
  jwks: createRemoteJWKSet(new URL("https://www.googleapis.com/oauth2/v3/certs")),
};
const REDIRECT_URI = "https://api.myapp.com/auth/google/callback";
const tempCookie = { httpOnly: true, secure: true, sameSite: "lax", maxAge: 10 * 60 * 1000, path: "/auth/google" };

app.get("/auth/google", (req, res) => {
  const state = randomToken(), nonce = randomToken(), verifier = randomToken(32);
  res.cookie("oauth_tmp", JSON.stringify({ state, nonce, verifier }), tempCookie);
  const url = new URL(GOOGLE.authorize);
  url.search = new URLSearchParams({
    client_id: process.env.GOOGLE_CLIENT_ID,
    redirect_uri: REDIRECT_URI,
    response_type: "code",
    scope: "openid email profile",
    state,                                   // CSRF protection for the login flow
    nonce,                                   // binds the ID token to this login attempt (replay protection)
    code_challenge: pkceChallenge(verifier),
    code_challenge_method: "S256",
  }).toString();
  res.redirect(url.toString());
});

app.get("/auth/google/callback", async (req, res) => {
  const tmp = JSON.parse(req.cookies.oauth_tmp ?? "null");
  res.clearCookie("oauth_tmp", { path: "/auth/google" });
  if (!tmp || req.query.state !== tmp.state) return res.status(400).send("Invalid state");
  if (req.query.error) return res.redirect("/login?error=oauth_denied");

  const tokenRes = await fetch(GOOGLE.token, {
    method: "POST",
    headers: { "Content-Type": "application/x-www-form-urlencoded" },
    body: new URLSearchParams({
      grant_type: "authorization_code",
      code: String(req.query.code),
      code_verifier: tmp.verifier,
      redirect_uri: REDIRECT_URI,
      client_id: process.env.GOOGLE_CLIENT_ID,
      client_secret: process.env.GOOGLE_CLIENT_SECRET,
    }),
    signal: AbortSignal.timeout(10_000),
  });
  if (!tokenRes.ok) return res.status(502).send("Token exchange failed");
  const { id_token } = await tokenRes.json();

  const { payload } = await jwtVerify(id_token, GOOGLE.jwks, {       // signature + exp checked here
    issuer: GOOGLE.issuer,
    audience: process.env.GOOGLE_CLIENT_ID,
  });
  if (payload.nonce !== tmp.nonce) return res.status(400).send("Invalid nonce");
  if (!payload.email_verified) return res.status(400).send("Email not verified");

  const user = await findOrCreateOAuthUser({ provider: "google", providerId: payload.sub, email: payload.email, name: payload.name });
  await startSession(req, res, user);                                  // your own session / tokens
  res.redirect("/dashboard");
});
```

Key rules:
- Identify users by **`provider` + `sub`** (stable ID), not by email alone.
- **Account linking** by email only if the provider says `email_verified` — otherwise an attacker could claim someone's account.
- Validate **state**, **nonce**, **issuer**, **audience**, **expiry** and the **signature** (JWKS). Libraries like `openid-client` do all of this.
- Keep `client_secret` on the server; exact-match **redirect URIs** registered with the provider.
- Don't use the provider's access token as your app's session — create your own session.

### 2. Multi-factor authentication with TOTP (authenticator apps)

**TOTP** (RFC 6238) = HMAC of the current 30-second time step with a shared secret → 6-digit code. The server and the app compute the same code independently.

```js
import crypto from "node:crypto";

const BASE32 = "ABCDEFGHIJKLMNOPQRSTUVWXYZ234567";
export function base32Encode(buf) {
  let bits = "", out = "";
  for (const byte of buf) bits += byte.toString(2).padStart(8, "0");
  for (let i = 0; i < bits.length; i += 5) out += BASE32[parseInt(bits.slice(i, i + 5).padEnd(5, "0"), 2)];
  return out;
}
export function base32Decode(str) {
  let bits = "";
  for (const ch of str.replace(/=+$/, "").toUpperCase()) bits += BASE32.indexOf(ch).toString(2).padStart(5, "0");
  const bytes = [];
  for (let i = 0; i + 8 <= bits.length; i += 8) bytes.push(parseInt(bits.slice(i, i + 8), 2));
  return Buffer.from(bytes);
}

export function totp(secret /* Buffer */, { time = Date.now(), step = 30, digits = 6 } = {}) {
  const counter = Math.floor(time / 1000 / step);
  const msg = Buffer.alloc(8);
  msg.writeBigUInt64BE(BigInt(counter));
  const hmac = crypto.createHmac("sha1", secret).update(msg).digest();
  const offset = hmac[hmac.length - 1] & 0x0f;                         // dynamic truncation
  const binary = (hmac.readUInt32BE(offset) & 0x7fffffff) % 10 ** digits;
  return String(binary).padStart(digits, "0");
}

// Verify with ±1 step clock drift; return the matched step so it can't be reused
export function verifyTotp(secret, code, { time = Date.now(), window = 1, lastUsedStep = -1 } = {}) {
  const current = Math.floor(time / 1000 / 30);
  for (let w = -window; w <= window; w++) {
    const stepNo = current + w;
    if (stepNo <= lastUsedStep) continue;                                // replay protection
    const expected = totp(secret, { time: stepNo * 30 * 1000 });
    if (code.length === expected.length && crypto.timingSafeEqual(Buffer.from(code), Buffer.from(expected))) return stepNo;
  }
  return null;
}
```

**Enrollment**

```js
app.post("/mfa/setup", requireAuth, async (req, res) => {
  const secret = crypto.randomBytes(20);                                  // 160-bit secret
  const base32 = base32Encode(secret);
  await db.user.update({ where: { id: req.user.id }, data: { pendingTotpSecret: encrypt(base32) } }); // encrypted at rest
  const otpauth = `otpauth://totp/MyApp:${encodeURIComponent(req.user.email)}?secret=${base32}&issuer=MyApp&digits=6&period=30`;
  res.json({ otpauth });                                                  // frontend renders it as a QR code
});

app.post("/mfa/verify-setup", requireAuth, async (req, res) => {
  const user = await db.user.findUnique({ where: { id: req.user.id } });
  const step = verifyTotp(base32Decode(decrypt(user.pendingTotpSecret)), req.body.code);
  if (step === null) return res.status(400).json({ error: "Invalid code" });
  const recoveryCodes = Array.from({ length: 10 }, () => crypto.randomBytes(5).toString("hex"));
  await db.user.update({
    where: { id: user.id },
    data: {
      totpSecret: user.pendingTotpSecret, pendingTotpSecret: null, totpLastStep: step, mfaEnabled: true,
      recoveryCodes: await Promise.all(recoveryCodes.map((c) => bcrypt.hash(c, 10))),   // store HASHED
    },
  });
  res.json({ recoveryCodes });                                            // show ONCE
});
```

**Login with MFA**
1. Password correct → create a **short-lived "MFA pending" state** (not a full session).
2. `POST /mfa/challenge { code }` → verify TOTP (or a recovery code, which is then deleted) → **store the used time step** (no replay) → full session.
3. Rate-limit MFA attempts (a 6-digit code is only 1,000,000 combinations).

MFA options by strength: SMS (weakest, SIM-swap) < email codes < **TOTP** < **passkeys / security keys** (phishing-resistant).

### 3. Passkeys (WebAuthn)

A **passkey** is a public/private key pair created by the user's device (Face ID, Touch ID, Windows Hello, phone, security key). The **private key never leaves the device**; the server stores only the **public key**.

Why passkeys are better than passwords:
- **Phishing-resistant**: the key is bound to your domain; a fake site can't use it.
- Nothing reusable to steal from your database (public keys only).
- Faster login, no password to remember; often counts as MFA on its own (possession + biometric/PIN).

```
Registration:  server → random challenge + user info → browser navigator.credentials.create()
               → device creates key pair, signs → server verifies attestation, stores {credentialId, publicKey, counter}
Login:         server → random challenge → navigator.credentials.get()
               → device signs the challenge with the private key → server verifies signature with the stored public key
```

```js
// Server (using @simplewebauthn/server) — sketch
import { generateRegistrationOptions, verifyRegistrationResponse,
         generateAuthenticationOptions, verifyAuthenticationResponse } from "@simplewebauthn/server";

const rpID = "myapp.com", origin = "https://myapp.com";

app.post("/passkeys/register/options", requireAuth, async (req, res) => {
  const options = await generateRegistrationOptions({
    rpName: "MyApp", rpID, userName: req.user.email,
    excludeCredentials: (await getPasskeys(req.user.id)).map((p) => ({ id: p.credentialId })),
  });
  await saveChallenge(req.user.id, options.challenge);           // single-use, short-lived
  res.json(options);
});

app.post("/passkeys/register/verify", requireAuth, async (req, res) => {
  const { verified, registrationInfo } = await verifyRegistrationResponse({
    response: req.body, expectedChallenge: await takeChallenge(req.user.id), expectedOrigin: origin, expectedRPID: rpID,
  });
  if (!verified) return res.status(400).json({ error: "Verification failed" });
  await savePasskey(req.user.id, registrationInfo.credential);     // id, publicKey, counter
  res.json({ ok: true });
});
// Login: generateAuthenticationOptions → browser startAuthentication() → verifyAuthenticationResponse
```

```js
// Browser (using @simplewebauthn/browser)
import { startRegistration } from "@simplewebauthn/browser";
const options = await (await fetch("/passkeys/register/options", { method: "POST" })).json();
const attestation = await startRegistration({ optionsJSON: options });
await fetch("/passkeys/register/verify", { method: "POST", headers: { "Content-Type": "application/json" }, body: JSON.stringify(attestation) });
```

Keep a fallback (password + MFA, or email recovery) and let users register multiple passkeys.

### 4. Account security essentials

#### Brute-force protection (throttling & lockout)

```js
// Progressive delay per account + limits per IP (Redis)
async function checkLoginAllowed(email, ip) {
  const [accountFails, ipFails] = await Promise.all([
    redis.get(`login:fail:acct:${email}`), redis.get(`login:fail:ip:${ip}`),
  ]);
  if (Number(ipFails) >= 100) return { allowed: false, retryAfter: 3600 };        // one IP hammering many accounts
  const fails = Number(accountFails) || 0;
  if (fails >= 5) {
    const delay = Math.min(2 ** (fails - 5) * 30, 3600);                         // 30s, 60s, 120s… capped at 1h
    const lastFail = Number(await redis.get(`login:last:${email}`)) || 0;
    if (Date.now() / 1000 - lastFail < delay) return { allowed: false, retryAfter: delay };
  }
  return { allowed: true };
}
```

- Prefer **temporary, increasing delays** over permanent lockout (permanent lockout lets attackers lock victims out = DoS).
- Limit per **account** and per **IP**; add CAPTCHA after several failures.
- Same error message for "wrong email" and "wrong password" (no account enumeration); run a dummy hash when the user doesn't exist (timing).
- Notify users of new-device logins and security changes (password/MFA changed).

#### Breached-password check (Have I Been Pwned, k-anonymity)

Only the **first 5 characters of the SHA-1 hash** leave your server; the API returns all matching suffixes.

```js
export async function isBreachedPassword(password, fetchFn = fetch) {
  const sha1 = crypto.createHash("sha1").update(password).digest("hex").toUpperCase();
  const prefix = sha1.slice(0, 5), suffix = sha1.slice(5);
  const res = await fetchFn(`https://api.pwnedpasswords.com/range/${prefix}`, {
    headers: { "Add-Padding": "true" },
    signal: AbortSignal.timeout(3000),
  });
  if (!res.ok) return false;                                 // fail open (don't block signups if the API is down)
  const body = await res.text();
  return body.split("\n").some((line) => {
    const [hashSuffix, count] = line.trim().split(":");
    return hashSuffix === suffix && Number(count) > 0;
  });
}
```

#### Password policy (NIST SP 800-63B style)

- Minimum length (≥ 8, better 12–15+), allow long passphrases (64+ chars) and all characters including spaces/emoji.
- **No** forced composition rules (1 uppercase + 1 symbol…) and **no** periodic forced rotation — rotate only on compromise.
- **Block** breached/common passwords and context-specific ones (app name, username).
- Allow paste and password managers; show a strength meter.

#### Sessions & tokens

- **Rotate the session ID** on login and privilege change (prevents session fixation).
- Let users **see and revoke sessions/devices**; revoke all sessions on password change.
- **Re-authenticate** (password/passkey/MFA) for sensitive actions: changing email/password, adding payout accounts, deleting the account.
- **Email verification / password reset / magic-link tokens**: random (≥ 128 bits), **stored hashed**, **single-use**, short expiry (15–60 min), invalidated on use and on password change.
- "Remember me" = a longer-lived **refresh/session token**, not a stored password.

### Interview Qs

1. OAuth 2.0 vs OpenID Connect? What is an ID token?
2. Walk through the Authorization Code flow. What are `state`, `nonce` and PKCE for?
3. How do you verify an ID token? (JWKS signature, iss, aud, exp, nonce)
4. Why identify OAuth users by `sub` rather than email? When is linking by email safe?
5. How does TOTP work? How do you handle clock drift and replay?
6. Why store recovery codes hashed? Why store TOTP secrets encrypted (not hashed)?
7. What are passkeys and why are they phishing-resistant?
8. Lockout vs throttling — which is better and why?
9. How does the HIBP k-anonymity password check protect privacy?
10. What does NIST recommend about password rules and rotation?
11. How should password reset tokens be generated, stored and expired?

---

## 28. CORS

**CORS (Cross-Origin Resource Sharing)**: browsers block frontend JS from reading responses from a different **origin** (scheme + host + port) unless the server opts in with response headers.

- `http://localhost:5173` → `http://localhost:3000` = different origin (port).
- CORS is enforced by the **browser**; curl/Postman/servers ignore it.

### Preflight

For "non-simple" requests (methods like PUT/DELETE/PATCH, `Content-Type: application/json`, custom headers like `Authorization`), the browser first sends an `OPTIONS` request:

```
OPTIONS /api/users
Origin: https://app.com
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: content-type, authorization
```

Server replies:

```
Access-Control-Allow-Origin: https://app.com
Access-Control-Allow-Methods: GET, POST, PUT, DELETE
Access-Control-Allow-Headers: Content-Type, Authorization
Access-Control-Allow-Credentials: true
Access-Control-Max-Age: 600
```

### Express

```js
import cors from "cors";

app.use(cors()); // allow all origins (public APIs only)

const allowed = ["https://myapp.com", "http://localhost:5173"];
app.use(cors({
  origin: (origin, cb) => (!origin || allowed.includes(origin) ? cb(null, true) : cb(new Error("Not allowed by CORS"))),
  credentials: true,        // allow cookies; can't be used with origin "*"
  methods: ["GET", "POST", "PUT", "PATCH", "DELETE"],
}));
```

```js
// Manual
app.use((req, res, next) => {
  res.setHeader("Access-Control-Allow-Origin", "https://myapp.com");
  res.setHeader("Access-Control-Allow-Headers", "Content-Type, Authorization");
  res.setHeader("Access-Control-Allow-Methods", "GET,POST,PUT,PATCH,DELETE");
  if (req.method === "OPTIONS") return res.sendStatus(204);
  next();
});
```

Frontend with cookies: `fetch(url, { credentials: "include" })`.

Dev alternative: a Vite/Next **proxy** so frontend and API appear same-origin.

---

## 29. Beyond Express: NestJS & Fastify

Express is minimal and unopinionated — great to learn, but large teams end up inventing their own structure, validation, DI and docs. Two popular alternatives:

- **NestJS** — an opinionated, TypeScript-first **framework** with modules, dependency injection and decorators (Angular-style). Runs on Express (default) or Fastify under the hood.
- **Fastify** — a fast, low-overhead **web framework** built around JSON-Schema validation/serialization, plugins and hooks.

### Comparison

| | Express | Fastify | NestJS | Hono |
|---|---|---|---|---|
| Style | Minimal, middleware | Minimal, plugins + hooks + schemas | Full framework (modules, DI, decorators) | Minimal, Web-standard APIs |
| Performance | OK | Very fast | Depends on adapter (Express/Fastify) | Very fast, runs on edge runtimes |
| Validation | Bring your own (zod) | Built in (JSON Schema/AJV, TypeBox) | `class-validator` pipes (or zod) | Validator middleware (zod) |
| TypeScript | Add-on types | Good (type providers) | First-class | First-class |
| Structure | You decide | Plugins/encapsulation | Enforced architecture | You decide |
| Best for | Small/medium apps, learning | High-throughput APIs, microservices | Large teams, enterprise, complex domains | Edge/serverless (Cloudflare Workers, Bun, Deno) |

---

### Part 1 — NestJS

### Setup

```bash
npm i -g @nestjs/cli
nest new shop-api
nest g resource users        # generates module + controller + service + DTOs + tests
npm run start:dev
```

### Building blocks

| Piece | Role | Decorator |
|---|---|---|
| **Module** | Groups related controllers/providers; the app is a tree of modules | `@Module()` |
| **Controller** | HTTP layer: routes, params, status codes | `@Controller()`, `@Get()`, `@Post()`… |
| **Provider / Service** | Business logic, injected via DI | `@Injectable()` |
| **DTO** | Shape + validation rules of incoming data | `class-validator` decorators |
| **Pipe** | Validate/transform input | `ValidationPipe`, `ParseIntPipe` |
| **Guard** | Allow/deny a request (auth, roles) | `@UseGuards()` |
| **Interceptor** | Wrap the handler (logging, timing, response mapping, caching) | `@UseInterceptors()` |
| **Exception filter** | Turn exceptions into responses | `@Catch()` |
| **Middleware** | Express-style `(req, res, next)` | `NestMiddleware` |

### Request lifecycle

```
Request → Middleware → Guards → Interceptors (before) → Pipes → Controller handler → Service
        ← Exception filters (on error) ← Interceptors (after) ← response
```

### Example 1 — a complete feature module

```ts
// users/dto/create-user.dto.ts
import { IsEmail, IsString, MinLength, IsOptional, IsIn } from "class-validator";

export class CreateUserDto {
  @IsString() @MinLength(2)
  name: string;

  @IsEmail()
  email: string;

  @IsString() @MinLength(8)
  password: string;

  @IsOptional() @IsIn(["user", "admin"])
  role?: "user" | "admin";
}
```

```ts
// users/users.service.ts
import { Injectable, NotFoundException, ConflictException } from "@nestjs/common";
import { PrismaService } from "../prisma/prisma.service";
import * as bcrypt from "bcrypt";

@Injectable()
export class UsersService {
  constructor(private readonly prisma: PrismaService) {}          // injected by Nest's DI container

  async create(dto: CreateUserDto) {
    const exists = await this.prisma.user.findUnique({ where: { email: dto.email } });
    if (exists) throw new ConflictException("Email already registered");
    const password = await bcrypt.hash(dto.password, 12);
    const { password: _, ...user } = await this.prisma.user.create({ data: { ...dto, password } });
    return user;
  }

  async findOne(id: number) {
    const user = await this.prisma.user.findUnique({ where: { id }, select: { id: true, name: true, email: true } });
    if (!user) throw new NotFoundException(`User ${id} not found`);   // → 404 automatically
    return user;
  }
}
```

```ts
// users/users.controller.ts
import { Controller, Get, Post, Body, Param, ParseIntPipe, UseGuards, HttpCode } from "@nestjs/common";

@Controller("users")
export class UsersController {
  constructor(private readonly users: UsersService) {}

  @Post()
  @HttpCode(201)
  create(@Body() dto: CreateUserDto) {
    return this.users.create(dto);
  }

  @Get(":id")
  @UseGuards(JwtAuthGuard)
  findOne(@Param("id", ParseIntPipe) id: number) {          // "42" → 42, "abc" → 400
    return this.users.findOne(id);
  }
}
```

```ts
// users/users.module.ts
@Module({
  imports: [PrismaModule],
  controllers: [UsersController],
  providers: [UsersService],
  exports: [UsersService],          // other modules (e.g. AuthModule) can inject UsersService
})
export class UsersModule {}

// main.ts
async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.useGlobalPipes(new ValidationPipe({
    whitelist: true,               // strip properties without decorators (blocks mass assignment)
    forbidNonWhitelisted: true,    // or reject them with 400
    transform: true,               // convert payloads to DTO class instances / primitive types
  }));
  app.enableCors({ origin: ["https://myapp.com"], credentials: true });
  app.setGlobalPrefix("api/v1");
  app.enableShutdownHooks();       // graceful shutdown (onModuleDestroy hooks)
  await app.listen(process.env.PORT ?? 3000);
}
bootstrap();
```

### Example 2 — auth guard + roles decorator

```ts
// roles.decorator.ts
import { SetMetadata } from "@nestjs/common";
export const Roles = (...roles: string[]) => SetMetadata("roles", roles);

// roles.guard.ts
@Injectable()
export class RolesGuard implements CanActivate {
  constructor(private reflector: Reflector) {}
  canActivate(ctx: ExecutionContext): boolean {
    const required = this.reflector.getAllAndOverride<string[]>("roles", [ctx.getHandler(), ctx.getClass()]);
    if (!required) return true;                         // no @Roles → allowed
    const { user } = ctx.switchToHttp().getRequest();   // set earlier by JwtAuthGuard
    return required.includes(user?.role);               // false → 403 Forbidden
  }
}

// usage
@Delete(":id")
@UseGuards(JwtAuthGuard, RolesGuard)
@Roles("admin")
remove(@Param("id", ParseIntPipe) id: number) { return this.users.remove(id); }
```

(`JwtAuthGuard` typically comes from `@nestjs/passport` + `passport-jwt`, or a small custom guard using `@nestjs/jwt` to verify the Bearer token and attach `request.user`.)

### Example 3 — interceptor & exception filter

```ts
// logging.interceptor.ts — time every request
@Injectable()
export class LoggingInterceptor implements NestInterceptor {
  private readonly logger = new Logger("HTTP");
  intercept(ctx: ExecutionContext, next: CallHandler): Observable<unknown> {
    const req = ctx.switchToHttp().getRequest();
    const start = Date.now();
    return next.handle().pipe(
      tap(() => this.logger.log(`${req.method} ${req.url} ${Date.now() - start}ms`)),
    );
  }
}

// all-exceptions.filter.ts — consistent error format
@Catch()
export class AllExceptionsFilter implements ExceptionFilter {
  catch(exception: unknown, host: ArgumentsHost) {
    const res = host.switchToHttp().getResponse();
    const status = exception instanceof HttpException ? exception.getStatus() : 500;
    const message = exception instanceof HttpException ? exception.message : "Internal server error";
    if (status >= 500) console.error(exception);
    res.status(status).json({ error: { status, message } });
  }
}

// main.ts
app.useGlobalInterceptors(new LoggingInterceptor());
app.useGlobalFilters(new AllExceptionsFilter());
```

### Config, docs & testing

```ts
// Config (validated env)
@Module({ imports: [ConfigModule.forRoot({ isGlobal: true, validate: (env) => EnvSchema.parse(env) })] })
export class AppModule {}
// inject: constructor(private config: ConfigService) {}  → this.config.get("DATABASE_URL")

// Swagger docs from decorators/DTOs
const doc = SwaggerModule.createDocument(app, new DocumentBuilder().setTitle("Shop API").addBearerAuth().build());
SwaggerModule.setup("docs", app, doc);
```

```ts
// Unit test with mocked dependency (DI makes this easy)
describe("UsersService", () => {
  let service: UsersService;
  const prisma = { user: { findUnique: jest.fn(), create: jest.fn() } };

  beforeEach(async () => {
    const moduleRef = await Test.createTestingModule({
      providers: [UsersService, { provide: PrismaService, useValue: prisma }],
    }).compile();
    service = moduleRef.get(UsersService);
  });

  it("throws 404 when the user doesn't exist", async () => {
    prisma.user.findUnique.mockResolvedValue(null);
    await expect(service.findOne(1)).rejects.toThrow(NotFoundException);
  });
});

// E2E: create the app from AppModule, then supertest(app.getHttpServer()).get("/api/v1/users/1")
```

Also built in / official packages: `@nestjs/schedule` (cron), `@nestjs/bullmq` (queues), `@nestjs/websockets` (gateways), `@nestjs/microservices` (Kafka, RabbitMQ, gRPC, Redis transports), `@nestjs/cqrs`, `@nestjs/throttler` (rate limiting), `@nestjs/cache-manager`.

**NestJS best practices**: one module per feature/domain; thin controllers, logic in services; global `ValidationPipe` with `whitelist`; guards for auth/roles; filters for a consistent error shape; config via `ConfigModule` with validation; avoid circular module dependencies (use `forwardRef` only as a last resort — refactor instead).

---

### Part 2 — Fastify

### Example 1 — basic server with schema validation & serialization

```js
import Fastify from "fastify";

const app = Fastify({ logger: true });          // pino logger built in

const userSchema = {
  type: "object",
  properties: { id: { type: "integer" }, name: { type: "string" }, email: { type: "string" } },
};

app.post("/users", {
  schema: {
    body: {
      type: "object",
      required: ["name", "email"],
      properties: {
        name: { type: "string", minLength: 2 },
        email: { type: "string", format: "email" },
      },
      additionalProperties: false,
    },
    response: { 201: userSchema },              // serializer: only these fields are sent (fast + no leaks)
  },
}, async (request, reply) => {
  const user = await createUser(request.body);  // body already validated → 400 automatically if invalid
  return reply.code(201).send(user);            // `password` would be dropped by the response schema
});

app.get("/users/:id", {
  schema: { params: { type: "object", properties: { id: { type: "integer" } } } },   // "42" coerced to 42
}, async (request) => getUser(request.params.id));

await app.listen({ port: 3000, host: "0.0.0.0" });
```

Response schemas make serialization **faster** (compiled with `fast-json-stringify`) and prevent leaking fields.

### Example 2 — TypeScript with TypeBox (types inferred from schemas)

```ts
import Fastify from "fastify";
import { Type, type Static } from "@sinclair/typebox";
import type { TypeBoxTypeProvider } from "@fastify/type-provider-typebox";

const app = Fastify({ logger: true }).withTypeProvider<TypeBoxTypeProvider>();

const CreateProduct = Type.Object({
  name: Type.String({ minLength: 1 }),
  price: Type.Integer({ minimum: 1 }),
});
type CreateProduct = Static<typeof CreateProduct>;

app.post("/products", { schema: { body: CreateProduct } }, async (req) => {
  req.body.price;        // typed as number — from the same schema that validates at runtime
  return { ok: true };
});
```

### Example 3 — plugins, decorators, hooks & encapsulation

Everything in Fastify is a **plugin**. Plugins are **encapsulated**: decorators/hooks registered inside a plugin are only visible to that plugin and its children — unless wrapped with `fastify-plugin`.

```js
import fp from "fastify-plugin";

// Shared plugin (visible app-wide thanks to fp)
const dbPlugin = fp(async (app) => {
  const db = await connectDb(process.env.DATABASE_URL);
  app.decorate("db", db);                               // available as app.db / request.server.db
  app.addHook("onClose", async () => db.close());        // graceful shutdown
});

// Auth plugin — adds a reusable `authenticate` preHandler
const authPlugin = fp(async (app) => {
  await app.register(import("@fastify/jwt"), { secret: process.env.JWT_SECRET });
  app.decorate("authenticate", async (request, reply) => {
    try { await request.jwtVerify(); } catch { return reply.code(401).send({ error: "Unauthorized" }); }
  });
});

// Encapsulated route plugin with its own prefix and hooks
async function adminRoutes(app) {
  app.addHook("onRequest", app.authenticate);            // applies ONLY to routes in this plugin
  app.get("/stats", async () => app.db.stats());
}

app.register(dbPlugin);
app.register(authPlugin);
app.register(adminRoutes, { prefix: "/admin" });
app.register(import("@fastify/cors"), { origin: ["https://myapp.com"] });
app.register(import("@fastify/helmet"));
app.register(import("@fastify/rate-limit"), { max: 100, timeWindow: "1 minute" });
```

**Hook lifecycle** (in order): `onRequest` → `preParsing` → `preValidation` → `preHandler` → handler → `preSerialization` → `onSend` → `onResponse` (plus `onError`, `onTimeout`).

### Error handling & testing

```js
app.setErrorHandler((error, request, reply) => {
  if (error.validation) return reply.code(400).send({ error: "Validation failed", details: error.validation });
  request.log.error(error);
  reply.code(error.statusCode ?? 500).send({ error: error.statusCode ? error.message : "Internal Server Error" });
});

// Testing without opening a port
import { test } from "node:test";
import assert from "node:assert/strict";

test("GET /health", async () => {
  const app = buildApp();                                  // factory that registers plugins/routes
  const res = await app.inject({ method: "GET", url: "/health" });
  assert.equal(res.statusCode, 200);
  assert.deepEqual(res.json(), { status: "ok" });
  await app.close();
});
```

**Fastify best practices**: define schemas for body/params/query **and responses**; use TypeBox or zod type providers for TS; structure the app as plugins (`app.js` factory + `server.js` that listens); use `fastify-plugin` only for things that must be shared; lean on the official `@fastify/*` ecosystem (cors, helmet, jwt, rate-limit, swagger, multipart, static).

### Interview Qs

1. Express vs Fastify vs NestJS — when would you pick each?
2. Why is Fastify fast? → Schema-compiled validation/serialization, efficient routing (find-my-way), low overhead, pino logging.
3. What is plugin encapsulation in Fastify? What does `fastify-plugin` do?
4. What are NestJS modules, controllers and providers?
5. How does dependency injection work in NestJS and why does it help testing?
6. Explain the NestJS request lifecycle (middleware → guards → interceptors → pipes → handler → filters).
7. Guard vs middleware vs interceptor in NestJS?
8. How do you validate input in NestJS? What do `whitelist` and `transform` do?
9. How do you implement role-based authorization in NestJS? → Custom `@Roles` decorator + `Reflector` + guard.
10. How do response schemas help security in Fastify? → Only declared fields are serialized.

---

## 30. MongoDB & Mongoose

**MongoDB** is a NoSQL **document** database storing BSON (JSON-like) documents in collections. **Mongoose** is an ODM (Object Data Modeling) library adding schemas, validation, middleware and relationships.

### Connect

```js
import mongoose from "mongoose";
await mongoose.connect(process.env.MONGO_URI);
mongoose.connection.on("error", (err) => console.error(err));
```

### Schema & model

```js
const userSchema = new mongoose.Schema(
  {
    name: { type: String, required: [true, "Name required"], trim: true, maxlength: 50 },
    email: { type: String, required: true, unique: true, lowercase: true, match: /.+@.+\..+/ },
    password: { type: String, required: true, minlength: 8, select: false }, // excluded by default
    role: { type: String, enum: ["user", "admin"], default: "user" },
    age: { type: Number, min: 0 },
    tags: [String],
    address: { city: String, zip: String },          // embedded sub-document
    posts: [{ type: mongoose.Schema.Types.ObjectId, ref: "Post" }], // reference
  },
  { timestamps: true } // createdAt, updatedAt
);

userSchema.index({ email: 1 });
userSchema.virtual("isAdult").get(function () { return this.age >= 18; });
userSchema.methods.greet = function () { return `Hi ${this.name}`; };      // instance method
userSchema.statics.findByEmail = function (email) { return this.findOne({ email }); }; // static

export const User = mongoose.model("User", userSchema);
```

### CRUD

```js
// Create
const u = await User.create({ name: "Rohit", email: "r@x.com", password: "hashed" });

// Read
await User.find({ age: { $gte: 18 }, role: { $in: ["user", "admin"] } })
  .select("name email")
  .sort({ createdAt: -1 })
  .skip(0).limit(10)
  .lean();                                  // plain JS objects, faster
await User.findById(id);
await User.findOne({ email });
await User.countDocuments({ role: "admin" });

// Update
await User.findByIdAndUpdate(id, { $set: { name: "New" }, $inc: { loginCount: 1 } }, { new: true, runValidators: true });
await User.updateMany({ role: "user" }, { $push: { tags: "beta" } });

// Delete
await User.findByIdAndDelete(id);
await User.deleteMany({ age: { $lt: 13 } });
```

Query operators: `$eq $ne $gt $gte $lt $lte $in $nin $and $or $not $exists $regex $elemMatch`.
Update operators: `$set $unset $inc $push $pull $addToSet $rename`.

### Relationships: embedding vs referencing

| Embed | Reference |
|---|---|
| One-to-few, read together (address, line items) | One-to-many/many-to-many, large or independent data |
| Single query, atomic updates | Needs `populate`/`$lookup` |
| 16MB doc limit | Unbounded growth OK |

```js
const posts = await Post.find().populate("author", "name email"); // like a JOIN
```

### Aggregation pipeline

```js
const stats = await Order.aggregate([
  { $match: { status: "paid", createdAt: { $gte: new Date("2026-01-01") } } },
  { $group: { _id: "$customerId", total: { $sum: "$amount" }, orders: { $sum: 1 } } },
  { $sort: { total: -1 } },
  { $limit: 5 },
  { $lookup: { from: "users", localField: "_id", foreignField: "_id", as: "customer" } },
  { $unwind: "$customer" },
  { $project: { _id: 0, name: "$customer.name", total: 1, orders: 1 } },
]);
```

### Mongoose middleware (hooks)

```js
userSchema.pre("save", async function () { /* hash password */ });
userSchema.post("save", function (doc) { console.log("saved", doc._id); });
userSchema.pre(/^find/, function () { this.where({ deleted: { $ne: true } }); }); // soft delete filter
```

### Transactions (replica set required)

```js
const session = await mongoose.startSession();
await session.withTransaction(async () => {
  await Account.updateOne({ _id: from }, { $inc: { balance: -100 } }, { session });
  await Account.updateOne({ _id: to }, { $inc: { balance: 100 } }, { session });
});
session.endSession();
```

---

## 31. SQL & Prisma

### SQL essentials

```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  name TEXT NOT NULL,
  created_at TIMESTAMPTZ DEFAULT now()
);
CREATE TABLE posts (
  id SERIAL PRIMARY KEY,
  user_id INT REFERENCES users(id) ON DELETE CASCADE,
  title TEXT NOT NULL,
  views INT DEFAULT 0
);

SELECT u.name, COUNT(p.id) AS post_count
FROM users u
LEFT JOIN posts p ON p.user_id = u.id
GROUP BY u.id
HAVING COUNT(p.id) > 2
ORDER BY post_count DESC
LIMIT 10;
```

Joins: `INNER` (matches in both), `LEFT` (all left + matches), `RIGHT`, `FULL OUTER`, `CROSS`.

### node-postgres with parameterized queries (prevents SQL injection)

```js
import pg from "pg";
const pool = new pg.Pool({ connectionString: process.env.DATABASE_URL, max: 10 });

// ❌ SQL injection: `SELECT * FROM users WHERE email = '${email}'`
// ✅ parameters
const { rows } = await pool.query("SELECT id, name FROM users WHERE email = $1", [email]);

// Transaction
const client = await pool.connect();
try {
  await client.query("BEGIN");
  await client.query("UPDATE accounts SET balance = balance - $1 WHERE id = $2", [100, fromId]);
  await client.query("UPDATE accounts SET balance = balance + $1 WHERE id = $2", [100, toId]);
  await client.query("COMMIT");
} catch (e) {
  await client.query("ROLLBACK");
  throw e;
} finally {
  client.release();
}
```

**Connection pooling**: reuse a fixed set of DB connections instead of opening one per request (opening connections is slow and DBs have limits).

### Prisma ORM

```prisma
// prisma/schema.prisma
datasource db { provider = "postgresql"; url = env("DATABASE_URL") }
generator client { provider = "prisma-client-js" }

model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String
  posts     Post[]
  createdAt DateTime @default(now())
}

model Post {
  id       Int    @id @default(autoincrement())
  title    String
  author   User   @relation(fields: [authorId], references: [id])
  authorId Int
  @@index([authorId])
}
```

```bash
npx prisma migrate dev --name init   # create & apply migration
npx prisma generate                  # generate typed client
npx prisma studio                    # GUI
```

```js
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

const user = await prisma.user.create({
  data: { email: "r@x.com", name: "Rohit", posts: { create: [{ title: "Hello" }] } },
  include: { posts: true },
});
const users = await prisma.user.findMany({
  where: { email: { contains: "@x.com" } },
  select: { id: true, name: true, _count: { select: { posts: true } } },
  orderBy: { createdAt: "desc" },
  skip: 0, take: 10,
});
await prisma.user.update({ where: { id: 1 }, data: { name: "New" } });
await prisma.user.delete({ where: { id: 1 } });
await prisma.$transaction([
  prisma.account.update({ where: { id: 1 }, data: { balance: { decrement: 100 } } }),
  prisma.account.update({ where: { id: 2 }, data: { balance: { increment: 100 } } }),
]);
```

Other ORMs/query builders: Drizzle, TypeORM, Sequelize, Knex, Kysely.

### N+1 query problem

```js
// ❌ 1 query for posts + N queries for authors
const posts = await prisma.post.findMany();
for (const p of posts) p.author = await prisma.user.findUnique({ where: { id: p.authorId } });

// ✅ one query with join/include
const posts2 = await prisma.post.findMany({ include: { author: true } });
```

---

## 32. SQL vs NoSQL, Indexing, Transactions

### SQL vs NoSQL

| SQL (Postgres, MySQL) | NoSQL (MongoDB, Redis, Cassandra, DynamoDB) |
|---|---|
| Tables, rows, fixed schema | Documents/key-value/wide-column/graph, flexible schema |
| Relationships & JOINs | Denormalized, embed data |
| ACID transactions | Often BASE / eventual consistency (Mongo supports ACID too) |
| Vertical scaling (plus read replicas, sharding) | Horizontal scaling built-in |
| Complex queries, reporting, finance | Rapidly changing schema, huge scale, caching |

### ACID

- **Atomicity** — all or nothing.
- **Consistency** — constraints always hold.
- **Isolation** — concurrent transactions don't interfere (levels: read uncommitted, read committed, repeatable read, serializable). Anomalies, lost updates and row locking: Section 33.
- **Durability** — committed data survives crashes.

### CAP theorem

In a distributed system during a network **Partition**, you choose **Consistency** or **Availability**.

### Indexes

A data structure (usually **B-tree**) that speeds up reads at the cost of slower writes and more storage.

```sql
CREATE INDEX idx_posts_user ON posts(user_id);
CREATE INDEX idx_users_email_lower ON users (lower(email));
CREATE INDEX idx_orders_user_date ON orders(user_id, created_at DESC); -- compound: order matters (left-prefix rule)
EXPLAIN ANALYZE SELECT * FROM posts WHERE user_id = 5;                 -- check index usage
```

```js
// Mongo
userSchema.index({ email: 1 }, { unique: true });
orderSchema.index({ userId: 1, createdAt: -1 });
db.orders.find({ userId: 5 }).explain("executionStats");
```

Index columns used in `WHERE`, `JOIN`, `ORDER BY`. Don't over-index write-heavy tables. Reading `EXPLAIN` output and when indexes are skipped: Section 33.

### Normalization

Organize tables to reduce redundancy: 1NF (atomic values), 2NF (no partial dependency), 3NF (no transitive dependency). Denormalize deliberately for read performance.

### Scaling databases

Read replicas, sharding (partition data across servers by a shard key), caching (Redis), connection pooling, query optimisation.

---

## 33. SQL Deep Dive: Joins, Window Functions, Query Plans & Locking

SQL interview rounds and everyday backend work need the same skills: joining correctly, grouping, handling `NULL`, ranking with window functions, reading a query plan, and not losing updates when two requests arrive at once. Every query below runs on **PostgreSQL 16** and **SQLite 3.39+** unless it is marked `-- PostgreSQL` or `-- SQLite`.

### Sample schema & data

All examples use these tables. Paste them into `psql` or `sqlite3 :memory:` and follow along.

```sql
CREATE TABLE departments (id INTEGER PRIMARY KEY, name TEXT NOT NULL);

CREATE TABLE employees (
  id            INTEGER PRIMARY KEY,
  name          TEXT NOT NULL,
  department_id INTEGER REFERENCES departments(id),   -- NULL = contractor with no department
  manager_id    INTEGER REFERENCES employees(id),     -- NULL = top of the org chart
  salary        INTEGER NOT NULL
);

CREATE TABLE customers (id INTEGER PRIMARY KEY, name TEXT NOT NULL, city TEXT);

CREATE TABLE orders (
  id          INTEGER PRIMARY KEY,
  customer_id INTEGER NOT NULL REFERENCES customers(id),
  order_date  DATE NOT NULL,
  status      TEXT NOT NULL CHECK (status IN ('paid', 'cancelled', 'refunded')),
  total       INTEGER NOT NULL                          -- money as integer paise, never floats
);

CREATE TABLE logins (user_id INTEGER NOT NULL, login_date DATE NOT NULL);

INSERT INTO departments VALUES (1, 'Engineering'), (2, 'Sales'), (3, 'HR'), (4, 'Legal');

INSERT INTO employees VALUES
  (1,  'Asha',  1,    NULL, 250000),
  (2,  'Ben',   1,    1,    180000),
  (3,  'Chen',  1,    2,    120000),
  (4,  'Divya', 1,    2,    190000),
  (5,  'Eli',   2,    1,    150000),
  (6,  'Farah', 2,    5,     90000),
  (7,  'Gopal', 2,    5,     90000),
  (8,  'Jay',   2,    5,     60000),
  (9,  'Hana',  3,    1,     80000),
  (10, 'Ivan',  NULL, 1,     70000);

INSERT INTO customers VALUES
  (1, 'Kiran', 'Mumbai'), (2, 'Leela', 'Delhi'), (3, 'Mohan', 'Mumbai'), (4, 'Nisha', 'Pune'), (5, 'Omar', NULL);

INSERT INTO orders VALUES
  (1, 1, '2026-01-05', 'paid',      50000),
  (2, 1, '2026-01-20', 'paid',      30000),
  (3, 2, '2026-01-22', 'cancelled', 20000),
  (4, 2, '2026-02-03', 'paid',      70000),
  (5, 3, '2026-02-14', 'paid',      40000),
  (6, 1, '2026-02-28', 'refunded',  10000),
  (7, 3, '2026-03-02', 'paid',      90000),
  (8, 5, '2026-03-15', 'paid',      25000),
  (9, 2, '2026-03-18', 'paid',      15000);

INSERT INTO logins VALUES
  (1, '2026-03-01'), (1, '2026-03-02'), (1, '2026-03-03'), (1, '2026-03-05'), (1, '2026-03-06'),
  (2, '2026-03-01'), (2, '2026-03-03');
```

### The order a query is evaluated in

You write `SELECT … FROM … WHERE …`, but the database evaluates it in this logical order:

```
FROM / JOIN → WHERE → GROUP BY → HAVING → SELECT (window functions run here) → DISTINCT → ORDER BY → LIMIT / OFFSET
```

This order explains most "why doesn't this work?" errors:

- `WHERE` runs before grouping, so it can't use aggregates. `WHERE COUNT(*) > 1` is an error; use `HAVING`.
- `WHERE` runs before `SELECT`, so it can't use window functions. Wrap the query in a CTE or subquery and filter outside.
- `WHERE` can't use a `SELECT` alias in Postgres (`column "yearly" does not exist`). SQLite allows it as an extension; don't rely on that. `ORDER BY` can use aliases everywhere.
- Window functions only see rows that survived `WHERE`, so `ROW_NUMBER()` numbers the filtered rows.

### JOINs

| Join | Returns |
|---|---|
| `INNER JOIN` (`JOIN`) | Only rows that match on both sides |
| `LEFT JOIN` | Every left row; right-side columns are `NULL` when nothing matches |
| `RIGHT JOIN` | Every right row. It's a `LEFT JOIN` with the tables swapped; prefer `LEFT` for readability |
| `FULL OUTER JOIN` | Every row from both sides |
| `CROSS JOIN` | Every combination (m × n rows) |
| Self join | A table joined to itself (employee ↔ manager) |
| Semi-join (`EXISTS`) | Left rows that **have** a match, each returned once |
| Anti-join (`NOT EXISTS`, or `LEFT JOIN … WHERE right.id IS NULL`) | Left rows with **no** match |

```sql
-- INNER: employees with their department (Ivan has no department, so he's dropped)
SELECT e.name, d.name AS department
FROM employees e
JOIN departments d ON d.id = e.department_id
ORDER BY e.id;
-- 9 rows: Asha Engineering … Hana HR

-- LEFT: every department, including ones with no employees
SELECT d.name, COUNT(e.id) AS headcount              -- COUNT(e.id), not COUNT(*): see the NULL section
FROM departments d
LEFT JOIN employees e ON e.department_id = d.id
GROUP BY d.id, d.name
ORDER BY d.id;
-- Engineering 4 · Sales 4 · HR 1 · Legal 0

-- FULL OUTER: departments with nobody AND people with no department
SELECT d.name AS department, e.name AS employee
FROM departments d
FULL OUTER JOIN employees e ON e.department_id = d.id
WHERE d.id IS NULL OR e.id IS NULL
ORDER BY employee NULLS FIRST;        -- NULLs sort last in Postgres, first in SQLite/MySQL: be explicit
-- Legal | NULL
-- NULL  | Ivan
```

**Self join.** Join a table to itself under two aliases:

```sql
-- Employees who earn more than their manager
SELECT e.name, e.salary, m.name AS manager, m.salary AS manager_salary
FROM employees e
JOIN employees m ON m.id = e.manager_id
WHERE e.salary > m.salary;
-- Divya | 190000 | Ben | 180000
```

**Semi-joins and anti-joins:**

```sql
-- Customers who ordered at least once. EXISTS returns each customer once and stops at the first match
SELECT c.name FROM customers c
WHERE EXISTS (SELECT 1 FROM orders o WHERE o.customer_id = c.id)
ORDER BY c.id;
-- Kiran, Leela, Mohan, Omar

-- Customers who never ordered: two correct ways
SELECT c.name FROM customers c
WHERE NOT EXISTS (SELECT 1 FROM orders o WHERE o.customer_id = c.id);
-- Nisha

SELECT c.name FROM customers c
LEFT JOIN orders o ON o.customer_id = c.id
WHERE o.id IS NULL;
-- Nisha
```

**Fan-out.** Joining to a "many" table gives one row per child row, so counts and sums quietly multiply:

```sql
-- "How many Mumbai customers have ordered?"
-- ❌ One row per ORDER, so this counts orders
SELECT COUNT(*) FROM customers c JOIN orders o ON o.customer_id = c.id WHERE c.city = 'Mumbai';
-- 5

-- ✅ Count customers
SELECT COUNT(*) FROM customers c
WHERE c.city = 'Mumbai' AND EXISTS (SELECT 1 FROM orders o WHERE o.customer_id = c.id);
-- 2
```

Joining two different child tables at once (orders **and** payments) multiplies them together, so each `SUM` gets inflated. Aggregate each child table in its own CTE, then join the totals.

**The LEFT JOIN that became an INNER JOIN** (a very common real bug):

```sql
-- Goal: every department with its number of employees earning > 100000
-- ❌ WHERE runs after the join and throws away the NULL rows, so HR and Legal vanish
SELECT d.name, COUNT(e.id) AS high_earners
FROM departments d
LEFT JOIN employees e ON e.department_id = d.id
WHERE e.salary > 100000
GROUP BY d.id, d.name
ORDER BY d.id;
-- Engineering 4 · Sales 1

-- ✅ Conditions on the RIGHT table go in ON; conditions on the LEFT table go in WHERE
SELECT d.name, COUNT(e.id) AS high_earners
FROM departments d
LEFT JOIN employees e ON e.department_id = d.id AND e.salary > 100000
GROUP BY d.id, d.name
ORDER BY d.id;
-- Engineering 4 · Sales 1 · HR 0 · Legal 0
```

### NULL and three-valued logic

- `NULL = NULL` is `NULL` ("unknown"), not true. Use `IS NULL` / `IS NOT NULL`, or `IS DISTINCT FROM` for a NULL-safe `<>` (SQLite 3.39+ supports it too).
- `WHERE` keeps only rows where the condition is **true**. Rows where it's unknown are dropped.
- `COUNT(*)` counts rows. `COUNT(col)` counts non-NULL values. `SUM`/`AVG`/`MIN`/`MAX` ignore NULLs.
- `SUM` over zero rows returns `NULL`, not 0. Use `COALESCE(SUM(x), 0)`.
- Any arithmetic or concatenation with `NULL` gives `NULL`: `'Hi ' || NULL` is `NULL`.

```sql
SELECT COUNT(*) AS all_rows, COUNT(city) AS with_city, COUNT(DISTINCT city) AS distinct_cities
FROM customers;
-- 5 | 4 | 3

SELECT COALESCE(SUM(total), 0) AS revenue FROM orders WHERE customer_id = 4;
-- 0 (SUM alone would return NULL)
```

**The `NOT IN` trap** (a favourite interview question):

```sql
-- Departments with no employees
-- ❌ Returns NOTHING. The subquery contains NULL (Ivan's department_id), and
--    "4 NOT IN (1, 2, 3, NULL)" means "4 <> 1 AND … AND 4 <> NULL", which is unknown, not true
SELECT name FROM departments
WHERE id NOT IN (SELECT department_id FROM employees);

-- ✅ NOT EXISTS is NULL-safe (and usually at least as fast)
SELECT name FROM departments d
WHERE NOT EXISTS (SELECT 1 FROM employees e WHERE e.department_id = d.id);
-- Legal
```

`IN` has no such problem; only `NOT IN` breaks when the list contains a NULL.

### Aggregation: GROUP BY, HAVING, conditional aggregates

```sql
-- Paid revenue per customer, only customers above 100000
SELECT c.name, SUM(o.total) AS paid_total, COUNT(*) AS paid_orders
FROM customers c
JOIN orders o ON o.customer_id = c.id
WHERE o.status = 'paid'                -- filters ROWS, before grouping
GROUP BY c.id, c.name
HAVING SUM(o.total) > 100000           -- filters GROUPS, after grouping
ORDER BY paid_total DESC;
-- Mohan | 130000 | 2
```

Every column in `SELECT` must either be aggregated or appear in `GROUP BY`. Postgres lets you skip columns that depend on a grouped primary key (`GROUP BY c.id` covers `c.name`). SQLite, and MySQL with `ONLY_FULL_GROUP_BY` off, silently return a value from an arbitrary row instead of raising an error, which is a real source of bugs.

**Conditional aggregation** turns rows into columns (a pivot):

```sql
SELECT c.name,
  COUNT(*) FILTER (WHERE o.status = 'paid')                     AS paid,
  COUNT(*) FILTER (WHERE o.status = 'cancelled')                AS cancelled,
  SUM(CASE WHEN o.status = 'refunded' THEN o.total ELSE 0 END)  AS refunded_amount   -- portable form (MySQL has no FILTER)
FROM customers c
JOIN orders o ON o.customer_id = c.id
GROUP BY c.id, c.name
ORDER BY c.id;
-- Kiran | 2 | 0 | 10000
-- Leela | 2 | 1 | 0
-- Mohan | 2 | 0 | 0
-- Omar  | 1 | 0 | 0
```

**Grouping by month.** Date functions are where SQL dialects differ most:

```sql
-- PostgreSQL
SELECT date_trunc('month', order_date)::date AS month, SUM(total) AS revenue
FROM orders WHERE status = 'paid'
GROUP BY 1 ORDER BY 1;
-- 2026-01-01 | 80000
-- 2026-02-01 | 110000
-- 2026-03-01 | 130000
```

```sql
-- SQLite (dates are stored as TEXT 'YYYY-MM-DD')
SELECT strftime('%Y-%m-01', order_date) AS month, SUM(total) AS revenue
FROM orders WHERE status = 'paid'
GROUP BY 1 ORDER BY 1;
-- same result
```

**Integer division:** `SELECT 7 / 2` returns `3` in Postgres and SQLite. For a decimal result write `7 * 1.0 / 2` or `7 / 2.0`, which is why the percentage queries below multiply by `100.0`, not `100`.

### Subqueries

```sql
-- Scalar subquery: employees paid above the company average (128000)
SELECT name, salary FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees)
ORDER BY salary DESC;
-- Asha 250000 · Divya 190000 · Ben 180000 · Eli 150000

-- Correlated subquery: re-evaluated for each outer row. Employees above THEIR department's average
SELECT e.name, e.department_id, e.salary
FROM employees e
WHERE e.salary > (SELECT AVG(x.salary) FROM employees x WHERE x.department_id = e.department_id)
ORDER BY e.id;
-- Asha 1 250000 · Divya 1 190000 · Eli 2 150000
```

Which to use when:

- **`EXISTS` / `NOT EXISTS`**: "is there a matching row?" It's NULL-safe and stops at the first match.
- **`IN (subquery)`**: fine for "matches any of". Avoid `NOT IN` with a nullable column.
- **`JOIN`**: when you need columns from the other table. Watch for fan-out.
- **Correlated subqueries**: easy to read. Modern planners often turn them into joins, but check `EXPLAIN` on big tables; a window function (`AVG(salary) OVER (PARTITION BY department_id)`) is often faster.

### CTEs (`WITH`)

A CTE names each step of a query, so you can read it top to bottom:

```sql
WITH paid AS (
  SELECT customer_id, SUM(total) AS spent
  FROM orders WHERE status = 'paid'
  GROUP BY customer_id
),
shares AS (
  SELECT customer_id, spent, spent * 100.0 / (SELECT SUM(spent) FROM paid) AS pct
  FROM paid
)
SELECT c.name, s.spent, ROUND(s.pct, 1) AS pct_of_revenue
FROM shares s
JOIN customers c ON c.id = s.customer_id
ORDER BY s.spent DESC;
-- Mohan | 130000 | 40.6
-- Leela |  85000 | 26.6
-- Kiran |  80000 | 25.0
-- Omar  |  25000 | 7.8
```

**Recursive CTEs** walk hierarchies such as org charts, category trees, comment threads and bills of materials:

```sql
WITH RECURSIVE org AS (
  SELECT id, name, 0 AS level, name AS path              -- anchor: where to start
  FROM employees WHERE manager_id IS NULL
  UNION ALL
  SELECT e.id, e.name, o.level + 1, o.path || ' > ' || e.name     -- step: children of rows found so far
  FROM employees e
  JOIN org o ON e.manager_id = o.id
  WHERE o.level < 20                                     -- depth guard: bad data with a cycle can't loop forever
)
SELECT level, path FROM org ORDER BY path;
-- 0 | Asha
-- 1 | Asha > Ben
-- 2 | Asha > Ben > Chen
-- 2 | Asha > Ben > Divya
-- 1 | Asha > Eli
-- 2 | Asha > Eli > Farah
-- 2 | Asha > Eli > Gopal
-- 2 | Asha > Eli > Jay
-- 1 | Asha > Hana
-- 1 | Asha > Ivan
```

**Filling gaps in a report.** A dashboard needs a row for every day, including days with no sales:

```sql
-- PostgreSQL: generate_series makes the calendar
SELECT d::date AS day, COALESCE(SUM(o.total), 0) AS revenue
FROM generate_series(DATE '2026-03-01', DATE '2026-03-05', INTERVAL '1 day') AS d
LEFT JOIN orders o ON o.order_date = d::date AND o.status = 'paid'
GROUP BY d
ORDER BY d;
-- 2026-03-01 | 0
-- 2026-03-02 | 90000
-- 2026-03-03 | 0
-- 2026-03-04 | 0
-- 2026-03-05 | 0
```

```sql
-- SQLite: a recursive CTE makes the calendar
WITH RECURSIVE days(day) AS (
  SELECT '2026-03-01'
  UNION ALL
  SELECT date(day, '+1 day') FROM days WHERE day < '2026-03-05'
)
SELECT d.day, COALESCE(SUM(o.total), 0) AS revenue
FROM days d
LEFT JOIN orders o ON o.order_date = d.day AND o.status = 'paid'
GROUP BY d.day
ORDER BY d.day;
-- same result
```

### Window functions

`fn() OVER (PARTITION BY … ORDER BY … frame)` computes a value across related rows **without collapsing them**. `GROUP BY` turns many rows into one; a window function keeps every row and adds a column.

| Function | Typical use |
|---|---|
| `ROW_NUMBER()` | Unique numbering: dedupe, pick one row per group |
| `RANK()` / `DENSE_RANK()` | Leaderboards, Nth highest with ties |
| `LAG()` / `LEAD()` | Previous or next row: growth, gaps between events, sessions |
| `SUM/AVG/COUNT/MIN/MAX … OVER` | Running totals, moving averages, percent of total |
| `FIRST_VALUE` / `LAST_VALUE` / `NTH_VALUE` | First or last value in the window (mind the frame, below) |
| `NTILE(n)` | Buckets: quartiles, deciles |

**Ranking and ties:**

```sql
SELECT name, salary,
  ROW_NUMBER() OVER (ORDER BY salary DESC, name) AS row_num,   -- 1,2,3,4: always unique (add a tiebreaker!)
  RANK()       OVER (ORDER BY salary DESC)       AS rnk,       -- 1,2,2,4: ties share a rank, then a gap
  DENSE_RANK() OVER (ORDER BY salary DESC)       AS dense      -- 1,2,2,3: ties share a rank, no gap
FROM employees
WHERE department_id = 2
ORDER BY salary DESC, name;
-- Eli   | 150000 | 1 | 1 | 1
-- Farah |  90000 | 2 | 2 | 2
-- Gopal |  90000 | 3 | 2 | 2
-- Jay   |  60000 | 4 | 4 | 3
```

**Top N per group** (the most-asked window question):

```sql
-- Top 2 salaries in each department, ties included (so DENSE_RANK)
WITH ranked AS (
  SELECT d.name AS department, e.name, e.salary,
         DENSE_RANK() OVER (PARTITION BY e.department_id ORDER BY e.salary DESC) AS rnk
  FROM employees e
  JOIN departments d ON d.id = e.department_id
)
SELECT department, name, salary
FROM ranked
WHERE rnk <= 2                  -- filter in the outer query: WHERE can't see window functions
ORDER BY department, rnk, name;
-- Engineering | Asha  | 250000
-- Engineering | Divya | 190000
-- HR          | Hana  |  80000
-- Sales       | Eli   | 150000
-- Sales       | Farah |  90000
-- Sales       | Gopal |  90000
```

Use `ROW_NUMBER()` instead when you need **exactly** N rows per group.

**Running totals, previous row and growth:**

```sql
WITH monthly AS (
  SELECT substr(CAST(order_date AS TEXT), 1, 7) AS month,       -- 'YYYY-MM' (portable; in Postgres prefer date_trunc)
         SUM(total) AS revenue
  FROM orders WHERE status = 'paid'
  GROUP BY 1
)
SELECT month, revenue,
  SUM(revenue) OVER (ORDER BY month) AS running_total,
  LAG(revenue) OVER (ORDER BY month) AS prev_month,
  ROUND((revenue - LAG(revenue) OVER (ORDER BY month)) * 100.0
        / NULLIF(LAG(revenue) OVER (ORDER BY month), 0), 1) AS growth_pct    -- NULLIF: no division-by-zero error
FROM monthly
ORDER BY month;
-- 2026-01 |  80000 |  80000 |   NULL | NULL
-- 2026-02 | 110000 | 190000 |  80000 | 37.5
-- 2026-03 | 130000 | 320000 | 110000 | 18.2
```

`PARTITION BY` restarts the calculation for each group:

```sql
SELECT customer_id, order_date, total,
  SUM(total)   OVER (PARTITION BY customer_id ORDER BY order_date) AS customer_running_total,
  ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date) AS nth_order
FROM orders WHERE status = 'paid'
ORDER BY customer_id, order_date;
-- 1 | 2026-01-05 | 50000 |  50000 | 1
-- 1 | 2026-01-20 | 30000 |  80000 | 2
-- 2 | 2026-02-03 | 70000 |  70000 | 1
-- 2 | 2026-03-18 | 15000 |  85000 | 2
-- 3 | 2026-02-14 | 40000 |  40000 | 1
-- 3 | 2026-03-02 | 90000 | 130000 | 2
-- 5 | 2026-03-15 | 25000 |  25000 | 1
```

Compare each row with its group without a self join. An empty `OVER ()` means "all rows":

```sql
SELECT name, salary,
  MAX(salary) OVER () - salary                    AS gap_to_top,
  ROUND(salary * 100.0 / SUM(salary) OVER (), 1)  AS pct_of_payroll
FROM employees
WHERE department_id = 1
ORDER BY salary DESC;
-- Asha  | 250000 |      0 | 33.8
-- Divya | 190000 |  60000 | 25.7
-- Ben   | 180000 |  70000 | 24.3
-- Chen  | 120000 | 130000 | 16.2
```

**Frames** choose which rows the window covers, for example for a moving average:

```sql
SELECT order_date, total,
  ROUND(AVG(total) OVER (ORDER BY order_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW)) AS moving_avg_3
FROM orders WHERE status = 'paid'
ORDER BY order_date;
-- 2026-01-05 | 50000 | 50000
-- 2026-01-20 | 30000 | 40000
-- 2026-02-03 | 70000 | 50000
-- 2026-02-14 | 40000 | 46667
-- 2026-03-02 | 90000 | 66667
-- 2026-03-15 | 25000 | 51667
-- 2026-03-18 | 15000 | 43333
```

**The default-frame gotcha.** With `ORDER BY` and no frame, the frame is `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`. `RANGE` includes all **ties** of the current row, so a running total jumps at ties, and `LAST_VALUE()` returns the current row's value, not the last row's:

```sql
SELECT name, salary,
  SUM(salary) OVER (ORDER BY salary)                             AS range_sum,   -- ties added together
  SUM(salary) OVER (ORDER BY salary, name ROWS UNBOUNDED PRECEDING) AS rows_sum, -- row by row
  LAST_VALUE(salary) OVER (ORDER BY salary)                      AS last_wrong,  -- ❌ just the current salary
  LAST_VALUE(salary) OVER (ORDER BY salary
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)    AS last_right   -- ✅ whole partition
FROM employees
WHERE department_id = 2
ORDER BY salary, name;
-- Jay   |  60000 |  60000 |  60000 |  60000 | 150000
-- Farah |  90000 | 240000 | 150000 |  90000 | 150000
-- Gopal |  90000 | 240000 | 240000 |  90000 | 150000
-- Eli   | 150000 | 390000 | 390000 | 150000 | 150000
```

### Classic interview queries

**1. Second highest salary, or `NULL` if there isn't one:**

```sql
-- a) DISTINCT + OFFSET, wrapped in a scalar subquery so "no second salary" returns NULL instead of zero rows
SELECT (SELECT DISTINCT salary FROM employees ORDER BY salary DESC LIMIT 1 OFFSET 1) AS second_highest;
-- 190000

-- b) Highest salary below the maximum (works in any SQL dialect)
SELECT MAX(salary) AS second_highest FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);
-- 190000

-- c) Nth highest (here N = 3) with DENSE_RANK: the version that generalizes
SELECT DISTINCT salary FROM (
  SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk FROM employees
) t
WHERE rnk = 3;
-- 180000
```

**2. Highest-paid employee in each department** (keeping ties):

```sql
SELECT d.name AS department, e.name, e.salary
FROM employees e
JOIN departments d ON d.id = e.department_id
WHERE e.salary = (SELECT MAX(x.salary) FROM employees x WHERE x.department_id = e.department_id)
ORDER BY d.name;
-- Engineering | Asha | 250000
-- HR          | Hana |  80000
-- Sales       | Eli  | 150000
```

Alternatives: `RANK() … WHERE rnk = 1`, or in Postgres `SELECT DISTINCT ON (department_id) … ORDER BY department_id, salary DESC`, which returns exactly one row per department.

**3. Find and delete duplicates**, keeping the oldest row:

```sql
CREATE TABLE subscribers (id INTEGER PRIMARY KEY, email TEXT NOT NULL);
INSERT INTO subscribers VALUES (1, 'a@x.com'), (2, 'B@x.com'), (3, 'A@X.com'), (4, 'c@x.com'), (5, 'b@x.com');

-- Find: emails that appear more than once (case-insensitive)
SELECT lower(email) AS email, COUNT(*) AS copies
FROM subscribers
GROUP BY lower(email)
HAVING COUNT(*) > 1
ORDER BY 1;
-- a@x.com | 2
-- b@x.com | 2

-- Delete: everything except the lowest id in each group
DELETE FROM subscribers
WHERE id IN (
  SELECT id FROM (
    SELECT id, ROW_NUMBER() OVER (PARTITION BY lower(email) ORDER BY id) AS rn
    FROM subscribers
  ) t
  WHERE rn > 1
);

SELECT id, email FROM subscribers ORDER BY id;
-- 1 | a@x.com
-- 2 | B@x.com
-- 4 | c@x.com

-- Then make sure it can't happen again
CREATE UNIQUE INDEX subscribers_email_unique ON subscribers (lower(email));
```

**4. Consecutive days (gaps and islands).** Find every login streak. The trick: `date - row_number` is the same for every day in an unbroken run.

```sql
-- PostgreSQL
WITH days AS (SELECT DISTINCT user_id, login_date FROM logins),
islands AS (
  SELECT user_id, login_date,
         login_date - CAST(ROW_NUMBER() OVER (PARTITION BY user_id ORDER BY login_date) AS INTEGER) AS grp
  FROM days
)
SELECT user_id, MIN(login_date) AS streak_start, MAX(login_date) AS streak_end, COUNT(*) AS days
FROM islands
GROUP BY user_id, grp
ORDER BY user_id, streak_start;
-- 1 | 2026-03-01 | 2026-03-03 | 3
-- 1 | 2026-03-05 | 2026-03-06 | 2
-- 2 | 2026-03-01 | 2026-03-01 | 1
-- 2 | 2026-03-03 | 2026-03-03 | 1
```

```sql
-- SQLite: the same query, with day numbers from julianday()
WITH days AS (SELECT DISTINCT user_id, login_date FROM logins),
islands AS (
  SELECT user_id, login_date,
         julianday(login_date) - ROW_NUMBER() OVER (PARTITION BY user_id ORDER BY login_date) AS grp
  FROM days
)
SELECT user_id, MIN(login_date) AS streak_start, MAX(login_date) AS streak_end, COUNT(*) AS days
FROM islands
GROUP BY user_id, grp
ORDER BY user_id, streak_start;
-- same result
```

For the longest streak per user, wrap it: `SELECT user_id, MAX(days) … GROUP BY user_id`.

**5. Median.** Postgres has ordered-set aggregates:

```sql
-- PostgreSQL
SELECT percentile_cont(0.5) WITHIN GROUP (ORDER BY salary) AS median_salary FROM employees;
-- 105000  (average of the two middle values, 90000 and 120000)
```

**6. Keyset pagination** instead of a large `OFFSET`:

```sql
-- ❌ OFFSET 10000 reads and throws away 10,000 rows, and pages shift when new rows arrive
-- SELECT id, order_date, total FROM orders ORDER BY order_date DESC, id DESC LIMIT 20 OFFSET 10000;

-- ✅ Continue after the last row of the previous page (fast with an index on (order_date, id))
SELECT id, order_date, total FROM orders
WHERE (order_date, id) < ('2026-02-14', 5)       -- the last row the client saw
ORDER BY order_date DESC, id DESC
LIMIT 3;
-- 4 | 2026-02-03 | 70000
-- 3 | 2026-01-22 | 20000
-- 2 | 2026-01-20 | 30000
```

**7. Upsert** (insert, or update if the row exists) as one atomic statement:

```sql
CREATE TABLE stock (sku TEXT PRIMARY KEY, qty INTEGER NOT NULL);
INSERT INTO stock VALUES ('PH-1', 5);

INSERT INTO stock (sku, qty) VALUES ('PH-1', 3), ('TB-2', 7)
ON CONFLICT (sku) DO UPDATE SET qty = stock.qty + EXCLUDED.qty;   -- EXCLUDED = the row you tried to insert

SELECT sku, qty FROM stock ORDER BY sku;
-- PH-1 | 8
-- TB-2 | 7
```

### Reading query plans (`EXPLAIN`)

**SQLite:** `EXPLAIN QUERY PLAN` shows whether each table is scanned in full (`SCAN`) or searched through an index (`SEARCH`):

```sql
-- SQLite
EXPLAIN QUERY PLAN SELECT * FROM orders WHERE customer_id = 2;
-- SCAN orders                                        ← reads every row

CREATE INDEX idx_orders_customer_date ON orders (customer_id, order_date);

EXPLAIN QUERY PLAN SELECT * FROM orders WHERE customer_id = 2;
-- SEARCH orders USING INDEX idx_orders_customer_date (customer_id=?)

EXPLAIN QUERY PLAN SELECT * FROM orders WHERE order_date = '2026-02-03';
-- SCAN orders                                        ← order_date isn't the index's LEFTMOST column

EXPLAIN QUERY PLAN SELECT customer_id, order_date FROM orders WHERE customer_id = 2 ORDER BY order_date;
-- SEARCH orders USING COVERING INDEX idx_orders_customer_date (customer_id=?)
--                                                    ← answered from the index alone, already sorted
```

**PostgreSQL:** `EXPLAIN ANALYZE` runs the query and shows the real plan with timings. Here it is on 200,000 rows:

```sql
-- PostgreSQL
CREATE TABLE big_orders AS
SELECT g AS id, (g % 5000) + 1 AS customer_id,
       TIMESTAMPTZ '2025-01-01 00:00+00' + g * INTERVAL '1 minute' AS created_at,
       (g * 37) % 100000 AS total
FROM generate_series(1, 200000) AS g;
ANALYZE big_orders;

EXPLAIN ANALYZE SELECT * FROM big_orders WHERE customer_id = 42;
CREATE INDEX idx_big_orders_customer ON big_orders (customer_id);
EXPLAIN ANALYZE SELECT * FROM big_orders WHERE customer_id = 42;
```

```text
-- before the index (real output; timings from a laptop, yours will differ)
Seq Scan on big_orders  (cost=0.00..3780.00 rows=40 width=20) (actual time=0.005..5.612 rows=40 loops=1)
  Filter: (customer_id = 42)
  Rows Removed by Filter: 199960
Planning Time: 0.044 ms
Execution Time: 5.618 ms

-- after the index
Bitmap Heap Scan on big_orders  (cost=4.60..143.89 rows=40 width=20) (actual time=0.011..0.031 rows=40 loops=1)
  Recheck Cond: (customer_id = 42)
  Heap Blocks: exact=40
  ->  Bitmap Index Scan on idx_big_orders_customer  (cost=0.00..4.59 rows=40 width=0) (actual time=0.007..0.007 rows=40 loops=1)
        Index Cond: (customer_id = 42)
Planning Time: 0.086 ms
Execution Time: 0.037 ms
```

The index made the query about 150× faster: it read 40 rows instead of scanning 200,000.

How to read a plan:

- Read it **inside out**: the most-indented node runs first and feeds its parent.
- `cost=startup..total` is the planner's estimate in abstract units. `actual time` is in milliseconds.
- Compare the estimated `rows=` with the `actual … rows=`. If they're far apart, the statistics are stale, so run `ANALYZE`, or the planner is misjudging the data.
- A `Seq Scan` with a huge `Rows Removed by Filter` on a big table usually means a missing index.
- Scan nodes: `Seq Scan` (whole table), `Index Scan` (index, then table), `Index Only Scan` (index alone), `Bitmap Heap Scan` (collect matching pages first, then read them; used for "medium" result sizes).
- Join nodes: `Nested Loop` (good when one side is small and the other is indexed), `Hash Join` (large unsorted inputs), `Merge Join` (both inputs sorted).
- `Sort Method: external merge  Disk: …` means the sort spilled to disk, so the query needs an index that provides the order, or more `work_mem`.
- `EXPLAIN (ANALYZE, BUFFERS)` adds the pages read from cache versus from disk.
- `EXPLAIN ANALYZE` **really executes** the statement. To test an `UPDATE` or `DELETE`, wrap it in `BEGIN; … ROLLBACK;`.

**Write "sargable" conditions.** The index works only if the indexed column is left alone:

```sql
-- PostgreSQL (with an index on big_orders(created_at))
CREATE INDEX idx_big_orders_created ON big_orders (created_at);

-- ❌ The cast runs on every row, so the index on created_at can't be used
EXPLAIN SELECT count(*) FROM big_orders WHERE created_at::date = DATE '2025-03-01';
-- Parallel Seq Scan on big_orders
--   Filter: ((created_at)::date = '2025-03-01'::date)

-- ✅ Compare the raw column with a half-open range [start, end)
EXPLAIN SELECT count(*) FROM big_orders
WHERE created_at >= TIMESTAMPTZ '2025-03-01 00:00+00' AND created_at < TIMESTAMPTZ '2025-03-02 00:00+00';
-- Index Only Scan using idx_big_orders_created on big_orders
--   Index Cond: ((created_at >= …) AND (created_at < …))
```

The range version is also more **correct**. For a `timestamptz`, `created_at::date` depends on the session's `TimeZone` setting, so the same row can fall on different days for different connections. For the same reason you can't fix it with an expression index: `CREATE INDEX … ((created_at::date))` fails with *functions in index expression must be marked IMMUTABLE*.

Indexing rules:

- **Leftmost prefix:** an index on `(a, b, c)` helps queries on `a`, `a, b` and `a, b, c`, but not `b` or `c` alone. Put equality columns first and range or sort columns last.
- **Functions on the column disable the index.** `WHERE lower(email) = …` needs an expression index on `(lower(email))`. For `created_at::date = …`, use a range instead.
- **`LIKE 'abc%'`** can use a B-tree index (in Postgres with a non-C collation, the index needs `text_pattern_ops`). **`LIKE '%abc'`** can't; use `pg_trgm` trigram indexes or full-text search (Section 34).
- **Low-selectivity columns** (booleans, a status with 3 values) rarely help on their own. Use a **partial index** instead: `CREATE INDEX … ON jobs (created_at) WHERE status = 'pending'`.
- **Covering indexes** (`CREATE INDEX … (customer_id) INCLUDE (total)`) allow an `Index Only Scan`.
- **Index your foreign keys.** Postgres doesn't do it automatically, and joins and `ON DELETE CASCADE` need them.
- Every index slows down writes and uses disk. Find unused ones with `pg_stat_user_indexes` (`idx_scan = 0`).
- On tiny tables the planner correctly prefers a `Seq Scan`, so test plans with realistic data volumes.

### Concurrency: isolation levels, lost updates & locking

Two requests that read and then write the same row at the same time can silently overwrite each other. Isolation levels define which anomalies the database prevents:

| Anomaly | What happens |
|---|---|
| Dirty read | You read another transaction's **uncommitted** changes |
| Non-repeatable read | You read the same row twice and get different values |
| Phantom read | You run the same query twice and new rows appear |
| **Lost update** | Two read-modify-write cycles run at once, and the second write overwrites the first |
| Write skew | Two transactions read the same data, update **different** rows, and together break a rule (e.g. both on-call doctors go off call) |

| Level (Postgres) | Prevents | Notes |
|---|---|---|
| Read committed (**Postgres default**) | Dirty reads | Each **statement** sees the latest committed data |
| Repeatable read | + non-repeatable reads, phantoms, lost updates | The whole transaction sees one snapshot. A concurrent update to the same row fails with `40001` |
| Serializable | + write skew | Behaves as if transactions ran one at a time. Can fail with `40001`, so **retry** |

Postgres treats read uncommitted as read committed. MySQL/InnoDB defaults to repeatable read.

**The lost-update bug.** Two withdrawals of 30 from a balance of 100 should leave 40:

```js
// ❌ Read-modify-write in application code. Both requests read 100, both write 70: one withdrawal is lost
const { rows } = await pool.query("SELECT balance FROM accounts WHERE id = $1", [id]);
await pool.query("UPDATE accounts SET balance = $1 WHERE id = $2", [rows[0].balance - amount, id]);
```

There are four fixes, from simplest to most general.

**1. Atomic conditional update.** Let the database do the math. This is the best fix when the logic fits in one statement:

```sql
UPDATE accounts SET balance = balance - 30
WHERE id = 1 AND balance >= 30;       -- check the affected row count: 0 means "insufficient funds"
```

**2. Pessimistic locking** with `SELECT … FOR UPDATE`. Other transactions trying to lock the same row wait until you commit:

```js
await withTransaction(pool, async (client) => {
  const { rows } = await client.query("SELECT balance FROM accounts WHERE id = $1 FOR UPDATE", [id]);
  if (rows[0].balance < amount) throw new Error("Insufficient funds");
  await client.query("UPDATE accounts SET balance = balance - $1 WHERE id = $2", [amount, id]);
});
```

**3. Optimistic locking** with a version column. Nobody waits; a conflicting save fails and you tell the user. This suits edit forms, where a person may take minutes between reading and saving:

```sql
-- The client sends back the version it loaded
UPDATE documents SET body = 'new text', version = version + 1
WHERE id = 7 AND version = 3;
-- 1 row updated → saved. 0 rows → someone else saved first → respond 409 Conflict
```

**4. Serializable (or repeatable read) plus retry.** The database detects the conflict and aborts one transaction with SQLSTATE `40001`. Your code retries the whole transaction:

```js
const LEVELS = new Set(["READ COMMITTED", "REPEATABLE READ", "SERIALIZABLE"]);

// Runs fn(client) in a transaction on ONE pooled connection; retries serialization failures and deadlocks
export async function withTransaction(pool, fn, { isolation = "READ COMMITTED", retries = 3 } = {}) {
  if (!LEVELS.has(isolation)) throw new Error(`Invalid isolation level: ${isolation}`);   // it's interpolated below
  for (let attempt = 1; ; attempt++) {
    const client = await pool.connect();
    let broken = false;
    try {
      await client.query(`BEGIN ISOLATION LEVEL ${isolation}`);
      const result = await fn(client);
      await client.query("COMMIT");
      return result;
    } catch (err) {
      await client.query("ROLLBACK").catch(() => { broken = true; });
      const retryable = err.code === "40001" || err.code === "40P01";   // serialization failure, deadlock
      if (!retryable || attempt >= retries) throw err;
      await new Promise((resolve) => setTimeout(resolve, 2 ** attempt * 10 + Math.random() * 10));   // backoff + jitter
    } finally {
      client.release(broken);            // release(true) destroys a connection that failed to roll back
    }
  }
}

// Usage
await withTransaction(pool, (client) => transfer(client, fromId, toId, amount), { isolation: "SERIALIZABLE" });
```

A transaction must run on **one** client (`pool.connect()`). `pool.query()` can send each statement over a different connection, so a `BEGIN` sent through `pool.query()` doesn't protect the statements after it. Never call external APIs inside a transaction: it holds locks while you wait on the network.

**Deadlocks.** Transaction A locks row 1 and wants row 2, while B locks row 2 and wants row 1. Postgres detects this and aborts one of them with `40P01`. To avoid it, **always lock rows in the same order** (`SELECT … WHERE id IN (…) ORDER BY id FOR UPDATE`), keep transactions short, and retry on `40P01`.

**Job queues in plain Postgres** with `SKIP LOCKED`. Each worker claims a different row, and nobody waits:

```sql
-- PostgreSQL: each worker runs this in a loop
UPDATE jobs SET status = 'running', started_at = now()
WHERE id = (
  SELECT id FROM jobs
  WHERE status = 'pending'
  ORDER BY id
  LIMIT 1
  FOR UPDATE SKIP LOCKED           -- rows locked by other workers are skipped instead of waited on
)
RETURNING id;
```

`FOR UPDATE NOWAIT` fails immediately instead of waiting, which is useful for "someone else is editing this" checks.

### Interview Qs

1. What is the difference between `WHERE` and `HAVING`? → `WHERE` filters rows before grouping; `HAVING` filters groups after aggregation.
2. My `LEFT JOIN` behaves like an `INNER JOIN`. Why? → A `WHERE` condition on the right table removes the NULL rows. Move the condition into `ON`.
3. Why can `NOT IN (subquery)` return no rows? → If the subquery returns a `NULL`, every comparison is unknown. Use `NOT EXISTS`.
4. `COUNT(*)` vs `COUNT(col)` vs `COUNT(DISTINCT col)`? → All rows vs non-NULL values vs distinct non-NULL values.
5. `ROW_NUMBER` vs `RANK` vs `DENSE_RANK`? → Unique numbers vs shared ranks with gaps vs shared ranks without gaps.
6. Write a query for the second or Nth highest salary. → `DENSE_RANK() … WHERE rnk = N`, or `MAX(salary) WHERE salary < (SELECT MAX …)`.
7. How do you get the top N rows per group? → A window function in a CTE (`PARTITION BY group ORDER BY …`), filtered in the outer query.
8. How do you find and delete duplicates? → `GROUP BY … HAVING COUNT(*) > 1`; delete where `ROW_NUMBER() OVER (PARTITION BY key ORDER BY id) > 1`; then add a unique index.
9. Why can't you use a window function in `WHERE`? → `WHERE` is evaluated before `SELECT`, where window functions are computed. Filter in an outer query.
10. What is a correlated subquery? → A subquery that references the outer row, so it logically runs once per outer row.
11. CTE vs subquery? When do you need a recursive CTE? → CTEs are named, readable steps. Recursive CTEs walk hierarchies such as trees and org charts, or generate series.
12. What are gaps and islands? → Group consecutive values by `value - ROW_NUMBER()`.
13. How do you read `EXPLAIN ANALYZE`? → Read it inside out, compare estimated and actual rows, and look for Seq Scans with many rows removed, disk sorts, and slow nested loops.
14. When is an index not used? → A function or cast on the column, a non-leftmost column of a composite index, a leading `%` wildcard, low selectivity, tiny tables, or stale statistics.
15. What are covering and partial indexes? → A covering index includes every column the query needs (Index Only Scan). A partial index covers only rows matching a `WHERE` condition.
16. Name the isolation levels and the anomalies each prevents. What is Postgres's default? → See the table; the default is read committed.
17. What is a lost update and how do you prevent it? → Concurrent read-modify-write. Prevent it with an atomic `UPDATE`, `SELECT … FOR UPDATE`, a version column, or serializable isolation plus retry.
18. What causes a deadlock and how do you avoid it? → Two transactions locking rows in opposite order. Lock in a consistent order, keep transactions short, and retry on `40P01`.
19. How do you build a job queue on Postgres? → `FOR UPDATE SKIP LOCKED`.
20. Why prefer keyset pagination over `OFFSET`? → `OFFSET` scans and discards the skipped rows, and pages shift when new rows arrive. Keyset seeks straight through the index.

---

## 34. Search with PostgreSQL: Full-Text, Fuzzy Matching & Autocomplete

Most apps need a search box long before they need Elasticsearch. PostgreSQL has a real search engine built in: stemming, ranking, phrase and boolean queries, highlighting, typo-tolerant fuzzy matching and fast autocomplete, all indexed. Every query and output below was run on PostgreSQL 16.

| Need | Tool | Index |
|---|---|---|
| Exact values: SKU, email, status | `=` | B-tree |
| Words in text, with stemming and ranking ("running shoes") | **Full-text search** (`tsvector` / `tsquery`) | GIN |
| Typos and partial words ("labtop", "iphnoe") | **Trigrams** (`pg_trgm`) | GIN (`gin_trgm_ops`) |
| Search-as-you-type ("lap ba" → "Laptop Backpack") | Prefix queries on the `simple` config | GIN |
| Facets, synonyms and typo tolerance at scale, instant search on millions of documents | A search engine (Meilisearch, Typesense, OpenSearch) | Its own |

### 1. Why `ILIKE '%…%'` isn't search

`WHERE name ILIKE '%shoe%'` has four problems:

- It can't use a normal index.
- It doesn't understand language: "shoes" doesn't match "shoe", and "running" doesn't match "run".
- It has no idea which result is most relevant.
- It fails on the smallest typo.

Full-text search and trigrams fix each of these.

### 2. Full-text search in one minute

A **`tsvector`** is a document reduced to normalised words (**lexemes**) with their positions. Stop words are removed, and words are **stemmed** to their root. A **`tsquery`** is a search expression. `@@` asks "does this document match?"

```sql
SELECT to_tsvector('english', 'The quick brown foxes jumped over the lazy dogs');
-- 'brown':3 'dog':9 'fox':4 'jump':5 'lazi':8 'quick':2      ("the", "over" dropped; foxes → fox, jumped → jump)

SELECT to_tsvector('english', 'Running shoes for runners') @@ websearch_to_tsquery('english', 'run shoe');
-- t
```

The first argument is the **text search configuration**, the language rules. PostgreSQL 16 ships 29 of them, including `english`, `hindi`, `tamil`, `nepali` and `simple`:

- `simple` only lowercases: no stemming and no stop words. Use it for names, codes and autocomplete.
- `hindi` stems (दिल्ली → दिल्ल) but has no stop-word list.

List them with `SELECT cfgname FROM pg_ts_config`.

### 3. Turning user input into a query safely

| Function | Input `"red running shoes" -leather or boots` becomes | Use for |
|---|---|---|
| `websearch_to_tsquery` | `'red' <-> 'run' <-> 'shoe' & !'leather' \| 'boot'` | **Search boxes**: Google-like syntax (`"phrase"`, `or`, `-exclude`) and **never** throws |
| `plainto_tsquery` | For `red running shoes`: `'red' & 'run' & 'shoe'` | "All of these words" |
| `phraseto_tsquery` | For `red running shoes`: `'red' <-> 'run' <-> 'shoe'` | Exact phrase, words next to each other |
| `to_tsquery` | Requires operator syntax: `'red & shoes'` | Queries **you** build (like autocomplete below). **Throws on raw user input** |

```sql
SELECT to_tsquery('english', 'red shoes');
-- ERROR:  syntax error in tsquery: "red shoes"            ← a 500 error for anyone who types two words

SELECT websearch_to_tsquery('english', 'C++ & (rust) :* !!! "unclosed');
-- 'c' & 'rust' & 'unclos'                                   ← garbage in, still a valid query
```

### 4. Schema: a generated `tsvector` column + indexes

```sql
CREATE EXTENSION IF NOT EXISTS pg_trgm;

CREATE TABLE products (
  id          bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  name        text NOT NULL,
  brand       text NOT NULL,
  description text NOT NULL DEFAULT '',
  price_paise integer NOT NULL,
  -- weights: A (name) counts more than B (brand) and C (description) when ranking
  search      tsvector GENERATED ALWAYS AS (
                setweight(to_tsvector('english', name), 'A') ||
                setweight(to_tsvector('english', brand), 'B') ||
                setweight(to_tsvector('english', description), 'C')
              ) STORED
);

CREATE INDEX products_search_idx ON products USING gin (search);                        -- full-text
CREATE INDEX products_name_trgm_idx ON products USING gin (name gin_trgm_ops);           -- fuzzy + ILIKE '%…%'
CREATE INDEX products_name_prefix_idx ON products USING gin (to_tsvector('simple', name)); -- autocomplete

INSERT INTO products (name, brand, description, price_paise) VALUES
  ('Pegasus Running Shoes',       'Nike',      'Lightweight road running shoes with responsive cushioning.', 899900),
  ('Trail Running Shoes',         'Salomon',   'Grippy trail shoes for muddy and rocky runs.',               1099900),
  ('Leather Chelsea Boots',       'Clarks',    'Classic leather boots for the office and evenings.',          749900),
  ('Gaming Laptop RTX',           'Lenovo',    'Fast laptop for gaming and video editing, 16 GB RAM.',       12499900),
  ('Ultrabook Laptop 14',         'Dell',      'Thin and light laptop with all-day battery.',                 8999900),
  ('Laptop Backpack',             'Wildcraft', 'Water-resistant backpack that fits a 15 inch laptop.',         249900),
  ('iPhone 15',                   'Apple',     'Smartphone with a 48 MP camera.',                             6990000),
  ('Galaxy S24',                  'Samsung',   'Android phone with a bright AMOLED display.',                  7499900),
  ('Noise Cancelling Headphones', 'Sony',      'Wireless headphones with adaptive noise cancelling.',         2499000),
  ('Running Watch',               'Garmin',    'GPS watch that tracks runs, pace and heart rate.',            3199900);
```

- **A generated column** is always in sync, needs no triggers, and is computed once on write instead of on every search.
- **Always pass the configuration explicitly.** The one-argument `to_tsvector(description)` depends on a server setting, so PostgreSQL refuses it in generated columns (*generation expression is not immutable*) and indexes (*functions in index expression must be marked IMMUTABLE*).
- A query only uses an **expression index** if it repeats the **same expression** (`to_tsvector('simple', name)`).
- Nullable columns need `coalesce(col, '')`: `NULL || tsvector` is `NULL`, which would make the whole row unsearchable.

### 5. Ranked search

```sql
SELECT id, name, ts_rank(search, query, 32) AS rank      -- normalisation 32 → rank / (rank + 1), a 0–1 score
FROM products, websearch_to_tsquery('english', 'running shoes') AS query
WHERE search @@ query                                     -- uses the GIN index; rank only the matches
ORDER BY rank DESC, id
LIMIT 20;
-- 1 | Pegasus Running Shoes | 0.4994
-- 2 | Trail Running Shoes   | 0.4992

SELECT id, name FROM products, websearch_to_tsquery('english', 'laptop -gaming') AS query
WHERE search @@ query ORDER BY ts_rank(search, query, 32) DESC, id;
-- 5 | Ultrabook Laptop 14
-- 6 | Laptop Backpack

SELECT id, name FROM products, websearch_to_tsquery('english', 'run') AS query
WHERE search @@ query ORDER BY ts_rank(search, query, 32) DESC, id;
-- 1 | Pegasus Running Shoes           ("run" matches running, runs: stemming)
-- 2 | Trail Running Shoes
-- 10 | Running Watch
```

Business ranking usually mixes text relevance with other signals, for example `ORDER BY ts_rank(search, query, 32) * (1 + ln(1 + sales_count)) DESC`. Keep `id` (or another unique column) as the final tie-breaker so paging is stable.

### 6. Highlighting matches, safely

`ts_headline` returns a snippet with the matched words wrapped in markers. It's **not** an HTML sanitiser. Tested on PostgreSQL 16, it drops a `<script>` tag but passes other markup through untouched:

```sql
SELECT ts_headline('english', 'shoes <img src=x onerror=alert(1)> end', websearch_to_tsquery('english', 'shoes'));
-- <b>shoes</b> <img src=x onerror=alert(1)> end            ← rendering this as HTML is an XSS hole
```

Use private markers, escape everything, then turn the markers into `<mark>`. It's also slow (it re-parses each document), so run it **only on the rows you return**:

```sql
SELECT top.id, top.name,
       ts_headline('english', top.description, query,
                   'StartSel="<<", StopSel=">>", MaxFragments=2, MaxWords=12, MinWords=4') AS snippet
FROM (
  SELECT id, name, description, ts_rank(search, q, 32) AS rank
  FROM products, websearch_to_tsquery('english', 'running shoes') AS q
  WHERE search @@ q
  ORDER BY rank DESC, id
  LIMIT 20                                       -- headline only these 20, not every match
) AS top, websearch_to_tsquery('english', 'running shoes') AS query
ORDER BY top.rank DESC, top.id;
-- 1 | Pegasus Running Shoes | Lightweight road <<running>> <<shoes>> with responsive cushioning
-- 2 | Trail Running Shoes   | Grippy trail <<shoes>> for muddy and rocky <<runs>>
```

### 7. Typos and partial words: trigrams

`pg_trgm` splits text into 3-character pieces (`show_trgm('shoe')` → `{"  s"," sh",hoe,"oe ",sho}`) and measures overlap. It powers typo tolerance **and** makes `ILIKE '%…%'` indexable:

```sql
SELECT name, word_similarity('labtop', name) FROM products ORDER BY 2 DESC, name LIMIT 3;
-- Gaming Laptop RTX   | 0.4
-- Laptop Backpack     | 0.4
-- Ultrabook Laptop 14 | 0.4
```

| Function / operator | Meaning | Default threshold |
|---|---|---|
| `similarity(a, b)`, `a % b` | Whole strings are similar | `pg_trgm.similarity_threshold` = 0.3 |
| `word_similarity(q, text)`, `q <% text` | `q` is similar to **some word or part** of `text` (best for names and titles) | `pg_trgm.word_similarity_threshold` = **0.6** |

**The defaults miss real typos.** Measured on the data above: labtop 0.40, iphnoe 0.43, headfones 0.50, samsng 0.57. All are under 0.6, so `<%` finds none of them. Lower the threshold for your app. Test it against your own data; somewhere around 0.35 catches these while unrelated names score about 0.1:

```sql
ALTER DATABASE shop SET pg_trgm.word_similarity_threshold = 0.35;   -- new connections pick it up
-- or per transaction:  SET LOCAL pg_trgm.word_similarity_threshold = 0.35;
```

Operators (`%`, `<%`) use the trigram index; function calls in `WHERE` (`word_similarity(…) > 0.35`) don't. Short words have few trigrams, so a single transposed letter ("iphnoe") costs a lot of similarity; search engines handle typos on short words better.

A trigram index also accelerates `ILIKE '%…%'`. On 200,000 rows, `ILIKE '%3b9c1%'` took **69 ms** with a sequential scan and **0.37 ms** with the `gin_trgm_ops` index. For a pattern matching a quarter of the table, the planner still (correctly) prefers a sequential scan.

### 8. Autocomplete (search-as-you-type)

Prefix queries (`lap:*`) match any word starting with `lap`. **Use the `simple` configuration.** With `english`, the typed prefix isn't stemmed the way stored words were, so partially typed words stop matching:

```sql
SELECT name FROM products WHERE to_tsvector('simple', name) @@ to_tsquery('simple', 'lap:* & ba:*');
-- Laptop Backpack
SELECT name FROM products WHERE to_tsvector('simple', name) @@ to_tsquery('simple', 'runni:*') ORDER BY name;
-- Pegasus Running Shoes · Running Watch · Trail Running Shoes
SELECT name FROM products WHERE search @@ to_tsquery('english', 'runni:*');
-- (no rows: "running" is stored as the stem 'run', which doesn't start with "runni")
```

### 9. The Node service

```js
// search/products.js
const START = "\u0002";                     // private markers: never in real text, so escaping is simple
const STOP = "\u0003";
const HEADLINE_OPTIONS = `StartSel="${START}", StopSel="${STOP}", MaxFragments=2, MaxWords=15, MinWords=5`;

export async function searchProducts(pool, rawQuery, { limit = 20 } = {}) {
  const q = String(rawQuery ?? "").trim().slice(0, 200);
  if (q.length < 2) return { mode: "empty", results: [] };

  const fullText = await pool.query(
    `SELECT top.id, top.name, top.brand, top.price_paise,
            ts_headline('english', top.description, query, $3) AS snippet
       FROM (SELECT id, name, brand, price_paise, description, ts_rank(search, q, 32) AS rank
               FROM products, websearch_to_tsquery('english', $1) AS q
              WHERE search @@ q
              ORDER BY rank DESC, id
              LIMIT $2) AS top,
            websearch_to_tsquery('english', $1) AS query
      ORDER BY top.rank DESC, top.id`,
    [q, limit, HEADLINE_OPTIONS],
  );
  if (fullText.rowCount > 0) return { mode: "fulltext", results: fullText.rows };

  // Nothing matched: probably a typo, so fall back to fuzzy matching on names and brands
  const fuzzy = await pool.query(
    `SELECT id, name, brand, price_paise, NULL AS snippet,
            greatest(word_similarity($1, name), word_similarity($1, brand)) AS score
       FROM products
      WHERE $1 <% name OR $1 <% brand
      ORDER BY score DESC, id
      LIMIT $2`,
    [q, limit],
  );
  return { mode: fuzzy.rowCount > 0 ? "fuzzy" : "none", results: fuzzy.rows };
}

// "lap ba" → "lap:* & ba:*". Letters, combining marks and digits only, so the query can never be invalid syntax
export function toPrefixQuery(input) {
  const words = String(input ?? "").toLowerCase().match(/[\p{L}\p{M}\p{N}]+/gu) ?? [];   // \p{M}: Hindi vowel signs
  return words.slice(0, 5).map((w) => `${w}:*`).join(" & ");
}

export async function autocomplete(pool, rawQuery, { limit = 8 } = {}) {
  const prefixQuery = toPrefixQuery(rawQuery);
  if (prefixQuery.replace(/[^\p{L}\p{M}\p{N}]/gu, "").length < 2) return [];
  const { rows } = await pool.query(
    `SELECT id, name FROM products
      WHERE to_tsvector('simple', name) @@ to_tsquery('simple', $1)   -- same expression as the index
      ORDER BY length(name), name
      LIMIT $2`,
    [prefixQuery, limit],
  );
  return rows;
}

// Escape the snippet, THEN turn the private markers into <mark> tags
const escapeHtml = (s) => s.replace(/[&<>"']/g, (c) => ({ "&": "&amp;", "<": "&lt;", ">": "&gt;", '"': "&quot;", "'": "&#39;" })[c]);
export function snippetToHtml(snippet) {
  return escapeHtml(snippet ?? "").replaceAll(START, "<mark>").replaceAll(STOP, "</mark>");
}
```

```js
// search/routes.js
import express from "express";
import { autocomplete, searchProducts, snippetToHtml } from "./products.js";

export function searchRouter(pool) {
  const router = express.Router();

  router.get("/search", async (req, res, next) => {
    try {
      const { mode, results } = await searchProducts(pool, req.query.q);
      res.json({ mode, results: results.map((r) => ({ ...r, snippet: r.snippet && snippetToHtml(r.snippet) })) });
    } catch (err) {
      next(err);
    }
  });

  router.get("/autocomplete", async (req, res, next) => {
    try {
      res.set("Cache-Control", "public, max-age=60");        // popular prefixes repeat a lot
      res.json(await autocomplete(pool, req.query.q));
    } catch (err) {
      next(err);
    }
  });

  return router;
}
```

In React, you can skip HTML strings entirely: split the raw snippet on the markers and render `<mark>` for the matched parts, as in the regex "highlight" question in `javascript.md`. On the client, **debounce** autocomplete requests (~200 ms), **abort** stale ones with `AbortController`, require 2+ characters, and support arrow-key selection (the accessible combobox in `react.md` → "Accessibility (a11y)").

### 10. Search that gets better over time

- **Log every search** with its result count, and review **zero-result** queries weekly. They show missing synonyms ("mobile" vs "phone"), missing products, and typos worth handling.
- **Facets** are `GROUP BY` counts over the matching rows (`SELECT brand, count(*) … WHERE search @@ query GROUP BY brand`). Compute them from the same query as the results.
- **Synonyms:** expand the query in code (`phone` → `phone or mobile or smartphone`), or add a thesaurus dictionary to a custom text search configuration.
- **Accents:** the `unaccent` extension (`unaccent('Crème brûlée café')` → `Creme brulee cafe`) inside a custom configuration makes "cafe" find "café".
- **Protect the endpoint:** cap query length, rate-limit it (search is expensive), set a `statement_timeout` for the search role, and cache popular queries briefly.
- **Measure:** p95 latency, zero-result rate, and click-through on the first results.

### 11. When to move to a dedicated search engine

| Signal | Stay on PostgreSQL | Consider Meilisearch / Typesense / OpenSearch |
|---|---|---|
| Data size | Up to a few million rows per searchable table | Tens of millions+, or many searchable entities |
| Typo tolerance | Trigram fallback is enough | Instant typo-tolerant search on every keystroke |
| Features | Ranking + highlights + simple facets | Rich faceting, synonyms UI, geo and vector (hybrid) search, analytics |
| Operations | One system, transactional consistency | A second system to run, plus syncing (outbox or CDC, eventual consistency) |

Start with PostgreSQL; move when measurements say so. If you do add an engine, the database stays the **source of truth**: index changes through the outbox pattern or change-data-capture, and be able to rebuild the index from scratch.

### Interview Qs

1. Why is `ILIKE '%term%'` a poor search? → No index (without trigrams), no stemming, no ranking, no typo tolerance.
2. What are `tsvector` and `tsquery`? → A normalised, stemmed list of lexemes with positions, and a boolean/phrase query over lexemes; `@@` tests a match.
3. `to_tsquery` vs `plainto_tsquery` vs `websearch_to_tsquery`? → Operator syntax (throws on bad input) vs all-words vs Google-like syntax that never throws. Use websearch for user input.
4. How do you make full-text search fast? → A stored generated `tsvector` column (or expression) with a GIN index, and only ranking the rows that matched.
5. Why must you pass the language configuration to `to_tsvector` in indexes? → The one-argument form depends on a setting, so it isn't immutable and can't be indexed.
6. How do you rank results? What do the weights do? → `ts_rank`/`ts_rank_cd` with `setweight` A–D, so title matches outrank description matches; combine with business signals.
7. Is `ts_headline` output safe to render as HTML? → No. It passes markup through. Use private markers, escape, then add `<mark>`, and only headline the returned rows.
8. How does `pg_trgm` enable typo tolerance? What's the catch? → Trigram overlap similarity with GIN-indexed operators. The default thresholds (0.3 / 0.6) often miss real typos, so tune them on real data.
9. Why does prefix autocomplete fail with the `english` config? → Stored words are stemmed ("running" → `run`) but typed prefixes aren't, so `runni:*` matches nothing. Use `simple`.
10. When would you introduce Elasticsearch, OpenSearch or Meilisearch? → Scale, instant typo-tolerant UX, rich facets or analytics, accepting the cost of a second system and sync.

---

## 35. Database Migrations & Seeding

A **migration** is a versioned, code-reviewed script that changes the database schema (create table, add column, add index) or data. Migrations are to your database what git commits are to your code.

Why:
- Every environment (your laptop, CI, staging, production, teammates) gets the **same schema**, in the **same order**.
- Changes are **reviewed, repeatable and reversible**.
- The DB records which migrations already ran (a `migrations` / `_prisma_migrations` table), so each runs **exactly once**.

**Never** change production schemas by hand or with `sync({ force: true })` / `synchronize: true` / auto-create-tables in production.

### Tools

| Tool | Stack |
|---|---|
| **Prisma Migrate** | Prisma ORM (schema file → SQL migrations) |
| **Drizzle Kit** | Drizzle ORM |
| **Knex migrations** | Knex query builder |
| **node-pg-migrate** | Plain Postgres |
| **TypeORM / Sequelize CLI** | Those ORMs |
| **migrate-mongo** | MongoDB (data/index migrations) |
| **Alembic** | Python/SQLAlchemy (see FastAPI notes) |

### Example 1 — Prisma workflow

```bash
# 1. edit prisma/schema.prisma (e.g. add `phone String?` to User)
npx prisma migrate dev --name add_user_phone   # DEV: generates SQL migration + applies it + regenerates client
# → prisma/migrations/20260924_add_user_phone/migration.sql  (commit this!)

npx prisma migrate deploy                     # CI/PROD: apply pending migrations only (never generates, never resets)
npx prisma migrate status
npx prisma db seed                            # run the seed script
```

```sql
-- prisma/migrations/20260924_add_user_phone/migration.sql
ALTER TABLE "User" ADD COLUMN "phone" TEXT;
CREATE INDEX "User_phone_idx" ON "User"("phone");
```

`migrate dev` may **reset** the dev DB when history diverges — never run it against production.

### Example 2 — Knex migration with up/down

```bash
npx knex migrate:make create_orders
npx knex migrate:latest      # apply
npx knex migrate:rollback    # undo last batch
```

```js
// migrations/20260924120000_create_orders.js
export async function up(knex) {
  await knex.schema.createTable("orders", (t) => {
    t.uuid("id").primary().defaultTo(knex.raw("gen_random_uuid()"));
    t.integer("user_id").notNullable().references("id").inTable("users").onDelete("CASCADE");
    t.integer("total_paise").notNullable();
    t.enu("status", ["pending", "paid", "shipped", "cancelled"]).notNullable().defaultTo("pending");
    t.timestamps(true, true);                   // created_at, updated_at
    t.index(["user_id", "created_at"]);
  });
}

export async function down(knex) {
  await knex.schema.dropTable("orders");
}
```

### Zero-downtime migrations: Expand → Migrate → Contract

During a deploy, **old and new versions of your app run at the same time** (rolling deploys). A migration must work with **both**.

**Renaming a column** `name` → `full_name` safely:

1. **Expand**: add `full_name` (nullable). Deploy code that **writes both** columns and reads `full_name ?? name`.
2. **Migrate**: backfill `full_name = name` for old rows (in batches).
3. Deploy code that reads/writes only `full_name`.
4. **Contract**: drop `name` in a later release.

A direct `RENAME COLUMN` would break the old app version still running → errors during the deploy.

**Adding a NOT NULL column to a big table**:

```sql
-- 1. add nullable (fast, no table rewrite)
ALTER TABLE users ADD COLUMN country TEXT;
-- 2. backfill in batches (avoid locking millions of rows at once)
UPDATE users SET country = 'IN' WHERE id BETWEEN 1 AND 10000 AND country IS NULL;   -- repeat per batch
-- 3. then enforce
ALTER TABLE users ALTER COLUMN country SET NOT NULL;
```

**Indexes on large Postgres tables**: `CREATE INDEX CONCURRENTLY` (doesn't block writes; can't run inside a transaction).

### Risky operations checklist

| Operation | Risk | Safer approach |
|---|---|---|
| Drop column/table | Old code still uses it | Stop using in code first, drop in a later release |
| Rename column/table | Breaks running app version | Expand/contract |
| Change column type | Table rewrite + lock | New column + backfill + switch |
| Add NOT NULL without default | Fails on existing rows / locks | Nullable → backfill → constraint |
| Add index on big table | Blocks writes | `CONCURRENTLY` |
| Big data update in one statement | Long locks, huge transaction | Batch it; run as a job |

### Schema migrations vs data migrations

- **Schema migration**: structure (tables, columns, indexes, constraints).
- **Data migration**: transform existing data (backfill, split a name into first/last, fix bad rows). Keep them **idempotent**, batched, and often run as a separate script/job so a slow data fix doesn't block deploys.

### Seeding

**Seed data** = initial/sample data: dev/demo data, test fixtures, or required reference data (roles, countries, plans).

```js
// prisma/seed.js — IDEMPOTENT: safe to run many times (upsert, not create)
import { PrismaClient } from "@prisma/client";
import { faker } from "@faker-js/faker";
const prisma = new PrismaClient();

async function main() {
  // Reference data (needed in every environment)
  for (const name of ["admin", "editor", "viewer"]) {
    await prisma.role.upsert({ where: { name }, update: {}, create: { name } });
  }

  // Dev-only fake data
  if (process.env.NODE_ENV !== "production") {
    faker.seed(42);                                    // deterministic → same data every run
    for (let i = 0; i < 20; i++) {
      const email = faker.internet.email().toLowerCase();
      await prisma.user.upsert({
        where: { email },
        update: {},
        create: { email, name: faker.person.fullName(), role: { connect: { name: "viewer" } } },
      });
    }
  }
}

main().finally(() => prisma.$disconnect());
```

```json
// package.json
{ "prisma": { "seed": "node prisma/seed.js" } }
```

### Migrations in CI/CD

1. PR includes the migration file → reviewed like code (check for locks, data loss, reversibility).
2. CI spins up a fresh DB, runs **all** migrations from scratch, then tests (catches broken migration history).
3. Deploy pipeline runs `migrate deploy` **once** (a dedicated job/step, not in every app instance on startup — avoids race conditions with multiple replicas), then rolls out the new app version.
4. Take backups before risky migrations; know how to roll forward (a fix migration) — in production, rolling **forward** is usually safer than rolling back.

### MongoDB "migrations"

Schemaless doesn't mean no migrations: you still need to add indexes, rename fields, backfill values. Options: `migrate-mongo` scripts, or handle both shapes in code (schema versioning field `schemaVersion: 2`) and migrate lazily on read/write.

### Interview Qs

1. What are database migrations and why use them?
2. `prisma migrate dev` vs `prisma migrate deploy`?
3. How do you rename a column with zero downtime? → Expand → migrate → contract.
4. How do you add a NOT NULL column to a table with millions of rows?
5. Schema vs data migrations?
6. What is seeding? Why should seeds be idempotent?
7. Where should migrations run in a deployment? → Once, as a pipeline step before rolling out the new version.
8. Rollback vs roll forward?

---

## 36. Data Import Pipelines: Stream CSV → Validate → Batch Insert → Report

"Upload a CSV of 200,000 products" is a classic real-world feature — and a classic way to crash a server (reading the whole file into memory, inserting row by row, or dying on row 150,000 with no idea which rows were saved).

### What a good import does

- **Streams** the file (constant memory, any size).
- **Validates every row** and reports errors **with line numbers**, instead of failing the whole file silently.
- **Inserts in batches** (hundreds/thousands of rows per query), not one query per row.
- Applies **backpressure** — reads more only when the database has caught up.
- Is **idempotent** — re-running the same file doesn't create duplicates (upsert by a natural key like SKU).
- Reports **progress** and a **summary** (inserted, updated, skipped, failed) plus a downloadable **error report**.
- Enforces **limits** (file size, row count, columns) and runs **in a background job** for big files.

```
Browser ──upload──► object storage (S3) ──► POST /imports → 202 {jobId}
                                                  │ enqueue
Worker: stream from S3 → parse CSV → validate row → batch (1,000) → upsert → progress → error report → notify
```

### 1. Parsing CSV as a stream

Use a real parser in production — CSV has quotes, escaped quotes, commas and newlines inside fields, BOMs and CRLF line endings. `csv-parse` handles all of it:

```js
import { createReadStream } from "node:fs";
import { parse } from "csv-parse";

const parser = createReadStream("products.csv").pipe(
  parse({ columns: true, bom: true, trim: true, skip_empty_lines: true, relax_column_count: false }),
);
for await (const record of parser) {
  // record = { sku: "PH-1", name: "Phone", price: "19999", … }   (strings — validate & convert next)
}
```

What a parser does, in a small tested version (useful for understanding and for interviews):

```js
// Async generator: yields { line, values } for each record. Handles quotes, "" escapes,
// commas/newlines inside quotes, CRLF and a UTF-8 BOM. Reads chunk by chunk (constant memory).
export async function* parseCsv(chunks) {
  let field = "", record = [], inQuotes = false, line = 1, recordLine = 1, first = true, pendingQuote = false;
  const endField = () => { record.push(field); field = ""; };
  for await (let chunk of chunks) {
    chunk = typeof chunk === "string" ? chunk : chunk.toString("utf8");
    if (first) { chunk = chunk.replace(/^\uFEFF/, ""); first = false; }
    for (const ch of chunk) {
      if (pendingQuote) {                       // previous char was a quote inside a quoted field
        pendingQuote = false;
        if (ch === '"') { field += '"'; continue; }   // "" → literal quote
        inQuotes = false;                            // it was the closing quote; handle ch normally below
      }
      if (inQuotes) {
        if (ch === '"') pendingQuote = true;
        else { field += ch; if (ch === "\n") line++; }
      } else if (ch === '"' && field === "") inQuotes = true;
      else if (ch === ",") endField();
      else if (ch === "\r") continue;               // CRLF → handled by \n
      else if (ch === "\n") {
        endField();
        if (!(record.length === 1 && record[0] === "")) yield { line: recordLine, values: record };   // skip blank lines
        record = []; line++; recordLine = line;
      } else field += ch;
    }
  }
  if (pendingQuote) inQuotes = false;
  if (inQuotes) throw new Error(`Unclosed quote starting on line ${recordLine}`);
  if (field !== "" || record.length) { endField(); yield { line: recordLine, values: record }; }
}
```

### 2. Validating rows (with line numbers)

```js
import { z } from "zod";

export const ProductRow = z.object({
  sku: z.string().trim().min(1, "SKU is required").max(40),
  name: z.string().trim().min(1, "Name is required").max(200),
  price: z.coerce.number({ message: "Price must be a number" }).int("Price must be whole paise").positive("Price must be > 0"),
  stock: z.coerce.number().int().min(0).default(0),
  category: z.enum(["electronics", "books", "accessories"], { message: "Unknown category" }),   // `message` works in Zod v3.23+ and v4
});

export const REQUIRED_HEADERS = ["sku", "name", "price", "stock", "category"];

export function validateHeaders(headers) {
  const normalized = headers.map((h) => h.trim().toLowerCase());
  const missing = REQUIRED_HEADERS.filter((h) => !normalized.includes(h));
  if (missing.length) throw new Error(`Missing columns: ${missing.join(", ")}`);
  return normalized;
}

export function validateRow(headers, { line, values }) {
  const raw = Object.fromEntries(headers.map((h, i) => [h, values[i] ?? ""]));
  const result = ProductRow.safeParse(raw);
  if (result.success) return { ok: true, line, data: result.data };
  return { ok: false, line, raw, errors: result.error.issues.map((i) => `${i.path.join(".")}: ${i.message}`) };
}
```

### 3. Batching with backpressure

```js
// Group any (async) iterable into arrays of `size`
export async function* batch(iterable, size) {
  let current = [];
  for await (const item of iterable) {
    current.push(item);
    if (current.length >= size) { yield current; current = []; }
  }
  if (current.length) yield current;
}
```

**Backpressure comes for free with `for await`**: the loop doesn't pull the next chunk from the file until the current batch has been written, so memory stays flat even if the database is slow.

```js
// ❌ No backpressure: every row fires a query immediately → thousands of concurrent queries,
//    exhausted connection pool, memory grows with the whole file, errors lose their line numbers
parser.on("data", (row) => db.product.create({ data: row }));

// ✅ Pull-based: one batch in flight at a time
for await (const rows of batch(validRows, 1000)) await repo.upsertMany(rows);
```

### 4. The import function

```js
export async function importProducts(chunks, repo, { batchSize = 1000, maxRows = 200_000, onProgress, signal } = {}) {
  const stats = { processed: 0, inserted: 0, updated: 0, failed: 0 };
  const errors = [];
  let headers = null;

  async function* validRows() {
    for await (const record of parseCsv(chunks)) {
      signal?.throwIfAborted();                                    // cancellable
      if (!headers) { headers = validateHeaders(record.values); continue; }
      stats.processed++;
      if (stats.processed > maxRows) throw new Error(`Too many rows (max ${maxRows})`);
      const result = validateRow(headers, record);
      if (result.ok) yield result.data;
      else {
        stats.failed++;
        if (errors.length < 10_000) errors.push({ line: result.line, errors: result.errors, raw: result.raw });   // bounded
      }
    }
  }

  for await (const rows of batch(validRows(), batchSize)) {
    const { inserted, updated } = await repo.upsertMany(rows);     // one query/transaction per batch
    stats.inserted += inserted;
    stats.updated += updated;
    onProgress?.({ ...stats });
  }
  if (!headers) throw new Error("File is empty");
  return { stats, errors };
}
```

Upsert = idempotent re-runs (same SKU → update, not duplicate):

```js
// Postgres via a query builder / raw SQL
// INSERT INTO products (sku, name, price, stock, category) VALUES … 
// ON CONFLICT (sku) DO UPDATE SET name = EXCLUDED.name, price = EXCLUDED.price, stock = EXCLUDED.stock, category = EXCLUDED.category
// RETURNING (xmax = 0) AS inserted;          -- Postgres trick: true for inserts, false for updates

// Prisma: createMany({ data: rows, skipDuplicates: true }) for insert-only imports,
// or chunked upserts inside a $transaction when you need updates.
```

### 5. The error report

Give users a CSV of the rows that failed, with reasons, so they can fix and re-upload just those.

```js
const csvCell = (v) => {
  let s = v == null ? "" : String(v);
  if (/^[=+\-@\t\r]/.test(s)) s = "'" + s;                          // neutralize spreadsheet formulas
  return /[",\n\r]/.test(s) ? `"${s.replace(/"/g, '""')}"` : s;
};

export function errorReportCsv(errors, headers) {
  const lines = [["line", ...headers, "errors"].map(csvCell).join(",")];
  for (const e of errors) lines.push([e.line, ...headers.map((h) => e.raw?.[h]), e.errors.join("; ")].map(csvCell).join(","));
  return "\uFEFF" + lines.join("\r\n");
}
```

### 6. Wiring it up

```js
// Small files: import synchronously straight from the upload stream (with a size limit)
import busboy from "busboy";

app.post("/api/imports/products", requireAdmin, (req, res, next) => {
  const bb = busboy({ headers: req.headers, limits: { files: 1, fileSize: 20 * 1024 * 1024 } });   // 20 MB
  bb.on("file", async (_name, file) => {
    file.on("limit", () => file.destroy(new Error("File too large (max 20 MB)")));
    try {
      const { stats, errors } = await importProducts(file, productRepo, { batchSize: 1000 });
      res.json({ stats, errors: errors.slice(0, 100), errorCount: errors.length });
    } catch (err) {
      next(err);
    }
  });
  req.pipe(bb);
});

// Big files: upload to S3 via pre-signed URL → POST /api/imports {key} → enqueue a BullMQ job →
// the worker streams from S3 (s3.send(new GetObjectCommand(...))).Body into importProducts,
// updates job progress, stores the error report, and notifies the user when done.
```

### 7. All-or-nothing vs partial imports

| Strategy | How | When |
|---|---|---|
| **Partial** (default) | Import valid rows, report invalid ones | Catalog/contacts uploads — users fix and re-upload failures |
| **All-or-nothing** | Validate the whole file first (dry run), then import in one transaction — or load into a **staging table** and swap/merge in one transaction | Financial data, anything where half an import is worse than none |
| **Dry run** | Validate and report without writing | Let users preview errors before committing |

### 8. Performance tips

- Batch size 500–5,000 rows; measure. Multi-row `INSERT`/`upsert` in one statement.
- Postgres: **`COPY`** into a staging table is the fastest bulk path (millions of rows/minute), then `INSERT … SELECT … ON CONFLICT`.
- For huge one-off loads: drop/disable non-essential indexes, load, then rebuild.
- Parallelize carefully: 2–4 concurrent batches with a limit, never unbounded.
- Stream from object storage directly; never buffer the whole file.
- Keep error lists bounded (store the full report as a file, not in memory).

### Security & limits

File size and row limits, allowed MIME/extension **and** content checks, required headers, per-field length limits, formula-injection-safe error reports, authorization (who may import into which tenant), rate-limit import endpoints, and audit logs (who imported what, when).

### Interview Qs

1. How would you import a 2 GB CSV without running out of memory?
2. What is backpressure? Why is `stream.on("data", row => db.insert(row))` dangerous?
3. How do you make an import idempotent?
4. How do you report validation errors to users?
5. Partial import vs all-or-nothing — how would you implement each?
6. Why batch inserts? What's the fastest way to bulk-load Postgres?
7. When should an import run as a background job?
8. What is CSV formula injection?

---

## 37. File Uploads

Use **multer** for `multipart/form-data`.

```js
import multer from "multer";
import path from "node:path";
import crypto from "node:crypto";

const storage = multer.diskStorage({
  destination: "uploads/",
  filename: (req, file, cb) => cb(null, crypto.randomUUID() + path.extname(file.originalname)),
});

const upload = multer({
  storage,
  limits: { fileSize: 5 * 1024 * 1024 }, // 5MB
  fileFilter: (req, file, cb) => {
    const ok = ["image/jpeg", "image/png", "image/webp"].includes(file.mimetype);
    cb(ok ? null : new Error("Only images allowed"), ok);
  },
});

app.post("/api/avatar", auth, upload.single("avatar"), (req, res) => {
  res.json({ url: `/uploads/${req.file.filename}`, size: req.file.size });
});
app.post("/api/gallery", upload.array("photos", 10), (req, res) => res.json(req.files.map((f) => f.filename)));
```

Production: upload to object storage (S3, R2, Cloudinary) — ideally via **pre-signed URLs** so files go directly from browser to storage without passing through your server.

```js
import { S3Client, PutObjectCommand } from "@aws-sdk/client-s3";
import { getSignedUrl } from "@aws-sdk/s3-request-presigner";
const s3 = new S3Client({ region: "ap-south-1" });

app.post("/api/upload-url", auth, async (req, res) => {
  const key = `avatars/${req.user.sub}/${crypto.randomUUID()}.png`;
  const url = await getSignedUrl(s3, new PutObjectCommand({ Bucket: "my-bucket", Key: key, ContentType: "image/png" }), { expiresIn: 60 });
  res.json({ url, key });
});
```

Security: validate type & size, never trust the original filename, store outside web root or in object storage, scan if needed.

---

## 38. Caching with Redis

**Redis** is an in-memory key-value data store — super fast. Used for caching, sessions, rate limiting, queues, pub/sub, leaderboards (sorted sets), distributed locks.

### Cache-aside pattern

```js
import { createClient } from "redis";
const redis = createClient({ url: process.env.REDIS_URL });
await redis.connect();

async function getProduct(id) {
  const key = `product:${id}`;
  const cached = await redis.get(key);
  if (cached) return JSON.parse(cached);                        // cache hit

  const product = await Product.findById(id).lean();            // cache miss -> DB
  if (product) await redis.set(key, JSON.stringify(product), { EX: 300 }); // TTL 5 min
  return product;
}

async function updateProduct(id, data) {
  const p = await Product.findByIdAndUpdate(id, data, { new: true });
  await redis.del(`product:${id}`);                             // invalidate
  return p;
}
```

### Cache middleware

```js
const cache = (ttl = 60) => async (req, res, next) => {
  const key = `cache:${req.originalUrl}`;
  const hit = await redis.get(key);
  if (hit) return res.set("X-Cache", "HIT").json(JSON.parse(hit));
  const json = res.json.bind(res);
  res.json = (body) => {
    if (res.statusCode === 200) redis.set(key, JSON.stringify(body), { EX: ttl });
    return json(body);
  };
  next();
};
app.get("/api/products", cache(120), listProducts);
```

### Other Redis data types

```js
await redis.incr("page:views");                         // counters
await redis.hSet("user:1", { name: "Rohit", age: "25" }); // hashes
await redis.lPush("queue", "job1");                     // lists
await redis.sAdd("online", "user1");                    // sets
await redis.zAdd("leaderboard", { score: 100, value: "rohit" }); // sorted sets
await redis.zRange("leaderboard", 0, 9, { REV: true });
await redis.publish("chat", "hello");                   // pub/sub
await redis.set("lock:order:1", "1", { NX: true, EX: 10 }); // simple distributed lock
```

### Caching strategies & problems

- **Cache-aside** (lazy), **write-through**, **write-behind**, **read-through**.
- Eviction: LRU, LFU, TTL.
- **Cache stampede**: many requests miss at once → use locks / request coalescing / stale-while-revalidate.
- **Cache invalidation** is hard — prefer TTLs + explicit deletes on writes.
- Other caching layers: HTTP caching (`Cache-Control`, `ETag`), CDN, in-process LRU (`lru-cache`).

---

## 39. Rate Limiting

Limit how many requests a client can make in a time window — protects against brute force, abuse and DoS.

```js
import rateLimit from "express-rate-limit";

const apiLimiter = rateLimit({
  windowMs: 15 * 60 * 1000,
  limit: 100,                    // 100 requests / 15 min / IP
  standardHeaders: "draft-7",
  legacyHeaders: false,
  message: { error: "Too many requests, try again later" },
});
const loginLimiter = rateLimit({ windowMs: 15 * 60 * 1000, limit: 5 });

app.use("/api", apiLimiter);
app.post("/auth/login", loginLimiter, login);
// multi-instance: use a Redis store so limits are shared
```

### Algorithms

- **Fixed window** — count per window; bursty at edges.
- **Sliding window log/counter** — smoother.
- **Token bucket** — tokens refill at a rate; allows bursts up to bucket size.
- **Leaky bucket** — processes at a constant rate.

```js
// Fixed-window limiter with Redis
async function isAllowed(ip, limit = 100, windowSec = 60) {
  const key = `rl:${ip}:${Math.floor(Date.now() / 1000 / windowSec)}`;
  const count = await redis.incr(key);
  if (count === 1) await redis.expire(key, windowSec);
  return count <= limit;
}
```

Behind a proxy/load balancer: `app.set("trust proxy", 1)` so `req.ip` is the real client IP.

---

## 40. Security

### OWASP-style checklist for Node APIs

1. **Injection** (SQL/NoSQL/command) — parameterized queries, ORMs, validate input, never `exec` user input.
2. **Broken auth** — hash passwords (bcrypt/argon2), rate limit login, MFA, secure cookies, short-lived tokens.
3. **Sensitive data exposure** — HTTPS everywhere, don't log secrets, `select: false` for passwords, encrypt at rest.
4. **Broken access control** — check authorization on every request, prevent IDOR.
5. **Security misconfiguration** — `helmet`, disable `X-Powered-By`, no stack traces in prod.
6. **XSS** — escape output, CSP header, sanitize HTML.
7. **CSRF** — SameSite cookies, CSRF tokens for cookie-based auth.
8. **Vulnerable dependencies** — `npm audit`, Dependabot/Renovate, lockfile, minimal deps.
9. **Insufficient logging** — log auth events, monitor.
10. **SSRF** — validate/allowlist URLs your server fetches.
11. **DoS** — body size limits, rate limiting, timeouts, avoid ReDoS (catastrophic regex backtracking: see javascript.md → Regular Expressions → ReDoS).
12. **Prototype pollution** — don't deep-merge untrusted JSON into objects; validate schemas.
13. **Secrets** — env vars / secret managers, never in git.
14. **Mass assignment** — whitelist fields instead of `Object.assign(user, req.body)`.

### NoSQL injection example

```js
// ❌ req.body = { "email": "a@b.com", "password": { "$ne": null } } bypasses the check
const user = await User.findOne({ email: req.body.email, password: req.body.password });

// ✅ validate types (zod) + compare hashes in code
```

### Mass assignment

```js
// ❌ user can send { "role": "admin" }
await User.findByIdAndUpdate(id, req.body);
// ✅ pick allowed fields
const { name, bio } = req.body;
await User.findByIdAndUpdate(id, { name, bio });
```

### Command injection

```js
import { exec, execFile } from "node:child_process";
// ❌ exec(`convert ${req.query.file} out.png`)   -> "a.png; rm -rf /"
// ✅ execFile("convert", [file, "out.png"])        -> args are not parsed by a shell
```

### helmet headers

`Content-Security-Policy`, `Strict-Transport-Security`, `X-Content-Type-Options: nosniff`, `X-Frame-Options`, `Referrer-Policy`, `Cross-Origin-*` policies.

```js
app.disable("x-powered-by");
app.use(helmet());
app.use(express.json({ limit: "100kb" }));
```

---

## 41. OWASP API Security Top 10 (2023) with Examples

The **OWASP API Security Top 10** lists the most common and damaging API vulnerabilities. Most real breaches of modern apps come from the first three — authorization bugs, not exotic hacks. (FastAPI versions: `fastapi.md` → "OWASP API Top 10 in FastAPI".)

| # | Risk | One-line summary |
|---|---|---|
| API1 | **Broken Object Level Authorization (BOLA)** | Change an ID in the URL → see someone else's data |
| API2 | **Broken Authentication** | Weak login, token or session handling |
| API3 | **Broken Object Property Level Authorization** | Responses leak fields; requests can set fields they shouldn't (mass assignment) |
| API4 | **Unrestricted Resource Consumption** | No limits on size, rate, pagination, cost |
| API5 | **Broken Function Level Authorization** | Regular users can call admin endpoints |
| API6 | **Unrestricted Access to Sensitive Business Flows** | Bots abuse a legit flow (scalping, spam signups, coupon abuse) |
| API7 | **Server-Side Request Forgery (SSRF)** | Your server fetches an attacker-chosen URL (internal services, cloud metadata) |
| API8 | **Security Misconfiguration** | Debug mode, verbose errors, open CORS, missing headers, default creds |
| API9 | **Improper Inventory Management** | Forgotten old/test API versions and undocumented endpoints |
| API10 | **Unsafe Consumption of APIs** | Blindly trusting data from third-party APIs |

### API1 — Broken Object Level Authorization (BOLA / IDOR)

The #1 API vulnerability. The endpoint checks **who** you are but not **whether this object is yours**.

```js
// ❌ any logged-in user can read ANY invoice by changing the id
app.get("/api/invoices/:id", requireAuth, async (req, res) => {
  res.json(await db.invoice.findUnique({ where: { id: req.params.id } }));
});

// ✅ scope the query to the owner (or check tenant/role explicitly)
app.get("/api/invoices/:id", requireAuth, async (req, res) => {
  const invoice = await db.invoice.findFirst({ where: { id: req.params.id, ownerId: req.user.id } });
  if (!invoice) return res.status(404).json({ error: "Not found" });     // 404, not 403 → don't reveal it exists
  res.json(toInvoiceDTO(invoice));
});
```

```js
// A reusable, testable policy
export function canAccess(user, resource, action = "read") {
  if (!user || !resource) return false;
  if (user.role === "admin") return true;
  if (resource.tenantId !== user.tenantId) return false;                 // never cross tenants
  if (action === "read") return resource.ownerId === user.id || resource.sharedWith?.includes(user.id) === true;
  return resource.ownerId === user.id;                                   // write/delete: owner only
}
```

Fixes: enforce ownership **in every data-access path** (queries filtered by owner/tenant), use random IDs (UUIDs) as defence in depth (not as the fix), and write tests that access another user's objects and expect 404/403.

### API2 — Broken Authentication

- Rate-limit and slow down login, OTP and password-reset endpoints; lock out progressively (see Advanced Authentication).
- Strong password hashing (Argon2/bcrypt), breached-password checks, MFA for sensitive accounts.
- JWTs: verify signature **and** `exp`/`iss`/`aud`, pin the algorithm (`algorithms: ["HS256"]`), short-lived access tokens, rotate refresh tokens, revoke on logout/password change.
- Don't put tokens in URLs (they end up in logs); use HttpOnly Secure cookies or the `Authorization` header.
- Same response for "unknown email" and "wrong password" (no account enumeration).

```js
// ❌ decode without verifying, or accepting whatever algorithm the token claims
const unverified = jwt.decode(token);                 // anyone can forge this
// ✅
const payload = jwt.verify(token, process.env.JWT_SECRET, { algorithms: ["HS256"], issuer: "api.myapp.com", audience: "myapp-web" });
```

### API3 — Broken Object Property Level Authorization

Two sides: **excessive data exposure** (responses include fields the caller shouldn't see) and **mass assignment** (requests set fields the caller shouldn't change).

```js
// ❌ returns the DB row: passwordHash, internal flags, other users' emails…
res.json(user);
// ❌ copies whatever the client sent: { "role": "admin", "credits": 999999, "emailVerified": true }
await db.user.update({ where: { id: req.user.id }, data: req.body });
```

```js
// ✅ explicit output DTO
export const toUserDTO = (u) => ({ id: u.id, name: u.name, avatarUrl: u.avatarUrl, createdAt: u.createdAt });

// ✅ explicit input whitelist (or a strict schema: z.object({...}).strict())
export function pickAllowed(body, allowed) {
  if (body === null || typeof body !== "object" || Array.isArray(body)) throw new TypeError("Body must be an object");
  const unknown = Object.keys(body).filter((k) => !allowed.includes(k));
  if (unknown.length) {
    const err = new Error(`Unknown or forbidden fields: ${unknown.join(", ")}`);
    err.status = 400;
    throw err;
  }
  return Object.fromEntries(allowed.filter((k) => Object.hasOwn(body, k)).map((k) => [k, body[k]]));
}

app.patch("/api/me", requireAuth, async (req, res) => {
  const data = pickAllowed(req.body, ["name", "avatarUrl", "bio"]);
  res.json(toUserDTO(await db.user.update({ where: { id: req.user.id }, data })));
});
```

Also: different DTOs per role (owner vs public vs admin), and GraphQL field-level authorization.

### API4 — Unrestricted Resource Consumption

Every request costs CPU, memory, bandwidth, DB time or **money** (SMS, email, AI, maps). Attackers (or bugs) can exhaust them.

```js
app.use(express.json({ limit: "100kb" }));                               // body size
app.use("/api", rateLimit({ windowMs: 60_000, limit: 120, store: redisStore }));   // per IP/user rate limit

// Pagination limits: clamp whatever the client asks for
export function parsePagination(query, { defaultLimit = 20, maxLimit = 100 } = {}) {
  const limit = Math.min(maxLimit, Math.max(1, Number.parseInt(query.limit, 10) || defaultLimit));
  const page = Math.max(1, Number.parseInt(query.page, 10) || 1);
  return { limit, offset: (page - 1) * limit };
}
// GET /api/products?limit=1000000  → limit 100, not a million rows
```

Also: upload size/count limits, timeouts on everything, query complexity limits (GraphQL depth/cost), limit expensive operations per user (exports, AI calls, SMS), spending caps/alerts on paid third-party APIs, and pagination on **every** list endpoint.

### API5 — Broken Function Level Authorization

Hiding the admin button in the UI isn't security — attackers call `DELETE /api/admin/users/42` directly.

```js
// ✅ deny by default: protect whole routers, not individual handlers
const admin = express.Router();
admin.use(requireAuth, requireRole("admin"));
admin.delete("/users/:id", deleteUser);
admin.post("/refunds", issueRefund);
app.use("/api/admin", admin);

// ✅ route inventory test: every registered route must declare its access level
// (e.g. fail CI if a route under /api/admin has no role middleware)
```

Watch for: HTTP-method confusion (GET is checked, PUT on the same path isn't), "hidden" internal endpoints exposed publicly, admin actions available on regular routes via a flag in the body.

### API6 — Unrestricted Access to Sensitive Business Flows

The endpoint works as designed, but **automated abuse** hurts the business: bots buying all limited stock, mass fake signups for referral credit, coupon brute-forcing, spamming reviews/comments, scraping prices.

Defences: per-account/device limits on the flow ("2 per customer"), CAPTCHA/turnstile or proof-of-work on abused flows, device fingerprinting & bot detection, delaying rewards until actions are verified (referral credit after first paid order), anomaly detection & alerts, queueing/lotteries for hot releases.

### API7 — Server-Side Request Forgery (SSRF)

Any feature that fetches a **user-provided URL** — link previews, webhooks, "import from URL", image proxies, PDF generators — can be pointed at **internal** addresses: `http://169.254.169.254/latest/meta-data/` (cloud credentials), `http://localhost:6379` (Redis), `http://10.0.0.5/admin`.

```js
import dns from "node:dns/promises";
import net from "node:net";

const blocked = new net.BlockList();
for (const [ip, prefix] of [
  ["0.0.0.0", 8], ["10.0.0.0", 8], ["100.64.0.0", 10], ["127.0.0.0", 8], ["169.254.0.0", 16],
  ["172.16.0.0", 12], ["192.0.0.0", 24], ["192.168.0.0", 16], ["198.18.0.0", 15], ["224.0.0.0", 4], ["240.0.0.0", 4],
]) blocked.addSubnet(ip, prefix, "ipv4");
for (const [ip, prefix] of [["::", 128], ["::1", 128], ["fc00::", 7], ["fe80::", 10], ["ff00::", 8]]) blocked.addSubnet(ip, prefix, "ipv6");

export function isBlockedAddress(address) {
  const family = net.isIP(address);
  if (family === 4) return blocked.check(address, "ipv4");
  if (family === 6) {
    const mapped = /^::ffff:(\d+\.\d+\.\d+\.\d+)$/i.exec(address);      // IPv4-mapped IPv6 (::ffff:127.0.0.1)
    return mapped ? blocked.check(mapped[1], "ipv4") : blocked.check(address, "ipv6");
  }
  return true;                                                          // not an IP → block
}

export async function assertSafeUrl(input, { allowedPorts = [80, 443], lookup = dns.lookup } = {}) {
  let url;
  try { url = new URL(input); } catch { throw new Error("Invalid URL"); }
  if (!["http:", "https:"].includes(url.protocol)) throw new Error("Only http(s) URLs are allowed");
  const port = Number(url.port || (url.protocol === "https:" ? 443 : 80));
  if (!allowedPorts.includes(port)) throw new Error("Port not allowed");
  if (url.username || url.password) throw new Error("Credentials in URL are not allowed");
  const host = url.hostname.replace(/^\[|\]$/g, "");                    // strip IPv6 brackets
  const addresses = net.isIP(host) ? [{ address: host }] : await lookup(host, { all: true });
  if (!addresses.length || addresses.some((a) => isBlockedAddress(a.address))) throw new Error("Destination not allowed");
  return { url, addresses };
}
```

More SSRF rules:
- **Re-check after every redirect** (`redirect: "manual"`, validate each `Location`) — an allowed host can redirect to `169.254.169.254`.
- **DNS rebinding**: the name can resolve to a public IP during the check and a private IP during the fetch — connect to the **validated IP** (custom `lookup` / agent) or use an egress proxy that enforces the rules.
- Prefer **allowlists** of domains when the use case allows it (e.g. webhooks only to customer-verified domains).
- Run URL-fetching in an isolated network segment with no access to internal services; use IMDSv2 on AWS.
- Timeouts and response-size limits on the fetch.

### API8 — Security Misconfiguration

```js
app.disable("x-powered-by");
app.use(helmet());                                                       // CSP, HSTS, nosniff, frame protection…
app.use(cors({ origin: ["https://myapp.com"], credentials: true }));     // never "*" with credentials
app.use((err, req, res, next) => {
  req.log.error({ err }, "unhandled error");
  res.status(err.status ?? 500).json({ error: err.status ? err.message : "Internal Server Error" });   // no stack traces
});
```

Checklist: `NODE_ENV=production`, no debug endpoints/dev tools in prod, TLS everywhere, secrets not in images/repos, least-privilege DB users and cloud IAM, patched dependencies and base images, directory listing off, API docs protected if private, cookies `HttpOnly; Secure; SameSite`.

### API9 — Improper Inventory Management

Old `/api/v1` (without the new auth checks), `staging.api.myapp.com` with production data, an undocumented `/debug/users` endpoint — attackers find them.

Defences: an up-to-date **inventory** of every API, version and environment (the OpenAPI spec as source of truth, generated from code); retire old versions on a schedule (Deprecation/Sunset headers); the same security controls on every version; never use real production data in non-prod without anonymization; API gateway in front of everything.

### API10 — Unsafe Consumption of APIs

Data from partner/third-party APIs is **untrusted input** too.

```js
// ✅ validate third-party responses, bound their size and time, never follow redirects blindly
const res = await fetch(partnerUrl, { signal: AbortSignal.timeout(5000), redirect: "error" });
if (!res.ok) throw new Error(`Partner API ${res.status}`);
const body = PartnerRate.parse(await res.json());                        // Zod schema — reject unexpected shapes
```

Also: TLS only, verify webhook signatures, sanitize anything you later render (stored XSS via partner data), parameterize anything you put in queries, and treat the partner as possibly compromised.

### Security testing checklist

- [ ] BOLA tests: user B requests user A's objects (read/update/delete) → 404/403
- [ ] Mass assignment tests: send `role`, `isAdmin`, `credits`, `tenantId` → rejected/ignored
- [ ] Response tests: sensitive fields never appear (`passwordHash`, tokens, internal flags)
- [ ] Function-level tests: every admin route rejects regular users
- [ ] Limits: body size, pagination max, rate limits, upload limits
- [ ] SSRF tests: localhost, private ranges, metadata IP, decimal/IPv6/mapped forms, redirects
- [ ] Automated scanners (OWASP ZAP), dependency audits, and periodic penetration tests

### Interview Qs

1. What is BOLA/IDOR and how do you prevent it systematically?
2. Excessive data exposure vs mass assignment — examples and fixes?
3. Why isn't hiding admin buttons in the UI enough?
4. What resource limits should every API have?
5. What is SSRF? Why is `169.254.169.254` special? How do DNS rebinding and redirects bypass naive checks?
6. How do old API versions become security risks?
7. Why should third-party API responses be validated?

---

## 42. Webhooks & Payment Integration

### What is a webhook?

A **webhook** is an HTTP request **another service sends to your server** when something happens ("reverse API"): Stripe/Razorpay → "payment succeeded", GitHub → "push happened", Shopify → "order created".

```
Polling:  your server → "anything new?" → provider   (every N seconds, wasteful)
Webhook:  provider → POST https://api.you.com/webhooks/stripe  → your server  (instantly, when it happens)
```

### The rules for RECEIVING webhooks

1. **Verify the signature** — anyone can POST to your URL. Providers sign the **raw body** with a shared secret (HMAC-SHA256).
2. **Use the raw body** for verification — re-serialized JSON won't match the signature.
3. **Check the timestamp** (reject old events) → prevents **replay attacks**.
4. **Respond 2xx fast** (within a few seconds) → then process asynchronously (queue). Slow responses = timeouts = the provider retries.
5. **Be idempotent** — providers deliver **at least once**: the same event can arrive twice. Store processed event IDs.
6. **Don't assume order** — `payment.succeeded` can arrive before `order.created`. Fetch the latest state from the provider API if needed.
7. **Log** every received event (ID, type, status) for debugging and replay.

### Example 1 — Generic HMAC signature verification (Express)

```js
import crypto from "node:crypto";
import express from "express";

const app = express();

// IMPORTANT: raw body for the webhook route (before any express.json() for this path)
app.post("/webhooks/provider", express.raw({ type: "application/json" }), async (req, res) => {
  const signature = req.get("X-Signature");            // e.g. "t=1727150000,v1=5257a869..."
  const { t, v1 } = Object.fromEntries(signature?.split(",").map((kv) => kv.split("=")) ?? []);

  // 1. Replay protection: reject events older than 5 minutes
  if (!t || Math.abs(Date.now() / 1000 - Number(t)) > 300) return res.status(400).send("stale");

  // 2. Recompute the signature over "timestamp.rawBody"
  const expected = crypto
    .createHmac("sha256", process.env.WEBHOOK_SECRET)
    .update(`${t}.${req.body.toString("utf8")}`)
    .digest("hex");

  // 3. Constant-time comparison (prevents timing attacks)
  const valid = v1 && v1.length === expected.length &&
    crypto.timingSafeEqual(Buffer.from(v1), Buffer.from(expected));
  if (!valid) return res.status(401).send("bad signature");

  const event = JSON.parse(req.body.toString("utf8"));

  // 4. Idempotency: insert event id with a UNIQUE constraint; duplicate → already handled
  const inserted = await db.webhookEvent.createMany({
    data: [{ id: event.id, type: event.type, payload: event, status: "received" }],
    skipDuplicates: true,
  });
  if (inserted.count === 0) return res.sendStatus(200);   // duplicate delivery — ack and ignore

  // 5. Ack fast, process in the background
  await webhookQueue.add("process", { eventId: event.id });
  res.sendStatus(200);
});
```

### Example 2 — Stripe (using the official SDK)

```js
import Stripe from "stripe";
const stripe = new Stripe(process.env.STRIPE_SECRET_KEY);

app.post("/webhooks/stripe", express.raw({ type: "application/json" }), async (req, res) => {
  let event;
  try {
    event = stripe.webhooks.constructEvent(req.body, req.get("stripe-signature"), process.env.STRIPE_WEBHOOK_SECRET);
  } catch (err) {
    return res.status(400).send(`Webhook Error: ${err.message}`);
  }

  switch (event.type) {
    case "checkout.session.completed":
    case "payment_intent.succeeded":
      await queue.add("fulfill-order", { eventId: event.id, objectId: event.data.object.id });
      break;
    case "payment_intent.payment_failed":
      await queue.add("payment-failed", { eventId: event.id });
      break;
    case "charge.refunded":
      await queue.add("refund", { eventId: event.id });
      break;
    default:
      break;                                         // ignore events you don't handle (still return 2xx)
  }
  res.json({ received: true });
});
```

Local testing: `stripe listen --forward-to localhost:3000/webhooks/stripe`, or tunnels like ngrok / Cloudflare Tunnel for other providers.

### Payment integration: the safe flow

```
1. Client: "I want to buy cart X"          → POST /api/checkout
2. Server: calculates the amount FROM THE DB (never trust a client-sent price)
           creates a pending Order + a payment order/intent with the provider (idempotency key!)
           returns the provider's order id / client secret
3. Client: opens the provider's hosted checkout / payment sheet (card data never touches your server)
4. Provider → Client: success callback (DON'T mark paid yet — the client can be faked)
   Client → Server: POST /api/payments/verify { orderId, paymentId, signature }
5. Server: verifies the payment signature / fetches payment status from the provider API
6. Provider → Server: WEBHOOK payment.captured  ← the source of truth (works even if the user closed the tab)
7. Server: marks Order paid (idempotently), sends receipt, triggers fulfilment
```

### Example 3 — Razorpay-style order creation & verification

```js
import Razorpay from "razorpay";
const razorpay = new Razorpay({ key_id: process.env.RZP_KEY_ID, key_secret: process.env.RZP_KEY_SECRET });

app.post("/api/checkout", auth, async (req, res) => {
  const cart = await getCart(req.user.id);
  const amountPaise = cart.items.reduce((s, i) => s + i.product.pricePaise * i.qty, 0); // server-side price

  const order = await db.order.create({
    data: { userId: req.user.id, amountPaise, status: "pending", items: { create: cart.items.map(toOrderItem) } },
  });

  const rzpOrder = await razorpay.orders.create({
    amount: amountPaise,             // integer paise
    currency: "INR",
    receipt: order.id,               // your order id — links provider order ↔ your order
    notes: { userId: req.user.id },
  });

  await db.order.update({ where: { id: order.id }, data: { providerOrderId: rzpOrder.id } });
  res.json({ orderId: order.id, providerOrderId: rzpOrder.id, amount: amountPaise, key: process.env.RZP_KEY_ID });
});

app.post("/api/payments/verify", auth, async (req, res) => {
  const { providerOrderId, paymentId, signature } = req.body;
  const expected = crypto
    .createHmac("sha256", process.env.RZP_KEY_SECRET)
    .update(`${providerOrderId}|${paymentId}`)
    .digest("hex");
  const ok = signature?.length === expected.length &&
    crypto.timingSafeEqual(Buffer.from(signature), Buffer.from(expected));
  if (!ok) return res.status(400).json({ error: "Payment verification failed" });

  // Mark paid only if still pending (idempotent conditional update)
  await db.order.updateMany({
    where: { providerOrderId, userId: req.user.id, status: "pending" },
    data: { status: "paid", paymentId },
  });
  res.json({ status: "paid" });
});
// ...and ALSO handle the payment.captured webhook the same idempotent way.
```

### Idempotency in payments

- **Outgoing** (you → provider): send an **Idempotency-Key** (e.g. your order ID) when creating charges, so a retried request never charges twice.
- **Incoming** (provider → you): dedupe webhook events by **event ID** (unique constraint).
- **Your own API**: accept an `Idempotency-Key` header on `POST /orders`, store key → response; replay the stored response for repeats.

```js
// Idempotency-Key middleware (simplified)
async function idempotency(req, res, next) {
  const key = req.get("Idempotency-Key");
  if (!key) return next();
  const existing = await redis.get(`idem:${req.user.id}:${key}`);
  if (existing) {
    const { status, body } = JSON.parse(existing);
    return res.status(status).json(body);                 // same response as the first time
  }
  const json = res.json.bind(res);
  res.json = (body) => {
    redis.set(`idem:${req.user.id}:${key}`, JSON.stringify({ status: res.statusCode, body }), { EX: 86400 });
    return json(body);
  };
  next();
}
```

(Production versions also lock the key while the first request is in progress, so two concurrent duplicates don't both run.)

### Payment best practices

- **Amounts as integers** in the smallest unit (paise/cents); store currency alongside.
- **Never trust the client** for price, discount, currency or "payment succeeded".
- **Webhooks are the source of truth**; client callbacks are only UX.
- **Never store card numbers** — use hosted checkout / tokenization (keeps you out of most PCI-DSS scope).
- Keep an **order state machine** (`pending → paid → shipped`, `pending → failed`, `paid → refunded`) and only allow valid transitions.
- **Reconciliation** job: periodically compare your orders with the provider's records to catch missed webhooks.
- Handle **refunds, partial refunds, disputes/chargebacks**, and **payment timeouts** (expire pending orders).
- Separate **test and live keys**; restrict dashboard access; rotate secrets.
- Log payment events with order IDs (never log full card data or secrets).

### SENDING webhooks (if your platform notifies others)

- Sign payloads (HMAC with a per-subscriber secret) and include a timestamp + event ID.
- Deliver from a **queue** with **retries + exponential backoff** (e.g. up to 24–72 hours), then mark as failed.
- Keep a **delivery log** subscribers can inspect, and allow **manual replay**.
- Short timeouts (e.g. 10s); treat non-2xx as failure.
- Support **secret rotation** (accept two secrets during rotation).
- Protect against **SSRF**: validate subscriber URLs (no internal IPs/localhost).

### Interview Qs

1. What is a webhook? Webhook vs polling?
2. How do you verify a webhook is genuine? → HMAC signature over the raw body + timestamp + constant-time compare.
3. Why do you need the raw body?
4. How do you handle duplicate webhook deliveries? → Idempotency via unique event IDs.
5. Why respond quickly and process asynchronously?
6. Walk through a secure payment flow. Why shouldn't the client send the amount?
7. Client success callback vs webhook — which is the source of truth?
8. What is an idempotency key? How would you implement one?
9. How do you avoid charging a customer twice on retries?
10. What is payment reconciliation?

---

## 43. Logging & Monitoring

`console.log` is synchronous for terminals/files and unstructured. Use a **structured logger**: **pino** (fastest) or **winston**.

```js
import pino from "pino";
import pinoHttp from "pino-http";

const logger = pino({ level: process.env.LOG_LEVEL || "info", redact: ["req.headers.authorization", "password"] });
app.use(pinoHttp({ logger }));

logger.info({ userId: 1, orderId: 99 }, "order placed");
logger.error({ err }, "payment failed");
```

Log levels: `fatal > error > warn > info > debug > trace`.

Best practices:
- JSON logs → shipped to ELK / Loki / Datadog / CloudWatch.
- Include a **request/correlation ID** to trace a request across services.
- Don't log passwords, tokens, PII.
- **Metrics** (Prometheus + Grafana): request rate, error rate, latency p95/p99, event loop lag, memory.
- **Tracing**: OpenTelemetry.
- **Error tracking**: Sentry.
- **Health checks**: `/health` (liveness), `/ready` (readiness — DB connected?).

```js
import { AsyncLocalStorage } from "node:async_hooks";
const als = new AsyncLocalStorage();
app.use((req, res, next) => {
  const requestId = req.get("x-request-id") ?? crypto.randomUUID();
  res.set("x-request-id", requestId);
  als.run({ requestId }, next); // available in any async code for this request
});
const log = (msg) => logger.info({ requestId: als.getStore()?.requestId }, msg);
```

---

## 44. Observability Hands-On: Logs, Metrics, Traces, SLOs & Alerts

**Monitoring** tells you *that* something is wrong; **observability** lets you ask *why* without shipping new code. It rests on three signals, tied together by a **trace ID**:

| Signal | Answers | Example | Tools |
|---|---|---|---|
| **Logs** | What exactly happened in this request? | `{"level":"error","msg":"payment failed","orderId":7,"traceId":"4bf9…"}` | pino → Loki / ELK / Datadog / CloudWatch |
| **Metrics** | How is the system behaving overall? Trends, alerts | `http_request_duration_seconds` p95 = 420 ms | prom-client → Prometheus → Grafana |
| **Traces** | Where did the time go across services? | API 480 ms → DB 350 ms → Redis 2 ms | OpenTelemetry → Jaeger / Tempo / Honeycomb |

(+ **error tracking** — Sentry — and **profiles** — CPU/heap flame graphs.)

### 1. What to measure

- **RED** (for every service/endpoint): **R**ate (req/s), **E**rrors (failed req/s or %), **D**uration (latency percentiles p50/p95/p99).
- **USE** (for resources): **U**tilization, **S**aturation (queue length, waiting), **E**rrors — CPU, memory, DB pool, disk.
- **Four golden signals** (Google SRE): latency, traffic, errors, saturation.
- **Node-specific**: event-loop lag, heap used, GC pauses, active handles, open sockets.
- **Business metrics**: orders/min, payment success rate, signups — often the first sign something is broken.

Use **percentiles, not averages**: an average of 100 ms can hide 5% of users waiting 3 seconds.

```js
// Why percentiles: nearest-rank percentile of latency samples
export function percentile(samples, p) {
  if (!samples.length) return NaN;
  const sorted = [...samples].sort((a, b) => a - b);
  const rank = Math.ceil((p / 100) * sorted.length);
  return sorted[Math.max(0, rank - 1)];
}
const latencies = [...Array(95).fill(100), ...Array(5).fill(3000)];   // 95 fast requests, 5 very slow
latencies.reduce((a, b) => a + b) / latencies.length;   // average 245 ms  — looks fine
percentile(latencies, 50);                              // 100 ms
percentile(latencies, 99);                              // 3000 ms — 1 in 100 users waits 3 s
```

### 2. Structured logging with pino

```js
// logger.js
import pino from "pino";

export const logger = pino({
  level: process.env.LOG_LEVEL ?? "info",
  base: { service: "orders-api", env: process.env.NODE_ENV, version: process.env.APP_VERSION },
  redact: { paths: ["req.headers.authorization", "req.headers.cookie", "*.password", "*.cardNumber"], censor: "[REDACTED]" },
  timestamp: pino.stdTimeFunctions.isoTime,
});
```

```js
// app.js — one log line per request with request ID + trace ID
import pinoHttp from "pino-http";
import { randomUUID } from "node:crypto";
import { trace } from "@opentelemetry/api";

app.use(pinoHttp({
  logger,
  genReqId: (req, res) => {
    const id = req.headers["x-request-id"] ?? randomUUID();
    res.setHeader("x-request-id", id);
    return id;
  },
  customProps: () => ({ traceId: trace.getActiveSpan()?.spanContext().traceId }),   // jump from a log line to its trace
  customLogLevel: (req, res, err) => (err || res.statusCode >= 500 ? "error" : res.statusCode >= 400 ? "warn" : "info"),
  autoLogging: { ignore: (req) => req.url === "/health" },                         // don't spam health checks
}));

// In handlers: req.log is a child logger that already carries the request ID
app.post("/orders", async (req, res) => {
  req.log.info({ itemCount: req.body.items.length }, "creating order");
  const order = await orders.create(req.body);
  req.log.info({ orderId: order.id, totalPaise: order.total }, "order created");   // business event
  res.status(201).json(order);
});
```

Logging rules: JSON to **stdout** (the platform ships it), one event per line, consistent field names (`orderId`, not sometimes `order_id`), **no secrets/PII**, `info` in production (`debug` only temporarily), log **errors with the error object** (`logger.error({ err }, "msg")`) so stack traces are captured.

### 3. Metrics with Prometheus (prom-client)

Prometheus **scrapes** a `/metrics` endpoint every ~15 s and stores time series; Grafana draws dashboards; Alertmanager sends alerts.

```js
// metrics.js
import client from "prom-client";

export const registry = new client.Registry();
client.collectDefaultMetrics({ register: registry });      // CPU, memory, event-loop lag, GC, handles…

export const httpDuration = new client.Histogram({
  name: "http_request_duration_seconds",
  help: "HTTP request latency",
  labelNames: ["method", "route", "status_class"],
  buckets: [0.01, 0.05, 0.1, 0.25, 0.5, 1, 2.5, 5],       // choose around your SLO (e.g. 0.3 s)
  registers: [registry],
});

export const ordersCreated = new client.Counter({
  name: "orders_created_total",
  help: "Orders successfully created",
  labelNames: ["payment_method"],
  registers: [registry],
});

export const queueDepth = new client.Gauge({
  name: "jobs_waiting",
  help: "Jobs waiting in the email queue",
  registers: [registry],
  async collect() { this.set(await emailQueue.getWaitingCount()); },   // computed at scrape time
});
```

```js
// middleware: RED metrics for every request
app.use((req, res, next) => {
  const end = httpDuration.startTimer();
  res.on("finish", () => {
    end({
      method: req.method,
      route: req.route?.path ?? "unmatched",               // ROUTE PATTERN (/orders/:id), never the raw URL
      status_class: `${Math.floor(res.statusCode / 100)}xx`,
    });
  });
  next();
});

// expose (protect it: internal network only, or auth)
app.get("/metrics", async (req, res) => {
  res.set("Content-Type", registry.contentType);
  res.end(await registry.metrics());
});

// business metric
ordersCreated.inc({ payment_method: "upi" });
```

**Cardinality warning**: every unique label combination is a separate time series. **Never** use user IDs, emails, order IDs or raw URLs (`/orders/123`) as labels — that creates millions of series and can take Prometheus down. Use bounded values (route pattern, status class, method).

**Metric types**: **Counter** (only goes up: requests, errors, orders), **Gauge** (up/down: queue depth, connections, memory), **Histogram** (distribution → percentiles: latency, payload size), Summary (client-side quantiles; prefer histograms).

**PromQL you'll actually use**

```promql
# Requests per second, per route
sum by (route) (rate(http_request_duration_seconds_count[5m]))

# Error ratio (5xx / all)
sum(rate(http_request_duration_seconds_count{status_class="5xx"}[5m]))
  / sum(rate(http_request_duration_seconds_count[5m]))

# p95 latency per route
histogram_quantile(0.95, sum by (le, route) (rate(http_request_duration_seconds_bucket[5m])))

# Event-loop lag p99 (from default metrics)
nodejs_eventloop_lag_p99_seconds
```

### 4. Distributed tracing with OpenTelemetry

A **trace** is the whole journey of one request; each step is a **span** (name, start/end time, attributes, status). The **trace context** travels between services in the W3C `traceparent` header, so one trace spans API → auth service → DB → queue → worker.

```js
// instrumentation.mjs — load BEFORE the app so libraries get patched
import { NodeSDK } from "@opentelemetry/sdk-node";
import { getNodeAutoInstrumentations } from "@opentelemetry/auto-instrumentations-node";
import { OTLPTraceExporter } from "@opentelemetry/exporter-trace-otlp-http";

const sdk = new NodeSDK({
  serviceName: "orders-api",
  traceExporter: new OTLPTraceExporter({ url: process.env.OTEL_EXPORTER_OTLP_ENDPOINT ?? "http://localhost:4318/v1/traces" }),
  instrumentations: [getNodeAutoInstrumentations({ "@opentelemetry/instrumentation-fs": { enabled: false } })],
});
sdk.start();
process.on("SIGTERM", () => sdk.shutdown().finally(() => process.exit(0)));   // flush spans on shutdown
```

```bash
node --import ./instrumentation.mjs src/server.js
```

Auto-instrumentation creates spans for incoming HTTP requests, Express routes, outgoing `fetch`/`http`, Postgres/MySQL/Mongo/Redis clients, and more — **no code changes**. Add **manual spans** for important business steps:

```js
import { trace, SpanStatusCode } from "@opentelemetry/api";
const tracer = trace.getTracer("orders");

export async function checkout(cart, user) {
  return tracer.startActiveSpan("checkout", async (span) => {
    span.setAttributes({ "cart.items": cart.items.length, "user.tier": user.tier });   // no PII
    try {
      const priced = await priceCart(cart);            // child spans are created automatically inside
      const payment = await chargePayment(priced);
      span.setAttribute("payment.provider", payment.provider);
      return payment;
    } catch (err) {
      span.recordException(err);
      span.setStatus({ code: SpanStatusCode.ERROR, message: err.message });
      throw err;
    } finally {
      span.end();                                     // always end spans
    }
  });
}
```

Production setup: apps send telemetry to an **OpenTelemetry Collector** (batching, sampling, redaction, fan-out to vendors), which forwards to Jaeger/Tempo/Honeycomb/Datadog. Use **sampling** (e.g. keep 10% of normal traces but 100% of errors and slow requests — tail sampling in the collector) to control cost.

### 5. Error tracking

```js
import * as Sentry from "@sentry/node";
Sentry.init({
  dsn: process.env.SENTRY_DSN,
  environment: process.env.NODE_ENV,
  release: process.env.APP_VERSION,          // group errors by deploy → "this started after v1.8.2"
  tracesSampleRate: 0.1,
});
// Express: Sentry.setupExpressErrorHandler(app) after routes; upload source maps in CI for readable stack traces
```

### 6. Health checks

| Probe | Question | Check | On failure |
|---|---|---|---|
| **Liveness** `/health` | Is the process alive (not deadlocked)? | Return 200 quickly — no dependency checks | Restart the container |
| **Readiness** `/ready` | Can it serve traffic right now? | DB/Redis reachable, warm-up done, not shutting down | Remove from the load balancer (no restart) |
| **Startup** | Has slow startup finished? | Migrations/caches loaded | Wait before liveness checks begin |

Putting dependency checks in **liveness** is a classic mistake: a DB blip restarts every pod at once.

### 7. SLOs, error budgets & alerting

- **SLI** (indicator): what you measure — e.g. "% of `/checkout` requests that succeed in < 500 ms".
- **SLO** (objective): the target — e.g. "99.9% over 30 days".
- **Error budget** = 100% − SLO = how much failure is allowed. Budget left → ship features; budget burned → focus on reliability.

```js
export function errorBudgetMinutes(slo, windowDays = 30) {
  return (1 - slo) * windowDays * 24 * 60;          // minutes of "full outage" the SLO allows
}
errorBudgetMinutes(0.999);    // 43.2 minutes / 30 days
errorBudgetMinutes(0.9999);   // 4.32 minutes / 30 days

// Burn rate: how fast you're spending the budget (1 = exactly on budget for the window)
export const burnRate = (observedErrorRatio, slo) => observedErrorRatio / (1 - slo);
burnRate(0.0144, 0.999);      // 14.4 → a 30-day budget would be gone in ~2 days
```

**Alerting rules**
- Alert on **symptoms users feel** (error rate, latency SLO burn), not on every CPU spike.
- **Multi-window burn-rate alerts**: page when burning fast (e.g. burn rate > 14.4 over 1 h *and* 5 min), ticket when burning slowly (> 1 over 3 days).
- Every alert needs an **owner** and a **runbook** (what to check, how to mitigate).
- Kill noisy alerts — alert fatigue makes people ignore the important one.

```yaml
# Prometheus alert rule (fast burn of a 99.9% availability SLO)
- alert: CheckoutErrorBudgetFastBurn
  expr: |
    (sum(rate(http_request_duration_seconds_count{route="/checkout",status_class="5xx"}[1h]))
      / sum(rate(http_request_duration_seconds_count{route="/checkout"}[1h]))) > (14.4 * 0.001)
    and
    (sum(rate(http_request_duration_seconds_count{route="/checkout",status_class="5xx"}[5m]))
      / sum(rate(http_request_duration_seconds_count{route="/checkout"}[5m]))) > (14.4 * 0.001)
  labels: { severity: page, team: payments }       # who gets paged
  annotations:
    summary: "Checkout is burning its error budget fast"
    runbook: "https://wiki.example.com/runbooks/checkout-errors"
```

### 8. The incident workflow (how the pieces connect)

1. **Alert** fires: checkout error-budget fast burn.
2. **Dashboard** (RED per route): errors started at 14:02, only `/checkout`, p95 latency jumped too.
3. **Deploy markers / release** in Sentry: v1.8.2 went out at 14:00.
4. **Traces**: slow spans are all in `POST payments-provider/orders` → provider timing out.
5. **Logs** filtered by `traceId`: `ETIMEDOUT` after 10 s, retries amplifying load.
6. **Mitigate**: roll back / feature-flag off / lower timeouts; **fix**; then a **blameless post-mortem** with action items (e.g. circuit breaker, alert on provider latency).

### Observability checklist

- [ ] Structured JSON logs with request ID + trace ID; secrets redacted
- [ ] RED metrics per route + default runtime metrics; no high-cardinality labels
- [ ] OpenTelemetry tracing (auto-instrumentation + key business spans), sampled
- [ ] Error tracking with releases & source maps
- [ ] Liveness/readiness probes done right
- [ ] Dashboards per service (RED + saturation + business KPIs)
- [ ] SLOs for critical user journeys; burn-rate alerts with runbooks
- [ ] Telemetry flushed on graceful shutdown

### Interview Qs

1. Logs vs metrics vs traces — what does each answer?
2. What are the RED and USE methods?
3. Why use percentiles instead of averages for latency?
4. What is metric cardinality and why can it break Prometheus?
5. Counter vs gauge vs histogram?
6. How does distributed tracing work across services? (spans, context propagation, `traceparent`)
7. Liveness vs readiness probes — why not check the DB in liveness?
8. SLI vs SLO vs SLA; what is an error budget? Compute the budget for 99.9% over 30 days.
9. What is a burn-rate alert and why is it better than a static error threshold?
10. Walk through how you'd investigate a production latency spike.

---

## 45. child_process

Run other programs/scripts as **separate OS processes** (separate memory, separate V8).

| Method | Shell? | Output | Use |
|---|---|---|---|
| `exec(cmd, cb)` | Yes | Buffered (maxBuffer) | Short shell commands |
| `execFile(file, args, cb)` | No | Buffered | Safer, run a binary with args |
| `spawn(cmd, args)` | No (unless `shell: true`) | **Streamed** | Long-running / large output |
| `fork(modulePath)` | No | IPC channel | Run another **Node** script, message passing |

### Example 1 — exec & execFile

```js
import { exec, execFile } from "node:child_process";
import { promisify } from "node:util";
const execP = promisify(exec);

const { stdout } = await execP("git rev-parse --short HEAD");
console.log("commit", stdout.trim());

execFile("node", ["--version"], (err, out) => console.log(out));
```

### Example 2 — spawn with streaming output

```js
import { spawn } from "node:child_process";
const ls = spawn("ls", ["-la", "/usr"]);
ls.stdout.on("data", (d) => process.stdout.write(d));
ls.stderr.on("data", (d) => process.stderr.write(d));
ls.on("close", (code) => console.log("exited with", code));

// ffmpeg example: spawn("ffmpeg", ["-i", "in.mp4", "out.webm"])
```

### Example 3 — fork with IPC

```js
// parent.js
import { fork } from "node:child_process";
const child = fork("./heavy.js");
child.send({ n: 45 });
child.on("message", (msg) => { console.log("fib:", msg.result); child.kill(); });

// heavy.js
process.on("message", ({ n }) => {
  const fib = (x) => (x < 2 ? x : fib(x - 1) + fib(x - 2));
  process.send({ result: fib(n) });
});
```

---

## 46. Worker Threads

Run JS in **parallel threads** within the same process (each has its own V8 isolate & event loop). Best for **CPU-intensive** tasks (image processing, hashing, parsing big JSON, compression). Can share memory with `SharedArrayBuffer`.

### Example 1 — offload a CPU task

```js
// main.js
import { Worker } from "node:worker_threads";

function runFib(n) {
  return new Promise((resolve, reject) => {
    const worker = new Worker(new URL("./fib-worker.js", import.meta.url), { workerData: n });
    worker.once("message", resolve);
    worker.once("error", reject);
    worker.once("exit", (code) => code !== 0 && reject(new Error(`Worker exited ${code}`)));
  });
}

app.get("/fib/:n", async (req, res) => {
  res.json({ result: await runFib(Number(req.params.n)) }); // event loop stays free
});

// fib-worker.js
import { parentPort, workerData } from "node:worker_threads";
const fib = (x) => (x < 2 ? x : fib(x - 1) + fib(x - 2));
parentPort.postMessage(fib(workerData));
```

### Example 2 — shared memory

```js
const shared = new SharedArrayBuffer(4);
const counter = new Int32Array(shared);
// pass `shared` to workers via workerData; use Atomics.add(counter, 0, 1) to avoid races
```

Creating workers is expensive → use a **pool** (`piscina`) for many tasks.

### Worker threads vs child processes vs cluster

| Worker threads | child_process | cluster |
|---|---|---|
| Threads in same process | Separate processes | Multiple processes sharing a port |
| Can share memory | No shared memory (IPC only) | No shared memory |
| Light(er) weight | Heavier | Heavier |
| CPU-bound JS tasks | Run external programs / isolation | Scale HTTP server across cores |

---

## 47. Cluster & Scaling

A single Node process uses **one CPU core** for JS. The **cluster** module forks multiple worker processes that share the same server port; the primary distributes connections (round-robin on most platforms).

```js
import cluster from "node:cluster";
import os from "node:os";
import http from "node:http";

if (cluster.isPrimary) {
  const n = os.availableParallelism();
  console.log(`Primary ${process.pid} forking ${n} workers`);
  for (let i = 0; i < n; i++) cluster.fork();
  cluster.on("exit", (worker, code) => {
    console.log(`Worker ${worker.process.pid} died (${code}), restarting`);
    cluster.fork();
  });
} else {
  http.createServer((req, res) => res.end(`handled by ${process.pid}`)).listen(3000);
}
```

In practice use **PM2** cluster mode or run multiple containers behind a load balancer:

```bash
pm2 start app.js -i max      # one process per core
pm2 reload app               # zero-downtime reload
pm2 logs / pm2 monit
```

### Scaling strategies

- **Vertical** — bigger machine.
- **Horizontal** — more instances behind a **load balancer** (Nginx, AWS ALB, k8s).
- Keep servers **stateless** — sessions in Redis, files in S3, so any instance can serve any request.
- Sticky sessions only if unavoidable (e.g. some WebSocket setups).
- Caching (Redis, CDN), DB read replicas, queues for async work, microservices.

**Interview Qs**
- How to use all CPU cores in Node? → cluster / PM2 / multiple containers; worker threads for CPU tasks.
- Why stateless servers? → Horizontal scaling and resilience.

---

## 48. WebSockets & Real-time

**HTTP** is request–response. **WebSocket** is a persistent, **full-duplex** TCP connection (starts with an HTTP `Upgrade` handshake) — server and client can push messages anytime. Used for chat, live notifications, multiplayer games, collaborative editing, live dashboards.

### ws library

```js
import { WebSocketServer } from "ws";
const wss = new WebSocketServer({ port: 8080 });

wss.on("connection", (socket, req) => {
  socket.send(JSON.stringify({ type: "welcome" }));
  socket.on("message", (raw) => {
    const msg = JSON.parse(raw);
    // broadcast to everyone
    for (const client of wss.clients) {
      if (client.readyState === 1) client.send(JSON.stringify({ type: "chat", text: msg.text }));
    }
  });
  socket.on("close", () => console.log("disconnected"));
});

// browser
const ws = new WebSocket("ws://localhost:8080");
ws.onmessage = (e) => console.log(JSON.parse(e.data));
ws.send(JSON.stringify({ text: "hi" }));
```

### Socket.IO (rooms, reconnection, fallbacks, acknowledgements)

```js
import { Server } from "socket.io";
const io = new Server(httpServer, { cors: { origin: "http://localhost:5173" } });

io.use((socket, next) => {                       // auth middleware
  try { socket.user = jwt.verify(socket.handshake.auth.token, SECRET); next(); }
  catch { next(new Error("unauthorized")); }
});

io.on("connection", (socket) => {
  socket.on("join", (roomId) => socket.join(roomId));
  socket.on("message", ({ roomId, text }, ack) => {
    io.to(roomId).emit("message", { from: socket.user.name, text }); // room broadcast
    ack?.({ ok: true });
  });
  socket.on("typing", (roomId) => socket.to(roomId).emit("typing", socket.user.name)); // everyone except sender
  socket.on("disconnect", () => {});
});
// Scale across instances with @socket.io/redis-adapter
```

### Server-Sent Events (SSE) — one-way server → client over HTTP

```js
app.get("/events", (req, res) => {
  res.set({ "Content-Type": "text/event-stream", "Cache-Control": "no-cache", Connection: "keep-alive" });
  res.flushHeaders();
  const id = setInterval(() => res.write(`data: ${JSON.stringify({ time: Date.now() })}\n\n`), 1000);
  req.on("close", () => clearInterval(id));
});
// browser: new EventSource("/events").onmessage = (e) => console.log(e.data);
```

### Comparison

| Polling | Long polling | SSE | WebSocket |
|---|---|---|---|
| Client asks every N sec | Server holds request until data | Server → client stream over HTTP | Bi-directional persistent |
| Simple, wasteful | Better, still overhead | Auto-reconnect, text only | Lowest latency, most flexible |

---

## 49. Streaming Responses & Server-Sent Events in Depth

Streaming sends a response **in pieces as they become ready**: live notifications, job progress, log tails, and, most visibly, AI chat answers appearing word by word. The previous section showed a minimal SSE endpoint. This one covers what production streaming needs: the wire format, resuming after a reconnect, heartbeats, backpressure, stopping work when the client leaves, errors after the `200` has already gone out, a streaming `POST` client for chat, and the proxy settings that silently break it all.

| Option | Direction | Good for | Limits |
|---|---|---|---|
| **SSE via `EventSource`** | Server → client | Notifications, feeds, progress | `GET` only, no custom headers; auto-reconnects and resumes with `Last-Event-ID` |
| **SSE over `fetch` streaming** | Server → client (after a request body) | **LLM chat**: `POST` a prompt with an auth header, stream the answer | You write the parser and the reconnect logic yourself |
| **WebSocket** | Both ways | Chat rooms, multiplayer, collaborative editing | A separate protocol: sticky sessions, its own auth and proxy config |
| **Long polling** | Server → client | Legacy environments | A new request per message |

SSE is plain HTTP, so it works through proxies, HTTP/2, authentication middleware and browser devtools without special handling. Choose WebSockets only when the **client** also needs to send a stream of messages.

### 1. The wire format

A response with `Content-Type: text/event-stream` is UTF-8 text. Each event is a group of `field: value` lines, ended by a **blank line**:

```text
retry: 3000                  ← the client should wait 3 s before reconnecting

: ping                       ← a comment: ignored by clients, useful as a heartbeat

event: notification          ← event type (default "message")
id: 42                       ← sent back as the Last-Event-ID header when the client reconnects
data: {"text":"Order shipped"}

data: first line             ← several data: lines join with "\n"
data: second line

```

```js
// sse/format.js: encode one event
const LINE_BREAK = /\r\n|\r|\n/;

export function formatEvent({ event, data, id, retry, comment } = {}) {
  if (event !== undefined && LINE_BREAK.test(event)) throw new Error("SSE event name must not contain line breaks");
  if (id !== undefined && /[\r\n\0]/.test(String(id))) throw new Error("SSE id must not contain line breaks or NUL");
  let out = "";
  if (comment !== undefined) for (const line of String(comment).split(LINE_BREAK)) out += `: ${line}\n`;
  if (event !== undefined) out += `event: ${event}\n`;
  if (id !== undefined) out += `id: ${id}\n`;
  if (retry !== undefined) out += `retry: ${retry}\n`;
  if (data !== undefined) {
    const text = typeof data === "string" ? data : JSON.stringify(data);
    for (const line of text.split(LINE_BREAK)) out += `data: ${line}\n`;   // a newline in data MUST become a new data: line
  }
  return `${out}\n`;
}
```

Writing raw text with an embedded newline as a single `data:` line (`res.write("data: " + text + "\n\n")`) is a classic bug. The client sees the rest of the text as unknown fields and silently drops it. If an event name or id comes from user input, a newline in it can inject fields, so the formatter rejects those.

### 2. Server: a notifications feed that survives reconnects

```js
// sse/stream.js: open a response as an event stream
import { formatEvent } from "./format.js";

export function openEventStream(res, { retryMs = 3_000, maxBufferedBytes = 1_000_000 } = {}) {
  res.writeHead(200, {
    "Content-Type": "text/event-stream; charset=utf-8",
    "Cache-Control": "no-cache, no-transform",  // no-transform: proxies and compression middleware must not buffer or alter it
    "X-Accel-Buffering": "no",                  // nginx: don't buffer this response
    Connection: "keep-alive",                   // HTTP/1.1 only (on HTTP/2, Node drops it with a warning)
  });
  res.write(formatEvent({ retry: retryMs }));

  return {
    // Send one event. A client that can't keep up is dropped; it reconnects and catches up via Last-Event-ID
    send(evt) {
      if (res.writableEnded || res.destroyed) return false;
      res.write(formatEvent(evt));
      if (res.writableLength > maxBufferedBytes) {
        res.destroy();
        return false;
      }
      return true;
    },
    // For single-consumer streams (chat): wait until the socket has room before producing more
    drained() {
      if (!res.writableNeedDrain) return Promise.resolve();
      return new Promise((resolve) => {
        const done = () => { res.off("drain", done); res.off("close", done); resolve(); };
        res.on("drain", done);
        res.on("close", done);
      });
    },
  };
}
```

```js
// sse/notifications.js
import express from "express";
import { openEventStream } from "./stream.js";

// Demo storage: an in-memory log. In production, use Redis Streams (XADD / XRANGE by id) or a table
// with an auto-increment id, plus Redis pub/sub so every server instance sees every event.
const log = [];
const clients = new Set();
let nextId = 1;

export function publish(event, data) {
  const entry = { id: String(nextId++), event, data };
  log.push(entry);
  if (log.length > 1_000) log.shift();
  for (const client of clients) client.send(entry);
}

export const notifications = express.Router();

notifications.get("/stream", (req, res) => {
  const stream = openEventStream(res);
  // The browser sends Last-Event-ID automatically when it reconnects; ?since= covers the very first connection
  const lastSeen = Number(req.get("Last-Event-ID") ?? req.query.since ?? 0) || 0;
  for (const entry of log) if (Number(entry.id) > lastSeen) stream.send(entry);   // replay what was missed
  clients.add(stream);                              // synchronous replay + add: no event can slip in between

  const heartbeat = setInterval(() => stream.send({ comment: "ping" }), 15_000);   // shorter than any proxy idle timeout
  res.on("close", () => {
    clearInterval(heartbeat);
    clients.delete(stream);
  });
});
```

Filter per user in real code (`publish(userId, …)` and a `Map` of clients per user), and authenticate the stream like any other route. A same-origin `EventSource` sends cookies, and a cross-origin one does with `{ withCredentials: true }` plus CORS credentials. `EventSource` can't set an `Authorization` header. Don't put long-lived tokens in the URL, because URLs end up in logs; use a cookie, or a short-lived single-use ticket.

### 3. Server: streaming an LLM-style answer

```js
// sse/chat.js
import express from "express";
import { setTimeout as sleep } from "node:timers/promises";
import { openEventStream } from "./stream.js";

// Stand-in for an LLM: yields tokens over time and stops when the signal aborts
export const generation = { started: 0, aborted: 0 };
async function* generateTokens(prompt, { signal }) {
  generation.started++;
  if (prompt === "fail") throw new Error("model overloaded");
  const words = `You asked: "${prompt}". Streaming sends each token as soon as it is ready.`.split(" ");
  try {
    for (const word of words) {
      await sleep(30, undefined, { signal });      // rejects as soon as the client disconnects
      yield `${word} `;
    }
  } catch (err) {
    if (signal.aborted) generation.aborted++;
    throw err;
  }
}

export const chat = express.Router();

chat.post("/", express.json({ limit: "32kb" }), async (req, res) => {
  const prompt = typeof req.body?.prompt === "string" ? req.body.prompt.trim().slice(0, 2_000) : "";
  if (!prompt) return res.status(400).json({ error: "prompt is required" });   // validate BEFORE streaming: status codes still work

  const stream = openEventStream(res);
  const upstream = new AbortController();
  res.on("close", () => upstream.abort());         // client left → stop generating (and stop paying for tokens)
  let tokens = 0;
  try {
    for await (const text of generateTokens(prompt, { signal: upstream.signal })) {
      stream.send({ event: "token", data: { text } });
      tokens++;
      await stream.drained();
    }
    stream.send({ event: "done", data: { tokens } });
  } catch (err) {
    // The 200 and headers are already sent, so errors must travel INSIDE the stream
    if (!upstream.signal.aborted) stream.send({ event: "error", data: { message: "Generation failed, please retry" } });
  } finally {
    res.end();
  }
});

// Proxying a real provider's SSE stream is the same loop over the upstream body, using the parser below:
//   const upstreamRes = await fetch(PROVIDER_URL, { method: "POST", headers, body, signal: upstream.signal });
//   for await (const evt of parseEventStream(upstreamRes.body)) stream.send({ event: "token", data: { text: pickText(evt) } });
```

```js
// sse/app.js
import express from "express";
import { chat } from "./chat.js";
import { notifications } from "./notifications.js";

export const app = express();
app.use("/api/chat", chat);
app.use("/api/notifications", notifications);
```

### 4. Client: parsing a stream from `fetch`

`EventSource` can't send a `POST` body or headers, so chat clients read the stream from `fetch` and parse it themselves. The key difficulty is that **network chunks don't line up with events**: one chunk can hold half an event, or three and a half. The parser must buffer, split on any of the three line endings the spec allows (`\r\n`, `\n`, `\r`), and dispatch on blank lines:

```js
// sse/parse.js: turn a text/event-stream body into events (browsers and Node 18+)
export async function* parseEventStream(body) {
  const reader = body.pipeThrough(new TextDecoderStream()).getReader();   // also strips a leading BOM
  let buffer = "";
  let data = [];
  let type = "";
  let retry;
  let lastEventId = "";                          // persists across events, like EventSource.lastEventId
  try {
    for (;;) {
      const { value, done } = await reader.read();
      if (done) return;                          // a final event without its blank line is discarded (per spec)
      buffer += value;
      for (;;) {
        const match = /\r\n|\n|\r/.exec(buffer);
        if (!match) break;
        if (match[0] === "\r" && match.index === buffer.length - 1) break;   // maybe half of "\r\n": wait for more
        const line = buffer.slice(0, match.index);
        buffer = buffer.slice(match.index + match[0].length);

        if (line === "") {                       // blank line → dispatch the event
          if (data.length > 0) yield { event: type || "message", data: data.join("\n"), id: lastEventId, retry };
          data = [];
          type = "";
          retry = undefined;
          continue;
        }
        if (line.startsWith(":")) continue;      // comment / heartbeat
        const colon = line.indexOf(":");
        const field = colon === -1 ? line : line.slice(0, colon);
        let fieldValue = colon === -1 ? "" : line.slice(colon + 1);
        if (fieldValue.startsWith(" ")) fieldValue = fieldValue.slice(1);
        if (field === "data") data.push(fieldValue);
        else if (field === "event") type = fieldValue;
        else if (field === "id" && !fieldValue.includes("\0")) lastEventId = fieldValue;
        else if (field === "retry" && /^\d+$/.test(fieldValue)) retry = Number(fieldValue);
      }
    }
  } finally {
    await reader.cancel().catch(() => {});       // the consumer stopped early → close the connection too
  }
}
```

```js
// sse/client.js: stream a chat answer (POST + JSON body + auth header)
import { parseEventStream } from "./parse.js";

export async function streamChat(url, prompt, { onToken, signal, token } = {}) {
  const res = await fetch(url, {
    method: "POST",
    headers: { "Content-Type": "application/json", Accept: "text/event-stream", ...(token && { Authorization: `Bearer ${token}` }) },
    body: JSON.stringify({ prompt }),
    signal,                                      // abort() = "Stop generating"; the server sees the disconnect
  });
  if (!res.ok) throw new Error((await res.json().catch(() => ({}))).error ?? `HTTP ${res.status}`);
  for await (const evt of parseEventStream(res.body)) {
    const payload = JSON.parse(evt.data);
    if (evt.event === "token") onToken?.(payload.text);
    else if (evt.event === "error") throw new Error(payload.message);
    else if (evt.event === "done") return payload;
  }
  throw new Error("Stream ended before it finished");   // connection dropped mid-answer
}
```

### 5. React: a chat hook with "Stop generating"

```jsx
import { useCallback, useEffect, useRef, useState } from "react";
import { streamChat } from "./sse/client.js";

export function useChatStream(url) {
  const [text, setText] = useState("");
  const [status, setStatus] = useState("idle");              // idle | streaming | done | stopped | error
  const [error, setError] = useState(null);
  const controllerRef = useRef(null);

  const start = useCallback(async (prompt) => {
    controllerRef.current?.abort();                           // a new question cancels the previous answer
    const controller = new AbortController();
    controllerRef.current = controller;
    setText("");
    setError(null);
    setStatus("streaming");
    try {
      await streamChat(url, prompt, { signal: controller.signal, onToken: (t) => setText((prev) => prev + t) });
      setStatus("done");
    } catch (err) {
      if (controller.signal.aborted) setStatus("stopped");
      else { setError(err.message); setStatus("error"); }
    }
  }, [url]);

  const stop = useCallback(() => controllerRef.current?.abort(), []);
  useEffect(() => () => controllerRef.current?.abort(), []);  // unmount → close the stream
  return { text, status, error, start, stop };
}

export function ChatBox() {
  const { text, status, error, start, stop } = useChatStream("/api/chat");
  const [prompt, setPrompt] = useState("");
  return (
    <form onSubmit={(e) => { e.preventDefault(); start(prompt); }}>
      <label htmlFor="prompt">Ask a question</label>
      <input id="prompt" value={prompt} onChange={(e) => setPrompt(e.target.value)} />
      <button type="submit">Send</button>
      <button type="button" onClick={stop} disabled={status !== "streaming"}>Stop generating</button>
      {/* Not a live region: a screen reader would announce every token. Announce completion instead */}
      <div className="answer" aria-busy={status === "streaming"}>{text}</div>
      <p role="status">{status === "done" ? "Answer complete" : status === "stopped" ? "Stopped" : ""}</p>
      {error && <p role="alert">{error}</p>}
    </form>
  );
}
```

`setText` runs once per token, which is fine for chat speeds. For very fast streams (logs, thousands of events a second), collect tokens in a ref and flush them to state once per animation frame.

**`EventSource` for feeds.** It reconnects by itself (after the server's `retry:` delay) and sends the last `id` it saw as the `Last-Event-ID` header, so the server can replay what was missed. It does **not** reconnect if the server answers with a non-200 status or a different content type, or when you call `close()`. Answering `204 No Content` is how a server tells it to stop for good.

```js
const source = new EventSource("/api/notifications/stream");
source.addEventListener("notification", (e) => showToast(JSON.parse(e.data)));   // named events need addEventListener
source.onerror = () => {
  if (source.readyState === EventSource.CLOSED) showBanner("Live updates stopped. Refresh to retry.");
  // readyState CONNECTING means it's already retrying on its own
};
```

### 6. Infrastructure: what silently breaks streaming

- **Response buffering** in nginx, CDNs or compression middleware holds the events and then delivers them all at the end. Send `X-Accel-Buffering: no` (nginx) and `Cache-Control: no-transform` (the `compression` middleware skips such responses), or turn buffering off for the route (`proxy_buffering off;`).
- **Idle timeouts** close quiet connections: nginx's `proxy_read_timeout` and the AWS ALB idle timeout both default to 60 s. Send a heartbeat comment more often than the shortest timeout on the path, and raise `proxy_read_timeout` for the streaming routes.
- **Browser connection limits:** over HTTP/1.1, a browser allows only **6 connections per domain**, and every open `EventSource` uses one, so a few tabs can starve normal requests. Serve over **HTTP/2** (streams are multiplexed), and share one connection per tab.
- **Scaling out:** each instance only knows its own clients, so publish through Redis pub/sub (or a broker), and keep replayable history in Redis Streams or the database. Include the stream in your graceful shutdown: stop accepting, then close the streams, and clients reconnect to another instance.
- **Serverless and some platforms** limit response duration or buffer responses. Check before choosing streaming there.
- **Measure:** open streams, events sent, dropped slow consumers, and time-to-first-token for chat.

### Interview Qs

1. SSE vs WebSocket: when do you pick each? → SSE for one-way server → client updates over plain HTTP (auto-reconnect, works through proxies and HTTP/2). WebSocket when the client also streams messages.
2. How does SSE resume after a disconnect? → Events carry an `id`; `EventSource` reconnects after the `retry:` delay and sends `Last-Event-ID`; the server replays newer events from a log.
3. Why can't you use `EventSource` for an LLM chat request? → It's `GET`-only and can't set headers. Use `fetch` with a `POST` body and parse `res.body` as a stream.
4. Why does a streaming parser need a buffer? → Network chunks don't align with events or even lines. Buffer, split on line endings and dispatch on blank lines.
5. How do you report an error halfway through a stream? → The status code is already sent, so send an in-band `error` event (and a final `done` on success, so clients can detect truncation).
6. What should happen when the client disconnects mid-generation? → Abort the upstream work (an `AbortController` tied to the response's `close` event). It saves CPU and model tokens.
7. What is backpressure in streaming? How do you handle a slow client? → `res.write()` returning `false` means the buffer is full. Wait for `drain` (single consumer), or drop the slow client and let it resume with `Last-Event-ID` (fan-out).
8. Why do streams arrive all at once in production but fine locally? → Proxy, CDN or compression buffering. Use `X-Accel-Buffering: no`, `Cache-Control: no-transform` and `proxy_buffering off`.
9. Why send heartbeats? → Proxies and load balancers close idle connections (often after 60 s). A comment line every 15 s keeps them open.
10. How do you scale SSE across several servers? → Fan out through Redis pub/sub or a broker, keep replayable history in Redis Streams or the database, and make clients reconnect to any instance.
11. What's the browser's HTTP/1.1 connection limit problem? → 6 connections per domain, and each `EventSource` holds one. Use HTTP/2 and one shared connection.

---

## 50. Job Queues

Move slow or unreliable work (emails, image processing, reports, webhooks) **out of the request cycle** into background workers. Gives retries, scheduling, rate control.

### BullMQ (Redis-based)

```js
import { Queue, Worker } from "bullmq";
const connection = { host: "localhost", port: 6379 };

export const emailQueue = new Queue("emails", { connection });

// producer (in a route)
app.post("/signup", async (req, res) => {
  const user = await createUser(req.body);
  await emailQueue.add("welcome", { userId: user.id }, { attempts: 3, backoff: { type: "exponential", delay: 5000 } });
  res.status(201).json(user); // respond fast
});

// consumer (separate process)
new Worker("emails", async (job) => {
  const user = await getUser(job.data.userId);
  await sendEmail(user.email, "Welcome!");
}, { connection, concurrency: 5 });

// scheduled/repeating job
await emailQueue.add("digest", {}, { repeat: { pattern: "0 9 * * *" } }); // every day 9am
```

Cron in-process: `node-cron`. Message brokers for microservices: RabbitMQ, Kafka, AWS SQS.

---

## 51. BullMQ in Depth

**BullMQ** is the standard Redis-backed job queue for Node.js: retries with backoff, delays, priorities, rate limiting, scheduled jobs, parent/child flows, progress, and a dashboard. (Design principles are shared with Celery — see `fastapi.md` → "Task Queues in Depth".)

### Building blocks

| Piece | Role |
|---|---|
| `Queue` | Producer side: `queue.add(name, data, opts)` |
| `Worker` | Consumer: runs a processor function for each job |
| `Job` | One unit of work: `id`, `name`, `data`, `attemptsMade`, progress, return value |
| `QueueEvents` | Listen to job events globally (across processes) |
| `FlowProducer` | Parent/child job trees |

**Job states**: `waiting` → `active` → `completed` / `failed`; plus `delayed` (scheduled/backoff), `prioritized`, `waiting-children` (flows).

**Redis requirements**: set `maxmemory-policy noeviction` (evicted keys = lost jobs), enable persistence (AOF), and give workers `maxRetriesPerRequest: null`.

### 1. Producer: adding jobs

```js
// queues.js
import { Queue } from "bullmq";

export const connection = { host: process.env.REDIS_HOST ?? "localhost", port: 6379 };

export const emailQueue = new Queue("emails", {
  connection,
  defaultJobOptions: {
    attempts: 5,
    backoff: { type: "exponential", delay: 1000 },    // 1s, 2s, 4s, 8s…
    removeOnComplete: { age: 24 * 3600, count: 1000 }, // keep Redis small
    removeOnFail: { age: 7 * 24 * 3600 },               // keep failures a week for debugging
  },
});

export const reportQueue = new Queue("reports", { connection });   // slow jobs get their own queue
```

```js
// adding jobs
await emailQueue.add("welcome", { userId: user.id });                               // pass IDs, not objects
await emailQueue.add("welcome", { userId: user.id }, { jobId: `welcome-${user.id}` }); // same jobId → not added twice
await emailQueue.add("reminder", { cartId }, { delay: 60 * 60 * 1000 });            // run in 1 hour
await emailQueue.add("password-reset", { userId }, { priority: 1 });                // lower number = higher priority
await emailQueue.addBulk(users.map((u) => ({ name: "digest", data: { userId: u.id } })));
```

### 2. Worker: processing jobs

```js
// workers/email.worker.js — runs as its OWN process/container, not inside the web server
import { Worker, UnrecoverableError } from "bullmq";
import { connection } from "../queues.js";

const worker = new Worker(
  "emails",
  async (job) => {
    const user = await db.user.findUnique({ where: { id: job.data.userId } });
    if (!user) throw new UnrecoverableError(`user ${job.data.userId} not found`);   // don't retry — it won't help
    if (await alreadySent(job.name, user.id)) return { skipped: true };             // idempotency guard

    await job.updateProgress(50);
    const res = await emailProvider.send(templates[job.name](user), {
      idempotencyKey: `${job.name}-${user.id}`,
      signal: AbortSignal.timeout(10_000),
    });
    await markSent(job.name, user.id);
    return { messageId: res.id };                       // stored as job.returnvalue
  },
  {
    connection: { ...connection, maxRetriesPerRequest: null },
    concurrency: 10,                                   // parallel jobs in this process (I/O-bound work)
    limiter: { max: 50, duration: 1000 },              // at most 50 jobs/s — respect the provider's rate limit
  },
);

worker.on("completed", (job, result) => logger.info({ jobId: job.id, result }, "email sent"));
worker.on("failed", (job, err) => {
  logger.error({ jobId: job?.id, attempts: job?.attemptsMade, err }, "email job failed");
  if (job && job.attemptsMade >= (job.opts.attempts ?? 1)) alertOnCall(job, err);   // retries exhausted
});

// graceful shutdown: finish active jobs, stop taking new ones
for (const signal of ["SIGTERM", "SIGINT"]) process.on(signal, async () => { await worker.close(); process.exit(0); });
```

Important worker facts:
- **Retries**: a thrown error → retry with backoff until `attempts` is exhausted → job moves to **failed**.
- **`UnrecoverableError`**: fail immediately without retries (bad input, missing record).
- **Stalled jobs**: a worker holds a **lock** on an active job and renews it. If the lock expires (worker crashed, or the **event loop was blocked** by CPU work), the job is considered **stalled** and moved back to waiting — it will run **again**. Another reason jobs must be idempotent. CPU-heavy work → **sandboxed processors** (a separate file run in a child process/worker thread) or worker threads.
- **Concurrency** is per worker process; scale by running more worker processes/containers.

### 3. Custom backoff with jitter

```js
// Full-jitter exponential backoff: spreads retries so they don't all hit the provider at once
export function backoffWithJitter(attemptsMade, { base = 1000, cap = 5 * 60_000, random = Math.random } = {}) {
  const max = Math.min(cap, base * 2 ** Math.max(0, attemptsMade - 1));
  return Math.round(random() * max);
}

// register it on the worker, then use it per job
// new Worker("emails", processor, { connection, settings: { backoffStrategy: (attemptsMade) => backoffWithJitter(attemptsMade) } });
// queue.add("welcome", data, { attempts: 6, backoff: { type: "custom" } });
```

### 4. Idempotency with Redis `SET NX`

Jobs run **at least once**. Guard side effects with an atomic "claim" key:

```js
// Returns true if this caller claimed the key (first time), false if it was already claimed.
export async function claimOnce(redis, key, ttlSeconds = 7 * 24 * 3600) {
  const result = await redis.set(`once:${key}`, "1", "EX", ttlSeconds, "NX");   // NX = only if Not eXists
  return result === "OK";
}

// in a processor
new Worker("invoices", async (job) => {
  if (!(await claimOnce(redis, `invoice-email-${job.data.invoiceId}`))) return { skipped: "duplicate" };
  await sendInvoiceEmail(job.data.invoiceId);
}, { connection: { ...connection, maxRetriesPerRequest: null } });
```

Caveat: if the job fails *after* claiming, the retry is skipped. For must-succeed side effects, set the claim **after** success (as `markSent` does above), or store the status in the database alongside the business data.

### 5. Scheduled & repeatable jobs

```js
// BullMQ v5.16+: Job Schedulers (upsert is idempotent — safe to run on every deploy)
await reportQueue.upsertJobScheduler(
  "nightly-sales-report",                          // scheduler id
  { pattern: "0 2 * * *", tz: "Asia/Kolkata" },    // cron: 02:00 every day, IST
  { name: "sales-report", data: { range: "yesterday" } },
);
await emailQueue.upsertJobScheduler("digest-every-6h", { every: 6 * 60 * 60 * 1000 }, { name: "digest" });

// Older versions: queue.add("sales-report", data, { repeat: { pattern: "0 2 * * *" }, jobId: "nightly-sales-report" })
```

Only one job is created per scheduled time even with many workers — no duplicate cron runs (unlike running `node-cron` in every web replica).

### 6. Flows: parent job waits for its children

```js
import { FlowProducer } from "bullmq";
const flow = new FlowProducer({ connection });

await flow.add({
  name: "build-zip",
  queueName: "exports",
  data: { exportId },
  children: photoIds.map((id) => ({ name: "resize", queueName: "images", data: { photoId: id } })),
});

// in the "exports" worker: results of all children are available once they finish
// const childResults = await job.getChildrenValues();   // { "bull:images:123": { url: "…" }, … }
```

### 7. Express integration: enqueue, return 202, poll status

```js
// pure mapping from a BullMQ job to an API response (easy to test)
export function toJobStatus(job, state) {
  if (!job) return null;
  return {
    id: job.id,
    state,                                                        // waiting | active | completed | failed | delayed …
    progress: typeof job.progress === "number" ? job.progress : 0,
    result: state === "completed" ? job.returnvalue ?? null : null,
    error: state === "failed" ? job.failedReason ?? "Unknown error" : null,
    attempts: job.attemptsMade ?? 0,
  };
}

app.post("/api/reports", requireAuth, async (req, res) => {
  const report = await db.report.create({ data: { ownerId: req.user.id, status: "queued" } });   // commit first
  const job = await reportQueue.add("sales-report", { reportId: report.id }, { jobId: `report-${report.id}` });
  res.status(202).json({ jobId: job.id, statusUrl: `/api/jobs/${job.id}` });
});

app.get("/api/jobs/:id", requireAuth, async (req, res) => {
  const job = await reportQueue.getJob(req.params.id);
  if (!job || !(await userOwnsJob(req.user, job))) return res.status(404).json({ error: "Not found" });
  res.json(toJobStatus(job, await job.getState()));
});
```

Push instead of poll: listen with `QueueEvents` (`completed`/`failed`/`progress`) and forward to the user via WebSocket/SSE.

### 8. Monitoring

```js
import { createBullBoard } from "@bull-board/api";
import { BullMQAdapter } from "@bull-board/api/bullMQAdapter";
import { ExpressAdapter } from "@bull-board/express";

const serverAdapter = new ExpressAdapter();
serverAdapter.setBasePath("/admin/queues");
createBullBoard({ queues: [new BullMQAdapter(emailQueue), new BullMQAdapter(reportQueue)], serverAdapter });
app.use("/admin/queues", requireAdmin, serverAdapter.getRouter());   // protect it!
```

- Metrics to export: waiting/active/failed/delayed counts per queue (`queue.getJobCounts()`), job duration, failure rate, oldest waiting job age. **Alert on growing queue depth** and on failed jobs.
- Retry failed jobs from the dashboard after fixing the cause (`job.retry()`), or clean them (`queue.clean()`).

### BullMQ checklist

- [ ] Redis: `noeviction`, persistence, monitored memory; workers use `maxRetriesPerRequest: null`
- [ ] Workers deployed separately from the web app; graceful `worker.close()` on SIGTERM
- [ ] `attempts` + backoff for transient errors; `UnrecoverableError` for permanent ones
- [ ] Idempotent processors (jobId dedupe, idempotency keys, status checks)
- [ ] Jobs enqueued after the DB commit; job data = IDs, small & JSON-serializable
- [ ] `removeOnComplete` / `removeOnFail` retention so Redis doesn't grow forever
- [ ] Separate queues for slow vs urgent work; `limiter` for rate-limited providers
- [ ] CPU-heavy processors sandboxed (no event-loop blocking → no stalled jobs)
- [ ] Job Schedulers for cron work (one run per tick across replicas)
- [ ] Bull Board (protected) + queue-depth/failure metrics and alerts

### Interview Qs

1. How does BullMQ work (Queue, Worker, Redis) and what job states exist?
2. How do retries and backoff work? When would you throw `UnrecoverableError`?
3. What is a stalled job and what causes it?
4. How do you prevent duplicate jobs and make processors idempotent?
5. Why run workers in separate processes from the API?
6. How do you schedule a nightly job without it running on every server replica?
7. How do you report job progress to the frontend?
8. Why must Redis use `maxmemory-policy noeviction` for queues?

---

## 52. Testing

### Types

- **Unit** — single function/module in isolation (mock dependencies).
- **Integration** — multiple parts together (route + DB).
- **E2E** — whole system as a user would.

### Unit test (Vitest / Jest)

```js
// utils/price.js
export const applyDiscount = (price, pct) => {
  if (pct < 0 || pct > 100) throw new RangeError("invalid discount");
  return Math.round(price * (1 - pct / 100) * 100) / 100;
};

// utils/price.test.js
import { describe, it, expect } from "vitest";
import { applyDiscount } from "./price.js";

describe("applyDiscount", () => {
  it("applies percentage", () => expect(applyDiscount(200, 10)).toBe(180));
  it("throws on invalid pct", () => expect(() => applyDiscount(100, 150)).toThrow(RangeError));
});
```

### Mocking

```js
import { vi } from "vitest";
import * as mailer from "../services/mailer.js";

vi.spyOn(mailer, "sendEmail").mockResolvedValue({ ok: true });
await registerUser({ email: "a@b.com" });
expect(mailer.sendEmail).toHaveBeenCalledWith("a@b.com", expect.any(String));

vi.useFakeTimers(); vi.advanceTimersByTime(1000);
```

### API integration test with Supertest

```js
import request from "supertest";
import { app } from "../app.js"; // export app without calling listen()

describe("POST /api/todos", () => {
  it("creates a todo", async () => {
    const res = await request(app).post("/api/todos").send({ title: "Test" }).expect(201);
    expect(res.body).toMatchObject({ title: "Test", done: false });
  });
  it("validates title", async () => {
    await request(app).post("/api/todos").send({}).expect(400);
  });
  it("requires auth", async () => {
    await request(app).get("/api/profile").expect(401);
  });
});
```

Use a separate test DB (Docker, `mongodb-memory-server`, Testcontainers); reset data between tests.

### Built-in test runner (Node 20+)

```js
import { test, describe, mock } from "node:test";
import assert from "node:assert/strict";

describe("math", () => {
  test("adds", () => assert.equal(1 + 1, 2));
  test("async", async () => assert.deepEqual(await Promise.resolve([1]), [1]));
});
// node --test
```

---

## 53. Performance & Debugging

### Tips

- Never block the event loop (no sync I/O in handlers, offload CPU work).
- Use streams for large data.
- Cache (Redis, HTTP headers, CDN).
- DB: indexes, avoid N+1, select only needed fields, pagination, connection pooling.
- Compression (gzip/brotli) — often done at the reverse proxy.
- `Promise.all` for independent async work.
- Use cluster/PM2 to use all cores.
- Keep dependencies lean; faster frameworks (Fastify) if needed.
- Measure: `autocannon` / `k6` load testing, `clinic.js` (doctor, flame, bubbleprof), `--prof`, `--cpu-prof`.

```js
// Measure event loop lag
import { monitorEventLoopDelay } from "node:perf_hooks";
const h = monitorEventLoopDelay({ resolution: 20 });
h.enable();
setInterval(() => console.log("p99 lag ms", h.percentile(99) / 1e6), 5000);
```

### Debugging

```bash
node --inspect app.js        # open chrome://inspect, set breakpoints
node --inspect-brk app.js    # break on first line
```

VS Code debugger (launch.json / auto attach), `debugger;` statement, `console.table`, `console.time/timeEnd`.

### Memory leaks

Common causes:
1. Global variables / module-level caches that grow forever.
2. Event listeners added per request and never removed.
3. Timers (`setInterval`) not cleared.
4. Closures holding large objects.
5. Unbounded in-memory queues/arrays.

```js
// ❌ leak: grows forever
const cache = {};
app.get("/user/:id", async (req, res) => {
  cache[req.params.id] ??= await getUser(req.params.id);
  res.json(cache[req.params.id]);
});
// ✅ bounded LRU with TTL
import { LRUCache } from "lru-cache";
const lru = new LRUCache({ max: 1000, ttl: 60_000 });
```

Find leaks: `process.memoryUsage()`, `--inspect` + Chrome DevTools heap snapshots (compare two snapshots), `--heapsnapshot-signal=SIGUSR2`, clinic heapprofiler. `--max-old-space-size=4096` to raise heap limit (not a fix).

---

## 54. Graceful Shutdown

On `SIGTERM` (Docker/Kubernetes stop, PM2 reload): stop accepting new connections, finish in-flight requests, close DB/Redis connections, then exit. Otherwise users get dropped requests and data can be corrupted.

```js
const server = app.listen(PORT);

async function shutdown(signal) {
  console.log(`${signal} received, shutting down`);
  server.close(async () => {                    // stops new connections, waits for open ones
    try {
      await mongoose.connection.close();
      await redis.quit();
      console.log("clean exit");
      process.exit(0);
    } catch (e) {
      console.error(e);
      process.exit(1);
    }
  });
  setTimeout(() => process.exit(1), 10_000).unref(); // force exit if it takes too long
}

process.on("SIGTERM", () => shutdown("SIGTERM"));
process.on("SIGINT", () => shutdown("SIGINT"));
```

---

## 55. Microservices

### Monolith vs Microservices

| Monolith | Microservices |
|---|---|
| One codebase & deployable | Many small services, each owns its data |
| Simple to develop, test, deploy early | Independent deploys & scaling, tech freedom |
| Scaling = scale everything | Complex: network, observability, data consistency |
| Great starting point | Useful when teams/domains grow |

### Key concepts

- **API Gateway** — single entry point: routing, auth, rate limiting, aggregation (Kong, AWS API Gateway, Nginx).
- **Service discovery** — find service addresses (k8s DNS, Consul).
- **Communication** — sync (REST, gRPC) vs async (events via Kafka/RabbitMQ/SQS).
- **Database per service**; consistency via **Saga pattern** (sequence of local transactions + compensating actions) instead of distributed transactions.
- **Circuit breaker** — stop calling a failing service for a while (`opossum`).
- **Retries with backoff + timeouts + idempotency**. Both are implemented and tested in Section 56, along with bulkheads, load shedding and fallbacks.
- **Observability** — centralized logs, metrics, distributed tracing.
- **Event-driven architecture**, CQRS, outbox pattern.
- **BFF** (Backend For Frontend).

```js
// Publish an event (RabbitMQ with amqplib)
import amqp from "amqplib";
const conn = await amqp.connect(process.env.AMQP_URL);
const ch = await conn.createChannel();
await ch.assertExchange("orders", "fanout", { durable: true });
ch.publish("orders", "", Buffer.from(JSON.stringify({ type: "OrderPlaced", orderId: 1 })), { persistent: true });

// Consume
const q = await ch.assertQueue("email-service", { durable: true });
await ch.bindQueue(q.queue, "orders", "");
ch.consume(q.queue, (msg) => {
  const event = JSON.parse(msg.content.toString());
  // handle...
  ch.ack(msg);
});
```

---

## 56. Resilience: Timeouts, Retries, Circuit Breakers & Load Shedding

Every network call eventually fails: the payment provider has a bad minute, a database failover takes 20 seconds, a partner API starts answering in 30 seconds instead of 300 ms. The danger isn't the failure itself, it's the **cascade**. Requests waiting on the slow dependency pile up, holding sockets, memory and database connections, until *your* service falls over and takes its callers with it. Resilience patterns make a service **fail fast, recover by itself, and degrade gracefully**.

| Pattern | Protects against | One-line rule |
|---|---|---|
| **Timeout** | Waiting forever on a slow dependency | Every network call has one, and it's shorter than your caller's |
| **Retry with backoff + jitter** | Brief, transient failures | Only transient errors, only idempotent operations, few attempts |
| **Circuit breaker** | Hammering a dependency that's down | After repeated failures, fail instantly for a while, then test carefully |
| **Bulkhead** (concurrency limit) | One slow dependency using up all resources | Cap concurrent calls per dependency; reject when the queue is full |
| **Load shedding** | Your own service being overloaded | Reject early with `503` + `Retry-After` instead of slowing down for everyone |
| **Fallback** | A failed optional dependency breaking the page | Serve stale data, a default, or hide the feature |
| **Deadline propagation** | Work done after the caller has already given up | Pass the remaining time budget downstream |

Everything below is dependency-free and uses Node 20+ built-ins (`fetch`, `AbortSignal.timeout`, `AbortSignal.any`, `timers/promises`). It was tested against a local HTTP server that fails on purpose.

### 1. Timeouts everywhere

Node's `fetch` has **no overall timeout**. Its underlying client (undici) only gives up after 10 s trying to connect, or **5 minutes** without response headers or between body chunks, so a server that trickles data can hold a request forever. Many database and HTTP clients have no timeout at all.

```js
// resilience/http.js
export class HttpError extends Error {
  constructor(status, retryAfterMs) {
    super(`HTTP ${status}`);
    this.name = "HttpError";
    this.status = status;
    this.retryAfterMs = retryAfterMs;
  }
}

// "Retry-After: 30" (seconds) or "Retry-After: Wed, 21 Oct 2026 07:28:00 GMT" (a date)
export function parseRetryAfter(value, now = Date.now()) {
  if (!value) return undefined;
  const seconds = Number(value);
  if (Number.isFinite(seconds)) return Math.max(0, seconds * 1000);
  const date = Date.parse(value);
  return Number.isNaN(date) ? undefined : Math.max(0, date - now);
}

// One attempt: a timeout for THIS attempt, plus an optional caller signal (client disconnected, overall deadline)
export async function fetchJson(url, { timeoutMs = 2_000, signal, ...init } = {}) {
  const timeout = AbortSignal.timeout(timeoutMs);
  const res = await fetch(url, { ...init, signal: signal ? AbortSignal.any([signal, timeout]) : timeout });
  if (!res.ok) {
    await res.body?.cancel();                 // release the connection back to the pool
    throw new HttpError(res.status, parseRetryAfter(res.headers.get("retry-after")));
  }
  return res.json();
}
```

When the timeout fires, `fetch` rejects with an error whose `name` is `"TimeoutError"`. Set timeouts on the other clients too:

- **Postgres (`pg`):** `connectionTimeoutMillis` on the pool, plus `statement_timeout` for queries.
- **Redis (`ioredis`):** `connectTimeout` and `commandTimeout`.
- **Your own HTTP server:** `server.requestTimeout` (default 300 s) and `server.headersTimeout`.

**Timeouts must shrink as you go deeper.** If the browser gives up after 10 s and your API calls a service with a 15 s timeout, you do 5 s of work nobody will read. Pass the remaining budget downstream (section 6).

### 2. Retries done right

Retries turn brief blips into successes. Done carelessly, they turn an outage into a **retry storm**: every client multiplies its traffic just when the dependency is weakest.

- Retry **only transient failures**: timeouts, network errors, `408`, `429`, `502`, `503`, `504`. Never `400`/`401`/`403`/`404`/`422`; the answer won't change. A `500` is often a deterministic bug, so retrying it just triples the load.
- Retry **only idempotent operations**: `GET`, `PUT`, `DELETE`, or a `POST` carrying an **`Idempotency-Key`** (Section 42) so the server can deduplicate it.
- Use **exponential backoff with full jitter**. Randomising the wait keeps thousands of clients from retrying in lockstep.
- **Respect `Retry-After`**. If the server asks for longer than you're willing to wait, give up.
- **Retry at one layer only.** Three layers each retrying three times means up to 27 calls for one user request.

```js
// resilience/retry.js
import { setTimeout as sleep } from "node:timers/promises";
import { HttpError } from "./http.js";

const RETRYABLE_STATUS = new Set([408, 429, 502, 503, 504]);

export function isTransient(err) {
  if (err instanceof HttpError) return RETRYABLE_STATUS.has(err.status);
  if (err?.name === "TimeoutError") return true;                             // AbortSignal.timeout fired
  return err instanceof TypeError && err.message === "fetch failed";          // connection refused/reset, DNS…
}

export async function retry(fn, { retries = 3, baseMs = 100, maxMs = 5_000, shouldRetry = isTransient,
  signal, random = Math.random, onRetry } = {}) {
  for (let attempt = 0; ; attempt++) {
    try {
      return await fn(attempt);
    } catch (err) {
      if (attempt >= retries || !shouldRetry(err) || signal?.aborted) throw err;
      if ((err.retryAfterMs ?? 0) > maxMs) throw err;                        // server wants a longer pause than we allow
      const backoff = random() * Math.min(maxMs, baseMs * 2 ** attempt);     // full jitter: 0…base·2^attempt
      const delay = Math.max(backoff, err.retryAfterMs ?? 0);                 // never sooner than Retry-After
      onRetry?.({ attempt: attempt + 1, delay, err });
      await sleep(delay, undefined, { signal });                             // stop waiting if the caller gives up
    }
  }
}
```

### 3. Circuit breaker

When a dependency is down, retrying every request only adds load and makes every user wait for a timeout. A circuit breaker watches recent results and **stops calling** once too many fail:

```
          failure rate ≥ threshold                   openMs elapsed
 CLOSED ───────────────────────────────► OPEN ─────────────────────────► HALF-OPEN
 (calls pass,                            (calls fail instantly           (ONE trial call)
  results recorded)                       with CircuitOpenError)          │        │
     ▲                                          ▲                         │ ok     │ fails
     └──────────────────────────────────────────┼─────────────────────────┘        │
                                                └──────────────────────────────────┘
```

```js
// resilience/circuit-breaker.js
import { isTransient } from "./retry.js";

export class CircuitOpenError extends Error {
  constructor(name, retryInMs) {
    super(`Circuit "${name}" is open`);
    this.name = "CircuitOpenError";
    this.retryInMs = retryInMs;
  }
}

export class CircuitBreaker {
  #state = "closed";          // "closed" | "open" (half-open is "open" after openMs has passed)
  #results = [];              // rolling window of recent outcomes: true = ok, false = failure
  #openedAt = 0;
  #trialInFlight = false;

  constructor({ name, windowSize = 20, minCalls = 10, failureRate = 0.5, openMs = 30_000,
    isFailure = isTransient, now = Date.now, onStateChange = () => {} } = {}) {
    Object.assign(this, { name, windowSize, minCalls, failureRate, openMs, isFailure, now, onStateChange });
  }

  get state() {
    if (this.#state === "open" && this.now() - this.#openedAt >= this.openMs) return "half-open";
    return this.#state;
  }

  async exec(fn) {
    const state = this.state;
    if (state === "open") throw new CircuitOpenError(this.name, this.openMs - (this.now() - this.#openedAt));
    if (state === "half-open") {
      if (this.#trialInFlight) throw new CircuitOpenError(this.name, 0);   // only one trial call at a time
      this.#trialInFlight = true;
    }
    try {
      const result = await fn();
      this.#record(true, state);
      return result;
    } catch (err) {
      this.#record(!this.isFailure(err), state);    // a 404 is not the dependency being unhealthy
      throw err;
    } finally {
      if (state === "half-open") this.#trialInFlight = false;
    }
  }

  #record(ok, stateAtStart) {
    if (stateAtStart === "half-open") return this.#transition(ok ? "closed" : "open");
    if (this.#state !== "closed") return;           // a slow call finishing after the circuit opened
    this.#results.push(ok);
    if (this.#results.length > this.windowSize) this.#results.shift();
    const failures = this.#results.filter((r) => !r).length;
    if (this.#results.length >= this.minCalls && failures / this.#results.length >= this.failureRate) {
      this.#transition("open");
    }
  }

  #transition(to) {
    const from = this.state;
    this.#state = to;
    this.#results = [];
    if (to === "open") this.#openedAt = this.now();
    this.onStateChange({ name: this.name, from, to });   // log it and export it as a metric
  }
}
```

Design choices worth explaining in an interview:

- A **failure rate over a rolling window** with a **minimum number of calls**, so 1 failure out of 1 call doesn't open the circuit at 3 a.m. when traffic is low.
- **Only dependency-health failures count** (timeouts, network errors, 5xx). Your own bad requests (4xx) don't.
- **Half-open allows one trial call.** Letting everything through at once could knock over a dependency that's just recovering.
- Use **one breaker per dependency** (or per host). A broken SMS provider shouldn't stop payments.

In production you can use **`opossum`**, the common Node library, which also wraps the call in a timeout:

```js
import CircuitBreaker from "opossum";

const ratesBreaker = new CircuitBreaker((pair) => fetchJson(`${process.env.RATES_URL}/${pair}`), {
  timeout: 2_000,                // fail the call after 2 s
  errorThresholdPercentage: 50,  // open when ≥ 50% of calls in the window fail…
  volumeThreshold: 10,           // …once there have been at least 10 calls
  resetTimeout: 30_000,          // then try a half-open trial after 30 s
});
ratesBreaker.fallback(() => ({ rate: null, stale: true }));
ratesBreaker.on("open", () => console.warn("rates circuit opened"));

const usdInr = await ratesBreaker.fire("USD-INR");
```

### 4. Bulkhead: cap concurrent calls per dependency

Named after a ship's watertight compartments. Without a cap, 2,000 requests stuck on a slow dependency hold 2,000 sockets and promises in memory. With a cap of 20 and a short queue, the rest fail immediately, and other endpoints keep working.

```js
// resilience/bulkhead.js
export class BulkheadFullError extends Error {
  name = "BulkheadFullError";
}

export function createLimiter(maxConcurrent, { maxQueue = Infinity } = {}) {
  let active = 0;
  const queue = [];
  const next = () => {
    if (active >= maxConcurrent || queue.length === 0) return;
    active++;
    const { fn, resolve, reject } = queue.shift();
    Promise.resolve().then(fn).then(resolve, reject).finally(() => { active--; next(); });
  };
  return function limit(fn) {
    if (active >= maxConcurrent && queue.length >= maxQueue) {
      return Promise.reject(new BulkheadFullError(`Too many concurrent calls (max ${maxConcurrent} + queue ${maxQueue})`));
    }
    return new Promise((resolve, reject) => { queue.push({ fn, resolve, reject }); next(); });
  };
}
```

### 5. Putting them together

Each attempt gets its own timeout. The breaker counts every attempt. Retries stop immediately when the circuit is open, because `CircuitOpenError` isn't transient. The bulkhead caps the whole thing.

```js
// resilience/dependency.js
import { CircuitBreaker } from "./circuit-breaker.js";
import { createLimiter } from "./bulkhead.js";
import { fetchJson } from "./http.js";
import { retry } from "./retry.js";

export function createDependency({ name, timeoutMs = 2_000, retries = 2, maxConcurrent = 20, maxQueue = 50,
  breaker: breakerOptions = {}, retryOptions = {} }) {
  const breaker = new CircuitBreaker({ name, ...breakerOptions });
  const limit = createLimiter(maxConcurrent, { maxQueue });
  return {
    breaker,
    getJson: (url, { signal } = {}) =>
      limit(() => retry(() => breaker.exec(() => fetchJson(url, { timeoutMs, signal })), { retries, signal, ...retryOptions })),
  };
}

// usage: one instance per dependency, created once at startup
// const rates = createDependency({ name: "rates-api", timeoutMs: 1_500, retries: 2 });
// const quote = await rates.getJson(`${RATES_URL}/USD-INR`, { signal: clientGone.signal });
```

### 6. Deadline propagation

Send the caller's **remaining time** downstream, so no service keeps working on a request whose caller has already timed out. Pass a *relative* budget (gRPC does the same with `grpc-timeout`). An absolute timestamp breaks when server clocks differ.

```js
// resilience/deadline.js
export const TIMEOUT_HEADER = "x-request-timeout-ms";

export function deadline({ defaultBudgetMs = 10_000, maxBudgetMs = 30_000 } = {}) {
  return (req, res, next) => {
    const asked = Number(req.get(TIMEOUT_HEADER));
    const budget = Number.isFinite(asked) && asked > 0 ? Math.min(asked, maxBudgetMs) : defaultBudgetMs;
    req.deadline = Date.now() + budget;
    next();
  };
}

// Remaining budget for a downstream call, minus a margin for our own work afterwards
export function remainingMs(req, marginMs = 50) {
  return Math.max(0, req.deadline - Date.now() - marginMs);
}

// In a handler:
// const budget = remainingMs(req);
// if (budget === 0) return res.status(504).json({ error: "Deadline exceeded" });
// const data = await fetchJson(url, { timeoutMs: budget, headers: { [TIMEOUT_HEADER]: String(budget) } });
```

### 7. Load shedding: protect yourself

When your own service is overloaded, slowing down for **everyone** is worse than quickly rejecting **some** requests. Shed load when too many requests are in flight or the event loop is lagging, and keep health checks exempt:

```js
// resilience/load-shedding.js
import { monitorEventLoopDelay } from "node:perf_hooks";

export function loadShedding({ maxInFlight = 200, maxLagMs = 200, exempt = ["/healthz", "/readyz"] } = {}) {
  const lag = monitorEventLoopDelay({ resolution: 20 });
  lag.enable();
  setInterval(() => lag.reset(), 5_000).unref();        // look at recent lag, not all-time
  let inFlight = 0;

  const middleware = (req, res, next) => {
    if (exempt.includes(req.path)) return next();
    const lagMs = lag.percentile(99) / 1e6;              // nanoseconds → milliseconds
    if (inFlight >= maxInFlight || lagMs > maxLagMs) {
      res.set("Retry-After", "2");
      return res.status(503).json({ error: "Server busy, please retry shortly" });
    }
    inFlight++;
    res.once("close", () => { inFlight--; });            // fires for completed AND aborted responses
    next();
  };
  middleware.stats = () => ({ inFlight, p99LagMs: lag.percentile(99) / 1e6 });
  return middleware;
}
```

With Fastify, `@fastify/under-pressure` does this. The load balancer or gateway should also enforce per-client rate limits (Section 39) before requests reach Node.

### 8. Fallbacks and graceful degradation

Decide **per dependency** what the product does when it fails:

| Dependency | Fallback |
|---|---|
| Exchange rates, product recommendations | Serve the last good value (stale), and mark it stale in the response |
| Reviews widget, "people also bought" | Hide the section; the page still works |
| Email or SMS sending | Put it on a queue and deliver later |
| Payments, auth | **No fallback**: fail clearly. Never "assume success" for money or permissions |

```js
// resilience/fallback.js — per-process "last known good" cache (use Redis to share it across instances)
const lastGood = new Map();                              // keep the key set small and bounded (e.g. currency pairs)

export async function withStaleFallback(key, fn, { maxStaleMs = 60 * 60_000, now = Date.now } = {}) {
  try {
    const value = await fn();
    lastGood.set(key, { value, at: now() });
    return { value, stale: false };
  } catch (err) {
    const cached = lastGood.get(key);
    if (cached && now() - cached.at <= maxStaleMs) return { value: cached.value, stale: true, error: err.message };
    throw err;
  }
}
```

### 9. Observability and testing

- **Measure every dependency:** latency percentiles, error rate, timeouts, retries, breaker state changes and bulkhead rejections. An alert on "circuit open for more than 5 minutes" is often your first sign of a partner outage.
- **Tune from data:** set each timeout a little above the dependency's p99 latency, not a round guess.
- **Test failure on purpose:** unit-test the state machines with an injected clock (`now`), as above; use **fault injection** (Toxiproxy adds latency and drops connections between services); run load tests with a dependency degraded; and in mature setups, run chaos experiments in staging.

### Interview Qs

1. Why is a slow dependency often worse than a dead one? → Requests pile up holding sockets, memory and pool connections until the caller itself fails (cascading failure). Fail fast with timeouts.
2. Which errors and requests should you retry? → Transient errors (timeouts, network errors, 408/429/502/503/504) on idempotent operations or ones carrying an idempotency key. Never 4xx validation or auth errors.
3. Why exponential backoff with **jitter**? → Backoff gives the dependency room to recover; jitter spreads clients out so they don't retry in synchronized waves.
4. What is a retry storm? How do you prevent one? → Retries multiplying load during an outage. Use few attempts, retry at one layer, use retry budgets and circuit breakers, and respect `Retry-After`.
5. Explain the circuit breaker's states. → Closed (calls pass, failures counted) → open (fail fast) → after a wait, half-open (one trial call) → closed on success, open on failure.
6. Why a failure *rate* with a minimum call count instead of "3 failures"? → It avoids opening on tiny samples and scales with traffic.
7. What is a bulkhead? → Separate resource limits per dependency, so one slow dependency can't exhaust everything.
8. Load shedding vs rate limiting? → Rate limiting caps each *client's* usage; load shedding protects the *server* by rejecting work when it's overloaded, whoever sent it.
9. What is deadline propagation? Why send a relative timeout? → Downstream services stop working on requests the caller has abandoned. A relative budget avoids depending on synchronized clocks.
10. In what order do you compose timeout, retry and circuit breaker? → Timeout innermost (per attempt), then the breaker (counts each attempt), then retry outermost (and it doesn't retry `CircuitOpenError`); a bulkhead around it all.
11. Give examples of good and bad fallbacks. → Good: stale exchange rates, hiding recommendations, queueing emails. Bad: pretending a payment or a permission check succeeded.

---

## 57. GraphQL Basics

A query language for APIs: **single endpoint**, client asks for exactly the fields it needs.

- **Schema** (types), **Query** (read), **Mutation** (write), **Subscription** (real-time), **Resolvers** (functions that fetch data).

```js
import { ApolloServer } from "@apollo/server";
import { startStandaloneServer } from "@apollo/server/standalone";

const typeDefs = `#graphql
  type User { id: ID!, name: String!, posts: [Post!]! }
  type Post { id: ID!, title: String! }
  type Query { users: [User!]!, user(id: ID!): User }
  type Mutation { createUser(name: String!): User! }
`;

const resolvers = {
  Query: {
    users: () => db.users.findMany(),
    user: (_, { id }) => db.users.findUnique({ where: { id } }),
  },
  Mutation: { createUser: (_, { name }) => db.users.create({ data: { name } }) },
  User: { posts: (parent) => db.posts.findMany({ where: { authorId: parent.id } }) }, // N+1 -> use DataLoader
};

const server = new ApolloServer({ typeDefs, resolvers });
await startStandaloneServer(server, { listen: { port: 4000 } });
```

```graphql
query { user(id: "1") { name posts { title } } }
```

---

## 58. Deployment

### Dockerfile (multi-stage)

```dockerfile
FROM node:22-alpine AS deps
WORKDIR /app
COPY package*.json ./
RUN npm ci --omit=dev

FROM node:22-alpine
WORKDIR /app
ENV NODE_ENV=production
COPY --from=deps /app/node_modules ./node_modules
COPY . .
USER node
EXPOSE 3000
CMD ["node", "src/index.js"]
```

```yaml
# docker-compose.yml
services:
  api:
    build: .
    ports: ["3000:3000"]
    env_file: .env
    depends_on: [db, redis]
  db:
    image: postgres:17
    environment: { POSTGRES_PASSWORD: secret }
    volumes: [pgdata:/var/lib/postgresql/data]
  redis:
    image: redis:7
volumes: { pgdata: {} }
```

### Nginx as reverse proxy

```nginx
server {
  listen 80;
  server_name api.example.com;
  location / {
    proxy_pass http://localhost:3000;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Upgrade $http_upgrade;       # websockets
    proxy_set_header Connection "upgrade";
  }
}
```

Reverse proxy benefits: TLS termination, load balancing, gzip, static files, caching, rate limiting.

### Checklist

- `NODE_ENV=production`, env vars from a secret manager.
- Process manager (PM2) or orchestrator (Docker/Kubernetes/ECS) with restart policies.
- Health checks, graceful shutdown, logging, monitoring.
- CI/CD (GitHub Actions): lint → test → build → deploy.
- Platforms: Render, Railway, Fly.io, AWS (EC2/ECS/Lambda), Vercel (serverless), DigitalOcean.

```yaml
# .github/workflows/ci.yml
name: CI
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version: 22, cache: npm }
      - run: npm ci
      - run: npm run lint
      - run: npm test
```

### Serverless

Functions run on demand (AWS Lambda, Vercel, Cloudflare Workers). Pros: no servers, auto-scale, pay per use. Cons: cold starts, execution time limits, connection pooling issues with DBs (use proxies/serverless drivers).

---

## 59. Project Structure

### Layered architecture

```
src/
  config/            # env, db connection
  routes/            # URL -> controller mapping
  controllers/       # HTTP layer: read req, call service, send res
  services/          # business logic (no req/res)
  models/ or repositories/  # data access
  middleware/        # auth, validation, error handler
  validators/        # zod schemas
  utils/             # helpers
  jobs/              # queue workers
  app.js             # express app (exported for tests)
  server.js          # starts listening
tests/
```

```js
// controllers/user.controller.js
export const create = async (req, res) => {
  const user = await userService.register(req.body);
  res.status(201).json(user);
};

// services/user.service.js
export async function register({ email, password, name }) {
  if (await userRepo.findByEmail(email)) throw new AppError("Email already in use", 409);
  const hash = await bcrypt.hash(password, 12);
  const user = await userRepo.create({ email, name, password: hash });
  await emailQueue.add("welcome", { userId: user.id });
  return sanitize(user);
}
```

Why: separation of concerns, testability (services test without HTTP), easier to change DB or framework. Alternatives: feature/module-based folders (`modules/users/{routes,controller,service,model}`), NestJS modules.

---

## 60. Building & Publishing an npm Package

Publishing a package is how code is shared across repositories: a company utility library, an API client, a CLI tool, an open-source project. Getting it *mostly* right is easy. The hard parts are the ones users hit: the package works with `import` but not `require`, TypeScript picks up the wrong typings, `.env` ends up on the registry, or a "minor" release breaks everyone. This section builds a real package, `@acme/text-utils`, and verifies it the way a user would: by installing the packed tarball into fresh projects. Nothing here was actually published.

### 1. ESM-only or dual (ESM + CommonJS)?

| Consumer | ESM-only package | Dual package |
|---|---|---|
| ESM code (`import`) | ✅ | ✅ |
| CommonJS on **Node 20.19+ / 22.12+** (`require`) | ✅ `require(esm)` works, **unless** the package uses top-level `await` (`ERR_REQUIRE_ASYNC_MODULE`) | ✅ |
| CommonJS on Node 18 and older | ❌ `ERR_REQUIRE_ESM` | ✅ |
| Bundlers (Vite, webpack, esbuild) | ✅ | ✅ |

Measured on Node 18.20, 20.19 and 24.5: `require()` of an ESM-only package failed on 18, and succeeded on 20.19 and 24 (returning the named exports plus `default`).

**Recommendation:** if you can require Node ≥ 20.19 (`"engines"`), ship **ESM-only** and avoid top-level `await` in the entry point. It's one build, and there's no "dual package hazard" (the same library loaded twice, once per format, with two copies of its state). Ship **dual** only when you must support older Node or old tooling. The rest of this section shows dual, because it's the harder case.

### 2. The package

```text
text-utils/
├── src/index.ts        slugify, truncate
├── src/array.ts        chunk            → published as "@acme/text-utils/array"
├── src/cli.ts          the `slugify` command
├── tsup.config.ts
├── package.json
├── README.md, LICENSE
└── .env, test/ …       must NOT be published
```

```ts
// src/index.ts
/** Turn any title into a URL slug: "Crème Brûlée!" → "creme-brulee", "नमस्ते दुनिया" → "नमस्ते-दुनिया" */
export function slugify(text: string): string {
  return text.normalize("NFKD").replace(/(\p{Script=Latin})\p{M}+/gu, "$1").normalize("NFC").toLowerCase()
    .replace(/[^\p{L}\p{M}\p{N}]+/gu, "-").replace(/^-+|-+$/g, "");
}

/** Shorten text to `max` characters, adding "…" when cut */
export function truncate(text: string, max: number): string {
  return text.length <= max ? text : `${text.slice(0, Math.max(0, max - 1))}…`;
}
```

```ts
// src/array.ts
/** Split an array into chunks of `size` */
export function chunk<T>(items: readonly T[], size: number): T[][] {
  if (!Number.isInteger(size) || size < 1) throw new RangeError("size must be a positive integer");
  const out: T[][] = [];
  for (let i = 0; i < items.length; i += size) out.push(items.slice(i, i + size));
  return out;
}
```

```ts
// src/cli.ts
#!/usr/bin/env node
import { slugify } from "./index.js";

const input = process.argv.slice(2).join(" ");
if (!input) {
  console.error("Usage: slugify <text>");
  process.exit(1);
}
console.log(slugify(input));
```

(The `#!/usr/bin/env node` shebang must be the very first line of the real file; the `// src/cli.ts` label above is only for these notes.)

```ts
// tsup.config.ts
import { defineConfig } from "tsup";

export default defineConfig({
  entry: ["src/index.ts", "src/array.ts", "src/cli.ts"],
  format: ["esm", "cjs"],   // dist/index.js (ESM) + dist/index.cjs (CommonJS)
  dts: true,                // dist/index.d.ts + dist/index.d.cts
  clean: true,
  sourcemap: true,
  target: "node20",
});
```

```json
{
  "name": "@acme/text-utils",
  "version": "1.0.0",
  "description": "Tiny text helpers: slugify, truncate, chunk",
  "license": "MIT",
  "type": "module",
  "exports": {
    ".": {
      "import": { "types": "./dist/index.d.ts", "default": "./dist/index.js" },
      "require": { "types": "./dist/index.d.cts", "default": "./dist/index.cjs" }
    },
    "./array": {
      "import": { "types": "./dist/array.d.ts", "default": "./dist/array.js" },
      "require": { "types": "./dist/array.d.cts", "default": "./dist/array.cjs" }
    },
    "./package.json": "./package.json"
  },
  "main": "./dist/index.cjs",
  "types": "./dist/index.d.cts",
  "bin": { "slugify": "./dist/cli.js" },
  "files": ["dist"],
  "sideEffects": false,
  "engines": { "node": ">=20" },
  "repository": { "type": "git", "url": "git+https://github.com/acme/text-utils.git" },
  "publishConfig": { "access": "public" },
  "scripts": {
    "build": "tsup",
    "check": "publint && attw --pack . --profile node16",
    "prepublishOnly": "npm run build && npm run check"
  },
  "devDependencies": {
    "@arethetypeswrong/cli": "^0.18.5",
    "@types/node": "^20.19.43",
    "publint": "^0.3.24",
    "tsup": "^8.5.1",
    "typescript": "^5.9.3"
  }
}
```

### 3. What each field does

| Field | Why |
|---|---|
| `name` | A **scope** (`@acme/…`) groups a company's packages and avoids name squatting. Scoped packages are private by default on npm, hence `publishConfig.access: "public"` |
| `type: "module"` | `.js` files are ESM; `.cjs` files are CommonJS |
| **`exports`** | The package's **public API**. Only listed paths can be imported. `require("@acme/text-utils/dist/index.cjs")` fails with `ERR_PACKAGE_PATH_NOT_EXPORTED`, so internal files can change freely |
| Conditions (`import` / `require` / `types` / `default`) | Matched **in order**, first match wins. Put `types` first inside each branch, and `default` last |
| **Separate `types` per format** | ESM gets `.d.ts`, CommonJS gets `.d.cts`. A single top-level `types` pointing at the ESM `.d.ts` makes CommonJS users' TypeScript think the package is ESM-only (see below) |
| `"./package.json"` | Lets tools read your version and metadata despite `exports` |
| `main`, `types` | Fallbacks for old tools that don't understand `exports` |
| `bin` | Installs a command. npm makes it executable; the file needs a `#!/usr/bin/env node` first line |
| **`files`** | A **whitelist** of what gets published. Without it, npm publishes almost everything, **including `.env`** (verified below) |
| `sideEffects: false` | Tells bundlers unused exports can be tree-shaken |
| `engines` | Documents the Node versions you support |
| `peerDependencies` | For plugins (e.g. `react`): the **host** app provides it, so there aren't two copies. Mark optional ones in `peerDependenciesMeta` |
| `prepublishOnly` | Runs before `npm publish`: build and check, so a stale `dist/` can't ship |

### 4. Verify before you publish

**1. What will be published?** `npm pack --dry-run` lists every file:

```text
npm notice 12B LICENSE
npm notice 39B README.md
npm notice 1.4kB dist/index.cjs
npm notice 281B dist/index.d.cts
…
npm notice 1.2kB package.json
npm notice total files: 23
```

Only `dist/`, README, LICENSE and package.json: `.env`, `src/` and `test/` stayed out. With the `files` field removed, the same command listed **`.env`**, `src/*.ts`, `test/` and `tsconfig.json`. npm doesn't exclude `.env` on its own.

**2. Lint the package.** `publint` checks `package.json` against what's actually in the tarball. `@arethetypeswrong/cli` (attw) resolves every entry point the way TypeScript does for ESM, CommonJS and bundler users:

```text
$ npx attw --pack . --profile node16
                    "@acme/text-utils"   "@acme/text-utils/array"   "@acme/text-utils/package.json"
node16 (from CJS)   🟢 (CJS)             🟢 (CJS)                   🟢 (JSON)
node16 (from ESM)   🟢 (ESM)             🟢 (ESM)                   🟢 (JSON)
bundler             🟢                   🟢                         🟢 (JSON)
```

`--profile node16` ignores the legacy `node10` resolution, which doesn't understand `exports`; subpaths like `/array` always fail there. With a single top-level `types` for both formats, attw reports **"👺 Masquerading as ESM"** for CommonJS users. A CommonJS TypeScript project using `module: node16` then gets *TS1471: … only resolves to an ES module, which cannot be imported with 'require'*, even though the code runs fine.

**3. Install the tarball into a fresh project.** That's the only test that's exactly what users get:

```bash
npm pack                                   # → acme-text-utils-1.0.0.tgz
cd ../consumer && npm install ../text-utils/acme-text-utils-1.0.0.tgz
```

```js
// consumer/esm.js ("type": "module")
import { slugify, truncate } from "@acme/text-utils";
import { chunk } from "@acme/text-utils/array";
console.log(slugify("Crème Brûlée: 10 Recipes!"), truncate("Hello world", 8), chunk([1, 2, 3, 4, 5], 2));
// creme-brulee-10-recipes Hello w… [ [ 1, 2 ], [ 3, 4 ], [ 5 ] ]
```

```js
// consumer/cjs.cjs
const { slugify } = require("@acme/text-utils");
console.log(slugify("Hello World"));                           // hello-world
require("@acme/text-utils/dist/index.cjs");                    // ❌ ERR_PACKAGE_PATH_NOT_EXPORTED
```

```bash
npx slugify "Namaste Duniya 2026"          # namaste-duniya-2026
```

Also type-check a TypeScript consumer (`module: nodenext`) with both an ESM `.ts` file and a CommonJS `.cts` file. For libraries under active development, `npm link` or a workspace is quicker, but test the **packed tarball** before a release. Links hide `files` and `exports` mistakes.

### 5. Versioning: semver is a promise

| Change | Bump |
|---|---|
| Bug fix, no API change | **patch** 1.2.3 → 1.2.4 |
| New feature, backward compatible (a new export, a new optional parameter) | **minor** 1.2.3 → 1.3.0 |
| Anything that can break a user: removing or renaming an export, changing behaviour or defaults, **raising the minimum Node version**, adding a required peer dependency, **changing `exports`** (removing a path breaks deep importers), narrowing accepted input types | **major** 1.2.3 → 2.0.0 |

How users' ranges treat your versions (checked with the `semver` package npm uses):

| Range | Accepts | Rejects |
|---|---|---|
| `^1.2.3` | `1.9.9` | `2.0.0`, and `1.3.0-beta.1` (pre-releases are opt-in) |
| `~1.2.3` | `1.2.9` | `1.3.0` |
| `^0.2.3` | `0.2.9` | **`0.3.0`**: below 1.0, the *minor* number is the breaking one |
| `^0.0.3` | only `0.0.3` | `0.0.4` |

- **Pre-releases:** `npm version prerelease --preid beta` (→ `1.2.4-beta.0`), publish with `npm publish --tag next`, and users opt in with `npm install @acme/text-utils@next`. Without `--tag`, a pre-release becomes `latest` and everyone gets it.
- **Release automation:** with **Changesets**, each PR adds a small markdown file ("minor: add `chunk`"); a release PR bumps versions and writes the CHANGELOG; merging it publishes. `release-please` and `semantic-release` derive the bump from Conventional Commits instead.
- **Never reuse a version number.** npm refuses, even after an unpublish. Unpublishing is only allowed within 72 hours (later only under strict conditions), because others may depend on it. For a bad release, publish a fix and `npm deprecate @acme/text-utils@1.4.0 "Broken date parsing, use 1.4.1"`.

### 6. Publishing securely

Package registries are a favourite supply-chain target: a stolen npm token or a compromised maintainer account can push malware to every user.

- **Publish from CI, not a laptop.** Use npm **trusted publishing** (OIDC): GitHub Actions or GitLab CI proves its identity to npm, so no long-lived npm token exists to be stolen, and a **provenance** attestation links the package to the exact commit and workflow that built it.
- **Turn on 2FA** for your npm account and require it for publishing.
- **Don't ship install scripts** (`preinstall`/`postinstall`) unless unavoidable; they run on every user's machine. Users can install with `npm ci --ignore-scripts`.
- Keep runtime `dependencies` minimal; each one is code you're vouching for.

```yaml
# .github/workflows/release.yml: publish when a v* tag is pushed (trusted publishing, no NPM_TOKEN)
name: Release
on:
  push:
    tags: ["v*"]
permissions:
  contents: read
  id-token: write          # lets npm verify this workflow (OIDC) and sign provenance
jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 22
          registry-url: https://registry.npmjs.org
      - run: npm install -g npm@latest      # trusted publishing needs a recent npm CLI (11.5+)
      - run: npm ci
      - run: npm test
      - run: npm publish                     # runs prepublishOnly (build + checks) first
```

Configure the trusted publisher once in the package settings on npmjs.com (repository + workflow file name). This workflow was syntax-checked, not run.

### 7. Checklist before the first publish

- [ ] `files` whitelist; `npm pack --dry-run` shows no secrets, sources or tests
- [ ] `exports` covers every public entry point; `types` per format; `./package.json` exported
- [ ] `publint` and `attw --pack . --profile node16` are clean
- [ ] The packed tarball installs and works from ESM, CommonJS and TypeScript consumers
- [ ] `engines` set; `license`, `repository`, README with install and usage
- [ ] `prepublishOnly` builds and checks; publishing happens from CI with trusted publishing and 2FA
- [ ] Versioning plan: Changesets or release-please, CHANGELOG, pre-releases on the `next` tag

### Interview Qs

1. What does the `exports` field do? → It defines the package's public entry points, blocks deep imports (`ERR_PACKAGE_PATH_NOT_EXPORTED`), and selects files per condition (`import`/`require`/`types`).
2. How do you ship a package for both ESM and CommonJS? → Build both formats (tsup), use nested `import`/`require` conditions each with their own `types`, and verify with attw and a packed-tarball install.
3. Can CommonJS `require()` an ESM-only package? → On Node 20.19+/22.12+, yes, unless the module uses top-level `await`. On Node 18 and older it throws `ERR_REQUIRE_ESM`.
4. What is "Masquerading as ESM"? → CommonJS users get ESM type declarations (a single top-level `types`), so TypeScript treats the package as ESM-only and complains about `require`.
5. Why use a `files` whitelist? → Without it, npm publishes nearly everything, including `.env`, sources and tests.
6. What counts as a breaking change? → Removing or renaming exports or `exports` paths, behaviour or default changes, raising the minimum Node version, and new required peer dependencies.
7. What does `^0.2.3` allow? → `>=0.2.3 <0.3.0`: below 1.0 the minor version is treated as breaking.
8. How do you publish a beta without affecting users? → A pre-release version published with `--tag next`; users opt in with `@next`.
9. peerDependencies vs dependencies? → Peers are provided by the host app (a single shared copy, e.g. React); dependencies are installed for your package.
10. How do you publish securely? → From CI with trusted publishing (OIDC) and provenance, 2FA, no long-lived tokens, no install scripts.
11. How do you retract a bad release? → Publish a fix and `npm deprecate` the bad version. Unpublishing is limited, and version numbers can't be reused.

---

## 61. Monorepos: pnpm Workspaces, Turborepo & Shared Packages

A **monorepo** keeps several apps and libraries in one repository: an API, a worker, a web app, and the shared code between them. One PR can change a shared type and every app that uses it, and CI tests them together. The cost is tooling: builds must run in the right order, and only for what changed. Everything below was run with pnpm 9.12, Turborepo 2.11 and TypeScript 5.9.

| ✅ Good fit | ❌ Poor fit |
|---|---|
| Apps that share types, validation, UI components or clients | Unrelated projects that happen to belong to one company |
| Changes that often span frontend + backend + shared code | Teams that need independent release cadences and permissions |
| One team, or a few teams, owning related services | Very large orgs without investment in build tooling |

### 1. Layout

```text
acme/
├── pnpm-workspace.yaml
├── package.json            root: scripts + tooling only ("private": true)
├── turbo.json
├── tsconfig.json           references every project (tsc -b builds them in order)
├── apps/
│   ├── api/                @acme/api     depends on @acme/shared
│   └── worker/             @acme/worker  depends on @acme/shared
├── packages/
│   ├── shared/             @acme/shared  types + helpers, compiled to dist/
│   └── tsconfig/           @acme/tsconfig  the shared compiler settings
└── scripts/check-boundaries.mjs
```

The rule of thumb: **apps** are deployed and depend on **packages**; packages never depend on apps.

### 2. Workspace configuration

```yaml
# pnpm-workspace.yaml
packages:
  - "apps/*"
  - "packages/*"
```

```json
{
  "name": "acme-monorepo",
  "private": true,
  "packageManager": "pnpm@9.12.3",
  "scripts": {
    "build": "turbo run build",
    "test": "turbo run test",
    "typecheck": "tsc -b",
    "check:boundaries": "node scripts/check-boundaries.mjs"
  },
  "devDependencies": {
    "@types/node": "^20.19.43",
    "turbo": "^2.11.3",
    "typescript": "^5.9.3"
  }
}
```

**Shared compiler settings** live in their own tiny package, so every project `extends` the same file:

```json
{
  "compilerOptions": {
    "target": "es2022",
    "module": "nodenext",
    "moduleResolution": "nodenext",
    "strict": true,
    "composite": true,
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true,
    "skipLibCheck": true
  }
}
```

(`packages/tsconfig/base.json`; its `package.json` is just `{ "name": "@acme/tsconfig", "version": "0.0.0", "private": true, "files": ["base.json"] }`.)

**An internal package** (`packages/shared`), compiled to `dist/` so plain Node can run it:

```json
{
  "name": "@acme/shared",
  "version": "0.0.0",
  "private": true,
  "type": "module",
  "exports": { ".": { "types": "./dist/index.d.ts", "default": "./dist/index.js" } },
  "scripts": { "build": "tsc -b", "test": "node --test dist/" },
  "devDependencies": { "@acme/tsconfig": "workspace:*" }
}
```

```json
{ "extends": "@acme/tsconfig/base.json", "compilerOptions": { "rootDir": "src", "outDir": "dist" }, "include": ["src"] }
```

**An app** (`apps/api`) depends on it with the **`workspace:*`** protocol, which always links the local copy:

```json
{
  "name": "@acme/api",
  "version": "0.0.0",
  "private": true,
  "type": "module",
  "scripts": { "build": "tsc -b", "start": "node dist/main.js" },
  "dependencies": { "@acme/shared": "workspace:*" },
  "devDependencies": { "@acme/tsconfig": "workspace:*" },
  "files": ["dist"]
}
```

```json
{
  "extends": "@acme/tsconfig/base.json",
  "compilerOptions": { "rootDir": "src", "outDir": "dist" },
  "include": ["src"],
  "references": [{ "path": "../../packages/shared" }]
}
```

```ts
// apps/api/src/main.ts: imported like any npm package, never "../../packages/shared/src"
import { formatPaise, orderTotal, type Order } from "@acme/shared";

const orders: Order[] = [{ id: "o1", totalPaise: 1_999_900 }, { id: "o2", totalPaise: 49_900 }];
console.log(`api: total ${formatPaise(orderTotal(orders))}`);     // api: total ₹20,498.00
```

After `pnpm install`, `apps/api/node_modules/@acme/shared` is a **symlink** to `packages/shared`, so a change there is visible immediately. The root `tsconfig.json` (`{ "files": [], "references": [...all projects] }`) lets `tsc -b` type-check the whole repo in dependency order. A second run reports each project "is up to date" and does nothing (project references are covered in `typescript.md` → "Advanced TypeScript Features").

### 3. Running tasks

```bash
pnpm install                              # installs and links the whole workspace
pnpm -r build                             # every package, in dependency order: shared → worker, api
pnpm --filter @acme/api build             # one package
pnpm --filter "...@acme/shared" test      # shared + everything that DEPENDS on it (what a change could break)
pnpm --filter "@acme/api..." build        # api + everything IT depends on (what it needs to run)
pnpm --filter "./apps/*" build            # by folder
pnpm --filter @acme/worker add ms         # add a dependency to one package
pnpm add -D -w turbo                      # -w: add to the workspace root
```

Tested selections: `...@acme/shared` → shared, worker, api. `@acme/api...` → tsconfig, shared, api.

### 4. Why pnpm: no phantom dependencies

With **npm workspaces**, dependencies are hoisted into one root `node_modules`. When the worker declares `ms`, the API can `import ms` **without declaring it**, and it works by accident until the worker drops `ms` and the API breaks in production. With pnpm, each package only sees what it declares:

```text
worker (declares ms):        1m
api (doesn't declare ms):    ERR_MODULE_NOT_FOUND     ← pnpm
api (doesn't declare ms):    1m                        ← npm workspaces: a hidden bug
```

npm also doesn't understand `workspace:*` (`EUNSUPPORTEDPROTOCOL`); with npm workspaces you write `"*"`.

### 5. Turborepo: only rebuild what changed

`turbo` runs package scripts in dependency order, in parallel where possible, and **caches** each task's output keyed by a hash of its inputs (source files, dependencies' hashes, env vars you declare).

```json
{
  "$schema": "https://turbo.build/schema.json",
  "tasks": {
    "build": {
      "dependsOn": ["^build"],
      "outputs": ["dist/**", "tsconfig.tsbuildinfo"]
    },
    "test": {
      "dependsOn": ["build"]
    }
  }
}
```

- `"^build"` means "build my **dependencies** first"; plain `"build"` in `test` means "build **this** package first".
- `outputs` is what gets stored in the cache and **restored** on a cache hit.

What happened in the test repo:

| Change | shared | worker | api | Time |
|---|---|---|---|---|
| First run | build | build | build | a few seconds |
| Nothing changed | cached | cached | cached | 4 ms ("FULL TURBO") |
| Edited `apps/worker` only | cached | **build** | cached | — |
| Edited `packages/shared` | **build** | **build** | **build** | (dependents invalidated) |
| Deleted `apps/api/dist`, re-ran | cached | cached | cached | `dist/` **restored** from cache |

**Declare `outputs`.** Without it, a cache hit still says "FULL TURBO", but nothing is restored: `apps/api/dist` stayed **missing**, so a CI build "succeeds" and ships nothing.

**Keep `tsconfig.tsbuildinfo` in step with `dist/`.** After deleting `dist/` but not the `.tsbuildinfo` file, `tsc -b` reported every project "up to date" and **didn't rebuild**. Clean with `tsc -b --clean` (it removes both), and list both in turbo's `outputs`.

In CI, build and test only what a PR affects with `turbo run test --filter="...[origin/main]"`, and share the cache between machines and developers with **remote caching** (Vercel Remote Cache or a self-hosted server). Nx offers the same ideas plus code generators and module-boundary lint rules.

### 6. Enforce the boundaries

Nothing in a workspace stops a package from importing an app. Check it in CI:

```js
// scripts/check-boundaries.mjs: apps may depend on packages; packages and apps never depend on apps
import { existsSync, readFileSync, readdirSync } from "node:fs";
import { join } from "node:path";

const workspace = new Map();                                    // package name → { kind, pkg }
for (const [folder, kind] of [["apps", "app"], ["packages", "package"]]) {
  for (const dir of readdirSync(folder)) {
    const file = join(folder, dir, "package.json");
    if (!existsSync(file)) continue;
    const pkg = JSON.parse(readFileSync(file, "utf8"));
    workspace.set(pkg.name, { kind, pkg });
  }
}

const problems = [];
for (const [name, { kind, pkg }] of workspace) {
  const deps = { ...pkg.dependencies, ...pkg.devDependencies, ...pkg.peerDependencies };
  for (const dep of Object.keys(deps)) {
    if (workspace.get(dep)?.kind === "app") problems.push(`${name} (${kind}) must not depend on the app ${dep}`);
  }
}

if (problems.length > 0) {
  console.error(problems.join("\n"));
  process.exit(1);
}
console.log(`Boundaries OK (${workspace.size} workspace packages)`);
```

```text
$ pnpm check:boundaries
Boundaries OK (4 workspace packages)
# after adding "@acme/api" to packages/shared's dependencies:
@acme/shared (package) must not depend on the app @acme/api      (exit code 1)
```

Also ban relative imports that reach into another package (`../../packages/shared/src`) with ESLint's `import/no-relative-packages` rule. They bypass the package's `exports` and its build.

### 7. Deploying one app

A container for the API shouldn't contain the whole repo. **`pnpm deploy`** copies one package plus its production dependencies, with workspace packages copied in as real files instead of symlinks:

```bash
pnpm --filter @acme/api --prod deploy ../deploy-api
cd ../deploy-api && node dist/main.js     # api: total ₹20,498.00
```

With `"files": ["dist"]` in the app's `package.json`, the output is just `dist/`, `node_modules/` and `package.json`. Without it, `src/` and the tsconfig came along too. `--prod` leaves out devDependencies (no TypeScript in the image). Build first: `pnpm deploy` copies what's there; it doesn't build. Turborepo's `turbo prune @acme/api --docker` is the alternative, producing a pruned workspace for multi-stage Docker builds.

### 8. Good practices

- **One version of each external dependency** across the repo where possible (pnpm `catalog:` entries or a syncpack check), so apps don't drift apart.
- **Internal packages stay `"private": true`** and use `workspace:*`. Packages you publish get real versions with Changesets (`nodejs.md` → "Building & Publishing an npm Package").
- **CODEOWNERS per folder**, so the team owning `apps/api` reviews changes there.
- **Keep the root lean:** only tooling in the root `package.json`, never app dependencies.
- **Fast CI:** affected-only builds and tests plus remote caching. A monorepo whose CI rebuilds everything on every PR is slower than separate repos.

### Interview Qs

1. Monorepo vs polyrepo trade-offs? → Atomic cross-package changes, shared tooling and one CI vs build complexity, permissions and release independence.
2. What does `workspace:*` do? → It links the local workspace package instead of downloading from the registry (pnpm and Yarn; npm uses `"*"`).
3. What is a phantom dependency, and how does pnpm prevent it? → Importing a package you didn't declare, which works only because it's hoisted. pnpm's strict `node_modules` only exposes declared dependencies.
4. What does `"dependsOn": ["^build"]` mean in Turborepo? → Run `build` in all dependencies first.
5. How does Turborepo know what to rebuild? → It hashes each task's inputs, including its dependencies' hashes. Unchanged hashes are restored from the cache, including declared `outputs`.
6. Why must `outputs` be declared? → Otherwise a cache hit restores nothing, and the build directory can be missing even though turbo reports success.
7. `pnpm --filter "...pkg"` vs `"pkg..."`? → `...pkg` is the package plus its dependents; `pkg...` is the package plus its dependencies.
8. How do you run CI only for affected packages? → `turbo run test --filter="...[origin/main]"` (or `nx affected`), plus remote caching.
9. How do you ship a single app from a monorepo in Docker? → `pnpm deploy --prod` (or `turbo prune --docker`) to get just that app and its production dependencies.
10. How do you keep packages from depending on apps? → Boundary checks in CI (a script, Nx module-boundary rules, or ESLint), and no relative imports across packages.

---

## 62. Modern Node Features

- **Built-in `fetch`, `WebSocket` client, `AbortController`, `structuredClone`, Web Streams** (18–22).
- **`node --watch`** (auto-restart) and **`--env-file`**.
- **`node:test`** built-in test runner + `node --test --watch`, coverage.
- **Permission model** (`--permission`, `--allow-fs-read`).
- **`require(esm)`** (22+).
- **TypeScript type stripping** — run `.ts` files directly (`node app.ts`, Node 22.18+/23.6+ by default for erasable syntax).
- **`node:sqlite`** built-in SQLite module.
- **`util.parseArgs`, `util.styleText`**, `fs.glob`.
- **Single executable applications (SEA)**.
- `import.meta.dirname` / `import.meta.filename`.
- Even-numbered releases become **LTS** (use LTS in production).

---

## 63. System Design Basics for Backend Interviews

System design rounds test whether you can turn vague requirements into a **scalable, reliable architecture** and explain the **trade-offs**. There's no single right answer — clear reasoning matters most.

### 1. A framework for any design question (≈ 45 minutes)

1. **Clarify requirements** (5 min)
   - **Functional**: what must the system do? (shorten URLs, send messages, show a feed)
   - **Non-functional**: scale (users, requests/sec), latency, availability, consistency, durability, security, cost.
   - Out of scope: say explicitly what you're *not* designing.
2. **Estimate** (5 min): traffic, storage, bandwidth — to know if you need caching/sharding at all.
3. **API design**: main endpoints/events with inputs & outputs.
4. **Data model**: entities, relationships, access patterns → SQL or NoSQL, keys, indexes.
5. **High-level design**: boxes & arrows — clients, LB, services, DBs, caches, queues, CDN.
6. **Deep dives**: the 1–2 hardest parts (ID generation, fan-out, hot keys, consistency).
7. **Bottlenecks & trade-offs**: single points of failure, scaling limits, what you'd monitor, what you'd do at 10× scale.

### 2. Back-of-the-envelope estimation

```
QPS (average) = daily active users × actions per user per day / 86,400 (≈ 10^5 seconds)
Peak QPS      ≈ 2–5 × average
Storage/year  = writes per day × size per record × 365 (× replication factor)
Bandwidth     = QPS × response size
```

Example — 10M DAU, each creates 2 posts & reads 50 posts per day:
- Writes: 10M × 2 / 10^5 ≈ **200 writes/s** (peak ~1,000)
- Reads: 10M × 50 / 10^5 ≈ **5,000 reads/s** (peak ~20,000) → **read-heavy** (25:1) → caching + read replicas
- Storage: 20M posts/day × 1 KB ≈ 20 GB/day ≈ **7 TB/year** (+ media in object storage)

**Latency numbers to know (approximate)**

| Operation | Time |
|---|---|
| L1 cache / main memory reference | ~1 ns / ~100 ns |
| Read 1 MB sequentially from memory | ~10 µs |
| SSD random read | ~100 µs |
| Round trip within a data center | ~0.5 ms |
| Redis GET (same region) | ~0.5–1 ms |
| Simple indexed DB query | ~1–10 ms |
| Round trip across continents | ~100–150 ms |
| Read 1 MB from network (1 Gbps) | ~10 ms |

Takeaway: memory ≫ SSD ≫ network; avoid cross-region round trips on the hot path; cache aggressively.

### 3. Building blocks

#### Scaling & load balancing

- **Vertical scaling**: bigger machine — simple, has a ceiling and is a single point of failure.
- **Horizontal scaling**: more machines behind a **load balancer** — requires **stateless** services (sessions in Redis, files in object storage).
- **Load balancer**: L4 (TCP) or L7 (HTTP, can route by path/header); algorithms: round robin, least connections, IP hash (sticky); **health checks** remove bad instances; also does TLS termination.
- **Autoscaling** on CPU/latency/queue depth.

#### Caching layers

```
Browser cache → CDN → Reverse proxy cache → App cache (Redis) → DB buffer cache → DB
```

- Patterns: **cache-aside** (most common), read-through, write-through, write-behind.
- Invalidation: TTLs + explicit deletes on writes; versioned keys.
- Problems: **cache stampede** (many misses at once → locking/request coalescing/stale-while-revalidate), **hot keys** (replicate the key / local in-memory cache), **stale data** (short TTLs where freshness matters).
- Cache what's **read often, changes rarely**, and is expensive to compute.

#### Databases at scale

- **Replication (leader → followers)**: writes go to the leader, reads can go to **read replicas**. Watch **replication lag** — read-your-own-writes by reading from the leader right after a user's write.
- **Sharding / partitioning**: split data across servers by a **shard key** (user_id, tenant_id). Good key = even distribution + queries hit one shard. Bad key → **hot partitions**. **Consistent hashing** minimizes data movement when adding nodes.
- **SQL vs NoSQL**: SQL for relations, transactions, flexible queries; NoSQL (DynamoDB, Cassandra, MongoDB) for massive scale with known access patterns, flexible schemas, high write throughput.
- **Denormalize** for read performance (store computed counts, duplicate display data) — accept extra write work.
- **Indexes** for every hot query; **connection pooling** (PgBouncer) when many app instances connect.

#### Asynchronous processing: queues & events

- **Queues** (SQS, RabbitMQ, BullMQ/Redis) decouple producers from consumers, **absorb traffic spikes**, enable retries.
- **Event streams** (Kafka, Kinesis) — ordered, replayable logs; many consumers read the same events (analytics, search indexing, notifications).
- Delivery is usually **at-least-once** → consumers must be **idempotent** (dedupe by message ID).
- **Dead-letter queues** for messages that keep failing; alert on DLQ growth.
- Use async for anything the user doesn't need to wait for: emails, thumbnails, analytics, webhooks, search indexing.

#### Storage & CDN

- **Object storage** (S3/GCS/R2) for files/images/videos — cheap, durable; store only the URL/key in the DB.
- **CDN** for static assets & media (and cacheable API responses) close to users.

#### Consistency & correctness

- **CAP**: during a network partition, choose **consistency** (reject/queue some requests) or **availability** (serve possibly stale data).
- **Strong consistency**: everyone sees the latest write (bank balances, inventory reservations). **Eventual consistency**: replicas converge soon (likes count, feeds, profiles).
- **Idempotency keys** for retries on writes (payments, orders).
- **Distributed transactions** are hard → prefer single-DB transactions, the **outbox pattern** (write the event to an outbox table in the same transaction, publish it asynchronously), or **sagas** with compensating actions.

#### Reliability

- **Redundancy**: no single points of failure (multiple instances, multi-AZ DBs with automatic failover).
- **Timeouts, retries with backoff + jitter, circuit breakers, bulkheads** (isolate resources so one slow dependency can't take everything down).
- **Graceful degradation**: if recommendations are down, show the page without them.
- **Rate limiting & load shedding** to protect the system.
- **SLI/SLO/SLA**: measured indicator (p99 latency), internal target (99.9% of requests < 300 ms), external promise with penalties.

| Availability | Downtime per year |
|---|---|
| 99% ("two nines") | ~3.65 days |
| 99.9% | ~8.8 hours |
| 99.99% | ~53 minutes |
| 99.999% | ~5 minutes |

---

### 4. Design: URL Shortener (like bit.ly)

**Requirements**
- Functional: create a short URL for a long URL (optional custom alias, expiry); redirect short → long; basic click analytics.
- Non-functional: very **read-heavy** (~100:1), redirects **< 50 ms**, highly available, short codes unpredictable enough to not be enumerable (if privacy matters).

**Estimates**: 100M new URLs/month ≈ 40 writes/s; 100:1 reads → ~4,000 redirects/s (peak ~20k). 100M × 12 months × 5 years × ~500 bytes ≈ 3 TB.

**API**

```
POST /api/urls          { longUrl, customAlias?, expiresAt? }  → 201 { code, shortUrl }
GET  /{code}            → 302 Location: longUrl   (or 301)
GET  /api/urls/{code}/stats
```

**Short code generation** — 7 chars of base62 (`[0-9a-zA-Z]`) = 62⁷ ≈ **3.5 trillion** codes.

| Approach | Pros | Cons |
|---|---|---|
| Hash (MD5/SHA) of URL, take first 7 chars | Same URL → same code | Collisions must be checked & resolved |
| **Counter/ID → base62** (DB sequence, Snowflake IDs, or pre-allocated ID ranges per server) | No collisions, simple | Sequential codes are guessable (shuffle/encrypt the ID if needed) |
| Random 7 chars + uniqueness check | Unpredictable | Retry on collision (rare) |

```js
const ALPHABET = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";

function toBase62(num) {                 // num: BigInt or safe integer ID
  let n = BigInt(num), out = "";
  do { out = ALPHABET[Number(n % 62n)] + out; n /= 62n; } while (n > 0n);
  return out;
}
function fromBase62(str) {
  return [...str].reduce((n, ch) => n * 62n + BigInt(ALPHABET.indexOf(ch)), 0n);
}

toBase62(125);          // "21"
fromBase62("21");       // 125n
toBase62(62n ** 7n - 1n).length;      // 7 — the largest 7-char code (IDs below 62^7 ≈ 3.52 trillion)
toBase62(62n ** 7n).length;           // 8 — IDs from 62^7 upward need an 8th character
```

**Data model**: `urls(code PK, long_url, user_id, created_at, expires_at)`. A key-value lookup by `code` → any DB works; NoSQL (DynamoDB) or sharded SQL by `code` at huge scale.

**High-level design**

```
Client → CDN/LB → Redirect service ──► Redis cache (code → longUrl, LRU)
                        │ miss                     ▲
                        ▼                          │
                   URLs DB (replicated/sharded) ───┘
                        │
                  click event → Queue/Kafka → Analytics workers → Analytics store
```

**Deep dives**
- **Caching**: popular links are hit constantly → Redis cache-aside with LRU eviction; most redirects never touch the DB.
- **301 vs 302**: 301 (permanent) lets browsers cache → less load but **you lose click analytics**; 302 keeps every click visible.
- **Analytics**: don't write to the DB synchronously on each redirect — publish an event to a queue and aggregate asynchronously.
- **Abuse**: rate-limit creation, scan URLs for malware/phishing, block dangerous schemes (`javascript:`).
- **Expiry**: check `expires_at` on read + background cleanup job.

---

### 5. Design: Chat Application (like WhatsApp / Slack DMs)

**Requirements**
- Functional: 1:1 and group chat, online/last-seen presence, delivery & read receipts, message history, offline users get messages later + push notifications.
- Non-functional: low latency (< 200 ms delivery), message ordering per conversation, **no message loss**, huge concurrent connection counts.

**Key components**

```
Mobile/Web ◄──WebSocket──► Chat Gateway servers (hold connections)
                                │   ▲
               publish/route    ▼   │ deliver
                         Message service ──► Messages DB (partitioned by conversation_id)
                                │
                        Pub/Sub (Redis/Kafka) — routes messages to the gateway holding the recipient's socket
                                │
             Presence service (Redis: userId → gatewayId, lastSeen)     Push service (APNs/FCM) for offline users
```

**Message flow (1:1)**
1. Sender's client sends `{ tempId, conversationId, text }` over its WebSocket.
2. Gateway → Message service: validates, assigns a **server message ID + per-conversation sequence number**, **persists** it (durability before acknowledging).
3. Sends **ack** to the sender (`tempId → messageId`, single tick ✓).
4. Looks up the recipient's gateway in the **presence store**; publishes to that gateway via pub/sub → delivered over the recipient's socket.
5. Recipient's client acks delivery (double tick ✓✓) and later "read" (blue ticks) — receipts flow back the same way.
6. If the recipient is offline → **push notification**; on reconnect the client **syncs** all messages after its last known sequence number.

**Deep dives**
- **Scaling WebSockets**: each gateway holds ~100k+ connections; many gateways behind an L4 load balancer; a pub/sub layer routes messages between gateways (a user's socket lives on exactly one gateway).
- **Ordering**: rely on server-assigned per-conversation sequence numbers, not client clocks.
- **Delivery guarantees**: at-least-once delivery + client-side dedupe by message ID = effectively exactly-once display.
- **Storage**: write-heavy, append-only, read by conversation & time → wide-column DB (Cassandra/ScyllaDB) partitioned by `conversation_id`, clustered by message sequence; or Postgres partitioned tables at smaller scale.
- **Group chat**: fan-out on write to each member's inbox for small groups; for very large groups/channels, store once and let members pull (fan-out on read).
- **Presence**: heartbeat over the socket; Redis with TTL for online status; don't broadcast every presence change to everyone (only to open conversations/contacts, batched).
- **Media**: upload directly to object storage (pre-signed URL), send only the URL/metadata in the message.
- **Security**: TLS everywhere; end-to-end encryption (Signal protocol) if required — then the server only routes ciphertext.

---

### 6. Design sketch: News Feed (fan-out trade-off)

- **Fan-out on write (push)**: when a user posts, write the post ID into every follower's feed list (Redis). Reads are instant; writes are expensive for users with millions of followers.
- **Fan-out on read (pull)**: build the feed at read time by merging posts from followed users. Cheap writes, slow reads.
- **Hybrid** (what large social networks do): push for normal users, pull for celebrities, merge at read time; cache the first page of each feed; rank asynchronously.

### 7. Common trade-offs to talk about

| Decision | Trade-off |
|---|---|
| SQL vs NoSQL | Flexible queries & transactions vs horizontal scale & simple access patterns |
| Strong vs eventual consistency | Correctness vs latency/availability |
| Cache | Speed vs staleness & invalidation complexity |
| Sync vs async processing | Simplicity & immediate result vs resilience & throughput |
| Monolith vs microservices | Simplicity & speed early vs independent scaling/deploys later |
| Push vs pull (feeds, updates) | Fast reads vs cheap writes |
| Denormalization | Fast reads vs duplicated data & harder writes |
| 301 vs 302 redirect | Less load vs analytics |
| WebSocket vs SSE vs polling | Bi-directional & low latency vs simplicity |

### 8. System design best practices

- Start simple (a well-built monolith + Postgres + Redis handles a lot) and scale the **measured** bottleneck.
- Design for **failure**: timeouts, retries, idempotency, redundancy, graceful degradation.
- Keep services **stateless**; put state in databases, caches and object storage.
- Choose **data stores by access pattern**, not hype.
- Make everything **observable** (metrics, logs, traces, alerts) from day one.
- Prefer **async** for work the user doesn't wait on.
- Always state **assumptions and trade-offs** out loud in interviews.

### Interview Qs

1. Walk me through how you approach a system design question.
2. Estimate the QPS and storage for a service with 10M daily users.
3. Vertical vs horizontal scaling? Why must services be stateless to scale horizontally?
4. How do read replicas work? What is replication lag and how do you handle read-your-writes?
5. What is sharding? How do you choose a shard key? What is consistent hashing?
6. Where would you put caches in a system? How do you handle invalidation and stampedes?
7. When would you use a queue vs a direct API call? What is a dead-letter queue?
8. Explain CAP. Give examples where you'd choose consistency vs availability.
9. What is the outbox pattern and why is it needed?
10. Design a URL shortener. How do you generate short codes? 301 or 302?
11. Design a chat system. How are messages routed between WebSocket servers? How do you guarantee ordering and no loss?
12. Fan-out on write vs fan-out on read for a news feed?
13. What do 99.9% vs 99.99% availability mean in downtime?

---

## 64. Output-Based Questions

**Q1**
```js
console.log("A");
setTimeout(() => console.log("B"), 0);
setImmediate(() => console.log("C"));
process.nextTick(() => console.log("D"));
Promise.resolve().then(() => console.log("E"));
console.log("F");
```
> `A F D E` then `B C` (B/C order not guaranteed in main module; usually B then C).

**Q2**
```js
const fs = require("fs");
fs.readFile(__filename, () => {
  setTimeout(() => console.log("timeout"), 0);
  setImmediate(() => console.log("immediate"));
  process.nextTick(() => console.log("tick"));
});
```
> `tick immediate timeout`

**Q3**
```js
Promise.resolve().then(() => console.log("promise"));
process.nextTick(() => console.log("nextTick"));
```
> `nextTick promise`

**Q4**
```js
setTimeout(() => console.log("t1"), 0);
setTimeout(() => {
  console.log("t2");
  process.nextTick(() => console.log("tick in t2"));
}, 0);
setTimeout(() => console.log("t3"), 0);
```
> `t1 t2 tick in t2 t3`

**Q5**
```js
// a.js
module.exports = { x: 1 };
exports.y = 2;
// b.js
console.log(require("./a"));
```
> `{ x: 1 }` — `exports` still points to the old object.

**Q6**
```js
async function main() {
  console.log(1);
  await null;
  console.log(2);
}
main();
process.nextTick(() => console.log(3));
console.log(4);
```
> `1 4 3 2`

**Q7**
```js
const EventEmitter = require("events");
const e = new EventEmitter();
e.on("x", () => console.log("first"));
e.prependListener("x", () => console.log("zero"));
console.log("before");
e.emit("x");
console.log("after");
```
> `before zero first after` — emit is synchronous.

**Q8**
```js
const { Buffer } = require("buffer");
console.log(Buffer.from("héllo").length, "héllo".length);
```
> `6 5` — é takes 2 bytes in UTF-8.

---

## 65. Most Asked Interview Questions

### Core

1. **What is Node.js? Is it single-threaded?**
2. **Explain the event loop and its phases.**
3. **What is libuv? What uses the thread pool?**
4. **`process.nextTick` vs `setImmediate` vs `setTimeout(0)`.**
5. **Blocking vs non-blocking I/O; how to avoid blocking the event loop.**
6. **What is callback hell? How do promises/async-await help?**
7. **CommonJS vs ES Modules. `module.exports` vs `exports`.**
8. **How does `require` work? What is module caching?**
9. **What are streams? Types? Backpressure? `pipe` vs `pipeline`.**
10. **What is a Buffer?**
11. **What is EventEmitter? How are events handled?**
12. **What is `package.json` vs `package-lock.json`? Semver `^` vs `~`.**
13. **dependencies vs devDependencies vs peerDependencies.**
14. **npm vs npx.**
15. **What are global objects in Node? `__dirname` in ESM?**
16. **How to handle errors: sync, callbacks, promises, events, process-level?**
17. **`uncaughtException` vs `unhandledRejection`.**
18. **What is the REPL?** → Read-Eval-Print-Loop, run `node` with no args.

### Express / APIs

19. **What is Express? What is middleware? Types of middleware?**
20. **How does error-handling middleware work?**
21. **`app.use` vs `app.get`; `req.params` vs `req.query` vs `req.body`.**
22. **How to structure an Express project?**
23. **REST principles; PUT vs PATCH; idempotency; status codes.**
24. **REST vs GraphQL.**
25. **How do you validate requests?**
26. **How do you implement pagination, filtering, sorting?**
27. **What is CORS and how to enable it? What is a preflight request?**
28. **How to upload files?**

### Auth & Security

29. **Authentication vs authorization.**
30. **Session vs JWT; JWT structure; refresh tokens; revoking JWTs.**
31. **How to store passwords securely? Salt? bcrypt vs SHA256?**
32. **OAuth 2.0 flow.**
33. **How to secure a Node app?** → helmet, validation, rate limiting, parameterized queries, HTTPS, secrets management, dependency audits, CORS config, HttpOnly cookies.
34. **SQL/NoSQL injection, XSS, CSRF, IDOR — prevention.**
35. **Rate limiting algorithms.**

### Databases

36. **SQL vs NoSQL — when to choose which?**
37. **What are indexes? Trade-offs?**
38. **ACID; transactions in Mongo & SQL.**
39. **Embedding vs referencing in MongoDB; `populate`.**
40. **Aggregation pipeline.**
41. **N+1 problem.**
42. **Connection pooling.**
43. **ORM vs query builder vs raw SQL.**

### Scaling & Performance

44. **How to scale a Node app?** → cluster/PM2, horizontal scaling behind a load balancer, stateless design, caching, queues, DB optimization, CDN.
45. **Cluster vs worker threads vs child processes.**
46. **How to handle CPU-intensive tasks?**
47. **Caching strategies with Redis; cache invalidation.**
48. **How to find & fix memory leaks?**
49. **What is graceful shutdown?**
50. **WebSockets vs HTTP vs SSE vs polling.**
51. **Message queues — why & when?**
52. **Monolith vs microservices; API gateway; saga; circuit breaker.**
53. **How do you monitor & log a production Node app?**
54. **How to test Node APIs?**
55. **How to deploy a Node app? Docker basics; reverse proxy.**

### Quick answers

- **Why is Node good for real-time apps?** → Event-driven, handles many concurrent connections with low overhead.
- **Can Node do multithreading?** → Yes, via worker threads; libuv also uses threads internally.
- **What is `Zalgo`?** → APIs that are sometimes sync, sometimes async — unpredictable. Always be consistently async.
- **What is middleware chaining?** → Passing control with `next()` through a stack of functions.
- **How do you prevent callback hell?** → Promises, async/await, modularization, named functions.
- **What happens when you `require` a JSON file?** → Parsed and cached as an object.
- **Difference between `spawn` and `exec`?** → spawn streams output (no buffer limit, no shell by default); exec buffers output and uses a shell.
- **What is the default max heap size?** → Depends on system memory/version (commonly ~2–4GB on 64-bit); change with `--max-old-space-size`.

---

**End of Node.js notes.**
