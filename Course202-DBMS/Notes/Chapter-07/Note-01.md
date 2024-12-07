# Transaction

## Introduction to Transaction Concurrency in DBMS

**Transaction concurrency** in a Database Management System (DBMS) refers to the management of simultaneous transaction execution in a multi-user environment without violating the consistency, isolation, or integrity of the database. Concurrency ensures that multiple transactions can execute simultaneously while maintaining the database's correctness and preventing conflicts.

---

### **Key Concepts of Transaction Concurrency**

1. **Transaction**:

   - A transaction is a sequence of operations performed on a database, treated as a single logical unit. Transactions must satisfy the **ACID properties** (Atomicity, Consistency, Isolation, Durability).

2. **Concurrency**:
   - Concurrency occurs when two or more transactions are executed in an overlapping time frame. It improves system performance by utilizing resources efficiently.

---

### **Benefits of Concurrency**

1. **Improved Resource Utilization**:
   - Enables multiple transactions to share CPU, memory, and I/O, maximizing system throughput.
2. **Increased Throughput**:
   - Supports many users and applications accessing the database simultaneously.
3. **Reduced Waiting Time**:
   - Transactions are executed without waiting for the current one to finish entirely.

---

### **Challenges of Transaction Concurrency**

Concurrency can lead to various **problems** if not properly managed:

1. **Lost Updates**:
   - Occurs when two transactions update the same data simultaneously, and one update overwrites the other.
2. **Dirty Read**:

   - A transaction reads data that has been modified by another transaction but not yet committed.

3. **Uncommitted Dependency (Cascading Rollback)**:

   - If a transaction fails and is rolled back, other transactions depending on its updates must also roll back.

4. **Phantom Read**:
   - A transaction reads a set of rows that match a condition, but another transaction inserts/deletes rows that match the same condition, causing inconsistencies in subsequent reads.

---

### **Concurrency Control in DBMS**

Concurrency control mechanisms are implemented to address the challenges and ensure that the database operates correctly in a concurrent environment.

1. **Lock-Based Protocols**:

   - **Shared Lock (S)**: Allows multiple transactions to read a data item but prevents writing.
   - **Exclusive Lock (X)**: Prevents other transactions from reading or writing a data item.

2. **Timestamp-Based Protocols**:

   - Assigns timestamps to transactions, ensuring a serializable order of execution based on their start times.

3. **Optimistic Concurrency Control**:

   - Transactions execute without restrictions and validate data consistency before committing changes.

4. **Multiversion Concurrency Control (MVCC)**:

   - Maintains multiple versions of a data item to allow concurrent access by transactions without conflicts.

5. **Deadlock Management**:
   - Mechanisms to detect, prevent, or resolve deadlocks that arise when multiple transactions wait indefinitely for each other to release resources.

---

### **Conclusion**

Transaction concurrency is crucial for maintaining high performance and consistency in a multi-user database environment. Effective concurrency control techniques ensure data integrity, minimize conflicts, and support scalable, efficient database operations.

## ACID properties

In database systems, a **transaction** is a sequence of operations performed as a single logical unit of work. To ensure the reliability and consistency of a database, every transaction must adhere to the **ACID properties**:

---

### 1. **Atomicity**

- **Definition**: Ensures that a transaction is treated as a single, indivisible unit. Either all the operations of the transaction are completed successfully, or none are applied at all.
- **Key Point**: If any part of the transaction fails, the entire transaction is rolled back to its previous consistent state.
- **Example**:
  - In a banking system, transferring ₹500 from Account A to Account B involves two steps:
    1.  Deduct ₹500 from Account A.
    2.  Add ₹500 to Account B.
  - If the second step fails, the first step must also be undone to maintain consistency.

---

### 2. **Consistency**

- **Definition**: Ensures that a transaction brings the database from one consistent state to another consistent state, maintaining all predefined rules, constraints, and integrity.
- **Key Point**: The database should never be left in a partially updated or inconsistent state.
- **Example**:
  - A database constraint ensures that the total balance of all accounts in a bank must remain constant during a transaction. After transferring ₹500 from one account to another, the total balance remains unchanged.

---

### 3. **Isolation**

