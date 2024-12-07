# Relational Algebra

## Introduction to Relational Algebra

**Relational Algebra** is a procedural query language used to query and manipulate data in relational databases. It forms the theoretical foundation of relational databases and SQL. It operates on _relations_ (tables) and uses a set of operations to retrieve data or generate new relations.

---

### **Key Features of Relational Algebra**

1. **Set-Based:** Operates on sets of tuples (rows).
2. **Foundation for SQL:** Forms the mathematical basis for structured query languages like SQL.
3. **Procedural Nature:** Specifies _how_ to obtain results.
4. **Relational Model:** Operates on relations (tables), ensuring that inputs and outputs are relations.

---

### **Basic Operations**

The basic operations of relational algebra are categorized into:

1. **Unary Operations:** Operate on a single relation.
2. **Binary Operations:** Combine two relations.

#### **1. Unary Operations**

- **Selection (σ):** Filters rows based on a condition.
  - Example: `σ(condition)(R)` retrieves rows from relation `R` that satisfy the condition.
  - SQL Equivalent: `SELECT * FROM R WHERE condition;`
- **Projection (π):** Selects specific columns.
  - Example: `π(column1, column2)(R)`
  - SQL Equivalent: `SELECT column1, column2 FROM R;`
- **Rename (ρ):** Renames a relation or its attributes.
  - Example: `ρ(new_name, [new_columns])(R)`

#### **2. Binary Operations**

- **Union (∪):** Combines tuples from two relations, removing duplicates.
  - Example: `R ∪ S`
  - SQL Equivalent: `SELECT * FROM R UNION SELECT * FROM S;`
- **Set Difference (-):** Retrieves tuples in one relation but not in another.
  - Example: `R - S`
  - SQL Equivalent: `SELECT * FROM R EXCEPT SELECT * FROM S;`
- **Intersection (∩):** Retrieves common tuples from two relations.
  - Example: `R ∩ S`
  - SQL Equivalent: `SELECT * FROM R INTERSECT SELECT * FROM S;`
- **Cartesian Product (×):** Combines tuples from two relations.
  - Example: `R × S`
  - SQL Equivalent: `SELECT * FROM R, S;`
- **Join (⨝):** Combines tuples from two relations based on a condition.
  - Example: `R ⨝ condition S`
  - SQL Equivalent: `SELECT * FROM R JOIN S ON condition;`

#### **Derived Operations**

- **Natural Join (⋈):** Combines tuples with the same attribute values.
  - Example: `R ⋈ S`
- **Division (÷):** Divides one relation by another.
  - Example: `R ÷ S`

---

### **Why Learn Relational Algebra?**

1. **Conceptual Foundation:** Helps understand database theory and SQL queries.
2. **Query Optimization:** Enables understanding of query execution plans.
3. **Database Design:** Facilitates better schema design and normalization.

---

### **Example:**

Given two relations:

**Student**  
| ID | Name | Dept |  
|----|------|------|  
| 1 | John | CS |  
| 2 | Mary | EE |

**Enrollment**  
| ID | Course |  
|----|--------|  
| 1 | DBMS |  
| 2 | ML |

**Query:** Retrieve names of students enrolled in the course "DBMS."

1. Perform a **join**:  
   `Student ⨝ Student.ID = Enrollment.ID Enrollment`

2. Apply **selection**:  
   `σ(Course = 'DBMS')(Student ⨝ Enrollment)`

3. Apply **projection**:  
   `π(Name)(σ(Course = 'DBMS')(Student ⨝ Enrollment))`

Result: `John`

Relational algebra thus provides a systematic way to process queries and understand the theoretical aspects of database systems.

## Projection in Relational Algebra

**Projection**, denoted by \( \pi \), is a **unary operation** in relational algebra. It retrieves specific columns (attributes) from a relation (table) and eliminates duplicate rows to ensure the result remains a valid relation (set of tuples).

---

### **Definition**

- **Syntax:** \( \pi\_{A1, A2, \dots, An}(R) \)
  - \( A1, A2, \dots, An \): Attributes to be selected.
  - \( R \): Input relation (table).
- **Output:** A new relation with only the specified attributes and no duplicate rows.

---

### **Properties of Projection**

