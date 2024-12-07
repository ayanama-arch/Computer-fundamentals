# Transaction

## Shared-Exclusive Locking Protocol

The **Shared-Exclusive Locking Protocol** is a concurrency control mechanism used in database management systems (DBMS) to manage access to data items during transaction execution. It helps in maintaining the **ACID properties** (specifically, **Isolation**) by ensuring that multiple transactions do not conflict while accessing the same data item simultaneously.

#### **Lock Types in the Shared-Exclusive Protocol**

1. **Shared Lock (S Lock)**:

   - A **Shared Lock** allows a transaction to **read** a data item. Multiple transactions can hold **shared locks** on the same data item simultaneously, which allows **concurrent reads** of that data item.
   - However, no transaction can write to the data item while any other transaction holds a shared lock.

2. **Exclusive Lock (X Lock)**:
   - An **Exclusive Lock** allows a transaction to **write** to a data item. When a transaction holds an exclusive lock on a data item, no other transaction can read or write to that data item. In other words, it **excludes** other transactions from accessing the data item.

#### **Rules of the Shared-Exclusive Locking Protocol**

The Shared-Exclusive Locking Protocol operates based on the following rules:

1. **Shared Lock (S) Compatibility**:

   - If a transaction holds a shared lock on a data item, other transactions can also hold shared locks on that same data item.
   - Multiple **S Locks** can be held concurrently by different transactions on the same data item.
   - However, no transaction can acquire an **exclusive lock** (X) on the data item while shared locks are held.

2. **Exclusive Lock (X) Exclusivity**:

   - If a transaction holds an exclusive lock on a data item, no other transaction can acquire any lock (shared or exclusive) on that same data item.
   - A transaction must hold the exclusive lock in order to modify (write) the data item.

3. **Lock Upgrade**:
   - A transaction can request a **lock upgrade** from a shared lock to an exclusive lock if it intends to write to the data item.
   - This may lead to potential deadlock situations if another transaction holds a shared lock on the same data item.

#### **Lock Compatibility Table**

The following table summarizes the lock compatibility for the **Shared-Exclusive Locking Protocol**:

| Lock on Data Item      | Shared Lock (S) | Exclusive Lock (X) |
| ---------------------- | --------------- | ------------------ |
| **Shared Lock (S)**    | Yes (Multiple)  | No                 |
| **Exclusive Lock (X)** | No              | No                 |

- **Yes** means that the lock request is allowed.
- **No** means that the lock request is not allowed due to conflict.

#### **Example**

Consider two transactions, **T1** and **T2**, and a data item **A**.

1. **Scenario 1: Shared Locking**

   - **T1** acquires a shared lock on **A** (S).
   - **T2** also acquires a shared lock on **A** (S).
   - Both transactions can read **A** simultaneously because shared locks are compatible.

2. **Scenario 2: Exclusive Locking**

   - **T1** acquires an exclusive lock on **A** (X).
   - **T2** tries to acquire a shared lock on **A** (S), but it is **denied** because **T1** holds an exclusive lock on **A**.
   - **T2** also cannot acquire an exclusive lock on **A** because **T1** already holds the exclusive lock.

3. **Scenario 3: Lock Upgrade**
   - **T1** holds a shared lock on **A** (S) and now wants to write to **A**.
   - **T1** attempts to upgrade its lock to an exclusive lock (X). However, if **T2** is also holding a shared lock on **A**, **T1** will be **blocked** until **T2** releases the shared lock.

#### **Deadlocks in Shared-Exclusive Locking**

Deadlocks can occur when two or more transactions are waiting for locks in a way that causes a cycle. For example:

1. **T1** holds a shared lock on data item **A** and requests an exclusive lock.
2. **T2** holds a shared lock on data item **B** and requests an exclusive lock.
3. If **T1** needs a shared lock on **B** and **T2** needs a shared lock on **A**, both transactions are blocked, resulting in a **deadlock**.

To avoid deadlocks, DBMSs use techniques like **timeout** and **deadlock detection** to break the cycle.

---

### **Advantages of the Shared-Exclusive Locking Protocol**

1. **Concurrency**: It allows multiple transactions to read the same data item concurrently, which increases the level of parallelism in the system and improves throughput.
2. **Isolation**: By restricting concurrent writes, the protocol ensures that data consistency is maintained while providing isolation between transactions.
3. **Simplicity**: The protocol is easy to implement and understand, especially for scenarios where multiple transactions need to read the same data item without interfering with each other.

