# Security Best Practices

Securing your PERN app is mandatory.

## 1. Helmet
`helmet` is a middleware that sets secure HTTP headers automatically.

```javascript
import helmet from 'helmet';
app.use(helmet());
```

## 2. Rate Limiting
Prevent DDOS and brute-force attacks.

```javascript
import rateLimit from 'express-rate-limit';

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100 // limit each IP to 100 requests per windowMs
});

app.use(limiter);
```

## 3. Environment Variables
**NEVER** commit your `.env` file to GitHub.
Add `.env` to your `.gitignore`.

## 4. Input Validation (Zod)
Never trust `req.body`. Validate it before it touches your DB.

```javascript
import { z } from 'zod';

const UserSchema = z.object({
  email: z.string().email(),
  password: z.string().min(8)
});

// Inside controller
const result = UserSchema.safeParse(req.body);
if (!result.success) {
  return res.status(400).json(result.error);
}
```

## 5. SQL Injection & XSS
*   **SQL Injection**: Solved by using Parameterized Queries (see Node section).
*   **XSS (Cross Site Scripting)**: React automatically escapes content in JSX, protecting you from most XSS. Warning: Never use `dangerouslySetInnerHTML` unless absolutely necessary and sanitized.

---
[← Previous Section](./02-authentication-authorization.md) | [Next Section →](../05-devops-and-deployment/03-dockerization.md)
