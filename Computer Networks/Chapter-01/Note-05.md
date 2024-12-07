# Computer Networks (OLD NOTES-GATE SMASHERS)

## Introduction to Computer Network

A **computer network** is a system that connects multiple devices (computers, printers, phones, etc.) to share resources and information. These networks allow devices to communicate with each other, send data, and access services like the internet.

There are different types of computer networks based on their size and function, such as:

- **LAN (Local Area Network)**: Small area (e.g., a home or office).
- **WAN (Wide Area Network)**: Large area (e.g., multiple cities or countries).
- **MAN (Metropolitan Area Network)**: Covers a larger geographic area than LAN but smaller than WAN (e.g., a city).

## OSI Model - The 7 Layers of Networking

The **OSI (Open Systems Interconnection)** model is a conceptual framework that standardizes the way different devices in a network communicate. It divides network communication into seven layers. Each layer performs specific functions and works with the layers above and below it. The OSI model is a helpful guide for understanding how networks operate and troubleshooting network issues.

### The 7 Layers of the OSI Model:

1. **Physical Layer (Layer 1)**:

   - **Purpose**: Handles the actual transmission of raw bits (0s and 1s) over a physical medium (like cables or wireless signals).
   - **Example**: Ethernet cables, fiber optics, Wi-Fi signals.

2. **Data Link Layer (Layer 2)**:

   - **Purpose**: Ensures reliable communication between devices on the same network (local network). It manages how devices access the physical medium and handles error detection.
   - **Example**: Switches, MAC addresses.

3. **Network Layer (Layer 3)**:

   - **Purpose**: Responsible for routing data from one device to another across different networks. It decides the best path for the data to travel.
   - **Example**: Routers, IP addresses.

4. **Transport Layer (Layer 4)**:

   - **Purpose**: Ensures reliable data transfer between devices by providing error checking and flow control. It breaks down data into smaller packets.
   - **Example**: TCP (Transmission Control Protocol), UDP (User Datagram Protocol).

5. **Session Layer (Layer 5)**:

   - **Purpose**: Manages the sessions or connections between devices. It ensures that data exchanges between devices are properly synchronized and managed.
   - **Example**: NetBIOS, RPC (Remote Procedure Call).

6. **Presentation Layer (Layer 6)**:

   - **Purpose**: Translates data between the application and transport layers. It formats, compresses, or encrypts data for the application layer.
   - **Example**: SSL/TLS encryption, JPEG, GIF file formats.

7. **Application Layer (Layer 7)**:
   - **Purpose**: The topmost layer where end-user applications interact with the network. This layer is responsible for protocols and services that applications use to communicate.
   - **Example**: HTTP (web browsing), FTP (file transfer), SMTP (email).

### How OSI Model Works:

When data is sent over a network:

- **From the sender**: The data moves from the top (Application layer) to the bottom (Physical layer).
- **To the receiver**: The data moves back up from the bottom (Physical layer) to the top (Application layer).

The OSI model helps break down complex networking concepts into understandable layers, each with specific tasks that help in sending and receiving data reliably.

## TCP/IP

The **TCP/IP protocol suite** is a set of communication protocols used for the internet and other similar networks. It governs how data is transmitted over networks, ensuring different devices can communicate with each other. The suite is named after two of its primary protocols: **Transmission Control Protocol (TCP)** and **Internet Protocol (IP)**.

Here’s an overview of the main layers of the TCP/IP model:

### 1. **Application Layer**

- This is the top layer where end-user applications and processes reside. It is responsible for providing network services directly to users.
- **Protocols**: HTTP, FTP, SMTP, DNS, POP3, IMAP, and many others.

### 2. **Transport Layer**

- The transport layer ensures that data is transferred reliably between devices.
- **Protocols**:
  - **TCP (Transmission Control Protocol)**: Provides reliable, connection-oriented communication. It breaks data into packets, ensures they are delivered in the correct order, and handles retransmissions if packets are lost.
  - **UDP (User Datagram Protocol)**: Provides faster but unreliable communication. It’s often used where speed is crucial, and errors can be tolerated (e.g., video streaming).

### 3. **Internet Layer**

- This layer is responsible for addressing, routing, and delivering packets across networks.
- **Protocols**:
  - **IP (Internet Protocol)**: Defines IP addresses (IPv4 and IPv6) and is responsible for routing packets between devices. It is connectionless, meaning it doesn’t ensure the delivery of packets.
  - **ICMP (Internet Control Message Protocol)**: Used for error reporting and diagnostics (e.g., `ping`).

### 4. **Network Access Layer (Link Layer)**

- This is the lowest layer of the TCP/IP model. It defines how data is physically transmitted over the network, whether through Ethernet, Wi-Fi, or other technologies.
- **Protocols**: Ethernet, ARP (Address Resolution Protocol), PPP (Point-to-Point Protocol), and others.

