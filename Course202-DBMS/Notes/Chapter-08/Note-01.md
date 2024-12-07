# Transaction

## Cascading vs. Cascadeless Schedules in DBMS

Schedules determine the execution order of operations from multiple transactions. **Cascading** and **Cascadeless schedules** differ based on how transaction failures propagate and affect other transactions.

---

### **1. Cascading Schedules**

- **Definition**: A schedule in which the failure or rollback of one transaction causes other dependent transactions to roll back.
- **Characteristics**:
  - Transactions read uncommitted changes made by other transactions.
  - If a transaction is rolled back, all transactions that read its uncommitted changes must also roll back.
  - Leads to **Cascading Rollbacks**.

#### **Example**:

- **T1**: Writes `X = 50` but does not commit.
- **T2**: Reads `X = 50` (from T1) and continues execution.
- **T1**: Fails and rolls back.
- **Result**: Since T2 used uncommitted data from T1, T2 must also roll back.

#### **Problems with Cascading Schedules**:

1. Increased overhead due to rollbacks.
2. Complex recovery process.
3. Greater risk of data inconsistency.

---

### **2. Cascadeless Schedules**

- **Definition**: A schedule where a transaction can only read data that has been committed by other transactions. This eliminates the possibility of cascading rollbacks.
- **Characteristics**:
  - Transactions are not dependent on uncommitted changes from other transactions.
  - Simpler recovery process.
  - Guarantees data consistency.

#### **Example**:

- **T1**: Writes `X = 50` but does not commit.
- **T2**: Waits for T1 to commit before reading `X`.
- **Result**: Even if T1 fails and rolls back, T2 is unaffected since it has not yet accessed `X`.

#### **Advantages of Cascadeless Schedules**:

1. Eliminates cascading rollbacks.
2. Reduces recovery overhead.
3. Ensures consistency more effectively.

---

### **Key Differences**

| **Feature**               | **Cascading Schedule**                         | **Cascadeless Schedule**                     |
| ------------------------- | ---------------------------------------------- | -------------------------------------------- |
| **Read Uncommitted Data** | Allowed.                                       | Not allowed.                                 |
| **Rollback Propagation**  | Rollback of one transaction may affect others. | Rollback does not affect other transactions. |
| **Recovery Complexity**   | Complex due to cascading rollbacks.            | Simpler due to isolation of transactions.    |
| **Performance**           | Can be faster but riskier.                     | Safer but might require waiting for commits. |

---

### **Choosing Between Cascading and Cascadeless Schedules**

- **Cascadeless schedules** are preferred for systems where:

  - High consistency and reliability are critical.
  - Transactions are long-running and interdependent.

- **Cascading schedules** might be acceptable in systems prioritizing performance over strict consistency, provided recovery mechanisms are robust.

In modern databases, techniques like **Strict Two-Phase Locking (Strict 2PL)** and **MVCC (Multi-Version Concurrency Control)** are often used to enforce cascadeless schedules and maintain data integrity.

## Introduction to Serializability in Transactions

Serializability is a key concept in database management systems (DBMS) that ensures **concurrent execution of transactions** maintains data consistency. It is used to validate schedules (sequence of operations) in concurrent systems by determining if their outcome is equivalent to executing the transactions sequentially.

---

### **Why is Serializability Important?**

- In a multi-transaction environment, transactions can overlap to improve performance.
- Ensures that concurrent transactions do not lead to **data inconsistency**.
- It balances **concurrency** (better performance) and **consistency** (correct results).

---

### **Serial Schedule vs. Non-Serial Schedule**

1. **Serial Schedule**:

   - Transactions are executed one after another without overlapping.
   - Always consistent as there are no conflicts.
   - Example:
     - **T1**: Read(A), Write(A), Commit.
     - **T2**: Read(B), Write(B), Commit.

2. **Non-Serial Schedule**:
   - Transactions are executed concurrently, allowing interleaving of operations.
   - Can lead to inconsistencies unless validated for serializability.
   - Example:
     - **T1**: Read(A), **T2**: Read(B), **T1**: Write(A), **T2**: Write(B), Commit.

---

### **Serializability**

Serializability ensures that a **non-serial schedule** produces the same outcome as a serial schedule. There are two types of serializability:

1. **Conflict Serializability**:

   - A schedule is conflict serializable if it can be transformed into a serial schedule by swapping non-conflicting operations.
   - **Conflicting Operations**:
     - Access the same data item.
     - At least one operation is a **write**.
   - Example:
     - **Schedule**: T1 (Write A), T2 (Read A), T1 (Write B), T2 (Write B).
     - Conflict exists → needs validation.

