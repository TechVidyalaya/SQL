
# Chapter 1: Introduction to Databases

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand what a database is.
- Explain why databases are needed.
- Differentiate between data and information.
- Understand the types of databases.
- Learn what a Relational Database Management System (RDBMS) is.
- Understand where SQL is used in real-world applications.

---

# What is Data?

**Data** is a collection of raw facts that have not yet been processed.

### Examples

- Bikash
- 25
- ₹50,000
- Java
- 95

These values alone do not provide meaningful information.

---

# What is Information?

**Information** is processed and organized data that has meaning.

### Example

| Name | Age | Salary |
|------|-----|---------|
| Bikash | 25 | ₹50,000 |

Now the data provides useful information.

---

# What is a Database?

A **Database** is an organized collection of related data that can be easily stored, accessed, updated, and managed.

Think of a database as a digital filing cabinet.

Instead of keeping records on paper, organizations store them electronically.

---

# Why Do We Need Databases?

Imagine a college storing student records in notebooks.

Problems include:

- Difficult to search
- Data duplication
- Data loss
- No security
- Difficult to update records
- Multiple people cannot work simultaneously

Databases solve all these problems.

---

# Real-World Examples

Databases are used in almost every software application.

| Application | Stored Data |
|-------------|-------------|
| Banking | Customers, Accounts, Transactions |
| Amazon | Products, Orders, Payments |
| Hospital | Patients, Doctors, Appointments |
| College | Students, Courses, Marks |
| WhatsApp | Users, Messages, Media |
| YouTube | Videos, Comments, Subscribers |

---

# Types of Databases

## 1. Relational Database (RDBMS)

Stores data in tables.

Examples:

- MySQL
- PostgreSQL
- Oracle Database
- Microsoft SQL Server

This is the most commonly used database for enterprise applications.

---

## 2. NoSQL Database

Stores data in flexible formats such as documents, key-value pairs, graphs, or columns.

Examples:

- MongoDB
- Cassandra
- Redis
- Neo4j

Used for large-scale and high-performance applications.

---

# What is DBMS?

**DBMS** stands for **Database Management System**.

It is software used to create, manage, update, and retrieve data from a database.

Examples:

- MySQL
- Oracle Database
- SQL Server
- PostgreSQL

---

# What is RDBMS?

**RDBMS** stands for **Relational Database Management System**.

It stores data in the form of tables.

Each table consists of:

- Rows (Records)
- Columns (Fields)

Example:

| StudentID | Name | Branch |
|-----------|------|--------|
| 101 | Rahul | CSE |
| 102 | Priya | ECE |

The tables can be related using keys.

---

# DBMS vs RDBMS

| DBMS | RDBMS |
|------|--------|
| Stores data | Stores data in tables |
| Relationships are optional | Relationships are supported |
| Less suitable for large applications | Suitable for enterprise applications |
| Limited data integrity | High data integrity |

---

# What is SQL?

**SQL** stands for **Structured Query Language**.

SQL is used to communicate with relational databases.

Using SQL, we can:

- Create databases
- Create tables
- Insert data
- Update data
- Delete data
- Retrieve data
- Manage users and permissions

---

# Popular Database Systems

| Database | Company |
|----------|---------|
| MySQL | Oracle |
| PostgreSQL | PostgreSQL Global Development Group |
| Oracle Database | Oracle |
| Microsoft SQL Server | Microsoft |
| MariaDB | MariaDB Foundation |

---

# SQL in a Typical Application

```
Application
      │
      ▼
Backend (Java / Spring Boot)
      │
      ▼
SQL Queries
      │
      ▼
Database
```

The backend sends SQL queries to the database, which processes them and returns the required data.

---

# Advantages of Databases

- Fast data retrieval
- Reduced data duplication
- Improved data security
- Data consistency
- Multi-user access
- Easy backup and recovery
- Better data management

---

# Summary

In this chapter, you learned:

- Difference between data and information
- What a database is
- Why databases are important
- Types of databases
- DBMS and RDBMS
- Introduction to SQL
- Common database systems
- Advantages of databases

---

# Key Terms

- Data
- Information
- Database
- DBMS
- RDBMS
- SQL
- Table
- Row
- Column

---

# Practice Questions

### Multiple Choice Questions

**1. What does SQL stand for?**

A. Simple Query Language

B. Structured Query Language

C. Standard Question Language

D. Sequential Query Language

> **Answer:** B

---

**2. Which database is an RDBMS?**

A. MongoDB

B. Redis

C. MySQL

D. Cassandra

> **Answer:** C

---

**3. Data stored in an RDBMS is organized into:**

A. Files

B. Tables

C. Images

D. Folders

> **Answer:** B

---

### Short Answer Questions

1. What is a database?
2. Differentiate between data and information.
3. What is a DBMS?
4. What is an RDBMS?
5. Name any four relational databases.
6. List three advantages of databases.

---

# Hands-on Activity

Think of an online shopping application.

List at least five types of information that need to be stored in a database.

**Example:**

- Customers
- Products
- Orders
- Payments
- Delivery Details

---

## Next Chapter

**Chapter 2: Installing MySQL**