### **Disadvantages of the Shared-Exclusive Locking Protocol**

1. **Limited Concurrency for Writes**: Since an exclusive lock cannot coexist with any other lock (including shared locks), it reduces concurrency when transactions need to perform writes.
2. **Potential for Deadlocks**: As mentioned earlier, the protocol can lead to deadlocks, especially when transactions need to upgrade from shared to exclusive locks or when they hold shared locks on conflicting data items.
3. **Locking Overhead**: The management of locks (granting, upgrading, and releasing) introduces some overhead, particularly in high-concurrency environments.

---

### **Summary**

The **Shared-Exclusive Locking Protocol** is a concurrency control mechanism in DBMS that allows transactions to either **read** a data item (using a shared lock) or **write** to it (using an exclusive lock). It ensures that multiple transactions can read the same data item simultaneously but prevents concurrent writes. The protocol is simple to implement and helps achieve isolation but can lead to issues like deadlocks and reduced concurrency for write operations.

### **2-Phase Locking (2PL) Protocol in Transaction Concurrency Control**

The **2-Phase Locking Protocol** (2PL) is a concurrency control protocol used in **database management systems (DBMS)** to ensure that **transactions** are executed in a serializable manner. It is one of the most widely used techniques to maintain the **ACID properties**, particularly **Isolation**. The main goal of 2PL is to control the order of lock acquisition and release during the execution of transactions, preventing conflicts and ensuring consistency in concurrent transaction execution.

#### **Overview of 2-Phase Locking**

The **2-Phase Locking Protocol** guarantees **serializability** of transactions by requiring that:

- **Phase 1**: **Growing Phase** - A transaction can acquire locks but cannot release any lock.
- **Phase 2**: **Shrinking Phase** - A transaction can release locks but cannot acquire any new locks.

In other words, once a transaction starts releasing locks, it is not allowed to acquire any new locks.

#### **The Two Phases of 2PL**

1. **Growing Phase**:

   - During the **growing phase**, a transaction can acquire locks on data items, but it cannot release any locks.
   - In this phase, the transaction "grows" its set of locks.

2. **Shrinking Phase**:
   - After the transaction has released its first lock, it enters the **shrinking phase**.
   - During the shrinking phase, the transaction can only release locks, but it cannot acquire any new locks.
   - Once the transaction releases a lock, it can no longer acquire new locks.

This two-phase approach ensures that transactions do not interfere with each other in a way that could cause inconsistent results or violations of isolation.

---

### **How 2PL Ensures Serializability**

The 2PL protocol ensures **serializability**, which is the highest level of transaction isolation, by avoiding issues like **conflicts** or **inconsistent reads**. The protocol prevents **cyclic dependencies** (which could lead to deadlocks) between transactions by requiring that once a transaction starts releasing locks, it cannot acquire any more. This ensures that there is a clear and consistent order of operations for transactions, which can be serialized.

In simpler terms, 2PL guarantees that the transactions' outcomes are equivalent to a serial execution of the transactions (where transactions are executed one after the other without overlapping).

#### **Example of 2PL Protocol**

Consider two transactions **T1** and **T2** accessing data items **A** and **B**.

- **T1**: Wants to read **A** and write **B**.
- **T2**: Wants to write **A** and read **B**.

**T1** can:

1. Acquire a shared lock on **A**.
2. Acquire an exclusive lock on **B**.

**T2** can:

1. Acquire a shared lock on **B**.
2. Try to acquire an exclusive lock on **A**, but will be blocked until **T1** releases the locks on **A** and **B**.

In this case, if both transactions follow the 2PL protocol:

- **T1** enters the **growing phase** and locks **A** and **B**.
- After completing its operations, **T1** enters the **shrinking phase** and releases its locks on **A** and **B**.
- **T2**, which is in the growing phase, will eventually acquire its locks once **T1** releases its locks.

### **Strict 2PL and Conservative 2PL**

There are two variations of the basic 2PL protocol:

1. **Strict 2PL**:
   - In **Strict 2PL**, a transaction holds all its locks until it **commits** or **aborts**.
   - This ensures that no other transaction can access a data item that is locked by an uncommitted transaction.
   - Strict 2PL is more rigid and guarantees **serializability** and **recoverability** (transactions can be rolled back in case of failure).
2. **Conservative 2PL**:
   - In **Conservative 2PL**, a transaction locks all the data items it needs at the start and does not release any locks until it completes its operations.
   - It is less commonly used because it may block other transactions for a longer time, causing poor concurrency.

---

