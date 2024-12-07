# Networking

## Address Resolution Protocol (ARP)

**ARP (Address Resolution Protocol)** is a protocol used to map an **IP address** to a **MAC address** within a local network. It operates at the **Data Link Layer (Layer 2)** of the OSI model and is essential for devices in the same network to communicate with each other.

### Key Features of ARP:

1. **Purpose:** Resolves the 32-bit IP address to a 48-bit MAC (Media Access Control) address.
2. **Scope:** Operates only within a local area network (LAN). It does not work across routers.
3. **Protocol Type:** ARP is used in IPv4 networks. Its counterpart for IPv6 is **NDP (Neighbor Discovery Protocol)**.

---

### How ARP Works:

1. **Request:**
   - When a device (e.g., Computer A) wants to send data to another device (e.g., Computer B) on the same LAN, it knows the IP address of Computer B but not its MAC address.
   - Computer A sends an **ARP Request** broadcast on the network, asking, "Who has this IP address?"
2. **Reply:**
   - The device with the matching IP address (Computer B) responds with an **ARP Reply**, providing its MAC address.
3. **Caching:**
   - Computer A stores this IP-to-MAC mapping in its **ARP cache** for future use, avoiding repetitive requests.

---

### Types of ARP:

1. **Normal ARP:** Resolves the MAC address for a given IP.
2. **Reverse ARP (RARP):** Resolves the IP address for a given MAC (used in older systems).
3. **Proxy ARP:** A router answers ARP requests on behalf of another device to make it seem like they are on the same network.
4. **Gratuitous ARP:** A device announces its own IP-to-MAC mapping to update others' caches or check for address conflicts.

---

### ARP Packet Structure:

An ARP packet includes:

1. **Hardware Type:** Specifies the hardware (e.g., Ethernet).
2. **Protocol Type:** Specifies the protocol (e.g., IPv4).
3. **Hardware Address Length:** Length of the MAC address (e.g., 6 bytes).
4. **Protocol Address Length:** Length of the IP address (e.g., 4 bytes).
5. **Operation Code:** Indicates ARP Request (1) or ARP Reply (2).
6. **Sender Hardware Address:** MAC address of the sender.
7. **Sender Protocol Address:** IP address of the sender.
8. **Target Hardware Address:** MAC address of the target (unknown in request).
9. **Target Protocol Address:** IP address of the target.

---

### Limitations of ARP:

1. **Broadcast Traffic:** ARP requests are broadcast to all devices, which can lead to congestion in large networks.
2. **Security Vulnerabilities:** ARP is susceptible to attacks like:
   - **ARP Spoofing/Poisoning:** Malicious devices send fake ARP replies to redirect traffic.
3. **Obsolescence in IPv6:** Replaced by NDP in IPv6 networks.

---

### Etymology of ARP:

- **"Address"**: Refers to the network (IP) and hardware (MAC) addresses it resolves.
- **"Resolution"**: The process of converting one address type (IP) to another (MAC).
- **"Protocol"**: A set of rules defining its operation.

## NAT Explained - Network Address Translation

**NAT (Network Address Translation)** is a technique used to modify network address information in the headers of IP packets as they traverse a router or firewall. It allows multiple devices in a private network to share a single public IP address, enabling efficient use of the limited IPv4 address space.

---

### Key Features of NAT:

1. **Purpose:** Enables devices in a private network (using private IPs) to access the internet via a shared public IP address.
2. **Scope:** Operates on **Layer 3 (Network Layer)** of the OSI model.
3. **Primary Use:** Address conservation, security, and connecting private networks to public networks like the internet.

---

### Types of NAT:

1. **Static NAT:**

   - One-to-one mapping between a private IP address and a public IP address.
   - Typically used when a device (e.g., a server) needs to be consistently accessible from the internet.
   - Example: `192.168.1.10 -> 203.0.113.10`.

