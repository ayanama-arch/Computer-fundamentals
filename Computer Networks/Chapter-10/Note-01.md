# Networking

## Socket Programming

When multiple users send requests to your server simultaneously, especially when each request requires computing power (like data processing or complex calculations), the server must handle these concurrent requests efficiently. Here's how it typically works:

### **1. Concurrency and Parallelism:**

- **Concurrency** refers to the server’s ability to manage multiple requests at the same time, while **parallelism** refers to performing multiple tasks at the exact same time (usually with multiple CPU cores).
- Servers use various techniques to handle multiple requests simultaneously, even if those requests require significant computational resources.

### **2. Techniques Used by Servers to Handle Multiple Requests:**

#### **A. Event-Driven / Non-blocking I/O (Asynchronous Handling):**

- **Asynchronous Programming** (using Node.js, for example) is a common approach to handle multiple requests. The server doesn’t need to wait for a request to complete (such as a calculation or database query) before moving on to another request.
- Instead of blocking the server, it allows the server to process other requests while waiting for a response from the long-running tasks.

**Example:**

- If one request requires complex computation (like data processing) or waits for a database query, the server can continue handling other requests without being blocked. Once the computation or database query finishes, the server responds to that specific request.

#### **B. Load Balancing:**

- **Load Balancers** distribute incoming traffic across multiple servers or instances of your application, ensuring that no single server is overwhelmed with too many requests.
- When many users make requests at the same time, the load balancer will divide the workload, sending requests to different servers based on factors like server health and capacity.
- This allows the server infrastructure to scale horizontally and ensures that individual servers don’t get overloaded.

**Example:**

- If you have multiple backend servers running your application, a load balancer will direct requests to the least loaded server, ensuring better resource utilization and preventing a single server from being overburdened.

#### **C. Threading (for CPU-bound Tasks):**