- **Definition**: Ensures that multiple transactions executing simultaneously do not interfere with each other. Each transaction should behave as if it is the only transaction running on the system.
- **Key Point**: The intermediate states of a transaction are invisible to other transactions.
- **Example**:
  - Two transactions are running:
    1.  Transaction 1 updates Account A.
    2.  Transaction 2 reads Account A.
  - Transaction 2 should either see the value of Account A before Transaction 1 starts or after Transaction 1 completes, but not an intermediate value.

---

### 4. **Durability**

- **Definition**: Ensures that once a transaction is committed, its changes are permanently saved in the database, even in the event of a system crash or power failure.
- **Key Point**: Committed transactions survive system failures.
- **Example**:
  - After transferring ₹500 from Account A to Account B, the changes remain in the database, even if the system crashes immediately after the commit.

---

### **Summary**

| Property        | Ensures                                                          |
| --------------- | ---------------------------------------------------------------- |
| **Atomicity**   | All-or-nothing execution of transactions.                        |
| **Consistency** | Database remains in a valid state before and after transactions. |
| **Isolation**   | Transactions execute without interfering with each other.        |
| **Durability**  | Committed transactions persist permanently, even after failures. |

The ACID properties form the foundation of reliable transaction processing in database systems, ensuring data integrity and consistency in multi-user environments.

## Transaction States in DBMS

In a Database Management System (DBMS), a **transaction** goes through several states during its lifecycle. These states represent the stages of execution, from initiation to completion or failure. The main transaction states are:

---

### **1. Active State**

- **Description**: The transaction begins its execution and is in progress. All operations, such as read and write, are being performed on the database.
- **Key Point**:
  - The transaction can move to the next state or terminate due to failure.
- **Example**: A banking transaction starts with transferring money between accounts.

---

### **2. Partially Committed State**

- **Description**: After the final operation of the transaction is executed, it enters this state. It signifies that all the instructions of the transaction have been executed, but the changes are not yet permanent.
- **Key Point**:
  - The transaction is still not guaranteed to commit, as system failures may occur before changes are saved.
- **Example**: Completing the money deduction step in a transfer, but before the addition step is made permanent.

---

### **3. Committed State**

- **Description**: When all the operations of the transaction are successfully executed and the changes are permanently saved in the database, the transaction enters the committed state.
- **Key Point**:
  - Once committed, the transaction's results are durable and visible to other transactions.
- **Example**: Both deduction and addition in a money transfer are finalized, and the changes are saved.

---

### **4. Failed State**

- **Description**: If a transaction cannot be completed due to an error, crash, or failure, it enters the failed state. This means the transaction cannot proceed further.
- **Key Point**:
  - The database remains unaffected by partially executed operations due to rollback mechanisms.
- **Example**: Insufficient funds in Account A during a transfer cause the transaction to fail.

---

### **5. Aborted State**

- **Description**: If a transaction fails, the system ensures that all its changes are undone (rolled back), and the database is restored to its original state before the transaction started.
- **Key Point**:
  - After rolling back, the transaction is terminated, and it may be restarted if needed.
- **Example**: The rollback of a failed money transfer restores the initial balances of both accounts.

---

### **State Transition Diagram**

The lifecycle of a transaction can be represented as follows:

```
Start --> Active --> Partially Committed --> Committed
         |                   |
         |                   V
         ------> Failed --> Aborted
```

---

### **Key Transitions**

1. **Active → Partially Committed**: After all operations are executed.
2. **Partially Committed → Committed**: When changes are saved permanently.
3. **Active → Failed**: On encountering an error.
4. **Failed → Aborted**: When the transaction is rolled back.
5. **Aborted → Active**: If the transaction is restarted.

Understanding transaction states is crucial for ensuring reliable database operations, especially in multi-user and concurrent environments.

### **What is a Schedule in DBMS?**

A **schedule** in a DBMS is an arrangement of the operations (such as `read` and `write`) from multiple transactions, interleaved in a way that ensures the database's consistency and satisfies the **ACID properties**. It defines the order in which operations of concurrent transactions are executed.

---

### **Types of Schedules**

Schedules can be broadly categorized into two types based on their execution style: **Serial Schedules** and **Parallel Schedules**.

---

### **1. Serial Schedule**

- **Definition**: A schedule where transactions are executed one after another without overlapping or interleaving operations from different transactions.
- **Key Characteristics**:
  - Only one transaction is active at any point in time.
  - Transactions are executed sequentially.
  - The database remains consistent as there is no interference between transactions.
