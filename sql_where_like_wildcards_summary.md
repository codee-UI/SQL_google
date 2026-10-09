# SQL Filtering with `WHERE`, `LIKE`, and Wildcards — Concise Summary

## Objective

Learn how to filter SQL query results using:

- `WHERE` — apply a condition
- `=` — match an exact value
- `LIKE` — match a text pattern
- `%` — wildcard for any number of characters
- `_` — wildcard for exactly one character
- `DESCRIBE` — inspect table structure

These techniques help security analysts find specific records in large datasets efficiently.

---

## Why Filtering Matters

Security analysts often work with large logs and databases. Filtering helps isolate relevant records such as:

- Login attempts from a specific user
- Devices running a particular operating system
- Employees in a specific department
- Machines in a specific office or building
- Events matching a suspicious pattern

---

# 1. `WHERE` — Filter Exact Values

Basic syntax:

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

Example:

```sql
SELECT firstname, lastname, title, email
FROM employees
WHERE title = 'IT Staff';
```

This returns only rows where `title` equals `IT Staff`.

### Important

String values should be placed in single quotes:

```sql
WHERE operating_system = 'OS 2';
```

Column names should not be quoted.

---

# 2. `LIKE` — Filter by Pattern

Use `LIKE` when you want to match a pattern rather than an exact value.

Example:

```sql
SELECT lastname, firstname, title, email
FROM employees
WHERE title LIKE 'IT%';
```

This returns values beginning with `IT`, such as:

- `IT Staff`
- `IT Manager`

---

# 3. Wildcards

## `%` — Any Number of Characters

Examples:

```text
'a%'
```

matches values beginning with `a`.

```text
'%a'
```

matches values ending with `a`.

```text
'%a%'
```

matches values containing `a` anywhere.

---

## `_` — Exactly One Character

Examples:

```text
'a_'
```

matches two-character values beginning with `a`.

```text
'a__'
```

matches three-character values beginning with `a`.

```text
'N_'
```

matches values such as:

```text
NY
NV
NS
NT
```

---

# 4. `DESCRIBE` — Inspect Table Structure

Use:

```sql
DESCRIBE machines;
DESCRIBE employees;
```

`DESCRIBE` shows:

- Column names
- Data types
- Whether null values are allowed
- Key information

This is useful when you need to confirm exact field names before writing a query.

---

# Lab Scenario

You need to:

1. List organization machines
2. Find devices running `OS 2`
3. Find employees in Finance and Sales
4. Identify employees using machines in the South building

---

## Task 1 — List All Organization Machines

Query:

```sql
SELECT device_id, operating_system
FROM machines;
```

### Lab Answer

Number of rows returned:

```text
200
```

---

## Task 2 — Find Machines Running `OS 2`

Query:

```sql
SELECT device_id, operating_system
FROM machines
WHERE operating_system = 'OS 2';
```

### Lab Answer

Number of machines using `OS 2`:

```text
80
```

---

## Task 3 — Find Employees by Department

### Finance

```sql
SELECT *
FROM employees
WHERE department = 'Finance';
```

### Lab Answer

First employee ID:

```text
1003
```

### Sales

```sql
SELECT *
FROM employees
WHERE department = 'Sales';
```

### Lab Answer

Number of employees in Sales:

```text
33
```

---

## Task 4 — Identify Employee Machines

### Find the Employee in `South-109`

```sql
SELECT *
FROM employees
WHERE office = 'South-109';
```

### Lab Answer

Employee username:

```text
jlansky
```

---

## Find All Employees in the South Building

```sql
SELECT *
FROM employees
WHERE office LIKE 'South%';
```

`South%` means:

- Starts with `South`
- Any number of characters may follow

Examples:

```text
South-109
South-210
South-315
```

### Lab Answer

Department of the first returned employee:

```text
Finance
```

---

# Complete Lab Workflow

```sql
DESCRIBE machines;
DESCRIBE employees;

SELECT device_id, operating_system
FROM machines;

SELECT device_id, operating_system
FROM machines
WHERE operating_system = 'OS 2';

SELECT *
FROM employees
WHERE department = 'Finance';

SELECT *
FROM employees
WHERE department = 'Sales';

SELECT *
FROM employees
WHERE office = 'South-109';

SELECT *
FROM employees
WHERE office LIKE 'South%';
```

---

# Lab Answers

| Question | Answer |
|---|---|
| Rows returned from `machines` | `200` |
| Machines using `OS 2` | `80` |
| First Finance employee ID | `1003` |
| Employees in Sales | `33` |
| Employee in `South-109` | `jlansky` |
| First South-building employee department | `Finance` |

---

# Pattern Summary

| Pattern | Meaning |
|---|---|
| `'a%'` | Starts with `a` |
| `'%a'` | Ends with `a` |
| `'%a%'` | Contains `a` |
| `'a_'` | `a` plus one character |
| `'a__'` | `a` plus two characters |
| `'N_'` | `N` plus one character |

---

# Command Summary

| SQL Element | Purpose |
|---|---|
| `WHERE` | Filter rows by condition |
| `=` | Exact match |
| `LIKE` | Pattern match |
| `%` | Any number of characters |
| `_` | Exactly one character |
| `DESCRIBE` | Show table structure |

---

# Security Relevance

These SQL filters help security analysts:

- Find outdated systems
- Locate specific users
- Identify devices in affected locations
- Search security logs efficiently
- Reduce large datasets to relevant records
- Detect potentially suspicious activity

---

# Core Takeaway

Use:

```sql
WHERE
```

for exact conditions,

```sql
LIKE
```

for pattern-based filtering,

```text
%
```

for any number of characters,

and:

```text
_
```

for exactly one character.

Example:

```sql
SELECT *
FROM employees
WHERE office LIKE 'South%';
```

This returns all employees whose office begins with `South`.
