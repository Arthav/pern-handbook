# Total Beginner Guide: From Scratch to "Hello World"

This guide assumes you have **never** coded before. We will setup your computer and get a website running.

---

## Phase 1: The Setup (Do this once)

### Step 1: Install VS Code (The Editor)
This is where we write code.
1.  Go to [code.visualstudio.com](https://code.visualstudio.com/).
2.  Download for your OS (Windows or Mac).
3.  Install it (Keep all defaults checked).

### Step 2: Install Node.js (The Engine)
This lets us run JavaScript outside the browser.
1.  Go to [nodejs.org](https://nodejs.org/).
2.  Download the **LTS (Long Term Support)** version.
3.  **Windows**: Run the installer. Default settings are fine.
4.  **Mac**: Run the installer.
5.  **Verify**:
    *   Open your Terminal (Mac: Cmd+Space, type "Terminal") or Command Prompt (Windows: Start, type "cmd").
    *   Type: `node -v` and hit Enter.
    *   You should see numbers (e.g., `v18.16.0`). If not, restart your computer and try again.

### Step 3: Install Git (The Saver)
1.  **Windows**: Download [Git for Windows](https://gitforwindows.org/). Run installer. Keep clicking "Next" (Defaults are fine).
2.  **Mac**: Open Terminal. Type `git --version`. If not installed, it will prompt you to install Apple Developer Tools. Say yes.

---

## Phase 2: Building Your First Server (Backend)

We will make a simple computer program that says "Hello".

1.  **Create a Folder**:
    *   Create a folder on your Desktop named `my-first-pern`.
    *   Open VS Code.
    *   File -> Open Folder -> Select `my-first-pern`.

2.  **Open the Terminal in VS Code**:
    *   In the top menu, click `Terminal` -> `New Terminal`.
    *   A panel opens at the bottom. This is where you talk to the computer.

3.  **Initialize the Project**:
    *   Type `npm init -y` and hit Enter.
    *   This creates a `package.json` file (It's like an ID card for your project).

4.  **Install Express**:
    *   Type `npm install express`.
    *   You will see a `node_modules` folder appear. These are connection libraries.

5.  **Write the Code**:
    *   Create a NEW FILE named `server.js` in the file explorer (left side).
    *   Paste this EXACT code:

```javascript
/* server.js */
import express from 'express';

const app = express();

// When someone goes to "/" (the homepage), say Hello.
app.get('/', (req, res) => {
  res.send('<h1>Hello from the Backend! 🚀</h1>');
});

// Start the server on port 3000
app.listen(3000, () => {
  console.log('Server running at http://localhost:3000');
});
```

6.  **Fix the "Module" Setting**:
    *   Open `package.json`.
    *   Add `"type": "module",` above `"scripts"`. It should look like this:
    ```json
    "version": "1.0.0",
    "type": "module",
    "description": "",
    ```

7.  **Run It**:
    *   In the terminal: `node server.js`
    *   It should say: `Server running at http://localhost:3000`
    *   Go to your Browser (Chrome). Type `http://localhost:3000`.
    *   **Success!** You should see "Hello from the Backend!".

---

## Phase 3: The Frontend (React)

Now let's make a pretty interface.

1.  **Stop the Server**:
    *   Click in the terminal. Press `Ctrl + C` to stop the server.

2.  **Create React App**:
    *   Run this command: `npm create vite@latest client -- --template react`
    *   It will create a folder named `client`.

3.  **Run React**:
    *   Go into the folder: `cd client`
    *   Install tools: `npm install`
    *   Start it: `npm run dev`

4.  **See it**:
    *   The terminal will show a link like `http://localhost:5173`.
    *   Ctrl+Click it (or type it in Chrome).
    *   **Success!** You see the Vite + React splash screen.

## Conclusion
You just setup a development environment, wrote a backend API, and launched a React frontend.

**Windows vs Mac Differences?**
*   **Terminal**: Windows uses Powershell, Mac uses Zsh. Most commands like `cd`, `npm`, `node` are the same.
*   **Permissions**: Mac might ask for password (sudo) more often for global installs.

**What's Next?**
Go to [01. PostgreSQL Database](../01-postgresql-database/01-basics.md) to start learning how to save data.

---
[← Previous Section](../07-quiz-and-faq/02-faq.md)
