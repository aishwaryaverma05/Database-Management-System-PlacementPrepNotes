# Phase 1 — DBMS Fundamentals

> **Goal:** Understand the basic concepts of DBMS and prepare for entry-level technical interviews.

## 1. What is DBMS and RDBMS?

### DBMS (Database Management System)

A DBMS is software that allows users to **store, organize, retrieve, update and manage data** efficiently.

**Examples:** MongoDB, file-based database systems, Microsoft Access.

### RDBMS (Relational Database Management System)

An RDBMS stores data in the form of **tables (rows and columns)** and uses relationships between tables to organize data.

**Examples:** MySQL, PostgreSQL, Oracle, SQL Server.

Example:

**Student table**

| Student_ID | Name | Department_ID |
|---|---|---|
| 101 | Aman | 1 |
| 102 | Riya | 2 |

**Department table**

| Department_ID | Department_Name |
|---|---|
| 1 | CSE |
| 2 | ECE |

Here, `Department_ID` connects the two tables.

### DBMS vs RDBMS

| DBMS | RDBMS |
|---|---|
| General database management system | Relational database management system |
| Data may use different storage models | Data is organized into related tables |
| Relationships depend on the database model | Relationships commonly use primary and foreign keys |
| Constraints depend on the system | Supports relational constraints and integrity |
| Examples include MongoDB and Microsoft Access | Examples include MySQL and PostgreSQL |

**Remember:** Every RDBMS is a DBMS, but every DBMS is not an RDBMS.

---

## 2. File System vs DBMS

A file system stores data in files, whereas a DBMS manages data through specialized database software.

| File System | DBMS |
|---|---|
| Data is stored in separate files | Data is managed in a database |
| Redundancy may be high | Redundancy can be controlled |
| Data consistency is harder to maintain | Constraints and transactions help maintain consistency |
| Searching and querying may require custom code | Supports query languages such as SQL |
| Security is generally managed at file level | Can provide fine-grained access control |
| Concurrent updates are harder to coordinate | Provides concurrency-control mechanisms |
| Backup and recovery may require manual processes | Provides database backup and recovery mechanisms |

### Example

Suppose a college stores student details in separate Excel files for fees, attendance and examinations.

The same student's details may appear multiple times. If the phone number changes in one file but not the others, the information becomes inconsistent.

A DBMS can maintain related information in organized tables and help prevent such problems.

### Limitations of a DBMS

- Higher setup and maintenance cost.
- Requires memory, storage and computing resources.
- Needs administration and technical expertise.
- A database failure can affect many applications if proper backup and recovery are absent.
- May introduce complexity for very small applications.

---

## 3. Advantages and Disadvantages of DBMS

### Advantages

1. **Reduced redundancy:** Minimizes unnecessary duplication of data.
2. **Improved consistency:** Helps keep related data correct and synchronized.
3. **Security:** Controls who can access or modify data.
4. **Data integrity:** Constraints help ensure valid data.
5. **Concurrency:** Coordinates simultaneous access by multiple users.
6. **Backup and recovery:** Helps restore data after failures.
7. **Data independence:** Some changes to storage can be made without changing application programs.
8. **Data sharing:** Multiple authorized users and applications can use the same database.

### Disadvantages

1. High initial and maintenance costs.
2. Requires skilled professionals.
3. Uses system resources.
4. Complex to design and manage.
5. A centralized failure can affect many users.
6. Security breaches may expose a large amount of data.

**Interview tip:** Never say a DBMS completely eliminates redundancy or guarantees security. It helps control redundancy and provides security mechanisms when configured properly.

---

## 4. Types of Databases

Databases can be classified by their data model, structure or intended use.

### A. Relational Database

- Stores structured data in tables.
- Uses relationships, keys and often SQL.
- Examples: MySQL, PostgreSQL, Oracle.

**Use case:** Banking, college management, e-commerce orders.

### B. NoSQL Database

Designed for data models that do not rely exclusively on traditional relational tables.

Common categories:

- **Document:** MongoDB — JSON-like documents.
- **Key-value:** Redis — key-value pairs.
- **Wide-column:** Cassandra — column-family-based storage.
- **Graph:** Neo4j — nodes and relationships.

**Use case:** Flexible product catalogs, caching, social networks and large distributed applications.

### C. Hierarchical Database

- Organizes data in a tree-like parent-child structure.
- A child generally has one parent in the traditional hierarchical model.

**Use case:** Data with a natural hierarchy.

### D. Network Database

- Organizes records through links.
- A record can have multiple parent relationships.

### E. Object-Oriented Database

- Stores data as objects, supporting object-oriented concepts.

### F. Distributed Database

- Data is stored across multiple networked locations.
- The system coordinates access to that distributed data.

**Use case:** Applications operating across regions or data centers.

### G. Centralized Database

- Database is maintained at one central location or system.
- Users or applications access it over a network when required.

