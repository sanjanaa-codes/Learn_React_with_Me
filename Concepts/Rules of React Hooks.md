### 🧠 The 4 Rules of React Hooks

#### 1. **Only call hooks inside React function components (or custom hooks)**

✅ *Where you can use hooks:*

* Inside a React component (e.g., `function App() { ... }`)
* Inside another custom hook (e.g., `useMyCustomHook()`)

🚫 *Where you CANNOT:*

* Regular JS functions
* Event handlers
* Loops or conditionals outside components

🪄 **Think of it like:** Hooks are “lifelines” connected to React’s heart. If you call them outside, React can’t track their state anymore.

---

#### 2. **Call hooks only at the top level**

✅ Always call hooks before any `return`, `if`, or loop.
🚫 Don’t call hooks **inside** `if` statements, `for` loops, or nested functions.

🪄 **Think of it like:**
React builds a mental map — “Hook #1 = useState, Hook #2 = useEffect.”
If you call a hook *conditionally*, React loses track of which hook is which on re-render — hence the **Invalid Hook Call** error.

---

#### 3. **You can call multiple hooks — but in the same order every render**

✅ Multiple hooks = fine.
🚫 Changing their order = chaos.

🪄 **Example:**

```js
// ✅ valid
const [count, setCount] = useState(0);
useEffect(() => { console.log(count); }, [count]);
```

```js
// 🚫 invalid
if (count > 0) {
  useEffect(() => console.log(count), [count]);
}
```

React expects the second hook to always be `useEffect`.
But now sometimes it’s skipped — *boom*, confusion.

---

#### 4. **If you want conditional logic — put it *inside* the hook**

✅ Correct way:

```js
useEffect(() => {
  if (count > 5) {
    console.log("Count is big!");
  }
}, [count]);
```

React still knows this `useEffect` exists, every render. Only its *content* changes conditionally — not the hook itself.

---

### ⚡ TL;DR Memory Hook Trick

> 🪝 “Hooks must always stay at the top of the function,
> called in the same order,
> and only inside React land.”

---
