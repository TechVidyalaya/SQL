# Chapter 20: Mini Project – Employee Management System

## Learning Objectives

By the end of this chapter, you will be able to:

- Apply all SQL concepts learned in this course.
- Design a relational database.
- Create tables with relationships.
- Perform CRUD operations.
- Write joins, subqueries, views, indexes, and transactions.
- Build a complete SQL project.

---

# Project Overview

In this project, you will build a simple **Employee Management System**.

The system will manage:

- Employees
- Departments
- Salaries
- Projects

---

# Database Design

## Tables

- departments
- employees
- projects
- employee_projects

---

# Entity Relationship Diagram (ERD)

```
Departments
--------------
department_id (PK)
department_name

        │
        │
        ▼

Employees
--------------
employee_id (PK)
employee_name
salary
department_id (FK)

        │
        │
        ▼

Employee_Projects
--------------------
employee_id (FK)
project_id (FK)

        ▲
        │
        │

Projects
--------------
project_id (PK)
project_name
```

---

# Step 1: Create Database

```sql
CREATE DATABASE employee_management;

USE employee_management;
```

---

# Step 2: Create Departments Table

```sql
CREATE TABLE departments (

    department_id INT PRIMARY KEY,

    department_name VARCHAR(100)

);
```

---

# Step 3: Create Employees Table

```sql
CREATE TABLE employees (

    employee_id INT PRIMARY KEY,

    employee_name VARCHAR(100),

    salary DECIMAL(10,2),

    department_id INT,

    FOREIGN KEY (department_id)

    REFERENCES departments(department_id)

);
```

---

# Step 4: Create Projects Table

```sql
CREATE TABLE projects (

    project_id INT PRIMARY KEY,

    project_name VARCHAR(100)

);
```

---

# Step 5: Create Employee Projects Table

```sql
CREATE TABLE employee_projects (

    employee_id INT,

    project_id INT,

    PRIMARY KEY(employee_id, project_id),

    FOREIGN KEY(employee_id)

    REFERENCES employees(employee_id),

    FOREIGN KEY(project_id)

    REFERENCES projects(project_id)

);
```

---

# Step 6: Insert Sample Data

### Departments

```sql
INSERT INTO departments
VALUES

(1,'IT'),

(2,'HR'),

(3,'Finance');
```

---

### Employees

```sql
INSERT INTO employees
VALUES

(101,'Rahul',65000,1),

(102,'Priya',50000,2),

(103,'Amit',72000,1),

(104,'Sneha',58000,3);
```

---

### Projects

```sql
INSERT INTO projects
VALUES

(1,'Payroll'),

(2,'Inventory'),

(3,'CRM');
```

---

### Employee Projects

```sql
INSERT INTO employee_projects
VALUES

(101,1),

(101,2),

(102,3),

(103,1),

(104,2);
```

---

# Step 7: Retrieve Data

Display all employees.

```sql
SELECT *
FROM employees;
```

---

Display employees with department names.

```sql
SELECT

e.employee_name,

d.department_name,

e.salary

FROM employees e

INNER JOIN departments d

ON e.department_id = d.department_id;
```

---

Display employees with project names.

```sql
SELECT

e.employee_name,

p.project_name

FROM employees e

JOIN employee_projects ep

ON e.employee_id = ep.employee_id

JOIN projects p

ON ep.project_id = p.project_id;
```

---

# Step 8: Update Data

Increase IT employee salaries by 10%.

```sql
UPDATE employees

SET salary = salary * 1.10

WHERE department_id = 1;
```

---

# Step 9: Delete Data

Delete an employee.

```sql
DELETE

FROM employees

WHERE employee_id = 104;
```

---

# Step 10: Aggregate Queries

Average salary by department.

```sql
SELECT

department_id,

AVG(salary) AS average_salary

FROM employees

GROUP BY department_id;
```

---

Highest salary.

```sql
SELECT

MAX(salary)

FROM employees;
```

---

# Step 11: Subquery

Employees earning more than average salary.

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

# Step 12: Create a View

