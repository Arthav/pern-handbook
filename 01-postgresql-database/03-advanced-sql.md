# Advanced SQL Patterns

As you grow, simple CRUD isn't enough. You need to ask complex questions of your data.

## 1. Joins
Combining rows from two or more tables.

*   `INNER JOIN`: Returns records that have matching values in both tables.
*   `LEFT JOIN`: Returns all records from the left table, and the matched records from the right table. (Useful for finding "Users with NO posts").
*   `RIGHT JOIN`: Opposite of Left.
*   `FULL OUTER JOIN`: Return all records when there is a match in either left or right.

```sql
-- Get all users and their post count
SELECT 
  u.username, 
  COUNT(p.id) as post_count
FROM users u
LEFT JOIN posts p ON u.id = p.user_id
GROUP BY u.id;
```

## 2. Aggregations & Group By
Summarizing data.
*   `COUNT`, `SUM`, `AVG`, `MAX`, `MIN`.
*   `HAVING`: Like a `WHERE` clause, but for aggregated groups.

```sql
-- Find users who have posted more than 10 times
SELECT user_id, COUNT(*) 
FROM posts 
GROUP BY user_id 
HAVING COUNT(*) > 10;
```

## 3. CTEs (Common Table Expressions)
"Temporary tables" for a single query. Makes complex queries readable.

```sql
WITH regional_sales AS (
    SELECT region, SUM(amount) AS total_sales
    FROM orders
    GROUP BY region
), top_regions AS (
    SELECT region
    FROM regional_sales
    WHERE total_sales > (SELECT SUM(total_sales)/10 FROM regional_sales)
)
SELECT *
FROM orders
WHERE region IN (SELECT region FROM top_regions);
```

## 4. Window Functions
Perform an aggregate-like operation across a set of rows related to the current row.

```sql
-- Rank employees by salary within their department
SELECT 
  employee_name, 
  department, 
  salary,
  RANK() OVER (PARTITION BY department ORDER BY salary DESC) as salary_rank
FROM employees;
```
