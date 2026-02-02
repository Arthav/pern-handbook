# PostgreSQL Performance Tuning

A slow database kills user experience.

## 1. Indexing
indexes make `SELECT` faster but `INSERT/UPDATE` slower (because the index needs updating).

### B-Tree (Default)
Good for `<`, `<=`, `=`, `>=`, `>` operations.
```sql
CREATE INDEX idx_users_email ON users(email);
```

### GIN (Generalized Inverted Index)
Crucial for JSONB and Array columns.
```sql
CREATE INDEX idx_metadata ON logs USING GIN (metadata);
```

### When to Index?
*   Columns used frequently in `WHERE` clauses.
*   Foreign Key columns (improves JOIN speed).
*   Columns used in `ORDER BY`.

### When NOT to Index?
*   Low cardinality columns (e.g., `gender`: 'M', 'F'). The DB scanner usually finds it faster to scan the whole table than jump through an index for 50% of the rows.

## 2. EXPLAIN ANALYZE
The most important tool for debugging queries. It shows the execution plan and actual runtime.

```sql
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'test@example.com';
```

Look for:
*   **Seq Scan**: Bad on large tables. Means it read every single row.
*   **Index Scan**: Good. It jumped straight to the data using an index.

## 3. JSONB Performance
Postgres allows schema-less data with JSONB.
*   Use `JSONB` (binary, indexed), not `JSON` (text only).
*   Don't abuse it. If you have structured data, use columns. Use JSONB for "Attributes" that vary wildly between rows.

```sql
-- Querying inside JSONB
SELECT * FROM products WHERE specs @> '{"color": "red"}';
```
