```
my-app/
├── node_modules/
├── public/
│   └── index.html
├── src/
│   ├── index.js
│   ├── App.js
│   └── index.css
├── package.json
└── README.md
```

---

### 🧩 `public/index.html`

Make sure this file has a root div:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React From Scratch</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

---

### ⚙️ `src/index.js`

This is your **entry point**.

```javascript
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App"; // Import your component

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

---

### 🧱 `src/App.js`

This is your **first component**.

```javascript
const App = () => {
  return (
    <div>
      <h1>Hello</h1>
      <p>Sub Tag</p>
    </div>
  );
};

export default App;
```

---

### 🎨 `src/index.css`

A global stylesheet.

```css
h1 {
  font-size: 100px;
  color: #4f46e5;
}

p {
  color: gray;
  font-size: 24px;
}
```

---

### 💡 What You Just Built

* `index.js` → entry file (mounts React app into the real DOM)
* `App.js` → a **functional component** returning JSX
* `index.css` → global styles applied across the app
* `React.StrictMode` → helps catch potential bugs (only runs in dev)

---

### ✅ Output

Your page should display:

```
Hello
Sub Tag
```

with your styles applied.

---
