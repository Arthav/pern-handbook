# API Design: Connecting Frontend & Backend

## 1. RESTful Standards
REST (Representational State Transfer) is a set of rules.

### Resource Naming
*   Use Nouns, not Verbs.
*   Use Plurals.

| Action | Bad URL ❌ | Good URL ✅ |
| :--- | :--- | :--- |
| **Get all users** | `/getUsers` | `GET /users` |
| **Create user** | `/createUser` | `POST /users` |
| **Get specific user** | `/users?id=123` | `GET /users/123` |
| **Update user** | `/updateUser` | `PATCH /users/123` |
| **Delete user** | `/deleteUser` | `DELETE /users/123` |

### HTTP Status Codes
Stop sending `200 OK` for errors!

*   `200`: OK (Success)
*   `201`: Created (After POST)
*   `400`: Bad Request (Invalid input)
*   `401`: Unauthorized (Not logged in)
*   `403`: Forbidden (Logged in, but no permission)
*   `404`: Not Found
*   `500`: Internal Server Error (Your code crashed)

## 2. Dealing with CORS
Cross-Origin Resource Sharing. The browser blocks requests from `localhost:5173` (React) to `localhost:3000` (Node) by default.

### The Fix
Install `cors` on your Express backend.

```javascript
import cors from 'cors';
app.use(cors({
  origin: 'http://localhost:5173', // Only allow your frontend
  credentials: true // Allow cookies to be sent
}));
```

---
[← Previous Section](../03-react-frontend/03-state-management.md) | [Next Section →](./02-authentication-authorization.md)
