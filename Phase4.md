# Phase 6: Functional Dependencies and Normalization

## 1. Functional Dependency (FD)

A functional dependency means one attribute determines another attribute.

It is written as `A → B`, meaning if we know A, we can determine B uniquely.

**Example:**

`Student_ID → Student_Name`

If every student has a unique Student_ID, knowing the ID tells us the student's name.

**Remember:** The value of A must uniquely determine the value of B.

## 2. Database Anomalies

Poorly designed tables can cause three problems.

### Insertion Anomaly
We cannot insert some information without inserting unrelated information.

Example: We cannot add a new course until at least one student enrolls in it.

### Update Anomaly
The same information is stored in multiple rows, so we must update it everywhere.

Example: If a department name appears in 100 rows, changing it requires updating all 100 rows.

### Deletion Anomaly
Deleting one record accidentally removes other useful information.

Example: Deleting the last student enrolled in a course also removes the only record of that course.

**Solution:** Normalization helps reduce these anomalies.

## 3. What is Normalization?

Normalization is the process of organizing database tables to reduce unnecessary data duplication and prevent insertion, update, and deletion anomalies.

It usually involves dividing a large table into smaller related tables.

## 4. First Normal Form (1NF)

A table is in **1NF** when each cell contains a single value and there are no repeating groups.

**Not in 1NF:**

| Student_ID | Name | Phone |
|---|---|---|
| 101 | Rahul | 9876, 8765 |
| 102 | Priya | 7654 |

The Phone column contains multiple values in one cell.

**In 1NF:**

| Student_ID | Name | Phone |
|---|---|---|
| 101 | Rahul | 9876 |
| 101 | Rahul | 8765 |
| 102 | Priya | 7654 |

**Remember:** One cell = One value.

## 5. Second Normal Form (2NF)

A table is in **2NF** when:
- It is already in 1NF.
- Every non-key attribute depends on the whole candidate key, not just part of a composite candidate key.

This removes **partial dependency**.

**Example:**

Consider an Enrollment table:

| Student_ID | Course_ID | Student_Name | Course_Name |
|---|---|---|---|
| 101 | C01 | Rahul | DBMS |
| 101 | C02 | Rahul | Python |
| 102 | C01 | Priya | DBMS |

Assume `(Student_ID, Course_ID)` is the composite key.

- `Student_ID → Student_Name`
- `Course_ID → Course_Name`

Student_Name depends only on Student_ID, and Course_Name depends only on Course_ID. Neither depends on the entire composite key.

**Solution:** Split the table into:

- Student(`Student_ID`, `Student_Name`)
- Course(`Course_ID`, `Course_Name`)
- Enrollment(`Student_ID`, `Course_ID`)

**Remember:** 2NF = 1NF + No partial dependency.

## 6. Third Normal Form (3NF)

A table is in **3NF** when:
- It is already in 2NF.
- There is no transitive dependency of a non-key attribute on a candidate key.

In simple words, non-key attributes should not depend on other non-key attributes in a way that violates 3NF.

**Example:**

| Student_ID | Student_Name | Dept_ID | Dept_Name |
|---|---|---|---|
| 101 | Rahul | D01 | CSE |
| 102 | Priya | D02 | ECE |

Dependencies:

- `Student_ID → Dept_ID`
- `Dept_ID → Dept_Name`

Therefore, `Student_ID → Dept_Name` indirectly through Dept_ID.

**Solution:** Split into:

- Student(`Student_ID`, `Student_Name`, `Dept_ID`)
- Department(`Dept_ID`, `Dept_Name`)

**Remember:** 3NF removes transitive dependency when it violates the normal form.

## 7. BCNF (Boyce-Codd Normal Form)

BCNF is a stronger version of 3NF.

A table is in **BCNF** if, for every non-trivial functional dependency `X → Y`, X is a super key.

**Simple meaning:** Whenever one attribute or set of attributes determines another, the determining side must be a super key.

**Remember:**
- 1NF: Atomic values.
- 2NF: No partial dependency.
- 3NF: No violating transitive dependency.
- BCNF: Every determinant in a non-trivial functional dependency is a super key.

## 8. Quick Comparison

| Normal Form | Main Requirement |
|---|---|
| 1NF | Each cell contains a single value |
| 2NF | 1NF + no partial dependency |
| 3NF | 2NF + no violating transitive dependency |
| BCNF | Every determinant of a non-trivial FD is a super key |

Each higher normal form builds on the requirements of the previous forms.

---

## Quick Revision: One-Line Answers

1. **What is functional dependency?** A relationship where one attribute or set of attributes determines another.
2. **What is normalization?** Organizing tables to reduce duplication and anomalies.
3. **What is an insertion anomaly?** Difficulty inserting data without unrelated data.
4. **What is an update anomaly?** The same information must be updated in multiple places.
5. **What is a deletion anomaly?** Deleting one record unintentionally removes other useful information.
6. **What is 1NF?** Every cell contains a single value.
7. **What is 2NF?** 1NF with no partial dependency of non-prime attributes on candidate keys.
8. **What is 3NF?** 2NF with no transitive dependency that violates 3NF.
9. **What is BCNF?** Every determinant in a non-trivial functional dependency is a super key.
10. **Why do we normalize tables?** To reduce duplication and prevent data anomalies.