2. **Dynamic NAT:**

   - A pool of public IP addresses is used to map private IPs.
   - When a private IP initiates a connection, it is temporarily assigned an available public IP from the pool.

3. **PAT (Port Address Translation) / Overloading:**
   - Multiple devices share a single public IP address by using different port numbers.
   - Most common form of NAT.
   - Example:
     - Device A: `192.168.1.2:12345 -> 203.0.113.10:54321`
     - Device B: `192.168.1.3:12346 -> 203.0.113.10:54322`

---

### How NAT Works:

1. **Request from Private Network to Internet:**
   - A device in the private network sends a packet with its **private IP** as the source.
   - The NAT router replaces the source IP with its public IP and forwards the packet to the internet.
2. **Response from the Internet:**
   - The external server sends a response back to the public IP of the NAT router.
   - The NAT router translates the public IP back to the original private IP using its NAT table and delivers the packet to the appropriate device.

---

### Advantages of NAT:

1. **IP Address Conservation:**
   - Allows multiple devices to share a single public IP.
2. **Security:**
   - Devices in the private network are not directly accessible from the internet.
3. **Flexibility:**
   - Enables private IP addressing within local networks without affecting internet connectivity.

---

### Limitations of NAT:

1. **Breaks End-to-End Connectivity:**
   - NAT modifies packet headers, which can disrupt certain protocols (e.g., VoIP, IPsec).
2. **Dependency on NAT Table:**
   - The router must maintain a NAT table, which can grow large in high-traffic environments.
3. **Not Needed in IPv6:**
   - IPv6 has a vast address space, eliminating the need for address conservation.

---

### Etymology of NAT:

- **"Network"**: Relates to the networking aspect of IP communication.
- **"Address"**: Refers to IP addresses (private and public) it translates.
- **"Translation"**: The process of mapping one IP address to another.

## Transport Layer | Responsibilities of Transport Layer | OSI Model

### **Transport Layer in the OSI Model**

The **Transport Layer** is the fourth layer of the **OSI (Open Systems Interconnection) model**. It is responsible for **end-to-end communication** between devices in a network, ensuring data is delivered **reliably, accurately**, and **in order**.

---

### **Responsibilities of the Transport Layer**

1. **Segmentation and Reassembly:**

   - Divides large data streams into smaller, manageable segments for transmission.
   - Reassembles the segments at the destination to recreate the original data.

2. **Connection Management:**

   - Establishes, maintains, and terminates connections between devices.
   - Types of connections:
     - **Connection-Oriented Communication:** Ensures a reliable connection (e.g., TCP).
     - **Connectionless Communication:** Sends data without prior setup (e.g., UDP).

3. **Flow Control:**

   - Regulates data flow to prevent the sender from overwhelming the receiver.
   - Uses techniques like **windowing** to manage data transmission speed.

4. **Error Detection and Correction:**

   - Ensures data integrity by detecting errors in transmission and requesting retransmission if necessary.
   - Common methods include checksums.

5. **Reliable Data Delivery:**

   - Confirms that data is delivered without duplication, loss, or corruption.
   - Utilizes acknowledgments (ACK) and retransmissions in connection-oriented protocols.

6. **Multiplexing and Demultiplexing:**

   - Multiplexing: Allows multiple applications to use the same network connection simultaneously by assigning **port numbers**.
   - Demultiplexing: Directs incoming data to the correct application based on the port number.

7. **Data Integrity and Sequencing:**

   - Ensures that data packets are received in the correct order.
   - Adds sequence numbers to packets to help with reordering at the receiver’s end.

8. **Port Addressing:**
   - Identifies specific processes or applications on a device using **port numbers** (e.g., HTTP uses port 80).

---

### **Transport Layer Protocols**

1. **TCP (Transmission Control Protocol):**

   - Reliable, connection-oriented protocol.
   - Ensures data delivery, flow control, and error correction.
   - Common applications: Web browsing (HTTP/HTTPS), email (SMTP), file transfer (FTP).

