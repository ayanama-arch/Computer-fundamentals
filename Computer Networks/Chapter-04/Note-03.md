# Networking

### Ethernet Frame Format (IEEE 802.3

Ethernet, defined by the **IEEE 802.3** standard, uses a structured frame format to encapsulate data for transmission at the **Data Link Layer** of the OSI model. The Ethernet frame contains various fields to ensure data is transmitted efficiently and reliably across a network.

---

### **Structure of an Ethernet Frame**

The Ethernet frame consists of the following key fields:

| **Field**                          | **Length (Bytes)** | **Description**                                                                 |
| ---------------------------------- | ------------------ | ------------------------------------------------------------------------------- |
| **Preamble**                       | 7                  | Synchronization sequence to alert receiving devices of incoming data.           |
| **Start of Frame Delimiter (SFD)** | 1                  | Marks the beginning of the frame.                                               |
| **Destination MAC Address**        | 6                  | MAC address of the receiving device.                                            |
| **Source MAC Address**             | 6                  | MAC address of the sending device.                                              |
| **EtherType/Length**               | 2                  | Indicates the type of protocol (e.g., IPv4, IPv6) or length of the payload.     |
| **Payload (Data)**                 | 46–1500            | Actual data being transmitted (can include headers for higher-layer protocols). |
| **Frame Check Sequence (FCS)**     | 4                  | CRC for error detection.                                                        |

---

### **Detailed Description of Fields**

1. **Preamble (7 Bytes):**

   - A sequence of alternating `1`s and `0`s (`101010...`) used to synchronize the sending and receiving devices.
   - Ensures that the receiver's clock is in sync with the transmitter.

2. **Start of Frame Delimiter (SFD) (1 Byte):**

   - A special sequence (`10101011`) indicating the start of the actual frame data.
   - Follows the preamble.

3. **Destination MAC Address (6 Bytes):**

   - Specifies the MAC address of the intended recipient.
   - Can be a **unicast** (single device), **multicast** (group of devices), or **broadcast** address.

4. **Source MAC Address (6 Bytes):**

   - Identifies the MAC address of the device sending the frame.

5. **EtherType/Length (2 Bytes):**

   - Can specify:
     - **EtherType**: Indicates the type of higher-layer protocol (e.g., IPv4, IPv6, ARP).
     - **Length**: Indicates the length of the data payload in some Ethernet variants.
   - Values greater than `1500` indicate EtherType, while values less than or equal to `1500` represent length.

6. **Payload (Data) (46–1500 Bytes):**

   - Contains the actual data being transmitted, such as an IP packet.
   - The minimum payload size is **46 bytes**, and padding is added if the data is smaller.

7. **Frame Check Sequence (FCS) (4 Bytes):**
   - A **Cyclic Redundancy Check (CRC)** used to detect transmission errors.
   - The receiver recalculates the CRC and compares it with the FCS value. If they differ, the frame is discarded.

---

### **Minimum and Maximum Frame Size**

1. **Minimum Frame Size:**

   - 64 bytes (including all fields).
   - Frames smaller than this are considered "runt frames" and are discarded.

2. **Maximum Frame Size:**
   - 1518 bytes (excluding optional extensions like jumbo frames).
   - Frames larger than this are "giant frames" and are typically discarded unless jumbo frames are supported.

---

### **Visual Representation of Ethernet Frame**

```
+----------+------+--------------------+------------------+---------+------------+-----+
| Preamble | SFD  | Destination MAC   | Source MAC       | Type/   | Payload    | FCS |
| (7 bytes)| (1B) | Address (6 bytes) | Address (6 bytes)| Length  | (46–1500B) |(4B)|
+----------+------+--------------------+------------------+---------+------------+-----+
```

---

### **Additional Notes**

- **Padding:** If the payload is less than 46 bytes, padding (extra bytes) is added to ensure the frame meets the minimum size of 64 bytes.
- **Interframe Gap:** After each frame, a mandatory gap (96-bit times) is maintained to allow devices time to process the frame and prepare for the next transmission.

---

### **Use Cases of Ethernet Frames**

1. **IPv4 and IPv6 Networking:** Encapsulates IP packets for LAN communication.
2. **ARP (Address Resolution Protocol):** Resolves MAC addresses from IP addresses.
3. **VLAN Tagging (802.1Q):** Adds a 4-byte VLAN tag to the Ethernet frame for network segmentation.