2. **View Serializability**:
   - A schedule is view serializable if it produces the same **final state** as a serial schedule.
   - More general than conflict serializability, but harder to test.
   - Focuses on **read-from relationships** and **final writes**.

---

### **Transactions, Concurrency, and Control**

#### **Transactions**:

- A transaction is a unit of work that performs operations on the database.
- Must satisfy **ACID properties** (Atomicity, Consistency, Isolation, Durability).

#### **Concurrency**:

- Concurrent execution of transactions improves system performance but introduces challenges like:
  - **Lost Updates**
  - **Dirty Reads**
  - **Phantom Reads**
  - **Unrepeatable Reads**

#### **Concurrency Control**:

Mechanisms to ensure the consistency of concurrent transactions:

1. **Lock-Based Protocols**:
   - Shared Lock (Read).
   - Exclusive Lock (Write).
   - Two-Phase Locking (2PL) ensures serializability.
2. **Timestamp-Based Protocols**:
   - Assigns a timestamp to each transaction to determine execution order.
3. **Optimistic Concurrency Control**:

   - Assumes low conflict, validates serializability before committing.

4. **Validation-Based Protocols**:
   - Checks conflict only during the validation phase, ensuring no inconsistencies.

---

### **Summary**

- Serializability validates whether concurrent transactions maintain the database's consistency.
- **Serial schedules** are inherently consistent but inefficient.
- **Concurrency control techniques** ensure that non-serial schedules are serializable, maintaining consistency while improving performance.

## Conflict Equivalent Schedules

In database systems, a **schedule** represents the sequence of operations (reads and writes) from multiple transactions. A schedule is **conflict equivalent** to another if the following conditions are met:

1. **Same Operations**: The two schedules must contain the exact same operations (read and write) from the transactions.
2. **Same Order of Conflicting Operations**: The order of conflicting operations (those that access the same data item and at least one is a write) must be the same in both schedules.

---

### **Conflict in Schedules**

Two operations conflict if:

- They belong to different transactions.
- They operate on the same data item.
- At least one of them is a **write** operation.

For example:

- **T1**: Write(A)
- **T2**: Read(A)
  - These two operations **conflict** because T1 writes to A and T2 reads A.

### **Conditions for Conflict Equivalence**

Two schedules are **conflict equivalent** if:

- They involve the same **transactions** and **operations**.
- The order of **conflicting operations** is preserved between the two schedules.

This means that the two schedules can be transformed into each other by **rearranging non-conflicting operations** (those that do not operate on the same data item or at least one is not a write).

---

### **Example of Conflict Equivalent Schedules**

#### Schedule 1:

1. **T1**: Write(A)
2. **T2**: Read(A)
3. **T1**: Write(B)
4. **T2**: Write(B)

#### Schedule 2:

1. **T2**: Read(A)
2. **T1**: Write(A)
3. **T2**: Write(B)
4. **T1**: Write(B)

**Explanation**:

- In both schedules, the **conflicting operations** between **T1** and **T2** are:
  - **T1's Write(A)** and **T2's Read(A)** (conflict because of access to the same data item A).
  - **T1's Write(B)** and **T2's Write(B)** (conflict because both write to the same data item B).
- The **order of these conflicting operations** is the same in both schedules. In Schedule 1, T1’s Write(A) happens before T2’s Read(A), and in Schedule 2, T1’s Write(A) happens before T2’s Read(A).
- Hence, **Schedule 1 and Schedule 2 are conflict equivalent**.

---

### **Non-Conflict Equivalent Example**

#### Schedule 1:

1. **T1**: Write(A)
2. **T2**: Read(A)
3. **T1**: Write(B)
4. **T2**: Write(B)

#### Schedule 2:

1. **T1**: Write(A)
2. **T2**: Write(B)
3. **T1**: Write(B)
4. **T2**: Read(A)

**Explanation**:

- In **Schedule 1**, **T1's Write(A)** occurs before **T2's Read(A)**.
- In **Schedule 2**, **T2's Read(A)** occurs after **T1's Write(A)**.
- The order of conflicting operations is **changed**. In Schedule 1, **T2** reads **A** after **T1** writes it, but in Schedule 2, **T2** writes **B** before reading **A**.
- Therefore, **Schedule 1 and Schedule 2 are not conflict equivalent**.

---

### **Importance of Conflict Equivalence**

- **Conflict equivalence** is important because it helps us determine whether two schedules are **serializable**. Two schedules that are conflict equivalent will produce the same result as some serial schedule (where transactions are executed one after another).
- **Conflict serializability** relies on identifying whether non-serial schedules are conflict equivalent to a serial schedule.

---

### **Key Points**:

1. **Conflict Equivalent Schedules** maintain the order of conflicting operations.
2. **Non-conflicting operations** can be swapped freely without changing the outcome.
3. Conflict equivalence is used to **verify if a schedule is serializable**, ensuring the integrity of data when transactions execute concurrently.

## Conflict Serializability

**Conflict Serializability** is a property of a schedule that ensures the final outcome of executing multiple transactions concurrently is the same as some **serial execution** of those transactions. A schedule is **conflict serializable** if it is conflict equivalent to a **serial schedule**.

#### **Why is Conflict Serializability Important?**

- It ensures that the execution of concurrent transactions is consistent with a serial execution, which guarantees data consistency.
- Helps in maintaining the **ACID properties** (especially isolation) when transactions are executed concurrently.

---

### **Conflict Equivalent vs Conflict Serializable**

- **Conflict Equivalent**: Two schedules are conflict equivalent if they have the same operations and the same order of conflicting operations.
- **Conflict Serializable**: A schedule is conflict serializable if its conflicting operations can be rearranged (by swapping non-conflicting operations) to obtain a serial schedule.

In simple terms, a **conflict serializable** schedule can be **rearranged** into a serial schedule by swapping only non-conflicting operations.

---

### **How to Check Conflict Serializability?**

The **Precedence Graph** (also known as a **Serialization Graph**) is used to determine if a schedule is conflict serializable.

### **Precedence Graph (Serialization Graph)**

A **Precedence Graph** is a directed graph used to check if a schedule is conflict serializable. It represents **transactions** and their **dependencies** based on conflicting operations.

#### **Steps to Create a Precedence Graph**:

1. **Nodes**: Each node represents a transaction in the schedule.
2. **Edges**: Directed edges are drawn from transaction **Ti** to **Tj** if:

   - **Ti** performs a write on a data item that **Tj** later reads or writes (i.e., there is a conflict between Ti and Tj).
   - The direction of the edge indicates the order in which the transactions must be executed to preserve the conflict relationship.

   Specifically, an edge **Ti → Tj** is drawn if:

   - **Ti** writes a data item **X**, and **Tj** writes or reads **X** after **Ti**.
   - **Ti** reads **X**, and **Tj** writes **X** after **Ti**.

#### **Example**: Conflict Serializability and Precedence Graph

Consider the following schedule with **T1** and **T2**:

1. **T1**: Write(A)
2. **T2**: Read(A)
3. **T1**: Write(B)
4. **T2**: Write(B)

**Step 1**: Create the Precedence Graph:

- **T1** writes **A**, and **T2** reads **A**, so **T1 → T2** (because T2 must read A after T1 writes it).
- **T1** writes **B**, and **T2** writes **B**, so **T1 → T2** (because both write to the same item, and T2 must write B after T1).

The Precedence Graph looks like:

```
T1 → T2
```

**Step 2**: Check for Cycles:

- The graph has no cycles. A cycle in the graph would indicate that the schedule cannot be conflict serializable.

Since the graph is **acyclic**, the schedule is **conflict serializable**.

---

### **Example of Non-Conflict Serializable Schedule**

Consider the following schedule with **T1** and **T2**:

1. **T1**: Write(A)
2. **T2**: Write(A)
3. **T1**: Write(B)
4. **T2**: Write(B)

**Step 1**: Create the Precedence Graph:

- **T1** writes **A**, and **T2** writes **A**. There is a conflict, and we draw an edge **T1 → T2** or **T2 → T1**.
- **T1** writes **B**, and **T2** writes **B**. Again, we draw an edge **T1 → T2** or **T2 → T1**.

The Precedence Graph could look like either of the following:

- **T1 → T2 → T1** (if conflicting writes on **A** and **B** have circular dependencies).
- **T2 → T1 → T2** (another circular dependency).

**Step 2**: Check for Cycles:

- This graph **has a cycle**, which means that the schedule cannot be conflict serializable.

Since the graph has a **cycle**, the schedule is **not conflict serializable**.

---

### **Key Points of Conflict Serializability**:

1. **Conflict Serializable** schedules can be transformed into a serial schedule by rearranging non-conflicting operations.
2. The **Precedence Graph** helps in determining conflict serializability by checking for cycles.
3. If the Precedence Graph is **acyclic**, the schedule is **conflict serializable**.
4. **Cycle** in the Precedence Graph indicates the schedule is **not conflict serializable**.

### **Summary**

- **Conflict Serializability** ensures that concurrent transactions can be executed without violating consistency by ensuring that their operations can be reordered into a serial schedule.
- A **Precedence Graph** is a visual tool to check if a schedule is conflict serializable by looking at transaction dependencies.

