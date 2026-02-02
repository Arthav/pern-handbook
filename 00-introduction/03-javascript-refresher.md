# JavaScript Refresher for PERN

You don't need to know *everything* in JS, but you must master these concepts to work effectively with PERN.

## 1. Async/Await & Promises
Node.js backend work is almost entirely asynchronous (DB calls, API requests).

### The Best Practice (Async/Await)
Stop using `.then().catch()` chains for complex logic. It leads to callback hell.

```javascript
// BAD ❌
const getUser = (id) => {
  db.query('SELECT * FROM users WHERE id = $1', [id])
    .then(user => {
      return db.query('SELECT * FROM posts WHERE user_id = $1', [user.id])
    })
    .catch(err => console.error(err));
}

// GOOD (Senior) ✅
const getUserData = async (id) => {
  try {
    const user = await db.query('SELECT * FROM users WHERE id = $1', [id]);
    if (!user) throw new Error('User not found');

    const posts = await db.query('SELECT * FROM posts WHERE user_id = $1', [user.id]);
    return { user, posts };
  } catch (error) {
    // Centralized error handling usually happens here
    console.error('Service Error:', error.message);
    throw error;
  }
};
```

## 2. Destructuring & Spreading
Used heavily in React props and Express middleware.

```javascript
// Object Destructuring
const { id, username, ...rest } = req.body; // Separate sensitive info

// Array Destructuring (React Hooks)
const [state, setState] = useState(null);

// Spread Operator (Immutability)
const updatedUser = { ...oldUser, email: 'new@example.com' }; 
// 👆 Creates a NEW object, crucial for React re-renders.
```

## 3. Template Literals
Clean string concatenation.

```javascript
const query = `SELECT * FROM users WHERE age > ${minAge}`; // ⚠️ WARN: SQL Injection risk if used directly in DB queries!
// We will learn to NEVER do the above for SQL, but for logging it's fine:
console.log(`User ${username} logged in at ${new Date()}`);
```

## 4. Arrow Functions & 'this'
Arrow functions preserve the `this` context from the surrounding scope.

```javascript
// Concise implicit return
const activeUsers = users.filter(u => u.isActive);

// In Controllers
app.get('/users', (req, res) => { ... });
```

## 5. Modules (ESM vs CommonJS)
Node.js historically used CommonJS (`require`). Modern Node and React use ES Modules (`import`).

**We will stick to ES Modules (`import/export`) throughout this guide** because it creates parity between frontend and backend code.

```javascript
// CommonJS (Legacy/Default Node)
const express = require('express');
module.exports = app;

// ES Modules (Modern Standard)
import express from 'express';
export default app;
```
*Note: To use ESM in Node, add `"type": "module"` to your `package.json`.*

## 6. Higher Order Functions
Functions that take functions as arguments (map, filter, reduce).

```javascript
// Common in React rendering lists
{items.map(item => <ListItem key={item.id} item={item} />)}
```

---
[← Previous Section](./02-environment-setup.md) | [Next Section →](../01-postgresql-database/01-basics.md)
