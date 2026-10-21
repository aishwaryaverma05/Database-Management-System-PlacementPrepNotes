# Phase 7: Transactions and Concurrency

## 1. What is a Transaction?

A **transaction** is a group of database operations treated as one logical unit of work.

**Example:** Transferring ₹500 from Account A to Account B.

1. Deduct ₹500 from Account A.
2. Add ₹500 to Account B.

Both operations should succeed together. If one fails, the transaction should be rolled back to avoid an incomplete transfer.

## 2. ACID Properties

ACID properties help ensure reliable database transactions.

### Atomicity
A transaction happens completely or not at all.

**Example:** Money should not be deducted without being credited to the other account.

### Consistency
A transaction takes the database from one valid state to another, maintaining defined rules and constraints.

**Example:** A bank transfer should preserve the total balance across both accounts.

### Isolation
Concurrent transactions should not interfere in ways that produce results inconsistent with the chosen isolation level.

**Example:** Two users booking the last available seat should not both successfully reserve it.

### Durability
Once a transaction is committed, its changes should survive a system crash, subject to the database's durability guarantees.

**Example:** After a successful payment is confirmed, the saved transaction should not disappear after a restart.

**Memory trick:** A = All or nothing, C = Correct state, I = Independent execution, D = Data stays saved.

## 3. COMMIT and ROLLBACK

### COMMIT
Permanently saves the transaction's changes.

```sql
COMMIT;
```

### ROLLBACK
Undoes uncommitted changes in the current transaction.

```sql
ROLLBACK;
```

**Example:**

```sql
BEGIN;

UPDATE Accounts
SET Balance = Balance - 500
WHERE Account_ID = 1;

-- If everything is correct:
COMMIT;

-- If something goes wrong before commit:
ROLLBACK;
```

Exact transaction syntax and behavior can vary by DBMS.

## 4. Concurrent Transactions

Concurrency means multiple transactions execute during overlapping periods.

**Example:** Two users try to update the same bank account at nearly the same time.

**Why is concurrency useful?**
- Allows multiple users to access the database.
- Improves throughput and resource utilization.

However, poor concurrency control can cause incorrect or inconsistent results.

## 5. Problems in Concurrent Transactions

### Lost Update
One transaction overwrites another transaction's update, causing one change to be lost.

**Example:** Two transactions read a balance of ₹1,000. One adds ₹200 and another deducts ₹100. If both write results based on the original balance, the final balance may incorrectly become ₹900 or ₹1,200 instead of ₹1,100.

### Dirty Read
A transaction reads data written by another transaction that has not yet committed.

**Example:** Transaction A changes a balance to ₹500 but has not committed. Transaction B reads ₹500. If A rolls back, B has read a value that was never committed.

### Non-Repeatable Read
A transaction reads the same row twice but gets different values because another transaction updates and commits that row between the reads.

**Example:** A transaction reads a price of ₹100, then reads it again and gets ₹120.

### Phantom Read
A transaction runs the same condition-based query twice but gets a different set of rows because another transaction inserts or deletes matching rows and commits.

**Example:** A query finds 5 employees earning more than ₹50,000. When repeated, it finds 6.

**Remember:**
- Dirty read = Reading uncommitted data.
- Non-repeatable read = Same row, different value.
- Phantom read = Different set of matching rows.
- Lost update = One update overwrites another.

## 6. Shared and Exclusive Locks

Locks help control concurrent access to data.

### Shared Lock (S Lock)
Used for reading data. Multiple transactions can generally hold shared locks on the same item.

### Exclusive Lock (X Lock)
Used for modifying data. It prevents conflicting access by other transactions.

| Shared Lock | Exclusive Lock |
|---|---|
| Mainly for reading | For writing |
| Multiple shared locks can coexist | Conflicts with other shared and exclusive locks |
| Used to protect read operations | Used to protect modifications |

## 7. Two-Phase Locking (2PL)

2PL is a locking protocol used to ensure conflict serializability.

It has two phases:

1. **Growing Phase:** A transaction can acquire locks but cannot release them.
2. **Shrinking Phase:** A transaction can release locks but cannot acquire new ones.

**Important:** Basic 2PL ensures conflict serializability, but it does not guarantee freedom from deadlocks.

## 8. Deadlock

A deadlock occurs when two or more transactions wait indefinitely for resources locked by one another.

**Example:**
- Transaction A locks Row 1 and waits for Row 2.
- Transaction B locks Row 2 and waits for Row 1.

Neither can proceed.

**How can deadlocks be handled?**
- Prevent deadlocks through suitable resource-ordering rules.
- Detect deadlocks and roll back a transaction.
- Use timeouts to stop transactions waiting too long.

## 9. Transaction Isolation Levels

Isolation levels control how much one transaction can observe the effects of concurrent transactions.

| Isolation Level | Simple Meaning |
|---|---|
| Read Uncommitted | May allow dirty reads |
| Read Committed | Prevents dirty reads |
| Repeatable Read | Prevents dirty reads and non-repeatable reads under the standard model |
| Serializable | Strongest standard isolation level; aims for results equivalent to serial execution |

**Remember:** Higher isolation generally provides stronger protection against concurrency anomalies but may reduce concurrency or performance.

Exact behavior, especially for phantom reads, depends on the DBMS implementation.

---

## Quick Revision: One-Line Answers

1. **What is a transaction?** A group of database operations treated as one logical unit.
2. **What are ACID properties?** Atomicity, Consistency, Isolation, and Durability.
3. **What is COMMIT?** Saves the transaction's changes.
4. **What is ROLLBACK?** Undoes uncommitted changes.
5. **What is concurrency?** Multiple transactions executing during overlapping periods.
6. **What is a dirty read?** Reading another transaction's uncommitted data.
7. **What is a non-repeatable read?** Reading the same row twice and getting different values.
8. **What is a phantom read?** Getting a different set of rows for the same query.
9. **What is a lost update?** One transaction overwrites another transaction's update.
10. **What is a deadlock?** Transactions wait indefinitely for resources held by one another.
11. **What is 2PL?** A locking protocol with growing and shrinking phases.
12. **Which isolation level is strongest?** Serializable.
13. **What is a shared lock?** A lock generally used for reading.
14. **What is an exclusive lock?** A lock used for modifying data.
