# IP Addresssing

## Intro to IP Addressing

1. **Definition**:  
   IP addressing refers to the method used to assign a unique identifier to each device on a network.

2. **Structure**:

   - **32-bit Address**: Each IPv4 address is a 32-bit binary number.
   - **8 Bytes**: Equivalent to 4 groups (octets) of 8 bits each.
   - **4 Octets**: Each octet represents 8 bits in the IP address.

3. **Parts of an IP Address**:

   - **Network Part**: Identifies the network the device belongs to.
   - **Host Part**: Identifies the specific device within that network.

4. **Representation**:

   - **Dotted Decimal Notation**: The 32-bit binary address is converted into decimal and written as four numbers separated by dots (e.g., 192.168.1.1).

5. **Decimal Range**:

   - Each octet ranges from **0 to 255** (since 2⁸ = 256 possible values).

6. **Key Points**:
   - Easy human readability due to dotted decimal format.
   - Divided into classes (A, B, C, etc.) based on the network and host part division.

## IPv4 Addressing

### Notes on IPv4 Addressing

#### **1. Total IPv4 Addresses**

- IPv4 is a **32-bit** addressing system.
- Total possible addresses: \( 2^{32} = 4,294,967,296 \) (~4.3 billion).

#### **2. IPv4 Classes**

IPv4 addresses are divided into **5 classes** (A, B, C, D, E) based on the first few bits of the address. Each class serves a different purpose.

---

### **Class A**

- N.H.H.H
- **Range**: 1.0.0.0 to 127.255.255.255
- **Network Part**: First **8 bits (1 octet)**.
- **Host Part**: Last **24 bits (3 octets)**.
- **Number of Networks**: \( 2^7 = 128 \) (but 0 and 127 are reserved).
- **Hosts per Network**: \( 2^{24} - 2 = 16,777,214 \).
- **Purpose**: Large networks, e.g., ISPs or multinational companies.
- **Example**: **10.0.0.1**

---

### **Class B**

- **Range**: 128.0.0.0 to 191.255.255.255
- **Network Part**: First **16 bits (2 octets)**.
- **Host Part**: Last **16 bits (2 octets)**.
- **Number of Networks**: \( 2^{14} = 16,384 \).
- **Hosts per Network**: \( 2^{16} - 2 = 65,534 \).
- **Purpose**: Medium-sized networks, e.g., universities or regional ISPs.
- **Example**: **172.16.0.1**

`NOTE:` Network Id is where all host part are 0.

---

### **Class C**

- **Range**: 192.0.0.0 to 223.255.255.255
- **Network Part**: First **24 bits (3 octets)**.
- **Host Part**: Last **8 bits (1 octet)**.
- **Number of Networks**: \( 2^{21} = 2,097,152 \).
- **Hosts per Network**: \( 2^8 - 2 = 254 \).
- **Purpose**: Small networks, e.g., small businesses or home networks.
- **Example**: **192.168.1.1**

---

### **Class D** (Multicast)

- **Range**: 224.0.0.0 to 239.255.255.255
- **Purpose**: Reserved for multicast groups.
- **Example**: **224.0.1.1** (used in streaming or conferencing).

---

### **Class E** (Reserved)

- **Range**: 240.0.0.0 to 255.255.255.255
- **Purpose**: Experimental use only. Not used for public networks.
- **Example**: No specific example as it is not used publicly.

---

### **Key Points**

- **IP Address = Network Part + Host Part**
- The **division of Network and Host parts** depends on the class.
- **Dotted Decimal Notation**: Each address is written as four decimal numbers separated by dots.
- **Reserved Addresses**:
  - 127.0.0.0/8 (Loopback/Localhost).
  - 0.0.0.0 (Default route).

This structure ensures efficient IP address management for different-sized networks.

## Subment Mask

### **Subnet Mask**

A **subnet mask** is a 32-bit number used in IPv4 addressing to divide an IP address into two parts:

1. **Network Part**: Identifies the network.
2. **Host Part**: Identifies the individual devices (hosts) within that network.

---

### **Purpose of Subnet Mask**

1. **Segmentation**: Divides a larger network into smaller subnetworks (subnets).
2. **Routing**: Helps routers determine which part of an IP address is the network and which is the host.
3. **Efficient Address Use**: Optimizes the use of IP addresses by avoiding unnecessary allocations.

---

### **Representation**

- A subnet mask is written in **dotted decimal notation**, just like an IP address.
- Example: **255.255.255.0**

