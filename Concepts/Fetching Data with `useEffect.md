
# 🌐 Fetching Data with `useEffect` in React

## 🔹 Overview

In React, **fetching data from third-party APIs** (like cryptocurrency or weather data) is considered a **side-effect**, because it interacts with something outside the component (the web).
To handle side-effects, React provides the **`useEffect`** hook.

---

## ⚙️ Basic Structure

```js
useEffect(() => {
  // data fetching logic goes here
}, []);
```

* The first argument is a **function** that performs the effect (e.g., fetching data).
* The second argument (dependency array) determines **when** the effect runs.

  * `[]` → runs **once** when the component mounts.

---

## 🧩 Example: Fetching Bitcoin Data

```js
import { useState, useEffect } from "react";

export default function App() {
  const [btcData, setBtcData] = useState({});

  useEffect(() => {
    fetch("https://api.coindesk.com/v1/bpi/currentprice.json")
      .then((response) => response.json())
      .then((jsonData) => setBtcData(jsonData.bpi.USD))
      .catch((error) => console.log(error));
  }, []);

  return (
    <>
      <h1>Current BTC/USD data</h1>
      <p>Code: {btcData.code}</p>
      <p>Symbol: {btcData.symbol}</p>
      <p>Rate: {btcData.rate}</p>
      <p>Description: {btcData.description}</p>
      <p>Rate Float: {btcData.rate_float}</p>
    </>
  );
}
```

✅ `useEffect` runs once
✅ Fetches BTC data from Coindesk API
✅ Updates state with the USD section of the data
✅ Triggers a re-render with updated data

---

## 🧼 Cleaner Version (Using a Separate Function)

```js
import { useState, useEffect } from "react";

export default function App() {
  const [btcData, setBtcData] = useState({});

  const fetchData = () => {
    fetch("https://api.coindesk.com/v1/bpi/currentprice.json")
      .then((response) => response.json())
      .then((jsonData) => setBtcData(jsonData.bpi.USD))
      .catch((error) => console.log(error));
  };

  useEffect(() => {
    fetchData();
  }, []);

  return (
    <>
      <h1>Current BTC/USD data</h1>
      <p>Code: {btcData.code}</p>
      <p>Symbol: {btcData.symbol}</p>
      <p>Rate: {btcData.rate}</p>
      <p>Description: {btcData.description}</p>
      <p>Rate Float: {btcData.rate_float}</p>
    </>
  );
}
```

📘 This approach improves **readability** and **organization** by separating logic from the hook call.

---

## 🎭 Conditional Rendering

Since data fetching might be **delayed** or **fail**, you can display different content based on data availability.

### Example:

```js
return someStateVariable.length > 0 ? (
  <div>
    <h1>Data returned:</h1>
    <h2>{someStateVariable.results[0].price}</h2>
  </div>
) : (
  <h1>Data pending...</h1>
);
```

### How It Works:

* If `someStateVariable.length > 0`, data has been fetched → display data.
* If not, show a **loading message** (“Data pending…”).

### Notes:

* Works best when the state variable is initialized as an **empty array** (`useState([])`).
* Once the fetch completes, updating the state triggers a **re-render**, replacing the pending message with the data.

---

## 💡 Key Takeaways

| Concept                   | Explanation                                                   |
| ------------------------- | ------------------------------------------------------------- |
| **Side-effect**           | Any operation outside React’s rendering (e.g., fetching data) |
| **useEffect()**           | Handles side-effects in React                                 |
| **Dependency Array**      | Controls when the effect runs                                 |
| **Conditional Rendering** | Renders UI based on data readiness                            |
| **Error Handling**        | Always include `.catch()` or try/catch with async/await       |

---

## ⚡ Async/Await Alternative (Modern Approach)

```js
useEffect(() => {
  async function fetchData() {
    try {
      const res = await fetch("https://api.coindesk.com/v1/bpi/currentprice.json");
      const jsonData = await res.json();
      setBtcData(jsonData.bpi.USD);
    } catch (error) {
      console.error(error);
    }
  }
  fetchData();
}, []);
```

This version is easier to read and handles errors more gracefully.

---