Ethernet frames form the backbone of local area network (LAN) communication, providing a reliable structure for data transfer while ensuring compatibility with a variety of higher-layer protocols.

## Token Ring (IEEE 802.5

The **Token Ring** network protocol is a **local area network (LAN)** standard defined by **IEEE 802.5**, originally developed by IBM. It operates using a token-passing mechanism where a token (a special frame) circulates around the network, granting the device holding it permission to transmit data. This ensures controlled access to the shared communication medium and avoids collisions.

---

### **Key Features of Token Ring**

1. **Topology:**

   - Uses a **logical ring** topology where data travels in one direction around the ring.
   - Physically, it often uses a **star topology** with a central hub called a **Multistation Access Unit (MAU)**.

2. **Token Passing:**

   - Only the device holding the token can transmit data, preventing collisions.
   - Once data is transmitted, the token is released and passed to the next device in the ring.

3. **Deterministic Access:**
   - Predictable performance since each device gets a chance to transmit.
   - Well-suited for real-time applications where delay predictability is crucial.

---

### **Token Ring Frame Format**

A Token Ring frame consists of the following fields:

| **Field**                      | **Description**                                                                      |
| ------------------------------ | ------------------------------------------------------------------------------------ |
| **Starting Delimiter (SD)**    | Marks the start of the frame.                                                        |
| **Access Control (AC)**        | Controls the priority of access to the token.                                        |
| **Frame Control (FC)**         | Indicates whether the frame contains data or control information.                    |
| **Destination Address (DA)**   | MAC address of the receiving device.                                                 |
| **Source Address (SA)**        | MAC address of the transmitting device.                                              |
| **Data**                       | Contains the payload or actual data being transmitted.                               |
| **Frame Check Sequence (FCS)** | Error-checking field using cyclic redundancy check (CRC).                            |
| **Ending Delimiter (ED)**      | Marks the end of the frame.                                                          |
| **Frame Status (FS)**          | Indicates whether the frame was received and processed correctly by the destination. |

---

### **Operation of Token Ring**

1. **Token Circulation:**

   - A token circulates around the ring when no device is transmitting.
   - Devices monitor the token to determine when it is their turn to transmit.

2. **Transmission:**

   - When a device wants to send data, it captures the token.
   - The device modifies the token into a data frame, appending its source and destination addresses.
   - The frame travels around the ring until it reaches the intended recipient.

3. **Acknowledgment:**

   - The receiving device copies the data and marks the frame as "read."
   - The frame continues back to the sender, confirming successful delivery.

4. **Token Release:**
   - Once the sender confirms the delivery, it releases a new token into the ring, allowing other devices to transmit.

---

### **Advantages of Token Ring**

1. **Collision-Free Transmission:**
   - The token-passing method prevents collisions, making it more efficient than contention-based protocols like Ethernet (CSMA/CD) under high traffic.
2. **Deterministic Access:**

   - Ensures equal access to the network, making it ideal for time-sensitive applications.

3. **Error Detection:**
   - Built-in mechanisms like the **Frame Check Sequence (FCS)** ensure reliable communication.

---

### **Disadvantages of Token Ring**

1. **Latency:**
   - Devices must wait for the token to reach them, causing delays in high-traffic networks.
2. **Single Point of Failure:**
   - If the token is lost or a device in the ring fails, the entire network is affected.
3. **Scalability Issues:**

   - Performance degrades as the number of devices increases due to longer token circulation times.

4. **Higher Cost:**
   - Token Ring hardware (e.g., MAUs) is more expensive than Ethernet hardware.

---

### **Token Ring vs. Ethernet**

| **Feature**            | **Token Ring**              | **Ethernet**               |
| ---------------------- | --------------------------- | -------------------------- |
| **Access Method**      | Token-passing               | CSMA/CD or CSMA/CA         |
| **Collision Handling** | Collision-free              | Collisions can occur       |
| **Topology**           | Logical ring, physical star | Logical bus, physical star |
| **Efficiency**         | High under heavy load       | High under light load      |
| **Cost**               | Higher                      | Lower                      |
| **Scalability**        | Limited due to latency      | Better scalability         |

---

### **Applications**

1. **Industrial Networks:**
   - Used in real-time systems requiring collision-free and predictable performance.
