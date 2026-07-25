
# Chapter 17: Triggers

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand what a Trigger is.
- Learn when triggers are executed.
- Create and delete triggers.
- Use `BEFORE` and `AFTER` triggers.
- Access `NEW` and `OLD` values.
- Implement audit logging using triggers.

---

# What is a Trigger?

A **Trigger** is a special database object that automatically executes when a specific event occurs on a table.

Unlike Stored Procedures, triggers are **not called manually**.

They are automatically executed when data is:

- Inserted
- Updated
- Deleted

---

# Why Use Triggers?

Triggers are commonly used to:

- Maintain audit logs
- Validate data
- Automatically update related tables
- Track changes
- Enforce business rules

---

# Trigger Events

Triggers can be fired for three events:

- **INSERT**
- **UPDATE**
- **DELETE**

Each event can have:

- **BEFORE**
- **AFTER**

---

# Trigger Types

| Trigger | Description |
|----------|-------------|
| BEFORE INSERT | Runs before inserting a row |
| AFTER INSERT | Runs after inserting a row |
| BEFORE UPDATE | Runs before updating a row |
| AFTER UPDATE | Runs after updating a row |
| BEFORE DELETE | Runs before deleting a row |
| AFTER DELETE | Runs after deleting a row |

---

# Creating a Trigger

## Syntax

```sql
DELIMITER //

CREATE TRIGGER trigger_name

BEFORE INSERT
ON table_name

FOR EACH ROW

BEGIN

    SQL statements;

END //

DELIMITER ;
```

---

# Example: BEFORE INSERT Trigger

Prevent employees from having a negative salary.

```sql
DELIMITER //

CREATE TRIGGER check_salary

BEFORE INSERT
ON employees

FOR EACH ROW

BEGIN

    IF NEW.salary < 0 THEN
        SET NEW.salary = 0;
    END IF;

END //

DELIMITER ;
```

Whenever a new employee is inserted, the salary cannot be negative.

---

# AFTER INSERT Trigger

Create an audit table.

```sql
CREATE TABLE employee_logs (

    log_id INT AUTO_INCREMENT PRIMARY KEY,

    message VARCHAR(255)

);
```

Create the trigger.

```sql
DELIMITER //

CREATE TRIGGER employee_insert_log

AFTER INSERT
ON employees

FOR EACH ROW

BEGIN

    INSERT INTO employee_logs(message)

    VALUES (
        CONCAT('Employee Added: ', NEW.employee_name)
    );

END //

DELIMITER ;
```

---

# Testing the Trigger

```sql
INSERT INTO employees

VALUES
(101, 'Rahul', 'IT', 65000);
```

Automatically, a log entry is created.

```text
Employee Added: Rahul
```

---

# BEFORE UPDATE Trigger

```sql
DELIMITER //

CREATE TRIGGER salary_validation

BEFORE UPDATE
ON employees

FOR EACH ROW

BEGIN

    IF NEW.salary < 0 THEN
        SET NEW.salary = OLD.salary;
    END IF;

END //

DELIMITER ;
```

Negative salary updates are prevented.

---

# AFTER UPDATE Trigger

```sql
DELIMITER //

CREATE TRIGGER employee_update_log

AFTER UPDATE
ON employees

FOR EACH ROW

BEGIN

    INSERT INTO employee_logs(message)

    VALUES (

        CONCAT(
            'Salary changed for ',
            NEW.employee_name
        )

    );

END //

DELIMITER ;
```

---

# BEFORE DELETE Trigger

```sql
DELIMITER //

CREATE TRIGGER prevent_delete

BEFORE DELETE
ON employees

FOR EACH ROW

BEGIN

    IF OLD.department = 'Management' THEN

        SIGNAL SQLSTATE '45000'

        SET MESSAGE_TEXT = 'Management employees cannot be deleted';

    END IF;

END //

DELIMITER ;
```

The deletion is blocked for employees in the Management department.

---

# OLD vs NEW

| Keyword | Used For |
|----------|----------|
| NEW | Access new values during INSERT or UPDATE |
| OLD | Access existing values during UPDATE or DELETE |

---

# Example

```sql
UPDATE employees

SET salary = 70000

WHERE employee_id = 101;
```