2. **UDP (User Datagram Protocol):**
   - Unreliable, connectionless protocol.
   - Faster but does not guarantee delivery or order.
   - Common applications: Video streaming, online gaming, VoIP.

---

### **Functions at a Glance**

| **Function**           | **Explanation**                                                 |
| ---------------------- | --------------------------------------------------------------- |
| **Connection Control** | Manages connections (setup, maintain, terminate).               |
| **Reliable Delivery**  | Ensures data is error-free, complete, and in order.             |
| **Segmentation**       | Splits data for efficient transfer.                             |
| **Flow Control**       | Prevents data overflow by balancing sender and receiver speeds. |
| **Error Handling**     | Detects and corrects transmission errors.                       |
| **Port Numbering**     | Allows multiple applications to share a network connection.     |

---

### **Etymology of the Transport Layer**

- **"Transport":** Derived from Latin _transportare_ ("to carry across"), indicating its role in carrying data across networks.
- **Layer:** Indicates its structured position within the OSI model.

## Why both IP & Port address is used for Connection | Socket Address

A **socket address** is the combination of an **IP address** and a **port number**. It uniquely identifies a specific communication endpoint in a network, allowing devices and applications to send and receive data precisely.

---

### **Components of a Socket Address**

1. **IP Address:**
   - Identifies the device (host) in the network.
   - Examples: `192.168.1.1` (IPv4) or `2001:db8::1` (IPv6).
2. **Port Number:**
   - Identifies the specific application or process on the device.
   - Examples:
     - `80` for HTTP (web browsing),
     - `443` for HTTPS (secure web browsing),
     - `22` for SSH (remote terminal).

Together, they create a **socket** in the format:  
`<IP Address>:<Port Number>`  
For example:

- `192.168.1.2:5000`
- `203.0.113.10:80`

---

### **Why is a Socket Address Important?**

A socket address allows:

1. **Multiple Applications to Communicate Simultaneously:**
   - A single device can host multiple services (e.g., a web server, FTP server) by associating each with a different port.
   - Example: A server at `203.0.113.10` can have:
     - Web service: `203.0.113.10:80`
     - File transfer service: `203.0.113.10:21`
2. **End-to-End Communication:**

   - Combines the IP (to locate the device) with the port (to locate the application) for precise data delivery.
   - Example:
     - Your browser communicates with `192.168.1.10:80` (web server on port 80).

3. **Unique Identification of Connections:**
   - Even if two devices have the same IP, they can be distinguished by their ports.
   - Example: Two applications on `192.168.1.2`:
     - App 1 uses `192.168.1.2:5000`
     - App 2 uses `192.168.1.2:5001`

---

### **Socket Address in Client-Server Communication**

In a client-server model:

1. **Client Side:**

   - The client uses its own IP and an ephemeral (temporary) port number for the connection.
   - Example: Client uses `192.168.1.2:49321`.

2. **Server Side:**
   - The server uses a well-known IP and port number to listen for incoming connections.
   - Example: Server listens on `203.0.113.10:80`.

When the connection is established, the complete **socket pair** uniquely identifies the session:

- `Client Socket Address`: `192.168.1.2:49321`
- `Server Socket Address`: `203.0.113.10:80`

---

### **Analogy**

Think of a socket address as:

- **IP Address** = The street address of a building.
- **Port Number** = The specific apartment in that building.

Without both, a delivery (data) cannot reach its precise destination.

---

## Transmission control protocol | TCP Header | Transport layer

### **Transmission Control Protocol (TCP)**

**Transmission Control Protocol (TCP)** is a **connection-oriented** protocol at the Transport Layer of the OSI and TCP/IP models. It ensures reliable data transfer between devices, meaning data is delivered without errors, in the correct order, and without duplication.

---

### **Key Features of TCP**:

1. **Reliable Communication**:
   - Guarantees data delivery through acknowledgments and retransmissions if data is lost or corrupted.
