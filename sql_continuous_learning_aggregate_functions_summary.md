# Continuous Learning in SQL — Aggregate Functions Summary

## Objective

Extend basic SQL skills by learning how aggregate functions summarize data and how to continue building SQL knowledge independently.

Main aggregate functions covered:

- `COUNT()` — counts rows or non-NULL values
- `AVG()` — calculates the average of numeric values
- `SUM()` — calculates the total of numeric values

---

## What Are Aggregate Functions?

Aggregate functions perform a calculation across multiple data points and return a single summarized result.

Instead of returning every matching row, they return a calculated value.

Examples:

- Number of login attempts
- Average number of events
- Total amount of numeric data

---

## `COUNT()`

`COUNT()` returns the number of records represented by the selected column, excluding `NULL` values.

Example:

```sql
SELECT COUNT(firstname)
FROM customers;
```

This returns one value representing the number of non-NULL entries in the `firstname` column.

### Count with a Filter

```sql
SELECT COUNT(firstname)
FROM customers
WHERE country = 'USA';
```

This counts only customers whose `country` value is `USA`.

---

## `AVG()`

`AVG()` returns the average of numeric values in a column.

General syntax:

```sql
SELECT AVG(column_name)
FROM table_name;
```

Example pattern:

```sql
SELECT AVG(numeric_column)
FROM table_name;
```

Use `AVG()` when you need a mean or average value.

---

## `SUM()`

`SUM()` returns the total of numeric values in a column.

General syntax:

```sql
SELECT SUM(column_name)
FROM table_name;
```

Example pattern:

```sql
SELECT SUM(numeric_column)
FROM table_name;
```

Use `SUM()` when you need a cumulative total.

---

## Aggregate Function Syntax

The general structure is:

```sql
SELECT AGGREGATE_FUNCTION(column_name)
FROM table_name;
```

With filtering:

```sql
SELECT AGGREGATE_FUNCTION(column_name)
FROM table_name
WHERE condition;
```

Examples:

```sql
SELECT COUNT(firstname)
FROM customers;
```

```sql
SELECT COUNT(firstname)
FROM customers
WHERE country = 'USA';
```

---

## Quick Comparison

| Function | Purpose | Returns |
|---|---|---|
| `COUNT()` | Count records/non-NULL values | One number |
| `AVG()` | Calculate average | One number |
| `SUM()` | Calculate total | One number |

---

## Security Relevance

Aggregate functions can help security analysts summarize large datasets.

Possible uses include:

- Count failed login attempts
- Count suspicious events
- Count devices needing updates
- Calculate averages across numeric security data
- Sum volumes or event totals
- Combine filters with aggregate functions for focused analysis

Example concept:

```sql
SELECT COUNT(username)
FROM log_in_attempts
WHERE success = FALSE;
```

This pattern can be used to count failed login attempts if the database structure supports those fields.

---

## Continuous SQL Learning

SQL includes many more capabilities beyond basic filtering and joins.

A useful learning approach is to:

1. Identify the result you need.
2. Determine which table contains the data.
3. Search for the SQL feature that can produce that result.
4. Practice the query on sample data.
5. Verify that the output matches your goal.
6. Repeat with increasingly complex tasks.

Continue practicing with databases and explore additional SQL concepts through trusted learning resources.

---

## Skills Built So Far

Your SQL foundation now includes:

```text
SELECT
FROM
WHERE
ORDER BY
LIKE
%
_
>
<
>=
<=
=
<>
!=
BETWEEN
AND
OR
NOT
INNER JOIN
LEFT JOIN
RIGHT JOIN
COUNT
AVG
SUM
```

These concepts support progressively more advanced data analysis.

---

## Core Takeaway

Aggregate functions summarize data rather than returning all individual records.

Use:

```sql
COUNT()
```

to count,

```sql
AVG()
```

to calculate an average,

and:

```sql
SUM()
```

to calculate a total.

They become even more useful when combined with filters such as `WHERE`.
