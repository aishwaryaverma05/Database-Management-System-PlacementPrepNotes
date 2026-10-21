# Phase 2: Relational Model and Keys

## 1. Relational Model

The relational model stores data in the form of **tables (relations)**.

Example: Student table

| Student_ID | Name | Marks |
|---|---|---:|
| 101 | Rahul | 85 |
| 102 | Priya | 90 |
| 103 | Aman | 78 |

### Important Terms

- **Table (Relation):** Collection of related data.
- **Row (Tuple):** One complete record in a table.
- **Column (Attribute):** A property of the data, such as Name or Marks.
- **Domain:** The set of valid values allowed for an attribute.

Example: Marks may have a domain of integers from 0 to 100, depending on the database rules.

**Remember:** Row = Record, Column = Attribute.

## 2. Super Key

A **Super Key** is any column or combination of columns that uniquely identifies each row in a table.

Example: Student table has `Student_ID`, `Email`, and `Name`.

If `Student_ID` is unique:
- `{Student_ID}` is a super key.
- `{Student_ID, Name}` is also a super key.
- `{Student_ID, Email}` is also a super key.

**Important:** A super key may contain extra, unnecessary columns.

## 3. Candidate Key

A **Candidate Key** is a minimal super key. It uniquely identifies a row and has no unnecessary attributes.

Example:
- `Student_ID` is unique.
- `Email` is also unique.

Both can be candidate keys if each uniquely identifies a student.

**Remember:** Every candidate key is a super key, but every super key is not a candidate key.

## 4. Primary Key

A **Primary Key** is the candidate key selected to uniquely identify each row.

Example: `Student_ID` is selected as the primary key.

### Properties
- Must be unique.
- Cannot contain NULL values.
- Only one primary key constraint can be defined per table.
- It can contain multiple columns.

## 5. Foreign Key

A **Foreign Key** is a column or set of columns that references a primary key or another eligible unique key in another or the same table.

Example:

**Department table**

| Dept_ID | Dept_Name |
|---|---|
| 1 | CSE |
| 2 | ECE |

**Student table**

| Student_ID | Name | Dept_ID |
|---|---|---|
| 101 | Rahul | 1 |
| 102 | Priya | 2 |

Here, `Dept_ID` in Student references `Dept_ID` in Department.

### Why use a Foreign Key?
- Connects related tables.
- Prevents invalid references.
- Maintains referential integrity.

**Remember:** Primary Key identifies a row; Foreign Key connects related data.

## 6. Alternate Key

An **Alternate Key** is a candidate key that was not selected as the primary key.

Example:
- `Student_ID` and `Email` are candidate keys.
- `Student_ID` is selected as the primary key.
- `Email` becomes an alternate key.

## 7. Composite Key

A **Composite Key** is a key made up of two or more columns.

Example: Enrollment table

| Student_ID | Course_ID | Grade |
|---|---|---|
| 101 | C01 | A |
| 101 | C02 | B |
| 102 | C01 | A |

Here, the combination `(Student_ID, Course_ID)` uniquely identifies an enrollment record, assuming a student can enroll in a course only once.

Neither column alone uniquely identifies every row.

**Remember:** Composite Key = Combination of columns.

## 8. Primary Key vs UNIQUE

| Primary Key | UNIQUE Constraint |
|---|---|
| Uniquely identifies each row | Prevents duplicate values |
| Cannot contain NULL | NULL handling depends on the DBMS |
| One primary key constraint per table | Multiple UNIQUE constraints can exist |
| Can be composite | Can also be composite |

**Example:** `Student_ID` can be the primary key, while `Email` has a UNIQUE constraint.

## 9. Natural Key vs Surrogate Key

### Natural Key
A key that has real-world meaning.

Example: Email address, if it is guaranteed to be unique and suitable for identification.

### Surrogate Key
An artificially generated identifier with no business meaning.

Example: An auto-generated `Student_ID` such as 101, 102, 103.

| Natural Key | Surrogate Key |
|---|---|
| Has real-world meaning | Created for identification |
| May change if real-world data changes | Usually remains stable |
| Example: Email | Example: Generated Student_ID |

## 10. Entity Integrity

Entity integrity means **every row must have a valid primary key**.

A primary key cannot be NULL or duplicated.

Example: Two students cannot have the same `Student_ID`.

## 11. Referential Integrity

Referential integrity ensures that a foreign key refers to an existing row in the referenced table, or is NULL if the relationship permits it.

Example: A student cannot use `Dept_ID = 5` if no such department exists and the foreign key requires a valid reference.

This prevents invalid relationships between tables.

---

## Quick Revision: One-Line Answers

1. **What is a relational model?** A way of organizing data in tables.
2. **What is a tuple?** A row in a table.
3. **What is an attribute?** A column in a table.
4. **What is a super key?** Any set of columns that uniquely identifies a row.
5. **What is a candidate key?** A minimal super key.
6. **What is a primary key?** The candidate key selected to identify rows.
7. **What is a foreign key?** A key that references a key in another or the same table.
8. **What is an alternate key?** A candidate key not selected as the primary key.
9. **What is a composite key?** A key consisting of multiple columns.
10. **What is entity integrity?** A primary key must be unique and non-NULL.
11. **What is referential integrity?** Foreign key references must remain valid.
12. **Can a table have multiple primary keys?** No, but one primary key can contain multiple columns.
13. **Can a table have multiple candidate keys?** Yes.
14. **Can a foreign key contain NULL?** Yes, if the column permits NULL.
15. **Can a foreign key contain duplicate values?** Yes, unless additional constraints prevent them.