- **Example**:

  - Transaction T1: `read(A), write(A)`
  - Transaction T2: `read(B), write(B)`
  - Serial Execution: T1 completes all its operations before T2 begins.

  ```
  T1: read(A) → write(A)
  T2: read(B) → write(B)
  ```

- **Advantages**:
  - Simple and easy to implement.
  - Guarantees consistency since there are no conflicts.
- **Disadvantages**:
  - Inefficient in multi-user environments as it does not utilize concurrency.

---

### **2. Parallel (Concurrent) Schedule**

- **Definition**: A schedule where operations from multiple transactions are interleaved, and transactions are executed concurrently.
- **Key Characteristics**:
  - Transactions overlap in execution.
  - Proper concurrency control mechanisms are required to avoid conflicts and maintain database consistency.
- **Example**:

  - Transaction T1: `read(A), write(A)`
  - Transaction T2: `read(B), write(B)`
  - Parallel Execution:
    ```
    T1: read(A)
    T2: read(B)
    T1: write(A)
    T2: write(B)
    ```

- **Advantages**:
  - Utilizes resources efficiently.
  - Improves system throughput and performance.
- **Disadvantages**:
  - Risk of concurrency problems like **dirty reads**, **lost updates**, or **non-repeatable reads**.
  - Requires additional overhead for concurrency control mechanisms.

---

### **Comparison: Serial vs Parallel Schedule**

| Feature                | Serial Schedule                    | Parallel Schedule                      |
| ---------------------- | ---------------------------------- | -------------------------------------- |
| **Execution**          | Transactions execute sequentially. | Transactions execute concurrently.     |
| **Concurrency**        | No concurrency.                    | High concurrency.                      |
| **Consistency**        | Easy to maintain.                  | Requires concurrency control.          |
| **Performance**        | Slower due to no parallelism.      | Faster due to efficient resource use.  |
| **Conflict Potential** | None, as there’s no interleaving.  | Potential conflicts if not controlled. |

---

### **Key Insight**

Both types of schedules aim to ensure that the database remains consistent. However, **parallel schedules** are more common in multi-user systems as they enhance performance, provided that appropriate **concurrency control mechanisms** (like locking or timestamping) are in place to prevent conflicts.

## Concurrency Problems in DBMS

Concurrency issues arise when multiple transactions are executed simultaneously without proper synchronization, leading to inconsistencies in the database. The major concurrency problems are:

---

### **1. Dirty Read**

- **Definition**: Occurs when a transaction reads data that has been modified by another transaction but not yet committed. If the modifying transaction is rolled back, the reading transaction will have used invalid or inconsistent data.
- **Example**:
  - **Transaction T1**: Updates `Account A` balance from ₹5000 to ₹4000 (but not committed).
  - **Transaction T2**: Reads the updated balance of ₹4000.
  - **T1** rolls back, reverting `Account A` balance to ₹5000.
  - **Problem**: T2 acted on incorrect data.
- **Impact**: Leads to incorrect decisions or computations.

---

### **2. Incorrect Summary**

- **Definition**: Occurs when one transaction is computing an aggregate summary while another transaction is modifying the data being summarized. This results in incorrect or inconsistent aggregate values.
- **Example**:
  - **Transaction T1**: Calculates the total balance of all bank accounts.
  - **Transaction T2**: Adds ₹1000 to an account being summarized by T1.
  - T1 might include the addition partially or miss it altogether, leading to an incorrect total.
- **Impact**: Summaries or reports generated during such operations can be invalid.

---

### **3. Lost Update**

- **Definition**: Occurs when two or more transactions read and update the same data item, and the update from one transaction overwrites the update from another, resulting in a loss of one of the updates.
- **Example**:
  - Initial `Account A` balance = ₹5000.
  - **Transaction T1**: Withdraws ₹1000. (`New balance = ₹4000`).
  - **Transaction T2**: Deposits ₹2000. (`New balance = ₹7000`).
  - Both T1 and T2 read the initial balance of ₹5000. T1 writes ₹4000, and T2 writes ₹7000, overwriting T1's update.
- **Impact**: T1's update is lost, leading to data inconsistency.

---

### **4. Phantom Read**

