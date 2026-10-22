# Phase 8: Indexing and Query Performance

## 1. What is an Index?

An **index** is a data structure that helps the database find records faster without scanning the entire table in many cases.

**Example:** A book's index helps you find a topic without reading every page.

Suppose a Student table has 1 lakh records. Finding a student by Student_ID may require checking many rows without a suitable index. An index can help locate the record faster.

## 2. Why Do We Need Indexes?

- Speed up searching and filtering.
- Improve performance of suitable queries.
- Help with some JOIN and sorting operations.

**Disadvantage:** Indexes need extra storage and can slow down INSERT, UPDATE, and DELETE operations because the indexes may also need updating.

## 3. Clustered vs Non-Clustered Index

### Clustered Index
Organizes table data according to the index's key order in systems that support clustered storage.

### Non-Clustered Index
Stores index entries separately from the table's main data, with references to the corresponding rows.

| Clustered Index | Non-Clustered Index |
|---|---|
| Organizes the table's data by the index key | Stores a separate index structure |
| Determines the data's organization in supported systems | Points to the corresponding data rows |
| A table generally has one clustering order | A table can have multiple non-clustered indexes |

**Note:** Exact behavior depends on the DBMS. For example, MySQL InnoDB organizes table data by its primary key, while other systems use different implementations.

## 4. Primary vs Secondary Index

- **Primary index:** In the traditional DBMS classification, an index built on the primary ordering key of a data file.
- **Secondary index:** An additional index that provides another way to access records.

**Important:** In real DBMS products, the term *primary index* can have a different meaning. Do not assume it always means a clustered index.

## 5. Composite Index

A composite index uses **two or more columns**.

Example:

```sql
CREATE INDEX idx_dept_salary
ON Employee (Department_ID, Salary);
```

This index can help queries that filter by `Department_ID`, or by `Department_ID` together with `Salary`.

**Important:** Column order matters. An index on `(Department_ID, Salary)` generally does not work as efficiently for a query filtering only on `Salary`.

## 6. B-Tree vs B+ Tree

Both are balanced tree structures used to search data efficiently.

- **B-Tree:** Keys and associated records or pointers may be stored in internal and leaf nodes.
- **B+ Tree:** Internal nodes guide the search, while data entries are stored at leaf level; leaf nodes are commonly linked for efficient range scans.

**Remember:** B+ Trees are widely used for database indexes because they support efficient searches and range queries.

## 7. Full Table Scan vs Index Scan

### Full Table Scan
The database examines the table's rows to find matching records.

### Index Scan
The database uses an index to locate relevant records.

**Example:** If you need only 10 students from a table containing 1 lakh students, a suitable index may be faster.

However, if you need most of the table's rows, a full table scan may be more efficient.

## 8. When May an Index Not Help?

- When a query returns a large portion of the table.
- When the indexed column has low selectivity for the query.
- When a function or expression prevents the database from using a regular index efficiently.
- When the table is very small.
- When the query filters on a column that is not well supported by the index's column order.

**Example:** An index on `(Department_ID, Salary)` may not be ideal for a query filtering only on `Salary`.

## 9. Basic Query Optimization

Query optimization means choosing an efficient way to execute an SQL query.

The database optimizer considers factors such as indexes, available statistics, join order, and estimated costs.

Example:

```sql
SELECT *
FROM Employee
WHERE Employee_ID = 101;
```

If `Employee_ID` has a suitable index, the optimizer may use it instead of scanning the entire table.

### EXPLAIN

`EXPLAIN` shows the execution plan selected or estimated by the database.

```sql
EXPLAIN
SELECT *
FROM Employee
WHERE Employee_ID = 101;
```

It can help you understand whether the database uses an index, scans the table, or chooses a particular join strategy.

---

## Quick Revision: One-Line Answers

1. **What is an index?** A data structure that helps retrieve records efficiently.
2. **Why do we use indexes?** To speed up suitable searches and queries.
3. **What is the disadvantage of indexing?** Extra storage and slower writes.
4. **What is a composite index?** An index created on multiple columns.
5. **Why does column order matter?** The leading columns determine which queries can benefit efficiently.
6. **What is a full table scan?** Examining table rows to find matching records.
7. **What is an index scan?** Using an index to locate relevant records.
8. **What is a B+ Tree?** A balanced tree structure commonly used for database indexes.
9. **What is query optimization?** Choosing an efficient way to execute a query.
10. **What does EXPLAIN do?** Shows the query execution plan or its estimated strategy.
