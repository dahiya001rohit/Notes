# TypeScript — Complete Notes

> Every major TypeScript concept, each with an explanation, 2–3 examples and interview questions.
> Covers the type system, generics, advanced/utility types, classes, modules, config, and TS with React & Node.
> The **Most Asked Interview Questions** and **type challenges** are at the end.

---

## Table of Contents

1. [What is TypeScript](#1-what-is-typescript)
2. [Setup & Compilation](#2-setup--compilation)
3. [Basic Types](#3-basic-types)
4. [any, unknown, never, void](#4-any-unknown-never-void)
5. [Type Inference & Annotations](#5-type-inference--annotations)
6. [Arrays & Tuples](#6-arrays--tuples)
7. [Objects: type aliases & interfaces](#7-object-types)
8. [type vs interface](#8-type-vs-interface)
9. [Union & Intersection Types](#9-union--intersection-types)
10. [Literal Types & `as const`](#10-literal-types--as-const)
11. [Type Narrowing & Type Guards](#11-type-narrowing--type-guards)
12. [Discriminated Unions & Exhaustiveness](#12-discriminated-unions)
13. [Functions](#13-functions)
14. [Function Overloads](#14-function-overloads)
15. [Enums](#15-enums)
16. [Generics](#16-generics)
17. [Generic Constraints & Defaults](#17-generic-constraints--defaults)
18. [keyof, typeof, Indexed Access Types](#18-keyof-typeof-indexed-access)
19. [Mapped Types](#19-mapped-types)
20. [Conditional Types & `infer`](#20-conditional-types--infer)
21. [Template Literal Types](#21-template-literal-types)
22. [Utility Types (all built-ins + implementations)](#22-utility-types)
23. [Type Assertions, Non-null `!`, `satisfies`](#23-type-assertions-non-null--satisfies)
24. [Classes in TS](#24-classes)
25. [Abstract Classes & Interfaces with Classes](#25-abstract-classes)
26. [Index Signatures & Record](#26-index-signatures)
27. [Readonly & Immutability](#27-readonly--immutability)
28. [Modules, Namespaces, Declaration Files (.d.ts)](#28-modules-namespaces-declaration-files)
29. [Declaration Merging & Module Augmentation](#29-declaration-merging--module-augmentation)
30. [Decorators](#30-decorators)
31. [tsconfig.json explained](#31-tsconfigjson)
32. [Structural Typing, Variance, Excess Property Checks](#32-structural-typing)
33. [TypeScript with React](#33-typescript-with-react)
34. [Typing React Components: Advanced Patterns](#34-typing-react-components-advanced-patterns)
35. [TypeScript with Node & Express](#35-typescript-with-node--express)
36. [Runtime Validation with Zod](#36-runtime-validation-with-zod)
37. [End-to-End Type Safety: Shared Schemas, tRPC & OpenAPI Codegen](#37-end-to-end-type-safety-shared-schemas-trpc--openapi-codegen)
38. [Branded Types & Other Patterns](#38-patterns)
39. [Advanced TypeScript Features](#39-advanced-typescript-features)
40. [Production TypeScript Best Practices](#40-production-typescript-best-practices)
41. [Common Errors & Fixes](#41-common-errors--fixes)
42. [Type Challenges](#42-type-challenges)
43. [Most Asked Interview Questions](#43-most-asked-interview-questions)

---

## 1. What is TypeScript

**TypeScript** is a **statically typed superset of JavaScript** by Microsoft. Any valid JS is valid TS. TS code compiles (transpiles) to plain JavaScript; **types are erased at runtime**.

Benefits:
- Catch bugs at **compile time** (typos, wrong args, null access).
- Great editor tooling: autocomplete, refactors, go-to-definition.
- Self-documenting code; safer large-scale refactoring.
- Modern JS features compiled down to older targets.

```ts
// JS: fails at runtime
function area(r) { return Math.PI * r * r; }
area("10"); // "10" * "10" works by coercion... bugs hide

// TS: fails at compile time
function areaTs(r: number): number { return Math.PI * r * r; }
areaTs("10"); // ❌ Argument of type 'string' is not assignable to parameter of type 'number'.
```

```ts
const user = { name: "Rohit", age: 25 };
user.nmae; // ❌ Property 'nmae' does not exist. Did you mean 'name'?
```

### Static vs dynamic typing

- **Static** (TS, Java): types checked at compile time.
- **Dynamic** (JS, Python): types checked at runtime.
- TS is also **gradual**: you can opt out with `any`.

**Interview Qs**
- Does TS run in the browser? → No, it's compiled to JS (or types are stripped by tools like esbuild/SWC/Node).
- Do types exist at runtime? → No. For runtime checks use type guards / validation (Zod).
- TS vs JS? → TS = JS + static types + tooling.

---

## 2. Setup & Compilation

```bash
npm i -D typescript
npx tsc --init          # creates tsconfig.json
npx tsc                 # compile project
npx tsc --noEmit        # type-check only
npx tsc -w              # watch mode
npx tsx src/index.ts    # run TS directly (dev)
node src/index.ts       # Node 23.6+/22.18+ strips erasable types natively
```

- **tsc** type-checks AND emits JS.
- **esbuild / SWC / Babel / Vite** only strip types (fast) — no type checking → run `tsc --noEmit` in CI.

---

## 3. Basic Types

```ts
let username: string = "Rohit";
let age: number = 25;          // int & float are both number
let big: bigint = 100n;
let isActive: boolean = true;
let nothing: null = null;
let notSet: undefined = undefined;
let id: symbol = Symbol("id");

let anything: any = 4;         // opt out of type checking
let unsure: unknown = "maybe"; // safe any
function log(): void {}        // returns nothing
function fail(): never { throw new Error(); } // never returns

let obj: object = { a: 1 };    // any non-primitive
let fn: Function = () => {};   // avoid; use specific signatures
```

### Example — object & function types inline

```ts
let point: { x: number; y: number } = { x: 1, y: 2 };
let greet: (name: string) => string = (n) => `Hi ${n}`;
let maybeName: string | null = null;
```

### Primitive wrappers — avoid

```ts
let s1: string = "a";  // ✅
let s2: String = "a";  // ❌ wrapper object type — don't use
```

---

## 4. any, unknown, never, void

### any

Disables type checking. Spreads silently ("any is contagious"). Avoid; use `unknown` instead.

```ts
let a: any = "hello";
a.foo.bar();       // no error at compile time, crashes at runtime
let n: number = a; // any is assignable to everything
```

### unknown

Type-safe counterpart of `any`: you can assign anything to it, but you **must narrow** before using it.

```ts
let value: unknown = JSON.parse('{"x":1}');
value.x;                         // ❌ 'value' is of type 'unknown'
if (typeof value === "object" && value !== null && "x" in value) {
  console.log(value.x);          // ✅ narrowed
}

function handleError(err: unknown) {
  if (err instanceof Error) return err.message;
  return String(err);
}
try { /* ... */ } catch (e) { handleError(e); } // catch variables are `unknown` with strict mode
```

### never

A value that **never occurs**. Used for:
1. Functions that never return (throw / infinite loop).
2. Exhaustiveness checks.
3. Impossible branches in conditional types (filtering).

```ts
function throwError(msg: string): never {
  throw new Error(msg);
}

type Shape = "circle" | "square";
function area(s: Shape) {
  switch (s) {
    case "circle": return 1;
    case "square": return 2;
    default:
      const _exhaustive: never = s; // error if a new Shape is added and not handled
      return _exhaustive;
  }
}

type NonString<T> = T extends string ? never : T;
type R = NonString<string | number | boolean>; // number | boolean
```

### void

Function returns nothing useful (`undefined`).

```ts
function logMsg(msg: string): void { console.log(msg); }

// A void-returning callback type allows functions that return values:
const nums: number[] = [];
[1, 2].forEach((n) => nums.push(n)); // push returns number, still OK
```

### Comparison

| | Assign anything to it | Use it without checks | Assignable to others |
|---|---|---|---|
| `any` | ✅ | ✅ | ✅ (everything) |
| `unknown` | ✅ | ❌ | only `any`/`unknown` |
| `never` | ❌ (nothing) | — | ✅ (everything) |
| `void` | `undefined` | — | — |

**Interview Qs**
- any vs unknown? → unknown forces narrowing; any disables checks.
- What is never used for? (above)
- void vs undefined? → void = "ignore the return value"; undefined is an actual value type.

---

## 5. Type Inference & Annotations

TS **infers** types when you don't write them. Annotate where inference can't help (function params, empty arrays, public APIs).

```ts
let count = 5;            // inferred: number
const name = "Rohit";     // inferred: "Rohit" (literal, because const)
let arr = [1, 2, 3];      // number[]
let mixed = [1, "a"];     // (string | number)[]
const user = { id: 1, name: "A" }; // { id: number; name: string }

function add(a: number, b: number) { return a + b; } // return type inferred: number

const nums = [1, 2, 3].map((n) => n * 2); // number[] — callback param inferred (contextual typing)
window.addEventListener("click", (e) => e.clientX); // e: MouseEvent (contextual)
```

```ts
let items = [];           // any[] (implicit) — annotate!
let items2: string[] = [];

let x;                    // any
x = 5;                    // evolves to number (with noImplicitAny it's still tracked)
```

### Widening

```ts
let a = "hello";        // string (widened, since let can change)
const b = "hello";      // "hello" literal
const obj = { status: "ok" }; // { status: string } — properties widen
const obj2 = { status: "ok" } as const; // { readonly status: "ok" }
```

**Best practice**: annotate function parameters and exported function return types; let TS infer locals.

---

## 6. Arrays & Tuples

### Arrays

```ts
let names: string[] = ["a", "b"];
let scores: Array<number> = [1, 2];
let matrix: number[][] = [[1, 2], [3, 4]];
let users: { id: number; name: string }[] = [];
let ro: readonly string[] = ["x"];   // ReadonlyArray<string>
ro.push("y");                         // ❌
```

### Tuples

Fixed-length arrays with known types at each position.

```ts
let pair: [string, number] = ["age", 25];
pair[0].toUpperCase();
pair = [25, "age"];         // ❌ order matters

// Named & optional & rest elements
type Point3D = [x: number, y: number, z?: number];
type StringsThenNumber = [...string[], number];
const p: Point3D = [1, 2];

// Returning tuples (like React's useState)
function useCounter(): [number, () => void] {
  let c = 0;
  return [c, () => c++];
}
const [value, inc] = useCounter();

// readonly tuple
const rgb: readonly [number, number, number] = [255, 0, 0];
```

```ts
// Without annotation, a returned array is inferred as a union array:
function bad() { return ["a", 1]; }        // (string | number)[]
function good() { return ["a", 1] as const; } // readonly ["a", 1]
```

---

## 7. Object Types

### Type alias

```ts
type User = {
  readonly id: number;        // can't be reassigned
  name: string;
  email?: string;             // optional -> string | undefined
  address: {
    city: string;
    zip: string;
  };
  greet(): string;            // method
  onLogin: (date: Date) => void;
};

const u: User = {
  id: 1,
  name: "Rohit",
  address: { city: "Delhi", zip: "110001" },
  greet() { return "hi"; },
  onLogin: () => {},
};
u.id = 2;          // ❌ readonly
u.email?.toLowerCase();
```

### Interface

```ts
interface Product {
  id: number;
  title: string;
  price: number;
  tags?: string[];
}

interface DigitalProduct extends Product {   // extension
  downloadUrl: string;
}

interface Timestamps { createdAt: Date; updatedAt: Date }
interface Post extends Product, Timestamps {} // multiple extension
```

### Optional properties & `exactOptionalPropertyTypes`

```ts
type Opts = { debug?: boolean };
const o: Opts = { debug: undefined }; // allowed by default; error with exactOptionalPropertyTypes
```

---

## 8. type vs interface

| Feature | `type` | `interface` |
|---|---|---|
| Object shapes | ✅ | ✅ |
| Primitives, unions, tuples, function types | ✅ `type ID = string \| number` | ❌ (objects only) |
| Extend | `&` intersection | `extends` (better error messages, cached) |
| **Declaration merging** | ❌ duplicate identifier | ✅ same-name interfaces merge |
| Mapped / conditional types | ✅ | ❌ |
| `implements` in classes | ✅ (if object type) | ✅ |
| Computed/template literal keys | ✅ | limited |

```ts
// Only type can do these
type ID = string | number;
type Pair = [number, number];
type Handler = (e: Event) => void;
type Keys = keyof User;
type Partialize<T> = { [K in keyof T]?: T[K] };

// Only interface merges
interface Window { myGlobal: string }   // adds to the built-in Window
interface Box { width: number }
interface Box { height: number }        // Box = { width; height }

// Extending both ways
interface A { a: string }
type B = A & { b: number };
interface C extends B { c: boolean }    // interface can extend a type alias (object type)
```

**Rule of thumb**: `interface` for public object shapes/APIs that may be extended (and for libraries); `type` for unions, tuples, functions, and type-level programming. Be consistent in a codebase.

---

## 9. Union & Intersection Types

### Union `A | B` — value is **one of** the types

```ts
type Status = "idle" | "loading" | "success" | "error";
let id: string | number;

function printId(id: string | number) {
  // only members common to both are allowed without narrowing
  console.log(id.toString());
  if (typeof id === "string") console.log(id.toUpperCase());
  else console.log(id.toFixed(2));
}

type Result = { ok: true; data: string } | { ok: false; error: Error };
```

### Intersection `A & B` — value has **all** properties of both

```ts
type HasName = { name: string };
type HasAge = { age: number };
type Person = HasName & HasAge;
const p: Person = { name: "A", age: 1 };

type WithTimestamps<T> = T & { createdAt: Date; updatedAt: Date };
type DBUser = WithTimestamps<{ id: number; email: string }>;

type Impossible = string & number; // never
```

```ts
// Conflicting property types
type X = { a: string } & { a: number }; // a: never  -> object is unusable
```

**Interview Q**: Union vs intersection? → Union = either (fewer guaranteed props); intersection = both (more props).

---

## 10. Literal Types & `as const`

A literal type is an exact value as a type.

```ts
let direction: "up" | "down" | "left" | "right";
direction = "up";      // ✅
direction = "north";   // ❌

type Dice = 1 | 2 | 3 | 4 | 5 | 6;
type Bool = true;

function setAlign(align: "left" | "center" | "right") {}
```

### `as const` — deep readonly literal inference

```ts
const config = {
  env: "prod",
  ports: [80, 443],
} as const;
// { readonly env: "prod"; readonly ports: readonly [80, 443] }

// Derive a union from an array (enum alternative)
const ROLES = ["admin", "editor", "viewer"] as const;
type Role = (typeof ROLES)[number]; // "admin" | "editor" | "viewer"

const COLORS = { primary: "#00f", danger: "#f00" } as const;
type ColorName = keyof typeof COLORS;              // "primary" | "danger"
type ColorValue = (typeof COLORS)[ColorName];      // "#00f" | "#f00"
```

### Literal inference gotcha

```ts
const req = { url: "/api", method: "GET" };
function send(url: string, method: "GET" | "POST") {}
send(req.url, req.method); // ❌ method is `string`
// fixes:
const req2 = { url: "/api", method: "GET" } as const;
const req3 = { url: "/api", method: "GET" as const };
```

---

## 11. Type Narrowing & Type Guards

**Narrowing** = refining a broad type to a more specific one inside a code branch, via control-flow analysis.

### Built-in narrowing techniques

```ts
function demo(x: string | number | string[] | null | Date) {
  // typeof
  if (typeof x === "string") x.toUpperCase();

  // truthiness
  if (x) { /* excludes null, "" , 0 */ }

  // equality
  if (x === null) return;

  // Array.isArray
  if (Array.isArray(x)) x.join(",");

  // instanceof
  if (x instanceof Date) x.getFullYear();
}

// `in` operator
type Fish = { swim: () => void };
type Bird = { fly: () => void };
function move(a: Fish | Bird) {
  if ("swim" in a) a.swim();
  else a.fly();
}
```

### Custom type guard (type predicate `x is T`)

```ts
interface Cat { meow(): void; kind: "cat" }
interface Dog { bark(): void; kind: "dog" }

function isCat(pet: Cat | Dog): pet is Cat {
  return (pet as Cat).meow !== undefined;
}

function speak(pet: Cat | Dog) {
  if (isCat(pet)) pet.meow();
  else pet.bark();
}

// Filtering nulls with a guard
const values = [1, null, 2, undefined, 3];
const clean = values.filter((v): v is number => v != null); // number[]
// TS 5.5+ infers this predicate automatically for simple arrow functions
```

### Assertion functions

```ts
function assertIsString(val: unknown): asserts val is string {
  if (typeof val !== "string") throw new TypeError("Not a string");
}
function assert(cond: unknown, msg?: string): asserts cond {
  if (!cond) throw new Error(msg);
}

function process(input: unknown) {
  assertIsString(input);
  input.toUpperCase(); // narrowed to string after the call
}
```

### Type guard for API data

```ts
interface User { id: number; name: string }
function isUser(x: unknown): x is User {
  return typeof x === "object" && x !== null &&
    typeof (x as any).id === "number" && typeof (x as any).name === "string";
}
const data: unknown = await fetch("/api/me").then((r) => r.json());
if (isUser(data)) console.log(data.name);
```

**Interview Qs**
- What is a type guard? → A runtime check that narrows a type in a branch (typeof, instanceof, in, predicates).
- `x is T` vs `asserts x is T`? → Predicate returns boolean for `if`; assertion throws and narrows after the call.

---

## 12. Discriminated Unions

A union of object types sharing a **common literal property** (the discriminant / tag). Switching on it narrows perfectly. One of the most useful TS patterns.

### Example 1 — shapes

```ts
type Circle = { kind: "circle"; radius: number };
type Square = { kind: "square"; side: number };
type Rect = { kind: "rect"; width: number; height: number };
type Shape = Circle | Square | Rect;

function area(s: Shape): number {
  switch (s.kind) {
    case "circle": return Math.PI * s.radius ** 2;
    case "square": return s.side ** 2;
    case "rect": return s.width * s.height;
    default: {
      const _never: never = s; // compile error if a new Shape kind is unhandled
      throw new Error(`Unknown shape: ${_never}`);
    }
  }
}
```

### Example 2 — async state (no impossible states)

```ts
type RequestState<T> =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: T }
  | { status: "error"; error: string };

function render(state: RequestState<string[]>) {
  if (state.status === "success") return state.data.join(", "); // data only exists here
  if (state.status === "error") return state.error;
  return "…";
}
```

### Example 3 — reducer actions

```ts
type Action =
  | { type: "add"; item: { id: string; name: string } }
  | { type: "remove"; id: string }
  | { type: "clear" };

function reducer(state: { id: string; name: string }[], action: Action) {
  switch (action.type) {
    case "add": return [...state, action.item];
    case "remove": return state.filter((i) => i.id !== action.id);
    case "clear": return [];
  }
}
```

### Result type pattern (errors as values)

```ts
type Result<T, E = Error> = { ok: true; value: T } | { ok: false; error: E };

function parseAge(input: string): Result<number, string> {
  const n = Number(input);
  return Number.isInteger(n) && n >= 0 ? { ok: true, value: n } : { ok: false, error: "Invalid age" };
}
const r = parseAge("25");
if (r.ok) console.log(r.value + 1);
else console.error(r.error);
```

---

## 13. Functions

```ts
// Declaration
function add(a: number, b: number): number { return a + b; }

// Arrow with type
const sub = (a: number, b: number): number => a - b;

// Function type alias
type MathOp = (a: number, b: number) => number;
const mul: MathOp = (a, b) => a * b; // params inferred

// Call signature in an interface/object type (functions with properties)
interface Logger {
  (msg: string): void;
  level: "info" | "debug";
}

// Construct signature
type Ctor<T> = new (...args: any[]) => T;
```

### Optional, default & rest parameters

```ts
function greet(name: string, greeting?: string) {       // greeting: string | undefined
  return `${greeting ?? "Hello"}, ${name}`;
}
function greet2(name: string, greeting = "Hello") {}    // inferred string, optional
function sum(...nums: number[]): number { return nums.reduce((a, b) => a + b, 0); }

// Destructured parameters
function createUser({ name, age = 18 }: { name: string; age?: number }) {}
```

### `this` parameter

```ts
interface Button { label: string; onClick(this: Button): void }
function handler(this: HTMLButtonElement, e: MouseEvent) { this.disabled = true; }
```

### Callbacks & void

```ts
function fetchData(cb: (err: Error | null, data?: string) => void) {}
```

### Generic functions (see Section 16)

```ts
function first<T>(arr: T[]): T | undefined { return arr[0]; }
```

---

## 14. Function Overloads

Multiple **call signatures** for one implementation — when return type depends on the argument types in a way unions can't express.

```ts
function parse(input: string): string[];
function parse(input: number): number[];
function parse(input: string | number): string[] | number[] {
  return typeof input === "string" ? input.split(",") : [input];
}
const a = parse("a,b"); // string[]
const b = parse(5);     // number[]
parse(true);            // ❌ no matching overload
```

```ts
function createElement(tag: "a"): HTMLAnchorElement;
function createElement(tag: "canvas"): HTMLCanvasElement;
function createElement(tag: string): HTMLElement;
function createElement(tag: string): HTMLElement {
  return document.createElement(tag);
}
```

```ts
// Often a generic/conditional type is cleaner than overloads:
function wrap<T extends string | number>(x: T): T extends string ? string[] : number[] {
  return (typeof x === "string" ? [x] : [x]) as any;
}
```

Rules: the implementation signature isn't callable from outside; order overloads from most specific to least.

---

## 15. Enums

Named set of constants.

### Numeric enum

```ts
enum Direction { Up, Down, Left, Right }          // 0,1,2,3
enum Status { Active = 1, Inactive, Banned }       // 1,2,3
Direction.Up;          // 0
Direction[0];          // "Up"  (reverse mapping — numeric enums only)
```

### String enum

```ts
enum Role {
  Admin = "ADMIN",
  User = "USER",
}
function check(r: Role) { if (r === Role.Admin) {} }
check(Role.Admin);
check("ADMIN"); // ❌ string enums are nominal-ish
```

### const enum

```ts
const enum Color { Red = "RED", Green = "GREEN" }
const c = Color.Red; // inlined as "RED" — no runtime object
```

### Enums generate runtime code

```js
// enum Direction { Up, Down } compiles to:
var Direction;
(function (Direction) {
  Direction[Direction["Up"] = 0] = "Up";
  Direction[Direction["Down"] = 1] = "Down";
})(Direction || (Direction = {}));
```

### Modern alternative: union + `as const` object

```ts
const ROLE = { Admin: "ADMIN", User: "USER" } as const;
type Role2 = (typeof ROLE)[keyof typeof ROLE]; // "ADMIN" | "USER"
function setRole(r: Role2) {}
setRole(ROLE.Admin);
setRole("USER"); // ✅ plain strings allowed
```

Prefer unions/`as const` objects: no runtime surprises, tree-shakeable, works with `erasableSyntaxOnly` / Node type stripping (enums are NOT erasable syntax).

**Interview Qs**
- Enum vs union type? (above)
- What is a const enum? → Inlined at compile time; no generated object.

---

## 16. Generics

**Generics** let you write reusable code that works with **many types** while keeping type safety — "type parameters" like function parameters but for types.

### Example 1 — identity & arrays

```ts
function identity<T>(value: T): T { return value; }
identity<string>("hi"); // explicit
identity(42);           // inferred T = number

function last<T>(arr: T[]): T | undefined { return arr[arr.length - 1]; }
const l = last([1, 2, 3]);       // number | undefined
const s = last(["a", "b"]);      // string | undefined

// vs any: loses type info
function lastAny(arr: any[]): any { return arr.at(-1); }
```

### Example 2 — generic interfaces & types

```ts
interface ApiResponse<T> {
  data: T;
  status: number;
  message?: string;
}
type User = { id: number; name: string };

async function getJson<T>(url: string): Promise<T> {
  const res = await fetch(url);
  if (!res.ok) throw new Error(res.statusText);
  return res.json() as Promise<T>;
}
const res = await getJson<ApiResponse<User[]>>("/api/users");
res.data[0].name;

type Paginated<T> = { items: T[]; page: number; total: number };
type Nullable<T> = T | null;
```

### Example 3 — generic classes

```ts
class Stack<T> {
  #items: T[] = [];
  push(item: T) { this.#items.push(item); }
  pop(): T | undefined { return this.#items.pop(); }
  peek(): T | undefined { return this.#items.at(-1); }
  get size() { return this.#items.length; }
}
const s1 = new Stack<number>();
s1.push(1);
s1.push("2"); // ❌

class Cache<K, V> {
  private map = new Map<K, V>();
  get(k: K) { return this.map.get(k); }
  set(k: K, v: V) { this.map.set(k, v); return this; }
}
```

### Multiple type params

```ts
function pair<A, B>(a: A, b: B): [A, B] { return [a, b]; }
function mapObj<T, U>(obj: Record<string, T>, fn: (v: T) => U): Record<string, U> {
  return Object.fromEntries(Object.entries(obj).map(([k, v]) => [k, fn(v)]));
}
```

### Generic React-style hook

```ts
function useLocalState<T>(key: string, initial: T): [T, (v: T) => void] {
  let value: T = initial;
  return [value, (v) => { value = v; }];
}
const [theme, setTheme] = useLocalState("theme", "light"); // T = string
```

**Interview Qs**
- Why generics over any? → Keep the relationship between input and output types.
- Can you have generic arrow functions in .tsx? → Yes: `const f = <T,>(x: T) => x;` (comma avoids JSX ambiguity).

---

## 17. Generic Constraints & Defaults

### Constraints with `extends`

```ts
function getLength<T extends { length: number }>(x: T): number {
  return x.length;
}
getLength("hello");   // ✅
getLength([1, 2]);    // ✅
getLength(10);        // ❌ number has no length

// keyof constraint — type-safe property access
function getProp<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}
const user = { name: "Rohit", age: 25 };
getProp(user, "name"); // string
getProp(user, "age");  // number
getProp(user, "email"); // ❌ "email" not in keyof user

// Merge two objects
function merge<A extends object, B extends object>(a: A, b: B): A & B {
  return { ...a, ...b };
}
```

### Defaults

```ts
interface ApiResponse<T = unknown> { data: T; status: number }
const r: ApiResponse = { data: "anything", status: 200 }; // T = unknown

type EventHandler<E extends Event = MouseEvent> = (e: E) => void;
```

### `const` type parameters (TS 5.0)

```ts
function routes<const T extends readonly string[]>(r: T) { return r; }
const r2 = routes(["/home", "/about"]); // readonly ["/home", "/about"] instead of string[]
```

### `NoInfer` (TS 5.4)

```ts
function createFSM<S extends string>(states: S[], initial: NoInfer<S>) {}
createFSM(["idle", "loading"], "idle");   // ✅
createFSM(["idle", "loading"], "done");   // ❌ (without NoInfer, "done" would widen S)
```

---

## 18. keyof, typeof, Indexed Access

### keyof — union of an object type's keys

```ts
type User = { id: number; name: string; email: string };
type UserKeys = keyof User; // "id" | "name" | "email"

type ArrKeys = keyof string[]; // number | "length" | "push" | ...
type Dict = { [k: string]: number };
type DictKeys = keyof Dict; // string | number
```

### typeof (type context) — get the type of a value

```ts
const settings = { theme: "dark", fontSize: 14, notifications: true };
type Settings = typeof settings; // { theme: string; fontSize: number; notifications: boolean }

function createUser() { return { id: 1, name: "A", roles: ["admin"] }; }
type CreatedUser = ReturnType<typeof createUser>;

const handlers = { onClick() {}, onHover() {} };
type HandlerName = keyof typeof handlers; // "onClick" | "onHover"
```

### Indexed access types `T[K]`

```ts
type User2 = { id: number; profile: { bio: string; links: string[] } };
type Profile = User2["profile"];               // { bio; links }
type Links = User2["profile"]["links"];        // string[]
type IdOrProfile = User2["id" | "profile"];    // number | {...}

const users = [{ id: 1, name: "a" }];
type OneUser = (typeof users)[number];          // { id: number; name: string }

type Tuple = [string, number];
type Second = Tuple[1];                          // number
```

---

## 19. Mapped Types

Create new types by **transforming each property** of another type: `{ [K in Keys]: ... }`.

### Example 1 — rebuilding built-ins

```ts
type MyPartial<T> = { [K in keyof T]?: T[K] };
type MyRequired<T> = { [K in keyof T]-?: T[K] };           // -? removes optional
type MyReadonly<T> = { readonly [K in keyof T]: T[K] };
type Mutable<T> = { -readonly [K in keyof T]: T[K] };       // -readonly removes readonly
type Nullable<T> = { [K in keyof T]: T[K] | null };
```

### Example 2 — key remapping with `as`

```ts
type Getters<T> = {
  [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};
type Person = { name: string; age: number };
type PersonGetters = Getters<Person>;
// { getName: () => string; getAge: () => number }

// Filter keys by value type
type PickByType<T, V> = { [K in keyof T as T[K] extends V ? K : never]: T[K] };
type StringProps = PickByType<{ a: string; b: number; c: string }, string>; // { a: string; c: string }

// Remove a key
type RemoveKind<T> = { [K in keyof T as Exclude<K, "kind">]: T[K] };
```

### Example 3 — form state from a model

```ts
type FormErrors<T> = { [K in keyof T]?: string };
type Touched<T> = { [K in keyof T]: boolean };
type LoginForm = { email: string; password: string };
const errors: FormErrors<LoginForm> = { email: "Required" };

// Event handler map
type EventMap = { click: MouseEvent; keydown: KeyboardEvent };
type Handlers = { [E in keyof EventMap as `on${Capitalize<E>}`]: (e: EventMap[E]) => void };
// { onClick: (e: MouseEvent) => void; onKeydown: (e: KeyboardEvent) => void }
```

---

## 20. Conditional Types & `infer`

`T extends U ? X : Y` — like a ternary at the type level.

### Example 1 — basics

```ts
type IsString<T> = T extends string ? true : false;
type A = IsString<"hi">;  // true
type B = IsString<42>;    // false

type TypeName<T> =
  T extends string ? "string" :
  T extends number ? "number" :
  T extends boolean ? "boolean" :
  T extends Function ? "function" : "object";
```

### Distributive conditional types

When `T` is a naked type parameter and receives a union, the condition is applied **to each member**.

```ts
type ToArray<T> = T extends any ? T[] : never;
type R1 = ToArray<string | number>; // string[] | number[]

// Prevent distribution by wrapping in []
type ToArrayND<T> = [T] extends [any] ? T[] : never;
type R2 = ToArrayND<string | number>; // (string | number)[]

type MyExclude<T, U> = T extends U ? never : T;
type R3 = MyExclude<"a" | "b" | "c", "a">; // "b" | "c"
```

### Example 2 — `infer` (extract a type from inside another)

```ts
type MyReturnType<T> = T extends (...args: any[]) => infer R ? R : never;
type MyParameters<T> = T extends (...args: infer P) => any ? P : never;
type UnwrapPromise<T> = T extends Promise<infer U> ? UnwrapPromise<U> : T; // recursive (like Awaited)
type ElementType<T> = T extends (infer E)[] ? E : T;
type FirstArg<T> = T extends (first: infer F, ...rest: any[]) => any ? F : never;

type R4 = MyReturnType<() => Promise<number>>;   // Promise<number>
type R5 = UnwrapPromise<Promise<Promise<string>>>; // string
type R6 = ElementType<string[]>;                  // string
```

### Example 3 — infer in template literals & tuples

```ts
type Head<T extends any[]> = T extends [infer H, ...any[]] ? H : never;
type Tail<T extends any[]> = T extends [any, ...infer R] ? R : [];
type Last<T extends any[]> = T extends [...any[], infer L] ? L : never;

type RouteParams<S extends string> =
  S extends `${string}:${infer Param}/${infer Rest}` ? Param | RouteParams<`/${Rest}`> :
  S extends `${string}:${infer Param}` ? Param : never;
type P = RouteParams<"/users/:userId/posts/:postId">; // "userId" | "postId"
```

---

## 21. Template Literal Types

Build string literal types using template syntax.

```ts
type Size = "sm" | "md" | "lg";
type Color = "red" | "blue";
type ClassName = `btn-${Size}-${Color}`; // 6 combinations: "btn-sm-red" | ...

type EventName<T extends string> = `on${Capitalize<T>}`;
type ClickEvent = EventName<"click">; // "onClick"

type CssUnit = `${number}px` | `${number}rem` | `${number}%`;
const w: CssUnit = "12px";   // ✅
const h: CssUnit = "12 px";  // ❌

type ApiRoute = `/api/${"users" | "posts"}/${string}`;
const route: ApiRoute = "/api/users/42";
```

Intrinsic string types: `Uppercase<S>`, `Lowercase<S>`, `Capitalize<S>`, `Uncapitalize<S>`.

```ts
// Typed event emitter using template literals
type PropEventSource<T> = {
  on<K extends string & keyof T>(event: `${K}Changed`, cb: (newValue: T[K]) => void): void;
};
declare function makeWatched<T>(obj: T): T & PropEventSource<T>;
const person = makeWatched({ name: "A", age: 26 });
person.on("ageChanged", (v) => v.toFixed()); // v: number
person.on("emailChanged", () => {});          // ❌
```

---

## 22. Utility Types

Built-in generic types for common transformations. Know what each does **and how to implement it**.

| Utility | What it does |
|---|---|
| `Partial<T>` | All props optional |
| `Required<T>` | All props required |
| `Readonly<T>` | All props readonly |
| `Pick<T, K>` | Keep only keys K |
| `Omit<T, K>` | Remove keys K |
| `Record<K, V>` | Object with keys K and values V |
| `Exclude<U, E>` | Remove union members assignable to E |
| `Extract<U, E>` | Keep union members assignable to E |
| `NonNullable<T>` | Remove null & undefined |
| `ReturnType<F>` | Return type of function |
| `Parameters<F>` | Params tuple of function |
| `ConstructorParameters<C>` | Params of a class constructor |
| `InstanceType<C>` | Instance type of a class |
| `Awaited<T>` | Unwrap Promise (recursively) |
| `ThisParameterType<F>` / `OmitThisParameter<F>` | Work with `this` params |
| `NoInfer<T>` | Block inference from a position |
| `Uppercase/Lowercase/Capitalize/Uncapitalize` | String literal transforms |

### Examples

```ts
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
  role?: "admin" | "user";
}

type UpdateUserDto = Partial<Omit<User, "id">>;            // PATCH body
type PublicUser = Omit<User, "password">;                   // safe to send to client
type Credentials = Pick<User, "email" | "password">;
type CompleteUser = Required<User>;                         // role required
type FrozenUser = Readonly<User>;

type RolePermissions = Record<"admin" | "user", string[]>;
const perms: RolePermissions = { admin: ["*"], user: ["read"] };
type UsersById = Record<number, User>;

type T1 = Exclude<"a" | "b" | "c", "a" | "b">;              // "c"
type T2 = Extract<string | number | (() => void), Function>;// () => void
type T3 = NonNullable<string | null | undefined>;           // string

function createUser(name: string, age: number) { return { id: 1, name, age }; }
type NewUser = ReturnType<typeof createUser>;               // { id: number; name: string; age: number }
type CreateArgs = Parameters<typeof createUser>;            // [name: string, age: number]

class Api { constructor(public baseUrl: string, public timeout: number) {} }
type ApiArgs = ConstructorParameters<typeof Api>;           // [string, number]
type ApiInstance = InstanceType<typeof Api>;                // Api

type Data = Awaited<ReturnType<typeof fetchUsers>>;         // unwrap async function result
declare function fetchUsers(): Promise<User[]>;
```

### Implementations (interview favourite)

```ts
type MyPartial<T> = { [K in keyof T]?: T[K] };
type MyRequired<T> = { [K in keyof T]-?: T[K] };
type MyReadonly<T> = { readonly [K in keyof T]: T[K] };
type MyPick<T, K extends keyof T> = { [P in K]: T[P] };
type MyOmit<T, K extends keyof any> = { [P in keyof T as P extends K ? never : P]: T[P] };
// or: Pick<T, Exclude<keyof T, K>>
type MyRecord<K extends keyof any, V> = { [P in K]: V };
type MyExclude<T, U> = T extends U ? never : T;
type MyExtract<T, U> = T extends U ? T : never;
type MyNonNullable<T> = T extends null | undefined ? never : T; // built-in now: T & {}
type MyReturnType<T extends (...a: any) => any> = T extends (...a: any) => infer R ? R : never;
type MyParameters<T extends (...a: any) => any> = T extends (...a: infer P) => any ? P : never;
type MyAwaited<T> = T extends PromiseLike<infer U> ? MyAwaited<U> : T;
type MyInstanceType<T extends abstract new (...a: any) => any> = T extends abstract new (...a: any) => infer R ? R : never;
```

### Custom utilities worth knowing

```ts
type DeepPartial<T> = { [K in keyof T]?: T[K] extends object ? DeepPartial<T[K]> : T[K] };
type DeepReadonly<T> = { readonly [K in keyof T]: T[K] extends object ? DeepReadonly<T[K]> : T[K] };
type ValueOf<T> = T[keyof T];
type Optional<T, K extends keyof T> = Omit<T, K> & Partial<Pick<T, K>>; // make some keys optional
type Prettify<T> = { [K in keyof T]: T[K] } & {};                       // flatten intersections in tooltips
type Mutable<T> = { -readonly [K in keyof T]: T[K] };

type CreatePostInput = Optional<{ id: string; title: string; published: boolean }, "id" | "published">;
// { title: string; id?: string; published?: boolean }
```

---

## 23. Type Assertions, Non-null `!`, `satisfies`

### Type assertion (`as`)

Tell the compiler "trust me, it's this type". No runtime effect or check.

```ts
const input = document.getElementById("email") as HTMLInputElement;
input.value;

const data = JSON.parse(raw) as { id: number };  // unchecked!

// Only allowed between compatible types; force with unknown (dangerous)
const n = "hello" as unknown as number;

// Angle bracket syntax (not in .tsx)
const el = <HTMLCanvasElement>document.querySelector("canvas");
```

### Non-null assertion `!`

```ts
const root = document.getElementById("root")!; // HTMLElement (removes null)
user.address!.city;                            // runtime crash if actually null
```

Prefer real checks (`if (!root) throw ...`) or optional chaining over `!`.

### `satisfies` (TS 4.9)

Checks that a value matches a type **without widening** it — you keep the precise inferred type.

```ts
type Colors = Record<"red" | "green" | "blue", string | [number, number, number]>;

const palette1: Colors = { red: [255, 0, 0], green: "#0f0", blue: "#00f" };
palette1.green.toUpperCase(); // ❌ type is string | tuple (annotation widened it)

const palette2 = { red: [255, 0, 0], green: "#0f0", blue: "#00f" } satisfies Colors;
palette2.green.toUpperCase(); // ✅ green is string
palette2.red.map((c) => c);   // ✅ red is the tuple
// and typos/missing keys are still errors:
const bad = { red: "#f00", gren: "#0f0" } satisfies Colors; // ❌
```

```ts
const routes = {
  home: "/",
  user: "/users/:id",
} satisfies Record<string, `/${string}`>;
type RouteName = keyof typeof routes; // "home" | "user" (not string!)
```

| `: Type` annotation | `as Type` assertion | `satisfies Type` |
|---|---|---|
| Checks and widens to Type | No real check, forces Type | Checks, keeps inferred narrow type |

---

## 24. Classes

```ts
class Account {
  // property declarations
  public owner: string;
  private balance: number;          // TS-only privacy (compile time)
  protected type = "savings";       // accessible in subclasses
  readonly id: string;
  #pin: number;                     // JS private field (runtime privacy)
  static bankName = "TS Bank";

  constructor(owner: string, initial = 0, pin = 0) {
    this.owner = owner;
    this.balance = initial;
    this.id = crypto.randomUUID();
    this.#pin = pin;
  }

  deposit(amount: number): this {   // `this` type enables chaining
    if (amount <= 0) throw new Error("Invalid amount");
    this.balance += amount;
    return this;
  }

  get currentBalance(): number { return this.balance; }
  set pin(v: number) { this.#pin = v; }

  static compare(a: Account, b: Account) { return a.balance - b.balance; }
}

const acc = new Account("Rohit", 100).deposit(50).deposit(25);
acc.currentBalance; // 175
acc.balance;        // ❌ private
acc.id = "x";       // ❌ readonly
```

### Parameter properties (shorthand)

```ts
class User {
  constructor(
    public readonly id: number,
    public name: string,
    private password: string,
  ) {}
}
// Note: parameter properties aren't "erasable syntax" (not supported by Node's type stripping).
```

### Access modifiers

| Modifier | Class | Subclass | Outside |
|---|---|---|---|
| `public` (default) | ✅ | ✅ | ✅ |
| `protected` | ✅ | ✅ | ❌ |
| `private` | ✅ | ❌ | ❌ |
| `#private` (JS) | ✅ | ❌ | ❌ — enforced at runtime |

`private` is erased at runtime (`(obj as any).balance` works); `#field` is truly private.

### Inheritance & override

```ts
class Animal {
  constructor(protected name: string) {}
  speak(): string { return `${this.name} makes a sound`; }
}
class Dog extends Animal {
  override speak(): string {            // `override` keyword (noImplicitOverride)
    return `${super.speak()} — woof`;
  }
}
```

### implements

```ts
interface Serializable { serialize(): string }
interface Comparable<T> { compareTo(other: T): number }

class Money implements Serializable, Comparable<Money> {
  constructor(public amount: number, public currency: string) {}
  serialize() { return JSON.stringify(this); }
  compareTo(o: Money) { return this.amount - o.amount; }
}
```

`implements` only checks the shape — it doesn't add types to the class members.

---

## 25. Abstract Classes

A class that **can't be instantiated** and may contain abstract members that subclasses **must** implement. Unlike interfaces, it can hold real implementation and state.

```ts
abstract class Shape {
  constructor(public name: string) {}
  abstract area(): number;                     // must implement
  describe(): string {                          // shared implementation
    return `${this.name} with area ${this.area().toFixed(2)}`;
  }
}

class Circle extends Shape {
  constructor(private r: number) { super("circle"); }
  area() { return Math.PI * this.r ** 2; }
}

new Shape("x");                 // ❌ Cannot create an instance of an abstract class
new Circle(2).describe();       // "circle with area 12.57"
```

```ts
// Template method pattern for repositories
abstract class Repository<T extends { id: string }> {
  protected items = new Map<string, T>();
  abstract validate(item: T): boolean;
  save(item: T) {
    if (!this.validate(item)) throw new Error("invalid");
    this.items.set(item.id, item);
  }
  find(id: string) { return this.items.get(id); }
}
class UserRepo extends Repository<{ id: string; email: string }> {
  validate(u: { id: string; email: string }) { return u.email.includes("@"); }
}
```

### Abstract class vs interface

| Abstract class | Interface |
|---|---|
| Can have implementation & state | Only shape (no implementation) |
| Exists at runtime (JS class) | Erased at compile time |
| Single inheritance (`extends`) | Multiple (`implements A, B`) |
| Constructors, access modifiers | No constructors |

---

## 26. Index Signatures

For objects with **unknown keys** but known value types.

```ts
interface StringMap {
  [key: string]: string;
}
const headers: StringMap = { "Content-Type": "json", Accept: "*/*" };

interface Scores {
  [subject: string]: number;
  total: number;             // named props must match the index signature type
  // name: string;           // ❌ string not assignable to number
}

type Dictionary<T> = { [key: string]: T };
const cache: Dictionary<{ value: string; expires: number }> = {};
```

With `noUncheckedIndexedAccess`, reading an index gives `T | undefined` (safer):

```ts
const m: Record<string, number> = {};
const v = m["missing"]; // number | undefined with the flag
```

### Record vs index signature vs Map

```ts
type Status = "active" | "inactive";
const labels: Record<Status, string> = { active: "On", inactive: "Off" }; // all keys required
const counts: Partial<Record<Status, number>> = { active: 1 };
const map = new Map<string, number>(); // dynamic keys, frequent add/remove
```

---

## 27. Readonly & Immutability

```ts
interface Config {
  readonly apiUrl: string;
  readonly retries: number;
}
const cfg: Config = { apiUrl: "/api", retries: 3 };
cfg.retries = 5; // ❌

const arr: readonly number[] = [1, 2, 3];
arr.push(4);     // ❌
const arr2: ReadonlyArray<number> = arr;

function total(items: readonly number[]) {  // accept both mutable & readonly
  return items.reduce((a, b) => a + b, 0);
}

type ReadonlyUser = Readonly<{ name: string; tags: string[] }>;
const ru: ReadonlyUser = { name: "a", tags: [] };
ru.tags.push("x"); // ✅ allowed — Readonly is shallow! Use DeepReadonly
```

`readonly` is compile-time only. Use `Object.freeze` for runtime immutability (TS types it as `Readonly<T>`).

---

## 28. Modules, Namespaces, Declaration Files

### Modules

Any file with a top-level `import`/`export` is a module (own scope). Otherwise it's a global script.

```ts
// types.ts
export interface User { id: number; name: string }
export type Role = "admin" | "user";

// app.ts
import type { User, Role } from "./types";       // type-only import (erased)
import { type User as U, fetchUser } from "./api"; // inline type modifier
export type { User };
```

`verbatimModuleSyntax: true` forces you to mark type-only imports with `type`, so the emitted JS is predictable.

### Namespaces (legacy)

```ts
namespace Validation {
  export const isEmail = (s: string) => s.includes("@");
}
Validation.isEmail("a@b.com");
```

Prefer ES modules. Namespaces are mainly seen in older code and `.d.ts` files.

### Declaration files (`.d.ts`)

Contain **only types** (no implementation) — describe the shape of JS code.

```ts
// types/global.d.ts
declare global {
  interface Window { analytics: { track(event: string): void } }
  var __APP_VERSION__: string;
}
export {};

// Typing an untyped JS library
// types/legacy-lib.d.ts
declare module "legacy-lib" {
  export function doThing(input: string): number;
  const version: string;
  export default version;
}

// Non-code imports
declare module "*.svg" {
  const src: string;
  export default src;
}
declare module "*.module.css" {
  const classes: Record<string, string>;
  export default classes;
}

// Ambient declarations
declare const API_URL: string;
declare function gtag(...args: unknown[]): void;
```

### DefinitelyTyped

Types for JS packages: `npm i -D @types/express @types/node`. Many packages ship their own types (`"types"` field in package.json).

---

## 29. Declaration Merging & Module Augmentation

### Interface merging

```ts
interface Settings { theme: string }
interface Settings { fontSize: number }
const s: Settings = { theme: "dark", fontSize: 14 }; // merged
```

### Module augmentation — extend third-party types

```ts
// Add `user` to Express Request
// src/types/express.d.ts
import "express";
declare module "express-serve-static-core" {
  interface Request {
    user?: { id: string; role: "admin" | "user" };
  }
}
```

```ts
// Extend process.env types
declare global {
  namespace NodeJS {
    interface ProcessEnv {
      NODE_ENV: "development" | "production" | "test";
      DATABASE_URL: string;
      JWT_SECRET: string;
    }
  }
}
export {};
```

```ts
// Add a method to Array (augmenting globals)
declare global {
  interface Array<T> { last(): T | undefined }
}
Array.prototype.last = function () { return this[this.length - 1]; };
```

### Function + namespace merging

```ts
function greet(name: string) { return `Hi ${name}`; }
namespace greet { export const version = "1.0"; }
greet.version;
```

---

## 30. Decorators

Functions that annotate/modify classes and members. TS 5.0 supports **standard (TC39) decorators**; the older `experimentalDecorators` flavour is used by NestJS, Angular, TypeORM.

```ts
// Standard decorators (TS 5+)
function logged<This, Args extends any[], Ret>(
  target: (this: This, ...args: Args) => Ret,
  context: ClassMethodDecoratorContext<This, (this: This, ...args: Args) => Ret>
) {
  const name = String(context.name);
  return function (this: This, ...args: Args): Ret {
    console.log(`→ ${name}(${args.join(", ")})`);
    const result = target.call(this, ...args);
    console.log(`← ${name} returned ${result}`);
    return result;
  };
}

class Calculator {
  @logged
  add(a: number, b: number) { return a + b; }
}
new Calculator().add(2, 3);
```

```ts
// NestJS style (experimentalDecorators + emitDecoratorMetadata)
@Controller("users")
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  @Get(":id")
  findOne(@Param("id") id: string) {
    return this.usersService.findOne(id);
  }

  @Post()
  @UseGuards(AuthGuard)
  create(@Body() dto: CreateUserDto) {
    return this.usersService.create(dto);
  }
}
```

---

## 31. tsconfig.json

```jsonc
{
  "compilerOptions": {
    /* Language & output */
    "target": "ES2022",                 // JS version to emit
    "lib": ["ES2023", "DOM", "DOM.Iterable"], // built-in type definitions available
    "module": "NodeNext",               // module system: ESNext / NodeNext / CommonJS / Preserve
    "moduleResolution": "NodeNext",     // how imports are resolved ("Bundler" for Vite/Next)
    "outDir": "dist",
    "rootDir": "src",
    "sourceMap": true,
    "declaration": true,                // emit .d.ts (for libraries)
    "jsx": "react-jsx",                 // for React

    /* Type checking */
    "strict": true,                     // enables all strict flags below
    // strictNullChecks, noImplicitAny, strictFunctionTypes, strictBindCallApply,
    // strictPropertyInitialization, noImplicitThis, alwaysStrict, useUnknownInCatchVariables
    "noUncheckedIndexedAccess": true,   // arr[i] -> T | undefined
    "exactOptionalPropertyTypes": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "noImplicitOverride": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,

    /* Interop */
    "esModuleInterop": true,            // default-import CommonJS modules
    "allowSyntheticDefaultImports": true,
    "resolveJsonModule": true,          // import data from "./x.json"
    "isolatedModules": true,            // each file transpilable alone (required by esbuild/SWC/Babel)
    "verbatimModuleSyntax": true,       // explicit `import type`
    "skipLibCheck": true,               // skip type-checking .d.ts in node_modules (faster)
    "allowJs": true,                    // gradual migration from JS
    "checkJs": false,
    "erasableSyntaxOnly": true,         // TS 5.8: ban enums/namespaces/param properties (for Node type stripping)

    /* Paths */
    "baseUrl": ".",
    "paths": { "@/*": ["src/*"] },
    "types": ["node", "vitest/globals"]
  },
  "include": ["src"],
  "exclude": ["node_modules", "dist"]
}
```

### Important strict flags explained

- **`strictNullChecks`** — `null`/`undefined` aren't assignable to other types; you must handle them.
- **`noImplicitAny`** — error when TS can't infer and falls back to `any`.
- **`strictPropertyInitialization`** — class props must be initialized in the constructor (or use `!`/`?`).
- **`strictFunctionTypes`** — function params checked contravariantly.
- **`useUnknownInCatchVariables`** — `catch (e)` is `unknown`.

```ts
// strictNullChecks in action
function len(s: string | null) {
  return s.length;      // ❌ 's' is possibly 'null'
  return s?.length ?? 0; // ✅
}
```

Project references (`"references"`, `"composite": true`) help monorepos build faster.

---

## 32. Structural Typing

TS uses **structural typing** ("duck typing"): compatibility is based on **shape**, not on declared names (unlike Java/C#'s nominal typing).

```ts
interface Point { x: number; y: number }
class Coord { constructor(public x: number, public y: number) {} }

const p: Point = new Coord(1, 2);     // ✅ same shape, no `implements` needed
const q: Point = { x: 1, y: 2, z: 3 } as { x: number; y: number; z: number }; // ✅ extra props OK via variable

function logPoint(p: Point) {}
const obj = { x: 1, y: 2, label: "a" };
logPoint(obj);                        // ✅ extra props fine when passing a variable
```

### Excess property checking

Object **literals** assigned directly get an extra check for unknown properties (to catch typos).

```ts
logPoint({ x: 1, y: 2, label: "a" }); // ❌ Object literal may only specify known properties
```

### Assignability rules (simplified)

- Subtype → supertype is OK (`{a; b}` assignable to `{a}`).
- `never` → assignable to everything; everything → `unknown`.
- Functions: fewer parameters are fine (`(a) => void` assignable to `(a, b) => void`); params are **contravariant**, return types **covariant**.

```ts
let handler: (e: MouseEvent, extra: string) => void;
handler = (e) => {};            // ✅ ignoring params is allowed

type Animal = { name: string };
type Dog = Animal & { bark(): void };
let fnAnimal = (a: Animal) => {};
let fnDog = (d: Dog) => {};
fnDog = fnAnimal; // ✅ a function accepting any Animal can handle Dogs
fnAnimal = fnDog; // ❌ with strictFunctionTypes (Dog handler may call bark on a plain Animal)
```

### Variance annotations (TS 4.7)

```ts
interface Producer<out T> { get(): T }        // covariant
interface Consumer<in T> { set(v: T): void }  // contravariant
```

---

## 33. TypeScript with React

### Typing props

```tsx
type ButtonProps = {
  label: string;
  variant?: "primary" | "secondary" | "danger";
  onClick?: () => void;
  disabled?: boolean;
};

function Button({ label, variant = "primary", onClick, disabled = false }: ButtonProps) {
  return <button className={`btn-${variant}`} onClick={onClick} disabled={disabled}>{label}</button>;
}
```

### children & extending native element props

```tsx
import type { ReactNode, ComponentProps, ComponentPropsWithoutRef, PropsWithChildren } from "react";

type CardProps = { title: string; children: ReactNode };
function Card({ title, children }: CardProps) { return <section><h2>{title}</h2>{children}</section>; }

// Accept all native <button> props + custom ones
type IconButtonProps = ComponentPropsWithoutRef<"button"> & { icon: ReactNode };
function IconButton({ icon, children, ...rest }: IconButtonProps) {
  return <button {...rest}>{icon}{children}</button>;
}

type InputProps = ComponentProps<"input"> & { label: string; error?: string };

// Props of another component
type ButtonPropsFromComp = ComponentProps<typeof Button>;
```

`ReactNode` = anything renderable (string, number, element, array, null…). `ReactElement` / `JSX.Element` = only elements.

### Hooks

```tsx
const [count, setCount] = useState(0);                       // inferred number
const [user, setUser] = useState<User | null>(null);          // explicit when initial is null
const [items, setItems] = useState<string[]>([]);             // explicit for empty arrays

const inputRef = useRef<HTMLInputElement>(null);              // DOM ref -> RefObject<HTMLInputElement | null>
inputRef.current?.focus();
const timerRef = useRef<number | undefined>(undefined);       // mutable value

type State = { count: number };
type Action = { type: "inc" } | { type: "dec" } | { type: "set"; payload: number };
function reducer(state: State, action: Action): State {
  switch (action.type) {
    case "inc": return { count: state.count + 1 };
    case "dec": return { count: state.count - 1 };
    case "set": return { count: action.payload };
  }
}
const [state, dispatch] = useReducer(reducer, { count: 0 });

const total = useMemo(() => items.length, [items]);          // inferred
const handle = useCallback((id: string) => {}, []);
```

### Events

```tsx
const onChange = (e: React.ChangeEvent<HTMLInputElement>) => setValue(e.target.value);
const onSelect = (e: React.ChangeEvent<HTMLSelectElement>) => {};
const onSubmit = (e: React.FormEvent<HTMLFormElement>) => { e.preventDefault(); };
const onClick = (e: React.MouseEvent<HTMLButtonElement>) => {};
const onKey = (e: React.KeyboardEvent<HTMLInputElement>) => { if (e.key === "Enter") {} };
// Handler type aliases:
const onChange2: React.ChangeEventHandler<HTMLInputElement> = (e) => {};
```

Tip: hover over the `onChange` prop in your editor to see the exact event type.

### Context with a typed custom hook

```tsx
type AuthContextValue = { user: User | null; login(email: string, pw: string): Promise<void>; logout(): void };
const AuthContext = createContext<AuthContextValue | null>(null);

export function useAuth() {
  const ctx = useContext(AuthContext);
  if (!ctx) throw new Error("useAuth must be used within AuthProvider");
  return ctx; // AuthContextValue (non-null)
}
```

### Generic components

```tsx
type ListProps<T> = {
  items: T[];
  renderItem: (item: T) => ReactNode;
  getKey: (item: T) => string | number;
};
function List<T>({ items, renderItem, getKey }: ListProps<T>) {
  return <ul>{items.map((i) => <li key={getKey(i)}>{renderItem(i)}</li>)}</ul>;
}

<List items={users} getKey={(u) => u.id} renderItem={(u) => u.name} /> // T inferred as User

// Generic Select
type SelectProps<T extends string> = { value: T; options: readonly T[]; onChange: (v: T) => void };
function Select<T extends string>({ value, options, onChange }: SelectProps<T>) {
  return (
    <select value={value} onChange={(e) => onChange(e.target.value as T)}>
      {options.map((o) => <option key={o}>{o}</option>)}
    </select>
  );
}
```

### Discriminated props (mutually exclusive props)

```tsx
type LinkButton = { as: "link"; href: string };
type ActionButton = { as: "button"; onClick: () => void };
type SmartButtonProps = (LinkButton | ActionButton) & { label: string };

function SmartButton(props: SmartButtonProps) {
  if (props.as === "link") return <a href={props.href}>{props.label}</a>;
  return <button onClick={props.onClick}>{props.label}</button>;
}
<SmartButton as="link" href="/" label="Home" />;
<SmartButton as="link" onClick={() => {}} label="x" />; // ❌
```

### forwardRef & polymorphic basics

```tsx
const Input = forwardRef<HTMLInputElement, ComponentProps<"input">>((props, ref) => <input ref={ref} {...props} />);
// React 19: function Input({ ref, ...props }: ComponentProps<"input">) { ... }
```

### Typing fetch hooks

```tsx
function useFetch<T>(url: string) {
  const [data, setData] = useState<T | null>(null);
  const [error, setError] = useState<Error | null>(null);
  useEffect(() => {
    fetch(url).then((r) => r.json() as Promise<T>).then(setData).catch(setError);
  }, [url]);
  return { data, error };
}
const { data } = useFetch<User[]>("/api/users"); // data: User[] | null
```

Advanced patterns (polymorphic `as` props, `never`-based prop combinations, generics with `memo` and refs, a type-safe table, typed context + reducer, and the React 19 `useReducer` typing change) are in Section 34.

---

## 34. Typing React Components: Advanced Patterns

The previous section covers everyday typing. This one covers the patterns behind design-system and library components: wrapping native elements, props that must or mustn't appear together, polymorphic `as` props, generic components that stay generic, and a fully typed context + reducer. Every block below was type-checked with **TypeScript 5.9 + `@types/react` 19** in `strict` mode. Lines marked ❌ were confirmed to be compile errors.

### 1. Wrapping native elements (React 19 refs)

In React 19, `ref` is an ordinary prop for function components, so `forwardRef` is no longer needed.

| Type | Contains |
|---|---|
| `ComponentPropsWithRef<"button">` | All `<button>` props **including `ref`** |
| `ComponentPropsWithoutRef<"button">` | All `<button>` props without `ref` |
| `ComponentProps<"button">` | For native elements, the same as `…WithRef` in React 19's types |
| `ComponentProps<typeof MyComponent>` | The props of an existing component |

```tsx
import { useId, type ComponentPropsWithRef } from "react";

type InputProps = ComponentPropsWithRef<"input"> & { label: string; error?: string };

export function Input({ label, error, id, ref, ...rest }: InputProps) {
  const generatedId = useId();                // always call hooks unconditionally, then choose
  const inputId = id ?? generatedId;
  const errorId = `${inputId}-error`;
  return (
    <div>
      <label htmlFor={inputId}>{label}</label>
      <input ref={ref} id={inputId} aria-invalid={error ? true : undefined}
        aria-describedby={error ? errorId : undefined} {...rest} />
      {error && <p id={errorId}>{error}</p>}
    </div>
  );
}
```

**Exposing an imperative API** (`play()`, `focus()`, `scrollToBottom()`) instead of the raw DOM node:

```tsx
import { useImperativeHandle, useRef, type Ref } from "react";

export type VideoHandle = { play(): void; pause(): void };

export function Video({ src, ref }: { src: string; ref?: Ref<VideoHandle> }) {
  const videoRef = useRef<HTMLVideoElement>(null);
  useImperativeHandle(ref, () => ({
    play: () => void videoRef.current?.play(),     // play() returns a Promise; `void` marks it as intentionally ignored
    pause: () => videoRef.current?.pause(),
  }), []);
  return <video ref={videoRef} src={src} />;
}

export function Player() {
  const player = useRef<VideoHandle>(null);
  return (
    <>
      <Video ref={player} src="/intro.mp4" />
      <button type="button" onClick={() => player.current?.play()}>Play</button>
    </>
  );
}
```

### 2. Overriding a native prop: `Omit` first

A component that takes native `<input>` props but changes `onChange` to receive a **number** must remove the native version first. An intersection (`&`) doesn't replace a property. It combines both types, so the parameter becomes `number | ChangeEvent`:

```tsx
import { useState, type ComponentPropsWithoutRef } from "react";

// ❌ Intersection: onChange's parameter is typed `number | ChangeEvent<HTMLInputElement>`
type BadNumberInputProps = ComponentPropsWithoutRef<"input"> & { value: number; onChange: (value: number) => void };
function BadNumberInput(props: BadNumberInputProps) { return <input {...props} type="number" />; }
const bad = <BadNumberInput value={1} onChange={(n) => console.log(n + 1)} />;   // ❌ Operator '+' cannot be applied

// ✅ Omit the native props you redefine
type NumberInputProps = Omit<ComponentPropsWithoutRef<"input">, "value" | "onChange" | "type"> & {
  value: number;
  onChange: (value: number) => void;
};

export function NumberInput({ value, onChange, ...rest }: NumberInputProps) {
  return <input {...rest} type="number" value={value} onChange={(e) => onChange(e.currentTarget.valueAsNumber)} />;
}

export function QuantityPicker() {
  const [qty, setQty] = useState(1);
  return <NumberInput value={qty} onChange={setQty} min={1} max={10} aria-label="Quantity" />;   // setQty gets a number
}
```

### 3. Props that must or mustn't go together

A union of prop shapes plus `?: never` makes invalid combinations compile errors:

```tsx
import type { ComponentPropsWithoutRef, ReactNode } from "react";

// Controlled OR uncontrolled, never half of each
type Controlled = { value: string; onChange: (value: string) => void; defaultValue?: never };
type Uncontrolled = { defaultValue?: string; value?: never; onChange?: never };
type TextFieldProps = { label: string } & (Controlled | Uncontrolled);

export function TextField(props: TextFieldProps) {
  if (props.value !== undefined) {
    const { value, onChange } = props;               // narrowed to Controlled: onChange is defined
    return <input aria-label={props.label} value={value} onChange={(e) => onChange(e.target.value)} />;
  }
  return <input aria-label={props.label} defaultValue={props.defaultValue} />;
}

const ok1 = <TextField label="Name" value="Asha" onChange={(v) => console.log(v)} />;
const ok2 = <TextField label="Name" defaultValue="Asha" />;
const bad1 = <TextField label="Name" value="Asha" />;                                       // ❌ value without onChange
const bad2 = <TextField label="Name" value="Asha" onChange={() => {}} defaultValue="x" />;  // ❌ both modes at once

// An icon-only button MUST have an accessible name
type ButtonProps = ComponentPropsWithoutRef<"button"> &
  ({ children: ReactNode; icon?: ReactNode } | { icon: ReactNode; children?: never; "aria-label": string });

export function Button({ icon, children, ...rest }: ButtonProps) {
  return <button type="button" {...rest}>{icon}{children}</button>;
}

const save = <Button>Save</Button>;
const close = <Button icon="✕" aria-label="Close dialog" />;
const unlabeled = <Button icon="✕" />;                                                     // ❌ missing aria-label
```

**Don't destructure the discriminant away from the rest.** Narrowing doesn't carry over to a `...rest` object:

```tsx
type LinkProps = { kind: "link"; href: string };
type ActionProps = { kind: "action"; onClick: () => void };

export function SmartButton(props: LinkProps | ActionProps) {
  const { kind, ...rest } = props;
  if (kind === "link") return <a href={rest.href}>Go</a>;               // ❌ 'href' does not exist on type '{ href: string } | { onClick: () => void }'
  return null;
}

export function SmartButtonFixed(props: LinkProps | ActionProps) {
  if (props.kind === "link") return <a href={props.href}>Go</a>;        // ✅ narrow the whole props object
  return <button type="button" onClick={props.onClick}>Go</button>;
}
```

### 4. Polymorphic components (`as` prop)

A design-system `<Text>` or `<Box>` should render as any element and accept **that element's** props:

```tsx
import type { ComponentPropsWithRef, ElementType, ReactNode } from "react";

// Own props P, plus `as`, plus every prop of the chosen element except the ones P redefines
export type PolymorphicProps<E extends ElementType, P = object> =
  P & { as?: E } & Omit<ComponentPropsWithRef<E>, keyof P | "as">;

type TextOwnProps = { size?: "sm" | "md" | "lg"; tone?: "default" | "muted"; className?: string };

export function Text<E extends ElementType = "span">({ as, size = "md", tone = "default", className, ...rest }:
  PolymorphicProps<E, TextOwnProps>) {
  const Component: ElementType = as ?? "span";
  return <Component className={[`text-${size}`, `tone-${tone}`, className].filter(Boolean).join(" ")} {...rest} />;
}

// A router-style link component, to show `as` with a custom component
function RouterLink({ to, children }: { to: string; children?: ReactNode }) {
  return <a href={to}>{children}</a>;
}

const t1 = <Text>Plain span</Text>;
const t2 = <Text as="a" href="/pricing" size="lg">Pricing</Text>;          // href is allowed on "a"
const t3 = <Text as={RouterLink} to="/about">About</Text>;                  // RouterLink's props
const t4 = <Text as="label" htmlFor="email" tone="muted">Email</Text>;
const t5 = <Text as="button" href="/x">Nope</Text>;                         // ❌ href doesn't exist on <button>
const t6 = <Text as={RouterLink} href="/about">About</Text>;                // ❌ RouterLink needs `to`, not `href`
```

Polymorphic types are powerful but slow down type-checking in large codebases and produce long error messages. Many libraries use an **`asChild`** prop instead (Radix `Slot`): `<Button asChild><a href="/">Home</a></Button>` merges the button's props and behaviour into its single child. That's simpler to type, because the child element keeps its own props.

### 5. Generic components that stay generic

```tsx
import { memo, type ReactNode, type Ref } from "react";

type ListProps<T> = { items: readonly T[]; getKey: (item: T) => string | number; renderItem: (item: T) => ReactNode };

// In .tsx files, write a generic arrow function as <T,> (the comma tells the parser it's not a JSX tag)
export const List = <T,>({ items, getKey, renderItem }: ListProps<T>) => (
  <ul>{items.map((item) => <li key={getKey(item)}>{renderItem(item)}</li>)}</ul>
);

// memo() loses the type parameter (items become `unknown`). Cast it back:
export const MemoList = memo(List) as typeof List;

type Product = { id: string; name: string; pricePaise: number };
const products: Product[] = [{ id: "p1", name: "Phone", pricePaise: 1_999_900 }];

const l1 = <MemoList items={products} getKey={(p) => p.id} renderItem={(p) => p.name} />;   // p: Product
const l2 = <List<Product> items={[]} getKey={(p) => p.id} renderItem={(p) => p.name} />;    // explicit type argument in JSX

// React 19: `ref` as a prop keeps generics (forwardRef used to erase them)
type SelectProps<T extends string> = {
  options: readonly T[];
  value: T;
  onChange: (value: T) => void;
  ref?: Ref<HTMLSelectElement>;
};

export function Select<T extends string>({ options, value, onChange, ref }: SelectProps<T>) {
  return (
    <select ref={ref} value={value} onChange={(e) => onChange(e.target.value as T)}>
      {options.map((o) => <option key={o} value={o}>{o}</option>)}
    </select>
  );
}
```

**`NoInfer` (TypeScript 5.4+)** stops one prop from widening a type parameter that should come from another prop:

```tsx
type SegmentedProps<T extends string> = { label: string; options: readonly T[]; defaultValue: NoInfer<T> };
export function Segmented<T extends string>({ label, options, defaultValue }: SegmentedProps<T>) {
  return (
    <div role="radiogroup" aria-label={label}>
      {options.map((o) => <label key={o}><input type="radio" name={label} defaultChecked={o === defaultValue} />{o}</label>)}
    </div>
  );
}

const s1 = <Segmented label="Range" options={["day", "week"]} defaultValue="week" />;
const s2 = <Segmented label="Range" options={["day", "week"]} defaultValue="month" />;   // ❌ without NoInfer, T would silently widen to include "month"
```

**A type-safe table.** Each column's `render` receives the correctly typed value for its `key`:

```tsx
import type { ReactNode } from "react";

// One member per key: { key: "name"; render?(value: string, row) } | { key: "joined"; render?(value: Date, row) } | …
export type Column<T> = {
  [K in keyof T]: { key: K; header: string; render?(value: T[K], row: T): ReactNode };
}[keyof T];

// `render` uses method syntax on purpose: TypeScript checks methods bivariantly, which lets the
// union of columns be passed to this generic helper (a function-typed property would be rejected)
function renderCell<T, K extends keyof T>(column: { key: K; render?(value: T[K], row: T): ReactNode }, row: T) {
  return column.render ? column.render(row[column.key], row) : String(row[column.key]);
}

export function Table<T extends { id: string | number }>({ rows, columns }: { rows: readonly T[]; columns: readonly Column<T>[] }) {
  return (
    <table>
      <thead><tr>{columns.map((c) => <th key={String(c.key)} scope="col">{c.header}</th>)}</tr></thead>
      <tbody>
        {rows.map((row) => (
          <tr key={row.id}>{columns.map((c) => <td key={String(c.key)}>{renderCell(c, row)}</td>)}</tr>
        ))}
      </tbody>
    </table>
  );
}

type User = { id: number; name: string; joined: Date; admin: boolean };
const users: User[] = [{ id: 1, name: "Asha", joined: new Date("2026-01-05"), admin: true }];

const table = (
  <Table rows={users} columns={[
    { key: "name", header: "Name" },
    { key: "joined", header: "Joined", render: (d) => d.toLocaleDateString("en-IN") },   // d: Date
    { key: "admin", header: "Role", render: (isAdmin) => (isAdmin ? "Admin" : "Member") },  // isAdmin: boolean
  ]} />
);
const wrongType = <Table rows={users} columns={[{ key: "joined", header: "Joined", render: (d) => d.toFixed(2) }]} />;   // ❌ Date has no toFixed
const wrongKey = <Table rows={users} columns={[{ key: "email", header: "Email" }]} />;                               // ❌ "email" isn't a key of User
```

### 6. Context + reducer, fully typed

```tsx
import { createContext, useContext, useReducer, type Dispatch, type ReactNode } from "react";

export type CartItem = { sku: string; name: string; pricePaise: number; qty: number };
export type CartState = { items: CartItem[] };
export type CartAction =
  | { type: "added"; item: Omit<CartItem, "qty"> }
  | { type: "qtyChanged"; sku: string; qty: number }
  | { type: "removed"; sku: string }
  | { type: "cleared" };

function assertNever(value: never): never {
  throw new Error(`Unhandled action: ${JSON.stringify(value)}`);
}

export function cartReducer(state: CartState, action: CartAction): CartState {
  switch (action.type) {
    case "added": {
      const exists = state.items.some((i) => i.sku === action.item.sku);
      return exists
        ? { items: state.items.map((i) => (i.sku === action.item.sku ? { ...i, qty: i.qty + 1 } : i)) }
        : { items: [...state.items, { ...action.item, qty: 1 }] };
    }
    case "qtyChanged":
      return { items: state.items.map((i) => (i.sku === action.sku ? { ...i, qty: action.qty } : i)).filter((i) => i.qty > 0) };
    case "removed":
      return { items: state.items.filter((i) => i.sku !== action.sku) };
    case "cleared":
      return { items: [] };
    default:
      return assertNever(action);   // add an action type and forget to handle it → compile error here
  }
}

// A reusable helper: a context that throws a clear error when used outside its provider
export function createSafeContext<T>(name: string) {
  const Context = createContext<T | null>(null);
  Context.displayName = name;
  function useSafeContext(): T {
    const value = useContext(Context);
    if (value === null) throw new Error(`use${name} must be used inside <${name}Provider>`);
    return value;
  }
  return [Context.Provider, useSafeContext] as const;
}

// State and dispatch in SEPARATE contexts: components that only dispatch don't re-render on every change
const [CartStateProvider, useCartState] = createSafeContext<CartState>("CartState");
const [CartDispatchProvider, useCartDispatch] = createSafeContext<Dispatch<CartAction>>("CartDispatch");
export { useCartState, useCartDispatch };

export function CartProvider({ children, initial = { items: [] } }: { children: ReactNode; initial?: CartState }) {
  const [state, dispatch] = useReducer(cartReducer, initial);   // types come from cartReducer; no type arguments
  return (
    <CartDispatchProvider value={dispatch}>
      <CartStateProvider value={state}>{children}</CartStateProvider>
    </CartDispatchProvider>
  );
}

export function AddToCart({ product }: { product: Omit<CartItem, "qty"> }) {
  const dispatch = useCartDispatch();
  const addWrong = () => dispatch({ type: "added", sku: product.sku });   // ❌ "added" needs `item`
  return <button type="button" onClick={() => dispatch({ type: "added", item: product })}>Add to cart</button>;
}

export function CartCount() {
  const { items } = useCartState();
  return <span>{items.reduce((n, i) => n + i.qty, 0)} items</span>;
}
```

**React 19 type change:** `useReducer<Reducer<State, Action>>(reducer, init)`, the explicit form common in older code and tutorials, is now an error (*Expected 2 type arguments, but got 1*). Annotate the reducer's parameters and let `useReducer` infer everything. For the same reason, prefer annotating the reducer function over passing type arguments to hooks in general.

### 7. Typing custom hooks

```tsx
import { useCallback, useEffect, useState } from "react";

// Return tuples `as const`, or the types merge into one array type
export function useToggle(initial = false) {
  const [on, setOn] = useState(initial);
  const toggle = useCallback(() => setOn((v) => !v), []);
  return [on, toggle] as const;            // readonly [boolean, () => void]
}

function useToggleLoose(initial = false) {
  const [on, setOn] = useState(initial);
  return [on, () => setOn((v) => !v)];     // (boolean | (() => void))[]
}
function LooseDemo() {
  const [looseOn] = useToggleLoose();
  const flag: boolean = looseOn;                     // ❌ boolean | (() => void) isn't assignable to boolean
  return <p>{String(flag)}</p>;
}

// A discriminated union for async state: impossible states (data AND error) can't be represented
export type AsyncState<T> =
  | { status: "loading" }
  | { status: "success"; data: T }
  | { status: "error"; error: Error };

export function useJson<T>(url: string): AsyncState<T> {
  const [state, setState] = useState<AsyncState<T>>({ status: "loading" });
  useEffect(() => {
    const controller = new AbortController();
    setState({ status: "loading" });
    fetch(url, { signal: controller.signal })
      .then((res) => {
        if (!res.ok) throw new Error(`HTTP ${res.status}`);
        return res.json() as Promise<T>;             // an assertion: validate with Zod for untrusted data
      })
      .then((data) => setState({ status: "success", data }))
      .catch((error: unknown) => {
        if (controller.signal.aborted) return;
        setState({ status: "error", error: error instanceof Error ? error : new Error(String(error)) });
      });
    return () => controller.abort();
  }, [url]);
  return state;
}

export function Orders() {
  const orders = useJson<{ id: string; totalPaise: number }[]>("/api/orders");
  if (orders.status === "loading") return <p>Loading…</p>;
  if (orders.status === "error") return <p role="alert">{orders.error.message}</p>;
  return <ul>{orders.data.map((o) => <li key={o.id}>{o.id}</li>)}</ul>;   // data exists only in "success"
}
```

### 8. What TypeScript can't check in JSX

Every JSX expression has the same type (`JSX.Element`), so TypeScript **can't restrict which components are passed as children**:

```tsx
import type { ReactElement } from "react";

type TabProps = { title: string };
function Tab(_: TabProps) { return null; }
function Tabs(_: { children: ReactElement<TabProps> | ReactElement<TabProps>[] }) { return null; }

const looksSafe = <Tabs><div>Not a tab</div></Tabs>;   // ✅ compiles: no error, even though it's wrong
```

If a component needs specific children, make that part of the API: take data (`tabs={[{ title, content }]}`), or use compound components that register themselves through context.

### 9. Styles: CSS variables and variant maps

```tsx
import "react";
import type { CSSProperties } from "react";

// Allow CSS custom properties in `style` (put this in a .d.ts or any module once)
declare module "react" {
  interface CSSProperties {
    [key: `--${string}`]: string | number | undefined;
  }
}

export const gridStyle: CSSProperties = { "--gap": "8px", display: "grid", gap: "var(--gap)" };

type Variant = "primary" | "secondary" | "danger";

// `satisfies` checks that every variant has a class (and no extra keys) while keeping the literal types
export const variantClass = {
  primary: "bg-blue-700 text-white",
  secondary: "bg-gray-100 text-gray-900",
  danger: "bg-red-700 text-white",
} satisfies Record<Variant, string>;
```

### Interview Qs

1. `ComponentPropsWithRef` vs `ComponentPropsWithoutRef` vs `ComponentProps`? → With `ref`, without `ref`, and (for native elements in React 19's types) the same as with `ref`. `ComponentProps<typeof X>` extracts a component's props.
2. Do you still need `forwardRef`? → Not in React 19: `ref` is a regular prop for function components, and typing it as a prop also keeps generic components generic.
3. How do you change the type of a native prop such as `onChange`? → `Omit` it first. An intersection combines both types instead of replacing one.
4. How do you make props mutually exclusive or required together? → A union of prop shapes, using `?: never` for the forbidden ones.
5. How do you type a polymorphic `as` prop? What's the alternative? → `P & { as?: E } & Omit<ComponentPropsWithRef<E>, keyof P | "as">`. The alternative is `asChild`/Slot composition.
6. How do you write a generic arrow component in a `.tsx` file? → `<T,>(props: Props<T>) => …`.
7. Why does `memo(GenericComponent)` lose its generics? How do you fix it? → `memo`'s signature doesn't preserve type parameters; cast with `as typeof GenericComponent`.
8. What does `NoInfer` do? → It excludes a position from type-parameter inference, so that argument is checked against `T` instead of widening it.
9. How do you type reducer actions safely? → A discriminated union of actions, `switch` on `type`, and `assertNever` in `default` for exhaustiveness.
10. Why split state and dispatch contexts? → `dispatch` is stable, so components that only dispatch don't re-render when state changes.
11. Why return `as const` from custom hooks that return tuples? → Otherwise TypeScript infers an array of the union of all element types.
12. Can TypeScript enforce that `children` are `<Tab>` elements? → No. JSX expressions are all `JSX.Element`. Design the API around data or context instead.
13. What changed in `useReducer`'s types in React 19? → The single `Reducer<S, A>` type argument form was removed; let it infer from the annotated reducer.

---

## 35. TypeScript with Node & Express

```bash
npm i express
npm i -D typescript @types/node @types/express tsx
```

```ts
// src/app.ts
import express, { type Request, type Response, type NextFunction } from "express";

const app = express();
app.use(express.json());

interface User { id: number; name: string; email: string }
interface CreateUserBody { name: string; email: string }
interface UserParams { id: string }
interface ListQuery { page?: string; limit?: string }

const users: User[] = [];

// Request<Params, ResBody, ReqBody, Query>
app.get("/users", (req: Request<{}, User[], {}, ListQuery>, res: Response<User[]>) => {
  const page = Number(req.query.page ?? 1);
  res.json(users.slice((page - 1) * 10, page * 10));
});

app.get("/users/:id", (req: Request<UserParams>, res: Response<User | { error: string }>) => {
  const user = users.find((u) => u.id === Number(req.params.id));
  if (!user) return res.status(404).json({ error: "Not found" });
  res.json(user);
});

app.post("/users", (req: Request<{}, User, CreateUserBody>, res: Response<User>) => {
  const user: User = { id: users.length + 1, ...req.body };
  users.push(user);
  res.status(201).json(user);
});

// Typed error class + error middleware
class HttpError extends Error {
  constructor(public status: number, message: string) { super(message); }
}
app.use((err: unknown, req: Request, res: Response, next: NextFunction) => {
  const status = err instanceof HttpError ? err.status : 500;
  const message = err instanceof Error ? err.message : "Unknown error";
  res.status(status).json({ error: message });
});

export default app;
```

### Typed middleware adding `req.user`

```ts
// src/types/express.d.ts — module augmentation (see section 29)
declare module "express-serve-static-core" {
  interface Request { user?: { id: string; role: "admin" | "user" } }
}

// middleware
import type { RequestHandler } from "express";
export const auth: RequestHandler = (req, res, next) => {
  const token = req.headers.authorization?.split(" ")[1];
  if (!token) return res.status(401).json({ error: "Unauthorized" });
  req.user = verify(token); // typed
  next();
};
```

### Typed service layer & env

```ts
export interface UserRepository {
  findById(id: string): Promise<User | null>;
  create(data: Omit<User, "id">): Promise<User>;
}

export class UserService {
  constructor(private readonly repo: UserRepository) {}
  async getOrThrow(id: string): Promise<User> {
    const u = await this.repo.findById(id);
    if (!u) throw new HttpError(404, "User not found");
    return u;
  }
}
```

### Scripts

```json
{
  "scripts": {
    "dev": "tsx watch src/index.ts",
    "build": "tsc",
    "start": "node dist/index.js",
    "typecheck": "tsc --noEmit"
  }
}
```

---

## 36. Runtime Validation with Zod

Types disappear at runtime; data from APIs, forms, env vars and `JSON.parse` is untrusted. **Zod** gives runtime validation **and** infers the TS type from the schema → single source of truth.

```ts
import { z } from "zod";

const UserSchema = z.object({
  id: z.number().int().positive(),
  name: z.string().min(2),
  email: z.string().email(),
  role: z.enum(["admin", "user"]).default("user"),
  tags: z.array(z.string()).optional(),
  address: z.object({ city: z.string() }).nullable(),
});

type User = z.infer<typeof UserSchema>;         // TS type derived from the schema
type UserInput = z.input<typeof UserSchema>;    // before defaults/transforms

const result = UserSchema.safeParse(await res.json());
if (!result.success) {
  console.error(result.error.issues);
} else {
  const user: User = result.data;               // fully typed & validated
}

UserSchema.parse(data);                          // throws ZodError on failure
const CreateUser = UserSchema.omit({ id: true });
const UpdateUser = CreateUser.partial();
const Id = z.coerce.number();                    // "42" -> 42
const Slug = z.string().regex(/^[a-z0-9-]+$/).transform((s) => s.toLowerCase());
```

Alternatives: Valibot, ArkType, Yup, io-ts, TypeBox.

---

## 37. End-to-End Type Safety: Shared Schemas, tRPC & OpenAPI Codegen

**The problem**: the backend changes a field (`name` → `fullName`), the frontend still compiles, and users get `undefined` in production. End-to-end type safety makes the **compiler catch API contract mismatches**, and runtime validation catches whatever still slips through.

### The options

| Approach | How types reach the client | Backend language | Best for |
|---|---|---|---|
| Hand-written TS interfaces on both sides | Copy & pray | Any | ❌ Avoid — they drift |
| **Shared Zod schemas** (monorepo package) | Import the same schema/types | TS | TS full-stack teams with a REST API |
| **tRPC** | `import type { AppRouter }` — inferred, no codegen | TS only | TS monorepos where the API is only for your own frontend |
| **OpenAPI + codegen** | Generate TS types/clients from the spec | **Any** (FastAPI, NestJS, Go, Java…) | Public/partner APIs, polyglot teams, mobile clients |
| **GraphQL + codegen** | Generate types from schema + queries | Any | Many clients with different data needs |

### 1. Shared Zod schemas in a monorepo

```
packages/contracts/src/user.ts   ← schemas + inferred types (no server/browser-only code)
apps/api                         ← validates requests with the schemas
apps/web                         ← validates forms and parses responses with the same schemas
```

```ts
// packages/contracts/src/user.ts
import { z } from "zod";

export const CreateUserInput = z.object({
  name: z.string().trim().min(2).max(50),
  email: z.string().email(),
  password: z.string().min(8),
});
export type CreateUserInput = z.infer<typeof CreateUserInput>;

export const UserDTO = z.object({                  // what the API RETURNS (no password, no internal fields)
  id: z.string(),
  name: z.string(),
  email: z.string().email(),
  createdAt: z.string().datetime(),                // JSON has no Date type — dates travel as ISO strings
});
export type UserDTO = z.infer<typeof UserDTO>;

export const UserListResponse = z.object({ items: z.array(UserDTO), nextCursor: z.string().nullable() });
export type UserListResponse = z.infer<typeof UserListResponse>;
```

```ts
// apps/api — Express route using the shared schemas
import { CreateUserInput, type UserDTO } from "@acme/contracts";

app.post("/api/users", async (req, res) => {
  const parsed = CreateUserInput.safeParse(req.body);
  if (!parsed.success) return res.status(400).json({ error: parsed.error.flatten() });
  const user = await usersService.create(parsed.data);
  const dto: UserDTO = { id: user.id, name: user.name, email: user.email, createdAt: user.createdAt.toISOString() };
  res.status(201).json(dto);                       // compile error if the DTO shape drifts
});
```

```ts
// apps/web — typed + validated API client and form
import { CreateUserInput, UserDTO } from "@acme/contracts";

export async function createUser(input: CreateUserInput): Promise<UserDTO> {
  const res = await fetch("/api/users", { method: "POST", headers: { "Content-Type": "application/json" }, body: JSON.stringify(input) });
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  return UserDTO.parse(await res.json());          // runtime check: catches deploy mismatches
}

// Same schema drives form validation
const form = useForm<CreateUserInput>({ resolver: zodResolver(CreateUserInput) });
```

**Never export database/ORM types** (Prisma models) to the client — map to explicit DTOs so internal columns (password hashes, flags) can't leak and DB refactors don't break clients.

### 2. tRPC — call backend functions with full types, no codegen

tRPC exposes **procedures** (queries/mutations) from a **router**. The client imports **only the router's type**; TypeScript infers every input and output.

```ts
// server/trpc.ts
import { initTRPC, TRPCError } from "@trpc/server";
import { z } from "zod";

type Context = { user: { id: string; role: "user" | "admin" } | null };
const t = initTRPC.context<Context>().create();

export const router = t.router;
export const publicProcedure = t.procedure;
export const protectedProcedure = t.procedure.use(({ ctx, next }) => {
  if (!ctx.user) throw new TRPCError({ code: "UNAUTHORIZED" });
  return next({ ctx: { user: ctx.user } });        // downstream ctx.user is non-null (typed!)
});

// server/routers/app.ts
export const appRouter = router({
  post: router({
    byId: publicProcedure
      .input(z.object({ id: z.string() }))
      .query(async ({ input }) => {
        const post = await db.post.findUnique({ where: { id: input.id } });
        if (!post) throw new TRPCError({ code: "NOT_FOUND", message: "Post not found" });
        return { id: post.id, title: post.title, createdAt: post.createdAt.toISOString() };
      }),
    create: protectedProcedure
      .input(z.object({ title: z.string().min(1).max(200) }))
      .mutation(({ input, ctx }) => db.post.create({ data: { title: input.title, authorId: ctx.user.id } })),
  }),
});
export type AppRouter = typeof appRouter;          // ← the ONLY thing the client imports (type-only)

// server/index.ts (Express adapter; Next.js/Fastify adapters exist too)
import { createExpressMiddleware } from "@trpc/server/adapters/express";
app.use("/trpc", createExpressMiddleware({ router: appRouter, createContext: ({ req }) => ({ user: getUserFromRequest(req) }) }));
```

```ts
// client
import { createTRPCClient, httpBatchLink } from "@trpc/client";
import type { AppRouter } from "../server/routers/app";

const trpc = createTRPCClient<AppRouter>({ links: [httpBatchLink({ url: "/trpc" })] });

const post = await trpc.post.byId.query({ id: "p1" });   // post: { id: string; title: string; createdAt: string }
await trpc.post.create.mutate({ title: "Hello" });
await trpc.post.create.mutate({ title: 123 });            // ❌ compile error: number is not a string
```

tRPC also integrates with **TanStack Query** (typed `useQuery`/`useMutation` with query keys generated for you), batches requests, and supports subscriptions.

**tRPC trade-offs**
- ✅ Zero codegen, instant rename-refactors across client and server, great DX.
- ❌ TypeScript-only; client and server must share a repo/package; not a documented public REST API (though OpenAPI adapters exist); couples frontend to backend deploys.

### 3. How the "magic" works — a tiny typed RPC in 30 lines

tRPC's core trick is just TypeScript inference over a router object:

```ts
type Validator<T> = { parse: (input: unknown) => T };

type Procedure<I, O> = { input: Validator<I>; handler: (input: I) => Promise<O> };

function procedure<I>(input: Validator<I>) {
  return { handle: <O>(handler: (input: I) => Promise<O>): Procedure<I, O> => ({ input, handler }) };
}

// Client type = for each procedure, a function taking its input and returning its output
type Client<R> = { [K in keyof R]: R[K] extends Procedure<infer I, infer O> ? (input: I) => Promise<O> : never };

function createClient<R extends Record<string, Procedure<any, any>>>(call: (name: string, input: unknown) => Promise<unknown>): Client<R> {
  return new Proxy({}, { get: (_, name: string) => (input: unknown) => call(name, input) }) as Client<R>;
}

// ---- server side
const num: Validator<number> = { parse: (x) => { if (typeof x !== "number") throw new Error("not a number"); return x; } };
const serverRouter = {
  double: procedure(num).handle(async (n) => n * 2),
  greet: procedure({ parse: (x) => String(x) }).handle(async (name) => ({ message: `Hi ${name}` })),
};
type ServerRouter = typeof serverRouter;

// ---- client side (only the TYPE crosses the boundary)
const api = createClient<ServerRouter>(async (name, input) => {
  const proc = serverRouter[name as keyof ServerRouter] as Procedure<unknown, unknown>;
  return proc.handler(proc.input.parse(input));              // real life: an HTTP call
});

const doubled: number = await api.double(21);               // 42, typed as number
const { message } = await api.greet("Rohit");               // typed as string
// @ts-expect-error — wrong input type is a compile error…
await api.double("21").catch((e) => console.log(e.message));   // …and still rejected at runtime: "not a number"
```

### 4. OpenAPI codegen — type safety across languages

When the backend is **FastAPI** (Python), NestJS, Spring, Go…, the OpenAPI spec is the contract. Generate TypeScript from it.

```bash
# FastAPI serves its schema at /openapi.json
npx openapi-typescript http://localhost:8000/openapi.json -o src/api/schema.d.ts
```

```ts
import createClient from "openapi-fetch";
import type { paths, components } from "./api/schema";

export type User = components["schemas"]["UserOut"];         // named after the Pydantic model
const api = createClient<paths>({ baseUrl: "/api" });

const { data, error } = await api.GET("/users/{user_id}", { params: { path: { user_id: 1 } } });
if (data) console.log(data.email);                            // typed from the Pydantic response_model
await api.POST("/users", { body: { email: "a@b.com", name: "A", password: "Secret123" } });   // body type-checked
```

- Tools: **openapi-typescript + openapi-fetch** (types only, tiny runtime), **orval** / **@hey-api/openapi-ts** (generate clients and TanStack Query hooks, optionally Zod schemas), **kubb**.
- Run codegen in CI and **fail the build if the generated file changes unexpectedly** or the spec has breaking changes (`oasdiff` / `openapi-diff`).
- In FastAPI, give routes stable `operation_id`s and response models so generated names are clean.

### 5. GraphQL codegen (brief)

GraphQL has a typed schema by design. **GraphQL Code Generator** generates TS types (and typed hooks) for each query you write, so selecting a field that doesn't exist is a compile error. Good when many clients need different shapes of the same data.

### Choosing

- **TS frontend + TS backend in one repo, internal API** → tRPC (or shared Zod contracts with REST).
- **Python/Go/Java backend, or public/mobile API** → OpenAPI + codegen.
- **Many clients with very different data needs** → GraphQL + codegen.
- **Always**: validate at runtime on the server, and parse critical responses on the client (types disappear at runtime; deploys don't happen atomically).

### Best practices

- One source of truth for every contract (schema file, router, or spec) — never duplicate shapes by hand.
- Explicit **DTOs**, not ORM entities, in API responses.
- Dates as ISO strings, money as integer minor units, IDs as strings in contracts.
- Treat contract changes like API versioning: additive changes are safe; breaking changes need a version or a coordinated rollout (backend accepts old + new, then clients migrate).
- Check contracts in CI (typecheck, generated-code diff, breaking-change detection).

### Interview Qs

1. What is end-to-end type safety and why doesn't TypeScript alone give it?
2. How does tRPC share types without code generation?
3. When would you choose OpenAPI codegen over tRPC?
4. Why should API responses use DTOs instead of ORM/Prisma types?
5. Even with shared types, why validate responses at runtime?
6. How do you detect breaking API contract changes in CI?

---

## 38. Patterns

### Branded (nominal) types

Prevent mixing values that share a primitive type.

```ts
type Brand<T, B extends string> = T & { readonly __brand: B };
type UserId = Brand<string, "UserId">;
type OrderId = Brand<string, "OrderId">;

const toUserId = (s: string) => s as UserId;
function getUser(id: UserId) {}

const uid = toUserId("u_1");
const oid = "o_1" as OrderId;
getUser(uid);   // ✅
getUser(oid);   // ❌ OrderId not assignable to UserId
getUser("u_1"); // ❌ plain string not allowed
```

### Builder with fluent `this` typing

```ts
class QueryBuilder<T> {
  private filters: Partial<T> = {};
  where<K extends keyof T>(key: K, value: T[K]): this {
    this.filters[key] = value;
    return this;
  }
  build() { return this.filters; }
}
new QueryBuilder<{ age: number; name: string }>().where("age", 30).where("name", "A").build();
```

### Type-safe event emitter

```ts
type Events = {
  login: { userId: string };
  logout: undefined;
  message: { from: string; text: string };
};

class TypedEmitter<E extends Record<string, unknown>> {
  private listeners: { [K in keyof E]?: Array<(payload: E[K]) => void> } = {};
  on<K extends keyof E>(event: K, fn: (payload: E[K]) => void) {
    (this.listeners[event] ??= []).push(fn);
    return () => { this.listeners[event] = this.listeners[event]?.filter((f) => f !== fn); };
  }
  emit<K extends keyof E>(event: K, payload: E[K]) {
    this.listeners[event]?.forEach((fn) => fn(payload));
  }
}

const bus = new TypedEmitter<Events>();
bus.on("login", (p) => p.userId);           // p: { userId: string }
bus.emit("message", { from: "a", text: "hi" });
bus.emit("login", { user: "x" });           // ❌
```

### Type-safe API client

```ts
type Endpoints = {
  "GET /users": { response: User[] };
  "GET /users/:id": { response: User };
  "POST /users": { body: Omit<User, "id">; response: User };
};

async function api<K extends keyof Endpoints>(
  route: K,
  ...args: Endpoints[K] extends { body: infer B } ? [body: B] : []
): Promise<Endpoints[K]["response"]> {
  const [method, path] = (route as string).split(" ");
  const res = await fetch(path, { method, body: args[0] ? JSON.stringify(args[0]) : undefined });
  return res.json();
}

const users = await api("GET /users");                       // User[]
const created = await api("POST /users", { name: "A", email: "a@b.com" }); // User
```

### Exhaustive object maps

```ts
type Status = "draft" | "published" | "archived";
const statusLabel: Record<Status, string> = {
  draft: "Draft",
  published: "Live",
  archived: "Archived", // missing a key -> compile error
};
```

---

## 39. Advanced TypeScript Features

Features you meet in libraries, framework code and senior interviews. (`satisfies`, `const` type parameters, `NoInfer` and the basics of `using` are in Production TypeScript Best Practices; variance annotations are in Structural Typing.)

### 1. Polymorphic `this` types

Returning `this` (the type) keeps method chaining working in **subclasses**.

```ts
class QueryBuilder {
  protected parts: string[] = [];
  where(cond: string): this {          // `this`, not `QueryBuilder`
    this.parts.push(`WHERE ${cond}`);
    return this;
  }
  build(): string { return this.parts.join(" "); }
}

class PagedQueryBuilder extends QueryBuilder {
  limit(n: number): this {
    this.parts.push(`LIMIT ${n}`);
    return this;
  }
}

new PagedQueryBuilder().where("age > 18").limit(10).build();   // ✅ `where` returns PagedQueryBuilder
// With `where(): QueryBuilder`, `.limit` would be a type error.
```

`this`-based type guards on methods:

```ts
class FileNode {
  isDirectory(): this is DirectoryNode { return this instanceof DirectoryNode; }
}
class DirectoryNode extends FileNode { children: FileNode[] = []; }

declare const node: FileNode;
if (node.isDirectory()) node.children.length;   // narrowed to DirectoryNode
```

### 2. Constructor types, abstract constructors & typed mixins

```ts
type Constructor<T = {}> = new (...args: any[]) => T;
type AbstractConstructor<T = {}> = abstract new (...args: any[]) => T;   // accepts abstract classes too

// Factory that works with any class
function create<T>(Ctor: Constructor<T>, ...args: unknown[]): T {
  return new Ctor(...args);
}

// Typed mixins: functions that take a class and return an extended class
function Timestamped<TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    createdAt = new Date();
    touch() { this.createdAt = new Date(); }
  };
}

function SoftDeletable<TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    deletedAt: Date | null = null;
    softDelete() { this.deletedAt = new Date(); }
    get isDeleted() { return this.deletedAt !== null; }
  };
}

class User { constructor(public name: string) {} }
const AuditedUser = SoftDeletable(Timestamped(User));

const u = new AuditedUser("Rohit");
u.touch(); u.softDelete();
u.name; u.createdAt; u.isDeleted;           // all typed
type AuditedUserInstance = InstanceType<typeof AuditedUser>;
```

### 3. `unique symbol` & symbol-keyed properties

A `unique symbol` type is tied to **one specific** symbol declaration — useful for hidden/private-ish keys and strongly typed branding.

```ts
const ID: unique symbol = Symbol("id");          // `const x = Symbol()` is inferred as unique symbol too

interface Entity {
  [ID]: string;                                  // property keyed by that exact symbol
  name: string;
}
const e: Entity = { [ID]: "e_1", name: "Box" };
e[ID];                                           // string

// Branding with a declared unique symbol (no runtime cost)
declare const brand: unique symbol;
type Brand<T, B extends string> = T & { readonly [brand]: B };
type Email = Brand<string, "Email">;
const toEmail = (s: string): Email => {
  if (!s.includes("@")) throw new Error("invalid email");
  return s as Email;
};
```

### 4. Auto-accessors (`accessor`) & modern decorators with metadata

`accessor` (TS 4.9 / ECMAScript decorators) creates a private backing field with a getter/setter pair — the target that **field decorators** need to intercept reads/writes.

```ts
function logged<This, V>(
  target: ClassAccessorDecoratorTarget<This, V>,
  context: ClassAccessorDecoratorContext<This, V>,
): ClassAccessorDecoratorResult<This, V> {
  return {
    set(value) {
      console.log(`${String(context.name)} = ${String(value)}`);
      target.set.call(this, value);
    },
  };
}

class Settings {
  @logged accessor theme = "light";              // like a field, but with get/set under the hood
}
new Settings().theme = "dark";                   // logs "theme = dark"
```

**Decorator metadata** (TS 5.2): decorators can write to `context.metadata`, readable later via `Class[Symbol.metadata]` — the basis for validation/serialization libraries built on standard decorators.

```ts
function required(_: undefined, context: ClassFieldDecoratorContext) {
  const list = (context.metadata.required ??= []) as (string | symbol)[];
  list.push(context.name);
}
class SignUp {
  @required email = "";
  @required password = "";
}
// SignUp[Symbol.metadata]?.required → ["email", "password"]  (needs a runtime/polyfill providing Symbol.metadata)
```

### 5. Explicit resource management in depth (`using`, `DisposableStack`)

Any object with `[Symbol.dispose]()` (or `[Symbol.asyncDispose]()` for `await using`) is cleaned up **automatically when the block exits** — even on `return` or thrown errors, in reverse order of declaration. It replaces nested `try/finally`.

```ts
class TempDir implements Disposable {
  constructor(public path: string) { console.log("create", path); }
  [Symbol.dispose]() { console.log("remove", this.path); }
}

class Lock implements Disposable {
  constructor(private name: string) { console.log("lock", name); }
  [Symbol.dispose]() { console.log("unlock", this.name); }
}

function buildReport() {
  using lock = new Lock("report");
  using dir = new TempDir("/tmp/report-1");
  // ... work that may throw ...
  return "done";
}   // prints: unlock order is reverse → "remove /tmp/report-1", then "unlock report"
```

```ts
// DisposableStack: collect cleanups dynamically (like a defer list)
function openMany(paths: string[]) {
  using stack = new DisposableStack();
  const handles = paths.map((p) => stack.use(openHandle(p)));   // each disposed when the stack is
  stack.defer(() => console.log("all closed"));                   // arbitrary cleanup callback
  return process(handles);
}

// Transaction that rolls back unless committed
async function transfer(db: Db) {
  await using tx = await db.begin();       // tx[Symbol.asyncDispose] = rollback if not committed
  await tx.debit(1, 100);
  await tx.credit(2, 100);
  await tx.commit();
}
```

Needs `"lib": ["esnext"]` (or `"esnext.disposable"`) and a runtime that provides `Symbol.dispose`/`DisposableStack` (recent Node/browsers) or a polyfill; TS downlevels the syntax.

### 6. Method vs property syntax: a variance gotcha

With `strictFunctionTypes`, **function-typed properties** are checked soundly (parameters contravariant), but **method-shorthand** signatures stay **bivariant** (less safe) for backwards compatibility.

```ts
interface Animal { name: string }
interface Dog extends Animal { bark(): void }

interface HandlerProp { handle: (a: Animal) => void }   // property syntax → strict
interface HandlerMethod { handle(a: Animal): void }     // method syntax → bivariant

const dogOnly = (d: Dog) => d.bark();

const h1: HandlerProp = { handle: dogOnly };    // ❌ error: Dog handler can't accept every Animal
const h2: HandlerMethod = { handle: dogOnly };  // ✅ allowed (unsound!) — may call bark() on a Cat at runtime
```

Prefer **property syntax** (`handle: (a: Animal) => void`) for callback types in your own interfaces.

### 7. Advanced `infer`: constraints & recursion

```ts
// `infer X extends C` (TS 4.7): infer AND constrain in one step
type FirstString<T> = T extends [infer H extends string, ...unknown[]] ? H : never;
type A = FirstString<["a", 1]>;   // "a"
type B = FirstString<[1, "a"]>;   // never

// Parse a number out of a string literal type
type ToNumber<S> = S extends `${infer N extends number}` ? N : never;
type C = ToNumber<"42">;          // 42

// Tail-recursive conditional types (TS 4.5) can recurse ~1000 levels
type Repeat<S extends string, N extends number, Acc extends string[] = []> =
  Acc["length"] extends N ? Acc : Repeat<S, N, [...Acc, S]>;
type D = Repeat<"x", 3>;          // ["x", "x", "x"]

// A recursive JSON type
type Json = string | number | boolean | null | Json[] | { [key: string]: Json };
const config: Json = { name: "app", ports: [80, 443], nested: { debug: true } };
```

### 8. `ThisType` for object literal APIs

```ts
type StoreDef<S, A> = { state: S; actions: A & ThisType<S & A> };   // `this` inside actions = state + actions

function defineStore<S, A>(def: StoreDef<S, A>): S & A {
  return Object.assign({}, def.state, def.actions);
}

const counter = defineStore({
  state: { count: 0 },
  actions: {
    increment() { this.count++; },               // `this.count` is typed
    add(n: number) { this.count += n; this.increment(); },
  },
});
counter.add(5);
```

(Libraries like Vue's Options API and Pinia use this pattern.)

### 9. Module resolution & dual packages (real-world pain)

| `moduleResolution` | Use for |
|---|---|
| `bundler` | Apps built with Vite/webpack/Next (extensionless imports, `exports` field) |
| `nodenext` / `node16` | Code run directly by Node (ESM needs `.js` extensions in relative imports, respects `"type"` and `exports`) |
| `node10` (old "node") | Legacy CJS projects only |

```jsonc
// Node ESM project
{ "compilerOptions": { "module": "nodenext", "moduleResolution": "nodenext", "target": "es2022" } }
```

```ts
// With nodenext + "type": "module": relative imports need the RUNTIME extension
import { add } from "./math.js";     // ✅ even though the source file is math.ts
import { add } from "./math";        // ❌ error in nodenext ESM
```

Publishing a library for both ESM and CJS consumers:

```json
{
  "name": "@acme/utils",
  "type": "module",
  "exports": {
    ".": {
      "import": { "types": "./dist/index.d.ts", "default": "./dist/index.js" },
      "require": { "types": "./dist/index.d.cts", "default": "./dist/index.cjs" }
    }
  },
  "files": ["dist"]
}
```

Check packages with **`@arethetypeswrong/cli`** (`npx attw --pack`) and build with **tsup/tsdown**.

### 10. Monorepos & project references

```jsonc
// packages/shared/tsconfig.json
{
  "compilerOptions": {
    "composite": true,          // required for referenced projects
    "declaration": true,
    "declarationMap": true,     // "go to definition" jumps to the .ts source, not .d.ts
    "outDir": "dist",
    "rootDir": "src"
  }
}

// apps/web/tsconfig.json
{
  "compilerOptions": { "outDir": "dist" },
  "references": [{ "path": "../../packages/shared" }]
}

// root tsconfig.json — build everything in dependency order, incrementally
{ "files": [], "references": [{ "path": "packages/shared" }, { "path": "apps/web" }, { "path": "apps/api" }] }
```

```bash
tsc --build            # (tsc -b) builds referenced projects in order, skips unchanged ones
tsc -b --watch
```

Monorepo tips:
- Use package manager **workspaces** (pnpm/npm/yarn) so apps import `@acme/shared` like a normal package.
- Share a base config (`@acme/tsconfig/base.json`) and `extends` it.
- Avoid deep relative imports across packages (`../../../packages/shared/src`).
- Orchestrate builds/tests with **Turborepo** or **Nx** (caching, only affected packages).

Hands-on walkthrough (pnpm workspaces, Turborepo caching, boundaries, deploying one app): `nodejs.md` → "Monorepos: pnpm Workspaces, Turborepo & Shared Packages".

### 11. Diagnosing slow type-checking

```bash
tsc --noEmit --extendedDiagnostics      # time spent, number of types/instantiations
tsc --noEmit --generateTrace trace      # open in https://ui.perfetto.dev or @typescript/analyze-trace
```

Common causes & fixes:
- Huge unions (thousands of members) and deeply recursive conditional types → simplify or cache intermediate types.
- **Intersections of many object types** → prefer `interface ... extends` (cached relationships).
- Missing return type annotations on big exported functions → annotate them.
- Type-checking `node_modules` → `skipLibCheck: true`.
- One giant project → project references / smaller `include`.
- TypeScript's **native Go compiler** (`tsgo`, TypeScript 7) makes checking large projects much faster.

### Interview Qs

1. What is the polymorphic `this` type and why is it useful for fluent APIs?
2. How do you type a mixin? What is `abstract new (...) => T`?
3. What is `unique symbol`?
4. What does the `accessor` keyword do and why do decorators need it?
5. How does `using` / `await using` work? What order are resources disposed in?
6. Why are method-shorthand parameters bivariant even with `strictFunctionTypes`?
7. What does `infer X extends string` do?
8. What is `ThisType`?
9. `moduleResolution: bundler` vs `nodenext`? Why do you need `.js` extensions in TS ESM for Node?
10. How do project references speed up monorepo builds?
11. How would you debug slow type-checking?

---

## 40. Production TypeScript Best Practices

TypeScript only protects you as much as you let it. These are the habits that make types **actually catch bugs** in real codebases, instead of being decoration full of `any` and `as`.

### 1. Strict config + type-check in CI

```jsonc
{
  "compilerOptions": {
    "strict": true,                       // non-negotiable for new code
    "noUncheckedIndexedAccess": true,     // arr[i] / record[key] → T | undefined
    "exactOptionalPropertyTypes": true,   // `a?: string` ≠ `a: string | undefined`
    "noImplicitOverride": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "verbatimModuleSyntax": true,         // forces `import type` → predictable emitted JS
    "isolatedModules": true,              // compatible with esbuild/SWC/Vite
    "skipLibCheck": true
  }
}
```

```json
// package.json — bundlers DON'T type-check, so do it explicitly
{ "scripts": { "typecheck": "tsc --noEmit", "lint": "eslint ." } }
```

Run `typecheck` in CI and pre-commit. A green build with type errors is a false sense of safety.

### 2. Ban `any` — use `unknown`, generics or proper types

`any` switches off checking **and spreads** to everything it touches.

```ts
// ❌ any leaks: no errors anywhere downstream
function parse(json: string): any { return JSON.parse(json); }
const user = parse(raw);
user.nmae.toUpperCase();            // compiles, crashes at runtime

// ✅ unknown forces a check
function parseJson(json: string): unknown { return JSON.parse(json); }
const data = parseJson(raw);
if (isUser(data)) data.name.toUpperCase();

// ✅ generics keep the relationship between input and output
function first<T>(items: readonly T[]): T | undefined { return items[0]; }
```

When you truly must silence the compiler, be explicit and leave a reason:

```ts
// @ts-expect-error — lib types are wrong for v3.2, remove after upgrading (JIRA-123)
legacyLib.init({ mode: "fast" });
```

`@ts-expect-error` fails when the error disappears (so it won't go stale); prefer it over `@ts-ignore`.

### 3. Validate at the boundaries — don't `as`-cast external data

Types don't exist at runtime. Data from **APIs, forms, `JSON.parse`, localStorage, env vars, URL params, webhooks, queues** is `unknown` until validated.

```ts
// ❌ a lie to the compiler — if the API changes, you find out in production
const user = (await res.json()) as User;

// ✅ validate once at the edge; everything inside is truly typed
import { z } from "zod";
const UserSchema = z.object({ id: z.string(), name: z.string(), email: z.string().email() });
type User = z.infer<typeof UserSchema>;         // type derived from the schema — single source of truth

async function getUser(id: string): Promise<User> {
  const res = await fetch(`/api/users/${id}`);
  if (!res.ok) throw new HttpError(res.status, await res.text());
  return UserSchema.parse(await res.json());
}
```

**Single source of truth** for types:
- Zod schemas → `z.infer` (validation + types).
- Prisma/Drizzle schema → generated DB types.
- OpenAPI spec → generated API client types (`openapi-typescript`).
- tRPC / shared monorepo package → end-to-end types.

Never hand-write the same shape in three places.

### 4. Let inference work; annotate the edges

```ts
// ✅ annotate parameters and exported/public return types
export function calculateTotal(items: readonly CartItem[], discountPct = 0): number {
  const subtotal = items.reduce((sum, i) => sum + i.pricePaise * i.qty, 0); // inferred number
  return Math.round(subtotal * (1 - discountPct / 100));
}

// ❌ noise — the compiler already knows
const count: number = 5;
const names: string[] = users.map((u: User): string => u.name);

// ✅ `satisfies` checks config objects without widening them
const routes = {
  home: "/",
  profile: "/profile/:id",
} satisfies Record<string, `/${string}`>;
type RouteName = keyof typeof routes;           // "home" | "profile"

// ✅ `as const` for literal constants
export const ROLES = ["admin", "editor", "viewer"] as const;
export type Role = (typeof ROLES)[number];
```

Explicit return types on exported functions give better error messages (at the function, not at every caller) and faster type-checking in big projects.

### 5. Model the domain so impossible states are impossible

```ts
// ❌ "optional soup" — allows nonsense like { status: "success", error: "x" } or loading + data
interface State { status: string; data?: User[]; error?: string; loading?: boolean }

// ✅ discriminated union — each state carries exactly what it needs
type State =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: User[] }
  | { status: "error"; error: string };

// ✅ exhaustiveness helper — adding a new status breaks the build until handled
export function assertNever(x: never): never {
  throw new Error(`Unhandled case: ${JSON.stringify(x)}`);
}
function render(s: State) {
  switch (s.status) {
    case "idle": return "Start";
    case "loading": return "Loading…";
    case "success": return `${s.data.length} users`;
    case "error": return s.error;
    default: return assertNever(s);
  }
}
```

More domain-modelling tools:
- **Branded types** for IDs and units (`UserId` vs `OrderId`, `Paise` vs `Rupees`) — see Patterns.
- **Literal unions** instead of `string` (`"INR" | "USD"`).
- **Required vs optional** chosen deliberately; separate `CreateUserInput`, `UpdateUserInput`, `User` types instead of one type with everything optional.

### 6. Prefer unions & `as const` objects over enums; use `import type`

```ts
// ✅ no runtime surprises, tree-shakeable, works with Node's type stripping
export const OrderStatus = { Pending: "pending", Paid: "paid", Shipped: "shipped" } as const;
export type OrderStatus = (typeof OrderStatus)[keyof typeof OrderStatus];

import type { User } from "./types";             // erased completely from the JS output
import { type Order, createOrder } from "./orders";
```

### 7. Readonly inputs, no mutation of arguments

```ts
function totals(items: readonly LineItem[]): number { /* can't push/sort in place */ }

interface Props {
  readonly user: Readonly<User>;
  readonly tags: readonly string[];
}
```

Accept `readonly` inputs (callers can pass both mutable and readonly arrays); return fresh data.

### 8. Handle null/undefined honestly

```ts
// ❌ non-null assertions hide real bugs
const el = document.getElementById("root")!;
const city = user.address!.city;

// ✅ narrow or fail loudly with a useful message
const root = document.getElementById("root");
if (!root) throw new Error("#root element missing in index.html");

const city2 = user.address?.city ?? "Unknown";

// ✅ with noUncheckedIndexedAccess
const first = items[0];               // Item | undefined
if (first) use(first);
```

### 9. Type errors properly

```ts
try {
  await saveOrder(order);
} catch (err) {                        // err: unknown (useUnknownInCatchVariables)
  if (err instanceof HttpError && err.status === 409) return showConflict();
  const message = err instanceof Error ? err.message : String(err);
  logger.error({ message }, "save failed");
  throw err;
}

// Result type when failure is an expected outcome
type Result<T, E = string> = { ok: true; value: T } | { ok: false; error: E };
```

### 10. Generics: useful, constrained, not clever

```ts
// ✅ constrained & meaningful
function groupBy<T, K extends PropertyKey>(items: readonly T[], getKey: (item: T) => K): Record<K, T[]> {
  const out = {} as Record<K, T[]>;
  for (const item of items) (out[getKey(item)] ??= []).push(item);
  return out;
}

// ❌ a generic that isn't used to relate anything — just use the concrete type
function logValue<T>(value: T): void { console.log(value); }   // `value: unknown` is simpler
```

Rules: a type parameter should appear **at least twice** (relating inputs/outputs); prefer descriptive names (`TItem`, `TKey`) in complex signatures; keep advanced type-level programming in libraries/utilities, not scattered through app code.

### 11. Typing async code & API layers

```ts
// Generic fetch helper that REQUIRES a schema → typed AND validated
async function request<T>(url: string, schema: z.ZodType<T>, init?: RequestInit): Promise<T> {
  const res = await fetch(url, init);
  if (!res.ok) throw new HttpError(res.status, res.statusText);
  return schema.parse(await res.json());
}
const products = await request("/api/products", z.array(ProductSchema)); // Product[]

type Data = Awaited<ReturnType<typeof loadDashboard>>;   // derive types from functions instead of duplicating
```

### 12. Typing state libraries (TanStack Query, Redux Toolkit)

```ts
// TanStack Query v5: queryOptions keeps key + fn + data type together
import { queryOptions, useQuery } from "@tanstack/react-query";

export const productQuery = (id: string) =>
  queryOptions({
    queryKey: ["products", id] as const,
    queryFn: () => request(`/api/products/${id}`, ProductSchema),
    staleTime: 60_000,
  });

const { data } = useQuery(productQuery(id));             // data: Product | undefined
queryClient.setQueryData(productQuery(id).queryKey, p);   // typed: must be a Product
```

```ts
// Redux Toolkit: infer types from the store, create typed hooks once
export const store = configureStore({ reducer: { cart: cartReducer, user: userReducer } });
export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch;

export const useAppDispatch = useDispatch.withTypes<AppDispatch>();
export const useAppSelector = useSelector.withTypes<RootState>();

// slice with typed payloads
const cartSlice = createSlice({
  name: "cart",
  initialState: { items: [] as CartItem[] },
  reducers: {
    added(state, action: PayloadAction<CartItem>) { state.items.push(action.payload); },
  },
});
```

### 13. Lint rules that catch real bugs (typescript-eslint)

```js
// eslint.config.js
import tseslint from "typescript-eslint";
export default tseslint.config(
  ...tseslint.configs.strictTypeChecked,
  {
    languageOptions: { parserOptions: { projectService: true } },
    rules: {
      "@typescript-eslint/no-floating-promises": "error",       // forgot to await → silent failures
      "@typescript-eslint/no-misused-promises": "error",        // async fn where a void callback is expected
      "@typescript-eslint/switch-exhaustiveness-check": "error",
      "@typescript-eslint/no-explicit-any": "error",
      "@typescript-eslint/consistent-type-imports": "error",
      "@typescript-eslint/no-unnecessary-condition": "warn",    // checks that can never be false
      "@typescript-eslint/no-non-null-assertion": "warn",
    },
  },
);
```

```ts
// Bugs these rules catch
saveUser(user);                                   // no-floating-promises: unhandled rejection
button.addEventListener("click", async () => { await save(); }); // fine
items.forEach(async (i) => await save(i));        // no-misused-promises: forEach ignores the promise
function greet(user: User) { if (user) {} }        // no-unnecessary-condition: `user` can never be null here
```

### 14. Newer TypeScript features worth using

```ts
// satisfies (4.9) — see #4

// const type parameters (5.0): infer literal types without `as const` at call sites
function defineRoutes<const T extends readonly string[]>(routes: T) { return routes; }
const r = defineRoutes(["/home", "/about"]);      // readonly ["/home", "/about"]

// using / await using (5.2) — explicit resource management (auto cleanup at block end)
class DbConnection implements AsyncDisposable {
  async query(sql: string) { /* ... */ }
  async [Symbol.asyncDispose]() { await this.close(); }
  private async close() {}
}
async function report() {
  await using db = await openConnection();        // closed automatically, even if an error is thrown
  return db.query("SELECT 1");
}
// (needs a runtime with Symbol.dispose/asyncDispose — modern Node — or a polyfill)

// NoInfer (5.4): stop a parameter from influencing inference
function createStore<T extends string>(states: T[], initial: NoInfer<T>) {}

// Inferred type predicates (5.5): filter narrows automatically
const ids = [1, null, 3].filter((x) => x !== null); // number[]

// erasableSyntaxOnly (5.8): forbid enums/namespaces/parameter properties so Node can run .ts by stripping types
```

TypeScript is also being ported to a **native (Go) compiler** (`tsgo`, TypeScript 7), which makes type-checking large projects many times faster — same language, faster tooling.

### 15. Project organization

- **Colocate** types with the code that owns them (`orders/types.ts`), not one giant `types.ts`.
- Share cross-app types through a package (`@acme/api-types`) or generated clients.
- Pick **one convention** (`type` vs `interface`) and enforce it with lint.
- Path aliases (`@/…`) to avoid `../../../`.
- Keep type-check fast: `skipLibCheck`, `incremental`, project references in monorepos, avoid huge recursive types in hot paths.

### 16. Migrating a JS codebase to TypeScript

1. Add `tsconfig` with `allowJs: true`, `checkJs: false`, `strict: false`; get the build working.
2. Rename files gradually (`.js` → `.ts`), starting with **leaf utilities** and **boundaries** (API client, models).
3. Add types for external data first (schemas at the edges).
4. Turn on strict flags **one at a time** (`noImplicitAny` → `strictNullChecks` → …), fixing errors per folder.
5. Track remaining `any`/`@ts-expect-error` counts and burn them down; block new ones with lint.

### Production checklist

- [ ] `strict` + extra safety flags; `tsc --noEmit` in CI
- [ ] No `any` (lint-enforced); `unknown` + narrowing instead
- [ ] External data validated with schemas; types inferred from schemas/codegen
- [ ] Discriminated unions + exhaustive switches for state machines
- [ ] No non-null assertions without a comment; no `as` on external data
- [ ] `import type`, unions/`as const` instead of enums
- [ ] typescript-eslint type-aware rules (`no-floating-promises`, `no-misused-promises`, exhaustiveness)
- [ ] Explicit types on exported functions & public APIs
- [ ] Typed state/query hooks (`withTypes`, `queryOptions`)
- [ ] `@ts-expect-error` with reasons only; tracked and reduced

### Interview Qs

1. How do you make TypeScript "actually safe" in a large codebase?
2. Why is `as` dangerous for API responses? What do you do instead?
3. `any` vs `unknown` — and how do you prevent `any` from spreading?
4. How do you keep frontend and backend types in sync?
5. How do you make impossible states unrepresentable?
6. What does `noUncheckedIndexedAccess` change?
7. `@ts-ignore` vs `@ts-expect-error`?
8. Which ESLint rules catch async bugs in TS? → `no-floating-promises`, `no-misused-promises`.
9. What is `using` / explicit resource management?
10. How would you migrate a large JS project to TS?

---

## 41. Common Errors & Fixes

| Error | Meaning / Fix |
|---|---|
| `Object is possibly 'null' / 'undefined'` | Narrow (`if`, `?.`, `??`), or assert if you're sure |
| `Property 'x' does not exist on type 'Y'` | Typo, missing type, or needs narrowing (`in`, guard) |
| `Type 'string' is not assignable to type '"a" \| "b"'` | Literal widened → `as const` or annotate |
| `Argument of type 'X' is not assignable to parameter of type 'Y'` | Wrong shape; check the types |
| `Element implicitly has an 'any' type because expression of type 'string' can't be used to index type` | Use `keyof typeof obj` or a `Record<string, T>` |
| `Parameter 'x' implicitly has an 'any' type` | Add a type annotation |
| `Cannot find module 'x' or its corresponding type declarations` | Install `@types/x` or add `declare module "x"` |
| `'x' is declared but its value is never read` | Remove it or prefix with `_` |
| `Not all code paths return a value` | Add a return in every branch |
| `Type instantiation is excessively deep` | Recursive type too deep; simplify |
| `Property 'x' has no initializer` | Initialize in constructor, make optional, or `x!: T` |
| `This expression is not callable` | Union of incompatible function types; narrow first |
| `An object literal may only specify known properties` | Excess property check; fix typo or widen type |

```ts
// Indexing an object with a string
const colors = { red: "#f00", blue: "#00f" };
function getColor(name: string) {
  return colors[name];                               // ❌ implicit any
}
function getColor2(name: keyof typeof colors) {
  return colors[name];                               // ✅
}
function getColor3(name: string) {
  return name in colors ? colors[name as keyof typeof colors] : undefined; // ✅ runtime check
}

// Object.keys returns string[] (not keyof T) because objects can have extra keys at runtime
for (const key of Object.keys(colors) as (keyof typeof colors)[]) console.log(colors[key]);
```

---

## 42. Type Challenges

Classic "implement this type" questions (from type-challenges).

```ts
// 1. First element of a tuple
type First<T extends any[]> = T extends [infer F, ...any[]] ? F : never;
type F1 = First<[3, 2, 1]>; // 3

// 2. Length of a tuple
type Length<T extends readonly any[]> = T["length"];
type L1 = Length<["a", "b", "c"]>; // 3

// 3. If
type If<C extends boolean, T, F> = C extends true ? T : F;

// 4. Concat tuples
type Concat<A extends any[], B extends any[]> = [...A, ...B];

// 5. Includes
type Includes<T extends readonly any[], U> = U extends T[number] ? true : false;

// 6. Push / Unshift
type Push<T extends any[], U> = [...T, U];
type Unshift<T extends any[], U> = [U, ...T];

// 7. Tuple to object
type TupleToObject<T extends readonly (string | number | symbol)[]> = { [K in T[number]]: K };
type TO = TupleToObject<["a", "b"]>; // { a: "a"; b: "b" }

// 8. Trim left
type TrimLeft<S extends string> = S extends ` ${infer R}` | `\n${infer R}` | `\t${infer R}` ? TrimLeft<R> : S;

// 9. Replace
type Replace<S extends string, From extends string, To extends string> =
  From extends "" ? S : S extends `${infer L}${From}${infer R}` ? `${L}${To}${R}` : S;

// 10. Deep readonly
type DeepReadonly<T> = { readonly [K in keyof T]: T[K] extends Function ? T[K] : T[K] extends object ? DeepReadonly<T[K]> : T[K] };

// 11. Union to intersection
type UnionToIntersection<U> = (U extends any ? (x: U) => void : never) extends (x: infer I) => void ? I : never;

// 12. Flatten array type
type Flatten<T extends any[]> = T extends [infer H, ...infer R]
  ? H extends any[] ? [...Flatten<H>, ...Flatten<R>] : [H, ...Flatten<R>]
  : [];
type FL = Flatten<[1, [2, [3]], 4]>; // [1, 2, 3, 4]

// 13. Get required keys
type RequiredKeys<T> = { [K in keyof T]-?: {} extends Pick<T, K> ? never : K }[keyof T];
type RK = RequiredKeys<{ a: string; b?: number }>; // "a"

// 14. Dot-path keys of a nested object
type Paths<T> = T extends object
  ? { [K in keyof T & string]: T[K] extends object ? K | `${K}.${Paths<T[K]>}` : K }[keyof T & string]
  : never;
type P = Paths<{ user: { name: string; address: { city: string } } }>;
// "user" | "user.name" | "user.address" | "user.address.city"

// 15. Readonly for specific keys only
type MyReadonly2<T, K extends keyof T = keyof T> = Omit<T, K> & { readonly [P in K]: T[P] };
```

---

## 43. Most Asked Interview Questions

### Basics

1. **What is TypeScript and why use it over JavaScript?**
2. **Is TypeScript compiled or interpreted? Do types exist at runtime?** → Transpiled to JS; types are erased.
3. **What are the basic types in TS?**
4. **`any` vs `unknown` vs `never` vs `void`.**
5. **`type` vs `interface` — when to use which?**
6. **What is type inference?**
7. **Union vs intersection types.**
8. **What are literal types? What does `as const` do?**
9. **What are tuples?**
10. **What are enums? Numeric vs string vs const enums? Alternatives?**
11. **Optional properties & optional chaining.**
12. **`null` vs `undefined` & `strictNullChecks`.**

### Intermediate

13. **What is type narrowing? List narrowing techniques.**
14. **What are type guards / user-defined type predicates (`x is T`)?**
15. **What are discriminated unions? How do you do exhaustiveness checking?**
16. **What are generics? Why not `any`?**
17. **Generic constraints (`extends`), `keyof` constraint example.**
18. **`keyof` and `typeof` operators.**
19. **Indexed access types.**
20. **Function overloads — when to use?**
21. **Access modifiers: public/private/protected vs `#private`.**
22. **Abstract class vs interface.**
23. **What is `readonly`? Is it deep?**
24. **Type assertion (`as`) vs type casting — are they the same?** → Assertion is compile-time only; no conversion happens.
25. **Non-null assertion `!` — risks?**
26. **What is `satisfies` and how is it different from annotation?**
27. **What are declaration files (`.d.ts`)? What is DefinitelyTyped?**
28. **How do you add types to an untyped library?**
29. **What is structural typing? Excess property checks?**
30. **What does `strict` enable in tsconfig?**

### Advanced

31. **Explain all utility types; implement `Partial`, `Pick`, `Omit`, `Record`, `ReturnType`.**
32. **What are mapped types? Key remapping with `as`?**
33. **What are conditional types? Distributive conditional types?**
34. **What does `infer` do?**
35. **Template literal types.**
36. **Declaration merging & module augmentation (e.g. adding `user` to Express `Request`).**
37. **Covariance & contravariance in function parameters.**
38. **Branded types.**
39. **Decorators.**
40. **How do you type a React component's props, children, events, refs, context, and generic components?**
41. **How to type Express request params/body/query?**
42. **How do you validate API data at runtime and keep types in sync?** → Zod + `z.infer`.
43. **Why does `Object.keys` return `string[]`?** → Structural typing: objects may have extra keys at runtime.
44. **Difference between `interface extends` and `&`?** → extends errors on conflicting props and is faster to check; `&` silently creates `never` for conflicts.
45. **How do you migrate a JS project to TS?** → `allowJs`, rename files gradually, start with loose settings and tighten `strict` flags, add types to boundaries first, use `// @ts-check` / JSDoc.
46. **`@ts-ignore` vs `@ts-expect-error`?** → expect-error fails if there is no error (so it doesn't go stale); prefer it.
47. **What is `declare`?** → Tells TS something exists (declared elsewhere, e.g. global script) without emitting code.
48. **What is `unique symbol`, `abstract new`, `this` types?** (advanced trivia)

### Quick-fire answers

- **`interface` or `type` for React props?** → Either; many teams use `type` for flexibility (unions).
- **How to make all properties optional except one?** → `Partial<T> & Pick<T, "id">`.
- **How to get the type of array elements?** → `(typeof arr)[number]` or `T[number]`.
- **How to get the resolved type of an async function?** → `Awaited<ReturnType<typeof fn>>`.
- **How to make a type from object values?** → `(typeof obj)[keyof typeof obj]`.
- **How to type a function that accepts any function?** → `(...args: any[]) => unknown` (not `Function`).
- **What is `object` vs `Object` vs `{}`?** → `object` = non-primitive; `{}` = anything except null/undefined; `Object` = similar to `{}`, avoid.

---

**End of TypeScript notes.**
