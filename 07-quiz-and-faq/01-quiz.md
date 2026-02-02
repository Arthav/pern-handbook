# PERN Stack Quiz

Test your specific knowledge of the PERN stack.

## Questions

### Section 1: PostgreSQL
1.  **What is the difference between `VARCHAR` and `TEXT` in PostgreSQL?**
2.  **Why would you use a transaction (`BEGIN` ... `COMMIT`)?**
3.  **What does ACID stand for?**
4.  **True or False**: You should always store images directly in the database as `BYTEA`.

### Section 2: Express & Node
5.  **How is `req.params` different from `req.query`?**
6.  ** What happens if you forget to call `next()` in a middleware?**
7.  **Why should you avoid `fs.readFileSync` in a production server?**
8.  **What is the purpose of `process.env`?**

### Section 3: React
9.  **Why does React need a `key` prop when rendering lists?**
10. **Explain "Lifting State Up".**
11. **What is the dependency array in `useEffect`, and what happens if it's empty `[]`?**
12. **Difference between `props` and `state`?**

### Section 4: Integration & DevOps
13. **What is CORS and why does it block my frontend?**
14. **Where should you store your Database Password?**
15. **What is a "Reverse Proxy" (Nginx)?**

---

## Answers

### PostgreSQL
1.  **Diff**: Under the hood in Postgres, there is no performance difference. `VARCHAR(n)` just enforces a length limit.
2.  **Transactions**: To ensure a group of actions all succeed or all fail (e.g., deducting money from User A and adding to User B).
3.  **ACID**: Atomicity, Consistency, Isolation, Durability.
4.  **False**: Store the *path* (URL) to the image (hosted on S3/Cloudinary). Storing binary data bloats the DB.

### Express & Node
5.  **Params**: Part of the URL path (`/users/:id` -> `req.params.id`). **Query**: After the `?` (`/users?page=2` -> `req.query.page`).
6.  **Forgot next()**: The request hangs indefinitely until the browser times out.
7.  **Blocking**: It blocks the Event Loop. No other user can get a response until the file finishes reading.
8.  **Env**: To store secrets (API Keys, DB URLs) securely outside the code.

### React
9.  **Keys**: Help React identify which items have changed, added, or removed. Crucial for performance and avoiding bugs in input state.
10. **Lifting State**: Moving state to a common ancestor component so multiple children can share/update it.
11. **Deps**: Controls when the effect runs. `[]` means it runs only once on mount (like `componentDidMount`).
12. **Props vs State**: Props are passed *down* (read-only). State is managed *interally* (changing).

### Integration
13. **CORS**: Browser security feature blocking requests to a different domain. It protects users, not servers.
14. **Process.env**: In a `.env` file, loaded into `process.env`. Never in git.
15. **Reverse Proxy**: A server (Nginx) that sits in front of your App (Node), handling SSL, caching, and routing.

---
[← Previous Section](../06-senior-concepts-capstone/02-capstone-project.md) | [Next Section →](./02-faq.md)
