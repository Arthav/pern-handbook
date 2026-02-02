# Connect Node to Postgres

## Option 1: `pg` (node-postgres)
The default, unopinionated driver. Fast and lightweight. Best for learning SQL.

```javascript
import pg from 'pg';
const { Pool } = pg;

const pool = new Pool({
  connectionString: process.env.DATABASE_URL
});

export default pool;
```

## Option 2: ORMs (Object-Relational Mappers)
ORMs let you write JS objects instead of SQL.

### Drizzle ORM (Modern, High Performance)
Currently the most recommended ORM in the Node ecosystem (2024+). It's type-safe and extremely light.

```javascript
// schema.ts
import { pgTable, text, serial } from "drizzle-orm/pg-core";

export const users = pgTable('users', {
  id: serial('id').primaryKey(),
  name: text('name'),
});

// usage
const result = await db.select().from(users);
```

### Prisma (Easiest developer experience)
Very popular, but can be slower due to its Rust binary overhead on heavy loads.

## Security: SQL Injection
NEVER concatenate inputs.

```javascript
// ❌ VULNERABLE
pool.query(`SELECT * FROM users WHERE id = ${req.body.id}`); 
// If id is "1; DROP TABLE users;", you are dead.

// ✅ SAFE (Parameterized Queries)
pool.query('SELECT * FROM users WHERE id = $1', [req.body.id]);
```
The driver sends the query and the data separately. The DB treats the data strictly as literal values, never as executable code.

---
[← Previous Section](./03-architecture.md) | [Next Section →](../03-react-frontend/01-react-foundations.md)