### **Advantages of 2PL**

1. **Guarantees Serializability**:

   - The primary benefit of 2PL is that it guarantees **serializability**, which is the highest standard of transaction isolation. This ensures that the results of transactions are consistent and that concurrent transactions behave as though they were executed sequentially.

2. **Prevents Conflicts**:

   - By controlling when locks can be acquired and released, 2PL prevents conflicting operations, such as a transaction reading a value that another transaction is concurrently updating.

3. **Widely Adopted**:
   - 2PL is widely used in database systems to provide **isolation** without sacrificing performance too much.

---

### **Disadvantages of 2PL**

1. **Deadlocks**:

   - The 2PL protocol does not guarantee the absence of **deadlocks**. Deadlocks can occur if two transactions hold locks and wait indefinitely for each other’s locks to be released.
   - For example, if **T1** holds a lock on **A** and waits for a lock on **B**, while **T2** holds a lock on **B** and waits for a lock on **A**, a deadlock occurs.

2. **Blocking**:

   - Because 2PL restricts the acquisition of new locks once the transaction starts releasing them, it can lead to increased **blocking** of other transactions, reducing overall system throughput and concurrency.

3. **Performance Overhead**:

   - The protocol may cause a significant performance hit, especially when many transactions are competing for the same resources, as transactions are forced to wait for locks to be released.

4. **Starvation**:
   - Starvation can occur if a transaction is blocked for a long period, particularly in high-concurrency environments, because transactions are forced to wait for locks to be released.

---

### **Deadlock and Deadlock Prevention in 2PL**

To handle **deadlocks**, databases often implement strategies such as:

1. **Deadlock Detection**:

   - The system periodically checks for cycles in the transaction graph and resolves deadlocks by aborting one of the transactions involved.

2. **Timeouts**:

   - Transactions are timed out if they are waiting for a lock too long, and the transaction is aborted or rolled back to prevent a deadlock.

3. **Wait-Die and Wound-Wait Schemes**:
   - These schemes help to prioritize which transaction should be aborted to resolve deadlocks, based on transaction timestamps.

---

### **Summary**

The **2-Phase Locking Protocol** is a concurrency control mechanism used in DBMS to ensure **serializability** of transactions by enforcing two distinct phases for each transaction: the **growing phase** (where locks can only be acquired) and the **shrinking phase** (where locks can only be released). While 2PL guarantees serializability, it can suffer from **deadlocks**, **blocking**, and **performance overhead**. Despite these challenges, 2PL is a foundational concept for transaction concurrency control in many database systems.

## Strict 2PL, Rigorous 2PL, and Conservative 2PL

The **2-Phase Locking (2PL) Protocol** is a fundamental concurrency control technique used in database management systems (DBMS) to ensure **serializability** of transactions. However, there are variations of 2PL that impose different levels of constraints on transaction behavior, primarily in terms of lock acquisition and release. These variations are:

1. **Strict 2PL**
2. **Rigorous 2PL**
3. **Conservative 2PL**

Each variation has its own rules and implications for transaction concurrency and isolation. Let's break down each one in detail.

---

### **1. Strict 2PL (Strict Two-Phase Locking)**

**Strict 2PL** is a more rigid form of the **2PL protocol** where transactions are required to hold all their locks until **commitment** or **abortion**. Once a transaction has acquired locks, it must hold them until it has completed all its operations and is about to **commit** or **abort**.

#### **Rules of Strict 2PL**:

- A transaction can acquire and hold locks during the **growing phase**.
- The transaction enters the **shrinking phase** only after it has released its first lock.
- **Critical Rule**: A transaction **must not release any lock** until it has finished all its operations and is about to commit or abort. Once the transaction releases a lock, it cannot acquire any new locks.

#### **Advantages**:

- **No Cascading Aborts**: Strict 2PL ensures **recoverability** because transactions that are still active are not allowed to release any locks before they are finished. Thus, the system can guarantee that any transaction aborted will not lead to cascading aborts.
- **Serializability**: Strict 2PL guarantees **serializability** because once a transaction releases its first lock, it cannot acquire any more locks, preventing conflicts that might violate serializability.

#### **Disadvantages**:

- **Blocking**: Since transactions hold all locks until commit, **other transactions** may be blocked for long periods, particularly in highly concurrent systems.
- **Reduced Concurrency**: The requirement to hold locks until commit reduces the level of concurrency and can affect the overall performance of the system.

---

### **2. Rigorous 2PL (Rigorous Two-Phase Locking)**

