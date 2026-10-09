# SQL Basics for Security Analysis — Concise Summary

## Objective
Learn foundational SQL used to retrieve and organize security-relevant data.

Main keywords:
- `SELECT` — choose columns
- `FROM` — choose table
- `ORDER BY` — sort results
- `DESC` — descending sort
- `*` — all columns

## Basic Query Structure

```sql
SELECT column_name
FROM table_name;
```

Example:

```sql
SELECT employee_id, device_id
FROM employees;
```

The semicolon `;` ends the query.

## `SELECT`

Specific columns:

```sql
SELECT customerid, city
FROM customers;
```

All columns:

```sql
SELECT *
FROM customers;
```

## `ORDER BY`

Ascending:

```sql
SELECT customerid, city, country
FROM customers
ORDER BY city;
```

Descending:

```sql
SELECT customerid, city, country
FROM customers
ORDER BY city DESC;
```

Multiple columns:

```sql
SELECT customerid, city, country
FROM customers
ORDER BY country, city;
```

SQL sorts by the first column first, then the second when needed.

# Lab Scenario

You need to:
1. Review employee devices that may require updates
2. Investigate login activity
3. Sort login attempts by date and time

The main tables are:
- `machines`
- `log_in_attempts`

## Task 1 — Retrieve Device Data

All device information:

```sql
SELECT *
FROM machines;
```

Device ID and email client:

```sql
SELECT device_id, email_client
FROM machines;
```

**Answer:** Third-row email client = `Email Client 2`

Device, OS, and patch date:

```sql
SELECT device_id, operating_system, OS_patch_date
FROM machines;
```

**Answer:** First patch date = `2021-09-01`

Older patch dates can help identify systems that may need updates.

## Task 2 — Investigate Login Activity

Login locations:

```sql
SELECT event_id, country
FROM log_in_attempts;
```

**Answer:** Login attempts from Australia = `No`

Login date and time:

```sql
SELECT username, login_date, login_time
FROM log_in_attempts;
```

**Answer:** Fifth-row username = `jrafael`

All login data:

```sql
SELECT *
FROM log_in_attempts;
```

## Task 3 — Sort Login Attempts

Sort by date:

```sql
SELECT *
FROM log_in_attempts
ORDER BY login_date;
```

**Answer:** First record = `ivelasco on 2022-05-08`

Sort by date and time:

```sql
SELECT *
FROM log_in_attempts
ORDER BY login_date, login_time;
```

**Answer:** First record = `bsand at 00:19:11`

## Complete Lab Workflow

```sql
SELECT *
FROM machines;

SELECT device_id, email_client
FROM machines;

SELECT device_id, operating_system, OS_patch_date
FROM machines;

SELECT event_id, country
FROM log_in_attempts;

SELECT username, login_date, login_time
FROM log_in_attempts;

SELECT *
FROM log_in_attempts;

SELECT *
FROM log_in_attempts
ORDER BY login_date;

SELECT *
FROM log_in_attempts
ORDER BY login_date, login_time;
```

## Lab Answers

| Question | Answer |
|---|---|
| Third-row email client | `Email Client 2` |
| First patch date | `2021-09-01` |
| Australia login attempts | `No` |
| Fifth-row username | `jrafael` |
| First record sorted by date | `ivelasco — 2022-05-08` |
| First record sorted by date/time | `bsand — 00:19:11` |

## Common SQL Issues

If you forget the semicolon and see:

```text
->
```

enter:

```sql
;
```

Also verify table and column spelling if a query fails or returns unexpected results.

## Command Summary

| SQL Keyword | Purpose |
|---|---|
| `SELECT` | Choose columns |
| `FROM` | Choose table |
| `*` | Return all columns |
| `ORDER BY` | Sort results |
| `DESC` | Sort descending |

## Security Relevance

SQL can help security analysts:
- Identify devices with outdated patches
- Review login activity
- Check geographic login patterns
- Examine suspicious login times
- Organize data for investigations

## Core Takeaway

```sql
SELECT columns
FROM table
ORDER BY column;
```

These skills are the foundation for more advanced filtering with clauses such as `WHERE`.
