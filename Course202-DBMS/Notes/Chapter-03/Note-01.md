# Joins

## Introduction to Joins and its types | Need of Joins with example | DBMS

In **Relational Algebra**, which is a procedural query language used to query relational databases, joins are represented as operations that combine relations based on certain conditions. The concept of joins in relational algebra is similar to SQL, but it is expressed using set theory and mathematical operations.

Let's look at the types of joins and their equivalents in relational algebra.

---

### **Basic Operations in Relational Algebra:**

1. **Selection (σ)**: Selects rows that satisfy a given predicate.

   - **Syntax:** `σ_condition(R)`
   - **Example:** `σ_employee_id = 2 (Employee)` selects the row where `employee_id = 2` in the `Employee` relation.

2. **Projection (π)**: Selects specific columns from a relation.

   - **Syntax:** `π_column_list(R)`
   - **Example:** `π_employee_name(Employee)` selects the `employee_name` column from the `Employee` relation.

3. **Cartesian Product (×)**: Returns the Cartesian product (cross-product) of two relations.

   - **Syntax:** `R × S`
   - **Example:** `Employee × Department` returns all possible combinations of rows from the two relations.

4. **Renaming (ρ)**: Renames relations or attributes for clarity.
   - **Syntax:** `ρ_new_name(R)`

---

### **Joins in Relational Algebra:**

#### 1. **INNER JOIN (θ-Join or Conditional Join)**

- **Definition:** Combines tuples from two relations based on a condition (called **theta-join**). The condition typically involves matching values of one or more attributes from each relation.
- **Notation:** `R ⋈_condition S`
- **Example:**

  ```
  Employee ⋈ Employee.employee_id = Department.employee_id Department
  ```

  This is an **inner join** that returns all employee and department rows where `employee_id` in both relations match.

  **Steps:**

  1.  Perform Cartesian product: `Employee × Department`
  2.  Apply the condition: `σ(Employee.employee_id = Department.employee_id)`

#### 2. **LEFT OUTER JOIN**

- **Definition:** Returns all the tuples from the left relation (R) and the matching tuples from the right relation (S). If there is no match, NULL-like values are introduced for attributes of S.
- **Relational Algebra Representation:**
  Relational algebra does not natively support outer joins, but we can simulate a **left outer join** using:

  - **Union** of an inner join and a projection of non-matching tuples from the left relation.

  **Example:**

  ```
  (Employee ⋈ Employee.employee_id = Department.employee_id Department)
  ∪
  (π_employee_name, employee_id(Employee) − π_employee_name, employee_id(Employee ⋈ Employee.employee_id = Department.employee_id Department))
  ```

  This query returns:

  - All matched rows from `Employee ⋈ Department`
  - Plus the rows from `Employee` that don’t match in the `Department` relation.

#### 3. **RIGHT OUTER JOIN**

- **Definition:** Returns all the tuples from the right relation (S) and the matching tuples from the left relation (R). If there is no match, NULL-like values are introduced for attributes of R.
- **Relational Algebra Representation:** Simulated similarly to **left outer join**, but focusing on the right relation.

  **Example:**

  ```
  (Employee ⋈ Employee.employee_id = Department.employee_id Department)
  ∪
  (π_department_name, employee_id(Department) − π_department_name, employee_id(Employee ⋈ Employee.employee_id = Department.employee_id Department))
  ```

#### 4. **FULL OUTER JOIN**

- **Definition:** Returns all tuples from both relations. If there is no match, NULL-like values are introduced for the attributes of the unmatched relation.
- **Relational Algebra Representation:** Combine both left and right outer joins using **union**.

  **Example:**

  ```
  (Employee ⋈ Employee.employee_id = Department.employee_id Department)
  ∪
  (π_employee_name, employee_id(Employee) − π_employee_name, employee_id(Employee ⋈ Employee.employee_id = Department.employee_id Department))
  ∪
  (π_department_name, employee_id(Department) − π_department_name, employee_id(Employee ⋈ Employee.employee_id = Department.employee_id Department))
  ```

#### 5. **CROSS JOIN (CARTESIAN PRODUCT)**

- **Definition:** Produces the Cartesian product of two relations, meaning every row from one relation is paired with every row from the other.
- **Notation:** `R × S`
- **Example:**
  ```
  Employee × Department
  ```
  This produces all combinations of rows from `Employee` and `Department`.

#### 6. **NATURAL JOIN (⋈)**

- **Definition:** A special kind of join where the join condition is implicitly based on all columns with the same name in both relations.
- **Notation:** `R ⋈ S`
- **Example:**
  If both `Employee` and `Department` have a common column `employee_id`, a natural join would automatically join based on that column:
  ```
  Employee ⋈ Department
  ```

#### 7. **SELF JOIN**

- **Definition:** Joining a relation with itself to compare rows within the same relation.
- **Notation:** Use **renaming** to differentiate the instances of the relation.
- **Example:**
  ```
  ρ(E1, Employee) ⋈ E1.manager_id = E2.employee_id ρ(E2, Employee)
  ```
  This joins the `Employee` table with itself to find employees and their managers.

---

### **Example of Relational Algebra for a Join**

Let’s consider the example with two tables: `Employee` and `Department`.

**Employee Table:**
| employee_id | employee_name | manager_id |
|-------------|----------------|------------|
| 1 | Alice | NULL |
| 2 | Bob | 1 |
| 3 | Charlie | 1 |

**Department Table:**
| department_id | department_name | employee_id |
|---------------|-----------------|-------------|
| 1 | HR | 2 |
| 2 | IT | 3 |

**Task**: Fetch all employee names and their department names using relational algebra.

- We perform a **theta-join** between the `Employee` and `Department` relations, where `employee_id` in both relations matches:
  ```
  π(employee_name, department_name) (Employee ⋈ Employee.employee_id = Department.employee_id Department)
  ```
- **Explanation**:
  1. The **theta-join** combines the `Employee` and `Department` tables based on the condition that `Employee.employee_id = Department.employee_id`.
  2. Then, we apply a **projection (π)** to get only the `employee_name` and `department_name` columns.

This returns:

| employee_name | department_name |
| ------------- | --------------- |
| Bob           | HR              |
| Charlie       | IT              |

---

In **Relational Algebra**, joins are an essential operation for combining relations, similar to how SQL joins work, but they are expressed using mathematical set operations and join conditions.
