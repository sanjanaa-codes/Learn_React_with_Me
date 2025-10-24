#### 1. **node_modules/**

* Contains all dependencies and packages your app needs (React, ReactDOM, etc.).
* It’s **not shared** on GitHub since it’s huge (200–300 MB).
* Instead, `package.json` is shared — it records **what dependencies** and **which versions** to install.
* Reinstall anytime with:

  ```bash
  npm install
  ```

---

#### 2. **public/**

* Contains static files that the browser can directly access.
* **index.html** → the single file React ultimately renders into.
* **favicon.ico, logo.png, manifest.json, robots.txt** are stored here.
* React never modifies this file — it only injects content *into* it.

---

#### 3. **src/**

* The heart of your React app — all your code lives here.
* Includes:

  * `index.js` → entry point (first file React runs)
  * `App.js` → main component rendered inside `index.js`
  * Any components, hooks, styles, utilities, etc.
* This is where you’ll work **95% of the time**.

---

#### 4. **.gitignore**

* Lists files/folders that should not be uploaded to GitHub.

  * Example: `node_modules/`, `build/`, `.env`

---

#### 5. **package.json**

* Like your project’s “identity card.”
* Contains:

  * Project name and version
  * Dependencies
  * Scripts (e.g. `npm start`, `npm run build`)
* Example:

  ```json
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build"
  }
  ```

---

#### 6. **How Rendering Works Behind the Scene**

* React is a **Single Page Application (SPA)** — only one HTML file (`index.html`).
* React takes all your JS (components, logic, CSS) and compiles it into one file called:

  ```
  /static/js/bundle.js
  ```
* This bundle is automatically injected into `index.html` inside the `<div id="root"></div>` element.
* That’s why the actual HTML file looks empty — React fills it **dynamically** in the browser.

---

#### 7. **Important Ports & Commands**

* Development server: `http://localhost:3000`
* Common commands:

  ```bash
  npm start      # Runs the app locally
  npm run build  # Creates production build
  npm test       # Runs test suite
  ```

---

