# Networking

## What is Routing Protocols

### **What Are Routing Protocols?**

**Routing protocols** are algorithms and rules used by routers to determine the best path for data packets to travel across a network. They enable routers to communicate with each other, share information about network topology, and dynamically adjust to changes in the network.

Routing protocols ensure efficient, reliable, and optimized packet delivery across interconnected networks (internetworks).

---

### **Key Functions of Routing Protocols**

1. **Path Discovery**: Identify possible routes between source and destination.
2. **Path Selection**: Choose the best route based on metrics like cost, distance, or speed.
3. **Topology Maintenance**: Update the routing table dynamically to reflect network changes (e.g., failures or new links).
4. **Packet Forwarding**: Use the routing table to forward packets along the selected path.

---

### **Types of Routing**

Routing can be broadly classified into:

1. **Static Routing**:

   - Routes are manually configured by network administrators.
   - Suitable for small, stable networks.
   - Pros: Simple, predictable.
   - Cons: Does not adapt to changes in the network.

2. **Dynamic Routing**:
   - Routes are automatically adjusted using routing protocols.
   - Suitable for large, dynamic networks.
   - Pros: Adapts to changes, scalable.
   - Cons: Requires more processing and bandwidth.

---

### **Types of Routing Protocols**

Routing protocols are classified into **interior** and **exterior** based on the area they operate.

#### **1. Interior Gateway Protocols (IGPs)**

- Used within a single autonomous system (AS).
- Examples:
  - **RIP (Routing Information Protocol)**: Distance-vector protocol, simple but less efficient.
  - **OSPF (Open Shortest Path First)**: Link-state protocol, faster convergence and scalable.
  - **EIGRP (Enhanced Interior Gateway Routing Protocol)**: Cisco proprietary, hybrid protocol with advanced features.

#### **2. Exterior Gateway Protocols (EGPs)**

- Used to route between different autonomous systems.
- Example:
  - **BGP (Border Gateway Protocol)**: Core protocol of the internet, used for inter-AS routing.

#### **3. Protocol Classification Based on Algorithm**

- **Distance-Vector Protocols**:
  - Determine routes based on distance metrics (e.g., hop count).
  - Example: RIP.
- **Link-State Protocols**:
  - Build a complete map of the network and calculate the shortest path.
  - Example: OSPF, IS-IS (Intermediate System to Intermediate System).
- **Path-Vector Protocols**:

  - Use path information instead of distance or state.
  - Example: BGP.

- **Hybrid Protocols**:
  - Combine features of distance-vector and link-state protocols.
  - Example: EIGRP.

---

### **Common Routing Protocols**

| **Protocol** | **Type**        | **Key Features**                                 |
| ------------ | --------------- | ------------------------------------------------ |
| RIP          | Distance-Vector | Simple, max 15 hops, slow convergence.           |
| OSPF         | Link-State      | Uses Dijkstra's algorithm, fast convergence.     |
| EIGRP        | Hybrid          | Efficient, supports unequal-cost load balancing. |
| BGP          | Path-Vector     | Internet's core protocol, policy-based routing.  |
| IS-IS        | Link-State      | Scalable, often used by ISPs.                    |

---

### **Key Metrics Used by Routing Protocols**

Routing protocols rely on metrics to determine the best path. Examples include:

- **Hop Count**: Number of routers a packet passes through (used by RIP).
- **Bandwidth**: Link capacity (used by OSPF, EIGRP).
- **Delay**: Time taken to traverse a path.
- **Cost**: Administratively assigned value for a route.
- **Reliability**: Historical success of a link.

---

### **Conclusion**

Routing protocols are essential for managing the flow of data across networks. They enable routers to dynamically adapt to changes, ensuring efficient and reliable communication. The choice of a routing protocol depends on the network's size, complexity, and specific requirements.

## Distance Vector Routing Algorithm

The **Distance Vector Routing Algorithm** is a simple, distributed routing protocol used in networks to find the best path to a destination. It relies on information exchanged between routers to determine the "distance" (metric) and "direction" (vector) to reach network destinations.

---

### **Key Features of Distance Vector Routing**

