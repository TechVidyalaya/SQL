# Chapter 7: Sorting and Filtering Data

## Learning Objectives

By the end of this chapter, you will be able to:

- Sort query results using `ORDER BY`.
- Filter records using the `WHERE` clause.
- Limit the number of returned rows.
- Remove duplicate records using `DISTINCT`.
- Combine multiple filtering conditions.
- Write efficient search queries.

---

# Introduction

When working with databases, we rarely need all the data.

Instead, we usually want to:

- Find specific records
- Sort data
- Remove duplicates
- Display only the required number of rows

SQL provides powerful clauses to achieve this.

---

# Sample Table

```sql
employees
```

| employee_id | employee_name | department | salary | city |
|--------------|--------------|------------|---------|------|
| 1 | Rahul | IT | 65000 | Bhubaneswar |
| 2 | Priya | HR | 50000 | Cuttack |
| 3 | Amit | Finance | 75000 | Delhi |
| 4 | Sneha | IT | 62000 | Bangalore |
| 5 | Karan | HR | 48000 | Bhubaneswar |

---

# WHERE Clause

The `WHERE` clause filters rows based on a condition.

## Syntax

```sql
SELECT column_name
FROM table_name
WHERE condition;
```

---

## Example

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

### Output

| employee_name | department |
|---------------|------------|
| Rahul | IT |
| Sneha | IT |

---

# Multiple Conditions

## AND Operator

Returns records only if **both** conditions are true.

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 60000;
```

---

## OR Operator

Returns records if **any** condition is true.

```sql
SELECT *
FROM employees
WHERE city = 'Delhi'
OR city = 'Cuttack';
```

---

## NOT Operator

Returns records that do not satisfy a condition.

```sql
SELECT *
FROM employees
WHERE NOT department = 'HR';
```

---

# ORDER BY

Sorts the result set.

## Ascending Order (Default)

```sql
SELECT *
FROM employees
ORDER BY salary;
```

---

## Descending Order

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

---

# Sorting by Multiple Columns

```sql
SELECT *
FROM employees
ORDER BY department ASC,
salary DESC;
```

Employees are first sorted by department and then by salary.

---

# DISTINCT

Removes duplicate values.

## Example

```sql
SELECT DISTINCT department
FROM employees;
```

### Output

```
IT
HR
Finance
```

---

# LIMIT

Returns only a specified number of rows.

```sql
SELECT *
FROM employees
LIMIT 3;
```

Returns the first three records.

---

# OFFSET with LIMIT

Skip a certain number of rows.

```sql
SELECT *
FROM employees
LIMIT 2 OFFSET 3;
```

Returns two rows after skipping the first three.

---

# BETWEEN

Retrieve values within a range.

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 50000 AND 70000;
```

---

# IN Operator

Check multiple values.

```sql
SELECT *
FROM employees
WHERE city IN ('Delhi', 'Bhubaneswar');
```

---

# LIKE Operator

Used for searching patterns.

## Starts With

```sql
SELECT *
FROM employees
WHERE employee_name LIKE 'R%';
```

---

## Ends With

```sql
SELECT *
FROM employees
WHERE employee_name LIKE '%a';
```

---

## Contains

```sql
SELECT *
FROM employees
WHERE employee_name LIKE '%it%';
```

---

## Single Character

```sql
SELECT *
FROM employees
WHERE employee_name LIKE '_m%';
```

Matches names where the second character is **m**.

---

# Combining Filtering and Sorting

```sql
SELECT employee_name,
salary
FROM employees
WHERE department='IT'
ORDER BY salary DESC;
```

---

# Practical Example

Display the top two highest-paid IT employees.

```sql
SELECT employee_name,
salary
FROM employees
WHERE department='IT'
ORDER BY salary DESC
LIMIT 2;
```

---

# Best Practices

- Filter data before sorting whenever possible.
- Use `DISTINCT` only when required.
- Always specify `ORDER BY` if the order matters.
- Use `LIMIT` when displaying records in applications.
- Avoid unnecessary wildcard searches on large tables.

---

# Summary

In this chapter, you learned:

- WHERE
- ORDER BY
- DISTINCT
- LIMIT
- OFFSET
- BETWEEN
- IN
- LIKE
- Combining filtering and sorting

---

# Key Terms

- WHERE
- ORDER BY
- ASC
- DESC
- DISTINCT
- LIMIT
- OFFSET
- LIKE
- BETWEEN
- IN

---

# Practice Questions

### Multiple Choice Questions

**1. Which clause is used to sort records?**

A. SORT

B. ORDER

C. ORDER BY

D. GROUP BY

> **Answer:** C

---

**2. Which keyword removes duplicate values?**

A. UNIQUE

B. DISTINCT

C. REMOVE

D. DELETE

> **Answer:** B

---

**3. Which clause limits the number of returned rows?**

A. TOP

B. LIMIT

C. FIRST

D. FETCH

> **Answer:** B

---

**4. Which operator searches using patterns?**

A. BETWEEN

B. IN

C. LIKE

D. EXISTS

> **Answer:** C

---

# Hands-on Exercise

## 1. Display all employees.

```sql
SELECT *
FROM employees;
```

---

## 2. Display only IT employees.

```sql
SELECT *
FROM employees
WHERE department='IT';
```

---

## 3. Display employees earning more than 60,000.

```sql
SELECT *
FROM employees
WHERE salary > 60000;
```

---

## 4. Display employees sorted by salary.

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

---

## 5. Display unique departments.

```sql
SELECT DISTINCT department
FROM employees;
```

---

## 6. Display the first three employees.

```sql
SELECT *
FROM employees
LIMIT 3;
```

---

## 7. Display employees from Bhubaneswar or Delhi.

```sql
SELECT *
FROM employees
WHERE city IN ('Bhubaneswar', 'Delhi');
```

---

# Mini Challenge

Using the `employees` table, write SQL queries to:

1. Display employees from the HR department.
2. Display employees whose salary is between 45,000 and 70,000.
3. Display employee names starting with **S**.
4. Display the five highest-paid employees.
5. Display unique cities.
6. Sort employees by department and then by employee name.

---

## Interview Tips

- `WHERE` filters rows **before** sorting.
- `ORDER BY` sorts rows after filtering.
- `DISTINCT` removes duplicate values from the result set.
- `LIMIT` is commonly used for pagination.
- `%` matches zero or more characters, while `_` matches exactly one character.

---

## Next Chapter

**Chapter 8: GROUP BY and HAVING**
