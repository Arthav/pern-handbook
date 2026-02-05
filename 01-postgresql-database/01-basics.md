# PostgreSQL Basics

PostgreSQL is an object-relational database management system (ORDBMS). It uses SQL (Structured Query Language).

## Prerequisites: Running These Commands
To follow this section, you need PostgreSQL installed. If you haven't done this yet, go back to [00. Environment Setup](../00-introduction/02-environment-setup.md).

**How to run the SQL commands below?**
1.  **VS Code (Recommended)**: Use the "PostgreSQL" extension by Microsoft. Connect to your database and open a new query file (`.sql`).
2.  **PGAdmin / DBeaver**: Open the tool, connect to your database, and open the "Query Tool".

## 1. terminology
*   **Database**: A container for your data (e.g., `my_app`).
*   **Schema**: A namespace within a database (default is `public`).
*   **Table**: A collection of rows and columns (e.g., `users`).
*   **Row (Record)**: A single item of data.
*   **Column (Field)**: A specific attribute of that data.

## 2. Basic Data Types
Choosing the right data type is critical for performance and integrity.

| Type | Description | Use Case |
| :--- | :--- | :--- |
| `SERIAL` / `BIGSERIAL` | Auto-incrementing integer | Primary Keys (IDs). Use `BIGSERIAL` for large tables. |
| `VARCHAR(n)` | Variable-length string | Usernames, Emails. `TEXT` is identical in performance in Postgres. |
| `BOOLEAN` | True/False | Flags (is_active, is_verified). |
| `INTEGER` | Whole numbers | Counts, quantities. |
| `DECIMAL` / `NUMERIC` | Exact numbers | **Money/Currency**. Never use `FLOAT` for money! |
| `TIMESTAMP WITH TIME ZONE` | Date and Time | Created_at timestamps. Always prefer `TIMESTAMPTZ` over `TIMESTAMP`. |
| `JSONB` | Binary JSON | Flexible data, config settings. |

## 3. Basic CRUD Operations

### Create (INSERT)
```sql
INSERT INTO users (username, email, password_hash)
VALUES ('john_doe', 'john@example.com', 'hashed_secret')
RETURNING id, username; -- 👈 Postgres exclusive! Get data back immediately.
```

### Read (SELECT)
```sql
SELECT * FROM users; -- Get all columns (Avoid in production for large tables)
SELECT username, email FROM users WHERE id = 1; -- Specific columns
```

### Update (UPDATE)
```sql
UPDATE users
SET email = 'new_email@example.com', updated_at = NOW()
WHERE id = 1;
-- ⚠️ ALWAYS include a WHERE clause, or you update EVERY row!
```

### Delete (DELETE)
```sql
DELETE FROM users WHERE id = 1;
```

## 4. Foreign Keys (Relationships)
Linking tables together.

```sql
CREATE TABLE posts (
  id BIGSERIAL PRIMARY KEY,
  user_id BIGINT REFERENCES users(id) ON DELETE CASCADE, -- 👈 If user is deleted, delete their posts too
  title TEXT NOT NULL,
  content TEXT
);
```

---
[← Previous Section](../00-introduction/03-javascript-refresher.md) | [Next Section →](./02-schema-design.md)
