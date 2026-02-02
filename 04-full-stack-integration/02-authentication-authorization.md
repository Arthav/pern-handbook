# Authentication & Authorization

## 1. JWT vs Sessions
*   **Sessions**: Store user ID on the server (Redis/DB). Give user a generic cookie ID.
    *   *Pros*: Easy to revoke access.
    *   *Cons*: Server needs memory/DB lookup on every request.
*   **JWT (JSON Web Tokens)**: Store user data *inside* the encryption token itself.
    *   *Pros*: Stateless (Server doesn't need to remember anything).
    *   *Cons*: Hard to revoke (blacklist required).

**We will use JWT for this guide (Industry Standard for REST APIs).**

## 2. The Auth Flow
1.  **Register**: User sends email/pass. Server hashes pass (Using `bcrypt`), saves to DB.
2.  **Login**: User sends email/pass. Server compares hash. If match, Server signs a JWT `jsonwebtoken` and sends it back.
3.  **Access**: Frontend sends JWT in `Authorization: Bearer <token>` header for every request.
4.  **Verify**: Middleware checks the signature. If valid, attaches `user` to `req`.

## 3. Implementation Example

### Backend (Middleware)
```javascript
import jwt from 'jsonwebtoken';

export const authenticateToken = (req, res, next) => {
  const authHeader = req.headers['authorization'];
  const token = authHeader && authHeader.split(' ')[1]; // "Bearer <TOKEN>"

  if (!token) return res.sendStatus(401);

  jwt.verify(token, process.env.JWT_SECRET, (err, user) => {
    if (err) return res.sendStatus(403);
    req.user = user;
    next();
  });
};
```

### Frontend (Axios Interceptor)
Automatically attach token to every request.

```javascript
import axios from 'axios';

const api = axios.create({ baseURL: 'http://localhost:3000' });

api.interceptors.request.use((config) => {
  const token = localStorage.getItem('token');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});
```
