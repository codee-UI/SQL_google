# SQL Reference Guide — Google Cybersecurity Certificate

## Overview

This reference summarizes the SQL concepts covered in the course:

1. Query a database
2. Apply filters
3. Join tables
4. Perform calculations

---

# 1. Query a Database

## `SELECT`

Specifies which columns to return.

```sql
SELECT employee_id
FROM employees;
```

Return all columns:

```sql
SELECT *
FROM employees;
```

## `FROM`

Specifies which table to query.

```sql
SELECT *
FROM employees;
```

## `ORDER BY`

Sorts query results.

Ascending order:

```sql
SELECT *
FROM employees
ORDER BY department;
```

Equivalent:

```sql
ORDER BY department ASC;
```

Descending order:

```sql
SELECT *
FROM employees
ORDER BY city DESC;
```

Sort by multiple columns:

```sql
SELECT *
FROM employees
ORDER BY country, city;
```

SQL sorts by `country` first, then by `city` when multiple rows have the same country.

---

# 2. Apply Filters to SQL Queries

## `WHERE`

Begins a filter condition.

```sql
SELECT *
FROM employees
WHERE title = 'IT Staff';
```

---

## `AND`

Both conditions must be true.

```sql
SELECT *
FROM customers
WHERE region = 5
  AND country = 'USA';
```

---

## `OR`

Either condition can be true.

```sql
SELECT *
FROM customers
WHERE country = 'Canada'
   OR country = 'USA';
```

---

## `NOT`

Negates a condition.

```sql
SELECT *
FROM customers
WHERE NOT country = 'Mexico';
```

---

## `BETWEEN`

Filters values within an inclusive range.

```sql
SELECT *
FROM employees
WHERE hiredate BETWEEN '2002-01-01' AND '2003-01-01';
```

Both boundary values are included.

---

# Comparison Operators

| Operator | Meaning | Example |
|---|---|---|
| `=` | Equal to | `WHERE birthdate = '1980-05-15'` |
| `>` | Greater than | `WHERE birthdate > '1970-01-01'` |
| `>=` | Greater than or equal to | `WHERE birthdate >= '1965-06-30'` |
| `<` | Less than | `WHERE date < '2023-01-31'` |
| `<=` | Less than or equal to | `WHERE date <= '2020-12-31'` |
| `<>` | Not equal to | `WHERE date <> '2023-02-28'` |
| `!=` | Not equal to | `WHERE date != '2023-05-14'` |

---

# Pattern Matching with `LIKE`

Use `LIKE` with wildcards to search for text patterns.

## `%` Wildcard

`%` represents zero or more characters.

Starts with `a`:

```sql
WHERE value LIKE 'a%'
```

Ends with `a`:

```sql
WHERE value LIKE '%a'
```

Contains `a` anywhere:

```sql
WHERE value LIKE '%a%'
```

Example:

```sql
SELECT *
FROM employees
WHERE title LIKE 'IT%';
```

---

## `_` Wildcard

`_` represents exactly one character.

Examples:

```text
'a_'   → a followed by one character
'a__'  → a followed by two characters
'_a'   → one character followed by a
'_a_'  → a with one character on each side
```

Example:

```sql
SELECT *
FROM customers
WHERE state LIKE 'N_';
```

---

# 3. Join Tables

Joins combine related tables using a shared column.

General pattern:

```sql
SELECT *
FROM table1
JOIN table2
ON table1.shared_column = table2.shared_column;
```

---

## `INNER JOIN`

Returns only rows that match in both tables.

```sql
SELECT *
FROM employees
INNER JOIN machines
ON employees.device_id = machines.device_id;
```

---

## `LEFT JOIN`

Returns all rows from the first/left table and matching rows from the second/right table.

```sql
SELECT *
FROM employees
LEFT JOIN machines
ON employees.device_id = machines.device_id;
```

Unmatched right-table fields are returned as `NULL`.

---

## `RIGHT JOIN`

Returns all rows from the second/right table and matching rows from the first/left table.

```sql
SELECT *
FROM employees
RIGHT JOIN machines
ON employees.device_id = machines.device_id;
```

Unmatched left-table fields are returned as `NULL`.

---

## `FULL OUTER JOIN`

Returns all records from both tables.

```sql
SELECT *
FROM employees
FULL OUTER JOIN machines
ON employees.device_id = machines.device_id;
```

---

## Join Comparison

| Join | Matching Rows | Unmatched Left | Unmatched Right |
|---|---:|---:|---:|
| `INNER JOIN` | Yes | No | No |
| `LEFT JOIN` | Yes | Yes | No |
| `RIGHT JOIN` | Yes | No | Yes |
| `FULL OUTER JOIN` | Yes | Yes | Yes |

---

# 4. Perform Calculations

Aggregate functions summarize multiple rows and return a calculated result.

## `AVG()`

Returns the average of numeric values.

```sql
SELECT AVG(height)
FROM people;
```

---

## `COUNT()`

Returns the number of non-NULL values in a selected column.

```sql
SELECT COUNT(firstname)
FROM customers;
```

With a filter:

```sql
SELECT COUNT(firstname)
FROM customers
WHERE country = 'USA';
```

---

## `SUM()`

Returns the total of numeric values.

```sql
SELECT SUM(cost)
FROM purchases;
```

---

# Compact SQL Cheat Sheet

```sql
-- Query data
SELECT column1, column2
FROM table_name;

-- All columns
SELECT *
FROM table_name;

-- Sort
SELECT *
FROM table_name
ORDER BY column1 ASC;

SELECT *
FROM table_name
ORDER BY column1 DESC;

-- Exact filter
SELECT *
FROM table_name
WHERE column1 = 'value';

-- Multiple conditions
SELECT *
FROM table_name
WHERE condition1 AND condition2;

SELECT *
FROM table_name
WHERE condition1 OR condition2;

-- Exclude
SELECT *
FROM table_name
WHERE NOT column1 = 'value';

-- Range
SELECT *
FROM table_name
WHERE column1 BETWEEN value1 AND value2;

-- Pattern
SELECT *
FROM table_name
WHERE column1 LIKE 'text%';

-- Inner join
SELECT *
FROM table1
INNER JOIN table2
ON table1.id = table2.id;

-- Left join
SELECT *
FROM table1
LEFT JOIN table2
ON table1.id = table2.id;

-- Count
SELECT COUNT(column1)
FROM table_name;

-- Average
SELECT AVG(column1)
FROM table_name;

-- Sum
SELECT SUM(column1)
FROM table_name;
```

---

# Cybersecurity Use Cases

These SQL features can support tasks such as:

- Investigating failed login attempts
- Filtering records by date and time
- Finding suspicious locations or users
- Identifying devices requiring updates
- Correlating users with machines
- Joining login events with employee records
- Counting security events
- Summarizing numeric security data

---

# Core Takeaway

A practical SQL workflow is:

```text
SELECT → choose columns
FROM → choose table
WHERE → filter
ORDER BY → sort
JOIN → combine tables
COUNT / AVG / SUM → summarize
```

These commands form a strong foundation for security-focused database analysis.