1. **Attribute Selection:** Reduces the number of attributes in the result by keeping only those specified.
2. **Duplicate Elimination:** Removes duplicate tuples in the resulting relation.
3. **Order Independence:** Projection does not consider the order of attributes.

---

### **Example**

Consider a relation \( Student \):

| **ID** | **Name** | **Dept** | **Year** |
| ------ | -------- | -------- | -------- |
| 1      | Alice    | CS       | 2        |
| 2      | Bob      | EE       | 3        |
| 3      | Alice    | CS       | 2        |

#### **Projection Query**

1. **Retrieve only names:**  
   \( \pi\_{Name}(Student) \)  
   Result:

   | **Name** |
   | -------- |
   | Alice    |
   | Bob      |

2. **Retrieve names and departments:**  
   \( \pi\_{Name, Dept}(Student) \)  
   Result:

   | **Name** | **Dept** |
   | -------- | -------- |
   | Alice    | CS       |
   | Bob      | EE       |

---

### **SQL Equivalent**

Projection in relational algebra corresponds to the `SELECT` clause in SQL for specific columns:

- Relational Algebra: \( \pi\_{Name, Dept}(Student) \)
- SQL:
  ```sql
  SELECT Name, Dept FROM Student;
  ```

---

### **Key Use Cases**

1. **Extract Relevant Data:** Retrieve only the attributes necessary for analysis or further processing.
2. **Data Simplification:** Reduce the dimensionality of data for clarity and performance.

---

### **Limitations**

- Projection alone cannot filter rows; it only selects columns. For filtering, **selection** (\( \sigma \)) is used in combination with projection.

For example:  
Retrieve names of students in the "CS" department:  
\( \pi*{Name}(\sigma*{Dept='CS'}(Student)) \)  
This combines **selection** and **projection** to filter rows first and then select the desired attribute(s).

## Selection in Relational Algebra

**Selection**, denoted by \( \sigma \), is a **unary operation** in relational algebra that filters rows (tuples) from a relation (table) based on a given condition (predicate). It retrieves only those rows that satisfy the specified condition, leaving the structure of the relation unchanged.

---

### **Definition**

- **Syntax:** \( \sigma\_{condition}(R) \)
  - \( condition \): A Boolean expression (predicate) that specifies the filter criteria.
  - \( R \): Input relation (table).
- **Output:** A new relation containing rows from \( R \) that satisfy the \( condition \).

---

### **Properties of Selection**

1. **Row Filtering:** Selection reduces the number of rows in the output relation.
2. **Attributes Unchanged:** All columns of the original relation are included in the result.
3. **Predicate Evaluation:** Supports conditions involving comparisons (`=`, `<`, `>`, `<=`, `>=`, `!=`) and logical operators (`AND`, `OR`, `NOT`).
4. **Order Independence:** The order of rows in the output is not considered.

---

### **Example**

Consider a relation \( Student \):

| **ID** | **Name** | **Dept** | **Year** |
| ------ | -------- | -------- | -------- |
| 1      | Alice    | CS       | 2        |
| 2      | Bob      | EE       | 3        |
| 3      | Charlie  | CS       | 2        |
| 4      | David    | ME       | 1        |

#### **Selection Queries**

1. **Select students from the CS department:**  
   \( \sigma\_{Dept = 'CS'}(Student) \)  
   Result:

   | **ID** | **Name** | **Dept** | **Year** |
   | ------ | -------- | -------- | -------- |
   | 1      | Alice    | CS       | 2        |
   | 3      | Charlie  | CS       | 2        |

2. **Select students in their 2nd year:**  
   \( \sigma\_{Year = 2}(Student) \)  
   Result:

   | **ID** | **Name** | **Dept** | **Year** |
   | ------ | -------- | -------- | -------- |
   | 1      | Alice    | CS       | 2        |
   | 3      | Charlie  | CS       | 2        |

3. **Select CS students in their 2nd year:**  
   \( \sigma\_{Dept = 'CS' \, AND \, Year = 2}(Student) \)  
   Result:

   | **ID** | **Name** | **Dept** | **Year** |
   | ------ | -------- | -------- | -------- |
   | 1      | Alice    | CS       | 2        |
   | 3      | Charlie  | CS       | 2        |