- **Definition**: Occurs when a transaction reads a set of rows that satisfy a condition, but another transaction inserts, updates, or deletes rows that affect the result of the first transaction's query during its execution.
- **Example**:
  - **Transaction T1**: Reads all employees with salaries greater than ₹50,000.
  - **Transaction T2**: Inserts a new employee with a salary of ₹55,000 during T1's execution.
  - T1 re-executes the query and sees different results.
- **Impact**: Leads to inconsistent query results.

---

### **Comparison of Concurrency Problems**

| Problem               | Cause                                                    | Example Impact                                      |
| --------------------- | -------------------------------------------------------- | --------------------------------------------------- |
| **Dirty Read**        | Reading uncommitted changes from another transaction.    | Decisions based on uncommitted or rolled-back data. |
| **Incorrect Summary** | Simultaneous updates during an aggregate computation.    | Inaccurate totals or reports.                       |
| **Lost Update**       | Overwriting updates from concurrent transactions.        | Data updates are lost, causing inconsistency.       |
| **Phantom Read**      | Changes in query results due to concurrent transactions. | Inconsistent query outputs or views.                |

---

### **Preventing Concurrency Problems**

Concurrency problems can be mitigated by using **Concurrency Control Techniques**:

1. **Locking Protocols**:
   - Shared and exclusive locks.
   - Strict two-phase locking (2PL).
2. **Timestamp Ordering**:
   - Transactions execute in the order of their timestamps.
3. **Multiversion Concurrency Control (MVCC)**:
   - Maintains multiple versions of data to allow consistent reads.
4. **Isolation Levels**:
   - Define the degree of concurrency and consistency:
     - Read Uncommitted (allows dirty reads).
     - Read Committed (prevents dirty reads).
     - Repeatable Read (prevents lost updates and dirty reads).
     - Serializable (prevents all concurrency problems).

Proper implementation of these mechanisms ensures data consistency, integrity, and reliability in a multi-transaction environment.

## Irrecoverable vs. Recoverable Schedules in Transactions

In a database system, **schedules** determine the sequence of operations from multiple transactions. The distinction between **recoverable** and **irrecoverable schedules** relates to whether or not a system can recover from a failure without violating data consistency.

---

### **1. Irrecoverable Schedules**

- **Definition**: A schedule where a transaction commits before another transaction, from which it has read uncommitted data, either commits or aborts.
- **Key Problem**: If the first transaction (which provided uncommitted data) aborts after the second transaction commits, the database cannot be rolled back to a consistent state.
- **Characteristics**:
  - Transactions depend on uncommitted changes from other transactions.
  - Cannot ensure data consistency after a failure.
- **Example**:
  - **Transaction T1** writes `A=50` but does not commit.
  - **Transaction T2** reads `A=50` and commits.
  - T1 later aborts.
  - **Result**: T2's committed changes are based on invalid data, making recovery impossible.
- **Impact**: Leads to permanent inconsistency in the database.

---

### **2. Recoverable Schedules**

- **Definition**: A schedule where a transaction commits only after ensuring that any transaction from which it has read uncommitted data also commits.
- **Key Advantage**: Ensures that the database can recover to a consistent state even if a failure occurs.
- **Characteristics**:
  - Ensures dependencies between transactions are properly managed.
  - Maintains data integrity and consistency.
- **Example**:
  - **Transaction T1** writes `A=50` but does not commit.
  - **Transaction T2** reads `A=50` but waits for T1 to commit before committing itself.
  - T1 commits successfully.
  - **Result**: T2's commit is valid because it depends on committed data.
- **Impact**: The database can always recover from failures.

---

### **Key Differences**

| **Feature**              | **Irrecoverable Schedule**                 | **Recoverable Schedule**                       |
| ------------------------ | ------------------------------------------ | ---------------------------------------------- |
| **Definition**           | Commit happens before dependencies commit. | Commit happens only after dependencies commit. |
| **Recovery Feasibility** | Cannot recover without inconsistency.      | Can recover without inconsistency.             |
| **Consistency**          | May violate data consistency.              | Ensures data consistency.                      |
| **Use in Systems**       | Rarely allowed due to risks.               | Preferred for ensuring reliability.            |

---

### **Why Use Recoverable Schedules?**

Recoverable schedules are essential in practical database systems because they:

1. Prevent cascading aborts.
2. Ensure data consistency after failures.
3. Maintain the integrity of inter-transaction dependencies.

Irrecoverable schedules, on the other hand, are considered unsafe and are avoided in real-world systems.
