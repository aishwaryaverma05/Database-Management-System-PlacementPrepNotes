# Phase 2 — Relational Model and Keys

> **Goal:** Understand relational tables, database keys, and integrity constraints with examples commonly used in technical interviews.

## 1. Tables, Rows, Columns, Attributes, Tuples and Domains

The relational model represents data using relations, which are commonly displayed as tables.

Consider the following `Student` table:

| Student_ID | Name | Age | Dept_ID |
|---|---|---:|---:|
| 101 | Aman | 20 | 10 |
| 102 | Riya | 21 | 20 |
| 103 | Neha | 19 | 10 |

### Important Terminology

- **Relation:** A table in the relational model. Example: `Student`.
- **Tuple:** A single row representing one record. Example: `(101, Aman, 20, 10)`.
- **Attribute:** A named property of a relation. Example: `Student_ID`, `Name`, `Age`.
- **Column:** The vertical representation of an attribute in a table.
- **Domain:** The set of permitted values for an attribute. Example: `Age` may have a domain of positive integers within an application's allowed range.
- **Degree:** Number of attributes (columns) in a relation.
- **Cardinality:** Number of tuples (rows) in a relation.

For the example above:
- Degree = 4
- Cardinality = 3

**Memory trick:**
- Row = Tuple
- Column = Attribute
- Allowed values = Domain
- Number of columns = Degree
- Number of rows = Cardinality

---

## 2. Super Key and Candidate Key

Keys help uniquely identify records in a table.

### Super Key

A super key is any set of one or more attributes that uniquely identifies each row in a table.

Example: Suppose `Student_ID` is unique and `Email` is also unique in the `Student` table.

Possible super keys:
- `{Student_ID}`
- `{Email}`
- `{Student_ID, Name}`
- `{Student_ID, Email}`

All these sets uniquely identify a student.

A super key may contain unnecessary attributes.

### Candidate Key

A candidate key is a **minimal super key**. It uniquely identifies each row, and removing any attribute from it would make it lose that property.

If both `Student_ID` and `Email` are individually unique:

Candidate keys:
- `{Student_ID}`
- `{Email}`

`{Student_ID, Name}` is not a candidate key because `Student_ID` alone is enough.

### Super Key vs Candidate Key

| Super Key | Candidate Key |
|---|---|
| Uniquely identifies a row | Uniquely identifies a row |
| May contain extra attributes | Contains no unnecessary attributes |
| Not necessarily minimal | Always minimal |
| Every candidate key is a super key | Every super key is not necessarily a candidate key |

**Remember:** Candidate key = minimal super key.

---

## 3. Primary Key and Alternate Key

A table can have multiple candidate keys, but one is selected as its primary key.

### Primary Key

A primary key is the candidate key selected to uniquely identify each row in a table.

Properties:
- Must be unique.
- Cannot contain `NULL`.
- Only one primary key constraint can be defined per table.
- That primary key may contain one or multiple columns.

Example:

| Student_ID (PK) | Name |
|---|---|
| 101 | Aman |
| 102 | Riya |

`Student_ID` is the primary key.

### Alternate Key

An alternate key is a candidate key that was not selected as the primary key.

Suppose both `Student_ID` and `Email` are candidate keys. If `Student_ID` is selected as the primary key, `Email` is an alternate key.

### Primary Key vs Alternate Key

| Primary Key | Alternate Key |
|---|---|
| Selected candidate key | Remaining candidate key(s) |
| Uniquely identifies each row | Also uniquely identifies each row |
| Cannot contain NULL | A candidate key cannot contain NULL |
| One primary key constraint per table | A table may have multiple alternate keys |

**Important:** An alternate key is not just any unique column; it must qualify as a candidate key.

---

## 4. Foreign Key

A foreign key is a column or set of columns in one table that references a primary key or another eligible unique key in a referenced table.

It establishes a relationship between tables.

### Example

**Department table**

| Dept_ID (PK) | Dept_Name |
|---|---|
| 10 | CSE |
| 20 | ECE |

**Student table**

| Student_ID (PK) | Name | Dept_ID (FK) |
|---|---|---|
| 101 | Aman | 10 |
| 102 | Riya | 20 |
| 103 | Neha | 10 |

Here:
- `Department.Dept_ID` is the primary key.
- `Student.Dept_ID` is a foreign key referencing `Department.Dept_ID`.

This prevents a student from referencing a department that does not exist, when the foreign key constraint is enforced.

### Important Foreign Key Properties

- A table can have multiple foreign keys.
- Foreign key values may repeat.
- A foreign key may contain `NULL` if the constraint permits it.
- A foreign key does not have to be unique.
- The referenced column(s) must satisfy the database's foreign-key reference requirements, typically a primary key or eligible unique key.

### What happens when referenced data is deleted?

