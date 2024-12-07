# Indexing

## Why Indexing is Used in Databases

**Indexing** is a technique used in databases to speed up the retrieval of records, ensuring faster query processing and enhancing overall system performance. It works similarly to an index in a book: instead of scanning through all the pages to find specific information, you can go straight to the page number listed in the index. In databases, an index helps to quickly locate and access data without scanning the entire table.

Here are the key reasons why indexing is used:

#### 1. **Faster Query Processing**:

- **Speeding up search operations**: Indexing reduces the amount of data the database needs to scan when processing queries. Instead of going through every record in a table, the database can use the index to directly locate the rows that match the query's conditions.
- **Improved performance for SELECT queries**: Especially in large databases, queries that would normally require scanning thousands or millions of rows can be completed in a fraction of the time with an index.

#### 2. **Efficient Sorting**:

- **ORDER BY operations**: Indexes can be used to optimize sorting operations. If an index is created on a column that is frequently used in `ORDER BY` clauses, the database can use the index to return the sorted results directly, without having to sort the data after retrieval.

#### 3. **Faster Joins**:

- **Optimizing joins**: When performing joins between tables, especially for large tables, indexes on the join columns can greatly speed up the process of matching rows between tables.
- **Reduction in table scans**: Without indexing, a join would require scanning each table and comparing every row, which is inefficient. Indexes reduce this overhead by quickly identifying matching rows.

#### 4. **Improved Aggregate Operations**:

- **Efficient grouping and aggregation**: Indexes can help optimize operations like `GROUP BY` or `COUNT()`, as the database can efficiently locate the necessary data for grouping without scanning the entire table.

#### 5. **Faster Updates, Deletions, and Insertions**:

- While indexing speeds up retrieval operations, it also helps maintain the integrity and organization of the database when rows are inserted, updated, or deleted. The index helps the database quickly find rows that need to be updated or deleted.

#### 6. **Enhanced Uniqueness and Integrity Constraints**:

- **Primary Keys and Unique Constraints**: Indexing enforces constraints like `PRIMARY KEY` and `UNIQUE`. When a column is indexed as a unique key, it ensures that no duplicate values are inserted, maintaining data integrity.

#### 7. **Optimized Search with Multiple Columns**:

- **Composite indexes**: Indexing allows the creation of **composite indexes** that involve more than one column, optimizing queries that filter or sort data based on multiple attributes.

---

### **Indexing Beginning: How Indexes Are Created**

In most relational database management systems (RDBMS), an index is created on a column (or set of columns) of a table to facilitate faster data retrieval. Here’s an overview of how indexing begins:

#### 1. **Basic Index Creation**:

- Indexes are typically created using the `CREATE INDEX` SQL command.
- Example SQL to create an index:
  ```sql
  CREATE INDEX idx_customer_name ON customers (customer_name);
  ```
  In this case, an index is created on the `customer_name` column of the `customers` table. The index allows faster searching for customer records by name.

#### 2. **Types of Indexes**:

- **Single-column index**: An index created on a single column (as shown in the above example).
- **Composite index**: An index created on multiple columns to optimize queries involving several columns in the WHERE clause.
  ```sql
  CREATE INDEX idx_customer_name_email ON customers (customer_name, email);
  ```

#### 3. **B-tree Index**:

- The most common type of index, especially in relational databases, is the **B-tree (Balanced Tree)** index.
- In a B-tree, the data is organized in a hierarchical structure, allowing for efficient searching, insertion, and deletion. The search operation in a B-tree index is similar to binary search, making it very fast.

#### 4. **Hash Index**:

- A **hash index** uses a hash function to map search keys to their corresponding data rows.
- It is efficient for equality searches (`=`), but not suitable for range queries (e.g., `BETWEEN`).

#### 5. **Bitmap Index**:

- Bitmap indexes are particularly efficient for columns with a low cardinality (i.e., a small number of distinct values).
- These indexes use bitmaps (bit arrays) to represent the presence or absence of values, making them efficient for certain types of queries.

#### 6. **Clustered vs. Non-clustered Indexes**:

- **Clustered index**: The data rows in the table are sorted and stored in the order of the index. A table can have only one clustered index because the data can be physically sorted in only one way.
- **Non-clustered index**: The index structure is separate from the data rows. Multiple non-clustered indexes can be created on a table, and they point to the data rows based on the indexed values.

#### 7. **Index Maintenance**:

- As records are inserted, updated, or deleted, indexes must be maintained. The database system automatically updates the index when changes occur to the underlying data.

#### 8. **Choosing Which Columns to Index**:

- Not every column should be indexed, as creating indexes introduces overhead for storage and maintenance.
- Columns frequently used in `WHERE` clauses, `JOIN` conditions, `ORDER BY`, and `GROUP BY` clauses are prime candidates for indexing.
- Columns with a high cardinality (many distinct values) are usually better candidates for indexing than those with low cardinality.

---

### **Conclusion**

**Indexing** plays a crucial role in optimizing the performance of a database by speeding up data retrieval, improving query efficiency, and ensuring faster sorting and searching. It works by creating a separate data structure that allows the database system to quickly locate the desired data. However, while indexes improve **read operations**, they do introduce overhead on **write operations** (insert, update, and delete) since the indexes must be maintained. Therefore, creating and managing indexes requires careful consideration of the database workload and query patterns.

## Types of Indexes in Databases

Indexes are crucial for optimizing query performance by enabling faster search, retrieval, and sorting of data. Various types of indexes are used based on specific needs, data types, and query patterns. Below are the most common types of indexes:

---

### 1. **B-tree Index (Balanced Tree Index)**

