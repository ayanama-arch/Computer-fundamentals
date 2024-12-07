# DBMS

`Database`: Collection of related data.
`DBMS`: It is software which provides an environment to store and retrieve the data in convenient and efficient manner.

## 2-Tier vs 3-Tier Architecture

`2 Tier:` Client + Database
`3 Tier:` Client + server + Database

### 2-Tier Architecture

- **Client Tier**: This tier includes the user interface (UI) or client application that interacts directly with the database server.
- **Database Tier**: The database server manages the storage, retrieval, and manipulation of data. It handles database operations and queries sent from the client tier.

#### Characteristics

- Simple architecture with two main layers: client and database server.
- Direct communication between the client and the database server.
- Client applications often include business logic and database access code, leading to tight coupling and less scalability.
- Suitable for small-scale applications or when the number of users is limited.

### 3-Tier Architecture

- **Presentation Tier (Client Tier)**: This tier contains the user interface (UI) components, responsible for presenting data to users and capturing user input.
- **Application Tier (Middle Tier)**: The application server or middle tier processes user requests, implements business logic, and communicates with the database server.
- **Database Tier**: Similar to the 2-tier architecture, the database server manages data storage, retrieval, and manipulation.

#### Key Points

- Separation of concerns into three layers: `presentation`, `application`, and `database`.
- The presentation tier focuses on user interaction, the application tier handles business logic, and the database tier manages data storage and retrieval.
- Improved scalability and flexibility due to the separation of business logic from the user interface and database operations.
- Enables easier maintenance, updates, and modifications as each tier can be developed, deployed, and managed independently.

## Schema(structure)

- It is a logical representation of Database.

## Three Schema Architecture

### External Schema (View Level)

- **Description**: The external schema represents the user's view of the data. It defines how different user groups or applications perceive and access the data.
- **Purpose**: Allows for data customization and provides a tailored view of the database for different user roles or applications.
- **Components**: Includes multiple external schemas, each tailored to a specific user group or application's requirements.
- **Example**: In a university database, the external schema for students may include information about courses, grades, and schedules, while the external schema for faculty may include teaching assignments, research data, and student evaluations.

### Conceptual Schema (Logical Level)

- **Description**: The conceptual schema represents the logical structure of the entire database. It defines the data model, relationships between entities, constraints, and rules.
- **Purpose**: Provides a unified and abstract view of the database independent of specific user views or applications.
- **Components**: Includes entities, attributes, relationships, and integrity constraints defined in the data model (e.g., ER model, relational model).
- **Example**: In a hospital management system, the conceptual schema includes entities like patients, doctors, treatments, and relationships such as patient-doctor appointments, treatment records, and medical histories.

### Internal Schema (Physical Level)

- **Description**: The internal schema represents the physical storage and organization of data within the database. It defines how data is stored on storage devices and accessed by the DBMS.
- **Purpose**: Focuses on optimizing data storage, access paths, indexing, and physical-level security.
- **Components**: Includes data structures (e.g., tables, indexes), storage allocation, access methods, and low-level details like file organization and indexing techniques.
- **Example**: In a retail database, the internal schema specifies the storage of product data using B-trees for fast retrieval, index structures for efficient searches, and disk allocation strategies for data distribution.

### Advantages of Three Schema Architecture

- **Data Independence**: Separation of external, conceptual, and internal schemas provides data independence at each level. Changes in one schema do not affect the others, promoting flexibility and ease of maintenance.
- **Abstraction**: Provides abstraction by hiding physical storage details from users and applications, focusing on logical and conceptual data models.
- **Security and Integrity**: Allows for different levels of security and integrity constraints at each schema level, ensuring data protection and consistency.
- **Scalability and Customization**: Supports scalability by accommodating diverse user views and application requirements through external schemas, without impacting the underlying conceptual or internal schemas.

The Three Schema Architecture serves as a foundational framework for designing and managing complex databases, promoting data organization, abstraction, and flexibility across different levels of data management.

