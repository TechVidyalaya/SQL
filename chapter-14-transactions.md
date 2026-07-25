# Chapter 14: Transactions

## Learning Objectives

By the end of this chapter, you will be able to:

- Understand what a transaction is.
- Learn the ACID properties.
- Use `COMMIT`, `ROLLBACK`, and `SAVEPOINT`.
- Understand auto-commit mode.
- Apply transactions in real-world scenarios.
- Maintain data consistency during database operations.

---

# What is a Transaction?

A **Transaction** is a sequence of one or more SQL statements that are executed as a single unit of work.

A transaction ensures that either:

- **All operations succeed**, or
- **None of them are applied.**

This helps maintain data consistency.

---

# Real-World Example

Imagine transferring ₹5,000 from Account A to Account B.

Step 1

```
Account A = ₹20,000
Account B = ₹10,000
```

Step 2

Deduct ₹5,000 from Account A.

```
Account A = ₹15,000
```

Step 3

Add ₹5,000 to Account B.

```
Account B = ₹15,000
```

If the system crashes after Step 2 but before Step 3, the money is lost.

A transaction prevents this by ensuring both operations complete successfully.

---

# Transaction Flow

```
START TRANSACTION

↓

Execute SQL Statements

↓

Success?
   │
 ┌─┴──────────┐
 │            │
Yes          No
 │            │
COMMIT    ROLLBACK
```

---

# Starting a Transaction

```sql
START TRANSACTION;
```

or

```sql
BEGIN;
```

---

# COMMIT

`COMMIT` permanently saves all changes made during a transaction.

## Example

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 5000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 5000
WHERE account_id = 2;

COMMIT;
```

The transfer is now permanently saved.

---

# ROLLBACK

`ROLLBACK` cancels all changes made during the current transaction.

## Example

```sql
START TRANSACTION;

UPDATE employees
SET salary = salary + 10000;

ROLLBACK;
```

The salary update is cancelled.

---

# SAVEPOINT

A **SAVEPOINT** creates a checkpoint inside a transaction.

Instead of rolling back the entire transaction, you can roll back to a specific point.

---

## Example

```sql
START TRANSACTION;

UPDATE employees
SET salary = salary + 5000
WHERE employee_id = 101;

SAVEPOINT salary_updated;

UPDATE employees
SET department = 'HR'
WHERE employee_id = 101;

ROLLBACK TO salary_updated;

COMMIT;
```

Result:

- Salary update is saved.
- Department update is cancelled.

---

# Releasing a SAVEPOINT

```sql
RELEASE SAVEPOINT salary_updated;
```

The savepoint is removed.

---

# Auto Commit

By default, MySQL uses **Auto Commit** mode.

Every SQL statement is committed automatically.

Example

```sql
UPDATE employees
SET salary = 60000
WHERE employee_id = 1;
```

The change is immediately saved.

---

# Disable Auto Commit

```sql
SET autocommit = 0;
```

Now you must explicitly use:

```sql
COMMIT;
```

or

```sql
ROLLBACK;
```

---

# ACID Properties

Transactions follow the **ACID** principles.

---

## A – Atomicity

A transaction is treated as a single unit.

Either all operations succeed or none do.

---

## C – Consistency

A transaction moves the database from one valid state to another.

Rules and constraints remain intact.

---

## I – Isolation

Multiple transactions do not interfere with each other.

Each transaction behaves as if it is running alone.

---

## D – Durability

Once committed, changes remain permanent even after a system crash.

---

# ACID Summary

| Property | Description |
|-----------|-------------|
| Atomicity | All or nothing |
| Consistency | Valid data before and after transaction |
| Isolation | Transactions do not affect each other |
| Durability | Committed data is permanent |

---

# Practical Example

Suppose an online shopping application.

Steps:

1. Reduce product stock.
2. Create order.
3. Process payment.
4. Generate invoice.

If payment fails:

```
ROLLBACK
```

Everything returns to its original state.

---

# Transaction Example

```sql
START TRANSACTION;

INSERT INTO orders(customer_name, amount)
VALUES ('Rahul', 2500);

UPDATE inventory
SET quantity = quantity - 1
WHERE product_id = 101;

COMMIT;
```

---

# Best Practices

- Keep transactions as short as possible.
- Always commit successful transactions.
- Roll back transactions when errors occur.
- Avoid unnecessary locks.
- Use savepoints for complex transactions.

---

# Summary

In this chapter, you learned:

- Transactions
- COMMIT
- ROLLBACK
- SAVEPOINT
- Auto Commit
- ACID properties
- Transaction workflow

---

# Key Terms

- Transaction
- COMMIT
- ROLLBACK
- SAVEPOINT
- Auto Commit
- Atomicity
- Consistency
- Isolation
- Durability
- ACID

---

# Practice Questions

### Multiple Choice Questions

**1. Which command permanently saves a transaction?**

A. SAVE

B. COMMIT

C. FINISH

D. APPLY

> **Answer:** B

---

**2. Which command cancels all changes in a transaction?**

A. DELETE

B. CANCEL

C. ROLLBACK

D. RESET

> **Answer:** C

---

**3. Which ACID property ensures all operations succeed or none do?**

A. Consistency

B. Durability

C. Isolation

D. Atomicity

> **Answer:** D

---

**4. Which command creates a checkpoint within a transaction?**

A. MARK

B. SAVEPOINT

C. CHECKPOINT

D. HOLD

> **Answer:** B

---

# Hands-on Exercise

Create a sample table.

```sql
CREATE TABLE accounts (

    account_id INT PRIMARY KEY,

    account_holder VARCHAR(100),

    balance DECIMAL(10,2)

);
```

---

Insert sample data.

```sql
INSERT INTO accounts
VALUES
(1, 'Rahul', 20000),
(2, 'Priya', 10000);
```

---

Transfer ₹5,000.

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 5000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 5000
WHERE account_id = 2;

COMMIT;
```

---

Test Rollback.

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

ROLLBACK;
```

Verify the balance remains unchanged.

---

# Mini Challenge

Using the `accounts` table:

1. Transfer ₹2,000 from Account 1 to Account 2.
2. Use a transaction to perform both updates.
3. Create a savepoint after deducting the amount.
4. Roll back to the savepoint.
5. Commit the final transaction.
6. Verify the balances.

---

## Interview Tips

- Transactions ensure **data integrity** by treating multiple SQL statements as a single unit.
- `COMMIT` permanently saves changes, while `ROLLBACK` undoes uncommitted changes.
- `SAVEPOINT` allows partial rollbacks within a transaction.
- The **ACID** properties are one of the most frequently asked SQL interview topics and are fundamental to relational databases.

---

## Next Chapter

**Chapter 15: Normalization**
