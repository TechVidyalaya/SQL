# Chapter 18: SQL Best Practices

## Learning Objectives

By the end of this chapter, you will be able to:

- Write clean and readable SQL queries.
- Improve SQL query performance.
- Follow database design best practices.
- Write secure SQL code.
- Avoid common SQL mistakes.
- Build production-ready SQL applications.

---

# What are SQL Best Practices?

SQL Best Practices are guidelines that help you write:

- Efficient queries
- Readable code
- Secure applications
- Maintainable databases
- High-performance systems

Following these practices reduces bugs and improves application performance.

---

# Use Meaningful Table and Column Names

❌ Poor Naming

```sql
CREATE TABLE t1 (

    id INT,

    n VARCHAR(100)

);
```

---

✅ Good Naming

```sql
CREATE TABLE employees (

    employee_id INT,

    employee_name VARCHAR(100)

);
```

Meaningful names make the database easier to understand.

---

# Select Only Required Columns

❌ Avoid

```sql
SELECT *
FROM employees;
```

---

✅ Prefer

```sql
SELECT

employee_id,

employee_name,

salary

FROM employees;
```

Selecting only required columns improves performance.

---

# Always Use WHERE Carefully

❌ Dangerous

```sql
DELETE FROM employees;
```

Deletes every record.

---

✅ Safe

```sql
DELETE
FROM employees
WHERE employee_id = 101;
```

Always verify the `WHERE` condition before executing `UPDATE` or `DELETE`.

---

# Use Primary Keys

Every table should have a Primary Key.

```sql
CREATE TABLE employees (

    employee_id INT PRIMARY KEY,

    employee_name VARCHAR(100)

);
```

Benefits:

- Unique identification
- Faster searches
- Better relationships

---

# Use Appropriate Data Types

❌ Poor Choice

```sql
salary VARCHAR(50)
```

---

✅ Better Choice

```sql
salary DECIMAL(10,2)
```

Choosing the correct data type improves storage efficiency and performance.

---

# Normalize Your Database

Avoid duplicate information.

Instead of:

```
Employee
Department
Manager
Department Phone
```

Store department details in a separate table and link using a Foreign Key.

---

# Create Indexes Wisely

Indexes improve search performance.

```sql
CREATE INDEX idx_employee_name
ON employees(employee_name);
```

Do not create unnecessary indexes, as they slow down insert and update operations.

---

# Use Aliases

Aliases improve readability.

```sql
SELECT

e.employee_name,

d.department_name

FROM employees e

JOIN departments d

ON e.department_id = d.department_id;
```

---

# Format SQL Queries Properly

❌ Hard to Read

```sql
SELECT employee_name,salary FROM employees WHERE salary>50000;
```

---

✅ Easy to Read

```sql
SELECT

    employee_name,

    salary

FROM employees

WHERE salary > 50000;
```

Proper formatting makes maintenance easier.

---

# Use Transactions for Critical Operations

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

Transactions ensure data consistency.

---

# Prevent SQL Injection

Never build SQL queries using string concatenation.

❌ Unsafe

```sql
SELECT *
FROM users
WHERE username = '" + username + "';
```

---

✅ Safe

Use **Prepared Statements** (supported by programming languages such as Java, Python, C#, etc.).

```sql
SELECT *
FROM users
WHERE username = ?;
```

---

# Backup Your Database

Regular backups protect against:

- Hardware failures
- Accidental deletion
- Cyber attacks
- Data corruption

Always maintain a backup strategy.

---

# Avoid Duplicate Data

Store information once.

Use:

- Primary Keys
- Foreign Keys
- Normalization

to reduce redundancy.

---

# Comment Complex Queries

Example

```sql
-- Display employees earning more than 60,000

SELECT *

FROM employees

WHERE salary > 60000;
```

Comments make SQL easier to understand.

---

# Use Constraints

Apply constraints whenever possible.

Examples:

```sql
PRIMARY KEY

FOREIGN KEY

UNIQUE

NOT NULL

CHECK
```

Constraints help maintain data integrity.

---

# Limit Large Result Sets

Instead of returning thousands of rows:

```sql
SELECT *
FROM employees
LIMIT 10;
```

Useful during development and testing.

---

# Best Practices Summary

| Best Practice | Benefit |
|---------------|----------|
| Use meaningful names | Better readability |
| Select required columns | Faster queries |
| Use indexes wisely | Better performance |
| Normalize data | Less redundancy |
| Use transactions | Data consistency |
| Use constraints | Better data integrity |
| Format SQL | Easier maintenance |
| Use prepared statements | Better security |

---

# Common Mistakes to Avoid

- Using `SELECT *` unnecessarily.
- Forgetting the `WHERE` clause in `UPDATE` or `DELETE`.
- Creating too many indexes.
- Ignoring normalization.
- Using incorrect data types.
- Not backing up the database.
- Writing unreadable SQL queries.

---

# Real-World Example

Instead of:

```sql
SELECT *
FROM orders;
```

Use:

```sql
SELECT

order_id,

customer_name,

total_amount

FROM orders

WHERE order_date >= '2026-01-01'

ORDER BY order_date DESC

LIMIT 20;
```

This query is more efficient and returns only the required data.

---

# Summary

In this chapter, you learned:

- SQL coding standards.
- Performance optimization techniques.
- Database design best practices.
- Security recommendations.
- Common mistakes to avoid.
- Production-ready SQL development practices.

---

# Key Terms

- SQL Best Practices
- Prepared Statement
- Primary Key
- Foreign Key
- Normalization
- Index
- Transaction
- Constraint
- SQL Injection

---

# Practice Questions

### Multiple Choice Questions

**1. Which query is generally recommended?**

A.

```sql
SELECT *
FROM employees;
```

B.

```sql
SELECT employee_name
FROM employees;
```

> **Answer:** B

---

**2. Which feature helps prevent SQL Injection?**

A. Index

B. View

C. Prepared Statement

D. Trigger

> **Answer:** C

---

**3. Why should transactions be used?**

A. To reduce storage

B. To maintain data consistency

C. To increase duplicate data

D. To remove indexes

> **Answer:** B

---

**4. Which clause limits the number of returned rows?**

A. GROUP BY

B. ORDER BY

C. LIMIT

D. HAVING

> **Answer:** C

---

# Hands-on Exercise

Using the `employees` table:

### Display only required columns.

```sql
SELECT

employee_id,

employee_name,

salary

FROM employees;
```

---

### Display the top 5 highest-paid employees.

```sql
SELECT

employee_name,

salary

FROM employees

ORDER BY salary DESC

LIMIT 5;
```

---

### Create an index.

```sql
CREATE INDEX idx_department
ON employees(department);
```

---

### Display employees in the IT department.

```sql
SELECT

employee_name,

salary

FROM employees

WHERE department = 'IT';
```

---

# Mini Challenge

You are reviewing a database for an Employee Management System.

1. Replace every `SELECT *` query with specific column names.
2. Add a Primary Key and required constraints to the tables.
3. Create an index on a frequently searched column.
4. Rewrite a poorly formatted query into a readable format.
5. Identify one query that should use a transaction.

---

## Interview Tips

- Avoid `SELECT *` in production code; retrieve only the columns you need.
- Always use **Prepared Statements** to protect against SQL Injection.
- Create indexes only on columns that are frequently searched or joined.
- Keep SQL queries readable with proper formatting and meaningful aliases.
- Use transactions for operations that involve multiple related changes.

---

## Next Chapter

**Chapter 19: SQL Interview Questions**
