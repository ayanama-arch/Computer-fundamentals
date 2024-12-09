# Intro to the Relational Model

## Relational Database Concepts

---

### **1. Relation:**

- A **relation** is a table in a database, which consists of rows and columns.
- Each **row** (also called a **tuple**) represents a single record.
- Each **column** (also called an **attribute**) represents a field or property of the record.
- Example: A **students** relation might have rows like student data and columns like `student_id`, `name`, and `age`.

**Example of a relation (students):**
| student_id | name | age |
|------------|--------|-----|
| 1 | Alice | 20 |
| 2 | Bob | 22 |

---

### **2. Attributes:**

- **Attributes** are the columns in a relation (table).
- They describe the properties or fields of the relation.
- Example: In the **students** table, `student_id`, `name`, and `age` are attributes.

---

### **3. Relations Are Unordered:**

- **Relations** are **unordered**, meaning that the order of the rows in a table does not matter.
- You can reorder the rows in any way, and the relation remains the same.
- **Key Point**: In relational algebra, the result of operations like **select** or **project** is still a relation, and its rows are unordered.

---

### **4. DB Schema:**

- The **DB Schema** defines the structure of the database.
- It includes the **relations (tables)**, the **attributes (columns)** of each relation, and the constraints (rules) on the data.
- The schema does not contain data, only the **structure** and relationships between tables.
- Example: A **students** schema might define a table with attributes like `student_id`, `name`, and `age`.

**Example of a simple schema:**

```
students(student_id, name, age)
```

---

### **5. Keys:**

- **Keys** are sets of attributes that uniquely identify rows in a relation.
- Types of keys:
  - **Superkey**: A set of attributes that can uniquely identify rows.
  - **Candidate Key**: A minimal superkey (no redundant attributes).
  - **Primary Key**: A selected candidate key used to uniquely identify each row in the table.
- Example: In the **students** table, `{student_id}` could be a **primary key**, as it uniquely identifies each student.

---

### **6. Relational Query Language:**

- **Relational Query Languages** are used to interact with and manipulate data in relational databases.
- **SQL (Structured Query Language)** is the most popular **relational query language**.
- It allows you to perform operations like **select**, **insert**, **update**, and **delete** data in relations (tables).
- Example: To get all students who are 20 years old, you would use an SQL query:
  ```sql
  SELECT * FROM students WHERE age = 20;
  ```

---

### Summary:

- **Relation**: A table in a database with rows and columns.
- **Attributes**: Columns in a relation, describing fields of the data.
- **Relations Are Unordered**: The rows in a relation have no specific order.
- **DB Schema**: Defines the structure of the database (tables, attributes, and constraints).
- **Keys**: Attributes or sets of attributes used to uniquely identify rows in a table (superkey, candidate key, primary key).
- **Relational Query Language**: A language used to query and manipulate data in a relational database, like SQL.

## Relational Algebra Operations

---

### **1. Superkey:**

- A **superkey** is a set of attributes (columns) in a relation that can uniquely identify a tuple (row).
- Example: In the **instructor** table, `{ID}`, `{ID, name}`, `{ID, department}` can all be superkeys, because they can uniquely identify an instructor.

### **2. Candidate Key:**

- A **candidate key** is a **minimal** superkey. It's a superkey with no redundant attributes.
- Example: `{ID}` is a candidate key for the **instructor** table because it uniquely identifies instructors and doesn't contain any unnecessary attributes.

### **3. Primary Key:**

- A **primary key** is one of the candidate keys chosen to uniquely identify rows in the table.
- Example: `{ID}` might be selected as the primary key for **instructor** because it uniquely identifies each instructor and is minimal.

---

### **4. Select Operation (σ):**

- **Select (σ)** operation selects tuples (rows) from a relation that satisfy a given condition (predicate).
- Notation: \( \sigma\_{p}(r) \), where \( p \) is the condition.
- Example: To find all instructors in the "Physics" department:
  - Query: \( \sigma\_{dept_name="Physics"}(\text{instructor}) \)
  - This will return rows where the department name is "Physics".

### **5. Project Operation (π):**

- **Project (π)** operation selects specific columns (attributes) from a relation, removing duplicate rows.
- Notation: \( \pi\_{attributes}(r) \)
- Example: To find the names of all instructors:
  - Query: \( \pi\_{name}(\text{instructor}) \)
  - This will return a list of instructor names (with duplicates removed).

---

### **6. Cartesian Product (×):**

- **Cartesian Product** combines every row from one relation with every row from another relation.
- Result: The number of rows in the product will be the product of the number of rows in both relations.
- Notation: \( R \times S \)
- Example: If **students** has 2 rows and **courses** has 2 rows, the result will have 4 rows.

  - **students**:  
    | student_id | name |
    |------------|--------|
    | 101 | Alice |
    | 102 | Bob |

  - **courses**:  
    | course_id | course_name |
    |-----------|-------------|
    | C1 | Math |
    | C2 | Physics |

  - **Cartesian Product** (students × courses):
    | student_id | name | course_id | course_name |
    |------------|--------|-----------|-------------|
    | 101 | Alice | C1 | Math |
    | 101 | Alice | C2 | Physics |
    | 102 | Bob | C1 | Math |
    | 102 | Bob | C2 | Physics |

---

### **7. Key Differences between Select and Project:**

- **Select (σ)**: Filters rows based on a condition (predicate).
  - Example: Select instructors from the "Physics" department.
- **Project (π)**: Selects specific columns and removes duplicates.
  - Example: List instructor names without duplicates.
- Both return relations, but **Select** operates on rows, while **Project** operates on columns.

---

### **8. Comparison Between Select and Project:**

- **Select** operation extracts rows based on conditions, while **Project** extracts columns.
- **Select**: Filters data, keeping all columns.
- **Project**: Reduces the number of columns, removing duplicates.

---

### **Summary:**

- **Superkey**: A set of attributes that uniquely identifies rows.
- **Candidate Key**: A minimal superkey.
- **Primary Key**: A selected candidate key for the table.
- **Select (σ)**: Filters rows based on a condition.
- **Project (π)**: Selects columns, removing duplicates.
- **Cartesian Product (×)**: Combines every row from one table with every row from another table, resulting in all possible combinations.

These operations form the core of relational algebra, which is used to manipulate data in relational databases.

page-18 to be continued
