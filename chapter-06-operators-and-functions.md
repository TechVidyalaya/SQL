# Chapter 6: Operators and Functions

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand SQL operators.
- Use arithmetic, comparison, logical, and special operators.
- Work with string, numeric, and date functions.
- Use aggregate functions.
- Write practical SQL queries using operators and functions.

---

# What are SQL Operators?

Operators are symbols or keywords used to perform operations on data.

They help us:

- Compare values
- Perform calculations
- Filter records
- Combine conditions

---

# Types of SQL Operators

- Arithmetic Operators
- Comparison Operators
- Logical Operators
- Special Operators

---

# Sample Table

```sql
CREATE TABLE employees (

    employee_id INT PRIMARY KEY,

    employee_name VARCHAR(100),

    department VARCHAR(50),

    salary DECIMAL(10,2),

    age INT,

    city VARCHAR(50)

);
```

---

# Arithmetic Operators

| Operator | Description | Example |
|----------|-------------|---------|
| + | Addition | salary + 1000 |
| - | Subtraction | salary - 500 |
| * | Multiplication | salary * 12 |
| / | Division | salary / 2 |
| % | Modulus | age % 2 |

### Example

```sql
SELECT employee_name,
       salary,
       salary + 5000 AS new_salary
FROM employees;
```

---

# Comparison Operators

| Operator | Description |
|----------|-------------|
| = | Equal |
| != or <> | Not Equal |
| > | Greater Than |
| < | Less Than |
| >= | Greater Than or Equal |
| <= | Less Than or Equal |

### Example

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

---

```sql
SELECT *
FROM employees
WHERE age <= 30;
```

---

# Logical Operators

Logical operators combine multiple conditions.

| Operator | Description |
|----------|-------------|
| AND | Both conditions must be true |
| OR | At least one condition must be true |
| NOT | Reverses a condition |

### AND Example

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 50000;
```

---

### OR Example

```sql
SELECT *
FROM employees
WHERE city = 'Delhi'
OR city = 'Bhubaneswar';
```

---

### NOT Example

```sql
SELECT *
FROM employees
WHERE NOT department = 'HR';
```

---

# BETWEEN Operator

Selects values within a range.

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 40000 AND 70000;
```

---

# IN Operator

Checks multiple values.

```sql
SELECT *
FROM employees
WHERE city IN ('Delhi', 'Bhubaneswar', 'Cuttack');
```

---

# LIKE Operator

Used for pattern matching.

| Symbol | Meaning |
|---------|---------|
| % | Zero or more characters |
| _ | Exactly one character |

---

### Starts With

```sql
SELECT *
FROM employees
WHERE employee_name LIKE 'R%';
```

---

### Ends With

```sql
SELECT *
FROM employees
WHERE employee_name LIKE '%a';
```

---

### Contains

```sql
SELECT *
FROM employees
WHERE employee_name LIKE '%it%';
```

---

# IS NULL

Finds NULL values.

```sql
SELECT *
FROM employees
WHERE city IS NULL;
```

---

# IS NOT NULL

```sql
SELECT *
FROM employees
WHERE city IS NOT NULL;
```

---

# String Functions

## UPPER()

Converts text to uppercase.

```sql
SELECT UPPER(employee_name)
FROM employees;
```

---

## LOWER()

```sql
SELECT LOWER(employee_name)
FROM employees;
```

---

## LENGTH()

Returns the number of characters.

```sql
SELECT employee_name,
       LENGTH(employee_name)
FROM employees;
```

---

## CONCAT()

Joins strings.

```sql
SELECT CONCAT(employee_name, ' - ', department)
FROM employees;
```

---

# Numeric Functions

## ROUND()

```sql
SELECT ROUND(4567.896, 2);
```

Output

```
4567.90
```

---

## CEIL()

Rounds up.

```sql
SELECT CEIL(45.2);
```

Output

```
46
```

---

## FLOOR()

Rounds down.

```sql
SELECT FLOOR(45.9);
```

Output

```
45
```

---

## ABS()

Returns the absolute value.

```sql
SELECT ABS(-100);
```

Output

```
100
```

---