### Key Points:

- **IP** is responsible for addressing and routing data between devices on different networks.
- **TCP** ensures reliable delivery of data between devices, handling retransmissions in case of packet loss.
- **UDP**, on the other hand, allows for faster, connectionless communication with no guarantee of delivery.
- **Application Layer protocols** provide communication services directly to end-users (e.g., web browsing, email, file transfer).

This suite was designed to be flexible and scalable, supporting a wide variety of applications, from simple file transfers to complex web-based applications.

## Topology

### **Topologies in Computer Networks**

Network topology refers to the arrangement of different elements (links, devices, etc.) in a computer network. The choice of topology impacts network performance, cost, and scalability. Here’s an overview of some common network topologies:

---

### **1. Mesh Topology**

In a **Mesh** topology, every device is connected to every other device in the network. This provides high redundancy and reliability since multiple paths are available for data transmission.

**Key Points**:

- **Full Mesh**: Every device is connected to every other device in the network. High fault tolerance, but expensive and complex to set up.
- **Partial Mesh**: Only some devices are interconnected, reducing cost and complexity while still providing some redundancy.
- **Advantages**:
  - High reliability and fault tolerance.
  - Multiple paths for data, which ensures no single point of failure.
  - Good for large networks where uptime is critical.
- **Disadvantages**:
  - Expensive due to the large number of cables and connections.
  - Complex to install and configure.
  - Maintenance can be difficult.

---

### **2. Star Topology**

In a **Star** topology, all devices are connected to a central device, such as a switch or hub. The central device acts as a mediator for data transmission.

**Key Points**:

- **Central Device**: The central hub or switch is crucial for managing traffic between devices.
- **Advantages**:
  - Easy to set up and manage.
  - Failures in individual devices do not affect the network (only the affected device).
  - Scalable—new devices can be added easily without affecting other devices.
- **Disadvantages**:
  - If the central hub fails, the entire network is down.
  - Requires more cable than other topologies (since each device needs a separate cable to the central device).

---

### **3. Hub Topology** (often referred to as **Star with a Hub**)

A **Hub** topology is a variation of Star topology, where instead of a switch, a hub is used as the central device. A hub is a basic networking device that forwards packets to all connected devices, regardless of the destination.

**Key Points**:

- **Hub**: A hub broadcasts data to all devices connected to it, unlike a switch, which routes data more intelligently.
- **Advantages**:
  - Simple to implement.
  - Cost-effective.
- **Disadvantages**:
  - Performance can degrade with high traffic, as all data is broadcast to all devices.
  - No intelligence (i.e., no filtering of traffic), leading to security and bandwidth issues.
  - Limited scalability due to performance degradation as the number of devices increases.

---

### **4. Bus Topology**

In a **Bus** topology, all devices are connected to a single central cable, known as the "bus" or backbone. Data sent by any device is broadcast to all devices on the network, but only the destination device processes it.

**Key Points**:

- **Single Cable**: A single cable serves as the backbone connecting all devices.
- **Advantages**:
  - Simple and cost-effective for small networks.
  - Easy to implement and extend.
- **Disadvantages**:
  - Performance degrades as more devices are added.
  - If the backbone cable fails, the entire network goes down.
  - Difficult to isolate faults.
  - Limited scalability and not very robust.

---

### **5. Hybrid Topology**

A **Hybrid** topology combines two or more different topologies to leverage the advantages of each. For example, you could combine a **Star** topology with a **Bus** topology to form a hybrid.

**Key Points**:

- **Combination of Topologies**: A mix of Star, Mesh, Bus, or Ring topologies.
- **Advantages**:
  - Flexible and scalable.
  - Can be customized to meet specific needs.
  - Combines the strengths of multiple topologies.
- **Disadvantages**:
  - Can be complex to design and implement.
  - Expensive due to the use of different topologies.
  - Maintenance can be complicated.

---

### **Summary of Key Advantages and Disadvantages**:

| **Topology** | **Advantages**                                                             | **Disadvantages**                                                        |
| ------------ | -------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **Mesh**     | High reliability, fault tolerance, multiple paths, good for large networks | Expensive, complex, high maintenance                                     |
| **Star**     | Easy to set up, scalable, failure isolated to single devices               | Hub failure brings down the whole network, more cabling required         |
| **Hub**      | Simple, cost-effective                                                     | Poor performance under heavy traffic, security issues, no intelligence   |
| **Bus**      | Simple, cost-effective for small networks                                  | Performance degrades, single point of failure, difficult fault isolation |
| **Hybrid**   | Flexible, combines the benefits of different topologies                    | Complex to design and implement, expensive, difficult to maintain        |

Each topology has its own strengths and weaknesses, and the choice depends on the scale of the network, the required reliability, and the budget available.