1. **Routing by Rumor**:

   - Each router shares its routing table with its immediate neighbors.
   - Routers only know about their neighbors and depend on neighbors' information for routes to other destinations.

2. **Metric-Based Routing**:

   - Uses metrics like **hop count**, **delay**, or **bandwidth** to determine the best route.

3. **Periodic Updates**:

   - Routing tables are updated at regular intervals or when a significant network change occurs.

4. **Routing Table Exchange**:
   - Routers exchange their routing tables with neighbors, and this information is used to update their own tables.

---

### **How Distance Vector Routing Works**

1. **Initialization**:

   - Each router initializes its routing table with a **direct cost** to its immediate neighbors.
   - For all other destinations, it sets the cost to infinity (unreachable).

2. **Exchange Updates**:

   - Routers periodically share their routing tables with neighbors.

3. **Updating Routing Tables**:

   - When a router receives a table from a neighbor, it updates its own table using the **Bellman-Ford Algorithm**:

     \[
     D(X, Y) = \min[D(X, N) + D(N, Y)]
     \]
     Where:

     - \( D(X, Y) \): Cost from router \( X \) to destination \( Y \).
     - \( D(X, N) \): Cost from \( X \) to neighbor \( N \).
     - \( D(N, Y) \): Cost from \( N \) to \( Y \) (as reported by \( N \)).

4. **Convergence**:
   - Over time, routers' tables converge to a consistent state where each router has the best path to every destination.

---

### **Example**

#### Initial Setup

Assume a network of three routers \( A \), \( B \), and \( C \):

- \( A \) is directly connected to \( B \) (cost 1) and \( C \) (cost 5).
- \( B \) is directly connected to \( A \) (cost 1) and \( C \) (cost 2).
- \( C \) is directly connected to \( A \) (cost 5) and \( B \) (cost 2).

#### Routing Table at \( A \)

| Destination | Next Hop | Cost |
| ----------- | -------- | ---- |
| \( B \)     | \( B \)  | 1    |
| \( C \)     | \( C \)  | 5    |

#### After Exchange

- \( B \) informs \( A \) that it can reach \( C \) via \( B \) with a cost of \( 2 \).
- \( A \) updates its route to \( C \) with:
  \[
  D(A, C) = D(A, B) + D(B, C) = 1 + 2 = 3
  \]

#### Updated Table at \( A \)

| Destination | Next Hop | Cost |
| ----------- | -------- | ---- |
| \( B \)     | \( B \)  | 1    |
| \( C \)     | \( B \)  | 3    |

---

### **Advantages of Distance Vector Routing**

1. **Simple Implementation**: Easy to understand and configure.
2. **Efficient for Small Networks**: Suitable for networks with fewer nodes.
3. **Dynamic Updates**: Automatically adapts to network changes.

---

### **Disadvantages of Distance Vector Routing**

1. **Slow Convergence**: Takes time to stabilize after network changes, leading to issues like routing loops.
2. **Count-to-Infinity Problem**:

   - When a link fails, incorrect information can propagate indefinitely.
   - Solutions include techniques like:
     - **Split Horizon**: Prevents sending information about a route back to the source.
     - **Route Poisoning**: Marks an unreachable route with an infinite metric.
     - **Hold-Down Timer**: Prevents updates to a route for a certain period.

3. **Limited Scalability**: Inefficient for large or complex networks.

---

### **Examples of Distance Vector Protocols**

1. **RIP (Routing Information Protocol)**:

   - Metric: Hop count.
   - Maximum hops: 15.
   - Updates every 30 seconds.

2. **EIGRP (Enhanced Interior Gateway Routing Protocol)**:
   - Metric: Bandwidth, delay, reliability.
   - Cisco proprietary, hybrid of distance vector and link state.

---

### **Conclusion**

Distance Vector Routing is a foundational routing algorithm that prioritizes simplicity and adaptability. While it's effective for small networks, its limitations, such as slow convergence and the count-to-infinity problem, make it less suitable for large-scale networks. Advanced protocols like OSPF or hybrid protocols like EIGRP address these limitations for modern networking needs.

## Count-to-Infinity Problem in Distance Vector Routing

