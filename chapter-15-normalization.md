
# Chapter 15: Normalization

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand what normalization is.
- Learn why normalization is important.
- Identify data redundancy and anomalies.
- Understand the Normal Forms (1NF, 2NF, 3NF, BCNF).
- Design well-structured relational databases.

---

# What is Normalization?

**Normalization** is the process of organizing data in a database to:

- Reduce data redundancy (duplicate data)
- Improve data consistency
- Eliminate update, insert, and delete anomalies
- Make the database easier to maintain

In simple terms, normalization means **storing each piece of information only once**.

---

# Why Do We Need Normalization?

Imagine storing employee and department information in a single table.

| Employee ID | Employee Name | Department | Manager |
|-------------|---------------|------------|----------|
| 101 | Rahul | IT | John |
| 102 | Amit | IT | John |
| 103 | Priya | HR | Smith |

Notice that the department and manager information is repeated.

Problems include:

- Wasted storage
- Difficult updates
- Higher chance of inconsistent data

---

# Problems Without Normalization

## 1. Data Redundancy

The same information is stored multiple times.

Example:

```
Department = IT
Manager = John
```

Repeated for every IT employee.

---

## 2. Update Anomaly

Suppose the IT manager changes from **John** to **David**.

Every IT employee record must be updated.

If one record is missed, the database becomes inconsistent.

---

## 3. Insert Anomaly

You cannot insert a new department until at least one employee joins that department.

---

## 4. Delete Anomaly

If the last employee in the HR department leaves, deleting the employee record also deletes the department information.

---

# What are Normal Forms?

Normalization is performed in stages called **Normal Forms (NF)**.

The common normal forms are:

- First Normal Form (1NF)
- Second Normal Form (2NF)
- Third Normal Form (3NF)
- Boyce-Codd Normal Form (BCNF)

---

# First Normal Form (1NF)

### Rule

- Each column should contain a single value.
- No repeating groups.
- Each row should be unique.

---

## Not in 1NF

| Student | Subjects |
|----------|----------------|
| Rahul | Java, SQL, Python |

Multiple subjects are stored in one column.

---

## In 1NF

| Student | Subject |
|----------|----------|
| Rahul | Java |
| Rahul | SQL |
| Rahul | Python |

Each cell contains only one value.

---

# Second Normal Form (2NF)

### Rules

- Must already be in 1NF.
- Every non-key column should depend on the entire Primary Key.

---

## Example

| Student ID | Course ID | Student Name | Course Name |
|-------------|------------|--------------|--------------|

Here:

- Student Name depends only on Student ID.
- Course Name depends only on Course ID.

They should be separated.

---

## After 2NF

### Students

| Student ID | Student Name |
|-------------|--------------|
| 101 | Rahul |

---

### Courses

| Course ID | Course Name |
|------------|-------------|
| C101 | Java |

---

### Student_Course

| Student ID | Course ID |
|------------|------------|

Duplicate information is removed.

---

# Third Normal Form (3NF)

### Rules

- Must already be in 2NF.
- No transitive dependency.

A non-key column should not depend on another non-key column.

---

## Example

| Employee ID | Department | Manager |
|-------------|------------|----------|

Here,

```
Employee ID
        ↓
Department
        ↓
Manager
```

Manager depends on Department, not Employee ID.

---

## After 3NF

### Employees

| Employee ID | Employee Name | Department ID |
|-------------|---------------|---------------|

---

### Departments

| Department ID | Department Name | Manager |
|---------------|-----------------|----------|

Now the manager information is stored only once.

---

# Boyce-Codd Normal Form (BCNF)

BCNF is a stricter version of 3NF.

### Rule

Every determinant must be a candidate key.

BCNF is mainly required in advanced database design and is less commonly encountered in beginner-level applications.

---

# Normal Forms Summary

| Normal Form | Purpose |
|--------------|----------|
| 1NF | Remove repeating groups |
| 2NF | Remove partial dependency |
| 3NF | Remove transitive dependency |
| BCNF | Stronger version of 3NF |

---

# Before and After Normalization

### Before

```
Employees Table

Employee
Department
Manager
Department Phone
Department Location
```

Department information is repeated for every employee.

---

### After

```
Employees
------------
Employee ID
Employee Name
Department ID

Departments
--------------
Department ID
Department Name
Manager
Location
Phone
```

No repeated department information.

---

# Advantages of Normalization

- Reduces duplicate data.
- Saves storage space.
- Improves data consistency.
- Simplifies updates.
- Reduces anomalies.
- Makes database design scalable.

---

# Disadvantages of Normalization

- More tables are created.
- Queries may require more joins.
- Complex reports may become slower.
- Database design requires more planning.

---

# Denormalization

Sometimes databases intentionally store duplicate data to improve performance.

This process is called **Denormalization**.

It is commonly used in:

- Reporting systems
- Data warehouses
- Analytics applications

---

# Best Practices

- Normalize databases during the design phase.
- Use Primary Keys and Foreign Keys appropriately.
- Avoid unnecessary duplication.
- Do not over-normalize small databases.
- Balance normalization and performance based on application requirements.

---

# Summary

In this chapter, you learned:

- What normalization is.
- Problems caused by redundant data.
- Update, Insert, and Delete anomalies.
- 1NF, 2NF, 3NF, and BCNF.
- Benefits and limitations of normalization.

---

# Key Terms

- Normalization
- Redundancy
- Anomaly
- 1NF
- 2NF
- 3NF
- BCNF
- Denormalization

---

# Practice Questions

### Multiple Choice Questions

**1. What is the primary goal of normalization?**

A. Increase duplicate data

B. Reduce data redundancy

C. Improve internet speed

D. Create more tables unnecessarily

> **Answer:** B

---

**2. Which normal form ensures each column contains atomic values?**

A. 1NF

B. 2NF

C. 3NF

D. BCNF

> **Answer:** A

---

**3. Which normal form removes transitive dependencies?**

A. 1NF

B. 2NF

C. 3NF

D. 4NF

> **Answer:** C

---

**4. What is the main disadvantage of normalization?**

A. Data inconsistency

B. More duplicate data

C. More tables and joins

D. Loss of data

> **Answer:** C

---

# Hands-on Exercise

Design a database for a college.

### Step 1 (Unnormalized)

| Student ID | Student Name | Course | Instructor |
|-------------|--------------|---------|------------|
| 101 | Rahul | Java | Amit |
| 101 | Rahul | SQL | Priya |

---

### Step 2 (1NF)

Separate each course into individual rows.

---

### Step 3 (2NF)

Create separate tables:

- Students
- Courses
- Student_Course

---

### Step 4 (3NF)

Move instructor details to a separate **Courses** table.

---

# Mini Challenge

A company stores the following in one table:

- Employee ID
- Employee Name
- Department Name
- Department Manager
- Department Phone
- Project Name

Normalize this design up to **Third Normal Form (3NF)** by identifying the tables, primary keys, and relationships.

---

## Interview Tips

- **Normalization** reduces redundancy and improves data consistency.
- **1NF** removes repeating groups and ensures atomic values.
- **2NF** removes partial dependencies.
- **3NF** removes transitive dependencies.
- In real-world OLTP systems, databases are typically designed up to **3NF**, while **BCNF** is used for more complex scenarios.

---

## Next Chapter

**Chapter 16: Stored Procedures and Functions**
