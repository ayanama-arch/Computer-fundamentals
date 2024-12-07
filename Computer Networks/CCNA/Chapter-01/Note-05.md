## TCP/IP Protocol suite

The **TCP/IP protocol suite** is a set of communication protocols used for interconnecting network devices on the internet. It stands for **Transmission Control Protocol/Internet Protocol**, and it is the foundation of modern networking. Unlike the OSI model, which has seven layers, TCP/IP is generally structured into **four layers**.

### TCP/IP Layers and Their Functions:

#### 1. **Application Layer**:

- **Purpose**: Provides the interface between the network and the application software.
- **Key Protocols**:
  - **HTTP/HTTPS**: For web communication.
  - **SMTP, IMAP, POP3**: For email communication.
  - **FTP**: For file transfers.
  - **DNS**: Resolves domain names to IP addresses.
  - **SNMP**: For network management.
- **Corresponds to**: The Application, Presentation, and Session layers of the OSI model.

#### 2. **Transport Layer**:

- **Purpose**: Ensures reliable or unreliable delivery of data across the network.
- **Key Protocols**:
  - **TCP (Transmission Control Protocol)**:
    - Reliable, connection-oriented protocol.
    - Ensures data is delivered without errors, in the correct order.
  - **UDP (User Datagram Protocol)**:
    - Unreliable, connectionless protocol.
    - Used for applications requiring speed over reliability (e.g., video streaming, gaming).
- **Corresponds to**: The Transport layer of the OSI model.

#### 3. **Internet Layer**:

- **Purpose**: Handles the addressing, routing, and delivery of data packets.
- **Key Protocols**:
  - **IP (Internet Protocol)**:
    - Responsible for addressing and routing packets.
    - Versions: IPv4 and IPv6.
  - **ICMP (Internet Control Message Protocol)**:
    - Used for error messages and diagnostic tools like `ping`.
  - **ARP (Address Resolution Protocol)**:
    - Resolves IP addresses to MAC addresses.
  - **NAT (Network Address Translation)**:
    - Maps private IP addresses to a public IP address.
- **Corresponds to**: The Network layer of the OSI model.

#### 4. **Network Access Layer** (Link Layer):

- **Purpose**: Handles the physical transmission of data across the network.
- **Key Components**:
  - Protocols and technologies like Ethernet, Wi-Fi, and PPP.
  - MAC addresses and physical hardware interaction.
- **Corresponds to**: The Data Link and Physical layers of the OSI model.

---

### Comparison: TCP/IP vs. OSI Model

| **TCP/IP Layer**     | **Equivalent OSI Layers**          |
| -------------------- | ---------------------------------- |
| Application Layer    | Application, Presentation, Session |
| Transport Layer      | Transport                          |
| Internet Layer       | Network                            |
| Network Access Layer | Data Link, Physical                |

---

### Strengths of TCP/IP:

- **Widely Adopted**: Backbone of the internet.
- **Scalable**: Works for small networks and the global internet.
- **Robust**: Handles errors efficiently.
- **Interoperable**: Supports diverse hardware and software.

---

### Weaknesses of TCP/IP:

- **Not Strictly Layered**: Some functionalities overlap.
- **Less Modular**: OSI provides clearer distinctions between layers.
- **Limited in Modern Features**: Gradual evolution has added complexities (e.g., IPv4 exhaustion requiring IPv6).

The TCP/IP model’s simplicity and practicality have made it the de facto standard for networking today.

## Protocol Data Unit

A **Protocol Data Unit (PDU)** is a packet of data that is exchanged between layers of the network protocol stack. Each layer in a network model (like the OSI model or TCP/IP model) has its own specific type of PDU, which includes control information (headers and trailers) and the actual data being transmitted.

### PDUs in Different Layers of the OSI Model

Each layer of the OSI model deals with a different PDU type:

1. **Application Layer, Presentation Layer, and Session Layer**:

   - **PDU Name**: **Data**
   - **Description**: At these upper layers, the PDU is simply referred to as "data," as it represents the information being exchanged between applications.

2. **Transport Layer**:

   - **PDU Name**: **Segment** (TCP) / **Datagram** (UDP)
   - **Description**: The transport layer divides the data into smaller units (segments or datagrams) and adds headers to ensure proper delivery.

3. **Network Layer**:

   - **PDU Name**: **Packet**
   - **Description**: A packet is created when the network layer adds addressing information (e.g., source and destination IP addresses).

4. **Data Link Layer**:

   - **PDU Name**: **Frame**
   - **Description**: A frame is formed by encapsulating the packet with a header and a trailer that include information such as MAC addresses and error-checking data (CRC).

5. **Physical Layer**:
   - **PDU Name**: **Bits**
   - **Description**: The frame is converted into a stream of bits (1s and 0s) for physical transmission over the medium (e.g., cables, fiber optics, or wireless).

---

### PDU Structure

A typical PDU contains:

- **Header**: Contains control information like source/destination addresses, sequence numbers, and error detection codes.
- **Payload (Data)**: The actual user data or the encapsulated PDU from the higher layer.
- **Trailer**: Found in some layers (e.g., Data Link Layer), providing error-checking or framing information.

