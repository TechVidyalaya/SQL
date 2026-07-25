# Chapter 3: Database and Table Operations

## Learning Objectives

By the end of this chapter, you will be able to:

- Create a database.
- View existing databases.
- Select a database.
- Delete a database.
- Create tables.
- View table structures.
- Modify tables.
- Delete tables.

---

# What is a Database?

A **database** is a collection of related tables.

For example, an Employee Management System may contain:

- Employees
- Departments
- Projects
- Salaries

Each of these is stored in a separate table.

---

# Creating a Database

Use the `CREATE DATABASE` statement.

### Syntax

```sql
CREATE DATABASE database_name;
```

### Example

```sql
CREATE DATABASE company_db;
```

---

# Viewing All Databases

```sql
SHOW DATABASES;
```

### Sample Output

| Database |
|----------|
| company_db |
| mysql |
| sys |
| information_schema |

---

# Selecting a Database

Before creating tables, select the database.

### Syntax

```sql
USE database_name;
```

### Example

```sql
USE company_db;
```

Now all operations will be performed inside `company_db`.

---

# Deleting a Database

### Syntax

```sql
DROP DATABASE database_name;
```

### Example

```sql
DROP DATABASE company_db;
```

> **Warning:** This permanently deletes the database and all its tables.

---

# Creating a Table

A table stores related data in rows and columns.

### Syntax

```sql
CREATE TABLE table_name (
    column_name datatype,
    column_name datatype
);
```

### Example

```sql
CREATE TABLE employees (
    id INT,
    name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

---

# Viewing All Tables

```sql
SHOW TABLES;
```

### Sample Output

| Tables_in_company_db |
|----------------------|
| employees |

---

# Viewing Table Structure

Use the `DESCRIBE` command.

### Syntax

```sql
DESCRIBE table_name;
```

### Example

```sql
DESCRIBE employees;
```

### Output

| Field | Type | Null | Key |
|------|------|------|-----|
| id | int | YES | |
| name | varchar(100) | YES | |
| salary | decimal(10,2) | YES | |

---

# Renaming a Table

```sql
RENAME TABLE employees TO employee_details;
```

---

# Adding a New Column

Use the `ALTER TABLE` statement.

### Example

```sql
ALTER TABLE employees
ADD email VARCHAR(100);
```

---

# Modifying a Column

```sql
ALTER TABLE employees
MODIFY salary DECIMAL(12,2);
```

---

# Renaming a Column

```sql
ALTER TABLE employees
RENAME COLUMN name TO employee_name;
```

---

# Dropping a Column

```sql
ALTER TABLE employees
DROP COLUMN email;
```

---

# Deleting a Table

### Syntax

```sql
DROP TABLE table_name;
```

### Example

```sql
DROP TABLE employees;
```

> **Warning:** All data inside the table will be permanently deleted.

---

# Database vs Table

| Database | Table |
|----------|-------|
| Collection of tables | Collection of rows and columns |
| Stores multiple tables | Stores actual data |
| Created using `CREATE DATABASE` | Created using `CREATE TABLE` |

---

# Common SQL Commands

| Command | Purpose |
|----------|---------|
| CREATE DATABASE | Create a database |
| SHOW DATABASES | Display all databases |
| USE | Select a database |
| DROP DATABASE | Delete a database |
| CREATE TABLE | Create a table |
| SHOW TABLES | Display all tables |
| DESCRIBE | View table structure |
| ALTER TABLE | Modify a table |
| DROP TABLE | Delete a table |

---

# Best Practices

- Use meaningful database names.
- Use singular or plural table names consistently.
- Avoid spaces in names.
- Prefer lowercase names.
- Always back up important data before using `DROP`.

---

# Summary

In this chapter, you learned:

- How to create and delete databases.
- How to select a database.
- How to create tables.
- How to view table structures.
- How to modify tables using `ALTER TABLE`.
- How to delete tables.

---

# Key Terms

- Database
- Table
- Row
- Column
- CREATE DATABASE
- CREATE TABLE
- ALTER TABLE
- DROP TABLE
- DESCRIBE

---

# Practice Questions

### Multiple Choice Questions

**1. Which command creates a new database?**

A.

```sql
NEW DATABASE company_db;
```

B.

```sql
CREATE DATABASE company_db;
```

C.

```sql
MAKE DATABASE company_db;
```

D.

```sql
ADD DATABASE company_db;
```

> **Answer:** B

---

**2. Which command displays all tables in the selected database?**

A.

```sql
SHOW TABLES;
```

B.

```sql
LIST TABLES;
```

C.

```sql
DISPLAY TABLES;
```

D.

```sql
GET TABLES;
```

> **Answer:** A

---

**3. Which statement is used to modify a table?**

A. UPDATE TABLE

B. MODIFY TABLE

C. ALTER TABLE

D. CHANGE TABLE

> **Answer:** C

---

# Hands-on Exercise

## Step 1: Create a Database

```sql
CREATE DATABASE company_db;
```

## Step 2: Select the Database

```sql
USE company_db;
```

## Step 3: Create an Employees Table

```sql
CREATE TABLE employees (
    id INT,
    name VARCHAR(100),
    department VARCHAR(50),
    salary DECIMAL(10,2)
);
```

## Step 4: View Tables

```sql
SHOW TABLES;
```

## Step 5: View Table Structure

```sql
DESCRIBE employees;
```

## Step 6: Add a Column

```sql
ALTER TABLE employees
ADD email VARCHAR(100);
```

## Step 7: Delete the Table

```sql
DROP TABLE employees;
```

---

## Mini Challenge

Create a database named **college_db** and a table named **students** with the following columns:

- student_id
- name
- age
- course
- email

Then:

1. Display all tables.
2. Describe the table.
3. Add a `phone_number` column.
4. Rename the `course` column to `course_name`.

---

## Next Chapter

**Chapter 4: Data Types and Constraints**