### H. Cloud Database

- Database hosted on cloud infrastructure, often with managed services.

**Examples:** Amazon RDS, Google Cloud SQL, Azure SQL Database.

**Important:** These categories can overlap. For example, a relational database can be distributed and cloud-hosted.

---

## 5. Schema vs Instance

### Schema

The schema is the **structure or design of a database**.

It defines tables, columns, data types, relationships and constraints.

Example:

`Student(Student_ID INT, Name VARCHAR(50), Age INT)`

### Instance

An instance is the **actual data stored in the database at a particular moment**.

Example:

| Student_ID | Name | Age |
|---|---|---|
| 101 | Aman | 20 |
| 102 | Riya | 21 |

### Difference

| Schema | Instance |
|---|---|
| Database structure | Current database contents |
| Changes relatively infrequently | Changes frequently |
| Defined using database definition operations | Changes through insert, update and delete operations |
| Similar to a blueprint | Similar to the actual building's current contents |

**Memory trick:** Schema = design; Instance = data at a specific time.

---

## 6. Three-Schema Architecture

The three-schema architecture separates a database into three levels to support abstraction and data independence.

### A. External Level (View Level)

- Highest level.
- Shows only the data needed by a particular user or application.
- Different users can have different views of the same database.

**Example:** A student sees marks and attendance, while an accounts employee sees fee details.

### B. Conceptual Level (Logical Level)

- Describes the overall logical structure of the database.
- Defines entities, attributes, relationships and constraints.
- Hides physical storage details.

**Example:** The college database contains Student, Course, Faculty and Enrollment tables and their relationships.

### C. Internal Level (Physical Level)

- Lowest level.
- Describes how data is physically stored and accessed.
- Includes storage organization, file structures and indexes.

**Example:** How student records are stored on disk and which indexes are used.

### Architecture diagram

```text
Users / Applications
        |
        v
External Level
(User-specific views)
        |
        v
Conceptual Level
(Overall logical structure)
        |
        v
Internal Level
(Physical storage details)
        |
        v
Physical Storage
```

**Memory trick:**

- External = What a user sees.
- Conceptual = What the whole database contains.
- Internal = How the data is stored.

---

## 7. Data Abstraction and Data Independence

### Data Abstraction

Data abstraction means **hiding unnecessary implementation details and showing only the relevant information**.

Example: A banking app displays your account balance without showing how the database stores the account record on disk.

The three levels of abstraction are:

1. **Physical abstraction:** Hides storage details.
2. **Logical abstraction:** Hides the complexity of the complete logical structure from users.
3. **View abstraction:** Shows only the required part of the database.

The view level corresponds to the external level in the three-schema architecture.

### Data Independence

Data independence is the ability to change the schema at one level without requiring changes at the next higher level, subject to the relevant mappings.

There are two types:

#### A. Physical Data Independence

The ability to change the internal or physical schema without changing the conceptual schema or application logic that depends on it.

**Example:** Adding an index or changing the physical file organization without changing the table structure or application queries.

- Generally easier to achieve.
- Deals with physical storage changes.

#### B. Logical Data Independence

The ability to change the conceptual schema without requiring changes to external schemas or application programs, where the relevant views and mappings can be preserved.

**Example:** Adding a new optional attribute to a table without affecting existing user views and applications that do not use that attribute.

- Generally harder to achieve.
- Deals with logical structure changes.

### Physical vs Logical Data Independence

| Physical | Logical |
|---|---|
| Changes the internal schema | Changes the conceptual schema |
| Storage-level changes | Logical structure changes |
| Usually easier | Usually harder |
| Example: Add an index | Example: Add a column without affecting existing views |

**Remember:** Data abstraction hides details; data independence allows certain changes without affecting higher levels.

---

# Quick Revision — One-Minute Summary

- **DBMS:** Software to manage databases.
- **RDBMS:** Relational DBMS that organizes data in tables.
- **File system vs DBMS:** DBMS offers structured querying, constraints, concurrency control and recovery mechanisms.
- **Advantages:** Reduced redundancy, consistency, security, integrity, sharing and recovery.
- **Database types:** Relational, NoSQL, hierarchical, network, object-oriented, distributed, centralized and cloud.
- **Schema:** Database design.
- **Instance:** Data at a particular time.
- **External level:** User-specific view.
- **Conceptual level:** Overall logical structure.
- **Internal level:** Physical storage.
- **Data abstraction:** Hide unnecessary details.
- **Physical independence:** Change storage without changing the logical schema.
- **Logical independence:** Change logical structure without changing external views or applications, where mappings permit.

---

# Important Interview Questions and Answers

## Basic Questions

### Q1. What is a DBMS?

A DBMS is software used to create, store, retrieve, update and manage data in a database. It provides mechanisms for querying, access control, integrity and recovery.

### Q2. What is the difference between DBMS and RDBMS?