Depending on the foreign key definition, the database may:
- Reject the deletion (`RESTRICT` or `NO ACTION`, depending on the DBMS and constraints).
- Delete related child rows using `ON DELETE CASCADE`.
- Set the child foreign key to `NULL` using `ON DELETE SET NULL`, if permitted.

**Interview tip:** A foreign key maintains referential integrity; it does not automatically make the foreign key column unique.

---

## 5. Composite Key

A composite key is a key formed using two or more attributes together to uniquely identify a row.

### Example: Enrollment table

| Student_ID | Course_ID | Grade |
|---|---|---|
| 101 | C01 | A |
| 101 | C02 | B |
| 102 | C01 | A |

A student can enroll in multiple courses, and a course can contain multiple students.

Neither `Student_ID` nor `Course_ID` alone uniquely identifies an enrollment.

Together, `(Student_ID, Course_ID)` uniquely identify each enrollment, assuming a student can enroll in a course only once.

Therefore, they form a composite key.

### Key points

- Contains two or more attributes.
- Uniqueness comes from the combination.
- May be a composite primary key or another composite candidate key.
- A composite key is not necessarily a super key with unnecessary columns; it can be minimal.

**Memory trick:** Composite = combination.

---

## 6. Natural Key vs Surrogate Key

### Natural Key

A natural key uses an attribute that already has real-world meaning and can uniquely identify a record.

Examples:
- A person's government-issued identifier, where legally appropriate.
- An ISBN for a book edition.
- A business's registered identifier.

Advantages:
- Has real-world meaning.
- May avoid introducing an additional identifier.

Disadvantages:
- Real-world values may change.
- Values may be long or sensitive.
- Uniqueness and validity depend on the chosen attribute and business rules.

### Surrogate Key

A surrogate key is an artificially generated identifier that has no meaningful business information of its own.

Examples:
- Auto-incrementing `Student_ID`.
- A generated UUID such as `550e8400-e29b-41d4-a716-446655440000`.

Advantages:
- Usually stable when business details change.
- Can be compact and convenient for relationships.
- Does not expose meaningful personal information by itself.

Disadvantages:
- Requires a generated identifier.
- Does not automatically enforce real-world uniqueness. For example, two records may still have the same email unless an appropriate constraint is added.

### Natural vs Surrogate Key

| Natural Key | Surrogate Key |
|---|---|
| Comes from meaningful real-world data | Artificially generated |
| Example: ISBN | Example: generated Book_ID |
| May change when real-world data changes | Usually designed to remain stable |
| Can expose sensitive or business information | Often avoids exposing business meaning |
| Can be long or complex | Often simple and compact |

**Important:** A surrogate key does not remove the need for unique constraints on important business attributes.

---

## 7. Entity Integrity and Referential Integrity

Integrity constraints help keep database data valid and consistent.

### A. Entity Integrity

Entity integrity means that every row can be uniquely identified by its primary key.

Rules:
- A primary key must be unique.
- A primary key cannot contain `NULL`.

Example:

| Student_ID (PK) | Name |
|---|---|
| 101 | Aman |
| 102 | Riya |

Invalid cases:
- Two rows with `Student_ID = 101`.
- A row with `Student_ID = NULL`.

These violate primary key requirements.

### B. Referential Integrity

Referential integrity ensures that a foreign key refers to a valid record in the referenced table, or has a permitted `NULL` value.

Example:

Department table:

| Dept_ID (PK) |
|---|
| 10 |
| 20 |

Student table:

| Student_ID | Dept_ID (FK) |
|---|---|
| 101 | 10 |
| 102 | 20 |

A student with `Dept_ID = 30` would violate referential integrity if department 30 does not exist and the foreign key constraint is enforced.

### Entity vs Referential Integrity

| Entity Integrity | Referential Integrity |
|---|---|
| Applies to primary keys | Applies to foreign keys |
| Prevents duplicate or NULL primary key values | Prevents invalid foreign key references |
| Identifies each row | Maintains valid relationships between tables |

**Memory trick:**
- Entity integrity = Every row has a valid identity.
- Referential integrity = Every reference points to a valid record, or is NULL when allowed.

---

# Quick Revision — All Keys at a Glance

| Key | Meaning |
|---|---|
| Super Key | Any attribute set that uniquely identifies a row |
| Candidate Key | Minimal super key |
| Primary Key | Candidate key selected as the main identifier |
| Alternate Key | Candidate key not selected as the primary key |
| Foreign Key | Attribute set referencing an eligible key in another or the same table |
| Composite Key | Key formed from two or more attributes |
| Natural Key | Key derived from meaningful real-world data |
| Surrogate Key | Artificially generated identifier |

**Important relationships:**
- Every candidate key is a super key.
- One candidate key is selected as the primary key.
- Other candidate keys become alternate keys.
- A composite key can be a candidate key or a primary key.
- A natural or surrogate key can serve as a primary key.
- A foreign key may reference a primary key or another eligible unique key.

---

# Important Interview Questions and Answers

## Basic Concepts

### Q1. What is the relational model?