- In traditional multi-threaded server architectures (like with Java or Python's `threading` module), each request could be handled by a separate thread. If you’re running compute-heavy tasks (CPU-bound operations), this approach allows multiple tasks to be processed in parallel.
- The server assigns different CPU threads to handle different user requests. However, this approach is limited by the number of available CPU cores—too many threads could lead to **context switching** and inefficiency.

**Example:**

- A server with 8 CPU cores can handle 8 threads concurrently, but more than 8 threads might cause performance degradation due to the overhead of context switching.

#### **D. Worker Queues (Task Queues):**

- For very compute-intensive tasks, you may need to use **task queues** to manage load.
- When a user’s request requires significant computation (such as heavy data processing), it can be added to a queue (like **RabbitMQ**, **Redis Queue**, or **Amazon SQS**), and the task can be processed by **worker processes**.
- Worker processes are dedicated to pulling tasks from the queue and performing computations asynchronously, without affecting the responsiveness of the server for other users.

**Example:**

- A user submits a request for data processing, and the task is added to a queue. Worker servers or processes pull tasks from the queue and process them. Meanwhile, the server can continue serving other users without waiting for the computation to complete.

### **3. Caching to Reduce Load:**

- **Caching** is a technique to store the results of frequent computations or database queries, so that if the same data or result is requested again, it can be quickly retrieved from the cache, avoiding repetitive calculations.
- This reduces the load on your server and improves response times for users.

**Example:**

- If many users request the same data (like a popular report), the server can cache the result after computing it once, and subsequent requests can get the result directly from the cache (e.g., using **Redis** or **Memcached**).

### **4. Horizontal and Vertical Scaling:**

- **Vertical Scaling:** You increase the resources (CPU, RAM) of a single server. This is useful for improving the performance of individual instances but has limits.
- **Horizontal Scaling:** You add more servers or instances of your application to handle increased load. Horizontal scaling is more scalable and is commonly used in large-scale applications to handle high traffic and computationally expensive tasks.

**Example:**

- If you have high traffic, you might run your application on several servers (e.g., multiple EC2 instances on AWS). Load balancers distribute incoming requests among these servers, allowing the system to handle more traffic efficiently.

### **5. Microservices and Distributed Computing:**

- If your application grows, you might consider breaking it into smaller, manageable services (microservices) that can be deployed on separate servers. These services can be optimized for specific tasks and scale independently.
- In addition, distributed computing frameworks like **Apache Kafka**, **Apache Spark**, or **MapReduce** can help distribute the computation-heavy tasks across multiple nodes, allowing the system to scale efficiently.

---

### **In Summary:**

When multiple users request computation-heavy tasks, modern servers handle this load using:

1. **Asynchronous (non-blocking) programming** to avoid waiting on tasks.
2. **Load balancing** to distribute requests across multiple servers.
3. **Threading** or **Worker Queues** to parallelize compute-intensive tasks.
4. **Caching** to speed up frequent requests.
5. **Horizontal scaling** (multiple servers) and sometimes **vertical scaling** (more powerful servers) to handle more users.

By leveraging these techniques, you can ensure that your application scales effectively and provides a smooth user experience even under heavy load. Let me know if you'd like to dive deeper into any of these strategies!

## Need of IPv6 Protocol

The **IPv6 (Internet Protocol version 6)** protocol is the latest version of the Internet Protocol designed to replace the older **IPv4** protocol. It was introduced to address several issues and limitations in IPv4, which is still widely used today. IPv6 is necessary due to the increasing demand for IP addresses as the internet continues to grow and expand, along with several other technical reasons.

Here are the primary **needs** for the IPv6 protocol:

### 1. **Exhaustion of IPv4 Addresses**

- **IPv4** uses a 32-bit address space, which provides about 4.3 billion unique IP addresses. While this might have seemed like a large number initially, the rapid growth of the internet, the proliferation of internet-connected devices (like smartphones, IoT devices, etc.), and the expansion of the internet to more regions, have caused IPv4 addresses to be exhausted.
- **IPv6** uses a 128-bit address space, providing a virtually unlimited number of addresses (approximately 340 undecillion, or \( 3.4 \times 10^{38} \) addresses). This ensures that there will be enough addresses for the foreseeable future.

**Example**:

- IPv4 has already reached exhaustion in many regions, leading to the adoption of techniques like **NAT (Network Address Translation)** to extend the use of the available addresses, which complicates network configurations. IPv6 eliminates the need for NAT by providing enough addresses for each device to have its own unique address.

### 2. **Simplified Network Configuration**

- **IPv6** offers automatic configuration via **Stateless Address Autoconfiguration (SLAAC)**. Devices can automatically configure themselves with an IPv6 address without requiring a DHCP (Dynamic Host Configuration Protocol) server.
- With IPv4, **DHCP** is required for address assignment, and there are manual configurations for devices on smaller networks, which can become cumbersome.

**Benefits:**

- IPv6 reduces the administrative burden on network administrators by automating the address configuration and eliminating manual IP assignment for each device.

### 3. **Improved Security Features**

- **IPv6** was designed with security in mind. The protocol mandates the use of **IPsec** (Internet Protocol Security), which provides confidentiality, integrity, and authentication at the IP layer.
- In contrast, while **IPv4** also supports IPsec, it is not mandatory, meaning many IPv4 networks lack this layer of security.
- IPv6 encryption (through IPsec) ensures better data protection and secure communication between devices.

### 4. **Better Performance and Efficiency**

- **IPv6** simplifies packet headers, which allows routers to process packets more efficiently. This can lead to better network performance, especially in large-scale networks.
- **IPv4** requires additional checks for fragmentation and header options, whereas **IPv6** minimizes the need for fragmentation at the router level by requiring that devices send packets that fit the Maximum Transmission Unit (MTU) size.

**Improved efficiency**:

- IPv6 routers can process packets more quickly and efficiently, which improves the overall performance of large-scale networks.

### 5. **End-to-End Connectivity**

- **IPv6** restores the end-to-end connectivity that was a hallmark of the original internet design. In IPv4 networks, many devices are behind NAT (Network Address Translation) or firewalls, which can complicate direct communication between devices.
- With IPv6, every device can have its unique, globally routable address, making it easier for devices to communicate directly with each other (peer-to-peer) without the need for NAT.

**Example**:

- Devices like IoT devices, smart home systems, and other interconnected devices can easily communicate with each other over IPv6 without needing to route traffic through a central server or rely on NAT.

### 6. **Better Support for Mobile Devices**

- **IPv6** offers better support for **mobile devices** by enabling **mobile IP** functionality, which allows devices to seamlessly move between networks without losing their IP address.
- This is important for the growth of mobile internet usage and ensures that mobile devices can stay connected even when changing network access points.

**IPv6 and Mobile IP**:

- It allows devices (such as smartphones or tablets) to retain their IP address when moving from one network to another, such as from a Wi-Fi network to a cellular network.

### 7. **Improved Multicast and Anycast Support**

- **IPv6** improves support for **multicast** and **anycast** communications:
  - **Multicast** allows data to be sent to multiple destinations in a single transmission, which is more efficient than sending individual messages.
  - **Anycast** allows data to be sent to the nearest or best destination out of a group of potential receivers. This is ideal for improving services like load balancing and content delivery.

**In contrast**, IPv4 has limited support for multicast and no native support for anycast.

### 8. **Future-Proofing**

- **IPv6** is designed to support the growing trend of the **Internet of Things (IoT)**. As more devices are connected to the internet, the number of devices needing unique IP addresses is increasing dramatically. IPv6 provides the scalability needed to accommodate this growth.

**Example**:

- A smart city might have billions of devices, such as sensors, cameras, smart meters, and other IoT devices. IPv6 provides the capacity to handle this massive number of devices, unlike IPv4.

### **Summary of the Key Needs for IPv6:**

1. **Address Space**: To solve the problem of IPv4 address exhaustion.
2. **Simplified Configuration**: To automate and simplify network configurations.
3. **Security**: Mandatory support for IPsec to improve security.
4. **Performance**: More efficient packet processing and routing.
5. **End-to-End Connectivity**: Direct communication without the need for NAT.
6. **Mobile Support**: Better support for mobile devices and mobility.
7. **Multicast/Anycast**: Enhanced support for multicast and anycast services.
8. **Scalability for IoT**: Supports the rapid growth of IoT devices.

### **Conclusion:**

IPv6 is necessary to meet the growing demand for IP addresses, improve security, simplify network management, and ensure efficient communication between billions of devices. As the internet continues to evolve, IPv6 is positioned as the key enabler for continued growth and innovation in networked communication.

## IPSec Protocol

**IPsec (Internet Protocol Security)** is a suite of protocols used to secure **IP communications** by authenticating and encrypting each IP packet in a communication session. It operates at the **Network Layer** of the OSI model (Layer 3), and it is designed to provide secure data transmission over an insecure network like the internet.

IPsec ensures confidentiality, integrity, and authenticity of data, making it essential for securing VPNs (Virtual Private Networks), site-to-site communications, and various other network security applications.

### Key Features of IPsec:

1. **Confidentiality**:
   - Ensures that the data being transmitted cannot be read by unauthorized parties. This is achieved through encryption.
2. **Data Integrity**:

   - Ensures that the data has not been tampered with during transmission. Integrity is typically maintained through the use of hash functions (e.g., HMAC).

3. **Authentication**:

   - Verifies that the sender of the data is who they claim to be. Authentication can be done using certificates or pre-shared keys (PSK).

4. **Anti-Replay Protection**:

   - Prevents attackers from capturing and re-transmitting legitimate packets to deceive the recipient into processing them again.

5. **Access Control**:
   - Limits access to authorized devices and networks through policies defined in the IPsec configuration.

### How IPsec Works:

IPsec operates in two main modes:

#### 1. **Transport Mode**:

- In this mode, only the **payload** (the data being transmitted) of the IP packet is encrypted and/or authenticated.
- The **IP header** remains intact, so the packet can still be routed based on the original destination address.
- **Transport mode** is typically used for end-to-end communications between two devices, like in VPNs where communication is secure between two hosts.

**Use case**: Communicating securely between two systems (e.g., client-server model).

#### 2. **Tunnel Mode**:

- In tunnel mode, **both the payload and the original IP header** are encrypted and authenticated.
- A new IP header is added to the packet, which helps in routing it through the network.
- **Tunnel mode** is typically used for site-to-site VPNs where two networks (often separated by untrusted networks like the internet) communicate securely with each other.

**Use case**: Securing communication between two networks, like connecting two branch offices through a secure VPN tunnel over the internet.

### IPsec Protocol Components:

1. **Authentication Header (AH)**:

   - Provides **data integrity**, **authentication**, and **anti-replay protection**. AH ensures that the data has not been altered and that it came from a legitimate source.
   - AH does not provide encryption, so data remains in plaintext.

   **Note**: AH is less commonly used in modern IPsec deployments because it cannot encrypt data, and ESP (Encapsulating Security Payload) is preferred for encryption.

2. **Encapsulating Security Payload (ESP)**:

   - Provides **data confidentiality** (encryption), **data integrity**, **authentication**, and **anti-replay protection**.
   - It encrypts the entire IP packet's payload, ensuring that data is confidential during transmission.
   - ESP is more commonly used in IPsec because it provides encryption, unlike AH.

3. **Security Associations (SAs)**:

   - An **SA** is a set of policies and parameters used to define the secure communication between two parties.
   - An SA is unidirectional, meaning two SAs are needed for a full-duplex communication (one for sending data and one for receiving data).
   - SAs are identified by a unique **Security Parameter Index (SPI)** and stored in a **Security Association Database (SAD)**.

4. **Key Management**:
   - IPsec requires key management to securely exchange encryption keys and establish a secure connection.
   - Two main protocols for key management in IPsec are:
     - **Internet Key Exchange (IKE)**: A protocol used to automate the process of negotiating, generating, and distributing encryption keys and establishing secure communication channels. It typically uses **Diffie-Hellman** for key exchange and **RSA** for authentication.
     - **Manual Keying**: In some simple cases, keys may be manually set up between the two parties, but this is generally not scalable or secure for larger systems.

### IPsec Protocol Architecture:

1. **Security Policy Database (SPD)**:

   - The SPD is a database on each device that specifies which traffic is protected by IPsec and how (i.e., which IPsec policies apply to which traffic).
   - The SPD also defines whether the traffic will be encrypted, authenticated, or both.

2. **Security Association Database (SAD)**:
   - The SAD is a database that stores information about the active security associations (SAs). Each entry in the SAD contains the specific algorithms, keys, and parameters used for securing a particular communication.

### IPsec and VPNs:

IPsec is widely used in Virtual Private Networks (VPNs) because of its ability to securely encrypt data over untrusted networks such as the internet. It creates a secure "tunnel" between the client and the server (or between two networks) to protect data as it travels between them.

- **Site-to-Site VPNs**: Connect two networks (e.g., branch offices) securely over the internet, allowing seamless communication between them.
- **Remote Access VPNs**: Allow individual users to securely access a private network from anywhere on the internet, ensuring the privacy and integrity of their data.

### Key Benefits of IPsec:

1. **Strong Encryption**: Ensures that data cannot be read by unauthorized parties.
2. **Authentication**: Guarantees that data is from a legitimate source.
3. **Data Integrity**: Ensures data has not been altered during transmission.
4. **Flexibility**: Can be used for various types of network security (VPNs, host-to-host, and site-to-site).
5. **Compatibility**: IPsec works across different networks and operating systems, allowing interoperability.

### Example Use Case: VPN Tunnel with IPsec

When a user wants to connect to a company’s internal network from a remote location (using a laptop or mobile device), an IPsec VPN can be used. The steps would generally involve:

- The user’s device sends an IPsec request to the VPN server.
- The VPN server authenticates the user and establishes a secure tunnel using IPsec (through ESP or AH).
- Data from the user is encrypted, transmitted over the internet, and decrypted at the other end of the tunnel.
- The user can now securely access internal company resources as if they were on the local network.

### Conclusion:

IPsec is an essential protocol for securing network communications. It provides confidentiality, authentication, data integrity, and anti-replay protection for IP packets, making it vital for securing communications in VPNs, remote access, and other network security applications. Its flexibility and robustness make it a key component in modern network security architectures.

## Transport Mode vs Tunnel Mode

**Transport Mode** and **Tunnel Mode** are two modes of operation in **IPsec (Internet Protocol Security)**, each with its distinct characteristics and use cases. Both modes aim to secure IP communications, but they do so in different ways depending on the specific requirements of the network.

### 1. **Transport Mode:**

- **Description**: In **Transport Mode**, only the **payload** (the data portion) of the IP packet is encrypted and/or authenticated. The **IP header** remains intact, meaning the original header, which contains routing information (e.g., source and destination IP addresses), is left unaltered.

- **Encryption/Authentication**:

  - Only the data (payload) is encrypted, and optionally, data integrity is ensured through hashing and authentication.
  - The **IP header** is **not encrypted** but may be **authenticated** for integrity.

- **Usage**:
  - **Transport Mode** is typically used for **end-to-end communication** between two hosts (e.g., client-to-server communication).
  - It is often used in situations where encryption or integrity protection is only required for the data and not for the entire IP packet.
- **Advantages**:
  - **Efficient**: Since only the payload is encrypted, this mode typically incurs less overhead than Tunnel Mode.
  - **Faster**: Since the IP header is left unaltered, packets are processed faster, which makes Transport Mode suitable for scenarios that require low-latency communication.
- **Example Use Case**:

  - **Host-to-Host** communication where two devices (like computers) on the same network or in a private network communicate securely without the need for changes to the routing information.

- **Diagram**:
  ```
  +--------------------------------------------+
  |   Original IP Packet                      |
  |--------------------------------------------|
  | Header: Source IP, Destination IP, etc.    |   <- Unchanged
  | Payload: Data (to be encrypted/authenticated) |
  +--------------------------------------------+
  ```

---

### 2. **Tunnel Mode:**

- **Description**: In **Tunnel Mode**, the **entire IP packet** (both the IP header and the payload) is encrypted and/or authenticated. A new **outer IP header** is added, which contains the destination address for the tunnel (i.e., the destination of the encrypted packet), while the original header is protected within the encrypted data.

- **Encryption/Authentication**:
  - Both the **IP header** and **payload** are encrypted.
  - A **new outer header** is added to route the packet through the network.
- **Usage**:
  - **Tunnel Mode** is primarily used for **network-to-network communication** (site-to-site VPNs) or for **host-to-network** connections (e.g., a client connecting to a VPN gateway).
  - It is ideal for creating secure tunnels between networks over untrusted networks (like the internet).
- **Advantages**:
  - **Privacy**: The entire IP packet, including the original IP header, is encrypted, which hides both the data and the routing information.
  - **Secure Site-to-Site Communication**: Tunnel Mode is used for securely connecting entire networks (e.g., branch offices to headquarters) over insecure networks (e.g., the internet).
  - **Network Flexibility**: By adding an outer IP header, Tunnel Mode can be used to mask the internal network structure and routing information.
- **Example Use Case**:

  - **VPN Tunnel** between two networks, such as connecting a branch office to a central office over the internet.

- **Diagram**:
  ```
  +------------------------------------------------------+
  |   Outer IP Header (New routing header)               |
  |   (Encrypted/Authenticated)                          |
  |------------------------------------------------------|
  |   Encrypted Original IP Header + Encrypted Payload   |  <- Entire packet encrypted
  |   (Data and original routing info)                   |
  +------------------------------------------------------+
  ```

---

### **Key Differences Between Transport Mode and Tunnel Mode:**

| **Feature**            | **Transport Mode**                                                              | **Tunnel Mode**                                                                         |
| ---------------------- | ------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **What is Encrypted**  | Only the **payload** (data) is encrypted.                                       | **Entire packet** (IP header + payload) is encrypted.                                   |
| **IP Header**          | **Unchanged**, only the payload is secured.                                     | **Encrypted**, and a new outer header is added.                                         |
| **Use Case**           | Primarily for **end-to-end communication** between hosts.                       | Typically for **site-to-site VPNs** or **network-to-network** communication.            |
| **Overhead**           | **Lower**, because only the payload is encrypted.                               | **Higher**, due to encryption of the entire packet and addition of outer headers.       |
| **Routing**            | No changes to routing information, as the IP header is not modified.            | Routing is based on the new outer header, while the internal network info is protected. |
| **Common Application** | Used for **client-to-server** communication or host-to-host secure connections. | Used for **VPNs** (site-to-site or remote access) and securing entire network traffic.  |

### Conclusion:

- **Transport Mode** is suitable for situations where only the **data** needs to be secured and when the routing information should remain visible, typically used for **host-to-host** communication.
- **Tunnel Mode** is best for **network-to-network** communications, especially when creating secure **VPN tunnels**, as it encrypts both the data and routing information, ensuring full privacy across insecure networks like the internet.

## Bandwidth vs. Throughput vs. Latency

**Bandwidth**, **Throughput**, and **Latency** are key concepts in networking and performance measurement. Though they are often used interchangeably, they each describe distinct aspects of network performance. Here's a breakdown of each term:

### 1. **Bandwidth**

- **Definition**: Bandwidth refers to the **maximum capacity** of a network connection or link to transmit data. It is the upper limit of the amount of data that can be transmitted over the network in a given period of time. It is typically measured in **bits per second (bps)**, with common units being **kilobits per second (Kbps)**, **megabits per second (Mbps)**, or **gigabits per second (Gbps)**.

- **Analogies**: Think of bandwidth as the width of a pipe. A wider pipe can carry more water, just as a higher bandwidth allows more data to be transferred at once.

- **Important Note**: Bandwidth is a **theoretical limit** of data transfer capacity, which means that it’s the potential maximum, not necessarily the actual data transfer.

- **Example**: A broadband connection with a bandwidth of **100 Mbps** means the connection can theoretically transfer 100 megabits of data every second.

---

### 2. **Throughput**

- **Definition**: Throughput is the actual **amount of data** that is successfully transmitted over the network in a given period of time. It is sometimes called **effective bandwidth** or **actual bandwidth** because it measures the real-world data transfer rate, factoring in network conditions, congestion, and other real-world issues.

- **Difference from Bandwidth**: While bandwidth is the **maximum capacity**, throughput is the **real-world performance**. Throughput can never exceed the available bandwidth, but it may be less than bandwidth due to factors such as packet loss, network congestion, and protocol overhead.

- **Units**: Throughput is measured in the same units as bandwidth, such as **Mbps** or **Gbps**.

- **Example**: If a network link has a bandwidth of **100 Mbps**, but network congestion or packet loss reduces the actual transfer rate to **80 Mbps**, the throughput is **80 Mbps**.

- **Factors Affecting Throughput**:
  - **Network congestion**: Heavy traffic can reduce throughput.
  - **Protocol overhead**: Network protocols (TCP/IP headers, encryption, etc.) add overhead that reduces the effective data transmitted.
  - **Packet loss**: Lost packets must be retransmitted, affecting throughput.
  - **Latency**: Higher latency can also impact throughput by reducing the efficiency of data transfers.

---

### 3. **Latency**

- **Definition**: Latency refers to the **time delay** it takes for data to travel from the source to the destination across the network. It is the **lag** or delay before the transfer of data begins and is typically measured in **milliseconds (ms)**.

- **Types of Latency**:

  - **Propagation Latency**: The time it takes for a signal to travel from the sender to the receiver through the medium (such as copper wires, fiber optics, or wireless).
  - **Transmission Latency**: The time it takes to push all the packet's bits into the link.
  - **Processing Latency**: Time taken by routers, switches, and other network devices to process packets.
  - **Queuing Latency**: Time spent waiting in the network's buffers due to congestion or high traffic.

- **Analogies**: Latency can be compared to the time it takes for a car to travel from point A to point B. Even if the car (data) is capable of driving at high speeds (high bandwidth), the **time it takes to travel** from A to B is determined by the road conditions (latency).

- **Example**: If a ping test to a server returns **20 ms**, it means that it takes **20 milliseconds** for data to travel from your computer to the server and back.

- **Factors Affecting Latency**:
  - **Distance**: The farther apart the source and destination are, the higher the latency (this is particularly noticeable in satellite connections due to the long distance to the satellite).
  - **Network devices**: Routers, switches, and other devices that handle and forward the data can add processing delays.
  - **Congestion**: High network traffic can lead to increased queuing delays, which adds latency.

---

### Comparison of Bandwidth, Throughput, and Latency:

| **Aspect**            | **Bandwidth**                                      | **Throughput**                                                  | **Latency**                                                          |
| --------------------- | -------------------------------------------------- | --------------------------------------------------------------- | -------------------------------------------------------------------- |
| **Definition**        | Maximum capacity of data transfer over a network.  | Actual amount of data transferred over the network.             | Time delay for data to travel from source to destination.            |
| **Units**             | Bits per second (bps), Kbps, Mbps, Gbps            | Same as bandwidth: bps, Kbps, Mbps, Gbps                        | Milliseconds (ms)                                                    |
| **What it Measures**  | Potential maximum data rate.                       | Actual data transfer rate in real-world conditions.             | Delay or lag between sending and receiving data.                     |
| **Real-World Impact** | Indicates network’s theoretical capacity.          | Indicates the actual performance of the network.                | Affects user experience in applications (e.g., video calls, gaming). |
| **Limitations**       | Does not account for congestion, packet loss, etc. | Can be lower than bandwidth due to congestion, overhead, etc.   | Can be affected by distance, network devices, and congestion.        |
| **Example**           | A network link with **100 Mbps** bandwidth.        | Actual throughput of **80 Mbps** in the presence of congestion. | Latency of **20 ms** to connect to a server.                         |

---

### Summary:

- **Bandwidth** is the **maximum potential speed** of data transfer over a network link.
- **Throughput** is the **actual achieved speed** of data transfer, factoring in network conditions and congestion.
- **Latency** is the **delay** before data starts to transfer, affecting the time it takes to send data from source to destination.

In practice, high **bandwidth** and low **latency** are both important for a fast, efficient network. However, even with high bandwidth, **throughput** can be impacted by **latency**, network congestion, or packet loss. Therefore, to achieve optimal network performance, all three aspects—bandwidth, throughput, and latency—must be considered.
