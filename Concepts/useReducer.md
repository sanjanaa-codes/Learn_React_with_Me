## ⚛️ Understanding `useReducer` in React

### 🧩 Why useReducer?

While the **`useState`** hook is great for managing simple state, it becomes cumbersome when:

* State logic is **complex** or involves **multiple sub-values**.
* The **next state depends on the previous** state.

In such cases, **`useReducer`** provides a cleaner, scalable solution.

---

### ⚙️ What is `useReducer`?

You can think of it as a **supercharged version of `useState`**.

It takes:

1. A **reducer function** → defines how state changes.
2. An **initial state** → the starting value.

It returns:

* The **current state**.
* A **dispatch function** → used to trigger state changes.

---

### 🧠 Key Concepts

* A **reducer** function accepts `(state, action)` and returns a **new state**.
* The **action** is an object, usually with a `type` property, describing what to do.
* You call `dispatch({ type: "ACTION_TYPE" })` instead of `setState()`.

---

### 🍋 Example: Little Lemon Restaurant Wallet App

```jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "BUY_INGREDIENTS":
      return { money: state.money - 10 };
    case "SELL_MEAL":
      return { money: state.money + 10 };
    case "CELEBRITY_VISIT":
      return { money: state.money + 5000 };
    default:
      return state; // Always return current state if no matching action
  }
}

function App() {
  const initialState = { money: 100 };
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div style={{ textAlign: "center", marginTop: "50px" }}>
      <h1>Little Lemon Restaurant</h1>
      <h2>Wallet: ${state.money}</h2>

      <div style={{ marginTop: "20px" }}>
        <button onClick={() => dispatch({ type: "BUY_INGREDIENTS" })}>
          Buy Ingredients (-$10)
        </button>

        <button
          onClick={() => dispatch({ type: "SELL_MEAL" })}
          style={{ marginLeft: "10px" }}
        >
          Sell Meal (+$10)
        </button>

        <button
          onClick={() => dispatch({ type: "CELEBRITY_VISIT" })}
          style={{ marginLeft: "10px" }}
        >
          Celebrity Visit (+$5000)
        </button>
      </div>
    </div>
  );
}

export default App;
```

---

### 🧾 How it Works

1. **`useReducer(reducer, initialState)`** initializes the state and provides a dispatcher.
2. The **reducer** function decides how to update the state based on the **action type**.
3. **`dispatch({ type: "BUY_INGREDIENTS" })`** triggers that change.

---

### 💡 Benefits of useReducer

✅ Simplifies complex or dependent state logic
✅ Keeps code **clean and organized**
✅ Easier to **extend** with new action types
✅ Makes behavior **predictable** and easy to debug

---

### 🪄 Takeaway

> Use `useState` for simple UI states.
> Use `useReducer` when your state transitions follow **clear, defined rules** — like a mini state machine.

---
