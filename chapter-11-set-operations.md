# Chapter 11: Set Operations

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand what Set Operations are.
- Combine the results of multiple queries.
- Use `UNION` and `UNION ALL`.
- Understand `INTERSECT` and `EXCEPT`.
- Learn MySQL alternatives for unsupported set operations.
- Apply set operations in real-world scenarios.

---

# What are Set Operations?

Set operations combine the results of two or more `SELECT` statements into a single result.

Think of it as combining two lists into one.

Each `SELECT` statement must have:

- The same number of columns
- Similar data types
- Columns in the same order

---

# Types of Set Operations

- UNION
- UNION ALL
- INTERSECT *(Not supported directly in MySQL)*
- EXCEPT *(Not supported directly in MySQL)*

---

# Sample Tables

## current_employees

| employee_id | employee_name |
|--------------|---------------|
| 101 | Rahul |
| 102 | Priya |
| 103 | Amit |

---

## former_employees

| employee_id | employee_name |
|--------------|---------------|
| 103 | Amit |
| 104 | Sneha |
| 105 | Karan |

---

# UNION

`UNION` combines the results of two queries and removes duplicate rows.

## Syntax

```sql
SELECT column_list
FROM table1

UNION

SELECT column_list
FROM table2;
```

---

## Example

```sql
SELECT employee_name
FROM current_employees

UNION

SELECT employee_name
FROM former_employees;
```

### Output

| Employee Name |
|---------------|
| Rahul |
| Priya |
| Amit |
| Sneha |
| Karan |

Notice that **Amit** appears only once.

---

# UNION ALL

`UNION ALL` combines all rows, including duplicates.

```sql
SELECT employee_name
FROM current_employees

UNION ALL

SELECT employee_name
FROM former_employees;
```

### Output

| Employee Name |
|---------------|
| Rahul |
| Priya |
| Amit |
| Amit |
| Sneha |
| Karan |

---

# UNION vs UNION ALL

| UNION | UNION ALL |
|--------|-----------|
| Removes duplicates | Keeps duplicates |
| Slightly slower | Faster |
| Used when unique results are required | Used when duplicates are acceptable |

---

# Rules for UNION

The queries must have:

✔ Same number of columns

✔ Compatible data types

✔ Similar column order

---

## Correct Example

```sql
SELECT employee_id,
       employee_name
FROM current_employees

UNION

SELECT employee_id,
       employee_name
FROM former_employees;
```

---

## Incorrect Example

```sql
SELECT employee_id,
       employee_name
FROM current_employees

UNION

SELECT employee_name
FROM former_employees;
```

This produces an error because the number of columns is different.

---

# ORDER BY with UNION

`ORDER BY` is written only once, after the final query.

```sql
SELECT employee_name
FROM current_employees

UNION

SELECT employee_name
FROM former_employees

ORDER BY employee_name;
```

---

# INTERSECT

`INTERSECT` returns only the common rows from both queries.

Example:

```
Current Employees
Rahul
Priya
Amit

Former Employees
Amit
Sneha
```

Result:

```
Amit
```

> **Note:** MySQL does **not** support `INTERSECT` directly.

---

# MySQL Alternative for INTERSECT

Use an `INNER JOIN`.

```sql
SELECT c.employee_name
FROM current_employees c
INNER JOIN former_employees f
ON c.employee_id = f.employee_id;
```

---

# EXCEPT

`EXCEPT` returns rows from the first query that are not present in the second query.

Example

```
Current Employees
Rahul
Priya
Amit

Former Employees
Amit
Sneha
```

Result

```
Rahul
Priya
```

> **Note:** MySQL does **not** support `EXCEPT` directly.

---

# MySQL Alternative for EXCEPT

Use a `LEFT JOIN`.

```sql
SELECT c.employee_name
FROM current_employees c
LEFT JOIN former_employees f
ON c.employee_id = f.employee_id
WHERE f.employee_id IS NULL;
```

---

# Practical Example

Combine employees from two company branches.

### branch_a

| Employee |
|----------|
| Rahul |
| Priya |

### branch_b

| Employee |
|----------|
| Amit |
| Priya |

```sql
SELECT employee_name
FROM branch_a

UNION

SELECT employee_name
FROM branch_b;
```

Result

```
Rahul
Priya
Amit
```

---

# Best Practices

- Use `UNION` when duplicate records should be removed.
- Use `UNION ALL` for better performance if duplicates are acceptable.
- Ensure both queries return compatible columns.
- Apply `ORDER BY` only once at the end.
- Use `JOIN` techniques in MySQL to simulate `INTERSECT` and `EXCEPT`.

---

# Summary

In this chapter, you learned:

- Set operations
- UNION
- UNION ALL
- INTERSECT
- EXCEPT
- MySQL alternatives for unsupported operations

---

# Key Terms

- UNION
- UNION ALL
- INTERSECT
- EXCEPT
- INNER JOIN
- LEFT JOIN

---

# Practice Questions

### Multiple Choice Questions

**1. Which operator removes duplicate rows?**

A. UNION ALL

B. UNION

C. JOIN

D. GROUP BY

> **Answer:** B

---

**2. Which operator keeps duplicate rows?**

A. UNION

B. UNION ALL

C. DISTINCT

D. GROUP BY

> **Answer:** B

---

**3. Which set operation is not directly supported in MySQL?**

A. UNION

B. UNION ALL

C. INTERSECT

D. Both INTERSECT and EXCEPT

> **Answer:** D

---

**4. Which MySQL operation can simulate INTERSECT?**

A. LEFT JOIN

B. RIGHT JOIN

C. INNER JOIN

D. CROSS JOIN

> **Answer:** C

---

# Hands-on Exercise

Create two tables:

```sql
CREATE TABLE current_employees (
    employee_id INT,
    employee_name VARCHAR(100)
);

CREATE TABLE former_employees (
    employee_id INT,
    employee_name VARCHAR(100)
);
```

Insert sample records and perform the following:

### 1. Combine all employees without duplicates.

```sql
SELECT employee_name
FROM current_employees

UNION

SELECT employee_name
FROM former_employees;
```

---

### 2. Combine all employees including duplicates.

```sql
SELECT employee_name
FROM current_employees

UNION ALL

SELECT employee_name
FROM former_employees;
```

---

### 3. Display common employees.

```sql
SELECT c.employee_name
FROM current_employees c
INNER JOIN former_employees f
ON c.employee_id = f.employee_id;
```

---

### 4. Display employees present only in the current employees table.

```sql
SELECT c.employee_name
FROM current_employees c
LEFT JOIN former_employees f
ON c.employee_id = f.employee_id
WHERE f.employee_id IS NULL;
```

---

# Mini Challenge

Using two tables (`branch_a` and `branch_b`), write SQL queries to:

1. Display all employees without duplicates.
2. Display all employees including duplicates.
3. Find employees working in both branches.
4. Find employees working only in Branch A.
5. Sort the final result alphabetically.

---

## Interview Tips

- `UNION` automatically removes duplicate rows.
- `UNION ALL` is faster because it does not perform duplicate elimination.
- Both queries in a set operation must return the same number of columns with compatible data types.
- MySQL does not support `INTERSECT` and `EXCEPT`; use `INNER JOIN` and `LEFT JOIN` instead.

---

## Next Chapter

**Chapter 12: Views**
