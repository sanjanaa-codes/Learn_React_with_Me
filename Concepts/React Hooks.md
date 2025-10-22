
Understanding React Hooks

-> Introduction
  React Hooks were introduced at a React conference to simplify how developers manage state and lifecycle in React components.

-> Purpose of Hooks 

  * Replace class components with a simpler, functional approach.
  * Make React code "cleaner, modular, and more reusable".
  * Help avoid "large, bloated components" that are hard to maintain.

-> Benefits of Using Hooks 

  * Simplify complex logic in components.
  * Improve **performance** and **readability**.
  * Make code **easier to share and manage**.
  * Eliminate the need for classes — you can use state and other React features in functional components.

-> Adoption at Meta 

  * Meta engineers tested hooks internally before public release.
  * Internal teams found major improvements in developer experience and performance.
  * Hooks were rolled out gradually in a **non-breaking way** — old class components still work.

-> Learning Advice 

  * Hooks may feel confusing or “magical” at first — that’s normal.
  * Be patient and keep practicing; they become intuitive with use.
  * Don’t rely on old class syntax; **invest time to learn hooks properly**.
  * Once mastered, hooks make your code **more logical and consistent**.

-> Why Hooks Were Introduced**

Before hooks, developers used **class components** to manage state and lifecycle methods (`this.state`, `componentDidMount`, etc.).
Problems with class components:

* Hard to reuse logic between components.
* Large, bloated code with `this` bindings.
* Difficult to read and test.

Hooks solve these by letting functional components handle state and side effects cleanly.
-> Most Common React Hooks 

(a) useState – Manage Component State 

 Purpose-Adds state to a functional component.

**Syntax:**

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0); // state variable + setter
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```
-> Interview Tip: 
`useState` is ideal for values that **change over time** — e.g., form inputs, toggle buttons, counters.
 Explain like this: `useState` lets React remember values between renders and update the UI when that value changes 

---
 (b) useEffect – Handle Side Effects 

**Purpose:** Perform side effects like API calls, timers, subscriptions, or DOM updates.

 Syntax 

```jsx
import { useState, useEffect } from "react";

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => setSeconds(s => s + 1), 1000);
    return () => clearInterval(timer); // cleanup
  }, []); // empty dependency → runs once

  return <p>Time: {seconds}s</p>;
}
```

-> Interview Tip 

* Think of `useEffect` as combining `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`.
* Always **return a cleanup function** when using intervals, event listeners, or subscriptions.
* The **dependency array** decides when the effect runs:

  * `[]` → once (on mount)
  * `[value]` → when `value` changes

---
 (c) useContext – Global Data Access 

 Purpose - Lets you access **global data** (like theme, user info, or language) without prop drilling.

**Example:**

```jsx
import { createContext, useContext } from "react";

const ThemeContext = createContext("light");

function Child() {
  const theme = useContext(ThemeContext);
  return <p>Current theme: {theme}</p>;
}

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Child />
    </ThemeContext.Provider>
  );
}
```
 Interview Tip 
Say: “`useContext` allows components to share data easily without passing props manually down multiple levels.”

---

 (d) useRef – Access DOM or Persist Values**

 Purpose 

1. Directly access DOM elements (like input focus).
2. Store values that don’t cause re-renders when changed.

 Example 1 (DOM 

```jsx
import { useRef } from "react";

function InputFocus() {
  const inputRef = useRef();

  const handleFocus = () => inputRef.current.focus();

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
}
```

 Example 2 (Persist Value) 

```jsx
const count = useRef(0);
count.current++;
```

**Interview Tip:**
Explain: “`useRef` doesn’t trigger re-renders when updated — it’s perfect for storing mutable values or DOM references.”

---

(e) useMemo – Optimize Performance**

**Purpose:** Memoizes (remembers) **expensive computations** so they’re not recalculated unnecessarily.

**Example:**

```jsx
import { useMemo, useState } from "react";

function ExpensiveCalculation({ num }) {
  const result = useMemo(() => {
    console.log("Calculating...");
    return num * 2;
  }, [num]);

  return <p>Result: {result}</p>;
}
```

**Interview Tip:**
“`useMemo` prevents costly recalculations unless dependencies change — boosting performance.”

---

(f) useCallback – Optimize Functions**

**Purpose:** Prevents functions from being recreated unnecessarily on every render.

**Example:**

```jsx
import { useState, useCallback } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => setCount(c => c + 1), []);

  return <button onClick={increment}>Count: {count}</button>;
}
```

**Interview Tip:**
“`useCallback` memoizes the function definition — useful when passing callbacks to child components to avoid re-renders.”

---

(g) useReducer – Complex State Management**

**Purpose:** Alternative to `useState` for managing complex or interrelated state logic (similar to Redux reducer).

**Example:**

```jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "increment": return { count: state.count + 1 };
    case "decrement": return { count: state.count - 1 };
    default: return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
      <button onClick={() => dispatch({ type: "decrement" })}>−</button>
    </div>
  );
}
```

**Interview Tip:**
“`useReducer` helps organize complex state transitions — making logic predictable and maintainable.”

---

4. Hook Rules (Always Follow These!)**

1. Only call hooks **at the top level** (not inside loops or conditionals).
2. Only call hooks **inside React functional components or custom hooks**.

---

5. Custom Hooks (Bonus for Interviews)**

**Purpose:** Reuse logic across components by creating your own hook.

**Example:**

```jsx
import { useState, useEffect } from "react";

function useFetch(url) {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch(url).then(res => res.json()).then(setData);
  }, [url]);

  return data;
}

function App() {
  const user = useFetch("https://api.example.com/user");
  return <div>{user ? user.name : "Loading..."}</div>;
}
```

**Interview Tip:**
Say: “Custom hooks let me package reusable logic — like fetching data or handling forms — cleanly across components.”

---

6. Summary Table (For Quick Revision)**

| Hook          | Purpose                       | Example Use Case                |
| ------------- | ----------------------------- | ------------------------------- |
| `useState`    | Manage state                  | Counter, toggle, form input     |
| `useEffect`   | Side effects                  | API call, timer, event listener |
| `useContext`  | Global data                   | Theme, language, user info      |
| `useRef`      | DOM access or mutable storage | Input focus, previous value     |
| `useMemo`     | Cache computed values         | Expensive calculation           |
| `useCallback` | Cache functions               | Avoid re-renders in child       |
| `useReducer`  | Complex state logic           | Shopping cart, form reducer     |

---
