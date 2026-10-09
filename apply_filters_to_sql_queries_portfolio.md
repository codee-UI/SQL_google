# Apply Filters to SQL Queries

## Project Description

As a security professional, I used SQL to investigate potential security issues involving employee login activity and workstation updates. I queried the `log_in_attempts` and `employees` tables and applied filters with `WHERE`, `AND`, `OR`, `NOT`, `LIKE`, and the `%` wildcard to retrieve only the records relevant to each security task.

---

## Retrieve After-Hours Failed Login Attempts

A potential security incident occurred after normal business hours, so I needed to identify all unsuccessful login attempts made after 18:00.

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
  AND success = FALSE;
```

### How the Query Works

- `SELECT *` returns all columns from the table.
- `FROM log_in_attempts` identifies the table containing login activity.
- `WHERE` begins the filter.
- `login_time > '18:00'` returns only login attempts made after 18:00.
- `AND` requires both conditions to be true.
- `success = FALSE` limits the results to failed login attempts.

This query isolates failed after-hours activity for further security investigation.

**Lab result:** 19 failed login attempts occurred after 18:00.

> **Portfolio screenshot suggestion:** Capture the query and several rows of its MariaDB output.

---

## Retrieve Login Attempts on Specific Dates

A suspicious event occurred on `2022-05-09`. I reviewed login attempts from that date and the previous day, `2022-05-08`.

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
   OR login_date = '2022-05-08';
```

### How the Query Works

- `login_date = '2022-05-09'` identifies login attempts on the incident date.
- `OR` allows either date condition to be true.
- `login_date = '2022-05-08'` includes the day before the incident.

Using `OR` is appropriate because a record only needs to match one of the two dates.

**Lab result:** 75 login attempts occurred across these two dates.

> **Portfolio screenshot suggestion:** Capture the query and output showing records from both dates.

---

## Retrieve Login Attempts Outside of Mexico

The investigation determined that the suspicious login activity did not originate in Mexico. The `country` column contains both `MEX` and `MEXICO`, so I used pattern matching to exclude both forms.

```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

### How the Query Works

- `LIKE 'MEX%'` matches values beginning with `MEX`.
- `%` represents any number of additional characters.
- This pattern matches both `MEX` and `MEXICO`.
- `NOT` reverses the condition and returns login attempts from all other countries.

This is more reliable than excluding only one exact country value.

**Lab result:** 144 login attempts originated outside Mexico.

> **Portfolio screenshot suggestion:** Capture the query and output showing countries other than Mexico.

---

## Retrieve Employees in Marketing

The organization needed to update machines used by Marketing employees located in the East building.

```sql
SELECT *
FROM employees
WHERE department = 'Marketing'
  AND office LIKE 'East%';
```

### How the Query Works

- `department = 'Marketing'` filters for Marketing employees.
- `AND` requires the office condition to also be true.
- `office LIKE 'East%'` matches office values beginning with `East`.
- `%` allows any office number to follow, such as `East-170` or `East-320`.

This query returns only Marketing employees whose offices are in the East building.

**Lab result:** The first employee returned was `elarson`.

> **Portfolio screenshot suggestion:** Capture the query and several matching Marketing/East records.

---

## Retrieve Employees in Finance or Sales

A different security update was required for employees in either the Finance or Sales department.

```sql
SELECT *
FROM employees
WHERE department = 'Finance'
   OR department = 'Sales';
```

### How the Query Works

- The first condition selects Finance employees.
- `OR` allows a row to match either department.
- The second condition selects Sales employees.

`OR` is required because an employee does not need to belong to both departments; matching either one is sufficient.

**Lab result:** The first Sales employee returned was `lrodriqu`.

> **Portfolio screenshot suggestion:** Capture the query and output showing both Finance and Sales records.

---

## Retrieve All Employees Not in IT

The Information Technology department had already received the required update, so I needed to identify employees in every other department.

```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

### How the Query Works

- `department = 'Information Technology'` represents the group that should be excluded.
- `NOT` reverses this condition.
- The query therefore returns employees from all departments except Information Technology.

**Lab result:** 161 employees were outside the Information Technology department.

An equivalent filter could also be written as:

```sql
WHERE department <> 'Information Technology';
```

or:

```sql
WHERE department != 'Information Technology';
```

> **Portfolio screenshot suggestion:** Capture the query and a portion of the resulting employee list.

---

## SQL Techniques Demonstrated

| SQL Feature | Security Use in This Project |
|---|---|
| `WHERE` | Filters records to specific conditions |
| `AND` | Requires multiple conditions to be true |
| `OR` | Returns records matching either condition |
| `NOT` | Excludes records that match a condition |
| `LIKE` | Searches text values by pattern |
| `%` | Matches any number of characters in a pattern |
| `>` | Filters values greater than a threshold |
| `FALSE` | Identifies unsuccessful login attempts |

---

## Tables Used

### `log_in_attempts`

Relevant fields:

- `event_id`
- `username`
- `login_date`
- `login_time`
- `country`
- `ip_address`
- `success`

### `employees`

Relevant fields:

- `employee_id`
- `device_id`
- `username`
- `department`
- `office`

---

## Complete Query Set

```sql
-- Failed login attempts after business hours
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
  AND success = FALSE;

-- Login attempts on May 9 or May 8
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
   OR login_date = '2022-05-08';

-- Login attempts outside Mexico
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';

-- Marketing employees in East offices
SELECT *
FROM employees
WHERE department = 'Marketing'
  AND office LIKE 'East%';

-- Finance or Sales employees
SELECT *
FROM employees
WHERE department = 'Finance'
   OR department = 'Sales';

-- Employees outside Information Technology
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

---

## Results Summary

| Investigation | Result |
|---|---:|
| Failed login attempts after 18:00 | 19 |
| Login attempts on 2022-05-08 or 2022-05-09 | 75 |
| Login attempts outside Mexico | 144 |
| First Marketing employee in East building | `elarson` |
| First Sales employee returned | `lrodriqu` |
| Employees not in Information Technology | 161 |

---

## Security Relevance

The queries demonstrate how SQL can support common security operations, including:

- Investigating suspicious login behavior
- Reviewing activity within a defined incident window
- Excluding known geographic locations from analysis
- Identifying employees affected by security updates
- Targeting departments or office locations
- Reducing large datasets to only relevant security records

---

## Summary

I used SQL filters to investigate login activity and identify employees whose machines required security updates. I applied `AND`, `OR`, and `NOT` to combine or exclude conditions, and used `LIKE` with the `%` wildcard to match location and country patterns. These techniques allowed me to retrieve focused, security-relevant records from the `log_in_attempts` and `employees` tables efficiently.

---

## Portfolio Self-Assessment Checklist

- [x] Included a project description
- [x] Included typed SQL queries suitable for a portfolio
- [x] Explained the purpose of each query
- [x] Demonstrated filtering by date and time
- [x] Demonstrated `AND` and `OR`
- [x] Demonstrated `NOT`
- [x] Demonstrated `LIKE` with `%`
- [x] Included a final summary