The **Count-to-Infinity Problem** is a classic issue in **distance vector routing algorithms**, where routers continuously exchange incorrect routing information, causing routing loops and delays in convergence. It occurs when a network topology change, such as a link failure, is not correctly or quickly propagated through the network.

---

### **How the Problem Arises**

1. **Initial State**:

   - Routers share routing tables periodically with neighbors.
   - Each router maintains the distance (or metric) to every destination.

2. **Link Failure**:

   - A direct link between two routers fails.
   - The router that detects the failure updates its table and reports the destination as unreachable (or assigns it a very high cost, e.g., "infinity").

3. **Incorrect Updates Spread**:

   - Neighboring routers, unaware of the failure, continue advertising outdated routes.
   - Routers update their tables using these incorrect routes, assuming they can still reach the failed destination.

4. **Increasing Metrics**:
   - Each router adds its own cost to the reported distance from its neighbor.
   - This process continues indefinitely (or until the metric reaches a defined maximum, often 16 in RIP), creating the **count-to-infinity** problem.

---

### **Example Scenario**

#### Network Topology

- \( A \), \( B \), and \( C \) are routers.
- \( A \) connects directly to \( B \) (cost 1).
- \( B \) connects directly to \( C \) (cost 1).
- Initially, \( A \to C \) via \( B \) with cost \( 2 \).

#### Link Failure

1. Link between \( B \) and \( C \) fails.
2. \( B \) updates its table and marks \( C \) as unreachable (infinite cost).

#### Incorrect Updates

1. \( A \) still thinks \( C \) is reachable via \( B \) and advertises this route to \( B \) with cost \( 3 \).
2. \( B \), believing \( A \)'s information, updates its table to reflect \( C \)'s cost as \( 4 \) via \( A \).
3. This cycle continues, with costs incrementing until the maximum (e.g., 16) is reached.

---

### **Why It Happens**

- **Lack of Global Knowledge**:
  - Distance vector algorithms rely on local information shared between neighbors.
- **Delayed Convergence**:
  - Each router updates its table based on outdated or incorrect information from neighbors.

---

### **Solutions to Count-to-Infinity Problem**

1. **Split Horizon**:

   - Prevents a router from advertising a route back to the neighbor from which it learned the route.
   - Example: If \( A \) learned about \( C \) from \( B \), \( A \) does not advertise \( C \) to \( B \).

2. **Split Horizon with Poison Reverse**:

   - Instead of suppressing updates, the route is advertised with an "infinity" metric to explicitly indicate it is unreachable.

3. **Route Poisoning**:

   - When a route becomes unreachable, it is advertised with an infinite metric immediately, speeding up convergence.

4. **Hold-Down Timers**:

   - Prevents a router from accepting new updates for a route for a fixed duration after marking it unreachable.
   - This avoids rapid propagation of incorrect updates.

5. **Maximum Metric**:

   - A limit (e.g., 16 in RIP) is defined as "infinity."
   - The route is removed once the metric exceeds this limit, stopping the loop.

6. **Triggered Updates**:
   - Immediate updates are sent when a significant topology change occurs, reducing the time for convergence.

---

### **Protocols and the Count-to-Infinity Problem**

- **RIP** (Routing Information Protocol):

  - Susceptible to this problem due to its distance vector nature.
  - Limits the metric to 16, which defines "infinity" and stops the loop.

- **EIGRP** (Enhanced Interior Gateway Routing Protocol):
  - A hybrid protocol that mitigates this problem using advanced techniques like diffusing computations and route summarization.

---

### **Conclusion**

The count-to-infinity problem is a significant limitation of distance vector routing algorithms. While simple and easy to implement, these protocols rely on local information, leading to delayed convergence and routing loops. Techniques like split horizon and route poisoning mitigate this issue, but modern protocols (e.g., OSPF) avoid it entirely by using a different routing algorithm, like link-state routing.

## Link-State Routing

**Link-State Routing** is a dynamic routing algorithm that determines the best path in a network by having each router maintain a complete map of the network's topology. Unlike **distance-vector routing**, which relies on neighbors for route updates, link-state routing uses a more complex and efficient approach to ensure faster convergence and scalability in large networks.

