# JavaScript — Complete Notes

> Every major JS concept, each with an explanation, 2–3 examples and common interview questions.
> The **Most Asked Interview Questions** section and **Output-Based Questions** are at the end.

---

## Table of Contents

1. [Getting Started: What is JavaScript & Your First Program](#1-getting-started-what-is-javascript--your-first-program)
2. [var, let, const](#2-var-let-const)
3. [Data Types](#3-data-types)
4. [Operators, Control Flow & Loops](#4-operators-control-flow--loops)
5. [Type Coercion, == vs ===](#5-type-coercion--vs-)
6. [Functions (all types)](#6-functions)
7. [Scope, Lexical Scope, Scope Chain](#7-scope-lexical-scope-scope-chain)
8. [Hoisting & Temporal Dead Zone](#8-hoisting--temporal-dead-zone)
9. [How JavaScript Runs](#9-how-javascript-runs)
10. [Execution Context & Call Stack](#10-execution-context--call-stack)
11. [Closures](#11-closures)
12. [The `this` Keyword](#12-the-this-keyword)
13. [call, apply, bind (+ polyfills)](#13-call-apply-bind)
14. [Objects in Depth](#14-objects-in-depth)
15. [Copying: Shallow vs Deep](#15-shallow-vs-deep-copy)
16. [Destructuring, Spread, Rest](#16-destructuring-spread-rest)
17. [Prototypes & Inheritance](#17-prototypes--prototypal-inheritance)
18. [Classes](#18-classes)
19. [OOP in JavaScript (Object-Oriented Programming)](#19-oop-in-javascript-object-oriented-programming)
20. [Arrays & Array Methods (+ polyfills)](#20-arrays--array-methods)
21. [Strings](#21-strings)
22. [Higher-Order Functions, Currying, Composition](#22-higher-order-functions-currying-composition)
23. [Functional Programming in Depth](#23-functional-programming-in-depth)
24. [Debounce & Throttle](#24-debounce--throttle)
25. [Event Loop](#25-event-loop)
26. [Callbacks & Callback Hell](#26-callbacks--callback-hell)
27. [Promises (+ polyfills)](#27-promises)
28. [Async / Await](#28-async--await)
29. [Iterators & Generators](#29-iterators--generators)
30. [Symbol, Map, Set, WeakMap, WeakSet, WeakRef](#30-symbol-map-set-weakmap-weakset)
31. [Modules (CommonJS vs ESM)](#31-modules)
32. [Build Tooling: Transpilers, Bundlers & the JS Toolchain](#32-build-tooling-transpilers-bundlers--the-js-toolchain)
33. [Error Handling](#33-error-handling)
34. [Debugging JavaScript](#34-debugging-javascript)
35. [DOM & Events (Bubbling, Capturing, Delegation)](#35-dom--events)
36. [Browser Storage & Cookies](#36-browser-storage--cookies)
37. [Memory Management & Garbage Collection](#37-memory-management--garbage-collection)
38. [Strict Mode](#38-strict-mode)
39. [Proxy & Reflect](#39-proxy--reflect)
40. [Getters, Setters, Property Descriptors](#40-getters-setters-property-descriptors)
41. [Design Patterns](#41-design-patterns)
42. [Web APIs (fetch, AbortController, Workers, rAF, Observers)](#42-web-apis)
43. [Binary Data & Files in the Browser](#43-binary-data--files-in-the-browser)
44. [Browser Internals: Rendering Pipeline, Web Components & Service Workers (PWA)](#44-browser-internals-rendering-pipeline-web-components--service-workers-pwa)
45. [Date, Math, Number, Intl](#45-date-math-number-intl)
46. [Dates & Time Zones in Depth](#46-dates--time-zones-in-depth)
47. [Regular Expressions](#47-regular-expressions)
48. [Networking for Frontend: What Happens When You Type a URL](#48-networking-for-frontend-what-happens-when-you-type-a-url)
49. [Performance Concepts](#49-performance-concepts)
50. [Security Basics (XSS, CSRF, CORS)](#50-security-basics)
51. [Modern JS (ES6 → ES2025)](#51-modern-js-features)
52. [Polyfill Collection](#52-polyfill-collection)
53. [Testing JavaScript (Vitest / Jest)](#53-testing-javascript-vitest--jest)
54. [Production-Grade JavaScript](#54-production-grade-javascript)
55. [Code Smells & Refactoring Catalog](#55-code-smells--refactoring-catalog)
56. [Data Structures & Algorithms in JavaScript](#56-data-structures--algorithms-in-javascript)
57. [Output-Based Questions](#57-output-based-questions)
58. [Most Asked Interview Questions](#58-most-asked-interview-questions)

---

## 1. Getting Started: What is JavaScript & Your First Program

**JavaScript (JS)** is the programming language of the web. HTML gives a page its structure, CSS its looks, and JavaScript its **behaviour**: clicks, forms, animations, fetching data, and whole apps like Gmail or Figma.

Where JavaScript runs:
- **In the browser** — every browser has a JS engine (Chrome's is V8).
- **On the server / your computer** — with **Node.js** (APIs, scripts, tools).
- Also mobile apps (React Native), desktop apps (Electron), edge functions.

JS is **dynamically typed** (no type declarations), **single-threaded** (one thing at a time, with async for waiting), and has nothing to do with Java despite the name.

### Three ways to run JavaScript

**1. Browser console** — press `F12` / `Cmd+Option+J` → Console tab → type code:

```js
2 + 3            // 5
"hello".toUpperCase()  // "HELLO"
```

**2. In a web page** with a `<script>` tag:

```html
<!DOCTYPE html>
<html>
  <body>
    <h1 id="title">Hello</h1>
    <button id="btn">Click me</button>

    <!-- external file (preferred) -->
    <script src="app.js" defer></script>
  </body>
</html>
```

```js
// app.js
const title = document.getElementById("title");
document.getElementById("btn").addEventListener("click", () => {
  title.textContent = "You clicked!";
});
```

**3. With Node.js** — run a `.js` file from the terminal:

```js
// hello.js
console.log("Hello, World!");
```

```bash
node hello.js      # → Hello, World!
node               # interactive REPL (type .exit to quit)
```

### console — showing output & debugging

```js
console.log("Hello");                 // normal output
console.log("Age:", 25, true);        // many values, separated by spaces
const name = "Rohit";
console.log(`Hi ${name}`);            // template literal — put variables inside ${}

console.error("Something failed");    // red error output
console.warn("Careful!");             // yellow warning
console.table([{ id: 1, name: "A" }, { id: 2, name: "B" }]); // table view
console.log(typeof name);             // "string"
```

### Getting input (browser only)

```js
const userName = prompt("What is your name?");   // always returns a string (or null)
alert(`Hello, ${userName}!`);                     // popup message
const ok = confirm("Are you sure?");              // true / false

const age = Number(prompt("Your age?"));          // convert string → number
```

(Real apps use HTML forms and inputs instead of popups.)

### Comments

```js
// single-line comment

/*
  multi-line
  comment
*/

/**
 * JSDoc comment — documents a function for editors/tools.
 * @param {number} a
 * @param {number} b
 * @returns {number}
 */
function add(a, b) { return a + b; }
```

### Statements, semicolons & blocks

- A program is a list of **statements**, usually one per line.
- Semicolons `;` end statements. JS inserts them automatically if you forget (**ASI**), but that can cause bugs — most teams use semicolons or let **Prettier** handle it.
- `{ }` groups statements into a **block** (for `if`, loops, functions).
- JS is **case-sensitive**: `name` and `Name` are different.

```js
let score = 10;
if (score > 5) {
  console.log("Passed");
}
```

```js
// ASI trap: a newline after `return` ends the statement
function getUser() {
  return
  { name: "A" };
}
getUser(); // undefined!
```

### Your first small programs

```js
// 1. Even or odd
const n = 7;
if (n % 2 === 0) {
  console.log(`${n} is even`);
} else {
  console.log(`${n} is odd`);
}
```

```js
// 2. Multiplication table
const num = 5;
for (let i = 1; i <= 10; i++) {
  console.log(`${num} x ${i} = ${num * i}`);
}
```

```js
// 3. Simple function
function greet(name) {
  return `Hello, ${name}!`;
}
console.log(greet("Rohit"));  // Hello, Rohit!
```

```js
// 4. Counter button (browser)
let count = 0;
const button = document.querySelector("#btn");
button.addEventListener("click", () => {
  count++;
  button.textContent = `Clicked ${count} times`;
});
```

### Common beginner errors

| Error | Meaning | Example |
|---|---|---|
| `SyntaxError` | Invalid code (missing bracket, quote, comma) | `if (x > 5 { }` |
| `ReferenceError` | Using a variable that doesn't exist (often a typo) | `console.log(nmae)` |
| `TypeError` | Using a value the wrong way | `null.length`, `undefined()` |
| `RangeError` | Value out of allowed range | `new Array(-1)`, infinite recursion |

Read the error message + the file/line number it points to; the browser console and Node both show them.

### Good habits from day one

- Use `const` by default, `let` when the value changes, never `var` (see next section).
- Use `===` instead of `==`.
- Use meaningful names (`totalPrice`, not `tp`) in `camelCase`.
- Put scripts at the end of `<body>` or use `defer`.
- Use an editor with ESLint + Prettier (VS Code).

**Interview Qs**
- What is JavaScript? Where can it run? → Browser and server (Node.js), plus mobile/desktop via frameworks.
- Java vs JavaScript? → Unrelated languages; similar name for marketing reasons.
- Is JS case-sensitive? → Yes.
- Are semicolons required? → No (ASI), but relying on ASI can cause bugs like the `return` newline trap.
- Difference between `console.log` and `alert`? → Console output for developers vs a blocking popup for users.

---

## 2. var, let, const

| Feature | `var` | `let` | `const` |
|---|---|---|---|
| Scope | Function | Block | Block |
| Hoisted | Yes, initialised to `undefined` | Yes, but in TDZ | Yes, but in TDZ |
| Re-declare in same scope | ✅ | ❌ | ❌ |
| Re-assign | ✅ | ✅ | ❌ |
| Creates property on `window` (global) | ✅ | ❌ | ❌ |
| Must initialise at declaration | ❌ | ❌ | ✅ |

### Example 1 — block scope

```js
if (true) {
  var a = 1;
  let b = 2;
  const c = 3;
}
console.log(a); // 1
console.log(b); // ReferenceError: b is not defined
```

### Example 2 — redeclaration

```js
var x = 1;
var x = 2;     // fine
let y = 1;
let y = 2;     // SyntaxError: Identifier 'y' has already been declared
```

### Example 3 — const with objects

`const` makes the **binding** immutable, not the value.

```js
const user = { name: "A" };
user.name = "B";      // allowed (mutating)
user = {};            // TypeError: Assignment to constant variable
const frozen = Object.freeze({ n: 1 });
frozen.n = 2;         // silently ignored (TypeError in strict mode)
```

### Example 4 — The classic loop problem

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// 3 3 3  -> one shared `i` (function scoped)

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// 0 1 2  -> a new `i` binding per iteration
```

Fix with `var` using a closure (IIFE):

```js
for (var i = 0; i < 3; i++) {
  (function (j) {
    setTimeout(() => console.log(j), 100);
  })(i);
}
// 0 1 2
```

### Global object

```js
var g1 = "var";
let g2 = "let";
console.log(window.g1); // "var"
console.log(window.g2); // undefined
```

**Interview Qs**
- Why was `let/const` introduced? → Block scoping, TDZ to catch use-before-declare bugs, no accidental redeclaration, no global object pollution.
- Can you change a `const` array? → Yes, you can `push` etc. You can't reassign it.
- Default choice? → `const` by default, `let` when you need to reassign, avoid `var`.

---

## 3. Data Types

JS has **8 types**: 7 primitives + Object.

| Primitive | Example |
|---|---|
| `string` | `"hi"` |
| `number` | `42`, `3.14`, `NaN`, `Infinity` |
| `bigint` | `10n` |
| `boolean` | `true` |
| `undefined` | declared but not assigned |
| `null` | intentional "no value" |
| `symbol` | `Symbol("id")` — unique |

**Object (reference type)**: objects, arrays, functions, Date, RegExp, Map, Set…

### Primitive vs Reference

- Primitives are **immutable** and **copied by value**.
- Objects are **copied by reference** (the variable holds a reference/address).

```js
let a = 10;
let b = a;   // copy of the value
b = 20;
console.log(a); // 10
```

```js
const obj1 = { name: "Rohit" };
const obj2 = obj1;   // same reference
obj2.name = "Dev";
console.log(obj1.name); // "Dev"
```

```js
// Comparing objects compares references
console.log({} === {});        // false
const x = {}; const y = x;
console.log(x === y);          // true
```

### typeof

```js
typeof "a"          // "string"
typeof 1            // "number"
typeof NaN          // "number"   <- trap
typeof 1n           // "bigint"
typeof true         // "boolean"
typeof undefined    // "undefined"
typeof null         // "object"   <- historical bug
typeof Symbol()     // "symbol"
typeof {}           // "object"
typeof []           // "object"   -> use Array.isArray
typeof function(){} // "function"
typeof undeclaredVar // "undefined" (no ReferenceError)
```

### null vs undefined

| `undefined` | `null` |
|---|---|
| Default value of uninitialised variables, missing params, missing props | Assigned deliberately to mean "empty" |
| `typeof` → `"undefined"` | `typeof` → `"object"` |
| `Number(undefined)` → `NaN` | `Number(null)` → `0` |

```js
null == undefined   // true (loose)
null === undefined  // false
```

### NaN

"Not a Number" — result of invalid math. It's the **only value not equal to itself**.

```js
NaN === NaN          // false
Number.isNaN(NaN)    // true
isNaN("hello")       // true  (coerces to number first — unreliable)
Number.isNaN("hello")// false (no coercion — correct)
Object.is(NaN, NaN)  // true
```

### Number precision

Numbers are IEEE-754 64-bit doubles.

```js
0.1 + 0.2              // 0.30000000000000004
0.1 + 0.2 === 0.3      // false
Math.abs(0.1 + 0.2 - 0.3) < Number.EPSILON // true
Number.MAX_SAFE_INTEGER // 9007199254740991 (2^53 - 1)
9007199254740993n + 1n  // BigInt for bigger exact integers
```

**Interview Qs**
- Why is `typeof null` "object"? → Bug from the first JS version (type tag 0 = object, null pointer was 0). Never fixed for backwards compatibility.
- How to check an array? → `Array.isArray(x)`.
- How to check an actual object? → `x !== null && typeof x === "object" && !Array.isArray(x)`.

---

## 4. Operators, Control Flow & Loops

The building blocks every program uses. Interviewers love the edge cases here (short-circuiting, `??` vs `||`, `for...in` vs `for...of`, switch fall-through, `++i` vs `i++`).

### 1. Arithmetic operators

```js
10 + 3;   // 13
10 - 3;   // 7
10 * 3;   // 30
10 / 3;   // 3.3333333333333335  (no integer division — use Math.trunc)
10 % 3;   // 1   remainder (sign follows the dividend: -10 % 3 === -1)
2 ** 10;  // 1024 exponent (same as Math.pow(2, 10))

Math.trunc(10 / 3);  // 3 — integer division
((-10 % 3) + 3) % 3; // 2 — true modulo for negatives (useful for circular indexes)

1 / 0;    // Infinity
-1 / 0;   // -Infinity
0 / 0;    // NaN
```

### 2. Increment / decrement — prefix vs postfix

```js
let a = 5;
const b = a++; // postfix: returns OLD value, then increments → b = 5, a = 6
const c = ++a; // prefix: increments first, returns NEW value → c = 7, a = 7

let i = 0;
console.log(i++ + ++i); // 0 + 2 = 2
```

In production, prefer `i += 1` on its own line — clearer than `++` hidden inside expressions.

### 3. Assignment operators

```js
let x = 10;
x += 5;   // 15
x -= 3;   // 12
x *= 2;   // 24
x /= 4;   // 6
x %= 4;   // 2
x **= 3;  // 8

// Logical assignment (ES2021)
let user = { name: "", age: 0, theme: null };
user.name ||= "Guest";   // assigns if falsy        → "Guest"
user.age ??= 18;          // assigns if null/undefined → stays 0
user.theme ??= "dark";    // → "dark"
user.isAdmin &&= false;   // assigns only if truthy (undefined stays undefined)
```

### 4. Comparison operators

```js
5 > 3;          // true
"b" > "a";      // true — strings compare by UTF-16 code units, lexicographically
"10" > "9";     // false! string comparison: "1" < "9"
10 > "9";       // true  — string converted to number
"apple" < "Apple"; // false — uppercase letters have smaller codes ("A"=65, "a"=97)

null >= 0;      // true  (relational → Number(null) = 0)
null == 0;      // false (== treats null specially)
undefined > 0;  // false (NaN comparisons are always false)
NaN <= NaN;     // false
```

Use `localeCompare` for human sorting, and convert explicitly (`Number(x)`) before comparing mixed types.

### 5. Logical operators & short-circuiting

`&&`, `||` and `??` **return one of the operands** (not necessarily a boolean) and **stop evaluating** as soon as the result is known.

| Operator | Returns | Short-circuits when |
|---|---|---|
| `a \|\| b` | first **truthy** operand, else the last | `a` is truthy |
| `a && b` | first **falsy** operand, else the last | `a` is falsy |
| `a ?? b` | `a` unless it is `null`/`undefined`, else `b` | `a` is not null/undefined |
| `!a` | boolean opposite | — |

```js
"hello" || "default";  // "hello"
"" || "default";        // "default"
0 || 10;                // 10   ⚠️ 0 is a valid value but gets replaced
0 ?? 10;                // 0    ✅
null ?? "fallback";     // "fallback"

"a" && "b";             // "b"
0 && "b";               // 0
user && user.name;      // old-school safe access (now: user?.name)

// Short-circuit prevents calls
isLoggedIn && showDashboard();       // runs only if logged in
cache.get(key) || computeAndStore(); // computes only on a miss

!!"text";               // true  — double NOT converts to boolean
Boolean("text");        // true  — clearer
```

`??` cannot be mixed with `||`/`&&` without parentheses:

```js
a || b ?? c;    // SyntaxError
(a || b) ?? c;  // ✅
```

**Precedence**: `!` > `&&` > `||` = `??` (same level, but `??` can't be mixed with `&&`/`||` without parentheses).

```js
true || false && false;   // true  (&& binds tighter: true || (false && false))
```

### 6. Ternary (conditional) operator

```js
const status = age >= 18 ? "adult" : "minor";

// Nested ternaries get unreadable fast — use if/else or a lookup table instead
const grade = score >= 90 ? "A" : score >= 75 ? "B" : score >= 50 ? "C" : "F";
```

### 7. Other operators

```js
// typeof / instanceof / in / delete / void
typeof 42;                    // "number"
[] instanceof Array;          // true
"name" in { name: "A" };      // true (checks prototype chain too)
const o = { a: 1 }; delete o.a; // removes a property (returns true)
void 0;                       // undefined

// Comma operator — evaluates all, returns the LAST (rarely used outside for-loops)
let r = (1, 2, 3);            // 3
for (let i = 0, j = 10; i < j; i++, j--) {}

// Optional chaining & nullish (covered in Objects)
user?.profile?.email;
user.getName?.();

// Spread / rest (covered in Destructuring)
Math.max(...[1, 2, 3]);

// Unary plus / minus convert to number
+"42";    // 42
-"5";     // -5
+true;    // 1
+"";      // 0
+"abc";   // NaN
```

### 8. Bitwise operators

Work on 32-bit signed integers. Rare in app code, common in interviews/DSA, flags and performance tricks.

```js
5 & 3;    // 1   AND   (101 & 011 = 001)
5 | 3;    // 7   OR    (101 | 011 = 111)
5 ^ 3;    // 6   XOR   (101 ^ 011 = 110)
~5;       // -6  NOT   (-(n + 1))
5 << 1;   // 10  left shift  (× 2)
5 >> 1;   // 2   right shift (÷ 2, keeps sign)
-5 >>> 0; // 4294967291 unsigned right shift

// Practical uses
const isEven = (n) => (n & 1) === 0;
const isPowerOfTwo = (n) => n > 0 && (n & (n - 1)) === 0;
~~4.7;          // 4 — truncate (only safe for 32-bit ints; prefer Math.trunc)
[1, 2, 3, 2, 1].reduce((a, b) => a ^ b); // 3 — find the single non-duplicate

// Permission flags
const READ = 1, WRITE = 2, DELETE = 4;   // 001, 010, 100
let perms = READ | WRITE;                 // 011
const canWrite = (perms & WRITE) !== 0;   // true
perms &= ~WRITE;                          // remove WRITE → 001
```

### 9. Operator precedence (most useful part)

From high to low (simplified):

1. `()` grouping
2. `.` `[]` `?.` `()` call, `new`
3. `++` `--` (postfix)
4. `!` `~` `+x` `-x` `++x` `--x` `typeof` `void` `delete` `await`
5. `**` (right-associative)
6. `*` `/` `%`
7. `+` `-`
8. `<<` `>>` `>>>`
9. `<` `<=` `>` `>=` `in` `instanceof`
10. `==` `!=` `===` `!==`
11. `&` → `^` → `|`
12. `&&`
13. `||` `??`
14. `? :` ternary
15. `=` `+=` … assignment (right-associative)
16. `,` comma

```js
2 + 3 * 4;        // 14
(2 + 3) * 4;      // 20
2 ** 3 ** 2;      // 512 = 2 ** 9 (right-to-left)
-2 ** 2;          // SyntaxError — must write (-2) ** 2
typeof 1 + 2;     // "number2" — typeof binds first
a = b = c = 5;    // assignment is right-associative
```

**Best practice**: when in doubt, add parentheses. Readability beats memorizing the table.

---

### 10. if / else

```js
if (score >= 90) {
  grade = "A";
} else if (score >= 75) {
  grade = "B";
} else {
  grade = "C";
}
```

Best practices:
- Always use braces (avoid the `if (x) doThing();` single-line trap when someone adds a second line).
- Prefer **early returns** over deep nesting.
- Prefer **positive conditions** (`if (isValid)` over `if (!isInvalid)`).
- Extract complex conditions into well-named variables.

```js
// ❌
if (user && user.age >= 18 && user.country === "IN" && !user.banned && user.kyc === "done") {}

// ✅
const isAdult = user.age >= 18;
const isEligibleRegion = user.country === "IN";
const isVerified = user.kyc === "done" && !user.banned;
if (isAdult && isEligibleRegion && isVerified) {}
```

### 11. switch

Uses **strict equality (`===`)**. Without `break`, execution **falls through** into the next case.

```js
function getDayType(day) {
  switch (day) {
    case "sat":
    case "sun":                // intentional fall-through: groups cases
      return "weekend";
    case "mon":
    case "tue":
    case "wed":
    case "thu":
    case "fri":
      return "weekday";
    default:
      throw new Error(`Unknown day: ${day}`);
  }
}
```

```js
// ❌ Accidental fall-through bug
switch (status) {
  case "paid":
    sendReceipt();
  case "shipped":        // runs for "paid" too — missing break!
    sendTracking();
    break;
}

// switch(true) pattern for ranges
switch (true) {
  case score >= 90: grade = "A"; break;
  case score >= 75: grade = "B"; break;
  default: grade = "C";
}

// Block scope per case to avoid "already declared" errors
switch (action.type) {
  case "add": {
    const item = action.payload;
    break;
  }
  case "remove": {
    const item = action.id; // OK, separate block
    break;
  }
}
```

**Lookup object vs switch**: for simple value → value mappings, a lookup object/Map is shorter and easier to extend.

```js
const HTTP_MESSAGES = { 200: "OK", 404: "Not Found", 500: "Server Error" };
const msg = HTTP_MESSAGES[code] ?? "Unknown";
```

---

### 12. Loops

#### for

```js
for (let i = 0; i < 5; i++) console.log(i);      // 0..4
for (let i = arr.length - 1; i >= 0; i--) {}      // reverse
for (let i = 0; i < arr.length; i += 2) {}        // step by 2
```

#### while & do...while

```js
let attempts = 0;
while (attempts < 3 && !connected) {
  connected = tryConnect();
  attempts++;
}

// do...while runs AT LEAST once
let input;
do {
  input = prompt("Enter a number > 10");
} while (Number(input) <= 10);
```

#### for...of — iterate **values** of iterables

Works on arrays, strings, Maps, Sets, NodeLists, `arguments`, generators — **not plain objects**.

```js
for (const fruit of ["apple", "mango"]) console.log(fruit);
for (const ch of "hi👍") console.log(ch);                   // handles emojis correctly
for (const [key, value] of new Map([["a", 1]])) {}
for (const [i, item] of ["x", "y"].entries()) console.log(i, item); // with index
for (const [k, v] of Object.entries({ a: 1, b: 2 })) {}    // objects via entries
```

#### for...in — iterate **keys** (enumerable, including inherited)

```js
const user = { name: "A", age: 25 };
for (const key in user) console.log(key, user[key]);

// ⚠️ Don't use for...in on arrays: keys are strings, order/extra props can surprise you
const arr = [10, 20];
arr.extra = "x";
for (const i in arr) console.log(i); // "0", "1", "extra"
for (const v of arr) console.log(v); // 10, 20
```

| | `for...in` | `for...of` |
|---|---|---|
| Iterates | Keys (property names, as strings) | Values |
| Works on | Any object (incl. inherited enumerable props) | Iterables (arrays, strings, Map, Set…) |
| Use for | Plain objects (prefer `Object.keys/entries`) | Arrays & collections |

#### Array methods vs loops

```js
const nums = [1, 2, 3, 4];
nums.forEach((n) => console.log(n));  // side effects, can't break
nums.map((n) => n * 2);               // transform
nums.filter((n) => n % 2);            // select
nums.some((n) => n > 3);              // stops at first true (like break)
nums.find((n) => n > 1);              // stops at first match
```

Use `for...of` when you need `break`/`continue`/`await` in sequence, or when performance-critical. Use array methods for readable transformations.

### 13. break, continue, labels

```js
for (const n of [1, 2, 3, 4, 5]) {
  if (n === 2) continue;   // skip this iteration
  if (n === 4) break;      // exit the loop
  console.log(n);          // 1, 3
}

// Labels: break out of NESTED loops
outer: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (i * j === 2) break outer;    // exits both loops
    console.log(i, j);
  }
}
```

(Labels are rare — extracting the nested loop into a function and using `return` is usually cleaner.)

### 14. Loops + async

```js
const ids = [1, 2, 3];

// Sequential (each waits for the previous)
for (const id of ids) {
  await saveItem(id);
}

// Parallel
await Promise.all(ids.map((id) => saveItem(id)));

// ❌ forEach doesn't wait
ids.forEach(async (id) => await saveItem(id));

// for await...of over async iterables (streams, paginated APIs)
for await (const page of fetchPages()) render(page);
```

### 15. Loop performance & pitfalls

```js
// Infinite loop — forgot to update the condition variable
let k = 0;
while (k < 5) { console.log(k); } // never ends → freezes the tab

// Modifying an array while iterating over it
const list = [1, 2, 3, 4];
for (let i = 0; i < list.length; i++) {
  if (list[i] % 2 === 0) list.splice(i, 1); // skips elements! iterate backwards or use filter
}
const odd = list.filter((n) => n % 2 !== 0); // ✅

// Closures in loops with var (see var/let section)
for (var v = 0; v < 3; v++) setTimeout(() => console.log(v)); // 3 3 3
for (let v2 = 0; v2 < 3; v2++) setTimeout(() => console.log(v2)); // 0 1 2

// O(n²) nested lookups → use a Map/Set
const allowed = new Set(allowedIds);
items.filter((it) => allowed.has(it.id)); // O(n) instead of items.filter(it => allowedIds.includes(it.id))
```

### 16. Exceptions as control flow (try/catch/finally)

Covered fully in Error Handling. Rule: use exceptions for **exceptional** cases, not normal branching.

```js
// ❌ using exceptions for normal logic
try { const user = users.find((u) => u.id === id); user.name; } catch { return "Unknown"; }
// ✅
return users.find((u) => u.id === id)?.name ?? "Unknown";
```

### Output questions

```js
console.log(1 + 2 + "3");         // "33"
console.log("1" + 2 + 3);         // "123"
console.log(3 > 2 > 1);           // false
console.log(0 || null || "" || undefined); // undefined (last operand)
console.log(1 && "a" && 0 && "b"); // 0
console.log(null ?? 0 ?? 1);      // 0
let n = 1; console.log(n++ + n++); // 1 + 2 = 3
console.log(typeof typeof 1);     // "string"
console.log(!!"false", !!0, !![]); // true false true
console.log([] + null + 1);       // "null1"
for (const x in "ab") console.log(x); // "0", "1"
```

### Interview Qs

- **`||` vs `??`?** → `||` falls back on any falsy value (0, "", false); `??` only on null/undefined.
- **What do `&&` and `||` return?** → One of the operands (not necessarily a boolean) — short-circuit evaluation.
- **Prefix vs postfix increment?**
- **`for...in` vs `for...of` vs `forEach`?** (table above; forEach can't break or await)
- **How does `switch` compare values?** → Strict equality `===`. What happens without `break`? → Fall-through.
- **How do you break out of nested loops?** → Labels, or extract into a function and `return`.
- **Why is `"10" > "9"` false?** → Both strings → lexicographic comparison.
- **Give a real use of bitwise operators.** → Permission flags, even/odd, power-of-two check, XOR single-number problem.
- **Operator precedence of `&&` and `||`?** → `&&` binds tighter.

---

## 5. Type Coercion, == vs ===

**Coercion** = automatic (implicit) or manual (explicit) conversion of a value from one type to another.

- **Explicit**: `Number("5")`, `String(5)`, `Boolean(0)`, `parseInt("10px")`.
- **Implicit**: happens with operators — `+`, `-`, `==`, `if (...)`.

### Rules for `+`

If either operand is a string → string concatenation. Otherwise → numeric addition.

```js
1 + "2"        // "12"
"3" - 1        // 2   (- always numeric)
"3" * "2"      // 6
true + 1       // 2
null + 1       // 1
undefined + 1  // NaN
[] + []        // ""
[] + {}        // "[object Object]"
{} + []        // 0 in console (the {} is parsed as a block), "[object Object]" in an expression
"5" + 3 - 2    // "53" - 2 = 51
+"42"          // 42 (unary plus converts to number)
```

### Truthy & Falsy

Falsy values (only these 8): `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN`.
Everything else is truthy — including `"0"`, `"false"`, `[]`, `{}`, `function(){}`.

```js
if ([]) console.log("empty array is truthy");   // runs
if ("0") console.log("'0' is truthy");            // runs
Boolean(" ")  // true (space)
!!NaN         // false
```

### `==` (loose) vs `===` (strict)

- `===` compares **type and value**, no coercion.
- `==` coerces types first (Abstract Equality Algorithm).

```js
0 == ""          // true
0 == "0"         // true
"" == "0"        // false  (both strings, compared directly)
false == "0"     // true
null == 0        // false  (null only == undefined)
null >= 0        // true   (relational ops convert null to 0!)
[] == false      // true   ([] -> "" -> 0, false -> 0)
[] == ![]        // true
NaN == NaN       // false
```

### `Object.is`

Same as `===` except two edge cases:

```js
Object.is(NaN, NaN) // true   (=== gives false)
Object.is(0, -0)    // false  (=== gives true)
```

### Object → primitive conversion

Objects are converted with `Symbol.toPrimitive`, then `valueOf()`, then `toString()`.

```js
const money = {
  amount: 100,
  [Symbol.toPrimitive](hint) {
    return hint === "string" ? `$${this.amount}` : this.amount;
  },
};
console.log(`${money}`); // "$100"
console.log(money + 50); // 150
```

**Interview Qs**
- Difference between `==` and `===`? → `==` coerces, `===` doesn't. Prefer `===`; the only common use of `==` is `x == null` to check both null and undefined.
- Why `[] == ![]` is true? → `![]` is `false` → `[] == false` → both sides become `0`.

---

## 6. Functions

Functions are **first-class citizens**: they can be stored in variables, passed as arguments, returned from functions and have properties.

### Function declaration vs expression vs arrow

```js
// Declaration — hoisted
function add(a, b) { return a + b; }

// Expression — not hoisted (variable is)
const sub = function (a, b) { return a - b; };

// Named function expression — name is only visible inside
const fact = function f(n) { return n <= 1 ? 1 : n * f(n - 1); };

// Arrow function
const mul = (a, b) => a * b;
const square = x => x * x;
const makeObj = () => ({ ok: true }); // wrap object literal in ()
```

### Arrow vs normal functions

| Normal function | Arrow function |
|---|---|
| Own `this` (depends on call) | No own `this` — uses lexical `this` |
| Has `arguments` object | No `arguments` (use rest `...args`) |
| Can be used with `new` | Cannot be a constructor |
| Has `prototype` property | No `prototype` |
| Hoisted (declaration) | Not hoisted |
| Can be a method nicely | Bad as object methods (this = outer) |

```js
const obj = {
  name: "Rohit",
  normal() { console.log(this.name); },
  arrow: () => console.log(this.name),
};
obj.normal(); // "Rohit"
obj.arrow();  // undefined (this = module/global)
```

```js
// Arrow is great inside methods for callbacks
const timer = {
  seconds: 0,
  start() {
    setInterval(() => {
      this.seconds++; // `this` = timer (lexical)
    }, 1000);
  },
};
```

```js
function normal() { console.log(arguments); }
normal(1, 2); // [Arguments] { '0': 1, '1': 2 }

const arrow = (...args) => console.log(args);
arrow(1, 2);  // [1, 2]
```

### IIFE (Immediately Invoked Function Expression)

Runs immediately, creates a private scope. Used before modules existed.

```js
(function () {
  const privateVar = "secret";
  console.log("IIFE ran");
})();

(() => console.log("arrow IIFE"))();

const counter = (function () {
  let count = 0;
  return { inc: () => ++count, get: () => count };
})();
counter.inc(); counter.get(); // 1
```

### Parameters vs Arguments

- **Parameters**: names in the definition. **Arguments**: actual values passed.

```js
function greet(name = "Guest", greeting = `Hello ${name}`) { // default params can use earlier params
  return greeting;
}
greet();          // "Hello Guest"
greet(undefined); // default used (undefined triggers default)
greet(null);      // "Hello null" (null does NOT trigger default)
```

### Rest parameters

```js
function sum(...nums) { return nums.reduce((a, b) => a + b, 0); }
sum(1, 2, 3); // 6

function log(first, ...rest) { console.log(first, rest); }
log(1, 2, 3); // 1 [2, 3]
```

### Pure vs Impure functions

- **Pure**: same input → same output, no side effects.
- **Impure**: depends on/changes outside state, I/O, random, dates.

```js
const pureAdd = (a, b) => a + b;

let total = 0;
const impureAdd = (x) => (total += x); // modifies outside state
```

### Callback functions

A function passed to another function to be called later.

```js
function fetchData(cb) {
  setTimeout(() => cb({ id: 1 }), 500);
}
fetchData((data) => console.log(data));

[1, 2, 3].forEach((n) => console.log(n)); // also a callback
```

### Function properties

```js
function demo(a, b, c) {}
demo.length; // 3 (number of declared params, excluding rest/defaults)
demo.name;   // "demo"
demo.custom = "functions are objects";
```

### First-class vs Higher-order

- **First-class function**: language feature — functions are values.
- **Higher-order function (HOF)**: a function that takes and/or returns a function (`map`, `filter`, `setTimeout`, `debounce`).

**Interview Qs**
- Function statement vs expression vs declaration? → Statement = declaration (`function a(){}`), expression = assigned to a variable. Only declarations are fully hoisted.
- Anonymous function? → Function without a name; used as a value (callbacks). Can't be used as a declaration.
- Why can't arrow functions be constructors? → They have no `[[Construct]]`, no `prototype`, no own `this`.

---

## 7. Scope, Lexical Scope, Scope Chain

**Scope** = where a variable is accessible.

### Types of scope

1. **Global scope** — declared outside any function/block.
2. **Function (local) scope** — declared inside a function.
3. **Block scope** — `let`/`const` inside `{}` (if, for, while, plain blocks).
4. **Module scope** — top-level of an ES module is private to that module.

```js
const globalVar = "global";

function outer() {
  const fnVar = "function";
  if (true) {
    const blockVar = "block";
    console.log(globalVar, fnVar, blockVar); // all accessible
  }
  console.log(blockVar); // ReferenceError
}
outer();
```

### Lexical Scope (Static Scope)

**Lexical** = "based on where code is written". A function's scope is decided by **where it is defined in the source code**, not where it's called from.

```js
const name = "global";

function printName() {
  console.log(name);
}

function run() {
  const name = "inside run";
  printName(); // prints "global" — printName was DEFINED in global scope
}
run();
```

```js
function outer() {
  const secret = 42;
  function inner() {
    console.log(secret); // inner can see outer's variables (lexically nested)
  }
  return inner;
}
outer()(); // 42
```

### Lexical Environment

Every execution context has a **Lexical Environment** = 
- an **Environment Record** (the local variables), plus
- a reference to the **outer** lexical environment.

### Scope Chain

When a variable is used, JS looks in the current scope → then the outer one → … → global. If not found → `ReferenceError`. This chain of lookups is the **scope chain**.

```js
const a = 1;
function f1() {
  const b = 2;
  function f2() {
    const c = 3;
    console.log(a + b + c); // 6 — c (own), b (f1), a (global)
  }
  f2();
}
f1();
```

### Variable Shadowing

An inner variable with the same name "shadows" the outer one.

```js
let count = 10;
function f() {
  let count = 20; // shadows outer count
  console.log(count); // 20
}
f();
console.log(count); // 10
```

**Illegal shadowing**: you can't shadow a `let` with a `var` inside a nested block (because var would escape to the same function scope).

```js
let x = 1;
{
  var x = 2; // SyntaxError: Identifier 'x' has already been declared
}

var y = 1;
{
  let y = 2; // legal
}
```

### Dynamic scope (JS does NOT have it)

In dynamic scoping, variables resolve by the call stack. JS doesn't do this — but `this` behaves *somewhat* dynamically (depends on how a function is called).

**Interview Qs**
- What is lexical scope? → Scope determined by the physical placement of code; inner functions access outer variables.
- What is the scope chain? → The chain of lexical environments JS walks through to resolve an identifier.
- What's the difference between scope and context? → Scope = variable visibility. Context = the value of `this`.

---

## 8. Hoisting & Temporal Dead Zone

**Hoisting** = during the **creation phase** of an execution context, JS allocates memory for declarations before executing code. It looks like declarations are "moved to the top".

| Declaration | Hoisted? | Initial value |
|---|---|---|
| `var` | Yes | `undefined` |
| `let` / `const` | Yes | uninitialised (TDZ) |
| `function` declaration | Yes | the full function |
| function expression / arrow | Only the variable (as var/let/const rules) | — |
| `class` | Yes | uninitialised (TDZ) |

### Example 1 — var

```js
console.log(a); // undefined
var a = 5;
// engine sees: var a; console.log(a); a = 5;
```

### Example 2 — function declaration vs expression

```js
greet();  // "hello" — fully hoisted
function greet() { console.log("hello"); }

sayHi();  // TypeError: sayHi is not a function (it's undefined)
var sayHi = function () { console.log("hi"); };

sayBye(); // ReferenceError: Cannot access 'sayBye' before initialization
const sayBye = () => console.log("bye");
```

### Example 3 — TDZ

**Temporal Dead Zone** = time from the start of the block until the `let/const` declaration line is executed. Accessing the variable in the TDZ throws `ReferenceError`.

```js
{
  // TDZ for `score` starts
  console.log(typeof score); // ReferenceError (even typeof!)
  let score = 10;            // TDZ ends
}
```

```js
let x = "outer";
function test() {
  console.log(x); // ReferenceError — inner x is hoisted and in TDZ, shadows outer
  let x = "inner";
}
test();
```

### Function vs var name clash

```js
console.log(typeof foo); // "function" — function declarations win during creation
var foo = 1;
function foo() {}
console.log(typeof foo); // "number" — assignment runs during execution
```

**Interview Qs**
- Are let/const hoisted? → Yes, but they aren't initialised, so accessing them before declaration throws (TDZ).
- Why TDZ? → Catches bugs, makes `const` meaningful (can't observe it before it's assigned).

---

## 9. How JavaScript Runs

**JavaScript** is a high-level, single-threaded, garbage-collected, dynamically typed, multi-paradigm language (functional + OOP + prototype-based).

- **Single-threaded**: one call stack, does one thing at a time.
- **Non-blocking**: async work (timers, network, I/O) is handed to the environment (browser Web APIs / Node's libuv), and results come back through the **event loop**.
- **JIT compiled**: modern engines (V8 in Chrome/Node, SpiderMonkey in Firefox, JavaScriptCore in Safari) parse → build an AST → interpret into bytecode (Ignition in V8) → optimise hot code into machine code (TurboFan in V8). If the assumptions turn out wrong, the code is de-optimised.

### Engine vs Runtime

| Engine | Runtime |
|---|---|
| Parses and executes JS (V8) | Engine + APIs + event loop |
| Has the call stack and memory heap | Browser: DOM, fetch, setTimeout, localStorage |
| | Node: fs, http, process, libuv |

### Memory heap vs call stack

- **Call stack**: keeps track of which function is running (LIFO). Primitive values of local variables live in stack frames.
- **Heap**: unstructured memory where objects, arrays and functions live.

```js
function a() { b(); }
function b() { c(); }
function c() { console.trace(); } // shows c <- b <- a <- global
a();
```

```js
// Stack overflow: recursion without a base case
function recurse() { recurse(); }
recurse(); // RangeError: Maximum call stack size exceeded
```

**Interview Qs**
- Is JS interpreted or compiled? → Both: JIT compiled. It's parsed and compiled right before (and during) execution.
- Is JS single-threaded? → The language runs on one main thread, but the runtime uses other threads (libuv thread pool, browser threads, Web Workers).

---

## 10. Execution Context & Call Stack

An **Execution Context (EC)** is the environment where JS code is evaluated. Types:

1. **Global EC** — created once when the script starts. Creates the global object (`window` / `global`) and `this`.
2. **Function EC** — created on every function call.
3. **Eval EC** — for code inside `eval` (avoid).

### Two phases

1. **Creation (memory) phase**
   - Creates the lexical environment and variable environment.
   - `var` → `undefined`, functions → full definition, `let/const` → uninitialised.
   - Determines `this`.
   - Sets outer environment reference (scope chain).
2. **Execution phase** — runs code line by line, assigns values, calls functions.

```js
var n = 2;
function square(num) {
  var ans = num * num;
  return ans;
}
var square2 = square(n);
var square4 = square(4);
```

Step by step:
1. Global EC creation: `n = undefined`, `square = fn`, `square2 = undefined`, `square4 = undefined`.
2. Execution: `n = 2`. Call `square(2)` → new function EC pushed on stack → `num=2, ans=undefined` → execution `ans=4` → return → EC popped.
3. Same for `square(4)`.

### Call stack (LIFO)

```js
function first() {
  console.log("first start");
  second();
  console.log("first end");
}
function second() {
  console.log("second");
}
first();
// Stack: [global] -> [global, first] -> [global, first, second] -> [global, first] -> [global]
```

**Interview Qs**
- What is an execution context? → Wrapper holding the variables, scope chain and `this` for the currently running code.
- What happens when a function is called? → New EC is created and pushed to the call stack; after return it's popped.

---

## 11. Closures

A **closure** is a function **bundled together with its lexical environment**. A function remembers the variables of the scope where it was created **even after that outer function has finished executing**.

### Example 1 — Basic

```js
function outer() {
  const message = "Hello from outer";
  return function inner() {
    console.log(message);
  };
}
const fn = outer(); // outer has finished
fn();               // "Hello from outer" — inner still has access
```

### Example 2 — Counter (data privacy)

```js
function createCounter() {
  let count = 0; // private
  return {
    increment: () => ++count,
    decrement: () => --count,
    getCount: () => count,
  };
}
const c1 = createCounter();
const c2 = createCounter();
c1.increment(); c1.increment();
c2.increment();
console.log(c1.getCount(), c2.getCount()); // 2 1 — each has its own closure
console.log(c1.count); // undefined — truly private
```

### Example 3 — Function factory

```js
function multiplier(factor) {
  return (n) => n * factor;
}
const double = multiplier(2);
const triple = multiplier(3);
double(5); // 10
triple(5); // 15
```

### Example 4 — Closures capture variables, not values

```js
function make() {
  let x = 1;
  const get = () => x;
  x = 99;
  return get;
}
make()(); // 99 — sees the latest value
```

### Use cases of closures

1. Data privacy / encapsulation (module pattern)
2. Function factories
3. Memoization / caching
4. Currying & partial application
5. `once` functions
6. Debounce & throttle
7. Event handlers & callbacks that keep state
8. Iterators / generators-like behaviour

### Memoization with closure

```js
function memoize(fn) {
  const cache = new Map();
  return function (...args) {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);
    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}

const slowSquare = (n) => { for (let i = 0; i < 1e8; i++); return n * n; };
const fastSquare = memoize(slowSquare);
fastSquare(9); // slow first time
fastSquare(9); // instant (cached)
```

### once()

```js
function once(fn) {
  let called = false, result;
  return function (...args) {
    if (!called) {
      called = true;
      result = fn.apply(this, args);
    }
    return result;
  };
}
const init = once(() => console.log("initialised"));
init(); // "initialised"
init(); // nothing
```

### Closure disadvantage — memory

Variables in a closure are not garbage collected while the closure is reachable. Holding big data in long-lived closures (e.g. event listeners never removed) → memory leak.

```js
function attach() {
  const bigData = new Array(1e6).fill("x");
  document.getElementById("btn").addEventListener("click", () => {
    console.log(bigData.length); // bigData lives as long as the listener
  });
}
```

### Closure scope chain

Closures have access to 3 scopes: own, outer function(s), global.

```js
const g = "g";
function a() {
  const x = "x";
  return function b() {
    const y = "y";
    return function c() {
      console.log(g, x, y); // all three
    };
  };
}
a()()();
```

**Interview Qs**
- What is a closure? → A function along with references to its surrounding state (lexical environment). Created every time a function is created.
- Real-world use? → Private variables, memoize, debounce, React hooks (`useState` relies on closures), event handlers.
- Stale closure (React)? → A callback captured old state because it closed over an old render's variables.
- Output of the `var` loop with `setTimeout`? → `3 3 3`; fix with `let` or IIFE.

---

## 12. The `this` Keyword

`this` refers to the **object that is executing the current function**. Its value depends on **how** a function is called (except arrow functions, which use lexical `this`).

### The 5 binding rules (priority high → low)

1. **`new` binding** — `this` = newly created object.
2. **Explicit binding** — `call`, `apply`, `bind` → `this` = the given object.
3. **Implicit binding** — `obj.method()` → `this` = `obj`.
4. **Default binding** — plain call `fn()` → `this` = `globalThis` (non-strict) or `undefined` (strict).
5. **Arrow functions** — ignore all rules above; take `this` from the enclosing lexical scope.

### Example 1 — Global & default

```js
console.log(this); // browser: window | Node CommonJS module: {} (module.exports) | ESM: undefined

function show() { console.log(this); }
show(); // window (non-strict), undefined (strict mode)
```

### Example 2 — Implicit binding & losing `this`

```js
const user = {
  name: "Rohit",
  greet() { console.log("Hi " + this.name); },
};
user.greet();          // "Hi Rohit"

const fn = user.greet; // method extracted
fn();                  // "Hi undefined" — default binding now

setTimeout(user.greet, 0);              // "Hi undefined" — lost again
setTimeout(() => user.greet(), 0);      // "Hi Rohit"
setTimeout(user.greet.bind(user), 0);   // "Hi Rohit"
```

### Example 3 — Nested functions

```js
const obj = {
  val: 10,
  outer() {
    function inner() { console.log(this.val); }
    inner(); // undefined — plain call, default binding

    const innerArrow = () => console.log(this.val);
    innerArrow(); // 10 — lexical this
  },
};
obj.outer();
```

### Example 4 — `new`

```js
function Person(name) {
  // this = {} (new object, linked to Person.prototype)
  this.name = name;
  // return this (implicit)
}
const p = new Person("A");
console.log(p.name); // "A"
```

### What `new` does (4 steps)

1. Creates an empty object.
2. Sets its `[[Prototype]]` to `Constructor.prototype`.
3. Calls the constructor with `this` = the new object.
4. Returns the object (unless the constructor returns another object).

```js
function myNew(Constructor, ...args) {
  const obj = Object.create(Constructor.prototype);
  const result = Constructor.apply(obj, args);
  return result !== null && (typeof result === "object" || typeof result === "function")
    ? result
    : obj;
}
```

### `this` in classes & event handlers

```js
class Button {
  constructor(label) { this.label = label; }
  handleClick() { console.log(this.label); }
}
const b = new Button("Save");
const handler = b.handleClick;
handler(); // TypeError — classes run in strict mode, this = undefined

// Fix: arrow class field or bind in constructor
class Button2 {
  label = "Save";
  handleClick = () => console.log(this.label);
}
```

```js
// DOM: `this` in a normal listener = the element
document.querySelector("button").addEventListener("click", function () {
  console.log(this); // <button>
});
document.querySelector("button").addEventListener("click", () => {
  console.log(this); // window (lexical)
});
```

**Interview Qs**
- `this` inside an arrow function? → Taken from the enclosing scope at definition time; can't be changed by call/apply/bind.
- Why does `this` get lost in callbacks? → The function is called as a plain function, not as `obj.method()`.
- `this` in strict vs non-strict plain call? → `undefined` vs `globalThis`.

---

## 13. call, apply, bind

All three set `this` explicitly.

| Method | Invokes immediately? | Arguments |
|---|---|---|
| `call(thisArg, a, b)` | Yes | comma separated |
| `apply(thisArg, [a, b])` | Yes | array |
| `bind(thisArg, a, b)` | No — returns a new function | comma separated (partial application) |

```js
const person = { name: "Rohit" };
function intro(city, country) {
  return `${this.name} from ${city}, ${country}`;
}

intro.call(person, "Delhi", "India");     // "Rohit from Delhi, India"
intro.apply(person, ["Delhi", "India"]);  // same
const bound = intro.bind(person, "Delhi");
bound("India");                           // same
```

### Use cases

```js
// Borrowing methods
const arrayLike = { 0: "a", 1: "b", length: 2 };
Array.prototype.map.call(arrayLike, (x) => x.toUpperCase()); // ["A", "B"]

// apply with Math (older pattern; now use spread)
Math.max.apply(null, [1, 5, 3]); // 5
Math.max(...[1, 5, 3]);          // 5

// bind for partial application
const multiply = (a, b) => a * b;
const double = multiply.bind(null, 2);
double(4); // 8
```

A bound function **can't be re-bound**:

```js
function f() { return this.x; }
const g = f.bind({ x: 1 });
g.bind({ x: 2 })(); // 1
```

### Polyfills

```js
Function.prototype.myCall = function (ctx, ...args) {
  ctx = ctx ?? globalThis;
  ctx = Object(ctx); // box primitives
  const key = Symbol("fn");
  ctx[key] = this;           // `this` is the function
  const result = ctx[key](...args);
  delete ctx[key];
  return result;
};

Function.prototype.myApply = function (ctx, args = []) {
  return this.myCall(ctx, ...args);
};

Function.prototype.myBind = function (ctx, ...preset) {
  const fn = this;
  return function bound(...later) {
    // support `new bound()` — ignore ctx in that case
    if (new.target) return new fn(...preset, ...later);
    return fn.apply(ctx, [...preset, ...later]);
  };
};

intro.myCall(person, "Pune", "India");
intro.myBind(person, "Pune")("India");
```

**Interview Qs**
- Difference between call/apply/bind? (table above)
- Write a bind polyfill. (above)
- What happens if you pass `null` to call? → Non-strict: `this` = globalThis. Strict: `this` = null.

---

## 14. Objects in Depth

### Creating objects

```js
const a = { x: 1 };                         // literal
const b = new Object();                     // constructor
const c = Object.create(protoObj);          // with a given prototype
const d = Object.create(null);              // no prototype at all (pure dictionary)
function P(x) { this.x = x; } const e = new P(1); // constructor function
class Q { constructor(x) { this.x = x; } }  // class
const f = Object.fromEntries([["x", 1]]);   // from entries
```

### Property access

```js
const user = { name: "A", "full name": "A B", 1: "one" };
user.name;
user["full name"];
const key = "name";
user[key];          // dynamic key
user[1];            // keys are strings (or symbols): "1"
```

### Computed property names & shorthand

```js
const field = "email";
const name = "Rohit";
const obj = {
  name,                     // shorthand for name: name
  [field]: "a@b.com",       // computed key
  [`${field}Verified`]: true,
  greet() { return "hi"; }, // method shorthand
};
```

### Useful Object static methods

```js
const o = { a: 1, b: 2 };
Object.keys(o);      // ["a", "b"]
Object.values(o);    // [1, 2]
Object.entries(o);   // [["a",1],["b",2]]
Object.fromEntries(Object.entries(o).map(([k, v]) => [k, v * 10])); // {a:10,b:20}
Object.assign({}, o, { c: 3 }); // merge (shallow)
Object.hasOwn(o, "a");          // true (modern hasOwnProperty)
"a" in o;                        // true (also checks prototype chain)
Object.getOwnPropertyNames(o);
Object.getPrototypeOf(o) === Object.prototype; // true
Object.groupBy([1, 2, 3, 4], (n) => (n % 2 ? "odd" : "even")); // ES2024
```

### Iterating an object

```js
const scores = { math: 90, sci: 80 };
for (const key in scores) {          // also iterates inherited enumerable props
  if (Object.hasOwn(scores, key)) console.log(key, scores[key]);
}
for (const [k, v] of Object.entries(scores)) console.log(k, v);
```

### Freeze vs Seal vs preventExtensions

| | Add props | Delete props | Modify values |
|---|---|---|---|
| `Object.preventExtensions` | ❌ | ✅ | ✅ |
| `Object.seal` | ❌ | ❌ | ✅ |
| `Object.freeze` | ❌ | ❌ | ❌ |

All are **shallow**.

```js
const cfg = Object.freeze({ db: { host: "x" } });
cfg.db.host = "y"; // works! nested object not frozen

function deepFreeze(obj) {
  Object.values(obj).forEach((v) => {
    if (typeof v === "object" && v !== null) deepFreeze(v);
  });
  return Object.freeze(obj);
}
```

### Optional chaining & nullish coalescing

```js
const user = { profile: { address: null } };
user.profile?.address?.city;   // undefined (no error)
user.getName?.();               // undefined — method may not exist
user.list?.[0];                 // optional index

const count = 0;
count || 10;  // 10  (|| falls back for ANY falsy)
count ?? 10;  // 0   (?? falls back only for null/undefined)

let settings = {};
settings.theme ??= "dark";  // logical nullish assignment
settings.count ||= 1;
settings.enabled &&= false;
```

### Comparing objects (deep equal)

```js
function deepEqual(a, b) {
  if (Object.is(a, b)) return true;
  if (typeof a !== "object" || typeof b !== "object" || a === null || b === null) return false;
  if (Array.isArray(a) !== Array.isArray(b)) return false;
  const keysA = Object.keys(a), keysB = Object.keys(b);
  if (keysA.length !== keysB.length) return false;
  return keysA.every((k) => Object.hasOwn(b, k) && deepEqual(a[k], b[k]));
}
deepEqual({ a: [1, { b: 2 }] }, { a: [1, { b: 2 }] }); // true
```

### Flatten a nested object (common interview)

```js
function flattenObj(obj, prefix = "", out = {}) {
  for (const [k, v] of Object.entries(obj)) {
    const key = prefix ? `${prefix}.${k}` : k;
    if (v && typeof v === "object" && !Array.isArray(v)) flattenObj(v, key, out);
    else out[key] = v;
  }
  return out;
}
flattenObj({ a: 1, b: { c: 2, d: { e: 3 } } }); // { a:1, "b.c":2, "b.d.e":3 }
```

**Interview Qs**
- `in` vs `hasOwnProperty`? → `in` checks the prototype chain too.
- `Object.freeze` deep? → No, shallow.
- `for...in` vs `for...of`? → `for...in` iterates keys (enumerable, including inherited) of objects; `for...of` iterates values of iterables (arrays, strings, Map, Set).

---

## 15. Shallow vs Deep Copy

- **Shallow copy**: top-level properties copied; nested objects still shared.
- **Deep copy**: everything copied recursively; no shared references.

### Shallow copy ways

```js
const orig = { a: 1, nested: { b: 2 } };
const s1 = { ...orig };
const s2 = Object.assign({}, orig);
const arr2 = [...[1, 2]];
const arr3 = [1, 2].slice();

s1.nested.b = 99;
console.log(orig.nested.b); // 99 — shared!
```

### Deep copy ways

```js
// 1. structuredClone (modern, best built-in)
const deep = structuredClone({ d: new Date(), m: new Map([[1, 2]]), nested: { x: 1 } });
// supports Date, Map, Set, RegExp, typed arrays, circular refs.
// does NOT support functions, DOM nodes, class prototypes (become plain objects).

// 2. JSON trick (limited)
const j = JSON.parse(JSON.stringify(obj));
// loses: functions, undefined, Symbols, Infinity/NaN -> null, Date -> string, Map/Set -> {}; breaks on circular refs.
```

### Custom deep clone (handles circular refs)

```js
function deepClone(value, seen = new WeakMap()) {
  if (value === null || typeof value !== "object") return value;
  if (value instanceof Date) return new Date(value);
  if (value instanceof RegExp) return new RegExp(value);
  if (seen.has(value)) return seen.get(value);

  const copy = Array.isArray(value) ? [] : Object.create(Object.getPrototypeOf(value));
  seen.set(value, copy);
  for (const key of Reflect.ownKeys(value)) {
    copy[key] = deepClone(value[key], seen);
  }
  return copy;
}

const a = { x: 1 }; a.self = a;
const b = deepClone(a);
console.log(b.self === b); // true
```

**Interview Qs**
- Is spread a deep copy? → No, shallow.
- Best way to deep clone? → `structuredClone`, or a library (lodash `cloneDeep`) when you need functions/prototypes.

---

## 16. Destructuring, Spread, Rest

### Array destructuring

```js
const [a, b, ...rest] = [1, 2, 3, 4]; // a=1 b=2 rest=[3,4]
const [x, , z] = [1, 2, 3];           // skip
const [p = 10, q = 20] = [1];         // defaults: p=1 q=20

// Swap
let m = 1, n = 2;
[m, n] = [n, m];
```

### Object destructuring

```js
const user = { id: 1, name: "Rohit", address: { city: "Delhi" } };
const { name, age = 25 } = user;                 // default
const { name: userName } = user;                 // rename
const { address: { city } } = user;              // nested
const { id, ...others } = user;                  // rest: {name, address}

function show({ name, address: { city } = {} }) { // in params
  return `${name} - ${city}`;
}
```

### Spread

```js
const arr = [1, 2];
const more = [...arr, 3, 4];
const merged = { ...{ a: 1 }, ...{ a: 2, b: 3 } }; // {a:2, b:3} — later wins
Math.max(...arr);
const chars = [..."hello"];          // ["h","e","l","l","o"]
const unique = [...new Set([1,1,2])]; // [1, 2]
```

### Rest vs Spread

- **Spread** expands (right side / call site).
- **Rest** collects (left side / parameter). Rest must be last.

**Interview Qs**
- Remove a property immutably? → `const { password, ...safe } = user;`
- Default value only for `undefined`? → Yes, `null` doesn't trigger default.

---

## 17. Prototypes & Prototypal Inheritance

Every JS object has a hidden internal property `[[Prototype]]` pointing to another object (or `null`). When you access a property that doesn't exist on the object, JS looks it up on the prototype, then its prototype… this is the **prototype chain**. It ends at `Object.prototype` whose prototype is `null`.

### `__proto__` vs `prototype`

- `obj.__proto__` (or `Object.getPrototypeOf(obj)`) — the actual prototype of an **object instance**.
- `Fn.prototype` — a property on **constructor functions**; becomes the `__proto__` of objects created with `new Fn()`.

```js
function Car(brand) { this.brand = brand; }
Car.prototype.drive = function () { return `${this.brand} is driving`; };

const bmw = new Car("BMW");
bmw.drive();                                   // found on Car.prototype
bmw.__proto__ === Car.prototype;               // true
Car.prototype.__proto__ === Object.prototype;  // true
Object.prototype.__proto__;                    // null
bmw.hasOwnProperty("brand");                   // true
bmw.hasOwnProperty("drive");                   // false (inherited)
```

### Example — Object.create inheritance

```js
const animal = {
  eats: true,
  speak() { return `${this.name} makes a sound`; },
};
const dog = Object.create(animal);
dog.name = "Tommy";
dog.speak(); // "Tommy makes a sound"
dog.eats;    // true (from prototype)
```

### Example — Constructor inheritance (pre-ES6)

```js
function Animal(name) { this.name = name; }
Animal.prototype.speak = function () { return `${this.name} speaks`; };

function Dog(name, breed) {
  Animal.call(this, name);           // inherit instance props
  this.breed = breed;
}
Dog.prototype = Object.create(Animal.prototype); // inherit methods
Dog.prototype.constructor = Dog;
Dog.prototype.bark = function () { return "woof"; };

const d = new Dog("Rex", "Lab");
d.speak(); // "Rex speaks"
d instanceof Animal; // true
```

### Why put methods on prototype?

Methods on the prototype are **shared** by all instances (one copy in memory). Methods defined in the constructor are recreated per instance.

### Extending built-ins (don't do it in real code)

```js
Array.prototype.last = function () { return this[this.length - 1]; };
[1, 2, 3].last(); // 3
```

### instanceof polyfill

```js
function myInstanceOf(obj, Ctor) {
  let proto = Object.getPrototypeOf(obj);
  while (proto) {
    if (proto === Ctor.prototype) return true;
    proto = Object.getPrototypeOf(proto);
  }
  return false;
}
```

**Interview Qs**
- What is prototypal inheritance? → Objects inherit directly from other objects via the prototype chain.
- Classical vs prototypal? → Classical copies a blueprint (class) into instances; prototypal links objects together; JS classes are sugar over prototypes.
- End of prototype chain? → `null`.

---

## 18. Classes

ES6 classes are **syntactic sugar** over constructor functions + prototypes. Class bodies always run in **strict mode**, and classes are hoisted but stay in the TDZ.

```js
class Person {
  // public field
  species = "human";
  // private field
  #ssn;
  // static
  static count = 0;

  constructor(name, ssn) {
    this.name = name;
    this.#ssn = ssn;
    Person.count++;
  }

  // method (goes on prototype)
  greet() { return `Hi, I'm ${this.name}`; }

  // getter / setter
  get maskedSsn() { return "***" + this.#ssn.slice(-2); }
  set nickname(v) { this._nick = v.trim(); }

  // private method
  #validate() { return this.#ssn.length === 9; }

  // static method
  static create(name) { return new Person(name, "000000000"); }

  // static block (ES2022)
  static { /* static initialisation logic */ }
}

const p = new Person("Rohit", "123456789");
p.greet();
p.maskedSsn;       // "***89"
p.#ssn;            // SyntaxError — private
Person.create("A");
Person.count;
```

### Inheritance

```js
class Animal {
  constructor(name) { this.name = name; }
  speak() { return `${this.name} makes a sound`; }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name);         // must call before using `this`
    this.breed = breed;
  }
  speak() {
    return super.speak() + " (woof)"; // call parent method
  }
}

new Dog("Rex", "Lab").speak(); // "Rex makes a sound (woof)"
```

### Getters/setters with validation

```js
class Temperature {
  #celsius = 0;
  get fahrenheit() { return this.#celsius * 9 / 5 + 32; }
  set fahrenheit(f) {
    if (typeof f !== "number") throw new TypeError("number expected");
    this.#celsius = (f - 32) * 5 / 9;
  }
}
const t = new Temperature();
t.fahrenheit = 212;
t.fahrenheit; // 212
```

### Abstract-like class & mixins

```js
class Shape {
  constructor() {
    if (new.target === Shape) throw new Error("Shape is abstract");
  }
  area() { throw new Error("area() must be implemented"); }
}

const CanFly = (Base) => class extends Base { fly() { return "flying"; } };
class Bird extends CanFly(Animal) {}
new Bird("Tweety").fly();
```

### OOP pillars in JS (full deep dive in Section 19)

1. **Encapsulation** — private fields `#x`, closures.
2. **Abstraction** — exposing a simple API, hiding internals.
3. **Inheritance** — `extends`, prototype chain.
4. **Polymorphism** — method overriding (same method name, different behaviour).

**Interview Qs**
- Are classes hoisted? → Yes, but in TDZ; can't use before declaration.
- `super` purpose? → Call parent constructor/methods.
- Private fields vs `_underscore`? → `#` is enforced by the engine; `_` is just a convention.
- Class vs constructor function? → Class: strict mode, must use `new`, non-enumerable methods, TDZ, cleaner syntax.

---

## 19. OOP in JavaScript (Object-Oriented Programming)

**OOP** is a way of organizing code around **objects** that bundle **data (properties/state)** and **behaviour (methods)** together, instead of keeping data and functions separate.

JS is **multi-paradigm**: you can write procedural, functional or OOP code. Its OOP is **prototype-based** (objects inherit from other objects); `class` is syntax sugar over prototypes (see Sections 17–18).

### Procedural vs OOP vs Functional

```js
// Procedural: data and functions are separate
const account = { owner: "Rohit", balance: 100 };
function deposit(acc, amount) { acc.balance += amount; }
deposit(account, 50);

// OOP: data + behaviour together; state protected inside the object
class Account {
  #balance = 0;
  constructor(owner) { this.owner = owner; }
  deposit(amount) { this.#balance += amount; return this; }
  get balance() { return this.#balance; }
}
new Account("Rohit").deposit(50).balance; // 50

// Functional: pure functions, immutable data
const depositFn = (acc, amount) => ({ ...acc, balance: acc.balance + amount });
const updated = depositFn(account, 50); // original untouched
```

### Core vocabulary

| Term | Meaning | JS example |
|---|---|---|
| **Class** | Blueprint for objects | `class User {}` |
| **Object / Instance** | A thing created from a class | `new User()` |
| **Property / Field** | Data on an object | `this.name` |
| **Method** | Function on an object | `user.login()` |
| **Constructor** | Sets up a new instance | `constructor(name) {}` |
| **State** | Current values of an object's properties | `{ balance: 100 }` |
| **Interface** | A contract of methods an object must have | Duck typing / TS `interface` |
| **Static member** | Belongs to the class, not instances | `User.count`, `Date.now()` |

### 5 ways to create objects in JS

```js
// 1. Object literal — one-off objects
const user1 = { name: "A", greet() { return `Hi ${this.name}`; } };

// 2. Factory function — returns a new object; closures give privacy; no `new`/`this` issues
function createUser(name) {
  let loginCount = 0; // private
  return {
    name,
    login() { loginCount++; return `${name} logged in ${loginCount} times`; },
  };
}
const user2 = createUser("B");

// 3. Constructor function — pre-ES6 classes
function User(name) { this.name = name; }
User.prototype.greet = function () { return `Hi ${this.name}`; };
const user3 = new User("C");

// 4. ES6 class — modern standard
class Person {
  constructor(name) { this.name = name; }
  greet() { return `Hi ${this.name}`; }
}
const user4 = new Person("D");

// 5. Object.create — set the prototype directly
const proto = { greet() { return `Hi ${this.name}`; } };
const user5 = Object.create(proto, { name: { value: "E", enumerable: true } });
```

**Factory vs class**: factories give real privacy via closures and never break on lost `this`, but each object gets its own copy of methods (more memory). Classes share methods via the prototype, support `instanceof` and `extends`, and are more familiar to most teams.

---

### The 4 Pillars of OOP

### Pillar 1 — Encapsulation

**Bundle data and the methods that use it together, and hide internal state** so it can only change through controlled methods. Protects invariants (rules that must always be true, like "balance can't go negative").

Ways to encapsulate in JS:
1. `#private` fields & methods (real privacy, enforced by the engine).
2. Closures (factory functions / module pattern).
3. Getters/setters for controlled access.
4. `_underscore` naming (convention only — NOT private).
5. `WeakMap` private data (older pattern).
6. `Object.freeze` / non-writable properties.

```js
// ❌ No encapsulation: anyone can break the rules
const wallet = { balance: 100 };
wallet.balance = -5000; // invalid state, nobody stopped it

// ✅ Encapsulated
class BankAccount {
  #balance = 0;
  #transactions = [];

  constructor(owner, initialDeposit = 0) {
    this.owner = owner;
    if (initialDeposit > 0) this.deposit(initialDeposit);
  }

  deposit(amount) {
    this.#validateAmount(amount);
    this.#balance += amount;
    this.#log("deposit", amount);
    return this;
  }

  withdraw(amount) {
    this.#validateAmount(amount);
    if (amount > this.#balance) throw new Error("Insufficient funds");
    this.#balance -= amount;
    this.#log("withdraw", amount);
    return this;
  }

  get balance() { return this.#balance; }                 // read-only from outside
  get history() { return [...this.#transactions]; }        // return a COPY, not the internal array

  #validateAmount(amount) {                                // private helper
    if (!Number.isFinite(amount) || amount <= 0) throw new RangeError("Amount must be positive");
  }
  #log(type, amount) {
    this.#transactions.push({ type, amount, at: new Date().toISOString() });
  }
}

const acc = new BankAccount("Rohit", 100);
acc.deposit(50).withdraw(30);
acc.balance;           // 120
acc.balance = 1e6;     // ignored (no setter) — TypeError in strict mode
acc.#balance;          // SyntaxError
acc.history.push({});  // doesn't affect the real history (copy)
```

```js
// Encapsulation with closures (factory)
function createCounter() {
  let count = 0;
  return {
    increment: () => ++count,
    reset: () => (count = 0),
    get value() { return count; },
  };
}
```

```js
// Setter with validation
class Product {
  #price = 0;
  get price() { return this.#price; }
  set price(value) {
    if (typeof value !== "number" || value < 0) throw new TypeError("Invalid price");
    this.#price = Math.round(value * 100) / 100;
  }
}
const p = new Product();
p.price = 99.999; // stored as 100
```

**Why it matters in production**: fewer invalid states, you can change internals without breaking callers, and there's one place to put validation and logging.

### Pillar 2 — Abstraction

**Expose only what's necessary (a simple interface) and hide the complex implementation details.** Callers know **what** an object does, not **how**.

Real-life: you press a car's accelerator without knowing how fuel injection works. `fetch()` hides TCP, TLS and HTTP parsing.

```js
// The caller doesn't know/care about SMTP, retries, templates, providers
class EmailService {
  async sendWelcome(user) {
    const html = this.#renderTemplate("welcome", { name: user.name });
    await this.#sendWithRetry({ to: user.email, subject: "Welcome!", html });
  }
  #renderTemplate(name, data) { /* complex templating */ return `<h1>Hi ${data.name}</h1>`; }
  async #sendWithRetry(msg, attempts = 3) { /* provider API, retries, backoff, logging */ }
}

await new EmailService().sendWelcome({ name: "Rohit", email: "r@x.com" }); // simple API
```

JS has no `abstract` keyword (TypeScript does). Emulate an **abstract class** with `new.target` and "not implemented" methods:

```js
class PaymentGateway {
  constructor() {
    if (new.target === PaymentGateway) throw new TypeError("PaymentGateway is abstract");
  }
  // abstract methods — subclasses MUST implement
  async charge(amount, currency) { throw new Error(`${this.constructor.name} must implement charge()`); }
  async refund(transactionId) { throw new Error(`${this.constructor.name} must implement refund()`); }

  // concrete shared method (template method pattern)
  async pay(order) {
    if (order.total <= 0) throw new Error("Invalid total");
    const tx = await this.charge(order.total, order.currency);
    console.log(`Paid ${order.total} via ${this.constructor.name}: ${tx.id}`);
    return tx;
  }
}

class StripeGateway extends PaymentGateway {
  async charge(amount, currency) { /* Stripe API */ return { id: "stripe_123" }; }
  async refund(id) { /* ... */ }
}
class RazorpayGateway extends PaymentGateway {
  async charge(amount, currency) { /* Razorpay API */ return { id: "rzp_456" }; }
  async refund(id) { /* ... */ }
}

new PaymentGateway();                        // TypeError: abstract
await new StripeGateway().pay({ total: 500, currency: "INR" });
```

**Encapsulation vs Abstraction**

| Encapsulation | Abstraction |
|---|---|
| **Hiding data** (protect state) | **Hiding complexity** (simple interface) |
| How: private fields, closures, getters/setters | How: abstract classes, interfaces, clean public API |
| "Don't touch my internals" | "You don't need to know my internals" |
| Implementation-level concern | Design-level concern |

### Pillar 3 — Inheritance

**A class (child/subclass) acquires properties and methods of another class (parent/superclass)** → reuse code and model "**is-a**" relationships (a `Dog` **is an** `Animal`).

```js
class Employee {
  constructor(name, salary) {
    this.name = name;
    this.salary = salary;
  }
  getAnnualSalary() { return this.salary * 12; }
  describe() { return `${this.name} earns ${this.getAnnualSalary()}/yr`; }
}

class Manager extends Employee {
  constructor(name, salary, reports = []) {
    super(name, salary);            // MUST call super() before using `this`
    this.reports = reports;
  }
  getAnnualSalary() {               // override
    const base = super.getAnnualSalary(); // reuse parent logic
    return base + this.reports.length * 10000; // bonus per report
  }
  addReport(emp) { this.reports.push(emp); return this; }
}

class Intern extends Employee {
  getAnnualSalary() { return this.salary * 6; } // 6-month internship
}

const dev = new Employee("Asha", 100000);
const mgr = new Manager("Rohit", 150000, [dev]);
mgr.describe();               // uses Manager's getAnnualSalary via `this`
mgr instanceof Manager;       // true
mgr instanceof Employee;      // true
Object.getPrototypeOf(Manager.prototype) === Employee.prototype; // true (prototype chain)
```

**Types of inheritance**
- **Single**: `B extends A`.
- **Multilevel**: `C extends B extends A`.
- **Hierarchical**: `B extends A`, `C extends A`.
- **Multiple**: ❌ not supported directly (a class has one prototype) → use **mixins** or **composition**.

**Extending built-ins**

```js
class HttpError extends Error {
  constructor(status, message) {
    super(message);
    this.name = "HttpError";
    this.status = status;
  }
}
class Stack extends Array {
  peek() { return this[this.length - 1]; }
}
```

**Problems with deep inheritance**
- **Tight coupling**: changing the parent can break every child (fragile base class problem).
- **Gorilla/banana problem**: "You wanted a banana but got a gorilla holding the banana and the entire jungle" — you inherit everything, even what you don't need.
- Rigid hierarchies break when requirements change (is a `FlyingFish` a `Fish` or a `Bird`?).
- **Rule**: keep hierarchies shallow (1–2 levels). Prefer composition.

### Pillar 4 — Polymorphism

**"Many forms"**: the same method call behaves differently depending on the object that receives it. Callers write code against a common interface and don't need `if/else` on types.

**Runtime polymorphism (method overriding)**

```js
class Shape {
  area() { return 0; }
  toString() { return `${this.constructor.name} with area ${this.area().toFixed(2)}`; }
}
class Circle extends Shape {
  constructor(r) { super(); this.r = r; }
  area() { return Math.PI * this.r ** 2; }
}
class Rectangle extends Shape {
  constructor(w, h) { super(); this.w = w; this.h = h; }
  area() { return this.w * this.h; }
}
class Triangle extends Shape {
  constructor(b, h) { super(); this.b = b; this.h = h; }
  area() { return 0.5 * this.b * this.h; }
}

const shapes = [new Circle(2), new Rectangle(3, 4), new Triangle(6, 2)];
shapes.forEach((s) => console.log(s.toString())); // same call, different behaviour
const totalArea = shapes.reduce((sum, s) => sum + s.area(), 0);
```

**Replacing if/else chains with polymorphism (real production refactor)**

```js
// ❌ Every new channel = edit this function (violates Open/Closed)
function notify(user, channel, msg) {
  if (channel === "email") sendEmail(user.email, msg);
  else if (channel === "sms") sendSms(user.phone, msg);
  else if (channel === "push") sendPush(user.deviceToken, msg);
}

// ✅ Polymorphic: each notifier knows how to send itself
class EmailNotifier { send(user, msg) { return sendEmail(user.email, msg); } }
class SmsNotifier   { send(user, msg) { return sendSms(user.phone, msg); } }
class PushNotifier  { send(user, msg) { return sendPush(user.deviceToken, msg); } }

const notifiers = { email: new EmailNotifier(), sms: new SmsNotifier(), push: new PushNotifier() };
async function notifyAll(user, msg) {
  await Promise.allSettled(user.channels.map((c) => notifiers[c].send(user, msg)));
}
// Adding WhatsApp = add a class + a map entry; existing code untouched
```

**Duck typing ("if it walks like a duck…")** — JS polymorphism doesn't need inheritance; any object with the right method works.

```js
const logger1 = { log: (m) => console.log(m) };
const logger2 = { log: (m) => fs.appendFileSync("app.log", m + "\n") };
const logger3 = { log: (m) => fetch("/logs", { method: "POST", body: m }) };

function runJob(logger) { logger.log("job started"); } // works with any of them
```

**Compile-time polymorphism / method overloading** — JS doesn't support multiple functions with the same name; the last definition wins. Emulate it by checking arguments:

```js
class Calculator {
  add(...args) {
    if (args.length === 1 && Array.isArray(args[0])) return args[0].reduce((a, b) => a + b, 0);
    if (args.every((a) => typeof a === "string")) return args.join("");
    return args.reduce((a, b) => a + b, 0);
  }
}
const c = new Calculator();
c.add(1, 2);        // 3
c.add([1, 2, 3]);   // 6
c.add("a", "b");    // "ab"
```

(TypeScript has overload signatures — see TS notes.)

---

### Composition over Inheritance

**Inheritance** = "is-a" (`Dog is an Animal`). **Composition** = "has-a" (`Car has an Engine`) — build objects by combining small, focused pieces.

```js
// ❌ Inheritance explosion
class Animal {}
class FlyingAnimal extends Animal { fly() {} }
class SwimmingAnimal extends Animal { swim() {} }
class Duck extends ??? {} // needs to fly AND swim → stuck

// ✅ Composition with behaviour objects
const canFly = (state) => ({ fly: () => `${state.name} flies` });
const canSwim = (state) => ({ swim: () => `${state.name} swims` });
const canQuack = (state) => ({ quack: () => `${state.name}: Quack!` });

function createDuck(name) {
  const state = { name };
  return Object.assign({}, state, canFly(state), canSwim(state), canQuack(state));
}
function createPenguin(name) {
  const state = { name };
  return Object.assign({}, state, canSwim(state));
}
createDuck("Donald").fly();   // "Donald flies"
createPenguin("Pingu").fly;   // undefined — penguins can't fly, and we didn't hack around it
```

```js
// ✅ Composition with classes (has-a + delegation)
class Engine {
  start() { return "engine started"; }
}
class GPS {
  route(to) { return `routing to ${to}`; }
}
class Car {
  constructor(engine = new Engine(), gps = new GPS()) { // dependencies injected
    this.engine = engine;
    this.gps = gps;
  }
  drive(to) { return `${this.engine.start()}, ${this.gps.route(to)}`; }
}
new Car().drive("Delhi");
new Car(new ElectricEngine()).drive("Pune"); // swap parts without subclassing
```

### Mixins (sharing behaviour across unrelated classes)

```js
const Serializable = (Base) => class extends Base {
  toJSON() { return { type: this.constructor.name, ...this }; }
};
const Timestamped = (Base) => class extends Base {
  constructor(...args) { super(...args); this.createdAt = new Date(); }
};
const EventTarget_ = (Base) => class extends Base {
  #handlers = {};
  on(e, fn) { (this.#handlers[e] ??= []).push(fn); }
  emit(e, ...a) { this.#handlers[e]?.forEach((fn) => fn(...a)); }
};

class Model {}
class User extends Serializable(Timestamped(EventTarget_(Model))) {
  constructor(name) { super(); this.name = name; }
}
const u = new User("Rohit");
u.on("save", () => console.log("saved"));
JSON.stringify(u); // {"type":"User","createdAt":"...","name":"Rohit"}
```

### Object relationships

| Relationship | Meaning | Lifetime | Example |
|---|---|---|---|
| **Association** | Objects use each other | Independent | `Teacher` ↔ `Student` |
| **Aggregation** (weak has-a) | Whole contains parts, parts can exist alone | Independent | `Team` has `Player`s |
| **Composition** (strong has-a) | Whole owns parts; parts die with the whole | Dependent | `House` has `Room`s, `Order` has `OrderLine`s |
| **Inheritance** (is-a) | Specialization | — | `Admin` is a `User` |

```js
// Aggregation: players passed in, exist without the team
class Team { constructor(players) { this.players = players; } }
// Composition: order lines created and owned by the order
class Order {
  #lines = [];
  addItem(product, qty) { this.#lines.push({ product, qty }); }
  get total() { return this.#lines.reduce((s, l) => s + l.product.price * l.qty, 0); }
}
```

---

### SOLID Principles (with JS examples)

Five design principles for maintainable OOP code. Very common in interviews.

#### S — Single Responsibility Principle

**A class/module should have one reason to change** (one job).

```js
// ❌ One class doing validation, DB, emails and PDFs
class UserManager {
  validate(user) {}
  saveToDb(user) {}
  sendWelcomeEmail(user) {}
  generateReportPdf(user) {}
}

// ✅ Split by responsibility
class UserValidator { validate(user) { /* rules */ } }
class UserRepository { async save(user) { /* DB */ } }
class EmailService { async sendWelcome(user) { /* email */ } }

class UserService {                     // orchestrates, doesn't do everything itself
  constructor(validator, repo, email) {
    Object.assign(this, { validator, repo, email });
  }
  async register(data) {
    this.validator.validate(data);
    const user = await this.repo.save(data);
    await this.email.sendWelcome(user);
    return user;
  }
}
```

#### O — Open/Closed Principle

**Open for extension, closed for modification.** Add new behaviour by adding code, not by editing working code.

```js
// ❌ Every new discount type = modify this function
function getDiscount(type, amount) {
  if (type === "festive") return amount * 0.2;
  if (type === "student") return amount * 0.1;
  return 0;
}

// ✅ Register new strategies without touching existing ones
const discountStrategies = new Map([
  ["festive", (amt) => amt * 0.2],
  ["student", (amt) => amt * 0.1],
]);
const registerDiscount = (type, fn) => discountStrategies.set(type, fn);
const getDiscount2 = (type, amt) => (discountStrategies.get(type) ?? (() => 0))(amt);

registerDiscount("employee", (amt) => amt * 0.3); // extension
```

#### L — Liskov Substitution Principle

**Subclasses must be usable anywhere the parent is expected, without breaking behaviour.** A child shouldn't strengthen preconditions, weaken postconditions, or throw for things the parent supports.

```js
// ❌ Classic violation: Square extends Rectangle
class Rectangle {
  setWidth(w) { this.width = w; }
  setHeight(h) { this.height = h; }
  area() { return this.width * this.height; }
}
class Square extends Rectangle {
  setWidth(w) { this.width = this.height = w; }
  setHeight(h) { this.width = this.height = h; }
}
function resize(rect) {
  rect.setWidth(5);
  rect.setHeight(4);
  console.assert(rect.area() === 20, "expected 20"); // fails for Square (16)
}

// ❌ Another violation: a subclass that throws for a parent method
class Bird { fly() {} }
class Penguin extends Bird { fly() { throw new Error("can't fly"); } }

// ✅ Model capabilities separately
class Shape { area() {} }
class Rect extends Shape { constructor(w, h) { super(); this.w = w; this.h = h; } area() { return this.w * this.h; } }
class Sq extends Shape { constructor(s) { super(); this.s = s; } area() { return this.s ** 2; } }
```

#### I — Interface Segregation Principle

**Don't force clients to depend on methods they don't use.** Prefer many small interfaces over one fat one.

```js
// ❌ Fat interface: every device must implement everything
class Machine {
  print() {} scan() {} fax() {}
}
class BasicPrinter extends Machine {
  scan() { throw new Error("not supported"); } // forced to implement junk
  fax() { throw new Error("not supported"); }
}

// ✅ Small capabilities composed as needed
const Printer = { print(doc) { console.log("printing", doc); } };
const Scanner = { scan() { return "scanned"; } };
const basicPrinter = Object.assign({}, Printer);
const allInOne = Object.assign({}, Printer, Scanner);
```

#### D — Dependency Inversion Principle

**High-level modules shouldn't depend on low-level details; both should depend on abstractions.** Pass dependencies in (dependency injection) instead of hard-coding them.

```js
// ❌ Hard-wired to MySQL and a real mailer → can't swap or unit test
class OrderService {
  constructor() {
    this.db = new MySQLDatabase();
    this.mailer = new SendGridMailer();
  }
}

// ✅ Depend on an "interface" (anything with save()/send()), inject it
class OrderService2 {
  constructor({ orderRepo, mailer }) {
    this.orderRepo = orderRepo;
    this.mailer = mailer;
  }
  async placeOrder(order) {
    const saved = await this.orderRepo.save(order);
    await this.mailer.send(order.email, `Order ${saved.id} confirmed`);
    return saved;
  }
}

// production wiring
const service = new OrderService2({ orderRepo: new PostgresOrderRepo(pool), mailer: new SesMailer() });

// test wiring — no DB, no emails
const fakeRepo = { save: async (o) => ({ ...o, id: 1 }) };
const fakeMailer = { sent: [], async send(to, msg) { this.sent.push({ to, msg }); } };
const testService = new OrderService2({ orderRepo: fakeRepo, mailer: fakeMailer });
```

### Other design principles used in real code

- **DRY** (Don't Repeat Yourself) — one source of truth for each piece of knowledge. But don't over-abstract things that only look similar.
- **KISS** (Keep It Simple) — the simplest solution that works.
- **YAGNI** (You Aren't Gonna Need It) — don't build for hypothetical future needs.
- **Law of Demeter** — talk to friends, not strangers: avoid `order.customer.address.city.zip.format()` chains; ask `order.getShippingZip()`.
- **Separation of concerns** — UI, business logic and data access in different layers.
- **Tell, don't ask** — tell an object to do something (`account.withdraw(50)`) instead of pulling its data out and deciding for it (`if (account.balance > 50) account.balance -= 50`).
- **Favor composition over inheritance.**
- **Program to an interface, not an implementation.**

---

### Useful OOP techniques in JS

**Method chaining (fluent interface)** — return `this`.

```js
class QueryBuilder {
  #table; #wheres = []; #limit; #order;
  from(t) { this.#table = t; return this; }
  where(cond) { this.#wheres.push(cond); return this; }
  orderBy(col, dir = "ASC") { this.#order = `${col} ${dir}`; return this; }
  limit(n) { this.#limit = n; return this; }
  build() {
    let sql = `SELECT * FROM ${this.#table}`;
    if (this.#wheres.length) sql += ` WHERE ${this.#wheres.join(" AND ")}`;
    if (this.#order) sql += ` ORDER BY ${this.#order}`;
    if (this.#limit) sql += ` LIMIT ${this.#limit}`;
    return sql;
  }
}
new QueryBuilder().from("users").where("age > 18").orderBy("name").limit(10).build();
```

**Static factory methods** — named constructors, validation, caching.

```js
class Money {
  constructor(paise, currency) { this.paise = paise; this.currency = currency; Object.freeze(this); }
  static fromRupees(rupees, currency = "INR") { return new Money(Math.round(rupees * 100), currency); }
  static zero(currency = "INR") { return new Money(0, currency); }
  add(other) {
    if (other.currency !== this.currency) throw new Error("Currency mismatch");
    return new Money(this.paise + other.paise, this.currency); // immutable value object
  }
  toString() { return new Intl.NumberFormat("en-IN", { style: "currency", currency: this.currency }).format(this.paise / 100); }
}
Money.fromRupees(10.1).add(Money.fromRupees(0.2)).toString(); // "₹10.30" — no float bugs
```

**Customizing built-in behaviour**

```js
class Temperature {
  constructor(c) { this.c = c; }
  toString() { return `${this.c}°C`; }                  // `${t}`, string concat
  toJSON() { return { celsius: this.c }; }              // JSON.stringify
  valueOf() { return this.c; }                          // t1 > t2, t + 1
  [Symbol.toPrimitive](hint) { return hint === "string" ? this.toString() : this.c; }
  get [Symbol.toStringTag]() { return "Temperature"; } // Object.prototype.toString.call(t)
  static [Symbol.hasInstance](obj) { return typeof obj?.c === "number"; } // custom instanceof
}
const t = new Temperature(30);
`${t}`;               // "30°C"
t + 5;                // 35
JSON.stringify(t);    // {"celsius":30}
```

**Checking types in OOP code**

```js
obj instanceof Class;          // prototype chain check (breaks across iframes/realms)
obj.constructor.name;          // "Circle"
typeof obj.send === "function"; // duck typing — preferred for "interfaces"
Object.prototype.toString.call([]); // "[object Array]"
```

**`this` pitfalls in OOP code** — methods lose `this` when passed as callbacks.

```js
class Timer {
  seconds = 0;
  tick() { this.seconds++; }
  start() {
    setInterval(this.tick, 1000);              // ❌ this = undefined
    setInterval(() => this.tick(), 1000);      // ✅ arrow
    setInterval(this.tick.bind(this), 1000);   // ✅ bind
  }
  handleClick = () => { this.seconds = 0; };   // ✅ arrow class field (bound per instance)
}
```

---

### OOP vs Functional Programming — when to use which

| OOP | Functional |
|---|---|
| Objects hold state + behaviour | Pure functions transform immutable data |
| Good for entities with identity & lifecycle (User, Order, Game character, UI widgets, SDK clients) | Good for data transformations, pipelines, React UI, reducers |
| Encapsulation, polymorphism | Composition, higher-order functions, immutability |
| Risk: deep hierarchies, hidden mutable state | Risk: harder to model stateful things |

Modern JS/React code is **mostly functional** (hooks, pure components, reducers, `map/filter/reduce`), with **classes** for: error types, SDK/API clients, services on the backend (NestJS), data structures, game engines, and domain models. Use both where they fit.

---

### Real-world example — Shopping Cart (OOP design)

```js
class Product {
  constructor({ id, name, price, stock }) {
    Object.assign(this, { id, name, price, stock });
  }
  isInStock(qty = 1) { return this.stock >= qty; }
}

class CartItem {
  constructor(product, qty) { this.product = product; this.qty = qty; }
  get subtotal() { return this.product.price * this.qty; }
}

class Cart {
  #items = new Map();            // productId -> CartItem
  #coupon = null;

  add(product, qty = 1) {
    if (!product.isInStock(qty)) throw new Error(`${product.name} is out of stock`);
    const existing = this.#items.get(product.id);
    if (existing) existing.qty += qty;
    else this.#items.set(product.id, new CartItem(product, qty));
    return this;
  }
  remove(productId) { this.#items.delete(productId); return this; }
  applyCoupon(coupon) { this.#coupon = coupon; return this; }

  get items() { return [...this.#items.values()]; }
  get subtotal() { return this.items.reduce((s, i) => s + i.subtotal, 0); }
  get discount() { return this.#coupon ? this.#coupon.apply(this.subtotal) : 0; }
  get total() { return Math.max(0, this.subtotal - this.discount); }
}

// Polymorphic coupons
class PercentCoupon { constructor(pct) { this.pct = pct; } apply(amount) { return (amount * this.pct) / 100; } }
class FlatCoupon { constructor(off, min = 0) { Object.assign(this, { off, min }); } apply(amount) { return amount >= this.min ? this.off : 0; } }

const phone = new Product({ id: 1, name: "Phone", price: 20000, stock: 5 });
const cover = new Product({ id: 2, name: "Cover", price: 500, stock: 10 });
const cart = new Cart().add(phone).add(cover, 2).applyCoupon(new PercentCoupon(10));
cart.total; // 18900
```

### LLD (Low-Level Design) — Parking Lot (common interview)

```js
const VehicleSize = Object.freeze({ SMALL: 1, MEDIUM: 2, LARGE: 3 });

class Vehicle {
  constructor(plate, size) {
    if (new.target === Vehicle) throw new TypeError("Vehicle is abstract");
    this.plate = plate;
    this.size = size;
  }
}
class Bike extends Vehicle { constructor(p) { super(p, VehicleSize.SMALL); } }
class Car extends Vehicle { constructor(p) { super(p, VehicleSize.MEDIUM); } }
class Truck extends Vehicle { constructor(p) { super(p, VehicleSize.LARGE); } }

class Spot {
  constructor(id, size) { this.id = id; this.size = size; this.vehicle = null; }
  get isFree() { return this.vehicle === null; }
  canFit(v) { return this.isFree && v.size <= this.size; }
}

class Ticket {
  constructor(vehicle, spot) {
    this.id = crypto.randomUUID();
    this.vehicle = vehicle;
    this.spot = spot;
    this.entryTime = Date.now();
  }
}

class ParkingLot {
  #spots; #tickets = new Map();
  constructor(spots, pricingStrategy) {
    this.#spots = spots;
    this.pricing = pricingStrategy; // injected (Strategy pattern)
  }
  park(vehicle) {
    const spot = this.#spots
      .filter((s) => s.canFit(vehicle))
      .sort((a, b) => a.size - b.size)[0];             // smallest spot that fits
    if (!spot) throw new Error("Parking full");
    spot.vehicle = vehicle;
    const ticket = new Ticket(vehicle, spot);
    this.#tickets.set(ticket.id, ticket);
    return ticket;
  }
  unpark(ticketId, now = Date.now()) {
    const ticket = this.#tickets.get(ticketId);
    if (!ticket) throw new Error("Invalid ticket");
    ticket.spot.vehicle = null;
    this.#tickets.delete(ticketId);
    const hours = Math.ceil((now - ticket.entryTime) / 3_600_000) || 1;
    return this.pricing.calculate(ticket.vehicle, hours);
  }
  get availableSpots() { return this.#spots.filter((s) => s.isFree).length; }
}

const hourlyPricing = { calculate: (v, hours) => hours * { 1: 10, 2: 30, 3: 60 }[v.size] };
const lot = new ParkingLot(
  [new Spot(1, VehicleSize.SMALL), new Spot(2, VehicleSize.MEDIUM), new Spot(3, VehicleSize.LARGE)],
  hourlyPricing
);
const t1 = lot.park(new Car("DL01AB1234"));
lot.availableSpots;  // 2
lot.unpark(t1.id);   // 30
```

This covers: abstraction (abstract `Vehicle`), inheritance (`Car extends Vehicle`), encapsulation (private `#spots`), polymorphism (size per subclass, pluggable pricing), composition (lot has spots, ticket has a vehicle and a spot), and SRP/DIP (pricing injected).

Other LLD questions to practise: Library management, Elevator system, Tic-tac-toe/Chess, Splitwise, BookMyShow, Vending machine, Rate limiter, LRU cache, Logger, Snake & Ladder.

---

### OOP Interview Questions

1. **What is OOP? What are its 4 pillars?** → Encapsulation, Abstraction, Inheritance, Polymorphism.
2. **Is JavaScript object-oriented?** → Yes, prototype-based OOP; `class` is sugar over prototypes. It's also functional and procedural.
3. **Class-based vs prototype-based inheritance?** → Classes copy a blueprint; prototypes link objects in a chain at runtime; JS classes still use prototypes underneath.
4. **Encapsulation vs abstraction?** (table above)
5. **How do you create private members in JS?** → `#private`, closures, WeakMap; `_underscore` is only a convention.
6. **How do you create an abstract class in JS?** → `new.target` check in the constructor + methods that throw "not implemented"; or TS `abstract`.
7. **Does JS support multiple inheritance?** → No; use mixins or composition.
8. **Does JS support method overloading?** → No; the last definition wins. Emulate with argument checks (or TS overloads).
9. **Method overriding & `super`?** → Redefine a parent method in the child; `super.method()` calls the parent version.
10. **Composition vs inheritance — which and why?** → Prefer composition: loose coupling and flexible, avoids fragile hierarchies. Inheritance for true, stable "is-a" relationships.
11. **Explain SOLID with examples.**
12. **What is dependency injection? Why does it help testing?**
13. **Association vs aggregation vs composition.**
14. **What is duck typing?**
15. **What is a mixin?**
16. **Factory function vs class vs constructor function.**
17. **What is method chaining and how do you implement it?** → Return `this`.
18. **What is the `new` keyword doing?** (see Section 12)
19. **Static vs instance members.**
20. **What is a value object? Why immutable?** → Objects compared by value (Money, Date range); immutability prevents shared-state bugs.
21. **Design a parking lot / library / cart in OOP.**
22. **Why can overriding break Liskov Substitution?** → If the child changes expected behaviour (Square/Rectangle, Penguin.fly throwing).
23. **What problems does OOP have?** → Hidden mutable state, deep hierarchies, over-engineering (factories of factories), `this` binding issues in JS.

---

## 20. Arrays & Array Methods

### Mutating vs non-mutating

| Mutating (change original) | Non-mutating (return new) |
|---|---|
| `push`, `pop`, `shift`, `unshift` | `map`, `filter`, `reduce`, `concat` |
| `splice`, `sort`, `reverse`, `fill` | `slice`, `flat`, `flatMap`, `join` |
| `copyWithin` | `toSorted`, `toReversed`, `toSpliced`, `with` (ES2023) |

```js
const a = [3, 1, 2];
a.toSorted();       // [1, 2, 3], a unchanged
a.with(0, 99);      // [99, 1, 2], a unchanged
a.at(-1);           // 2 (negative index)
```

### map, filter, reduce

```js
const nums = [1, 2, 3, 4, 5];
nums.map((n) => n * 2);                // [2,4,6,8,10]
nums.filter((n) => n % 2 === 0);       // [2,4]
nums.reduce((acc, n) => acc + n, 0);   // 15

// Chain: sum of squares of even numbers
nums.filter((n) => n % 2 === 0).map((n) => n * n).reduce((a, b) => a + b, 0); // 20
```

```js
// reduce: group by
const people = [{ name: "A", age: 20 }, { name: "B", age: 30 }, { name: "C", age: 20 }];
const byAge = people.reduce((acc, p) => {
  (acc[p.age] ??= []).push(p.name);
  return acc;
}, {});
// { 20: ["A","C"], 30: ["B"] }

// reduce: count frequency
const freq = [..."banana"].reduce((acc, ch) => ((acc[ch] = (acc[ch] || 0) + 1), acc), {});
// { b:1, a:3, n:2 }
```

### find, findIndex, findLast, some, every, includes, indexOf

```js
const users = [{ id: 1, active: true }, { id: 2, active: false }];
users.find((u) => u.id === 2);        // {id:2...}
users.findIndex((u) => u.id === 2);   // 1
users.findLast((u) => u.active);      // {id:1...}
users.some((u) => u.active);          // true
users.every((u) => u.active);         // false
[1, 2, NaN].includes(NaN);            // true
[1, 2, NaN].indexOf(NaN);             // -1 (uses ===)
```

### slice vs splice

```js
const arr = [1, 2, 3, 4, 5];
arr.slice(1, 3);     // [2, 3] — original unchanged, end excluded
arr.splice(1, 2);    // removes 2 items from index 1 -> returns [2, 3], arr = [1,4,5]
arr.splice(1, 0, "x", "y"); // insert -> arr = [1,"x","y",4,5]
```

### sort — the trap

Default `sort` converts elements to **strings** and sorts lexicographically.

```js
[10, 1, 5, 100].sort();                 // [1, 10, 100, 5]
[10, 1, 5, 100].sort((a, b) => a - b);  // [1, 5, 10, 100]
[10, 1, 5, 100].sort((a, b) => b - a);  // descending
users.sort((a, b) => a.name.localeCompare(b.name)); // strings
```

### flat & flatMap

```js
[1, [2, [3, [4]]]].flat();         // [1, 2, [3, [4]]]
[1, [2, [3, [4]]]].flat(Infinity); // [1, 2, 3, 4]
["a b", "c"].flatMap((s) => s.split(" ")); // ["a","b","c"]
```

### Creating arrays

```js
Array.from({ length: 3 }, (_, i) => i * 2); // [0, 2, 4]
Array.from("abc");                           // ["a","b","c"]
Array.of(7);                                 // [7]  vs  Array(7) -> 7 empty slots
new Array(3).fill(0);                        // [0,0,0]
```

### forEach vs map

- `forEach` returns `undefined`, used for side effects. Can't `break` (use `for...of` or `some`).
- `map` returns a new array.

### Removing duplicates, intersection, difference

```js
const x = [1, 2, 2, 3], y = [2, 3, 4];
[...new Set(x)];                           // [1,2,3]
x.filter((v) => y.includes(v));            // intersection
x.filter((v) => !y.includes(v));           // difference
new Set(x).intersection(new Set(y));       // ES2025 Set methods
```

### Polyfills (very common in interviews)

```js
Array.prototype.myMap = function (cb, thisArg) {
  const out = [];
  for (let i = 0; i < this.length; i++) {
    if (i in this) out[i] = cb.call(thisArg, this[i], i, this);
  }
  return out;
};

Array.prototype.myFilter = function (cb, thisArg) {
  const out = [];
  for (let i = 0; i < this.length; i++) {
    if (i in this && cb.call(thisArg, this[i], i, this)) out.push(this[i]);
  }
  return out;
};

Array.prototype.myReduce = function (cb, initial) {
  let i = 0;
  let acc = initial;
  if (arguments.length < 2) {
    if (this.length === 0) throw new TypeError("Reduce of empty array with no initial value");
    acc = this[0];
    i = 1;
  }
  for (; i < this.length; i++) {
    if (i in this) acc = cb(acc, this[i], i, this);
  }
  return acc;
};

Array.prototype.myForEach = function (cb, thisArg) {
  for (let i = 0; i < this.length; i++) {
    if (i in this) cb.call(thisArg, this[i], i, this);
  }
};

// flat polyfill
function flatten(arr, depth = 1) {
  return depth > 0
    ? arr.reduce((acc, v) => acc.concat(Array.isArray(v) ? flatten(v, depth - 1) : v), [])
    : arr.slice();
}
flatten([1, [2, [3, [4]]]], Infinity); // [1,2,3,4]
```

### Array-like objects

Have `length` and indexed keys but no array methods: `arguments`, `NodeList`, strings.

```js
function f() { return Array.from(arguments); }
const nodes = [...document.querySelectorAll("div")];
```

### Chunk an array

```js
const chunk = (arr, size) =>
  Array.from({ length: Math.ceil(arr.length / size) }, (_, i) => arr.slice(i * size, i * size + size));
chunk([1, 2, 3, 4, 5], 2); // [[1,2],[3,4],[5]]
```

**Interview Qs**
- map vs forEach? → map returns a new array; forEach returns undefined.
- Does `sort` mutate? → Yes. Use `toSorted` or `[...arr].sort()`.
- Empty an array? → `arr.length = 0` (mutates; all references see it), or `arr = []` (new array).
- Check if an array contains an object with a property? → `some`.

---

## 21. Strings

Strings are **immutable** primitives; methods return new strings.

```js
const s = "  Hello World  ";
s.length;                 // 15
s.trim();                 // "Hello World"
s.toUpperCase();
s.includes("World");      // true
s.startsWith("  He");     // true
s.indexOf("o");           // 6
s.slice(2, 7);            // "Hello"
s.slice(-3);              // "d  "
s.substring(2, 7);        // "Hello" (no negative indexes)
s.split(" ");
s.replace("l", "L");      // first only
s.replaceAll("l", "L");   // all
"ab".repeat(3);           // "ababab"
"5".padStart(3, "0");     // "005"
"abc".at(-1);             // "c"
"abc".charCodeAt(0);      // 97
String.fromCharCode(97);  // "a"
```

### Template literals & tagged templates

```js
const name = "Rohit", age = 25;
const msg = `Name: ${name}, next year: ${age + 1}`;
const multi = `line 1
line 2`;

function highlight(strings, ...values) {
  return strings.reduce((out, str, i) => out + str + (values[i] !== undefined ? `<b>${values[i]}</b>` : ""), "");
}
highlight`Hi ${name}, you are ${age}`; // "Hi <b>Rohit</b>, you are <b>25</b>"
```

### Common string interview programs

```js
const reverse = (str) => [...str].reverse().join("");
const isPalindrome = (str) => {
  const clean = str.toLowerCase().replace(/[^a-z0-9]/g, "");
  return clean === [...clean].reverse().join("");
};
const capitalizeWords = (str) => str.replace(/\b\w/g, (c) => c.toUpperCase());
const isAnagram = (a, b) => [...a].sort().join("") === [...b].sort().join("");
const countVowels = (str) => (str.match(/[aeiou]/gi) || []).length;
const firstNonRepeating = (str) => [...str].find((c) => str.indexOf(c) === str.lastIndexOf(c));
const camelToSnake = (s) => s.replace(/[A-Z]/g, (c) => "_" + c.toLowerCase());
```

**Interview Qs**
- `slice` vs `substring` vs `substr`? → slice supports negatives; substring swaps args if start > end, treats negatives as 0; substr is deprecated.
- Are strings mutable? → No. `str[0] = "x"` does nothing.

---

## 22. Higher-Order Functions, Currying, Composition

### Higher-order function

```js
function withLogging(fn) {
  return function (...args) {
    console.log(`Calling ${fn.name} with`, args);
    return fn(...args);
  };
}
const loggedAdd = withLogging((a, b) => a + b);
loggedAdd(1, 2);
```

### Currying

Transforming `f(a, b, c)` into `f(a)(b)(c)`. Each call returns a function that takes the next argument.

```js
// Manual
const add = (a) => (b) => (c) => a + b + c;
add(1)(2)(3); // 6

// Real use: reusable configured functions
const log = (level) => (msg) => console.log(`[${level}] ${msg}`);
const error = log("ERROR");
error("Something broke");
```

### Generic curry function

```js
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) return fn.apply(this, args);
    return (...next) => curried.apply(this, [...args, ...next]);
  };
}
const sum3 = (a, b, c) => a + b + c;
const cs = curry(sum3);
cs(1)(2)(3); // 6
cs(1, 2)(3); // 6
cs(1)(2, 3); // 6
```

### Infinite currying — `sum(1)(2)(3)()`

```js
function sum(a) {
  return function (b) {
    if (b === undefined) return a;
    return sum(a + b);
  };
}
sum(1)(2)(3)(); // 6

// Variant using valueOf: sum(1)(2)(3) + 0
function sum2(a) {
  const fn = (b) => sum2(a + b);
  fn.valueOf = () => a;
  return fn;
}
+sum2(1)(2)(3); // 6
```

### Partial application

Fixing some arguments of a function, returning a function for the rest.

```js
const greet = (greeting, name) => `${greeting}, ${name}`;
const hello = greet.bind(null, "Hello");
hello("Rohit"); // "Hello, Rohit"
```

**Currying vs Partial**: currying always produces unary functions chained; partial application fixes any number of args once.

### Compose & Pipe

```js
const compose = (...fns) => (x) => fns.reduceRight((acc, fn) => fn(acc), x); // right -> left
const pipe = (...fns) => (x) => fns.reduce((acc, fn) => fn(acc), x);         // left -> right

const inc = (x) => x + 1;
const dbl = (x) => x * 2;
compose(inc, dbl)(5); // inc(dbl(5)) = 11
pipe(inc, dbl)(5);    // dbl(inc(5)) = 12
```

**Interview Qs**
- Why currying? → Reusability, function specialisation, cleaner composition.
- Implement `sum(1)(2)(3)()`. (above)

---

## 23. Functional Programming in Depth

**Functional Programming (FP)** is a style where programs are built from **pure functions** that transform **immutable data**, composed together, with **side effects pushed to the edges**. React (pure components, hooks), Redux (reducers), array methods and RxJS are all FP-inspired, so understanding FP makes modern JS code make sense.

(Higher-order functions, currying, partial application, `compose`/`pipe` are in the previous section.)

### Core principles

| Principle | Meaning |
|---|---|
| **Pure functions** | Same input → same output, no side effects |
| **Immutability** | Never change data; create new data |
| **First-class & higher-order functions** | Functions are values: pass, return, store them |
| **Composition** | Build big behaviour from small functions |
| **Declarative style** | Say *what* you want (`filter`), not *how* (index loops) |
| **Avoid shared mutable state** | Pass data in, return data out |
| **Referential transparency** | A call can be replaced with its result without changing the program |

### Imperative vs declarative

```js
const orders = [
  { id: 1, status: "paid", total: 500, country: "IN" },
  { id: 2, status: "pending", total: 300, country: "US" },
  { id: 3, status: "paid", total: 1200, country: "IN" },
];

// Imperative: HOW (mutable accumulator, index bookkeeping)
let revenue = 0;
for (let i = 0; i < orders.length; i++) {
  if (orders[i].status === "paid" && orders[i].country === "IN") revenue += orders[i].total;
}

// Declarative/functional: WHAT
const isPaid = (o) => o.status === "paid";
const inCountry = (c) => (o) => o.country === c;
const sum = (xs) => xs.reduce((a, b) => a + b, 0);

const revenue2 = sum(orders.filter(isPaid).filter(inCountry("IN")).map((o) => o.total)); // 1700
```

The small named functions (`isPaid`, `inCountry`) are reusable, testable and read like English.

---

### 1. Pure functions & side effects (deeper)

**Side effects** = anything a function does besides returning a value: mutating arguments or outer variables, network/DB calls, reading/writing files or storage, `console.log`, DOM changes, timers, `Date.now()`, `Math.random()`, throwing.

```js
// ❌ impure — depends on & changes outside state, hidden time dependency
let discountPct = 10;
function applyDiscount(cart) {
  cart.total = cart.total * (1 - discountPct / 100);   // mutates the argument
  cart.updatedAt = Date.now();                         // hidden input (time)
  return cart;
}

// ✅ pure — everything it needs comes in, result goes out
const applyDiscountPure = (cart, pct, now) => ({
  ...cart,
  total: Math.round(cart.total * (1 - pct / 100)),
  updatedAt: now,
});
```

Benefits: trivially **testable** (no mocks), **cacheable** (memoize), **safe to run in parallel / re-run** (React StrictMode double-render), easy to reason about.

#### Functional core, imperative shell (the production pattern)

Real apps must do side effects. Keep the **business logic pure** (the core) and do I/O in a thin outer layer (the shell).

```js
// CORE — pure, 100% unit-testable
function priceOrder(items, coupon, taxRate) {
  const subtotal = items.reduce((s, i) => s + i.pricePaise * i.qty, 0);
  const discount = coupon?.type === "percent" ? Math.round(subtotal * coupon.value / 100) : coupon?.value ?? 0;
  const taxable = Math.max(0, subtotal - discount);
  const tax = Math.round(taxable * taxRate);
  return { subtotal, discount, tax, total: taxable + tax };
}

// SHELL — side effects only (DB, HTTP, time)
async function checkoutHandler(req, res) {
  const cart = await db.cart.find(req.user.id);                 // I/O
  const coupon = await db.coupon.find(req.body.couponCode);     // I/O
  const pricing = priceOrder(cart.items, coupon, 0.18);         // pure
  const order = await db.order.create({ ...pricing, userId: req.user.id, createdAt: new Date() }); // I/O
  res.json(order);
}
```

### 2. Immutability in practice

```js
const user = { name: "A", address: { city: "Delhi" }, tags: ["js"] };

// Objects
const renamed = { ...user, name: "B" };
const moved = { ...user, address: { ...user.address, city: "Pune" } };   // copy each level you change
const { tags, ...withoutTags } = user;                                    // "delete" immutably

// Arrays — non-mutating methods (ES2023+)
const nums = [3, 1, 2];
nums.toSorted();          // [1, 2, 3]  (sort mutates!)
nums.toReversed();        // [2, 1, 3]
nums.with(0, 99);         // [99, 1, 2]
nums.toSpliced(1, 1);     // [3, 2]
[...nums, 4];             // add
nums.filter((n) => n !== 1);                    // remove
nums.map((n) => (n === 2 ? 20 : n));            // update

// Freeze to catch accidental mutation (shallow!)
const CONFIG = Object.freeze({ retries: 3 });
```

**Structural sharing**: an immutable update copies only the path that changed; untouched parts are **shared** by reference. That's why React/Redux can detect changes with a cheap `===` check.

```js
const next = { ...user, address: { ...user.address, city: "Pune" } };
next.tags === user.tags;        // true  — shared (unchanged)
next.address === user.address;  // false — changed path copied
```

**Immer** lets you write "mutating" code that produces immutable results (used inside Redux Toolkit):

```js
import { produce } from "immer";
const nextState = produce(state, (draft) => {
  draft.cart.items.push(newItem);        // looks like mutation
  draft.cart.total += newItem.price;     // Immer builds a new object with structural sharing
});
```

### 3. Declarative data pipelines

```js
const products = [
  { name: "Phone", category: "electronics", price: 20000, rating: 4.5 },
  { name: "Book", category: "books", price: 500, rating: 4.8 },
  { name: "Laptop", category: "electronics", price: 60000, rating: 4.2 },
];

// Top-rated electronics names, sorted by price
const result = products
  .filter((p) => p.category === "electronics")
  .filter((p) => p.rating >= 4.3)
  .toSorted((a, b) => a.price - b.price)
  .map((p) => p.name);                           // ["Phone"]

// Common reduce recipes
const indexBy = (xs, key) => Object.fromEntries(xs.map((x) => [x[key], x]));
const countBy = (xs, fn) => xs.reduce((acc, x) => ((acc[fn(x)] = (acc[fn(x)] ?? 0) + 1), acc), {});
const partition = (xs, pred) => xs.reduce(([yes, no], x) => (pred(x) ? [[...yes, x], no] : [yes, [...no, x]]), [[], []]);

Object.groupBy(products, (p) => p.category);      // built-in groupBy (ES2024)
countBy(products, (p) => p.category);             // { electronics: 2, books: 1 }
const [cheap, pricey] = partition(products, (p) => p.price < 10000);
```

**Don't overuse `reduce`** — if a `map`/`filter`/`for...of` is clearer, use it. `reduce` that builds objects by spreading every iteration (`{...acc, [k]: v}`) is O(n²); mutate the local accumulator instead (it's still pure from the outside).

### 4. Point-free style

Writing functions without mentioning their arguments, by composing other functions.

```js
const trim = (s) => s.trim();
const toLower = (s) => s.toLowerCase();
const pipe = (...fns) => (x) => fns.reduce((v, f) => f(v), x);

// pointed
const normalizeEmail = (email) => toLower(trim(email));
// point-free
const normalizeEmail2 = pipe(trim, toLower);

["  A@B.com "].map(normalizeEmail2);   // ["a@b.com"]
```

Great for small, well-named building blocks; unreadable when overdone. Beware passing functions that take extra args directly (`["1","2","3"].map(parseInt)` → `[1, NaN, NaN]`).

### 5. Handy functional utilities

```js
const identity = (x) => x;
const constant = (x) => () => x;
const not = (fn) => (...args) => !fn(...args);
const tap = (fn) => (x) => { fn(x); return x; };           // side effect in a pipeline (logging)
const prop = (key) => (obj) => obj?.[key];
const unique = (xs) => [...new Set(xs)];
const range = (n) => Array.from({ length: n }, (_, i) => i);

const activeEmails = pipe(
  (users) => users.filter(not((u) => u.banned)),
  tap((users) => console.log("active:", users.length)),
  (users) => users.map(prop("email")),
  unique,
);
```

### 6. Recursion, tail calls & trampolines

FP favours recursion over loops, but **JS engines (V8) don't do tail-call optimization**, so deep recursion overflows the stack.

```js
const sumTo = (n) => (n === 0 ? 0 : n + sumTo(n - 1));
sumTo(100_000);   // RangeError: Maximum call stack size exceeded
```

A **trampoline** turns recursion into a loop: the function returns a **thunk** (a function to call next) instead of recursing directly.

```js
const trampoline = (fn) => (...args) => {
  let result = fn(...args);
  while (typeof result === "function") result = result();
  return result;
};

const sumToT = trampoline(function sum(n, acc = 0) {
  return n === 0 ? acc : () => sum(n - 1, acc + n);   // return a thunk instead of recursing
});
sumToT(100_000);   // 5000050000 — no stack overflow
```

In practice: use loops or an explicit stack for deep/unbounded data; keep recursion for naturally recursive, bounded structures (trees, nested JSON).

### 7. Handling "nothing" and errors functionally

#### Option / Maybe — safe access without null checks everywhere

Modern JS gives most of this for free with `?.` and `??`:

```js
const city = user?.address?.city ?? "Unknown";
```

A tiny Maybe shows the idea of chaining operations that skip when a value is missing:

```js
const Maybe = (value) => ({
  map: (fn) => (value == null ? Maybe(null) : Maybe(fn(value))),
  getOrElse: (fallback) => value ?? fallback,
});

Maybe(user).map((u) => u.address).map((a) => a.city).map((c) => c.toUpperCase()).getOrElse("UNKNOWN");
```

#### Result / Either — errors as values

Instead of throwing, return `{ ok: true, value }` or `{ ok: false, error }`. Callers **must** handle both; failures compose through a pipeline.

```js
const Ok = (value) => ({ ok: true, value });
const Err = (error) => ({ ok: false, error });

const parseAge = (input) => {
  const n = Number(input);
  return Number.isInteger(n) ? Ok(n) : Err("Age must be a whole number");
};
const checkAdult = (age) => (age >= 18 ? Ok(age) : Err("Must be 18+"));

// chain: run the next step only if the previous succeeded
const andThen = (result, fn) => (result.ok ? fn(result.value) : result);

const r1 = andThen(parseAge("21"), checkAdult);   // { ok: true, value: 21 }
const r2 = andThen(parseAge("abc"), checkAdult);  // { ok: false, error: "Age must be a whole number" }
const r3 = andThen(parseAge("15"), checkAdult);   // { ok: false, error: "Must be 18+" }
```

Use exceptions for truly unexpected failures; use Result values for **expected** outcomes (validation, "not found", business rule violations). Libraries: `neverthrow`, `fp-ts`, `Effect`; Zod's `safeParse` returns a Result-like object.

### 8. Functors & monads (the intuition, no jargon overload)

- A **functor** is a container you can `map` over while keeping its shape: `Array.prototype.map`, `Maybe.map`.
- A **monad** also lets you **flatten** nested containers when a function itself returns a container: `Array.prototype.flatMap`, `Promise.then` (returning a promise inside `then` doesn't give `Promise<Promise<T>>`).

```js
[1, 2].map((x) => [x, x * 10]);      // [[1,10],[2,20]] — nested
[1, 2].flatMap((x) => [x, x * 10]);  // [1,10,2,20]     — flattened

fetchUser(1).then((u) => fetchPosts(u.id));   // Promise<Posts>, not Promise<Promise<Posts>>
```

You already use these patterns daily; the names just describe them.

### 9. Lazy evaluation

Compute values only when needed — useful for large or infinite sequences.

```js
function* naturals() { let n = 1; while (true) yield n++; }

// Iterator helpers (ES2025): lazy, no intermediate arrays
const firstFiveEvenSquares = naturals()
  .map((n) => n * n)
  .filter((n) => n % 2 === 0)
  .take(5)
  .toArray();                        // [4, 16, 36, 64, 100]
```

Array chains are **eager** (each step builds a whole new array) — fine for normal sizes; for huge data or streams, use lazy iterators/generators or a single loop.

### 10. FP in React & Redux

- **Components are (ideally) pure functions** of props + state → same inputs, same UI. Side effects go in event handlers/effects (the "imperative shell").
- **Reducers** are pure: `(state, action) => newState`, no mutation, no API calls.
- **Immutable updates** let React bail out with `Object.is` comparisons; mutation causes missed re-renders.
- **Derived data** is computed with pure functions (and memoized selectors).
- **Hooks composition** = function composition for stateful logic.

```js
// Memoized selector (reselect / RTK createSelector) — pure + cached
import { createSelector } from "@reduxjs/toolkit";
const selectItems = (state) => state.cart.items;
const selectTotal = createSelector([selectItems], (items) => items.reduce((s, i) => s + i.price * i.qty, 0));
```

### 11. Libraries

| Library | For |
|---|---|
| **Immer** | Immutable updates with mutable syntax |
| **Ramda**, **lodash/fp**, **Remeda** | Curried, data-last utility functions for composition (Remeda is TS-first) |
| **fp-ts**, **Effect** | Typed FP: Option, Either, Task, dependency & error management |
| **RxJS** | Functional reactive programming with streams (Angular, complex async UIs) |
| **Immutable.js** | Persistent data structures (less common now) |

### 12. Trade-offs & best practices

- ✅ Pure functions for business logic; side effects at the edges.
- ✅ Immutable updates for shared/state data; local mutation inside a function is fine if nothing outside can observe it.
- ✅ Small, well-named functions composed together.
- ✅ Declarative array methods for clarity.
- ⚠️ Don't chase point-free/"clever" code at the cost of readability — the team has to maintain it.
- ⚠️ Chained `map/filter/reduce` on huge arrays creates intermediate arrays — use one loop or lazy iterators when profiling shows it matters.
- ⚠️ Deep recursion → stack overflow in JS; prefer loops/trampolines.
- ⚠️ Deep-cloning big objects on every update is slow — update only the changed path (structural sharing).

### Interview Qs

1. What is functional programming? Its core principles?
2. What is a pure function? Give examples of side effects.
3. What is immutability and why does React/Redux rely on it?
4. What is referential transparency?
5. Declarative vs imperative — example?
6. What is "functional core, imperative shell"?
7. What is point-free style? Pros/cons?
8. Does JavaScript have tail-call optimization? What is a trampoline?
9. What are Maybe and Either/Result? When would you return errors as values instead of throwing?
10. Explain functor/monad with JS examples. → `map` vs `flatMap`, `Promise.then`.
11. What is structural sharing?
12. Eager vs lazy evaluation in JS?

---

## 24. Debounce & Throttle

Both are **rate-limiting techniques** for functions that get called too often — typing, scrolling, resizing, mouse moves, button spam, window focus, websocket messages. Without them you fire hundreds of API calls or re-renders per second, which wastes network, CPU and battery and can cause race conditions.

Both are built on **closures** (to remember the timer / last-call time across calls) + **higher-order functions** (they take a function and return a new, wrapped function).

### The one-line definitions

- **Debounce**: "Wait until the calls **stop** for `X` ms, then run **once**." Every new call **resets** the timer.
- **Throttle**: "Run **at most once every** `X` ms, no matter how many calls come in." Calls in between are ignored (or the last one is saved for later).

### Visual timeline

```
Events (user typing / scrolling):
time →   0   100  200  300  400  500  600  700  800  900  1000 1100 1200
events:  x    x    x    x              x    x                         

debounce(fn, 300)   (trailing):
                                  ✅ runs at 600 (300ms after last event at 300)
                                                      ✅ runs at 1000 (300ms after 700)

throttle(fn, 300)   (leading):
         ✅ 0          ✅ 300              ✅ 600         (every 300ms while events keep coming)
```

- Debounce → the function runs **after the burst ends** (1 call per burst).
- Throttle → the function runs **regularly during the burst** (1 call per interval).

### Debounce vs Throttle

| | Debounce | Throttle |
|---|---|---|
| Runs | After calls stop for X ms | At most once every X ms |
| Number of runs in a 5s continuous burst (X=500) | 1 (at the end) | ~10 |
| Timer | Reset on every call | Not reset |
| Good when you care about | The **final** value | **Regular updates** during activity |
| Typical uses | Search box, autocomplete, form auto-save, resize end, validation while typing, "save draft" | Scroll position, infinite scroll, mousemove / drag, window resize while resizing, analytics tracking, button spam, game input, rate-limited APIs |

**Rule of thumb**: "Do this *when the user is done*" → debounce. "Do this *while* the user is doing it, but not too often" → throttle.

---

### Debounce — basic (trailing)

```js
function debounce(fn, delay = 300) {
  let timerId; // survives between calls thanks to the closure

  return function (...args) {
    clearTimeout(timerId);                          // cancel the previous scheduled call
    timerId = setTimeout(() => {
      fn.apply(this, args);                         // keep `this` and the latest args
    }, delay);
  };
}
```

How it works step by step:
1. First call → schedule `fn` in 300ms.
2. Another call 100ms later → cancel the old timer, schedule again in 300ms.
3. No calls for 300ms → the timer finally fires → `fn` runs once with the **latest** arguments.

### Example 1 — search input (most asked)

```js
const input = document.querySelector("#search");

async function searchProducts(query) {
  if (!query.trim()) return renderResults([]);
  const res = await fetch(`/api/products?q=${encodeURIComponent(query)}`);
  renderResults(await res.json());
}

const debouncedSearch = debounce(searchProducts, 400);
input.addEventListener("input", (e) => debouncedSearch(e.target.value));
// Typing "iphone" quickly = 6 input events → only ONE API call, 400ms after the last key
```

### Example 2 — auto-save a form draft

```js
const saveDraft = debounce(async (data) => {
  await fetch("/api/drafts/42", { method: "PUT", body: JSON.stringify(data) });
  statusEl.textContent = "Saved ✓";
}, 1000);

editor.addEventListener("input", () => {
  statusEl.textContent = "Saving…";
  saveDraft({ content: editor.value });
});
```

### Example 3 — resize end (recalculate layout once)

```js
window.addEventListener("resize", debounce(() => {
  console.log("Final size:", window.innerWidth, window.innerHeight);
  recalculateChartLayout();
}, 200));
```

### Why `fn.apply(this, args)` and not just `fn()`?

- `args` → forwards the **latest** arguments (e.g. the latest input value).
- `this` → keeps the right `this` when the debounced function is used as a method or a DOM listener.

```js
const obj = {
  name: "search box",
  log: debounce(function () { console.log(this.name); }, 100),
};
obj.log(); // "search box" — works because we used a regular function + apply(this)
// If the wrapper used an arrow function, `this` would be lost.
```

### Common debounce bug — creating a new debounced function every time

```js
// ❌ BUG: a new debounce (new timer) is created on every event → nothing is debounced
input.addEventListener("input", (e) => debounce(search, 300)(e.target.value));

// ✅ create ONCE, reuse
const debouncedSearch = debounce(search, 300);
input.addEventListener("input", (e) => debouncedSearch(e.target.value));
```

(Same bug in React — see "Debounce/Throttle in React" below.)

---

### Debounce — production version (leading, trailing, maxWait, cancel, flush)

Real libraries (lodash `debounce`) support options:
- **leading**: run on the **first** call immediately, then ignore until calls stop.
- **trailing**: run after calls stop (default).
- **maxWait**: guarantee it runs at least once every `maxWait` ms even if calls never stop (e.g. a user who types non-stop still gets auto-saves).
- **cancel()**: drop the pending call (e.g. on component unmount / route change).
- **flush()**: run the pending call **right now** (e.g. save immediately before the page closes).

```js
function debounce(fn, wait = 300, { leading = false, trailing = true, maxWait } = {}) {
  let timerId = null;
  let maxTimerId = null;
  let lastArgs = null;
  let lastThis = null;
  let result;

  function invoke() {
    const args = lastArgs, ctx = lastThis;
    lastArgs = lastThis = null;
    clearTimeout(maxTimerId);
    maxTimerId = null;
    result = fn.apply(ctx, args);
    return result;
  }

  function onTimerEnd() {
    timerId = null;
    if (trailing && lastArgs) invoke(); // only if there were calls after the leading one
    lastArgs = lastThis = null;
  }

  function debounced(...args) {
    lastArgs = args;
    lastThis = this;
    const isFirstCallOfBurst = timerId === null;

    clearTimeout(timerId);
    timerId = setTimeout(onTimerEnd, wait);

    if (isFirstCallOfBurst && leading) {
      invoke();
    }
    if (maxWait !== undefined && maxTimerId === null && lastArgs) {
      maxTimerId = setTimeout(() => { if (lastArgs) invoke(); }, maxWait);
    }
    return result;
  }

  debounced.cancel = () => {
    clearTimeout(timerId);
    clearTimeout(maxTimerId);
    timerId = maxTimerId = lastArgs = lastThis = null;
  };

  debounced.flush = () => {
    if (timerId === null) return result;
    clearTimeout(timerId);
    timerId = null;
    return lastArgs ? invoke() : result;
  };

  debounced.pending = () => timerId !== null;

  return debounced;
}
```

```js
// leading: "submit" button that ignores double/triple clicks
const submitOrder = debounce(placeOrder, 1000, { leading: true, trailing: false });
payBtn.addEventListener("click", submitOrder); // first click fires immediately, spam clicks ignored

// maxWait: autosave at least every 5 seconds while typing continuously
const autosave = debounce(save, 1000, { maxWait: 5000 });

// flush before leaving the page so no edits are lost
window.addEventListener("beforeunload", () => autosave.flush());

// cancel on route change
router.on("leave", () => autosave.cancel());
```

### Async debounce (returns a promise with the result)

```js
function debounceAsync(fn, wait) {
  let timer;
  let pendingRejects = [];
  return (...args) =>
    new Promise((resolve, reject) => {
      clearTimeout(timer);
      pendingRejects.forEach((r) => r(new Error("debounced"))); // reject superseded calls
      pendingRejects = [reject];
      timer = setTimeout(async () => {
        pendingRejects = [];
        try { resolve(await fn(...args)); } catch (e) { reject(e); }
      }, wait);
    });
}

const checkUsername = debounceAsync((name) => fetch(`/api/username/${name}`).then((r) => r.json()), 400);
checkUsername("roh").catch(() => {});        // superseded
const { available } = await checkUsername("rohit"); // only this one hits the API
```

### Debounce + race conditions (important in production)

Debounce reduces calls, but **responses can still arrive out of order** (request for "ro" is slow, request for "rohit" is fast → the old result overwrites the new one). Combine debounce with **AbortController** or a "latest request wins" check.

```js
let controller;
const search = debounce(async (q) => {
  controller?.abort();                 // cancel the previous in-flight request
  controller = new AbortController();
  try {
    const res = await fetch(`/api/search?q=${q}`, { signal: controller.signal });
    render(await res.json());
  } catch (e) {
    if (e.name !== "AbortError") showError(e);
  }
}, 300);
```

---

### Throttle — basic (leading, timestamp-based)

```js
function throttle(fn, interval = 300) {
  let lastRun = 0;
  return function (...args) {
    const now = Date.now();
    if (now - lastRun >= interval) {
      lastRun = now;
      fn.apply(this, args);
    }
  };
}
```

Runs immediately on the first call, then ignores calls until `interval` has passed. **Problem**: the **last** call in a burst may be dropped (e.g. final scroll position never reported).

### Throttle — timer-based (leading + trailing)

Remembers the last ignored call and runs it at the end of the interval, so you never lose the final state.

```js
function throttle(fn, interval = 300, { leading = true, trailing = true } = {}) {
  let timerId = null;
  let lastArgs = null;
  let lastThis = null;
  let lastRun = 0;

  function run() {
    lastRun = Date.now();
    timerId = null;
    fn.apply(lastThis, lastArgs);
    lastArgs = lastThis = null;
  }

  function throttled(...args) {
    const now = Date.now();
    if (!lastRun && !leading) lastRun = now;      // skip the first immediate call if leading=false
    const remaining = interval - (now - lastRun);
    lastArgs = args;
    lastThis = this;

    if (remaining <= 0 || remaining > interval) {
      clearTimeout(timerId);
      run();                                       // enough time passed → run now
    } else if (!timerId && trailing) {
      timerId = setTimeout(run, remaining);        // schedule the trailing call
    }
  }

  throttled.cancel = () => {
    clearTimeout(timerId);
    timerId = lastArgs = lastThis = null;
    lastRun = 0;
  };
  return throttled;
}
```

### Example 1 — scroll progress bar / "back to top" button

```js
const onScroll = throttle(() => {
  const scrolled = window.scrollY / (document.body.scrollHeight - window.innerHeight);
  progressBar.style.width = `${scrolled * 100}%`;
  backToTop.hidden = window.scrollY < 500;
}, 100);
window.addEventListener("scroll", onScroll, { passive: true });
```

### Example 2 — infinite scroll

```js
const checkNearBottom = throttle(() => {
  const nearBottom = window.innerHeight + window.scrollY >= document.body.offsetHeight - 300;
  if (nearBottom && !isLoading && hasMore) loadNextPage();
}, 200);
window.addEventListener("scroll", checkNearBottom, { passive: true });
// (IntersectionObserver is usually better for infinite scroll — no scroll handler needed.)
```

### Example 3 — drag / mousemove / sending cursor position over websocket

```js
const sendCursor = throttle((x, y) => socket.emit("cursor", { x, y }), 50); // max 20 msgs/sec
canvas.addEventListener("mousemove", (e) => sendCursor(e.clientX, e.clientY));
```

### Example 4 — preventing button spam / API rate limits

```js
const likePost = throttle(() => api.like(postId), 2000, { trailing: false });
likeBtn.addEventListener("click", likePost); // at most one like request every 2s
```

### Throttle with requestAnimationFrame (best for visual updates)

For animations/visual updates, sync with the screen refresh rate (~60fps = ~16ms) instead of a fixed interval.

```js
function rafThrottle(fn) {
  let frameId = null;
  let lastArgs;
  const throttled = (...args) => {
    lastArgs = args;
    if (frameId !== null) return;
    frameId = requestAnimationFrame(() => {
      frameId = null;
      fn(...lastArgs);
    });
  };
  throttled.cancel = () => cancelAnimationFrame(frameId);
  return throttled;
}

window.addEventListener("scroll", rafThrottle(() => {
  header.classList.toggle("shrink", window.scrollY > 80);
}), { passive: true });
```

---

### Debounce/Throttle in React (common interview + production bug)

Every render creates new functions. If you call `debounce()` directly inside the component body, you get a **new debounced function (with a new timer) on every render** → debounce does nothing.

```jsx
// ❌ BUG: new debounce each render
function Search() {
  const [q, setQ] = useState("");
  const debounced = debounce((v) => fetchResults(v), 400);
  return <input value={q} onChange={(e) => { setQ(e.target.value); debounced(e.target.value); }} />;
}
```

**Fix 1 — debounce the value (simplest, most common)**

```jsx
function useDebounce(value, delay = 400) {
  const [debounced, setDebounced] = useState(value);
  useEffect(() => {
    const t = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(t);          // cleanup resets the timer on every change
  }, [value, delay]);
  return debounced;
}

function Search() {
  const [q, setQ] = useState("");
  const debouncedQ = useDebounce(q, 400);
  useEffect(() => {
    if (!debouncedQ) return;
    const controller = new AbortController();
    fetch(`/api/search?q=${debouncedQ}`, { signal: controller.signal }).then(/* ... */).catch(() => {});
    return () => controller.abort();       // handles out-of-order responses
  }, [debouncedQ]);
  return <input value={q} onChange={(e) => setQ(e.target.value)} />;
}
```

**Fix 2 — stable debounced callback with useRef/useMemo**

```jsx
function useDebouncedCallback(callback, delay) {
  const callbackRef = useRef(callback);
  useEffect(() => { callbackRef.current = callback; }, [callback]); // always call the latest callback

  const debounced = useMemo(
    () => debounce((...args) => callbackRef.current(...args), delay),
    [delay]
  );
  useEffect(() => () => debounced.cancel?.(), [debounced]); // cancel on unmount
  return debounced;
}

function Editor({ docId }) {
  const save = useDebouncedCallback((text) => api.save(docId, text), 1000);
  return <textarea onChange={(e) => save(e.target.value)} />;
}
```

**Throttled scroll in React**

```jsx
function useScrollY(interval = 100) {
  const [y, setY] = useState(0);
  useEffect(() => {
    const onScroll = throttle(() => setY(window.scrollY), interval);
    window.addEventListener("scroll", onScroll, { passive: true });
    return () => {
      window.removeEventListener("scroll", onScroll);
      onScroll.cancel?.();
    };
  }, [interval]);
  return y;
}
```

In production, most teams use **lodash** (`lodash.debounce`, `lodash.throttle`) or **use-debounce** instead of hand-written versions. You still need to understand them for interviews and bugs.

### Debounce vs Throttle vs useDeferredValue / useTransition

- Debounce/throttle **delay the work** by a fixed time.
- React's `useDeferredValue` / `useTransition` **don't delay requests**; they let React render expensive UI at lower priority. Use them for heavy rendering, and debounce for network calls.

### Choosing the delay

| Use case | Typical delay |
|---|---|
| Search / autocomplete | 250–500ms debounce |
| Form validation while typing | 300–500ms debounce |
| Auto-save | 1000–2000ms debounce (+ maxWait ~5–10s) |
| Resize end | 150–250ms debounce |
| Scroll / mousemove UI | rAF throttle or 50–100ms throttle |
| Analytics events | 1000ms+ throttle |
| Button double-click protection | leading debounce 500–1000ms |

### Testing debounce/throttle (fake timers)

```js
import { vi, test, expect } from "vitest";

test("debounce calls once after the delay", () => {
  vi.useFakeTimers();
  const fn = vi.fn();
  const d = debounce(fn, 300);
  d("a"); d("b"); d("c");
  expect(fn).not.toHaveBeenCalled();
  vi.advanceTimersByTime(300);
  expect(fn).toHaveBeenCalledTimes(1);
  expect(fn).toHaveBeenCalledWith("c"); // latest args
  vi.useRealTimers();
});

test("throttle runs at most once per interval", () => {
  vi.useFakeTimers();
  const fn = vi.fn();
  const t = throttle(fn, 100);
  t(); t(); t();                 // first runs immediately
  expect(fn).toHaveBeenCalledTimes(1);
  vi.advanceTimersByTime(100);   // trailing call
  expect(fn).toHaveBeenCalledTimes(2);
  vi.useRealTimers();
});
```

### Interview Qs

- **Debounce vs throttle? Give real examples.** → Search box (debounce) vs scroll handler (throttle).
- **Implement debounce.** → clearTimeout + setTimeout inside a closure; forward `this` and args.
- **Implement throttle (both timestamp and timer versions).**
- **What are leading and trailing options?** → Leading = run on the first call; trailing = run after the wait with the last args.
- **What's `maxWait`?** → Upper bound so a debounced function still runs during non-stop calls; debounce with `maxWait = wait` behaves like throttle.
- **Which JS concepts do they use?** → Closures, higher-order functions, timers/event loop, `this`/apply.
- **Why doesn't debounce work in my React component?** → New debounced function every render; use `useMemo`/`useRef` or debounce the value.
- **Does debounce prevent race conditions?** → No. Also cancel old requests (AbortController) or ignore stale responses.
- **Debounce vs throttle for infinite scroll?** → Throttle (or IntersectionObserver); debounce would wait until scrolling stops.
- **How would you debounce on the server?** → That's rate limiting / request coalescing (see Node notes).

---

## 25. Event Loop

JS runs on one thread, so async work is handled like this:

1. **Call Stack** — runs synchronous code.
2. **Web APIs / Node APIs** — timers, fetch, DOM events, fs run outside the JS thread.
3. **Callback (Macrotask) Queue** — `setTimeout`, `setInterval`, `setImmediate`, I/O, UI events, `MessageChannel`.
4. **Microtask Queue** — Promise callbacks (`.then/.catch/.finally`), `await` continuations, `queueMicrotask`, `MutationObserver`. (Node also has `process.nextTick`, which runs even before promises.)
5. **Event Loop** — when the call stack is empty:
   - run **ALL** microtasks (including new ones added during this step),
   - (browser) render if needed (`requestAnimationFrame` runs before paint),
   - take **ONE** macrotask, run it, repeat.

```
┌──────────────┐     ┌───────────────┐
│  Call Stack  │ ◄── │  Event Loop   │
└──────────────┘     └───────┬───────┘
                             │ 1st: all microtasks
                   ┌─────────▼─────────┐
                   │ Microtask Queue   │  Promise.then, await, queueMicrotask
                   └───────────────────┘
                             │ 2nd: one macrotask
                   ┌─────────▼─────────┐
                   │ Macrotask Queue   │  setTimeout, setInterval, I/O, events
                   └───────────────────┘
```

### Example 1 — classic order

```js
console.log("1");
setTimeout(() => console.log("2"), 0);
Promise.resolve().then(() => console.log("3"));
console.log("4");
// 1 4 3 2
```

### Example 2 — nested

```js
console.log("start");
setTimeout(() => {
  console.log("timeout 1");
  Promise.resolve().then(() => console.log("promise inside timeout"));
}, 0);
setTimeout(() => console.log("timeout 2"), 0);
Promise.resolve()
  .then(() => console.log("promise 1"))
  .then(() => console.log("promise 2"));
queueMicrotask(() => console.log("microtask"));
console.log("end");

// start
// end
// promise 1
// microtask
// promise 2
// timeout 1
// promise inside timeout
// timeout 2
```

### Example 3 — async/await ordering

```js
async function a() {
  console.log("a start");
  await b();
  console.log("a end"); // goes to microtask queue
}
async function b() { console.log("b"); }

console.log("script start");
a();
console.log("script end");
// script start, a start, b, script end, a end
```

### setTimeout(fn, 0) isn't really 0

It means "at least 0 ms, after the stack is clear and microtasks are done". Browsers clamp nested timers to ≥ 4ms after 5 levels.

### Microtask starvation

If microtasks keep adding microtasks, macrotasks (and rendering) never run.

```js
function loop() { Promise.resolve().then(loop); }
loop(); // page freezes
```

### Blocking the event loop

```js
setTimeout(() => console.log("timer"), 0);
const start = Date.now();
while (Date.now() - start < 3000) {} // blocks 3s
// "timer" prints only after 3 s
```

**Interview Qs**
- Explain the event loop. (above)
- Microtask vs macrotask? → Microtasks (promises) run right after current sync code, all of them, before the next macrotask (timers).
- Why does a promise callback run before `setTimeout(…, 0)`? → Microtask queue has priority.
- How to not block the UI with heavy computation? → Web Workers, chunking with `setTimeout`/`requestIdleCallback`, or move it to the server.

---

## 26. Callbacks & Callback Hell

A **callback** is a function passed into another function to be executed later (sync like `map`, or async like `setTimeout`).

### Callback hell (Pyramid of doom)

Nested async callbacks → hard to read, handle errors, and maintain.

```js
getUser(1, (err, user) => {
  if (err) return handleError(err);
  getOrders(user.id, (err, orders) => {
    if (err) return handleError(err);
    getOrderDetails(orders[0].id, (err, details) => {
      if (err) return handleError(err);
      getShipping(details.shipId, (err, ship) => {
        console.log(ship);
      });
    });
  });
});
```

### Inversion of control

You hand your callback to someone else's code and trust it to call it **once**, with correct args, at the right time. It might call it twice, never, or synchronously. Promises fix this (a promise settles only once).

### Error-first callbacks (Node convention)

```js
const fs = require("fs");
fs.readFile("a.txt", "utf8", (err, data) => {
  if (err) return console.error(err);
  console.log(data);
});
```

### Fix: Promises / async-await

```js
async function run() {
  try {
    const user = await getUser(1);
    const orders = await getOrders(user.id);
    const details = await getOrderDetails(orders[0].id);
    const ship = await getShipping(details.shipId);
    console.log(ship);
  } catch (e) {
    handleError(e);
  }
}
```

### Promisify a callback function

```js
function promisify(fn) {
  return (...args) =>
    new Promise((resolve, reject) => {
      fn(...args, (err, result) => (err ? reject(err) : resolve(result)));
    });
}
const readFileP = promisify(fs.readFile);
// Node has util.promisify built-in
```

---

## 27. Promises

A **Promise** is an object representing the eventual completion (or failure) of an async operation.

### States

- `pending` → initial
- `fulfilled` → resolved with a value
- `rejected` → failed with a reason

Once **settled** (fulfilled/rejected) it never changes.

### Creating & consuming

```js
const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    const ok = Math.random() > 0.5;
    ok ? resolve("Success!") : reject(new Error("Failed"));
  }, 1000);
});

p.then((value) => console.log(value))
 .catch((err) => console.error(err.message))
 .finally(() => console.log("done")); // runs either way, receives no value
```

The executor runs **synchronously**:

```js
console.log("A");
new Promise((res) => { console.log("B"); res(); });
console.log("C");
// A B C
```

### Chaining

`.then` returns a **new promise**. Returning a value passes it on; returning a promise waits for it; throwing rejects.

```js
fetch("/api/user")
  .then((res) => res.json())             // returns a promise
  .then((user) => fetch(`/api/posts/${user.id}`))
  .then((res) => res.json())
  .then((posts) => console.log(posts))
  .catch((err) => console.error(err));   // catches ANY error above
```

```js
Promise.resolve(1)
  .then((x) => x + 1)        // 2
  .then((x) => { throw new Error("boom"); })
  .then((x) => console.log("skipped"))
  .catch((e) => { console.log(e.message); return 10; }) // recovers
  .then((x) => console.log(x)); // 10
```

### Promise combinators

| Method | Resolves when | Rejects when |
|---|---|---|
| `Promise.all([...])` | **all** fulfill → array of values (in order) | **any one** rejects (fail-fast) |
| `Promise.allSettled([...])` | all settle → `[{status, value/reason}]` | never |
| `Promise.race([...])` | first to **settle** (fulfill or reject) | first settles with rejection |
| `Promise.any([...])` | first to **fulfill** | all reject → `AggregateError` |

```js
const fast = new Promise((r) => setTimeout(() => r("fast"), 100));
const slow = new Promise((r) => setTimeout(() => r("slow"), 500));
const fail = new Promise((_, rej) => setTimeout(() => rej(new Error("fail")), 200));

Promise.all([fast, slow]).then(console.log);          // ["fast", "slow"] after 500ms
Promise.all([fast, fail, slow]).catch((e) => console.log(e.message)); // "fail"
Promise.allSettled([fast, fail]).then(console.log);
// [{status:"fulfilled", value:"fast"}, {status:"rejected", reason: Error}]
Promise.race([slow, fail]).catch((e) => console.log("race:", e.message)); // "fail"
Promise.any([fail, slow]).then(console.log);          // "slow"
```

### Timeout a promise with race

```js
const withTimeout = (promise, ms) =>
  Promise.race([
    promise,
    new Promise((_, reject) => setTimeout(() => reject(new Error("Timeout")), ms)),
  ]);
withTimeout(fetch("/slow"), 3000).catch(console.error);
```

### Promise.withResolvers (ES2024)

```js
const { promise, resolve, reject } = Promise.withResolvers();
button.onclick = () => resolve("clicked");
await promise;
```

### Sequential vs Parallel

```js
const ids = [1, 2, 3];

// Sequential (one after another) — slow
for (const id of ids) {
  const u = await fetchUser(id);
}

// Parallel — fast
const users = await Promise.all(ids.map(fetchUser));
```

### Retry with backoff

```js
async function retry(fn, retries = 3, delay = 500) {
  try {
    return await fn();
  } catch (err) {
    if (retries === 0) throw err;
    await new Promise((r) => setTimeout(r, delay));
    return retry(fn, retries - 1, delay * 2);
  }
}
```

### Concurrency limit (run N at a time)

```js
async function promisePool(tasks, limit) {
  const results = [];
  let i = 0;
  async function worker() {
    while (i < tasks.length) {
      const idx = i++;
      results[idx] = await tasks[idx]();
    }
  }
  await Promise.all(Array.from({ length: limit }, worker));
  return results;
}
```

### Polyfills

```js
Promise.myAll = function (promises) {
  return new Promise((resolve, reject) => {
    const results = [];
    let done = 0;
    if (promises.length === 0) return resolve([]);
    promises.forEach((p, i) => {
      Promise.resolve(p).then((val) => {
        results[i] = val;
        if (++done === promises.length) resolve(results);
      }, reject);
    });
  });
};

Promise.myAllSettled = function (promises) {
  return Promise.myAll(
    promises.map((p) =>
      Promise.resolve(p).then(
        (value) => ({ status: "fulfilled", value }),
        (reason) => ({ status: "rejected", reason })
      )
    )
  );
};

Promise.myRace = function (promises) {
  return new Promise((resolve, reject) => {
    promises.forEach((p) => Promise.resolve(p).then(resolve, reject));
  });
};

Promise.myAny = function (promises) {
  return new Promise((resolve, reject) => {
    const errors = [];
    let rejected = 0;
    if (promises.length === 0) return reject(new AggregateError([], "All promises were rejected"));
    promises.forEach((p, i) => {
      Promise.resolve(p).then(resolve, (err) => {
        errors[i] = err;
        if (++rejected === promises.length) reject(new AggregateError(errors, "All promises were rejected"));
      });
    });
  });
};
```

### Custom Promise implementation (simplified)

```js
class MyPromise {
  #state = "pending";
  #value;
  #handlers = [];

  constructor(executor) {
    const settle = (state, value) => {
      if (this.#state !== "pending") return;
      if (state === "fulfilled" && value && typeof value.then === "function") {
        return value.then((v) => settle("fulfilled", v), (e) => settle("rejected", e));
      }
      this.#state = state;
      this.#value = value;
      this.#handlers.forEach((h) => h());
    };
    try {
      executor((v) => settle("fulfilled", v), (e) => settle("rejected", e));
    } catch (e) {
      settle("rejected", e);
    }
  }

  then(onFulfilled, onRejected) {
    return new MyPromise((resolve, reject) => {
      const run = () =>
        queueMicrotask(() => {
          const cb = this.#state === "fulfilled" ? onFulfilled : onRejected;
          if (typeof cb !== "function") {
            return this.#state === "fulfilled" ? resolve(this.#value) : reject(this.#value);
          }
          try { resolve(cb(this.#value)); } catch (e) { reject(e); }
        });
      this.#state === "pending" ? this.#handlers.push(run) : run();
    });
  }

  catch(onRejected) { return this.then(undefined, onRejected); }
  finally(cb) {
    return this.then(
      (v) => MyPromise.resolve(cb()).then(() => v),
      (e) => MyPromise.resolve(cb()).then(() => { throw e; })
    );
  }
  static resolve(v) { return v instanceof MyPromise ? v : new MyPromise((r) => r(v)); }
  static reject(e) { return new MyPromise((_, r) => r(e)); }
}
```

### Unhandled rejections

```js
Promise.reject(new Error("oops")); // "Uncaught (in promise)" warning
window.addEventListener("unhandledrejection", (e) => console.log(e.reason));
process.on("unhandledRejection", (reason) => {}); // Node
```

**Interview Qs**
- Promise states? → pending, fulfilled, rejected.
- `Promise.all` vs `allSettled`? → all fails fast; allSettled waits for all and never rejects.
- `race` vs `any`? → race = first settled (either way); any = first fulfilled.
- Is `.then` sync? → Registering is sync; the callback runs async as a microtask.
- Polyfill for Promise.all. (above)

---

## 28. Async / Await

`async/await` is syntactic sugar over promises that makes async code look synchronous.

- An `async` function **always returns a promise**.
- `await` pauses the function (not the thread!) until the promise settles; the rest of the function runs as a microtask.
- `await` can only be used inside `async` functions or at the top level of ES modules.

```js
async function getNum() { return 5; }
getNum().then(console.log); // 5  (wrapped in Promise.resolve)

async function fails() { throw new Error("x"); }
fails().catch((e) => console.log(e.message)); // "x"
```

### Example — fetch with error handling

```js
async function loadUser(id) {
  try {
    const res = await fetch(`/api/users/${id}`);
    if (!res.ok) throw new Error(`HTTP ${res.status}`); // fetch doesn't reject on 404/500!
    return await res.json();
  } catch (err) {
    console.error("Failed:", err.message);
    return null;
  } finally {
    console.log("request finished");
  }
}
```

### Example — parallel with await

```js
// ❌ Sequential — total time = t1 + t2
const user = await getUser();
const posts = await getPosts();

// ✅ Parallel — total time = max(t1, t2)
const [user2, posts2] = await Promise.all([getUser(), getPosts()]);

// ✅ Start both, await later
const userP = getUser();
const postsP = getPosts();
const u = await userP, p = await postsP;
```

### await in loops

```js
// forEach does NOT wait for async callbacks
[1, 2, 3].forEach(async (id) => { await save(id); });
console.log("done?"); // runs before saves finish

// sequential
for (const id of [1, 2, 3]) await save(id);

// parallel
await Promise.all([1, 2, 3].map((id) => save(id)));

// for await...of — for async iterables
for await (const chunk of stream) process(chunk);
```

### sleep helper

```js
const sleep = (ms) => new Promise((r) => setTimeout(r, ms));
await sleep(1000);
```

### Top-level await (ES modules)

```js
// config.mjs
const res = await fetch("/config.json");
export const config = await res.json();
```

### Promises vs async/await

| Promises | async/await |
|---|---|
| `.then` chain | looks synchronous |
| `.catch` | `try/catch` |
| Good for combinators | Good for step-by-step logic |
| Both are the same thing underneath | |

**Interview Qs**
- What does an async function return? → Always a promise.
- Does await block the thread? → No, it suspends only that function; the event loop continues.
- How to handle errors? → try/catch, or `.catch()` on the returned promise.
- Why is `forEach` + `async` a bug? → forEach ignores returned promises.

---

## 29. Iterators & Generators

### Iterator protocol

An object is an **iterator** if it has `next()` returning `{ value, done }`.
An object is **iterable** if it has `[Symbol.iterator]()` returning an iterator. Iterables work with `for...of`, spread, destructuring, `Array.from`.

```js
const range = {
  from: 1,
  to: 4,
  [Symbol.iterator]() {
    let cur = this.from, last = this.to;
    return {
      next: () => (cur <= last ? { value: cur++, done: false } : { value: undefined, done: true }),
    };
  },
};
for (const n of range) console.log(n); // 1 2 3 4
[...range]; // [1,2,3,4]
```

### Generators

`function*` returns a generator object (both iterator and iterable). `yield` pauses; `next()` resumes.

```js
function* counter() {
  yield 1;
  yield 2;
  return 3;
}
const g = counter();
g.next(); // {value:1, done:false}
g.next(); // {value:2, done:false}
g.next(); // {value:3, done:true}
g.next(); // {value:undefined, done:true}
```

```js
// Infinite ID generator — lazy evaluation
function* idGen() {
  let id = 1;
  while (true) yield id++;
}
const ids = idGen();
ids.next().value; // 1
ids.next().value; // 2
```

```js
// Two-way communication
function* conversation() {
  const name = yield "What's your name?";
  const hobby = yield `Hi ${name}, hobby?`;
  return `${name} likes ${hobby}`;
}
const c = conversation();
c.next().value;          // "What's your name?"
c.next("Rohit").value;   // "Hi Rohit, hobby?"
c.next("coding").value;  // "Rohit likes coding"
```

```js
// yield* delegates
function* inner() { yield "a"; yield "b"; }
function* outer() { yield 1; yield* inner(); yield 2; }
[...outer()]; // [1, "a", "b", 2]
```

### Async generators

```js
async function* paginate(url) {
  let next = url;
  while (next) {
    const res = await fetch(next).then((r) => r.json());
    yield res.items;
    next = res.nextPage;
  }
}
for await (const items of paginate("/api/items?page=1")) console.log(items);
```

### Iterator helpers (ES2025)

```js
idGen().filter((n) => n % 2).map((n) => n * 10).take(3).toArray(); // [10, 30, 50]
```

**Interview Qs**
- Generator use cases? → Lazy sequences, infinite streams, pagination, custom iterables, redux-saga.
- Iterable vs iterator? → Iterable has `[Symbol.iterator]`; the iterator has `next()`.

---

## 30. Symbol, Map, Set, WeakMap, WeakSet

### Symbol

Unique and immutable primitive, often used as a hidden/non-colliding object key.

```js
const id = Symbol("id");
const id2 = Symbol("id");
id === id2; // false

const user = { name: "A", [id]: 123 };
Object.keys(user);                 // ["name"] — symbols are skipped
JSON.stringify(user);              // {"name":"A"}
Object.getOwnPropertySymbols(user);// [Symbol(id)]

Symbol.for("app") === Symbol.for("app"); // true — global registry
```

Well-known symbols: `Symbol.iterator`, `Symbol.asyncIterator`, `Symbol.toPrimitive`, `Symbol.hasInstance`, `Symbol.toStringTag`.

### Map vs Object

| Map | Object |
|---|---|
| Any key type (objects, functions) | Only strings/symbols |
| Keeps insertion order | Mostly ordered (integer keys first) |
| `.size` | `Object.keys(o).length` |
| Directly iterable | Need `Object.entries` |
| Better for frequent add/remove | Better for fixed structures / JSON |
| No prototype key collisions | `"__proto__"`/`"constructor"` risk |

```js
const m = new Map();
const keyObj = { id: 1 };
m.set("a", 1).set(keyObj, "object key");
m.get(keyObj);    // "object key"
m.has("a");       // true
m.size;           // 2
m.delete("a");
for (const [k, v] of m) console.log(k, v);
new Map(Object.entries({ x: 1 }));    // object -> map
Object.fromEntries(m);                // map -> object
```

### Set

Collection of unique values.

```js
const s = new Set([1, 2, 2, 3]);
s.add(4); s.has(2); s.delete(1); s.size; // 3
[...s];

// ES2025 set methods
const A = new Set([1, 2, 3]), B = new Set([2, 3, 4]);
A.union(B);               // {1,2,3,4}
A.intersection(B);        // {2,3}
A.difference(B);          // {1}
A.symmetricDifference(B); // {1,4}
A.isSubsetOf(B);          // false
```

### WeakMap & WeakSet

- Keys (WeakMap) / values (WeakSet) must be **objects** (or non-registered symbols).
- Hold them **weakly** — if nothing else references the key, it can be garbage collected.
- **Not iterable**, no `size`, no `clear`.

```js
// Private data per instance / caching without leaks
const privateData = new WeakMap();
class User {
  constructor(pw) { privateData.set(this, { pw }); }
  check(pw) { return privateData.get(this).pw === pw; }
}

// Tracking visited DOM nodes
const visited = new WeakSet();
function visit(node) {
  if (visited.has(node)) return;
  visited.add(node);
}
```

### WeakRef & FinalizationRegistry

```js
let big = { data: new Array(1e6) };
const ref = new WeakRef(big);
big = null;
ref.deref(); // object or undefined if collected

const registry = new FinalizationRegistry((heldValue) => console.log("cleaned", heldValue));
registry.register(someObj, "someObj");
```

**Interview Qs**
- Map vs Object? (table)
- Map vs WeakMap? → WeakMap keys are objects held weakly, not iterable, prevents leaks.
- Use of Symbol? → Unique keys, hidden properties, customizing built-in behaviour.

---

## 31. Modules

Modules let you split code into files with their own scope.

### CommonJS (Node, older)

```js
// math.js
const add = (a, b) => a + b;
module.exports = { add };
// or exports.add = add;

// app.js
const { add } = require("./math");
```

### ES Modules (standard)

```js
// math.mjs
export const add = (a, b) => a + b;
export default function sub(a, b) { return a - b; }

// app.mjs
import sub, { add } from "./math.mjs";
import * as math from "./math.mjs";
import { add as plus } from "./math.mjs";
export { add } from "./math.mjs"; // re-export
```

### Dynamic import (lazy loading / code splitting)

```js
button.addEventListener("click", async () => {
  const { heavyChart } = await import("./chart.js");
  heavyChart();
});
```

### CJS vs ESM

| CommonJS | ES Modules |
|---|---|
| `require` / `module.exports` | `import` / `export` |
| Synchronous loading | Asynchronous, statically analysable |
| Loaded at runtime (can be conditional) | Imports hoisted, resolved before execution |
| Exports a **copy** of the value | **Live bindings** (read-only view of the export) |
| `this` = `module.exports` | `this` = `undefined` |
| Tree-shaking hard | Tree-shakeable |
| `__dirname` available | Use `import.meta.url` / `import.meta.dirname` |
| Strict mode optional | Always strict |

```js
// Live binding demo (ESM)
// counter.mjs
export let count = 0;
export const inc = () => count++;
// main.mjs
import { count, inc } from "./counter.mjs";
inc();
console.log(count); // 1 (CJS equivalent would print 0)
```

### Named vs default export

- Named: many per file, must import with same name (or rename with `as`). Better for refactoring/auto-imports.
- Default: one per file, importer picks any name.

**Interview Qs**
- Tree shaking? → Bundler removes unused exports; works because ESM imports are static.
- Module pattern before ES6? → IIFE + closures.

---

## 32. Build Tooling: Transpilers, Bundlers & the JS Toolchain

Browsers don't run your source code as written: JSX, TypeScript, modern syntax, hundreds of npm modules, CSS modules, image imports. The **build toolchain** turns that source into optimized files browsers can load quickly.

### What a build does

```
src/ (TS, JSX, ESM imports, CSS, images, env vars)
   │  1. Resolve imports (node_modules, aliases like @/components)
   │  2. Transform: TS → JS, JSX → JS, modern syntax → target syntax
   │  3. Bundle: combine modules into a few files (chunks)
   │  4. Optimize: tree-shake, minify, code-split, hash filenames, compress
   │  5. Emit assets + source maps + manifest
   ▼
dist/  index.html, assets/app.3f9a1c.js, assets/vendor.8b2e.js, assets/app.c1d2.css
```

---

### 1. Transpilers (compilers): Babel, SWC, esbuild, tsc

A **transpiler** converts code from one version/syntax of a language to another: new JS → older JS, TypeScript → JS, JSX → `jsx()` calls.

| Tool | Written in | Notes |
|---|---|---|
| **Babel** | JS | Most configurable, huge plugin ecosystem, slower |
| **SWC** | Rust | ~20x faster than Babel; used by Next.js, Vite React SWC plugin, Jest via `@swc/jest` |
| **esbuild** | Go | Extremely fast transpile + bundle; used inside Vite for dev |
| **tsc** | TS | The only one that **type-checks**; others just strip types |
| **Oxc** | Rust | New fast parser/transformer/linter (powers Rolldown) |

```js
// Input (modern + JSX)
const user = data?.user ?? "guest";
const App = () => <h1 className="title">Hi {user}</h1>;

// Output (targeting older browsers)
var _data$user;
var user = (_data$user = data === null || data === void 0 ? void 0 : data.user) !== null && _data$user !== void 0 ? _data$user : "guest";
var App = function () { return _jsx("h1", { className: "title", children: ["Hi ", user] }); };
```

```json
// babel.config.json
{
  "presets": [
    ["@babel/preset-env", { "useBuiltIns": "usage", "corejs": "3.38" }],
    ["@babel/preset-react", { "runtime": "automatic" }],
    "@babel/preset-typescript"
  ]
}
```

**Important**: esbuild/SWC/Babel only **remove** TypeScript types — they never report type errors. Always run `tsc --noEmit` in CI (or in your editor / pre-commit).

### 2. Transpiling vs Polyfilling

| Transpiling | Polyfilling |
|---|---|
| Rewrites **syntax** at build time | Adds missing **APIs** at runtime |
| `?.`, `??`, arrow functions, classes, `async/await`, spread | `Promise`, `Array.prototype.flat`, `Object.groupBy`, `structuredClone`, `fetch` |
| Done by Babel/SWC/esbuild | Done by **core-js** or manual polyfills |

```js
// Syntax can be transpiled:
const x = a ?? b;          // → a !== null && a !== void 0 ? a : b

// An API can't be transpiled — it must exist at runtime → polyfill:
[1, [2]].flat();           // needs Array.prototype.flat in old browsers
```

```js
// A hand-written polyfill (feature detection first!)
if (!Array.prototype.at) {
  Array.prototype.at = function (i) {
    i = Math.trunc(i) || 0;
    if (i < 0) i += this.length;
    return this[i];
  };
}
```

- **core-js** + Babel `useBuiltIns: "usage"` injects only the polyfills your code actually uses for your target browsers.
- Polyfills add bytes — target modern browsers when you can.

### 3. Browserslist — defining your target browsers

One config shared by Babel, SWC, Autoprefixer, PostCSS, Lightning CSS, ESLint compat plugins.

```json
// package.json
{
  "browserslist": [
    "> 0.5%, last 2 versions, not dead",
    "not op_mini all"
  ]
}
```

```bash
npx browserslist                       # see the resolved list
npx browserslist "baseline widely available"
```

Vite's default build target is "baseline widely available" modern browsers (ES2020+ features, native ESM), which is why modern Vite output is small. Use `@vitejs/plugin-legacy` only if you must support old browsers.

---

### 4. Bundlers

A **bundler** follows `import` statements from entry points, builds a **dependency graph**, and outputs optimized bundles.

Why still bundle when browsers support ES modules natively?
- Thousands of small module requests (node_modules!) → slow waterfalls even with HTTP/2.
- Tree-shaking, minification, code-splitting, hashing, asset handling (CSS, images, fonts), env variables, JSX/TS transforms.

| Tool | Notes |
|---|---|
| **Vite** | Dev: native ESM served on demand + esbuild pre-bundling of deps → instant start & fast HMR. Build: Rollup (moving to Rolldown, a Rust Rollup). Default choice for new React/Vue/Svelte SPAs |
| **Webpack** | Most configurable & mature; loaders + plugins; Module Federation (micro-frontends). Common in older/enterprise apps |
| **Rollup** | Great ESM output & tree-shaking; best for **libraries** |
| **esbuild** | Blazing fast bundler; limited plugin/code-splitting features; great for scripts, Lambdas, internal tools |
| **Rspack / Rsbuild** | Rust, webpack-compatible API, much faster — easy migration from webpack |
| **Turbopack** | Rust bundler inside Next.js |
| **Parcel** | Zero-config |
| **tsup / tsdown / unbuild** | Simple library bundlers (ESM + CJS + .d.ts) |

### Vite config example

```js
// vite.config.js
import { defineConfig, loadEnv } from "vite";
import react from "@vitejs/plugin-react-swc";
import path from "node:path";

export default defineConfig(({ mode }) => {
  const env = loadEnv(mode, process.cwd(), "");
  return {
    plugins: [react()],
    resolve: { alias: { "@": path.resolve(__dirname, "src") } },   // import Button from "@/components/Button"
    server: {
      port: 5173,
      proxy: { "/api": { target: "http://localhost:3000", changeOrigin: true } }, // avoid CORS in dev
    },
    build: {
      target: "es2020",
      sourcemap: "hidden",          // generate maps but don't reference them publicly (upload to Sentry)
      rollupOptions: {
        output: {
          manualChunks: { react: ["react", "react-dom"], charts: ["recharts"] }, // split big vendors
        },
      },
      chunkSizeWarningLimit: 600,
    },
    define: { __APP_VERSION__: JSON.stringify(env.npm_package_version) },
  };
});
```

```js
// Env vars in Vite — only VITE_* are exposed to client code (and they are PUBLIC)
const apiUrl = import.meta.env.VITE_API_URL;
import.meta.env.MODE;    // "development" | "production"
import.meta.env.DEV;     // boolean
```

### Webpack config example (for reading older codebases)

```js
// webpack.config.js
const HtmlWebpackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = (env, argv) => ({
  entry: "./src/index.tsx",
  output: {
    path: __dirname + "/dist",
    filename: "[name].[contenthash].js",     // hashed filenames for long-term caching
    clean: true,
  },
  resolve: { extensions: [".tsx", ".ts", ".js"], alias: { "@": __dirname + "/src" } },
  module: {
    rules: [                                  // LOADERS transform files
      { test: /\.[jt]sx?$/, exclude: /node_modules/, use: "swc-loader" },
      { test: /\.css$/, use: [MiniCssExtractPlugin.loader, "css-loader", "postcss-loader"] },
      { test: /\.(png|svg|jpg|woff2)$/, type: "asset" },
    ],
  },
  plugins: [                                  // PLUGINS act on the whole build
    new HtmlWebpackPlugin({ template: "./public/index.html" }),
    new MiniCssExtractPlugin({ filename: "[name].[contenthash].css" }),
  ],
  optimization: { splitChunks: { chunks: "all" }, runtimeChunk: "single" },
  devtool: argv.mode === "production" ? "hidden-source-map" : "eval-cheap-module-source-map",
  devServer: { hot: true, historyApiFallback: true, port: 3000 },
});
```

**Loader vs plugin**: a loader transforms individual files as they're imported (TS → JS, CSS → JS module); a plugin hooks into the whole build (generate HTML, extract CSS, define env vars, analyze bundle).

---

### 5. Tree Shaking (dead-code elimination)

Removes exports that are never imported. Works because **ES module imports/exports are static** (analyzable at build time).

```js
// utils.js
export const used = () => "used";
export const unused = () => "never imported";   // removed from the bundle

// app.js
import { used } from "./utils.js";
```

What breaks tree-shaking:
- **CommonJS** (`require`/`module.exports`) — dynamic, hard to analyze.
- Importing a whole namespace object and using it dynamically: `import * as _ from "lodash"; _[name]()`.
- **Side effects** at module top level (the bundler must keep the module in case the side effect matters).
- Barrel files (`index.js` re-exporting everything) — can pull in more than needed.

```js
// ❌ pulls in all of lodash (CommonJS build)
import _ from "lodash";
_.debounce(fn, 300);

// ✅ ESM build, tree-shakeable
import { debounce } from "lodash-es";
// ✅ or a direct path import
import debounce from "lodash/debounce";
```

```json
// package.json of a library — tells bundlers modules have no side effects (safe to drop if unused)
{ "sideEffects": false }
// or list files that DO have side effects:
{ "sideEffects": ["*.css", "./src/polyfills.js"] }
```

### 6. Code Splitting

Split the bundle into chunks loaded **on demand** so the first load only ships what the first screen needs.

```js
// Dynamic import → separate chunk
button.addEventListener("click", async () => {
  const { exportToPdf } = await import("./pdf-export.js"); // loaded only when clicked
  exportToPdf(data);
});
```

```jsx
// React route-based splitting
const Dashboard = lazy(() => import("./pages/Dashboard"));
const Settings = lazy(() => import("./pages/Settings"));
```

Types:
- **Entry splitting** — multiple entry points (e.g. app + admin).
- **Vendor splitting** — `node_modules` in a separate long-cached chunk.
- **Dynamic (lazy) splitting** — routes, modals, heavy libraries (charts, editors, maps, PDF).

Don't over-split: hundreds of tiny chunks add request overhead and waterfalls.

### 7. Minification

Shrinks code without changing behaviour: removes whitespace/comments, shortens variable names (mangling), removes dead code, simplifies expressions. Tools: **Terser** (classic), **esbuild**, **SWC** minifier; for CSS: **Lightning CSS**, cssnano.

```js
// before
function calculateTotal(items) {
  // sum all prices
  return items.reduce((total, item) => total + item.price, 0);
}
// after
function c(t){return t.reduce((e,r)=>e+r.price,0)}
```

Also: remove `console.log` in production builds (`esbuild.drop: ["console", "debugger"]` in Vite).

### 8. Content Hashing & Caching

Output files include a hash of their content: `app.3f9a1c.js`. Content changes → new hash → new URL → browsers fetch the new file. Unchanged files keep their hash → stay cached.

→ Serve hashed assets with `Cache-Control: public, max-age=31536000, immutable`, and `index.html` with `no-cache` (see Networking section).

### 9. Source Maps

A **source map** (`app.js.map`) maps minified/bundled code back to the original source, so stack traces and the debugger show your real files and line numbers.

| Setting | Use |
|---|---|
| `eval-cheap-module-source-map` / Vite dev default | Fast rebuilds in development |
| `source-map` | Full quality, file referenced publicly (anyone can see your original code) |
| `hidden-source-map` / Vite `sourcemap: "hidden"` | Generated but not referenced → **upload to Sentry**, don't serve publicly |
| none | Smallest output, but production errors are unreadable |

```js
//# sourceMappingURL=app.js.map    ← the comment that links a bundle to its map
```

### 10. HMR (Hot Module Replacement)

In development, when you save a file, only that module is swapped in the running app — **without a full reload**, keeping state (e.g. React component state with React Fast Refresh).

- Vite HMR is fast because it serves native ESM and only re-transforms the changed file.
- Fast Refresh keeps component state if the file only exports components; editing hooks order or non-component exports can force a remount/reload.

### 11. Asset handling

```js
import logoUrl from "./logo.svg";          // → "/assets/logo.8b2e.svg"
import styles from "./Button.module.css";  // → { primary: "Button_primary__x7a" } (scoped class names)
import data from "./data.json";            // parsed JSON
import workerUrl from "./worker.js?url";   // Vite query suffixes: ?url, ?raw, ?worker, ?inline
```

- Small assets can be **inlined** as base64 data URLs (fewer requests; bigger JS).
- `public/` folder files are copied as-is (not hashed) — use for `robots.txt`, `favicon.ico`.

### 12. CSS tooling

- **PostCSS** — plugin pipeline (Autoprefixer adds vendor prefixes based on browserslist; Tailwind v3 ran as a PostCSS plugin).
- **Lightning CSS** — Rust CSS parser/transformer/minifier (prefixing, nesting, minification) — used by Vite optionally and Tailwind v4.
- **Sass/Less** preprocessors; **CSS Modules** for scoping; **Tailwind** for utility classes.

### 13. Analyzing & budgeting bundles

```bash
npx vite-bundle-visualizer              # treemap of what's in your Vite bundle
npx source-map-explorer dist/assets/*.js
# webpack: webpack-bundle-analyzer
# check a package's cost before installing: bundlephobia.com / pkg-size.dev
```

Common wins: replace moment.js (→ date-fns/dayjs/Intl), lodash → lodash-es or native, import icons individually, lazy-load charts/editors/maps, drop unused polyfills, dedupe duplicate package versions (`npm dedupe`, `npm ls <pkg>`).

Set **performance budgets** (e.g. initial JS < 170KB gzipped) and fail CI when exceeded (`size-limit`, Lighthouse CI).

### 14. Monorepos & build orchestration

- **Workspaces**: npm/pnpm/yarn workspaces share dependencies and link local packages.
- **Turborepo** / **Nx**: run tasks across packages with caching (`turbo run build` rebuilds only what changed) and task pipelines.
- Share configs (`@company/eslint-config`, `@company/tsconfig`) and types (`@company/api-types`) across apps.

Hands-on walkthrough (pnpm workspaces, Turborepo caching, boundaries, deploying one app): `nodejs.md` → "Monorepos: pnpm Workspaces, Turborepo & Shared Packages".

### 15. Library publishing (ESM + CJS + types)

```json
{
  "name": "@me/utils",
  "type": "module",
  "exports": {
    ".": {
      "import": { "types": "./dist/index.d.ts", "default": "./dist/index.js" },
      "require": { "types": "./dist/index.d.cts", "default": "./dist/index.cjs" }
    }
  },
  "files": ["dist"],
  "sideEffects": false,
  "scripts": { "build": "tsup src/index.ts --format esm,cjs --dts" }
}
```

Each format needs its **own** type declarations. A single top-level `"types": "./dist/index.d.ts"` hands CommonJS users the ESM typings, which `attw` reports as "Masquerading as ESM". Full walkthrough with verification: `nodejs.md` → "Building & Publishing an npm Package".

---

### Best practices

- Use **Vite** for new SPAs (or a framework like Next.js that owns the build); don't hand-roll webpack configs without a reason.
- Keep the toolchain **fast**: SWC/esbuild for transforms, `tsc --noEmit` separately for type-checking.
- Define targets once with **browserslist**; avoid shipping polyfills modern users don't need.
- **Hash** asset filenames; long-cache them; `no-cache` the HTML.
- **Code-split** routes and heavy features; watch bundle size in CI.
- Prefer **ESM** dependencies and named imports for tree-shaking.
- **Hidden source maps** uploaded to your error tracker.
- Only `VITE_*`/`NEXT_PUBLIC_*` env vars reach the client — never put secrets there.
- Pin tool versions via the lockfile; upgrade regularly.

### Interview Qs

1. **What is a bundler and why do we need one?** → Dependency graph → optimized chunks; handles transforms, tree-shaking, minification, splitting, hashing, assets.
2. **Transpiler vs bundler vs minifier?**
3. **Transpiling vs polyfilling?** → Syntax at build time vs missing APIs at runtime.
4. **What is Babel? What is core-js?**
5. **Why is Vite faster than webpack in development?** → Serves native ESM on demand (no full bundle), esbuild pre-bundles dependencies, HMR only re-processes changed modules.
6. **What is tree shaking? Why does it need ES modules? What breaks it?**
7. **What is code splitting? How do you do it in React?** → `import()` / `React.lazy`.
8. **What are source maps? Should you ship them to production?** → Generate hidden maps and upload to error tracking.
9. **What is HMR?**
10. **What is content hashing and why does it matter for caching?**
11. **Webpack loader vs plugin?**
12. **How do you reduce bundle size?** (see "Analyzing & budgeting bundles" above)
13. **What is browserslist?**
14. **Does esbuild/SWC check TypeScript types?** → No — only `tsc` does.
15. **What does `"sideEffects": false` do?**

---

## 33. Error Handling

### try / catch / finally

```js
try {
  JSON.parse("{bad json");
} catch (err) {
  console.log(err.name);    // "SyntaxError"
  console.log(err.message);
} finally {
  console.log("always runs");
}
```

`finally` overrides `return`:

```js
function f() {
  try { return "try"; } finally { return "finally"; }
}
f(); // "finally"
```

### Built-in error types

`Error`, `SyntaxError`, `ReferenceError`, `TypeError`, `RangeError`, `URIError`, `EvalError`, `AggregateError`.

```js
undefinedVar;          // ReferenceError
null.x;                // TypeError
new Array(-1);         // RangeError
decodeURIComponent("%"); // URIError
```

### Custom errors

```js
class ValidationError extends Error {
  constructor(field, message) {
    super(message);
    this.name = "ValidationError";
    this.field = field;
  }
}

try {
  throw new ValidationError("email", "Invalid email");
} catch (e) {
  if (e instanceof ValidationError) console.log(e.field, e.message);
  else throw e; // rethrow unknown errors
}
```

### Error cause (ES2022)

```js
try {
  await db.connect();
} catch (err) {
  throw new Error("Could not start app", { cause: err });
}
```

### Async errors

```js
// try/catch does NOT catch errors thrown inside a setTimeout callback later
try {
  setTimeout(() => { throw new Error("late"); }, 0);
} catch (e) { /* never reached */ }

// global handlers
window.onerror = (msg, src, line, col, err) => {};
window.addEventListener("unhandledrejection", (e) => {});
```

**Interview Qs**
- Can `finally` change a return value? → Yes if it returns itself.
- Throw non-Error values? → Possible, but always throw `Error` objects for stack traces.

---

## 34. Debugging JavaScript

Debugging is a skill, not luck. Good debuggers follow a process and know their tools well enough that finding a bug takes minutes, not hours.

### 1. The debugging process

1. **Reproduce** reliably (exact steps, input, browser, user, environment). Can't reproduce → add logging/telemetry first.
2. **Read the error**: message, **stack trace** (top frame in *your* code), file & line. Most answers are right there.
3. **Isolate**: shrink the problem — which component/function/commit? Comment things out, use smaller input, `git bisect`.
4. **Hypothesize** one cause at a time, then **verify** with a breakpoint or log — don't guess-and-edit randomly.
5. **Fix the root cause**, not the symptom (a `?.` that hides an `undefined` is usually a symptom fix).
6. **Prevent**: add a regression test; add validation/types/logging so it can't silently happen again.

```bash
# Find the commit that introduced a bug (binary search over history)
git bisect start
git bisect bad                 # current commit is broken
git bisect good v2.3.0         # this old version worked
# git checks out a middle commit → test it → mark:
git bisect good   # or: git bisect bad
# …repeat until git prints the first bad commit
git bisect reset
```

### 2. Console — more than `console.log`

```js
console.log("user", user);                        // label your logs
console.log({ user, cart, total });               // shorthand: prints variable names too
console.table(users);                             // arrays of objects as a table
console.dir(document.body);                       // object view of a DOM node
console.group("checkout"); console.log("step 1"); console.groupEnd();
console.time("render"); render(); console.timeEnd("render");   // render: 12.3ms
console.count("fetchUser called");                // how many times was this hit?
console.assert(items.length > 0, "cart is empty", cart);        // logs only when false
console.trace("who called me?");                  // prints the call stack
console.warn("deprecated"); console.error(err);   // levels are filterable in DevTools
```

**Pitfall — live objects**: the console shows an object **as it is when you expand it**, not when it was logged. Log a snapshot when state changes quickly:

```js
console.log(JSON.parse(JSON.stringify(state)));   // or structuredClone(state)
```

Remove debug logs before committing (ESLint `no-console`), and use a real logger in production.

### 3. Breakpoints & stepping (DevTools → Sources)

```js
function applyCoupon(cart, coupon) {
  debugger;                                       // pauses here when DevTools is open
  return cart.total - coupon.value;
}
```

Better than editing code — click the line number in **Sources**:

| Breakpoint type | Use for |
|---|---|
| **Line** breakpoint | Pause at a line |
| **Conditional** breakpoint (right-click → *Add conditional breakpoint*) | Pause only when `user.id === 42` or `i > 1000` |
| **Logpoint** (right-click → *Add logpoint*) | `console.log` without editing/redeploying code |
| **DOM breakpoints** (Elements → right-click node → *Break on*) | Who modified/removed this element or attribute? |
| **Event listener breakpoints** | Pause on any `click`, `keydown`, `message`, timer… |
| **XHR/fetch breakpoints** | Pause when a request URL contains `/api/orders` |
| **Pause on exceptions** (caught / uncaught) | Stop exactly where an error is thrown |

While paused:
- **Step over** (F10) — next line; **Step into** (F11) — enter the function; **Step out** (Shift+F11); **Resume** (F8).
- **Scope** panel: local/closure/global variables (great for stale-closure bugs).
- **Call Stack**: how you got here (with **async stack traces** across `await`/timers).
- **Watch** expressions; hover variables; run code in the Console **in the paused scope**.
- Add third-party/framework scripts to the **Ignore List** so stepping skips library internals.

### 4. Console utilities (Chrome DevTools)

```js
$0                              // element currently selected in the Elements panel
$$("button.primary")           // querySelectorAll as an array
$_                              // result of the last evaluated expression
copy(apiResponse)               // copy any value to the clipboard (as JSON)
getEventListeners($0)           // listeners attached to the selected element
monitorEvents(window, "resize") // log events as they fire (unmonitorEvents to stop)
queryObjects(Promise)           // all live objects created by a constructor (leak hunting)
```

**Snippets** (Sources → Snippets) save reusable scripts; **Local Overrides** let you edit a production file/response locally to test a fix.

### 5. Network panel

- Check **status**, **request headers/payload**, **response/preview**, and **timing** (DNS, connect, TTFB, download).
- Filter by `Fetch/XHR`; enable **Preserve log** across navigations/redirects; **Disable cache** while debugging.
- **Throttle** to Slow 4G / offline to reproduce loading & race-condition bugs.
- Right-click → **Copy as fetch / cURL** to replay a request in the console or terminal; **Block request URL** to test failure handling.
- CORS errors: the preflight `OPTIONS` request and response headers tell you what the server is missing.

### 6. Application, Performance & Memory panels

- **Application**: localStorage/sessionStorage/IndexedDB, cookies (flags, expiry), service workers (update/unregister), cache storage.
- **Performance**: record an interaction → flame chart; red corners = **long tasks**; purple "Layout" blocks with "Forced reflow" warnings = layout thrashing; check what JS ran on the main thread. (See Browser Internals → rendering pipeline.)
- **Lighthouse**: Core Web Vitals and actionable audits.
- **Memory**: find leaks by comparing heap snapshots.

**Memory-leak workflow**
1. Open Memory → take **heap snapshot 1**.
2. Do the suspect action several times (open/close a modal, navigate away and back).
3. Force GC (trash-can icon) → take **snapshot 2** → view **Comparison**.
4. Look for growing counts of your objects, **Detached** DOM nodes, arrays/maps that keep growing.
5. Follow the **Retainers** path to see what still references them (a listener, a timer, a cache, a closure).

### 7. Debugging async code & race conditions

- Turn on **async stack traces** (on by default in Chrome) to see which `await`/`setTimeout` led here.
- Add **timestamps and request IDs** to logs to see interleaving: `console.log(performance.now().toFixed(1), "search", q, requestId)`.
- Throttle the network to make races reproducible (slow first request, fast second one).
- Watch for **unhandled rejections** (`window.addEventListener("unhandledrejection", …)`).
- Common async bugs: missing `await`, `forEach` with async callbacks, stale responses overwriting newer ones, state updated after unmount, promises never resolving (forgot to call `resolve`).

### 8. Framework devtools

- **React DevTools**: component tree, props/state/hooks inspection, "Highlight updates", **Profiler** (why did this render?).
- **Redux DevTools**: action log, state diff, time-travel.
- **TanStack Query Devtools**: cache state, stale/fetching status, refetch manually.
- Vue/Angular have equivalents.

### 9. Source maps

Minified production code is unreadable; **source maps** map it back to your original files and line numbers.

- Dev servers (Vite, Next) provide them automatically.
- Production: generate **hidden** source maps and upload them to your error tracker (Sentry) instead of serving them publicly (see Build Tooling).
- If breakpoints land on the wrong lines → stale or missing source maps; rebuild/clear cache.

### 10. Debugging Node.js

```bash
node --inspect src/server.js          # attach a debugger on port 9229
node --inspect-brk src/script.js      # pause on the first line (debug startup code)
# Chrome → chrome://inspect → "Open dedicated DevTools for Node"

NODE_DEBUG=http,net node app.js       # verbose core-module logs
DEBUG=express:* node app.js           # libraries using the `debug` package
node --trace-warnings app.js          # stack traces for warnings (e.g. MaxListenersExceeded)
node --heapsnapshot-signal=SIGUSR2 app.js   # take heap snapshots from a running process
```

**VS Code** (`.vscode/launch.json`) — the most comfortable way to debug:

```jsonc
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug API server",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/src/server.js",
      "envFile": "${workspaceFolder}/.env",
      "skipFiles": ["<node_internals>/**"]
    },
    {
      "name": "Attach to running process",
      "type": "node",
      "request": "attach",
      "port": 9229
    },
    {
      "name": "Debug frontend in Chrome",
      "type": "chrome",
      "request": "launch",
      "url": "http://localhost:5173",
      "webRoot": "${workspaceFolder}/src"
    }
  ]
}
```

Debugging tests: `vitest --inspect-brk --no-file-parallelism` (then attach), or use the VS Code Vitest/Jest extensions' "Debug test" button.

### 11. Debugging production issues

- You can't attach a debugger to users' browsers — rely on **error tracking** (Sentry: stack trace + source maps + breadcrumbs + release + user), **structured logs** with **request/correlation IDs**, and **session replay** where privacy allows.
- Reproduce with the **same version** (release tag), feature flags and data shape; never debug on production data without permission/anonymization.
- Use **feature flags** to turn a broken feature off while you investigate.
- Compare "what changed?": deploys, config/env vars, dependency updates, traffic patterns, third-party APIs.
- Write the **post-mortem**: root cause, impact, fix, and what prevents it next time (blameless).

### 12. Common bug checklist

| Symptom | Usual suspects |
|---|---|
| `Cannot read properties of undefined` | Data not loaded yet, wrong API shape, typo in property, missing `await` |
| Value is stale | Stale closure, missing effect dependency, cache not invalidated, mutation without re-render |
| Works sometimes | Race condition, timing, order of async responses, uninitialized state |
| Works locally, fails in prod | Env vars, build differences, CORS, HTTPS/cookies, minification, time zone, caching/CDN |
| `this` is undefined | Method passed as a callback without binding |
| Wrong number / comparison | Floating point, string vs number (`"10" > "9"`), `==` coercion, `parseInt` without radix |
| Off by one | `<` vs `<=`, 0-based months in `Date`, `slice` end exclusive |
| Infinite loop / re-render | Effect updating its own dependency, recursion without a base case |
| Memory grows | Listeners/intervals not cleaned up, unbounded caches, detached DOM |

### Interview Qs

1. Walk me through how you debug a bug you can't immediately explain.
2. Conditional breakpoint vs logpoint vs `debugger`?
3. How do you find which code modified a DOM element? (DOM breakpoints)
4. How do you debug a memory leak in a web app?
5. How do you debug a race condition between two API requests?
6. How do you debug a Node.js server? (`--inspect`, VS Code)
7. What are source maps and how do you debug minified production errors?
8. What is `git bisect`?
9. Why can `console.log` of an object show values that weren't there when it was logged?

---

## 35. DOM & Events

### DOM

The **Document Object Model** is a tree representation of the HTML that JS can read & modify.

```js
const el = document.getElementById("app");
const first = document.querySelector(".item");       // first match
const all = document.querySelectorAll(".item");      // static NodeList
const live = document.getElementsByClassName("item"); // live HTMLCollection

const div = document.createElement("div");
div.textContent = "Hello";          // safe (no HTML parsing)
div.innerHTML = "<b>Hi</b>";         // parses HTML — XSS risk with user input
div.classList.add("active");
div.classList.toggle("open");
div.setAttribute("data-id", "5");
div.dataset.id;                      // "5"
div.style.color = "red";
el.append(div);
div.remove();
```

### Reflow vs Repaint

- **Reflow (layout)**: recalculating positions/sizes (changing width, adding elements, reading `offsetHeight` after a write). Expensive.
- **Repaint**: redraw pixels without layout change (color, visibility).
- Minimise with batching, `DocumentFragment`, CSS transforms, avoiding layout thrashing (read-write-read-write).

```js
const frag = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
  const li = document.createElement("li");
  li.textContent = i;
  frag.appendChild(li);
}
list.appendChild(frag); // one reflow instead of 1000
```

### Event propagation — 3 phases

1. **Capturing** — from `window` down to the target.
2. **Target** — at the element.
3. **Bubbling** — from target back up to `window`.

By default listeners run in the **bubbling** phase. Pass `{ capture: true }` (or `true`) for capturing.

```html
<div id="grandparent">
  <div id="parent">
    <button id="child">Click</button>
  </div>
</div>
```

```js
["grandparent", "parent", "child"].forEach((id) => {
  document.getElementById(id).addEventListener("click", () => console.log("bubble", id));
  document.getElementById(id).addEventListener("click", () => console.log("capture", id), true);
});
// Clicking the button:
// capture grandparent, capture parent, capture child, bubble child, bubble parent, bubble grandparent
```

### stopPropagation vs preventDefault vs stopImmediatePropagation

- `e.stopPropagation()` — stops the event going further up/down the tree.
- `e.stopImmediatePropagation()` — also stops other listeners on the **same** element.
- `e.preventDefault()` — cancels the browser default action (form submit, link navigation, checkbox toggle). Doesn't stop propagation.

```js
form.addEventListener("submit", (e) => {
  e.preventDefault(); // no page reload
});
```

### Event Delegation

Attach **one** listener on a parent instead of many on children; use `e.target` to find what was clicked. Works for dynamically added children, uses less memory.

```js
document.getElementById("todo-list").addEventListener("click", (e) => {
  const item = e.target.closest("li");
  if (!item) return;
  if (e.target.matches(".delete")) item.remove();
  else item.classList.toggle("done");
});
```

### `e.target` vs `e.currentTarget`

- `target` — element that was actually clicked (deepest).
- `currentTarget` — element the listener is attached to.

### Listener options

```js
el.addEventListener("scroll", handler, { passive: true }); // won't call preventDefault -> smoother scroll
el.addEventListener("click", handler, { once: true });     // auto-removed after first call
const controller = new AbortController();
el.addEventListener("click", handler, { signal: controller.signal });
controller.abort(); // removes the listener
el.removeEventListener("click", handler); // must be the same function reference
```

### Custom events

```js
const evt = new CustomEvent("user:login", { detail: { id: 1 }, bubbles: true });
document.addEventListener("user:login", (e) => console.log(e.detail.id));
document.dispatchEvent(evt);
```

### DOMContentLoaded vs load

- `DOMContentLoaded` — HTML parsed, DOM ready (images may still load).
- `load` — everything including images, CSS, iframes loaded.

### script: async vs defer

| | Download | Execution | Order |
|---|---|---|---|
| normal `<script>` | blocks parsing | immediately | in order |
| `async` | parallel | as soon as downloaded (blocks parsing then) | not guaranteed |
| `defer` | parallel | after HTML parsed, before DOMContentLoaded | in order |
| `type="module"` | deferred by default | | |

**Interview Qs**
- Event bubbling vs capturing? (above)
- What is event delegation and why? (above)
- Which events don't bubble? → `focus`, `blur` (use `focusin/focusout`), `mouseenter/mouseleave`, `load`, `scroll` on elements.

---

## 36. Browser Storage & Cookies

| | localStorage | sessionStorage | Cookies | IndexedDB |
|---|---|---|---|---|
| Capacity | ~5–10MB | ~5MB | ~4KB each | Large (hundreds of MB+) |
| Expiry | Never (until cleared) | Tab close | Set via `Expires/Max-Age` | Never |
| Sent to server | No | No | **Yes, every request** | No |
| Scope | Origin | Origin + tab | Domain/path | Origin |
| API | Sync, strings only | Sync, strings only | `document.cookie` string | Async, structured data |

```js
localStorage.setItem("user", JSON.stringify({ id: 1 }));
const user = JSON.parse(localStorage.getItem("user"));
localStorage.removeItem("user");
localStorage.clear();

sessionStorage.setItem("step", "2");

// listen to changes from other tabs
window.addEventListener("storage", (e) => console.log(e.key, e.newValue));
```

### Cookies

```js
document.cookie = "theme=dark; max-age=86400; path=/; SameSite=Lax; Secure";
document.cookie; // "theme=dark; other=1"
```

Cookie flags:
- `HttpOnly` — JS can't read it (protects from XSS stealing). Set by server only.
- `Secure` — only sent over HTTPS.
- `SameSite=Strict|Lax|None` — CSRF protection.
- `Domain`, `Path`, `Expires`, `Max-Age`.

**Where to store auth tokens?** → Prefer an `HttpOnly; Secure; SameSite` cookie. localStorage is readable by any JS (XSS risk).

---

## 37. Memory Management & Garbage Collection

JS allocates memory automatically and frees it through **garbage collection**.

### Mark-and-sweep

The GC starts from **roots** (global object, current call stack), marks everything reachable, then sweeps (frees) the unreachable. V8 uses a **generational** GC: young generation (Scavenger, frequent) and old generation (Mark-Sweep-Compact, less often).

```js
let user = { name: "A" };
user = null; // object now unreachable -> collectible
```

```js
// Circular references are fine with mark-and-sweep
function make() {
  const a = {}, b = {};
  a.b = b; b.a = a;
}
make(); // both are unreachable after return -> collected
```

### Common memory leaks

1. Accidental globals (`x = 10` without declaration in sloppy mode).
2. Forgotten timers (`setInterval` never cleared).
3. Event listeners not removed.
4. Detached DOM nodes still referenced in JS.
5. Closures holding large data.
6. Unbounded caches (use `WeakMap` / LRU).

```js
// Leak
const cache = {};
function process(el) { cache[el.id] = el; } // DOM nodes never freed

// Fix
const cache2 = new WeakMap();
function process2(el) { cache2.set(el, computeStuff(el)); }
```

```js
// Leak: interval keeps closure alive
const id = setInterval(() => updateWidget(bigData), 1000);
// Fix
clearInterval(id);
```

Debug with Chrome DevTools → Memory tab → heap snapshots, allocation timeline.

---

## 38. Strict Mode

`"use strict";` at the top of a file/function opts into a stricter JS. ES modules and classes are strict automatically.

What changes:
- Assigning to undeclared variables throws `ReferenceError`.
- `this` in plain functions is `undefined` (not `window`).
- Writing to read-only / frozen properties throws.
- Duplicate parameter names are a SyntaxError.
- `with` is not allowed; `delete` on plain variables not allowed.
- Octal literals like `010` not allowed.
- `eval` doesn't leak variables into the surrounding scope.

```js
"use strict";
x = 10; // ReferenceError: x is not defined

function f() { return this; }
f(); // undefined

const o = Object.freeze({ a: 1 });
o.a = 2; // TypeError
```

---

## 39. Proxy & Reflect

A **Proxy** wraps an object and intercepts operations (get, set, has, deleteProperty, apply, construct…) through **traps**. **Reflect** provides the default behaviour for each trap.

### Example 1 — Validation

```js
const user = new Proxy({}, {
  set(target, key, value) {
    if (key === "age" && (!Number.isInteger(value) || value < 0)) {
      throw new TypeError("Age must be a positive integer");
    }
    return Reflect.set(target, key, value);
  },
});
user.age = 25;   // ok
user.age = -1;   // TypeError
```

### Example 2 — Default values / negative array index

```js
const withDefault = new Proxy({}, {
  get: (t, k) => (k in t ? t[k] : "N/A"),
});
withDefault.name; // "N/A"

const arr = new Proxy([1, 2, 3], {
  get(t, k, r) {
    const i = Number(k);
    return Number.isInteger(i) && i < 0 ? t[t.length + i] : Reflect.get(t, k, r);
  },
});
arr[-1]; // 3
```

### Example 3 — Reactivity (how Vue 3 works)

```js
function reactive(obj, onChange) {
  return new Proxy(obj, {
    set(t, k, v) {
      const ok = Reflect.set(t, k, v);
      onChange(k, v);
      return ok;
    },
  });
}
const state = reactive({ count: 0 }, (k, v) => console.log(`${k} -> ${v}`));
state.count++; // "count -> 1"
```

---

## 40. Getters, Setters, Property Descriptors

Every property has a **descriptor**:
- Data descriptor: `value`, `writable`, `enumerable`, `configurable`.
- Accessor descriptor: `get`, `set`, `enumerable`, `configurable`.

```js
const obj = {};
Object.defineProperty(obj, "id", {
  value: 1,
  writable: false,     // can't change
  enumerable: false,   // hidden from keys/for...in/JSON
  configurable: false, // can't delete or redefine
});
obj.id = 2;          // ignored (TypeError in strict)
Object.keys(obj);    // []
Object.getOwnPropertyDescriptor(obj, "id");
```

`defineProperty` defaults are all `false`; normal assignment defaults are all `true`.

```js
const account = {
  _balance: 0,
  get balance() { return `₹${this._balance}`; },
  set balance(v) {
    if (v < 0) throw new Error("negative");
    this._balance = v;
  },
};
account.balance = 500;
account.balance; // "₹500"
```

```js
// Computed property via defineProperty
const person = { first: "Rohit", last: "Dahiya" };
Object.defineProperty(person, "full", {
  get() { return `${this.first} ${this.last}`; },
  enumerable: true,
});
```

---

## 41. Design Patterns

### Module pattern

```js
const Cart = (() => {
  const items = []; // private
  return {
    add: (item) => items.push(item),
    total: () => items.reduce((s, i) => s + i.price, 0),
  };
})();
```

### Singleton

```js
class Database {
  static #instance;
  constructor() {
    if (Database.#instance) return Database.#instance;
    Database.#instance = this;
  }
}
new Database() === new Database(); // true
// ES modules are singletons by nature: `export const db = new Database()`
```

### Factory

```js
function createUser(type, name) {
  const roles = {
    admin: { permissions: ["read", "write", "delete"] },
    guest: { permissions: ["read"] },
  };
  return { name, type, ...roles[type] };
}
```

### Observer / Pub-Sub (Event Emitter) — very common interview

```js
class EventEmitter {
  #events = new Map();

  on(event, listener) {
    if (!this.#events.has(event)) this.#events.set(event, []);
    this.#events.get(event).push(listener);
    return () => this.off(event, listener); // unsubscribe fn
  }
  off(event, listener) {
    const list = this.#events.get(event);
    if (list) this.#events.set(event, list.filter((l) => l !== listener && l.original !== listener));
  }
  once(event, listener) {
    const wrapper = (...args) => {
      this.off(event, wrapper);
      listener(...args);
    };
    wrapper.original = listener;
    this.on(event, wrapper);
  }
  emit(event, ...args) {
    (this.#events.get(event) || []).slice().forEach((l) => l(...args));
    return this.#events.has(event);
  }
}

const bus = new EventEmitter();
const unsub = bus.on("msg", (m) => console.log("got", m));
bus.once("msg", () => console.log("only once"));
bus.emit("msg", "hi"); // got hi, only once
bus.emit("msg", "yo"); // got yo
unsub();
```

### Other patterns worth knowing

- **Decorator** — wrap a function/object to add behaviour (`withLogging`, `memoize`).
- **Strategy** — pick an algorithm at runtime from a map of functions.
- **Mediator**, **Command**, **Prototype**, **Facade**, **Adapter**.

```js
// Strategy
const discounts = {
  none: (p) => p,
  festive: (p) => p * 0.8,
  vip: (p) => p * 0.7,
};
const finalPrice = (price, type) => discounts[type](price);
```

---

## 42. Web APIs

### fetch

```js
const res = await fetch("/api/users", {
  method: "POST",
  headers: { "Content-Type": "application/json", Authorization: `Bearer ${token}` },
  body: JSON.stringify({ name: "Rohit" }),
  credentials: "include", // send cookies cross-origin
});
if (!res.ok) throw new Error(res.statusText); // fetch only rejects on network errors
const data = await res.json();
```

### AbortController — cancel requests

```js
const controller = new AbortController();
fetch("/api/search?q=a", { signal: controller.signal })
  .then((r) => r.json())
  .catch((e) => { if (e.name === "AbortError") console.log("cancelled"); });
controller.abort();

// Timeout shortcut
fetch("/api", { signal: AbortSignal.timeout(5000) });
```

### Web Workers

Run JS on a background thread; no DOM access; communicate via `postMessage`.

```js
// main.js
const worker = new Worker("worker.js");
worker.postMessage(1e9);
worker.onmessage = (e) => console.log("sum:", e.data);

// worker.js
onmessage = (e) => {
  let sum = 0;
  for (let i = 0; i < e.data; i++) sum += i;
  postMessage(sum);
};
```

Service Workers: proxy between app and network — offline caching, push notifications, PWAs.

### requestAnimationFrame

Runs a callback before the next repaint (~60fps). Paused in background tabs.

```js
function animate(t) {
  box.style.transform = `translateX(${(t / 10) % 300}px)`;
  requestAnimationFrame(animate);
}
requestAnimationFrame(animate);
```

### Observers

```js
// IntersectionObserver — lazy load / infinite scroll
const io = new IntersectionObserver((entries) => {
  entries.forEach((e) => {
    if (e.isIntersecting) {
      e.target.src = e.target.dataset.src;
      io.unobserve(e.target);
    }
  });
}, { rootMargin: "200px" });
document.querySelectorAll("img[data-src]").forEach((img) => io.observe(img));

// ResizeObserver
new ResizeObserver(([entry]) => console.log(entry.contentRect.width)).observe(panel);

// MutationObserver — watch DOM changes
new MutationObserver((mutations) => console.log(mutations)).observe(root, { childList: true, subtree: true });
```

### Other useful APIs

`navigator.clipboard.writeText()`, `navigator.geolocation`, `Notification`, `history.pushState` (SPA routing), `URL` & `URLSearchParams`, `BroadcastChannel`, `WebSocket`, `EventSource` (SSE), `crypto.randomUUID()`.

```js
const url = new URL("https://x.com/search?q=js&page=2");
url.searchParams.get("q");     // "js"
url.searchParams.set("page", 3);
url.toString();
```

---

## 43. Binary Data & Files in the Browser

Uploads, previews, CSV/PDF exports, image compression, hashing, downloads with progress — all of these need JavaScript's binary data APIs.

### 1. The building blocks

| Type | What it is |
|---|---|
| `ArrayBuffer` | A fixed-size chunk of raw bytes (no way to read it directly) |
| Typed arrays (`Uint8Array`, `Int16Array`, `Float32Array`…) | Views that read/write the buffer as numbers of one type |
| `DataView` | Read/write mixed types at any offset, with explicit endianness |
| `Blob` | Immutable binary data + MIME type (can live on disk, not only in memory) |
| `File` | A `Blob` with `name` and `lastModified` (from `<input type="file">`, drag & drop, paste) |
| `ReadableStream` | Data arriving in chunks (fetch bodies, `blob.stream()`) |

```js
const buffer = new ArrayBuffer(8);                 // 8 zeroed bytes
const bytes = new Uint8Array(buffer);
bytes[0] = 255;
bytes[1] = 256;                                    // wraps around → 0 (Uint8 is 0–255)
new Uint8ClampedArray([300, -5]);                  // [255, 0] — clamps instead (used for canvas pixels)

// DataView: explicit byte order (network protocols, file formats)
const view = new DataView(new ArrayBuffer(4));
view.setUint32(0, 0x12345678);                     // big-endian by default
[...new Uint8Array(view.buffer)];                  // [0x12, 0x34, 0x56, 0x78]
view.setUint32(0, 0x12345678, true);               // little-endian
[...new Uint8Array(view.buffer)];                  // [0x78, 0x56, 0x34, 0x12]
```

### 2. Text ↔ bytes, base64 & hex

```js
const encoder = new TextEncoder();                 // always UTF-8
const utf8 = encoder.encode("₹ Hi 👋");             // Uint8Array — "₹" is 3 bytes, "👋" is 4
new TextDecoder().decode(utf8);                    // "₹ Hi 👋"
"₹ Hi 👋".length;                                   // 7 (UTF-16 code units) vs utf8.length === 11 bytes

// btoa/atob only handle Latin-1 → go through bytes for Unicode-safe base64
export function toBase64(bytes) {
  let binary = "";
  for (let i = 0; i < bytes.length; i += 0x8000) {                 // chunk to avoid call-stack limits
    binary += String.fromCharCode(...bytes.subarray(i, i + 0x8000));
  }
  return btoa(binary);
}
export function fromBase64(b64) {
  return Uint8Array.from(atob(b64), (ch) => ch.charCodeAt(0));
}
export const toHex = (bytes) => [...bytes].map((b) => b.toString(16).padStart(2, "0")).join("");

try { btoa("₹"); } catch (e) { console.log(e.name); }  // ❌ "InvalidCharacterError" — btoa only handles Latin-1
toBase64(encoder.encode("₹"));                      // ✅ "4oK5"
// Newer runtimes also have Uint8Array.fromBase64 / bytes.toBase64() / toHex() built in — check support first.
```

### 3. Blob & File

```js
const blob = new Blob(['{"hello":"world"}'], { type: "application/json" });
blob.size;                                          // 17 (bytes)
blob.type;                                          // "application/json"
await blob.text();                                  // '{"hello":"world"}'
await blob.arrayBuffer();                           // ArrayBuffer
blob.slice(0, 8);                                   // new Blob with the first 8 bytes (no copy until read)
blob.stream();                                      // ReadableStream of chunks

const file = new File(["name,email\nRohit,r@x.com\n"], "users.csv", { type: "text/csv" });
file.name; file.size; file.lastModified;
```

Getting files from the user:

```js
// <input type="file" accept="image/*,.pdf" multiple>
input.addEventListener("change", () => {
  for (const file of input.files) console.log(file.name, file.type, file.size);
});

// Drag & drop
dropzone.addEventListener("dragover", (e) => e.preventDefault());           // required to allow dropping
dropzone.addEventListener("drop", (e) => {
  e.preventDefault();
  const files = [...e.dataTransfer.files];
});

// Paste (e.g. screenshots)
document.addEventListener("paste", (e) => {
  const images = [...e.clipboardData.files].filter((f) => f.type.startsWith("image/"));
});
```

### 4. Reading files

```js
// Modern: promise-based Blob methods
const text = await file.text();
const buffer = await file.arrayBuffer();

// Legacy: FileReader (events) — still seen in older code and for readAsDataURL
const reader = new FileReader();
reader.onload = () => console.log(reader.result);      // string / ArrayBuffer / data URL
reader.onerror = () => console.error(reader.error);
reader.readAsText(file);                               // readAsArrayBuffer / readAsDataURL
```

**Large files**: don't `await file.text()` a 2 GB file — stream it:

```js
export async function countLines(blob) {
  const reader = blob.stream().pipeThrough(new TextDecoderStream()).getReader();
  let lines = 0, last = "";
  for (;;) {
    const { value, done } = await reader.read();
    if (done) break;
    lines += value.split("\n").length - 1;
    last = value.at(-1) ?? last;
  }
  return blob.size > 0 && last !== "\n" ? lines + 1 : lines;       // count a final line without "\n"
}
```

### 5. Hashing a file (dedupe, integrity checks)

```js
export async function sha256Hex(blob) {
  const digest = await crypto.subtle.digest("SHA-256", await blob.arrayBuffer());
  return [...new Uint8Array(digest)].map((b) => b.toString(16).padStart(2, "0")).join("");
}
await sha256Hex(new Blob(["hello"]));   // "2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824"
```

(`crypto.subtle` needs a secure context — HTTPS or localhost.)

### 6. Checking what a file really is (magic bytes)

`file.type` comes from the file **extension** — anyone can rename `virus.exe` to `photo.jpg`. Check the first bytes ("magic numbers"), and always re-validate on the server.

```js
const SIGNATURES = [
  { type: "image/png", bytes: [0x89, 0x50, 0x4e, 0x47, 0x0d, 0x0a, 0x1a, 0x0a] },
  { type: "image/jpeg", bytes: [0xff, 0xd8, 0xff] },
  { type: "image/gif", bytes: [0x47, 0x49, 0x46, 0x38] },            // "GIF8"
  { type: "application/pdf", bytes: [0x25, 0x50, 0x44, 0x46, 0x2d] }, // "%PDF-"
  { type: "application/zip", bytes: [0x50, 0x4b, 0x03, 0x04] },       // also .docx/.xlsx
];

export async function sniffType(blob) {
  const head = new Uint8Array(await blob.slice(0, 16).arrayBuffer());
  const webp = head.length >= 12 && String.fromCharCode(...head.slice(0, 4)) === "RIFF" && String.fromCharCode(...head.slice(8, 12)) === "WEBP";
  if (webp) return "image/webp";
  return SIGNATURES.find((s) => s.bytes.every((b, i) => head[i] === b))?.type ?? null;
}
```

### 7. Previews: object URLs vs data URLs

```js
const url = URL.createObjectURL(file);        // "blob:https://app.com/uuid" — instant, no copying
img.src = url;
img.onload = () => URL.revokeObjectURL(url);  // free the memory when done (React: revoke in effect cleanup)
```

| Object URL (`blob:`) | Data URL (`data:image/png;base64,…`) |
|---|---|
| Points at the Blob in memory — fast, any size | Whole file inlined as base64 text (~33% bigger) |
| Must be revoked | Freed with the string |
| Valid only in this document | Can be stored/sent as text |

### 8. Generating downloads (CSV, JSON, files from APIs)

```js
export function toCsv(rows, columns) {
  const escape = (value) => {
    const s = value == null ? "" : String(value);
    return /[",\n\r]/.test(s) ? `"${s.replace(/"/g, '""')}"` : s;   // quote fields with commas/quotes/newlines
  };
  const lines = [columns.map((c) => escape(c.label)), ...rows.map((r) => columns.map((c) => escape(r[c.key])))];
  return lines.map((l) => l.join(",")).join("\r\n");
}

export function downloadBlob(blob, filename) {
  const url = URL.createObjectURL(blob);
  const a = Object.assign(document.createElement("a"), { href: url, download: filename });
  document.body.append(a);
  a.click();
  a.remove();
  setTimeout(() => URL.revokeObjectURL(url), 0);
}

const csv = toCsv(orders, [{ key: "id", label: "Order ID" }, { key: "customer", label: "Customer" }, { key: "total", label: "Total (₹)" }]);
downloadBlob(new Blob(["\uFEFF" + csv], { type: "text/csv;charset=utf-8" }), "orders.csv");   // BOM → Excel reads UTF-8 (₹, names) correctly
```

**CSV injection**: values starting with `=`, `+`, `-`, `@` can run as formulas when opened in Excel. For user-generated content, prefix such cells with `'`.

Downloading a protected file from your API:

```js
const res = await fetch(`/api/invoices/${id}/pdf`, { headers: { Authorization: `Bearer ${token}` } });
if (!res.ok) throw new Error(`Download failed (${res.status})`);
downloadBlob(await res.blob(), `invoice-${id}.pdf`);
// Large files: prefer a server-side Content-Disposition response or a short-lived pre-signed URL (no blob in memory)
```

### 9. Streams: download progress & compression

```js
export async function fetchWithProgress(url, onProgress) {
  const res = await fetch(url);
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  const total = Number(res.headers.get("Content-Length")) || 0;      // 0 if unknown (e.g. compressed)
  const reader = res.body.getReader();
  const chunks = [];
  let received = 0;
  for (;;) {
    const { value, done } = await reader.read();
    if (done) break;
    chunks.push(value);
    received += value.length;
    onProgress?.({ received, total, percent: total ? Math.round((received / total) * 100) : null });
  }
  return new Blob(chunks);
}
```

```js
// Built-in gzip/deflate (no library): compress a file before upload, or decompress a .gz download
export async function gzip(blob) {
  return new Response(blob.stream().pipeThrough(new CompressionStream("gzip"))).blob();
}
export async function gunzip(blob) {
  return new Response(blob.stream().pipeThrough(new DecompressionStream("gzip"))).blob();
}
```

(Upload progress needs `XMLHttpRequest`'s `upload.onprogress` — see React notes: Real-time & Rich Interactions.)

### 10. Images: resize & compress before upload

Phone photos are 4–12 MB; resizing in the browser saves bandwidth and upload time.

```js
export async function resizeImage(file, { maxWidth = 1600, quality = 0.8, type = "image/webp" } = {}) {
  const bitmap = await createImageBitmap(file);                  // decodes (respects EXIF orientation in modern browsers)
  const scale = Math.min(1, maxWidth / bitmap.width);
  const canvas = new OffscreenCanvas(Math.round(bitmap.width * scale), Math.round(bitmap.height * scale));
  canvas.getContext("2d").drawImage(bitmap, 0, 0, canvas.width, canvas.height);
  bitmap.close();
  return canvas.convertToBlob({ type, quality });                // e.g. 8 MB JPEG → ~300 KB WebP
}
```

Also: re-encoding strips most metadata (including GPS location in EXIF) — good for privacy.

### 11. Heavy binary work off the main thread

Parsing, hashing or compressing large files blocks the UI — move it to a **Web Worker**. `ArrayBuffer`s can be **transferred** (zero-copy) instead of cloned:

```js
const buffer = await file.arrayBuffer();
worker.postMessage({ buffer }, [buffer]);   // ownership moves to the worker; buffer.byteLength is now 0 here
```

### 12. Saving files directly (File System Access API)

Chromium-only for now: `showSaveFilePicker()` / `showOpenFilePicker()` let editors open and save files in place. Always feature-detect and fall back to `downloadBlob`. The **Origin Private File System** (`navigator.storage.getDirectory()`) gives fast private storage for large app data.

### Security checklist

- Never trust `file.type` or the extension — sniff magic bytes and **validate again on the server**.
- Enforce size limits before reading or uploading.
- **SVG can contain scripts** — don't render user-uploaded SVGs inline; sanitize or serve from a separate domain with `Content-Disposition: attachment`.
- Don't open user-uploaded HTML in your origin.
- Revoke object URLs; don't keep huge blobs in memory.
- Escape CSV cells (quotes) and neutralize formula injection.

### Interview Qs

1. ArrayBuffer vs typed array vs DataView vs Blob?
2. Why doesn't `btoa("₹")` work? How do you base64-encode Unicode?
3. Why is `"👋".length === 2` but it takes 4 bytes in UTF-8?
4. Object URL vs data URL — when would you use each? Why revoke?
5. How do you generate and download a CSV entirely in the browser? Why add a BOM?
6. How do you read a very large file without freezing the page?
7. How do you verify a file's real type?
8. How do you show download progress with `fetch`?
9. How would you compress an image before uploading it?
10. What are transferable objects?

---

## 44. Browser Internals: Rendering Pipeline, Web Components & Service Workers (PWA)

### Part 1 — The rendering pipeline in depth

After the first page load (see Networking section), the browser keeps re-rendering as JS and CSS change things. Every visual update goes through the **pixel pipeline**:

```
JavaScript → Style → Layout → Paint → Composite
(change DOM/   (which CSS   (sizes &    (fill pixels  (combine layers
 styles)        rules apply)  positions)  into layers)   on the GPU)
```

At **60 fps** each frame has **~16.6 ms** (8 ms at 120 Hz) — and the browser needs some of that itself, so your JS gets ~10 ms. Miss it → **jank** (dropped frames).

### Which CSS changes trigger what

| You change… | Layout (reflow) | Paint | Composite | Cost |
|---|---|---|---|---|
| `width`, `height`, `top/left`, `margin`, `padding`, `font-size`, `display`, adding/removing elements, text changes | ✅ | ✅ | ✅ | 🔴 Highest |
| `color`, `background`, `box-shadow`, `border-radius`, `visibility`, `outline` | ❌ | ✅ | ✅ | 🟠 Medium |
| `transform`, `opacity` (on a composited layer), `filter` (often) | ❌ | ❌ | ✅ | 🟢 Cheapest |

**Rule for smooth animations: animate only `transform` and `opacity`.**

```css
/* ❌ animates layout every frame */
.panel { transition: left 300ms; }
.panel.open { left: 0; }

/* ✅ GPU-composited, no layout/paint */
.panel { transition: transform 300ms; transform: translateX(-100%); }
.panel.open { transform: translateX(0); }
```

### Layers & compositing

The browser can put elements on their own **compositor layers** (GPU textures). Moving a layer with `transform` just re-composites — no layout or paint.

```css
.drawer { will-change: transform; }   /* hint: promote to its own layer before animating */
```

Don't sprinkle `will-change` everywhere — every layer costs GPU memory. Add it just before an animation, remove it after, or only on elements that animate constantly.

### Layout thrashing (forced synchronous layout)

Reading a layout property (`offsetHeight`, `getBoundingClientRect()`, `scrollTop`, `clientWidth`, `getComputedStyle`) **after** writing styles forces the browser to calculate layout **immediately**. Doing read/write/read/write in a loop recalculates layout on every iteration.

```js
// ❌ Thrashing: write → read → write → read… (N forced layouts)
for (const box of boxes) {
  box.style.width = box.parentElement.offsetWidth / 2 + "px";
}

// ✅ Batch: all reads first, then all writes (1 layout)
const widths = boxes.map((box) => box.parentElement.offsetWidth);
boxes.forEach((box, i) => { box.style.width = widths[i] / 2 + "px"; });

// ✅ Or schedule writes for the next frame
const w = el.offsetWidth;                    // read now
requestAnimationFrame(() => { el.style.width = w * 2 + "px"; });   // write before next paint
```

### Long tasks & responsiveness (INP)

A **long task** is any main-thread work > **50 ms**. While it runs, clicks and typing can't be handled → poor **INP** (Interaction to Next Paint).

```js
// ❌ One 400ms task blocks input
function processAll(items) { items.forEach(expensiveWork); }

// ✅ Yield to the browser between chunks so it can handle input & paint
async function processInChunks(items, chunkSize = 50) {
  for (let i = 0; i < items.length; i += chunkSize) {
    items.slice(i, i + chunkSize).forEach(expensiveWork);
    await yieldToMain();
  }
}
function yieldToMain() {
  if (globalThis.scheduler?.yield) return scheduler.yield();      // modern API (Chromium)
  return new Promise((resolve) => setTimeout(resolve, 0));        // fallback
}
```

Other tools:
- **Web Workers** for heavy computation (parsing, image processing, crypto).
- `requestIdleCallback` for low-priority background work (analytics, prefetching).
- Debounce/throttle high-frequency handlers; `passive: true` scroll/touch listeners.
- In React: `useTransition` / `useDeferredValue`, virtualization, memoization.

### Rendering-friendly CSS

```css
/* Skip rendering work for off-screen sections until they're near the viewport */
.feed-item { content-visibility: auto; contain-intrinsic-size: auto 400px; }

/* Tell the browser changes inside won't affect outside layout */
.widget { contain: layout paint; }

/* Reserve space for media & ads → no layout shift (CLS).
   Set width/height attributes on <img>/<video>: browsers derive the aspect ratio from them. */
img, video { max-width: 100%; height: auto; }
.hero { aspect-ratio: 16 / 9; }           /* explicit ratio for containers/backgrounds */
.ad-slot { min-height: 250px; }
```

### Layout shift (CLS) — causes & fixes

| Cause | Fix |
|---|---|
| Images/videos without dimensions | Set `width`/`height` or `aspect-ratio` |
| Ads/embeds/iframes injected late | Reserve space with `min-height` |
| Web fonts swapping (FOUT) changing text size | `font-display: optional/swap` + `size-adjust`, preload fonts |
| Content inserted above existing content (banners) | Insert below, or reserve space, or overlay |
| Animating layout properties | Animate `transform` instead |

### requestAnimationFrame vs setTimeout for visuals

`requestAnimationFrame(cb)` runs `cb` **right before the next paint**, synced to the display refresh rate, and pauses in background tabs. `setTimeout` fires at arbitrary times → uneven animations and wasted work.

```js
function animateProgress(el, to, duration = 500) {
  const start = performance.now();
  const from = parseFloat(el.dataset.progress ?? 0);
  function frame(now) {
    const t = Math.min(1, (now - start) / duration);
    const eased = 1 - (1 - t) ** 3;                          // ease-out cubic
    const value = from + (to - from) * eased;
    el.style.transform = `scaleX(${value / 100})`;           // composite-only
    if (t < 1) requestAnimationFrame(frame);
    else el.dataset.progress = to;
  }
  requestAnimationFrame(frame);
}
```

For most UI animations, prefer **CSS transitions/animations** or the **Web Animations API** (`el.animate(...)`) — they can run on the compositor even when the main thread is busy. The **View Transitions API** (`document.startViewTransition(() => updateDOM())`) animates between UI states/pages.

### Debugging rendering in DevTools

- **Performance panel**: record → flame chart shows Scripting (yellow), Rendering/Layout (purple), Painting (green); red triangles = long tasks; "Forced reflow" warnings point to thrashing.
- **Rendering tab**: Paint flashing, Layout Shift Regions, FPS meter.
- **Layers panel**: see compositor layers and memory.
- **Lighthouse / Web Vitals extension**: LCP, INP, CLS.

---

### Part 2 — Web Components & Shadow DOM

**Web Components** are browser-native, framework-agnostic reusable components. Three standards:

1. **Custom Elements** — define your own HTML tags (`<star-rating>`) with a JS class.
2. **Shadow DOM** — encapsulated DOM + CSS (styles don't leak in or out).
3. **HTML `<template>` & `<slot>`** — reusable markup and content projection.

### Example — a `<star-rating>` custom element

```js
class StarRating extends HTMLElement {
  static observedAttributes = ["value", "max"];     // attributes that trigger attributeChangedCallback
  #shadow = this.attachShadow({ mode: "open" });

  // Lifecycle callbacks
  connectedCallback() {                              // added to the DOM
    this.#shadow.addEventListener("click", this.#onClick);
    this.render();
  }
  disconnectedCallback() {                           // removed from the DOM → clean up
    this.#shadow.removeEventListener("click", this.#onClick);
  }
  attributeChangedCallback(name, oldValue, newValue) {
    if (oldValue !== newValue) this.render();
  }

  // Property ↔ attribute reflection
  get value() { return Number(this.getAttribute("value") ?? 0); }
  set value(v) { this.setAttribute("value", String(v)); }
  get max() { return Number(this.getAttribute("max") ?? 5); }

  #onClick = (e) => {
    const star = e.target.closest("button");
    if (!star) return;
    this.value = Number(star.dataset.value);
    this.dispatchEvent(new CustomEvent("change", {
      detail: { value: this.value },
      bubbles: true,
      composed: true,                                // cross the shadow boundary
    }));
  };

  render() {
    const stars = Array.from({ length: this.max }, (_, i) => i + 1)
      .map((n) => `<button part="star" data-value="${n}" aria-label="${n} stars"
                     aria-pressed="${n <= this.value}">${n <= this.value ? "★" : "☆"}</button>`)
      .join("");
    this.#shadow.innerHTML = `
      <style>
        :host { display: inline-flex; gap: 2px; }          /* styles the custom element itself */
        :host([disabled]) { pointer-events: none; opacity: .5; }
        button { all: unset; cursor: pointer; font-size: var(--star-size, 24px); color: var(--star-color, gold); }
      </style>
      ${stars}`;
  }
}

customElements.define("star-rating", StarRating);    // name MUST contain a hyphen
```

```html
<star-rating value="3" max="5" style="--star-color: tomato"></star-rating>
<script>
  document.querySelector("star-rating")
    .addEventListener("change", (e) => console.log("rated", e.detail.value));
</script>
```

### Shadow DOM essentials

- `attachShadow({ mode: "open" })` → accessible via `el.shadowRoot`; `"closed"` hides it (rarely worth it).
- **Style encapsulation**: page CSS doesn't style shadow content; shadow CSS doesn't leak out.
- Ways to style from outside (the public styling API):
  - **CSS custom properties** inherit through the boundary (`--star-color`).
  - **`::part(name)`** for elements marked with `part="name"`: `star-rating::part(star) { font-size: 32px; }`.
  - `:host`, `:host(.class)`, `:host-context()` inside the component.
- Events from inside are **retargeted** to the host element; custom events need `composed: true` to escape.

### Slots — projecting content

```js
class UserCard extends HTMLElement {
  constructor() {
    super();
    this.attachShadow({ mode: "open" }).innerHTML = `
      <style>
        .card { border: 1px solid #ddd; border-radius: 8px; padding: 12px; }
        ::slotted(img) { width: 48px; border-radius: 50%; }   /* style projected light-DOM content */
      </style>
      <div class="card">
        <slot name="avatar"></slot>
        <h3><slot name="name">Anonymous</slot></h3>          <!-- fallback content -->
        <slot></slot>                                          <!-- default slot -->
      </div>`;
  }
}
customElements.define("user-card", UserCard);
```

```html
<user-card>
  <img slot="avatar" src="/rohit.jpg" alt="">
  <span slot="name">Rohit</span>
  <p>Frontend developer</p>
</user-card>
```

### `<template>` and declarative shadow DOM

```html
<!-- Inert markup, cloned by JS (not rendered until used) -->
<template id="row-tpl">
  <li class="row"><span class="name"></span></li>
</template>
<script>
  const tpl = document.getElementById("row-tpl");
  const row = tpl.content.cloneNode(true);
  row.querySelector(".name").textContent = "Item 1";
  list.append(row);
</script>

<!-- Declarative Shadow DOM: shadow root in HTML (works with SSR, no JS needed to render) -->
<my-banner>
  <template shadowrootmode="open">
    <style>p { color: white; background: navy; padding: 8px; }</style>
    <p><slot></slot></p>
  </template>
  Sale ends today!
</my-banner>
```

### When to use Web Components

✅ Design systems shared across **different frameworks** (React + Angular + plain HTML), embeddable widgets (chat, payments, maps) on third-party sites, micro-frontends, long-lived components that should outlive framework churn.
⚠️ Trade-offs: SSR is harder, forms need `ElementInternals` (`static formAssociated = true`) to participate, accessibility across shadow boundaries (ARIA ID references) needs care, less ergonomic than a framework without a helper library.

Libraries: **Lit** (tiny, reactive properties + templates), **Stencil**, **FAST**. React 19 fully supports custom elements (passes properties and handles custom events).

**Shadow DOM vs Virtual DOM**: Shadow DOM is a **browser feature for encapsulation**; Virtual DOM is a **library technique for efficient updates**. Unrelated, can be combined.

---

### Part 3 — Service Workers & Progressive Web Apps (PWA)

A **Service Worker (SW)** is a script that runs in the background, **separate from the page**, acting as a **programmable network proxy** between your app and the network.

- Intercepts `fetch` requests → offline support, custom caching.
- Receives **push** messages and shows notifications even when the site is closed.
- **Background sync** — retry actions when connectivity returns.
- No DOM access; communicates with pages via `postMessage`.
- **HTTPS only** (localhost allowed); scoped to its folder (`/sw.js` controls the whole origin).

### Lifecycle

```
register() → install (precache assets) → waiting (old SW still controls open tabs)
           → activate (clean old caches) → controls pages → handles fetch/push/sync events
```

A new SW version **waits** until all tabs using the old one are closed — unless you call `skipWaiting()` (then prompt the user to reload for consistency).

### Registering

```js
// main.js
if ("serviceWorker" in navigator) {
  window.addEventListener("load", async () => {
    const reg = await navigator.serviceWorker.register("/sw.js");
    reg.addEventListener("updatefound", () => {
      const newWorker = reg.installing;
      newWorker?.addEventListener("statechange", () => {
        if (newWorker.state === "installed" && navigator.serviceWorker.controller) {
          showToast("New version available", { action: "Reload", onClick: () => {
            newWorker.postMessage({ type: "SKIP_WAITING" });
          }});
        }
      });
    });
    navigator.serviceWorker.addEventListener("controllerchange", () => window.location.reload());
  });
}
```

### A service worker with caching strategies

```js
// sw.js
const VERSION = "v3";
const STATIC_CACHE = `static-${VERSION}`;
const RUNTIME_CACHE = `runtime-${VERSION}`;
const PRECACHE = ["/", "/offline.html", "/manifest.webmanifest", "/icons/icon-192.png"];

self.addEventListener("install", (event) => {
  event.waitUntil(caches.open(STATIC_CACHE).then((cache) => cache.addAll(PRECACHE)));
});

self.addEventListener("activate", (event) => {
  event.waitUntil((async () => {
    const keys = await caches.keys();
    await Promise.all(keys.filter((k) => ![STATIC_CACHE, RUNTIME_CACHE].includes(k)).map((k) => caches.delete(k)));
    await self.clients.claim();                       // control open pages immediately
  })());
});

self.addEventListener("message", (event) => {
  if (event.data?.type === "SKIP_WAITING") self.skipWaiting();
});

self.addEventListener("fetch", (event) => {
  const { request } = event;
  const url = new URL(request.url);
  if (request.method !== "GET" || url.origin !== location.origin) return;   // let the browser handle it
  if (url.pathname.startsWith("/api/")) return;       // don't cache private API data by default

  if (request.mode === "navigate") {
    event.respondWith(networkFirst(request));          // HTML: fresh when online, cached/offline page otherwise
  } else if (url.pathname.startsWith("/assets/")) {
    event.respondWith(cacheFirst(request));            // hashed assets never change
  } else {
    event.respondWith(staleWhileRevalidate(request));  // images, fonts, etc.
  }
});

async function cacheFirst(request) {
  const cached = await caches.match(request);
  if (cached) return cached;
  const response = await fetch(request);
  if (response.ok) (await caches.open(RUNTIME_CACHE)).put(request, response.clone());
  return response;
}

async function networkFirst(request) {
  try {
    const response = await fetch(request);
    (await caches.open(RUNTIME_CACHE)).put(request, response.clone());
    return response;
  } catch {
    return (await caches.match(request)) ?? caches.match("/offline.html");
  }
}

async function staleWhileRevalidate(request) {
  const cache = await caches.open(RUNTIME_CACHE);
  const cached = await cache.match(request);
  const network = fetch(request).then((response) => {
    if (response.ok) cache.put(request, response.clone());
    return response;
  }).catch(() => cached);
  return cached ?? network;                             // instant if cached; updated in the background
}
```

In real projects use **Workbox** (or `vite-plugin-pwa`, which wraps it) — it handles precache manifests with hashes, strategies, expiration and updates.

### Caching strategies summary

| Strategy | Use for |
|---|---|
| **Cache first** | Hashed static assets, fonts |
| **Network first** | HTML pages, frequently changing data |
| **Stale-while-revalidate** | Avatars, non-critical API data, images |
| **Network only** | Payments, auth, analytics, anything private/real-time |
| **Cache only** | Precached app shell |

### PWA essentials

A **Progressive Web App** is a website that can be installed and work offline like an app:

1. Served over **HTTPS**.
2. A **Web App Manifest**.
3. A **Service Worker** (offline support).

```json
// manifest.webmanifest
{
  "name": "Shop App",
  "short_name": "Shop",
  "start_url": "/?source=pwa",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#4f46e5",
  "icons": [
    { "src": "/icons/icon-192.png", "sizes": "192x192", "type": "image/png" },
    { "src": "/icons/icon-512.png", "sizes": "512x512", "type": "image/png", "purpose": "any maskable" }
  ]
}
```

```html
<link rel="manifest" href="/manifest.webmanifest">
<meta name="theme-color" content="#4f46e5">
```

Extra capabilities: **push notifications** (Push API + `Notification`, needs user permission and a push server using VAPID keys), **background sync**, **periodic sync**, install prompt (`beforeinstallprompt`), share target, badging.

### Service worker pitfalls

- **Stale app after deploy**: users keep the old version until the new SW activates → show an "update available" prompt; never cache `index.html` cache-first.
- **Caching private data**: responses for logged-in users can leak to the next user on a shared device → don't cache authenticated API responses, clear caches on logout.
- **Caching errors**: only cache `response.ok` responses (and be careful with opaque cross-origin responses).
- **Unbounded caches**: set expiration/limits (Workbox `ExpirationPlugin`).
- **A broken SW can brick the site** for returning users → keep an escape hatch (deploy a SW that unregisters itself), test updates carefully.
- Debug in DevTools → **Application** tab (Service Workers, Cache Storage, "Update on reload", "Bypass for network", Unregister).

### Interview Qs

1. Explain the pixel pipeline (JS → Style → Layout → Paint → Composite).
2. Reflow vs repaint vs composite? Which CSS properties are cheapest to animate?
3. What is layout thrashing and how do you fix it?
4. What is a long task? How do you keep the main thread responsive (INP)?
5. What does `will-change` do? Why not use it everywhere?
6. What causes layout shift (CLS) and how do you prevent it?
7. `requestAnimationFrame` vs `setTimeout` for animations?
8. What are Web Components? The three technologies involved?
9. What is Shadow DOM? How do you style a component from outside (`::part`, CSS variables)?
10. Shadow DOM vs Virtual DOM?
11. What is a Service Worker and its lifecycle? Why does a new SW "wait"?
12. Explain cache-first vs network-first vs stale-while-revalidate.
13. What makes a web app a PWA?
14. What are the risks of service workers in production?

---

## 45. Date, Math, Number, Intl

```js
// Number
Number("12px");         // NaN
parseInt("12px");       // 12
parseFloat("3.14abc");  // 3.14
parseInt("101", 2);     // 5 (binary)
(1234.5678).toFixed(2); // "1234.57" (string)
Number.isInteger(5.0);  // true
(255).toString(16);     // "ff"
1_000_000;              // numeric separator

// Math
Math.round(4.5); Math.floor(-4.5); Math.ceil(4.1); Math.trunc(-4.9); // 5, -5, 5, -4
Math.max(...[1, 9, 3]);
Math.random();                                         // [0, 1)
const randInt = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min;

// Date
const now = new Date();
now.toISOString();          // "2026-09-24T..Z"
now.getMonth();             // 0-based!
new Date(2026, 0, 31);      // Jan 31 2026
Date.now();                 // ms timestamp
const diffDays = (new Date("2026-12-25") - new Date("2026-09-24")) / 86400000;

// Intl — formatting
new Intl.NumberFormat("en-IN", { style: "currency", currency: "INR" }).format(123456.78); // "₹1,23,456.78"
new Intl.DateTimeFormat("en-GB", { dateStyle: "medium" }).format(now);
new Intl.RelativeTimeFormat("en", { numeric: "auto" }).format(-1, "day"); // "yesterday"
new Intl.PluralRules("en").select(1); // "one"
```

---

## 46. Dates & Time Zones in Depth

Date bugs are the most common "works on my machine" bugs: they depend on the **user's time zone**, **daylight saving time (DST)** and **how dates were parsed**. Get the mental model right and most of them disappear.

### 1. The mental model: four different things

| Concept | Example | How to store / send |
|---|---|---|
| **Instant** — an exact moment, same everywhere | "Payment captured at 2026-09-24T07:30:00Z" | UTC ISO string (`…Z`) or epoch ms; Postgres `timestamptz` |
| **Calendar date** — a day, no time, no zone | Birthday `2026-09-24`, invoice due date | `"YYYY-MM-DD"` string; Postgres `date` |
| **Wall-clock time in a zone** — what a clock on a wall shows somewhere | "Standup 09:30 in Asia/Kolkata, every weekday" | Local date-time + **IANA zone name** |
| **Duration** | "30 minutes", "14 days" | Number of units / ISO duration `PT30M` |

- A **time zone** (`Asia/Kolkata`, `America/New_York`) is a set of rules (offset + DST history); an **offset** (`+05:30`, `-04:00`) is just the current difference from UTC. New York is `-05:00` in winter and `-04:00` in summer — so **store zone names, not offsets**, for anything in the future.
- `Date` in JavaScript is always an **instant** (milliseconds since 1970-01-01 UTC). It has no time zone — it's only *displayed* in the environment's local zone.

### 2. `Date` gotchas you must know

```js
// 1. Months are 0-based
new Date(2026, 9, 24);                     // 24 **October** 2026

// 2. Parsing rules differ by format
new Date("2026-09-24");                    // date-only ISO  → UTC midnight
new Date("2026-09-24T00:00");              // date-time without Z → LOCAL midnight
new Date("2026-09-24T00:00Z");             // with Z → UTC
new Date("24/09/2026");                    // non-ISO → Invalid Date (or browser-specific guesses) — never parse these

// So in New York, the "same" date displays as the day before:
new Date("2026-09-24").toLocaleDateString("en-US", { timeZone: "America/New_York" });   // "9/23/2026"

// 3. Date objects are mutable
const start = new Date(2026, 0, 31);
const next = start;                        // same object!
next.setMonth(1);                          // Jan 31 + 1 month → "Feb 31" overflows to March 3; `start` changed too

// 4. Invalid dates don't throw
const d = new Date("not a date");
Number.isNaN(d.getTime());                 // true — always validate
d.toISOString();                           // ❌ throws RangeError: Invalid time value

// 5. toISOString() is always UTC — slicing it for "today's date" is a bug east of UTC late at night… and west of UTC in the evening
new Date(2026, 8, 24, 3, 0).toISOString().slice(0, 10);   // in India (UTC+5:30): "2026-09-23" ❌

// 6. getTimezoneOffset() has the "wrong" sign: minutes to ADD to local time to get UTC
new Date().getTimezoneOffset();            // India: -330, New York (summer): 240
```

### 3. Safe helpers for calendar dates

```js
// Local calendar date as "YYYY-MM-DD" (NOT toISOString().slice(0, 10))
export function toLocalISODate(date = new Date()) {
  const y = date.getFullYear();
  const m = String(date.getMonth() + 1).padStart(2, "0");
  const d = String(date.getDate()).padStart(2, "0");
  return `${y}-${m}-${d}`;
}

// Parse "YYYY-MM-DD" as a LOCAL date (midnight), validating it's a real day
export function parseISODate(s) {
  const m = /^(\d{4})-(\d{2})-(\d{2})$/.exec(s);
  if (!m) throw new Error(`Invalid date format: ${s}`);
  const [y, mo, d] = [Number(m[1]), Number(m[2]), Number(m[3])];
  const date = new Date(y, mo - 1, d);
  if (date.getFullYear() !== y || date.getMonth() !== mo - 1 || date.getDate() !== d) throw new Error(`Invalid date: ${s}`);   // 2026-02-30
  return date;
}

// Whole calendar days between two "YYYY-MM-DD" dates (DST-proof: compute in UTC)
export function daysBetween(a, b) {
  const [ay, am, ad] = a.split("-").map(Number);
  const [by, bm, bd] = b.split("-").map(Number);
  return Math.round((Date.UTC(by, bm - 1, bd) - Date.UTC(ay, am - 1, ad)) / 86_400_000);
}

// Age in whole years on a given day
export function ageOn(birthISO, onISO) {
  const [by, bm, bd] = birthISO.split("-").map(Number);
  const [y, m, d] = onISO.split("-").map(Number);
  return y - by - (m < bm || (m === bm && d < bd) ? 1 : 0);
}
```

### 4. Adding time: calendar days vs 24 hours (DST!)

On a DST change day, a "day" is **23 or 25 hours**. Adding milliseconds and adding calendar days give different results.

```js
// In America/New_York, DST starts at 02:00 on 8 March 2026 (clocks jump to 03:00)
const noon = new Date(2026, 2, 7, 12, 0);                  // 7 March, 12:00 local

const plus24h = new Date(noon.getTime() + 24 * 60 * 60 * 1000);
plus24h.getHours();                                        // 13 ❌ — "tomorrow at noon" became 13:00

const plus1Day = new Date(noon);
plus1Day.setDate(plus1Day.getDate() + 1);                  // calendar arithmetic
plus1Day.getHours();                                       // 12 ✅
```

Rules: use **calendar arithmetic** (`setDate`, date libraries, Temporal) for "same time tomorrow / next month"; use **milliseconds** only for exact durations ("expires in 24 hours", timeouts).

Months overflow too: `Jan 31 + 1 month` isn't Feb 31. Decide the rule (clamp to month end — what most libraries do) and use a library that implements it.

### 5. Displaying in a specific time zone

```js
const paidAt = new Date("2026-09-24T07:30:00Z");           // instant from the API

new Intl.DateTimeFormat("en-IN", { dateStyle: "medium", timeStyle: "short", timeZone: "Asia/Kolkata" }).format(paidAt);
// "24 Sept 2026, 1:00 pm"
new Intl.DateTimeFormat("en-US", { dateStyle: "medium", timeStyle: "short", timeZone: "America/New_York" }).format(paidAt);
// "Sep 24, 2026, 3:30 AM"

Intl.DateTimeFormat().resolvedOptions().timeZone;          // the user's IANA zone, e.g. "Asia/Kolkata"
```

Get the parts of an instant **in any zone** (e.g. "which calendar day is this in the customer's zone?"):

```js
export function partsInZone(date, timeZone) {
  const parts = new Intl.DateTimeFormat("en-US", {
    timeZone, hourCycle: "h23",
    year: "numeric", month: "2-digit", day: "2-digit", hour: "2-digit", minute: "2-digit",
  }).formatToParts(date);
  const get = (type) => Number(parts.find((p) => p.type === type).value);
  return { year: get("year"), month: get("month"), day: get("day"), hour: get("hour"), minute: get("minute") };
}

export const isoDateInZone = (date, timeZone) => {
  const { year, month, day } = partsInZone(date, timeZone);
  return `${year}-${String(month).padStart(2, "0")}-${String(day).padStart(2, "0")}`;
};

isoDateInZone(new Date("2026-09-24T20:00:00Z"), "Asia/Kolkata");      // "2026-09-25" (01:30 next day in India)
isoDateInZone(new Date("2026-09-24T20:00:00Z"), "America/New_York");  // "2026-09-24"
```

**Zone names aren't stable strings**: the same zone can come back as `"Asia/Kolkata"` or the older alias `"Asia/Calcutta"` depending on the runtime's ICU data. Don't compare zone names with `===` to decide behaviour — normalize (or compare the resulting offsets/dates).

### 6. Temporal — the modern date/time API

`Temporal` fixes `Date`'s design: immutable values, separate types for each concept, DST-aware arithmetic, time zones built in. It's shipping in modern browsers; use `@js-temporal/polyfill` elsewhere (check support for your targets).

```js
// Instant: an exact moment
const now = Temporal.Now.instant();
const paid = Temporal.Instant.from("2026-09-24T07:30:00Z");

// PlainDate: a calendar date (no time, no zone) — birthdays, due dates
const due = Temporal.PlainDate.from("2026-01-31");
due.add({ months: 1 }).toString();                         // "2026-02-28" (clamped, not overflowed)
due.until(Temporal.PlainDate.from("2026-03-01")).days;     // 29
Temporal.PlainDate.compare(due, Temporal.PlainDate.from("2026-02-01"));   // -1

// ZonedDateTime: wall-clock time in a zone — meetings, schedules
const standup = Temporal.ZonedDateTime.from("2026-03-07T12:00[America/New_York]");
standup.add({ days: 1 }).toString();                       // "2026-03-08T12:00:00-04:00[America/New_York]" ✅ DST-aware
standup.add({ hours: 24 }).toString();                     // "2026-03-08T13:00:00-04:00[America/New_York]" (exact hours)
paid.toZonedDateTimeISO("Asia/Kolkata").toPlainTime().toString();   // "13:00:00"

// Duration
const d = Temporal.Duration.from({ hours: 1, minutes: 90 });
d.round({ largestUnit: "hour" }).toString();               // "PT2H30M"
```

### 7. Libraries

| Library | Notes |
|---|---|
| **date-fns** (+ `@date-fns/tz`) | Functional, tree-shakeable, works on native `Date` |
| **Luxon** | Immutable `DateTime` with first-class time zones & `Intl` formatting |
| **Day.js** | Tiny, Moment-like API (plugins for timezone/UTC) |
| **Temporal** (+ polyfill) | The future standard; prefer it for new code where available |
| Moment.js | Legacy / maintenance mode — don't start new projects with it |

```js
import { addDays, differenceInCalendarDays, format, parseISO } from "date-fns";

const due = parseISO("2026-09-24");                      // parses date-only as LOCAL midnight (unlike new Date())
format(addDays(due, 7), "dd MMM yyyy");                  // "01 Oct 2026"
differenceInCalendarDays(parseISO("2026-12-25"), due);   // 92
```

### 8. Backend, database & API rules

- Servers, databases and cron jobs run in **UTC**.
- API responses: instants as ISO strings **with `Z` or an offset** (`2026-09-24T07:30:00Z`); dates as `YYYY-MM-DD`.
- Postgres: `timestamptz` for instants (stored as UTC), `date` for calendar dates. Avoid `timestamp without time zone` for instants.
- **Future local events** (reminders at 09:00, recurring meetings): store the **local time + IANA zone**, and compute the instant close to the time — DST rules and even zone definitions change by law.
- "Today" / "this month" reports: decide **whose** day (the user's or the business's zone) and compute boundaries in that zone.
- Keep your runtime's time-zone data updated (browser/Node/OS/`tzdata`).

### 9. Testing date code

```js
// Freeze "now"
vi.useFakeTimers();
vi.setSystemTime(new Date("2026-03-07T17:00:00Z"));

// Run the suite in a non-UTC zone in CI to catch UTC-only assumptions
// package.json: "test:tz": "TZ=America/New_York vitest run && TZ=Asia/Kolkata vitest run"
```

Test the nasty days: DST start/end, 29 Feb, 31st of the month, year boundaries, and times near midnight in zones far from UTC (Kolkata +05:30, Auckland +13:00, Honolulu −10:00).

### Gotchas checklist

- [ ] Never `new Date("YYYY-MM-DD")` for local dates; never `toISOString().slice(0, 10)` for "today"
- [ ] Months are 0-based; `Date` is mutable; invalid dates don't throw until `toISOString()`
- [ ] Calendar arithmetic for "tomorrow / next month"; ms arithmetic only for exact durations
- [ ] Store instants in UTC, dates as `YYYY-MM-DD`, future local events as time + IANA zone
- [ ] Format for display with `Intl` and an explicit `timeZone`
- [ ] Don't compare time-zone names as strings
- [ ] Tests run under several `TZ` values with a frozen clock

### Interview Qs

1. Instant vs calendar date vs wall-clock time — how do you store each?
2. Why does `new Date("2026-09-24")` show 23 September in the US?
3. Why is `toISOString().slice(0, 10)` a bug for "today's date"?
4. What happens when you add 24 hours across a DST change? How do you add "one day" correctly?
5. Time zone vs offset — why store `America/New_York` instead of `-05:00`?
6. How do you show an instant in the customer's time zone?
7. What problems does Temporal solve?
8. How do you test date logic reliably?

---

## 47. Regular Expressions

A regular expression ("regex") is a small pattern language for finding, validating, extracting and replacing text. It's the right tool for **short, well-defined patterns** (IDs, codes, tokens, log lines) and the wrong tool for nested formats such as HTML, JSON or full URLs, where you should use a real parser (`DOMParser`, `JSON.parse`, `new URL()`).

### Creating a regex

```js
const a = /\d{3}-\d{4}/g;                    // literal: compiled once, the best choice for fixed patterns
const b = new RegExp("\\d{3}-\\d{4}", "g");  // constructor: for patterns built at runtime. Note the DOUBLE backslash in a string
a.source;                                     // → "\\d{3}-\\d{4}"
a.flags;                                      // → "g"
String(b) === String(a);                      // → true
```

**Never put raw user input into `new RegExp()`.** Characters such as `.`, `*`, `(` and `?` have special meanings, so `"a.b"` would also match `"axb"`, and input like `"(a+)+$"` can freeze the process (see ReDoS below). Escape the input first:

```js
// ES2025: RegExp.escape (Node 24+ and current browsers; check support before shipping)
const escape = RegExp.escape ?? ((s) => s.replace(/[.*+?^${}()|[\]\\/]/g, "\\$&"));   // fallback for older runtimes

const userQuery = "1+1=2?";
new RegExp(userQuery).test("1+1=2?");          // → false  (+ and ? are treated as quantifiers)
new RegExp(escape(userQuery)).test("1+1=2?");  // → true
```

### Syntax cheat sheet

| Pattern | Meaning |
|---|---|
| `.` | Any character except line breaks (use the `s` flag to include them) |
| `\d` `\w` `\s` | Digit `[0-9]`, word character `[A-Za-z0-9_]`, whitespace. **ASCII only** for `\d` and `\w`, even with the `u` flag |
| `\D` `\W` `\S` | The opposites |
| `[abc]` `[^abc]` `[a-z]` | Character class, negated class, range |
| `^` `$` | Start and end of the input (or of each line with the `m` flag) |
| `\b` `\B` | Word boundary, not a word boundary |
| `*` `+` `?` | 0 or more, 1 or more, 0 or 1 (**greedy**: as many as possible) |
| `{n}` `{n,}` `{n,m}` | Exactly n, at least n, between n and m |
| `*?` `+?` `??` `{n,m}?` | **Lazy** versions: as few as possible |
| `(x)` | Capturing group, referenced as `$1` or `\1` |
| `(?:x)` | Non-capturing group (grouping only) |
| `(?<name>x)` | Named group, referenced as `$<name>` or `\k<name>` |
| `x\|y` | Alternation: x or y |
| `(?=x)` `(?!x)` | Lookahead: followed by x, not followed by x |
| `(?<=x)` `(?<!x)` | Lookbehind: preceded by x, not preceded by x |
| `\p{L}` `\p{N}` `\p{Script=Devanagari}` | Unicode property escapes (need the `u` or `v` flag) |
| `\.` `\\` `\/` | Escaped special characters |

### Flags

| Flag | Name | Effect |
|---|---|---|
| `g` | global | Find **all** matches. Makes `test`/`exec` **stateful** via `lastIndex` |
| `i` | ignoreCase | Case-insensitive |
| `m` | multiline | `^` and `$` match at every line start and end |
| `s` | dotAll | `.` also matches `\n` |
| `u` | unicode | Code-point aware: emoji count as one character, `\p{…}` works, invalid escapes become errors |
| `v` | unicodeSets | `u` plus set operations in classes and multi-character string properties (ES2024) |
| `y` | sticky | Match only **at** `lastIndex`, not anywhere after it (for tokenizers) |
| `d` | hasIndices | Adds `match.indices` with start and end positions for every group |

```js
/^\w+$/m.test("bad input\nok");   // → true   (m: "ok" alone on the second line satisfies ^…$)
/a.c/.test("a\nc");                // → false
/a.c/s.test("a\nc");               // → true
"😀".length;                       // → 2      (a UTF-16 surrogate pair)
/^.$/.test("😀");                  // → false
/^.$/u.test("😀");                 // → true
```

### Which method to use

| Method | Returns | Use for |
|---|---|---|
| `re.test(str)` | `true` / `false` | Validation, "does it match?" |
| `str.match(re)` without `g` | First match with groups, `index` and `input`, or `null` | Extract one thing |
| `str.match(re)` with `g` | Array of matched strings (no groups), or `null` | Get all matched strings |
| `str.matchAll(re)` (needs `g`) | Iterator of full match objects | All matches **with** groups and indexes |
| `str.replace(re, x)` | New string | Replace the first match (or all with `g`) |
| `str.replaceAll(re, x)` (needs `g`) | New string | Replace all; with a plain string pattern it needs no regex at all |
| `str.split(re)` | Array | Split on a pattern. Capture groups are **included** in the result |
| `str.search(re)` | Index or `-1` | Position of the first match |
| `re.exec(str)` | Match object or `null` | Loops with `g`/`y`, tokenizers |

```js
"2026-09-24".match(/(\d+)-(\d+)/).slice(0, 3);   // → ["2026-09", "2026", "09"]
"2026-09-24".match(/\d+/g);                       // → ["2026", "09", "24"]
"no digits".match(/\d+/g);                        // → null   (so `.length` would crash: use `?? []`)
[..."a1b22c333".matchAll(/\d+/g)].map((m) => [m[0], m.index]);   // → [["1", 1], ["22", 3], ["333", 6]]
"one, two,three".split(/\s*,\s*/);                // → ["one", "two", "three"]
"1,2;3".split(/([,;])/);                          // → ["1", ",", "2", ";", "3"]   (captured separators are kept)
"a.b.c".split(".");                               // → ["a", "b", "c"]
"a.b.c".split(/./);                               // → ["", "", "", "", "", ""]  (. means "any character")
```

`matchAll` and `replaceAll` **throw a `TypeError`** when given a regex without the `g` flag.

### The `lastIndex` trap (`g` and `y` are stateful)

A regex with `g` or `y` remembers where its last match ended (`re.lastIndex`), and the **next** `test`/`exec` call starts searching from there:

```js
const hasA = /a/g;
hasA.test("a");      // → true    (lastIndex is now 1)
hasA.test("a");      // → false   (searches from index 1 of "a", finds nothing, resets lastIndex to 0)
hasA.test("a");      // → true

// ❌ A real bug: a shared global regex used in a filter skips matching items
const startsWithA = /^a/gi;
["apple", "avocado", "apricot"].filter((w) => startsWithA.test(w));   // → ["apple", "apricot"]

// ✅ Use no g flag for test(); g is only for finding many matches in ONE string
const startsWithA2 = /^a/i;
["apple", "avocado", "apricot"].filter((w) => startsWithA2.test(w));  // → ["apple", "avocado", "apricot"]
```

With `g`, `str.match`, `replace` and `replaceAll` always start from index 0, and `matchAll`/`split` work on a copy, so the trap is mainly `test` and `exec`.

### Groups and backreferences

```js
// Named groups make extraction readable
const LOG = /^(?<level>INFO|WARN|ERROR) \[(?<time>[\d:]+)\] (?<msg>.*)$/;
const { level, time, msg } = "ERROR [12:04:55] Payment failed".match(LOG).groups;
[level, time, msg];                 // → ["ERROR", "12:04:55", "Payment failed"]

// Optional groups that didn't take part are undefined
"5kg".match(/(\d+)(?:\.(\d+))?kg/)[2];      // → undefined

// Backreferences: match the SAME text again. Here, doubled words
"this is is a test test".match(/\b(\w+) \1\b/g);   // → ["is is", "test test"]
/^(?<q>["']).*\k<q>$/.test(`"mixed'`);            // → false  (closing quote must match the opening one)
```

**Duplicate named groups (ES2025).** Alternatives can reuse a name, which is handy when parsing several formats:

```js
// ES2025 (Node 24+)
const DATE = /(?<y>\d{4})-(?<m>\d{2})|(?<m>\d{2})\/(?<y>\d{4})/;
"2026-09".match(DATE).groups.y;     // → "2026"
"09/2026".match(DATE).groups.y;     // → "2026"
```

### Greedy vs lazy

```js
const html = "<b>bold</b> and <i>italic</i>";
html.match(/<.+>/)[0];        // → "<b>bold</b> and <i>italic</i>"   greedy: runs to the LAST >
html.match(/<.+?>/)[0];       // → "<b>"                               lazy: stops at the first >
html.match(/<[^>]+>/g);       // → ["<b>", "</b>", "<i>", "</i>"]      best: a negated class can't overshoot and backtracks less
```

Prefer a **negated class** (`[^>]+`, `[^"]*`) over `.*?`. It says exactly what may appear and is faster. (This is an illustration: don't parse real HTML with regex.)

### Lookarounds

Lookarounds check what comes before or after a position **without consuming it**:

```js
// Several independent rules at once, using lookaheads at the start
const STRONG = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{12,}$/;
STRONG.test("Sunshine2026!");          // → true
STRONG.test("sunshine2026!");          // → false  (no uppercase)

// Lookbehind: amounts after a ₹ sign, without the sign
"Paid ₹1200 and ₹85, not $40".match(/(?<=₹)\d+/g);    // → ["1200", "85"]

// Negative lookahead: identifiers that are NOT function calls
"call foo() and bar but not baz()".match(/\b[a-z]+\b(?!\()/g);   // → ["call", "and", "bar", "but", "not"]

// Thousands separators with a lookahead (in real code use Intl.NumberFormat)
"1234567".replace(/\B(?=(\d{3})+(?!\d))/g, ",");      // → "1,234,567"
```

For password rules, modern guidance (NIST) favours **minimum length plus a check against breached passwords** over composition rules. Enforce the rules on the server too.

### Replace in depth

The replacement **string** understands special patterns:

| Pattern | Inserts |
|---|---|
| `$&` | The whole match |
| `$1`, `$2` … | Capture groups |
| `$<name>` | A named group |
| `` $` `` / `$'` | The text before / after the match |
| `$$` | A literal `$` |

```js
"2026-09-24".replace(/(\d+)-(\d+)-(\d+)/, "$3/$2/$1");                  // → "24/09/2026"
"2026-09-24".replace(/(?<y>\d+)-(?<m>\d+)-(?<d>\d+)/, "$<d>.$<m>.$<y>"); // → "24.09.2026"
"cost: 5".replace(/\d+/, "$$$&");                                       // → "cost: $5"

// A replacement FUNCTION receives (match, g1, g2, …, offset, input, groups)
"background-color".replace(/-([a-z])/g, (_, ch) => ch.toUpperCase());   // → "backgroundColor"
"backgroundColor".replace(/[A-Z]/g, (ch) => "-" + ch.toLowerCase());    // → "background-color"
"4111 1111 1111 1234".replace(/\d(?=(?:\s?\d){4})/g, "•");             // → "•••• •••• •••• 1234"
```

**Replacement strings from users are a bug.** `$&` or `$1` inside them gets expanded. Pass a function, whose return value is inserted literally:

```js
const template = "Hello NAME";
const userName = "Mr $& Smith";
template.replace("NAME", userName);        // → "Hello Mr NAME Smith"    ❌ $& expanded to the matched text
template.replace("NAME", () => userName);  // → "Hello Mr $& Smith"      ✅
```

A **string** pattern replaces only the first occurrence: `"a-b-c".replace("-", "+")` gives `"a+b-c"`. Use `replaceAll("-", "+")` for all of them. No regex needed.

### Unicode: the `u` and `v` flags

```js
// \w is ASCII-only, so it rejects most real names
/^\w+$/.test("José");                                  // → false
/^[\p{L}\p{M}' -]+$/u.test("José");                    // → true
/^[\p{L}\p{M}' -]+$/u.test("नमस्ते");                   // → true   (\p{M}: Devanagari vowel signs are combining marks)
/^[\p{L}' -]+$/u.test("नमस्ते");                         // → false  (without \p{M})

"राम and Ram".match(/\p{Script=Devanagari}+/gu);      // → ["राम"]
[..."I ❤️ JS 🎉".matchAll(/\p{Extended_Pictographic}/gu)].length;   // → 2
```

The `v` flag (ES2024) adds **set operations** in character classes, plus properties that match whole emoji sequences:

```js
/^[\p{L}--[a-zA-Z]]+$/v.test("नमस्ते");        // → false  (-- subtracts: letters except ASCII. नमस्ते has combining marks)
/^[\p{L}--[a-zA-Z]]+$/v.test("éñü");            // → true
/[\p{L}&&\p{ASCII}]/v.test("é");                // → false  (&& intersects: ASCII letters only)

const family = "\u{1F468}\u200D\u{1F469}\u200D\u{1F467}";    // 👨‍👩‍👧: 3 people joined by zero-width joiners
family.length;                                   // → 8
/^\p{RGI_Emoji}$/v.test(family);                 // → true   (one emoji, even though it's 5 code points)
```

**`v` is stricter inside classes.** Characters such as `-`, `(`, `)`, `[`, `{`, `/` and `|` must be escaped: `[\w.+-]` is a **syntax error** with `v` (write `[\w.+\-]`). This matters in HTML: browsers compile the `pattern` attribute with the `v` flag, and an invalid pattern is **silently ignored**, so the field quietly stops validating:

```html
<!-- ❌ Invalid with v: the browser ignores it, and anything is accepted -->
<input name="email" pattern="[\w.+-]+@[\w-]+\.[a-z]{2,}">
<!-- ✅ Escape - inside classes -->
<input name="email" pattern="[\w.+\-]+@[\w\-]+\.[a-z]{2,}">
```

### Sticky flag: writing a tokenizer

`y` matches only **at** `lastIndex`. That's exactly what a lexer needs, and it's a common interview question:

```js
const TOKEN = /\s*(?:(?<num>\d+(?:\.\d+)?)|(?<op>[-+*\/()]))/y;

function tokenize(src) {
  const tokens = [];
  TOKEN.lastIndex = 0;
  while (TOKEN.lastIndex < src.length) {
    if (/^\s*$/.test(src.slice(TOKEN.lastIndex))) break;          // only trailing whitespace left
    const at = TOKEN.lastIndex;
    const m = TOKEN.exec(src);
    if (!m) throw new SyntaxError(`Unexpected character at ${at}: "${src.slice(at).trimStart()[0]}"`);
    tokens.push(m.groups.num ? { type: "num", value: Number(m.groups.num) } : { type: "op", value: m.groups.op });
  }
  return tokens;
}

tokenize("12 + 3.5*(4 - 1)").map((t) => t.value);   // → [12, "+", 3.5, "*", "(", 4, "-", 1, ")"]
```

Without `y`, `exec` would skip over invalid characters and silently continue from the next valid token.

### Match indices (`d` flag)

`d` gives the start and end of every group, which is useful for highlighting and error messages:

```js
const m = /(?<key>\w+)=(?<value>\w+)/d.exec("  retries=3");
m.indices.groups.value;           // → [10, 11]
m.indices[0];                     // → [2, 11]
```

### Inline modifiers (ES2025)

`(?i:…)` turns a flag on (or `(?-i:…)` off) for one part of the pattern only:

```js
// ES2025 (Node 24+)
/^(?i:ref)-[A-Z]{3}$/.test("REF-ABC");   // → true
/^(?i:ref)-[A-Z]{3}$/.test("ref-abc");   // → false  (only "ref" is case-insensitive)
```

### Validation that holds up

- **Anchor the whole pattern.** `/\d+/.test("abc123")` is `true`; use `/^\d+$/`. With alternation, anchor the group: `/^(?:jpg|png)$/`, **not** `/^jpg|png$/` (which means "starts with jpg OR ends with png").
- **Never add the `m` flag to a validation regex.** With `m`, `^…$` can match any single line, so `"<script>\n123"` passes `/^\d+$/m`.
- **JS vs Python `$`.** In JavaScript, `$` (without `m`) matches only at the very end. In Python it also matches **before a trailing newline**, so `re.match(r"^\d+$", "123\n")` succeeds. Use `re.fullmatch` in Python.
- **A regex checks shape, not meaning.** `^\d{4}-\d{2}-\d{2}$` accepts `2026-02-30`, so parse the value afterwards. The same goes for URLs: use `new URL()` and check `protocol`.
- **Email:** keep it loose (`^[^\s@]+@[^\s@]+\.[^\s@]+$`) and prove the address works by sending a confirmation email. Over-strict email regexes reject real addresses such as `a+tag@x.co.in`.
- **Limit length before matching** (`maxLength`, Zod `.max()`); it also caps ReDoS risk.
- Validate on the **server**. Client-side `pattern` or Zod checks are only for user experience.

```js
// Common Indian formats (shape only)
const PIN = /^[1-9]\d{5}$/;                         // 6-digit PIN code, can't start with 0
const MOBILE = /^(?:\+91[\s-]?)?[6-9]\d{9}$/;       // 10 digits starting 6–9, optional +91
const PAN = /^[A-Z]{5}\d{4}[A-Z]$/;                 // ABCDE1234F
const HEX_COLOR = /^#(?:[\da-f]{3}|[\da-f]{6})$/i;

[PIN.test("110001"), PIN.test("011001")];                     // → [true, false]
[MOBILE.test("+91 98765 43210"), MOBILE.test("+91-9876543210")];  // → [false, true]
[PAN.test("ABCDE1234F"), HEX_COLOR.test("#1a2B3c"), HEX_COLOR.test("#1234")];   // → [true, true, false]
```

The first mobile number fails because of the space **inside** the number. Normalize input before validating (`value.replace(/[\s-]/g, "")`), and store a canonical form.

### ReDoS: catastrophic backtracking

JavaScript's regex engine **backtracks**: when a match fails, it goes back and tries every other way the quantifiers could have split the input. With **nested or overlapping quantifiers**, the number of ways grows **exponentially** with the input length:

```js
const EVIL = /^(\w+\s?)*$/;        // "words separated by optional spaces". Looks harmless
// Measured on Node 24 with input "a".repeat(n) + "!":
//   n = 20 →  ~30 ms
//   n = 24 →  ~75 ms
//   n = 26 → ~300 ms      each extra character DOUBLES the time
//   n = 40 → over an hour (extrapolated)
```

Node runs regexes on the **main thread**, so one request with a 40-character string freezes the whole server for every user. This is **ReDoS** (Regular expression Denial of Service). Real outages:

- **Stack Overflow (2016):** a whitespace-trimming regex hit a post containing about 20,000 consecutive spaces.
- **Cloudflare (2019):** a WAF rule containing `.*(?:.*=.*)` pushed CPUs to 100% across their network.

**Dangerous shapes:**

| Shape | Why it explodes | Safe rewrite |
|---|---|---|
| `(a+)+`, `(\w+\s?)*` | A quantified group containing a quantifier: many ways to split the same text | `^\w+(?:\s\w+)*$` (each character can be matched only one way) |
| `(a\|a)*`, `(\w\|\d)+` | Overlapping alternatives | Make the alternatives mutually exclusive: `\w+` |
| `.*x.*y.*` on long input | Many `.*` try every split | Use negated classes: `[^x]*x[^y]*y` |

```js
const SAFE = /^\w+(?:\s\w+)*$/;
SAFE.test("hello big world");               // → true
SAFE.test("a".repeat(100_000) + "!");       // → false  (answers instantly)
```

**Defences, from most to least important:**

1. **Cap input length** before any regex runs (body-size limits, `maxLength`, schema `.max()`).
2. **Never build a regex from user input** without `RegExp.escape`.
3. **Write patterns where each character can match only one way**: no nested quantifiers, no overlapping alternatives, and negated classes instead of `.*`.
4. **Lint for it.** `eslint-plugin-regexp` has a `no-super-linear-backtracking` rule; `recheck` analyses individual patterns.
5. **Use a linear-time engine for untrusted patterns.** The `re2` npm package (Google RE2) guarantees linear time but has no backreferences or lookarounds. V8 also has an experimental linear engine: run `node --enable-experimental-regexp-engine` and add the `l` flag (`/^(a+)+$/l` answers instantly).
6. For user-supplied **patterns** (search filters, rules engines), run them in a worker thread with a timeout, or accept only a limited glob syntax.

### Handy recipes

```js
// Collapse whitespace
"  too    many   spaces ".trim().replace(/\s+/g, " ");        // → "too many spaces"

// Slug: drop accents on LATIN letters only, keep letters/marks/digits, hyphenate
const slugify = (s) => s.normalize("NFKD")
  .replace(/(\p{Script=Latin})\p{M}+/gu, "$1")        // é → e, but Devanagari/Tamil vowel signs stay
  .normalize("NFC").toLowerCase()
  .replace(/[^\p{L}\p{M}\p{N}]+/gu, "-").replace(/^-+|-+$/g, "");
slugify("  Crème Brûlée: 10 Recipes!  ");                     // → "creme-brulee-10-recipes"
slugify("नमस्ते दुनिया");                                        // → "नमस्ते-दुनिया"
// (Stripping every \p{M} would give "नमसत-दनय": Hindi vowel signs are combining marks too)

// camelCase / PascalCase → snake_case, keeping acronyms together
const toSnake = (s) => s.replace(/([A-Z]+)([A-Z][a-z])/g, "$1_$2").replace(/([a-z\d])([A-Z])/g, "$1_$2").toLowerCase();
[toSnake("userId"), toSnake("XMLHttpRequest"), toSnake("parseJSON2Data")];   // → ["user_id", "xml_http_request", "parse_json2_data"]

// Hashtags in any script
"Loving #JavaScript and #हिंदी #2026!".match(/#[\p{L}\p{M}\p{N}_]+/gu);   // → ["#JavaScript", "#हिंदी", "#2026"]

// Template interpolation with a callback (unknown keys stay visible)
const render = (tpl, data) => tpl.replace(/\{\{\s*(\w+)\s*\}\}/g, (m, key) => (key in data ? String(data[key]) : m));
render("Hi {{ name }}, you owe {{amount}} {{currency}}", { name: "Asha", amount: 500 });   // → "Hi Asha, you owe 500 {{currency}}"
```

Use plain string methods when they're enough. `s.startsWith("http")`, `s.includes("@")`, `s.split(",")` and `s.replaceAll("-", "")` are clearer and faster than the regex versions.

### Interview coding question: highlight search matches

Split with a **capturing** group: the matches land at the odd indexes of the result.

```js
const escapeRe = RegExp.escape ?? ((s) => s.replace(/[.*+?^${}()|[\]\\/]/g, "\\$&"));

function highlightParts(text, query) {
  if (!query.trim()) return [{ text, match: false }];
  return text
    .split(new RegExp(`(${escapeRe(query)})`, "gi"))
    .map((part, i) => ({ text: part, match: i % 2 === 1 }))
    .filter((p) => p.text !== "");
}

highlightParts("C++ and c++ (not C#)", "c++").map((p) => (p.match ? `[${p.text}]` : p.text)).join("");
// → "[C++] and [c++] (not C#)"
```

In React, render each part as `<mark>{p.text}</mark>` or `{p.text}`. This returns parts rather than an HTML string, so there's no `dangerouslySetInnerHTML` and no XSS.

### Output questions

```js
const r = /o/g;
console.log(r.test("foo"), r.test("foo"), r.test("foo"));   // true true false (lastIndex: 2, 3, then reset)
console.log("aaa".replace("a", "b"));                       // "baa": a string pattern replaces only the first
console.log("x".replace(/x/, "$&$&"));                      // "xx"
console.log("abc".match(/z/)?.length ?? 0);                 // 0 (match returns null, not [])
console.log("2026".split(/(\d)/).length);                   // 9: 4 digits captured + 5 empty strings around them
```

### Interview Qs

1. Greedy vs lazy quantifiers? → Greedy takes as much as possible and gives back; lazy takes as little as possible. A negated class is often better than either.
2. Why does `re.test()` alternate between `true` and `false`? → `g`/`y` make it stateful through `lastIndex`. Don't use `g` with `test`.
3. `match` vs `matchAll` vs `exec`? → `match` with `g` gives strings only; `matchAll` gives full match objects (groups, index); `exec` is the low-level loop.
4. Lookahead vs lookbehind? → Assertions about what follows or precedes a position, without consuming characters.
5. Capturing vs non-capturing vs named groups? → Captures are stored (`$1`); `(?:…)` only groups; named groups (`(?<n>…)`) are readable and resilient to reordering.
6. How do you build a regex from user input safely? → `RegExp.escape` (or the escape fallback), plus a length cap.
7. What is ReDoS? How do you prevent it? → Exponential backtracking from nested or overlapping quantifiers. Cap input length, avoid dangerous shapes, lint, or use RE2 / a linear engine.
8. What do the `u` and `v` flags change? → `u`: code points, `\p{…}`, strict escapes. `v`: `u` plus class set operations and emoji-sequence properties, with stricter class syntax.
9. Why can the `m` flag break validation? → `^` and `$` then match per line, so one valid line passes.
10. When should you NOT use a regex? → HTML, JSON, URLs, dates or anything nested: use a parser. Simple checks: use string methods.
11. How does `split` treat capture groups? → Captured text is included in the resulting array.
12. What does the `y` flag do? → Matches only at `lastIndex`, which is the basis of tokenizers.

---

## 48. Networking for Frontend: What Happens When You Type a URL

The classic interview question, and the foundation for understanding performance, caching, CORS and security. It covers everything between pressing Enter and seeing pixels.

### Anatomy of a URL

```
https://shop.example.com:443/products/42?color=red&size=m#reviews
└─┬─┘   └──────┬───────┘└┬┘└────┬─────┘└──────┬────────┘└──┬──┘
scheme       host       port   path          query       fragment (never sent to server)
```

- **Origin** = scheme + host + port → `https://shop.example.com:443`. Same-origin policy, CORS, cookies and storage are all scoped by origin (cookies by domain/site).
- **Site** = scheme + registrable domain (`example.com`) → used by `SameSite` cookies.

```js
const url = new URL("https://shop.example.com/products/42?color=red#reviews");
url.origin;                     // "https://shop.example.com"
url.searchParams.get("color");  // "red"
url.hash;                       // "#reviews"
```

### The full journey (step by step)

**1. Browser processes the input**
- Is it a URL or a search term? Adds `https://` if missing.
- **HSTS** check: if the domain is on the HSTS list, the browser forces HTTPS without trying HTTP.
- Checks for a **Service Worker** that may answer from cache (PWAs).
- Checks the **HTTP cache** (memory/disk) — a fresh cached response means no network at all.

**2. DNS resolution** — turn `shop.example.com` into an IP address
1. Browser DNS cache → 2. OS cache (`/etc/hosts`) → 3. Router → 4. **Recursive resolver** (ISP, 8.8.8.8, 1.1.1.1), which asks:
   - **Root** server → "ask the `.com` TLD servers"
   - **TLD** server → "ask example.com's authoritative nameserver"
   - **Authoritative** nameserver → "shop.example.com = 93.184.216.34"
5. Result cached according to the record's **TTL**.

Record types: `A` (IPv4), `AAAA` (IPv6), `CNAME` (alias), `MX` (mail), `TXT` (verification, SPF), `NS` (nameservers).

**3. TCP connection** — 3-way handshake (1 round trip)
```
Client → SYN → Server
Client ← SYN-ACK ← Server
Client → ACK → Server        (connection open)
```

**4. TLS handshake** (HTTPS) — agree on encryption and verify identity
- Client sends supported ciphers + key share (**ClientHello**).
- Server sends its **certificate** + key share (**ServerHello**).
- Browser verifies the certificate chain (signed by a trusted Certificate Authority, domain matches, not expired/revoked).
- Both derive the same symmetric session key → encrypted from now on.
- **TLS 1.3**: 1 round trip (0-RTT on resumption). TLS 1.2 needed 2.

TLS gives: **confidentiality** (encryption), **integrity** (no tampering), **authentication** (you're really talking to that server).

**5. HTTP request**
```
GET /products/42?color=red HTTP/2
Host: shop.example.com
User-Agent: Mozilla/5.0 ...
Accept: text/html
Accept-Encoding: gzip, br
Cookie: session=abc123
If-None-Match: "v5-etag"
```

**6. Server side**
- Usually hits a **CDN edge** first (may serve cached content directly).
- Then **load balancer** → **reverse proxy** (Nginx) → **app server** (Node/FastAPI) → DB/cache → response.

**7. HTTP response**
```
HTTP/2 200
Content-Type: text/html; charset=utf-8
Content-Encoding: br
Cache-Control: no-cache
ETag: "v6-etag"
Set-Cookie: session=abc123; HttpOnly; Secure; SameSite=Lax
Content-Security-Policy: default-src 'self'
```

**8. Browser renders the page (Critical Rendering Path)**
1. **Parse HTML → DOM** (incrementally, as bytes arrive).
2. Discover subresources (CSS, JS, images, fonts) — the **preload scanner** starts fetching them early.
3. **Parse CSS → CSSOM**. CSS is **render-blocking** (no paint until CSSOM is ready).
4. **JavaScript**: a normal `<script>` **blocks HTML parsing** (downloads + executes). `defer`/`async`/`type="module"` avoid that.
5. **Render tree** = DOM + CSSOM (only visible nodes).
6. **Layout (reflow)** — compute size and position of every box.
7. **Paint** — fill pixels (text, colors, images, shadows) into layers.
8. **Composite** — GPU combines layers → pixels on screen.
9. Events: `DOMContentLoaded` (DOM parsed, deferred scripts run) → `load` (all resources loaded).

**9. After load** — JS hydrates/attaches handlers, lazy resources load, connections stay open (keep-alive) for reuse.

```
Enter → [cache/SW] → DNS → TCP → TLS → HTTP request → server/CDN → response
      → HTML parse → DOM + CSSOM → render tree → layout → paint → composite → 🎉
```

---

### HTTP essentials

**Methods**: GET (read, cacheable), POST (create), PUT (replace), PATCH (partial update), DELETE, HEAD (headers only), OPTIONS (CORS preflight).

**Status code families**

| Range | Meaning | Common |
|---|---|---|
| 1xx | Informational | 101 Switching Protocols (WebSocket), 103 Early Hints |
| 2xx | Success | 200 OK, 201 Created, 204 No Content, 206 Partial Content (video/range) |
| 3xx | Redirect / cache | 301 Moved Permanently, 302 Found, 304 Not Modified, 307/308 (keep method) |
| 4xx | Client error | 400, 401 Unauthenticated, 403 Forbidden, 404, 405, 409 Conflict, 413 Too Large, 422, 429 Too Many Requests |
| 5xx | Server error | 500, 502 Bad Gateway, 503 Unavailable, 504 Gateway Timeout |

**Important headers**

| Header | Purpose |
|---|---|
| `Content-Type` | Body format (`application/json`, `text/html`, `multipart/form-data`) |
| `Accept`, `Accept-Encoding`, `Accept-Language` | Content negotiation |
| `Authorization` | `Bearer <token>`, `Basic ...` |
| `Cookie` / `Set-Cookie` | Session state |
| `Cache-Control`, `ETag`, `Last-Modified`, `If-None-Match`, `Vary` | Caching |
| `Origin`, `Access-Control-Allow-*` | CORS |
| `Content-Security-Policy`, `Strict-Transport-Security`, `X-Content-Type-Options` | Security |
| `Location` | Redirect target / created resource URL |
| `Retry-After` | With 429/503 |

### HTTP/1.1 vs HTTP/2 vs HTTP/3

| | HTTP/1.1 | HTTP/2 | HTTP/3 |
|---|---|---|---|
| Transport | TCP | TCP | **QUIC over UDP** |
| Format | Text | Binary frames | Binary frames |
| Parallel requests | ~6 connections per host, one request at a time each | **Multiplexing**: many streams on one connection | Multiplexing with independent streams |
| Head-of-line blocking | Yes (per connection) | Fixed at HTTP level, still at TCP level (one lost packet stalls all streams) | **Fixed** (streams independent) |
| Header compression | No | HPACK | QPACK |
| Handshake | TCP + TLS | TCP + TLS | Combined, 1-RTT (0-RTT resume) |
| Connection migration (Wi-Fi → 4G) | No | No | **Yes** (connection IDs) |

Impact on frontend practices:
- HTTP/1.1 era hacks (domain sharding, sprite sheets, concatenating everything into one bundle) are **less necessary** with HTTP/2+. Moderate code-splitting is fine.
- Fewer origins = fewer DNS/TCP/TLS handshakes → self-host critical fonts/scripts or `preconnect`.

---

### HTTP Caching (very important for performance)

**Cache-Control directives**

| Directive | Meaning |
|---|---|
| `max-age=N` | Fresh for N seconds (no request at all) |
| `s-maxage=N` | Max age for shared caches (CDN) |
| `no-cache` | Can store, but must **revalidate** with the server every time (ETag → 304) |
| `no-store` | Never store (sensitive data: banking, personal pages) |
| `private` | Only the browser may cache (not CDNs) — user-specific data |
| `public` | Any cache may store |
| `immutable` | Won't change during max-age — don't even revalidate on reload |
| `stale-while-revalidate=N` | Serve stale while fetching a fresh copy in the background |
| `must-revalidate` | Once stale, must revalidate before use |

**Revalidation (conditional requests)**

```
1st request:  200 OK   ETag: "abc"       (body sent)
Later:        GET ... If-None-Match: "abc"
Response:     304 Not Modified            (no body → saves bandwidth)
```
(`Last-Modified` / `If-Modified-Since` works the same with dates.)

**The standard strategy for a web app**

| Resource | Header | Why |
|---|---|---|
| Hashed assets `app.3f9a1c.js`, `logo.8b2e.png` | `Cache-Control: public, max-age=31536000, immutable` | Filename changes when content changes → cache forever |
| `index.html` | `Cache-Control: no-cache` | Always check for a new deploy (which references new hashed files) |
| Public API data | `Cache-Control: public, max-age=60, stale-while-revalidate=300` | Short freshness, fast responses |
| User-specific API data | `Cache-Control: private, no-cache` or `no-store` | Never cached by CDNs |

```js
// Express example
app.use("/assets", express.static("dist/assets", { maxAge: "1y", immutable: true }));
app.get("*", (req, res) => {
  res.set("Cache-Control", "no-cache");
  res.sendFile(path.resolve("dist/index.html"));
});
```

**`Vary` header**: tells caches the response depends on a request header (`Vary: Accept-Encoding`, `Vary: Origin`) so they store separate copies.

**Cache layers**: memory cache → HTTP disk cache → Service Worker cache → CDN edge → reverse proxy cache → app cache (Redis) → DB.

**Service Worker strategies**: cache-first (static assets), network-first (HTML/API), stale-while-revalidate (avatars, non-critical data).

---

### CDN (Content Delivery Network)

A global network of edge servers that cache content close to users (Cloudflare, CloudFront, Fastly, Akamai).

- Lower latency (fewer km → fewer ms), less load on origin servers.
- DDoS protection, TLS termination, HTTP/3, image optimization, edge functions.
- Cache invalidation via hashed filenames (best) or purge APIs.

---

### Resource hints & loading priorities

```html
<!-- Start DNS + TCP + TLS early for a critical third-party origin -->
<link rel="preconnect" href="https://api.example.com" crossorigin>
<link rel="dns-prefetch" href="https://analytics.example.com">

<!-- Fetch a critical resource for THIS page early (fonts, hero image, critical CSS) -->
<link rel="preload" href="/fonts/inter.woff2" as="font" type="font/woff2" crossorigin>
<link rel="preload" href="/hero.avif" as="image" fetchpriority="high">
<link rel="modulepreload" href="/assets/app.js">

<!-- Low-priority fetch for the NEXT navigation -->
<link rel="prefetch" href="/checkout.js">

<!-- Priority hints -->
<img src="hero.avif" fetchpriority="high" alt="">
<img src="footer.png" loading="lazy" fetchpriority="low" alt="">

<!-- Scripts -->
<script src="app.js" defer></script>            <!-- parallel download, runs after parsing, in order -->
<script src="analytics.js" async></script>      <!-- runs as soon as downloaded, any order -->
<script type="module" src="main.js"></script>   <!-- deferred by default -->
```

### Compression

- **gzip** (universal) and **Brotli** (`br`, ~15–20% smaller for text) for HTML/CSS/JS/JSON/SVG.
- Don't compress already-compressed formats (JPEG, PNG, WebP, MP4, WOFF2).
- Usually done by the CDN/reverse proxy.

---

### Optimizing the Critical Rendering Path (checklist)

1. **Reduce round trips**: fewer origins, `preconnect`, HTTP/2+, CDN, 103 Early Hints.
2. **Smaller critical bytes**: minify, compress (Brotli), tree-shake, code-split, remove unused CSS.
3. **Unblock rendering**: inline critical CSS, load the rest async; `defer` scripts; avoid synchronous third-party scripts in `<head>`.
4. **Prioritize the LCP element**: preload/`fetchpriority="high"` the hero image; don't lazy-load it.
5. **Fonts**: `font-display: swap`, preload the main font, subset fonts, self-host.
6. **Images**: modern formats (AVIF/WebP), responsive `srcset`/`sizes`, explicit `width`/`height` (prevents CLS), lazy-load below the fold.
7. **Avoid layout thrashing** and long JS tasks (keeps INP low).
8. **SSR/SSG** for content-heavy pages so HTML arrives ready to paint.

**Core Web Vitals**: **LCP** (Largest Contentful Paint, loading, ≤ 2.5s), **INP** (Interaction to Next Paint, responsiveness, ≤ 200ms), **CLS** (Cumulative Layout Shift, visual stability, ≤ 0.1). Also **TTFB** and **FCP**.

---

### Reading the DevTools Network tab

Timing phases for each request:
- **Queueing/Stalled** — waiting for a connection slot or lower priority.
- **DNS Lookup**, **Initial connection** (TCP), **SSL** (TLS).
- **Request sent**.
- **Waiting (TTFB)** — server think time + network latency. High TTFB → slow backend/DB, no CDN caching.
- **Content Download** — large payload or slow network.

Tips: throttle to "Fast 4G"/"Slow 3G", disable cache to test cold loads, check the **Size** column ("disk cache", "memory cache", "service worker"), look at the **waterfall** for request chains (A waits for B waits for C = waterfall problem).

---

### Other networking concepts worth knowing

- **IP, TCP vs UDP**: TCP = reliable, ordered, connection-based (HTTP/1.1, HTTP/2, WebSockets). UDP = fast, no guarantees (video calls, gaming, DNS, QUIC/HTTP/3).
- **Latency vs bandwidth**: latency = time per round trip (distance, handshakes); bandwidth = data per second. Web performance is usually **latency-bound** → reduce round trips.
- **Keep-alive**: reuse TCP connections for multiple requests.
- **WebSockets / SSE / long polling** — real-time options (see Node notes: WebSockets & Real-time).
- **CORS** and preflight (see Security Basics).
- **Cookies**: `HttpOnly`, `Secure`, `SameSite`, `Domain`, `Path` (see Browser Storage & Cookies).
- **Proxy vs reverse proxy**: a forward proxy acts for clients (corporate proxy); a reverse proxy acts for servers (Nginx, load balancer, CDN).
- **Load balancing**: round robin, least connections, IP hash (sticky sessions); L4 (TCP) vs L7 (HTTP) balancers.
- **REST vs GraphQL vs gRPC vs tRPC** — API styles over HTTP.

### Interview Qs

1. **What happens when you type a URL and press Enter?** → Cache/SW check → DNS → TCP → TLS → HTTP request → server/CDN → response → parse HTML/CSS → DOM/CSSOM → render tree → layout → paint → composite.
2. **How does DNS resolution work?** → Browser/OS cache → recursive resolver → root → TLD → authoritative; cached by TTL.
3. **What does TLS provide? Describe the handshake.**
4. **HTTP/1.1 vs HTTP/2 vs HTTP/3?** → Multiplexing, header compression, QUIC/UDP removes TCP head-of-line blocking.
5. **Explain HTTP caching: `no-cache` vs `no-store`, ETag, 304.**
6. **How would you cache a React/Vite build?** → Hashed assets immutable for 1 year; `index.html` `no-cache`.
7. **What is the critical rendering path? What blocks rendering?** → CSS blocks render; sync JS blocks parsing.
8. **`async` vs `defer` vs `module` scripts?**
9. **`preload` vs `prefetch` vs `preconnect`?** → Current page critical resource / next navigation / early connection setup.
10. **What is a CDN and why use it?**
11. **What is TTFB and what makes it high?**
12. **TCP vs UDP?**
13. **What are Core Web Vitals and how do you improve them?**
14. **301 vs 302 vs 307 vs 308?** → Permanent vs temporary; 307/308 preserve the HTTP method and body.
15. **What is HSTS?** → Header telling browsers to only use HTTPS for the domain (prevents SSL-stripping downgrade attacks).

---

## 49. Performance Concepts

- **Debounce/throttle** frequent events.
- **Lazy loading** (images with `loading="lazy"`, dynamic `import()`).
- **Code splitting & tree shaking**.
- **Memoization** for expensive pure functions.
- **Avoid layout thrashing**; batch DOM reads then writes.
- **Virtualization** for long lists (render only visible rows).
- **Web Workers** for CPU-heavy work.
- **Caching**: HTTP cache, service workers, CDN.
- **Critical rendering path**: minimise render-blocking CSS/JS, `defer` scripts, preload key assets.
- **Core Web Vitals**: LCP (loading), INP (interactivity), CLS (visual stability).
- Measure with `performance.now()`, `performance.mark/measure`, Lighthouse, DevTools Performance tab.

```js
const t0 = performance.now();
heavyTask();
console.log(`took ${performance.now() - t0}ms`);
```

---

## 50. Security Basics

### XSS (Cross-Site Scripting)

Attacker injects script into your page (e.g. via user input rendered as HTML).

```js
// ❌ vulnerable
comment.innerHTML = userInput; // "<img src=x onerror=alert(document.cookie)>"
// ✅ safe
comment.textContent = userInput;
// If HTML is required: sanitize (DOMPurify) + Content-Security-Policy header.
```

### CSRF (Cross-Site Request Forgery)

A malicious site makes the victim's browser send an authenticated request (cookies auto-attached). Defenses: `SameSite` cookies, CSRF tokens, checking `Origin` header.

### CORS (Cross-Origin Resource Sharing)

Browsers block JS from reading responses from a different origin (protocol + host + port) unless the server allows it with headers like `Access-Control-Allow-Origin`. Non-simple requests (PUT, custom headers, JSON content type) trigger a **preflight** `OPTIONS` request first. CORS is enforced by the **browser**, not the server.

### Other

- Never use `eval` / `new Function` with user input.
- Prototype pollution: don't merge untrusted objects into objects blindly (`__proto__` keys).
- Clickjacking: `X-Frame-Options` / CSP `frame-ancestors`.

---

## 51. Modern JS Features

| Version | Key features |
|---|---|
| **ES6 / ES2015** | let/const, arrow fns, classes, template literals, destructuring, default/rest/spread, Promises, modules, Map/Set, Symbol, iterators, generators, `for...of`, Proxy/Reflect |
| ES2016 | `Array.prototype.includes`, `**` exponent |
| ES2017 | async/await, `Object.values/entries`, `padStart/padEnd` |
| ES2018 | Rest/spread for objects, `Promise.finally`, async iteration, regex named groups |
| ES2019 | `flat`, `flatMap`, `Object.fromEntries`, `trimStart/End`, optional catch binding |
| ES2020 | `?.`, `??`, BigInt, `Promise.allSettled`, `globalThis`, dynamic `import()` |
| ES2021 | `replaceAll`, `Promise.any`, `??= ||= &&=`, numeric separators, WeakRef |
| ES2022 | Class fields & private `#`, top-level await, `.at()`, `Object.hasOwn`, error `cause` |
| ES2023 | `findLast`, `toSorted`, `toReversed`, `toSpliced`, `with` |
| ES2024 | `Object.groupBy`, `Map.groupBy`, `Promise.withResolvers`, well-formed strings |
| ES2025 | Iterator helpers, Set methods (`union`, `intersection`…), `RegExp.escape`, JSON modules, `Promise.try` |

---

## 52. Polyfill Collection

Quick list of polyfills/implementations interviewers ask. Most are written above:
- `map`, `filter`, `reduce`, `forEach`, `flat` → Section 20
- `call`, `apply`, `bind` → Section 13
- `Promise.all`, `allSettled`, `race`, `any`, custom Promise → Section 27
- `debounce`, `throttle` → Section 24
- `curry`, `compose`, `pipe` → Section 22
- `memoize`, `once` → Section 11
- `deepClone`, `deepEqual`, `flattenObj` → Sections 14–15
- `EventEmitter` → Section 41
- `new` operator, `instanceof` → Sections 12, 17

A few more:

```js
// Object.assign
Object.myAssign = function (target, ...sources) {
  const to = Object(target);
  for (const src of sources) {
    if (src == null) continue;
    for (const key of Reflect.ownKeys(src)) {
      if (Object.prototype.propertyIsEnumerable.call(src, key)) to[key] = src[key];
    }
  }
  return to;
};

// Object.create
function objectCreate(proto) {
  function F() {}
  F.prototype = proto;
  return new F();
}

// Array.prototype.some / every / find
Array.prototype.mySome = function (cb) {
  for (let i = 0; i < this.length; i++) if (i in this && cb(this[i], i, this)) return true;
  return false;
};
Array.prototype.myEvery = function (cb) {
  for (let i = 0; i < this.length; i++) if (i in this && !cb(this[i], i, this)) return false;
  return true;
};
Array.prototype.myFind = function (cb) {
  for (let i = 0; i < this.length; i++) if (cb(this[i], i, this)) return this[i];
};

// setInterval using setTimeout
function mySetInterval(fn, delay) {
  let id;
  const tick = () => { fn(); id = setTimeout(tick, delay); };
  id = setTimeout(tick, delay);
  return () => clearTimeout(id);
}

// JSON.stringify (simplified)
function stringify(v) {
  if (v === null) return "null";
  if (typeof v === "string") return `"${v.replace(/"/g, '\\"')}"`;
  if (typeof v === "number" || typeof v === "boolean") return Number.isFinite(v) || typeof v === "boolean" ? String(v) : "null";
  if (Array.isArray(v)) return `[${v.map((x) => (x === undefined || typeof x === "function" ? "null" : stringify(x))).join(",")}]`;
  if (typeof v === "object") {
    const parts = Object.entries(v)
      .filter(([, x]) => x !== undefined && typeof x !== "function" && typeof x !== "symbol")
      .map(([k, x]) => `"${k}":${stringify(x)}`);
    return `{${parts.join(",")}}`;
  }
}

// get(obj, "a.b[0].c") like lodash
function get(obj, path, fallback) {
  const keys = path.replace(/\[(\d+)\]/g, ".$1").split(".");
  let cur = obj;
  for (const k of keys) {
    if (cur == null) return fallback;
    cur = cur[k];
  }
  return cur === undefined ? fallback : cur;
}
get({ a: { b: [{ c: 5 }] } }, "a.b[0].c"); // 5

// LRU cache (Map keeps insertion order)
class LRUCache {
  constructor(cap) { this.cap = cap; this.map = new Map(); }
  get(k) {
    if (!this.map.has(k)) return -1;
    const v = this.map.get(k);
    this.map.delete(k); this.map.set(k, v);
    return v;
  }
  put(k, v) {
    this.map.delete(k);
    this.map.set(k, v);
    if (this.map.size > this.cap) this.map.delete(this.map.keys().next().value);
  }
}
```

---

## 53. Testing JavaScript (Vitest / Jest)

Tests let you change code without fear. Examples use **Vitest** (the default for Vite projects); **Jest** has almost the same API (`vi.fn()` ↔ `jest.fn()`). React component testing is in `react.md`, API testing in `nodejs.md`.

### 1. What to test

| Level | What | Speed | Tools |
|---|---|---|---|
| **Unit** | One function/module in isolation (pure logic) | ms | Vitest/Jest |
| **Integration** | Several units together (component + hooks + mocked network; route + DB) | 10–100 ms | Vitest + Testing Library + MSW, Supertest |
| **End-to-end** | The real app in a browser, like a user | seconds | Playwright, Cypress |

The **testing trophy**: some unit tests for tricky logic, **most** tests at the integration level, a few E2E tests for critical journeys (login, checkout), plus static checks (TypeScript, ESLint) at the base.

Test **behaviour** (inputs → outputs, what the user sees), **edge cases** (empty, zero, negative, max, null, unicode, time zones), **error paths**, and every **bug you fix** (regression test).

### 2. Setup & anatomy of a test

```bash
npm i -D vitest
# package.json → "scripts": { "test": "vitest", "test:run": "vitest run", "coverage": "vitest run --coverage" }
```

```js
// src/utils/slugify.js
export function slugify(text) {
  return text
    .normalize("NFKD")
    .replace(/(\p{Script=Latin})\p{M}+/gu, "$1")      // remove accents from Latin letters (é → e)
    .normalize("NFC")
    .toLowerCase()
    .replace(/[^\p{L}\p{M}\p{N}]+/gu, "-")            // anything that isn't a letter, mark or digit → dash
    .replace(/^-+|-+$/g, "");                          // trim dashes
}
```

```js
// src/utils/slugify.test.js   (files named *.test.js / *.spec.js are picked up automatically)
import { describe, it, expect } from "vitest";
import { slugify } from "./slugify.js";

describe("slugify", () => {
  it("lowercases and joins words with dashes", () => {
    // Arrange → Act → Assert (AAA)
    const input = "Hello World";
    const result = slugify(input);
    expect(result).toBe("hello-world");
  });

  it("removes accents and special characters", () => {
    expect(slugify("Café & Crème!")).toBe("cafe-creme");
  });

  it("trims leading/trailing separators", () => {
    expect(slugify("  --Hi--  ")).toBe("hi");
  });

  it("returns an empty string for input without letters or digits", () => {
    expect(slugify("!!!")).toBe("");
  });

  it("keeps non-Latin scripts intact", () => {
    expect(slugify("नमस्ते दुनिया")).toBe("नमस्ते-दुनिया");      // an ASCII-only [^a-z0-9] slug would return ""
  });
});
```

Name tests as **behaviour sentences** ("returns an empty string for …") so failures read like bug reports.

### 3. Matchers you'll use daily

```js
expect(2 + 2).toBe(4);                                 // strict equality (Object.is) — primitives
expect({ a: 1, b: { c: 2 } }).toEqual({ a: 1, b: { c: 2 } });   // deep equality — objects/arrays
expect(result).toStrictEqual(expected);                // also checks undefined props & class types
expect(user).toMatchObject({ name: "Rohit" });         // subset match
expect([1, 2, 3]).toContain(2);
expect(list).toHaveLength(3);
expect(0.1 + 0.2).toBeCloseTo(0.3);                    // floats!
expect(value).toBeNull(); expect(value).toBeDefined(); expect(value).toBeTruthy();
expect("hello world").toMatch(/world/);
expect(() => parse("bad")).toThrow("Invalid input");   // wrap the call in a function
expect(order).not.toHaveProperty("password");

// Asymmetric matchers for "any value of this shape"
expect(createUser("a@b.com")).toEqual({
  id: expect.any(String),
  email: "a@b.com",
  createdAt: expect.any(Date),
});
expect(log).toHaveBeenCalledWith(expect.stringContaining("failed"), expect.objectContaining({ orderId: 7 }));
```

`toBe` on objects compares **references** — use `toEqual` for data.

### 4. Table-driven tests (`test.each`)

```js
// src/cart.js
export function cartTotal(items, { discountPct = 0 } = {}) {
  if (discountPct < 0 || discountPct > 100) throw new RangeError("discount must be 0–100");
  const subtotal = items.reduce((sum, i) => sum + i.pricePaise * i.qty, 0);
  return Math.round(subtotal * (1 - discountPct / 100));
}
```

```js
import { test, expect } from "vitest";
import { cartTotal } from "./cart.js";

test.each([
  { items: [], discountPct: 0, expected: 0 },
  { items: [{ pricePaise: 1000, qty: 2 }], discountPct: 0, expected: 2000 },
  { items: [{ pricePaise: 999, qty: 3 }], discountPct: 10, expected: 2697 },   // rounding
  { items: [{ pricePaise: 500, qty: 1 }], discountPct: 100, expected: 0 },
])("cartTotal($items.length items, $discountPct%) = $expected", ({ items, discountPct, expected }) => {
  expect(cartTotal(items, { discountPct })).toBe(expected);
});

test("rejects invalid discounts", () => {
  expect(() => cartTotal([], { discountPct: 150 })).toThrow(RangeError);
});
```

### 5. Async code

```js
test("resolves with the user", async () => {
  await expect(getUser(1)).resolves.toMatchObject({ id: 1 });
});

test("rejects for a missing user", async () => {
  await expect(getUser(999)).rejects.toThrow("not found");
});

test("classic async/await form", async () => {
  const user = await getUser(1);
  expect(user.name).toBe("Rohit");
});
```

Always `await` (or `return`) the promise — otherwise the test finishes before the assertion runs and passes falsely.

### 6. Mocks, spies & stubs

**Prefer dependency injection** (pass collaborators in) — then tests just pass fakes, no module mocking needed.

```js
// src/userService.js — dependencies injected
export function createUserService({ fetchFn, logger }) {
  return {
    async getUser(id) {
      const res = await fetchFn(`/api/users/${id}`);
      if (!res.ok) {
        logger.error("user fetch failed", { id, status: res.status });
        throw new Error(`User ${id} not found`);
      }
      return res.json();
    },
  };
}
```

```js
import { test, expect, vi } from "vitest";
import { createUserService } from "./userService.js";

test("returns the user from the API", async () => {
  const fetchFn = vi.fn().mockResolvedValue({ ok: true, json: async () => ({ id: 1, name: "Rohit" }) });
  const service = createUserService({ fetchFn, logger: { error: vi.fn() } });

  await expect(service.getUser(1)).resolves.toEqual({ id: 1, name: "Rohit" });
  expect(fetchFn).toHaveBeenCalledOnce();
  expect(fetchFn).toHaveBeenCalledWith("/api/users/1");
});

test("logs and throws on 404", async () => {
  const logger = { error: vi.fn() };
  const service = createUserService({ fetchFn: vi.fn().mockResolvedValue({ ok: false, status: 404 }), logger });

  await expect(service.getUser(9)).rejects.toThrow("User 9 not found");
  expect(logger.error).toHaveBeenCalledWith("user fetch failed", { id: 9, status: 404 });
});
```

```js
// vi.fn — a fake function that records calls
const cb = vi.fn();
cb.mockReturnValue(42);                    // or mockReturnValueOnce, mockResolvedValue, mockRejectedValue
cb.mockImplementation((x) => x * 2);
cb.mock.calls;                             // [[arg1, arg2], ...]

// vi.spyOn — watch (and optionally replace) an existing method
const spy = vi.spyOn(console, "error").mockImplementation(() => {});   // silence + assert
expect(spy).toHaveBeenCalledTimes(1);
spy.mockRestore();

// vi.mock — replace a whole module (hoisted to the top of the file)
vi.mock("./emailClient.js", () => ({ sendEmail: vi.fn().mockResolvedValue({ ok: true }) }));

// Globals
vi.stubGlobal("fetch", vi.fn());
vi.stubEnv("API_URL", "http://test");
```

Use `afterEach(() => vi.restoreAllMocks())` (or `restoreMocks: true` in config) so mocks don't leak between tests. For network-heavy code, **MSW** (Mock Service Worker) mocks at the HTTP level — more realistic than mocking `fetch` per test.

### 7. Time: fake timers & fixed dates

```js
import { beforeEach, afterEach, test, expect, vi } from "vitest";

beforeEach(() => vi.useFakeTimers());
afterEach(() => vi.useRealTimers());

test("retries after the backoff delay", async () => {
  const task = vi.fn().mockRejectedValueOnce(new Error("flaky")).mockResolvedValue("ok");
  const promise = retry(task, { retries: 1, delayMs: 1000 });

  await vi.advanceTimersByTimeAsync(1000);        // fast-forward without really waiting
  await expect(promise).resolves.toBe("ok");
  expect(task).toHaveBeenCalledTimes(2);
});

test("trial expires after 14 days", () => {
  vi.setSystemTime(new Date("2026-01-15T00:00:00Z"));   // Date.now() / new Date() now return this
  expect(isTrialExpired({ trialEndsAt: "2026-01-14T00:00:00Z" })).toBe(true);
});
```

Never `await sleep(1000)` in tests — slow and flaky. (Debounce/throttle tests with fake timers: see Debounce & Throttle.)

### 8. Setup, teardown & isolation

```js
import { beforeAll, afterAll, beforeEach, afterEach } from "vitest";

let db;
beforeAll(async () => { db = await createTestDb(); });   // once per file (expensive setup)
afterAll(async () => { await db.close(); });
beforeEach(async () => { await db.reset(); });           // fresh state for EVERY test
afterEach(() => vi.restoreAllMocks());
```

Each test must pass **alone and in any order** — no shared mutable state between tests.

### 9. Testing DOM code

```js
// vitest.config.js → test: { environment: "jsdom" }   (or "happy-dom")
import { screen } from "@testing-library/dom";
import userEvent from "@testing-library/user-event";
import { mountCounter } from "./counter.js";

test("increments when clicked", async () => {
  document.body.innerHTML = `<div id="app"></div>`;
  mountCounter(document.getElementById("app"));
  const user = userEvent.setup();

  await user.click(screen.getByRole("button", { name: /count: 0/i }));
  expect(screen.getByRole("button", { name: /count: 1/i })).toBeTruthy();
});
```

Query by **role/label/text** (what users see), not by CSS classes or IDs.

### 10. Snapshots — use sparingly

```js
expect(formatInvoice(order)).toMatchInlineSnapshot(`"INV-0007 • ₹2,697.00 • PAID"`);
```

Good for small, stable outputs (formatters, error messages, generated config). Bad for large component trees: huge snapshots get rubber-stamped with `-u` and stop catching bugs.

### 11. Coverage

```bash
vitest run --coverage        # v8 coverage: statements, branches, functions, lines
```

- Coverage shows what's **not** tested; high coverage doesn't prove tests are good.
- Look at **branch** coverage for important logic (both sides of every `if`).
- Set a reasonable floor in CI (e.g. 70–80%) and focus on critical modules rather than chasing 100%.

### 12. TDD — Red → Green → Refactor

1. **Red**: write a failing test for the next small behaviour.
2. **Green**: write the simplest code that makes it pass.
3. **Refactor**: clean up while the tests stay green.

```js
// 1. RED
test("password is weak when shorter than 8 characters", () => {
  expect(passwordStrength("abc")).toBe("weak");
});
// 2. GREEN
export const passwordStrength = (pw) => (pw.length < 8 ? "weak" : "ok");
// 3. next RED: "strong when it has 12+ chars with digits and symbols" … and so on
```

TDD shines for business rules, parsers and bug fixes (write the failing test that reproduces the bug first).

### 13. Node's built-in test runner

No dependencies needed for small libraries/scripts:

```js
import { test, describe, mock } from "node:test";
import assert from "node:assert/strict";
import { slugify } from "./slugify.js";

describe("slugify", () => {
  test("joins words", () => assert.equal(slugify("Hello World"), "hello-world"));
  test("mock functions", () => {
    const fn = mock.fn(() => 1);
    fn();
    assert.equal(fn.mock.callCount(), 1);
  });
});
// node --test   (add --watch, --experimental-test-coverage)
```

### 14. Good tests vs bad tests

**F.I.R.S.T.**: **F**ast, **I**ndependent, **R**epeatable (same result every run), **S**elf-validating (pass/fail, no manual checking), **T**imely (written with the code).

| Anti-pattern | Why it hurts | Instead |
|---|---|---|
| Testing implementation details (private functions, internal state, CSS classes) | Breaks on every refactor | Test public behaviour/output |
| Mocking everything | Tests pass while the real integration is broken | Mock only boundaries (network, time, randomness) |
| Real network/time/randomness | Flaky tests | MSW, fake timers, seeded data |
| `sleep()` in tests | Slow & flaky | Fake timers, `findBy*` / `waitFor` |
| One giant test checking 10 things | Hard to see what broke | One behaviour per test |
| Shared state between tests | Order-dependent failures | Fresh setup in `beforeEach` |
| No assertion / not awaiting promises | False passes | `await expect(...)`, `expect.assertions(n)` |
| Snapshotting huge outputs | Rubber-stamped updates | Targeted assertions |

### 15. Tests in CI

- Run `vitest run` (not watch mode) on every PR; fail the build on failures.
- Run only affected tests locally (`vitest --changed`), everything in CI.
- Track and **fix flaky tests immediately** (quarantine if needed) — flaky tests destroy trust.
- Keep the suite fast (parallel by default in Vitest; avoid real I/O in unit tests).

### Interview Qs

1. Unit vs integration vs E2E tests? What is the testing trophy?
2. `toBe` vs `toEqual` vs `toStrictEqual`?
3. How do you test async code? What happens if you forget `await`?
4. Mock vs spy vs stub? When should you avoid mocking?
5. How do you test code that uses `setTimeout` or `Date.now()`?
6. How does dependency injection make testing easier?
7. What makes a test flaky and how do you fix it?
8. What is TDD? Describe red-green-refactor.
9. Is 100% coverage a good goal?
10. What are snapshot tests good and bad for?

---

## 54. Production-Grade JavaScript

Interview code and tutorials only have to work once. **Production code** has to keep working for years with real users, bad networks, bad input, multiple developers and 3am incidents. This section covers the patterns and habits used in real codebases.

### 1. Clean Code & Naming

```js
// ❌
const d = 86400000;
function proc(a, f) { return a.filter((x) => x.s === f).map((x) => x.n); }

// ✅
const MS_PER_DAY = 24 * 60 * 60 * 1000;
function getNamesByStatus(users, status) {
  return users.filter((user) => user.status === status).map((user) => user.name);
}
```

Rules that matter most:
- **Names reveal intent**: `isLoading`, `hasAccess`, `canEdit` (booleans), `getUser`/`fetchOrders`/`calculateTotal` (verbs for functions), `userList`/`usersById` (data shape).
- **No magic numbers/strings** → named constants (`MAX_RETRIES = 3`, `STATUS.ACTIVE`).
- **Small functions** that do one thing; a function name with "and" is a smell.
- **Early returns (guard clauses)** instead of deep nesting.
- **Max ~3 parameters** → use an options object beyond that.
- **Consistent style** enforced by tools (ESLint + Prettier), not code review arguments.
- **Comments explain *why*, not *what*** — the code already says what.

```js
// ❌ Arrow-shaped nested code
function processOrder(order) {
  if (order) {
    if (order.items.length > 0) {
      if (order.paid) {
        ship(order);
      } else { throw new Error("Not paid"); }
    } else { throw new Error("Empty"); }
  } else { throw new Error("No order"); }
}

// ✅ Guard clauses
function processOrder2(order) {
  if (!order) throw new Error("No order");
  if (order.items.length === 0) throw new Error("Empty order");
  if (!order.paid) throw new Error("Order not paid");
  ship(order);
}
```

```js
// ❌ Boolean trap & positional args
createUser("Rohit", "r@x.com", true, false, 30);

// ✅ Options object: self-documenting, order-independent, easy to extend
createUser({ name: "Rohit", email: "r@x.com", isAdmin: true, sendWelcomeEmail: false, trialDays: 30 });
function createUser({ name, email, isAdmin = false, sendWelcomeEmail = true, trialDays = 14 }) { /* ... */ }
```

```js
// ✅ Lookup tables instead of long if/else or switch
const STATUS_LABEL = { pending: "Pending", shipped: "On the way", delivered: "Delivered" };
const label = STATUS_LABEL[order.status] ?? "Unknown";
```

```js
// Comments: why, not what
// ❌ increment i by 1
i++;
// ✅ Razorpay sends amounts in paise, so convert before storing in rupees
const amountInRupees = payload.amount / 100;
```

### 2. Project Structure & Modules

- One module = one responsibility; export a small public API.
- Group by **feature** (`features/cart/`, `features/auth/`) rather than by type once the app grows.
- Keep **pure business logic** separate from I/O (DOM, fetch, DB) → easy to test.
- Avoid circular imports; avoid "utils.js" dumping grounds (split `date.js`, `money.js`, `string.js`).
- Barrel files (`index.js` re-exports) are convenient but can hurt tree-shaking and cause circular imports. Use them sparingly.

```
src/
  features/
    cart/
      cart.service.js     # business logic (pure where possible)
      cart.api.js         # network calls
      cart.store.js       # state
      cart.test.js
  lib/
    http.js               # fetch wrapper
    logger.js
    config.js
  utils/
    money.js
    date.js
```

### 3. Configuration & Environment

```js
// config.js — read, validate and freeze config in ONE place
const required = (name) => {
  const value = process.env[name];
  if (value === undefined || value === "") throw new Error(`Missing env var: ${name}`);
  return value;
};

export const config = Object.freeze({
  env: process.env.NODE_ENV ?? "development",
  apiUrl: required("API_URL"),
  requestTimeoutMs: Number(process.env.REQUEST_TIMEOUT_MS ?? 10_000),
  features: Object.freeze({
    newCheckout: process.env.FEATURE_NEW_CHECKOUT === "true",
  }),
});
// Fail fast at startup instead of crashing on the first request that needs a missing value.
```

- Never hard-code URLs, keys or secrets. Never commit `.env` (commit `.env.example`).
- Frontend env vars (`VITE_*`, `NEXT_PUBLIC_*`) are **public** — bundled into JS that anyone can read.
- Env values are **strings**: `"false"` is truthy! Parse explicitly.

### 4. Error Handling Strategy

**Principles**
1. **Never swallow errors silently.**
2. Catch errors **where you can do something useful** (retry, fallback, show a message). Otherwise let them bubble up.
3. **Throw `Error` objects** (with stack traces), never strings.
4. Distinguish **expected/operational errors** (validation, 404, network) from **bugs** (TypeError).
5. Show **friendly messages to users**, send **detailed errors to logs/monitoring**.
6. Add **context** when rethrowing (`cause`).
7. Have a **global safety net** (window `error`/`unhandledrejection`, Node process handlers, React error boundaries).

```js
// ❌ Swallowing — the bug disappears, data silently wrong
try { await saveOrder(order); } catch (e) {}

// ❌ Losing the original error
try { await saveOrder(order); } catch (e) { throw new Error("Save failed"); }

// ✅ Add context, keep the cause
try {
  await saveOrder(order);
} catch (err) {
  throw new Error(`Failed to save order ${order.id}`, { cause: err });
}
```

**Custom error hierarchy**

```js
export class AppError extends Error {
  constructor(message, { code = "INTERNAL", status = 500, details, cause, expose = false } = {}) {
    super(message, { cause });
    this.name = this.constructor.name;
    this.code = code;          // machine-readable, stable (for frontend logic/i18n)
    this.status = status;
    this.details = details;
    this.expose = expose;      // safe to show the message to users?
  }
}
export class ValidationError extends AppError {
  constructor(details) { super("Validation failed", { code: "VALIDATION_ERROR", status: 400, details, expose: true }); }
}
export class NotFoundError extends AppError {
  constructor(resource) { super(`${resource} not found`, { code: "NOT_FOUND", status: 404, expose: true }); }
}
export class NetworkError extends AppError {
  constructor(cause) { super("Network request failed", { code: "NETWORK", status: 0, cause }); }
}

// Handling by type
try {
  await loadProfile();
} catch (err) {
  if (err instanceof NotFoundError) showEmptyState();
  else if (err instanceof NetworkError) showToast("You're offline. Retrying…");
  else { reportError(err); showToast("Something went wrong"); }
}
```

**Result pattern (errors as values)** — useful where failure is normal and you don't want try/catch everywhere:

```js
async function safe(promise) {
  try { return [null, await promise]; }
  catch (err) { return [err, null]; }
}

const [err, user] = await safe(fetchUser(id));
if (err) return handle(err);
console.log(user.name);
```

**Partial failures** — don't let one failure kill everything:

```js
const results = await Promise.allSettled(widgets.map((w) => loadWidget(w.id)));
const loaded = results.filter((r) => r.status === "fulfilled").map((r) => r.value);
const failed = results.filter((r) => r.status === "rejected");
if (failed.length) reportError(new AggregateError(failed.map((f) => f.reason), "Some widgets failed"));
```

**Global handlers (browser)**

```js
window.addEventListener("error", (e) => reportError(e.error ?? e.message));
window.addEventListener("unhandledrejection", (e) => reportError(e.reason));
```

**`finally` for cleanup**

```js
setLoading(true);
try {
  await submit();
} catch (e) {
  showError(e);
} finally {
  setLoading(false); // runs on success AND failure — no stuck spinners
}
```

### 5. Defensive Programming & Validation

**Validate at the boundaries** (user input, API responses, URL params, localStorage, env vars, third-party webhooks). Inside your own code, trust your types.

```js
// Validate external data with a schema (Zod) — types disappear at runtime
import { z } from "zod";
const UserSchema = z.object({ id: z.number(), name: z.string(), email: z.string().email() });

const data = await res.json();
const parsed = UserSchema.safeParse(data);
if (!parsed.success) throw new AppError("Unexpected API response", { details: parsed.error.issues });
const user = parsed.data; // safe
```

```js
// Safe JSON parse (localStorage can contain anything)
function readJSON(key, fallback) {
  try {
    const raw = localStorage.getItem(key);
    return raw ? JSON.parse(raw) : fallback;
  } catch {
    return fallback; // corrupted value or storage disabled (Safari private mode)
  }
}
```

```js
// Defaults: ?? keeps valid falsy values (0, "", false); || does not
const pageSize = options.pageSize ?? 20;     // 0 stays 0
const title = input.title?.trim() || "Untitled"; // empty string → default (intended here)

// Don't over-use optional chaining — it hides bugs where a value SHOULD exist
const city = user?.address?.city;            // fine for truly optional data
const orderTotal = order.total;              // required field → let it crash loudly if missing (and fix the root cause)
```

```js
// Assertions for "impossible" states — fail loudly and early
function assert(condition, message) {
  if (!condition) throw new Error(`Assertion failed: ${message}`);
}
assert(items.length <= MAX_ITEMS, "cart exceeded max items");
```

### 6. Immutability & Avoiding Shared Mutable State

Shared mutable objects cause the hardest bugs: something changes an object somewhere else, and a different part of the app breaks.

```js
// ❌ Mutating function arguments
function addTax(order) {
  order.total *= 1.18;      // caller's object silently changed
  return order;
}

// ✅ Return new data
const addTax2 = (order) => ({ ...order, total: order.total * 1.18 });

// ❌ Mutating arrays in place when others hold a reference
state.items.sort();            // mutates
// ✅
const sorted = state.items.toSorted(); // or [...state.items].sort()

// Freeze constants/config so accidental mutation throws (strict mode)
export const ROLES = Object.freeze(["admin", "editor", "viewer"]);
```

- Default to `const`, non-mutating array methods (`map`, `filter`, `toSorted`, `with`), spread for updates.
- Use `structuredClone` when you truly need a deep copy.
- Return copies from getters (`get items() { return [...this.#items]; }`).

### 7. Async Code in Production

Real networks are slow, flaky and unordered. Every network call needs answers to: **timeout? retry? cancel? duplicates? order?**

**Timeouts** — `fetch` has no timeout by default and can hang forever.

```js
const res = await fetch(url, { signal: AbortSignal.timeout(8000) });
```

**Retry with exponential backoff + jitter** — retry only **transient** errors (network, 429, 5xx), never 4xx validation errors. Jitter avoids thousands of clients retrying at the same moment ("thundering herd").

```js
const sleep = (ms) => new Promise((r) => setTimeout(r, ms));

async function withRetry(fn, { retries = 3, baseDelay = 300, maxDelay = 5000, shouldRetry = isTransient } = {}) {
  for (let attempt = 0; ; attempt++) {
    try {
      return await fn(attempt);
    } catch (err) {
      if (attempt >= retries || !shouldRetry(err)) throw err;
      const backoff = Math.min(maxDelay, baseDelay * 2 ** attempt); // 300, 600, 1200...
      const jitter = Math.random() * backoff;                         // "full jitter"
      await sleep(jitter);
    }
  }
}

function isTransient(err) {
  if (err.name === "AbortError") return false;           // user cancelled
  if (err.name === "TypeError") return true;             // fetch network failure
  return [408, 429, 500, 502, 503, 504].includes(err.status);
}
```

**Cancellation** — cancel work nobody needs anymore (user navigated away, typed a new query).

```js
const controller = new AbortController();
loadDashboard({ signal: controller.signal });
// later (route change / unmount / new search)
controller.abort();

async function loadDashboard({ signal }) {
  const [user, stats] = await Promise.all([
    fetch("/api/me", { signal }).then((r) => r.json()),
    fetch("/api/stats", { signal }).then((r) => r.json()),
  ]);
  signal.throwIfAborted();
  render(user, stats);
}
```

**Race conditions — "latest request wins"**

```js
let latestRequestId = 0;
async function loadResults(query) {
  const requestId = ++latestRequestId;
  const data = await api.search(query);
  if (requestId !== latestRequestId) return; // a newer request started → ignore stale response
  render(data);
}
```

**Prevent double submits / duplicate work**

```js
// 1. Disable the button while the request is in flight
// 2. Dedupe identical in-flight requests
const inFlight = new Map();
function dedupedFetch(url) {
  if (!inFlight.has(url)) {
    inFlight.set(url, fetch(url).then((r) => r.json()).finally(() => inFlight.delete(url)));
  }
  return inFlight.get(url); // concurrent callers share one request
}

// 3. Idempotency key for payments/orders — server ignores duplicates with the same key
const idempotencyKey = crypto.randomUUID(); // created once per checkout attempt
await fetch("/api/orders", { method: "POST", headers: { "Idempotency-Key": idempotencyKey }, body });
```

**Concurrency limits** — don't fire 1,000 requests at once (browser caps ~6 connections per host; servers rate-limit you).

```js
async function mapWithConcurrency(items, limit, fn) {
  const results = new Array(items.length);
  let next = 0;
  const workers = Array.from({ length: Math.min(limit, items.length) }, async () => {
    while (next < items.length) {
      const i = next++;
      results[i] = await fn(items[i], i);
    }
  });
  await Promise.all(workers);
  return results;
}
await mapWithConcurrency(fileList, 3, uploadFile); // 3 uploads at a time
```

**Polling done right**

```js
async function pollJob(jobId, { interval = 2000, timeout = 60_000, signal } = {}) {
  const deadline = Date.now() + timeout;
  while (Date.now() < deadline) {
    signal?.throwIfAborted();
    const job = await api.getJob(jobId);
    if (job.status === "done") return job.result;
    if (job.status === "failed") throw new AppError(job.error);
    await sleep(interval);            // setTimeout-based loop, not setInterval (no overlapping calls)
  }
  throw new AppError("Job timed out", { code: "TIMEOUT" });
}
```

**Other async rules**
- Always `await` or `return` promises — a "floating" promise's error becomes an unhandled rejection. (ESLint: `no-floating-promises` in TS.)
- Don't mix `await` inside `forEach`; use `for...of` or `Promise.all`.
- Run independent calls in parallel with `Promise.all`, and use `allSettled` when partial failure is OK.
- Always clean up timers, intervals, listeners and subscriptions.

### 8. API Client Layer (centralized fetch wrapper)

Don't scatter raw `fetch` calls everywhere. Centralize base URL, headers, auth, JSON parsing, error normalization, timeouts and retries.

```js
// lib/http.js
import { config } from "./config.js";

export class HttpError extends Error {
  constructor(status, message, body) {
    super(message);
    this.name = "HttpError";
    this.status = status;
    this.body = body;
  }
}

let getToken = () => null;
export const setTokenProvider = (fn) => { getToken = fn; };

async function request(path, { method = "GET", body, headers = {}, timeout = config.requestTimeoutMs, signal, retries = method === "GET" ? 2 : 0 } = {}) {
  const url = new URL(path, config.apiUrl);
  const timeoutSignal = AbortSignal.timeout(timeout);
  const finalSignal = signal ? AbortSignal.any([signal, timeoutSignal]) : timeoutSignal;

  return withRetry(async () => {
    const token = getToken();
    const res = await fetch(url, {
      method,
      signal: finalSignal,
      headers: {
        Accept: "application/json",
        ...(body !== undefined && { "Content-Type": "application/json" }),
        ...(token && { Authorization: `Bearer ${token}` }),
        ...headers,
      },
      body: body !== undefined ? JSON.stringify(body) : undefined,
    });

    const isJson = res.headers.get("content-type")?.includes("application/json");
    const data = res.status === 204 ? null : isJson ? await res.json() : await res.text();

    if (!res.ok) {
      const message = (isJson && data?.error?.message) || res.statusText || "Request failed";
      throw new HttpError(res.status, message, data);
    }
    return data;
  }, { retries }); // retry GETs only — POST retries need idempotency keys
}

export const http = {
  get: (p, o) => request(p, o),
  post: (p, body, o) => request(p, { ...o, method: "POST", body }),
  put: (p, body, o) => request(p, { ...o, method: "PUT", body }),
  patch: (p, body, o) => request(p, { ...o, method: "PATCH", body }),
  delete: (p, o) => request(p, { ...o, method: "DELETE" }),
};

// features/users/users.api.js — feature-level API functions
export const usersApi = {
  list: (params) => http.get(`/users?${new URLSearchParams(params)}`),
  get: (id) => http.get(`/users/${encodeURIComponent(id)}`),
  update: (id, patch) => http.patch(`/users/${encodeURIComponent(id)}`, patch),
};
```

Benefits: one place to add auth refresh, logging, error reporting, headers or a base URL change. Components call `usersApi.get(id)` and never deal with raw `fetch`.

### 9. Caching

```js
// In-memory cache with TTL
function createTTLCache(ttlMs) {
  const store = new Map();
  return {
    get(key) {
      const hit = store.get(key);
      if (!hit) return undefined;
      if (Date.now() > hit.expires) { store.delete(key); return undefined; }
      return hit.value;
    },
    set(key, value) { store.set(key, { value, expires: Date.now() + ttlMs }); },
    delete: (key) => store.delete(key),
    clear: () => store.clear(),
  };
}

const userCache = createTTLCache(60_000);
async function getUserCached(id) {
  const cached = userCache.get(id);
  if (cached) return cached;
  const user = await usersApi.get(id);
  userCache.set(id, user);
  return user;
}
```

- **Stale-while-revalidate**: show cached data immediately, refetch in the background, update the UI. (TanStack Query / SWR do this for you.)
- **Bound every cache** (max size / LRU / TTL) — an unbounded Map is a memory leak.
- **Invalidate** on writes (`userCache.delete(id)` after update).
- Cache the **promise** (not just the result) to dedupe concurrent requests.

### 10. Money & Numbers

Floating point math is not exact: `0.1 + 0.2 = 0.30000000000000004`. **Never use floats for money.**

```js
// ✅ Store money as integers in the smallest unit (paise/cents)
const priceInPaise = 19999;              // ₹199.99
const qty = 3;
const totalPaise = priceInPaise * qty;   // exact integer math

// Percentages: round explicitly, once, at a defined step
const gstPaise = Math.round(totalPaise * 0.18);

// Format only for display
const formatINR = (paise) =>
  new Intl.NumberFormat("en-IN", { style: "currency", currency: "INR" }).format(paise / 100);
formatINR(totalPaise + gstPaise); // "₹707.96"

// Splitting a bill without losing a paisa
function splitEvenly(totalPaise, people) {
  const base = Math.floor(totalPaise / people);
  const remainder = totalPaise % people;
  return Array.from({ length: people }, (_, i) => base + (i < remainder ? 1 : 0));
}
splitEvenly(1000, 3); // [334, 333, 333] — sums to 1000 exactly
```

- `toFixed` returns a **string** and rounds oddly (`(1.005).toFixed(2) === "1.00"`).
- Parse user input carefully: `Number("")` is `0`, `parseFloat("12abc")` is `12`, `Number("1,000")` is `NaN`.
- IDs from databases can exceed `Number.MAX_SAFE_INTEGER` (e.g. Twitter/Snowflake IDs) → keep them as **strings** (or BigInt).
- For heavy decimal math, use a library (`decimal.js`, `dinero.js`).

### 11. Dates & Time Zones

The #1 source of subtle production bugs.

```js
// ✅ Store & send timestamps in UTC ISO 8601
const createdAt = new Date().toISOString(); // "2026-09-24T07:30:00.000Z"

// ✅ Convert to the user's local time only for DISPLAY
new Intl.DateTimeFormat("en-IN", { dateStyle: "medium", timeStyle: "short", timeZone: "Asia/Kolkata" })
  .format(new Date(createdAt));

// ❌ Parsing non-ISO strings is inconsistent across browsers
new Date("24/09/2026");       // Invalid Date
new Date("2026-09-24");       // treated as UTC midnight → can show as Sep 23 in the US!
new Date("2026-09-24T00:00"); // treated as LOCAL midnight

// ❌ Months are 0-based
new Date(2026, 9, 24);        // October 24, not September!

// ❌ Adding days with milliseconds breaks around DST changes
// ✅ Use setDate (calendar-aware) or a library
const d = new Date();
d.setDate(d.getDate() + 7);
```

- Use **date-fns** / **Day.js** / **Luxon**, or the new **`Temporal`** API where available, for date math & time zones.
- Store the user's **IANA time zone** (`Intl.DateTimeFormat().resolvedOptions().timeZone` → `"Asia/Kolkata"`) when scheduling things like "every day at 9am".
- Dates-only values (birthdays) → store as `"YYYY-MM-DD"` strings, not timestamps.
- Test code with a fixed clock (`vi.setSystemTime`), never `new Date()` inside business logic without a way to inject it.

### 12. Strings, Unicode & i18n

```js
"👍".length;                     // 2 (UTF-16 code units!)
[..."👍"].length;                // 1 (code points)
[...new Intl.Segmenter().segment("👨‍👩‍👧")].length; // 1 (user-perceived character)

["b", "a", "Ä"].sort();                             // ["a", "b", "Ä"] — wrong for humans
["b", "a", "Ä"].sort((x, y) => x.localeCompare(y)); // ["a", "Ä", "b"]
const collator = new Intl.Collator("de", { sensitivity: "base" }); // faster for big lists

"İstanbul".toLowerCase();                       // locale issues → toLocaleLowerCase("tr")
"straße".normalize("NFC") === "straße".normalize("NFC"); // normalize before comparing user input
```

- Never concatenate translated sentences (`"You have " + n + " items"`); use an i18n library with plurals (`Intl.PluralRules`, i18next, FormatJS).
- Format numbers, currencies, dates and lists with `Intl`.
- Truncate by grapheme, not `.slice()`, when emojis are possible.

### 13. Security Checklist (frontend + JS)

- **XSS**: never `innerHTML` with user data; use `textContent`; sanitize with DOMPurify when HTML is needed; set a **Content-Security-Policy**.
- **Validate URLs** before using them in `href`/`src`: allow only `http:`/`https:`.
- **No secrets in frontend code** — anything in the bundle is public.
- **Tokens**: prefer HttpOnly Secure SameSite cookies over localStorage.
- **Never `eval`/`new Function`/`setTimeout("string")`** with dynamic input.
- **Prototype pollution**: don't deep-merge untrusted JSON; block `__proto__`/`constructor` keys; use `Object.create(null)` or `Map` for user-keyed dictionaries.
- **Open redirects**: validate `?redirect=` targets are same-origin paths.
- **postMessage**: always check `event.origin`.
- **Dependencies**: `npm audit`, lockfiles, Dependabot/Renovate, avoid tiny unmaintained packages.
- **Third-party scripts** (analytics, chat widgets) run with full access to your page — load only trusted ones, use SRI (`integrity`) for CDN scripts.

```js
// Safe URL check
function safeUrl(input) {
  try {
    const url = new URL(input, window.location.origin);
    return ["http:", "https:"].includes(url.protocol) ? url.href : null;
  } catch { return null; }
}

// Safe redirect after login
function safeRedirect(path) {
  return typeof path === "string" && path.startsWith("/") && !path.startsWith("//") ? path : "/";
}

// postMessage origin check
window.addEventListener("message", (e) => {
  if (e.origin !== "https://trusted.example.com") return;
  handle(e.data);
});
```

### 14. Performance in Production

- **Measure before optimizing** (Lighthouse, DevTools Performance, Web Vitals: LCP, INP, CLS).
- **Big lists**: paginate or virtualize; don't render 10,000 DOM nodes.
- **Expensive work**: memoize, move to a Web Worker, or chunk it (`scheduler.yield()` / `setTimeout` between chunks) to keep the UI responsive.
- **Network**: fewer requests, compress, cache, prefetch, lazy-load below-the-fold content, `loading="lazy"` for images.
- **Bundle**: code-split routes, tree-shake, analyze the bundle, drop heavy libraries (moment.js → date-fns/Intl; lodash → per-method imports or native).
- **Algorithm choice beats micro-optimizations**: `Map`/`Set` lookups (O(1)) instead of `array.find` in a loop (O(n²)).
- **Event handlers**: debounce/throttle, passive scroll listeners, event delegation.
- **Memory leaks**: remove listeners, clear intervals, abort requests, bound caches, beware of closures in long-lived objects.

```js
// ❌ O(n²): 10k orders x 10k users = 100M comparisons
orders.map((o) => ({ ...o, user: users.find((u) => u.id === o.userId) }));

// ✅ O(n): index once
const usersById = new Map(users.map((u) => [u.id, u]));
orders.map((o) => ({ ...o, user: usersById.get(o.userId) }));
```

### 15. Logging, Monitoring & Observability

- **Frontend**: error tracking (Sentry, Bugsnag), Real User Monitoring & Web Vitals, product analytics.
- **Structured logs** (objects, not string concatenation) with context: user id, request id, feature, app version.
- **Log levels**: `debug` (dev only), `info`, `warn`, `error`. Don't ship noisy `console.log`s to production.
- **Never log secrets, tokens, passwords or full card numbers/PII.**
- **Source maps** uploaded to your error tracker (not publicly served) so stack traces are readable.

```js
// lib/logger.js — tiny wrapper so you can swap the backend later
const LEVELS = { debug: 10, info: 20, warn: 30, error: 40 };
const minLevel = LEVELS[config.env === "production" ? "info" : "debug"];

function log(level, message, context = {}) {
  if (LEVELS[level] < minLevel) return;
  const entry = { level, message, time: new Date().toISOString(), ...context };
  console[level === "debug" ? "log" : level](entry);
  if (level === "error") sendToErrorTracker(entry);
}
export const logger = {
  debug: (m, c) => log("debug", m, c),
  info: (m, c) => log("info", m, c),
  warn: (m, c) => log("warn", m, c),
  error: (m, c) => log("error", m, c),
};

logger.error("Checkout failed", { orderId, userId, error: err.message, code: err.code });
```

### 16. Feature Flags & Safe Releases

Ship code **dark**, turn it on gradually, and turn it off instantly without a redeploy.

```js
const flags = await fetchFlags(user.id); // from LaunchDarkly / Unleash / GrowthBook / your own API
if (flags.newCheckout) renderNewCheckout();
else renderOldCheckout();

// Percentage rollout: deterministic per user AND per flag (full version: best-practices.md → "Feature Flags & Safe Rollouts")
function isInRollout(flagKey, userId, percent) {
  let hash = 0x811c9dc5;                                          // FNV-1a over "flag:user"
  for (const byte of new TextEncoder().encode(`${flagKey}:${userId}`)) hash = Math.imul(hash ^ byte, 0x01000193) >>> 0;
  return hash % 10_000 < Math.round(percent * 100);
}
```

Include the **flag key** in the hash. Hashing only the user id makes every 10% rollout pick the **same** 10% of users, so the same people get every risky change, and experiments contaminate each other.

- **Remove old flags** after rollout — stale flags become technical debt.
- Combine with canary releases, versioned APIs and backwards-compatible changes (expand → migrate → contract).

### 17. Testing Strategy

**Testing pyramid / trophy**: many fast unit tests for pure logic, a good number of integration tests (components with real behaviour, API routes with a test DB), few E2E tests for critical flows (login, checkout, payment).

What to test:
- Business rules & edge cases (empty, zero, negative, max, null, unicode, time zones).
- Bugs you've fixed (regression tests).
- Error paths, not just happy paths.
- Behaviour, not implementation details.

```js
// Make code testable: inject time, randomness and I/O
export function isTrialExpired(user, now = new Date()) {
  return now > new Date(user.trialEndsAt);
}

test("trial expires after end date", () => {
  expect(isTrialExpired({ trialEndsAt: "2026-01-10T00:00:00Z" }, new Date("2026-01-11T00:00:00Z"))).toBe(true);
  expect(isTrialExpired({ trialEndsAt: "2026-01-10T00:00:00Z" }, new Date("2026-01-09T00:00:00Z"))).toBe(false);
});
```

Tools: Vitest/Jest (unit), Testing Library (components), MSW (mock network), Playwright/Cypress (E2E), Supertest (APIs).

### 18. Code Quality Tooling

| Tool | Purpose |
|---|---|
| **ESLint** | Catch bugs & bad patterns (unused vars, missing awaits, hooks rules) |
| **Prettier** | Automatic formatting — no style debates |
| **TypeScript** (or JSDoc + `// @ts-check`) | Catch type errors before runtime |
| **Husky + lint-staged** | Run lint/format/tests on changed files before commit |
| **commitlint** | Enforce commit message convention |
| **CI (GitHub Actions)** | Lint, type-check, test, build on every PR |
| **Dependabot / Renovate** | Automated dependency updates |

```js
// JSDoc gives type-checking & autocomplete in plain JS files
// @ts-check
/**
 * Calculates the order total in paise.
 * @param {{ pricePaise: number, qty: number }[]} items
 * @param {number} [discountPercent=0]
 * @returns {number}
 */
export function orderTotal(items, discountPercent = 0) {
  const subtotal = items.reduce((sum, i) => sum + i.pricePaise * i.qty, 0);
  return Math.round(subtotal * (1 - discountPercent / 100));
}
```

### 19. Git Workflow & Code Review

- Small, focused PRs (easier to review, safer to revert).
- Branch naming: `feat/checkout-coupons`, `fix/login-redirect`.
- **Conventional commits**: `feat: add coupon support`, `fix: prevent double checkout submit`, `refactor:`, `chore:`, `docs:`, `test:`.
- PR description: what, why, how to test, screenshots for UI.
- Review checklist: correctness & edge cases, error handling, security, performance, naming/readability, tests, no leftover logs/TODOs, backwards compatibility.
- Never commit secrets (use pre-commit secret scanning); rotate a key immediately if one leaks.

### 20. Documentation

- **README**: what it is, how to run, env vars, scripts, architecture overview.
- **JSDoc/TSDoc** for public functions & non-obvious behaviour.
- **ADRs** (Architecture Decision Records): short docs explaining *why* a big decision was made.
- Keep docs next to the code so they're updated together.

### 21. Dependency Management

- Before adding a package: is it maintained? how big (bundlephobia)? license? can native JS do it?
- Commit the lockfile; use `npm ci` in CI.
- Pin major versions; upgrade regularly in small steps rather than once every 2 years.
- Remove unused dependencies (`npx depcheck`/`knip`).

### 22. Common Production Bugs (and fixes)

| Bug | Cause | Fix |
|---|---|---|
| Stale search results | Out-of-order responses | AbortController / latest-request-id |
| Double orders/payments | Double click, retries | Disable button, idempotency keys |
| Spinner stuck forever | Error path didn't reset loading | `finally` |
| "undefined is not a function" after deploy | Old cached JS bundle calling new API | Versioned assets, backwards-compatible APIs |
| Wrong dates for some users | Time zone / date-only parsing | UTC ISO storage, format with `Intl`, date libs |
| ₹0.30000000000000004 | Float money | Integer paise + `Intl.NumberFormat` |
| Memory grows until tab crashes | Listeners/intervals/caches never cleaned | Cleanup functions, bounded caches |
| Page freezes | Heavy sync work on main thread | Web Worker, chunking, virtualization |
| Works locally, breaks in prod | Missing/incorrect env vars | Validate config at startup |
| Random crash on some data | Unvalidated API response | Schema validation at boundaries |
| Silent failures | Swallowed errors, floating promises | Log/report errors, lint rules |
| Too many API calls | No debounce/throttle/dedupe | Debounce, throttle, request dedupe, caching |
| Sorting numbers wrong | Default `sort()` is string-based | `sort((a, b) => a - b)` |
| `0` rendered or treated as missing | `\|\|` instead of `??`, `&&` with numbers | `??`, explicit comparisons |
| Mutations leaking across components | Shared mutable objects | Immutable updates, copies |

### 23. Production Readiness Checklist

- [ ] Config validated at startup, no secrets in code
- [ ] All external input validated (forms, API responses, URL params, storage)
- [ ] Errors: user-friendly messages, detailed reporting, global handlers, no swallowed errors
- [ ] Every network call: timeout, error handling, cancellation where needed, retries only for transient errors
- [ ] Loading, empty, error and success states for every async UI
- [ ] No double submits (disabled buttons / idempotency)
- [ ] Debounce/throttle on high-frequency events
- [ ] Money as integers, dates in UTC, text via `Intl`
- [ ] Listeners, timers and subscriptions cleaned up
- [ ] Security: no `innerHTML` with user data, CSP, safe URLs, HttpOnly cookies
- [ ] Accessibility basics (semantic HTML, labels, keyboard, focus)
- [ ] Lint + format + type-check + tests in CI
- [ ] Logging/monitoring/source maps configured
- [ ] Feature flag or rollback plan for risky changes
- [ ] Performance budget checked (bundle size, Web Vitals)

### Production Interview Questions

1. **How do you handle errors in a large JS application?** → Error hierarchy, catch where you can act, global handlers, reporting (Sentry), friendly UI messages, `cause`.
2. **How do you prevent race conditions in async UI code?** → AbortController, latest-request-id, disabling concurrent actions.
3. **How do you implement retry logic? What is exponential backoff with jitter?**
4. **How do you prevent duplicate form submissions / double payments?**
5. **How would you design an API client layer for a frontend app?**
6. **How do you handle money in JavaScript?** → Integer minor units, `Intl.NumberFormat`, decimal libraries.
7. **What are common date/time zone pitfalls?**
8. **How do you make code testable?** → Pure functions, dependency injection, injecting time/randomness, separating I/O.
9. **How do you find and fix memory leaks?**
10. **What would you check in a code review?**
11. **What are feature flags and why use them?**
12. **How do you keep a codebase consistent across a team?** → ESLint, Prettier, TS, conventions, CI, PR reviews.
13. **Why validate API responses if the backend is yours?** → Deploys drift, bugs, third-party data, and types disappear at runtime.
14. **How do you secure a frontend app?** → XSS prevention, CSP, safe URLs, token storage, dependency hygiene, no secrets in bundle.

---

## 55. Code Smells & Refactoring Catalog

A **code smell** is a surface sign that code will be hard to change (not necessarily a bug). **Refactoring** = improving the structure of code **without changing its behaviour**, in small safe steps.

### How to refactor safely

1. **Have tests first** — if there are none, write **characterization tests** that lock in current behaviour (even if weird).
2. **Small steps**: one refactoring at a time, run tests after each, commit often.
3. **Use IDE refactorings** (Rename symbol, Extract function/variable, Move to file, Inline) — they update all references safely.
4. **Separate refactoring from behaviour changes** — never in the same commit/PR (reviewers can't tell what changed).
5. **Boy Scout rule**: improve the code you touch; don't start a giant rewrite.
6. For large legacy systems use the **Strangler Fig** pattern: route new functionality to new code, migrate piece by piece, delete the old path at the end.

**When NOT to refactor**: code that's about to be deleted, code nobody changes (stable and working), right before a risky release, or without tests on critical paths.

---

### 1. Long function → Extract Function

```js
// ❌ does validation, pricing, tax and formatting in one place
function checkout(cart, user) {
  if (!cart.items.length) throw new Error("Cart is empty");
  if (!user.address) throw new Error("Address required");
  let subtotal = 0;
  for (const item of cart.items) subtotal += item.pricePaise * item.qty;
  let discount = 0;
  if (user.isPremium) discount = Math.round(subtotal * 0.1);
  const tax = Math.round((subtotal - discount) * 0.18);
  return { subtotal, discount, tax, total: subtotal - discount + tax };
}

// ✅ each step has a name; each piece is testable
function validateCheckout(cart, user) {
  if (!cart.items.length) throw new Error("Cart is empty");
  if (!user.address) throw new Error("Address required");
}
const subtotalOf = (items) => items.reduce((sum, i) => sum + i.pricePaise * i.qty, 0);
const discountFor = (user, subtotal) => (user.isPremium ? Math.round(subtotal * PREMIUM_DISCOUNT) : 0);
const taxOn = (amount) => Math.round(amount * GST_RATE);

const PREMIUM_DISCOUNT = 0.1;
const GST_RATE = 0.18;

function checkout2(cart, user) {
  validateCheckout(cart, user);
  const subtotal = subtotalOf(cart.items);
  const discount = discountFor(user, subtotal);
  const tax = taxOn(subtotal - discount);
  return { subtotal, discount, tax, total: subtotal - discount + tax };
}
```

Signals: a function you have to scroll, comments separating "sections", many local variables, several levels of abstraction mixed together.

### 2. Magic numbers & strings → Named constants / enums

```js
// ❌
if (user.role === 2 && Date.now() - user.lastLogin > 2592000000) lockAccount(user);

// ✅
const ROLE = Object.freeze({ ADMIN: 1, EDITOR: 2, VIEWER: 3 });
const INACTIVITY_LIMIT_MS = 30 * 24 * 60 * 60 * 1000;   // 30 days
const isInactiveEditor = (u) => u.role === ROLE.EDITOR && Date.now() - u.lastLogin > INACTIVITY_LIMIT_MS;
if (isInactiveEditor(user)) lockAccount(user);
```

### 3. Deep nesting → Guard clauses

```js
// ❌ arrow code
function shippingCost(order) {
  if (order) {
    if (order.items.length > 0) {
      if (order.country === "IN") {
        if (order.total > 50000) {
          return 0;
        } else {
          return 4900;
        }
      } else {
        return 99900;
      }
    } else {
      return 0;
    }
  } else {
    throw new Error("No order");
  }
}

// ✅ handle special cases first, then the main path
function shippingCost2(order) {
  if (!order) throw new Error("No order");
  if (order.items.length === 0) return 0;
  if (order.country !== "IN") return 99900;
  return order.total > 50000 ? 0 : 4900;
}
```

### 4. Long parameter list / boolean flags → Options object or separate functions

```js
// ❌ what do true, false, 30 mean at the call site?
sendReport("r@x.com", "monthly", true, false, 30);

// ✅ self-documenting, order-independent, extensible
sendReport({ to: "r@x.com", type: "monthly", attachPdf: true, includeDrafts: false, rangeDays: 30 });

// ❌ a flag that switches between two behaviours
function renderUser(user, asCard) { return asCard ? renderCard(user) : renderRow(user); }
// ✅ two intention-revealing functions
const renderUserCard = (user) => renderCard(user);
const renderUserRow = (user) => renderRow(user);
```

### 5. Duplicate code → Extract shared function (Rule of Three)

```js
// ❌ same formatting logic copy-pasted in three places
const priceLabel = "₹" + (product.pricePaise / 100).toFixed(2);
const totalLabel = "₹" + (cart.totalPaise / 100).toFixed(2);

// ✅ one source of truth (and now it can use Intl properly)
const formatINR = (paise) => new Intl.NumberFormat("en-IN", { style: "currency", currency: "INR" }).format(paise / 100);
```

**Rule of three**: tolerate duplication twice; extract on the third occurrence. Don't merge code that only *looks* similar but changes for different reasons — the wrong abstraction is worse than duplication.

### 6. Switch on type → Lookup table / Polymorphism

```js
// ❌ every new plan = edit this switch (and every other switch on plan)
function monthlyPrice(plan) {
  switch (plan) {
    case "free": return 0;
    case "pro": return 49900;
    case "team": return 199900;
    default: throw new Error(`Unknown plan ${plan}`);
  }
}

// ✅ data-driven
const PLANS = {
  free: { pricePaise: 0, seats: 1 },
  pro: { pricePaise: 49900, seats: 1 },
  team: { pricePaise: 199900, seats: 10 },
};
function monthlyPrice2(plan) {
  const config = PLANS[plan];
  if (!config) throw new Error(`Unknown plan ${plan}`);
  return config.pricePaise;
}
```

When each case has different **behaviour** (not just data), use objects with a common interface — polymorphism (see OOP section, "Replacing if/else chains with polymorphism").

### 7. Primitive obsession → Value objects

Passing raw strings/numbers for domain concepts (money, email, phone, date ranges) spreads validation and formatting everywhere.

```js
// ❌ is this rupees or paise? validated? which currency?
function refund(orderId, amount, currency) { /* ... */ }

// ✅ a small immutable value object carries the rules
class Money {
  constructor(paise, currency = "INR") {
    if (!Number.isInteger(paise)) throw new TypeError("Money must be integer paise");
    this.paise = paise;
    this.currency = currency;
    Object.freeze(this);
  }
  static fromRupees(rupees, currency) { return new Money(Math.round(rupees * 100), currency); }
  add(other) { this.#same(other); return new Money(this.paise + other.paise, this.currency); }
  isGreaterThan(other) { this.#same(other); return this.paise > other.paise; }
  #same(other) { if (other.currency !== this.currency) throw new Error("Currency mismatch"); }
  toString() { return new Intl.NumberFormat("en-IN", { style: "currency", currency: this.currency }).format(this.paise / 100); }
}
function refund2(orderId, amount /* Money */) { /* ... */ }
```

### 8. Data clumps → Group into an object

```js
// ❌ the same 4 values always travel together
function createShipment(street, city, pincode, country) {}
function validateAddress(street, city, pincode, country) {}

// ✅
function createShipment2(address) {}
function validateAddress2({ street, city, pincode, country }) {}
```

### 9. Feature envy → Move the logic to the data it uses

```js
// ❌ this function is all about `order`'s internals
function orderIsFreeShipping(order) {
  return order.country === "IN" && order.items.reduce((s, i) => s + i.pricePaise * i.qty, 0) > 50000;
}

// ✅ the Order knows its own rules ("tell, don't ask")
class Order {
  constructor({ country, items }) { Object.assign(this, { country, items }); }
  get subtotal() { return this.items.reduce((s, i) => s + i.pricePaise * i.qty, 0); }
  get hasFreeShipping() { return this.country === "IN" && this.subtotal > 50000; }
}
```

### 10. Message chains → Law of Demeter

```js
// ❌ knows the whole object graph; breaks when any link changes (or is null)
const zip = order.customer.profile.address.zip;

// ✅ ask the nearest object for what you need
class Customer {
  constructor(profile) { this.profile = profile; }
  get shippingZip() { return this.profile?.address?.zip ?? null; }
}
```

### 11. God object / large module → Split by responsibility

A `utils.js` with 80 unrelated helpers, or a `UserService` that handles auth, emails, billing and reporting. Split by **reason to change** (Single Responsibility): `auth/`, `billing/`, `email/`, `dates.js`, `money.js`.

Signals: huge file, many unrelated imports, merge conflicts on every PR, tests needing enormous setup.

### 12. Mutating arguments & shared state → Pure functions

```js
// ❌ surprises every caller holding a reference
function addItem(cart, item) {
  cart.items.push(item);
  cart.count++;
  return cart;
}

// ✅ returns new data; callers decide what to do with it
const addItem2 = (cart, item) => ({ ...cart, items: [...cart.items, item], count: cart.count + 1 });
```

### 13. Loops with bookkeeping → Pipelines

```js
// ❌
const result = [];
for (let i = 0; i < users.length; i++) {
  if (users[i].active) {
    const name = users[i].firstName + " " + users[i].lastName;
    if (!result.includes(name)) result.push(name);
  }
}
result.sort();

// ✅
const result2 = [...new Set(
  users.filter((u) => u.active).map((u) => `${u.firstName} ${u.lastName}`)
)].sort();
```

### 14. Callback pyramids / promise chains → async/await

```js
// ❌
function loadDashboard(id, cb) {
  getUser(id, (err, user) => {
    if (err) return cb(err);
    getOrders(user.id, (err, orders) => {
      if (err) return cb(err);
      cb(null, { user, orders });
    });
  });
}

// ✅ (with promisified APIs)
async function loadDashboard2(id) {
  const user = await getUserAsync(id);
  const orders = await getOrdersAsync(user.id);
  return { user, orders };
}
```

### 15. Comments explaining confusing code → Rename / extract

```js
// ❌
// check if user can edit: must be owner or admin and post not locked
if ((p.a === u.id || u.r === 1) && !p.l) edit();

// ✅ the code says it; no comment needed
const isOwner = post.authorId === user.id;
const isAdmin = user.role === ROLE.ADMIN;
const canEdit = (isOwner || isAdmin) && !post.locked;
if (canEdit) edit();
```

### 16. Dead code & speculative generality → Delete it

Unused functions, commented-out blocks, parameters nobody passes, "pluggable" abstractions with one implementation, config options nobody sets. Delete them (git remembers). **YAGNI** — add flexibility when a real second use case arrives. Tools: `knip` (unused files/exports/deps), ESLint `no-unused-vars`, coverage reports.

### 17. Inconsistent naming → Rename

`getUser` / `fetchUserData` / `loadUsr` for the same idea; `data`, `info`, `temp`, `obj2`. Pick one vocabulary (domain language the business uses) and rename with the IDE.

### 18. Shotgun surgery & divergent change

- **Shotgun surgery**: one change requires edits in many files (e.g. adding a plan touches 12 switches) → centralize the knowledge (config/lookup table, one module).
- **Divergent change**: one file changes for many unrelated reasons → split it.

---

### Refactoring legacy code

- Write **characterization tests** around the current behaviour (snapshot the outputs for a range of inputs).
- Find **seams** — places where you can inject a dependency or wrap a function to isolate code for testing.
- Refactor in **small, reversible PRs**; use feature flags for risky swaps.
- **Strangler Fig**: new module/service handles new or migrated routes; old code shrinks until it can be deleted.
- Codemods (jscodeshift, ts-morph, `ast-grep`) for large mechanical changes across a codebase.

### Refactoring checklist

- [ ] Tests pass before starting (or characterization tests written)
- [ ] One refactoring per step; tests green after each
- [ ] No behaviour change mixed in
- [ ] Names reveal intent; functions small; no magic values
- [ ] Duplication removed only where it's the same knowledge
- [ ] Dead code deleted
- [ ] PR explains the *why* ("prepares for adding team plans")

### Interview Qs

1. What is a code smell? Name five and how you'd fix them.
2. What is refactoring? How do you make sure you don't change behaviour?
3. Guard clauses vs nested ifs?
4. What is primitive obsession? What's a value object?
5. Rule of three / "the wrong abstraction is worse than duplication" — explain.
6. What is the Law of Demeter?
7. How would you refactor a 2,000-line legacy file with no tests?
8. What is the Strangler Fig pattern?

---

## 56. Data Structures & Algorithms in JavaScript

Most JS interviews include at least one DSA round. Real frontend/backend code needs it too: picking a `Map` over an array lookup, avoiding O(n²) loops, building autocomplete (trie), dependency ordering (topological sort), priority queues for schedulers.

### 1. Big-O Notation

**Big-O** describes how the running time (or memory) **grows** as the input size `n` grows, ignoring constants. It's about the worst case unless stated otherwise.

| Big-O | Name | Example | n = 1,000,000 |
|---|---|---|---|
| O(1) | Constant | `arr[i]`, `map.get(k)`, `set.has(x)` | 1 step |
| O(log n) | Logarithmic | Binary search, balanced tree lookup | ~20 steps |
| O(n) | Linear | Loop once, `includes`, `indexOf` | 1M steps |
| O(n log n) | Linearithmic | Good sorting (`sort`, merge sort) | ~20M |
| O(n²) | Quadratic | Nested loops over the same data | 10¹² 😱 |
| O(2ⁿ) | Exponential | All subsets, naive recursive fib | impossible |
| O(n!) | Factorial | All permutations | impossible |

```js
// O(1)
const first = arr[0];

// O(n)
const total = arr.reduce((s, x) => s + x, 0);

// O(n²) — the classic accidental one
const dupes = arr.filter((x, i) => arr.indexOf(x) !== i);     // indexOf inside filter

// O(n) with a Set
const seen = new Set(), dupes2 = [];
for (const x of arr) seen.has(x) ? dupes2.push(x) : seen.add(x);

// O(log n) — halving each step
for (let i = n; i > 1; i = Math.floor(i / 2)) {}
```

Rules: drop constants (O(2n) → O(n)); keep the dominant term (O(n² + n) → O(n²)); different inputs get different variables (O(a + b), O(a·b)).

**Space complexity** counts extra memory: a new array of size n → O(n); recursion depth d → O(d) call stack.

### Cost of common JS operations

| Operation | Cost | Note |
|---|---|---|
| `arr[i]`, `arr.push()`, `arr.pop()` | O(1) | |
| `arr.shift()`, `arr.unshift()`, `splice` in middle | **O(n)** | Re-indexes everything → don't use `shift` for big queues |
| `includes`, `indexOf`, `find`, `filter`, `map` | O(n) | |
| `arr.sort()` | O(n log n) | TimSort in V8, stable |
| `slice`, spread `[...arr]`, `concat` | O(n) | Copies |
| `Map/Set` get/set/has/delete | O(1) avg | Use for lookups |
| `obj[key]` | O(1) avg | |
| `str + str` in a loop | O(n) each → O(n²) total | Use `array.join` |
| `Object.keys(obj)` | O(n) | |

---

### 2. Arrays & Strings — core patterns

#### Two pointers

Two indexes moving toward each other (or at different speeds). Works great on **sorted** arrays and strings.

```js
// Pair with target sum in a SORTED array — O(n) time, O(1) space
function pairSum(sorted, target) {
  let l = 0, r = sorted.length - 1;
  while (l < r) {
    const sum = sorted[l] + sorted[r];
    if (sum === target) return [l, r];
    sum < target ? l++ : r--;
  }
  return null;
}

// Palindrome check
function isPalindrome(s) {
  s = s.toLowerCase().replace(/[^a-z0-9]/g, "");
  for (let l = 0, r = s.length - 1; l < r; l++, r--) if (s[l] !== s[r]) return false;
  return true;
}

// Move zeros to the end in place (keep order)
function moveZeros(nums) {
  let write = 0;
  for (const n of nums) if (n !== 0) nums[write++] = n;
  while (write < nums.length) nums[write++] = 0;
  return nums;
}
```

#### Sliding window

Maintain a window `[left, right]` over a sequence and move it instead of recomputing from scratch. Signals: "longest/shortest **subarray/substring** with…", "max sum of k consecutive…".

```js
// Max sum of k consecutive elements — fixed window, O(n)
function maxSumK(nums, k) {
  let sum = 0;
  for (let i = 0; i < k; i++) sum += nums[i];
  let best = sum;
  for (let i = k; i < nums.length; i++) {
    sum += nums[i] - nums[i - k];        // slide: add new, remove old
    best = Math.max(best, sum);
  }
  return best;
}

// Longest substring without repeating characters — variable window, O(n)
function lengthOfLongestSubstring(s) {
  const lastSeen = new Map();
  let left = 0, best = 0;
  for (let right = 0; right < s.length; right++) {
    const ch = s[right];
    if (lastSeen.has(ch) && lastSeen.get(ch) >= left) left = lastSeen.get(ch) + 1; // shrink
    lastSeen.set(ch, right);
    best = Math.max(best, right - left + 1);
  }
  return best;
}
lengthOfLongestSubstring("abcabcbb"); // 3 ("abc")
```

#### Prefix sums

Precompute running totals so any range sum is O(1).

```js
function prefixSums(nums) {
  const pre = [0];
  for (const n of nums) pre.push(pre.at(-1) + n);
  return (l, r) => pre[r + 1] - pre[l];   // sum of nums[l..r]
}
const rangeSum = prefixSums([2, 4, 6, 8]);
rangeSum(1, 2); // 10

// Subarray sum equals k (count) — prefix sum + hash map, O(n)
function subarraySum(nums, k) {
  const counts = new Map([[0, 1]]);
  let sum = 0, result = 0;
  for (const n of nums) {
    sum += n;
    result += counts.get(sum - k) ?? 0;
    counts.set(sum, (counts.get(sum) ?? 0) + 1);
  }
  return result;
}
```

#### Hash map counting

```js
// Most frequent element, anagram check, first unique char — all O(n)
function topKFrequent(nums, k) {
  const freq = new Map();
  for (const n of nums) freq.set(n, (freq.get(n) ?? 0) + 1);
  return [...freq.entries()].sort((a, b) => b[1] - a[1]).slice(0, k).map(([n]) => n);
}
```

#### Binary search — O(log n) on sorted data

```js
function binarySearch(sorted, target) {
  let lo = 0, hi = sorted.length - 1;
  while (lo <= hi) {
    const mid = lo + Math.floor((hi - lo) / 2);
    if (sorted[mid] === target) return mid;
    sorted[mid] < target ? (lo = mid + 1) : (hi = mid - 1);
  }
  return -1;
}

// "Lower bound": first index where sorted[i] >= target (insertion point)
function lowerBound(sorted, target) {
  let lo = 0, hi = sorted.length;
  while (lo < hi) {
    const mid = (lo + hi) >> 1;
    sorted[mid] < target ? (lo = mid + 1) : (hi = mid);
  }
  return lo;
}
```

Binary search also works on **answers** ("minimum capacity to ship in D days") when a condition flips from false to true once.

---

### 3. Stack (LIFO)

Use a plain array: `push` / `pop` are O(1). Used for undo/redo, browser history, parsing, DFS, "next greater element".

```js
// Monotonic stack: next greater element for each item — O(n)
function nextGreater(nums) {
  const result = new Array(nums.length).fill(-1);
  const stack = [];                                  // indexes, values decreasing
  for (let i = 0; i < nums.length; i++) {
    while (stack.length && nums[i] > nums[stack.at(-1)]) {
      result[stack.pop()] = nums[i];
    }
    stack.push(i);
  }
  return result;
}
nextGreater([2, 1, 5, 3]); // [5, 5, -1, -1]

// Min stack: push/pop/getMin all O(1)
class MinStack {
  #items = []; #mins = [];
  push(x) { this.#items.push(x); this.#mins.push(Math.min(x, this.#mins.at(-1) ?? Infinity)); }
  pop() { this.#mins.pop(); return this.#items.pop(); }
  top() { return this.#items.at(-1); }
  getMin() { return this.#mins.at(-1); }
}
```

### 4. Queue (FIFO)

`array.shift()` is **O(n)** — fine for small queues, slow for big ones (BFS on large graphs, job queues).

```js
// O(1) queue using a head pointer
class Queue {
  #items = []; #head = 0;
  enqueue(x) { this.#items.push(x); }
  dequeue() {
    if (this.#head >= this.#items.length) return undefined;
    const x = this.#items[this.#head++];
    if (this.#head > 1000 && this.#head * 2 > this.#items.length) { // compact occasionally
      this.#items = this.#items.slice(this.#head);
      this.#head = 0;
    }
    return x;
  }
  peek() { return this.#items[this.#head]; }
  get size() { return this.#items.length - this.#head; }
}
```

### 5. Linked List

Nodes pointing to the next node. O(1) insert/delete at a known node, O(n) access by index. Rare in app code, common in interviews.

```js
class ListNode {
  constructor(val, next = null) { this.val = val; this.next = next; }
}
const fromArray = (arr) => arr.reduceRight((next, val) => new ListNode(val, next), null);
const toArray = (head) => { const out = []; for (let n = head; n; n = n.next) out.push(n.val); return out; };

// Reverse — O(n) time, O(1) space
function reverseList(head) {
  let prev = null, curr = head;
  while (curr) {
    const next = curr.next;
    curr.next = prev;
    prev = curr;
    curr = next;
  }
  return prev;
}
toArray(reverseList(fromArray([1, 2, 3]))); // [3, 2, 1]

// Middle node — fast & slow pointers
function middle(head) {
  let slow = head, fast = head;
  while (fast?.next) { slow = slow.next; fast = fast.next.next; }
  return slow;
}

// Cycle detection — Floyd's tortoise and hare
function hasCycle(head) {
  let slow = head, fast = head;
  while (fast?.next) {
    slow = slow.next;
    fast = fast.next.next;
    if (slow === fast) return true;
  }
  return false;
}

// Merge two sorted lists
function mergeSorted(a, b) {
  const dummy = new ListNode(0);
  let tail = dummy;
  while (a && b) {
    if (a.val <= b.val) { tail.next = a; a = a.next; } else { tail.next = b; b = b.next; }
    tail = tail.next;
  }
  tail.next = a ?? b;
  return dummy.next;
}
```

---

### 6. Recursion & Backtracking

Recursion = a function calling itself with a smaller problem + a **base case**. Backtracking = build a solution step by step and **undo** choices that don't work.

```js
// All subsets (power set) — O(2ⁿ)
function subsets(nums) {
  const result = [];
  (function backtrack(start, current) {
    result.push([...current]);
    for (let i = start; i < nums.length; i++) {
      current.push(nums[i]);          // choose
      backtrack(i + 1, current);      // explore
      current.pop();                  // un-choose
    }
  })(0, []);
  return result;
}
subsets([1, 2, 3]); // [[],[1],[1,2],[1,2,3],[1,3],[2],[2,3],[3]]

// All permutations — O(n!)
function permutations(nums) {
  const result = [];
  const used = new Array(nums.length).fill(false);
  (function backtrack(current) {
    if (current.length === nums.length) return result.push([...current]);
    for (let i = 0; i < nums.length; i++) {
      if (used[i]) continue;
      used[i] = true; current.push(nums[i]);
      backtrack(current);
      used[i] = false; current.pop();
    }
  })([]);
  return result;
}
```

JS has **no tail-call optimization** in practice → very deep recursion (~10k+ frames) throws `RangeError: Maximum call stack size exceeded`. Convert deep recursion to a loop with an explicit stack.

---

### 7. Trees

A **tree** = nodes with children and no cycles. **Binary tree**: ≤ 2 children. **BST** (binary search tree): left < node < right → O(log n) search when balanced. The DOM, JSON, file systems, React's component tree and org charts are all trees.

```js
class TreeNode {
  constructor(val, left = null, right = null) { Object.assign(this, { val, left, right }); }
}

//        4
//      /   \
//     2     6
//    / \   / \
//   1   3 5   7
const root = new TreeNode(4, new TreeNode(2, new TreeNode(1), new TreeNode(3)), new TreeNode(6, new TreeNode(5), new TreeNode(7)));

// DFS traversals (recursive)
const inorder = (n, out = []) => (n && (inorder(n.left, out), out.push(n.val), inorder(n.right, out)), out);
inorder(root); // [1,2,3,4,5,6,7] — inorder of a BST is SORTED
const preorder = (n, out = []) => (n && (out.push(n.val), preorder(n.left, out), preorder(n.right, out)), out);
const postorder = (n, out = []) => (n && (postorder(n.left, out), postorder(n.right, out), out.push(n.val)), out);

// BFS — level order traversal (uses a queue)
function levelOrder(root) {
  if (!root) return [];
  const levels = [], queue = [root];
  while (queue.length) {
    const size = queue.length, level = [];
    for (let i = 0; i < size; i++) {
      const node = queue.shift();                 // fine for interview sizes
      level.push(node.val);
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
    levels.push(level);
  }
  return levels;
}
levelOrder(root); // [[4],[2,6],[1,3,5,7]]

// Max depth
const maxDepth = (n) => (n ? 1 + Math.max(maxDepth(n.left), maxDepth(n.right)) : 0);

// Validate BST — pass allowed range down
function isValidBST(node, min = -Infinity, max = Infinity) {
  if (!node) return true;
  if (node.val <= min || node.val >= max) return false;
  return isValidBST(node.left, min, node.val) && isValidBST(node.right, node.val, max);
}

// Lowest common ancestor in a BST
function lcaBST(node, p, q) {
  while (node) {
    if (p < node.val && q < node.val) node = node.left;
    else if (p > node.val && q > node.val) node = node.right;
    else return node;
  }
  return null;
}
```

```js
// Real-world: walk a nested tree (menu / comments / file explorer)
function findById(nodes, id) {
  for (const node of nodes) {
    if (node.id === id) return node;
    const found = findById(node.children ?? [], id);
    if (found) return found;
  }
  return null;
}

// Build a tree from flat rows (parentId) — O(n) with a Map
function buildTree(rows) {
  const byId = new Map(rows.map((r) => [r.id, { ...r, children: [] }]));
  const roots = [];
  for (const node of byId.values()) {
    const parent = node.parentId == null ? null : byId.get(node.parentId);
    parent ? parent.children.push(node) : roots.push(node);
  }
  return roots;
}
```

### 8. Trie (prefix tree) — autocomplete

```js
class Trie {
  #root = { children: new Map(), end: false };
  insert(word) {
    let node = this.#root;
    for (const ch of word) {
      if (!node.children.has(ch)) node.children.set(ch, { children: new Map(), end: false });
      node = node.children.get(ch);
    }
    node.end = true;
  }
  #find(prefix) {
    let node = this.#root;
    for (const ch of prefix) {
      node = node.children.get(ch);
      if (!node) return null;
    }
    return node;
  }
  has(word) { return this.#find(word)?.end === true; }
  suggest(prefix, limit = 5) {
    const start = this.#find(prefix), out = [];
    (function dfs(node, path) {
      if (!node || out.length >= limit) return;
      if (node.end) out.push(path);
      for (const [ch, child] of node.children) dfs(child, path + ch);
    })(start, prefix);
    return out;
  }
}
const t = new Trie();
["react", "redux", "remix", "rust"].forEach((w) => t.insert(w));
t.suggest("re"); // ["react", "redux", "remix"]
```

### 9. Heap / Priority Queue

A **min-heap** always gives the smallest item in O(1), with O(log n) insert/remove. JS has **no built-in heap** — you write one (or use a library). Used for: top-K, schedulers, Dijkstra, merging K sorted lists, "k closest points".

```js
class MinHeap {
  #h = [];
  constructor(compare = (a, b) => a - b) { this.compare = compare; }
  get size() { return this.#h.length; }
  peek() { return this.#h[0]; }
  push(x) {
    const h = this.#h;
    h.push(x);
    let i = h.length - 1;
    while (i > 0) {                                   // bubble up
      const parent = (i - 1) >> 1;
      if (this.compare(h[i], h[parent]) >= 0) break;
      [h[i], h[parent]] = [h[parent], h[i]];
      i = parent;
    }
  }
  pop() {
    const h = this.#h;
    if (h.length === 0) return undefined;
    const top = h[0], last = h.pop();
    if (h.length) {
      h[0] = last;
      let i = 0;
      while (true) {                                  // sink down
        const l = 2 * i + 1, r = l + 1;
        let smallest = i;
        if (l < h.length && this.compare(h[l], h[smallest]) < 0) smallest = l;
        if (r < h.length && this.compare(h[r], h[smallest]) < 0) smallest = r;
        if (smallest === i) break;
        [h[i], h[smallest]] = [h[smallest], h[i]];
        i = smallest;
      }
    }
    return top;
  }
}

// K largest elements — keep a min-heap of size k → O(n log k)
function kLargest(nums, k) {
  const heap = new MinHeap();
  for (const n of nums) {
    heap.push(n);
    if (heap.size > k) heap.pop();
  }
  return Array.from({ length: heap.size }, () => heap.pop()).reverse();
}
kLargest([3, 1, 5, 12, 2, 11], 3); // [12, 11, 5]
```

### 10. Graphs

Nodes (vertices) connected by edges. Social networks, maps/routes, dependency graphs (npm packages, build steps, course prerequisites), recommendation systems.

```js
// Adjacency list
const graph = new Map([
  ["A", ["B", "C"]],
  ["B", ["D"]],
  ["C", ["D", "E"]],
  ["D", ["F"]],
  ["E", ["F"]],
  ["F", []],
]);

// BFS — shortest path in an UNWEIGHTED graph
function shortestPath(graph, start, goal) {
  const queue = [[start]];
  const visited = new Set([start]);
  while (queue.length) {
    const path = queue.shift();
    const node = path.at(-1);
    if (node === goal) return path;
    for (const next of graph.get(node) ?? []) {
      if (!visited.has(next)) {
        visited.add(next);
        queue.push([...path, next]);
      }
    }
  }
  return null;
}
shortestPath(graph, "A", "F"); // ["A", "B", "D", "F"]

// DFS — count connected components / islands (grid version)
function numIslands(grid) {
  let count = 0;
  const rows = grid.length, cols = grid[0].length;
  const sink = (r, c) => {
    if (r < 0 || c < 0 || r >= rows || c >= cols || grid[r][c] !== "1") return;
    grid[r][c] = "0";
    sink(r + 1, c); sink(r - 1, c); sink(r, c + 1); sink(r, c - 1);
  };
  for (let r = 0; r < rows; r++)
    for (let c = 0; c < cols; c++)
      if (grid[r][c] === "1") { count++; sink(r, c); }
  return count;
}

// Topological sort (Kahn's algorithm) — order tasks by dependencies; detects cycles
function topoSort(deps) {                 // deps: { task: [tasks it depends on] }
  const indegree = new Map(), next = new Map();
  for (const [task, reqs] of Object.entries(deps)) {
    indegree.set(task, indegree.get(task) ?? 0);
    for (const r of reqs) {
      indegree.set(r, indegree.get(r) ?? 0);
      indegree.set(task, indegree.get(task) + 1);
      next.set(r, [...(next.get(r) ?? []), task]);
    }
  }
  const queue = [...indegree].filter(([, d]) => d === 0).map(([t]) => t);
  const order = [];
  while (queue.length) {
    const t = queue.shift();
    order.push(t);
    for (const n of next.get(t) ?? []) {
      indegree.set(n, indegree.get(n) - 1);
      if (indegree.get(n) === 0) queue.push(n);
    }
  }
  if (order.length !== indegree.size) throw new Error("Cycle detected");
  return order;
}
topoSort({ build: ["install"], test: ["build"], deploy: ["test", "build"], install: [] });
// ["install", "build", "test", "deploy"]
```

**Dijkstra** (shortest path with positive weights) = BFS with a **min-heap** keyed by distance, O((V + E) log V).

---

### 11. Sorting algorithms

In real code use `arr.sort((a, b) => a - b)` / `toSorted` (TimSort: O(n log n), **stable**). Know these for interviews:

| Algorithm | Time (avg / worst) | Space | Stable | Notes |
|---|---|---|---|---|
| Bubble / Insertion | O(n²) | O(1) | ✅ | Insertion sort is fast on nearly-sorted/small arrays |
| Merge sort | O(n log n) / O(n log n) | O(n) | ✅ | Divide & conquer, predictable |
| Quick sort | O(n log n) / O(n²) | O(log n) | ❌ | Fast in practice; bad pivot → O(n²) |
| Heap sort | O(n log n) | O(1) | ❌ | |
| Counting / Radix | O(n + k) | O(k) | ✅ | Integers in a small range |

```js
function mergeSort(arr) {
  if (arr.length <= 1) return arr;
  const mid = arr.length >> 1;
  const left = mergeSort(arr.slice(0, mid)), right = mergeSort(arr.slice(mid));
  const out = [];
  let i = 0, j = 0;
  while (i < left.length && j < right.length) out.push(left[i] <= right[j] ? left[i++] : right[j++]);
  return out.concat(left.slice(i), right.slice(j));
}

function quickSort(arr) {
  if (arr.length <= 1) return arr;
  const pivot = arr[Math.floor(Math.random() * arr.length)];   // random pivot avoids worst case on sorted input
  const less = [], equal = [], greater = [];
  for (const x of arr) (x < pivot ? less : x > pivot ? greater : equal).push(x);
  return [...quickSort(less), ...equal, ...quickSort(greater)];
}
```

**Stable** sort = equal items keep their original order (sort by date, then stably by status → dates stay ordered within each status).

---

### 12. Dynamic Programming (DP)

Break a problem into **overlapping subproblems** and store results so each is solved once. Two styles: **memoization** (top-down recursion + cache) and **tabulation** (bottom-up loop).

```js
// Climbing stairs: ways to climb n steps taking 1 or 2 at a time (Fibonacci pattern)
function climbStairs(n) {
  let a = 1, b = 1;                     // ways(0), ways(1)
  for (let i = 2; i <= n; i++) [a, b] = [b, a + b];
  return b;
}

// Coin change: fewest coins to make amount — O(amount × coins)
function coinChange(coins, amount) {
  const dp = new Array(amount + 1).fill(Infinity);
  dp[0] = 0;
  for (let a = 1; a <= amount; a++)
    for (const c of coins) if (c <= a) dp[a] = Math.min(dp[a], dp[a - c] + 1);
  return dp[amount] === Infinity ? -1 : dp[amount];
}
coinChange([1, 5, 10], 27); // 5 (10+10+5+1+1)

// Memoization example: longest common subsequence
function lcs(a, b) {
  const memo = new Map();
  const go = (i, j) => {
    if (i === a.length || j === b.length) return 0;
    const key = `${i},${j}`;
    if (memo.has(key)) return memo.get(key);
    const res = a[i] === b[j] ? 1 + go(i + 1, j + 1) : Math.max(go(i + 1, j), go(i, j + 1));
    memo.set(key, res);
    return res;
  };
  return go(0, 0);
}
lcs("abcde", "ace"); // 3
```

DP signals: "number of ways", "min/max cost", "can you reach…", choices at each step where brute force repeats work.

### 13. Greedy & intervals

```js
// Merge overlapping intervals — sort, then sweep, O(n log n)
function mergeIntervals(intervals) {
  const sorted = intervals.toSorted((a, b) => a[0] - b[0]);
  const out = [];
  for (const [start, end] of sorted) {
    const last = out.at(-1);
    if (last && start <= last[1]) last[1] = Math.max(last[1], end);
    else out.push([start, end]);
  }
  return out;
}
mergeIntervals([[1, 3], [2, 6], [8, 10], [9, 12]]); // [[1,6],[8,12]]
// Real use: merging calendar busy slots, booking conflicts
```

---

### 14. Pattern cheat sheet

| Problem says… | Try |
|---|---|
| Sorted array, find pair/triplet | Two pointers / binary search |
| Longest/shortest subarray or substring with a condition | Sliding window |
| Range sums, "subarray sum = k" | Prefix sums (+ hash map) |
| "Have we seen this?", counting, grouping | Hash map / Set |
| Matching brackets, undo, "next greater" | Stack / monotonic stack |
| Level by level, shortest path (unweighted) | BFS (queue) |
| Explore all paths, connected components | DFS (recursion / stack) |
| All combinations/permutations/subsets | Backtracking |
| Top K, k-th largest, scheduling by priority | Heap |
| Dependencies / ordering / prerequisites | Topological sort |
| Prefix search, autocomplete | Trie |
| Count ways / min cost with overlapping subproblems | Dynamic programming |
| Linked list middle/cycle | Fast & slow pointers |
| Overlapping ranges | Sort + sweep (intervals) |

### 15. How to solve a problem in an interview

1. **Clarify**: input size, types, duplicates, negatives, empty input, expected output format.
2. **Examples**: walk through a normal case and edge cases out loud.
3. **Brute force first**: state it and its complexity.
4. **Optimize**: which pattern fits? Can a hash map remove a loop? Is the input sorted?
5. **Code** cleanly with good names; talk while you write.
6. **Test** with your examples; check edge cases (empty, one element, all same, very large).
7. **Complexity**: state time and space; mention trade-offs.

### 16. Most asked DSA questions in JS interviews

Arrays/strings: two sum, best time to buy/sell stock, contains duplicate, product of array except self, maximum subarray (Kadane), merge intervals, rotate array, valid anagram, group anagrams, longest substring without repeating chars, valid palindrome, longest common prefix.
Stack/queue: valid parentheses, min stack, daily temperatures, implement queue using stacks.
Linked list: reverse list, merge two sorted lists, detect cycle, remove nth from end, middle node.
Trees: max depth, invert tree, level order, validate BST, lowest common ancestor, serialize/deserialize.
Graphs: number of islands, clone graph, course schedule (topological sort), shortest path in grid.
DP: climbing stairs, house robber, coin change, longest increasing subsequence, LCS.
Heap: kth largest element, top K frequent, merge K sorted lists.
Frontend-flavoured: flatten nested array/object, deep clone, debounce/throttle, LRU cache, event emitter, DOM tree traversal, build tree from flat list, autocomplete with a trie.

```js
// Kadane's algorithm — maximum subarray sum, O(n)
function maxSubArray(nums) {
  let best = nums[0], current = nums[0];
  for (let i = 1; i < nums.length; i++) {
    current = Math.max(nums[i], current + nums[i]);   // extend or restart
    best = Math.max(best, current);
  }
  return best;
}
maxSubArray([-2, 1, -3, 4, -1, 2, 1, -5, 4]); // 6 ([4,-1,2,1])

// Best time to buy and sell stock (one transaction), O(n)
function maxProfit(prices) {
  let minPrice = Infinity, best = 0;
  for (const p of prices) {
    minPrice = Math.min(minPrice, p);
    best = Math.max(best, p - minPrice);
  }
  return best;
}

// Product of array except self — no division, O(n)
function productExceptSelf(nums) {
  const out = new Array(nums.length).fill(1);
  let left = 1;
  for (let i = 0; i < nums.length; i++) { out[i] = left; left *= nums[i]; }
  let right = 1;
  for (let i = nums.length - 1; i >= 0; i--) { out[i] *= right; right *= nums[i]; }
  return out;
}
```

### Interview Qs

1. What is Big-O? Time vs space complexity?
2. Why is `array.shift()` slow for queues? How would you build an O(1) queue?
3. Array vs linked list — trade-offs?
4. When would you use a Map/Set instead of an array?
5. BFS vs DFS — when to use each?
6. What is a heap? JS doesn't have one — how do you get a priority queue?
7. What is a trie and where is it used in frontend?
8. What is memoization vs tabulation?
9. What does "stable sort" mean? Is `Array.prototype.sort` stable? → Yes (required since ES2019).
10. How do you detect a cycle in a linked list / a dependency graph?

---

## 57. Output-Based Questions

Try to answer each before reading the answer.

**Q1**
```js
console.log(a);
var a = 1;
console.log(b);
let b = 2;
```
> `undefined`, then `ReferenceError: Cannot access 'b' before initialization`.

**Q2**
```js
for (var i = 0; i < 3; i++) setTimeout(() => console.log(i));
```
> `3 3 3`

**Q3**
```js
console.log(1);
setTimeout(() => console.log(2));
Promise.resolve().then(() => console.log(3));
console.log(4);
```
> `1 4 3 2`

**Q4**
```js
const obj = {
  name: "A",
  regular() { return this.name; },
  arrow: () => this?.name,
};
console.log(obj.regular(), obj.arrow());
```
> `A undefined`

**Q5**
```js
console.log([] + []);
console.log([] + {});
console.log(1 + "1" - 1);
console.log("b" + "a" + +"a" + "a");
```
> `""`, `"[object Object]"`, `10`, `"baNaNa"`

**Q6**
```js
console.log(typeof typeof 1);
```
> `"string"`

**Q7**
```js
let x = 1;
function f() {
  console.log(x);
  let x = 2;
}
f();
```
> `ReferenceError` (inner x in TDZ shadows outer x).

**Q8**
```js
const a = {};
const b = { key: "b" };
const c = { key: "c" };
a[b] = 123;
a[c] = 456;
console.log(a[b]);
```
> `456` — both objects become the key `"[object Object]"`.

**Q9**
```js
function foo() {
  return
  {
    ok: true;
  }
}
console.log(foo());
```
> `undefined` — automatic semicolon insertion after `return`.

**Q10**
```js
const p = new Promise((res) => {
  console.log(1);
  res(2);
  console.log(3);
});
p.then(console.log);
console.log(4);
```
> `1 3 4 2`

**Q11**
```js
console.log(0.1 + 0.2 === 0.3, 0.1 + 0.2);
```
> `false 0.30000000000000004`

**Q12**
```js
const arr = [1, 2, 3];
arr[10] = 11;
console.log(arr.length, arr.filter(() => true).length);
```
> `11 4` (empty slots skipped by filter).

**Q13**
```js
console.log([10, 1, 3].sort());
```
> `[1, 10, 3]`

**Q14**
```js
function Person() { this.name = "A"; }
Person.prototype.name = "B";
const p = new Person();
delete p.name;
console.log(p.name);
```
> `"B"` — falls back to the prototype.

**Q15**
```js
async function f() { return 1; }
console.log(f());
```
> `Promise { 1 }`

**Q16**
```js
console.log("start");
setTimeout(() => console.log("timeout"), 0);
(async () => {
  console.log("async start");
  await null;
  console.log("after await");
})();
Promise.resolve().then(() => console.log("then"));
console.log("end");
```
> `start, async start, end, after await, then, timeout`

**Q17**
```js
const user = { name: "A", greet() { return () => this.name; } };
const fn = user.greet();
console.log(fn());
```
> `"A"` — arrow captures `this` of greet, which is `user`.

**Q18**
```js
let a = { n: 1 };
let b = a;
a.x = a = { n: 2 };
console.log(a.x, b.x);
```
> `undefined { n: 2 }` — `a.x` target is resolved before assignment (on the old object).

**Q19**
```js
console.log(null == 0, null >= 0, undefined == 0);
```
> `false true false`

**Q20**
```js
const fns = [];
for (let i = 0; i < 3; i++) fns.push(() => i);
console.log(fns.map((f) => f()));
```
> `[0, 1, 2]`

**Q21**
```js
console.log(Math.max(), Math.min());
```
> `-Infinity Infinity`

**Q22**
```js
console.log([1, 2, 3].map(parseInt));
```
> `[1, NaN, NaN]` — `parseInt("2", 1)` and `parseInt("3", 2)` are invalid.

**Q23**
```js
var name = "global";
const obj = {
  name: "obj",
  getName: function () {
    return function () { return this.name; };
  },
};
console.log(obj.getName()());
```
> `"global"` in browser non-strict (plain call → window.name); `undefined` in Node/strict.

**Q24**
```js
Promise.resolve(1)
  .then((x) => { throw x + 1; })
  .catch((x) => x + 1)
  .then(console.log);
```
> `3`

**Q25**
```js
console.log(1 < 2 < 3, 3 > 2 > 1);
```
> `true false` — `3 > 2` → `true` → `true > 1` → `1 > 1` → false.

**Q26**
```js
const s = new Set([1, "1", 1, NaN, NaN]);
console.log(s.size);
```
> `3`

**Q27**
```js
function test(a, b = 2) {}
console.log(test.length);
```
> `1`

**Q28**
```js
setTimeout(() => console.log("A"), 0);
setImmediate?.(() => console.log("B")); // Node
process.nextTick?.(() => console.log("C"));
Promise.resolve().then(() => console.log("D"));
```
> Node: `C D A B` (A/B order can vary in the main module, but inside an I/O callback setImmediate comes first).

**Q29**
```js
const counter = (() => { let c = 0; return () => ++c; })();
counter(); counter();
console.log(counter());
```
> `3`

**Q30**
```js
console.log(typeof NaN, typeof null, typeof [], typeof class {});
```
> `number object object function`

---

## 58. Most Asked Interview Questions

### Fundamentals

1. **What are the data types in JS?** → 7 primitives (string, number, bigint, boolean, undefined, null, symbol) + object.
2. **Difference between `null` and `undefined`?** → undefined = not assigned by JS; null = intentionally empty, assigned by the dev.
3. **`==` vs `===`?** → Loose equality with coercion vs strict equality without.
4. **`var` vs `let` vs `const`?** → Scope (function vs block), hoisting (undefined vs TDZ), redeclaration, reassignment.
5. **What is hoisting?** → Declarations are set up in memory during the creation phase before code runs.
6. **What is the Temporal Dead Zone?** → Period between block start and let/const declaration where access throws.
7. **What is scope & scope chain?** → Visibility of variables; lookup walks outward through lexical environments.
8. **What is lexical scope?** → Scope decided by where functions are written, not called.
9. **What is a closure? Give real use cases.** → Function + remembered lexical environment; private state, memoize, debounce, hooks.
10. **What is an execution context?** → Environment holding variables, scope chain and `this`; created in two phases.
11. **Explain the call stack.** → LIFO stack tracking function calls.
12. **What is `this`? How is it decided?** → new > explicit > implicit > default; arrows are lexical.
13. **call vs apply vs bind?** → Invoke with args list / array / return bound function.
14. **Arrow vs regular function?** → this, arguments, new, prototype, hoisting.
15. **What is an IIFE and why?** → Immediately runs, creates private scope.
16. **What are first-class & higher-order functions?**
17. **Pure functions and side effects?**
18. **What is currying? Implement `sum(1)(2)(3)`.**
19. **Debounce vs throttle — implement both.**
20. **What is memoization?**

### Objects & Prototypes

21. **What is prototypal inheritance?**
22. **`__proto__` vs `prototype`?**
23. **How does `new` work? Implement it.**
24. **Class vs constructor function?**
25. **Shallow vs deep copy — how to deep copy?** → `structuredClone`, recursion, JSON (limited).
26. **`Object.freeze` vs `Object.seal`?**
27. **Map vs Object; WeakMap vs Map?**
28. **How do you check if a key exists in an object?** → `in`, `Object.hasOwn`, `?.`.
29. **What is optional chaining & nullish coalescing?**
30. **What are getters/setters & property descriptors?**

### Async

31. **Explain the event loop.** (Know the diagram and microtask vs macrotask.)
32. **What are promises? States?**
33. **Promise.all vs allSettled vs race vs any.**
34. **Implement Promise.all.**
35. **async/await vs promises.**
36. **How do you handle errors in async/await?**
37. **What is callback hell and how to avoid it?**
38. **How to run promises in parallel vs sequence? With a concurrency limit?**
39. **setTimeout 0 — why isn't it instant?**
40. **How to cancel a fetch request?** → AbortController.

### Arrays & Strings

41. **map vs forEach vs filter vs reduce.**
42. **Implement map/filter/reduce polyfills.**
43. **slice vs splice.**
44. **How to remove duplicates from an array?** → `[...new Set(arr)]`.
45. **Flatten a nested array.** → `flat(Infinity)` or recursion.
46. **Why does `[10,1,3].sort()` give wrong output?**
47. **Check if two strings are anagrams / palindrome.**
48. **Find the most frequent element.**

### Browser

49. **Event bubbling vs capturing vs delegation.**
50. **`e.target` vs `e.currentTarget`.**
51. **preventDefault vs stopPropagation.**
52. **localStorage vs sessionStorage vs cookies.**
53. **async vs defer scripts.**
54. **What is the critical rendering path? Reflow vs repaint?**
55. **What is CORS?**
56. **What is XSS / CSRF and how to prevent them?**
57. **How does garbage collection work? Common memory leaks?**
58. **Web Workers vs Service Workers.**

### Misc

59. **What is strict mode?**
60. **CommonJS vs ES modules?**
61. **What are generators and iterators?**
62. **What is a Symbol used for?**
63. **What is a Proxy?**
64. **What is event-driven programming?**
65. **What's new in ES6+?**
66. **Is JS pass-by-value or pass-by-reference?** → Always pass-by-value; for objects the value is a reference (sometimes called "pass by sharing").

```js
function change(obj) {
  obj.a = 2;        // mutates the shared object -> visible outside
  obj = { a: 3 };   // re-assigns local copy of the reference -> not visible outside
}
const o = { a: 1 };
change(o);
console.log(o.a); // 2
```

67. **What is the difference between `Object.keys` and `for...in`?** → keys = own enumerable only; for...in includes inherited enumerable.
68. **What is `globalThis`?** → Standard way to reach the global object in any environment.
69. **What is a polyfill vs a transpiler?** → Polyfill adds missing APIs at runtime (e.g. `Array.prototype.flat`); transpiler (Babel/TS/SWC) rewrites new syntax into older syntax (e.g. `?.`).
70. **What is `Object.is`?** → Like `===` but `NaN` equals `NaN` and `0 !== -0`.

### Machine coding / DSA style questions in JS interviews

- Implement `debounce`, `throttle`, `memoize`, `curry`, `once`, `pipe/compose`.
- Implement `Promise.all`, `Promise.race`, a promise pool with a concurrency limit, `retry`.
- Implement an `EventEmitter` with `on/off/once/emit`.
- Implement `deepClone`, `deepEqual`, `flatten` (array & object), lodash `get`.
- Implement an LRU cache.
- Implement `Array.prototype.map/filter/reduce`, `Function.prototype.bind`.
- Build a todo list / autocomplete with debounce / infinite scroll / star rating / tabs / modal in vanilla JS.
- Implement a `sleep`, `setInterval` with `setTimeout`, a task scheduler.
- Two-sum, anagram groups, balanced parentheses, reverse words, chunk array, group by.

```js
// Two sum — O(n)
function twoSum(nums, target) {
  const seen = new Map();
  for (let i = 0; i < nums.length; i++) {
    const need = target - nums[i];
    if (seen.has(need)) return [seen.get(need), i];
    seen.set(nums[i], i);
  }
  return [];
}

// Balanced parentheses
function isBalanced(s) {
  const pairs = { ")": "(", "]": "[", "}": "{" };
  const stack = [];
  for (const ch of s) {
    if ("([{".includes(ch)) stack.push(ch);
    else if (ch in pairs && stack.pop() !== pairs[ch]) return false;
  }
  return stack.length === 0;
}

// Group anagrams
const groupAnagrams = (words) =>
  Object.values(words.reduce((acc, w) => {
    const key = [...w].sort().join("");
    (acc[key] ??= []).push(w);
    return acc;
  }, {}));
```

---

**End of JavaScript notes.** Next: `typescript.md`, `react.md`, `nodejs.md`.
