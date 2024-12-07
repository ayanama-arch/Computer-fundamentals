# SQL

## Introduction to **Structured Query Language (SQL)**

**SQL (Structured Query Language)** is the standard programming language used for managing and manipulating **relational databases**. It allows users to create, update, manage, and query data stored in a database system. SQL is essential for developers, database administrators, and analysts working with databases.

### Key Points about **SQL**:

---

### 1. **History of SQL**:

- **Developed in the 1970s**: SQL was initially developed by **IBM** in the 1970s under the name **SEQUEL (Structured English Query Language)**. It was later renamed SQL due to trademark issues.
- **Relational Database Model**: SQL is designed to work with relational databases based on the **relational model** proposed by **E.F. Codd** in 1970.
- **Standardization**: SQL was standardized by **ANSI (American National Standards Institute)** and **ISO (International Organization for Standardization)** in the 1980s. This standardization allows SQL to be used across different database systems (like MySQL, PostgreSQL, SQL Server, Oracle, etc.), with minor variations in syntax and features.

---

### 2. **Types of SQL Statements**:

SQL commands are divided into several categories based on their functionality:

- **DML (Data Manipulation Language)**: Used for querying and modifying data.

  - **SELECT**: Retrieves data from the database.
  - **INSERT**: Adds new records to a table.
  - **UPDATE**: Modifies existing data in a table.
  - **DELETE**: Removes data from a table.

- **DDL (Data Definition Language)**: Used to define and modify database structure.

  - **CREATE**: Creates new tables, databases, indexes, etc.
  - **ALTER**: Modifies an existing database object (like a table).
  - **DROP**: Deletes tables or other database objects.
  - **TRUNCATE**: Removes all data from a table but retains its structure.

- **DCL (Data Control Language)**: Manages permissions and access control.

  - **GRANT**: Gives user permissions.
  - **REVOKE**: Removes user permissions.

- **TCL (Transaction Control Language)**: Manages transactions within the database.
  - **COMMIT**: Saves all changes made in the transaction.
  - **ROLLBACK**: Reverts changes made in the current transaction.
  - **SAVEPOINT**: Sets a point within a transaction to which you can roll back.

---

### 3. **Basic SQL Syntax**:

- **Case Insensitivity**: SQL is generally **case-insensitive**, but some systems may differentiate between keywords (which are usually uppercase) and data or table names (which are case-sensitive in some cases).
- **Queries and Commands**: SQL queries and commands typically end with a **semicolon (;)**, especially in scripts or when working with multiple statements.
- **Clauses**: SQL statements often use clauses like `WHERE`, `ORDER BY`, `GROUP BY`, etc., to filter, sort, or group data.

---

### 4. **Data Types in SQL**:

SQL supports various **data types** for storing different kinds of information:

- **Numeric Types**: `INT`, `FLOAT`, `DECIMAL`, etc.
- **String Types**: `VARCHAR`, `TEXT`, `CHAR`, etc.
- **Date and Time Types**: `DATE`, `TIME`, `DATETIME`, etc.
- **Other Types**: `BOOLEAN`, `BLOB`, `NULL`, etc.

---

### 5. **Basic SQL Queries**:

- **SELECT Statement**:
  ```sql
  SELECT column1, column2 FROM table_name;
  ```
- **WHERE Clause** (used to filter records):
  ```sql
  SELECT * FROM table_name WHERE condition;
  ```
- **ORDER BY Clause** (to sort results):
  ```sql
  SELECT * FROM table_name ORDER BY column_name DESC;
  ```
- **JOIN Operations**: Combines rows from two or more tables based on a related column.
  - **INNER JOIN**: Returns only matching rows.
  - **LEFT JOIN**: Returns all rows from the left table and matching rows from the right table.
  - **RIGHT JOIN**: Returns all rows from the right table and matching rows from the left table.
  - **FULL JOIN**: Returns all rows when there is a match in one of the tables.

---

### 6. **Normalization and Database Design**:

- **Normalization**: The process of organizing data to reduce redundancy and dependency. The common normal forms are:
  - **1NF (First Normal Form)**: Eliminates repeating groups and ensures atomicity.
  - **2NF (Second Normal Form)**: Removes partial dependency.
  - **3NF (Third Normal Form)**: Eliminates transitive dependency.
- **Denormalization**: In some cases, denormalizing (introducing redundancy) can improve performance.

---

### 7. **Indexes**:

- An **index** is used to speed up data retrieval operations in SQL.
- They are created on columns that are frequently queried, sorted, or used in joins.

---

### 8. **Transactions**:

- A **transaction** is a sequence of SQL operations executed as a single unit.
- SQL ensures that the operations within a transaction are **atomic**, **consistent**, **isolated**, and **durable** (ACID properties).
- **COMMIT** finalizes the transaction, and **ROLLBACK** undoes changes if an error occurs.

---

### 9. **Subqueries**:

- A **subquery** is a query nested inside another query, used to retrieve intermediate results. Subqueries can be used in the **SELECT**, **FROM**, and **WHERE** clauses.
- Example:
  ```sql
  SELECT name FROM employees WHERE id IN (SELECT employee_id FROM department WHERE name = 'Sales');
  ```

---

### 10. **Views**:

- A **view** is a virtual table based on the result of a query. It can be used to simplify complex queries and provide a more manageable interface to users.
- Example:
  ```sql
  CREATE VIEW employee_view AS SELECT * FROM employees WHERE department = 'HR';
  ```

---

### 11. **Stored Procedures and Functions**:

- **Stored Procedures**: Predefined SQL queries that can be executed multiple times.
- **Functions**: Similar to stored procedures but used to return a value. They can be used within SQL queries.

---

### 12. **Triggers**:

- A **trigger** is a stored procedure that automatically executes when a specific event occurs, such as **INSERT**, **UPDATE**, or **DELETE** on a table.

---

### 13. **SQL Constraints**:

- **NOT NULL**: Ensures that a column cannot have a NULL value.
- **PRIMARY KEY**: Uniquely identifies each record in a table.
- **FOREIGN KEY**: Enforces a relationship between two tables.
- **UNIQUE**: Ensures all values in a column are unique.
- **CHECK**: Ensures that all values in a column meet a specific condition.

---

### 14. **SQL Functions**:

- **Aggregate Functions**: Used to perform calculations on data in groups.
  - Examples: `SUM()`, `AVG()`, `COUNT()`, `MAX()`, `MIN()`.
- **String Functions**: Manipulate string data.
  - Examples: `CONCAT()`, `LENGTH()`, `SUBSTRING()`.
- **Date Functions**: Used to manipulate date and time.
  - Examples: `NOW()`, `DATEADD()`, `DATEDIFF()`.

---

### 15. **Security and Permissions**:

- **SQL Injection**: A vulnerability that allows attackers to inject malicious SQL code into a query. It is essential to prevent this by using parameterized queries or prepared statements.
- **Access Control**: **GRANT** and **REVOKE** commands are used to assign and remove privileges from users.

---

### 16. **SQL in Real-World Applications**:

- SQL is widely used in **web development**, **data analysis**, **business intelligence**, and **data warehousing**.
- **MySQL**, **PostgreSQL**, **Oracle**, and **SQL Server** are popular relational database systems that use SQL.

---

### Conclusion:

SQL is a powerful and versatile language for managing and querying data in relational databases. Whether you are building applications, conducting data analysis, or administering databases, mastering SQL is crucial for interacting with data efficiently and securely.

## Creating Table

To create a table in SQL, you need to define the structure of the table, including the table name, column names, and their respective data types. Below is an example of how you can create a simple table in SQL, followed by the execution of that SQL statement.

