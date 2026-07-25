# Chapter 10: Subqueries

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand what a subquery is.
- Write subqueries inside `SELECT`, `WHERE`, and `FROM` clauses.
- Use single-row and multi-row subqueries.
- Use correlated subqueries.
- Solve real-world problems using subqueries.

---

# What is a Subquery?

A **Subquery** (also called a **Nested Query**) is a query written inside another SQL query.

The inner query executes first, and its result is used by the outer query.

---

# Syntax

```sql
SELECT column_name
FROM table_name
WHERE column_name OPERATOR
(
    SELECT column_name
    FROM another_table
);
```

---

# Sample Table

## employees

| employee_id | employee_name | department_id | salary |
|-------------|---------------|---------------|---------|
| 101 | Rahul | 1 | 65000 |
| 102 | Priya | 2 | 50000 |
| 103 | Amit | 1 | 72000 |
| 104 | Sneha | 3 | 68000 |
| 105 | Karan | 2 | 45000 |

---

## departments

| department_id | department_name |
|---------------|-----------------|
| 1 | IT |
| 2 | HR |
| 3 | Finance |

---

# Single-Row Subquery

A single-row subquery returns only one value.

## Example

Display employees earning more than the average salary.

```sql
SELECT employee_name,
       salary
FROM employees
WHERE salary >
(
    SELECT AVG(salary)
    FROM employees
);
```

### Execution

1. Calculate the average salary.
2. Compare each employee's salary with the average.
3. Display matching employees.

---

# Subquery with WHERE

Display employees who work in the IT department.

```sql
SELECT employee_name
FROM employees
WHERE department_id =
(
    SELECT department_id
    FROM departments
    WHERE department_name = 'IT'
);
```

---

# Multi-Row Subquery

A multi-row subquery returns multiple values.

Use operators like:

- IN
- ANY
- ALL

---

## Example using IN

Display employees working in IT or Finance.

```sql
SELECT employee_name
FROM employees
WHERE department_id IN
(
    SELECT department_id
    FROM departments
    WHERE department_name IN ('IT', 'Finance')
);
```

---

# ANY Operator

Returns TRUE if the condition matches **at least one** value.

Example:

Display employees earning more than **any HR employee**.

```sql
SELECT employee_name,
       salary
FROM employees
WHERE salary > ANY
(
    SELECT salary
    FROM employees
    WHERE department_id = 2
);
```

---

# ALL Operator

Returns TRUE only if the condition satisfies **every** value.

Example:

Display employees earning more than **all HR employees**.

```sql
SELECT employee_name,
       salary
FROM employees
WHERE salary > ALL
(
    SELECT salary
    FROM employees
    WHERE department_id = 2
);
```

---

# EXISTS Operator

Checks whether a subquery returns any rows.

```sql
SELECT department_name
FROM departments d
WHERE EXISTS
(
    SELECT *
    FROM employees e
    WHERE e.department_id = d.department_id
);
```

Displays only departments that have employees.

---

# NOT EXISTS

Displays departments without employees.

```sql
SELECT department_name
FROM departments d
WHERE NOT EXISTS
(
    SELECT *
    FROM employees e
    WHERE e.department_id = d.department_id
);
```

---

# Subquery in SELECT

Display employee names along with the total number of employees.

```sql
SELECT
    employee_name,
    (
        SELECT COUNT(*)
        FROM employees
    ) AS total_employees
FROM employees;
```

---

# Subquery in FROM

```sql
SELECT
    AVG(salary) AS average_salary
FROM
(
    SELECT salary
    FROM employees
    WHERE salary > 50000
) AS employee_data;
```

---

# Correlated Subquery

A correlated subquery depends on the outer query.

It executes once for every row returned by the outer query.

---

## Example

Display employees earning more than the average salary of their own department.

```sql
SELECT employee_name,
       department_id,
       salary
FROM employees e
WHERE salary >
(
    SELECT AVG(salary)
    FROM employees
    WHERE department_id = e.department_id
);
```

The inner query runs separately for each department.

---

# Subquery vs JOIN

| Subquery | JOIN |
|-----------|------|
| Query inside another query | Combines tables |
| Easier for simple lookups | Better for displaying related data |
| May be slower for large datasets | Often performs better |

---

# Practical Example

Display the highest-paid employee.

```sql
SELECT employee_name,
       salary
FROM employees
WHERE salary =
(
    SELECT MAX(salary)
    FROM employees
);
```

---

# Best Practices

- Keep subqueries simple and readable.
- Use aliases for better clarity.
- Prefer JOINs when retrieving related data from multiple tables.
- Use correlated subqueries only when necessary.
- Test the inner query separately before combining it with the outer query.

---

# Summary

In this chapter, you learned:

- What a subquery is.
- Single-row subqueries.
- Multi-row subqueries.
- `IN`, `ANY`, and `ALL`.
- `EXISTS` and `NOT EXISTS`.
- Correlated subqueries.
- Differences between subqueries and joins.

---

# Key Terms

- Subquery
- Nested Query
- Correlated Subquery
- IN
- ANY
- ALL
- EXISTS
- NOT EXISTS

---

# Practice Questions

### Multiple Choice Questions

**1. A subquery is also known as a:**

A. Join

B. Nested Query

C. Function

D. Trigger

> **Answer:** B

---

**2. Which operator is used when a subquery returns multiple values?**

A. LIKE

B. BETWEEN

C. IN

D. LIMIT

> **Answer:** C

---

**3. Which operator checks whether a subquery returns any rows?**

A. EXISTS

B. DISTINCT

C. ORDER BY

D. GROUP BY

> **Answer:** A

---

**4. Which subquery executes once for every row of the outer query?**

A. Single-row Subquery

B. Multi-row Subquery

C. Correlated Subquery

D. Aggregate Subquery

> **Answer:** C

---

# Hands-on Exercise

## 1. Display employees earning more than the average salary.

```sql
SELECT employee_name,
       salary
FROM employees
WHERE salary >
(
    SELECT AVG(salary)
    FROM employees
);
```

---

## 2. Display employees working in the HR department.

```sql
SELECT employee_name
FROM employees
WHERE department_id =
(
    SELECT department_id
    FROM departments
    WHERE department_name = 'HR'
);
```

---

## 3. Display the highest-paid employee.

```sql
SELECT employee_name,
       salary
FROM employees
WHERE salary =
(
    SELECT MAX(salary)
    FROM employees
);
```

---

## 4. Display departments that have employees.

```sql
SELECT department_name
FROM departments d
WHERE EXISTS
(
    SELECT *
    FROM employees e
    WHERE e.department_id = d.department_id
);
```

---

# Mini Challenge

Using the `employees` and `departments` tables, write SQL queries to:

1. Display employees earning below the average salary.
2. Display the department with the highest average salary.
3. Display employees working in the Finance department using a subquery.
4. Display departments without employees.
5. Display employees earning more than all employees in the HR department.

---

## Interview Tips

- A subquery executes **inside** another SQL statement.
- `IN` is used when the subquery returns multiple values.
- `EXISTS` is often more efficient than `IN` for checking the existence of rows.
- Correlated subqueries execute once per row and may be slower on large datasets.
- For retrieving related data from multiple tables, a `JOIN` is often preferred over a subquery.

---

## Next Chapter

**Chapter 11: Set Operations**