A DBMS is the general category of database management systems. An RDBMS follows the relational model, organizing data into tables and supporting relationships and relational constraints.

### Q3. What is the difference between a file system and a DBMS?

A file system stores data in files, while a DBMS manages structured data and provides query processing, constraints, concurrency control and recovery mechanisms.

### Q4. Why do we need a DBMS?

We need a DBMS to manage large amounts of data efficiently, reduce unnecessary duplication, maintain integrity, control access and support multiple users.

### Q5. Can a DBMS completely eliminate data redundancy?

No. It can reduce and control unnecessary redundancy, but some redundancy may be intentional or unavoidable.

### Q6. Name some popular relational databases.

MySQL, PostgreSQL, Oracle Database and Microsoft SQL Server.

### Q7. What is a NoSQL database?

A NoSQL database uses a non-relational data model, such as documents, key-value pairs, wide-column data or graphs. It can be useful for flexible data structures and distributed workloads.

### Q8. What is the difference between SQL and NoSQL databases?

Relational SQL databases organize data into related tables and commonly use SQL. NoSQL databases use models such as documents, key-value pairs and graphs. Their consistency, querying and transaction capabilities depend on the specific system.

## Schema and Architecture Questions

### Q9. What is a database schema?

A schema defines the structure of a database, including tables, columns, data types, relationships and constraints.

### Q10. What is a database instance?

An instance is the actual data stored in the database at a particular moment.

### Q11. Can a schema change?

Yes. A schema can be modified using schema-definition operations, such as adding a column or creating a table.

### Q12. Explain the three-schema architecture.

It has three levels: external for user-specific views, conceptual for the overall logical structure and internal for physical storage.

### Q13. Why do we need three-schema architecture?

It separates user views, logical design and physical storage. This supports abstraction, security through appropriate views and data independence.

### Q14. What is the difference between the conceptual and internal schemas?

The conceptual schema describes what data exists and how it is related. The internal schema describes how that data is stored and accessed physically.

### Q15. Can different users have different external schemas?

Yes. Each user or application can have a view containing only the information it needs.

## Data Abstraction and Independence Questions

### Q16. What is data abstraction?

Data abstraction hides unnecessary details and exposes only the information relevant to a user.

### Q17. What is data independence?

It is the ability to change a schema at one level without requiring changes at the next higher level, provided the mappings and dependencies allow it.

### Q18. What are the two types of data independence?

Physical data independence and logical data independence.

### Q19. Which type of data independence is easier to achieve?

Physical data independence is generally easier because physical storage changes can often be made without changing the logical database structure.

### Q20. Give an example of physical data independence.

Adding an index or changing the physical storage organization without changing the table structure or application queries that use it.

### Q21. Give an example of logical data independence.

Adding a new column to a conceptual schema without affecting existing external views and applications that do not depend on that column.

### Q22. Why is logical data independence harder to achieve?

Logical changes can affect tables, relationships and attributes used by applications and views, so preserving all dependent interfaces can be more difficult.

### Q23. What is the relationship between data abstraction and data independence?

Data abstraction hides implementation details. Data independence allows certain changes at one schema level without affecting higher levels.

## Scenario-Based Questions

### Q24. A company changes its database storage method but keeps the same tables. Which concept is demonstrated?

Physical data independence.

### Q25. A student can see marks but cannot see salary information. Which level is relevant?

The external or view level. Access permissions also help enforce the restriction.

### Q26. A database has the same table structure, but new student records are inserted. What changes?

The instance changes; the schema remains the same.

### Q27. A college stores student information in multiple files, causing conflicting phone numbers. How can a DBMS help?

It can centralize or coordinate the relevant records, reduce unnecessary duplication and apply constraints and update mechanisms to improve consistency.

### Q28. An application adds an index to speed up searches. Should its SQL queries necessarily change?

No. Adding an index is normally a physical-level change and usually does not require query changes.

### Q29. Is a cloud database necessarily a NoSQL database?

No. Cloud describes where or how a database is hosted. Cloud databases can be relational or non-relational.

### Q30. Is every DBMS an RDBMS?

No. An RDBMS is a type of DBMS, but DBMSs can also use document, graph, key-value and other data models.

---

## Final Interview Checklist

Before marking Phase 1 complete, check whether you can explain these without looking at the notes:

- [ ] DBMS vs RDBMS
- [ ] File system vs DBMS
- [ ] Three advantages and three disadvantages of DBMS
- [ ] Relational vs NoSQL databases
- [ ] Schema vs instance
- [ ] External vs conceptual vs internal level
- [ ] Data abstraction vs data independence
- [ ] Physical vs logical data independence
- [ ] Two real-world examples of data independence

**Revision strategy:** Read the seven topics first, close the notes and answer the 30 questions aloud. If you can explain the concepts with examples rather than memorizing exact definitions, Phase 1 is in good shape for entry-level interviews.