## Introduction to View Serializability

**View Serializability** is a concept in database management systems (DBMS) that ensures the final outcome of a concurrent execution of transactions is equivalent to some serial execution of those transactions. Unlike **conflict serializability**, which focuses on the order of conflicting operations, **view serializability** considers the **read-from relationships** and **final writes** of data items in the schedule.

#### **Why View Serializability?**

- **Conflict serializability** is a stricter concept, ensuring that the conflicting operations in a schedule are arranged in the same order as in a serial schedule. However, **view serializability** is more general and flexible, as it allows certain non-conflicting schedules to be serializable as well.
- It focuses on the **final state** of the data rather than just the order of operations, which makes it useful in scenarios where the conflict serializability test may not be sufficient.

---

### **Key Concepts in View Serializability**

1. **Read-from Relationship**:
   - A **read-from relationship** exists when a transaction reads a value that was written by another transaction. For example, if **T2** reads data item **A** that was written by **T1**, then there is a **read-from relationship** from **T2** to **T1** for **A**.
2. **Final Write**:

   - The final write refers to the last transaction to write to a data item. This is important because, for a schedule to be view serializable, the final write in the schedule must align with the final write in the serial schedule.

3. **Schedule's View**:
   - The **view** of a schedule includes the following information:
     - **Which transaction reads which data item**.
     - **Which transaction wrote each data item**.
     - The **order** in which these operations occurred.

For a schedule to be **view serializable**, the final state of the data items (after all operations are executed) must match the final state that would have been produced by executing the transactions in some serial order.

---

### **Conditions for View Serializability**

A schedule is **view serializable** if it produces the same **final state** as a serial schedule. This requires satisfying the following conditions:

1. **Read-from consistency**:

   - If a transaction **T2** reads a data item **X** from **T1**, then the order of reading from **T1** and writing by **T1** must be preserved in both the serial and non-serial schedule. In other words, the schedule must respect the same **read-from relationships** as in a serial schedule.

2. **Final Write Consistency**:

   - The final write of each data item in a schedule must match the final write of that data item in the serial schedule. This ensures that the same final result is obtained regardless of the order in which transactions are executed.

3. **Transaction Dependencies**:
   - The schedule must maintain the dependency relationships between transactions that arise from **read-from** relationships and the **final write** to data items.

---

### **Example of View Serializability**

Let’s consider two transactions, **T1** and **T2**, and their operations:

- **T1**: Write(A)
- **T2**: Read(A), Write(B)
- **T1**: Write(B)

#### **Schedule 1:**

1. **T1**: Write(A)
2. **T2**: Read(A)
3. **T2**: Write(B)
4. **T1**: Write(B)

#### **Schedule 2:**

1. **T2**: Read(A)
2. **T1**: Write(A)
3. **T2**: Write(B)
4. **T1**: Write(B)

### **Analysis of View Serializability**:

- In **Schedule 1**, **T2** reads **A** from **T1** and writes **B** after **T1**. This schedule has the same **read-from relationship** as a serial schedule where **T1** writes **A**, followed by **T2** reading **A** and writing **B**, and finally, **T1** writes **B**.
- In **Schedule 2**, **T2** reads **A** before **T1** writes it. However, the **read-from relationship** is the same (T2 reads **A** from T1), and the final writes of **B** are consistent with a serial schedule where **T2** writes **B** after **T1** writes **A**.

Since **Schedule 1** and **Schedule 2** produce the same final outcome as a serial schedule, both are **view serializable**.

---

### **View Serializability vs Conflict Serializability**

- **Conflict Serializability** is a stricter condition. If a schedule is conflict serializable, it is also view serializable. However, the reverse is not necessarily true. A schedule can be **view serializable** but not conflict serializable.
- **View Serializability** considers **read-from relationships** and the **final state of the data**, while **conflict serializability** focuses on the **order of conflicting operations** (those accessing the same data item).

### **Checking View Serializability**

1. Identify the **read-from relationships** between transactions.
2. Ensure that the **final writes** of each data item are consistent with a serial execution.
3. Construct a **serialization graph** (similar to the Precedence Graph for conflict serializability) to ensure that the schedule’s dependencies match that of a serial execution.

---

### **Summary**

- **View Serializability** ensures that the **final state** produced by a schedule is the same as a serial execution.
- It is more flexible than conflict serializability and allows certain schedules to be serializable even if they are not conflict serializable.
- A schedule is **view serializable** if the **read-from relationships** and **final writes** are consistent with a serial schedule.
- View serializability is often harder to verify than conflict serializability but provides a broader framework for analyzing the correctness of concurrent transactions.