**Rigorous 2PL** is a stricter version of **Strict 2PL**. In this protocol, a transaction holds all its locks not just until commit, but **even after committing**. This means that a transaction that commits must **still retain all its locks** until it **releases them explicitly**.

#### **Rules of Rigorous 2PL**:

- A transaction acquires locks during the **growing phase**.
- During the **shrinking phase**, a transaction can release locks, but it **must not release any lock** until the transaction has committed.
- After the transaction commits, it **still holds all its locks** until it releases them explicitly.

#### **Advantages**:

- **Strict Recoverability**: Since transactions hold all locks until they release them, **rigorous 2PL** provides better **recoverability** compared to strict 2PL, reducing the chances of cascading aborts even further.
- **Enhanced Serializability**: It guarantees serializability and avoids conflicts between transactions.

#### **Disadvantages**:

- **More Blocking**: Transactions that are committed but still hold locks can block other transactions, especially in systems with high contention for data.
- **Performance Issues**: The lock retention after commit can reduce concurrency and degrade the overall performance of the system.

---

### **3. Conservative 2PL (Conservative Two-Phase Locking)**

**Conservative 2PL** is the most restrictive of the three protocols. In this variation, a transaction must **acquire all the locks it needs at the beginning** before performing any operations. Once all locks are acquired, the transaction can proceed with its operations and eventually release them after completing the task.

#### **Rules of Conservative 2PL**:

- A transaction **must acquire all locks** it will need before starting any operation (this means before it reads or writes any data).
- After acquiring the required locks, the transaction can perform its operations and must not acquire any new locks.
- Once the transaction finishes its operations, it enters the **shrinking phase** and releases the locks.

#### **Advantages**:

- **Guaranteed Serializability**: Since all the locks are acquired upfront and no new locks can be requested once the transaction begins, the system can guarantee serializability.
- **No Deadlocks**: Because all locks are acquired before operations begin, **deadlock prevention** is inherent in the protocol. Since transactions never wait for additional locks, cycles of waiting cannot occur.
- **Simplified Transaction Management**: The protocol makes it simpler to manage transactions since there is no need for dynamic lock management once the transaction starts.

#### **Disadvantages**:

- **Reduced Concurrency**: Since a transaction must acquire all locks at the beginning, it may block other transactions for a long time, leading to reduced system concurrency.
- **Potential for Long Waits**: If a transaction cannot acquire all the locks it needs (due to other transactions holding those locks), it must wait until all locks become available, leading to potentially long delays.
- **Poor Resource Utilization**: Since all locks are acquired upfront, some resources may remain locked and unused for a long time, which leads to inefficient use of system resources.

---

### **Comparison Summary**

| **Property**                  | **Strict 2PL**                              | **Rigorous 2PL**                                                | **Conservative 2PL**                                    |
| ----------------------------- | ------------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------------- |
| **Lock Acquisition**          | Locks acquired during growing phase         | Locks acquired during growing phase                             | Locks acquired before any operations                    |
| **Lock Release**              | Locks released only after commit            | Locks released after commit but retained until explicit release | Locks released after operations                         |
| **Lock Holding after Commit** | Not held after commit                       | Held until explicit release                                     | Not held after operation begins                         |
| **Deadlock**                  | Possible, but can be managed                | Less likely, since locks are held until commit                  | None (due to acquiring all locks upfront)               |
| **Concurrency**               | High, but may be blocked by long-held locks | Lower, as commits retain locks for longer                       | Lower due to upfront lock acquisition                   |
| **Serializability**           | Guaranteed                                  | Guaranteed                                                      | Guaranteed                                              |
| **Recovery**                  | Recoverable                                 | Highly recoverable                                              | Not easily recoverable if aborts occur during lock wait |

---

### **Conclusion**

- **Strict 2PL**: Guarantees serializability and recoverability, but can result in high contention for locks and blocking, especially in systems with high concurrency.
- **Rigorous 2PL**: A stricter version of Strict 2PL, providing even more strict recoverability but at the cost of potential performance issues due to long lock retention.
- **Conservative 2PL**: The most restrictive protocol, guaranteeing no deadlocks and serializability, but at the expense of concurrency and resource utilization efficiency. It may be ideal in situations where **deadlock prevention** is crucial, and performance is not the main concern.

Each of these variations of **2-Phase Locking** has its strengths and trade-offs, and the choice between them depends on the specific requirements of the application, such as **performance**, **transaction isolation**, **deadlock handling**, and **resource management**.

## Basic Timestamp Ordering Protocol