2. **Legacy Systems:**
   - Previously popular in corporate LANs but largely replaced by Ethernet due to cost and performance improvements.

---

### **Current Relevance**

Token Ring has largely been replaced by Ethernet in modern networks due to Ethernet’s simplicity, cost-effectiveness, and better performance in most use cases. However, its deterministic nature and efficient access control made it a foundational protocol in networking history.

## Network Layer in OSI Model

The **Network Layer** is the **third layer** of the **OSI (Open Systems Interconnection) Model**. It plays a critical role in facilitating communication between devices across different networks by determining the best path for data transmission.

---

### **Responsibilities of the Network Layer**

1. **Logical Addressing:**

   - Assigns unique addresses (e.g., IP addresses) to devices to enable identification and communication between hosts in different networks.
   - Logical addressing is essential for identifying the source and destination of data packets.

2. **Routing:**

   - Determines the best path for data to travel from source to destination.
   - Utilizes routing algorithms and protocols (e.g., RIP, OSPF, BGP) to forward packets efficiently.

3. **Packet Forwarding:**

   - Transfers packets from one network to another using routers.
   - Ensures that data reaches its intended destination by analyzing routing tables and forwarding decisions.

4. **Fragmentation and Reassembly:**

   - Divides larger packets into smaller fragments if the packet size exceeds the Maximum Transmission Unit (MTU) of the network.
   - Reassembles the fragments at the destination to reconstruct the original data.

5. **Error Handling and Diagnostics:**

   - Detects and reports errors using protocols like ICMP (Internet Control Message Protocol).
   - Helps identify network issues such as unreachable hosts or network congestion.

6. **Traffic Control:**

   - Manages data flow to prevent congestion in the network.
   - Ensures fair utilization of network resources.

7. **Quality of Service (QoS):**

   - Prioritizes certain types of traffic (e.g., VoIP, streaming) to meet performance requirements.
   - Ensures timely delivery of critical data.

8. **Inter-Network Communication:**
   - Enables communication between devices on different networks, making it possible to connect multiple subnetworks into a single larger network.

---

### **Key Protocols in the Network Layer**

1. **Internet Protocol (IP):**
   - IPv4 and IPv6 are the most widely used protocols for addressing and routing.
2. **ICMP (Internet Control Message Protocol):**
   - Used for error reporting and diagnostic functions.
3. **ARP (Address Resolution Protocol):**
   - Resolves IP addresses to MAC addresses in a local network.
4. **RARP (Reverse ARP):**
   - Maps MAC addresses to IP addresses.
5. **Routing Protocols:**
   - **RIP (Routing Information Protocol):** Simple distance-vector routing protocol.
   - **OSPF (Open Shortest Path First):** Link-state routing protocol for large networks.
   - **BGP (Border Gateway Protocol):** Protocol used to exchange routing information between different autonomous systems on the internet.

---

### **Functions in Real-World Scenarios**

- **Data Delivery Across Networks:**
  - E.g., Sending an email from a device in one country to another requires the network layer to ensure the packet travels across routers and reaches the recipient.
- **Error Reporting:**

  - If a router cannot forward a packet due to an unreachable network, ICMP sends an error message back to the source.

- **Path Optimization:**
  - Routing protocols determine the shortest or most reliable path to deliver data efficiently.

---

### **Comparison with Other OSI Layers**

| **Aspect**            | **Network Layer**                 | **Data Link Layer**                                          | **Transport Layer**               |
| --------------------- | --------------------------------- | ------------------------------------------------------------ | --------------------------------- |
| **Purpose**           | Routing and logical addressing    | Physical addressing and error-free transfer on a single link | Reliable end-to-end communication |
| **Addressing**        | Logical addressing (IP addresses) | Physical addressing (MAC addresses)                          | Port numbers for applications     |
| **Device**            | Router                            | Switch, bridge                                               | Host or server                    |
| **Protocol Examples** | IP, ICMP, ARP, RIP, OSPF          | Ethernet, Wi-Fi                                              | TCP, UDP                          |

---

### **Conclusion**

The Network Layer is essential for enabling inter-network communication by ensuring that data packets are logically addressed, routed, and forwarded efficiently to their destination. It acts as the backbone of the internet and most networking systems, providing the functionality to connect diverse networks worldwide.
