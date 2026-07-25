
# Chapter 16: Stored Procedures and Functions

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand Stored Procedures and Functions.
- Create and execute Stored Procedures.
- Create and use User-Defined Functions.
- Understand the differences between Procedures and Functions.
- Learn when to use each.

---

# What is a Stored Procedure?

A **Stored Procedure** is a collection of SQL statements stored inside the database.

Instead of writing the same SQL repeatedly, you can save it as a procedure and execute it whenever required.

Think of it as a reusable SQL program.

---

# Why Use Stored Procedures?

Stored Procedures help to:

- Reuse SQL code
- Reduce duplicate queries
- Improve performance
- Simplify complex operations
- Enhance security

---

# Creating a Stored Procedure

## Syntax

```sql
DELIMITER //

CREATE PROCEDURE procedure_name()

BEGIN

    SQL statements;

END //

DELIMITER ;
```

---

## Example

Display all employees.

```sql
DELIMITER //

CREATE PROCEDURE GetAllEmployees()

BEGIN

    SELECT *
    FROM employees;

END //

DELIMITER ;
```

---

# Executing a Stored Procedure

```sql
CALL GetAllEmployees();
```

---

# Stored Procedure with Parameters

Stored Procedures can accept parameters.

### Syntax

```sql
CREATE PROCEDURE procedure_name(IN parameter datatype)
```

---

## Example

Display employees belonging to a department.

```sql
DELIMITER //

CREATE PROCEDURE GetEmployeesByDepartment(

    IN dept VARCHAR(50)

)

BEGIN

    SELECT *
    FROM employees
    WHERE department = dept;

END //

DELIMITER ;
```

Execute it.

```sql
CALL GetEmployeesByDepartment('IT');
```

---

# Types of Parameters

| Type | Description |
|------|-------------|
| IN | Input parameter |
| OUT | Output parameter |
| INOUT | Input and Output |

---

# Example Using OUT Parameter

```sql
DELIMITER //

CREATE PROCEDURE GetEmployeeCount(

    OUT total INT

)

BEGIN

    SELECT COUNT(*)
    INTO total
    FROM employees;

END //

DELIMITER ;
```

Execute it.

```sql
CALL GetEmployeeCount(@count);

SELECT @count;
```

---

# What is a Function?

A **Function** is a reusable SQL program that always returns a single value.

Unlike a Stored Procedure, a Function can be used inside SQL statements.

---

# Creating a Function

## Syntax

```sql
DELIMITER //

CREATE FUNCTION function_name(parameter datatype)

RETURNS datatype

DETERMINISTIC

BEGIN

    SQL statements

    RETURN value;

END //

DELIMITER ;
```

---

## Example

Calculate annual salary.

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

---

# Using a Function

```sql
SELECT

employee_name,

AnnualSalary(salary)

FROM employees;
```

### Output

| Employee | Annual Salary |
|-----------|---------------|
| Rahul | 780000 |
| Priya | 600000 |

---

# Procedure vs Function

| Stored Procedure | Function |
|------------------|----------|
| May return zero, one, or many results | Returns exactly one value |
| Called using `CALL` | Used inside SQL statements |
| Can perform INSERT, UPDATE, DELETE | Primarily performs calculations |
| Supports IN, OUT, INOUT parameters | Supports only input parameters |

---

# Practical Example

Suppose an Employee Management System.

Instead of writing:

```sql
SELECT *
FROM employees
WHERE salary > 60000;
```

every time,

create a procedure.

```sql
DELIMITER //

CREATE PROCEDURE HighSalaryEmployees()

BEGIN

    SELECT *
    FROM employees
    WHERE salary > 60000;

END //

DELIMITER ;
```

Execute:

```sql
CALL HighSalaryEmployees();
```

---

# Using a Function in SELECT

```sql
SELECT

employee_name,

salary,

AnnualSalary(salary) AS annual_salary

FROM employees;
```

---

# Advantages of Stored Procedures

- Better performance
- Code reuse
- Easier maintenance
- Improved security
- Centralised business logic

---

# Advantages of Functions

- Can be used in SQL queries
- Simplifies calculations
- Improves readability
- Promotes code reuse

---

# Best Practices

- Keep procedures focused on one task.
- Use meaningful names.
- Validate input parameters.
- Use functions only for calculations or value transformations.
- Avoid writing complex business logic inside functions.

---

# Summary

In this chapter, you learned:

- Stored Procedures
- Procedure parameters
- CALL statement
- User-Defined Functions
- Function return values
- Differences between Procedures and Functions

---

# Key Terms

- Stored Procedure
- Function
- CALL
- RETURN
- IN
- OUT
- INOUT
- DELIMITER

---

# Practice Questions

### Multiple Choice Questions

**1. Which command executes a stored procedure?**

A. RUN

B. EXECUTE

C. CALL

D. START

> **Answer:** C

---

**2. A SQL Function always returns:**

A. Multiple tables

B. One value

C. Multiple rows only

D. Nothing

> **Answer:** B

---

**3. Which parameter type is used to pass values into a procedure?**

A. OUT

B. RETURN

C. IN

D. RESULT

> **Answer:** C

---

**4. Which object can be used directly inside a SELECT statement?**

A. Stored Procedure

B. Function

C. Trigger

D. Transaction

> **Answer:** B

---

# Hands-on Exercise

## Create a Procedure

```sql
DELIMITER //

CREATE PROCEDURE ShowEmployees()

BEGIN

    SELECT *
    FROM employees;

END //

DELIMITER ;
```

Execute it.

```sql
CALL ShowEmployees();
```

---

## Create a Function

```sql
DELIMITER //

CREATE FUNCTION Bonus(

salary DECIMAL(10,2)

)

RETURNS DECIMAL(10,2)

DETERMINISTIC

BEGIN

    RETURN salary * 0.10;

END //

DELIMITER ;
```

Use it.

```sql
SELECT

employee_name,

salary,

Bonus(salary) AS bonus

FROM employees;
```

---

# Mini Challenge

Using the `employees` table:

1. Create a procedure to display all employees from the HR department.
2. Create a procedure that accepts a department name as input.
3. Create a function to calculate annual salary.
4. Create a function to calculate a 15% bonus.
5. Use both functions in a `SELECT` query.

---

## Interview Tips

- A **Stored Procedure** is executed using the `CALL` statement and can perform multiple database operations.
- A **Function** must return a single value and can be used inside SQL statements such as `SELECT`, `WHERE`, or `ORDER BY`.
- Use **Stored Procedures** for business operations and **Functions** for calculations or reusable expressions.
- Remember the parameter types: **IN**, **OUT**, and **INOUT**.

---

## Next Chapter

**Chapter 17: Triggers**
