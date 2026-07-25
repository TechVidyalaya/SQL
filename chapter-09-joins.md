# Chapter 9: Joins

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand why joins are needed.
- Learn different types of SQL joins.
- Use INNER JOIN, LEFT JOIN, RIGHT JOIN, and CROSS JOIN.
- Understand SELF JOIN.
- Write queries by combining data from multiple tables.

---

# What are Joins?

In a relational database, data is often stored across multiple tables to reduce duplication.

A **JOIN** combines rows from two or more tables based on a related column.

For example:

- Employee details are stored in the **employees** table.
- Department details are stored in the **departments** table.

Using a JOIN, we can display employee names along with their department names.

---

# Sample Tables

## departments

| department_id | department_name |
|---------------|-----------------|
| 1 | IT |
| 2 | HR |
| 3 | Finance |
| 4 | Sales |

---

## employees

| employee_id | employee_name | department_id | salary |
|-------------|---------------|---------------|---------|
| 101 | Rahul | 1 | 65000 |
| 102 | Priya | 2 | 50000 |
| 103 | Amit | 1 | 72000 |
| 104 | Sneha | 3 | 68000 |
| 105 | Karan | NULL | 45000 |

---

# Why Use Joins?

Without joins, data would be duplicated in every table.

Instead of storing the department name repeatedly:

| employee_name | department_id |
|---------------|---------------|
| Rahul | 1 |
| Priya | 2 |

We store department details separately:

| department_id | department_name |
|---------------|-----------------|
| 1 | IT |
| 2 | HR |

This improves consistency and reduces storage.

---

# Types of Joins

- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- CROSS JOIN
- SELF JOIN

---

# INNER JOIN

Returns only the matching records from both tables.

## Syntax

```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

---

## Example

```sql
SELECT
    e.employee_name,
    d.department_name,
    e.salary
FROM employees e
INNER JOIN departments d
ON e.department_id = d.department_id;
```

### Output

| Employee | Department | Salary |
|-----------|------------|---------|
| Rahul | IT | 65000 |
| Priya | HR | 50000 |
| Amit | IT | 72000 |
| Sneha | Finance | 68000 |

Karan is not shown because there is no matching department.

---

# LEFT JOIN

Returns:

- All rows from the left table.
- Matching rows from the right table.
- NULL where no match exists.

## Example

```sql
SELECT
    e.employee_name,
    d.department_name
FROM employees e
LEFT JOIN departments d
ON e.department_id = d.department_id;
```

### Output

| Employee | Department |
|-----------|------------|
| Rahul | IT |
| Priya | HR |
| Amit | IT |
| Sneha | Finance |
| Karan | NULL |

---

# RIGHT JOIN

Returns:

- All rows from the right table.
- Matching rows from the left table.
- NULL where no match exists.

## Example

```sql
SELECT
    e.employee_name,
    d.department_name
FROM employees e
RIGHT JOIN departments d
ON e.department_id = d.department_id;
```

### Output

| Employee | Department |
|-----------|------------|
| Rahul | IT |
| Priya | HR |
| Sneha | Finance |
| NULL | Sales |

The Sales department has no employees.

---

# CROSS JOIN

Returns every possible combination of rows.

If:

- Employees = 5
- Departments = 4

Result = **20 rows**

## Example

```sql
SELECT
    e.employee_name,
    d.department_name
FROM employees e
CROSS JOIN departments d;
```

---

# SELF JOIN

A table can join with itself.

Useful for:

- Employee and Manager relationships
- Parent and Child records
- Categories and Subcategories

---

## Example

### employees

| employee_id | employee_name | manager_id |
|-------------|---------------|------------|
| 1 | Rahul | NULL |
| 2 | Priya | 1 |
| 3 | Amit | 1 |

```sql
SELECT
    e.employee_name,
    m.employee_name AS manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.employee_id;
```

### Output

| Employee | Manager |
|-----------|----------|
| Rahul | NULL |
| Priya | Rahul |
| Amit | Rahul |

---

# Using Table Aliases

Aliases make queries shorter and easier to read.

Instead of:

```sql
employees.employee_name
```

Use:

```sql
e.employee_name
```

Example:

```sql
FROM employees e
INNER JOIN departments d
```

---

# JOIN Comparison

| Join | Returns |
|------|----------|
| INNER JOIN | Matching rows only |
| LEFT JOIN | All left rows + matching right rows |
| RIGHT JOIN | All right rows + matching left rows |
| CROSS JOIN | Every possible combination |
| SELF JOIN | Table joined with itself |

---

# Practical Example

Display employee names, department names, and salaries.

```sql
SELECT
    e.employee_name,
    d.department_name,
    e.salary
FROM employees e
INNER JOIN departments d
ON e.department_id = d.department_id
ORDER BY e.salary DESC;
```

---

# Best Practices

- Use meaningful table aliases.
- Join tables using Primary Key and Foreign Key relationships.
- Select only required columns instead of `SELECT *`.
- Always verify the JOIN condition (`ON` clause).
- Use `LEFT JOIN` when unmatched records should also be displayed.

---

# Summary

In this chapter, you learned:

- Why joins are required.
- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- CROSS JOIN
- SELF JOIN
- Table aliases
- Writing multi-table queries

---

# Key Terms

- JOIN
- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- CROSS JOIN
- SELF JOIN
- Primary Key
- Foreign Key
- Alias

---

# Practice Questions

### Multiple Choice Questions

**1. Which JOIN returns only matching records?**

A. LEFT JOIN

B. RIGHT JOIN

C. INNER JOIN

D. CROSS JOIN

> **Answer:** C

---

**2. Which JOIN returns all rows from the left table?**

A. INNER JOIN

B. LEFT JOIN

C. CROSS JOIN

D. SELF JOIN

> **Answer:** B

---

**3. Which JOIN returns every possible combination of rows?**

A. INNER JOIN

B. CROSS JOIN

C. RIGHT JOIN

D. SELF JOIN

> **Answer:** B

---

**4. Which JOIN is used when a table joins with itself?**

A. LEFT JOIN

B. INNER JOIN

C. SELF JOIN

D. CROSS JOIN

> **Answer:** C

---

# Hands-on Exercise

Create the following tables:

### Departments

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50)
);
```

### Employees

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100),
    department_id INT,
    salary DECIMAL(10,2),
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

Insert sample data and perform:

### 1. Display employee names with department names.

```sql
SELECT
    e.employee_name,
    d.department_name
FROM employees e
INNER JOIN departments d
ON e.department_id = d.department_id;
```

---

### 2. Display all employees even if they have no department.

```sql
SELECT
    e.employee_name,
    d.department_name
FROM employees e
LEFT JOIN departments d
ON e.department_id = d.department_id;
```

---

### 3. Display all departments even if they have no employees.

```sql
SELECT
    e.employee_name,
    d.department_name
FROM employees e
RIGHT JOIN departments d
ON e.department_id = d.department_id;
```

---

# Mini Challenge

Using the `employees` and `departments` tables, write SQL queries to:

1. Display employee names with department names.
2. Display employees without a department.
3. Display departments without employees.
4. Display employees sorted by department and salary.
5. Count the number of employees in each department using a JOIN.

---

## Interview Tips

- `INNER JOIN` is the most commonly used join in interviews and real-world applications.
- `LEFT JOIN` is useful for finding unmatched records.
- A **Primary Key** in one table is commonly referenced as a **Foreign Key** in another.
- Table aliases improve query readability, especially when joining multiple tables.

---

## Next Chapter

**Chapter 10: Subqueries**
