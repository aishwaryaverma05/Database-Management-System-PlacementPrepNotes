# Phase 7: Transactions and Concurrency

## 1. What is a Transaction?

A transaction is a group of database operations treated as one unit.

**Example:** You transfer ₹500 from Account A to Account B.

1. ₹500 is deducted from Account A.
2. ₹500 is added to Account B.

Both operations should succeed together. If the transfer fails halfway, the database should undo the incomplete changes.

## 2. ACID Properties

ACID makes database transactions reliable.

- **Atomicity:** Either all operations happen or none happen.
- **Consistency:** The transaction follows database rules and keeps the data valid.
- **Isolation:** Concurrent transactions should not interfere incorrectly with each other.
- **Durability:** Once committed, changes survive failures covered by the database's durability guarantees.

**Example:** In a bank transfer, money should not disappear because only one part of the transfer succeeded.

## 3. COMMIT and ROLLBACK

- **COMMIT:** Saves the transaction's changes.
- **ROLLBACK:** Undoes uncommitted changes.

```sql
BEGIN;

UPDATE Accounts
SET Balance = Balance - 500
WHERE Account_ID = 1;

COMMIT;
```

If something goes wrong before committing, you can use `ROLLBACK` to undo the uncommitted changes.

## 4. Concurrent Transactions

Concurrency means multiple transactions are executing during overlapping periods.

**Example:** Two people try to book the last available seat at the same time.

Without proper control, both might think the seat is available. Concurrency control helps prevent such incorrect results.

## 5. Problems Caused by Concurrent Transactions

### Lost Update
Two transactions update the same data, and one overwrites the other's change.

**Example:** Both transactions read ₹1,000. One adds ₹200, while the other deducts ₹100. If both write results based on the old balance, one update may be lost.

### Dirty Read
A transaction reads another transaction's changes before they are committed.

**Example:** Transaction A changes a balance to ₹500 but has not committed. Transaction B reads ₹500. Then A rolls back, meaning B read a value that was never committed.

### Non-Repeatable Read
A transaction reads the same row twice but gets different values because another transaction updated and committed it between the reads.

**Example:** You read a product price of ₹100. Another transaction changes it to ₹120. You read the same row again and get ₹120.

### Phantom Read
A transaction runs the same query twice but gets a different set of matching rows because another transaction inserts or deletes rows and commits.

**Example:** Your query finds 5 employees earning above ₹50,000. When you run it again, it finds 6.

**Quick difference:**
- Dirty read = Reading uncommitted data.
- Non-repeatable read = Same row, different value.
- Phantom read = Different set of rows.
- Lost update = One change overwrites another.

## 6. Shared Lock vs Exclusive Lock

A lock is like a restriction on data that controls which transactions can read or modify it at the same time.

Imagine a bank account with a balance of ₹1,000.

### Shared Lock (S Lock) — Reading

Suppose you and another user both want to **check the balance**.

- Both can read the balance at the same time.
- Neither is modifying the balance.
- Multiple shared locks can exist on the same data.

This is called a Shared Lock.

### Exclusive Lock (X Lock) — Modifying

Now suppose you want to **withdraw ₹200**.

- The database needs to modify the balance.
- It obtains an Exclusive Lock according to its locking protocol.
- Conflicting reads and writes must wait while the lock is held.

This prevents another transaction from interfering with the protected update.

| Shared Lock (S) | Exclusive Lock (X) |
|---|---|
| Used for reading | Used for writing |
| Multiple readers can share the lock | Conflicting readers and writers must wait |
| Other shared locks are allowed | Other shared or exclusive locks conflict |

**Interview answer:** A Shared Lock allows multiple transactions to read the same data, whereas an Exclusive Lock protects data being modified from conflicting access.

## 7. Two-Phase Locking (2PL)

Now the important question: **When should a transaction acquire and release locks?**

Two-Phase Locking is a protocol that sets rules for acquiring and releasing locks. It helps ensure conflict serializability, meaning the concurrent execution is equivalent to some serial order of transactions.

It has two phases.

### Phase 1: Growing Phase

A transaction can acquire new locks but cannot release any locks.

Example:
- Acquire a lock on Account A.
- Acquire a lock on Account B.
- Both locks can be acquired during this phase.

### Phase 2: Shrinking Phase

Once a transaction releases its first lock, it cannot acquire any new locks.

Example:
- Release the lock on Account A.
- Release the lock on Account B.
- It cannot acquire another lock after releasing its first one.

**Easy way to remember:** First acquire locks, then release locks. Never acquire a new lock after releasing one.

**Important:** 2PL helps ensure conflict serializability, but it does not prevent deadlocks.

## 8. Deadlock

A deadlock occurs when transactions wait for each other indefinitely.

**Example:**
- Transaction A holds a lock on Account 1 and waits for Account 2.
- Transaction B holds a lock on Account 2 and waits for Account 1.

A waits for B, and B waits for A. Neither can proceed.

**How can it be handled?**
- Detect the deadlock and roll back one transaction.
- Use timeouts.
- Prevent circular waiting through appropriate resource-ordering rules.

## 9. Transaction Isolation Levels

Isolation levels control how much one transaction can see changes made by concurrent transactions.

| Level | Simple meaning |
|---|---|
| Read Uncommitted | May allow dirty reads |
| Read Committed | Prevents dirty reads |
| Repeatable Read | Prevents dirty and non-repeatable reads under the standard model |
| Serializable | Strongest standard level; aims to make transactions behave as if executed one by one |

Higher isolation generally provides stronger protection but can reduce concurrency or performance. Exact behavior depends on the DBMS.

---

## Quick Revision: One-Line Answers

1. **Transaction:** A group of database operations treated as one unit.
2. **ACID:** Atomicity, Consistency, Isolation, and Durability.
3. **COMMIT:** Saves transaction changes.
4. **ROLLBACK:** Undoes uncommitted changes.
5. **Concurrency:** Multiple transactions execute during overlapping periods.
6. **Shared Lock:** Allows multiple transactions to read the same data.
7. **Exclusive Lock:** Protects data being modified from conflicting access.
8. **2PL:** A protocol that requires locks to be acquired before any locks are released.
9. **Deadlock:** Transactions wait for resources held by each other.
10. **Serializable:** The strongest standard isolation level.
