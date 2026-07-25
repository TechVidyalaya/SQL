
# Chapter 12: Views

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand what a View is.
- Create and use SQL Views.
- Modify and delete Views.
- Learn the advantages and limitations of Views.
- Use Views in real-world applications.

---

# What is a View?

A **View** is a virtual table created from one or more SQL queries.

Unlike a regular table, a View does **not** store data permanently. It stores only the SQL query.

Whenever you query a View, MySQL executes the underlying SQL statement and returns the latest data.

---

# Why Use Views?

Views help to:

- Simplify complex SQL queries.
- Hide unnecessary columns.
- Improve data security.
- Provide reusable queries.
- Present data in a user-friendly format.

---

# Sample Tables

## employees

| employee_id | employee_name | department_id | salary |
|-------------|---------------|---------------|---------|
| 101 | Rahul | 1 | 65000 |
| 102 | Priya | 2 | 50000 |
| 103 | Amit | 1 | 72000 |

---

## departments

| department_id | department_name |
|---------------|-----------------|
| 1 | IT |
| 2 | HR |

---

# Creating a View

## Syntax

```sql
CREATE VIEW view_name AS
SELECT column_list
FROM table_name
WHERE condition;
```

---

## Example

Create a View to display employee names and salaries.

```sql
CREATE VIEW employee_view AS
SELECT employee_name,
       salary
FROM employees;
```

---

# Using a View

Once created, a View can be queried like a table.

```sql
SELECT *
FROM employee_view;
```

### Output

| employee_name | salary |
|---------------|---------|
| Rahul | 65000 |
| Priya | 50000 |
| Amit | 72000 |

---

# Creating a View with JOIN

Views are commonly created using multiple tables.

```sql
CREATE VIEW employee_department_view AS

SELECT
    e.employee_name,
    d.department_name,
    e.salary

FROM employees e

INNER JOIN departments d
ON e.department_id = d.department_id;
```

---

# Querying the View

```sql
SELECT *
FROM employee_department_view;
```

### Output

| Employee | Department | Salary |
|-----------|------------|---------|
| Rahul | IT | 65000 |
| Priya | HR | 50000 |
| Amit | IT | 72000 |

---

# Updating Data Through a View

If the View is based on a single table, updates are often allowed.

```sql
UPDATE employee_view
SET salary = 70000
WHERE employee_name = 'Rahul';
```

This updates the underlying **employees** table.

---

# Replacing a View

Use `CREATE OR REPLACE VIEW` to modify an existing View.

```sql
CREATE OR REPLACE VIEW employee_view AS

SELECT
    employee_name,
    salary,
    department_id

FROM employees;
```

---

# Viewing Existing Views

Display all tables and views.

```sql
SHOW FULL TABLES
WHERE TABLE_TYPE = 'VIEW';
```

---

# Viewing View Definition

```sql
SHOW CREATE VIEW employee_view;
```

This displays the SQL statement used to create the View.

---

# Dropping a View

Delete a View permanently.

```sql
DROP VIEW employee_view;
```

Only the View is removed.

The original tables remain unchanged.

---

# View vs Table

| View | Table |
|------|-------|
| Virtual table | Physical table |
| Stores SQL query | Stores actual data |
| Uses existing table data | Stores its own records |
| Can simplify complex queries | Holds original data |

---

# Advantages of Views

- Hide sensitive columns.
- Simplify complex joins.
- Improve code reusability.
- Provide consistent query results.
- Enhance database security.

---

# Limitations of Views

- Some Views cannot be updated.
- Complex Views may impact performance.
- Views depend on the underlying tables.
- Dropping a table may invalidate dependent Views.

---

# Practical Example

Create a View for high-paid employees.

```sql
CREATE VIEW high_salary_employees AS

SELECT
    employee_name,
    salary

FROM employees

WHERE salary > 60000;
```

Use the View.

```sql
SELECT *
FROM high_salary_employees;
```

---

# Best Practices

- Use Views to simplify frequently used queries.
- Give Views meaningful names.
- Avoid creating unnecessary nested Views.
- Use Views to restrict access to sensitive data.
- Document the purpose of each View.

---

# Summary

In this chapter, you learned:

- What a View is.
- Creating Views.
- Querying Views.
- Updating Views.
- Replacing Views.
- Dropping Views.
- Advantages and limitations of Views.

---

# Key Terms

- View
- Virtual Table
- CREATE VIEW
- CREATE OR REPLACE VIEW
- DROP VIEW
- SHOW CREATE VIEW

---

# Practice Questions

### Multiple Choice Questions

**1. A View is a:**

A. Physical table

B. Virtual table

C. Database

D. Stored Procedure

> **Answer:** B

---

**2. Which command creates a View?**

A. CREATE TABLE

B. CREATE VIEW

C. NEW VIEW

D. MAKE VIEW

> **Answer:** B

---

**3. Which command deletes a View?**

A. DELETE VIEW

B. REMOVE VIEW

C. DROP VIEW

D. TRUNCATE VIEW

> **Answer:** C

---

**4. Does deleting a View delete the original table?**

A. Yes

B. No

> **Answer:** B

---

# Hands-on Exercise

Create the following View:

```sql
CREATE VIEW employee_summary AS

SELECT
    employee_name,
    salary
FROM employees;
```

---

Display the View.

```sql
SELECT *
FROM employee_summary;
```

---

Replace the View.

```sql
CREATE OR REPLACE VIEW employee_summary AS

SELECT
    employee_name,
    salary,
    department_id
FROM employees;
```

---

Delete the View.

```sql
DROP VIEW employee_summary;
```

---

# Mini Challenge

Using the `employees` and `departments` tables:

1. Create a View showing employee names and department names.
2. Create a View showing employees earning more than 60,000.
3. Display all records from both Views.
4. Replace one View by adding the salary column.
5. Delete the View.

---

## Interview Tips

- A **View** is a virtual table that stores a SQL query, not the actual data.
- Changes made to the underlying tables are automatically reflected in the View.
- Views are commonly used for **security**, **simplifying complex queries**, and **reusability**.
- Simple Views based on a single table are usually updatable, while complex Views involving joins or aggregate functions may not be.

---

## Next Chapter

**Chapter 13: Indexes**
