# Chapter 4: Data Types and Constraints

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand SQL data types.
- Choose the appropriate data type for a column.
- Learn about NULL and NOT NULL.
- Understand PRIMARY KEY and FOREIGN KEY.
- Use UNIQUE, DEFAULT, and CHECK constraints.
- Apply constraints while creating tables.

---

# What are Data Types?

A **data type** specifies the kind of data that can be stored in a column.

Choosing the correct data type helps:

- Save storage space
- Improve performance
- Maintain data accuracy
- Prevent invalid data

---

# Categories of Data Types

MySQL data types can be grouped into:

- Numeric Data Types
- String Data Types
- Date and Time Data Types
- Boolean Data Type

---

# Numeric Data Types

| Data Type | Description | Example |
|-----------|-------------|---------|
| INT | Whole numbers | 100 |
| BIGINT | Large whole numbers | 9876543210 |
| DECIMAL(p,s) | Fixed decimal values | 25000.50 |
| FLOAT | Approximate decimal values | 98.75 |
| DOUBLE | Large decimal values | 12345.6789 |

### Example

```sql
salary DECIMAL(10,2)
```

Stores values like:

```
35000.50
50000.00
78500.75
```

---

# String Data Types

| Data Type | Description |
|-----------|-------------|
| CHAR(n) | Fixed-length text |
| VARCHAR(n) | Variable-length text |
| TEXT | Large text |

### Example

```sql
name VARCHAR(100)
```

---

# CHAR vs VARCHAR

| CHAR | VARCHAR |
|------|----------|
| Fixed size | Variable size |
| Faster for fixed-length values | Saves storage |
| Stores blank spaces | Stores only entered characters |

### Example

Employee Code

```
EMP001
EMP002
```

Use:

```sql
CHAR(6)
```

Employee Name

```
Rahul Sharma
Priya Das
```

Use:

```sql
VARCHAR(100)
```

---

# Date and Time Data Types

| Data Type | Example |
|-----------|----------|
| DATE | 2026-07-25 |
| TIME | 14:30:00 |
| DATETIME | 2026-07-25 14:30:00 |
| TIMESTAMP | Automatically stores date and time |
| YEAR | 2026 |

---

# Boolean Data Type

MySQL stores Boolean values as:

```
TRUE = 1
FALSE = 0
```

Example:

```sql
is_active BOOLEAN
```

---

# What are Constraints?

Constraints are rules applied to columns to ensure data accuracy and consistency.

They prevent invalid data from being inserted into the database.

---

# Common Constraints

- NOT NULL
- UNIQUE
- PRIMARY KEY
- FOREIGN KEY
- DEFAULT
- CHECK
- AUTO_INCREMENT

---

# NOT NULL Constraint

Ensures a column cannot contain NULL values.

### Example

```sql
CREATE TABLE employees (
    id INT,
    name VARCHAR(100) NOT NULL
);
```

The `name` column must always contain a value.

---

# UNIQUE Constraint

Ensures that all values in a column are different.

### Example

```sql
CREATE TABLE users (
    email VARCHAR(100) UNIQUE
);
```

Duplicate email addresses are not allowed.

---

# PRIMARY KEY

A Primary Key uniquely identifies each row in a table.

Properties:

- Unique
- Cannot be NULL
- One Primary Key per table

### Example

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

---

# AUTO_INCREMENT

Automatically generates sequential numbers.

### Example

```sql
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
);
```

Inserted rows:

| id | name |
|----|------|
| 1 | Rahul |
| 2 | Priya |
| 3 | Amit |

---

# DEFAULT Constraint

Assigns a default value when no value is provided.

### Example

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    city VARCHAR(50) DEFAULT 'Bhubaneswar'
);
```

If the city is omitted, it becomes:

```
Bhubaneswar
```

---

# CHECK Constraint

Ensures values satisfy a condition.

### Example

```sql
CREATE TABLE students (
    age INT CHECK(age >= 18)
);
```

Only ages 18 and above are allowed.

> **Note:** CHECK constraints are enforced in MySQL 8.0.16 and later.

---

# FOREIGN KEY

A Foreign Key creates a relationship between two tables.

### Departments Table

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);
```

### Employees Table

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

Now every employee must belong to a valid department.

---

# NULL vs NOT NULL

| NULL | NOT NULL |
|------|----------|
| Value may be missing | Value is mandatory |
| Optional field | Required field |

Example:

```
Middle Name → NULL

Employee Name → NOT NULL
```

---

# Complete Example

```sql
CREATE TABLE employees (

    employee_id INT AUTO_INCREMENT PRIMARY KEY,

    employee_name VARCHAR(100) NOT NULL,

    email VARCHAR(100) UNIQUE,

    salary DECIMAL(10,2),

    city VARCHAR(50) DEFAULT 'Bhubaneswar',

    age INT CHECK(age >= 18)

);
```

---

# Best Practices

- Always use a Primary Key.
- Use `VARCHAR` instead of `CHAR` unless the length is fixed.
- Choose appropriate numeric types.
- Avoid unnecessary NULL values.
- Use constraints to maintain data integrity.
- Use meaningful column names.

---

# Summary

In this chapter, you learned:

- SQL data types
- Numeric, string, and date data types
- Constraints
- PRIMARY KEY
- FOREIGN KEY
- UNIQUE
- DEFAULT
- CHECK
- AUTO_INCREMENT

---

# Key Terms

- INT
- VARCHAR
- DATE
- DECIMAL
- PRIMARY KEY
- FOREIGN KEY
- NOT NULL
- UNIQUE
- DEFAULT
- CHECK
- AUTO_INCREMENT

---

# Practice Questions

### Multiple Choice Questions

**1. Which data type stores variable-length text?**

A. CHAR

B. VARCHAR

C. INT

D. DATE

> **Answer:** B

---

**2. Which constraint uniquely identifies a record?**

A. UNIQUE

B. PRIMARY KEY

C. DEFAULT

D. CHECK

> **Answer:** B

---

**3. Which keyword automatically generates IDs?**

A. UNIQUE

B. AUTO_INCREMENT

C. DEFAULT

D. CHECK

> **Answer:** B

---

**4. Which constraint prevents duplicate values?**

A. UNIQUE

B. DEFAULT

C. CHECK

D. NOT NULL

> **Answer:** A

---

# Hands-on Exercise

Create a table named `students` with the following requirements:

- Student ID should auto-increment.
- Name should be mandatory.
- Email should be unique.
- Age must be at least 18.
- City should default to **Bhubaneswar**.

```sql
CREATE TABLE students (

    student_id INT AUTO_INCREMENT PRIMARY KEY,

    name VARCHAR(100) NOT NULL,

    email VARCHAR(100) UNIQUE,

    age INT CHECK(age >= 18),

    city VARCHAR(50) DEFAULT 'Bhubaneswar'

);
```

---

# Mini Challenge

Create a table named `products` with:

- Product ID (Auto Increment)
- Product Name (Mandatory)
- Price (Decimal)
- Category
- Stock (Default: 0)
- SKU (Unique)

Try adding a few sample records and observe how the constraints work.

---

## Next Chapter

**Chapter 5: CRUD Operations**
