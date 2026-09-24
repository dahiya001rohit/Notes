# React — Complete Notes

> Every major React concept, each with an explanation, 2–3 examples and interview questions.
> Covers React 18 & 19, hooks, performance, patterns, routing, state management, data fetching, testing and Next.js basics.
> The **Most Asked Interview Questions** are at the end.

---

## Table of Contents

1. [What is React](#1-what-is-react)
2. [JSX](#2-jsx)
3. [Components](#3-components)
4. [Props](#4-props)
5. [State & useState](#5-state--usestate)
6. [Event Handling (Synthetic Events)](#6-event-handling)
7. [Conditional Rendering](#7-conditional-rendering)
8. [Lists & Keys](#8-lists--keys)
9. [Forms: Controlled vs Uncontrolled](#9-forms-controlled-vs-uncontrolled)
10. [Rendering: when & why components re-render](#10-rendering--re-rendering)
11. [Virtual DOM, Reconciliation, Diffing & Fiber](#11-virtual-dom-reconciliation--fiber)
12. [useEffect](#12-useeffect)
13. [useRef](#13-useref)
14. [useContext & Context API](#14-usecontext--context-api)
15. [useReducer](#15-usereducer)
16. [useMemo](#16-usememo)
17. [useCallback](#17-usecallback)
18. [React.memo](#18-reactmemo)
19. [useLayoutEffect & useInsertionEffect](#19-uselayouteffect--useinsertioneffect)
20. [useImperativeHandle & forwardRef](#20-useimperativehandle--forwardref)
21. [useId, useTransition, useDeferredValue, useSyncExternalStore, useDebugValue](#21-more-hooks)
22. [React 19: Actions, use, useActionState, useOptimistic, useFormStatus](#22-react-19-features)
23. [Rules of Hooks](#23-rules-of-hooks)
24. [How Hooks Work Under the Hood (+ Children & cloneElement APIs)](#24-how-hooks-work-under-the-hood--children--cloneelement-apis)
25. [Custom Hooks](#25-custom-hooks)
26. [Lifting State Up & Prop Drilling](#26-lifting-state-up--prop-drilling)
27. [Component Lifecycle (Class Components)](#27-component-lifecycle-class-components)
28. [Fragments & Portals](#28-fragments--portals)
29. [Error Boundaries](#29-error-boundaries)
30. [Code Splitting: lazy & Suspense](#30-code-splitting-lazy--suspense)
31. [Advanced Patterns: HOC, Render Props, Compound Components, Controlled Props](#31-advanced-patterns)
32. [Performance Optimization](#32-performance-optimization)
33. [React 18: Concurrent Rendering & Automatic Batching](#33-react-18-concurrent-features)
34. [Strict Mode](#34-strict-mode)
35. [React Router](#35-react-router)
36. [State Management: Redux Toolkit, Zustand, Context](#36-state-management)
37. [State Management II: Choosing a Tool, Jotai, Redux-Saga & State Machines](#37-state-management-ii-choosing-a-tool-jotai-redux-saga--state-machines)
38. [Data Fetching: fetch, TanStack Query](#38-data-fetching)
39. [Styling in React](#39-styling)
40. [Internationalization (i18n), Theming & Dark Mode, Design Tokens](#40-internationalization-i18n-theming--dark-mode-design-tokens)
41. [Rendering Strategies: CSR, SSR, SSG, ISR, RSC](#41-rendering-strategies-csr-ssr-ssg-isr)
42. [Server Components & Next.js Basics](#42-server-components--nextjs-basics)
43. [Hydration](#43-hydration)
44. [Next.js App Router Deep Dive (+ Animations)](#44-nextjs-app-router-deep-dive--animations)
45. [Testing React](#45-testing-react)
46. [Testing React in Depth: Providers, MSW, Async UI, Router, Query & Playwright](#46-testing-react-in-depth-providers-msw-async-ui-router-query--playwright)
47. [Accessibility (a11y)](#47-accessibility-a11y)
48. [Security in React](#48-security-in-react)
49. [Folder Structure & Best Practices](#49-folder-structure--best-practices)
50. [Common Mistakes / Anti-patterns](#50-common-mistakes)
51. [Production React Patterns](#51-production-react-patterns)
52. [Real-time & Rich Interactions: WebSockets, Uploads with Progress, Drag & Drop](#52-real-time--rich-interactions-websockets-uploads-with-progress-drag--drop)
53. [Machine Coding Questions (with solutions)](#53-machine-coding-questions)
54. [Machine Coding II (Carousel, Kanban, Data Table, Wizard, Toasts, Comments)](#54-machine-coding-ii-carousel-kanban-data-table-wizard-toasts-comments)
55. [Output / Behaviour Questions](#55-output--behaviour-questions)
56. [Most Asked Interview Questions](#56-most-asked-interview-questions)

---

## 1. What is React

**React** is a JavaScript **library** (not a framework) for building user interfaces, made by Meta.

Key ideas:
- **Component-based** — UI is split into reusable, independent pieces.
- **Declarative** — you describe *what* the UI should look like for a given state; React figures out *how* to update the DOM.
- **Unidirectional data flow** — data flows parent → child via props.
- **Virtual DOM** — React keeps a lightweight tree in memory and updates only what changed.
- **"Learn once, write anywhere"** — React DOM (web), React Native (mobile), etc.

### Declarative vs Imperative

```js
// Imperative (vanilla JS): tell the browser each step
const btn = document.createElement("button");
btn.textContent = "Count: 0";
let count = 0;
btn.onclick = () => { count++; btn.textContent = `Count: ${count}`; };
document.body.append(btn);
```

```jsx
// Declarative (React): describe UI as a function of state
function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>Count: {count}</button>;
}
```

### Library vs Framework

React only handles the **view layer**. Routing, data fetching, forms, etc. come from libraries (React Router, TanStack Query) or a framework built on React (Next.js, Remix/React Router v7).

### Setting up a project

```bash
npm create vite@latest my-app -- --template react-ts
npx create-next-app@latest my-app
```

(Create React App is deprecated.)

**Interview Qs**
- Why React? → Components, declarative, virtual DOM efficiency, huge ecosystem, one-way data flow, hooks.
- Is React a framework? → No, a UI library.
- What is SPA? → Single Page Application: one HTML page; JS swaps views without full page reloads.

---

## 2. JSX

**JSX** = JavaScript XML. A syntax extension that lets you write HTML-like code in JS. It is compiled (Babel/SWC/esbuild) to `React.createElement` calls (or `jsx()` from `react/jsx-runtime` in the new transform).

```jsx
const el = <h1 className="title">Hello</h1>;
// compiles to:
const el2 = React.createElement("h1", { className: "title" }, "Hello");
// new JSX transform:
import { jsx as _jsx } from "react/jsx-runtime";
const el3 = _jsx("h1", { className: "title", children: "Hello" });
```

A React element is just a plain object:

```js
{ type: "h1", props: { className: "title", children: "Hello" }, key: null, ref: null }
```

### JSX rules

1. Return a **single root** element (use a Fragment `<>...</>` if needed).
2. Close all tags: `<img />`, `<br />`.
3. Use **camelCase** attributes: `className`, `htmlFor`, `onClick`, `tabIndex`.
4. `{}` embeds any JS **expression** (not statements like `if`/`for`).
5. `style` takes an object: `style={{ color: "red", fontSize: 16 }}`.
6. Comments: `{/* comment */}`.

### Example 1 — expressions

```jsx
function Greeting({ user }) {
  const hour = new Date().getHours();
  return (
    <div>
      <h1>Hello, {user.firstName + " " + user.lastName}!</h1>
      <p>{hour < 12 ? "Good morning" : "Good evening"}</p>
      <p>Items: {[1, 2, 3].map((n) => n * 2).join(", ")}</p>
    </div>
  );
}
```

### Example 2 — attributes & styles

```jsx
const imgUrl = "/logo.png";
const isActive = true;
<img src={imgUrl} alt="Logo" />;
<div className={`card ${isActive ? "active" : ""}`} style={{ padding: 8, backgroundColor: "#eee" }} />;
<label htmlFor="email">Email</label>;
<input id="email" type="email" disabled={!isActive} />;
```

### Example 3 — what renders

```jsx
<div>
  {true}{false}{null}{undefined}   {/* render nothing */}
  {0}                              {/* renders "0" — trap! */}
  {"text"}{42}                     {/* render as text */}
  {[<li key="a">a</li>, <li key="b">b</li>]} {/* arrays render each item */}
  {{ a: 1 }}                       {/* ❌ Error: objects are not valid as a React child */}
</div>
```

### JSX prevents injection

Values inside `{}` are escaped before rendering, so `<p>{userInput}</p>` is safe from XSS.

**Interview Qs**
- Can browsers read JSX? → No, it must be transpiled.
- Why `className` instead of `class`? → `class` is a reserved word in JS; JSX maps to DOM properties (`element.className`).
- Is JSX mandatory? → No, you can call `createElement` directly, but JSX is standard.

---

## 3. Components

A **component** is a function (or class) that returns React elements (JSX). Names must start with a **capital letter** (lowercase = HTML tag).

### Functional components (modern standard)

```jsx
function Welcome({ name }) {
  return <h1>Hello, {name}</h1>;
}
const Welcome2 = ({ name }) => <h1>Hello, {name}</h1>;
```

### Class components (legacy, still asked)

```jsx
import { Component } from "react";

class Welcome extends Component {
  state = { count: 0 };
  render() {
    return (
      <div>
        <h1>Hello, {this.props.name}</h1>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          {this.state.count}
        </button>
      </div>
    );
  }
}
```

### Functional vs Class

| Functional | Class |
|---|---|
| Plain function | Extends `React.Component` |
| Hooks for state/effects | `this.state`, lifecycle methods |
| No `this` | `this` binding issues |
| Less boilerplate, easier to test | More verbose |
| Recommended | Only needed for Error Boundaries (still) |

### Composition

Build complex UIs by nesting components. React favours **composition over inheritance**.

```jsx
function Card({ title, children }) {
  return (
    <div className="card">
      <h2>{title}</h2>
      <div className="card-body">{children}</div>
    </div>
  );
}

function App() {
  return (
    <Card title="Profile">
      <Avatar />
      <Bio />
    </Card>
  );
}
```

### Presentational vs Container components (pattern)

- **Presentational**: how things look, receive data via props, no data fetching.
- **Container**: how things work, fetch data, hold state, pass to presentational. (Custom hooks mostly replaced this split.)

### Components must be pure

Given the same props/state/context, a component should return the same JSX and not change anything outside itself during render.

```jsx
// ❌ impure — mutates outer variable during render
let guest = 0;
function Cup() { guest++; return <p>Tea cup #{guest}</p>; }

// ✅ pure
function Cup({ guest }) { return <p>Tea cup #{guest}</p>; }
```

### Never define components inside components

```jsx
function Parent() {
  // ❌ new Child type on every render -> remounts, loses state, loses focus
  function Child() { return <input />; }
  return <Child />;
}
```

**Interview Qs**
- Why capital names? → JSX treats lowercase as DOM tags.
- Stateless vs stateful components? → With/without internal state.
- What is `children`? → Special prop holding whatever is between a component's opening and closing tags.

---

## 4. Props

**Props** (properties) are read-only inputs passed from parent to child. They make components reusable.

### Example 1 — passing & destructuring with defaults

```jsx
function Button({ label = "Click", variant = "primary", onClick, disabled }) {
  return (
    <button className={`btn btn-${variant}`} onClick={onClick} disabled={disabled}>
      {label}
    </button>
  );
}

<Button label="Save" variant="success" onClick={handleSave} />
<Button /> {/* uses defaults */}
```

### Example 2 — passing any value (functions, objects, JSX)

```jsx
<UserCard
  user={{ name: "Rohit", age: 25 }}
  onSelect={(id) => console.log(id)}
  icon={<StarIcon />}
  isAdmin            // shorthand for isAdmin={true}
/>
```

### Example 3 — spreading props & rest

```jsx
function Input({ label, ...rest }) {
  return (
    <label>
      {label}
      <input {...rest} />   {/* forwards type, value, onChange, placeholder... */}
    </label>
  );
}
<Input label="Email" type="email" placeholder="you@x.com" required />
```

### Props are immutable

```jsx
function Child(props) {
  props.name = "x"; // ❌ never mutate props
}
```

To change what the parent sees, the parent passes a callback (child → parent communication):

```jsx
function Parent() {
  const [msg, setMsg] = useState("");
  return <Child onSend={setMsg} />;
}
function Child({ onSend }) {
  return <button onClick={() => onSend("Hi from child")}>Send</button>;
}
```

### children prop

```jsx
function Layout({ children }) {
  return <main className="container">{children}</main>;
}
<Layout><h1>Page</h1></Layout>;
```

### Props vs State

| Props | State |
|---|---|
| Passed from parent | Managed inside the component |
| Read-only | Can be updated with setter |
| Changing props → child re-renders | Changing state → component re-renders |
| Like function parameters | Like variables inside a function that persist |

### PropTypes (legacy) vs TypeScript

```tsx
type ButtonProps = { label: string; onClick?: () => void; variant?: "primary" | "danger" };
function Button({ label, onClick, variant = "primary" }: ButtonProps) { /* ... */ }
```

**Interview Qs**
- Can a child change props? → No, props are read-only.
- How does a child talk to a parent? → Callback props.
- Siblings? → Lift state to common parent / context / global store.

---

## 5. State & useState

**State** is data that changes over time and affects what's rendered. When state updates, React **re-renders** the component.

```jsx
const [state, setState] = useState(initialValue);
```

### Example 1 — counter

```jsx
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </>
  );
}
```

### Example 2 — functional updates (when new state depends on old)

State updates are **batched** and state is a **snapshot** for the current render.

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  const addThreeWrong = () => {
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1); // count is 0 in this render -> result: 1
  };

  const addThreeRight = () => {
    setCount((c) => c + 1);
    setCount((c) => c + 1);
    setCount((c) => c + 1); // queued updaters -> result: 3
  };
  // ...
}
```

### Example 3 — objects & arrays (immutability)

Never mutate state directly; always create a new object/array so React detects the change (`Object.is` comparison).

```jsx
const [user, setUser] = useState({ name: "A", address: { city: "Delhi" } });

// ❌ mutation — same reference, React may skip re-render
user.name = "B"; setUser(user);

// ✅ new object
setUser({ ...user, name: "B" });
setUser((u) => ({ ...u, address: { ...u.address, city: "Pune" } }));

const [todos, setTodos] = useState([]);
setTodos([...todos, newTodo]);                                     // add
setTodos(todos.filter((t) => t.id !== id));                        // remove
setTodos(todos.map((t) => (t.id === id ? { ...t, done: !t.done } : t))); // update
setTodos([...todos].sort((a, b) => a.title.localeCompare(b.title)));    // sort copy
```

### Lazy initial state

If the initial value is expensive, pass a function — it runs only on the first render.

```jsx
const [data, setData] = useState(() => JSON.parse(localStorage.getItem("data")) ?? []);
// vs useState(JSON.parse(...)) -> runs on every render (result ignored)
```

### State is a snapshot

```jsx
function Demo() {
  const [n, setN] = useState(0);
  const handle = () => {
    setN(n + 5);
    console.log(n);        // still 0 — logs the snapshot
    setTimeout(() => alert(n), 3000); // alerts 0 even after re-render
  };
}
```

### Same value → bail out

If you set the same value (`Object.is`), React skips re-rendering children.

### State structure principles

1. Group related state (`{x, y}` instead of two states that always change together).
2. Avoid contradictions (`isSending` + `isSent` → one `status` string).
3. **Avoid redundant/derived state** — compute during render.
4. Avoid duplication (store `selectedId` rather than a copy of the selected object).
5. Avoid deeply nested state (normalize).

```jsx
// ❌ derived state stored
const [items, setItems] = useState([]);
const [count, setCount] = useState(0); // must be kept in sync manually

// ✅ derive
const count = items.length;
const fullName = `${first} ${last}`;
const visible = todos.filter((t) => (filter === "done" ? t.done : true));
```

**Interview Qs**
- Why not mutate state directly? → React compares references; mutation won't trigger a render and breaks memoization/time-travel.
- Is setState sync or async? → Updates are queued and batched; the new value is available on the next render.
- Why use the functional updater? → When the next state depends on the previous, especially with multiple updates or stale closures.

---

## 6. Event Handling

React uses **SyntheticEvent** — a cross-browser wrapper around the native event with the same interface (`e.target`, `e.preventDefault()`, `e.stopPropagation()`). React 17+ attaches listeners at the **root container** (event delegation), not on `document`.

### Example 1 — basics

```jsx
function Form() {
  const handleClick = (e) => console.log("clicked", e.target);
  const handleSubmit = (e) => {
    e.preventDefault();       // must call explicitly; `return false` doesn't work
    console.log("submitted");
  };
  return (
    <form onSubmit={handleSubmit}>
      <button type="button" onClick={handleClick}>Click</button>
      <button type="submit">Submit</button>
    </form>
  );
}
```

### Example 2 — passing arguments

```jsx
// ❌ calls immediately on render
<button onClick={deleteItem(id)}>Delete</button>

// ✅ wrap in arrow function
<button onClick={() => deleteItem(id)}>Delete</button>
<button onClick={(e) => deleteItem(id, e)}>Delete</button>

// ✅ data attributes
<button data-id={id} onClick={(e) => deleteItem(e.currentTarget.dataset.id)}>Delete</button>
```

### Example 3 — propagation

```jsx
function Toolbar() {
  return (
    <div onClick={() => alert("toolbar")}>
      <button onClick={(e) => { e.stopPropagation(); alert("play"); }}>Play</button>
    </div>
  );
}
// capture phase: onClickCapture
<div onClickCapture={() => console.log("captured first")} />
```

### Common events

`onClick`, `onChange`, `onSubmit`, `onInput`, `onKeyDown`, `onKeyUp`, `onFocus`, `onBlur`, `onMouseEnter`, `onMouseLeave`, `onScroll`, `onDrag*`, `onPointerDown`, `onCopy`, `onPaste`.

Note: React's `onChange` fires on **every keystroke** (like native `input` event), not on blur.

### Typing events (TS)

```tsx
const onChange = (e: React.ChangeEvent<HTMLInputElement>) => setValue(e.target.value);
const onSubmit = (e: React.FormEvent<HTMLFormElement>) => e.preventDefault();
const onClick = (e: React.MouseEvent<HTMLButtonElement>) => {};
```

**Interview Qs**
- What are synthetic events? → React's normalized event wrapper for cross-browser consistency.
- Event pooling? → Removed in React 17 (used to reuse event objects; you had to call `e.persist()`).
- Where does React attach listeners? → Root container (React 17+).

---

## 7. Conditional Rendering

### Example 1 — if / early return

```jsx
function Dashboard({ user, loading, error }) {
  if (loading) return <Spinner />;
  if (error) return <ErrorMessage error={error} />;
  if (!user) return null; // render nothing
  return <h1>Welcome {user.name}</h1>;
}
```

### Example 2 — ternary & &&

```jsx
{isLoggedIn ? <Logout /> : <Login />}
{cart.length > 0 && <CartBadge count={cart.length} />}

// ⚠️ && with numbers
{items.length && <List />}      // renders "0" when empty!
{items.length > 0 && <List />}  // ✅
{!!items.length && <List />}    // ✅
```

### Example 3 — object map / switch

```jsx
const statusUI = {
  loading: <Spinner />,
  success: <Data />,
  error: <ErrorBox />,
};
return statusUI[status] ?? null;

function Icon({ type }) {
  switch (type) {
    case "success": return <CheckIcon />;
    case "error": return <XIcon />;
    default: return <InfoIcon />;
  }
}
```

### Hiding vs unmounting

```jsx
{show && <Modal />}                              // unmounts -> state lost
<Modal style={{ display: show ? "block" : "none" }} /> // stays mounted -> state kept
```

---

## 8. Lists & Keys

Render lists with `map`. Each item needs a **unique, stable `key`** among siblings.

### Example 1

```jsx
const users = [{ id: 1, name: "A" }, { id: 2, name: "B" }];
<ul>
  {users.map((u) => <li key={u.id}>{u.name}</li>)}
</ul>
```

### Why keys?

Keys tell React **which item is which** between renders so it can reorder/reuse DOM nodes and component state correctly instead of re-creating everything.

### Example 2 — why index as key is bad

```jsx
function TodoList() {
  const [todos, setTodos] = useState([{ id: 1, text: "A" }, { id: 2, text: "B" }]);
  const addTop = () => setTodos([{ id: Date.now(), text: "New" }, ...todos]);
  return (
    <>
      <button onClick={addTop}>Add to top</button>
      {todos.map((t, index) => (
        <div key={index}>          {/* ❌ */}
          {t.text} <input />       {/* typed input text shifts to the wrong item! */}
        </div>
      ))}
    </>
  );
}
```

When items are inserted/removed/reordered, index keys make React match the wrong components → wrong state, bugs with inputs, and unnecessary re-renders.

Index as key is OK only when: the list is static, never reordered/filtered, and items have no state.

### Example 3 — Fragment with key

```jsx
{glossary.map((item) => (
  <Fragment key={item.id}>
    <dt>{item.term}</dt>
    <dd>{item.description}</dd>
  </Fragment>
))}
```

### Key rules

- Unique among **siblings** only (not globally).
- Don't generate on the fly (`key={Math.random()}` → remounts every render).
- `key` isn't passed as a prop to the child (pass `id` separately if needed).
- Keys can also be used outside lists to **reset** a component's state.

**Interview Qs**
- Why are keys important? → Efficient, correct reconciliation.
- Can we use index as a key? → Only for static lists.
- Where do you put the key? → On the outermost element returned in `map`.

---

## 9. Forms: Controlled vs Uncontrolled

### Controlled component

Form value is stored in **React state**; the input reflects state and updates via `onChange`. React is the "single source of truth".

```jsx
function LoginForm() {
  const [form, setForm] = useState({ email: "", password: "", remember: false });
  const [errors, setErrors] = useState({});

  const handleChange = (e) => {
    const { name, value, type, checked } = e.target;
    setForm((f) => ({ ...f, [name]: type === "checkbox" ? checked : value }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    const errs = {};
    if (!form.email.includes("@")) errs.email = "Invalid email";
    if (form.password.length < 6) errs.password = "Min 6 chars";
    setErrors(errs);
    if (Object.keys(errs).length === 0) console.log("submit", form);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="email" value={form.email} onChange={handleChange} />
      {errors.email && <span>{errors.email}</span>}
      <input name="password" type="password" value={form.password} onChange={handleChange} />
      {errors.password && <span>{errors.password}</span>}
      <label>
        <input name="remember" type="checkbox" checked={form.remember} onChange={handleChange} /> Remember
      </label>
      <button disabled={!form.email || !form.password}>Login</button>
    </form>
  );
}
```

Other controlled inputs:

```jsx
<textarea value={bio} onChange={(e) => setBio(e.target.value)} />
<select value={country} onChange={(e) => setCountry(e.target.value)}>
  <option value="in">India</option>
  <option value="us">USA</option>
</select>
<input type="radio" name="size" value="M" checked={size === "M"} onChange={(e) => setSize(e.target.value)} />
```

### Uncontrolled component

The **DOM** holds the value; read it with a `ref` or `FormData` when needed.

```jsx
function Uncontrolled() {
  const nameRef = useRef(null);
  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(nameRef.current.value);
    const data = Object.fromEntries(new FormData(e.currentTarget)); // all fields by name
    console.log(data);
  };
  return (
    <form onSubmit={handleSubmit}>
      <input ref={nameRef} name="name" defaultValue="Rohit" />
      <input type="file" name="avatar" /> {/* file inputs are always uncontrolled */}
      <button>Save</button>
    </form>
  );
}
```

### Controlled vs Uncontrolled

| Controlled | Uncontrolled |
|---|---|
| `value` + `onChange` | `defaultValue` + `ref` / FormData |
| React state is source of truth | DOM is source of truth |
| Instant validation, conditional UI, formatting | Less code, fewer re-renders |
| Re-renders on every keystroke | Good for simple forms / file inputs / integrating non-React code |

### Warning: switching controlled ↔ uncontrolled

```jsx
const [v, setV] = useState();       // undefined -> uncontrolled at first
<input value={v} onChange={...} />  // warning when it becomes defined
// Fix: useState("")
```

### Form libraries

**React Hook Form** (uncontrolled + refs → fast) with **Zod** for schema validation; Formik (older).

```jsx
import { useForm } from "react-hook-form";
import { z } from "zod";
import { zodResolver } from "@hookform/resolvers/zod";

const schema = z.object({ email: z.string().email(), age: z.coerce.number().min(18) });

function SignUp() {
  const { register, handleSubmit, formState: { errors, isSubmitting } } = useForm({ resolver: zodResolver(schema) });
  return (
    <form onSubmit={handleSubmit(async (data) => await api.signUp(data))}>
      <input {...register("email")} />
      {errors.email && <p>{errors.email.message}</p>}
      <input {...register("age")} />
      <button disabled={isSubmitting}>Sign up</button>
    </form>
  );
}
```

**Interview Qs**
- Controlled vs uncontrolled? (table)
- How to handle multiple inputs with one handler? → `name` attribute + computed key `[name]: value`.

---

## 10. Rendering & Re-rendering

"Rendering" = React **calling your component function** to get JSX. It does NOT necessarily mean DOM updates.

### Three steps

1. **Trigger** — initial render (`createRoot().render()`) or a state update.
2. **Render** — React calls components and diffs.
3. **Commit** — React touches the DOM only where needed.

### When does a component re-render?

1. Its **state** changes (setState with a new value).
2. Its **parent re-renders** (by default, all children re-render, even if props didn't change!).
3. A **context** it consumes changes.
4. A custom hook it uses changes state internally.

**Props changing is not itself a trigger** — props change because the parent re-rendered.

### Example 1 — children re-render with parent

```jsx
function Parent() {
  const [count, setCount] = useState(0);
  return (
    <>
      <button onClick={() => setCount((c) => c + 1)}>{count}</button>
      <Child /> {/* re-renders every click even with no props */}
    </>
  );
}
function Child() {
  console.log("Child rendered");
  return <p>Child</p>;
}
```

### Example 2 — fix by moving state down

```jsx
function Parent() {
  return (
    <>
      <CounterButton /> {/* state lives here now */}
      <Child />         {/* no longer re-renders */}
    </>
  );
}
```

### Example 3 — fix by passing as children ("lift content up")

```jsx
function ScrollTracker({ children }) {
  const [y, setY] = useState(0);
  useEffect(() => {
    const onScroll = () => setY(window.scrollY);
    window.addEventListener("scroll", onScroll);
    return () => window.removeEventListener("scroll", onScroll);
  }, []);
  return <div data-y={y}>{children}</div>; // children elements were created by the parent -> not re-rendered
}

<ScrollTracker><ExpensiveTree /></ScrollTracker>
```

### Rendering root

```jsx
import { createRoot } from "react-dom/client";
createRoot(document.getElementById("root")).render(<App />);
```

**Interview Qs**
- Does a child re-render if its props don't change? → Yes if the parent re-renders, unless wrapped in `React.memo`.
- Does re-render mean DOM update? → No; DOM updates only when the diff finds changes.

---

## 11. Virtual DOM, Reconciliation & Fiber

### Virtual DOM

A lightweight **JS object representation** of the real DOM. On every state change:

1. React re-renders components → produces a new virtual DOM tree.
2. **Diffing**: compares new tree with the previous one.
3. **Commit**: applies only the minimal changes to the real DOM.

Real DOM operations (layout, paint) are expensive; JS object comparisons are cheap. The main benefit is actually the **declarative programming model** with acceptable performance, not that VDOM is "faster than the DOM".

### Reconciliation & the diffing algorithm

Comparing two trees generically is O(n³). React uses heuristics to make it **O(n)**:

1. **Different element types → rebuild the subtree.** `<div>` → `<span>` or `<A/>` → `<B/>` unmounts the old tree (state lost) and mounts a new one.
2. **Same type DOM element → keep the node, update changed attributes only.**
3. **Same type component → keep instance/state, re-render with new props.**
4. **Lists use `key`** to match children between renders.

```jsx
// Example 1: type change destroys state
{isLoggedIn ? <div><Counter /></div> : <section><Counter /></section>}
// Toggling -> Counter is unmounted & remounted, count resets to 0.
```

```jsx
// Example 2: same position, same type -> state preserved
{isAdmin ? <Counter label="admin" /> : <Counter label="user" />}
// Toggling keeps the same Counter state (same type at same position)

// Force a reset with a key:
{isAdmin ? <Counter key="admin" /> : <Counter key="user" />}
```

```jsx
// Example 3: resetting a form when a different user is selected
<ProfileForm key={userId} user={user} />
```

### Render phase vs Commit phase

- **Render phase**: call components, build new tree, diff. **Pure, no side effects**, can be paused/restarted/thrown away (in concurrent mode).
- **Commit phase**: apply DOM changes, run `useLayoutEffect`, then (asynchronously) `useEffect`. Cannot be interrupted.

### React Fiber

Fiber (React 16+) is the reimplementation of the reconciler. A **fiber** is a JS object representing a unit of work (one per component/element), linked as a tree (child, sibling, return).

What Fiber enables:
- **Incremental rendering** — split rendering work into chunks.
- **Pause, abort or reuse** work.
- **Priorities** — urgent updates (typing) before non-urgent (big list render).
- Foundation for **Concurrent features**, **Suspense**, **transitions**.
- Double buffering: `current` tree vs `workInProgress` tree; swapped on commit.

**Interview Qs**
- What is the virtual DOM? → In-memory UI tree used to compute minimal DOM updates.
- Shadow DOM vs Virtual DOM? → Shadow DOM is a browser feature for encapsulating styles/DOM in web components; VDOM is a React concept.
- What is reconciliation? → Process of diffing and updating the DOM.
- What is React Fiber? → The new reconciliation engine allowing interruptible, prioritized rendering.

---

## 12. useEffect

`useEffect` runs **side effects** after render is committed to the screen: data fetching, subscriptions, timers, manually changing the DOM, logging, syncing with external systems.

```jsx
useEffect(() => {
  // effect
  return () => {
    // cleanup (optional)
  };
}, [dependencies]);
```

### Dependency array behaviour

| Dependencies | Runs |
|---|---|
| none: `useEffect(fn)` | after **every** render |
| `[]` | once after mount (cleanup on unmount) |
| `[a, b]` | after mount + whenever `a` or `b` changed (`Object.is`) |

### Cleanup runs

- Before the effect runs again (with old values), and
- when the component unmounts.

### Example 1 — document title

```jsx
function Counter() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `Clicked ${count} times`;
  }, [count]);
  return <button onClick={() => setCount(count + 1)}>Click</button>;
}
```

### Example 2 — subscriptions & timers with cleanup

```jsx
function WindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);
  useEffect(() => {
    const onResize = () => setWidth(window.innerWidth);
    window.addEventListener("resize", onResize);
    return () => window.removeEventListener("resize", onResize); // prevent leak
  }, []);
  return <p>{width}px</p>;
}

function Clock() {
  const [time, setTime] = useState(new Date());
  useEffect(() => {
    const id = setInterval(() => setTime(new Date()), 1000);
    return () => clearInterval(id);
  }, []);
  return <p>{time.toLocaleTimeString()}</p>;
}
```

### Example 3 — data fetching with race-condition handling

```jsx
function User({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const controller = new AbortController();
    setLoading(true);
    setError(null);

    fetch(`/api/users/${userId}`, { signal: controller.signal })
      .then((res) => {
        if (!res.ok) throw new Error(`HTTP ${res.status}`);
        return res.json();
      })
      .then(setUser)
      .catch((err) => { if (err.name !== "AbortError") setError(err); })
      .finally(() => { if (!controller.signal.aborted) setLoading(false); });

    return () => controller.abort(); // cancel stale request when userId changes / unmount
  }, [userId]);

  if (loading) return <p>Loading…</p>;
  if (error) return <p>{error.message}</p>;
  return <h1>{user.name}</h1>;
}
```

Why cleanup matters: if `userId` changes from 1 → 2 quickly and response 1 arrives after 2, without cancellation the UI shows user 1 (race condition).

`useEffect` callback can't be `async` directly (it must return a cleanup function or nothing):

```jsx
useEffect(() => {
  let ignore = false;
  (async () => {
    const data = await fetchData();
    if (!ignore) setData(data);
  })();
  return () => { ignore = true; };
}, []);
```

### Stale closures in effects

```jsx
// ❌ count is always 0 inside the interval (captured from first render)
useEffect(() => {
  const id = setInterval(() => setCount(count + 1), 1000);
  return () => clearInterval(id);
}, []);

// ✅ updater function
useEffect(() => {
  const id = setInterval(() => setCount((c) => c + 1), 1000);
  return () => clearInterval(id);
}, []);
```

### Objects/functions in deps cause infinite loops

```jsx
// ❌ options is a new object every render -> effect runs every render
const options = { roomId };
useEffect(() => { connect(options); }, [options]);

// ✅ depend on primitives, or create the object inside the effect
useEffect(() => { connect({ roomId }); }, [roomId]);
```

```jsx
// ❌ infinite loop: effect sets state that's in its own deps without a guard
useEffect(() => { setCount(count + 1); }, [count]);
```

### You might not need an effect

- **Derived data** → compute during render (or `useMemo`), not effect + state.
- **Responding to a user event** → do it in the event handler.
- **Resetting state on prop change** → use a `key`.
- **Fetching** → prefer a data library (TanStack Query) or framework loaders.

```jsx
// ❌
const [fullName, setFullName] = useState("");
useEffect(() => setFullName(first + " " + last), [first, last]);
// ✅
const fullName = first + " " + last;

// ❌ POST in an effect triggered by a flag
useEffect(() => { if (submitted) post(form); }, [submitted]);
// ✅
const handleSubmit = () => post(form);
```

### useEffect vs lifecycle methods

| Class | Hook |
|---|---|
| `componentDidMount` | `useEffect(fn, [])` |
| `componentDidUpdate` | `useEffect(fn, [deps])` |
| `componentWillUnmount` | cleanup returned from `useEffect(fn, [])` |

**Interview Qs**
- When does useEffect run? → After the browser paints (async after commit).
- Why does my effect run twice in dev? → StrictMode mounts → unmounts → mounts to reveal missing cleanup.
- How to avoid infinite loops? → Correct dependencies, functional updates, avoid new object/function deps.
- useEffect vs useLayoutEffect? → Layout effect runs synchronously before paint.

---

## 13. useRef

`useRef` returns a mutable object `{ current: initialValue }` that **persists across renders**. Changing `.current` does **not** trigger a re-render.

Two main uses:
1. Access **DOM elements**.
2. Store **mutable values** that shouldn't cause re-renders (timer IDs, previous values, flags, latest callback).

### Example 1 — DOM access / focus

```jsx
function SearchBox() {
  const inputRef = useRef(null);
  useEffect(() => { inputRef.current.focus(); }, []);
  return (
    <>
      <input ref={inputRef} />
      <button onClick={() => inputRef.current.select()}>Select text</button>
    </>
  );
}
```

### Example 2 — stopwatch (storing interval ID)

```jsx
function Stopwatch() {
  const [time, setTime] = useState(0);
  const intervalRef = useRef(null);

  const start = () => {
    if (intervalRef.current) return;
    intervalRef.current = setInterval(() => setTime((t) => t + 10), 10);
  };
  const stop = () => {
    clearInterval(intervalRef.current);
    intervalRef.current = null;
  };
  useEffect(() => stop, []); // clear on unmount

  return (
    <>
      <p>{(time / 1000).toFixed(2)}s</p>
      <button onClick={start}>Start</button>
      <button onClick={stop}>Stop</button>
      <button onClick={() => { stop(); setTime(0); }}>Reset</button>
    </>
  );
}
```

### Example 3 — previous value & render count

```jsx
function usePrevious(value) {
  const ref = useRef();
  useEffect(() => { ref.current = value; }, [value]);
  return ref.current; // value from the previous render
}

function RenderCounter() {
  const renders = useRef(0);
  renders.current++;          // ok-ish for debugging; don't read refs to decide render output
  return <p>Rendered {renders.current} times</p>;
}
```

### Scroll into view, measure elements

```jsx
const bottomRef = useRef(null);
useEffect(() => { bottomRef.current?.scrollIntoView({ behavior: "smooth" }); }, [messages]);

const boxRef = useRef(null);
useLayoutEffect(() => { console.log(boxRef.current.getBoundingClientRect().height); }, []);
```

### Callback refs

A function ref runs when the node attaches/detaches — useful for lists or measuring.

```jsx
const itemsRef = useRef(new Map());
{items.map((item) => (
  <li key={item.id} ref={(node) => {
    if (node) itemsRef.current.set(item.id, node);
    else itemsRef.current.delete(item.id);
  }}>{item.name}</li>
))}
```

### useRef vs useState vs variable

| | Persists across renders | Triggers re-render |
|---|---|---|
| `useState` | ✅ | ✅ |
| `useRef` | ✅ | ❌ |
| local `let` variable | ❌ (reset each render) | ❌ |

**Rule**: don't read or write `ref.current` during rendering (except lazy init); use it in effects and handlers.

**Interview Qs**
- useRef vs useState? (table)
- useRef vs createRef? → createRef creates a new ref every render (class components); useRef keeps the same one.
- How to access a child's DOM node? → Pass a ref (`forwardRef` or `ref` as a prop in React 19).

---

## 14. useContext & Context API

**Context** passes data through the component tree **without prop drilling**. Good for "global" data: theme, auth user, locale, feature flags.

### Steps

1. `createContext(defaultValue)`
2. Wrap tree with `<Context.Provider value={...}>` (React 19: `<Context value={...}>` works too)
3. Read with `useContext(Context)` (or `use(Context)` in React 19)

### Example 1 — Theme

```jsx
const ThemeContext = createContext("light");

function App() {
  const [theme, setTheme] = useState("light");
  return (
    <ThemeContext.Provider value={theme}>
      <Toolbar />
      <button onClick={() => setTheme((t) => (t === "light" ? "dark" : "light"))}>Toggle</button>
    </ThemeContext.Provider>
  );
}

function Toolbar() { return <ThemedButton />; } // no theme prop passed

function ThemedButton() {
  const theme = useContext(ThemeContext);
  return <button className={`btn-${theme}`}>I am {theme}</button>;
}
```

### Example 2 — Auth context with custom hook (best practice)

```jsx
const AuthContext = createContext(null);

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  const login = useCallback(async (email, password) => {
    const u = await api.login(email, password);
    setUser(u);
  }, []);
  const logout = useCallback(() => setUser(null), []);

  const value = useMemo(() => ({ user, login, logout }), [user, login, logout]); // stable value
  return <AuthContext.Provider value={value}>{children}</AuthContext.Provider>;
}

export function useAuth() {
  const ctx = useContext(AuthContext);
  if (!ctx) throw new Error("useAuth must be used inside <AuthProvider>");
  return ctx;
}

// usage
function Navbar() {
  const { user, logout } = useAuth();
  return user ? <button onClick={logout}>Logout {user.name}</button> : <LoginLink />;
}
```

### Example 3 — Context + useReducer (mini Redux)

```jsx
const CartStateContext = createContext();
const CartDispatchContext = createContext();

function cartReducer(state, action) {
  switch (action.type) {
    case "add": return [...state, action.item];
    case "remove": return state.filter((i) => i.id !== action.id);
    default: throw new Error("Unknown action " + action.type);
  }
}

function CartProvider({ children }) {
  const [cart, dispatch] = useReducer(cartReducer, []);
  return (
    <CartStateContext.Provider value={cart}>
      <CartDispatchContext.Provider value={dispatch}>{children}</CartDispatchContext.Provider>
    </CartStateContext.Provider>
  );
}
// Components that only dispatch don't re-render when cart changes (split contexts)
```

### Performance gotcha

Every consumer re-renders when the Provider's `value` changes (by reference). An inline object `value={{ user, setUser }}` is new on every Provider render → all consumers re-render.

Fixes:
- `useMemo` the value.
- **Split contexts** (state vs dispatch, or by domain).
- For high-frequency updates, use a store with selectors (Zustand, Redux, `useSyncExternalStore`).

### Default value

Used only when there is **no Provider above** the consumer.

**Interview Qs**
- What problem does Context solve? → Prop drilling.
- Is Context a state management tool? → No, it's a dependency-injection/transport mechanism; state still lives in useState/useReducer.
- Context vs Redux? → Context: simple, low-frequency global values. Redux: large apps, frequent updates, devtools, middleware, selectors.
- Downsides? → All consumers re-render on value change; harder to reuse components.

---

## 15. useReducer

Alternative to `useState` for **complex state logic** — multiple sub-values, next state depends on previous, many related transitions.

```jsx
const [state, dispatch] = useReducer(reducer, initialState, init?);
```

A reducer is a **pure function** `(state, action) => newState`.

### Example 1 — counter

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "increment": return { count: state.count + 1 };
    case "decrement": return { count: state.count - 1 };
    case "set": return { count: action.payload };
    case "reset": return { count: 0 };
    default: return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });
  return (
    <>
      <p>{state.count}</p>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
      <button onClick={() => dispatch({ type: "set", payload: 100 })}>100</button>
    </>
  );
}
```

### Example 2 — fetch state machine

```jsx
const initial = { status: "idle", data: null, error: null };
function fetchReducer(state, action) {
  switch (action.type) {
    case "FETCH_START": return { ...state, status: "loading", error: null };
    case "FETCH_SUCCESS": return { status: "success", data: action.payload, error: null };
    case "FETCH_ERROR": return { ...state, status: "error", error: action.error };
    default: return state;
  }
}

function Posts() {
  const [{ status, data, error }, dispatch] = useReducer(fetchReducer, initial);
  useEffect(() => {
    dispatch({ type: "FETCH_START" });
    fetch("/api/posts")
      .then((r) => r.json())
      .then((d) => dispatch({ type: "FETCH_SUCCESS", payload: d }))
      .catch((e) => dispatch({ type: "FETCH_ERROR", error: e.message }));
  }, []);
  // ...
}
```

### Example 3 — todo app

```jsx
function todosReducer(todos, action) {
  switch (action.type) {
    case "added": return [...todos, { id: crypto.randomUUID(), text: action.text, done: false }];
    case "toggled": return todos.map((t) => (t.id === action.id ? { ...t, done: !t.done } : t));
    case "deleted": return todos.filter((t) => t.id !== action.id);
    case "edited": return todos.map((t) => (t.id === action.id ? { ...t, text: action.text } : t));
    default: throw new Error(`Unknown action: ${action.type}`);
  }
}
```

### useState vs useReducer

| useState | useReducer |
|---|---|
| Simple independent values | Complex, related state |
| Logic in event handlers | Logic centralised in reducer (easy to test) |
| Less code | More structure, predictable transitions |
| | `dispatch` is stable (good for passing down) |

**Interview Qs**
- When to use useReducer? (above)
- Is dispatch identity stable? → Yes, it never changes between renders.

---

## 16. useMemo

`useMemo` **caches the result of a calculation** between renders. It recomputes only when a dependency changes.

```jsx
const value = useMemo(() => expensiveCalc(a, b), [a, b]);
```

Use it for:
1. **Expensive computations** (filtering/sorting large lists, heavy math).
2. **Referential stability** — keeping the same object/array reference so memoized children or effect deps don't change.

### Example 1 — expensive filter

```jsx
function ProductList({ products, query, sortBy }) {
  const visible = useMemo(() => {
    console.log("filtering…");
    return products
      .filter((p) => p.name.toLowerCase().includes(query.toLowerCase()))
      .sort((a, b) => a[sortBy] - b[sortBy]);
  }, [products, query, sortBy]);

  const [dark, setDark] = useState(false); // toggling dark doesn't re-run the filter
  return (
    <div className={dark ? "dark" : ""}>
      <button onClick={() => setDark((d) => !d)}>Theme</button>
      {visible.map((p) => <ProductRow key={p.id} product={p} />)}
    </div>
  );
}
```

### Example 2 — stable object for memoized child / effect deps

```jsx
function Chart({ data, color }) {
  const options = useMemo(() => ({ color, animate: true }), [color]);
  return <MemoizedChart data={data} options={options} />; // options ref stable unless color changes
}
```

### Example 3 — derived stats

```jsx
const stats = useMemo(() => {
  const total = orders.reduce((s, o) => s + o.amount, 0);
  return { total, avg: orders.length ? total / orders.length : 0, max: Math.max(0, ...orders.map((o) => o.amount)) };
}, [orders]);
```

### When NOT to use

- Cheap calculations (the memo bookkeeping costs more).
- Everything "just in case" — it adds complexity.
- It's a **performance hint**, not a semantic guarantee (React may discard cache).
- The **React Compiler** (React 19 ecosystem) auto-memoizes, making most manual `useMemo/useCallback/memo` unnecessary in projects that enable it.

**Interview Qs**
- useMemo vs useCallback? → useMemo caches a **value**; useCallback caches a **function**. `useCallback(fn, deps) === useMemo(() => fn, deps)`.
- Does useMemo run during render? → Yes, synchronously during render (so no side effects inside).

---

## 17. useCallback

`useCallback` returns a **memoized function reference** that only changes when dependencies change.

```jsx
const handleClick = useCallback(() => doSomething(a), [a]);
```

Functions are recreated on every render (`() => {} !== () => {}`). This matters when:
1. The function is passed to a `React.memo` child.
2. The function is a dependency of `useEffect`/`useMemo`/another hook.

### Example 1 — with React.memo child

```jsx
const TodoItem = memo(function TodoItem({ todo, onToggle }) {
  console.log("render", todo.id);
  return <li onClick={() => onToggle(todo.id)}>{todo.text}</li>;
});

function TodoList() {
  const [todos, setTodos] = useState(initialTodos);
  const [text, setText] = useState("");

  const handleToggle = useCallback((id) => {
    setTodos((prev) => prev.map((t) => (t.id === id ? { ...t, done: !t.done } : t)));
  }, []); // no deps needed thanks to functional update

  return (
    <>
      <input value={text} onChange={(e) => setText(e.target.value)} /> {/* typing doesn't re-render items */}
      <ul>{todos.map((t) => <TodoItem key={t.id} todo={t} onToggle={handleToggle} />)}</ul>
    </>
  );
}
```

Without `useCallback`, `handleToggle` would be new each render → `memo` would be useless → every item re-renders on every keystroke.

### Example 2 — function as effect dependency

```jsx
function SearchResults({ query }) {
  const [results, setResults] = useState([]);

  const fetchResults = useCallback(async () => {
    const res = await fetch(`/api/search?q=${query}`);
    setResults(await res.json());
  }, [query]);

  useEffect(() => { fetchResults(); }, [fetchResults]); // runs only when query changes
}
```

### Example 3 — custom hook returning stable functions

```jsx
function useToggle(initial = false) {
  const [on, setOn] = useState(initial);
  const toggle = useCallback(() => setOn((v) => !v), []);
  const setTrue = useCallback(() => setOn(true), []);
  const setFalse = useCallback(() => setOn(false), []);
  return [on, { toggle, setTrue, setFalse }];
}
```

**Interview Qs**
- Does useCallback prevent the function from being created? → No, it's still created every render; React just returns the cached one if deps didn't change.
- When is useCallback useless? → When the consumer isn't memoized and not used in deps.

---

## 18. React.memo

`React.memo` is a **higher-order component** that skips re-rendering a component if its props are **shallowly equal** to the previous props.

```jsx
const MemoComp = React.memo(Component, arePropsEqual?);
```

### Example 1

```jsx
const Greeting = memo(function Greeting({ name }) {
  console.log("Greeting rendered");
  return <h3>Hello {name}</h3>;
});

function App() {
  const [name, setName] = useState("");
  const [address, setAddress] = useState("");
  return (
    <>
      <input value={name} onChange={(e) => setName(e.target.value)} />
      <input value={address} onChange={(e) => setAddress(e.target.value)} />
      <Greeting name={name} /> {/* doesn't re-render when address changes */}
    </>
  );
}
```

### Example 2 — memo broken by new references

```jsx
<Greeting name={name} style={{ color: "red" }} />    // new object each render -> memo useless
<Greeting name={name} onClick={() => {}} />          // new function each render
<Greeting name={name}><span>child</span></Greeting>  // children JSX is a new object each render
// fix: useMemo / useCallback / hoist constants outside the component
const style = { color: "red" };
```

### Example 3 — custom comparison

```jsx
const Row = memo(
  function Row({ item, onSelect }) { /* ... */ },
  (prev, next) => prev.item.id === next.item.id && prev.item.updatedAt === next.item.updatedAt
);
// return true = props equal = SKIP render
```

### Notes

- Memo doesn't stop re-renders caused by the component's **own state** or **context** it uses.
- Class equivalent: `PureComponent` / `shouldComponentUpdate`.

**Interview Qs**
- React.memo vs useMemo? → memo is for components (skip re-render); useMemo is for values inside a component.
- Why not wrap everything in memo? → Comparison cost, complexity, often broken by unstable props anyway.

---

## 19. useLayoutEffect & useInsertionEffect

### useLayoutEffect

Same signature as `useEffect`, but runs **synchronously after DOM mutations and before the browser paints**. Use when you need to **measure layout** and then update synchronously to avoid a visual flicker.

| useEffect | useLayoutEffect |
|---|---|
| Runs after paint (async) | Runs before paint (sync, blocks paint) |
| Most side effects | DOM measurements, tooltip/popover positioning, scroll restoration |
| Doesn't block UI | Can hurt performance if heavy |

### Example 1 — tooltip position

```jsx
function Tooltip({ targetRect, children }) {
  const ref = useRef(null);
  const [height, setHeight] = useState(0);

  useLayoutEffect(() => {
    setHeight(ref.current.getBoundingClientRect().height); // measured before paint
  }, []);

  const top = targetRect.top - height < 0 ? targetRect.bottom : targetRect.top - height;
  return <div ref={ref} style={{ position: "absolute", top }}>{children}</div>;
}
```

With `useEffect` the tooltip would first paint at the wrong position and then jump (flicker).

### Example 2 — order of execution

```jsx
function Order() {
  useEffect(() => console.log("useEffect"));
  useLayoutEffect(() => console.log("useLayoutEffect"));
  console.log("render");
  return null;
}
// render -> useLayoutEffect -> (paint) -> useEffect
```

### useInsertionEffect

Runs before any layout effects; meant only for **CSS-in-JS libraries** to inject `<style>` tags before layout is read. You'll rarely use it.

---

## 20. useImperativeHandle & forwardRef

### forwardRef (React ≤ 18)

Function components don't accept `ref` as a normal prop in older React. `forwardRef` lets a parent get a ref to a child's DOM node.

```jsx
const FancyInput = forwardRef(function FancyInput(props, ref) {
  return <input ref={ref} className="fancy" {...props} />;
});

function Parent() {
  const inputRef = useRef(null);
  return (
    <>
      <FancyInput ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>Focus</button>
    </>
  );
}
```

### React 19: `ref` is a normal prop

```jsx
function FancyInput({ ref, ...props }) {
  return <input ref={ref} {...props} />;
}
```

### useImperativeHandle

Customize what the parent gets through the ref — expose **only specific methods** instead of the whole DOM node.

```jsx
const VideoPlayer = forwardRef(function VideoPlayer({ src }, ref) {
  const videoRef = useRef(null);
  useImperativeHandle(ref, () => ({
    play: () => videoRef.current.play(),
    pause: () => videoRef.current.pause(),
    seek: (t) => { videoRef.current.currentTime = t; },
  }), []);
  return <video ref={videoRef} src={src} />;
});

function App() {
  const player = useRef(null);
  return (
    <>
      <VideoPlayer ref={player} src="/movie.mp4" />
      <button onClick={() => player.current.play()}>Play</button>
      <button onClick={() => player.current.seek(0)}>Restart</button>
    </>
  );
}
```

```jsx
// Modal with open/close methods
const Modal = forwardRef((props, ref) => {
  const [open, setOpen] = useState(false);
  useImperativeHandle(ref, () => ({ open: () => setOpen(true), close: () => setOpen(false) }));
  return open ? <div className="modal">{props.children}</div> : null;
});
```

Use sparingly — prefer props for things that can be expressed declaratively.

---

## 21. More Hooks

### useId

Generates **unique, stable IDs** that match between server and client (SSR-safe). For accessibility attributes, not list keys.

```jsx
function Field({ label }) {
  const id = useId();
  return (
    <>
      <label htmlFor={id}>{label}</label>
      <input id={id} aria-describedby={`${id}-hint`} />
      <p id={`${id}-hint`}>Must be 8+ chars</p>
    </>
  );
}
```

### useTransition

Marks a state update as **non-urgent** (a transition). React keeps the UI responsive for urgent updates (typing, clicking) and can interrupt the transition render.

```jsx
function TabContainer() {
  const [tab, setTab] = useState("about");
  const [isPending, startTransition] = useTransition();

  const selectTab = (next) => {
    startTransition(() => setTab(next)); // slow tab render won't block clicks
  };
  return (
    <>
      <button onClick={() => selectTab("about")}>About</button>
      <button onClick={() => selectTab("posts")}>Posts (slow)</button>
      {isPending && <Spinner />}
      {tab === "about" ? <About /> : <SlowPosts />}
    </>
  );
}
```

```jsx
// Filtering a big list
function Search({ items }) {
  const [query, setQuery] = useState("");
  const [filtered, setFiltered] = useState(items);
  const [isPending, startTransition] = useTransition();

  const onChange = (e) => {
    setQuery(e.target.value);                       // urgent: input stays snappy
    startTransition(() => {
      setFiltered(items.filter((i) => i.includes(e.target.value))); // non-urgent
    });
  };
  return (
    <>
      <input value={query} onChange={onChange} />
      <div style={{ opacity: isPending ? 0.5 : 1 }}>{filtered.map((i) => <p key={i}>{i}</p>)}</div>
    </>
  );
}
```

React 19: `startTransition` accepts **async functions** (Actions).

### useDeferredValue

Returns a **deferred (lagging) copy of a value**. Use when you don't control the setState (value comes from props).

```jsx
function SearchPage() {
  const [query, setQuery] = useState("");
  const deferredQuery = useDeferredValue(query);
  const isStale = query !== deferredQuery;
  return (
    <>
      <input value={query} onChange={(e) => setQuery(e.target.value)} />
      <div style={{ opacity: isStale ? 0.5 : 1 }}>
        <SlowList query={deferredQuery} /> {/* must be memo'd to benefit */}
      </div>
    </>
  );
}
const SlowList = memo(function SlowList({ query }) { /* heavy render */ });
```

**useTransition vs useDeferredValue**: transition wraps the **setter**; deferred value wraps the **value**. Unlike debounce, there's no fixed delay — it adapts to device speed and can be interrupted.

### useSyncExternalStore

Subscribe to an **external store** (browser APIs, a custom store, Redux internally) safely under concurrent rendering (no "tearing").

```jsx
function subscribe(callback) {
  window.addEventListener("online", callback);
  window.addEventListener("offline", callback);
  return () => {
    window.removeEventListener("online", callback);
    window.removeEventListener("offline", callback);
  };
}
function useOnlineStatus() {
  return useSyncExternalStore(subscribe, () => navigator.onLine, () => true /* server snapshot */);
}
```

```jsx
// Tiny global store
function createStore(initial) {
  let state = initial;
  const listeners = new Set();
  return {
    get: () => state,
    set: (fn) => { state = fn(state); listeners.forEach((l) => l()); },
    subscribe: (l) => { listeners.add(l); return () => listeners.delete(l); },
  };
}
const counterStore = createStore({ count: 0 });
function useStore(store, selector = (s) => s) {
  return useSyncExternalStore(store.subscribe, () => selector(store.get()));
}
function Count() {
  const count = useStore(counterStore, (s) => s.count);
  return <button onClick={() => counterStore.set((s) => ({ count: s.count + 1 }))}>{count}</button>;
}
```

### useDebugValue

Shows a label for custom hooks in React DevTools.

```jsx
function useOnline() {
  const online = useOnlineStatus();
  useDebugValue(online ? "Online" : "Offline");
  return online;
}
```

---

## 22. React 19 Features

### Actions

Functions that use async transitions. React manages pending state, errors, optimistic updates and form resets for you.

### `<form action={fn}>`

```jsx
function AddTodo() {
  async function addTodo(formData) {
    await api.createTodo(formData.get("title"));
  }
  return (
    <form action={addTodo}>   {/* form auto-resets after success */}
      <input name="title" />
      <SubmitButton />
    </form>
  );
}
```

### useFormStatus

Reads the pending status of the **parent** `<form>` (from `react-dom`).

```jsx
import { useFormStatus } from "react-dom";
function SubmitButton() {
  const { pending } = useFormStatus();
  return <button disabled={pending}>{pending ? "Saving…" : "Save"}</button>;
}
```

### useActionState

Manages the state returned by an action + pending flag.

```jsx
import { useActionState } from "react";

async function updateName(prevState, formData) {
  const name = formData.get("name");
  if (!name) return { error: "Name required" };
  await api.updateName(name);
  return { success: true, name };
}

function NameForm() {
  const [state, formAction, isPending] = useActionState(updateName, { error: null });
  return (
    <form action={formAction}>
      <input name="name" />
      <button disabled={isPending}>Update</button>
      {state.error && <p className="error">{state.error}</p>}
      {state.success && <p>Saved {state.name}</p>}
    </form>
  );
}
```

### useOptimistic

Shows an optimistic UI immediately while the async action runs; reverts automatically if it fails.

```jsx
function Messages({ messages, sendMessage }) {
  const [optimistic, addOptimistic] = useOptimistic(
    messages,
    (state, newText) => [...state, { text: newText, sending: true }]
  );
  async function formAction(formData) {
    const text = formData.get("text");
    addOptimistic(text);
    await sendMessage(text);
  }
  return (
    <>
      {optimistic.map((m, i) => <p key={i}>{m.text} {m.sending && <small>(sending…)</small>}</p>)}
      <form action={formAction}><input name="text" /></form>
    </>
  );
}
```

### `use` API

Reads a **promise** (suspends until resolved) or a **context**. Unlike hooks, it **can be called conditionally**.

```jsx
import { use, Suspense } from "react";

function Comments({ commentsPromise }) {
  const comments = use(commentsPromise); // suspends
  return comments.map((c) => <p key={c.id}>{c.text}</p>);
}

function Page() {
  const commentsPromise = fetchComments(); // ideally created in a server component / cached
  return (
    <Suspense fallback={<p>Loading…</p>}>
      <Comments commentsPromise={commentsPromise} />
    </Suspense>
  );
}

function Heading({ show }) {
  if (!show) return null;
  const theme = use(ThemeContext); // conditional is allowed with `use`
  return <h1 className={theme}>Hi</h1>;
}
```

### Other React 19 changes

- `ref` as a regular prop (no `forwardRef` needed); ref callbacks can return a cleanup function.
- `<Context value={...}>` instead of `<Context.Provider>`.
- Document metadata: `<title>`, `<meta>`, `<link>` rendered anywhere are hoisted to `<head>`.
- Stylesheet precedence & async script support; `preload`, `preinit` resource APIs.
- Better hydration error messages.
- **Server Components** and **Server Actions** (`"use server"`) stable.
- **React Compiler** (separate tool): auto-memoization at build time.

---

## 23. Rules of Hooks

1. **Only call hooks at the top level** — not inside loops, conditions, nested functions, or after early returns.
2. **Only call hooks from React functions** — function components or custom hooks (not regular JS functions, not class components).

### Why?

React tracks hooks **by call order** in a linked list on each fiber. If the order changes between renders, state gets mismatched.

```jsx
// ❌
function Bad({ loggedIn }) {
  if (loggedIn) {
    const [name, setName] = useState(""); // order changes when loggedIn changes
  }
  const [age, setAge] = useState(0);
}

// ❌ early return before hook
function Bad2({ data }) {
  if (!data) return null;
  const [x, setX] = useState(0);
}

// ✅
function Good({ loggedIn }) {
  const [name, setName] = useState("");
  const [age, setAge] = useState(0);
  if (!loggedIn) return null;
  // ...
}
```

Enforced by `eslint-plugin-react-hooks` (`rules-of-hooks` and `exhaustive-deps`).

---

## 24. How Hooks Work Under the Hood (+ Children & cloneElement APIs)

Knowing how hooks are implemented explains **why the Rules of Hooks exist**, why state is a **snapshot**, why **stale closures** happen, and why **dependency arrays** matter. Senior interviews often ask you to "implement useState".

### The core idea

A function component is just a function React calls on every render. It has no instance to store state in — so **React stores the state for you**, on the component's **fiber** (its node in React's internal tree), as a **list of hook slots in call order**.

```
Fiber for <Counter />
  memoizedState → [ hook0: useState(0) ] → [ hook1: useRef(null) ] → [ hook2: useEffect(...) ] → null
                     { state: 3, queue }      { current: <input> }      { deps: [3], cleanup }
```

On every render React walks this list **in order**: the 1st hook call gets slot 0, the 2nd gets slot 1, and so on. Hooks have **no names or keys** — only their **position**.

### Example 1 — a mini useState in ~20 lines

```js
// A tiny "React" for ONE component, to show the mechanics
let hooks = [];        // the component's hook slots (React keeps these on the fiber)
let cursor = 0;        // which slot the next hook call uses
let Component;         // the component function we render

function useState(initialValue) {
  const i = cursor;                          // capture THIS hook's slot index
  if (hooks[i] === undefined) {
    hooks[i] = typeof initialValue === "function" ? initialValue() : initialValue; // lazy init, 1st render only
  }
  const setState = (next) => {
    const value = typeof next === "function" ? next(hooks[i]) : next;   // functional updates
    if (Object.is(value, hooks[i])) return;  // same value → bail out, no re-render
    hooks[i] = value;
    render();                                // real React schedules & batches this
  };
  cursor++;
  return [hooks[i], setState];
}

function render() {
  cursor = 0;                                // reset before every render → hooks line up by order
  const output = Component();
  console.log(output);
  return output;
}

// Usage
function Counter() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState("Rohit");
  return { count, name, inc: () => setCount((c) => c + 1), rename: setName };
}

Component = Counter;
let app = render();   // { count: 0, name: "Rohit" }
app.inc();            // re-renders → { count: 1, name: "Rohit" }
```

**Why hooks can't be conditional** — with this implementation it's obvious:

```js
function Broken({ loggedIn }) {
  if (loggedIn) {
    const [user] = useState("A");   // slot 0 only when loggedIn
  }
  const [theme] = useState("dark"); // slot 0 OR slot 1 depending on loggedIn!
  // When loggedIn flips, `theme` reads the slot that used to hold `user` → corrupted state.
}
```

### Example 2 — adding useEffect, useRef and useMemo

```js
let pendingEffects = [];

function useEffect(callback, deps) {
  const i = cursor++;
  const prev = hooks[i];                               // { deps, cleanup } from last render
  const changed = !prev || !deps || deps.some((d, k) => !Object.is(d, prev.deps[k]));
  if (changed) {
    pendingEffects.push(() => {                        // effects run AFTER render/commit, not during
      prev?.cleanup?.();                               // cleanup of the previous effect first
      const cleanup = callback();
      hooks[i] = { deps, cleanup };
    });
  }
}

function useRef(initial) {
  const i = cursor++;
  if (hooks[i] === undefined) hooks[i] = { current: initial }; // same object forever → no re-render on change
  return hooks[i];
}

function useMemo(factory, deps) {
  const i = cursor++;
  const prev = hooks[i];
  if (prev && deps.every((d, k) => Object.is(d, prev.deps[k]))) return prev.value; // cache hit
  const value = factory();
  hooks[i] = { value, deps };
  return value;
}

const useCallback = (fn, deps) => useMemo(() => fn, deps);   // literally useMemo returning the function

function render() {
  cursor = 0;
  const output = Component();
  // "commit" happens here (DOM updates) … then effects run:
  pendingEffects.forEach((run) => run());
  pendingEffects = [];
  return output;
}
```

This shows:
- **Dependencies are compared with `Object.is`** → a new object/array/function every render = "changed" every render.
- **No deps array** → runs after every render; **`[]`** → `deps.some(...)` is always false after the first run → runs once.
- **Cleanup runs before the next effect** and (in real React) on unmount.
- **`useRef` is just a persistent object** — mutating `.current` doesn't call `render()`.
- **`useCallback(fn, deps)` = `useMemo(() => fn, deps)`**.

### Why state is a snapshot & where stale closures come from

Each render is a **separate function call** with its **own constants**. Event handlers and effects created during a render **close over that render's values**.

```jsx
function Counter() {
  const [count, setCount] = useState(0);   // render #1: count is the constant 0

  const handleClick = () => {
    setCount(count + 1);                   // "schedule count = 0 + 1"
    setTimeout(() => alert(count), 3000);  // closes over THIS render's count (0) forever
  };
  return <button onClick={handleClick}>{count}</button>;
}
```

- `setCount` doesn't change the `count` variable — it **schedules a new render** where `useState` returns the new value.
- A timer/interval/effect created in render #1 keeps seeing render #1's values → **stale closure**.
- Fixes: functional updates (`setCount(c => c + 1)`), correct effect dependencies, or a ref holding the latest value.

```jsx
// "latest value" ref pattern
const latestCount = useRef(count);
useEffect(() => { latestCount.current = count; });
useEffect(() => {
  const id = setInterval(() => console.log(latestCount.current), 1000); // always fresh
  return () => clearInterval(id);
}, []);
```

### How real React does it (what to say in interviews)

1. **Fiber + linked list**: each fiber's `memoizedState` points to a linked list of hook objects `{ memoizedState, queue, next }`.
2. **Dispatchers**: React swaps the implementation behind `useState` etc. depending on the phase — `HooksDispatcherOnMount` (create hooks) vs `HooksDispatcherOnUpdate` (read existing hooks). Outside rendering the dispatcher is a throwing one → **"Invalid hook call"** error when hooks are called in normal functions, class components, or with duplicate React copies.
3. **Update queues**: `setState` doesn't change state immediately; it pushes an **update object** onto the hook's queue and **schedules** a render with a priority (lane). During the next render React processes the queue → that's why multiple `setCount(c => c + 1)` calls all apply, and why updates are **batched**.
4. **Bail-out**: if the new state `Object.is` the old one, React can skip rendering the subtree.
5. **Effects**: during render React only records effects (tagged with flags); after **commit** it runs `useLayoutEffect` synchronously, then `useEffect` asynchronously after paint; cleanups run before re-running and on unmount.
6. **`useContext`** doesn't use a slot in the same way — it reads the nearest Provider value and subscribes the fiber to changes.
7. **Custom hooks** have no special machinery: they're functions that call hooks, so their hook calls just occupy consecutive slots in the calling component's list. That's why two components using the same custom hook get **independent** state.

### Bonus — a mini createElement + render (the "Virtual DOM" idea)

```js
function createElement(type, props, ...children) {
  return { type, props: { ...props, children: children.flat() } };   // what JSX compiles into
}

function renderToDOM(vnode, container) {
  if (typeof vnode === "string" || typeof vnode === "number") {
    container.appendChild(document.createTextNode(vnode));
    return;
  }
  if (typeof vnode.type === "function") {                            // component → call it
    return renderToDOM(vnode.type(vnode.props), container);
  }
  const el = document.createElement(vnode.type);
  for (const [key, value] of Object.entries(vnode.props)) {
    if (key === "children") continue;
    if (key.startsWith("on")) el.addEventListener(key.slice(2).toLowerCase(), value);
    else el.setAttribute(key === "className" ? "class" : key, value);
  }
  vnode.props.children.forEach((child) => renderToDOM(child, el));
  container.appendChild(el);
}

const Greeting = ({ name }) => createElement("h1", { className: "title" }, "Hello ", name);
renderToDOM(createElement(Greeting, { name: "Rohit" }), document.getElementById("root"));
```

Real React adds: diffing old vs new trees (reconciliation), keys, batching, scheduling, fibers, and event delegation.

---

### React.Children, cloneElement & isValidElement

APIs for inspecting/transforming the `children` prop. They're **legacy/uncommon** in modern React — prefer **composition, props or context** — but you'll meet them in component libraries and interviews.

```jsx
import { Children, cloneElement, isValidElement } from "react";

Children.count(children);                  // number of children (fragments count as 1, null/false ignored differently)
Children.toArray(children);                // flat array with keys assigned
Children.map(children, (child, i) => ...); // like Array.map, handles null/arrays/single child
Children.forEach(children, fn);
Children.only(children);                   // asserts exactly one child element, returns it
isValidElement(x);                         // is x a React element (not a string/number/null)?
cloneElement(element, extraProps);         // copy of the element with merged props (and optional new children)
```

### Example — injecting props into children (e.g. a RadioGroup)

```jsx
function RadioGroup({ name, value, onChange, children }) {
  return (
    <div role="radiogroup">
      {Children.map(children, (child) =>
        isValidElement(child)
          ? cloneElement(child, {
              name,
              checked: child.props.value === value,
              onChange: () => onChange(child.props.value),
            })
          : child
      )}
    </div>
  );
}

function Radio({ name, value, checked, onChange, children }) {
  return (
    <label>
      <input type="radio" name={name} value={value} checked={checked} onChange={onChange} />
      {children}
    </label>
  );
}

<RadioGroup name="plan" value={plan} onChange={setPlan}>
  <Radio value="free">Free</Radio>
  <Radio value="pro">Pro</Radio>
</RadioGroup>
```

### Example — adding separators between children

```jsx
function Breadcrumbs({ children }) {
  const items = Children.toArray(children);
  return (
    <nav aria-label="breadcrumb">
      {items.map((item, i) => (
        <span key={item.key}>
          {item}
          {i < items.length - 1 && " / "}
        </span>
      ))}
    </nav>
  );
}
```

### Why these are discouraged (and the alternatives)

- **Fragile**: wrapping a child in another component or a Fragment (`<><Radio/></>`) breaks the injection — `cloneElement` only sees the top-level element.
- **Implicit data flow**: props appear "from nowhere", hard to type and to trace.
- **Better alternatives**:
  - **Context** for compound components (`<Tabs>` + `<Tabs.Tab>` reading shared state from context — see Advanced Patterns).
  - **Render props** / passing data explicitly.
  - Accept an **array of data** (`items={[...]}`) and render it yourself.

```jsx
// Context-based version of RadioGroup — works no matter how deeply Radio is nested
const RadioCtx = createContext(null);
function RadioGroup2({ name, value, onChange, children }) {
  return <RadioCtx.Provider value={{ name, value, onChange }}><div role="radiogroup">{children}</div></RadioCtx.Provider>;
}
function Radio2({ value: optionValue, children }) {
  const { name, value, onChange } = useContext(RadioCtx);
  return (
    <label>
      <input type="radio" name={name} checked={value === optionValue} onChange={() => onChange(optionValue)} />
      {children}
    </label>
  );
}
```

### Interview Qs

1. **How does React know which state belongs to which `useState` call?** → Call order: hooks are stored as an ordered list on the component's fiber.
2. **Why can't hooks be called conditionally or in loops?** → The order would change between renders and slots would mismatch.
3. **Implement a basic `useState` (and `useEffect`).** (Examples above)
4. **Why does `console.log(count)` right after `setCount` show the old value?** → State is a per-render snapshot; setState schedules a new render.
5. **What is a stale closure and how do you fix it?**
6. **How are effect dependencies compared?** → `Object.is`, element by element.
7. **Is `useCallback` different from `useMemo`?** → `useCallback(fn, deps)` ≡ `useMemo(() => fn, deps)`.
8. **Why does "Invalid hook call" happen?** → Hooks called outside a component/custom hook, in a class, or two copies of React in the bundle.
9. **Do two components using the same custom hook share state?** → No — each gets its own slots.
10. **What do `React.Children.map` and `cloneElement` do? Why are they discouraged?**

---

## 25. Custom Hooks

A **custom hook** is a function whose name starts with `use` and that calls other hooks. It lets you **reuse stateful logic** (not state itself — each call gets its own state).

### Example 1 — useFetch

```jsx
function useFetch(url) {
  const [state, setState] = useState({ data: null, loading: true, error: null });

  useEffect(() => {
    const controller = new AbortController();
    setState((s) => ({ ...s, loading: true, error: null }));
    fetch(url, { signal: controller.signal })
      .then((r) => { if (!r.ok) throw new Error(r.statusText); return r.json(); })
      .then((data) => setState({ data, loading: false, error: null }))
      .catch((error) => { if (error.name !== "AbortError") setState({ data: null, loading: false, error }); });
    return () => controller.abort();
  }, [url]);

  return state;
}

function Users() {
  const { data, loading, error } = useFetch("/api/users");
  if (loading) return <Spinner />;
  if (error) return <p>{error.message}</p>;
  return data.map((u) => <p key={u.id}>{u.name}</p>);
}
```

### Example 2 — useDebounce

```jsx
function useDebounce(value, delay = 500) {
  const [debounced, setDebounced] = useState(value);
  useEffect(() => {
    const t = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(t);
  }, [value, delay]);
  return debounced;
}

function Search() {
  const [q, setQ] = useState("");
  const debouncedQ = useDebounce(q, 400);
  const { data } = useFetch(`/api/search?q=${debouncedQ}`);
  return <input value={q} onChange={(e) => setQ(e.target.value)} />;
}
```

### Example 3 — useLocalStorage

```jsx
function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    try {
      const stored = localStorage.getItem(key);
      return stored !== null ? JSON.parse(stored) : initialValue;
    } catch {
      return initialValue;
    }
  });
  useEffect(() => {
    try { localStorage.setItem(key, JSON.stringify(value)); } catch {}
  }, [key, value]);
  return [value, setValue];
}

const [theme, setTheme] = useLocalStorage("theme", "light");
```

### More useful custom hooks

```jsx
// useOnClickOutside
function useOnClickOutside(ref, handler) {
  useEffect(() => {
    const listener = (e) => {
      if (!ref.current || ref.current.contains(e.target)) return;
      handler(e);
    };
    document.addEventListener("mousedown", listener);
    document.addEventListener("touchstart", listener);
    return () => {
      document.removeEventListener("mousedown", listener);
      document.removeEventListener("touchstart", listener);
    };
  }, [ref, handler]);
}

// useWindowSize
function useWindowSize() {
  const [size, setSize] = useState({ w: window.innerWidth, h: window.innerHeight });
  useEffect(() => {
    const onResize = () => setSize({ w: window.innerWidth, h: window.innerHeight });
    window.addEventListener("resize", onResize);
    return () => window.removeEventListener("resize", onResize);
  }, []);
  return size;
}

// useInterval (Dan Abramov's pattern — always calls the latest callback)
function useInterval(callback, delay) {
  const saved = useRef(callback);
  useEffect(() => { saved.current = callback; }, [callback]);
  useEffect(() => {
    if (delay === null) return;
    const id = setInterval(() => saved.current(), delay);
    return () => clearInterval(id);
  }, [delay]);
}

// useIntersectionObserver (infinite scroll / lazy load)
function useInView(options) {
  const ref = useRef(null);
  const [inView, setInView] = useState(false);
  useEffect(() => {
    const el = ref.current;
    if (!el) return;
    const obs = new IntersectionObserver(([entry]) => setInView(entry.isIntersecting), options);
    obs.observe(el);
    return () => obs.disconnect();
  }, [options?.rootMargin, options?.threshold]);
  return [ref, inView];
}

// useMediaQuery
function useMediaQuery(query) {
  return useSyncExternalStore(
    (cb) => { const m = matchMedia(query); m.addEventListener("change", cb); return () => m.removeEventListener("change", cb); },
    () => matchMedia(query).matches,
    () => false
  );
}
```

**Interview Qs**
- Do two components using the same custom hook share state? → No, each call has its own state.
- Why must custom hooks start with `use`? → So the linter can enforce rules of hooks, and to signal that it may call hooks.

---

## 26. Lifting State Up & Prop Drilling

### Lifting state up

When two siblings need the same data, move the state to their **closest common parent** and pass it down via props.

```jsx
function TemperatureApp() {
  const [celsius, setCelsius] = useState(0);
  return (
    <>
      <CelsiusInput value={celsius} onChange={setCelsius} />
      <FahrenheitDisplay celsius={celsius} />
    </>
  );
}
function CelsiusInput({ value, onChange }) {
  return <input type="number" value={value} onChange={(e) => onChange(Number(e.target.value))} />;
}
function FahrenheitDisplay({ celsius }) {
  return <p>{(celsius * 9) / 5 + 32} °F</p>;
}
```

```jsx
// Accordion: only one panel open at a time
function Accordion({ items }) {
  const [openIndex, setOpenIndex] = useState(0);
  return items.map((item, i) => (
    <Panel key={item.id} title={item.title} isOpen={openIndex === i} onShow={() => setOpenIndex(i)}>
      {item.body}
    </Panel>
  ));
}
```

### Prop drilling

Passing props through many intermediate components that don't use them.

```jsx
<App user={user}>
  <Layout user={user}>
    <Sidebar user={user}>
      <Avatar user={user} />   {/* only this one needs it */}
```

Solutions:
1. **Component composition** — pass the rendered element as `children`/props so intermediate layers don't need the data.
2. **Context API**.
3. **State management library** (Redux, Zustand, Jotai).

```jsx
// Composition fix
function App() {
  const user = useUser();
  return <Layout sidebar={<Sidebar avatar={<Avatar user={user} />} />} />;
}
```

---

## 27. Component Lifecycle (Class Components)

Three phases: **Mounting → Updating → Unmounting** (+ Error handling).

### Mounting
1. `constructor(props)` — init state, bind methods.
2. `static getDerivedStateFromProps(props, state)` — rare; sync state from props.
3. `render()` — return JSX (pure).
4. `componentDidMount()` — DOM ready; fetch data, subscriptions.

### Updating (new props, setState, forceUpdate)
1. `static getDerivedStateFromProps`
2. `shouldComponentUpdate(nextProps, nextState)` — return false to skip render.
3. `render()`
4. `getSnapshotBeforeUpdate(prevProps, prevState)` — read DOM before changes (e.g. scroll position).
5. `componentDidUpdate(prevProps, prevState, snapshot)`

### Unmounting
- `componentWillUnmount()` — cleanup.

### Error handling
- `static getDerivedStateFromError(error)`, `componentDidCatch(error, info)`.

```jsx
class UserProfile extends React.Component {
  constructor(props) {
    super(props);
    this.state = { user: null };
    this.handleRefresh = this.handleRefresh.bind(this); // bind `this`
  }
  componentDidMount() { this.load(); }
  componentDidUpdate(prevProps) {
    if (prevProps.userId !== this.props.userId) this.load(); // compare to avoid loops
  }
  componentWillUnmount() { this.controller?.abort(); }
  shouldComponentUpdate(nextProps, nextState) {
    return nextState.user !== this.state.user || nextProps.userId !== this.props.userId;
  }
  async load() {
    this.controller = new AbortController();
    const res = await fetch(`/api/users/${this.props.userId}`, { signal: this.controller.signal });
    this.setState({ user: await res.json() });
  }
  handleRefresh() { this.load(); }
  render() {
    const { user } = this.state;
    return user ? <h1 onClick={this.handleRefresh}>{user.name}</h1> : <p>Loading</p>;
  }
}
```

`setState` in classes **merges** objects shallowly (unlike `useState`, which replaces), and takes an optional callback: `this.setState({ a: 1 }, () => console.log("updated"))`.

Deprecated/unsafe: `componentWillMount`, `componentWillReceiveProps`, `componentWillUpdate` (prefixed `UNSAFE_`).

**Interview Qs**
- Hooks equivalent of each lifecycle? → Section 12 table; `shouldComponentUpdate` → `React.memo`; `getDerivedStateFromError` → no hook yet (use class or `react-error-boundary`).

---

## 28. Fragments & Portals

### Fragments

Group children without adding an extra DOM node.

```jsx
function Columns() {
  return (
    <>
      <td>Name</td>
      <td>Age</td>
    </>
  );
}
// keyed fragments need the long form: <Fragment key={id}>...</Fragment>
```

Why: invalid HTML (`<div>` inside `<tr>`), CSS layouts (flex/grid children), fewer DOM nodes.

### Portals

Render children into a **different DOM node** outside the parent hierarchy — modals, tooltips, toasts, dropdowns (escape `overflow: hidden` / `z-index` stacking).

```jsx
import { createPortal } from "react-dom";

function Modal({ isOpen, onClose, children }) {
  if (!isOpen) return null;
  return createPortal(
    <div className="overlay" onClick={onClose}>
      <div className="modal" role="dialog" aria-modal="true" onClick={(e) => e.stopPropagation()}>
        {children}
        <button onClick={onClose}>Close</button>
      </div>
    </div>,
    document.getElementById("modal-root")
  );
}
```

Events from a portal **bubble through the React tree** (to React ancestors), not the DOM tree. Context also works normally.

```jsx
<div onClick={() => console.log("parent got click from portal")}>
  <Modal isOpen>…</Modal>
</div>
```

---

## 29. Error Boundaries

A class component that catches **JS errors during rendering, in lifecycle methods and constructors of its children**, logs them, and shows a fallback UI instead of crashing the whole app.

```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false, error: null };

  static getDerivedStateFromError(error) {
    return { hasError: true, error }; // render fallback
  }
  componentDidCatch(error, info) {
    logToService(error, info.componentStack); // side effects here
  }
  render() {
    if (this.state.hasError) {
      return this.props.fallback ?? (
        <div>
          <p>Something went wrong.</p>
          <button onClick={() => this.setState({ hasError: false })}>Try again</button>
        </div>
      );
    }
    return this.props.children;
  }
}

<ErrorBoundary fallback={<p>Widget failed</p>}>
  <Widget />
</ErrorBoundary>
```

### Does NOT catch

- Errors in **event handlers** (use try/catch).
- **Async** code (setTimeout, promises) — unless you set state to rethrow during render.
- **SSR** errors.
- Errors in the boundary itself.

```jsx
// Rethrow async error into boundary
const [, setState] = useState();
fetchData().catch((e) => setState(() => { throw e; }));
```

### react-error-boundary library

```jsx
import { ErrorBoundary } from "react-error-boundary";
<ErrorBoundary
  FallbackComponent={({ error, resetErrorBoundary }) => (
    <div><p>{error.message}</p><button onClick={resetErrorBoundary}>Retry</button></div>
  )}
  resetKeys={[userId]}
>
  <Profile userId={userId} />
</ErrorBoundary>
```

Place boundaries at different levels: whole app, route, widget.

---

## 30. Code Splitting: lazy & Suspense

**Code splitting** breaks the bundle into chunks loaded on demand → smaller initial download, faster first load.

### React.lazy + Suspense

```jsx
import { lazy, Suspense } from "react";

const Dashboard = lazy(() => import("./pages/Dashboard"));   // must be a default export
const Settings = lazy(() => import("./pages/Settings"));

function App() {
  return (
    <Suspense fallback={<Spinner />}>
      <Routes>
        <Route path="/dashboard" element={<Dashboard />} />
        <Route path="/settings" element={<Settings />} />
      </Routes>
    </Suspense>
  );
}
```

```jsx
// Named export
const Chart = lazy(() => import("./Chart").then((m) => ({ default: m.Chart })));

// Load on interaction
function Editor() {
  const [show, setShow] = useState(false);
  return (
    <>
      <button onClick={() => setShow(true)}>Open markdown preview</button>
      {show && (
        <Suspense fallback={<p>Loading preview…</p>}>
          <MarkdownPreview />
        </Suspense>
      )}
    </>
  );
}

// Preload on hover
const loadSettings = () => import("./pages/Settings");
<Link to="/settings" onMouseEnter={loadSettings}>Settings</Link>
```

### Suspense

Shows a fallback while children are "suspended" — waiting for lazy code, or data (with Suspense-enabled libraries/`use`/RSC). Nested Suspense boundaries create progressive loading.

```jsx
<Suspense fallback={<PageSkeleton />}>
  <Header />
  <Suspense fallback={<FeedSkeleton />}>
    <Feed />
  </Suspense>
</Suspense>
```

---

## 31. Advanced Patterns

### 1. Higher-Order Component (HOC)

A function that **takes a component and returns a new enhanced component**. Used for cross-cutting concerns (auth, logging, data injection). Mostly replaced by hooks today.

```jsx
function withAuth(Component) {
  return function Authenticated(props) {
    const { user } = useAuth();
    if (!user) return <Navigate to="/login" />;
    return <Component {...props} user={user} />;
  };
}
const ProtectedDashboard = withAuth(Dashboard);
```

```jsx
function withLoading(Component) {
  return function WithLoading({ isLoading, ...props }) {
    return isLoading ? <Spinner /> : <Component {...props} />;
  };
}
const UserListWithLoading = withLoading(UserList);
<UserListWithLoading isLoading={loading} users={users} />;
```

HOC downsides: wrapper hell, prop name collisions, harder to type, obscured data source.

### 2. Render Props

A component takes a **function as a prop** (or as `children`) that returns what to render.

```jsx
function MouseTracker({ render }) {
  const [pos, setPos] = useState({ x: 0, y: 0 });
  return <div onMouseMove={(e) => setPos({ x: e.clientX, y: e.clientY })}>{render(pos)}</div>;
}
<MouseTracker render={({ x, y }) => <p>Mouse at {x}, {y}</p>} />;

// children as a function
function DataLoader({ url, children }) {
  const { data, loading } = useFetch(url);
  return children({ data, loading });
}
<DataLoader url="/api/users">{({ data, loading }) => (loading ? "…" : data.length)}</DataLoader>;
```

### 3. Compound Components

Components that work together sharing implicit state via context (like `<select>` + `<option>`). Flexible API for the consumer.

```jsx
const TabsContext = createContext(null);

function Tabs({ defaultValue, children }) {
  const [active, setActive] = useState(defaultValue);
  return <TabsContext.Provider value={{ active, setActive }}>{children}</TabsContext.Provider>;
}
Tabs.List = function TabList({ children }) {
  return <div role="tablist">{children}</div>;
};
Tabs.Trigger = function Tab({ value, children }) {
  const { active, setActive } = useContext(TabsContext);
  return (
    <button role="tab" aria-selected={active === value} onClick={() => setActive(value)}>
      {children}
    </button>
  );
};
Tabs.Panel = function TabPanel({ value, children }) {
  const { active } = useContext(TabsContext);
  return active === value ? <div role="tabpanel">{children}</div> : null;
};

<Tabs defaultValue="a">
  <Tabs.List>
    <Tabs.Trigger value="a">Account</Tabs.Trigger>
    <Tabs.Trigger value="b">Billing</Tabs.Trigger>
  </Tabs.List>
  <Tabs.Panel value="a">Account settings…</Tabs.Panel>
  <Tabs.Panel value="b">Billing info…</Tabs.Panel>
</Tabs>
```

### 4. Controlled vs Uncontrolled components (component API design)

Let the consumer optionally control state:

```jsx
function Toggle({ on: controlledOn, defaultOn = false, onChange }) {
  const [internalOn, setInternalOn] = useState(defaultOn);
  const isControlled = controlledOn !== undefined;
  const on = isControlled ? controlledOn : internalOn;
  const toggle = () => {
    if (!isControlled) setInternalOn(!on);
    onChange?.(!on);
  };
  return <button aria-pressed={on} onClick={toggle}>{on ? "ON" : "OFF"}</button>;
}
<Toggle />                                  // uncontrolled
<Toggle on={isOn} onChange={setIsOn} />     // controlled
```

### 5. Container/Presentational → Custom hooks

```jsx
function useUsers() { /* fetch + state */ }
function UserTable({ users }) { /* just UI */ }
function UsersPage() { const { users } = useUsers(); return <UserTable users={users} />; }
```

### 6. Provider pattern, 7. Slots (props that take JSX)

```jsx
<PageLayout header={<Header />} sidebar={<Nav />} footer={<Footer />}>
  <Content />
</PageLayout>
```

### 8. State reducer pattern

Let consumers override how internal state changes by passing their own reducer (used by Downshift).

**Interview Qs**
- HOC vs custom hooks? → Hooks share logic without wrapper components or prop collisions; HOCs wrap components.
- What are compound components? (above)

---

## 32. Performance Optimization

### Checklist

1. **Measure first** — React DevTools Profiler ("Highlight updates"), Chrome Performance tab, `why-did-you-render`.
2. **Avoid unnecessary re-renders**:
   - Move state down / keep state local.
   - Lift content up (pass JSX as `children`).
   - `React.memo` + `useCallback` + `useMemo` for stable props.
   - Split contexts; memoize context value; use selector-based stores.
3. **Stable keys** in lists (never random, avoid index for dynamic lists).
4. **Virtualize long lists** — `react-window`, `@tanstack/react-virtual` render only visible rows.
5. **Code splitting** — `lazy`, route-based splitting, dynamic imports.
6. **Debounce/throttle** expensive handlers (search, resize, scroll).
7. **Concurrent features** — `useTransition`, `useDeferredValue` for heavy updates.
8. **Images** — lazy load, proper sizes, modern formats (WebP/AVIF), `next/image`.
9. **Bundle size** — tree shaking, analyze bundle (`vite-bundle-visualizer`), avoid huge libs (moment → date-fns/dayjs), import only what you need.
10. **Avoid inline heavy computation in render** — memoize or move to worker.
11. **Server-side** rendering / RSC to send less JS.
12. **Production build** — dev mode is much slower.
13. **React Compiler** — automatic memoization.

### Example — virtualization

```jsx
import { FixedSizeList as List } from "react-window";

function BigList({ items }) {
  return (
    <List height={600} itemCount={items.length} itemSize={35} width="100%">
      {({ index, style }) => <div style={style}>{items[index].name}</div>}
    </List>
  );
}
```

### Example — Profiler API

```jsx
<Profiler id="Sidebar" onRender={(id, phase, actualDuration) => console.log(id, phase, actualDuration)}>
  <Sidebar />
</Profiler>
```

### Example — expensive context split

```jsx
// ❌ single context with frequently changing value
<AppContext.Provider value={{ user, theme, cart, notifications }}>

// ✅ separate providers — cart updates don't re-render theme consumers
<UserProvider><ThemeProvider><CartProvider>{children}</CartProvider></ThemeProvider></UserProvider>
```

---

## 33. React 18 Concurrent Features

### createRoot

```jsx
// React 17
ReactDOM.render(<App />, root);
// React 18+
createRoot(root).render(<App />);
```

### Automatic batching

Multiple state updates are grouped into **one re-render** — now also inside promises, setTimeout and native event handlers (React 17 only batched inside React event handlers).

```jsx
setTimeout(() => {
  setCount((c) => c + 1);
  setFlag((f) => !f);
  // React 18: ONE render. React 17: TWO renders.
}, 1000);

// Opt out (rare)
import { flushSync } from "react-dom";
flushSync(() => setCount(1)); // DOM updated immediately
flushSync(() => setFlag(true));
```

### Concurrent rendering

React can **prepare multiple versions of the UI at once**, interrupt a render to handle something urgent, and discard stale work. It's opt-in via features: `startTransition`, `useTransition`, `useDeferredValue`, Suspense.

### Other 18 features

- **Transitions** (urgent vs non-urgent updates).
- **Suspense on the server** — streaming SSR with `renderToPipeableStream`, selective hydration.
- New hooks: `useId`, `useTransition`, `useDeferredValue`, `useSyncExternalStore`, `useInsertionEffect`.
- Strict Mode double-invokes effects in dev.

---

## 34. Strict Mode

`<StrictMode>` is a development-only tool that helps find bugs. No effect in production.

```jsx
createRoot(root).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

What it does in dev:
1. **Renders components twice** → catches impure render logic.
2. **Runs effects twice** (mount → unmount → mount) → catches missing cleanup.
3. **Runs ref callbacks twice**.
4. Warns about deprecated APIs (string refs, legacy context, `findDOMNode`, unsafe lifecycles).

```jsx
useEffect(() => {
  const conn = createConnection();
  conn.connect();
  return () => conn.disconnect(); // StrictMode verifies this cleanup exists
}, []);
```

**Interview Q**: Why does my `console.log`/API call happen twice? → StrictMode in development.

---

## 35. React Router

Client-side routing for SPAs: changes URL and view without full page reloads (uses History API).

### Setup (v6/v7 data router)

```jsx
import { createBrowserRouter, RouterProvider, Outlet, Link, NavLink } from "react-router-dom";

const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    errorElement: <ErrorPage />,
    children: [
      { index: true, element: <Home /> },
      { path: "about", element: <About /> },
      { path: "users", element: <Users />, loader: usersLoader },
      { path: "users/:userId", element: <UserDetail />, loader: userLoader },
      { path: "*", element: <NotFound /> },
    ],
  },
]);

function RootLayout() {
  return (
    <>
      <nav>
        <NavLink to="/" end className={({ isActive }) => (isActive ? "active" : "")}>Home</NavLink>
        <Link to="/about">About</Link>
      </nav>
      <Outlet /> {/* child routes render here */}
    </>
  );
}

createRoot(root).render(<RouterProvider router={router} />);
```

### Declarative style

```jsx
<BrowserRouter>
  <Routes>
    <Route path="/" element={<Layout />}>
      <Route index element={<Home />} />
      <Route path="products/:id" element={<Product />} />
      <Route path="dashboard/*" element={<Dashboard />} />
    </Route>
  </Routes>
</BrowserRouter>
```

### Hooks

```jsx
import { useParams, useNavigate, useSearchParams, useLocation, useLoaderData } from "react-router-dom";

function Product() {
  const { id } = useParams();                        // /products/42 -> "42"
  const navigate = useNavigate();
  const [searchParams, setSearchParams] = useSearchParams(); // ?sort=price
  const location = useLocation();                    // { pathname, search, state }
  const sort = searchParams.get("sort") ?? "name";

  return (
    <>
      <button onClick={() => navigate(-1)}>Back</button>
      <button onClick={() => navigate("/cart", { state: { from: location.pathname } })}>Cart</button>
      <button onClick={() => setSearchParams({ sort: "price" })}>Sort by price</button>
    </>
  );
}

async function userLoader({ params }) {
  const res = await fetch(`/api/users/${params.userId}`);
  if (!res.ok) throw new Response("Not Found", { status: 404 });
  return res.json();
}
function UserDetail() {
  const user = useLoaderData();
  return <h1>{user.name}</h1>;
}
```

### Protected routes

```jsx
function ProtectedRoute({ children }) {
  const { user } = useAuth();
  const location = useLocation();
  if (!user) return <Navigate to="/login" replace state={{ from: location }} />;
  return children;
}

<Route path="/dashboard" element={<ProtectedRoute><Dashboard /></ProtectedRoute>} />

// after login
const from = location.state?.from?.pathname || "/";
navigate(from, { replace: true });
```

**Interview Qs**
- `Link` vs `<a>`? → `Link` navigates client-side without reload; `<a>` reloads the page.
- BrowserRouter vs HashRouter? → Clean URLs using History API (needs server fallback to index.html) vs `#/path` (works on static hosts).
- How to pass data between routes? → URL params, search params, `navigate(path, { state })`, global state.

---

## 36. State Management

### Types of state

| Type | Tool |
|---|---|
| Local UI state | `useState`, `useReducer` |
| Shared/global client state | Context, Zustand, Redux Toolkit, Jotai |
| **Server state** (cached API data) | TanStack Query, RTK Query, SWR |
| URL state | Router search params |
| Form state | React Hook Form |

### Redux core concepts

- **Store** — single object tree holding app state.
- **Action** — plain object `{ type, payload }` describing what happened.
- **Reducer** — pure function `(state, action) => newState`.
- **Dispatch** — send an action to the store.
- **Selector** — read part of the state.
- **Middleware** — intercept actions (thunks for async, logging).
- Three principles: single source of truth, state is read-only, changes via pure functions.

Flow: `UI → dispatch(action) → middleware → reducer → new state → subscribed UI re-renders`.

### Redux Toolkit (RTK) — the modern way

```jsx
// store/counterSlice.js
import { createSlice, createAsyncThunk } from "@reduxjs/toolkit";

export const fetchUsers = createAsyncThunk("users/fetch", async () => {
  const res = await fetch("/api/users");
  return res.json();
});

const usersSlice = createSlice({
  name: "users",
  initialState: { list: [], status: "idle", error: null, count: 0 },
  reducers: {
    increment(state) { state.count += 1; },          // Immer lets you "mutate" safely
    addUser(state, action) { state.list.push(action.payload); },
    removeUser(state, action) { state.list = state.list.filter((u) => u.id !== action.payload); },
  },
  extraReducers: (builder) => {
    builder
      .addCase(fetchUsers.pending, (state) => { state.status = "loading"; })
      .addCase(fetchUsers.fulfilled, (state, action) => { state.status = "succeeded"; state.list = action.payload; })
      .addCase(fetchUsers.rejected, (state, action) => { state.status = "failed"; state.error = action.error.message; });
  },
});
export const { increment, addUser, removeUser } = usersSlice.actions;
export default usersSlice.reducer;

// store/index.js
import { configureStore } from "@reduxjs/toolkit";
export const store = configureStore({ reducer: { users: usersReducer } });

// main.jsx
<Provider store={store}><App /></Provider>

// component
import { useSelector, useDispatch } from "react-redux";
function Users() {
  const { list, status } = useSelector((s) => s.users);
  const dispatch = useDispatch();
  useEffect(() => { if (status === "idle") dispatch(fetchUsers()); }, [status, dispatch]);
  return list.map((u) => <p key={u.id} onClick={() => dispatch(removeUser(u.id))}>{u.name}</p>);
}
```

### RTK Query

```jsx
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query/react";
export const api = createApi({
  baseQuery: fetchBaseQuery({ baseUrl: "/api" }),
  tagTypes: ["Post"],
  endpoints: (b) => ({
    getPosts: b.query({ query: () => "posts", providesTags: ["Post"] }),
    addPost: b.mutation({ query: (body) => ({ url: "posts", method: "POST", body }), invalidatesTags: ["Post"] }),
  }),
});
export const { useGetPostsQuery, useAddPostMutation } = api;
```

### Zustand — minimal global store

```jsx
import { create } from "zustand";
import { persist } from "zustand/middleware";

const useCartStore = create(
  persist(
    (set, get) => ({
      items: [],
      add: (item) => set((s) => ({ items: [...s.items, item] })),
      remove: (id) => set((s) => ({ items: s.items.filter((i) => i.id !== id) })),
      total: () => get().items.reduce((sum, i) => sum + i.price, 0),
    }),
    { name: "cart" }
  )
);

function CartCount() {
  const count = useCartStore((s) => s.items.length); // selector -> re-renders only when count changes
  return <span>{count}</span>;
}
```

### Comparison

| | Context | Redux Toolkit | Zustand |
|---|---|---|---|
| Boilerplate | Low | Medium | Very low |
| Re-render control | Poor (all consumers) | Selectors | Selectors |
| DevTools / middleware | No | Excellent | Yes (middleware) |
| Best for | Theme, auth, low-frequency | Large apps, teams, complex flows | Small–large apps wanting simplicity |

**Interview Qs**
- Why Redux? → Predictable centralized state, devtools, middleware, scalable patterns.
- What is a thunk? → A function returned instead of an action; middleware runs it with `dispatch`/`getState` for async logic.
- Redux vs Context? (above)
- How does RTK allow mutation in reducers? → Immer creates an immutable copy from the "mutated" draft.

---

## 37. State Management II: Choosing a Tool, Jotai, Redux-Saga & State Machines

### Choosing where state lives (decision guide)

| Question | Put it in |
|---|---|
| Used by one component? | `useState` / `useReducer` |
| Shared by a few nearby components? | Lift to the closest common parent |
| Comes from the server (lists, profiles, orders)? | **TanStack Query / RTK Query / SWR** (server state) |
| Should survive refresh / be shareable (filters, tab, page)? | **URL** search params |
| Form inputs & validation? | **React Hook Form** (+ Zod) |
| Low-frequency global values (theme, locale, current user)? | **Context** |
| Frequently updated global client state (cart, editor, UI panels)? | **Zustand**, **Jotai**, or **Redux Toolkit** |
| Complex multi-step flows with strict rules (checkout, wizard, video player)? | **State machine** (`useReducer` or XState) |

Most apps need **much less global state** than they think once server state is in a query library and UI state lives in the URL.

---

### Jotai — atomic state

**Atoms** are tiny independent pieces of state. Components subscribe only to the atoms they use → fine-grained re-renders without selectors. Built "bottom-up" (compose small atoms) vs Redux's "top-down" single store.

```jsx
import { atom, useAtom, useAtomValue, useSetAtom } from "jotai";
import { atomWithStorage } from "jotai/utils";

// 1. Primitive atoms
export const cartAtom = atom([]);                           // [{ id, name, price, qty }]
export const themeAtom = atomWithStorage("theme", "light"); // persisted in localStorage

// 2. Derived (read-only) atom — recomputes when dependencies change
export const cartTotalAtom = atom((get) =>
  get(cartAtom).reduce((sum, item) => sum + item.price * item.qty, 0)
);

// 3. Write-only "action" atom
export const addToCartAtom = atom(null, (get, set, product) => {
  const cart = get(cartAtom);
  const existing = cart.find((i) => i.id === product.id);
  set(cartAtom, existing
    ? cart.map((i) => (i.id === product.id ? { ...i, qty: i.qty + 1 } : i))
    : [...cart, { ...product, qty: 1 }]);
});

// 4. Async atom (works with Suspense)
export const userIdAtom = atom(1);
export const userAtom = atom(async (get) => {
  const res = await fetch(`/api/users/${get(userIdAtom)}`);
  return res.json();
});
```

```jsx
function CartBadge() {
  const total = useAtomValue(cartTotalAtom);    // re-renders only when the total changes
  return <span>₹{total}</span>;
}

function AddButton({ product }) {
  const addToCart = useSetAtom(addToCartAtom);  // write-only → never re-renders on cart changes
  return <button onClick={() => addToCart(product)}>Add</button>;
}

function ThemeToggle() {
  const [theme, setTheme] = useAtom(themeAtom);
  return <button onClick={() => setTheme(theme === "light" ? "dark" : "light")}>{theme}</button>;
}
```

**Jotai vs Zustand vs Redux Toolkit**

| | Jotai | Zustand | Redux Toolkit |
|---|---|---|---|
| Model | Many small atoms | One (or few) stores with actions | Single store, slices, actions, reducers |
| Re-render control | Automatic per atom | Selectors | Selectors |
| Boilerplate | Very low | Very low | Medium |
| DevTools / middleware | Some | Yes | Excellent (time travel, middleware, RTK Query) |
| Sweet spot | Lots of independent/derived UI state, editors | Simple global stores | Large teams, complex domains, strict patterns |

---

### Redux-Saga — complex async workflows with generators

**Redux-Saga** is Redux middleware that handles side effects with **generator functions**. Sagas listen for actions and run async flows that can be **paused, cancelled, raced, debounced and tested** step by step. You'll see it in many existing codebases; for new code, **RTK Query** (data fetching) and the **RTK listener middleware** usually cover the same needs with less complexity.

Key effects (from `redux-saga/effects`): `takeEvery` / `takeLatest` (listen), `call` (call a function/promise), `put` (dispatch), `select` (read state), `fork`/`spawn` (run in parallel), `take` (wait for an action), `race`, `delay`, `cancel`, `all`, `debounce`.

```js
// sagas/userSaga.js
import { call, put, takeLatest, delay, race, take, select } from "redux-saga/effects";

function* fetchUser(action) {
  try {
    const user = yield call(api.getUser, action.payload.id);       // pauses until the promise resolves
    yield put({ type: "user/fetchSucceeded", payload: user });
  } catch (err) {
    yield put({ type: "user/fetchFailed", error: err.message });
  }
}

// Poll every 5s until "stopPolling" is dispatched
function* pollOrders() {
  while (true) {
    const { stop } = yield race({
      tick: delay(5000),
      stop: take("orders/stopPolling"),
    });
    if (stop) return;
    const status = yield select((state) => state.orders.filter);
    yield call(refreshOrders, status);
  }
}

export default function* rootSaga() {
  yield takeLatest("user/fetchRequested", fetchUser);   // new request cancels the previous one (no races)
  yield takeLatest("orders/startPolling", pollOrders);
}
```

```js
// store.js
import createSagaMiddleware from "redux-saga";
const sagaMiddleware = createSagaMiddleware();
export const store = configureStore({
  reducer,
  middleware: (getDefault) => getDefault({ thunk: false }).concat(sagaMiddleware),
});
sagaMiddleware.run(rootSaga);
```

Testing a saga = stepping through the generator (no real API calls):

```js
test("fetchUser success", () => {
  const gen = fetchUser({ payload: { id: 1 } });
  expect(gen.next().value).toEqual(call(api.getUser, 1));
  expect(gen.next({ id: 1, name: "A" }).value).toEqual(put({ type: "user/fetchSucceeded", payload: { id: 1, name: "A" } }));
});
```

**Modern alternative — RTK listener middleware** (async/await instead of generators):

```js
import { createListenerMiddleware } from "@reduxjs/toolkit";

export const listener = createListenerMiddleware();

listener.startListening({
  actionCreator: searchChanged,
  effect: async (action, api) => {
    api.cancelActiveListeners();          // like takeLatest: cancel previous runs
    await api.delay(300);                 // debounce
    const results = await searchApi(action.payload, { signal: api.signal });
    api.dispatch(searchResultsReceived(results));
  },
});
// configureStore({ ..., middleware: (gDM) => gDM().prepend(listener.middleware) })
```

**Thunks vs Sagas vs Listeners**: thunks for simple one-off async logic; listeners for reacting to actions (debounce, cancel, workflows) with async/await; sagas for very complex long-running flows in codebases that already use them.

---

### State machines: making impossible states impossible

Many UI bugs come from **invalid state combinations** (`isLoading && isError`, submitting twice, "success" screen with no data). A **finite state machine** lists the allowed states and which events move between them.

```jsx
// A small state machine with useReducer (no library needed)
const machine = {
  idle:       { SUBMIT: "submitting" },
  submitting: { SUCCESS: "success", FAILURE: "error" },
  error:      { SUBMIT: "submitting", RESET: "idle" },
  success:    { RESET: "idle" },
};

function reducer(state, event) {
  const next = machine[state.status][event.type];
  if (!next) return state;                                    // event not allowed in this state → ignored
  return { status: next, data: event.data ?? state.data, error: event.error ?? null };
}

function CheckoutButton({ pay }) {
  const [state, send] = useReducer(reducer, { status: "idle", data: null, error: null });

  async function handleClick() {
    if (!machine[state.status].SUBMIT) return;                // not allowed in this state → don't start another payment
    send({ type: "SUBMIT" });
    try {
      const receipt = await pay();
      send({ type: "SUCCESS", data: receipt });
    } catch (e) {
      send({ type: "FAILURE", error: e.message });
    }
  }

  if (state.status === "success") return <p>Paid! Receipt #{state.data.id}</p>;
  return (
    <>
      <button onClick={handleClick} disabled={state.status === "submitting"}>
        {state.status === "submitting" ? "Processing…" : "Pay"}
      </button>
      {state.status === "error" && <p role="alert">{state.error}</p>}
    </>
  );
}
```

For bigger flows (multi-step wizards, media players, complex forms with parallel states, timers, guards), **XState** gives statecharts, visual tooling and actors.

### Interview Qs

1. How do you decide where a piece of state should live?
2. Server state vs client state — why keep them separate?
3. What is Jotai and how does it differ from Redux/Zustand?
4. What are derived atoms / selectors and why do they reduce re-renders?
5. What is Redux-Saga? What do `call`, `put`, `takeLatest`, `race` do?
6. Thunk vs saga vs listener middleware?
7. Why are generators useful for side-effect management (and testing)?
8. What is a finite state machine and how does it prevent UI bugs?

---

## 38. Data Fetching

### Problems with fetching in useEffect

Race conditions, no caching, no dedupe, no retry, no background refetch, loading/error boilerplate, waterfalls.

### TanStack Query (React Query)

Manages **server state**: caching, deduping, background refetching, pagination, optimistic updates, retries.

```jsx
import { QueryClient, QueryClientProvider, useQuery, useMutation, useQueryClient } from "@tanstack/react-query";

const queryClient = new QueryClient({ defaultOptions: { queries: { staleTime: 60_000 } } });
<QueryClientProvider client={queryClient}><App /></QueryClientProvider>;

function Todos() {
  const { data, isPending, isError, error, isFetching } = useQuery({
    queryKey: ["todos"],
    queryFn: () => fetch("/api/todos").then((r) => r.json()),
  });
  if (isPending) return <Spinner />;
  if (isError) return <p>{error.message}</p>;
  return data.map((t) => <p key={t.id}>{t.title}</p>);
}

function Todo({ id }) {
  const { data } = useQuery({
    queryKey: ["todo", id],             // key includes variables -> cached per id
    queryFn: () => fetchTodo(id),
    enabled: !!id,                      // dependent query
  });
}

function AddTodo() {
  const qc = useQueryClient();
  const mutation = useMutation({
    mutationFn: (title) => fetch("/api/todos", { method: "POST", body: JSON.stringify({ title }) }),
    onSuccess: () => qc.invalidateQueries({ queryKey: ["todos"] }), // refetch list
  });
  return <button onClick={() => mutation.mutate("New")} disabled={mutation.isPending}>Add</button>;
}
```

Key concepts: `queryKey`, `staleTime` (how long data is fresh), `gcTime` (how long unused cache is kept), `refetchOnWindowFocus`, `invalidateQueries`, `useInfiniteQuery`, `prefetchQuery`, optimistic updates via `onMutate`.

### Axios interceptors (auth token + refresh)

```js
const api = axios.create({ baseURL: "/api" });
api.interceptors.request.use((config) => {
  const token = localStorage.getItem("token");
  if (token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});
api.interceptors.response.use(
  (res) => res,
  async (err) => {
    if (err.response?.status === 401 && !err.config._retry) {
      err.config._retry = true;
      await refreshToken();
      return api(err.config);
    }
    return Promise.reject(err);
  }
);
```

### Avoid waterfalls

```jsx
// ❌ child fetch starts only after parent's fetch finishes & renders
// ✅ fetch in parallel at the route level (loaders), Promise.all, or prefetch
```

---

## 39. Styling

| Approach | Example | Notes |
|---|---|---|
| Plain CSS | `import "./App.css"` | Global scope, name clashes |
| CSS Modules | `import s from "./Btn.module.css"; className={s.primary}` | Locally scoped class names |
| Tailwind CSS | `className="px-4 py-2 bg-blue-600 rounded"` | Utility-first, very popular |
| CSS-in-JS | styled-components, Emotion | Dynamic styles, runtime cost |
| Inline styles | `style={{ color: "red" }}` | No pseudo-classes/media queries |
| Component libs | MUI, Chakra, shadcn/ui, Radix | Prebuilt accessible components |

```jsx
// CSS Modules
import styles from "./Button.module.css";
<button className={`${styles.btn} ${isPrimary ? styles.primary : ""}`}>Go</button>;

// clsx for conditional classes
import clsx from "clsx";
<div className={clsx("card", { active: isActive, disabled })} />;

// styled-components
const Button = styled.button`
  padding: 8px 16px;
  background: ${(p) => (p.$primary ? "royalblue" : "white")};
  &:hover { opacity: 0.9; }
`;
```

---

## 40. Internationalization (i18n), Theming & Dark Mode, Design Tokens

### Part 1 — Internationalization (i18n)

- **i18n** (internationalization): building the app so it *can* support many languages/regions.
- **l10n** (localization): actually translating & adapting it for one locale (`hi-IN`, `de-DE`, `ar-SA`).
- A **locale** = language + region (`en-IN` vs `en-US` differ in number grouping, date order, currency).

What changes per locale: text, **plural rules**, number/currency/date/time formats, text direction (**RTL** for Arabic/Hebrew/Urdu), sorting, names/addresses, and layout (German text is ~30% longer than English).

#### Formatting with `Intl` (built into every browser & Node)

```js
new Intl.NumberFormat("en-IN", { style: "currency", currency: "INR" }).format(1234567.5);  // "₹12,34,567.50"
new Intl.NumberFormat("de-DE", { style: "currency", currency: "EUR" }).format(1234567.5);  // "1.234.567,50 €"
new Intl.NumberFormat("en", { notation: "compact" }).format(1_250_000);                    // "1.3M"

const d = new Date("2026-09-24T10:00:00Z");
new Intl.DateTimeFormat("en-GB", { dateStyle: "long", timeZone: "UTC" }).format(d);          // "24 September 2026"
new Intl.DateTimeFormat("hi-IN", { dateStyle: "long", timeZone: "UTC" }).format(d);          // "24 सितंबर 2026"

new Intl.RelativeTimeFormat("en", { numeric: "auto" }).format(-1, "day");                   // "yesterday"
new Intl.ListFormat("en", { style: "long", type: "conjunction" }).format(["A", "B", "C"]);  // "A, B, and C"

new Intl.PluralRules("en").select(1);    // "one"
new Intl.PluralRules("en").select(5);    // "other"
new Intl.PluralRules("ar").select(2);    // "two"   ← Arabic has 6 plural forms; never hard-code `count === 1`
```

Create formatters once and reuse them (constructing `Intl` objects in hot loops is slow).

**Testing gotcha**: `Intl` output often contains **non-breaking spaces** (U+00A0, U+202F) — e.g. the space before `€` in `"1.234.567,50 €"`. A test like `expect(format(x)).toBe("1.234.567,50 €")` typed with a normal space fails even though the strings look identical. Normalize (`s.replace(/\s/g, " ")`) or compare against another `Intl` call. Output can also change slightly between ICU/browser versions — don't snapshot it blindly.

#### react-i18next setup

```js
// i18n.js
import i18n from "i18next";
import { initReactI18next } from "react-i18next";
import LanguageDetector from "i18next-browser-languagedetector";
import HttpBackend from "i18next-http-backend";

i18n
  .use(HttpBackend)                 // lazy-load /locales/{lng}/{ns}.json instead of bundling every language
  .use(LanguageDetector)            // ?lng= → cookie/localStorage → browser language
  .use(initReactI18next)
  .init({
    fallbackLng: "en",
    supportedLngs: ["en", "hi", "de", "ar"],
    ns: ["common", "checkout"],
    defaultNS: "common",
    interpolation: { escapeValue: false },   // React already escapes
  });

export default i18n;
```

```json
// public/locales/en/common.json
{
  "greeting": "Hello, {{name}}!",
  "cart": {
    "items_one": "{{count}} item in your cart",
    "items_other": "{{count}} items in your cart"
  },
  "terms": "I agree to the <link>terms of service</link>",
  "price": "Total: {{amount, currency(INR)}}"
}
```

```jsx
import { useTranslation, Trans } from "react-i18next";

function CartSummary({ user, count, total }) {
  const { t, i18n } = useTranslation();
  return (
    <>
      <h2>{t("greeting", { name: user.name })}</h2>
      <p>{t("cart.items", { count })}</p>                        {/* picks _one / _other using plural rules */}
      <p>{t("price", { amount: total })}</p>
      <label>
        <input type="checkbox" />
        <Trans i18nKey="terms" components={{ link: <a href="/terms" /> }} />   {/* JSX inside translations */}
      </label>
      <select value={i18n.resolvedLanguage} onChange={(e) => i18n.changeLanguage(e.target.value)} aria-label="Language">
        <option value="en">English</option>
        <option value="hi">हिन्दी</option>
        <option value="ar">العربية</option>
      </select>
    </>
  );
}
```

Keep `<html lang>` and `dir` in sync with the language:

```js
i18n.on("languageChanged", (lng) => {
  document.documentElement.lang = lng;
  document.documentElement.dir = i18n.dir(lng);        // "rtl" for ar/he/ur
});
```

#### RTL-friendly CSS: use logical properties

```css
/* ❌ physical — wrong side in RTL */
.card { margin-left: 16px; padding-right: 8px; text-align: left; border-left: 4px solid; }

/* ✅ logical — flips automatically with dir="rtl" */
.card { margin-inline-start: 16px; padding-inline-end: 8px; text-align: start; border-inline-start: 4px solid; }
```

Also mirror directional icons (arrows, "back"), but not logos, media controls or numbers.

#### i18n best practices

- **Never concatenate** translated fragments (`t("hello") + name + t("welcome")`) — word order differs by language; use interpolation.
- Use **plural forms** from the library (`_one`, `_few`, `_many`, `_other` / ICU `{count, plural, …}`), never `count === 1 ? … : …`.
- **Keys by meaning** (`checkout.payButton`), not by English text; give translators **context** (descriptions, screenshots).
- Format numbers/dates/currency with **`Intl`** using the user's locale; store dates in UTC, money as minor units.
- Design for **text expansion** (+30–40%) and **RTL**; no text baked into images.
- **Pseudo-localization** in dev (e.g. `[Ĥéļļö ŵöŕļð !!!]`) to find hard-coded strings and layout overflow.
- **Lazy-load** languages/namespaces; fall back to a default language for missing keys (and report missing keys).
- **SEO**: locale in the URL (`/de/products`), `hreflang` alternate links, translated metadata. Next.js: `next-intl`.
- Persist the chosen language (cookie so the **server** can render the right locale too).
- Translation management platforms (Crowdin, Lokalise, Phrase) sync keys with your repo.
- Alternatives: **react-intl / FormatJS** (ICU message syntax), **Lingui**, **next-intl**.

---

### Part 2 — Theming & dark mode

The modern approach: **CSS custom properties (variables)** hold the theme; switching themes = changing variables on `<html>`. No re-render of the React tree needed.

```css
:root {
  --color-bg: #ffffff;
  --color-surface: #f6f7f9;
  --color-text: #111827;
  --color-text-muted: #4b5563;
  --color-primary: #4f46e5;
  --color-border: #e5e7eb;
  color-scheme: light;                    /* native form controls & scrollbars match the theme */
}

/* follow the OS when the user chose "system" (no data-theme attribute) */
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --color-bg: #0b0f19;
    --color-surface: #151b2b;
    --color-text: #e5e7eb;
    --color-text-muted: #9ca3af;
    --color-primary: #818cf8;             /* lighter primary keeps contrast on dark backgrounds */
    --color-border: #273044;
    color-scheme: dark;
  }
}

/* explicit user choice */
:root[data-theme="dark"] {
  --color-bg: #0b0f19;
  --color-surface: #151b2b;
  --color-text: #e5e7eb;
  --color-text-muted: #9ca3af;
  --color-primary: #818cf8;
  --color-border: #273044;
  color-scheme: dark;
}

body { background: var(--color-bg); color: var(--color-text); }
.card { background: var(--color-surface); border: 1px solid var(--color-border); }
.button-primary { background: var(--color-primary); }
```

#### Three-way preference: light / dark / system

```js
// pure logic (easy to test)
export function resolveTheme(preference, systemPrefersDark) {
  if (preference === "light" || preference === "dark") return preference;
  return systemPrefersDark ? "dark" : "light";                   // "system" or unknown → follow the OS
}
```

```jsx
import { useEffect, useState, useSyncExternalStore } from "react";

const query = "(prefers-color-scheme: dark)";
function useSystemDark() {
  return useSyncExternalStore(
    (cb) => { const m = matchMedia(query); m.addEventListener("change", cb); return () => m.removeEventListener("change", cb); },
    () => matchMedia(query).matches,
    () => false,                                                  // server snapshot
  );
}

export function useTheme() {
  const [preference, setPreference] = useState(() => {
    try { return localStorage.getItem("theme") ?? "system"; } catch { return "system"; }
  });
  const systemDark = useSystemDark();
  const resolved = resolveTheme(preference, systemDark);

  useEffect(() => {
    const root = document.documentElement;
    if (preference === "system") root.removeAttribute("data-theme");   // CSS media query takes over
    else root.setAttribute("data-theme", preference);
    try { localStorage.setItem("theme", preference); } catch {}
  }, [preference]);

  return { preference, resolved, setPreference };
}

function ThemeSwitcher() {
  const { preference, setPreference } = useTheme();
  return (
    <select aria-label="Theme" value={preference} onChange={(e) => setPreference(e.target.value)}>
      <option value="system">System</option>
      <option value="light">Light</option>
      <option value="dark">Dark</option>
    </select>
  );
}
```

#### Avoid the "flash of the wrong theme"

React runs after the first paint, so a saved dark preference would briefly show the light theme. Apply the theme **before paint** with a tiny inline script in `<head>`:

```html
<script>
  try {
    var t = localStorage.getItem("theme");
    if (t === "light" || t === "dark") document.documentElement.setAttribute("data-theme", t);
  } catch (e) {}
</script>
```

(In Next.js, `next-themes` handles this, plus `suppressHydrationWarning` on `<html>`.)

#### Tailwind dark mode

```css
/* Tailwind v4: dark: variant driven by the data-theme attribute */
@custom-variant dark (&:where([data-theme=dark], [data-theme=dark] *));
```

```jsx
<div className="bg-white text-gray-900 dark:bg-gray-950 dark:text-gray-100">…</div>
```

Better still: map Tailwind colors to your CSS variables (`bg-surface`, `text-muted`) so components don't need `dark:` everywhere.

#### Dark-mode design tips

- Don't just invert: use **dark grays** (not pure black) and **slightly desaturated/lighter** accent colors.
- Check **contrast** in both themes (WCAG AA: 4.5:1 for text).
- Shadows are barely visible on dark backgrounds — use **lighter surfaces/borders** to show elevation.
- Provide dark-friendly images/illustrations or use `<picture>` with `media="(prefers-color-scheme: dark)"`.
- Charts need theme-aware colors too.

---

### Part 3 — Design tokens

**Design tokens** are named, platform-agnostic design decisions — colors, spacing, typography, radii, shadows, motion, z-index — stored as data and turned into CSS variables, JS/TS constants, iOS and Android resources. They're the single source of truth shared by designers (Figma variables) and developers.

#### Three tiers

| Tier | Example | Purpose |
|---|---|---|
| **Primitive / global** | `color.indigo.600 = #4f46e5`, `space.4 = 16px` | The raw palette/scale |
| **Semantic / alias** | `color.action.primary = {color.indigo.600}`, `color.text.default` | Meaning — what the value is *for*; themes swap these |
| **Component** | `button.primary.bg = {color.action.primary}` | Optional, per-component overrides |

Components should use **semantic** tokens (`--color-text-muted`), never primitives (`--indigo-600`) — then a new theme or brand only remaps the semantic layer.

```json
{
  "color": {
    "indigo": { "600": { "$value": "#4f46e5", "$type": "color" } },
    "gray": { "900": { "$value": "#111827", "$type": "color" } }
  },
  "space": { "2": { "$value": "8px" }, "4": { "$value": "16px" } },
  "semantic": {
    "action-primary": { "$value": "{color.indigo.600}" },
    "text-default": { "$value": "{color.gray.900}" }
  }
}
```

#### Turning tokens into CSS variables (what Style Dictionary does, in miniature)

```js
// flatten nested tokens and resolve {references}
export function tokensToCssVars(tokens) {
  const flat = {};
  (function walk(node, path) {
    if (node && typeof node === "object" && "$value" in node) { flat[path.join(".")] = node.$value; return; }
    for (const [key, child] of Object.entries(node)) walk(child, [...path, key]);
  })(tokens, []);

  const resolve = (value, seen = new Set()) =>
    typeof value === "string"
      ? value.replace(/\{([^}]+)\}/g, (_, ref) => {
          if (seen.has(ref)) throw new Error(`Circular token reference: ${ref}`);
          if (!(ref in flat)) throw new Error(`Unknown token reference: ${ref}`);
          return resolve(flat[ref], new Set([...seen, ref]));
        })
      : value;

  return Object.entries(flat)
    .map(([name, value]) => `  --${name.replace(/\./g, "-")}: ${resolve(value)};`)
    .join("\n");
}
// → "  --color-indigo-600: #4f46e5;\n  --semantic-action-primary: #4f46e5;\n …"
```

In real projects use **Style Dictionary** (or Tokens Studio / Figma variables export) to generate CSS, TS, iOS and Android outputs from the same JSON, in CI.

#### Consuming tokens

```css
.button-primary {
  background: var(--semantic-action-primary);
  padding: var(--space-2) var(--space-4);
  border-radius: var(--radius-md);
  transition: background var(--motion-fast) ease-out;
}
```

```ts
// Generated TS tokens for charts, canvas, or JS animations
import { tokens } from "@acme/design-tokens";
chart.setColors([tokens.color.chart1, tokens.color.chart2]);
```

#### Design system best practices

- One **token source of truth** synced with design tools; generate code in CI (no hand-copied hex values).
- Semantic naming by **purpose** (`surface`, `text-muted`, `danger`), not by appearance (`light-gray-2`).
- Themes (dark, high-contrast, brands) = alternate **semantic** mappings.
- A small set of **primitive components** (Button, Input, Card, Modal) built on tokens; document them in **Storybook**.
- Lint for raw values (stylelint rules against hard-coded colors/px).
- Version the token package; changes go through review like code.

### Interview Qs

1. i18n vs l10n? What varies between locales besides text?
2. Why must you never build sentences by concatenating translated strings?
3. How do plural rules differ across languages? How does react-i18next handle them?
4. How do you support RTL languages in CSS?
5. How would you implement light/dark/system theming? Why CSS variables instead of React context for colors?
6. How do you prevent the flash of the wrong theme on page load?
7. What are design tokens? Primitive vs semantic tokens?
8. How do design tokens enable multi-brand or dark themes without changing components?

---

## 41. Rendering Strategies: CSR, SSR, SSG, ISR

| Strategy | HTML generated | Pros | Cons | Use for |
|---|---|---|---|---|
| **CSR** (Client-Side Rendering) | In browser by JS | Rich interactivity, cheap hosting | Slow first paint, weaker SEO | Dashboards, apps behind login |
| **SSR** (Server-Side Rendering) | On server per request | Fast first paint, SEO, fresh data | Server cost, TTFB | Personalised/dynamic pages |
| **SSG** (Static Site Generation) | At build time | Fastest (CDN), cheap | Stale until rebuild | Blogs, docs, marketing |
| **ISR** (Incremental Static Regeneration) | Static, regenerated in background after N seconds | Static speed + freshness | Some staleness | E-commerce product pages |
| **RSC** (React Server Components) | Components run on server, stream to client | Zero JS for server components, direct DB access | New mental model | Next.js App Router |
| **Streaming SSR** | Server sends HTML in chunks with Suspense | Faster TTFB & progressive UI | | |

---

## 42. Server Components & Next.js Basics

### React Server Components (RSC)

- Run **only on the server** (at build or request time). Their code is **never sent to the browser**.
- Can be `async` and access DB/filesystem/secrets directly.
- **Can't** use state, effects, browser APIs, or event handlers.
- **Client Components** are marked with `"use client"` at the top of a file; they're rendered on the server for the initial HTML and hydrated in the browser.
- Server components can render client components (pass serializable props). Client components can receive server components as `children`.

```jsx
// app/posts/page.jsx — Server Component (default in Next.js App Router)
import db from "@/lib/db";
import LikeButton from "./LikeButton";

export default async function PostsPage() {
  const posts = await db.post.findMany(); // direct DB access
  return posts.map((p) => (
    <article key={p.id}>
      <h2>{p.title}</h2>
      <LikeButton postId={p.id} />
    </article>
  ));
}
```

```jsx
// app/posts/LikeButton.jsx — Client Component
"use client";
import { useState } from "react";
export default function LikeButton({ postId }) {
  const [liked, setLiked] = useState(false);
  return <button onClick={() => setLiked(!liked)}>{liked ? "♥" : "♡"}</button>;
}
```

### Server Actions

```jsx
// app/actions.js
"use server";
import { revalidatePath } from "next/cache";
export async function createPost(formData) {
  await db.post.create({ data: { title: formData.get("title") } });
  revalidatePath("/posts");
}

// in a component
<form action={createPost}><input name="title" /><button>Create</button></form>
```

### Next.js App Router essentials

- File-based routing: `app/page.jsx`, `app/blog/[slug]/page.jsx`, `app/(group)/...`.
- Special files: `layout.jsx`, `page.jsx`, `loading.jsx` (Suspense), `error.jsx` (error boundary), `not-found.jsx`, `route.js` (API handler), `middleware.js`.
- Caching & data: `fetch(url, { cache: "force-cache" | "no-store", next: { revalidate: 60 } })`.
- `generateStaticParams` for SSG of dynamic routes; `generateMetadata` for SEO.
- `next/image`, `next/link`, `next/font` optimizations.

```jsx
// app/blog/[slug]/page.jsx
export async function generateStaticParams() {
  const posts = await getPosts();
  return posts.map((p) => ({ slug: p.slug }));
}
export async function generateMetadata({ params }) {
  const { slug } = await params;
  return { title: `Blog: ${slug}` };
}
export default async function Post({ params }) {
  const { slug } = await params;
  const post = await getPost(slug);
  return <article>{post.content}</article>;
}
```

**Interview Qs**
- Server vs Client Components? (above)
- Next.js vs React? → React is a UI library; Next.js is a full-stack framework (routing, SSR/SSG, API routes, optimizations).
- SSR vs SSG? (table)

---

## 43. Hydration

**Hydration** = React attaching event listeners and state to **server-rendered HTML** in the browser, making it interactive.

```jsx
import { hydrateRoot } from "react-dom/client";
hydrateRoot(document.getElementById("root"), <App />);
```

### Hydration mismatch

When the server HTML differs from the first client render. Causes: `Date.now()`, `Math.random()`, `window`/`localStorage` access during render, locale-dependent formatting, invalid HTML nesting (`<div>` in `<p>`), browser extensions.

```jsx
// ❌ mismatch
function Time() { return <p>{new Date().toLocaleTimeString()}</p>; }

// ✅ render client-only values after mount
function Time() {
  const [time, setTime] = useState(null);
  useEffect(() => setTime(new Date().toLocaleTimeString()), []);
  return <p>{time ?? "…"}</p>;
}
// or suppressHydrationWarning for unavoidable text differences
<time suppressHydrationWarning>{new Date().toISOString()}</time>
```

**Selective hydration** (React 18): with Suspense, parts hydrate independently and React prioritizes the parts the user interacts with.

---

## 44. Next.js App Router Deep Dive (+ Animations)

Builds on "Server Components & Next.js Basics" and "Hydration". Next.js APIs evolve quickly (caching changed a lot between versions 14 → 15 → 16), so always check the docs for **your** version. The concepts below are stable.

### 1. File conventions (App Router)

```
app/
├── layout.tsx              # root layout (required) — <html>, <body>, providers
├── page.tsx                # "/"
├── loading.tsx             # Suspense fallback for this segment (instant loading UI)
├── error.tsx               # error boundary for this segment ("use client")
├── not-found.tsx           # 404 UI (notFound())
├── global-error.tsx        # catches errors in the root layout
├── (marketing)/            # route GROUP — organizes files, not part of the URL
│   ├── about/page.tsx      # "/about"
│   └── layout.tsx          # layout only for marketing pages
├── dashboard/
│   ├── layout.tsx          # persistent dashboard shell (sidebar keeps state across pages)
│   ├── page.tsx            # "/dashboard"
│   ├── @analytics/page.tsx # PARALLEL route slot rendered next to children
│   └── settings/page.tsx   # "/dashboard/settings"
├── blog/
│   ├── [slug]/page.tsx     # dynamic segment "/blog/hello-world"
│   └── [...path]/page.tsx  # catch-all "/blog/a/b/c"
├── shop/[[...filters]]/page.tsx   # optional catch-all ("/shop" and "/shop/x/y")
├── photos/(.)[id]/page.tsx # INTERCEPTING route (open photo in a modal on client nav)
├── api/users/route.ts      # route handler (API endpoint)
├── _components/            # private folder — ignored by routing
├── sitemap.ts, robots.ts   # generated SEO files
└── opengraph-image.tsx     # generated OG image
```

- **Layouts persist** across navigation (don't re-mount) → good for shells, sidebars, players. `template.tsx` re-mounts on every navigation instead.
- `params` and `searchParams` are **Promises** in recent versions: `const { slug } = await params;`.

### 2. Server/Client boundary rules (the #1 source of confusion)

- Components are **Server Components by default**. `"use client"` at the top of a file marks it (and everything it imports) as client code.
- Push `"use client"` **down to the leaves** (buttons, forms, interactive widgets) — keep pages/layouts on the server.
- Props from server → client must be **serializable** (no functions, class instances, Dates become strings in some cases — pass plain data).
- A client component **can't import** a server component, but can render one passed as `children`/props:

```tsx
// app/dashboard/page.tsx (server)
import Sidebar from "./Sidebar";          // client component
import RecentOrders from "./RecentOrders";// server component (fetches data)

export default function Page() {
  return (
    <Sidebar>                             {/* client wrapper */}
      <RecentOrders />                    {/* still rendered on the server */}
    </Sidebar>
  );
}
```

- Protect server-only code from being bundled into the client:

```ts
// lib/db.ts
import "server-only";                     // build error if imported from a client component
export const db = new PrismaClient();
```

- Env vars without `NEXT_PUBLIC_` are only available on the server; `NEXT_PUBLIC_*` are **inlined into client JS** (public!).

### 3. Data fetching in Server Components

```tsx
// ❌ Waterfall: second request waits for the first
const user = await getUser(id);
const orders = await getOrders(id);

// ✅ Parallel
const [user, orders] = await Promise.all([getUser(id), getOrders(id)]);
```

### Streaming with Suspense

Render the page shell immediately and stream slow parts as they finish.

```tsx
// app/product/[id]/page.tsx
import { Suspense } from "react";

export default async function ProductPage({ params }: { params: Promise<{ id: string }> }) {
  const { id } = await params;
  const product = await getProduct(id);          // fast, needed for the main content
  return (
    <>
      <ProductDetails product={product} />
      <Suspense fallback={<ReviewsSkeleton />}>
        <Reviews productId={id} />               {/* slow — streamed in later */}
      </Suspense>
      <Suspense fallback={<RecsSkeleton />}>
        <Recommendations productId={id} />
      </Suspense>
    </>
  );
}

async function Reviews({ productId }: { productId: string }) {
  const reviews = await getReviews(productId);   // doesn't block the rest of the page
  return <ReviewList reviews={reviews} />;
}
```

Passing a promise to a client component and unwrapping it with `use()`:

```tsx
// server
const statsPromise = getStats();                 // don't await
return <Suspense fallback={<Spinner />}><StatsChart statsPromise={statsPromise} /></Suspense>;

// client
"use client";
import { use } from "react";
export function StatsChart({ statsPromise }: { statsPromise: Promise<Stats> }) {
  const stats = use(statsPromise);
  return <Chart data={stats} />;
}
```

### 4. Caching & revalidation

Conceptual layers (names used in the docs):

| Layer | Where | What | Duration |
|---|---|---|---|
| **Request memoization** | Server, per request | Identical `fetch` calls (or `React.cache()` functions) in one render run once | One request |
| **Data cache** | Server, persistent | Results of cached `fetch`/cached functions | Until revalidated |
| **Full route cache** | Server | Pre-rendered HTML + RSC payload of **static** routes | Until revalidated/redeployed |
| **Router cache** | Browser | RSC payloads of visited/prefetched routes (instant back/forward) | Session / short time |

**Static vs dynamic rendering**: a route is rendered **statically** at build time (fast, CDN-cacheable) unless it uses **dynamic APIs** — `cookies()`, `headers()`, `searchParams`, `connection()`, uncached data — in which case it renders **per request**.

```tsx
// Time-based revalidation (ISR): regenerate at most every 60s
const res = await fetch("https://api.shop.com/products", { next: { revalidate: 60, tags: ["products"] } });

// Never cache (always fresh)
const res2 = await fetch(url, { cache: "no-store" });

// Segment-level config
export const revalidate = 300;             // whole page ISR every 5 minutes

// On-demand revalidation after a mutation (Server Action / route handler / webhook)
import { revalidatePath, revalidateTag } from "next/cache";
revalidateTag("products");                 // everything tagged "products"
revalidatePath("/products");               // a specific path
```

```tsx
// Dedupe & cache non-fetch data access within a request (ORM calls)
import { cache } from "react";
export const getUser = cache(async (id: string) => db.user.findUnique({ where: { id } }));
// Called in layout + page + metadata → one DB query per request
```

Version notes:
- **v15** made `fetch` and GET route handlers **uncached by default** (opt in with `cache: "force-cache"`/`revalidate`).
- **v16** introduced **Cache Components**: the `"use cache"` directive (on functions/components/pages) with `cacheLife("hours")` and `cacheTag("products")` for explicit caching, plus Partial Prerendering (static shell + dynamic holes). Check which model your project uses.

```tsx
// Next 16 style (with cacheComponents enabled)
import { cacheLife, cacheTag } from "next/cache";
export async function getProducts() {
  "use cache";
  cacheLife("hours");
  cacheTag("products");
  return db.product.findMany();
}
```

### 5. Server Actions (and their security)

Server Actions are async functions marked `"use server"` that the client can call — used for mutations and forms.

```tsx
// app/posts/actions.ts
"use server";
import { z } from "zod";
import { revalidatePath } from "next/cache";
import { redirect } from "next/navigation";

const PostSchema = z.object({ title: z.string().min(1).max(200), body: z.string().max(10_000) });

export async function createPost(prevState: { error?: string } | undefined, formData: FormData) {
  const session = await auth();                                   // 1. AUTHENTICATE inside the action
  if (!session) return { error: "Please log in" };

  const parsed = PostSchema.safeParse(Object.fromEntries(formData));   // 2. VALIDATE input
  if (!parsed.success) return { error: parsed.error.issues[0].message };

  if (!(await canCreatePost(session.user))) return { error: "Not allowed" };   // 3. AUTHORIZE

  const post = await db.post.create({ data: { ...parsed.data, authorId: session.user.id } }); // server decides authorId
  revalidatePath("/posts");
  redirect(`/posts/${post.id}`);
}
```

```tsx
// app/posts/new/page.tsx
"use client";
import { useActionState } from "react";
import { createPost } from "../actions";

export default function NewPost() {
  const [state, formAction, pending] = useActionState(createPost, undefined);
  return (
    <form action={formAction}>
      <input name="title" required />
      <textarea name="body" />
      {state?.error && <p role="alert">{state.error}</p>}
      <button disabled={pending}>{pending ? "Publishing…" : "Publish"}</button>
    </form>
  );
}
```

**Security rules for Server Actions** — every action is effectively a **public POST endpoint**:
1. **Authenticate and authorize inside every action** (don't rely on the page or middleware having checked).
2. **Validate all input** (Zod) — the client can send anything, including extra fields.
3. **Never trust client-provided IDs for ownership** (`authorId`, `userId`, `price`) — derive from the session/DB.
4. Return **minimal data** (no full DB rows with secrets).
5. **Rate limit** sensitive actions (login, signup, OTP).
6. Next.js adds protections (unguessable action IDs, Origin checks, encryption of closed-over values) — they don't replace your checks.

### 6. Route Handlers (API endpoints)

```ts
// app/api/products/route.ts
import { NextRequest, NextResponse } from "next/server";

export async function GET(req: NextRequest) {
  const q = req.nextUrl.searchParams.get("q") ?? "";
  const products = await searchProducts(q);
  return NextResponse.json(products, { headers: { "Cache-Control": "public, s-maxage=60" } });
}

export async function POST(req: NextRequest) {
  const session = await auth();
  if (!session) return NextResponse.json({ error: "Unauthorized" }, { status: 401 });
  const body = ProductSchema.safeParse(await req.json());
  if (!body.success) return NextResponse.json({ error: body.error.flatten() }, { status: 400 });
  const product = await createProduct(body.data);
  return NextResponse.json(product, { status: 201 });
}

// app/api/webhooks/stripe/route.ts — raw body for signature verification
export async function POST(req: NextRequest) {
  const raw = await req.text();
  const event = stripe.webhooks.constructEvent(raw, req.headers.get("stripe-signature")!, process.env.STRIPE_WEBHOOK_SECRET!);
  // ...
  return NextResponse.json({ received: true });
}
```

Use route handlers for: webhooks, public APIs for other clients (mobile), file downloads, OAuth callbacks. For your own UI's mutations, Server Actions are usually simpler.

### 7. Middleware (renamed `proxy.ts` in Next.js 16)

Runs **before** a request reaches a route — for redirects, rewrites, headers, i18n, A/B tests, lightweight auth gating.

```ts
// middleware.ts (or proxy.ts in v16+)
import { NextResponse, type NextRequest } from "next/server";

export function middleware(req: NextRequest) {
  const session = req.cookies.get("session")?.value;
  if (!session && req.nextUrl.pathname.startsWith("/dashboard")) {
    const url = new URL("/login", req.url);
    url.searchParams.set("next", req.nextUrl.pathname);
    return NextResponse.redirect(url);
  }
  const res = NextResponse.next();
  res.headers.set("X-Frame-Options", "DENY");
  return res;
}

export const config = { matcher: ["/dashboard/:path*", "/account/:path*"] };
```

- Keep it **fast and light** (runs on every matched request); no heavy DB work.
- **Never rely on middleware as your only auth check** — a 2025 vulnerability (CVE-2025-29927) allowed bypassing Next.js middleware with a crafted header. Always check auth again in the **data layer / server actions / route handlers**.

### 8. Auth pattern: a Data Access Layer (DAL)

Centralize "who is the user and what can they see" in server-only functions that every page, action and route calls.

```ts
// lib/dal.ts
import "server-only";
import { cache } from "react";
import { cookies } from "next/headers";
import { redirect } from "next/navigation";

export const verifySession = cache(async () => {
  const token = (await cookies()).get("session")?.value;
  const session = token ? await decryptSession(token) : null;
  if (!session?.userId) redirect("/login");
  return session;                                          // cached for the rest of this request
});

export async function getMyOrders() {
  const { userId } = await verifySession();
  return db.order.findMany({
    where: { userId },                                     // ownership enforced in the query
    select: { id: true, total: true, status: true, createdAt: true },   // DTO: only safe fields
  });
}
```

Libraries: **Auth.js (NextAuth)**, **better-auth**, **Clerk**, **Supabase Auth**, **Lucia-style** custom sessions.

### 9. Built-in optimizations

```tsx
import Image from "next/image";
import Link from "next/link";
import Script from "next/script";
import { Inter } from "next/font/google";

const inter = Inter({ subsets: ["latin"], display: "swap" });  // self-hosted, no layout shift

<Image src="/hero.jpg" alt="Hero" width={1200} height={600} priority sizes="100vw" />  // resizing, WebP/AVIF, lazy by default
<Link href="/products" prefetch>Products</Link>                 // client navigation + prefetch
<Script src="https://analytics.example.com/a.js" strategy="afterInteractive" />   // or lazyOnload / worker
```

### 10. SEO & metadata

```tsx
// Static
export const metadata = { title: "Shop", description: "Best products" };

// Dynamic
export async function generateMetadata({ params }: { params: Promise<{ slug: string }> }) {
  const { slug } = await params;
  const post = await getPost(slug);
  return {
    title: post.title,
    description: post.excerpt,
    openGraph: { images: [post.coverUrl] },
    alternates: { canonical: `https://shop.com/blog/${slug}` },
  };
}

// app/sitemap.ts
export default async function sitemap() {
  const posts = await getPosts();
  return posts.map((p) => ({ url: `https://shop.com/blog/${p.slug}`, lastModified: p.updatedAt }));
}

// Pre-render dynamic routes at build time
export async function generateStaticParams() {
  return (await getPosts()).map((p) => ({ slug: p.slug }));
}
```

### 11. Errors, not found & redirects

```tsx
// app/dashboard/error.tsx — must be a client component
"use client";
export default function Error({ error, reset }: { error: Error & { digest?: string }; reset: () => void }) {
  return (
    <div role="alert">
      <p>Something went wrong.</p>
      <button onClick={reset}>Try again</button>
    </div>
  );
}

// In a server component
import { notFound, redirect } from "next/navigation";
const post = await getPost(slug);
if (!post) notFound();                 // renders not-found.tsx with 404
if (post.movedTo) redirect(`/blog/${post.movedTo}`);
```

Production error messages from server components are hidden from the client (only a `digest` ID) — log details on the server.

### 12. Deployment

- **Vercel**: zero-config (ISR, image optimization, edge middleware).
- **Self-hosting**: `output: "standalone"` in `next.config` → small Node server for Docker; configure a shared cache handler if running multiple instances (ISR/data cache must be shared), put a CDN in front.
- Static export (`output: "export"`) for pure static sites (no server features).

### 13. Common Next.js pitfalls

| Pitfall | Fix |
|---|---|
| `"use client"` at the top of pages → everything ships as JS | Push it down to interactive leaves |
| Data waterfalls in server components | `Promise.all`, Suspense boundaries, preload patterns |
| Secrets leaking via `NEXT_PUBLIC_` or passing full DB objects to client components | Server-only env vars, DTOs, `server-only` |
| Relying on middleware for auth | Check auth in DAL/actions/route handlers too |
| Stale data after a mutation | `revalidatePath`/`revalidateTag` (or `updateTag`) after writes |
| Accidentally dynamic pages (reading cookies in the root layout) | Isolate dynamic parts behind Suspense / specific segments |
| Hydration mismatch (`Date.now()`, `window` in render) | Client-only effects, `suppressHydrationWarning` for timestamps |
| Huge client bundles from big libraries in client components | Keep heavy libs server-side or `dynamic(() => import(...))` |

---

### Animations in React

**Order of preference**: CSS transitions/animations → Web Animations API → an animation library (**Motion**, formerly Framer Motion) for complex UI (exit animations, layout animations, gestures, orchestration).

#### CSS first

```tsx
function Drawer({ open, children }: { open: boolean; children: React.ReactNode }) {
  return <aside className={`drawer ${open ? "drawer--open" : ""}`} aria-hidden={!open}>{children}</aside>;
}
```

```css
.drawer { transform: translateX(-100%); transition: transform 250ms ease; }
.drawer--open { transform: translateX(0); }

@media (prefers-reduced-motion: reduce) {
  .drawer { transition: none; }       /* respect users who get motion sickness */
}
```

#### Motion (Framer Motion)

```tsx
"use client";
import { motion, AnimatePresence } from "motion/react";

// 1. Enter / exit animations (CSS can't animate unmounting elements easily)
function Toasts({ toasts }: { toasts: { id: string; text: string }[] }) {
  return (
    <ul>
      <AnimatePresence initial={false}>
        {toasts.map((t) => (
          <motion.li
            key={t.id}
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            exit={{ opacity: 0, x: 100 }}
            transition={{ duration: 0.2 }}
            layout                                  // smoothly move siblings when one is removed
          >
            {t.text}
          </motion.li>
        ))}
      </AnimatePresence>
    </ul>
  );
}

// 2. Gestures
<motion.button whileHover={{ scale: 1.05 }} whileTap={{ scale: 0.95 }}>Buy</motion.button>

// 3. Shared layout animation (e.g. active tab underline sliding between tabs)
{tabs.map((tab) => (
  <button key={tab} onClick={() => setActive(tab)}>
    {tab}
    {active === tab && <motion.div layoutId="underline" className="underline" />}
  </button>
))}

// 4. Respect reduced motion
import { useReducedMotion } from "motion/react";
const reduce = useReducedMotion();
<motion.div animate={{ x: reduce ? 0 : 100 }} />
```

Other options: **React Spring** (physics-based), **GSAP** (timelines, complex sequences), **Lottie** (designer-made animations), **auto-animate** (one-line list animations), and the **View Transitions API** (browser-native page/state transitions; React has experimental `<ViewTransition>` support).

#### Animation best practices

- Animate **`transform` and `opacity`** only (see Browser Internals in the JS notes); avoid animating `width/height/top/left`.
- Keep UI animations short: **150–300 ms**; use easing (ease-out for entering, ease-in for leaving).
- Always support **`prefers-reduced-motion`**.
- Don't block interaction on animations; don't animate on every keystroke/scroll without throttling.
- Lazy-load heavy animation libraries; prefer CSS for simple hover/focus states.

### Interview Qs

1. Explain App Router file conventions: layout vs template vs page vs loading vs error.
2. What are route groups, parallel routes and intercepting routes used for?
3. Server vs Client Components — rules for passing props and composing them?
4. How do you avoid data waterfalls and stream slow parts of a page?
5. Explain Next.js caching layers. What makes a route dynamic?
6. `revalidatePath` vs `revalidateTag`? Time-based vs on-demand revalidation?
7. What are Server Actions? How do you secure them?
8. Server Actions vs Route Handlers — when to use which?
9. What is middleware (proxy) for? Why shouldn't it be your only auth check?
10. What is a Data Access Layer and why use `server-only` and `React.cache`?
11. How does `next/image` improve performance?
12. How do you do exit animations in React? → `AnimatePresence` (Motion).
13. Which CSS properties should you animate and why? How do you support reduced motion?

---

## 45. Testing React

### Tools

- **Vitest / Jest** — test runner & assertions.
- **React Testing Library (RTL)** — test components the way users use them (by role/label/text, not implementation details).
- **user-event** — realistic user interactions.
- **MSW** (Mock Service Worker) — mock network requests.
- **Playwright / Cypress** — end-to-end tests.

### Example 1 — counter

```jsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import Counter from "./Counter";

test("increments count", async () => {
  const user = userEvent.setup();
  render(<Counter />);
  expect(screen.getByText("0")).toBeInTheDocument();
  await user.click(screen.getByRole("button", { name: "+" }));
  expect(screen.getByText("1")).toBeInTheDocument();
});
```

### Example 2 — async data

```jsx
test("shows users after loading", async () => {
  vi.spyOn(global, "fetch").mockResolvedValue({ ok: true, json: async () => [{ id: 1, name: "Rohit" }] });
  render(<Users />);
  expect(screen.getByText(/loading/i)).toBeInTheDocument();
  expect(await screen.findByText("Rohit")).toBeInTheDocument(); // findBy waits
});
```

### Example 3 — form & callback

```jsx
test("submits the form", async () => {
  const onSubmit = vi.fn();
  const user = userEvent.setup();
  render(<LoginForm onSubmit={onSubmit} />);
  await user.type(screen.getByLabelText(/email/i), "a@b.com");
  await user.type(screen.getByLabelText(/password/i), "secret1");
  await user.click(screen.getByRole("button", { name: /login/i }));
  expect(onSubmit).toHaveBeenCalledWith({ email: "a@b.com", password: "secret1" });
});
```

### Query priority

`getByRole` > `getByLabelText` > `getByPlaceholderText` > `getByText` > `getByDisplayValue` > `getByAltText` > `getByTitle` > `getByTestId`.

- `getBy*` — throws if not found (sync).
- `queryBy*` — returns null (to assert absence).
- `findBy*` — returns a promise (async appearance).

### Testing hooks

```jsx
import { renderHook, act } from "@testing-library/react";
test("useCounter", () => {
  const { result } = renderHook(() => useCounter());
  act(() => result.current.increment());
  expect(result.current.count).toBe(1);
});
```

---

## 46. Testing React in Depth: Providers, MSW, Async UI, Router, Query & Playwright

Builds on "Testing React". Goal: tests that behave like a user, run fast, and don't break when you refactor internals.

### 1. Project setup (Vitest + Testing Library + MSW)

```js
// vitest.config.js
import { defineConfig } from "vitest/config";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react()],
  test: {
    environment: "jsdom",                 // browser-like DOM
    setupFiles: ["./src/test/setup.js"],
    restoreMocks: true,                   // vi.spyOn/mocks reset between tests
    css: false,
  },
});
```

```js
// src/test/setup.js
import "@testing-library/jest-dom/vitest";   // toBeInTheDocument, toHaveTextContent, toBeDisabled…
import { afterAll, afterEach, beforeAll } from "vitest";
import { cleanup } from "@testing-library/react";
import { server } from "./server";

beforeAll(() => server.listen({ onUnhandledRequest: "error" }));   // fail on any request you didn't mock
afterEach(() => { server.resetHandlers(); cleanup(); });           // undo per-test overrides
afterAll(() => server.close());
```

### 2. Mock the network with MSW (not `fetch` mocks)

MSW intercepts requests at the network level, so your real API client, TanStack Query config and error handling all run in tests. The same handlers can power Storybook and local dev.

```js
// src/test/handlers.js
import { http, HttpResponse, delay } from "msw";

export const db = { products: [{ id: 1, name: "Phone", price: 20000 }, { id: 2, name: "Case", price: 500 }] };

export const handlers = [
  http.get("/api/products", ({ request }) => {
    const q = new URL(request.url).searchParams.get("q")?.toLowerCase() ?? "";
    return HttpResponse.json(db.products.filter((p) => p.name.toLowerCase().includes(q)));
  }),
  http.post("/api/products", async ({ request }) => {
    const body = await request.json();
    if (!body.name) return HttpResponse.json({ error: { message: "Name is required" } }, { status: 400 });
    return HttpResponse.json({ id: 3, ...body }, { status: 201 });
  }),
];

// src/test/server.js
import { setupServer } from "msw/node";
export const server = setupServer(...handlers);
```

Per-test overrides for edge cases:

```js
import { http, HttpResponse, delay } from "msw";
import { server } from "../test/server";

server.use(http.get("/api/products", () => HttpResponse.json([])));                          // empty state
server.use(http.get("/api/products", () => new HttpResponse(null, { status: 500 })));        // server error
server.use(http.get("/api/products", () => HttpResponse.error()));                           // network failure
server.use(http.get("/api/products", async () => { await delay(2000); return HttpResponse.json([]); }));   // slow
```

### 3. A custom render with all providers

Components rarely render alone — they need a router, a QueryClient, auth, theme… Wrap them **the same way the app does**, with a **fresh QueryClient per test** (no cache leaking between tests).

```jsx
// src/test/utils.jsx
import { vi } from "vitest";                      // needed unless test.globals is enabled
import { render } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import { MemoryRouter, Routes, Route } from "react-router-dom";
import { AuthContext } from "../auth/AuthProvider";

export function renderWithProviders(ui, { route = "/", path = "*", user = { id: 1, name: "Rohit", role: "user" } } = {}) {
  const queryClient = new QueryClient({
    defaultOptions: { queries: { retry: false, gcTime: Infinity }, mutations: { retry: false } },   // fail fast in tests
  });
  const auth = { user, login: vi.fn(), logout: vi.fn(), isPending: false };

  const result = render(
    <QueryClientProvider client={queryClient}>
      <AuthContext.Provider value={auth}>
        <MemoryRouter initialEntries={[route]}>
          <Routes>
            <Route path={path} element={ui} />
            <Route path="/login" element={<h1>Login page</h1>} />
          </Routes>
        </MemoryRouter>
      </AuthContext.Provider>
    </QueryClientProvider>
  );
  return { ...result, user: userEvent.setup(), queryClient, auth };
}

export * from "@testing-library/react";
```

### 4. Testing async UI: loading → data / empty / error

```jsx
import { describe, it, expect } from "vitest";
import { http, HttpResponse } from "msw";
import { server } from "../test/server";
import { renderWithProviders, screen, waitForElementToBeRemoved } from "../test/utils";
import { ProductList } from "./ProductList";

describe("ProductList", () => {
  it("shows products after loading", async () => {
    renderWithProviders(<ProductList />);
    expect(screen.getByRole("status", { name: /loading/i })).toBeInTheDocument();
    expect(await screen.findByRole("listitem", { name: /phone/i })).toBeInTheDocument();    // findBy waits
    expect(screen.getAllByRole("listitem")).toHaveLength(2);
  });

  it("shows an empty state", async () => {
    server.use(http.get("/api/products", () => HttpResponse.json([])));
    renderWithProviders(<ProductList />);
    expect(await screen.findByText(/no products yet/i)).toBeInTheDocument();
  });

  it("shows an error with a retry button that works", async () => {
    server.use(http.get("/api/products", () => new HttpResponse(null, { status: 500 })));
    const { user } = renderWithProviders(<ProductList />);
    expect(await screen.findByRole("alert")).toHaveTextContent(/something went wrong/i);

    server.resetHandlers();                                          // the next request succeeds
    await user.click(screen.getByRole("button", { name: /try again/i }));
    await waitForElementToBeRemoved(() => screen.queryByRole("alert"));
    expect(screen.getAllByRole("listitem")).toHaveLength(2);
  });
});
```

**Query cheat sheet**: `getBy*` (must exist now), `queryBy*` (assert absence → `null`), `findBy*` (async, waits up to 1s). Prefer `findBy` over `waitFor(() => getBy…)`; never `setTimeout`/sleep in tests.

### 5. Forms: typing, validation, submitted payload, pending state

```jsx
it("validates, submits the right payload, and disables the button while saving", async () => {
  let received;
  server.use(http.post("/api/products", async ({ request }) => {
    received = await request.json();                                 // assert what the UI actually sent
    return HttpResponse.json({ id: 3, ...received }, { status: 201 });
  }));
  const { user } = renderWithProviders(<NewProductForm />);

  await user.click(screen.getByRole("button", { name: /save/i }));
  expect(await screen.findByText(/name is required/i)).toBeInTheDocument();   // client validation

  await user.type(screen.getByLabelText(/name/i), "Charger");
  await user.clear(screen.getByLabelText(/price/i));
  await user.type(screen.getByLabelText(/price/i), "999");
  await user.selectOptions(screen.getByLabelText(/category/i), "accessories");
  await user.click(screen.getByRole("button", { name: /save/i }));

  expect(screen.getByRole("button", { name: /saving/i })).toBeDisabled();       // pending state
  expect(await screen.findByRole("status")).toHaveTextContent(/product created/i);
  expect(received).toEqual({ name: "Charger", price: 999, category: "accessories" });
});

it("uploads a file", async () => {
  const { user } = renderWithProviders(<AvatarUploader />);
  const file = new File(["png-bytes"], "me.png", { type: "image/png" });
  await user.upload(screen.getByLabelText(/choose or drop an image/i), file);
  expect(screen.getByRole("img", { name: /preview/i })).toBeInTheDocument();
});
```

### 6. Routing & protected routes

```jsx
it("redirects anonymous users to /login", () => {
  renderWithProviders(<RequireAuth><Dashboard /></RequireAuth>, { route: "/dashboard", user: null });
  expect(screen.getByRole("heading", { name: /login page/i })).toBeInTheDocument();
});

it("reads the :id route param", async () => {
  renderWithProviders(<ProductPage />, { route: "/products/1", path: "/products/:id" });
  expect(await screen.findByRole("heading", { name: "Phone" })).toBeInTheDocument();
});
```

### 7. Debounced search with fake timers

```jsx
import { vi, afterEach } from "vitest";
import userEvent from "@testing-library/user-event";
afterEach(() => vi.useRealTimers());

it("searches only after the user stops typing", async () => {
  vi.useFakeTimers({ shouldAdvanceTime: true });
  const requests = [];
  server.use(http.get("/api/products", ({ request }) => {
    requests.push(new URL(request.url).searchParams.get("q"));
    return HttpResponse.json([]);
  }));
  renderWithProviders(<ProductSearch />);
  const user = userEvent.setup({ advanceTimers: vi.advanceTimersByTime });   // user-event's own delays follow the fake clock

  await user.type(screen.getByRole("searchbox"), "phone");
  expect(requests).toEqual([]);                                         // nothing yet — still debouncing
  await vi.advanceTimersByTimeAsync(400);
  await screen.findByText(/no results/i);
  expect(requests).toEqual(["phone"]);                                  // exactly one request with the final text
});
```

With fake timers, always create user-event with `advanceTimers` (as above); otherwise its internal delays wait on real time and the test can hang.

### 8. Hooks, context & reducers

```jsx
import { renderHook, act } from "@testing-library/react";

it("useCart adds items and computes the total", () => {
  const wrapper = ({ children }) => <CartProvider>{children}</CartProvider>;   // hooks that need context
  const { result } = renderHook(() => useCart(), { wrapper });
  act(() => result.current.add({ id: 1, price: 500 }));
  act(() => result.current.add({ id: 1, price: 500 }));
  expect(result.current.items).toEqual([{ id: 1, price: 500, qty: 2 }]);
  expect(result.current.total).toBe(1000);
});

// Reducers and pure helpers need no React at all — test them directly (fastest tests you'll have)
it("cartReducer removes an item", () => {
  expect(cartReducer([{ id: 1, qty: 1 }], { type: "remove", id: 1 })).toEqual([]);
});
```

### 9. Accessibility checks in tests

```jsx
import { axe } from "vitest-axe";          // or jest-axe

it("has no detectable a11y violations", async () => {
  const { container } = renderWithProviders(<CheckoutForm />);
  expect(await axe(container)).toHaveNoViolations();
});
```

Querying by **role + accessible name** (`getByRole("button", { name: /save/i })`) already tests that controls are labelled; axe catches missing labels, bad ARIA, duplicate IDs, and some contrast issues (jsdom can't check everything — combine with manual keyboard and screen-reader testing).

### 10. What not to test

- Implementation details: state variable names, internal functions, which hook was called, CSS class names.
- Third-party libraries themselves (React Router, TanStack Query) — test **your** usage.
- Huge snapshots of component trees (they get rubber-stamped).
- Exact loading spinners timing — test that the final state appears.

### 11. End-to-end tests with Playwright

E2E tests run the **real app in real browsers** (Chromium, Firefox, WebKit) — few of them, covering the most important journeys.

```js
// playwright.config.js
import { defineConfig, devices } from "@playwright/test";

export default defineConfig({
  testDir: "./e2e",
  fullyParallel: true,
  retries: process.env.CI ? 2 : 0,
  reporter: [["html"], ["list"]],
  use: {
    baseURL: "http://localhost:5173",
    trace: "on-first-retry",               // time-travel trace for failed tests
    screenshot: "only-on-failure",
  },
  projects: [
    { name: "setup", testMatch: /auth\.setup\.js/ },
    { name: "chromium", use: { ...devices["Desktop Chrome"], storageState: "e2e/.auth/user.json" }, dependencies: ["setup"] },
    { name: "mobile", use: { ...devices["Pixel 7"], storageState: "e2e/.auth/user.json" }, dependencies: ["setup"] },
  ],
  webServer: { command: "npm run dev", url: "http://localhost:5173", reuseExistingServer: !process.env.CI },
});
```

```js
// e2e/auth.setup.js — log in once, reuse the session in every test (fast)
import { test as setup, expect } from "@playwright/test";

setup("authenticate", async ({ page }) => {
  await page.goto("/login");
  await page.getByLabel("Email").fill(process.env.E2E_EMAIL);
  await page.getByLabel("Password").fill(process.env.E2E_PASSWORD);
  await page.getByRole("button", { name: "Log in" }).click();
  await expect(page.getByRole("heading", { name: /dashboard/i })).toBeVisible();
  await page.context().storageState({ path: "e2e/.auth/user.json" });
});
```

```js
// e2e/checkout.spec.js
import { test, expect } from "@playwright/test";

test("user can buy a product", async ({ page }) => {
  await page.goto("/products");
  await page.getByRole("searchbox", { name: /search/i }).fill("phone");
  await page.getByRole("link", { name: /phone/i }).first().click();
  await page.getByRole("button", { name: /add to cart/i }).click();
  await expect(page.getByRole("link", { name: /cart \(1\)/i })).toBeVisible();   // auto-waits, no sleeps

  await page.getByRole("link", { name: /cart/i }).click();
  await page.getByRole("button", { name: /checkout/i }).click();
  await expect(page).toHaveURL(/\/checkout/);
  await expect(page.getByText(/order summary/i)).toBeVisible();
});

test("shows a friendly error when the API is down", async ({ page }) => {
  await page.route("**/api/products*", (route) => route.fulfill({ status: 500, body: "" }));   // mock one endpoint
  await page.goto("/products");
  await expect(page.getByRole("alert")).toContainText(/something went wrong/i);
});
```

```bash
npx playwright test                 # headless, all browsers/projects
npx playwright test --ui            # interactive runner
npx playwright codegen localhost:5173   # record actions into test code
npx playwright show-report          # HTML report with traces
```

Playwright tips: use **role/label locators** (not CSS/XPath), rely on **auto-waiting assertions** (`toBeVisible`, `toHaveURL`), seed test data via API calls in fixtures (not through the UI), isolate tests (each gets a fresh browser context), run against a production-like build in CI, and use the **trace viewer** to debug failures.

### 12. Which kind of test for what

| Test | Examples | Tool |
|---|---|---|
| Unit | Reducers, formatters, validation schemas, hooks without UI | Vitest |
| Integration (most) | A page/feature with providers + MSW: loading/error/empty, forms, routing | Vitest + Testing Library + MSW |
| Accessibility | Automated rule checks on key screens | vitest-axe + manual checks |
| Visual regression | Components/pages look unchanged | Storybook + Chromatic, or Playwright screenshots |
| E2E | Login, signup, checkout, payment — critical journeys across the real stack | Playwright |

### Interview Qs

1. Why use MSW instead of mocking `fetch` or your API module?
2. How do you test a component that needs Router, TanStack Query and auth context?
3. Why create a new QueryClient per test and disable retries?
4. `getBy` vs `queryBy` vs `findBy`? When do you use `waitFor`?
5. How do you test a debounced search?
6. How do you verify the payload a form submitted?
7. What shouldn't you test in React components?
8. How do Playwright tests stay fast and non-flaky? (storageState, auto-waiting, API seeding, isolation)
9. Where would you use E2E vs integration tests?

---

## 47. Accessibility (a11y)

Accessibility means people can use your app however they operate a computer: with a screen reader (blind and low-vision users), only a keyboard (motor impairments, power users), zoom or high contrast, voice control, or with a temporary limitation such as a broken arm or bright sunlight. It's also a legal requirement in many places: US ADA lawsuits, the European Accessibility Act (enforced from June 2025) and India's RPwD Act 2016 all point to **WCAG** (Web Content Accessibility Guidelines). The usual target is **WCAG 2.2 level AA**.

WCAG is organised around four principles (**POUR**): content must be **P**erceivable, **O**perable, **U**nderstandable and **R**obust. In practice, most of it comes down to the rules in this section.

### 1. Semantic HTML first

The first rule of ARIA is **don't use ARIA if a native element does the job**. Native elements come with a role, a name, keyboard support, focus handling and states for free.

| You need | Use | Not |
|---|---|---|
| An action | `<button type="button">` | `<div onClick>`, `<a href="#" onClick>` |
| Navigation to a URL | `<a href="/pricing">` | `<button onClick={() => navigate(...)}>` |
| Page regions | `<header>`, `<nav>`, `<main>`, `<aside>`, `<footer>` | `<div className="nav">` |
| A heading structure | `<h1>`–`<h6>` in order (one `<h1>` per page) | Bold `<div>`s, or skipping levels for styling |
| A list of things | `<ul>`/`<ol>` + `<li>` | Stacked `<div>`s |
| Tabular data | `<table>` with `<th scope>` | A CSS grid of `<div>`s |
| Grouped radios or checkboxes | `<fieldset>` + `<legend>` | A `<div>` with a heading |
| Show/hide section | `<details>` + `<summary>` | A custom toggle (unless you need custom behaviour) |
| A modal | `<dialog>` + `showModal()` | A `<div>` overlay with `z-index` |

What a `<div onClick>` costs you. To match one `<button>`, you'd need all of this, and it still isn't a real button (it doesn't submit forms and ignores `disabled`):

```jsx
// ❌ Not focusable, no role, no keyboard support: invisible to keyboard and screen-reader users
function BadSave({ onSave }) {
  return <div className="btn" onClick={onSave}>Save</div>;
}

// ❌ "Fixed": role, tabIndex, and Enter/Space handling (Space fires on keyup for real buttons)
function StillBadSave({ onSave }) {
  return (
    <div className="btn" role="button" tabIndex={0} onClick={onSave}
      onKeyDown={(e) => { if (e.key === "Enter") onSave(); if (e.key === " ") e.preventDefault(); }}
      onKeyUp={(e) => { if (e.key === " ") onSave(); }}>
      Save
    </div>
  );
}

// ✅ All of the above, for free
function GoodSave({ onSave }) {
  return <button type="button" className="btn" onClick={onSave}>Save</button>;
}
```

A **skip link** lets keyboard users jump past the navigation (WCAG 2.4.1 "Bypass Blocks"):

```jsx
function Layout({ children }) {
  return (
    <>
      <a href="#main" className="skip-link">Skip to main content</a>
      <header>{/* logo, nav … */}</header>
      <main id="main" tabIndex={-1}>{children}</main>
    </>
  );
}
```

```css
.skip-link { position: absolute; left: 1rem; top: 1rem; transform: translateY(-200%); }
.skip-link:focus { transform: translateY(0); }   /* visible only when focused */
```

### 2. Accessible names and descriptions

Every interactive element needs an **accessible name**: what a screen reader announces ("Save, button"). Browsers compute it in this order:

1. `aria-labelledby` (references other elements' text)
2. `aria-label`
3. Native labelling: `<label>`, the element's text content, `alt`, `<legend>`, `<caption>`
4. `title` (last resort; not reliably announced, and invisible to touch users)

```jsx
// Icon-only buttons need a name. Hide the decorative icon from screen readers
function IconButton({ label, icon, ...props }) {
  return (
    <button type="button" aria-label={label} {...props}>
      <span aria-hidden="true">{icon}</span>
    </button>
  );
}

// Or keep the text in the DOM but hide it visually (it's also translated by browser translation tools)
function CartButton({ count }) {
  return (
    <button type="button">
      <span aria-hidden="true">🛒 {count}</span>
      <span className="sr-only">Cart, {count} items</span>
    </button>
  );
}
```

```css
/* Visually hidden, still read by screen readers */
.sr-only {
  position: absolute; width: 1px; height: 1px; padding: 0; margin: -1px;
  overflow: hidden; clip: rect(0, 0, 0, 0); white-space: nowrap; border: 0;
}
```

Rules:

- **Placeholders are not labels.** They vanish when the user types, often have low contrast, and are unreliable as names. Use `<label>`.
- `aria-label` on a plain `<div>` or `<span>` with no role is **ignored**. Names belong on interactive elements, landmarks and images.
- **Descriptions** (`aria-describedby`) add secondary info read after the name: hints, error messages, "opens in a new tab".
- **Image `alt` text:** describe the *purpose*, not the pixels. Use `alt=""` for decorative images; an image inside a link describes the destination (`alt="Home"`, not `alt="logo.png"`). Never write "image of…".
- **Link text must make sense on its own.** Screen-reader users often navigate a list of links, where five "Read more" links are useless. Write "Read more about pricing", or add `sr-only` context.

### 3. Keyboard and focus

Everything you can do with a mouse must work with a keyboard (WCAG 2.1.1), and focus must never get stuck (2.1.2).

- **Tab order follows DOM order.** Fix the order in the markup, not with CSS or positive `tabIndex`.
- `tabIndex={0}` puts a custom element into the Tab order. `tabIndex={-1}` makes it focusable from code (`el.focus()`) but not with Tab. **Never use a positive `tabIndex`.**
- **Focus must be visible** (2.4.7) and not hidden behind sticky headers or cookie banners (2.4.11, new in WCAG 2.2).
- **Hit targets** should be at least 24×24 CSS pixels (2.5.8, new in 2.2). Browser-default buttons and inputs are only about **21px tall**, so an unstyled form fails this check. Set a minimum size (44×44 is the comfortable touch size).
- **Don't block paste** in password or code fields; password managers depend on it (3.3.8, new in 2.2).

```css
/* Show a clear focus ring for keyboard users; :focus-visible hides it for mouse clicks */
:focus-visible { outline: 3px solid #1a56db; outline-offset: 2px; }
/* ❌ Never remove it without a replacement:  *:focus { outline: none; } */

/* WCAG 2.5.8 target size: browser-default controls are ~21px tall */
button, input, select, [role="tab"], [role="menuitem"], [role="option"] { min-height: 24px; min-width: 24px; }

/* Keep focused elements from hiding under a sticky header */
html { scroll-padding-top: 5rem; }

/* Respect users who get motion sickness from animation */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important; animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important; scroll-behavior: auto !important;
  }
}
```

**Focus management in a single-page app.** When you change the page without a reload, the browser doesn't move focus or announce anything, and a screen-reader user is left where the old page's link used to be. Move focus to the new page's heading:

```jsx
import { useEffect, useRef } from "react";

// Focus the page heading whenever `key` changes (e.g. the route's pathname), but not on the first load
export function useFocusOnChange(key) {
  const ref = useRef(null);
  const previousKey = useRef(key);
  useEffect(() => {
    if (previousKey.current === key) return;       // first render (StrictMode runs this effect twice)
    previousKey.current = key;
    ref.current?.focus();
  }, [key]);
  return ref;
}

export function Page({ pathname, title, children }) {
  const headingRef = useFocusOnChange(pathname);
  return (
    <main>
      <h1 ref={headingRef} tabIndex={-1}>{title}</h1>
      {children}
    </main>
  );
}
```

Comparing with the previous key is deliberate. The common `isFirstRender` ref version (`if (isFirst.current) { isFirst.current = false; return; }`) **steals focus on the first load in development**, because StrictMode runs effects twice and the second run sees `isFirst` already set to `false`. Also update `document.title` on every route change; it's the first thing a screen reader announces in a new tab or window.

**Focus after destructive actions.** When the focused element disappears (you delete a row, or close a toast), focus falls back to `<body>` and keyboard users lose their place. Move focus to the next item, the previous item, or the list's heading.

**Two ways to handle arrow-key navigation inside a composite widget:**

| Technique | How | Used by |
|---|---|---|
| **Roving tabindex** | The current item has `tabIndex={0}`, the rest `-1`; arrow keys move real DOM focus | Tabs, toolbars, menus, radio groups, grids |
| **`aria-activedescendant`** | DOM focus stays on one element (the input); `aria-activedescendant` points at the "virtually focused" option's `id` | Comboboxes and listboxes, where the user keeps typing |

Either way, Tab moves **into** the widget once and **out** of it on the next press. Arrow keys move **within** it.

### 4. Modal dialogs

A modal must: be labelled (`aria-labelledby` pointing at its title); move focus inside when it opens; keep Tab inside; close on Escape; make the page behind it inert; and **return focus to the button that opened it** when it closes.

The native `<dialog>` element opened with `showModal()` does almost all of this for you. It renders in the top layer, makes the rest of the page inert, closes on Escape, focuses the first focusable element (or the one with the HTML `autofocus` attribute; see the React caveat below), and restores focus to the opener when it closes.

```jsx
import { useEffect, useId, useRef } from "react";

export function Modal({ open, onClose, title, children }) {
  const ref = useRef(null);
  const titleId = useId();

  useEffect(() => {
    const dialog = ref.current;
    if (open && !dialog.open) {
      dialog.showModal();                                  // showModal(), NOT the `open` attribute
      dialog.querySelector("[data-autofocus]")?.focus();   // optional initial focus (see pitfalls)
    }
    if (!open && dialog.open) dialog.close();
  }, [open]);

  return (
    <dialog
      ref={ref}
      aria-labelledby={titleId}
      onClose={onClose}                                              // fires on Escape and on close()
      onClick={(e) => { if (e.target === e.currentTarget) onClose(); }}   // backdrop click (see CSS)
      className="modal"
    >
      <div className="modal-body">
        <h2 id={titleId}>{title}</h2>
        {children}
        <button type="button" onClick={onClose}>Close</button>
      </div>
    </dialog>
  );
}
```

```css
/* Padding lives on the inner div, so a click on the dialog element itself can only be the backdrop */
.modal { padding: 0; border: none; border-radius: 12px; }
.modal-body { padding: 1.5rem; }
.modal::backdrop { background: rgb(0 0 0 / 0.5); }
body:has(dialog[open]) { overflow: hidden; }       /* stop the page scrolling behind the modal */
```

**Pitfalls:**

- ❌ `<dialog open>` (the attribute, or `dialog.show()`) opens a **non-modal** dialog: no inert background, no focus trap, and Escape doesn't close it. Use `showModal()`.
- ❌ Rendering the dialog conditionally (`{open && <dialog …>}`) with the `open` attribute is the same non-modal dialog. Keep it mounted and call `showModal()`/`close()`.
- ✅ For a **destructive confirmation** ("Delete project?"), focus the **safe** choice (Cancel), not Delete. React's `autoFocus` prop **doesn't work** here. React doesn't render the `autofocus` attribute; it calls `.focus()` when the element mounts, and at that moment the dialog is still closed. `showModal()` then just focuses the first focusable element. Mark the button with `data-autofocus` (handled in the effect above), or put the safe button first.
- A custom `<div role="dialog" aria-modal="true">` needs a hand-written focus trap, the `inert` attribute on the rest of the app (`<div id="app" inert>`), Escape handling and focus restoration. Use a tested library (React Aria, Radix) if you can't use `<dialog>`.

### 5. Tabs (roving tabindex)

The ARIA Authoring Practices Guide (**APG**) describes the expected keyboard behaviour for every widget. For tabs:

- Tab moves focus to the selected tab, and the next Tab moves into the panel.
- ← and → move between tabs (wrapping around); Home and End jump to the first and last.
- Here, arrows also select the tab ("automatic activation"). If panels are slow to load, select on Enter or Space instead.

```jsx
import { useId, useRef, useState } from "react";

export function Tabs({ label, tabs }) {                 // tabs: [{ id, title, content }]
  const [selected, setSelected] = useState(0);
  const tabRefs = useRef([]);
  const baseId = useId();

  const select = (index) => {
    const next = (index + tabs.length) % tabs.length;   // wrap around
    setSelected(next);
    tabRefs.current[next].focus();
  };

  const onKeyDown = (e) => {
    const target = { ArrowRight: selected + 1, ArrowLeft: selected - 1, Home: 0, End: tabs.length - 1 }[e.key];
    if (target === undefined) return;
    e.preventDefault();
    select(target);
  };

  return (
    <div>
      <div role="tablist" aria-label={label} onKeyDown={onKeyDown}>
        {tabs.map((tab, i) => (
          <button
            key={tab.id}
            ref={(el) => { tabRefs.current[i] = el; }}
            type="button"
            role="tab"
            id={`${baseId}-tab-${i}`}
            aria-selected={i === selected}
            aria-controls={`${baseId}-panel-${i}`}
            tabIndex={i === selected ? 0 : -1}          // roving tabindex: only the selected tab is in the Tab order
            onClick={() => select(i)}
          >
            {tab.title}
          </button>
        ))}
      </div>
      {tabs.map((tab, i) => (
        <div key={tab.id} role="tabpanel" id={`${baseId}-panel-${i}`} aria-labelledby={`${baseId}-tab-${i}`}
          tabIndex={0} hidden={i !== selected}>
          {tab.content}
        </div>
      ))}
    </div>
  );
}
```

### 6. Menu button

`role="menu"` is for **application menus of actions** (Edit, Duplicate, Delete), like a desktop app menu. It is **not** for site navigation: a nav dropdown is a *disclosure* (a `<button aria-expanded>` that shows a list of ordinary links). Screen readers switch into a special mode inside `role="menu"`, so using it for links makes navigation worse.

APG keyboard behaviour for a menu button:

- Enter, Space or ↓ on the button opens the menu and focuses the first item; ↑ opens it on the last item.
- ↑ and ↓ move between items (wrapping around); Home and End jump to the ends.
- Enter or Space activates an item and closes the menu.
- Escape closes the menu and returns focus to the button. Tab closes it and moves on.

```jsx
import { useEffect, useId, useRef, useState } from "react";

export function MenuButton({ label, items }) {        // items: [{ label, onSelect }]
  const [open, setOpen] = useState(false);
  const [active, setActive] = useState(0);
  const buttonRef = useRef(null);
  const itemRefs = useRef([]);
  const buttonId = useId();
  const menuId = useId();

  useEffect(() => {
    if (open) itemRefs.current[active]?.focus();       // roving focus follows `active`
  }, [open, active]);

  const openAt = (index) => { setActive(index); setOpen(true); };
  const close = ({ returnFocus = true } = {}) => {
    setOpen(false);
    if (returnFocus) buttonRef.current.focus();
  };
  const choose = (item) => { close(); item.onSelect(); };

  const onMenuKeyDown = (e) => {
    const target = { ArrowDown: active + 1, ArrowUp: active - 1, Home: 0, End: items.length - 1 }[e.key];
    if (target !== undefined) { e.preventDefault(); setActive((target + items.length) % items.length); }
    else if (e.key === "Escape") { e.preventDefault(); close(); }
    else if (e.key === "Tab") close({ returnFocus: false });   // let Tab move focus onward
    else if (e.key === "Enter" || e.key === " ") { e.preventDefault(); choose(items[active]); }
  };

  return (
    <div
      className="menu-wrapper"
      onBlur={(e) => { if (open && !e.currentTarget.contains(e.relatedTarget)) setOpen(false); }}   // click outside
    >
      <button
        ref={buttonRef}
        id={buttonId}
        type="button"
        aria-haspopup="menu"
        aria-expanded={open}
        aria-controls={menuId}
        onClick={() => (open ? close() : openAt(0))}
        onKeyDown={(e) => {
          if (e.key === "ArrowDown") { e.preventDefault(); openAt(0); }
          if (e.key === "ArrowUp") { e.preventDefault(); openAt(items.length - 1); }
        }}
      >
        {label}
      </button>
      <ul role="menu" id={menuId} aria-labelledby={buttonId} hidden={!open} onKeyDown={onMenuKeyDown}>
        {items.map((item, i) => (
          <li key={item.label} role="menuitem" tabIndex={-1} ref={(el) => { itemRefs.current[i] = el; }}
            onClick={() => choose(item)}>
            {item.label}
          </li>
        ))}
      </ul>
    </div>
  );
}
```

### 7. Combobox (autocomplete) with `aria-activedescendant`

Focus stays in the input so the user can keep typing. The highlighted option is announced through `aria-activedescendant`, and a status region announces how many results there are:

```jsx
import { useEffect, useId, useState } from "react";

export function Combobox({ label, options }) {          // options: string[]
  const [query, setQuery] = useState("");
  const [open, setOpen] = useState(false);
  const [active, setActive] = useState(-1);
  const id = useId();

  const matches = options.filter((o) => o.toLowerCase().includes(query.trim().toLowerCase()));
  const expanded = open && matches.length > 0;
  const optionId = (i) => `${id}-option-${i}`;

  useEffect(() => {                                      // keep the highlighted option visible in long lists
    if (active >= 0) document.getElementById(`${id}-option-${active}`)?.scrollIntoView({ block: "nearest" });
  }, [active, id]);

  const choose = (value) => { setQuery(value); setOpen(false); setActive(-1); };

  const onKeyDown = (e) => {
    if (e.key === "ArrowDown") {
      e.preventDefault();
      setOpen(true);
      setActive((a) => Math.min(a + 1, matches.length - 1));
    } else if (e.key === "ArrowUp") {
      e.preventDefault();
      setActive((a) => Math.max(a - 1, 0));
    } else if (e.key === "Enter" && expanded && active >= 0) {
      e.preventDefault();                                 // don't submit the surrounding form
      choose(matches[active]);
    } else if (e.key === "Escape") {
      if (expanded) { setOpen(false); setActive(-1); }    // first Escape closes the list
      else setQuery("");                                  // second Escape clears the input
    }
  };

  return (
    <div className="combobox">
      <label htmlFor={`${id}-input`}>{label}</label>
      <input
        id={`${id}-input`}
        role="combobox"
        aria-expanded={expanded}
        aria-controls={`${id}-listbox`}
        aria-autocomplete="list"
        aria-activedescendant={expanded && active >= 0 ? optionId(active) : undefined}
        autoComplete="off"
        value={query}
        onChange={(e) => { setQuery(e.target.value); setOpen(true); setActive(-1); }}
        onKeyDown={onKeyDown}
        onBlur={() => setOpen(false)}
      />
      <ul id={`${id}-listbox`} role="listbox" aria-label={label} hidden={!expanded}>
        {matches.map((m, i) => (
          <li key={m} id={optionId(i)} role="option" aria-selected={i === active}
            onMouseDown={(e) => e.preventDefault()}      // keep focus in the input when clicking
            onClick={() => choose(m)}>
            {m}
          </li>
        ))}
      </ul>
      <div role="status" className="sr-only">
        {open && query ? `${matches.length} result${matches.length === 1 ? "" : "s"} available` : ""}
      </div>
    </div>
  );
}
```

To add server results, combine it with the debounced, abortable fetch from the Autocomplete machine-coding question (Section 53). Before building your own, check whether a native `<select>`, `<input list>` + `<datalist>`, or a library combobox (React Aria, Downshift, Headless UI) does the job.

### 8. Live regions: announcing changes

Screen readers only read what the user moves to, so visual-only feedback ("Saved ✓", "3 results", a toast) is silent unless it's inside a **live region**:

| Region | Announced | Use for |
|---|---|---|
| `role="status"` (implies `aria-live="polite"`) | When the user is idle | "Saved", "5 results", "Added to cart" |
| `role="alert"` (implies `aria-live="assertive"`) | Immediately, interrupting | Errors that need attention now. Use sparingly |
| `aria-busy="true"` on a region | Suppresses announcements until it's `false` | Content that updates in several steps |

**The region must already exist in the DOM before its content changes.** Mounting `<div role="status">Saved</div>` at the moment you want to announce it is unreliable across screen readers. Render one empty region up front and change its text:

```jsx
import { createContext, useCallback, useContext, useRef, useState } from "react";

const AnnounceContext = createContext(() => {});

export function AnnouncerProvider({ children }) {
  const [message, setMessage] = useState("");
  const timer = useRef();
  const announce = useCallback((text) => {
    clearTimeout(timer.current);
    setMessage("");                                        // clear first, so repeating the same text is announced again
    timer.current = setTimeout(() => setMessage(text), 100);
  }, []);
  return (
    <AnnounceContext.Provider value={announce}>
      {children}
      <div role="status" className="sr-only">{message}</div>
    </AnnounceContext.Provider>
  );
}

export const useAnnounce = () => useContext(AnnounceContext);

// Usage: const announce = useAnnounce();  …  announce("Added to cart");
```

Toasts need a live region too, must stay visible long enough to read (or until dismissed), and must never be the **only** place an error appears. WCAG 4.1.3 ("Status Messages") covers this.

### 9. Accessible forms

- Every field has a visible `<label>`. Group radios and checkboxes with `<fieldset>` + `<legend>`.
- Use the right `type`, `inputMode` and **`autoComplete`** tokens (`name`, `email`, `tel`, `street-address`, `new-password`, `one-time-code`). They enable autofill and password managers, and help users with memory or motor impairments.
- Mark required fields with the `required` attribute (and a visible "required" hint), not only a red asterisk.
- On a failed submit: show the error **as text** next to the field, set `aria-invalid`, link the message with `aria-describedby`, and **move focus to the first invalid field**. The screen reader then reads the label, "invalid entry" and the error message. On long forms, add an error summary at the top.
- **Don't disable the submit button** until the form is valid. Users can't tell what's wrong, and a disabled button isn't focusable, so it's skipped entirely. Let them submit, then show the errors.
- Don't validate on every keystroke with announcements; validate on blur and on submit.

```jsx
import { useId, useState } from "react";

export function Field({ label, hint, error, ...inputProps }) {
  const id = useId();
  const hintId = hint ? `${id}-hint` : undefined;
  const errorId = error ? `${id}-error` : undefined;
  return (
    <div className="field">
      <label htmlFor={id}>{label}</label>
      {hint && <p id={hintId} className="hint">{hint}</p>}
      <input
        id={id}
        aria-invalid={error ? true : undefined}
        aria-describedby={[hintId, errorId].filter(Boolean).join(" ") || undefined}
        {...inputProps}
      />
      {error && <p id={errorId} className="error">{error}</p>}
    </div>
  );
}

export function SignupForm({ onSubmit }) {
  const [errors, setErrors] = useState({});

  function handleSubmit(e) {
    e.preventDefault();
    const form = e.currentTarget;
    const data = Object.fromEntries(new FormData(form));
    const next = {};
    if (!data.name.trim()) next.name = "Enter your full name";
    if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(data.email)) next.email = "Enter an email address like name@example.com";
    setErrors(next);
    const firstInvalid = Object.keys(next)[0];
    if (firstInvalid) form.elements.namedItem(firstInvalid).focus();
    else onSubmit(data);
  }

  return (
    <form noValidate onSubmit={handleSubmit}>          {/* noValidate: we show our own accessible errors */}
      <Field name="name" label="Full name" autoComplete="name" required error={errors.name} />
      <Field name="email" label="Email" type="email" autoComplete="email" required error={errors.email}
        hint="We'll send a confirmation link" />
      <button type="submit">Create account</button>
    </form>
  );
}
```

### 10. Visual design rules

- **Contrast** (1.4.3): at least **4.5:1** for normal text, **3:1** for large text (24px, or about 19px bold). UI components and meaningful graphics such as input borders, focus rings and icons need **3:1** (1.4.11).
- **Don't use colour alone**: pair a red border with an error icon and text, and underline links in body text.
- **Zoom and reflow:** the page works at 200% text size (1.4.4) and at 320 CSS px wide without horizontal scrolling (1.4.10). Use `rem` and let containers wrap.
- **Motion:** respect `prefers-reduced-motion`, and give auto-playing carousels and animations that last over 5 seconds a pause button (2.2.2).
- **Don't lock orientation or zoom:** never set `maximum-scale=1` or `user-scalable=no` in the viewport meta tag.

A contrast checker you can run in design-token tests:

```js
// WCAG relative luminance and contrast ratio for #rrggbb colours
function luminance(hex) {
  const [r, g, b] = hex.match(/[\da-f]{2}/gi).map((h) => {
    const c = parseInt(h, 16) / 255;
    return c <= 0.04045 ? c / 12.92 : ((c + 0.055) / 1.055) ** 2.4;
  });
  return 0.2126 * r + 0.7152 * g + 0.0722 * b;
}

export function contrastRatio(foreground, background) {
  const [light, dark] = [luminance(foreground), luminance(background)].sort((a, b) => b - a);
  return (light + 0.05) / (dark + 0.05);
}

contrastRatio("#000000", "#ffffff").toFixed(1);   // → "21.0"
contrastRatio("#767676", "#ffffff").toFixed(2);   // → "4.54"   the lightest grey that passes AA on white
contrastRatio("#777777", "#ffffff").toFixed(2);   // → "4.48"   fails
contrastRatio("#1a56db", "#ffffff") >= 4.5;       // → true     the focus-ring blue used above
```

### 11. Common mistakes

| ❌ Mistake | ✅ Fix |
|---|---|
| `<div onClick>` / `<span onClick>` | `<button type="button">` |
| `<a onClick>` with no `href` (not focusable) | `<button>` for actions, `<a href>` for navigation |
| `aria-hidden="true"` on something focusable, or on a parent of it | Remove it, or also make the content unfocusable (`inert`) |
| `role="button"` without `tabIndex` and key handlers | Use a real `<button>` |
| Positive `tabIndex` values | Fix the DOM order |
| `outline: none` with no replacement | `:focus-visible` styles |
| Placeholder or `title` as the only label | A visible `<label>` |
| Status text that appears but isn't in a live region | An always-rendered `role="status"` region |
| Menus that open only on hover | Open on click and keyboard too; hover can be an enhancement |
| `role="menu"` for site navigation | A disclosure button with a list of links |
| Auto-rotating carousel with no pause | A pause button; stop on hover and focus |
| Infinite scroll that makes the footer unreachable | A "Load more" button, or put the footer links elsewhere |
| "Click here" / "Read more" links | Descriptive link text |
| Error shown only as a red border | Text message + `aria-invalid` + `aria-describedby` |

### 12. Testing accessibility

Automated tools catch only **part** of the problems, roughly a third to a half. They can't tell whether alt text is meaningful, whether the focus order makes sense, or whether a screen-reader user can actually complete the flow. Use all four layers:

**1. Lint while coding:** `eslint-plugin-jsx-a11y` (its `recommended` config) flags `onClick` on non-interactive elements, missing `alt`, invalid ARIA and similar problems.

**2. Component tests: query by role.** `getByRole(role, { name })` only finds elements that are exposed correctly to assistive technology, so good tests double as accessibility checks. Drive them with the **keyboard**:

```jsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import { expect, test } from "vitest";
import { Tabs } from "./Tabs";

test("tabs follow the APG keyboard pattern", async () => {
  const user = userEvent.setup();
  render(<Tabs label="Settings" tabs={[
    { id: "profile", title: "Profile", content: "Profile form" },
    { id: "billing", title: "Billing", content: "Billing form" },
  ]} />);

  await user.tab();                                                  // Tab lands on the SELECTED tab
  expect(screen.getByRole("tab", { name: "Profile" })).toHaveFocus();

  await user.keyboard("{ArrowRight}");                               // arrows move focus and select
  const billing = screen.getByRole("tab", { name: "Billing" });
  expect(billing).toHaveFocus();
  expect(billing).toHaveAttribute("aria-selected", "true");
  expect(screen.getByRole("tabpanel", { name: "Billing" })).toHaveTextContent("Billing form");

  await user.tab();                                                  // the next Tab goes into the panel
  expect(screen.getByRole("tabpanel", { name: "Billing" })).toHaveFocus();
});
```

(`toHaveFocus`, `toHaveAttribute` and `toHaveTextContent` come from `@testing-library/jest-dom`.) The `description` option checks `aria-describedby` wiring, for example `getByRole("textbox", { name: "Email", description: /enter an email/i })`.

**Run axe in component tests.** `vitest-axe` and `jest-axe` wrap this; here it is directly with `axe-core`:

```jsx
import axe from "axe-core";
import { expect } from "vitest";

// jsdom does no layout or painting, so colour contrast can't be checked there (do it in the browser)
export async function expectNoAxeViolations(container) {
  const { violations } = await axe.run(container, { rules: { "color-contrast": { enabled: false } } });
  const summary = violations.map((v) => `${v.id}: ${v.nodes.map((n) => n.target.join(" ")).join(", ")}`);
  expect(summary).toEqual([]);
}
```

**jsdom lacks some browser APIs** these components use. Stub them in the test setup file:

```js
// vitest.setup.js
if (!HTMLDialogElement.prototype.showModal) {
  HTMLDialogElement.prototype.showModal = function () { this.setAttribute("open", ""); };
  HTMLDialogElement.prototype.close = function () {
    this.removeAttribute("open");
    this.dispatchEvent(new Event("close"));
  };
}
Element.prototype.scrollIntoView ??= function () {};
```

The stubs only prevent crashes. jsdom doesn't enforce the focus trap, inert background or Escape handling, so test those in a real browser.

**3. End-to-end tests in a real browser:** Playwright with `@axe-core/playwright` also checks colour contrast and real focus behaviour:

```js
import { test, expect } from "@playwright/test";
import AxeBuilder from "@axe-core/playwright";

test("checkout page has no detectable a11y violations", async ({ page }) => {
  await page.goto("/checkout");
  const results = await new AxeBuilder({ page })
    .withTags(["wcag2a", "wcag2aa", "wcag21a", "wcag21aa", "wcag22aa"])
    .analyze();
  expect(results.violations).toEqual([]);
});

test("the delete dialog traps focus and returns it", async ({ page }) => {
  await page.goto("/projects/1");
  const trigger = page.getByRole("button", { name: "Delete project" });
  await trigger.click();
  const dialog = page.getByRole("dialog", { name: "Delete project?" });
  await expect(dialog).toBeVisible();
  await page.keyboard.press("Escape");
  await expect(dialog).toBeHidden();
  await expect(trigger).toBeFocused();
});
```

**4. Manual checks before release (15 minutes):**

- **Keyboard only:** unplug the mouse. Can you reach and operate everything with Tab, Shift+Tab, Enter, Space, the arrow keys and Escape? Is focus always visible? Does it go somewhere sensible after dialogs close and items are deleted?
- **Screen reader:** VoiceOver on macOS (Cmd+F5; the rotor, VO+U, lists headings, links and landmarks), NVDA on Windows (free; H jumps between headings, D between landmarks, Insert+F7 lists elements), TalkBack on Android. Complete the main flow with your eyes closed.
- **Zoom** to 200% and **narrow** the window to 320px.
- Turn on **reduced motion** and a **high-contrast** or forced-colours mode.
- Run the **Lighthouse** accessibility audit or the **axe DevTools** extension on key pages.

### 13. Use a tested library for complex widgets

Comboboxes, date pickers, menus, and drag-and-drop with keyboard support are hard to get fully right across browsers and screen readers. **React Aria** (Adobe), **Radix UI** (which shadcn/ui is built on), **Headless UI**, **Ariakit** and **Downshift** implement the APG patterns and are tested with real assistive technology. Style them however you like. Building your own, as above, is how you learn the patterns and pass machine-coding rounds.

### Interview Qs

1. What is the first rule of ARIA? → Don't use ARIA when a native element provides the semantics and behaviour. ARIA changes only what's announced, never behaviour.
2. `<button>` vs `<div onClick>`? → A button is focusable, has a role, handles Enter and Space, supports `disabled` and form submission.
3. How is an accessible name computed? → `aria-labelledby` → `aria-label` → native label, content or `alt` → `title`.
4. `aria-label` vs `aria-labelledby` vs `aria-describedby`? → A direct string name; a name from other elements' text; secondary descriptive text.
5. How do you build an accessible modal? → `<dialog>` + `showModal()`: labelled, focus moves in, trapped, closes on Escape, inert background, focus returns to the trigger.
6. Roving tabindex vs `aria-activedescendant`? → Moving real focus with `tabIndex` 0/−1 vs keeping focus on one element and pointing at the active option by `id`.
7. What are live regions? Why must they exist before the update? → Regions whose changes are announced (`status` is polite, `alert` assertive). Screen readers watch existing regions for changes.
8. How do you handle focus on route changes in an SPA? → Move focus to the new `<h1>` (with `tabIndex={-1}`) or `<main>`, and update `document.title`.
9. How do you make form errors accessible? → Text errors, `aria-invalid`, `aria-describedby`, focus the first invalid field, and don't disable the submit button.
10. What are the WCAG contrast requirements? → 4.5:1 for text, 3:1 for large text and UI components.
11. What's new in WCAG 2.2? → Focus Not Obscured, 24×24 px target size, Accessible Authentication (allow paste and password managers), Redundant Entry, and more.
12. Why shouldn't you use `role="menu"` for navigation? → Menu roles are for app-style action menus; navigation should be a disclosure with links.
13. How do you test accessibility? → Lint, `getByRole` tests with keyboard interaction, axe (unit and E2E), and manual keyboard and screen-reader passes.
14. What can't automated tools catch? → Meaningful alt text, logical focus order, understandable content, and whether a flow is actually usable with assistive technology.

---

## 48. Security in React

- JSX **escapes** values automatically → protects from most XSS.
- `dangerouslySetInnerHTML` bypasses that — sanitize first:

```jsx
import DOMPurify from "dompurify";
<div dangerouslySetInnerHTML={{ __html: DOMPurify.sanitize(userHtml) }} />
```

- Validate URLs: `<a href={userUrl}>` can be `javascript:alert(1)` → allow only `http(s):`.
- Don't store sensitive tokens in localStorage if possible (HttpOnly cookies).
- Never put secrets in frontend env vars (`VITE_*`/`NEXT_PUBLIC_*` are public!).
- Keep dependencies updated (`npm audit`), use CSP headers.

---

## 49. Folder Structure & Best Practices

```
src/
  app/               # app setup: providers, router, store
  components/        # shared UI (Button, Modal, Input)
  features/          # feature-based modules
    auth/
      components/
      hooks/
      api.ts
      authSlice.ts
    products/
  hooks/             # shared custom hooks
  lib/ / utils/      # helpers, api client
  pages/ or routes/
  styles/
  types/
  main.tsx
```

Best practices:
- One component per file; small, focused components.
- Feature-based folders scale better than type-based.
- Use TypeScript.
- Keep state as local as possible; derive instead of duplicate.
- Custom hooks for reusable logic.
- Consistent naming: `PascalCase` components, `useXxx` hooks, `handleXxx` handlers, `onXxx` props.
- ESLint (react-hooks plugin) + Prettier.
- Absolute imports (`@/components/Button`).
- Error boundaries & loading states for every async UI.

---

## 50. Common Mistakes

1. Mutating state directly (`arr.push` then `setArr(arr)`).
2. Using index as key in dynamic lists.
3. Missing/incorrect `useEffect` dependencies → stale data or infinite loops.
4. Not cleaning up effects (listeners, intervals, subscriptions).
5. Storing derived data in state.
6. Defining components inside components.
7. Calling functions instead of passing them: `onClick={handle()}`.
8. `{count && <X/>}` rendering `0`.
9. Overusing context for frequently changing values.
10. Premature memoization everywhere / missing it where it matters.
11. Using `useEffect` for event-driven logic.
12. Reading state right after `setState` expecting the new value.
13. Not handling loading/error states.
14. Huge components with many responsibilities.
15. Async function directly as the `useEffect` callback.

---

## 51. Production React Patterns

How real React codebases are built. Tutorials show `useEffect` + `fetch` + `useState`. Production apps also need API layers, caching, error reporting, auth refresh, URL state, feature flags, forms with server errors, and consistent loading/empty/error UI.

### 1. API layer + TanStack Query (the standard setup)

Never call `fetch` directly inside components. Put a typed API function layer underneath and TanStack Query on top for caching, dedupe, retries and refetching.

```jsx
// lib/queryClient.js
import { QueryClient } from "@tanstack/react-query";

export const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      staleTime: 30_000,                          // data is fresh for 30s → no refetch storms
      retry: (count, err) => err.status >= 500 && count < 2, // don't retry 4xx
      refetchOnWindowFocus: true,
    },
    mutations: { retry: 0 },                      // never auto-retry writes (duplicates!)
  },
});
```

```jsx
// features/products/products.queries.js — query key factory keeps keys consistent
import { useQuery, useMutation, useQueryClient, keepPreviousData } from "@tanstack/react-query";
import { http } from "@/lib/http"; // central fetch wrapper (see JS notes: Production-Grade JavaScript)

export const productKeys = {
  all: ["products"],
  lists: () => [...productKeys.all, "list"],
  list: (filters) => [...productKeys.lists(), filters],
  detail: (id) => [...productKeys.all, "detail", id],
};

export function useProducts(filters) {
  return useQuery({
    queryKey: productKeys.list(filters),
    queryFn: ({ signal }) => http.get(`/products?${new URLSearchParams(filters)}`, { signal }), // auto-cancel
    placeholderData: keepPreviousData,            // keep old page visible while next page loads
  });
}

export function useProduct(id) {
  return useQuery({ queryKey: productKeys.detail(id), queryFn: () => http.get(`/products/${id}`), enabled: !!id });
}

export function useUpdateProduct() {
  const qc = useQueryClient();
  return useMutation({
    mutationFn: ({ id, ...patch }) => http.patch(`/products/${id}`, patch),
    onSuccess: (updated) => {
      qc.setQueryData(productKeys.detail(updated.id), updated); // update detail cache
      qc.invalidateQueries({ queryKey: productKeys.lists() });  // refetch lists
    },
  });
}
```

Components become simple:

```jsx
function ProductPage({ id }) {
  const { data: product, isPending, error } = useProduct(id);
  const update = useUpdateProduct();
  if (isPending) return <ProductSkeleton />;
  if (error) return <ErrorState error={error} />;
  return (
    <ProductForm
      product={product}
      saving={update.isPending}
      onSave={(patch) => update.mutate({ id, ...patch }, { onSuccess: () => toast.success("Saved") })}
    />
  );
}
```

### 2. Every async UI has 4 states: loading, error, empty, success

Forgetting the **empty** and **error** states is one of the most common production gaps.

```jsx
function AsyncView({ query, isEmpty = (d) => Array.isArray(d) && d.length === 0, empty, loading = <Spinner />, children }) {
  if (query.isPending) return loading;
  if (query.isError) return <ErrorState error={query.error} onRetry={query.refetch} />;
  if (isEmpty(query.data)) return empty ?? <EmptyState />;
  return children(query.data);
}

function Orders() {
  const query = useQuery({ queryKey: ["orders"], queryFn: fetchOrders });
  return (
    <AsyncView query={query} loading={<OrdersSkeleton />} empty={<EmptyState title="No orders yet" action={<Link to="/shop">Start shopping</Link>} />}>
      {(orders) => orders.map((o) => <OrderRow key={o.id} order={o} />)}
    </AsyncView>
  );
}

function ErrorState({ error, onRetry }) {
  const message = error.status === 404 ? "Not found" : error.status === 0 ? "You're offline" : "Something went wrong";
  return (
    <div role="alert">
      <p>{message}</p>
      {onRetry && <button onClick={() => onRetry()}>Try again</button>}
    </div>
  );
}
```

UX details that matter:
- **Skeletons** over spinners for content areas (less layout shift).
- Show **background refetch** subtly (`isFetching`) and don't blank the screen.
- Keep previous data while paginating/filtering.
- Don't flash a spinner for very fast loads (delay the spinner ~200ms).

### 3. Error handling layers

1. **Route-level error boundary** — a crash in one page doesn't kill the whole app.
2. **Widget-level boundaries** — for risky, independent parts (charts, third-party embeds).
3. **Mutations** → toast + keep the form data (never lose user input).
4. **Global reporting** → Sentry (with user id, route and release version).

```jsx
import { ErrorBoundary } from "react-error-boundary";
import { QueryErrorResetBoundary, QueryClient, MutationCache } from "@tanstack/react-query";
import * as Sentry from "@sentry/react";

function RouteBoundary({ children }) {
  return (
    <QueryErrorResetBoundary>
      {({ reset }) => (
        <ErrorBoundary
          onReset={reset}
          onError={(error, info) => Sentry.captureException(error, { extra: info })}
          fallbackRender={({ resetErrorBoundary }) => (
            <div role="alert">
              <h2>This page crashed</h2>
              <button onClick={resetErrorBoundary}>Reload section</button>
            </div>
          )}
        >
          {children}
        </ErrorBoundary>
      )}
    </QueryErrorResetBoundary>
  );
}

// Global mutation error toast
const queryClient2 = new QueryClient({
  mutationCache: new MutationCache({
    onError: (error) => toast.error(error.body?.error?.message ?? "Could not save. Please try again."),
  }),
});
```

### 4. Authentication in production

```jsx
// auth/AuthProvider.jsx
const AuthContext = createContext(null);

export function AuthProvider({ children }) {
  const qc = useQueryClient();
  const { data: user, isPending } = useQuery({
    queryKey: ["me"],
    queryFn: () => http.get("/auth/me"),       // cookie-based session / refresh handled by http layer
    retry: false,
    staleTime: Infinity,
  });

  const login = useCallback(async (credentials) => {
    const me = await http.post("/auth/login", credentials);
    qc.setQueryData(["me"], me);
  }, [qc]);

  const logout = useCallback(async () => {
    await http.post("/auth/logout").catch(() => {});
    qc.clear();                                  // wipe ALL cached user data
    window.location.assign("/login");            // hard reset of in-memory state
  }, [qc]);

  const value = useMemo(() => ({ user: user ?? null, isPending, login, logout }), [user, isPending, login, logout]);
  return <AuthContext.Provider value={value}>{children}</AuthContext.Provider>;
}

export function useAuth() {
  const ctx = useContext(AuthContext);
  if (!ctx) throw new Error("useAuth must be used inside AuthProvider");
  return ctx;
}

// Route guard
export function RequireAuth({ roles, children }) {
  const { user, isPending } = useAuth();
  const location = useLocation();
  if (isPending) return <FullPageSpinner />;          // don't redirect before we know!
  if (!user) return <Navigate to="/login" replace state={{ from: location }} />;
  if (roles && !roles.includes(user.role)) return <Forbidden />;
  return children;
}

// Permission-based UI
export function Can({ permission, children, fallback = null }) {
  const { user } = useAuth();
  return user?.permissions.includes(permission) ? children : fallback;
}
<Can permission="orders:refund"><RefundButton /></Can>
```

Key rules:
- **Hiding a button is UX, not security.** The server must check permissions on every request.
- On **401** anywhere → try a token refresh once → if that fails, log out and redirect (with a "return to" path).
- **Don't flash protected content** before auth is resolved; don't redirect while auth is still loading.
- On logout, **clear caches and stores** so the next user on the same device can't see the previous user's data.
- Access token in memory + refresh token in an HttpOnly cookie is a common secure setup.

```js
// Refresh-once logic inside the http layer (single in-flight refresh shared by all requests)
let refreshPromise = null;
async function refreshSession() {
  refreshPromise ??= fetch("/auth/refresh", { method: "POST", credentials: "include" })
    .then((r) => { if (!r.ok) throw new Error("refresh failed"); })
    .finally(() => { refreshPromise = null; });
  return refreshPromise;
}
// in request(): if (res.status === 401 && !isRetry) { await refreshSession(); return request(path, { ...opts, isRetry: true }); }
```

### 5. Forms in production

```jsx
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { z } from "zod";

// Share schemas between frontend and backend when possible (monorepo package)
export const profileSchema = z.object({
  name: z.string().trim().min(2, "Name is too short"),
  email: z.string().email("Enter a valid email"),
  phone: z.string().regex(/^[6-9]\d{9}$/, "Enter a valid 10-digit mobile number").optional().or(z.literal("")),
});

function ProfileForm({ user }) {
  const update = useUpdateProfile();
  const { register, handleSubmit, setError, reset, formState: { errors, isSubmitting, isDirty } } = useForm({
    resolver: zodResolver(profileSchema),
    defaultValues: user,
  });

  useUnsavedChangesWarning(isDirty);

  const onSubmit = handleSubmit(async (values) => {
    try {
      const saved = await update.mutateAsync(values);
      reset(saved);                                    // new baseline → isDirty false
      toast.success("Profile updated");
    } catch (err) {
      // Map server validation errors onto fields
      if (err.status === 400 && err.body?.details) {
        for (const [field, messages] of Object.entries(err.body.details)) {
          setError(field, { message: messages[0] });
        }
      } else if (err.status === 409) {
        setError("email", { message: "This email is already in use" });
      } else {
        setError("root", { message: "Could not save. Please try again." });
      }
    }
  });

  return (
    <form onSubmit={onSubmit} noValidate>
      <Field label="Name" error={errors.name?.message}><input {...register("name")} /></Field>
      <Field label="Email" error={errors.email?.message}><input type="email" {...register("email")} /></Field>
      <Field label="Mobile" error={errors.phone?.message}><input inputMode="numeric" {...register("phone")} /></Field>
      {errors.root && <p role="alert">{errors.root.message}</p>}
      <button type="submit" disabled={isSubmitting || !isDirty}>{isSubmitting ? "Saving…" : "Save"}</button>
    </form>
  );
}

function Field({ label, error, children }) {
  const id = useId();
  return (
    <div>
      <label htmlFor={id}>{label}</label>
      {cloneElement(children, { id, "aria-invalid": !!error, "aria-describedby": error ? `${id}-err` : undefined })}
      {error && <p id={`${id}-err`} role="alert">{error}</p>}
    </div>
  );
}

function useUnsavedChangesWarning(when) {
  useEffect(() => {
    if (!when) return;
    const handler = (e) => { e.preventDefault(); e.returnValue = ""; };
    window.addEventListener("beforeunload", handler);
    return () => window.removeEventListener("beforeunload", handler);
  }, [when]);
}
```

Checklist: client validation for UX + **server validation for security**, disable submit while submitting, show server errors on the right fields, never clear the form on failure, warn about unsaved changes, accessible labels and error messages.

### 6. URL as the source of truth (filters, search, pagination, tabs)

Filters and pagination belong in the URL, not only in `useState`: they survive refresh, can be shared and bookmarked, and the back button works.

```jsx
function ProductsPage() {
  const [params, setParams] = useSearchParams();
  const filters = {
    q: params.get("q") ?? "",
    category: params.get("category") ?? "all",
    page: Number(params.get("page") ?? 1),
    sort: params.get("sort") ?? "newest",
  };

  const updateFilter = (key, value) =>
    setParams((prev) => {
      const next = new URLSearchParams(prev);
      value ? next.set(key, value) : next.delete(key);
      if (key !== "page") next.set("page", "1");     // reset page when filters change
      return next;
    }, { replace: key === "q" });                    // don't spam history while typing

  // Debounced search box that writes to the URL
  const [search, setSearch] = useState(filters.q);
  const debouncedSearch = useDebounce(search, 400);
  useEffect(() => {
    if (debouncedSearch !== filters.q) updateFilter("q", debouncedSearch);
  }, [debouncedSearch]); // eslint-disable-line react-hooks/exhaustive-deps

  const { data, isPending } = useProducts(filters);  // query key includes filters → cached per combination

  return (
    <>
      <input value={search} onChange={(e) => setSearch(e.target.value)} placeholder="Search products" />
      <select value={filters.sort} onChange={(e) => updateFilter("sort", e.target.value)}>
        <option value="newest">Newest</option>
        <option value="price_asc">Price: low to high</option>
      </select>
      {/* list + pagination using updateFilter("page", n) */}
    </>
  );
}
```

### 7. Optimistic updates with rollback

Update the UI instantly, and roll back if the server fails. Use it for likes, toggles, reordering and todo checks. Don't use it for payments or anything the user must see confirmed.

```jsx
function useToggleTodo() {
  const qc = useQueryClient();
  return useMutation({
    mutationFn: ({ id, done }) => http.patch(`/todos/${id}`, { done }),
    onMutate: async ({ id, done }) => {
      await qc.cancelQueries({ queryKey: ["todos"] });            // stop in-flight refetch overwriting us
      const previous = qc.getQueryData(["todos"]);
      qc.setQueryData(["todos"], (old = []) => old.map((t) => (t.id === id ? { ...t, done } : t)));
      return { previous };
    },
    onError: (_err, _vars, ctx) => {
      qc.setQueryData(["todos"], ctx.previous);                   // rollback
      toast.error("Couldn't update. Changes reverted.");
    },
    onSettled: () => qc.invalidateQueries({ queryKey: ["todos"] }), // sync with server truth
  });
}
```

### 8. Environment config & feature flags

```js
// lib/env.js — validate once
import { z } from "zod";
export const env = z.object({
  VITE_API_URL: z.string().url(),
  VITE_SENTRY_DSN: z.string().optional(),
  VITE_ENABLE_NEW_CHECKOUT: z.enum(["true", "false"]).default("false"),
}).parse(import.meta.env);
// Remember: VITE_*/NEXT_PUBLIC_* are visible to everyone — never put secrets here.
```

```jsx
const FlagsContext = createContext({});
export function FlagsProvider({ children }) {
  const { data: flags = {} } = useQuery({ queryKey: ["flags"], queryFn: () => http.get("/flags"), staleTime: 5 * 60_000 });
  return <FlagsContext.Provider value={flags}>{children}</FlagsContext.Provider>;
}
export const useFlag = (name) => Boolean(useContext(FlagsContext)[name]);

function CheckoutRoute() {
  return useFlag("newCheckout") ? <NewCheckout /> : <LegacyCheckout />;
}
```

### 9. Reusable UI components (design system basics)

- Build a small set of **primitives** (Button, Input, Select, Modal, Toast, Tooltip) that everyone uses. Consistent styling and accessibility are then fixed in one place.
- Prefer accessible headless libraries (**Radix UI, React Aria, Headless UI**) or **shadcn/ui** over hand-rolling modals, menus and comboboxes: focus traps, keyboard navigation and ARIA are hard to get right.
- Components accept native props (`...rest`), forward refs, and have variants instead of one-off styles.

```jsx
const variants = { primary: "btn btn-primary", secondary: "btn btn-secondary", danger: "btn btn-danger" };
const sizes = { sm: "btn-sm", md: "", lg: "btn-lg" };

export function Button({ variant = "primary", size = "md", loading = false, disabled, children, className = "", ref, ...rest }) {
  return (
    <button
      ref={ref}
      className={`${variants[variant]} ${sizes[size]} ${className}`}
      disabled={disabled || loading}
      aria-busy={loading || undefined}
      {...rest}
    >
      {loading ? <Spinner size="sm" aria-hidden /> : null}
      {children}
    </button>
  );
}
```

### 10. Performance practices that actually matter

1. **Route-level code splitting** (`lazy` per page) and lazy-load heavy widgets (charts, editors, maps).
2. **Server state in TanStack Query** — removes most redundant fetching and global-state re-renders.
3. **Keep state close to where it's used**; split contexts; use selector-based stores for frequently changing global state.
4. **Virtualize** lists over a few hundred rows.
5. **Optimize images** (right size, WebP/AVIF, lazy, width/height to avoid CLS).
6. **Profile before memoizing** — React DevTools Profiler; add `memo/useMemo/useCallback` where the profiler shows waste (or enable React Compiler).
7. **Debounce** search inputs; **throttle** scroll/resize handlers; prefer IntersectionObserver.
8. Watch the **bundle** (analyzer) and track Web Vitals in production.

### 11. Analytics & tracking

```jsx
// One tracking function → swap providers without touching components
export function track(event, props = {}) {
  if (import.meta.env.DEV) return console.debug("[track]", event, props);
  window.analytics?.track(event, { ...props, path: location.pathname });
}

// Page views on route change
function usePageViews() {
  const location = useLocation();
  useEffect(() => { track("page_view", { path: location.pathname }); }, [location.pathname]);
}

<button onClick={() => { track("checkout_started", { cartValue }); startCheckout(); }}>Checkout</button>
```

Respect consent (cookie banners, GDPR): don't load trackers before consent.

### 12. Accessibility & i18n in production

- Semantic HTML first; every input has a label; visible focus; keyboard support; `aria-live` for async messages/toasts.
- Test with keyboard only and a screen reader; run axe in CI (`@axe-core/playwright`).
- i18n: `react-i18next` / FormatJS, never concatenate strings, use `Intl` for dates, numbers and currencies, support RTL if needed.

### 13. Testing strategy for React apps

- **Unit**: pure utils, reducers, hooks with logic (`renderHook`).
- **Integration (most value)**: render a page/feature with **MSW** mocking the network, interact like a user, assert what's on screen.
- **E2E**: critical flows (sign up, login, checkout) in Playwright against a staging environment.

```jsx
// MSW handler + integration test
import { http as mswHttp, HttpResponse } from "msw";
import { setupServer } from "msw/node";

const server = setupServer(
  mswHttp.get("*/products", () => HttpResponse.json([{ id: 1, name: "Phone", price: 20000 }]))
);
beforeAll(() => server.listen());
afterEach(() => server.resetHandlers());
afterAll(() => server.close());

test("shows products and handles server error", async () => {
  renderWithProviders(<ProductsPage />);
  expect(await screen.findByText("Phone")).toBeInTheDocument();

  server.use(mswHttp.get("*/products", () => new HttpResponse(null, { status: 500 })));
  await userEvent.click(screen.getByRole("button", { name: /refresh/i }));
  expect(await screen.findByRole("alert")).toHaveTextContent(/something went wrong/i);
});

// test-utils: wrap with the same providers as the app (fresh QueryClient per test)
function renderWithProviders(ui) {
  const qc = new QueryClient({ defaultOptions: { queries: { retry: false } } });
  return render(<QueryClientProvider client={qc}><MemoryRouter>{ui}</MemoryRouter></QueryClientProvider>);
}
```

### 14. Production React bugs & fixes

| Bug | Fix |
|---|---|
| Stale data after a mutation | Invalidate/update the right query keys |
| Search shows old results | Debounce + abort / query keys per search term |
| Double submit | Disable while pending, idempotency on server |
| Protected page flashes then redirects | Wait for auth to resolve before rendering/redirecting |
| Previous user's data visible after logout | Clear query cache & stores on logout |
| "Can't update state on unmounted component" / leaks | Cleanup effects, abort requests, cancel debounced fns |
| Infinite render/effect loops | Stable dependencies, derive instead of syncing state |
| Filters lost on refresh | Store them in the URL |
| Whole app white-screens on one error | Error boundaries per route/widget |
| Layout jumps while loading | Skeletons with fixed sizes, image dimensions |
| Hydration mismatch (SSR) | No `Date.now()`/`window` in render; client-only effects |
| Huge initial bundle | Route-level `lazy`, analyze bundle |

### 15. Production readiness checklist (React)

- [ ] API layer + query caching, no raw fetch in components
- [ ] Loading / empty / error / success states everywhere
- [ ] Route and widget error boundaries + Sentry with release & user context
- [ ] Auth: guarded routes, refresh-on-401, cache cleared on logout, server-side permission checks
- [ ] Forms: schema validation, server errors mapped to fields, no double submits, unsaved-changes warning
- [ ] Filters/pagination in URL
- [ ] Env validated; no secrets in client env vars; feature flags for risky features
- [ ] Code splitting, optimized images, virtualization for big lists, Web Vitals tracked
- [ ] Accessibility checked (keyboard, labels, focus, axe)
- [ ] Tests: MSW integration tests + E2E for critical flows
- [ ] ESLint (react-hooks), TypeScript strict, Prettier, CI

### Interview Qs

- **How do you structure data fetching in a large React app?** → API layer + TanStack Query with query key factories, invalidation on mutations.
- **How do you handle errors in React at scale?** → Boundaries per route/widget, mutation toasts, Sentry, retry UI.
- **How do you implement auth & protected routes? What happens on 401?**
- **Where should filter/pagination state live?** → URL search params.
- **What are optimistic updates and how do you roll back?**
- **How do you prevent showing stale data to a new user after logout?**
- **How do you map server validation errors into a form?**
- **What would you check before shipping a React feature to production?** (checklist above)

---

## 52. Real-time & Rich Interactions: WebSockets, Uploads with Progress, Drag & Drop

### Part 1 — WebSockets & Server-Sent Events in React

#### A robust `useWebSocket` hook (reconnect, backoff, heartbeat, cleanup)

```jsx
import { useEffect, useRef, useState, useCallback } from "react";

export function useWebSocket(url, { onMessage, enabled = true } = {}) {
  const [status, setStatus] = useState("connecting");   // connecting | open | closed
  const wsRef = useRef(null);
  const onMessageRef = useRef(onMessage);
  useEffect(() => { onMessageRef.current = onMessage; }, [onMessage]);  // latest handler, no reconnect on re-render

  useEffect(() => {
    if (!enabled) return;
    let attempt = 0;
    let reconnectTimer;
    let heartbeat;
    let closedByUs = false;

    function connect() {
      setStatus("connecting");
      const ws = new WebSocket(url);
      wsRef.current = ws;

      ws.onopen = () => {
        attempt = 0;
        setStatus("open");
        heartbeat = setInterval(() => ws.readyState === WebSocket.OPEN && ws.send(JSON.stringify({ type: "ping" })), 25_000);
      };
      ws.onmessage = (event) => {
        const msg = JSON.parse(event.data);
        if (msg.type !== "pong") onMessageRef.current?.(msg);
      };
      ws.onclose = () => {
        clearInterval(heartbeat);
        setStatus("closed");
        if (closedByUs) return;
        const delay = Math.min(30_000, 1000 * 2 ** attempt++) * (0.5 + Math.random() / 2);  // backoff + jitter
        reconnectTimer = setTimeout(connect, delay);
      };
      ws.onerror = () => ws.close();       // triggers onclose → reconnect
    }

    connect();
    return () => {                          // cleanup on unmount / url change
      closedByUs = true;
      clearTimeout(reconnectTimer);
      clearInterval(heartbeat);
      wsRef.current?.close();
    };
  }, [url, enabled]);

  const send = useCallback((data) => {
    if (wsRef.current?.readyState === WebSocket.OPEN) wsRef.current.send(JSON.stringify(data));
  }, []);

  return { status, send };
}
```

#### Wiring real-time events into TanStack Query

Let the socket **update or invalidate the cache** instead of keeping a parallel copy of the data in component state.

```jsx
function useLiveOrders() {
  const qc = useQueryClient();
  const query = useQuery({ queryKey: ["orders"], queryFn: fetchOrders });

  useWebSocket(`${WS_URL}/orders?token=${getToken()}`, {
    onMessage: (msg) => {
      if (msg.type === "order.updated") {
        qc.setQueryData(["orders"], (old = []) => old.map((o) => (o.id === msg.order.id ? msg.order : o)));
      } else if (msg.type === "order.created") {
        qc.invalidateQueries({ queryKey: ["orders"] });   // refetch to stay consistent
      }
    },
  });
  return query;
}
```

#### Server-Sent Events (one-way server → client)

```jsx
function useEventSource(url, onEvent) {
  const handler = useRef(onEvent);
  useEffect(() => { handler.current = onEvent; }, [onEvent]);
  useEffect(() => {
    const es = new EventSource(url, { withCredentials: true });   // auto-reconnects built in
    es.onmessage = (e) => handler.current(JSON.parse(e.data));
    return () => es.close();
  }, [url]);
}
// Great for notifications, progress updates, streaming AI responses.
```

`EventSource` is `GET`-only and can't send headers. For an AI chat (a `POST` prompt with an auth header, a streamed answer and a "Stop generating" button), use `fetch` with a stream parser: see `nodejs.md` → "Streaming Responses & Server-Sent Events in Depth" (tested `useChatStream` hook).

#### Real-time best practices

- **One connection per app** (share via context), not one per component.
- **Authenticate** the connection (short-lived token in the URL/first message or cookie); re-auth on reconnect.
- **Reconnect with exponential backoff + jitter**; show connection status to users when it matters ("Reconnecting…").
- **Resync after reconnect** (refetch or ask the server for missed events since the last event ID).
- **Throttle/batch** high-frequency updates (prices, cursors) — don't `setState` 100 times a second.
- Handle **out-of-order / duplicate** messages (versions/timestamps/IDs).
- Clean up sockets, intervals and listeners on unmount.

---

### Part 2 — File uploads with progress, preview & cancel

`fetch` has no **upload** progress events, so use **XMLHttpRequest** (or axios `onUploadProgress`, which uses XHR in browsers).

```jsx
function uploadFile(file, url, { onProgress, headers = {} } = {}) {
  const xhr = new XMLHttpRequest();
  const promise = new Promise((resolve, reject) => {
    xhr.upload.onprogress = (e) => { if (e.lengthComputable) onProgress?.(Math.round((e.loaded / e.total) * 100)); };
    xhr.onload = () => (xhr.status >= 200 && xhr.status < 300 ? resolve(xhr.response) : reject(new Error(`Upload failed (${xhr.status})`)));
    xhr.onerror = () => reject(new Error("Network error"));
    xhr.onabort = () => reject(new DOMException("Upload cancelled", "AbortError"));
    xhr.open("PUT", url);                                  // e.g. an S3 pre-signed URL
    Object.entries(headers).forEach(([k, v]) => xhr.setRequestHeader(k, v));
    xhr.send(file);
  });
  return { promise, cancel: () => xhr.abort() };
}
```

```jsx
const MAX_MB = 5;
const ALLOWED = ["image/jpeg", "image/png", "image/webp"];

function AvatarUploader({ onUploaded }) {
  const [file, setFile] = useState(null);
  const [preview, setPreview] = useState(null);
  const [progress, setProgress] = useState(0);
  const [error, setError] = useState(null);
  const [dragging, setDragging] = useState(false);
  const cancelRef = useRef(null);

  // Free the object URL when the preview changes/unmounts (avoid memory leaks)
  useEffect(() => () => { if (preview) URL.revokeObjectURL(preview); }, [preview]);

  function pick(f) {
    setError(null);
    if (!f) return;
    if (!ALLOWED.includes(f.type)) return setError("Only JPG, PNG or WebP images");
    if (f.size > MAX_MB * 1024 * 1024) return setError(`Max size is ${MAX_MB} MB`);
    setFile(f);
    setPreview(URL.createObjectURL(f));
  }

  async function upload() {
    try {
      const { uploadUrl, fileUrl } = await api.getUploadUrl({ type: file.type, size: file.size }); // server issues pre-signed URL
      const { promise, cancel } = uploadFile(file, uploadUrl, { onProgress: setProgress, headers: { "Content-Type": file.type } });
      cancelRef.current = cancel;
      await promise;
      onUploaded(fileUrl);
    } catch (e) {
      if (e.name !== "AbortError") setError(e.message);
      setProgress(0);
    } finally {
      cancelRef.current = null;
    }
  }

  return (
    <div
      onDragOver={(e) => { e.preventDefault(); setDragging(true); }}   // preventDefault is required to allow drop
      onDragLeave={() => setDragging(false)}
      onDrop={(e) => { e.preventDefault(); setDragging(false); pick(e.dataTransfer.files[0]); }}
      className={dragging ? "dropzone dropzone--active" : "dropzone"}
    >
      <label>
        Choose or drop an image
        <input type="file" accept={ALLOWED.join(",")} onChange={(e) => pick(e.target.files?.[0])} />
      </label>
      {preview && <img src={preview} alt="Preview" width={96} height={96} />}
      {progress > 0 && <progress value={progress} max={100} aria-label="Upload progress">{progress}%</progress>}
      {error && <p role="alert">{error}</p>}
      <button onClick={upload} disabled={!file || !!cancelRef.current}>Upload</button>
      {cancelRef.current && <button onClick={() => cancelRef.current()}>Cancel</button>}
    </div>
  );
}
```

Upload best practices:
- Validate type & size on the client (UX) **and** the server (security).
- Upload **directly to object storage** with pre-signed URLs (server never streams the bytes).
- Large files: **multipart/resumable uploads** (S3 multipart, tus protocol) so failures resume instead of restarting.
- Multiple files: limit concurrency (e.g. 3 at a time), per-file progress and retry.
- Revoke object URLs; compress/resize images client-side when appropriate.
- Accessible: real `<input type="file">` with a label; drag & drop as an enhancement, not the only way.

---

### Part 3 — Drag & drop

#### Native HTML5 drag & drop (simple reordering)

```jsx
function ReorderableList({ items, onReorder }) {
  const [dragIndex, setDragIndex] = useState(null);

  return (
    <ul>
      {items.map((item, index) => (
        <li
          key={item.id}
          draggable
          onDragStart={(e) => { setDragIndex(index); e.dataTransfer.effectAllowed = "move"; }}
          onDragOver={(e) => e.preventDefault()}             // allow dropping here
          onDrop={() => {
            if (dragIndex === null || dragIndex === index) return;
            const next = [...items];
            const [moved] = next.splice(dragIndex, 1);
            next.splice(index, 0, moved);
            onReorder(next);
            setDragIndex(null);
          }}
          style={{ opacity: dragIndex === index ? 0.5 : 1 }}
        >
          {item.label}
        </li>
      ))}
    </ul>
  );
}
```

Native DnD limitations: **no touch support on many mobile browsers**, **no keyboard support** (accessibility fail), hard to style the drag preview, inconsistent events.

#### dnd-kit (recommended for React) — accessible, touch + keyboard

```jsx
import { DndContext, closestCenter, PointerSensor, KeyboardSensor, useSensor, useSensors } from "@dnd-kit/core";
import { SortableContext, useSortable, arrayMove, verticalListSortingStrategy, sortableKeyboardCoordinates } from "@dnd-kit/sortable";
import { CSS } from "@dnd-kit/utilities";

function SortableItem({ id, children }) {
  const { attributes, listeners, setNodeRef, transform, transition, isDragging } = useSortable({ id });
  return (
    <li
      ref={setNodeRef}
      style={{ transform: CSS.Transform.toString(transform), transition, opacity: isDragging ? 0.6 : 1 }}
      {...attributes}                                     // role, tabIndex, aria-* for keyboard/screen readers
      {...listeners}                                      // pointer/keyboard handlers
    >
      {children}
    </li>
  );
}

function SortableTodoList({ todos, setTodos, onPersistOrder }) {
  const sensors = useSensors(
    useSensor(PointerSensor, { activationConstraint: { distance: 5 } }),       // don't hijack normal clicks
    useSensor(KeyboardSensor, { coordinateGetter: sortableKeyboardCoordinates }) // Space to pick up, arrows to move
  );

  function handleDragEnd({ active, over }) {
    if (!over || active.id === over.id) return;
    const oldIndex = todos.findIndex((t) => t.id === active.id);
    const newIndex = todos.findIndex((t) => t.id === over.id);
    const next = arrayMove(todos, oldIndex, newIndex);
    setTodos(next);                                        // optimistic UI
    onPersistOrder(next.map((t) => t.id));                 // save order to the server (rollback on failure)
  }

  return (
    <DndContext sensors={sensors} collisionDetection={closestCenter} onDragEnd={handleDragEnd}>
      <SortableContext items={todos.map((t) => t.id)} strategy={verticalListSortingStrategy}>
        <ul>{todos.map((t) => <SortableItem key={t.id} id={t.id}>{t.title}</SortableItem>)}</ul>
      </SortableContext>
    </DndContext>
  );
}
```

Other libraries: **Pragmatic drag and drop** (Atlassian, framework-agnostic, powers Jira/Trello-like boards), **react-dnd**. `react-beautiful-dnd` is deprecated.

Drag & drop best practices:
- Always offer a **keyboard alternative** (dnd-kit's keyboard sensor, or "Move up/down" buttons).
- Announce moves for screen readers (dnd-kit has live-region announcements).
- **Persist order** on the server with optimistic updates + rollback (store a `position`/rank field; fractional indexing avoids renumbering every row).
- Use an activation distance/delay so clicks and scrolling on touch devices still work.
- Keep dragged items' visual feedback clear (placeholder, drop indicator).

### Interview Qs

1. How would you build a reliable WebSocket connection in React? (reconnect, backoff, heartbeat, cleanup, single shared connection)
2. How do you combine real-time updates with a server-state cache like TanStack Query?
3. WebSocket vs SSE vs polling — which for notifications, chat, live prices?
4. How do you show upload progress? Why not `fetch`?
5. How do you upload large files safely? (pre-signed URLs, multipart/resumable, validation on server)
6. Why call `URL.revokeObjectURL`?
7. How does native drag & drop work (`draggable`, `dragover` + `preventDefault`, `drop`)? What are its limitations?
8. How do you make drag & drop accessible?
9. How would you persist the order of a reorderable list? (positions, optimistic update, fractional indexing)

---

## 53. Machine Coding Questions

Common React machine-coding rounds with compact solutions.

### 1. Todo App (add, toggle, delete, filter)

```jsx
function TodoApp() {
  const [todos, setTodos] = useState([]);
  const [text, setText] = useState("");
  const [filter, setFilter] = useState("all");

  const add = (e) => {
    e.preventDefault();
    if (!text.trim()) return;
    setTodos((t) => [...t, { id: crypto.randomUUID(), text: text.trim(), done: false }]);
    setText("");
  };
  const toggle = (id) => setTodos((t) => t.map((x) => (x.id === id ? { ...x, done: !x.done } : x)));
  const remove = (id) => setTodos((t) => t.filter((x) => x.id !== id));

  const visible = todos.filter((t) => (filter === "all" ? true : filter === "done" ? t.done : !t.done));

  return (
    <div>
      <form onSubmit={add}>
        <input value={text} onChange={(e) => setText(e.target.value)} placeholder="What to do?" />
        <button>Add</button>
      </form>
      {["all", "active", "done"].map((f) => (
        <button key={f} disabled={filter === f} onClick={() => setFilter(f)}>{f}</button>
      ))}
      <ul>
        {visible.map((t) => (
          <li key={t.id}>
            <input type="checkbox" checked={t.done} onChange={() => toggle(t.id)} />
            <span style={{ textDecoration: t.done ? "line-through" : "none" }}>{t.text}</span>
            <button onClick={() => remove(t.id)}>✕</button>
          </li>
        ))}
      </ul>
      <p>{todos.filter((t) => !t.done).length} items left</p>
    </div>
  );
}
```

### 2. Search with debounce (autocomplete)

```jsx
function Autocomplete() {
  const [query, setQuery] = useState("");
  const [results, setResults] = useState([]);
  const [loading, setLoading] = useState(false);
  const [active, setActive] = useState(-1);
  const debounced = useDebounce(query, 300);

  useEffect(() => {
    if (!debounced) return setResults([]);
    const controller = new AbortController();
    setLoading(true);
    fetch(`https://dummyjson.com/products/search?q=${encodeURIComponent(debounced)}`, { signal: controller.signal })
      .then((r) => r.json())
      .then((d) => setResults(d.products))
      .catch(() => {})
      .finally(() => setLoading(false));
    return () => controller.abort();
  }, [debounced]);

  const onKeyDown = (e) => {
    if (e.key === "ArrowDown") setActive((a) => Math.min(a + 1, results.length - 1));
    if (e.key === "ArrowUp") setActive((a) => Math.max(a - 1, 0));
    if (e.key === "Enter" && active >= 0) setQuery(results[active].title);
  };

  return (
    <div>
      <input value={query} onChange={(e) => setQuery(e.target.value)} onKeyDown={onKeyDown} />
      {loading && <p>Loading…</p>}
      <ul>
        {results.map((r, i) => (
          <li key={r.id} style={{ background: i === active ? "#eee" : "" }} onClick={() => setQuery(r.title)}>
            {r.title}
          </li>
        ))}
      </ul>
    </div>
  );
}
```

This version works with a mouse but isn't accessible: no label, no combobox roles, and the highlighted option isn't announced. The accessible version (label, `role="combobox"`, `aria-activedescendant`, a result-count status region) is in Section 47.

### 3. Infinite scroll

```jsx
function InfiniteList() {
  const [items, setItems] = useState([]);
  const [page, setPage] = useState(1);
  const [hasMore, setHasMore] = useState(true);
  const [loading, setLoading] = useState(false);
  const loaderRef = useRef(null);

  useEffect(() => {
    setLoading(true);
    fetch(`/api/items?page=${page}`)
      .then((r) => r.json())
      .then((data) => {
        setItems((prev) => [...prev, ...data.items]);
        setHasMore(data.hasMore);
      })
      .finally(() => setLoading(false));
  }, [page]);

  useEffect(() => {
    const el = loaderRef.current;
    if (!el) return;
    const obs = new IntersectionObserver(([entry]) => {
      if (entry.isIntersecting && hasMore && !loading) setPage((p) => p + 1);
    }, { rootMargin: "200px" });
    obs.observe(el);
    return () => obs.disconnect();
  }, [hasMore, loading]);

  return (
    <>
      {items.map((it) => <div key={it.id}>{it.title}</div>)}
      {hasMore && <div ref={loaderRef}>{loading ? "Loading…" : ""}</div>}
    </>
  );
}
```

### 4. Pagination

```jsx
function Paginated({ items, pageSize = 10 }) {
  const [page, setPage] = useState(1);
  const totalPages = Math.ceil(items.length / pageSize);
  const current = items.slice((page - 1) * pageSize, page * pageSize);
  return (
    <>
      {current.map((i) => <p key={i.id}>{i.name}</p>)}
      <button disabled={page === 1} onClick={() => setPage((p) => p - 1)}>Prev</button>
      {Array.from({ length: totalPages }, (_, i) => (
        <button key={i} onClick={() => setPage(i + 1)} style={{ fontWeight: page === i + 1 ? "bold" : "normal" }}>
          {i + 1}
        </button>
      ))}
      <button disabled={page === totalPages} onClick={() => setPage((p) => p + 1)}>Next</button>
    </>
  );
}
```

### 5. Star rating

```jsx
function StarRating({ max = 5, value, onChange }) {
  const [hover, setHover] = useState(0);
  return (
    <div role="radiogroup">
      {Array.from({ length: max }, (_, i) => i + 1).map((star) => (
        <span
          key={star}
          role="radio"
          aria-checked={value === star}
          style={{ cursor: "pointer", color: star <= (hover || value) ? "gold" : "gray", fontSize: 24 }}
          onClick={() => onChange(star)}
          onMouseEnter={() => setHover(star)}
          onMouseLeave={() => setHover(0)}
        >
          ★
        </span>
      ))}
    </div>
  );
}
```

### 6. Accordion

```jsx
function Accordion({ items, allowMultiple = false }) {
  const [open, setOpen] = useState(new Set());
  const toggle = (id) =>
    setOpen((prev) => {
      const next = new Set(allowMultiple ? prev : []);
      prev.has(id) ? next.delete(id) : next.add(id);
      return next;
    });
  return items.map((item) => (
    <div key={item.id}>
      <button aria-expanded={open.has(item.id)} onClick={() => toggle(item.id)}>{item.title}</button>
      {open.has(item.id) && <div>{item.content}</div>}
    </div>
  ));
}
```

### 7. Nested comments / file explorer (recursive component)

```jsx
function FileTree({ node, depth = 0 }) {
  const [open, setOpen] = useState(false);
  if (!node.children) return <div style={{ paddingLeft: depth * 16 }}>📄 {node.name}</div>;
  return (
    <div>
      <div style={{ paddingLeft: depth * 16, cursor: "pointer" }} onClick={() => setOpen(!open)}>
        {open ? "📂" : "📁"} {node.name}
      </div>
      {open && node.children.map((child) => <FileTree key={child.name} node={child} depth={depth + 1} />)}
    </div>
  );
}
```

### 8. Countdown timer / OTP input / progress bar

```jsx
function Countdown({ seconds }) {
  const [left, setLeft] = useState(seconds);
  useEffect(() => {
    if (left <= 0) return;
    const id = setTimeout(() => setLeft((l) => l - 1), 1000);
    return () => clearTimeout(id);
  }, [left]);
  const mm = String(Math.floor(left / 60)).padStart(2, "0");
  const ss = String(left % 60).padStart(2, "0");
  return <p>{mm}:{ss}</p>;
}

function OtpInput({ length = 4, onComplete }) {
  const [values, setValues] = useState(Array(length).fill(""));
  const refs = useRef([]);
  const handleChange = (i, v) => {
    if (!/^\d?$/.test(v)) return;
    const next = [...values];
    next[i] = v;
    setValues(next);
    if (v && i < length - 1) refs.current[i + 1].focus();
    if (next.every(Boolean)) onComplete(next.join(""));
  };
  const handleKeyDown = (i, e) => {
    if (e.key === "Backspace" && !values[i] && i > 0) refs.current[i - 1].focus();
  };
  return values.map((v, i) => (
    <input
      key={i}
      ref={(el) => (refs.current[i] = el)}
      value={v}
      maxLength={1}
      inputMode="numeric"
      onChange={(e) => handleChange(i, e.target.value)}
      onKeyDown={(e) => handleKeyDown(i, e)}
      style={{ width: 40, textAlign: "center" }}
    />
  ));
}

function ProgressBar({ value }) {
  const pct = Math.min(100, Math.max(0, value));
  return (
    <div role="progressbar" aria-valuenow={pct} aria-valuemin={0} aria-valuemax={100} style={{ background: "#eee" }}>
      <div style={{ width: `${pct}%`, background: "green", height: 8, transition: "width .3s" }} />
    </div>
  );
}
```

### 9. Modal with focus management

```jsx
function Dialog({ open, onClose, title, children }) {
  const ref = useRef(null);
  useEffect(() => {
    const d = ref.current;
    if (open) d.showModal();   // native <dialog> handles focus trap + Escape
    else d.close();
  }, [open]);
  return (
    <dialog ref={ref} onClose={onClose} aria-labelledby="dlg-title">
      <h2 id="dlg-title">{title}</h2>
      {children}
      <button onClick={onClose}>Close</button>
    </dialog>
  );
}
```

Section 47 has a fuller version: backdrop-click closing, scroll lock, and choosing the initial focus. React's `autoFocus` prop is ignored by `showModal()`.

### 10. Other common rounds

Image carousel, tic-tac-toe, traffic light, stopwatch, kanban drag & drop, shopping cart, multi-step form, dark-mode toggle with context, data table with sort/filter/pagination, chips input, toast notifications, typeahead with caching, poll widget, Snake game, calculator.

```jsx
// Tic-tac-toe winner check
const LINES = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
function winner(sq) {
  for (const [a, b, c] of LINES) if (sq[a] && sq[a] === sq[b] && sq[a] === sq[c]) return sq[a];
  return null;
}
function TicTacToe() {
  const [sq, setSq] = useState(Array(9).fill(null));
  const [xNext, setXNext] = useState(true);
  const w = winner(sq);                           // derived, not stored
  const play = (i) => {
    if (sq[i] || w) return;
    const next = sq.slice();
    next[i] = xNext ? "X" : "O";
    setSq(next);
    setXNext(!xNext);
  };
  return (
    <>
      <p>{w ? `Winner: ${w}` : sq.every(Boolean) ? "Draw" : `Next: ${xNext ? "X" : "O"}`}</p>
      <div style={{ display: "grid", gridTemplateColumns: "repeat(3, 60px)" }}>
        {sq.map((v, i) => <button key={i} style={{ height: 60 }} onClick={() => play(i)}>{v}</button>)}
      </div>
      <button onClick={() => { setSq(Array(9).fill(null)); setXNext(true); }}>Restart</button>
    </>
  );
}
```

---

## 54. Machine Coding II (Carousel, Kanban, Data Table, Wizard, Toasts, Comments)

### How machine-coding rounds are judged

1. **Clarify requirements** first (2–3 min): must-haves vs nice-to-haves, data shape, edge cases.
2. **Plan components & state** out loud: what's state, what's derived, where it lives.
3. **Get a working version early**, then improve (styling last).
4. **Separate logic from UI**: pure functions/reducers for the rules → easy to reason about and test.
5. **Handle edge cases**: empty data, loading/error, boundaries (first/last), rapid clicks.
6. **Accessibility**: semantic elements, labels, keyboard support, `aria-*`.
7. **Clean code**: small components, good names, no duplicated state, cleanup of timers/listeners.

---

### 1. Image carousel (autoplay, pause on hover, keyboard, dots)

```jsx
export const wrapIndex = (i, length) => ((i % length) + length) % length;   // -1 → last, length → 0

function Carousel({ images, interval = 3000 }) {
  const [index, setIndex] = useState(0);
  const [paused, setPaused] = useState(false);
  const count = images.length;

  const go = useCallback((delta) => setIndex((i) => wrapIndex(i + delta, count)), [count]);

  useEffect(() => {
    if (paused || count < 2) return;
    const id = setInterval(() => go(1), interval);
    return () => clearInterval(id);                     // restart timer when paused/interval changes
  }, [paused, interval, count, go]);

  if (count === 0) return <p>No images</p>;

  return (
    <section
      aria-roledescription="carousel"
      aria-label="Product images"
      tabIndex={0}
      onMouseEnter={() => setPaused(true)}
      onMouseLeave={() => setPaused(false)}
      onFocus={() => setPaused(true)}
      onBlur={() => setPaused(false)}
      onKeyDown={(e) => {
        if (e.key === "ArrowRight") go(1);
        if (e.key === "ArrowLeft") go(-1);
      }}
    >
      <img src={images[index].src} alt={images[index].alt} width={600} height={400} />
      <button onClick={() => go(-1)} aria-label="Previous slide">‹</button>
      <button onClick={() => go(1)} aria-label="Next slide">›</button>
      <div role="tablist" aria-label="Choose slide">
        {images.map((img, i) => (
          <button
            key={img.src}
            role="tab"
            aria-selected={i === index}
            aria-label={`Slide ${i + 1} of ${count}`}
            onClick={() => setIndex(i)}
          >
            {i === index ? "●" : "○"}
          </button>
        ))}
      </div>
      <p aria-live="polite" className="sr-only">Slide {index + 1} of {count}</p>
    </section>
  );
}
```

Follow-ups: lazy-load non-visible images, swipe on touch (pointer events), respect `prefers-reduced-motion` (no autoplay), infinite loop with transitions (clone first/last slides).

### 2. Kanban board (move cards between columns)

Normalized state: columns hold **card IDs**, cards stored once by ID.

```js
// pure logic — easy to test
export function moveCard(board, cardId, toColumn, toIndex) {
  const fromColumn = Object.keys(board.columns).find((c) => board.columns[c].includes(cardId));
  if (!fromColumn || !(toColumn in board.columns)) return board;

  const columns = { ...board.columns };
  columns[fromColumn] = columns[fromColumn].filter((id) => id !== cardId);
  const target = [...columns[toColumn]];
  const index = toIndex === undefined ? target.length : Math.max(0, Math.min(toIndex, target.length));
  target.splice(index, 0, cardId);
  columns[toColumn] = target;
  return { ...board, columns };
}

export function addCard(board, column, title, id = crypto.randomUUID()) {
  return {
    cards: { ...board.cards, [id]: { id, title } },
    columns: { ...board.columns, [column]: [...board.columns[column], id] },
  };
}
```

```jsx
const initialBoard = {
  cards: { c1: { id: "c1", title: "Design login" }, c2: { id: "c2", title: "Build API" } },
  columns: { todo: ["c1", "c2"], doing: [], done: [] },
};
const COLUMN_TITLES = { todo: "To do", doing: "In progress", done: "Done" };

function Kanban() {
  const [board, setBoard] = useState(initialBoard);
  const [dragged, setDragged] = useState(null);

  return (
    <div style={{ display: "grid", gridTemplateColumns: "repeat(3, 1fr)", gap: 16 }}>
      {Object.entries(board.columns).map(([columnId, cardIds]) => (
        <section
          key={columnId}
          aria-label={COLUMN_TITLES[columnId]}
          onDragOver={(e) => e.preventDefault()}
          onDrop={() => { if (dragged) setBoard((b) => moveCard(b, dragged, columnId)); setDragged(null); }}
        >
          <h2>{COLUMN_TITLES[columnId]} ({cardIds.length})</h2>
          {cardIds.map((id) => (
            <article key={id} draggable onDragStart={() => setDragged(id)}>
              {board.cards[id].title}
              {/* keyboard/touch alternative to drag & drop */}
              <select
                aria-label={`Move "${board.cards[id].title}" to`}
                value={columnId}
                onChange={(e) => setBoard((b) => moveCard(b, id, e.target.value))}
              >
                {Object.keys(board.columns).map((c) => <option key={c} value={c}>{COLUMN_TITLES[c]}</option>)}
              </select>
            </article>
          ))}
          <AddCardForm onAdd={(title) => setBoard((b) => addCard(b, columnId, title))} />
        </section>
      ))}
    </div>
  );
}
```

Follow-ups: persist to localStorage/server with optimistic updates, reorder within a column (drop position), dnd-kit for accessibility (see Real-time & Rich Interactions).

### 3. Data table (search, sort, pagination)

```js
// pure: derive visible rows from data + table state
export function getVisibleRows(rows, { query = "", sortKey = null, sortDir = "asc", page = 1, pageSize = 10, searchKeys = [] }) {
  const q = query.trim().toLowerCase();
  const filtered = q
    ? rows.filter((row) => searchKeys.some((k) => String(row[k] ?? "").toLowerCase().includes(q)))
    : rows;

  const sorted = sortKey
    ? filtered.toSorted((a, b) => {
        const x = a[sortKey], y = b[sortKey];
        const cmp = typeof x === "number" && typeof y === "number" ? x - y : String(x).localeCompare(String(y));
        return sortDir === "asc" ? cmp : -cmp;
      })
    : filtered;

  const totalPages = Math.max(1, Math.ceil(sorted.length / pageSize));
  const safePage = Math.min(Math.max(1, page), totalPages);
  return {
    rows: sorted.slice((safePage - 1) * pageSize, safePage * pageSize),
    total: sorted.length,
    totalPages,
    page: safePage,
  };
}

export const nextSort = (current, key) =>
  current.sortKey !== key ? { sortKey: key, sortDir: "asc" }
  : current.sortDir === "asc" ? { sortKey: key, sortDir: "desc" }
  : { sortKey: null, sortDir: "asc" };                       // third click clears sorting
```

```jsx
const COLUMNS = [
  { key: "name", label: "Name" },
  { key: "email", label: "Email" },
  { key: "age", label: "Age" },
];

function UsersTable({ users }) {
  const [query, setQuery] = useState("");
  const [sort, setSort] = useState({ sortKey: null, sortDir: "asc" });
  const [page, setPage] = useState(1);
  const deferredQuery = useDeferredValue(query);             // keep typing smooth on big tables

  const view = useMemo(
    () => getVisibleRows(users, { query: deferredQuery, ...sort, page, pageSize: 10, searchKeys: ["name", "email"] }),
    [users, deferredQuery, sort, page]
  );

  return (
    <>
      <input
        type="search"
        aria-label="Search users"
        value={query}
        onChange={(e) => { setQuery(e.target.value); setPage(1); }}   // reset page on new search
      />
      <table>
        <thead>
          <tr>
            {COLUMNS.map((col) => (
              <th
                key={col.key}
                aria-sort={sort.sortKey === col.key ? (sort.sortDir === "asc" ? "ascending" : "descending") : "none"}
              >
                <button onClick={() => setSort((s) => nextSort(s, col.key))}>
                  {col.label} {sort.sortKey === col.key ? (sort.sortDir === "asc" ? "▲" : "▼") : ""}
                </button>
              </th>
            ))}
          </tr>
        </thead>
        <tbody>
          {view.rows.length === 0 ? (
            <tr><td colSpan={COLUMNS.length}>No users found</td></tr>
          ) : (
            view.rows.map((u) => (
              <tr key={u.id}>{COLUMNS.map((c) => <td key={c.key}>{u[c.key]}</td>)}</tr>
            ))
          )}
        </tbody>
      </table>
      <nav aria-label="Pagination">
        <button disabled={view.page === 1} onClick={() => setPage(view.page - 1)}>Previous</button>
        <span> Page {view.page} of {view.totalPages} ({view.total} users) </span>
        <button disabled={view.page === view.totalPages} onClick={() => setPage(view.page + 1)}>Next</button>
      </nav>
    </>
  );
}
```

Follow-ups: server-side sorting/filtering/pagination with query params in the URL (TanStack Query + `useSearchParams`), row selection, column resizing, virtualization for 10k+ rows, TanStack Table for complex grids.

### 4. Multi-step form wizard (validation per step)

```js
// pure validators per step
export const STEPS = [
  { id: "account", fields: ["email", "password"], validate: (d) => ({
      ...(!/^\S+@\S+\.\S+$/.test(d.email ?? "") && { email: "Enter a valid email" }),
      ...((d.password ?? "").length < 8 && { password: "Min 8 characters" }),
    }) },
  { id: "profile", fields: ["name", "phone"], validate: (d) => ({
      ...(!(d.name ?? "").trim() && { name: "Name is required" }),
      ...(!/^[6-9]\d{9}$/.test(d.phone ?? "") && { phone: "Enter a valid 10-digit mobile number" }),
    }) },
  { id: "review", fields: [], validate: () => ({}) },
];

export function wizardReducer(state, action) {
  switch (action.type) {
    case "change":
      return { ...state, data: { ...state.data, [action.field]: action.value }, errors: { ...state.errors, [action.field]: undefined } };
    case "next": {
      const errors = STEPS[state.step].validate(state.data);
      if (Object.keys(errors).length) return { ...state, errors };            // stay, show errors
      return { ...state, errors: {}, step: Math.min(state.step + 1, STEPS.length - 1) };
    }
    case "back":
      return { ...state, errors: {}, step: Math.max(state.step - 1, 0) };      // data is kept
    case "submitting": return { ...state, status: "submitting" };
    case "submitted": return { ...state, status: "done" };
    case "failed": return { ...state, status: "idle", submitError: action.message };
    default: return state;
  }
}
```

```jsx
function SignupWizard({ onSubmit }) {
  const [state, dispatch] = useReducer(wizardReducer, { step: 0, data: {}, errors: {}, status: "idle" });
  const step = STEPS[state.step];
  const isLast = state.step === STEPS.length - 1;

  async function handleSubmit(e) {
    e.preventDefault();
    if (!isLast) return dispatch({ type: "next" });
    dispatch({ type: "submitting" });
    try {
      await onSubmit(state.data);
      dispatch({ type: "submitted" });
    } catch (err) {
      dispatch({ type: "failed", message: err.message });
    }
  }

  if (state.status === "done") return <p role="status">Account created 🎉</p>;

  return (
    <form onSubmit={handleSubmit} noValidate>
      <p>Step {state.step + 1} of {STEPS.length}</p>
      <progress value={state.step + 1} max={STEPS.length} />

      {step.fields.map((field) => (
        <label key={field}>
          {field}
          <input
            name={field}
            type={field === "password" ? "password" : "text"}
            value={state.data[field] ?? ""}
            aria-invalid={!!state.errors[field]}
            onChange={(e) => dispatch({ type: "change", field, value: e.target.value })}
          />
          {state.errors[field] && <span role="alert">{state.errors[field]}</span>}
        </label>
      ))}

      {step.id === "review" && <pre>{JSON.stringify({ ...state.data, password: "••••••••" }, null, 2)}</pre>}
      {state.submitError && <p role="alert">{state.submitError}</p>}

      <button type="button" onClick={() => dispatch({ type: "back" })} disabled={state.step === 0}>Back</button>
      <button type="submit" disabled={state.status === "submitting"}>
        {isLast ? (state.status === "submitting" ? "Creating…" : "Create account") : "Next"}
      </button>
    </form>
  );
}
```

Follow-ups: move focus to the first error or the step heading on step change, persist progress in sessionStorage/URL (`?step=2`), async validation (email taken?), React Hook Form + Zod per-step schemas.

### 5. Toast notification system (context + hook)

```js
export function toastsReducer(toasts, action) {
  switch (action.type) {
    case "add": return [...toasts, action.toast].slice(-3);          // keep at most 3 visible
    case "remove": return toasts.filter((t) => t.id !== action.id);
    default: return toasts;
  }
}
```

```jsx
const ToastContext = createContext(null);

export function ToastProvider({ children }) {
  const [toasts, dispatch] = useReducer(toastsReducer, []);
  const timers = useRef(new Map());

  const remove = useCallback((id) => {
    clearTimeout(timers.current.get(id));
    timers.current.delete(id);
    dispatch({ type: "remove", id });
  }, []);

  const show = useCallback((message, { type = "info", duration = 4000 } = {}) => {
    const id = crypto.randomUUID();
    dispatch({ type: "add", toast: { id, message, type } });
    if (duration > 0) timers.current.set(id, setTimeout(() => remove(id), duration));
    return id;
  }, [remove]);

  useEffect(() => () => timers.current.forEach(clearTimeout), []);   // clear all timers on unmount

  const api = useMemo(() => ({
    show,
    success: (m, o) => show(m, { ...o, type: "success" }),
    error: (m, o) => show(m, { ...o, type: "error", duration: 8000 }),
    dismiss: remove,
  }), [show, remove]);

  return (
    <ToastContext.Provider value={api}>
      {children}
      {createPortal(
        <div className="toast-region" role="region" aria-label="Notifications">
          {toasts.map((t) => (
            <div key={t.id} className={`toast toast--${t.type}`} role={t.type === "error" ? "alert" : "status"}>
              {t.message}
              <button onClick={() => remove(t.id)} aria-label="Dismiss notification">×</button>
            </div>
          ))}
        </div>,
        document.body
      )}
    </ToastContext.Provider>
  );
}

export function useToast() {
  const ctx = useContext(ToastContext);
  if (!ctx) throw new Error("useToast must be used inside <ToastProvider>");
  return ctx;
}

// usage
function SaveButton() {
  const toast = useToast();
  return <button onClick={async () => {
    try { await save(); toast.success("Saved"); } catch { toast.error("Could not save"); }
  }}>Save</button>;
}
```

Follow-ups: pause timers on hover, animations with `AnimatePresence`, dedupe identical messages, promise toasts (`loading → success/error`).

### 6. Nested comments with reply, edit & delete

```js
// pure tree helpers
export function addReply(comments, parentId, reply) {
  if (parentId === null) return [...comments, reply];
  return comments.map((c) =>
    c.id === parentId
      ? { ...c, replies: [...c.replies, reply] }
      : { ...c, replies: addReply(c.replies, parentId, reply) }
  );
}

export function updateComment(comments, id, text) {
  return comments.map((c) =>
    c.id === id ? { ...c, text } : { ...c, replies: updateComment(c.replies, id, text) }
  );
}

export function deleteComment(comments, id) {
  return comments
    .filter((c) => c.id !== id)
    .map((c) => ({ ...c, replies: deleteComment(c.replies, id) }));
}

export const countComments = (comments) => comments.reduce((n, c) => n + 1 + countComments(c.replies), 0);
```

```jsx
function CommentThread() {
  const [comments, setComments] = useState([]);
  const newComment = (text) => ({ id: crypto.randomUUID(), text, replies: [] });

  return (
    <section aria-label={`Comments (${countComments(comments)})`}>
      <CommentForm onSubmit={(text) => setComments((cs) => addReply(cs, null, newComment(text)))} />
      <CommentList
        comments={comments}
        onReply={(parentId, text) => setComments((cs) => addReply(cs, parentId, newComment(text)))}
        onEdit={(id, text) => setComments((cs) => updateComment(cs, id, text))}
        onDelete={(id) => setComments((cs) => deleteComment(cs, id))}
      />
    </section>
  );
}

function CommentList({ comments, depth = 0, ...handlers }) {
  return (
    <ul style={{ paddingLeft: depth ? 20 : 0 }}>
      {comments.map((c) => <CommentItem key={c.id} comment={c} depth={depth} {...handlers} />)}
    </ul>
  );
}

function CommentItem({ comment, depth, onReply, onEdit, onDelete }) {
  const [mode, setMode] = useState(null);           // null | "reply" | "edit"
  return (
    <li>
      {mode === "edit" ? (
        <CommentForm initial={comment.text} onSubmit={(t) => { onEdit(comment.id, t); setMode(null); }} onCancel={() => setMode(null)} />
      ) : (
        <p>{comment.text}</p>
      )}
      <button onClick={() => setMode("reply")}>Reply</button>
      <button onClick={() => setMode("edit")}>Edit</button>
      <button onClick={() => onDelete(comment.id)}>Delete</button>
      {mode === "reply" && (
        <CommentForm onSubmit={(t) => { onReply(comment.id, t); setMode(null); }} onCancel={() => setMode(null)} />
      )}
      {comment.replies.length > 0 && (
        <CommentList comments={comment.replies} depth={depth + 1} onReply={onReply} onEdit={onEdit} onDelete={onDelete} />
      )}
    </li>
  );
}

function CommentForm({ initial = "", onSubmit, onCancel }) {
  const [text, setText] = useState(initial);
  return (
    <form onSubmit={(e) => { e.preventDefault(); if (text.trim()) { onSubmit(text.trim()); setText(""); } }}>
      <textarea aria-label="Comment" value={text} onChange={(e) => setText(e.target.value)} />
      <button type="submit">Post</button>
      {onCancel && <button type="button" onClick={onCancel}>Cancel</button>}
    </form>
  );
}
```

Follow-ups: flat storage with `parentId` + build the tree with a Map (O(n)), collapse threads, limit nesting depth, optimistic server updates, "soft delete" that keeps replies ("[deleted]").

### Interview Qs

1. How do you structure state for a kanban board? Why normalize?
2. Why keep sorting/filtering/pagination as derived data instead of state?
3. What accessibility features does a carousel/table/wizard/toast need?
4. How do you avoid timer leaks in autoplay carousels and toast systems?
5. How do you update a deeply nested tree immutably?
6. How would you make the data table work with 100k rows? (server-side pagination, virtualization)
7. How do you preserve wizard data when the user goes back or refreshes?

---

## 55. Output / Behaviour Questions

**Q1. What does this show after one click?**
```jsx
function App() {
  const [n, setN] = useState(0);
  return <button onClick={() => { setN(n + 1); setN(n + 1); }}>{n}</button>;
}
```
> `1` — both use the same snapshot `n = 0`.

**Q2.**
```jsx
const handle = () => {
  setN((n) => n + 1);
  setN(n + 5);
  setN((n) => n + 1);
};
// n starts at 0
```
> `6` — queue: `0+1=1`, replace with `0+5=5`, `5+1=6`.

**Q3. What gets logged?**
```jsx
function App() {
  const [count, setCount] = useState(0);
  const click = () => { setCount(count + 1); console.log(count); };
  return <button onClick={click}>+</button>;
}
```
> Logs `0` the first click (old snapshot).

**Q4. How many renders?**
```jsx
useEffect(() => {
  setA(1); setB(2); setC(3);
}, []);
```
> One additional render (batched).

**Q5. Order of logs on mount?**
```jsx
function Child() {
  useEffect(() => console.log("child effect"));
  console.log("child render");
  return null;
}
function Parent() {
  useEffect(() => console.log("parent effect"));
  console.log("parent render");
  return <Child />;
}
```
> `parent render, child render, child effect, parent effect` — effects run children first (bottom-up).

**Q6. Does `Child` re-render when the button is clicked?**
```jsx
const Child = memo(({ onClick }) => <button onClick={onClick}>child</button>);
function Parent() {
  const [c, setC] = useState(0);
  return <><button onClick={() => setC(c + 1)}>{c}</button><Child onClick={() => {}} /></>;
}
```
> Yes — new function each render breaks memo. Use `useCallback`.

**Q7. What's rendered?**
```jsx
const items = [];
return <div>{items.length && <List />}</div>;
```
> `0`.

**Q8. Infinite loop?**
```jsx
const [data, setData] = useState([]);
useEffect(() => { setData([]); }, [data]);
```
> Yes — `[]` is a new reference each time → effect re-runs forever.

**Q9. What does the input show after typing when the state is set to the same value?**
```jsx
const [v, setV] = useState("");
<input value={v} onChange={() => setV("fixed")} />
```
> Always "fixed" — it's controlled; typing can't change it beyond what state says.

**Q10. Interval stuck at 1?**
```jsx
useEffect(() => {
  const id = setInterval(() => setCount(count + 1), 1000);
  return () => clearInterval(id);
}, []);
```
> Yes — stale closure; `count` is always 0. Use `setCount(c => c + 1)`.

---

## 56. Most Asked Interview Questions

### Basics

1. **What is React? Why use it?**
2. **What is JSX? How does the browser understand it?** → Transpiled to `createElement`/`jsx()` calls.
3. **What is the Virtual DOM? How does it work?**
4. **What is reconciliation / the diffing algorithm?**
5. **What is React Fiber?**
6. **Functional vs class components.**
7. **Props vs state.**
8. **What are keys and why are they important? Why not index?**
9. **Controlled vs uncontrolled components.**
10. **What are synthetic events?**
11. **What are fragments? Why use them?**
12. **What is prop drilling and how to avoid it?**
13. **What is lifting state up?**
14. **What is one-way data binding?**
15. **Can a browser read JSX? What is Babel?**

### Hooks

16. **What are hooks? Why were they introduced?** → Use state/lifecycle in function components, reuse stateful logic without HOCs/render props, simpler than classes.
17. **Rules of hooks & why.**
18. **useState — is setState async? Functional updates?**
19. **useEffect — dependency array, cleanup, when it runs.**
20. **useEffect vs useLayoutEffect.**
21. **useMemo vs useCallback vs React.memo.**
22. **useRef use cases; useRef vs useState.**
23. **useContext — how it works, performance issues.**
24. **useReducer vs useState.**
25. **What is a custom hook? Write useFetch / useDebounce / useLocalStorage.**
26. **What is a stale closure in React?**
27. **useTransition vs useDeferredValue.**
28. **What's new in React 19?** → Actions, `use`, `useActionState`, `useOptimistic`, `useFormStatus`, ref as prop, server components/actions, metadata tags, compiler.
29. **How do you replicate componentDidMount/DidUpdate/WillUnmount with hooks?**
30. **Why does useEffect run twice in development?**

### Advanced

31. **What are HOCs? Example.**
32. **Render props pattern.**
33. **Compound components.**
34. **Error boundaries — what they catch and don't.**
35. **Portals — use cases & event bubbling.**
36. **Code splitting, React.lazy & Suspense.**
37. **Automatic batching in React 18.**
38. **Concurrent rendering.**
39. **Strict mode.**
40. **Server components vs client components.**
41. **CSR vs SSR vs SSG vs ISR.**
42. **What is hydration? Hydration mismatch?**
43. **How does React decide to re-render? How to prevent unnecessary re-renders?**
44. **How do you optimise a slow React app?**
45. **Context API vs Redux.**
46. **Explain Redux flow; what is middleware / thunk?**
47. **Redux Toolkit benefits.**
48. **Why React Query? Server state vs client state.**
49. **How to handle forms and validation?**
50. **How to handle authentication & protected routes?**
51. **How does React Router work?**
52. **How to test React components?**
53. **Accessibility practices.**
54. **Security: XSS, dangerouslySetInnerHTML.**
55. **What is the React Compiler?**

### Quick answers to trickier ones

- **Why can't hooks be called conditionally?** → React stores hook state in call order per component; changing order mismatches state.
- **Why does React need immutable updates?** → Change detection uses `Object.is` reference comparison; mutation keeps the same reference.
- **What happens when you call setState in render?** → Infinite re-render loop ("Too many re-renders").
- **How does `key` reset state?** → Different key = different component identity → unmount + mount.
- **What causes "Cannot update a component while rendering a different component"?** → Calling a parent's setState during a child's render; move it into an effect or handler.
- **What's the difference between `element` and `component`?** → Component is a function/class; element is the plain object returned (`<App />`).
- **What is the `children` prop?** → Content between a component's tags; can be anything renderable, even a function.
- **Why use `useCallback` with `React.memo` only?** → Otherwise the memoized function reference isn't compared by anyone.
- **What is tearing?** → Different components showing different values of the same external store in one render under concurrent rendering; solved by `useSyncExternalStore`.
- **Shallow comparison?** → Compares each top-level prop with `Object.is`; nested changes with same reference are not detected.

---

**End of React notes.**
