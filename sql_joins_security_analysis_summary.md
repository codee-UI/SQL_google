# SQL Joins for Security Analysis — Concise Summary

## Objective
Learn how to combine related data from multiple SQL tables using joins.

Main join types:
- `INNER JOIN` — return only matching rows
- `LEFT JOIN` — return all rows from the left table and matching rows from the right
- `RIGHT JOIN` — return all rows from the right table and matching rows from the left
- `FULL OUTER JOIN` — return all rows from both tables

## `INNER JOIN`

Returns only rows where the join condition matches in both tables.

```sql
SELECT *
FROM employees
INNER JOIN machines
ON employees.device_id = machines.device_id;
```

If the same column exists in both tables, qualify it using `table.column`:

```sql
SELECT username,
       operating_system,
       employees.device_id
FROM employees
INNER JOIN machines
ON employees.device_id = machines.device_id;
```

## `LEFT JOIN`

Returns:
- all rows from the left table
- matching rows from the right table
- `NULL` when no right-table match exists

```sql
SELECT *
FROM employees
LEFT JOIN machines
ON employees.device_id = machines.device_id;
```

## `RIGHT JOIN`

Returns:
- all rows from the right table
- matching rows from the left table
- `NULL` when no left-table match exists

```sql
SELECT *
FROM employees
RIGHT JOIN machines
ON employees.device_id = machines.device_id;
```

A right join can often be rewritten as a left join by reversing table order.

## `FULL OUTER JOIN`

Returns all matching and unmatched rows from both tables.

```sql
SELECT *
FROM employees
FULL OUTER JOIN machines
ON employees.device_id = machines.device_id;
```

## Join Comparison

| Join Type | Matching Rows | Unmatched Left | Unmatched Right |
|---|---:|---:|---:|
| `INNER JOIN` | Yes | No | No |
| `LEFT JOIN` | Yes | Yes | No |
| `RIGHT JOIN` | Yes | No | Yes |
| `FULL OUTER JOIN` | Yes | Yes | Yes |

# Lab Scenario

You need to:
1. Match employees to machines
2. Find machines without assigned users
3. Find employees without assigned machines
4. Match employees to login attempts

Shared columns:
- `device_id` between `machines` and `employees`
- `username` between `employees` and `log_in_attempts`

## Task 1 — Match Employees to Machines

```sql
SELECT *
FROM machines
INNER JOIN employees
ON machines.device_id = employees.device_id;
```

**Lab result:** `185 rows`

Clearer real-world version:

```sql
SELECT machines.device_id,
       employees.username,
       machines.operating_system
FROM machines
INNER JOIN employees
ON machines.device_id = employees.device_id;
```

## Task 2 — Keep All Machines

```sql
SELECT *
FROM machines
LEFT JOIN employees
ON machines.device_id = employees.device_id;
```

If no employee matches, employee fields contain `NULL`.

**Lab result:** last username = `NULL`

## Task 2 — Keep All Employees

```sql
SELECT *
FROM machines
RIGHT JOIN employees
ON machines.device_id = employees.device_id;
```

**Lab result:** last username = `areyes`

## Task 3 — Match Employees to Login Attempts

```sql
SELECT *
FROM employees
INNER JOIN log_in_attempts
ON employees.username = log_in_attempts.username;
```

**Lab result:** `200 records`

## Complete Lab Workflow

```sql
SELECT *
FROM machines
INNER JOIN employees
ON machines.device_id = employees.device_id;

SELECT *
FROM machines
LEFT JOIN employees
ON machines.device_id = employees.device_id;

SELECT *
FROM machines
RIGHT JOIN employees
ON machines.device_id = employees.device_id;

SELECT *
FROM employees
INNER JOIN log_in_attempts
ON employees.username = log_in_attempts.username;
```

## Lab Answers

| Question | Answer |
|---|---|
| Rows from machines/employees inner join | `185` |
| Last username in left join | `NULL` |
| Last username in right join | `areyes` |
| Records from employees/login inner join | `200` |

## When to Use Each Join

Use `INNER JOIN` when you only want records that match in both tables.

Use `LEFT JOIN` when you want every row from your main/left table.

Use `RIGHT JOIN` when you want every row from the right table.

Use `FULL OUTER JOIN` when you need all records from both tables.

## Security Relevance

Joins help security analysts:
- connect users to devices
- identify unassigned machines
- identify employees without devices
- correlate login activity with employee records
- combine asset and authentication data
- support incident investigations

## Core Takeaway

A join needs:
1. Two related tables
2. A shared column
3. A join type
4. An `ON` condition

General pattern:

```sql
SELECT ...
FROM table1
JOIN table2
ON table1.shared_column = table2.shared_column;
```
