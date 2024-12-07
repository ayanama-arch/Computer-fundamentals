# Introduction

## Levels of Abstraction

Databases can be understood in terms of different levels of abstraction, design, and usage. These levels help organize the data management process, from the physical storage of data to how it is accessed by end-users. Here are the primary levels of databases:

### 1. **Physical Level (Internal Level)**

- **Description:** This is the lowest level of database abstraction. It deals with the physical storage of data on storage devices like hard drives or SSDs.
- **Concerns:**
  - How data is stored in blocks on the disk.
  - File structures and indexing mechanisms.
  - Memory management, data compression, and encryption.
  - Optimization of data access and retrieval speed.
- **Example:** A database administrator might work with physical storage aspects, deciding how to store indexes or how to distribute data across multiple storage devices.

### 2. **Logical Level (Conceptual Level)**

- **Description:** This level provides a higher-level abstraction of the database, defining what data is stored and how it is organized without specifying how it is stored.
- **Concerns:**
  - The structure of the entire database: tables, relationships, views, indexes.
  - Data integrity and constraints (e.g., primary keys, foreign keys).
  - The schema that defines the logical structure of the database.
- **Example:** Database designers and developers work at this level, designing the overall structure of the database, such as defining tables, relationships, and normalization rules.

### 3. **View Level (External Level)**

- **Description:** The highest level of database abstraction, the view level concerns how data is presented to end-users or applications. Users interact with the database at this level.
- **Concerns:**
  - Different views for different users or user groups.
  - Ensuring that users only see the data they are authorized to access.
  - Customizing the way data is presented based on user requirements.
- **Example:** An employee in a company might have a specific view of the customer database, showing only the data they need to perform their job. A different view might be available for managers, showing aggregated data.

### 4. **Data Model Level**

- **Description:** Though not traditionally listed as a "level," the data model defines the overall architecture and framework for how data is stored and accessed across the different levels.
- **Types of Data Models:**
  - **Hierarchical Model:** Organizes data in a tree-like structure.
  - **Network Model:** Represents data using graphs with more complex relationships.
  - **Relational Model:** Uses tables (relations) to represent data and relationships.
  - **Object-Oriented Model:** Integrates object-oriented programming principles into database design.
  - **NoSQL Models:** Includes key-value, document, column-family, and graph models, each tailored for specific data storage needs.

### 5. **Schema Levels (Three-Schema Architecture)**

- **Internal Schema:** Corresponds to the physical level, defining the physical storage structure.
- **Conceptual Schema:** Corresponds to the logical level, describing the database's overall structure.
- **External Schema:** Corresponds to the view level, defining different views for different users.

### 6. **Instances**

Actual content in database at particular point of time.

### Summary

- **Physical Level:** Deals with data storage on physical devices.
- **Logical Level:** Defines the structure and organization of the database.
- **View Level:** How data is presented to and interacted with by users.
- **Data Model Level:** Defines the framework for how data is represented across levels.
- **Schema Levels:** Three-schema architecture that includes internal, conceptual, and external schemas to manage database complexity.

Understanding these levels is crucial for database design, management, and usage, ensuring that the database system functions efficiently and meets the needs of both users and applications.

## DDL vs DML

**Data Definition Language (DDL)** and **Data Manipulation Language (DML)** are both subsets of SQL (Structured Query Language), but they serve different purposes in database management. Here's a breakdown of the key differences between DDL and DML:

### 1. **Purpose**:

- **DDL (Data Definition Language)**:
  - **Focus**: Defines and manages the structure of the database.
  - **Use**: Used to create, alter, and delete database objects such as tables, indexes, views, and schemas.
  - **Example Commands**: `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`.
- **DML (Data Manipulation Language)**:
  - **Focus**: Manipulates the data within the database objects.
  - **Use**: Used to retrieve, insert, update, and delete data in the database.
  - **Example Commands**: `SELECT`, `INSERT`, `UPDATE`, `DELETE`.

### 2. **Operation Type**:

- **DDL**:
  - **Structural Operations**: Changes the structure or schema of the database, such as creating a new table or altering an existing table’s structure.
- **DML**:
  - **Data Operations**: Focuses on the actual data within the database, such as adding a new record to a table or modifying existing data.

### 3. **Effect on Data**:

- **DDL**:
  - **Schema Impact**: Affects the database schema. For example, `DROP TABLE` removes the entire table, including all its data.
  - **Data Loss**: Can lead to data loss if objects are dropped or truncated.
- **DML**:
  - **Data Impact**: Affects the data stored in the database but does not alter the schema. For example, `UPDATE` modifies data in the existing table structure.

### 4. **Transaction Handling**:

- **DDL**:
  - **Auto-Commit**: Most DDL commands are automatically committed, meaning changes are immediately and permanently applied to the database. There's typically no rollback unless explicitly supported by the database system.
- **DML**:
  - **Transaction Control**: DML operations can be controlled with transaction commands like `COMMIT` and `ROLLBACK`, allowing changes to be confirmed or undone before they are finalized.

### 5. **Reversibility**:

- **DDL**:
  - **Non-Reversible**: DDL commands are often irreversible. For example, once a table is dropped using `DROP`, the data cannot be recovered unless there's a backup.
- **DML**:
  - **Reversible**: DML commands can be rolled back if they are part of a transaction that hasn’t been committed, allowing for data recovery if necessary.

### 6. **Examples**:

- **DDL Example**:

  ```sql
  CREATE TABLE Employees (
      EmployeeID INT PRIMARY KEY,
      FirstName VARCHAR(50),
      LastName VARCHAR(50)
  );
  ```

  This DDL command creates a new table called `Employees` with specified columns.

- **DML Example**:

  ```sql
  INSERT INTO Employees (EmployeeID, FirstName, LastName)
  VALUES (1, 'John', 'Doe');
  ```

  This DML command inserts a new record into the `Employees` table.

### Summary:

- **DDL**: Manages the structure of the database, including creating, modifying, and deleting database objects. It has an immediate and often irreversible impact on the database schema.
- **DML**: Manages the data within the database, allowing for data retrieval, insertion, updating, and deletion. It operates within transactions, offering more control over changes before they are finalized.
