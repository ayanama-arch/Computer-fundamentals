# SQL

## Constraints in SQL

In SQL, **constraints** are used to define the rules and limitations for the data in a table. They are important for maintaining the integrity, accuracy, and reliability of the data. Constraints ensure that the data entered into the database follows specific rules.

Here are the main types of **SQL constraints**:

---

### 1. **`NOT NULL` Constraint**

- **Purpose**: Ensures that a column **cannot** have a `NULL` value. It forces the user to provide a value when inserting or updating a row.
- **Usage**: Applied when you want to ensure that a column always contains a valid (non-null) value.

#### Example:

```sql
CREATE TABLE Employees (
    EmployeeID INT NOT NULL,
    Name VARCHAR(100) NOT NULL,
    Age INT
);
```

In this example, the `EmployeeID` and `Name` columns cannot have `NULL` values.

---

### 2. **`UNIQUE` Constraint**

- **Purpose**: Ensures that all values in a column (or a combination of columns) are unique. It prevents duplicate entries.
- **Usage**: Applied when you want to guarantee that no two rows have the same value in a particular column.

#### Example:

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Email VARCHAR(100) UNIQUE,
    Name VARCHAR(100)
);
```

In this example, the `Email` column will not allow duplicate email addresses.

---

### 3. **`PRIMARY KEY` Constraint**

- **Purpose**: Uniquely identifies each row in a table. A primary key must contain **unique values** and cannot contain `NULL` values.
- **Usage**: Applied to a column (or a combination of columns) that will uniquely identify each record in a table.
- **Note**: A table can have **only one** primary key, but it can consist of multiple columns (composite key).

#### Example:

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    Age INT
);
```

In this example, the `EmployeeID` column is the primary key, ensuring that each `EmployeeID` is unique.

---

### 4. **`FOREIGN KEY` Constraint**

- **Purpose**: Ensures that a value in one table corresponds to a value in another table. It is used to maintain the **referential integrity** between two tables.
- **Usage**: Applied to a column (or combination of columns) to create a relationship between two tables. The value in the foreign key column must match a value in the referenced primary key (or unique key) column of another table.

#### Example:

```sql
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100)
);

CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    DepartmentID INT,
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);
```

In this example, the `DepartmentID` in the `Employees` table must match a valid `DepartmentID` from the `Departments` table. If an invalid or non-existent `DepartmentID` is inserted into the `Employees` table, it will violate the foreign key constraint.

---

### 5. **`CHECK` Constraint**

- **Purpose**: Ensures that all values in a column satisfy a specific condition or expression. It is used to enforce domain integrity by allowing only specific values.
- **Usage**: Applied to a column to limit the range of values or enforce a condition on the column's values.

#### Example:

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    Age INT CHECK (Age >= 18)  -- Ensures that employees are at least 18 years old
);
```

In this example, the `CHECK` constraint ensures that the `Age` of an employee is 18 or more.

---

### 6. **`DEFAULT` Constraint**

- **Purpose**: Provides a default value for a column when no value is specified during an insert operation.
- **Usage**: Applied to a column when you want to provide a default value if the user does not provide a value for that column.

#### Example:

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    Status VARCHAR(10) DEFAULT 'Active'  -- Default value for Status is 'Active'
);
```

In this example, if no `Status` value is provided during insertion, the column will default to 'Active'.

---

### 7. **`INDEX` Constraint**

- **Purpose**: While not technically a constraint in the strictest sense, an **index** is often considered part of the database schema and is used to speed up query retrieval on columns that are frequently used in `WHERE`, `ORDER BY`, or `JOIN` conditions.
- **Usage**: Applied to columns to improve query performance by reducing the time it takes to search for data.

#### Example:

```sql
CREATE INDEX idx_employee_name
ON Employees (Name);
```

This creates an index on the `Name` column in the `Employees` table to make searches by name more efficient.

---

### 8. **`AUTO_INCREMENT` (or `SERIAL` in some DBMS)**

- **Purpose**: Automatically generates a unique value for a column when a new record is inserted. Typically used for primary key columns.
- **Usage**: Applied when you want the database to automatically generate a unique value for a column (usually an ID).

#### Example:

```sql
CREATE TABLE Employees (
    EmployeeID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100),
    Age INT
);
```

In this example, the `EmployeeID` will automatically increment whenever a new row is inserted.

---

### Summary Table of Constraints:

| **Constraint**     | **Purpose**                                              | **Can Be Applied To**                      | **Example**                                                       |
| ------------------ | -------------------------------------------------------- | ------------------------------------------ | ----------------------------------------------------------------- |
| **NOT NULL**       | Ensures a column cannot have NULL values                 | Any column                                 | `Name VARCHAR(100) NOT NULL`                                      |
| **UNIQUE**         | Ensures all values in a column are unique                | Any column                                 | `Email VARCHAR(100) UNIQUE`                                       |
| **PRIMARY KEY**    | Uniquely identifies each record, cannot be NULL          | One or more columns (usually 1)            | `EmployeeID INT PRIMARY KEY`                                      |
| **FOREIGN KEY**    | Ensures data integrity between two tables                | Column(s) referencing another table        | `FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)` |
| **CHECK**          | Ensures data meets a specified condition                 | Any column                                 | `Age INT CHECK (Age >= 18)`                                       |
| **DEFAULT**        | Provides a default value if no value is provided         | Any column                                 | `Status VARCHAR(10) DEFAULT 'Active'`                             |
| **INDEX**          | Speeds up data retrieval                                 | Any column (often used for lookup columns) | `CREATE INDEX idx_employee_name ON Employees (Name)`              |
| **AUTO_INCREMENT** | Automatically generates a unique number for each new row | Usually for primary key columns            | `EmployeeID INT AUTO_INCREMENT PRIMARY KEY`                       |

---

### Conclusion:

SQL constraints are crucial for maintaining data integrity and ensuring that the data in your database adheres to specific rules. By using constraints like `PRIMARY KEY`, `FOREIGN KEY`, `CHECK`, `DEFAULT`, and others, you can enforce rules for your data and prevent the insertion of invalid data.