# Date Functions

## CURDATE()

Returns today's date.

```sql
SELECT CURDATE();
```

---

## NOW()

Returns the current date and time.

```sql
SELECT NOW();
```

---

## YEAR()

```sql
SELECT YEAR(CURDATE());
```

---

## MONTH()

```sql
SELECT MONTH(CURDATE());
```

---

## DAY()

```sql
SELECT DAY(CURDATE());
```

---

# Aggregate Functions

Aggregate functions perform calculations on multiple rows.

| Function | Description |
|----------|-------------|
| COUNT() | Counts rows |
| SUM() | Total value |
| AVG() | Average value |
| MIN() | Smallest value |
| MAX() | Largest value |

---

## COUNT()

```sql
SELECT COUNT(*)
FROM employees;
```

---

## SUM()

```sql
SELECT SUM(salary)
FROM employees;
```

---

## AVG()

```sql
SELECT AVG(salary)
FROM employees;
```

---

## MIN()

```sql
SELECT MIN(salary)
FROM employees;
```

---

## MAX()

```sql
SELECT MAX(salary)
FROM employees;
```

---

# Practical Example

```sql
SELECT employee_name,
       salary,
       ROUND(salary * 1.10, 2) AS revised_salary
FROM employees
WHERE department = 'IT'
AND salary > 50000;
```

---

# Best Practices

- Use aliases (`AS`) for readable output.
- Prefer aggregate functions instead of manual calculations.
- Use `LIKE` carefully on large tables.
- Handle NULL values explicitly using `IS NULL` or `IS NOT NULL`.
- Keep conditions simple and readable.

---

# Summary

In this chapter, you learned:

- Arithmetic operators
- Comparison operators
- Logical operators
- BETWEEN, IN, and LIKE
- NULL checks
- String functions
- Numeric functions
- Date functions
- Aggregate functions

---

# Key Terms

- AND
- OR
- LIKE
- BETWEEN
- IN
- COUNT()
- SUM()
- AVG()
- MIN()
- MAX()
- UPPER()
- LOWER()
- CONCAT()

---

# Practice Questions

### Multiple Choice Questions

**1. Which operator is used for pattern matching?**

A. IN

B. LIKE

C. BETWEEN

D. AND

> **Answer:** B

---

**2. Which function returns the average value?**

A. SUM()

B. COUNT()

C. AVG()

D. TOTAL()

> **Answer:** C

---

**3. Which function converts text to uppercase?**

A. CAPITAL()

B. UPPER()

C. TOUPPER()

D. UCASE()

> **Answer:** B

---

**4. Which operator checks whether a value lies within a range?**

A. IN

B. BETWEEN

C. LIKE

D. OR

> **Answer:** B

---

# Hands-on Exercise

Assume the `employees` table contains employee data.

### 1. Display employees earning more than 60,000.

```sql
SELECT *
FROM employees
WHERE salary > 60000;
```

---

### 2. Display employees from IT or HR.

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR');
```

---

### 3. Display names in uppercase.

```sql
SELECT UPPER(employee_name)
FROM employees;
```

---

### 4. Display the total salary paid.

```sql
SELECT SUM(salary)
FROM employees;
```

---

### 5. Display the average salary.

```sql
SELECT AVG(salary)
FROM employees;
```

---

### 6. Display employees whose names start with 'A'.

```sql
SELECT *
FROM employees
WHERE employee_name LIKE 'A%';
```

---

# Mini Challenge

Using the `employees` table, write SQL queries to:

1. Find the highest salary.
2. Find the lowest salary.
3. Count employees in the IT department.
4. Display employees aged between 25 and 35.
5. Display employees whose city is not NULL.
6. Show each employee's salary after a 15% increment.

---

## Interview Tips

- `LIKE '%text%'` searches anywhere in a string.
- `COUNT(*)` counts all rows, including those with NULL values in other columns.
- Aggregate functions return a single result unless combined with `GROUP BY`.
- Use `BETWEEN` for inclusive ranges.
- `IS NULL` should be used instead of `= NULL`.

---

## Next Chapter

**Chapter 7: Sorting and Filtering Data**
