# Chapter 13: Indexes

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand what an Index is.
- Learn why indexes improve query performance.
- Create and remove indexes.
- Understand different types of indexes.
- Identify when to use and avoid indexes.
- Analyze query performance using indexes.

---

# What is an Index?

An **Index** is a special data structure that helps the database locate rows quickly without scanning the entire table.

Think of an index in a database like the index at the end of a book.

Instead of reading every page to find a topic, you use the index to jump directly to the required page.

Similarly, a database uses an index to find records much faster.

---

# Why Do We Need Indexes?

Imagine an employee table containing **10 million records**.

Without an index:

- Database scans every row.
- More disk reads.
- Slower query execution.

With an index:

- Database directly locates matching records.
- Fewer disk reads.
- Faster execution.

---

# Without Index

```
Employees Table

Row 1
Row 2
Row 3
...
Row 10,000,000
```

Database checks every row.

---

# With Index

```
Employee Name Index

Amit  ------> Row 245
Priya ------> Row 8921
Rahul ------> Row 154
Sneha ------> Row 6753
```

Database jumps directly to the required row.

---

# When Are Indexes Used?

Indexes are useful when columns are frequently used in:

- WHERE
- JOIN
- ORDER BY
- GROUP BY

Example:

```sql
SELECT *
FROM employees
WHERE employee_id = 105;
```

If `employee_id` is indexed, the query executes much faster.

---

# Creating an Index

## Syntax

```sql
CREATE INDEX index_name
ON table_name(column_name);
```

---

## Example

```sql
CREATE INDEX idx_employee_name
ON employees(employee_name);
```

Now searches on `employee_name` become faster.

---

# Viewing Indexes

```sql
SHOW INDEX
FROM employees;
```

This displays all indexes created on the table.

---

# Dropping an Index

## Syntax

```sql
DROP INDEX index_name
ON table_name;
```

---

## Example

```sql
DROP INDEX idx_employee_name
ON employees;
```

---

# Unique Index

A **Unique Index** ensures that duplicate values cannot exist.

```sql
CREATE UNIQUE INDEX idx_email
ON employees(email);
```

Now two employees cannot have the same email address.

---

# Composite Index

A composite index is created on multiple columns.

```sql
CREATE INDEX idx_department_salary
ON employees(department, salary);
```

Useful for queries like:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 60000;
```

---

# Primary Key Index

Every Primary Key automatically creates a unique index.

```sql
CREATE TABLE employees (

    employee_id INT PRIMARY KEY,

    employee_name VARCHAR(100)

);
```

No additional index is required for `employee_id`.

---

# Performance Example

Without Index

```sql
SELECT *
FROM employees
WHERE email='rahul@gmail.com';
```

Database checks every row.

---

With Index

```sql
CREATE INDEX idx_email
ON employees(email);
```

Now the database directly locates the required record.

---

# EXPLAIN Statement

Use `EXPLAIN` to see how MySQL executes a query.

```sql
EXPLAIN
SELECT *
FROM employees
WHERE employee_name='Rahul';
```

This helps determine whether an index is being used.

---

# Advantages of Indexes

- Faster searches
- Faster sorting
- Faster joins
- Improved query performance
- Efficient retrieval of large datasets

---

# Disadvantages of Indexes

- Consume additional storage.
- Slow down `INSERT`, `UPDATE`, and `DELETE` operations.
- Too many indexes reduce overall performance.
- Require maintenance as data changes.

---

# When Should You Create an Index?

Create indexes on columns that are:

- Frequently searched
- Used in JOIN conditions
- Used in WHERE clauses
- Used for sorting (`ORDER BY`)
- Used in grouping (`GROUP BY`)

---

# When Should You Avoid Indexes?

Avoid indexing columns that:

- Have very few unique values (e.g., Gender, Status).
- Are rarely searched.
- Are frequently updated.
- Belong to very small tables.

---

# Best Practices

- Create indexes only when needed.
- Prefer indexing frequently searched columns.
- Remove unused indexes.
- Use composite indexes carefully.
- Monitor query performance with `EXPLAIN`.

---

# Summary

In this chapter, you learned:

- What an Index is.
- Why indexes improve performance.
- Creating and deleting indexes.
- Unique and composite indexes.
- Using `EXPLAIN`.
- Advantages and disadvantages of indexes.

---

# Key Terms

- Index
- Unique Index
- Composite Index
- Primary Key Index
- EXPLAIN
- Query Optimization

---

# Practice Questions

### Multiple Choice Questions

**1. What is the primary purpose of an index?**

A. Store backup data

B. Improve query performance

C. Delete duplicate rows

D. Encrypt data

> **Answer:** B

---

**2. Which command creates an index?**

A.

```sql
ADD INDEX
```

B.

```sql
CREATE INDEX
```

C.

```sql
NEW INDEX
```

D.

```sql
MAKE INDEX
```

> **Answer:** B

---

**3. Which command displays indexes of a table?**

A.

```sql
SHOW INDEX
```

B.

```sql
SHOW TABLES
```

C.

```sql
DESCRIBE
```

D.

```sql
SHOW DATABASES
```

> **Answer:** A

---

**4. Which statement is true about indexes?**

A. They always improve every operation.

B. They slow down data retrieval.

C. They improve read performance but may slow write operations.

D. They are mandatory for every column.

> **Answer:** C

---

# Hands-on Exercise

Create an `employees` table.

```sql
CREATE TABLE employees (

    employee_id INT PRIMARY KEY,

    employee_name VARCHAR(100),

    email VARCHAR(100),

    department VARCHAR(50),

    salary DECIMAL(10,2)

);
```

---

### Create an Index

```sql
CREATE INDEX idx_employee_name
ON employees(employee_name);
```

---

### Create a Unique Index

```sql
CREATE UNIQUE INDEX idx_email
ON employees(email);
```

---

### Display Indexes

```sql
SHOW INDEX
FROM employees;
```

---

### Analyze Query Execution

```sql
EXPLAIN
SELECT *
FROM employees
WHERE employee_name='Rahul';
```

---

### Drop an Index

```sql
DROP INDEX idx_employee_name
ON employees;
```

---

# Mini Challenge

Using the `employees` table:

1. Create an index on the `department` column.
2. Create a composite index on `(department, salary)`.
3. Create a unique index on the `email` column.
4. Display all indexes.
5. Use `EXPLAIN` to verify whether an index is used for a search query.

---

## Interview Tips

- Indexes significantly improve **SELECT** query performance but can slow down **INSERT**, **UPDATE**, and **DELETE** operations.
- A **PRIMARY KEY** automatically creates a unique index.
- Composite indexes are most effective when queries filter on the leading column(s).
- Use `EXPLAIN` to understand how MySQL executes a query and whether an index is being utilized.

---

## Next Chapter

**Chapter 14: Transactions**
