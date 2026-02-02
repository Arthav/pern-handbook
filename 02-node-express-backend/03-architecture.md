# Backend Architecture Patterns

Stop writing all your logic in `app.js` or inside the routes.

## The Controller-Service-Repository Pattern
This is the industry standard for scalable Node.js apps.

### 1. Routes (`routes/`)
**Job**: Define endpoints and attach middleware.
**Don't**: Write business logic here.

```javascript
router.post('/register', AuthController.register);
```

### 2. Controllers (`controllers/`)
**Job**: Handle HTTP requests. Validate input, call services, send responses.
**Don't**: Query the database directly.

```javascript
export const register = async (req, res, next) => {
  try {
    const { email, password } = req.body;
    // Validate Input (e.g., Zod or Joi)
    if (!email) throw new Error('Email required');
    
    // Call Service
    const user = await AuthService.registerUser(email, password);
    
    // Send Response
    res.status(201).json(user);
  } catch (err) {
    next(err);
  }
};
```

### 3. Services (`services/`)
**Job**: Business logic. Hashing passwords, sending emails, calculating totals.
**Don't**: Know about `req` or `res`. A service function should be reusable anywhere (e.g., by a CLI script or CRON job).

```javascript
export const registerUser = async (email, password) => {
  const existing = await UserRepository.findByEmail(email);
  if (existing) throw new Error('User exists');

  const hashedPassword = await bcrypt.hash(password, 10);
  return await UserRepository.create({ email, password: hashedPassword });
};
```

### 4. Repository / Data Access Layer (`db/` or `models/`)
**Job**: Talk to the database. SQL queries live here.
**Don't**: Do business logic.

```javascript
export const findByEmail = async (email) => {
  const result = await pool.query('SELECT * FROM users WHERE email = $1', [email]);
  return result.rows[0];
};
```

## Benefits
1.  **Testability**: You can mock the Repository to test the Service without a real DB.
2.  **Maintainability**: Deeply nested logic is easier to track.
3.  **Flexibility**: Switching from Postgres to Mongo? Just rewrite the Repository layer. The Controllers and Services stay the same.