### Example SQL Table Creation:

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    DateOfBirth DATE,
    HireDate DATE,
    Salary DECIMAL(10, 2),
    Department VARCHAR(50)
);
```

### Explanation:

- **`EmployeeID INT PRIMARY KEY`**: Defines a column named `EmployeeID` as an integer and sets it as the primary key, meaning each value in this column must be unique and not null.
- **`FirstName VARCHAR(50)`**: A variable character column for storing the first name with a maximum length of 50 characters.
- **`LastName VARCHAR(50)`**: A variable character column for storing the last name with a maximum length of 50 characters.
- **`DateOfBirth DATE`**: A column for storing the date of birth of the employee.
- **`HireDate DATE`**: A column for storing the date when the employee was hired.
- **`Salary DECIMAL(10, 2)`**: A column for storing the salary of the employee, with 10 total digits and 2 decimal places.
- **`Department VARCHAR(50)`**: A column for storing the department name where the employee works.

### Executing the SQL Query:

To execute this query, you can use any relational database management system (RDBMS) like MySQL, PostgreSQL, or SQL Server. Below are the steps to execute it:

1. **In MySQL** (via command line or MySQL Workbench):

   - Open your MySQL client or MySQL Workbench.
   - Connect to your database.
   - Execute the query:

   ```sql
   CREATE TABLE Employees (
       EmployeeID INT PRIMARY KEY,
       FirstName VARCHAR(50),
       LastName VARCHAR(50),
       DateOfBirth DATE,
       HireDate DATE,
       Salary DECIMAL(10, 2),
       Department VARCHAR(50)
   );
   ```

2. **In PostgreSQL** (via psql or pgAdmin):

   - Open the PostgreSQL client or pgAdmin.
   - Connect to your database.
   - Run the SQL statement:

   ```sql
   CREATE TABLE Employees (
       EmployeeID INT PRIMARY KEY,
       FirstName VARCHAR(50),
       LastName VARCHAR(50),
       DateOfBirth DATE,
       HireDate DATE,
       Salary DECIMAL(10, 2),
       Department VARCHAR(50)
   );
   ```

3. **In SQL Server** (via SQL Server Management Studio):
   - Open SQL Server Management Studio (SSMS).
   - Connect to your server.
   - Create a new query and run the SQL query to create the table.

After successfully executing the command, the table `Employees` will be created in your database. You can then start inserting records into this table using the `INSERT INTO` statement.

### Example of Inserting Data:

```sql
INSERT INTO Employees (EmployeeID, FirstName, LastName, DateOfBirth, HireDate, Salary, Department)
VALUES (1, 'John', 'Doe', '1985-08-15', '2010-06-01', 55000.00, 'Engineering');
```

This will add a record for an employee with ID 1, name "John Doe", etc., into the `Employees` table.

## Alter Command

The `ALTER` command in SQL is a Data Definition Language (DDL) command used to modify an existing database object, such as a table. You can use `ALTER` to add, delete, or modify columns in a table, or even rename a table.

### Types of `ALTER` Commands:

1. **Add a New Column** to an Existing Table
2. **Modify an Existing Column** (e.g., change datatype, size)
3. **Drop/Delete a Column** from a Table
4. **Rename a Table or Column**

### 1. **Add a New Column to a Table**

To add a new column to an existing table, use the `ADD` keyword with the `ALTER` command.

#### Syntax:

```sql
ALTER TABLE table_name
ADD column_name data_type;
```

#### Example:

Let's say we have a table `Employees`, and we want to add a new column for the employee's email address.

```sql
ALTER TABLE Employees
ADD Email VARCHAR(100);
```

This will add an `Email` column of type `VARCHAR` with a maximum length of 100 characters to the `Employees` table.

### 2. **Modify an Existing Column**

If you want to modify the definition of a column (for example, changing its data type or size), use the `MODIFY` keyword (in MySQL) or `ALTER COLUMN` (in PostgreSQL/SQL Server).

#### Syntax (MySQL):

```sql
ALTER TABLE table_name
MODIFY column_name new_data_type;
```

#### Example (MySQL):

Let’s change the data type of the `Salary` column to `DECIMAL(12, 2)`.

```sql
ALTER TABLE Employees
MODIFY Salary DECIMAL(12, 2);
```

#### Syntax (PostgreSQL/SQL Server):

```sql
ALTER TABLE table_name
ALTER COLUMN column_name SET DATA TYPE new_data_type;
```

#### Example (PostgreSQL/SQL Server):

To change the `Salary` column to `DECIMAL(12, 2)`:

```sql
ALTER TABLE Employees
ALTER COLUMN Salary TYPE DECIMAL(12, 2);
```

### 3. **Drop/Delete a Column from a Table**

You can use the `DROP COLUMN` clause to delete a column from an existing table.

#### Syntax:

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

#### Example:

Let's say you want to remove the `Email` column from the `Employees` table.

```sql
ALTER TABLE Employees
DROP COLUMN Email;
```

### 4. **Rename a Table**

You can rename a table using the `RENAME TO` clause.

#### Syntax (MySQL/PostgreSQL/SQL Server):

```sql
ALTER TABLE old_table_name
RENAME TO new_table_name;
```

#### Example:

Let’s rename the `Employees` table to `Staff`.

```sql
ALTER TABLE Employees
RENAME TO Staff;
```

### 5. **Rename a Column**

To rename a column in a table, the syntax varies slightly across different database management systems.

#### Syntax (MySQL):

```sql
ALTER TABLE table_name
CHANGE old_column_name new_column_name data_type;
```

#### Example (MySQL):

Let’s rename the `FirstName` column to `GivenName`:

```sql
ALTER TABLE Employees
CHANGE FirstName GivenName VARCHAR(50);
```

#### Syntax (PostgreSQL/SQL Server):

```sql
ALTER TABLE table_name
RENAME COLUMN old_column_name TO new_column_name;
```

#### Example (PostgreSQL/SQL Server):

To rename `FirstName` to `GivenName`:

```sql
ALTER TABLE Employees
RENAME COLUMN FirstName TO GivenName;
```

### Full Example of Using `ALTER`:

Let’s combine multiple `ALTER` commands for a more complex scenario:

1. Add a `PhoneNumber` column.
2. Change the data type of `Salary` to `DECIMAL(12, 2)`.
3. Remove the `Department` column.
4. Rename the `LastName` column to `FamilyName`.

```sql
-- Add a PhoneNumber column
ALTER TABLE Employees
ADD PhoneNumber VARCHAR(15);

