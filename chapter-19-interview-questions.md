
# Chapter 19: SQL Interview Questions

## Learning Objectives

By the end of this chapter, you will be able to:

- Revise important SQL concepts.
- Prepare for SQL technical interviews.
- Answer commonly asked SQL questions.
- Practice query-based interview problems.
- Improve confidence for coding rounds.

---

# Interview Preparation Tips

Before attending an interview, make sure you are comfortable with:

- SQL syntax
- CRUD operations
- Joins
- Group By & HAVING
- Subqueries
- Views
- Indexes
- Transactions
- Normalization
- Stored Procedures
- Triggers

---

# Frequently Asked SQL Interview Questions

## 1. What is SQL?

**Answer:**

SQL (Structured Query Language) is used to create, manage, retrieve, and manipulate data stored in relational databases.

---

## 2. What is the difference between SQL and MySQL?

| SQL | MySQL |
|------|--------|
| A query language | A Relational Database Management System (RDBMS) |
| Standard language | Software that implements SQL |
| Used to interact with databases | Used to store and manage databases |

---

## 3. What is a Primary Key?

**Answer:**

A Primary Key uniquely identifies each record in a table.

Properties:

- Unique
- Cannot be NULL
- One Primary Key per table

---

## 4. What is a Foreign Key?

**Answer:**

A Foreign Key links one table to another and maintains referential integrity.

---

## 5. What is the difference between DELETE, TRUNCATE and DROP?

| DELETE | TRUNCATE | DROP |
|----------|-----------|------|
| Removes selected rows | Removes all rows | Deletes the entire table |
| Can use WHERE | Cannot use WHERE | Removes table structure |
| Can rollback (in transactions) | Usually faster | Table no longer exists |

---

## 6. What is the difference between WHERE and HAVING?

| WHERE | HAVING |
|---------|---------|
| Filters rows | Filters groups |
| Used before GROUP BY | Used after GROUP BY |
| Cannot use aggregate functions | Can use aggregate functions |

---

## 7. What is the difference between CHAR and VARCHAR?

| CHAR | VARCHAR |
|-------|----------|
| Fixed length | Variable length |
| Faster for fixed-size data | Saves storage space |

---

## 8. What are Joins?

Joins combine data from multiple tables.

Types:

- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- FULL JOIN

---

## 9. What is Normalization?

Normalization is the process of reducing duplicate data and improving database consistency.

Common normal forms:

- 1NF
- 2NF
- 3NF
- BCNF

---

## 10. What is an Index?

An Index is a data structure that improves query performance by allowing faster data retrieval.

---

## 11. What is a View?

A View is a virtual table created from a SQL query.

It does not store data permanently.

---

## 12. What is a Transaction?

A Transaction is a group of SQL statements executed as a single unit of work.

Key commands:

- COMMIT
- ROLLBACK
- SAVEPOINT

---

## 13. What are ACID Properties?

- **Atomicity** – All or nothing.
- **Consistency** – Maintains valid data.
- **Isolation** – Transactions do not interfere.
- **Durability** – Committed data remains permanent.

---

## 14. What is the difference between a Stored Procedure and a Function?

| Stored Procedure | Function |
|------------------|----------|
| Executed using `CALL` | Used inside SQL statements |
| May return multiple results | Returns one value |
| Can modify data | Usually performs calculations |

---

## 15. What is a Trigger?

A Trigger automatically executes when an `INSERT`, `UPDATE`, or `DELETE` operation occurs on a table.

---

# Query-Based Interview Questions

## Question 1

Display all employees earning more than 60,000.

```sql
SELECT *

FROM employees

WHERE salary > 60000;
```

---

## Question 2

Display employees in descending order of salary.

```sql
SELECT

employee_name,

salary

FROM employees

ORDER BY salary DESC;
```

---

## Question 3

Display the total salary of each department.

```sql
SELECT

department,

SUM(salary) AS total_salary

FROM employees

GROUP BY department;
```

---

## Question 4

Find employees whose salary is greater than the average salary.

```sql
SELECT *

FROM employees

WHERE salary >

(

SELECT AVG(salary)

FROM employees

);
```

---

## Question 5

Display employee names with department names.