2. **Connection-Oriented**:
   - Requires a three-way handshake to establish a connection and a four-way handshake to terminate it.
3. **Error Detection and Correction**:
   - Uses checksums to detect errors in data and retransmits lost packets.
4. **Flow Control**:
   - Prevents overwhelming the receiver by using window size adjustments.
5. **Sequencing**:
   - Assigns sequence numbers to packets to ensure they are reassembled in the correct order at the receiver.
6. **Full-Duplex Communication**:
   - Allows simultaneous data exchange in both directions.

---

### **TCP Header**

The **TCP header** is a part of each TCP segment. It contains essential information for managing communication between devices.

#### **Structure of the TCP Header (20–60 bytes)**:

| **Field**                 | **Size (bits)** | **Description**                                                                                                       |
| ------------------------- | --------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Source Port**           | 16              | Identifies the application or process on the sender's device.                                                         |
| **Destination Port**      | 16              | Identifies the application or process on the receiver's device.                                                       |
| **Sequence Number**       | 32              | Specifies the position of the first byte of data in the segment within the overall data stream.                       |
| **Acknowledgment Number** | 32              | Used to confirm receipt of data by the receiver; indicates the next byte expected from the sender.                    |
| **Data Offset**           | 4               | Specifies the size of the TCP header (in 32-bit words), allowing for optional fields.                                 |
| **Reserved**              | 6               | Reserved for future use; always set to zero.                                                                          |
| **Control Flags**         | 6               | Includes flags like SYN, ACK, FIN, RST, PSH, and URG to control connection establishment, termination, and data flow. |
| **Window Size**           | 16              | Indicates the size of the receive window, used for flow control.                                                      |
| **Checksum**              | 16              | Validates the integrity of the TCP header and data.                                                                   |
| **Urgent Pointer**        | 16              | Points to urgent data in the segment if the URG flag is set.                                                          |
| **Options (Optional)**    | Variable        | Provides additional functionalities, such as maximum segment size (MSS), window scaling, and timestamping.            |
| **Data (Payload)**        | Variable        | The actual data being transmitted by the application layer.                                                           |

---

#### **TCP Control Flags (6 bits)**:

- **SYN**: Initiates a connection.
- **ACK**: Acknowledges receipt of data.
- **FIN**: Terminates a connection.
- **RST**: Resets a connection.
- **PSH**: Indicates urgent data, prompting immediate delivery to the application.
- **URG**: Flags that urgent data exists, referenced by the Urgent Pointer.

---

### **TCP at the Transport Layer**

1. **Connection Establishment** (_Three-Way Handshake_):

   - **Step 1 (SYN):** The client sends a SYN segment to the server, requesting a connection.
   - **Step 2 (SYN-ACK):** The server responds with a SYN-ACK segment, acknowledging the client's request.
   - **Step 3 (ACK):** The client sends an ACK segment, completing the handshake.

2. **Data Transfer**:

   - Data is transmitted in segments, each with a sequence number.
   - Acknowledgments (ACKs) ensure reliable delivery and order.

3. **Connection Termination** (_Four-Way Handshake_):
   - **FIN/ACK exchange** ensures both parties agree to terminate the connection.

---

### **Benefits of TCP**:

1. Reliable data delivery.
2. Data sequencing and integrity checks.
3. Handles congestion and flow control.

### **Limitations of TCP**:

1. Increased overhead due to connection management and acknowledgments.
2. Slower than UDP for real-time applications like video streaming or gaming.

---

## TCP Connection Establishment and Termination

TCP (Transmission Control Protocol) uses **connection-oriented communication**, which requires a **three-way handshake** to establish a connection and a **four-way handshake** to terminate it. This ensures reliable communication.

---

### **1. Connection Establishment: Three-Way Handshake**

The three-way handshake is a process to establish a TCP connection between a client and a server. It ensures both parties are ready to communicate and agree on the parameters (e.g., sequence numbers).

