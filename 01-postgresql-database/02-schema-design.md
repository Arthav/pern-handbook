# Schema Design & Normalization

A well-designed database is the backbone of any application. Bad design = slow queries and buggy code.

## 1. Normalization
The process of organizing data to reduce redundancy (duplicates).

### First Normal Form (1NF)
*   Each column must contain atomic values (no lists of emails in one cell).
*   Each row must be unique.

### Second Normal Form (2NF)
*   Must be in 1NF.
*   All non-key columns must depend on the *entire* primary key.

### Third Normal Form (3NF) - The "Sweet Spot"
*   Must be in 2NF.
*   No transitive dependencies (Column C depends on Column B which depends on ID).
    *   *Example*: Don't store `city` and `state` in a `users` table if they depend on `zip_code`. Move them to a `locations` table.

## 2. Relationships

### One-to-One (1:1)
Rare. Usually means the data belongs in the same table, unless splitting for performance (vertical partitioning) or security.
*   *Example*: `User` <-> `UserProfile` (Strict separation of auth logic vs profile info).

### One-to-Many (1:N)
The most common relationship.
*   *Example*: One `User` has many `Posts`.
*   **Implementation**: Put the foreign key (`user_id`) on the "Many" side table (`posts`).

### Many-to-Many (M:N)
Requires a **Join Table** (Bridge Table).
*   *Example*: `Students` and `Classes`. A student takes many classes; a class has many students.
*   **Implementation**: Create a third table `student_classes`.

```sql
CREATE TABLE student_classes (
  student_id BIGINT REFERENCES students(id),
  class_id BIGINT REFERENCES classes(id),
  enrolled_at TIMESTAMPTZ DEFAULT NOW(),
  PRIMARY KEY (student_id, class_id) -- Composite Primary Key
);
```

## 3. Constraints (Data Integrity)
Never trust the frontend. Enforce rules at the DB level.

*   `NOT NULL`: Field cannot be empty.
*   `UNIQUE`: No duplicates (e.g., email).
*   `CHECK`: Custom validation rules.

```sql
CREATE TABLE products (
  price NUMERIC CHECK (price > 0), -- Price must be positive
  discount_percentage INTEGER CHECK (discount_percentage BETWEEN 0 AND 100)
);
```

---
[← Previous Section](./01-basics.md) | [Next Section →](./03-advanced-sql.md)
