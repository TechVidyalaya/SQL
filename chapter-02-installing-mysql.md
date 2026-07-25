# Chapter 2: Installing MySQL

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand what MySQL is.
- Install MySQL Server and MySQL Workbench.
- Connect to the MySQL Server.
- Create your first database connection.
- Execute your first SQL query.

---

# What is MySQL?

**MySQL** is one of the world's most popular **Relational Database Management Systems (RDBMS)**.

It stores data in tables and uses SQL (Structured Query Language) to manage and retrieve data.

MySQL is:

- Open-source
- Fast and reliable
- Cross-platform
- Widely used in web and enterprise applications

---

# Why Learn MySQL?

MySQL is commonly used with:

- Java + Spring Boot
- PHP + Laravel
- Python + Django
- Node.js + Express

Many companies use MySQL for backend development because it is stable, scalable, and easy to learn.

---

# MySQL Components

### 1. MySQL Server

- Stores the databases.
- Executes SQL queries.
- Manages users and permissions.

---

### 2. MySQL Workbench

A graphical tool that helps you:

- Connect to MySQL
- Write SQL queries
- Design databases
- View tables and data

---

# Installing MySQL

Download the latest version of:

- MySQL Server
- MySQL Workbench

Follow the installation wizard:

1. Download the installer.
2. Choose the **Developer Default** setup (recommended).
3. Install all required components.
4. Set a password for the **root** user.
5. Complete the installation.

> **Note:** Remember the root password. You will need it to connect to the database.

---

# Starting MySQL

Open **MySQL Workbench**.

You should see a connection named **Local Instance MySQL** (or similar).

Double-click the connection.

Enter the root password.

If everything is correct, the SQL Editor will open.

---

# MySQL Workbench Overview

The main sections are:

- **Navigator** – Shows databases and tables.
- **SQL Editor** – Write and execute SQL queries.
- **Result Grid** – Displays query results.
- **Output Panel** – Shows messages and errors.

---

# Running Your First SQL Query

Type the following query:

```sql
SELECT 'Hello, MySQL!';
```

Click the **Execute** button (⚡) or press:

- **Ctrl + Enter** (Windows/Linux)
- **Cmd + Enter** (macOS)

### Output

| Hello, MySQL! |
|----------------|
| Hello, MySQL! |

Congratulations! You have executed your first SQL query.

---

# Checking the MySQL Version

Run the following query:

```sql
SELECT VERSION();
```

### Sample Output

| VERSION() |
|-----------|
| 8.4.x |

This displays the version of your MySQL Server.

---

# Showing Existing Databases

```sql
SHOW DATABASES;
```

### Sample Output

```
information_schema
mysql
performance_schema
sys
```

These are system databases created automatically during installation.

---

# Common System Databases

| Database | Purpose |
|----------|---------|
| mysql | Stores user accounts and privileges |
| information_schema | Metadata about databases and tables |
| performance_schema | Performance monitoring |
| sys | Simplified performance views |

---

# Common Installation Issues

### Access Denied

**Cause:** Incorrect username or password.

**Solution:** Verify the username (`root`) and password.

---

### Cannot Connect to Server

**Cause:** MySQL Server is not running.

**Solution:** Start the MySQL service from the operating system or Services panel.

---

### Port Already in Use

**Cause:** Another application is using port **3306**.

**Solution:** Stop the conflicting application or configure MySQL to use a different port.

---

# Best Practices

- Use a strong password for the root account.
- Do not use the root account for everyday applications.
- Back up databases regularly.
- Keep MySQL updated to the latest stable version.

---

# Summary

In this chapter, you learned:

- What MySQL is.
- Components of MySQL.
- How to install MySQL Server and Workbench.
- How to connect to the server.
- How to execute your first SQL query.
- How to check the MySQL version.
- How to view available databases.

---

# Key Terms

- MySQL
- MySQL Server
- MySQL Workbench
- Root User
- SQL Editor
- Database Connection

---

# Practice Questions

### Multiple Choice Questions

**1. MySQL is a:**

A. Programming Language

B. Web Browser

C. Relational Database Management System

D. Operating System

> **Answer:** C

---

**2. Which tool provides a graphical interface for MySQL?**

A. IntelliJ IDEA

B. Eclipse

C. MySQL Workbench

D. VS Code

> **Answer:** C

---

**3. Which command displays all databases?**

A.

```sql
LIST DATABASES;
```

B.

```sql
SHOW DATABASES;
```

C.

```sql
DISPLAY DATABASES;
```

D.

```sql
GET DATABASES;
```

> **Answer:** B

---

# Hands-on Exercise

1. Install MySQL Server.
2. Install MySQL Workbench.
3. Connect to the local MySQL instance.
4. Execute:

```sql
SELECT 'Welcome to SQL';
```

5. Check the MySQL version:

```sql
SELECT VERSION();
```

6. Display all databases:

```sql
SHOW DATABASES;
```

---

## Next Chapter

**Chapter 3: Database and Table Operations**
