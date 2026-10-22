## 1. OLTP vs OLAP

### OLTP (Online Transaction Processing)
- Used to handle daily database transactions.
- Performs frequent INSERT, UPDATE, and DELETE operations.
- Focuses on fast transaction processing and data consistency.

**Example:** Bank deposits, online payments, and placing orders.

### OLAP (Online Analytical Processing)
- Used to analyze large amounts of data.
- Helps identify trends and make business decisions.
- Commonly performs complex queries and aggregations.

**Example:** Analyzing yearly sales to identify the best-performing products.

### OLTP vs OLAP

| OLTP | OLAP |
|---|---|
| Handles daily transactions. | Handles data analysis. |
| Usually works with current operational data. | Often analyzes historical data. |
| Many short transactions. | Complex analytical queries. |
| Example: Placing an order. | Example: Analyzing yearly sales. |

## 2. SQL vs NoSQL

### SQL Databases
- Store data mainly in structured tables with rows and columns.
- Usually use predefined schemas.
- Use SQL to query and manage data.
- Support relationships between tables.

**Examples:** MySQL, PostgreSQL, Oracle.

### NoSQL Databases
- Support data models such as documents, key-value pairs, and graphs.
- Can support flexible or evolving data structures.
- Often useful for large-scale or application-specific data requirements.
- Query methods depend on the database.

**Examples:** MongoDB, Redis, Cassandra, Neo4j.

### SQL vs NoSQL

| SQL | NoSQL |
|---|---|
| Mainly table-based. | Document, key-value, graph, and other models. |
| Often uses a predefined schema. | Often supports flexible schemas. |
| Relationships commonly use keys and joins. | Relationships depend on the data model. |
| Example: PostgreSQL. | Example: MongoDB. |

**Important:** SQL databases are not always limited to fixed schemas, and NoSQL databases are not always schema-free.

## 3. Relational vs Non-Relational Databases

### Relational Database
- Stores data in tables.
- Tables can be connected using primary and foreign keys.
- Suitable for structured data and relationships.

**Example:** A Student table connected to a Department table using Department_ID.

### Non-Relational Database
- Stores data using models other than traditional relational tables.
- Can represent data as documents, key-value pairs, graphs, or wide-column records.
- Useful when the application's data model benefits from these structures.

**Example:** MongoDB stores data in document-like records.

**Note:** SQL vs NoSQL describes database approaches and technologies, while relational vs non-relational describes the underlying data model. The terms are related but not perfectly interchangeable.

## 4. Types of NoSQL Databases

### A. Document Database
- Stores data as documents, commonly in JSON-like formats.
- Different documents can have different fields.
- Useful for product catalogs, content management, and user profiles.

**Example:** MongoDB.

Example document:

```json
{
  "student_id": 101,
  "name": "Aman",
  "skills": ["Python", "SQL"]
}
```

### B. Key-Value Database
- Stores data as a key and its associated value.
- Retrieves values using their keys.
- Useful for caching, sessions, and quick lookups.

**Example:** Redis.

Example:

```text
"user101" -> "Aman"
```

Here, `user101` is the key and `Aman` is the value.

### C. Graph Database
- Stores data as nodes and relationships (edges).
- Useful when connections between entities are important.
- Common applications include social networks and recommendation systems.

**Example:** Neo4j.

Example:
- Node 1: Aman
- Node 2: Riya
- Relationship: Aman FRIEND_OF Riya

## 5. Database Replication and Sharding

### Replication
- Replication means maintaining copies of data on multiple database servers.
- Helps improve availability and can support disaster recovery.
- Depending on the setup, copies may not be updated at exactly the same time.

**Example:** A secondary server maintains a copy of data from the primary server.

### Sharding
- Sharding means dividing data into smaller parts called shards.
- Each shard stores a portion of the total data.
- Helps distribute storage and workload across servers.

**Example:** Customer records are divided across servers based on Customer_ID.

### Replication vs Sharding

| Replication | Sharding |
|---|---|
| Copies data. | Splits data. |
| Can improve availability. | Can distribute storage and workload. |
| Multiple servers may hold the same records. | Different shards hold different portions of the data. |

## 6. Database Security and Access Control

Database security protects data from unauthorized access, modification, or deletion.

### Authentication
- Verifies the identity of a user.
- Example: Logging in using a username and password.

### Authorization
- Determines what an authenticated user is allowed to do.
- Example: A user can read records but cannot delete them.

### GRANT and REVOKE
- `GRANT` gives database permissions.
- `REVOKE` removes database permissions.

Example:

```sql
GRANT SELECT ON Employee TO analyst;
```

This allows `analyst` to read data from the Employee table, subject to the database's permission rules.

```sql
REVOKE SELECT ON Employee FROM analyst;
```

This removes that SELECT permission.

### Principle of Least Privilege
- Give users only the permissions they need.
- Avoid giving every user full database access.

**Other security practices:**
- Use strong authentication.
- Encrypt sensitive data.
- Audit database activity.
- Take regular backups.
- Protect database credentials.

## 7. Backup and Recovery

### Backup
A backup is a copy of database data that can be used to restore it after data loss or damage.

### Types of Backup

**Full Backup**
- Copies the entire database.

**Incremental Backup**
- Copies changes made since the most recent backup of the relevant type.

**Differential Backup**
- Copies changes made since the most recent full backup.

### Recovery
Recovery means restoring the database to a usable state after a failure.

Examples of failures:
- Hardware failure.
- Accidental deletion.
- Software crash.
- Data corruption.

### Transaction Log
- Records database changes and transaction activity.
- Can help recover committed changes or undo incomplete transactions, depending on the recovery system.

### Backup vs Recovery

| Backup | Recovery |
|---|---|
| Creates a copy of data. | Restores data after a failure. |
| Helps prepare for data loss. | Helps bring the database back to a usable state. |

**Important:** A backup is useful only if it can be restored successfully. Regularly test the recovery process.
