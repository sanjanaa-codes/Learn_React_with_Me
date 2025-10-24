
### 📘 Official Documentation

* Visit **[react.dev](https://react.dev)** — the official and best resource to learn React.
* Contains clear **concepts, examples, and references** for every topic (e.g., JSX, hooks, etc.).
* Always refer here before searching elsewhere.

---

### ⚙️ Ways to Start a React App

React projects need:

* Multiple packages
* Folder structure
* Configuration settings

Rather than setting these up manually, we use tools to generate them quickly.

---

### 🧩 Common Setup Tools

#### 1️⃣ **Create React App (CRA)**

* **Old official setup** created by Facebook.
* Handles all basic configuration, dependencies, and folder setup.
* Command:

  ```bash
  npx create-react-app my-project
  ```
* Commands inside project:

  ```bash
  npm start       # Run development server
  npm run build   # Create production build
  npm test        # Run tests
  ```
* ⚠️ “npm run eject” removes configuration — avoid it.

---

#### 2️⃣ **Set React App (Recommended)**

* Modern and faster version of CRA.
* Uses the same structure and flow but more updated internally.
* Command:

  ```bash
  npx set-react-app my-project
  ```
* Uses **.jsx** instead of **.js** for React files.
* Example:

  ```bash
  import App from './App.jsx'
  ```

---

#### 3️⃣ **Vite**

* Lightweight and extremely fast bundler.
* Used internally by Set React App.
* Command:

  ```bash
  npm create vite@latest my-project
  ```
* Choose:

  * Framework: React
  * Language: JavaScript
* Then:

  ```bash
  cd my-project
  npm install
  npm run dev     # instead of npm start
  ```
* Uses `.jsx` and `main.jsx` instead of `index.js`.

---

#### 4️⃣ **Next.js / Remix**

* Frameworks built on React for full-stack apps.
* ⚠️ Not recommended for beginners — learn core React first.

---

#### 5️⃣ **StackBlitz (Online Option)**

* Run React projects directly in the browser — no local setup needed.
* Great for testing or quick practice.
* URL: [stackblitz.com](https://stackblitz.com)

---

### 🧠 Key Concepts

* **npx** → executes packages
* **npm** → manages packages
* **npm start** → runs local dev server
* **npm run dev** → same, used with Vite
* **Ctrl + C** → stop the running server
* **Ctrl + `** → open VS Code terminal

---

### ✅ Summary

| Tool             | Command Example                | File Extension | Run Command   | Recommended |
| ---------------- | ------------------------------ | -------------- | ------------- | ----------- |
| Create React App | `npx create-react-app myApp`   | .js            | `npm start`   | ⚠️ Old      |
| Set React App    | `npx set-react-app myApp`      | .jsx           | `npm start`   | ✅ Yes       |
| Vite             | `npm create vite@latest myApp` | .jsx           | `npm run dev` | ✅ Fastest   |
| Next.js          | `npx create-next-app myApp`    | .js/.jsx/.tsx  | `npm run dev` | ❌ Beginner  |
| StackBlitz       | Online tool                    | .jsx           | Auto-run      | 🧪 Practice |

---
