# SQL

## SQL Aggregate functions

**SQL aggregate functions** are used to perform calculations on multiple rows of a table and return a single value. These functions are often used with the `GROUP BY` clause to group rows based on specific columns and then perform calculations on each group.

Here are the common **SQL aggregate functions**:

### 1. **COUNT()**

- **Purpose:** Returns the number of rows that match a specified condition.
- **Example:**
  ```sql
  SELECT COUNT(*) FROM employees;
  ```
  This counts the total number of rows in the `employees` table.

### 2. **SUM()**

- **Purpose:** Adds up the values in a column.
- **Example:**
  ```sql
  SELECT SUM(salary) FROM employees;
  ```
  This sums all the values in the `salary` column.

### 3. **AVG()**

- **Purpose:** Returns the average value of a numeric column.
- **Example:**
  ```sql
  SELECT AVG(salary) FROM employees;
  ```
  This calculates the average salary of all employees.

### 4. **MIN()**

- **Purpose:** Returns the minimum value in a column.
- **Example:**
  ```sql
  SELECT MIN(salary) FROM employees;
  ```
  This finds the lowest salary in the `salary` column.

### 5. **MAX()**

- **Purpose:** Returns the maximum value in a column.
- **Example:**
  ```sql
  SELECT MAX(salary) FROM employees;
  ```
  This finds the highest salary in the `salary` column.

### 6. **GROUP_CONCAT()** (MySQL) or **STRING_AGG()** (PostgreSQL)

- **Purpose:** Concatenates values from multiple rows into a single string.
- **Example (MySQL):**
  ```sql
  SELECT GROUP_CONCAT(name) FROM employees;
  ```
  This concatenates all the employee names into one comma-separated string.

### 7. **VARIANCE() and STDDEV()**

- **Purpose:** Calculate the variance and standard deviation of values in a numeric column.
- **Example (Variance):**
  ```sql
  SELECT VARIANCE(salary) FROM employees;
  ```
  This returns the variance of the `salary` column.
- **Example (Standard Deviation):**
  ```sql
  SELECT STDDEV(salary) FROM employees;
  ```
  This calculates the standard deviation of the `salary` column.

---

### **Using Aggregate Functions with GROUP BY**

You can use aggregate functions with the `GROUP BY` clause to group rows based on specific columns and perform calculations for each group.

**Example:**

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

This query calculates the average salary for each department in the `employees` table.

---

### **Important Notes:**

- **NULL Values:** Aggregate functions typically ignore `NULL` values, except `COUNT(*)`, which counts all rows, including those with `NULL` values.
- **DISTINCT:** You can use the `DISTINCT` keyword within aggregate functions to consider only unique values.
  - **Example:**
    ```sql
    SELECT COUNT(DISTINCT department) FROM employees;
    ```
    This counts the number of distinct departments.

These aggregate functions are useful for summarizing data, calculating statistics, and performing other types of analyses on groups of data.

## Correlated Subquery in SQL

A **correlated subquery** in SQL is a subquery that references columns from the outer query. This means that for each row processed by the outer query, the subquery is executed once and can return different results based on the values in the outer query's row.

### Key Characteristics of a Correlated Subquery:

1. The **subquery** depends on the **outer query** for its values.
2. The subquery is executed **once for each row** returned by the outer query.
3. It uses **values from the outer query** in its own **WHERE** or **HAVING** clause.
4. The subquery often appears in the **SELECT**, **WHERE**, or **FROM** clause of the outer query.

### Syntax of a Correlated Subquery:

```sql
SELECT column_name(s)
FROM table_name outer_table
WHERE column_name operator
    (SELECT column_name(s)
     FROM table_name inner_table
     WHERE condition);
```

### Example of a Correlated Subquery:

Let's consider a table `employees` with the following columns:

- `employee_id`
- `name`
- `salary`
- `department_id`

#### Scenario:

We want to find all employees who earn more than the average salary of their department.

```sql
SELECT e.name, e.salary, e.department_id
FROM employees e
WHERE e.salary >
    (SELECT AVG(e1.salary)
     FROM employees e1
     WHERE e1.department_id = e.department_id);
```

### Explanation:

- The **outer query** (`SELECT e.name, e.salary, e.department_id`) retrieves the name, salary, and department of employees.
- The **subquery** (`SELECT AVG(e1.salary) FROM employees e1 WHERE e1.department_id = e.department_id`) calculates the average salary for the department of each employee in the outer query.
- The **subquery** is **correlated** because it references `e.department_id` from the outer query. For each row of the outer query, the subquery is executed and calculates the average salary for that specific department.
- The **WHERE** condition of the outer query ensures that only employees whose salary is greater than their department’s average salary are returned.

### Correlated Subqueries vs Non-Correlated Subqueries:

- **Non-correlated subquery**: The subquery does not depend on the outer query and can be executed independently.

  - Example:
    ```sql
    SELECT name, salary
    FROM employees
    WHERE salary > (SELECT AVG(salary) FROM employees);
    ```
  - In this case, the subquery is independent of the outer query, and it calculates the average salary of all employees (not by department).

- **Correlated subquery**: The subquery depends on the outer query’s values, and it is evaluated for each row returned by the outer query.

### Use Cases for Correlated Subqueries:

1. **Finding rows based on a condition involving aggregate functions**: As shown in the example, correlated subqueries are useful for comparing individual rows against some aggregate value, such as the average or maximum salary in the same group or department.
2. **Existence check**: Correlated subqueries can be used to check for the existence of related rows in other tables.
   ```sql
   SELECT e.name
   FROM employees e
   WHERE EXISTS (
       SELECT 1
       FROM orders o
       WHERE o.employee_id = e.employee_id
   );
   ```
   This will return all employees who have at least one order.

### Performance Considerations:

- Correlated subqueries can be **slower** than non-correlated subqueries because the subquery is executed once for each row in the outer query.
- For performance reasons, it’s sometimes better to use **joins** or other techniques to avoid correlated subqueries, especially when dealing with large datasets.

In conclusion, correlated subqueries are a powerful tool for querying data where each row in the outer query requires a different calculation or condition based on its own values. However, they should be used with care when dealing with large datasets due to their potential impact on performance.

## Difference between Joins, Nested Subquery and Correlated Subquery

The **difference between Joins, Nested Subqueries, and Correlated Subqueries** lies in how they operate and how they combine or filter data from multiple tables. Let's break down each one to understand their unique characteristics:

### 1. **Joins**

A **Join** is used to combine rows from two or more tables based on a related column between them. It is the most efficient way to combine data from different tables when you need to retrieve information based on common attributes.

#### Types of Joins:

- **INNER JOIN**: Returns records that have matching values in both tables.
- **LEFT (OUTER) JOIN**: Returns all records from the left table and the matched records from the right table. If there is no match, `NULL` values are returned for columns from the right table.
- **RIGHT (OUTER) JOIN**: Returns all records from the right table and the matched records from the left table. If there is no match, `NULL` values are returned for columns from the left table.
- **FULL (OUTER) JOIN**: Returns records when there is a match in either the left or right table.

#### Example:

```sql
SELECT e.name, e.salary, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.department_id;
```

- This query joins the `employees` and `departments` tables on the `department_id` field. It returns the employee name, salary, and department name for each matching row in both tables.

### 2. **Nested Subquery (Non-correlated Subquery)**

A **nested subquery** is a subquery that is embedded within the `WHERE` or `HAVING` clause of another query. It does not depend on the outer query and can be executed independently.

#### Characteristics:

- A nested subquery is independent of the outer query.
- It is executed once and returns a result that is then used by the outer query.
- Typically used for filtering data based on aggregate functions or other scalar values.

#### Example (Nested Subquery):

```sql
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

- This query returns the names and salaries of employees whose salary is greater than the average salary in the entire `employees` table.
- The subquery `(SELECT AVG(salary) FROM employees)` is executed once and its result is used by the outer query.

### 3. **Correlated Subquery**

A **correlated subquery** is a type of subquery where the inner query references columns from the outer query. The subquery is evaluated once for each row processed by the outer query.

#### Characteristics:

- The inner query **depends on** the outer query and uses columns from the outer query.
- The subquery is executed multiple times, once for each row of the outer query.
- It is used when each row of the outer query needs to be compared to a calculated value or condition that is specific to that row.

#### Example (Correlated Subquery):

```sql
SELECT e.name, e.salary, e.department_id
FROM employees e
WHERE e.salary >
    (SELECT AVG(e1.salary) FROM employees e1 WHERE e1.department_id = e.department_id);
```

- In this query, the subquery references the `e.department_id` from the outer query, making it a correlated subquery.
- The subquery calculates the average salary for each department, and for each row in the outer query, it checks if the employee's salary is greater than the department's average salary.

---

### **Key Differences**

| **Aspect**          | **Join**                                                                              | **Nested Subquery**                                                              | **Correlated Subquery**                                                                                                             |
| ------------------- | ------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **Execution**       | Both tables are scanned and combined at once.                                         | The subquery is executed once and its result is used by the outer query.         | The subquery is executed once for each row of the outer query.                                                                      |
| **Data Dependency** | Independent rows from different tables are matched.                                   | Subquery is independent and does not reference the outer query.                  | Subquery depends on the outer query and uses its columns.                                                                           |
| **Performance**     | Generally faster, especially with indexing.                                           | Can be slower for large datasets since the subquery is executed once.            | Can be slower for large datasets as the subquery is executed multiple times.                                                        |
| **Usage**           | Ideal for combining related data from multiple tables.                                | Used for filtering data based on a scalar or aggregate value.                    | Used when each row needs to be compared to a calculated value for that specific row.                                                |
| **Flexibility**     | Very flexible and can be used with many different types of joins (inner, left, etc.). | Less flexible, as it can only be used in specific situations.                    | More flexible than nested subqueries, as it allows for row-by-row comparisons.                                                      |
| **Example**         | `SELECT * FROM table1 JOIN table2 ON table1.id = table2.id;`                          | `SELECT name FROM employees WHERE salary > (SELECT AVG(salary) FROM employees);` | `SELECT name FROM employees e WHERE e.salary > (SELECT AVG(e1.salary) FROM employees e1 WHERE e1.department_id = e.department_id);` |

---

### **When to Use Which?**

- **Use Joins** when you need to combine data from multiple tables based on common columns. Joins are usually more efficient and provide a simpler way to relate data.
- **Use Nested Subqueries** when you need to filter data based on an aggregate or scalar value and do not need to compare row-by-row.
- **Use Correlated Subqueries** when you need to perform a comparison for each row returned by the outer query, typically when you need the inner query to reference columns from the outer query.

Each approach has its strengths depending on the task at hand, so understanding when to use each can help optimize your queries and their performance.