---

### **Key Concepts of Link-State Routing**

1. **Network Topology Map**:

   - Each router builds a complete view of the entire network's structure.

2. **Link-State Advertisement (LSA)**:

   - Routers share information about their directly connected links (e.g., cost, status) with all other routers in the network.

3. **Shortest Path First (SPF)** Algorithm:

   - Routers use Dijkstra's algorithm to compute the shortest path from themselves to all other nodes.

4. **Decentralized Updates**:
   - Routers independently compute routing tables based on the network map, rather than relying on neighbors' distance vectors.

---

### **How Link-State Routing Works**

#### **1. Discovering Neighbors**

- Each router identifies its directly connected neighbors using a **Hello protocol**.

#### **2. Measuring Link Costs**

- Each router measures the cost (e.g., latency, bandwidth, or admin-defined values) of the links to its neighbors.

#### **3. Flooding Link-State Advertisements**

- Each router creates a **Link-State Advertisement (LSA)**, describing:
  - Its directly connected neighbors.
  - The cost of each link.
- LSAs are broadcast to all routers in the network.

#### **4. Building the Link-State Database (LSDB)**

- All routers collect LSAs and build an identical **link-state database** representing the network's complete topology.

#### **5. Computing the Shortest Path**

- Routers apply **Dijkstra's Algorithm** to the LSDB to calculate the shortest path to every destination.

#### **6. Updating the Routing Table**

- The shortest paths are used to populate the router's forwarding table for packet routing.

---

### **Dijkstra's Algorithm in Link-State Routing**

- **Goal**: Find the shortest path from the source router to all other routers.
- **Steps**:
  1. Initialize all nodes with an infinite cost, except the source node (cost = 0).
  2. Mark the source node as visited and calculate the cost to all its neighbors.
  3. Choose the unvisited node with the smallest cost and mark it as visited.
  4. Repeat until all nodes are visited.

---

### **Advantages of Link-State Routing**

1. **Fast Convergence**:

   - All routers quickly have a consistent view of the network after a topology change.

2. **Scalability**:

   - Efficient in large networks due to hierarchical designs (e.g., areas in OSPF).

3. **Loop-Free**:

   - The use of a global network map avoids routing loops.

4. **Accurate Path Selection**:
   - Uses multiple metrics (e.g., bandwidth, delay) for more precise path selection.

---

### **Disadvantages of Link-State Routing**

1. **Complexity**:

   - More computationally intensive than distance-vector protocols.

2. **Higher Resource Usage**:

   - Requires more memory and processing power to store and compute the LSDB.

3. **LSA Flooding Overhead**:
   - LSAs can cause significant network traffic, especially in large or rapidly changing networks.

---

### **Examples of Link-State Routing Protocols**

1. **OSPF (Open Shortest Path First)**:

   - Divides the network into areas for scalability.
   - Supports multi-metric path computation (e.g., cost based on bandwidth).

2. **IS-IS (Intermediate System to Intermediate System)**:
   - Similar to OSPF, often used in service provider networks.

---

### **Comparison with Distance-Vector Routing**

| Feature                   | Distance-Vector Routing    | Link-State Routing          |
| ------------------------- | -------------------------- | --------------------------- |
| **Routing Information**   | Shares only with neighbors | Builds a global network map |
| **Convergence Time**      | Slower, prone to loops     | Faster, loop-free           |
| **Routing Algorithm**     | Bellman-Ford               | Dijkstra's Algorithm        |
| **Resource Requirements** | Low                        | High                        |
| **Examples**              | RIP, EIGRP                 | OSPF, IS-IS                 |

---

### **Use Cases**

- **Link-State Routing** is best suited for:
  - Large, complex networks.
  - Scenarios requiring fast convergence and precise routing (e.g., data centers, ISPs).

---

### **Conclusion**

Link-state routing provides a powerful and efficient solution for modern networks, addressing many limitations of distance-vector algorithms. Its use of a global network map and Dijkstra's algorithm ensures accurate and loop-free routing, making it ideal for large-scale and high-performance environments. However, it requires careful management of resources and topology design.