#### **Steps in Three-Way Handshake**:

1. **SYN (Synchronize)**:

   - The client sends a TCP segment with the SYN flag set.
   - This segment contains an initial **sequence number** (e.g., `Seq = X`), which begins the sequence numbering for the session.
   - The client is essentially saying:  
     _"I want to start communication. Here’s my initial sequence number."_

   ```
   Client → Server: [SYN, Seq = X]
   ```

2. **SYN-ACK (Synchronize + Acknowledge)**:

   - The server responds with a TCP segment with both SYN and ACK flags set.
   - The **ACK** acknowledges the client’s sequence number (`Ack = X + 1`).
   - The **SYN** contains the server’s initial sequence number (`Seq = Y`).

   ```
   Server → Client: [SYN, Seq = Y, ACK = X + 1]
   ```

3. **ACK (Acknowledge)**:

   - The client sends a final ACK segment.
   - The **ACK** acknowledges the server’s sequence number (`Ack = Y + 1`).
   - After this step, the connection is established.

   ```
   Client → Server: [ACK, Seq = X + 1, ACK = Y + 1]
   ```

#### **Summary of Three-Way Handshake**:

| **Step**           | **Action**                 | **Control Flags** |
| ------------------ | -------------------------- | ----------------- |
| 1. Client → Server | Send initial SYN segment   | SYN               |
| 2. Server → Client | Respond with SYN-ACK       | SYN, ACK          |
| 3. Client → Server | Final acknowledgment (ACK) | ACK               |

---

### **2. Connection Termination: Four-Way Handshake**

TCP uses a four-step process to terminate a connection gracefully. Both the client and server must agree to terminate communication.

#### **Steps in Four-Way Handshake**:

1. **FIN (Finish)**:

   - The party initiating termination (e.g., client) sends a FIN segment.
   - This indicates it has no more data to send.

   ```
   Client → Server: [FIN, Seq = X]
   ```

2. **ACK (Acknowledge)**:

   - The receiver (e.g., server) acknowledges the FIN with an ACK.
   - The connection is now **half-closed**, meaning the server can still send data to the client.

   ```
   Server → Client: [ACK, Seq = Y, ACK = X + 1]
   ```

3. **FIN (Finish)**:

   - The server sends a FIN segment to indicate it has finished sending data.

   ```
   Server → Client: [FIN, Seq = Y]
   ```

4. **ACK (Acknowledge)**:

   - The client sends a final ACK to acknowledge the server's FIN.
   - The connection is fully terminated.

   ```
   Client → Server: [ACK, Seq = X + 1, ACK = Y + 1]
   ```

#### **Summary of Four-Way Handshake**:

| **Step**           | **Action**                     | **Control Flags** |
| ------------------ | ------------------------------ | ----------------- |
| 1. Client → Server | Initiates termination with FIN | FIN               |
| 2. Server → Client | Acknowledges FIN               | ACK               |
| 3. Server → Client | Sends its own FIN              | FIN               |
| 4. Client → Server | Acknowledges server's FIN      | ACK               |

---

### **Connection Reset (Optional)**

If an error occurs or one side needs to abruptly terminate the connection, a **RST (Reset)** flag is used to immediately close the connection without following the graceful handshake.

---

### **Visual Summary**

#### Connection Establishment (Three-Way Handshake):

```
Client          Server
   SYN  -------->
        <--------  SYN-ACK
   ACK  -------->
Connection Established
```

#### Connection Termination (Four-Way Handshake):

```
Client          Server
   FIN  -------->
        <--------  ACK
        <--------  FIN
   ACK  -------->
Connection Terminated
```

---

### **Why Use Handshakes?**

- **Three-Way Handshake**:
  - Ensures both parties are ready and agree on initial sequence numbers for reliable communication.
- **Four-Way Handshake**:
  - Gracefully closes the connection, ensuring all data is transmitted and acknowledged before termination.