---

### PDUs in the TCP/IP Model

- **Application Layer**: Data
- **Transport Layer**: Segment (TCP) / Datagram (UDP)
- **Internet Layer**: Packet
- **Network Access Layer**: Frame -> Bits

---

### Summary Table

| **Layer**   | **OSI PDU Name** | **Example**                  |
| ----------- | ---------------- | ---------------------------- |
| Application | Data             | HTTP request, email          |
| Transport   | Segment          | TCP/UDP header + data        |
| Network     | Packet           | IP header + segment          |
| Data Link   | Frame            | Ethernet frame               |
| Physical    | Bits             | Voltage levels, light pulses |

Understanding PDUs is essential for grasping how data moves across a network and how layers in network protocols interact.

## Application layer protocol

The **TCP/IP protocol suite** includes a set of application protocols that operate at the **Application Layer** to provide services for specific user activities like email, file transfer, and web browsing. These protocols rely on the underlying transport protocols (TCP or UDP) for data delivery.

Here are the key **application protocols** in the TCP/IP model:

---

### **1. HTTP (Hypertext Transfer Protocol)**

- **Purpose**: Used for web browsing and data transfer between a client (browser) and a web server.
- **Port**: 80 (default).
- **Secure Version**: **HTTPS** (over TLS/SSL, port 443).
- **Example**: Viewing a website (e.g., `www.google.com`).

---

### **2. FTP (File Transfer Protocol)**

- **Purpose**: Transfers files between computers on a network.
- **Ports**:
  - **Command Connection**: 21 (control).
  - **Data Transfer**: 20.
- **Example**: Uploading files to a web server.
- **Secure Version**: **SFTP** (via SSH).

---

### **3. SMTP (Simple Mail Transfer Protocol)**

- **Purpose**: Sends emails from a client to a mail server and between mail servers.
- **Port**: 25 (default), 587 (with encryption).
- **Example**: Sending an email via an email client (e.g., Outlook).

---

### **4. POP3 (Post Office Protocol, Version 3)**

- **Purpose**: Retrieves emails from a mail server to a client.
- **Port**: 110 (default), 995 (with encryption).
- **Limitation**: Emails are usually deleted from the server after retrieval.

---

### **5. IMAP (Internet Message Access Protocol)**

- **Purpose**: Retrieves emails like POP3 but allows email management directly on the server.
- **Port**: 143 (default), 993 (with encryption).
- **Example**: Gmail's webmail service.

---

### **6. DNS (Domain Name System)**

- **Purpose**: Resolves domain names to IP addresses.
- **Port**: 53.
- **Example**: Resolving `www.google.com` to its IP address.

---

### **7. Telnet**

- **Purpose**: Provides remote login to devices over a network.
- **Port**: 23.
- **Limitation**: Not secure (transmits data in plaintext).
- **Secure Version**: **SSH (Secure Shell)** on port 22.

---

### **8. DHCP (Dynamic Host Configuration Protocol)**

- **Purpose**: Automatically assigns IP addresses to devices on a network.
- **Ports**: 67 (server), 68 (client).
- **Example**: Assigning an IP to your laptop when connecting to Wi-Fi.

---

### **9. SNMP (Simple Network Management Protocol)**

- **Purpose**: Monitors and manages network devices like routers, switches, and servers.
- **Port**: 161 (queries), 162 (traps).

---

### **10. TFTP (Trivial File Transfer Protocol)**

- **Purpose**: Simplified file transfer with minimal functionality.
- **Port**: 69.
- **Example**: Transferring configuration files to a network device.

---

### **11. NTP (Network Time Protocol)**

- **Purpose**: Synchronizes the clocks of devices on a network.
- **Port**: 123.
- **Example**: Ensuring servers maintain the same time.

---

### **12. HTTPS (Hypertext Transfer Protocol Secure)**

- **Purpose**: Secure version of HTTP using TLS/SSL encryption.
- **Port**: 443.
- **Example**: Banking websites or any secure online transaction.

---

### **13. RDP (Remote Desktop Protocol)**

- **Purpose**: Enables remote access to Windows systems.
- **Port**: 3389.

---

### **14. LDAP (Lightweight Directory Access Protocol)**

- **Purpose**: Accesses and manages distributed directory services.
- **Port**: 389 (unencrypted), 636 (encrypted).
- **Example**: Centralized user authentication in organizations.

---

### **Transport Layer Dependencies**

- **TCP**: Used for reliable communication (e.g., HTTP, SMTP, FTP).
- **UDP**: Used for faster, connectionless protocols (e.g., DNS, DHCP, TFTP).

### **15. NNTP (Network News Transfer Protocol)**

- **Purpose**:  
  NNTP is used for reading, posting, and transferring articles on **Usenet**, a global distributed discussion system for newsgroups.
- **Port**:
  - **Port 119**: Default for non-encrypted communication.
  - **Port 563**: Secure version (NNTPS) with SSL/TLS encryption.
- **Example**:
  - Accessing and posting discussions in Usenet newsgroups (e.g., tech forums).
  - Sharing files or articles in binary newsgroups.

These protocols are essential for enabling communication and data exchange in various applications across the Internet and local networks.
