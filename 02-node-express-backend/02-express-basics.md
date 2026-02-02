# Express.js Basics & Middleware

Express is a routing and middleware web framework.

## 1. The Middleware Pattern
Middleware is a function that has access to the request object (`req`), the response object (`res`), and the next middleware function (`next`).

> Request -> Middleware 1 -> Middleware 2 -> ... -> Route Handler -> Response

```javascript
const logger = (req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next(); // 👈 CRITICAL: If you forget this, the request hangs forever!
};

app.use(logger); // Apply to all routes
```

## 2. Global Exception Handling (The Senior Way)
Don't write `try/catch` in every single controller. Use an error handling middleware at the **end** of your app chain.

```javascript
// In app.js
app.use(express.json());
app.use('/api', routes);

// 404 Handler
app.use((req, res, next) => {
  const error = new Error("Not Found");
  error.status = 404;
  next(error);
});

// Global Error Handler
app.use((err, req, res, next) => {
  res.status(err.status || 500).json({
    error: {
      message: err.message || "Internal Server Error",
    },
  });
});
```

## 3. Routing
Group your routes.

```javascript
// routes/users.js
import { Router } from 'express';
const router = Router();

router.get('/', getAllUsers);
router.post('/', createUser);

export default router;

// app.js
import userRoutes from './routes/users.js';
app.use('/users', userRoutes);
```

## 4. Request & Response
*   `req.body`: POST data (requires `express.json()` middleware).
*   `req.params`: URL parameters (`/users/:id` -> `req.params.id`).
*   `req.query`: Query strings (`/users?page=2` -> `req.query.page`).
*   `res.json({})`: Ensure you always send JSON APIs, not `res.send()`.

---
[← Previous Section](./01-node-internals.md) | [Next Section →](./03-architecture.md)