## Data Independence: Logical vs Physical

### Logical Data Independence

- **Definition**: Logical data independence refers to the ability to change the logical structure or schema of the database without affecting the external schema or application programs.
- **Purpose**: It allows modifications to the conceptual schema (logical organization of data) without requiring changes to the user views or external schemas.
- **Example**: Suppose a university updates its database schema to include additional attributes in the "Student" entity, such as "GPA" and "Major." Logical data independence ensures that existing student-facing applications or external schemas (e.g., student portals) remain functional without needing updates.

### Physical Data Independence

- **Definition**: Physical data independence refers to the ability to change the physical storage or organization of data without affecting the conceptual schema or application programs.
- **Purpose**: It enables modifications to the internal schema (physical storage structures) without impacting the logical or external schemas.
- **Example**: If the university decides to migrate its database from one storage system to another (e.g., from traditional hard drives to solid-state drives), physical data independence ensures that user applications and logical data models remain unaffected by the underlying storage changes.

### Advantages and Importance

- **Flexibility**: Data independence promotes flexibility by allowing changes at the logical or physical level without disrupting user applications or data access.
- **Maintenance**: It simplifies database maintenance and evolution over time. Changes can be made to improve performance, scalability, or storage efficiency without affecting user functionality.
- **Application Development**: Developers can focus on designing and updating user interfaces and application logic without being concerned about underlying database changes.
- **Data Integrity**: Ensures data integrity and consistency by separating logical data models from physical storage details, reducing the risk of data corruption during structural modifications.

Data independence, both logical and physical, is a key principle in database design and management, facilitating system evolution, scalability, and adaptability to changing business requirements.

## Integrity Constraints in Databases

Integrity constraints are rules or conditions that ensure the accuracy, consistency, and validity of data within a database. They help maintain data integrity by preventing invalid or inconsistent data from being inserted, updated, or deleted. Here are the common types of integrity constraints:

### 1. Entity Integrity Constraint (Primary Key Constraint)

- **Purpose**: Ensures that each row in a table is uniquely identifiable by defining a primary key.
- **Rule**: Primary key attributes must be unique and cannot contain NULL values.
- **Example**: In a "Students" table, the "StudentID" column can be defined as a primary key to ensure each student has a unique identifier.

### 2. Referential Integrity Constraint (Foreign Key Constraint)

- **Purpose**: Maintains consistency between related tables by ensuring that values in a foreign key column match values in a primary key column of another table.
- **Rule**: Foreign key values must exist in the referenced primary key column or be NULL if allowed.
- **Example**: In a "Orders" table, the "CustomerID" column can be a foreign key referencing the "CustomerID" column in the "Customers" table, ensuring that orders are associated with existing customers.

### 3. Domain Integrity Constraint

- **Purpose**: Defines acceptable values for attributes or columns based on their data types or domains.
- **Rule**: Specifies data constraints such as data ranges, allowed value lists, format requirements, and NULLability.
- **Example**: A "BirthDate" column may have a domain integrity constraint that ensures dates are within a specific range and not NULL.

### 4. Check Constraint

- **Purpose**: Allows custom validation rules to be defined for columns or tables.
- **Rule**: Specifies conditions that data must meet to be considered valid.
- **Example**: A "Status" column in an "Orders" table may have a check constraint to ensure only specific status values (e.g., 'Pending', 'Completed') are allowed.

### 5. Business Rules Constraint

- **Purpose**: Enforces business logic and rules specific to the application domain.
- **Rule**: Custom constraints based on business requirements, often implemented using check constraints or application-level validations.
- **Example**: A business rule may dictate that a product's price cannot be negative, leading to a check constraint on the "Price" column.

Integrity constraints play a crucial role in maintaining data quality, consistency, and reliability within a database, ensuring that data remains accurate and meaningful for users and applications.

## Candidate Keys and Primary Keys in Databases

### Candidate Key