-- Modify the Salary column
ALTER TABLE Employees
MODIFY Salary DECIMAL(12, 2);

-- Drop the Department column
ALTER TABLE Employees
DROP COLUMN Department;

-- Rename LastName to FamilyName
ALTER TABLE Employees
RENAME COLUMN LastName TO FamilyName;
```

### Important Notes:

- **`ALTER`** is used for modifying the structure of a table, not for modifying data.
- Always back up your database before running `ALTER` commands in a production environment, especially if you are dropping columns or changing data types.
- The exact syntax for `ALTER` may differ slightly between database management systems (DBMS). Always check the specific syntax for your DBMS (MySQL, PostgreSQL, SQL Server, etc.).

This should help you understand and implement the `ALTER` command in SQL! Let me know if you need more details or further examples.

## Difference between Alter and Update in SQL

The key difference between **`ALTER`** and **`UPDATE`** in SQL lies in their purpose and usage. They are used for entirely different tasks:

### 1. **`ALTER`** Command (DDL - Data Definition Language)

- **Purpose**: The `ALTER` command is used to modify the **structure** of a database object (like a table). It is part of the Data Definition Language (DDL) because it deals with defining or modifying database structures.
- **What It Does**: You can use `ALTER` to add, delete, or modify columns in a table, rename tables or columns, or even change the table's data type.
- **Effect**: It modifies the **schema** of the database object.

#### Example of `ALTER`:

- **Add a new column to a table**:

  ```sql
  ALTER TABLE Employees
  ADD Email VARCHAR(100);
  ```

- **Change the data type of an existing column**:

  ```sql
  ALTER TABLE Employees
  MODIFY Salary DECIMAL(12, 2);
  ```

- **Drop a column from a table**:

  ```sql
  ALTER TABLE Employees
  DROP COLUMN PhoneNumber;
  ```

- **Rename a table**:
  ```sql
  ALTER TABLE Employees
  RENAME TO Staff;
  ```

### 2. **`UPDATE`** Command (DML - Data Manipulation Language)

- **Purpose**: The `UPDATE` command is used to modify the **data** (records/rows) inside a table. It is part of the Data Manipulation Language (DML) because it deals with modifying the content or values stored in a table, not the structure.
- **What It Does**: You can use `UPDATE` to change the values of one or more columns in one or more rows of a table.
- **Effect**: It modifies the **data** within the existing schema of the table.

#### Example of `UPDATE`:

- **Update a specific row's value**:

  ```sql
  UPDATE Employees
  SET Salary = 60000
  WHERE EmployeeID = 1;
  ```

- **Update multiple rows with a condition**:

  ```sql
  UPDATE Employees
  SET Department = 'HR'
  WHERE Department = 'Finance';
  ```

- **Update all rows**:
  ```sql
  UPDATE Employees
  SET Salary = Salary + 5000;
  ```

---

### Key Differences:

| **Aspect**    | **`ALTER`**                                                                          | **`UPDATE`**                                                                    |
| ------------- | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------- |
| **Category**  | Data Definition Language (DDL)                                                       | Data Manipulation Language (DML)                                                |
| **Purpose**   | Modify the structure of the table (columns, data types, etc.)                        | Modify the data (values) of existing rows                                       |
| **Effect**    | Changes the table schema or structure                                                | Changes the data within the rows of a table                                     |
| **Use Cases** | Add/drop/modify columns, rename table/column                                         | Modify records, update field values                                             |
| **Impact**    | Affects table structure (schema)                                                     | Affects the content of the table (data)                                         |
| **Example**   | `ALTER TABLE Employees ADD PhoneNumber VARCHAR(15);`                                 | `UPDATE Employees SET Salary = 60000 WHERE EmployeeID = 1;`                     |
| **Rollback**  | Typically requires a backup before altering, as schema changes are difficult to undo | Changes can be undone with a `ROLLBACK` (if in a transaction) or by re-updating |

### In Summary:

- **`ALTER`** is used when you want to change the structure of a table, such as adding/removing columns or modifying the table schema.
- **`UPDATE`** is used when you want to change the actual data inside the table, such as modifying values in specific rows or columns.

## Difference between Delete, Drop & Truncate in SQL

In SQL, **`DELETE`**, **`DROP`**, and **`TRUNCATE`** are commands that are often used for removing data, but they each have different purposes, functionalities, and effects. Below is a detailed comparison of the three:

### 1. **`DELETE`**

- **Purpose**: The `DELETE` command is used to remove **rows** (data) from a table based on a specified condition. It can be used to delete some or all records from a table.
- **Operation Type**: It is a **DML (Data Manipulation Language)** operation because it modifies the data inside a table.
- **Can Be Rolled Back**: Since it is a DML operation, the `DELETE` command is **transactional**, meaning the changes can be rolled back if they are done within a transaction.
- **Trigger Activation**: If there are any triggers defined for the `DELETE` operation (like `AFTER DELETE`), they will be fired.
- **Effect on Table Structure**: The structure of the table (i.e., the schema) remains unchanged; only the data in the table is removed.
- **Performance**: It can be slower, especially when deleting a large number of rows, because each row is logged individually and a condition must be evaluated for each row.

#### Example:

```sql
DELETE FROM Employees WHERE Department = 'HR';
```

This deletes all employees who belong to the 'HR' department.

- **Deleting All Rows**: If you do not specify a `WHERE` clause, all rows will be deleted, but the table structure will remain intact.
  ```sql
  DELETE FROM Employees;
  ```

### 2. **`DROP`**

- **Purpose**: The `DROP` command is used to remove **entire database objects**, such as tables, views, indexes, or even the entire database itself.
- **Operation Type**: It is a **DDL (Data Definition Language)** operation because it modifies the structure of the database.
- **Can Be Rolled Back**: `DROP` is **not transactional**. Once executed, the operation cannot be rolled back (unless using transactions in specific DBMSs, but in most cases, it is permanent).
- **Effect on Table Structure**: The `DROP` command removes the **entire table**, including its structure and data.
- **Performance**: Since the entire table or database object is removed, it is generally faster than `DELETE` or `TRUNCATE`.

#### Example:

```sql
DROP TABLE Employees;
```

This deletes the entire `Employees` table from the database, including its structure and data.

- **Dropping a Database**:
  ```sql
  DROP DATABASE CompanyDB;
  ```

### 3. **`TRUNCATE`**

- **Purpose**: The `TRUNCATE` command is used to **delete all rows** from a table, but unlike `DELETE`, it does not log individual row deletions. It is typically faster when you want to clear out all data in a table.
- **Operation Type**: It is a **DDL (Data Definition Language)** operation because it deals with the structure of the table and not just the data.
- **Can Be Rolled Back**: In most DBMSs, `TRUNCATE` is **transactional**, so if issued within a transaction, it can be rolled back. However, it is not always fully reversible in all systems.
- **Effect on Table Structure**: Unlike `DELETE`, the table structure (schema) remains intact. Only the data is removed.
- **Performance**: `TRUNCATE` is much faster than `DELETE` because it does not log individual row deletions. It typically involves deallocating the entire data page rather than removing rows one by one.
- **Trigger Activation**: `TRUNCATE` does **not** activate triggers because it is a more low-level operation that doesn't individually delete rows.
- **Foreign Key Constraints**: `TRUNCATE` cannot be used if the table is referenced by a foreign key constraint in another table.

#### Example:

```sql
TRUNCATE TABLE Employees;
```

This removes all rows from the `Employees` table but leaves the table structure intact.

---

### Key Differences

| **Aspect**                  | **`DELETE`**                                                | **`DROP`**                                | **`TRUNCATE`**                                         |
| --------------------------- | ----------------------------------------------------------- | ----------------------------------------- | ------------------------------------------------------ |
| **Purpose**                 | Deletes rows from a table based on a condition              | Removes entire table or database object   | Removes all rows from a table, but keeps the structure |
| **Command Type**            | DML (Data Manipulation Language)                            | DDL (Data Definition Language)            | DDL (Data Definition Language)                         |
| **Can Be Rolled Back**      | Yes, if in a transaction                                    | No                                        | Yes, if in a transaction (depends on DBMS)             |
| **Affects Table Structure** | No (Only removes data)                                      | Yes (Removes table structure)             | No (Keeps table structure intact)                      |
| **Triggers Fired**          | Yes (If defined)                                            | No                                        | No                                                     |
| **Performance**             | Slower, especially with large tables                        | Fast (removes table entirely)             | Faster than `DELETE` (deletes in bulk)                 |
| **Foreign Key Constraints** | Can be used even with foreign keys (if no child rows exist) | Cannot be used if foreign key exists      | Cannot be used if foreign key exists                   |
| **Usage**                   | For deleting specific rows of data                          | For completely removing a table or object | For quickly removing all rows from a table             |

### When to Use Each:

- **Use `DELETE`**:

  - When you need to remove specific rows of data.
  - When you want to maintain the structure of the table and the ability to roll back changes.
  - When there are triggers that should be fired when rows are deleted.

- **Use `DROP`**:

  - When you need to permanently remove an entire table, database, or other database objects.
  - When you do not need the structure of the table anymore.
  - When you are cleaning up the database.

- **Use `TRUNCATE`**:
  - When you want to quickly remove all rows from a table.
  - When you do not need to fire triggers and do not care about rolling back the changes.
  - When you want a faster alternative to `DELETE` for removing all rows (without conditions).

---

### Conclusion:

- **`DELETE`**: Deletes specific data from a table, allows rollback, and can be slower for large tables.
- **`DROP`**: Completely removes a table or database object, irreversible.
- **`TRUNCATE`**: Removes all rows from a table, faster than `DELETE`, irreversible but does not affect the table structure.

Let me know if you need more examples or further clarification!
