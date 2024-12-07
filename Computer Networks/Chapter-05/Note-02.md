# Networking

## Classless Addressing

Classless addressing, also known as **Classless Inter-Domain Routing (CIDR)**, is a modern approach to IP addressing and routing in IPv4 and IPv6. It eliminates the rigid boundaries of classful addressing (Class A, B, C) and allows for more efficient and flexible allocation of IP addresses.

---

### **Key Features of Classless Addressing**

1. **No Fixed Classes**

   - IP addresses are not restricted to predefined classes (A, B, or C).
   - Subnets can have variable lengths, depending on the specific requirements.

2. **CIDR Notation**

   - The subnet mask is expressed as a **slash (/) followed by the number of bits** used for the network portion.  
     Example:
     - `192.168.1.0/24` means 24 bits are for the network, and 8 bits are for hosts.
     - `10.0.0.0/8` means 8 bits are for the network, and 24 bits are for hosts.

3. **Efficient Address Allocation**

   - IP addresses can be assigned in blocks of any size, minimizing waste.
   - Example: Instead of assigning a whole Class B block (65,534 addresses) to an organization needing only 4,000, CIDR allows for allocating just enough (e.g., `/20` for 4,096 addresses).

4. **Route Aggregation (Supernetting)**
   - Multiple contiguous networks can be combined into a single larger network to simplify routing tables.
   - Example: Networks `192.168.0.0/24`, `192.168.1.0/24`, and `192.168.2.0/24` can be aggregated into `192.168.0.0/22`.

---

### **Benefits of Classless Addressing**

1. **Efficient Use of IP Addresses**

   - Prevents over-allocation and under-utilization seen in classful addressing.
   - Helps delay IPv4 exhaustion.

2. **Flexible Subnetting**

   - Organizations can tailor subnet sizes to fit their needs, reducing waste.

3. **Simplified Routing**

   - CIDR reduces the size of routing tables by aggregating multiple routes into a single entry.

4. **Scalability**
   - Supports the rapid growth of the internet by efficiently managing IP space.

---

### **CIDR Notation and Examples**

- **Subnet Masks in CIDR:**

  - `/8`: 255.0.0.0 (Class A-like)
  - `/16`: 255.255.0.0 (Class B-like)
  - `/24`: 255.255.255.0 (Class C-like)

- **Address Block Examples:**
  - `192.168.0.0/26` allocates 64 IP addresses.
  - `10.0.0.0/12` allocates 1,048,576 IP addresses.

---

### **Comparison: Classful vs. Classless Addressing**

| **Aspect**         | **Classful Addressing**     | **Classless Addressing (CIDR)** |
| ------------------ | --------------------------- | ------------------------------- |
| Address Allocation | Fixed sizes (Class A, B, C) | Variable sizes (flexible)       |
| Subnet Mask        | Rigid, class-based          | Customizable with CIDR          |
| Routing Table Size | Larger                      | Smaller (due to aggregation)    |
| Efficiency         | Wastes IP addresses         | Maximizes utilization           |

---

### **Use Cases of Classless Addressing**

1. **Internet Service Providers (ISPs):** Allocate smaller IP blocks to customers based on their needs.
2. **Enterprise Networks:** Subdivide networks to create multiple subnets within the organization.
3. **Modern Routing Protocols:** Most modern protocols, like BGP, rely on CIDR for efficient routing.

---

### **Conclusion**

Classless addressing (CIDR) replaced classful addressing to address the inefficiencies of rigid IP classes. By allowing variable-length subnet masks and more precise allocation of IP addresses, it optimized address space usage and enabled the internet to scale effectively.

### Subnetting in CIDR (Classless Inter-Domain Routing) Addressing

CIDR (Classless Inter-Domain Routing) is a method of IP addressing that allows efficient allocation and routing of IP addresses by eliminating the rigid boundaries of classful addressing. Subnetting in CIDR involves dividing a given IP address block into smaller subnets using custom subnet masks, expressed in **CIDR notation**.

---

### **Key Features of CIDR Subnetting**

1. **Flexible Subnet Sizes:**
   - Unlike classful subnetting, CIDR allows variable subnet masks (e.g., `/22`, `/28`) regardless of the original class (A, B, or C).
2. **Efficient Address Utilization:**

   - Allocates IP addresses based on the exact number of hosts needed, minimizing waste.

