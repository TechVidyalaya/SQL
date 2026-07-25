# Chapter 5: CRUD Operations

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand CRUD operations.
- Insert data into a table.
- Retrieve data using `SELECT`.
- Update existing records.
- Delete records.
- Use the `WHERE` clause effectively.
- Perform basic CRUD operations on a database table.

---

# What is CRUD?

CRUD represents the four basic operations performed on data in a database.

| Operation | SQL Command | Purpose |
|-----------|-------------|---------|
| Create | INSERT | Add new records |
| Read | SELECT | Retrieve records |
| Update | UPDATE | Modify existing records |
| Delete | DELETE | Remove records |

Almost every application performs these four operations.

---

# Sample Table

We'll use the following table throughout this chapter.

```sql
CREATE TABLE employees (

    employee_id INT AUTO_INCREMENT PRIMARY KEY,

    employee_name VARCHAR(100) NOT NULL,

    department VARCHAR(50),

    salary DECIMAL(10,2),

    city VARCHAR(50)

);
```

---

# CREATE (INSERT)

The `INSERT INTO` statement adds new records.

## Syntax

```sql
INSERT INTO table_name
(column1, column2, ...)
VALUES
(value1, value2, ...);
```

## Example

```sql
INSERT INTO employees
(employee_name, department, salary, city)
VALUES
('Rahul', 'IT', 55000, 'Bhubaneswar');
```

---

# Inserting Multiple Records

```sql
INSERT INTO employees
(employee_name, department, salary, city)
VALUES
('Priya', 'HR', 48000, 'Cuttack'),
('Amit', 'Finance', 62000, 'Delhi'),
('Sneha', 'IT', 70000, 'Bangalore');
```

---

# READ (SELECT)

The `SELECT` statement retrieves data.

## Retrieve All Records

```sql
SELECT * FROM employees;
```

### Sample Output

| employee_id | employee_name | department | salary | city |
|-------------|---------------|------------|---------|------|
| 1 | Rahul | IT | 55000.00 | Bhubaneswar |
| 2 | Priya | HR | 48000.00 | Cuttack |
| 3 | Amit | Finance | 62000.00 | Delhi |

---

# Retrieve Specific Columns

```sql
SELECT employee_name, salary
FROM employees;
```

### Output

| employee_name | salary |
|---------------|---------|
| Rahul | 55000 |
| Priya | 48000 |
| Amit | 62000 |

---

# WHERE Clause

The `WHERE` clause filters records.

## Example

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

### Output

Only employees in the IT department.

---

# Using Comparison Operators

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

---

```sql
SELECT *
FROM employees
WHERE salary <= 60000;
```

---

# UPDATE

The `UPDATE` statement modifies existing records.

## Syntax

```sql
UPDATE table_name
SET column = value
WHERE condition;
```

## Example

Increase Rahul's salary.

```sql
UPDATE employees
SET salary = 60000
WHERE employee_name = 'Rahul';
```

---

# Updating Multiple Columns

```sql
UPDATE employees
SET
department = 'Engineering',
city = 'Hyderabad'
WHERE employee_id = 1;
```

---

# DELETE

The `DELETE` statement removes records.

## Syntax

```sql
DELETE FROM table_name
WHERE condition;
```

## Example

```sql
DELETE FROM employees
WHERE employee_id = 3;
```

Only the employee with ID 3 is deleted.

---

# DELETE Without WHERE

```sql
DELETE FROM employees;
```

⚠️ This removes **all records** from the table.

The table structure remains.

---

# Difference Between DELETE and DROP

| DELETE | DROP |
|---------|------|
| Removes records | Removes the entire table |
| Table remains | Table is deleted |
| Can use WHERE | Cannot use WHERE |

---

# TRUNCATE TABLE

Removes all records quickly.

```sql
TRUNCATE TABLE employees;
```

Difference:

- Deletes all rows.
- Table structure remains.
- Resets AUTO_INCREMENT (in most cases).

---

# CRUD Workflow

```
Create  → INSERT

Read    → SELECT

Update  → UPDATE

Delete  → DELETE
```

---

# Best Practices

- Always use a `WHERE` clause with `UPDATE`.
- Always use a `WHERE` clause with `DELETE`.
- Verify data using `SELECT` before updating or deleting.
- Use meaningful column names.
- Test queries on sample data before running them on production databases.

---

# Summary

In this chapter, you learned:

- CRUD operations
- INSERT
- SELECT
- UPDATE
- DELETE
- WHERE clause
- DELETE vs DROP vs TRUNCATE

---

# Key Terms

- CRUD
- INSERT
- SELECT
- UPDATE
- DELETE
- WHERE
- TRUNCATE

---

# Practice Questions

### Multiple Choice Questions

**1. Which SQL statement inserts new data?**

A. CREATE

B. INSERT

C. UPDATE

D. ADD

> **Answer:** B

---

**2. Which statement retrieves records?**

A. GET

B. READ

C. SELECT

D. FETCH

> **Answer:** C

---

**3. Which statement modifies existing records?**

A. ALTER

B. UPDATE

C. CHANGE

D. MODIFY

> **Answer:** B

---

**4. Which statement removes rows but keeps the table?**

A. DELETE

B. DROP

C. REMOVE

D. DESTROY

> **Answer:** A

---

# Hands-on Exercise

## Step 1: Insert Records

```sql
INSERT INTO employees
(employee_name, department, salary, city)
VALUES
('Rahul', 'IT', 55000, 'Bhubaneswar'),
('Priya', 'HR', 48000, 'Cuttack'),
('Amit', 'Finance', 62000, 'Delhi');
```

---

## Step 2: Display All Employees

```sql
SELECT * FROM employees;
```

---

## Step 3: Find Employees in IT

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

---

## Step 4: Increase Rahul's Salary

```sql
UPDATE employees
SET salary = 60000
WHERE employee_name = 'Rahul';
```

---

## Step 5: Delete an Employee

```sql
DELETE FROM employees
WHERE employee_name = 'Amit';
```

---

## Step 6: Verify Changes

```sql
SELECT * FROM employees;
```

---

# Mini Challenge

Create a `students` table and perform the following:

1. Insert five student records.
2. Display all students.
3. Display students from the "CSE" branch.
4. Update one student's city.
5. Delete one student.
6. Display the final table.

---

## Interview Tips

- `SELECT *` retrieves all columns.
- `WHERE` filters records.
- Forgetting the `WHERE` clause in `UPDATE` or `DELETE` affects **every row** in the table.
- `TRUNCATE` removes all rows faster than `DELETE`.
- `DROP` removes the table itself.

---

## Next Chapter

**Chapter 6: Operators and Functions**