```sql
SELECT

e.employee_name,

d.department_name

FROM employees e

INNER JOIN departments d

ON e.department_id = d.department_id;
```

---

## Question 6

Find the second highest salary.

```sql
SELECT DISTINCT salary

FROM employees

ORDER BY salary DESC

LIMIT 1 OFFSET 1;
```

---

## Question 7

Count the number of employees in each department.

```sql
SELECT

department,

COUNT(*) AS total_employees

FROM employees

GROUP BY department;
```

---

## Question 8

Display departments having more than five employees.

```sql
SELECT

department,

COUNT(*) AS total

FROM employees

GROUP BY department

HAVING COUNT(*) > 5;
```

---

## Question 9

Update Rahul's salary to 70,000.

```sql
UPDATE employees

SET salary = 70000

WHERE employee_name = 'Rahul';
```

---

## Question 10

Delete employees who have resigned.

```sql
DELETE

FROM employees

WHERE status = 'Resigned';
```

---

# Practical Coding Challenge

Given the following tables:

### employees

| employee_id | employee_name | department_id | salary |
|-------------|---------------|---------------|---------|
| 101 | Rahul | 1 | 65000 |
| 102 | Priya | 2 | 50000 |
| 103 | Amit | 1 | 72000 |

---

### departments

| department_id | department_name |
|---------------|-----------------|
| 1 | IT |
| 2 | HR |

Write SQL queries to:

1. Display all employees.
2. Find employees with salary greater than 60,000.
3. Count employees in each department.
4. Display employee names with department names.
5. Find the highest-paid employee.
6. Find the average salary by department.
7. Update an employee's salary.
8. Delete an employee.
9. Create an index on `employee_name`.
10. Create a View for high-salary employees.

---

# Common Interview Mistakes

- Forgetting the `WHERE` clause in `UPDATE` or `DELETE`.
- Confusing `WHERE` and `HAVING`.
- Using `SELECT *` unnecessarily.
- Not understanding JOIN types.
- Ignoring indexes and transactions.
- Forgetting NULL handling.

---

# Quick Revision Sheet

| Topic | Key Point |
|--------|-----------|
| Primary Key | Unique identifier |
| Foreign Key | Creates relationships |
| JOIN | Combines tables |
| GROUP BY | Groups records |
| HAVING | Filters grouped data |
| View | Virtual table |
| Index | Improves performance |
| Transaction | Ensures data consistency |
| Trigger | Executes automatically |
| Procedure | Executed with `CALL` |
| Function | Returns one value |
| Normalization | Reduces redundancy |

---

# Practice Questions

### Multiple Choice Questions

**1. Which JOIN returns only matching records?**

A. LEFT JOIN

B. RIGHT JOIN

C. INNER JOIN

D. FULL JOIN

> **Answer:** C

---

**2. Which command permanently saves a transaction?**

A. SAVE

B. COMMIT

C. ROLLBACK

D. FINISH

> **Answer:** B

---

**3. Which clause filters grouped records?**

A. WHERE

B. ORDER BY

C. HAVING

D. LIMIT

> **Answer:** C

---

**4. Which SQL object improves search performance?**

A. Trigger

B. View

C. Index

D. Procedure

> **Answer:** C

---

# Hands-on Exercise

Using the `employees` table:

1. Display the top 3 highest-paid employees.
2. Find the average salary.
3. Count employees by department.
4. Create a view for employees earning more than 60,000.
5. Create an index on `department`.
6. Write a transaction to transfer a bonus to two employees.

---

# Mini Mock Interview

**Q1:** Explain the difference between `WHERE` and `HAVING`.

**Q2:** What is the purpose of an Index?

**Q3:** Explain ACID properties.

**Q4:** What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?

**Q5:** How do you find the second highest salary?

Try answering these without looking at the notes.

---

## Interview Tips

- Be ready to explain concepts with examples, not just definitions.
- Practice writing SQL queries without using autocomplete.
- Interviewers often ask about **Joins**, **Indexes**, **Normalization**, **Transactions**, and **Subqueries**.
- Explain your thought process while solving query-based questions—it matters as much as the final answer.

---

## Next Chapter

**Chapter 20: Mini Project – Employee Management System**