The **Basic Timestamp Ordering Protocol** is a concurrency control mechanism used in database management systems (DBMS) to ensure **serializability** of transactions. It is based on the concept of **timestamps**, which are assigned to transactions at the time they start. This protocol prevents conflicts by ordering transactions according to their timestamps and ensuring that conflicting operations on data are executed in the correct order.

### **Key Concepts**:

1. **Timestamp**: Each transaction is assigned a unique timestamp when it starts. The timestamp typically reflects the **system time** or a **logical counter** that is incremented with each new transaction. This timestamp is used to order the transactions.
2. **Transaction Ordering**: The protocol enforces the following rule: for any two conflicting operations (i.e., operations that access the same data item), the operation from the transaction with the **earlier timestamp** must be executed first. This ensures that transactions are executed in the same order as they started, preserving **serializability**.

### **Steps in the Basic Timestamp Ordering Protocol**:

1. **Assigning Timestamps**:

   - Every transaction \( T \) gets a unique **timestamp** \( TS(T) \) when it is initiated.
   - \( TS(T) \) is assigned such that **earlier transactions** have smaller timestamps than **later transactions**.

2. **Transaction Actions**:
   - For each **read** or **write** operation on a data item, the system must check the timestamp of the transaction.
3. **Read Operation**:
   - A read operation on a data item \( X \) by a transaction \( T \) can proceed if **no later transaction** has written to \( X \) before \( T \)'s read operation.
   - Specifically, for a transaction \( T \) to read data item \( X \), the following must hold:
     - The last write to \( X \) must be by a transaction \( T' \) such that \( TS(T') < TS(T) \) (i.e., the write happened before the read).
4. **Write Operation**:

   - A write operation on data item \( X \) by a transaction \( T \) is allowed only if no conflicting write operation has occurred by a later transaction.
   - Specifically, for a transaction \( T \) to write to data item \( X \), the following must hold:
     - No transaction \( T' \) has read \( X \) after \( T \)'s write (\( TS(T') > TS(T) \)).
     - No transaction \( T' \) has written to \( X \) after \( T \)'s write (\( TS(T') > TS(T) \)).

5. **Conflict Resolution**:
   - If a transaction violates the above rules (e.g., a **write-write** or **read-write conflict** that violates the timestamp order), the transaction is **aborted**.
   - The aborted transaction is then rolled back, and the system retries it with a new timestamp.

### **Example**:

Assume we have two transactions, \( T_1 \) and \( T_2 \), with the following timestamps:

- \( TS(T_1) = 10 \)
- \( TS(T_2) = 20 \)

Both transactions want to access a data item \( X \).

#### Scenario 1: **Read Operation**

1. **T_1** performs a **read** on \( X \). The timestamp of **T_1** is smaller, so the read operation is allowed if **no later write** has occurred on \( X \).
2. If **T_2** tries to **read** \( X \) after **T_1**, and **T_1** has already written to \( X \), then **T_2** must wait or abort based on the protocol rules.

#### Scenario 2: **Write Operation**

1. If **T_1** writes to \( X \), the **timestamp of T_1** (i.e., 10) is used to determine if the write can happen. If a transaction with a timestamp **greater than 10** tries to write to \( X \), it will **violate serializability** and is aborted.
2. If **T_2** writes to \( X \), it must wait for any earlier transactions to complete first (in this case, **T_1**), ensuring proper ordering of actions.

---

### **Advantages of Basic Timestamp Ordering**:

- **Guaranteed Serializability**: The use of timestamps guarantees that transactions are serialized in the order they started, ensuring serializability of the execution schedule.
- **Deadlock-free**: Since transactions are not required to wait for each other (they simply abort if the order is violated), the protocol avoids deadlocks.

### **Disadvantages of Basic Timestamp Ordering**:

- **Abort and Retry**: Transactions can be aborted if they violate the timestamp order, leading to potential overhead for aborting and retrying transactions.
- **Performance Overhead**: Since each operation must be checked against the transaction timestamps, this can result in performance issues when there is a high contention for resources.
- **No Flexibility**: The protocol enforces strict ordering of transactions, which may limit flexibility in certain scenarios.

---

### **Conclusion**:

The **Basic Timestamp Ordering Protocol** is a powerful and simple concurrency control method that ensures serializability by assigning timestamps to transactions and enforcing order based on those timestamps. It guarantees a **deadlock-free** environment and **serializable** schedules, but at the cost of potentially high overhead due to transaction abortion and retrying.