- **Definition**: A candidate key is a set of one or more attributes (columns) in a table that uniquely identifies each row or record in the table.
- **Uniqueness**: Each candidate key must guarantee uniqueness, meaning no two rows can have the same combination of values for the candidate key attributes.
- **Example**: In a "Students" table, both the "StudentID" and "Email" columns could be candidate keys if they uniquely identify each student. However, only one of them will be chosen as the primary key.

### Primary Key (unique+Not Null)

- **Definition**: A primary key is a specific candidate key chosen as the main unique identifier for rows in a table.
- **Uniqueness**: Like candidate keys, a primary key must ensure uniqueness for each row in the table.
- **Non-Null Values**: Primary key attributes cannot contain NULL values, as they must uniquely identify each record.
- **Constraints**: Primary keys are subject to constraints such as entity integrity (ensuring uniqueness) and referential integrity (when used as foreign keys in related tables).
- **Example**: In the "Students" table, if "StudentID" is chosen as the primary key, it will uniquely identify each student, and no two students can have the same "StudentID."

### Key Differences

- **Number of Keys**: A table may have multiple candidate keys, but only one primary key.
- **Null Values**: Candidate keys can have NULL values (unless specified otherwise), while primary keys cannot.
- **Constraints**: Primary keys have additional constraints, such as being unique and non-null, compared to candidate keys.
- **Usage**: Primary keys are commonly used as foreign keys in related tables to establish relationships.
- **Selection**: The selection of a primary key from candidate keys depends on factors like uniqueness, stability, simplicity, and domain relevance.

### Example Scenario

- **Table**: Consider a "Customers" table in a retail database.
- **Candidate Keys**: Possible candidate keys could be "CustomerID," "Email," or "Phone Number," assuming each uniquely identifies a customer.
- **Primary Key**: If "CustomerID" is chosen as the primary key, it becomes the main identifier for customers, ensuring uniqueness and non-null values.

Candidate keys and primary keys are fundamental concepts in database design, ensuring data integrity and efficient data retrieval operations.

## Foreign Key in Databases

A foreign key is a key used to establish and enforce a relationship between two tables in a relational database. It helps maintain referential integrity by ensuring that the values in a column (or set of columns) in one table match the values in a primary key or unique key column(s) in another table.

### Key Characteristics

- **Relationship Establishment**: Links a column or set of columns in one table (child table) to the primary key or unique key column(s) in another table (parent table).
- **Referential Integrity**: Enforces data consistency by preventing actions that would violate the relationship, such as inserting a row with a non-existent foreign key value.
- **Data Validation**: Ensures that values in the foreign key column(s) exist in the referenced primary key or unique key column(s) of the parent table.
- **Cascading Actions**: Can define cascading actions such as ON DELETE and ON UPDATE to automatically propagate changes or enforce constraints when referenced records are modified or deleted.

### Example

Consider two tables in a bookstore database: "Books" and "Authors."

- **Books Table**:
  - Columns: BookID (Primary Key), Title, AuthorID (Foreign Key)
- **Authors Table**:
  - Columns: AuthorID (Primary Key), AuthorName

In this scenario:

- The "AuthorID" column in the "Books" table is a foreign key referencing the "AuthorID" column in the "Authors" table.
- It establishes a relationship between books and their respective authors.
- Ensures that each book's "AuthorID" value exists in the "Authors" table, maintaining referential integrity.

### Actions with Foreign Keys

1. **Insert**: When inserting a new row in the "Books" table, the value in the "AuthorID" column must match an existing "AuthorID" value in the "Authors" table.
2. **Update**: If an author's "AuthorID" is updated in the "Authors" table, corresponding "AuthorID" values in related rows of the "Books" table can be updated automatically (if cascading actions are defined).
3. **Delete**: Deleting an author's record in the "Authors" table can be restricted (if related books exist) or cascade-delete related books (if cascading delete is enabled).

Foreign keys play a crucial role in maintaining data integrity, enforcing relationships, and ensuring accurate data representation in relational databases.