The relational model organizes data into relations (tables) consisting of rows and columns, with keys and constraints used to identify records and maintain relationships.

### Q2. What is a tuple?

A tuple is a single row or record in a relation.

### Q3. What is an attribute?

An attribute is a named property of a relation, usually represented as a column.

### Q4. What is a domain?

A domain is the set of permitted values for an attribute, such as valid age values or allowed gender codes.

### Q5. What is the difference between degree and cardinality?

Degree is the number of attributes (columns) in a relation. Cardinality is the number of tuples (rows).

## Keys

### Q6. What is a super key?

A super key is any set of attributes that uniquely identifies every row in a table.

### Q7. What is a candidate key?

A candidate key is a minimal super key: it uniquely identifies each row, and no attribute can be removed without losing uniqueness.

### Q8. What is the difference between a super key and a candidate key?

A super key may contain extra attributes, while a candidate key is minimal.

### Q9. Can a table have multiple candidate keys?

Yes. For example, both `Student_ID` and `Email` can be candidate keys if each is unique and non-NULL.

### Q10. How many primary keys can a table have?

A table can have only one primary key constraint, although that primary key may consist of multiple columns.

### Q11. What is an alternate key?

An alternate key is a candidate key that was not chosen as the primary key.

### Q12. Can a primary key contain NULL?

No. A primary key cannot contain NULL values.

### Q13. What is a foreign key?

A foreign key is a column or group of columns that references an eligible key in a referenced table and helps enforce referential integrity.

### Q14. Can a foreign key contain duplicate values?

Yes. Multiple students may belong to the same department, so their `Dept_ID` foreign key values can repeat.

### Q15. Can a foreign key contain NULL?

Yes, if NULL is permitted by the foreign key column's constraints. A NULL foreign key does not identify a referenced row.

### Q16. Can a table have multiple foreign keys?

Yes. For example, an `Orders` table may reference both `Customers` and `Products`.

### Q17. What is a composite key?

A composite key uses two or more attributes together to uniquely identify a row.

### Q18. Is a composite key always a primary key?

No. It can be a candidate key or another key. It becomes the primary key only when selected as the primary key.

### Q19. What is the difference between a natural key and a surrogate key?

A natural key comes from meaningful real-world data, whereas a surrogate key is artificially generated, such as an auto-incrementing ID.

### Q20. Does a surrogate key guarantee that business data is unique?

No. Separate UNIQUE constraints may be needed for attributes such as email or registration number.

## Integrity Constraints

### Q21. What is entity integrity?

Entity integrity requires primary key values to be unique and non-NULL, ensuring that each row has a valid identity.

### Q22. What is referential integrity?

Referential integrity ensures that a foreign key refers to a valid referenced key, or contains NULL where allowed.

### Q23. What is the difference between entity integrity and referential integrity?

Entity integrity concerns primary keys and row identity. Referential integrity concerns foreign keys and valid relationships between records.

### Q24. What happens if you insert a foreign key value that does not exist in the parent table?

If the foreign key constraint is enforced, the database rejects the insert or update because the reference is invalid.

### Q25. What happens when a parent row is deleted while child rows reference it?

The result depends on the foreign key's delete action: the database may reject the deletion, cascade it to child rows, or set child foreign keys to NULL if permitted.

## Scenario-Based Questions

### Q26. If `Student_ID` and `Email` are both unique, but `Student_ID` is selected as the primary key, what is `Email`?

An alternate key, assuming both are valid candidate keys.

### Q27. Is `(Student_ID, Name)` a candidate key if `Student_ID` is already unique?

No. It is a super key but not a candidate key because `Name` is unnecessary for uniqueness.

### Q28. Why might an enrollment table use `(Student_ID, Course_ID)` as a composite primary key?

Because each student can enroll in multiple courses and each course can have multiple students, while the pair uniquely identifies one enrollment.

### Q29. A student row has `Dept_ID = 50`, but department 50 does not exist. Which constraint is violated?

Referential integrity, assuming `Dept_ID` is an enforced foreign key and no permitted NULL or other exception applies.

### Q30. A table contains two rows with the same primary key. Which integrity rule is violated?

Entity integrity, specifically the uniqueness requirement of the primary key.

---

# Final Interview Checklist

Before marking Phase 2 complete, make sure you can explain these without looking at the notes:

- [ ] Relation, tuple, attribute, domain, degree and cardinality
- [ ] Super key vs candidate key
- [ ] Primary key vs alternate key
- [ ] Foreign key and its NULL/duplicate behavior
- [ ] Composite key with an enrollment example
- [ ] Natural key vs surrogate key
- [ ] Entity integrity vs referential integrity
- [ ] What happens when a referenced parent row is deleted
- [ ] Identify candidate keys from a sample table

**Revision strategy:** Focus especially on the differences between super and candidate keys, primary and foreign keys, and entity and referential integrity. These distinctions are easy to mix up when answering quickly in interviews.
