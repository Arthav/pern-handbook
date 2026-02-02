# FAQ & Troubleshooting

Common issues you will run into.

## 1. "Connection Refused" (ECONNREFUSED)
**Error**: `connect ECONNREFUSED 127.0.0.1:5432`
**Cause**: The target service isn't running or isn't on that port.
**Fix**:
*   Is Postgres running? (`docker ps` or check Services).
*   Is it on the right port? (Default 5432).
*   Are you connecting to `localhost` inside Docker? (Inside Docker, `localhost` is the container itself. Use `host.docker.internal` or the service name `db`).

## 2. React: "Too many re-renders"
**Error**: `Error: Too many re-renders. React limits the number of renders to prevent an infinite loop.`
**Cause**: You are calling a state setter *during* render.
**Bad**: `<button onClick={setCount(count + 1)}>` (Calls immediately).
**Good**: `<button onClick={() => setCount(count + 1)}>` (Calls only on click).

## 3. "Cross-Origin Request Blocked" (CORS)
**Error**: `Access to fetch at ... has been blocked by CORS policy`
**Fix**: Install `cors` package on the **BACKEND (Express)**, not the frontend.
```js
app.use(cors({ origin: 'http://localhost:5173' }));
```

## 4. Environment Variables undefined
**Error**: `process.env.DB_URL` is `undefined`.
**Fix**:
*   Did you `import 'dotenv/config'` (or `require('dotenv').config()`) at the very top?
*   Is `.env` in the root folder (not `src`)?
*   **Vite**: Frontend env vars must start with `VITE_`. (`VITE_API_URL`). Backend vars do not.

## 5. "relation 'users' does not exist"
**Error**: `error: relation "users" does not exist`
**Fix**:
*   You connected to the wrong database name.
*   You forgot to run your migration/SQL script to create the table.
*   Schema mismatch (you created it in `postgres` schema, querying `public`).

---
[← Previous Section](./01-quiz.md) | [Next Section →](../08-beginner-tutorial/01-windows-mac-setup.md)
