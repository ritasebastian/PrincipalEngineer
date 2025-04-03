

## 📚 Definitions

### 🔹 What is **SQL**?

**SQL (Structured Query Language)** is used with **relational databases** (RDBMS).  
It follows a strict **schema** with **tables, rows, and columns**.

✅ Used when:
- Data is structured
- You need transactions (ACID)
- Complex relationships (joins) are needed

🛠 Examples: **PostgreSQL, MySQL, Oracle, SQL Server**

---

### 🔹 What is **NoSQL**?

**NoSQL (Not Only SQL)** is a type of database that stores data in **non-relational formats** like documents, key-value pairs, or graphs.

✅ Used when:
- Schema is flexible or dynamic
- High scalability is needed
- Storing unstructured/semi-structured data

🛠 Examples: **MongoDB (Document), Redis (Key-Value), Cassandra (Wide Column)**

---

## 🔁 PostgreSQL vs MongoDB (SQL vs NoSQL)

| Feature                  | **PostgreSQL** (SQL)                          | **MongoDB** (NoSQL)                          |
|--------------------------|-----------------------------------------------|----------------------------------------------|
| **Data Model**           | Tables (rows/columns)                         | JSON-like Documents (BSON)                   |
| **Schema**               | Fixed schema (enforced)                       | Flexible schema (schema-less)                |
| **Query Language**       | SQL                                           | MQL (Mongo Query Language) – JSON syntax     |
| **Joins**                | ✅ Supports complex joins                      | ❌ No traditional joins (but `$lookup` exists) |
| **ACID Transactions**    | ✅ Fully supported                             | ✅ Single & multi-doc (since v4.0)            |
| **Indexing**             | ✅ Rich indexing (B-tree, GiST, GIN)          | ✅ Rich indexing (single, compound, text)     |
| **Performance**          | Great for relational, normalized data         | Great for fast reads/writes, denormalized    |
| **Use Case**             | Banking, ERP, CRM, analytics                  | IoT, catalogs, mobile apps, CMS, logs        |
| **Storage Format**       | Row-based                                     | Binary JSON (BSON)                           |
| **Replication**          | Streaming Replication                         | Replica Sets + Sharding                      |
| **Horizontal Scaling**   | Harder, needs partitioning                    | Built-in sharding                            |
| **Popularity**           | Enterprise-grade RDBMS                        | Top NoSQL document DB                        |

---

## 🧠 Interview Cheat Sheet – SQL vs NoSQL

### 🔹 When to Use SQL (PostgreSQL, MySQL)
- Data is **relational**
- You need **ACID** and **JOINs**
- Schema is **structured and stable**
- Example: Financial systems, analytics, HR databases

### 🔹 When to Use NoSQL (MongoDB, etc.)
- Schema is **flexible/dynamic**
- Horizontal scalability is needed
- You want **high write throughput**
- Example: IoT, mobile apps, product catalogs

---

## 🔥 Sample Interview Q&A

### ✅ Q1: What is the difference between SQL and NoSQL databases?

**A**:  
SQL databases are relational, use structured schemas, and support SQL for queries. NoSQL databases are non-relational, allow flexible schemas, and use various data models like documents or key-value pairs. SQL is ideal for structured data and ACID needs. NoSQL is preferred for scalability and unstructured data.

---

### ✅ Q2: When would you choose PostgreSQL over MongoDB?

**A**:  
If I need complex queries, joins, strong data integrity, or structured reporting – I choose PostgreSQL. For rapid development, flexible data models, and high write volume (e.g., logs or user-generated content), MongoDB is a better fit.

---

### ✅ Q3: Does MongoDB support ACID transactions?

**A**:  
Yes, MongoDB supports multi-document ACID transactions since version 4.0 for replica sets and version 4.2 for sharded clusters.

---

### ✅ Q4: How does data modeling differ between SQL and NoSQL?

**A**:  
In SQL, data is normalized and split into related tables with foreign keys. In NoSQL (like MongoDB), data is usually denormalized, often embedded in a single document to reduce the need for joins and increase read performance.

---