3. **CIDR Notation:**

   - CIDR uses a **slash (/) notation** to indicate the number of bits used for the network portion of an address.  
     For example:
     - `/24` → 24 bits for the network, 8 bits for hosts.
     - Subnet mask: `255.255.255.0`.

4. **Aggregation (Supernetting):**
   - CIDR supports both subnetting (breaking down a block) and supernetting (combining multiple blocks).

---

### **How CIDR Subnetting Works**

#### **1. Start with a Block of IPs**

- A network administrator is assigned a block of IPs (e.g., `192.168.0.0/24`).

#### **2. Determine Subnet Requirements**

- Decide the number of subnets and hosts required in each subnet.

#### **3. Borrow Host Bits**

- Borrow bits from the host portion of the IP address to create subnets.
- The number of bits borrowed determines the number of subnets created.

#### **4. Calculate New Subnets**

- **Number of Subnets:** \( 2^n \), where \( n \) is the number of bits borrowed.
- **Hosts per Subnet:** \( 2^h - 2 \), where \( h \) is the number of remaining host bits (subtract 2 for network and broadcast addresses).

#### **5. Assign Subnet Ranges**

- Divide the original block into smaller ranges, ensuring no overlap.

---

### **Example: CIDR Subnetting**

#### **Requirement:**

- You are given `192.168.0.0/24` (256 IPs).
- Create 4 subnets.

#### **Step-by-Step Solution:**

1. **Borrow Bits for Subnets:**

   - \( 2^n \geq 4 \) → \( n = 2 \). Borrow 2 bits from the host portion.
   - New subnet mask: `/26` → `255.255.255.192`.

2. **Hosts per Subnet:**

   - Remaining host bits: \( 32 - 26 = 6 \).
   - \( 2^6 - 2 = 62 \) hosts per subnet.

3. **Subnet Ranges:**
   - Subnet 1: `192.168.0.0/26` → IP range: `192.168.0.0 - 192.168.0.63`
   - Subnet 2: `192.168.0.64/26` → IP range: `192.168.0.64 - 192.168.0.127`
   - Subnet 3: `192.168.0.128/26` → IP range: `192.168.0.128 - 192.168.0.191`
   - Subnet 4: `192.168.0.192/26` → IP range: `192.168.0.192 - 192.168.0.255`

---

### **Advantages of CIDR Subnetting**

1. **Efficient Utilization of IP Space:**

   - Networks get exactly the number of IPs needed, reducing wastage.

2. **Supports Hierarchical Design:**

   - Enables scalable and hierarchical subnetting for large networks.

3. **Simplified Routing:**

   - Aggregates multiple networks into a single routing entry (route summarization).

4. **Eliminates Class Boundaries:**
   - CIDR works seamlessly across traditional Class A, B, and C boundaries.

---

### **Disadvantages of CIDR Subnetting**

1. **Complex Planning:**

   - Requires careful planning to avoid overlapping subnets.

2. **Increased Management Overhead:**

   - Managing a large number of CIDR-based subnets can be challenging without tools.

3. **Incompatibility with Old Protocols:**
   - Older routing protocols (like RIP v1) do not support CIDR.

---

### **Comparison: Classful vs. CIDR Subnetting**

| **Aspect**                | **Classful Subnetting**          | **CIDR Subnetting**          |
| ------------------------- | -------------------------------- | ---------------------------- |
| Address Space Utilization | Often results in wastage         | Highly efficient             |
| Subnet Mask               | Fixed for all subnets            | Variable-length subnet masks |
| Routing                   | Limited aggregation              | Route summarization possible |
| Flexibility               | Rigid (Class A, B, C) boundaries | Flexible across any range    |

---

### **Use Cases of CIDR Subnetting**

1. **ISPs (Internet Service Providers):**

   - Allocate IP blocks to customers based on their specific needs.

2. **Corporate Networks:**

   - Divide large enterprise networks into smaller, manageable subnets.

3. **Data Centers and Cloud Environments:**
   - Dynamically allocate IPs based on the varying requirements of virtual machines or services.

---

### **CIDR Subnetting Example with VLSM**

#### Requirement:

- You have `172.16.0.0/16` and need:
  - Subnet A: 1000 hosts
  - Subnet B: 500 hosts
  - Subnet C: 200 hosts

#### Step-by-Step Allocation:

1. **Subnet A:**

   - \( 2^{10} = 1024 \) → `/22` → IP range: `172.16.0.0 - 172.16.3.255`.

2. **Subnet B:**

   - \( 2^{9} = 512 \) → `/23` → IP range: `172.16.4.0 - 172.16.5.255`.

3. **Subnet C:**

   - \( 2^{8} = 256 \) → `/24` → IP range: `172.16.6.0 - 172.16.6.255`.

4. **Remaining IPs:**
   - Can be allocated to additional subnets as needed.

---

### **Conclusion**

CIDR subnetting provides a scalable and efficient approach to IP address management. It eliminates the inefficiencies of classful addressing, supports flexible subnet sizes, and enhances routing efficiency. By using CIDR, organizations can optimize IP allocation for networks of any size.

## VLSM in Classless Addressing (CIDR)

LSM, or **Length Subnet Masking**, in Classless Addressing (CIDR) refers to using subnet masks of variable lengths to divide an IP address space into subnets. This approach leverages CIDR’s flexibility to allocate IP addresses based on specific requirements rather than being constrained by class boundaries (Class A, B, or C).

In CIDR, subnet masks are expressed in **slash notation (e.g., /24, /22)**, specifying the number of bits used for the network portion of the address.

---

### **How LSM Works in CIDR**

1. **Flexible Subnet Mask Lengths:**

   - CIDR allows different subnets to use subnet masks of varying lengths, depending on the number of hosts needed in each subnet.

2. **No Class Boundaries:**

   - Unlike classful addressing, CIDR ignores predefined class boundaries, enabling the creation of networks like `10.0.0.0/22`, which wouldn’t fit into a traditional Class A, B, or C structure.

3. **Efficient Address Utilization:**

   - By using custom subnet masks, LSM ensures IP addresses are allocated efficiently, minimizing wastage.

4. **Hierarchical Subnetting:**
   - Subnets can be further divided into smaller subnets as needed, using progressively longer subnet masks.

---

### **Example of LSM in CIDR**

#### Scenario:

You have the network block `192.168.0.0/24` (256 IPs) and need to create three subnets for the following requirements:

- Subnet A: 50 hosts
- Subnet B: 30 hosts
- Subnet C: 10 hosts

---

#### Step-by-Step Solution:

1. **Subnet A:**

   - Required hosts: 50
   - Minimum subnet size: \( 2^6 = 64 \) IPs (includes network and broadcast).
   - Subnet mask: `/26` → `255.255.255.192`.
   - Subnet range: `192.168.0.0 - 192.168.0.63`.

2. **Subnet B:**

   - Required hosts: 30
   - Minimum subnet size: \( 2^5 = 32 \) IPs.
   - Subnet mask: `/27` → `255.255.255.224`.
   - Subnet range: `192.168.0.64 - 192.168.0.95`.

3. **Subnet C:**

   - Required hosts: 10
   - Minimum subnet size: \( 2^4 = 16 \) IPs.
   - Subnet mask: `/28` → `255.255.255.240`.
   - Subnet range: `192.168.0.96 - 192.168.0.111`.

4. **Remaining Addresses:**
   - IPs from `192.168.0.112 - 192.168.0.255` can be allocated to additional subnets or reserved.

---

### **Benefits of LSM in CIDR**

1. **Optimized Address Allocation:**

   - Allocates addresses based on exact requirements, reducing waste.

2. **Flexibility in Design:**

   - Supports networks with varying sizes and requirements.

3. **Scalability:**

   - Networks can be easily expanded or subdivided as needed.

4. **Efficient Routing:**
   - Summarization reduces routing table entries (e.g., aggregating `192.168.0.0/26` and `192.168.0.64/27` into `192.168.0.0/25`).

---

### **Applications of LSM in CIDR**

1. **Enterprise Networks:**

   - Dividing departments, offices, or branches into subnets with different sizes.

2. **Service Providers:**

   - Allocating custom-sized IP blocks to customers based on their needs.

3. **Dynamic Environments:**
   - Data centers and cloud networks benefit from flexible and efficient subnetting.

---

### **Conclusion**

LSM in CIDR empowers network administrators to design and manage IP address spaces more efficiently. By tailoring subnet masks to meet specific needs, LSM ensures that IP addresses are utilized optimally, making it ideal for modern, dynamic networks.