- Each **1** in the subnet mask represents the **network part**, and each **0** represents the **host part**.

---

### **Subnet Mask Examples and Ranges**

| **Subnet Mask** | **CIDR Notation** | **Network Bits** | **Host Bits** | **Number of Hosts** | **Use Case**             |
| --------------- | ----------------- | ---------------- | ------------- | ------------------- | ------------------------ |
| 255.0.0.0       | /8                | 8                | 24            | 16,777,214          | Class A large networks.  |
| 255.255.0.0     | /16               | 16               | 16            | 65,534              | Class B medium networks. |
| 255.255.255.0   | /24               | 24               | 8             | 254                 | Class C small networks.  |
| 255.255.255.128 | /25               | 25               | 7             | 126                 | Smaller subnets.         |
| 255.255.255.192 | /26               | 26               | 6             | 62                  | Micro subnets.           |

---

### **Key Notes**

1. **Default Subnet Masks** (based on IP classes):

   - Class A: **255.0.0.0**
   - Class B: **255.255.0.0**
   - Class C: **255.255.255.0**

2. **CIDR Notation**:

   - Compact representation of subnet masks.
   - Example: `/24` means 24 bits for the network and the remaining 8 bits for hosts.

3. **Subnetting**:

   - Dividing a large network into smaller subnetworks to improve efficiency and security.

4. **Binary Representation**:
   - Subnet mask: **11111111.11111111.11111111.00000000**
   - IP Address: **192.168.1.10**
   - Network ID: **192.168.1.0**
   - Host Range: **192.168.1.1 to 192.168.1.254**

---

### **Example**

For **IP Address**: `192.168.1.10`  
With **Subnet Mask**: `255.255.255.0`

1. **Network Part**: `192.168.1`
2. **Host Part**: `10`
3. **Host Range**: `192.168.1.1` to `192.168.1.254`
4. **Broadcast Address**: `192.168.1.255`

A subnet mask is crucial for managing and segmenting networks effectively.

## CIDR or prefix length

### **CIDR (Classless Inter-Domain Routing) or Prefix Length**

---

### **Definition**

- **CIDR** is a method for assigning and representing IP addresses more efficiently than the traditional class-based system (Class A, B, C).
- The **prefix length** (also called CIDR notation) represents the number of bits used for the **network part** of an IP address.

---

### **Format**

- CIDR is written as:  
  **IP Address / Prefix Length**  
  Example: `192.168.1.0/24`
  - `192.168.1.0`: Network address.
  - `/24`: First 24 bits are for the network, leaving the remaining bits for host addresses.

---

### **Purpose**

1. **Efficient Addressing**: Avoids wasting IP addresses by allowing variable-length subnet masks.
2. **Flexible Subnetting**: Enables networks to be divided into subnets of varying sizes.
3. **Routing Efficiency**: Reduces the number of routing table entries using aggregation (supernetting).

---

### **Relationship to Subnet Masks**

The **prefix length** indicates the number of **1s** in the subnet mask.  
Example:

- `/24` = **255.255.255.0**
- `/16` = **255.255.0.0**
- `/8` = **255.0.0.0**

---

### **CIDR Examples**

| **CIDR Notation** | **Subnet Mask** | **Number of Hosts** | **Use Case**                     |
| ----------------- | --------------- | ------------------- | -------------------------------- |
| `/8`              | 255.0.0.0       | 16,777,214          | Very large networks (Class A).   |
| `/16`             | 255.255.0.0     | 65,534              | Medium-sized networks (Class B). |
| `/24`             | 255.255.255.0   | 254                 | Small networks (Class C).        |
| `/30`             | 255.255.255.252 | 2                   | Point-to-point links.            |

---

### **Benefits of CIDR**

1. **No Class Boundaries**: IP addresses are assigned based on actual needs rather than fixed classes.
2. **Aggregation**: Combines multiple IP ranges into a single routing table entry (e.g., multiple `/24` can aggregate to `/22`).
3. **Improved Scalability**: Supports a hierarchical network structure for efficient address allocation.

---

### **Example**

For `192.168.1.0/24`:

- **Subnet Mask**: `255.255.255.0`
- **Network Part**: `192.168.1` (24 bits).
- **Host Range**: `192.168.1.1` to `192.168.1.254`.
- **Broadcast Address**: `192.168.1.255`.

CIDR simplifies IP management, providing flexibility and efficiency for modern networks.
