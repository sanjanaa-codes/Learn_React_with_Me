
# Understanding `createRoot` in React 18

### 📘 Code Example

```jsx
import { createRoot } from "react-dom/client";

const root = createRoot(document.getElementById("root"));
root.render(<button>Click</button>);
```

---

### 🧠 Explanation

1. **Importing `createRoot`**

   ```js
   import { createRoot } from "react-dom/client";
   ```

   * In **React 18**, `createRoot` replaces the older `ReactDOM.render()` method.
   * It enables the **Concurrent Mode** features that make React more efficient and responsive.

2. **Creating a Root**

   ```js
   const root = createRoot(document.getElementById("root"));
   ```

   * This tells React **where** in the HTML DOM to render your app.
   * `document.getElementById("root")` refers to a `<div id="root"></div>` inside your `index.html`.

3. **Rendering the Component**

   ```js
   root.render(<button>Click</button>);
   ```

   * This mounts a simple `<button>` element inside the root div.
   * In a real project, you’d usually render the main component:

     ```js
     root.render(<App />);
     ```

---

### 💡 Notes

* The HTML file must have a root element like:

  ```html
  <div id="root"></div>
  ```
* Use `createRoot` **only once** at the entry point (usually `main.jsx` or `index.js`).
* `createRoot` is part of the **React 18 API** introduced to support concurrent rendering for better performance.

---