- **Most Common Type**: B-tree indexes are the most commonly used indexes in relational databases.
- **Structure**: This index organizes data in a tree structure, where each node has pointers to child nodes or data records, keeping the data sorted.
- **Operations**:
  - Search operations work similarly to binary search, allowing for efficient search, insertion, and deletion operations.
  - B-tree indexes are ideal for **range queries** (e.g., `<`, `<=`, `>`, `>=`) and **exact match** queries (e.g., `=`).
- **Example**: Creating a B-tree index on a column:
  ```sql
  CREATE INDEX idx_customer_name ON customers (customer_name);
  ```

---

### 2. **Clustered Index**

- **Physical Data Order**: A clustered index determines the physical order of data rows in the table. When a table has a clustered index, the rows are stored in the order of the indexed column(s).
- **Single Clustered Index**: A table can only have one clustered index because the data rows can only be sorted in one way.
- **Performance**: Ideal for queries that access data in sequential order (e.g., range queries).
- **Example**: Creating a clustered index on a primary key:
  ```sql
  CREATE CLUSTERED INDEX idx_pk ON employees (employee_id);
  ```

---

### 3. **Non-clustered Index**

- **Separate Storage**: A non-clustered index is stored separately from the actual table data. It contains pointers (references) to the actual data rows, which are stored in a different location.
- **Multiple Indexes**: A table can have multiple non-clustered indexes on different columns.
- **Ideal for**: Efficient for queries that frequently use columns in the `WHERE` clause or are involved in sorting (`ORDER BY`) or joining (`JOIN`).
- **Example**:
  ```sql
  CREATE NONCLUSTERED INDEX idx_name ON customers (last_name, first_name);
  ```

---

### 4. **Composite Index (Multi-column Index)**

- **Multiple Columns**: A composite index is created on multiple columns in a table. It helps optimize queries that filter on more than one column.
- **Performance**: This type of index is particularly useful for queries that involve conditions on multiple columns.
- **Limitations**: The order of columns in the index matters. Queries must use the columns in the same order as they appear in the index to benefit from it.
- **Example**:
  ```sql
  CREATE INDEX idx_name_dob ON employees (last_name, date_of_birth);
  ```

---

### 5. **Bitmap Index**

- **Efficient for Low Cardinality**: Bitmap indexes are useful when a column has low cardinality (few distinct values, e.g., gender, status flags).
- **Structure**: It uses bitmaps (bit arrays) for each distinct value of a column. Each bitmap corresponds to a value, and each bit in the bitmap represents the presence or absence of that value in a row.
- **Performance**: Bitmap indexes are very efficient for queries involving multiple conditions (e.g., `AND`, `OR`) and are often used in data warehousing or read-heavy systems.
- **Example**:
  ```sql
  CREATE BITMAP INDEX idx_gender ON employees (gender);
  ```

---

### 6. **Hash Index**

- **Based on Hashing**: Hash indexes use a hash function to map the indexed values to a specific hash value. The hash values are used to quickly locate the corresponding rows.
- **Ideal for Exact Match Queries**: Hash indexes are particularly effective for equality comparisons (`=`), but they are not suitable for range queries.
- **Performance**: Provides constant time lookup for exact matches, but not useful for ordered queries or range scans.
- **Example**: A hash index on an ID field:
  ```sql
  CREATE INDEX idx_id_hash ON employees (employee_id) USING HASH;
  ```

---

### 7. **Spatial Index**

- **For Spatial Data**: Spatial indexes are specialized indexes used for geographic or spatial data (such as points, lines, and polygons) stored in spatial databases.
- **Structure**: Typically uses techniques like **R-trees** or **Quadtrees** to organize and index spatial data.
- **Use Case**: Used for queries involving geographical searches, such as "find all locations within a given radius."
- **Example**:
  ```sql
  CREATE SPATIAL INDEX idx_location ON stores (location);
  ```

---

### 8. **Full-text Index**

- **For Text Search**: Full-text indexes are used for efficiently searching text-based columns, such as when performing searches for words or phrases in a large body of text.
- **Structure**: The index breaks down the text into tokens (words or terms) and creates an inverted index mapping each term to the rows that contain it.
- **Use Case**: Ideal for **search engines** or databases that require efficient **text search** features.
- **Example**:
  ```sql
  CREATE FULLTEXT INDEX idx_description ON products (product_description);
  ```

---

### 9. **Unique Index**

- **Enforces Uniqueness**: A unique index ensures that no two rows in the indexed column(s) have the same value.
- **Automatic Creation**: A unique index is often created automatically when a `PRIMARY KEY` or `UNIQUE` constraint is defined on a table.
- **Use Case**: Guarantees the integrity of columns that must have unique values (e.g., email addresses).
- **Example**:
  ```sql
  CREATE UNIQUE INDEX idx_email ON customers (email);
  ```

---

### 10. **Clustered vs. Non-clustered Index** (Comparison)

| **Feature**           | **Clustered Index**                             | **Non-clustered Index**                                  |
| --------------------- | ----------------------------------------------- | -------------------------------------------------------- |
| **Physical Order**    | Data rows are physically stored in index order  | Data rows are stored separately from the index           |
| **Number of Indexes** | Only one per table                              | Multiple indexes can exist per table                     |
| **Storage**           | The table data is re-ordered to match the index | The index is stored separately from table data           |
| **Performance**       | Faster for sequential access and range queries  | Faster for random access and specific queries            |
| **Use Case**          | Best for primary key or unique key columns      | Best for secondary indexes on frequently queried columns |

---

### **Conclusion**

The choice of index type depends on various factors such as query patterns, column data types, and the size of the data. While **B-tree** indexes are the most widely used, each index type has specific advantages that make it suitable for different situations. Using the right type of index can drastically improve query performance, reduce data retrieval time, and optimize overall system efficiency.
