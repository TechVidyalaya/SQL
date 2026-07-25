# Chapter 8: GROUP BY and HAVING

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand the purpose of `GROUP BY`.
- Group records based on one or more columns.
- Use aggregate functions with `GROUP BY`.
- Filter grouped data using `HAVING`.
- Differentiate between `WHERE` and `HAVING`.
- Write summary reports using SQL.

---

# Introduction

In many real-world applications, we need summary information rather than individual records.

Examples:

- Total salary department-wise
- Number of employees in each department
- Average salary by city
- Maximum salary in each department

SQL provides the **GROUP BY** clause to perform these operations.

---

# Sample Table

```sql
employees
```

| employee_id | employee_name | department | salary | city |
|--------------|--------------|------------|---------|------|
| 1 | Rahul | IT | 65000 | Bhubaneswar |
| 2 | Priya | HR | 50000 | Cuttack |
| 3 | Amit | Finance | 75000 | Delhi |
| 4 | Sneha | IT | 62000 | Bangalore |
| 5 | Karan | HR | 48000 | Bhubaneswar |
| 6 | Neha | IT | 70000 | Delhi |

---

# What is GROUP BY?

`GROUP BY` combines rows that have the same values into summary groups.

Instead of displaying every row, SQL returns one result for each group.

---

# Syntax

```sql
SELECT column_name,
       aggregate_function(column_name)
FROM table_name
GROUP BY column_name;
```

---

# COUNT()

Count employees in each department.

```sql
SELECT department,
       COUNT(*) AS total_employees
FROM employees
GROUP BY department;
```

### Output

| Department | Total Employees |
|------------|-----------------|
| IT | 3 |
| HR | 2 |
| Finance | 1 |

---

# SUM()

Find the total salary of each department.

```sql
SELECT department,
       SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

---

# AVG()

Find the average salary.

```sql
SELECT department,
       AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

---

# MAX()

Highest salary in each department.

```sql
SELECT department,
       MAX(salary) AS highest_salary
FROM employees
GROUP BY department;
```

---

# MIN()

Lowest salary in each department.

```sql
SELECT department,
       MIN(salary) AS lowest_salary
FROM employees
GROUP BY department;
```

---

# Grouping by Multiple Columns

```sql
SELECT city,
       department,
       COUNT(*) AS employees
FROM employees
GROUP BY city, department;
```

This creates separate groups for every city and department combination.

---

# HAVING Clause

The `HAVING` clause filters grouped data.

It works **after** `GROUP BY`.

---

# Syntax

```sql
SELECT column_name,
       aggregate_function(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

---

# Example

Display only departments having more than two employees.

```sql
SELECT department,
       COUNT(*) AS total_employees
FROM employees
GROUP BY department
HAVING COUNT(*) > 2;
```

### Output

| Department | Total Employees |
|------------|-----------------|
| IT | 3 |

---

# Another Example

Departments with an average salary greater than 60,000.

```sql
SELECT department,
       AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

---

# WHERE vs HAVING

| WHERE | HAVING |
|--------|---------|
| Filters individual rows | Filters grouped rows |
| Used before GROUP BY | Used after GROUP BY |
| Cannot use aggregate functions | Can use aggregate functions |

---

# Example Using WHERE and HAVING

Display departments with employees earning more than 50,000 and having an average salary greater than 60,000.

```sql
SELECT department,
       AVG(salary) AS average_salary
FROM employees
WHERE salary > 50000
GROUP BY department
HAVING AVG(salary) > 60000;
```

Execution order:

1. WHERE
2. GROUP BY
3. Aggregate Functions
4. HAVING
5. ORDER BY

---

# GROUP BY with ORDER BY

Display departments sorted by average salary.

```sql
SELECT department,
       AVG(salary) AS average_salary
FROM employees
GROUP BY department
ORDER BY average_salary DESC;
```

---

# Practical Example

Display cities having at least two employees.

```sql
SELECT city,
       COUNT(*) AS total_employees
FROM employees
GROUP BY city
HAVING COUNT(*) >= 2;
```

---

# Best Practices

- Use `GROUP BY` only when summarising data.
- Use meaningful aliases with aggregate functions.
- Use `WHERE` to reduce rows before grouping.
- Use `HAVING` to filter summary results.
- Combine `GROUP BY` with `ORDER BY` for better readability.

---

# Summary

In this chapter, you learned:

- GROUP BY
- Aggregate functions
- HAVING
- WHERE vs HAVING
- Grouping by multiple columns
- ORDER BY with GROUP BY

---

# Key Terms

- GROUP BY
- HAVING
- COUNT()
- SUM()
- AVG()
- MAX()
- MIN()
- Aggregate Function

---

# Practice Questions

### Multiple Choice Questions

**1. Which clause groups rows with similar values?**

A. ORDER BY

B. GROUP BY

C. HAVING

D. DISTINCT

> **Answer:** B

---

**2. Which clause filters grouped results?**

A. WHERE

B. FILTER

C. HAVING

D. LIMIT

> **Answer:** C

---

**3. Which function calculates the average?**

A. COUNT()

B. SUM()

C. AVG()

D. TOTAL()

> **Answer:** C

---

**4. Which clause executes before GROUP BY?**

A. HAVING

B. WHERE

C. ORDER BY

D. LIMIT

> **Answer:** B

---

# Hands-on Exercise

## 1. Count employees in each department.

```sql
SELECT department,
       COUNT(*)
FROM employees
GROUP BY department;
```

---

## 2. Find the total salary of each department.

```sql
SELECT department,
       SUM(salary)
FROM employees
GROUP BY department;
```

---

## 3. Find the average salary of each department.

```sql
SELECT department,
       AVG(salary)
FROM employees
GROUP BY department;
```

---

## 4. Display departments with more than one employee.

```sql
SELECT department,
       COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 1;
```

---

## 5. Display cities ordered by employee count.

```sql
SELECT city,
       COUNT(*) AS total_employees
FROM employees
GROUP BY city
ORDER BY total_employees DESC;
```

---

# Mini Challenge

Using the `employees` table, write SQL queries to:

1. Find the total salary of each city.
2. Find the highest salary in every department.
3. Find departments having more than two employees.
4. Find cities with an average salary greater than 55,000.
5. Display departments sorted by total salary.

---

## Interview Tips

- `WHERE` filters rows **before** grouping.
- `HAVING` filters groups **after** grouping.
- Every column in the `SELECT` clause that is not an aggregate function must appear in the `GROUP BY` clause.
- `GROUP BY` is frequently used with `COUNT()`, `SUM()`, `AVG()`, `MIN()`, and `MAX()`.

---

## Next Chapter

**Chapter 9: Joins**