```sql
CREATE VIEW high_salary_employees AS

SELECT

employee_name,

salary

FROM employees

WHERE salary > 60000;
```

---

# Step 13: Create an Index

```sql
CREATE INDEX idx_employee_name

ON employees(employee_name);
```

---

# Step 14: Transaction Example

Transfer a £500 bonus from one department budget to another.

```sql
START TRANSACTION;

UPDATE employees

SET salary = salary + 500

WHERE employee_id = 101;

UPDATE employees

SET salary = salary + 500

WHERE employee_id = 102;

COMMIT;
```

---

# Step 15: Create a Stored Procedure

```sql
DELIMITER //

CREATE PROCEDURE GetEmployees()

BEGIN

    SELECT *

    FROM employees;

END //

DELIMITER ;
```

Execute it.

```sql
CALL GetEmployees();
```

---

# Step 16: Create a Function

```sql
DELIMITER //

CREATE FUNCTION AnnualSalary(

monthly_salary DECIMAL(10,2)

)

RETURNS DECIMAL(10,2)

DETERMINISTIC

BEGIN

    RETURN monthly_salary * 12;

END //

DELIMITER ;
```

Use it.

```sql
SELECT

employee_name,

AnnualSalary(salary)

FROM employees;
```

---

# Step 17: Create a Trigger

```sql
DELIMITER //

CREATE TRIGGER employee_insert_log

AFTER INSERT

ON employees

FOR EACH ROW

BEGIN

    INSERT INTO employee_logs(message)

    VALUES(

        CONCAT(

        'Employee Added: ',

        NEW.employee_name

        )

    );

END //

DELIMITER ;
```

---

# Features Implemented

- Database creation
- Table creation
- Relationships
- CRUD operations
- Joins
- Aggregate functions
- Subqueries
- Views
- Indexes
- Transactions
- Stored Procedures
- Functions
- Triggers

---

# Project Enhancement Ideas

Try adding:

- Employee login
- Attendance table
- Leave management
- Payroll module
- Performance reviews
- Role-based access
- Audit logs
- Employee address and contact details

---

# Best Practices

- Use Primary and Foreign Keys.
- Follow normalization principles.
- Create indexes on frequently searched columns.
- Use transactions for critical operations.
- Keep SQL queries readable.
- Backup your database regularly.

---

# Final Project Challenge

Build an Employee Management System that supports:

- Employee registration
- Department management
- Project allocation
- Salary updates
- Employee search
- Reports
- Department-wise statistics
- Employee-project mapping
- High salary reports
- Audit logging using triggers

---

# Summary

Congratulations!

You have completed the SQL course and learned:

- SQL Basics
- Database Design
- CRUD Operations
- Constraints
- Functions
- Joins
- Group By
- Subqueries
- Views
- Indexes
- Transactions
- Normalization
- Stored Procedures
- Triggers
- SQL Best Practices
- Interview Questions
- Real-world Project

You are now ready to start building database-driven applications using SQL.

---

# Capstone Assignment

Design a **Library Management System** database.

Your solution should include:

1. At least 5 related tables.
2. Primary and Foreign Keys.
3. Sample data.
4. CRUD operations.
5. Joins.
6. Aggregate queries.
7. A View.
8. An Index.
9. A Stored Procedure.
10. A Trigger.
11. A Transaction.
12. At least 10 SQL queries demonstrating the system.

---

# Course Completion Checklist

| Topic | Status |
|--------|--------|
| SQL Basics | ✅ |
| CRUD Operations | ✅ |
| Constraints | ✅ |
| Joins | ✅ |
| Group By & HAVING | ✅ |
| Subqueries | ✅ |
| Views | ✅ |
| Indexes | ✅ |
| Transactions | ✅ |
| Normalization | ✅ |
| Stored Procedures | ✅ |
| Triggers | ✅ |
| SQL Best Practices | ✅ |
| Interview Questions | ✅ |
| Mini Project | ✅ |

---

## Congratulations! 🎉

You have successfully completed the **SQL Mastery** course.

Keep practising by solving real-world database problems, and you'll be well prepared for both software development and technical interviews.
