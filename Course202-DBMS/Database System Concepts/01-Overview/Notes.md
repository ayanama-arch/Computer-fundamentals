# **Chapter 1: Introduction**

## **Database Applications Examples (with examples):**

- **Enterprise Information:**
  - Sales: Tracking customer purchases, e.g., an online store like **Amazon** managing customer orders.
  - Accounting: Managing payments and receipts, e.g., **QuickBooks** for tracking business expenses.
- **Manufacturing:** Inventory management, e.g., a factory storing raw materials and tracking finished goods.
- **Banking and Finance:** Recording transactions, e.g., **Bank of America** managing customer accounts and loan data.
- **Education:** Student grades and course registration, e.g., **University ERPs** like Banner.
- **Airlines:** Flight reservations, e.g., booking tickets on **Air India**.
- **Telecommunication:** Call records and monthly bills, e.g., a telecom provider like **Airtel** generating bills.
- **Web-based Services:** Personalized recommendations on **Netflix** or **Flipkart**.

---

## **Purpose of Database Systems (Example for each issue):**

- **Data Redundancy and Inconsistency:**
  - Problem: Customer address is updated in one file but not others.
  - Solution: Centralized database ensures consistency.
- **Difficult Data Access:**
  - Problem: Retrieving monthly sales needs manual coding.
  - Solution: SQL query like `SELECT SUM(sales) FROM transactions WHERE MONTH = 'Jan';`.
- **Atomicity:**
  - Example: A funds transfer must either complete fully or roll back (no partial transfer).
- **Concurrent Access:**
  - Problem: Two ATMs withdraw ₹500 from a ₹1,000 account simultaneously, leading to incorrect balance.
  - Solution: Database locking mechanisms prevent such issues.

---

## **Data Models (Examples):**

- **Relational Model:** Tables for "Students" and "Courses" with a "Student-Course Enrollment" relationship.
- **Entity-Relationship Model:** A graphical representation where students "enroll in" courses.
- **Semi-structured Data:** XML/JSON for storing unstructured data like a product catalog:
  ```json
  { "Product": "Laptop", "Price": 50000, "Brand": "HP" }
  ```

---

## **Relational Model Example:**

| StudentID | Name  | Course  |
| --------- | ----- | ------- |
| 1         | Rahul | Math    |
| 2         | Priya | Science |

---

## **Languages (with examples):**

- **DDL:**
  ```sql
  CREATE TABLE Student (
      ID INT PRIMARY KEY,
      Name VARCHAR(50),
      Age INT
  );
  ```
- **DML:**
  - Procedural: Specify _how_ to retrieve data.
    ```sql
    SELECT Name FROM Student WHERE Age > 18;
    ```
  - Declarative: Specify _what_ data is needed.
    ```sql
    INSERT INTO Student (ID, Name, Age) VALUES (1, 'Rahul', 20);
    ```

---

## **SQL Query Language Example:**

To find all instructors in the Computer Science department:

```sql
SELECT name
FROM instructor
WHERE dept_name = 'Computer Science';
```

---

## **Database Design Example:**

- **Logical Design:** Decide attributes for the "Employee" table:
  - Attributes: `EmployeeID`, `Name`, `Position`, `Salary`.
- **Physical Design:** Store frequently accessed data in SSD for faster retrieval.

---

## **Components (Example Scenarios):**

- **Storage Manager:** Handles physical file storage, e.g., storing customer details in **PostgreSQL**.
- **Query Processor:** Optimizes and executes a query like:
  ```sql
  SELECT * FROM Orders WHERE CustomerID = 1;
  ```

---

## **Database Architectures (Examples):**

- **Two-Tier:** Desktop app directly interacts with the database, e.g., **MS Access**.
- **Three-Tier:** Web apps, e.g., **Amazon** frontend, application server, and database.

---

## **User Roles (with examples):**

- **Naive Users:** Use apps like **Instagram** without knowing database interactions.
- **Application Programmers:** Create the app, e.g., a developer building a ticket booking system.
- **Sophisticated Users:** Use SQL to run reports, e.g., a data analyst querying sales trends.
- **Specialized Users:** Build non-standard apps, e.g., a researcher building a **genomics database**.

---

## **History (Examples of Milestones):**

- **1970s:** IBM's **System R** prototype introduced relational databases.
- **1980s:** SQL became the standard; **Oracle** commercialized relational databases.
- **2000s:** **Google BigTable** and **NoSQL** databases for scalable storage.

---