---

### **SQL Equivalent**

Selection in relational algebra corresponds to the `WHERE` clause in SQL:

- Relational Algebra: \( \sigma\_{Year = 2}(Student) \)
- SQL:
  ```sql
  SELECT * FROM Student WHERE Year = 2;
  ```

---

### **Use Cases**

1. **Data Filtering:** Select rows based on criteria such as age, department, or location.
2. **Subset Creation:** Create a subset of data for further processing or analysis.
3. **Combined with Projection:** Often used alongside **projection** (\( \pi \)) to filter rows and select specific columns.

---

### **Combination Example:**

Retrieve names of students from the "CS" department in their 2nd year:

- Relational Algebra:  
  \( \pi*{Name}(\sigma*{Dept = 'CS' \, AND \, Year = 2}(Student)) \)
- SQL:
  ```sql
  SELECT Name FROM Student WHERE Dept = 'CS' AND Year = 2;
  ```
  Result:

| **Name** |
| -------- |
| Alice    |
| Charlie  |

---

### **Limitations**

- Selection alone cannot modify or compute new values; it strictly filters rows. For computations, additional operations like **aggregation** or **projection** are required.

## Cross Product (Cartesian Product) in Relational Algebra

**Cross Product**, also called the **Cartesian Product**, is a **binary operation** in relational algebra that combines every tuple from one relation with every tuple from another relation. The resulting relation contains all possible combinations of tuples from the two input relations.

---

### **Definition**

- **Syntax:** \( R \times S \)
  - \( R \): The first relation.
  - \( S \): The second relation.
- **Output:** A new relation consisting of all pairs of tuples \((r, s)\), where \( r \in R \) and \( s \in S \).

---

### **Key Characteristics**

1. **Tuple Combination:** If \( R \) has \( n \) tuples and \( S \) has \( m \) tuples, the resulting relation will have \( n \times m \) tuples.
2. **Attribute Combination:** The resulting relation will have all attributes from both relations.
   - If \( R \) has \( A \) attributes and \( S \) has \( B \) attributes, the result will have \( A + B \) attributes.
3. **No Conditions:** Cartesian product does not impose any conditions on how tuples are paired; all combinations are included.

---

### **Example**

Consider two relations:

**Student**  
| **ID** | **Name** |  
|--------|----------|  
| 1 | Alice |  
| 2 | Bob |

**Course**  
| **CourseID** | **CourseName** |  
|--------------|----------------|  
| 101 | Math |  
| 102 | Physics |

#### **Cross Product Query**

\( Student \times Course \)

**Result:**

| **ID** | **Name** | **CourseID** | **CourseName** |
| ------ | -------- | ------------ | -------------- |
| 1      | Alice    | 101          | Math           |
| 1      | Alice    | 102          | Physics        |
| 2      | Bob      | 101          | Math           |
| 2      | Bob      | 102          | Physics        |

---

### **SQL Equivalent**

Cartesian product in SQL is achieved using a `CROSS JOIN`:

```sql
SELECT *
FROM Student
CROSS JOIN Course;
```

---

### **Use Cases**

1. **Intermediate Step in Joins:** Cross product is often used as a step in **join** operations, where conditions are applied to filter the results of the Cartesian product.
2. **Pairwise Combination:** Useful in scenarios requiring all possible pairings of data from two sets.
3. **Combinatorial Analysis:** When all combinations of rows are needed for further computation.

---

### **Limitations**

1. **Data Explosion:** The number of tuples grows rapidly, making it computationally expensive for large relations.
   - Example: A relation with 1,000 tuples combined with another relation of 1,000 tuples produces 1,000,000 tuples.
2. **Rarely Used Directly:** Typically combined with **selection** (\( \sigma \)) to create meaningful results, as most use cases do not require all possible pairings.

---

### **Combination Example:**

Retrieve all students and their enrolled courses. Combine **cross product** and **selection** to match students to specific courses:

- **Relational Algebra:**  
  \( \sigma\_{Student.ID = Enrollment.StudentID}(Student \times Enrollment) \)

- **SQL Equivalent:**
  ```sql
  SELECT *
  FROM Student
  JOIN Enrollment
  ON Student.ID = Enrollment.StudentID;
  ```
