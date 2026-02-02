# Node.js Internals: What You Need to Know

## 1. Single Threaded Event Loop
Node.js runs on a single thread (the Main Thread).

*   **Blocking Code**: `JSON.parse(hugeFile)`, `fs.readFileSync`. These freeze your entire server. No one else can connect until it's done.
*   **Non-Blocking Code**: `fs.readFile`, `db.query`. These offload the work to the **Libuv** thread pool (C++ library) and continue processing other requests. When the work is done, a callback is added to the Event Queue.

### The Golden Rule
> **Don't Block the Event Loop.**

If you have heavy computation (image processing, video encoding), don't do it on the main thread. Use **Worker Threads** or a separate microservice.

## 2. CommonJS vs ES Modules
We discussed this in the Intro, but here is how it affects your backend structure.

### ES Modules (`import`) - The Modern Way
*   Enables Top-Level Await (Node 14.8+).
*   Standard across browser and server.
*   Requires `"type": "module"` in package.json or `.mjs` extension.

```javascript
// index.js
import { startServer } from './server.js';
await startServer(); // Top level await!
```

## 3. The `global` Object
In browser JS, you have `window`. In Node, you have `global`.
*   Avoid using global variables. They make testing a nightmare and cause race conditions.
*   Exceptions: `process.env` (Environment Variables).

## 4. `process`
*   `process.env`: Access environment variables (`API_KEY`, `DB_URL`).
*   `process.exit(1)`: Crash the app (1 = error, 0 = success).
*   `process.cwd()`: Current working directory.

---
[← Previous Section](../01-postgresql-database/04-performance.md) | [Next Section →](./02-express-basics.md)
