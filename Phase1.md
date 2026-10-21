# Phase 1: DBMS Fundamentals

## 1. What is DBMS?

**DBMS (Database Management System)** is software used to store, manage, retrieve, and update data efficiently.

**Examples:** MySQL, PostgreSQL, Oracle Database.

**Example:** A college uses a DBMS to store student details, marks, attendance, and fees.

### Advantages

- Reduces data duplication.
- Improves data security.
- Makes searching and updating easier.
- Supports backup and recovery.
- Maintains data consistency.

### Disadvantages

- Can be expensive to maintain.
- Requires storage and computing resources.
- Failure may affect many users if proper recovery is not available.

## 2. DBMS vs RDBMS

**RDBMS (Relational DBMS)** stores data in tables made of rows and columns and supports relationships between tables.

| DBMS                                                  | RDBMS                                               |
| ----------------------------------------------------- | --------------------------------------------------- |
| General term for database management systems          | A type of DBMS based on the relational model        |
| May use different data models                         | Stores data in tables                               |
| Relationships depend on the data model                | Relationships commonly use primary and foreign keys |
| Example: database systems using non-relational models | MySQL, PostgreSQL, Oracle                           |

**Remember:** Every RDBMS is a DBMS, but every DBMS is not an RDBMS.

## 3. File System vs DBMS

| File System                                             | DBMS                                              |
| ------------------------------------------------------- | ------------------------------------------------- |
| Data is stored in separate files                        | Data is managed in a database                     |
| More chances of data duplication                        | Helps reduce duplication                          |
| Searching and updating can be difficult                 | Queries make searching easier                     |
| Security is harder to manage centrally                  | Provides database-level access control            |
| Backup and consistency are mostly application-dependent | Provides database backup and consistency features |

**Example:** Managing student records using separate Excel files is harder than managing them through a database.

## 4. Types of Databases

- **Relational:** Stores data in tables. Example: MySQL.
- **Document:** Stores data as documents, often JSON-like. Example: MongoDB.
- **Key-Value:** Stores data as key-value pairs. Example: Redis.
- **Graph:** Stores data as nodes and relationships. Example: Neo4j.

**Placement tip:** Know the basic purpose and one example of each type.

## 5. Schema vs Instance

### Schema

The **structure or design** of a database.&#x20;

Example: A Student table has columns `Student_ID`, `Name`, and `Marks`.

### Instance

The **actual data stored** in the database at a particular time.

Example: `101, Rahul, 85`.

| Schema                         | Instance                                           |
| ------------------------------ | -------------------------------------------------- |
| Database structure             | Actual data                                        |
| Changes less frequently        | Changes frequently                                 |
| Defined during database design | Changes with insert, update, and delete operations |

**Easy trick:** Schema = Design; Instance = Data.

## 6. Three-Schema Architecture

It describes a database at three levels.

### External Level

- What an individual user sees.
- Different users can see different parts of the database.

Example: A student sees their own marks.

### Conceptual Level

- Describes the overall logical structure of the database.
- Includes tables, relationships, and constraints.

Example: Student, Course, and Enrollment tables and their relationships.

### Internal Level

- Describes how data is physically stored.
- Includes storage organization and indexes.

Example: How database records and indexes are stored on disk.

**Remember:** External = User view, Conceptual = Logical design, Internal = Physical storage.

## 7. Data Abstraction

Data abstraction means **hiding unnecessary implementation details** and showing users only what they need.

Example: When checking marks on a college portal, you see your marks, not how the database stores them on disk.

It has three levels:

- Physical level: How data is stored.
- Logical level: What data is stored and how it is related.
- View level: What a particular user can see.

## 8. Data Independence

Data independence means changing one level of a database without requiring major changes to the next higher level.

### Physical Data Independence

Changes in physical storage do not require changes to the logical structure.

**Example:** Changing how records are stored or adding an appropriate index without changing the table structure or application queries.

### Logical Data Independence

Changes in the logical structure do not require changes to user views or applications, provided those views and applications can remain compatible.

**Example:** Adding a new column to a table without affecting an existing application that uses the old columns.

| Physical                             | Logical                                                  |
| ------------------------------------ | -------------------------------------------------------- |
| Changes physical storage             | Changes logical schema                                   |
| Usually easier to achieve            | Usually harder to achieve                                |
| Example: Changing storage or indexes | Example: Adding a column while preserving existing views |

**Interview trick:** Physical data independence is generally easier than logical data independence.

---

## Quick Revision: One-Line Answers

1. **What is DBMS?** Software used to store, manage, and retrieve data.
2. **What is RDBMS?** A DBMS that organizes data using relational tables.
3. **What is a schema?** The structure or design of a database.
4. **What is an instance?** The actual data present at a particular time.
5. **What is data abstraction?** Hiding unnecessary database details.
6. **What is data independence?** Changing one database level without major changes to higher levels.
7. **Which data independence is easier?** Physical data independence.
8. **What are the three schema levels?** External, conceptual, and internal.
9. **Why use a DBMS instead of files?** For easier querying, better access control, and data consistency.
10. **Name two RDBMS examples.** MySQL and PostgreSQL.
