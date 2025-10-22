
````markdown
# JavaScript Modules

In JavaScript, a **module** is simply a file.

The purpose of using modules is to make your code **modular, reusable, and organized**.  
You can work with smaller files, and import/export them to build more **customizable and composable** applications.

A module can be as simple as a single function in a separate file.

---

## 📘 Example Function

```javascript
function addTwo(a, b) {
    console.log(a + b);
}
````

Say you have a file named **`addTwo.js`** that contains only the above code.
To make it a JavaScript module, you need to use the **`export`** syntax.

---

## 🚀 Module Exports

There are two main ways to export modules in JavaScript:

1. **Default Exports**
2. **Named Exports**

---

## 🟢 Default Exports

You can have **only one default export** per JavaScript module.

### Example 1 – Inline Export

```javascript
export default function addTwo(a, b) {
    console.log(a + b);
}
```

Here, the `export default` keywords are added directly before the function declaration.

### Example 2 – Separate Export Statement

```javascript
function addTwo(a, b) {
    console.log(a + b);
}

export default addTwo;
```

✅ Both versions are equivalent.

---

## 🟡 Named Exports

Named exports let you export **multiple functions, variables, or objects** from a file.
Unlike default exports, there’s **no limit** to the number of named exports.

### Example 1 – Inline Named Exports

```javascript
export function addTwo(a, b) {
    console.log(a + b);
}

export function addThree(a, b, c) {
    console.log(a + b + c);
}
```

### Example 2 – Export at the Bottom

```javascript
function addTwo(a, b) {
    console.log(a + b);
}

function addThree(a, b, c) {
    console.log(a + b + c);
}

export { addTwo, addThree };
```

✅ Both methods are valid for named exports.

---

## 📥 Importing Modules

Just like exporting, there are multiple ways to import modules.
The syntax depends on **how the module was exported**.

Assume you have two files:

* **`addTwo.js`**
* **`mathOperations.js`**

You want to import the `addTwo` function from `addTwo.js` into `mathOperations.js`.

---

### 🔹 Importing a Default Export

If `addTwo` was exported as a **default export**, the syntax is:

```javascript
// addTwo.js
function addTwo(a, b) {
    console.log(a + b);
}
export default addTwo;
```

Then, in **`mathOperations.js`**:

```javascript
import addTwo from "./addTwo";

// rest of the mathOperations.js code
```

📝 Notes:

* Use the `import` keyword followed by the **name you want to use locally**.
* Use the `from` keyword followed by the **file path (without .js extension)**.

---

### 🔸 Importing a Named Export

If the `addTwo` function was exported as a **named export**, the syntax changes slightly:

```javascript
import { addTwo } from "./addTwo";

// rest of the mathOperations.js code
```

🧠 Tip:
For named imports, always use **curly braces `{}`** around the names you import.

---

## 🧾 Summary

| Type of Export     | Export Syntax Example          | Import Syntax Example                          |
| ------------------ | ------------------------------ | ---------------------------------------------- |
| **Default Export** | `export default addTwo;`       | `import addTwo from "./addTwo";`               |
| **Named Export**   | `export { addTwo, addThree };` | `import { addTwo, addThree } from "./addTwo";` |

---

### ✅ Key Takeaways

* A **module** in JavaScript is just a separate file containing code.
* Use **`export`** to share code and **`import`** to use it elsewhere.
* You can have **only one default export** per file.
* You can have **multiple named exports**.
* The import syntax **depends** on whether it’s a default or named export.

---

💡 *Modular code = cleaner structure, easier debugging, and better scalability.*

```
