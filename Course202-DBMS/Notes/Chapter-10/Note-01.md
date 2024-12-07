# B-Tree

## Introduction to B-Tree

A **B-Tree** is a self-balancing search tree commonly used in databases and file systems to store and retrieve large amounts of data efficiently. It maintains sorted data and ensures logarithmic time complexity for operations like search, insert, and delete.

The B-Tree was introduced by Rudolf Bayer and Edward McCreight in 1972. It is an extension of binary search trees, designed to handle scenarios where data cannot fit in memory and is instead stored in external memory (like disks). The structure minimizes disk I/O operations by keeping the tree height small.

---

### **Key Properties of B-Tree**

1. **Balanced Tree**:

   - All leaves are at the same level.
   - The tree grows or shrinks from the root, ensuring balance.

2. **Multi-way Search Tree**:

   - A node can have more than two children (unlike binary search trees).

3. **Efficient Disk Access**:

   - Designed to read/write large chunks of data at once, reducing disk I/O operations.

4. **Sorted Data**:

   - Keys are stored in sorted order within each node.

5. **Logarithmic Height**:
   - For `n` keys, the height of the tree is `O(log_t n)`, where `t` is the minimum degree.

---

### **Structure of a B-Tree**

A B-Tree of order `m` (maximum number of children) has the following structural properties:

1. **Node Properties**:

   - Each node contains at most `m - 1` keys and at least `ceil(m/2) - 1` keys, except for the root, which can have fewer keys.
   - The keys within a node are stored in **sorted order**.
   - Each key in a node serves as a dividing point for the children (subtrees) of the node.

2. **Children Properties**:

   - A node with `k` keys has exactly `k + 1` children.
   - The subtree between two keys contains values that fall between those two keys.

3. **Root Properties**:

   - The root node can have a minimum of one key.

4. **Leaf Nodes**:

   - All leaf nodes are at the same level.

5. **Balanced Structure**:
   - The tree is always balanced, as all paths from the root to the leaves are of the same length.

---

### **Example of a B-Tree Structure**

#### Consider a B-Tree of order `4` (maximum 4 children per node):

- Keys: `[10, 20, 30, 40, 50, 60, 70]`

```
               [20, 40]
              /    |    \
         [10]  [30]   [50, 60, 70]
```

- The root node has two keys (`20` and `40`) and three children.
- The left child (`[10]`) contains values less than `20`.
- The middle child (`[30]`) contains values between `20` and `40`.
- The right child (`[50, 60, 70]`) contains values greater than `40`.

---

### **Operations on B-Tree**

1. **Search**:

   - Similar to a binary search but works across multiple keys in a node.
   - Navigate through the keys in the node and recurse into the appropriate child.

2. **Insertion**:

   - Insert the key in the correct node while maintaining sorted order.
   - If a node becomes overfilled (more than `m - 1` keys), split it into two nodes and promote a key to the parent.

3. **Deletion**:

   - Remove the key while ensuring structural properties.
   - May involve key redistribution from siblings or node merging.

4. **Traversal**:
   - Perform in-order traversal to retrieve all keys in sorted order.

---

### **Applications of B-Tree**

1. **Databases**:

   - Used in relational databases to store indexes (e.g., MySQL, PostgreSQL).

2. **File Systems**:

   - File systems like NTFS and EXT4 use B-Trees for directory organization.

3. **Indexing**:
   - Used in indexing large datasets due to its efficient search, insert, and delete operations.

---

### **Advantages of B-Trees**

1. Balanced structure ensures optimal performance for all operations.
2. Reduces disk I/O by grouping data into large nodes.
3. Handles large datasets efficiently.
4. Automatically adjusts its structure during insertions and deletions.

---

### **Disadvantages of B-Trees**

1. Implementation complexity compared to simpler structures like binary search trees.
2. High overhead for maintaining balance during updates.

---

In summary, B-Trees are a powerful data structure tailored for scenarios involving large datasets and disk storage, ensuring efficient and balanced operations.
