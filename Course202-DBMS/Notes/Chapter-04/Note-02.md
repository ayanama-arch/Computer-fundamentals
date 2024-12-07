# Relational Algebra

## Set Difference in Relational Algebra

**Set Difference**, denoted by \( R - S \), is a **binary operation** in relational algebra that retrieves tuples present in one relation but not in another. It is also known as **minus** or **except** operation.

---

### **Definition**

- **Syntax:** \( R - S \)
  - \( R \): The first relation.
  - \( S \): The second relation.
- **Output:** A new relation containing all tuples from \( R \) that are not in \( S \).

---

### **Key Characteristics**

1. **Set-Based Operation:** Both relations \( R \) and \( S \) must be union-compatible:
   - They must have the same number of attributes.
   - Corresponding attributes must have the same domain.
2. **Excludes Duplicates:** The result does not include any duplicates.
3. **Order Independence:** The order of rows is not considered.

---

### **Example**

Consider two relations:

**R (Students Enrolled in Sports)**  
| **ID** | **Name** |  
|--------|----------|  
| 1 | Alice |  
| 2 | Bob |  
| 3 | Charlie |

**S (Students Enrolled in Music)**  
| **ID** | **Name** |  
|--------|----------|  
| 2 | Bob |  
| 3 | Charlie |  
| 4 | David |

#### **Set Difference Query**

Find students enrolled in sports but not in music:  
\( R - S \)

**Result:**

| **ID** | **Name** |
| ------ | -------- |
| 1      | Alice    |

---

### **SQL Equivalent**

Set difference in relational algebra corresponds to the `EXCEPT` clause in SQL:

```sql
SELECT ID, Name
FROM R
EXCEPT
SELECT ID, Name
FROM S;
```

---

### **Use Cases**

1. **Exclusive Records:** Find data present in one dataset but not in another (e.g., customers who have made purchases but haven't subscribed to a newsletter).
2. **Error Checking:** Identify discrepancies between two datasets.
3. **Set-Theoretic Operations:** Used in database queries requiring comparison of two sets of records.

---

### **Limitations**

1. **Union Compatibility Required:** The operation fails if the relations do not have the same schema.
2. **No Attribute Renaming:** If attributes differ in name but have the same domain, they must first be renamed (using the \( \rho \) operator) to make the relations compatible.

---

### **Combination Example**

Find students enrolled in sports but not music, and project their names:

1. **Relational Algebra:**  
   \( \pi\_{Name}(R - S) \)

2. **SQL Equivalent:**
   ```sql
   SELECT Name
   FROM R
   EXCEPT
   SELECT Name
   FROM S;
   ```

## Union in Relational Algebra

**Union**, denoted by \( R \cup S \), is a **binary operation** in relational algebra that combines tuples from two relations into a single relation, removing duplicates. It includes all tuples that are present in either of the two input relations.

---

### **Definition**

- **Syntax:** \( R \cup S \)
  - \( R \): The first relation.
  - \( S \): The second relation.
- **Output:** A new relation containing all tuples that are in \( R \), in \( S \), or in both, with duplicates removed.

---

### **Key Characteristics**

1. **Set-Based Operation:** The result follows the properties of a set, meaning no duplicate tuples are included.
2. **Union Compatibility:** For \( R \cup S \) to be valid:
   - Both \( R \) and \( S \) must have the same number of attributes.
   - The domains of the corresponding attributes in \( R \) and \( S \) must match.
3. **Order Independence:** The output relation does not guarantee any specific order of tuples.

---

### **Example**

Consider two relations:

**R (Students in Sports Club)**  
| **ID** | **Name** |  
|--------|----------|  
| 1 | Alice |  
| 2 | Bob |

**S (Students in Music Club)**  
| **ID** | **Name** |  
|--------|----------|  
| 2 | Bob |  
| 3 | Charlie |

#### **Union Query**

Find all students who are in either the sports club, the music club, or both:  
\( R \cup S \)

**Result:**

| **ID** | **Name** |
| ------ | -------- |
| 1      | Alice    |
| 2      | Bob      |
| 3      | Charlie  |

---

### **SQL Equivalent**

Union in relational algebra corresponds to the `UNION` clause in SQL:

```sql
SELECT ID, Name
FROM R
UNION
SELECT ID, Name
FROM S;
```

---

### **Use Cases**

1. **Merging Records:** Combine data from two or more relations with similar attributes (e.g., employees from different departments).
2. **Data Integration:** Union is useful when merging datasets from different sources.
3. **Set Operations:** Perform basic set-theoretic operations in queries.

---

### **Limitations**

1. **Union Compatibility:** Both relations must have the same schema; otherwise, attributes must be aligned using operations like renaming (\( \rho \)).
2. **No Aggregations:** Union alone cannot perform computations or transformations.

---

### **Combination Example**

Find all students from the sports and music clubs, but only return their names:

1. **Relational Algebra:**  
   \( \pi\_{Name}(R \cup S) \)

2. **SQL Equivalent:**
   ```sql
   SELECT Name
   FROM R
   UNION
   SELECT Name
   FROM S;
   ```
