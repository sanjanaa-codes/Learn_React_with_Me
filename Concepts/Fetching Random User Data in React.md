
# 🍋 Fetching Random User Data in React (Little Lemon App Example)

## 🔹 Scenario

The **Little Lemon Restaurant** wants to run a competition where a **random customer** from their app receives a free meal.
To simulate this, we’ll use the **Random User API** to fetch a random customer’s details and display them once loaded.

---

## 🧠 Key Concepts

* **`useState()`** → Stores fetched data.
* **`useEffect()`** → Handles side effects like API calls.
* **Conditional Rendering** → Displays “Data pending…” until data is received.

---

## ⚙️ Code Example

```js
import { useState, useEffect } from "react";

export default function App() {
  const [userData, setUserData] = useState({});

  const fetchData = () => {
    fetch("https://randomuser.me/api/")
      .then((response) => response.json())
      .then((jsonData) => setUserData(jsonData.results[0]))
      .catch((error) => console.log(error));
  };

  useEffect(() => {
    fetchData();
  }, []);

  return Object.keys(userData).length > 0 ? (
    <div>
      <h1>Data returned:</h1>
      <h2>
        {userData.name.first} {userData.name.last}
      </h2>
      <img src={userData.picture.medium} alt="Random User" />
    </div>
  ) : (
    <h1>Data pending...</h1>
  );
}
```

---

## 🔍 Step-by-Step Breakdown

1. **Initialize State**

   ```js
   const [userData, setUserData] = useState({});
   ```

   The state starts empty, representing no data fetched yet.

2. **Define `fetchData()` Function**

   ```js
   const fetchData = () => {
     fetch("https://randomuser.me/api/")
       .then((response) => response.json())
       .then((jsonData) => setUserData(jsonData.results[0]));
   };
   ```

   * Fetches random user info.
   * Converts it to JSON.
   * Updates state with the fetched data.
   * ❗ No hooks are used inside this function (follows React’s Rules of Hooks).

3. **Use the `useEffect()` Hook**

   ```js
   useEffect(() => {
     fetchData();
   }, []);
   ```

   * Runs once after the initial render.
   * Triggers the data fetch operation.

4. **Conditional Rendering**

   ```js
   return Object.keys(userData).length > 0 ? (
     // show user data
   ) : (
     <h1>Data pending...</h1>
   );
   ```

   * `Object.keys(userData).length > 0` → checks if the object is no longer empty.
   * If data hasn’t loaded yet → show *“Data pending…”*.
   * Once data arrives → display the user’s name and image.

---

## 🧩 What Happens Internally

1. Component mounts → React renders *“Data pending…”*.
2. `useEffect()` runs → triggers `fetchData()`.
3. Fetch request is made to the **Random User API**.
4. When the response arrives → `setUserData()` updates the state.
5. React re-renders → displays *“Data returned”* and user info.

---

## 💡 Learning Points

| Concept                   | Explanation                                                                         |
| ------------------------- | ----------------------------------------------------------------------------------- |
| **Side Effects**          | Actions like fetching data or logging that happen outside React’s pure render cycle |
| **Rules of Hooks**        | Always call hooks at the top level, not inside loops or functions                   |
| **Re-render Trigger**     | Updating state causes React to re-render automatically                              |
| **Conditional Rendering** | Allows displaying fallback UI while waiting for data                                |

---

## 🧾 Practical Application for Little Lemon

The **Little Lemon team** can:

* Replace the `randomuser.me` API with their **customer database API**.
* Fetch the list of users.
* Randomly select one as the **winner** for the free meal giveaway.

---