During execution:

```
OLD.salary = 65000

NEW.salary = 70000
```

---

# Viewing Triggers

Display all triggers in the current database.

```sql
SHOW TRIGGERS;
```

---

# Dropping a Trigger

## Syntax

```sql
DROP TRIGGER trigger_name;
```

---

## Example

```sql
DROP TRIGGER employee_insert_log;
```

---

# Practical Example

Automatically update the last modified timestamp.

```sql
DELIMITER //

CREATE TRIGGER update_timestamp

BEFORE UPDATE
ON employees

FOR EACH ROW

BEGIN

    SET NEW.last_updated = NOW();

END //

DELIMITER ;
```

Every update automatically records the latest timestamp.

---

# Advantages of Triggers

- Automatic execution
- Reduces repetitive code
- Maintains audit history
- Improves data integrity
- Enforces business rules

---

# Limitations of Triggers

- Can make debugging difficult
- Hidden execution may confuse developers
- Excessive triggers can affect performance
- Complex trigger chains are hard to maintain

---

# Best Practices

- Keep trigger logic simple.
- Use meaningful trigger names.
- Avoid performing heavy processing inside triggers.
- Document every trigger clearly.
- Test triggers thoroughly before deployment.

---

# Summary

In this chapter, you learned:

- What triggers are.
- BEFORE and AFTER triggers.
- INSERT, UPDATE, and DELETE triggers.
- Using `NEW` and `OLD`.
- Creating audit logs.
- Viewing and deleting triggers.

---

# Key Terms

- Trigger
- BEFORE Trigger
- AFTER Trigger
- NEW
- OLD
- Audit Log
- SHOW TRIGGERS
- DROP TRIGGER

---

# Practice Questions

### Multiple Choice Questions

**1. When is a trigger executed?**

A. Only when called manually

B. Automatically when an event occurs

C. Only during SELECT queries

D. Only during transactions

> **Answer:** B

---

**2. Which keyword represents the new row values?**

A. CURRENT

B. OLD

C. NEW

D. VALUE

> **Answer:** C

---

**3. Which statement displays all triggers?**

A.

```sql
SHOW TRIGGERS;
```

B.

```sql
SHOW TABLES;
```

C.

```sql
SHOW EVENTS;
```

D.

```sql
SHOW DATABASES;
```

> **Answer:** A

---

**4. Which events can trigger a database trigger?**

A. INSERT, UPDATE, DELETE

B. SELECT only

C. CREATE only

D. DROP only

> **Answer:** A

---

# Hands-on Exercise

Create an audit table.

```sql
CREATE TABLE employee_logs (

    log_id INT AUTO_INCREMENT PRIMARY KEY,

    message VARCHAR(255)

);
```

---

Create an `AFTER INSERT` trigger.

```sql
DELIMITER //

CREATE TRIGGER employee_insert_log

AFTER INSERT
ON employees

FOR EACH ROW

BEGIN

    INSERT INTO employee_logs(message)

    VALUES (
        CONCAT('Employee Added: ', NEW.employee_name)
    );

END //

DELIMITER ;
```

---

Insert a new employee.

```sql
INSERT INTO employees

VALUES
(105, 'Priya', 'HR', 50000);
```

---

Verify the audit log.

```sql
SELECT *
FROM employee_logs;
```

---

Delete the trigger.

```sql
DROP TRIGGER employee_insert_log;
```

---

# Mini Challenge

Using the `employees` table:

1. Create a `BEFORE INSERT` trigger to prevent negative salaries.
2. Create an `AFTER UPDATE` trigger to log salary changes.
3. Create a `BEFORE DELETE` trigger to prevent deleting employees from the HR department.
4. Display all triggers.
5. Test each trigger with sample data.

---

## Interview Tips

- Triggers execute **automatically** when an `INSERT`, `UPDATE`, or `DELETE` event occurs.
- `NEW` refers to the new row values, while `OLD` refers to the existing row values.
- Triggers are commonly used for **audit logging**, **validation**, and **enforcing business rules**.
- Avoid placing complex business logic inside triggers, as they can make debugging and maintenance more difficult.

---

## Next Chapter

**Chapter 18: SQL Best Practices**
