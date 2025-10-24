
### 1️⃣ Counter App (Basic)

```jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "INCREMENT": return { count: state.count + 1 };
    case "DECREMENT": return { count: state.count - 1 };
    case "RESET": return { count: 0 };
    default: return state;
  }
}

export default function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <h1>{state.count}</h1>
      <button onClick={() => dispatch({ type: "INCREMENT" })}>+</button>
      <button onClick={() => dispatch({ type: "DECREMENT" })}>-</button>
      <button onClick={() => dispatch({ type: "RESET" })}>Reset</button>
    </div>
  );
}
```

---

### 2️⃣ Toggle Theme

```jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "TOGGLE_THEME":
      return { darkMode: !state.darkMode };
    default:
      return state;
  }
}

export default function ThemeToggler() {
  const [state, dispatch] = useReducer(reducer, { darkMode: false });

  return (
    <div style={{ background: state.darkMode ? "#333" : "#fff", color: state.darkMode ? "#fff" : "#000", padding: 20 }}>
      <p>Theme: {state.darkMode ? "Dark" : "Light"}</p>
      <button onClick={() => dispatch({ type: "TOGGLE_THEME" })}>Toggle</button>
    </div>
  );
}
```

---

### 3️⃣ Form Input Manager

```jsx
import { useReducer } from "react";

function reducer(state, action) {
  return { ...state, [action.name]: action.value };
}

export default function FormExample() {
  const [state, dispatch] = useReducer(reducer, { name: "", email: "" });

  function handleChange(e) {
    dispatch({ name: e.target.name, value: e.target.value });
  }

  return (
    <form>
      <input name="name" value={state.name} onChange={handleChange} placeholder="Name" />
      <input name="email" value={state.email} onChange={handleChange} placeholder="Email" />
      <p>{JSON.stringify(state)}</p>
    </form>
  );
}
```

---

### 4️⃣ Shopping Cart

```jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "ADD_ITEM":
      return [...state, action.item];
    case "REMOVE_ITEM":
      return state.filter((_, i) => i !== action.index);
    case "CLEAR_CART":
      return [];
    default:
      return state;
  }
}

export default function Cart() {
  const [cart, dispatch] = useReducer(reducer, []);

  return (
    <div>
      <button onClick={() => dispatch({ type: "ADD_ITEM", item: "Apple" })}>Add Apple</button>
      <button onClick={() => dispatch({ type: "ADD_ITEM", item: "Banana" })}>Add Banana</button>
      <button onClick={() => dispatch({ type: "CLEAR_CART" })}>Clear</button>
      <ul>
        {cart.map((item, index) => (
          <li key={index}>
            {item} <button onClick={() => dispatch({ type: "REMOVE_ITEM", index })}>x</button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

---

### 5️⃣ Todo List

```jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "ADD_TODO":
      return [...state, { id: Date.now(), text: action.text, done: false }];
    case "TOGGLE_TODO":
      return state.map(todo =>
        todo.id === action.id ? { ...todo, done: !todo.done } : todo
      );
    case "DELETE_TODO":
      return state.filter(todo => todo.id !== action.id);
    default:
      return state;
  }
}

export default function TodoApp() {
  const [todos, dispatch] = useReducer(reducer, []);
  let input;

  return (
    <div>
      <input ref={el => (input = el)} placeholder="Add todo" />
      <button onClick={() => {
        dispatch({ type: "ADD_TODO", text: input.value });
        input.value = "";
      }}>Add</button>

      <ul>
        {todos.map(todo => (
          <li key={todo.id}>
            <span
              style={{ textDecoration: todo.done ? "line-through" : "none" }}
              onClick={() => dispatch({ type: "TOGGLE_TODO", id: todo.id })}
            >
              {todo.text}
            </span>
            <button onClick={() => dispatch({ type: "DELETE_TODO", id: todo.id })}>x</button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

---

### 6️⃣ Authentication (Login/Logout)

```jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "LOGIN":
      return { ...state, user: action.user, isLoggedIn: true };
    case "LOGOUT":
      return { ...state, user: null, isLoggedIn: false };
    default:
      return state;
  }
}

export default function AuthApp() {
  const [state, dispatch] = useReducer(reducer, { user: null, isLoggedIn: false });

  return (
    <div>
      {state.isLoggedIn ? (
        <>
          <h3>Welcome, {state.user}</h3>
          <button onClick={() => dispatch({ type: "LOGOUT" })}>Logout</button>
        </>
      ) : (
        <button onClick={() => dispatch({ type: "LOGIN", user: "Sanjanaa" })}>Login</button>
      )}
    </div>
  );
}
```

---

### 7️⃣ API Loading State

```jsx
import { useEffect, useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "FETCH_START": return { ...state, loading: true, error: null };
    case "FETCH_SUCCESS": return { ...state, loading: false, data: action.data };
    case "FETCH_ERROR": return { ...state, loading: false, error: action.error };
    default: return state;
  }
}

export default function FetchData() {
  const [state, dispatch] = useReducer(reducer, { loading: false, data: null, error: null });

  useEffect(() => {
    dispatch({ type: "FETCH_START" });
    fetch("https://jsonplaceholder.typicode.com/posts/1")
      .then(res => res.json())
      .then(data => dispatch({ type: "FETCH_SUCCESS", data }))
      .catch(err => dispatch({ type: "FETCH_ERROR", error: err.message }));
  }, []);

  if (state.loading) return <p>Loading...</p>;
  if (state.error) return <p>Error: {state.error}</p>;
  return <pre>{JSON.stringify(state.data, null, 2)}</pre>;
}
```

---

### 8️⃣ Multi-State Dashboard

```jsx
import { useReducer } from "react";

const initialState = {
  balance: 100,
  points: 0,
  level: 1
};

function reducer(state, action) {
  switch (action.type) {
    case "DEPOSIT": return { ...state, balance: state.balance + action.amount };
    case "WITHDRAW": return { ...state, balance: state.balance - action.amount };
    case "ADD_POINTS": return { ...state, points: state.points + action.points };
    case "LEVEL_UP": return { ...state, level: state.level + 1 };
    default: return state;
  }
}

export default function Dashboard() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <h2>Balance: ${state.balance}</h2>
      <h3>Points: {state.points}</h3>
      <h3>Level: {state.level}</h3>
      <button onClick={() => dispatch({ type: "DEPOSIT", amount: 50 })}>Deposit</button>
      <button onClick={() => dispatch({ type: "WITHDRAW", amount: 20 })}>Withdraw</button>
      <button onClick={() => dispatch({ type: "ADD_POINTS", points: 10 })}>Add Points</button>
      <button onClick={() => dispatch({ type: "LEVEL_UP" })}>Level Up</button>
    </div>
  );
}
```

---

