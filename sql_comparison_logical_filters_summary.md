# SQL Comparison and Logical Filters — Concise Summary

## Objective
Learn to filter SQL data using comparison operators, ranges, and logical operators.

Main tools:
- `WHERE`
- `=`, `>`, `<`, `>=`, `<=`, `<>`, `!=`
- `BETWEEN ... AND ...`
- `AND`
- `OR`
- `NOT`
- `LIKE`

## Comparison Operators

| Operator | Meaning |
|---|---|
| `=` | Equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |
| `<>` | Not equal to |
| `!=` | Alternative not equal to |

Example:

```sql
SELECT *
FROM log_in_attempts
WHERE login_date > '2022-05-09';
```

### Inclusive vs Exclusive
- `>` and `<` are **exclusive**
- `>=`, `<=`, and `BETWEEN` are **inclusive**

## `BETWEEN`

```sql
SELECT *
FROM log_in_attempts
WHERE login_date BETWEEN '2022-05-09' AND '2022-05-11';
```

Both boundary dates are included.

# Lab 1 — Dates, Times, and Numbers

## Task 1 — Logins After a Date

```sql
SELECT *
FROM log_in_attempts
WHERE login_date > '2022-05-09';
```

**Answer:** `125`

On or after May 9:

```sql
SELECT *
FROM log_in_attempts
WHERE login_date >= '2022-05-09';
```

**Answer:** `165`

## Task 2 — Date Range

```sql
SELECT *
FROM log_in_attempts
WHERE login_date BETWEEN '2022-05-09' AND '2022-05-11';
```

**Answer:** `123`

## Task 3 — Time Filters

Before 07:00:

```sql
SELECT *
FROM log_in_attempts
WHERE login_time < '07:00:00';
```

**Answer:** fifth username = `eraab`

Between 06:00 and 07:00:

```sql
SELECT *
FROM log_in_attempts
WHERE login_time BETWEEN '06:00:00' AND '07:00:00';
```

**Answer:** earliest login = `06:01:31`

## Task 4 — Event ID Filters

```sql
SELECT event_id, username, login_date
FROM log_in_attempts
WHERE event_id >= 100;
```

**Answer:** third result date = `2022-05-09`

```sql
SELECT event_id, username, login_date
FROM log_in_attempts
WHERE event_id BETWEEN 100 AND 150;
```

**Answer:** seventh username = `tmitchel`

# Logical Operators

## `AND`

Both conditions must be true.

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
  AND success = FALSE;
```

## `OR`

Either condition can be true.

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
   OR login_date = '2022-05-08';
```

## `NOT`

Negates a condition.

```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

Equivalent alternatives:

```sql
WHERE department <> 'Information Technology'
```

```sql
WHERE department != 'Information Technology'
```

# Lab 2 — `AND`, `OR`, and `NOT`

## Task 1 — Failed Logins After Hours

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
  AND success = FALSE;
```

**Answer:** `19`

## Task 2 — Logins on Two Dates

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
   OR login_date = '2022-05-08';
```

**Answer:** `75`

## Task 3 — Logins Outside Mexico

```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

**Answer:** `144`

## Task 4 — Marketing Employees in East Building

```sql
SELECT *
FROM employees
WHERE department = 'Marketing'
  AND office LIKE 'East%';
```

**Answer:** `elarson`

## Task 5 — Finance or Sales

```sql
SELECT *
FROM employees
WHERE department = 'Finance'
   OR department = 'Sales';
```

**Answer:** first Sales username = `lrodriqu`

## Task 6 — Employees Not in IT

```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

**Answer:** `161`

# Complete Query Reference

```sql
-- After a date
SELECT *
FROM log_in_attempts
WHERE login_date > '2022-05-09';

-- On or after a date
SELECT *
FROM log_in_attempts
WHERE login_date >= '2022-05-09';

-- Date range
SELECT *
FROM log_in_attempts
WHERE login_date BETWEEN '2022-05-09' AND '2022-05-11';

-- Before a time
SELECT *
FROM log_in_attempts
WHERE login_time < '07:00:00';

-- Time range
SELECT *
FROM log_in_attempts
WHERE login_time BETWEEN '06:00:00' AND '07:00:00';

-- Numeric threshold
SELECT event_id, username, login_date
FROM log_in_attempts
WHERE event_id >= 100;

-- Numeric range
SELECT event_id, username, login_date
FROM log_in_attempts
WHERE event_id BETWEEN 100 AND 150;

-- AND
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
  AND success = FALSE;

-- OR
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
   OR login_date = '2022-05-08';

-- NOT + LIKE
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';

-- AND + LIKE
SELECT *
FROM employees
WHERE department = 'Marketing'
  AND office LIKE 'East%';

-- OR
SELECT *
FROM employees
WHERE department = 'Finance'
   OR department = 'Sales';

-- NOT
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

# Lab Answers Summary

| Question | Answer |
|---|---|
| Logins after 2022-05-09 | `125` |
| Logins on/after 2022-05-09 | `165` |
| Logins between 2022-05-09 and 2022-05-11 | `123` |
| Fifth username before 07:00 | `eraab` |
| Earliest login from 06:00–07:00 | `06:01:31` |
| Third result for event_id >= 100 | `2022-05-09` |
| Seventh result for event_id 100–150 | `tmitchel` |
| Failed logins after 18:00 | `19` |
| Logins on May 8 or May 9 | `75` |
| Logins outside Mexico | `144` |
| First Marketing/East username | `elarson` |
| First Sales username | `lrodriqu` |
| Employees not in IT | `161` |

## Security Relevance
These filters help security analysts:
- Investigate login activity in incident windows
- Identify after-hours access
- Find failed logins
- Detect suspicious geographic activity
- Target affected departments
- Filter event IDs
- Reduce large datasets to relevant records

## Core Takeaway

Comparison operators:

```text
>  <  >=  <=  =  <>  !=
```

Inclusive range:

```sql
BETWEEN ... AND ...
```

Logical operators:

```sql
AND
OR
NOT
```

Typical security query:

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
  AND success = FALSE;
```
