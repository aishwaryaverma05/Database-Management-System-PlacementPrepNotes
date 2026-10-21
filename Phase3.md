# Phase 3: Entity-Relationship (ER) Model

## 1. What is an ER Model?

The **Entity-Relationship (ER) Model** is used to design a database by identifying entities, their attributes, and relationships between them.

**Example:** In a college database, Student and Course are entities, and Enrolls is the relationship between them.

## 2. Entity and Entity Set

- **Entity:** A real-world object that can be identified.
- **Entity Set:** A collection of similar entities.

**Example:**
- One student, Rahul = Entity.
- All students in a college = Entity Set.

## 3. Attributes

An **attribute** is a property that describes an entity.

Example: A Student entity has Student_ID, Name, Age, and Email.

### Types of Attributes

- **Simple:** Cannot be divided further. Example: Age.
- **Composite:** Can be divided into smaller parts. Example: Address → City, State, PIN Code.
- **Single-valued:** Has one value per entity. Example: Date of Birth.
- **Multivalued:** Can have multiple values. Example: Phone Numbers.
- **Derived:** Calculated from another attribute. Example: Age calculated from Date of Birth.
- **Key Attribute:** Uniquely identifies an entity. Example: Student_ID.

**Remember:** A multivalued attribute can have multiple values for one entity, while a composite attribute can be split into smaller attributes.

## 4. Strong Entity vs Weak Entity

### Strong Entity
An entity that has its own primary key and can be identified independently.

Example: Student with Student_ID.

### Weak Entity
An entity that cannot be uniquely identified using its own attributes alone. It depends on an owner entity and usually uses a partial key combined with the owner's key.

Example: A Dependent belonging to an Employee. Dependent_Name alone may not be unique, so Employee_ID + Dependent_Name can identify the dependent if names are unique per employee.

| Strong Entity | Weak Entity |
|---|---|
| Has its own primary key | Depends on an owner entity for identification |
| Can be identified independently | Uses the owner's key with a partial key |
| Example: Employee | Example: Employee's Dependent |

## 5. Relationship and Relationship Set

A **relationship** represents an association between entities.

Example: A Student enrolls in a Course.

- Student and Course are entities.
- Enrolls is the relationship.

A **relationship set** is a collection of similar relationships.

Relationships can also have attributes. For example, an Enrolls relationship may have an Enrollment_Date or Grade.

## 6. Cardinality

Cardinality describes how many entities can be associated with another entity.

### One-to-One (1:1)
One person has one passport, and each passport belongs to one person.

### One-to-Many (1:N)
One department has many employees, but each employee belongs to one department.

### Many-to-Many (M:N)
Many students can enroll in many courses.

**Remember:** In a many-to-many relationship, a junction table is generally used when converting the design into relational tables.

## 7. Participation Constraints

Participation tells us whether every entity must participate in a relationship.

### Total Participation
Every entity must participate in the relationship.

Example: If every employee must belong to a department, each employee must participate in the Works_In relationship.

### Partial Participation
Some entities may not participate in the relationship.

Example: An employee may or may not manage a department.

**Remember:** Total = Mandatory; Partial = Optional.

## 8. ER Diagram Symbols

Common symbols used in a traditional ER diagram:

- **Rectangle:** Entity
- **Double Rectangle:** Weak Entity
- **Oval:** Attribute
- **Underlined Attribute:** Key Attribute
- **Double Oval:** Multivalued Attribute
- **Dashed Oval:** Derived Attribute
- **Diamond:** Relationship
- **Double Diamond:** Identifying relationship for a weak entity
- **Double Line:** Total participation

## 9. Converting an ER Diagram into Tables

Basic rules:

- **Strong entity:** Create a table with its attributes and primary key.
- **Weak entity:** Create a table containing the owner's key and its partial key.
- **One-to-One:** Place a foreign key on one side, usually where it best fits the participation and design requirements.
- **One-to-Many:** Place the foreign key on the many side.
- **Many-to-Many:** Create a junction table containing foreign keys to both entities.
- **Multivalued attribute:** Create a separate table for that attribute and the entity's key.

### Example: Student and Course

A student can enroll in multiple courses, and a course can have multiple students.

**Student table**

| Student_ID (PK) | Name |
|---|---|
| 101 | Rahul |
| 102 | Priya |

**Course table**

| Course_ID (PK) | Course_Name |
|---|---|
| C01 | DBMS |
| C02 | Python |

**Enrollment table**

| Student_ID (FK) | Course_ID (FK) |
|---|---|
| 101 | C01 |
| 101 | C02 |
| 102 | C01 |

Here, `(Student_ID, Course_ID)` can form a composite primary key if duplicate enrollments are not allowed.

---

## Quick Revision: One-Line Answers

1. **What is an ER model?** A database design model based on entities, attributes, and relationships.
2. **What is an entity?** A uniquely identifiable real-world object.
3. **What is an attribute?** A property of an entity.
4. **What is a weak entity?** An entity that depends on an owner entity for identification.
5. **What is a composite attribute?** An attribute that can be divided into smaller attributes.
6. **What is a multivalued attribute?** An attribute that can have multiple values for one entity.
7. **What is a derived attribute?** An attribute calculated from other stored information.
8. **What is cardinality?** It describes how many entities can be associated in a relationship.
9. **What is total participation?** Every entity must participate in the relationship.
10. **How do we represent an M:N relationship in tables?** By creating a junction table.
11. **Where is the foreign key placed in a 1:N relationship?** Usually on the many side.
12. **What is the difference between an entity and an attribute?** An entity is an object; an attribute describes that object.
