# Networking

## Circuit switching

**Circuit switching** is a method of communication in computer networks in which a dedicated communication path or "circuit" is established between two nodes (such as computers or phones) before data transmission begins. This path remains active for the duration of the communication session, providing a continuous and reserved channel for data flow. Circuit switching is widely used in traditional **telephone networks** and some **legacy computer networks** but is less common in modern computer networks, which often rely on **packet switching** instead.

### How Circuit Switching Works

Circuit switching involves three primary stages:

1. **Circuit Establishment**: A connection is established between the sender and receiver across a network of switches. This path is reserved and remains dedicated to the session.
2. **Data Transfer**: Once the circuit is established, data flows along this dedicated path. The path provides a consistent quality of service since it is not shared with other users.
3. **Circuit Teardown**: After the communication ends, the circuit is terminated, freeing up resources for other users.

### Characteristics of Circuit Switching

- **Dedicated Path**: The connection reserves a path through all the intermediary switches between the sender and receiver, ensuring a consistent communication channel.
- **Continuous Data Flow**: The data flows in a continuous stream, often ensuring low latency and minimal delay. This is ideal for real-time applications like voice calls.
- **Connection-Oriented**: Circuit switching requires establishing a connection before any data transfer, making it inherently connection-oriented.

### Advantages of Circuit Switching

1. **Predictable Performance**: Since the path is dedicated, users experience consistent performance without interruptions from other traffic.
2. **Low Latency**: There is minimal delay once the circuit is established, making it suitable for real-time applications like voice and video communication.
3. **Reliability**: Circuit switching ensures a stable and reliable connection as long as the circuit remains active.

### Disadvantages of Circuit Switching

1. **Inefficiency in Resource Usage**: The reserved circuit remains dedicated even if no data is being transmitted, leading to idle resources when there's no active communication.
2. **Setup Delay**: Establishing a dedicated path can introduce delays, especially if the network is busy, which can make circuit switching less ideal for data-intensive, bursty traffic.
3. **Scalability Limitations**: Circuit-switched networks require significant bandwidth and are less flexible in handling dynamic, high-volume data traffic.

### Circuit Switching vs. Packet Switching

| Feature                | Circuit Switching                              | Packet Switching                                             |
| ---------------------- | ---------------------------------------------- | ------------------------------------------------------------ |
| **Path Establishment** | Dedicated path established before transmission | No dedicated path; data sent in packets along various routes |
| **Efficiency**         | Inefficient due to dedicated, unused resources | More efficient; network resources shared among users         |
| **Latency**            | Low latency after setup                        | Potentially higher latency due to packet routing             |
| **Ideal Use**          | Voice calls, real-time communication           | Data communication, internet browsing, emails                |
| **Reliability**        | High reliability with dedicated circuit        | Packets may take different routes, subject to congestion     |

### Applications of Circuit Switching

- **Traditional Telephony**: Circuit switching is the basis of the Public Switched Telephone Network (PSTN), where a dedicated line is established for each call.
- **ISDN (Integrated Services Digital Network)**: Some legacy computer networks use circuit switching in ISDN connections to ensure dedicated bandwidth.
- **Some Military Networks**: Where reliable, continuous communication is essential.

Circuit switching has largely been replaced by packet switching in most modern data networks, particularly in the internet, as packet switching offers greater efficiency, scalability, and flexibility. However, circuit switching remains a relevant technology for specific use cases that demand dedicated bandwidth and low latency.

## Packet Switching

**Packet switching** is a communication method in computer networks where data is broken into smaller units called **packets** and sent independently across the network to reach the destination. Unlike circuit switching, which establishes a dedicated path for communication, packet switching sends packets through multiple routes, allowing them to traverse the network dynamically based on factors like network congestion and availability.

Packet switching is widely used in modern computer networks, including the **internet** and many other data networks, due to its efficiency, flexibility, and scalability.

### How Packet Switching Works

Packet switching involves three main stages:

1. **Data Segmentation**: Data is divided into packets, each containing a piece of the original message along with metadata, including the source and destination addresses.
2. **Packet Routing**: Each packet is routed independently through the network. Routers analyze the destination address of each packet and direct it toward its destination based on current network conditions, often taking different paths.
3. **Reassembly**: At the destination, packets are reassembled in the correct order to recreate the original message. This process accounts for packets arriving out of order due to taking different routes.

### Types of Packet Switching

There are two primary types of packet switching:

1. **Datagram Packet Switching**:

   - Each packet is treated independently and may take different paths to the destination.
   - Packets may arrive out of order and need to be reordered at the destination.
   - The internet uses a datagram packet-switching approach, with each packet following a potentially unique route.

2. **Virtual Circuit Packet Switching**:
   - A logical path, or "virtual circuit," is established between the source and destination, and packets follow this predetermined route.
   - Packets arrive in order, as they follow the same path through the network.
   - Virtual circuits are commonly used in **Frame Relay** and **ATM (Asynchronous Transfer Mode)** networks.

### Advantages of Packet Switching

1. **Efficient Use of Resources**: Packet switching shares network resources among multiple users, reducing idle time and making better use of available bandwidth.
2. **Scalability**: The network can handle a high volume of connections, as packets are routed dynamically based on current conditions.
3. **Reliability and Resilience**: If one route becomes congested or fails, packets can be rerouted, making packet-switched networks more resilient to failure.
4. **Cost-Effectiveness**: By allowing multiple connections to share the same network infrastructure, packet switching reduces the need for dedicated circuits, lowering costs.

### Disadvantages of Packet Switching

1. **Latency and Delay**: Due to variable routing and potential queuing at routers, packets may experience delays, making it less ideal for real-time applications like voice calls (though this is mitigated by technologies like **VoIP**).
2. **Potential Packet Loss**: Network congestion or routing errors can lead to packet loss, requiring retransmission and reassembly at the destination.
3. **Out-of-Order Delivery**: Since packets can take different paths, they may arrive out of order, adding complexity in reordering them at the destination.

### Comparison with Circuit Switching

| Feature                | Packet Switching                                   | Circuit Switching                                 |
| ---------------------- | -------------------------------------------------- | ------------------------------------------------- |
| **Path Establishment** | No dedicated path; packets routed dynamically      | Dedicated path established before communication   |
| **Efficiency**         | High; resources shared among multiple users        | Low; resources reserved even during inactivity    |
| **Latency**            | Potentially higher, but adaptable                  | Low after setup but setup may take time           |
| **Reliability**        | High, with alternate paths available               | Reliable but inflexible; vulnerable if path fails |
| **Ideal Use**          | Data transmission, internet browsing, file sharing | Real-time applications like traditional telephony |

### Applications of Packet Switching

- **Internet**: The internet relies on packet switching, with protocols like **IP** and **TCP** managing the packetization and reassembly process.
- **VoIP (Voice over Internet Protocol)**: Though originally a circuit-switched domain, voice communication has transitioned to packet switching, allowing voice data to be transmitted over the internet.
- **Email, Web Browsing, and File Sharing**: Packet switching is ideal for applications where data can be sent in chunks without requiring a dedicated path.

## Datagram Switching Vs Virtual Circuit Switching in Packet Switching

**Datagram Switching** and **Virtual Circuit Switching** are two methods of packet switching in computer networks, each with a different approach to routing packets from the source to the destination. While both methods break data into packets, they differ in terms of path establishment, routing behavior, and packet ordering. Let’s explore these two approaches:

---

### 1. **Datagram Switching**

In datagram switching, each packet is treated as an independent entity, with no predefined path established before transmission. Each packet, known as a **datagram**, contains the full source and destination addresses and can take different routes to reach the destination.

#### Characteristics of Datagram Switching

- **Independent Packets**: Each packet is routed individually and can take any available path to reach the destination.
- **Dynamic Routing**: Packets may follow different paths depending on network conditions (such as congestion or failures).
- **Out-of-Order Delivery**: Since packets can take different routes, they may arrive out of order and need to be reassembled in the correct order at the destination.
- **No Setup Required**: No path is established before sending packets; routing decisions are made dynamically as each packet reaches each router.

#### Advantages of Datagram Switching

1. **Scalability**: The network can handle more traffic, as packets can be dynamically rerouted.
2. **Fault Tolerance**: If a path fails, packets can be routed via alternate paths, making the network resilient to failures.
3. **No Initial Delay**: Because there is no need for path setup, datagram switching is faster to start transmitting data.

#### Disadvantages of Datagram Switching

1. **Out-of-Order Delivery**: Packets can arrive out of order, requiring reassembly at the destination.
2. **Higher Processing Overhead**: Routers need to make routing decisions for each packet, which can increase processing overhead.

#### Example Protocol: **Internet Protocol (IP)**

The IP protocol uses datagram switching. Each packet is routed independently, which is why packets in IP networks may arrive out of order.

---

### 2. **Virtual Circuit Switching**

In virtual circuit switching, a logical path (or "virtual circuit") is established between the source and the destination before data transfer begins. Once this path is established, all packets follow the same route and arrive in order.

#### Characteristics of Virtual Circuit Switching

- **Predefined Path**: A virtual circuit is established, and all packets follow this same path.
- **In-Order Delivery**: Since packets follow the same route, they arrive in order, eliminating the need for reordering.
- **Connection-Oriented**: Virtual circuit switching is connection-oriented; the path setup is required before sending data, similar to circuit switching but without a dedicated physical path.
- **Path Teardown**: Once data transmission is complete, the virtual circuit is torn down, freeing up resources.

#### Advantages of Virtual Circuit Switching

1. **Ordered Delivery**: Since all packets follow the same route, they arrive in the correct order, simplifying data reassembly.
2. **Efficient Routing**: Once a path is established, routers can forward packets more efficiently without recalculating routes for each packet.
3. **Reliable Connection**: Ensures a consistent route and reliable quality of service throughout the session.

#### Disadvantages of Virtual Circuit Switching

1. **Setup Delay**: Setting up a virtual circuit takes time, which can introduce initial delay.
2. **Less Flexibility**: Once a path is established, the network has less flexibility to reroute traffic if congestion or failure occurs on that path.

#### Example Protocol: **Transmission Control Protocol (TCP)**

Though TCP itself doesn’t establish a true virtual circuit at the network layer, it behaves like a virtual circuit at the transport layer by ensuring that packets arrive in order and providing reliable connection-oriented communication.

---

### Comparison Summary

| Feature                 | Datagram Switching                         | Virtual Circuit Switching                            |
| ----------------------- | ------------------------------------------ | ---------------------------------------------------- |
| **Path Setup**          | No setup; packets routed individually      | Path setup required before data transmission         |
| **Routing Flexibility** | Dynamic, packets take different routes     | Fixed path, all packets follow same route            |
| **Order of Delivery**   | Packets may arrive out of order            | Packets arrive in order                              |
| **Connection Type**     | Connectionless                             | Connection-oriented                                  |
| **Initial Delay**       | No initial delay                           | Initial setup delay                                  |
| **Reliability**         | Less reliable, best-effort delivery        | More reliable, maintains order                       |
| **Failure Handling**    | Resilient, can reroute packets dynamically | Less resilient, all packets affected by path failure |

---

### Use Cases and Applications

- **Datagram Switching**: Ideal for applications where delivery order is not critical, such as **streaming media**, **online gaming**, and **web browsing** (where lost or delayed packets can be handled by higher-layer protocols).
- **Virtual Circuit Switching**: Suitable for applications requiring **reliable, in-order delivery** with minimal disruption, such as **VoIP (Voice over IP)**, **video conferencing**, and **file transfer protocols (e.g., FTP)**.

In summary, **datagram switching** provides flexibility and fault tolerance with dynamic routing, while **virtual circuit switching** offers reliable, in-order packet delivery by establishing a stable path. The choice between them depends on the specific requirements for speed, reliability, and order of data delivery.

## Message Switching

**Message switching** is a data communication technique in computer networks in which entire messages are routed from the source to the destination. Unlike packet switching, where data is broken into smaller packets, or circuit switching, which establishes a dedicated connection, message switching transmits the whole message as a single unit, often storing it temporarily at each intermediate node along its path.

### How Message Switching Works

In message switching, each message is treated as a complete unit and is forwarded through the network in a store-and-forward manner:

1. **Message Creation**: A message is created at the source, containing the complete data along with header information, including the destination address.
2. **Store and Forward**: Each message is temporarily stored at intermediate nodes (routers or switches) along the route and is forwarded when the next node becomes available. This technique is known as **store-and-forward**.
3. **Arrival at Destination**: The message is delivered as a whole to the destination, often without any need for reassembly since it was not split into smaller parts.

### Characteristics of Message Switching

- **Store-and-Forward Mechanism**: Intermediate nodes store the message temporarily until they can forward it to the next node, ensuring message integrity but causing potential delays.
- **No Dedicated Path**: No reserved or dedicated path is established; each message is routed independently.
- **Flexible Routing**: Messages can take different routes depending on network conditions, similar to datagram switching in packet-switched networks.
- **Connectionless Transmission**: Message switching is inherently connectionless, with no setup phase required before sending the message.

### Advantages of Message Switching

1. **Flexible Routing**: Messages can be routed dynamically, adapting to network congestion and avoiding failed routes.
2. **Efficient Use of Resources**: There is no need for a dedicated path, so network resources are shared.
3. **Reliability**: Messages are stored and forwarded, meaning that even if one link fails, the message can wait until the route is restored.

### Disadvantages of Message Switching

1. **Higher Latency**: Since messages are stored and forwarded at each node, there may be considerable delay, especially with large messages.
2. **High Storage Requirement**: Intermediate nodes need storage capacity to temporarily hold large messages, leading to higher costs.
3. **Outdated for Modern Real-Time Applications**: Message switching is generally too slow for real-time communication needs, as it can introduce unpredictable delays.

### Comparison with Packet Switching and Circuit Switching

| Feature               | Message Switching                                        | Packet Switching                       | Circuit Switching                                    |
| --------------------- | -------------------------------------------------------- | -------------------------------------- | ---------------------------------------------------- |
| **Path Setup**        | No path setup; independent routing                       | No path setup; dynamic routing         | Path setup required before transmission              |
| **Transmission Type** | Store-and-forward for entire messages                    | Store-and-forward for small packets    | Continuous stream over a dedicated path              |
| **Latency**           | Higher latency due to store-and-forward of full messages | Lower latency for individual packets   | Low latency after setup; high during setup phase     |
| **Ideal Use**         | Email, document transfers (non-time-sensitive)           | Data transfer, internet browsing, VoIP | Real-time applications (e.g., traditional telephony) |
| **Reliability**       | High, but delayed delivery                               | High, with reassembly of packets       | High, with a continuous, stable connection           |

### Applications of Message Switching

- **Email Systems**: Early email systems used message switching, where each email was treated as a single message routed through the network.
- **Telegraph Networks**: Message switching was initially developed for telegraph networks, where the entire message needed to be transmitted from one office to another.
- **File Transfer Systems**: In cases where delivery time is not critical (such as archival backups or large document transfers), message switching can be used.

### Summary

Message switching is a robust but slower communication technique where entire messages are transmitted independently using a store-and-forward approach. While it is reliable and efficient for non-time-sensitive applications, it is generally considered outdated for modern, high-speed, and real-time communication needs.

## Unicast, Broadcast & Multicast

**Unicast, Broadcast, and Multicast** are three fundamental methods of data transmission in computer networks, each defining how messages are sent from one or more sources to one or more recipients. Here’s a breakdown of each method:

---

### 1. **Unicast**

Unicast is a one-to-one communication model, where data is sent from a single source to a single destination. It is the most common method of data transmission on the internet.

#### Characteristics of Unicast

- **One-to-One Communication**: A unicast message is addressed to a single, unique receiver.
- **Point-to-Point Transmission**: Each packet is sent from the source to the specific destination, with its own unique address.
- **Resource Usage**: Since data is sent to only one recipient, unicast transmission can be less demanding on network resources compared to broadcasting or multicasting.

#### Example of Unicast

- **Web Browsing**: When you access a website, your browser sends a unicast request to the web server, which responds with a unicast message containing the requested webpage.
- **Email**: Sending an email to a single recipient is also a unicast communication.

---

### 2. **Broadcast**

Broadcast is a one-to-all communication model, where data sent by a source is delivered to all devices on the network segment.

#### Characteristics of Broadcast

- **One-to-All Communication**: A broadcast message is intended for all devices within a specific network segment.
- **Network Segment Limitation**: Broadcast messages are usually confined to a single local network (subnet) and do not pass through routers to other network segments.
- **Resource Intensive**: Broadcasting can consume more network bandwidth as each device in the network segment receives and processes the broadcast message.

#### Example of Broadcast

- **Address Resolution Protocol (ARP)**: ARP broadcasts are used to map IP addresses to MAC addresses within a network. When a device doesn’t know the MAC address of another device on the same network, it sends an ARP broadcast to get the MAC address.
- **Dynamic Host Configuration Protocol (DHCP)**: When a device connects to a network, it broadcasts a DHCP request to find a DHCP server, which assigns it an IP address.

---

### 3. **Multicast**

Multicast is a one-to-many communication model, where data is sent from a single source to multiple specific recipients who have joined a multicast group.

#### Characteristics of Multicast

- **One-to-Many Communication**: A multicast message is intended for a specific group of devices that subscribe to the multicast group.
- **Efficient Resource Usage**: Multicast conserves bandwidth, as data is sent only to interested devices, rather than broadcasting to all devices on a network segment.
- **Requires Group Management**: Multicast typically requires protocols like **Internet Group Management Protocol (IGMP)** to manage multicast group memberships.

#### Example of Multicast

- **IPTV (Internet Protocol Television)**: IPTV uses multicast to stream video content to multiple subscribers in the same multicast group, optimizing bandwidth.
- **Video Conferencing**: Video conferencing tools use multicast for efficient distribution of video feeds to multiple participants.

---

### Comparison Summary

| Feature                   | Unicast                              | Broadcast                             | Multicast                                   |
| ------------------------- | ------------------------------------ | ------------------------------------- | ------------------------------------------- |
| **Type of Communication** | One-to-One                           | One-to-All                            | One-to-Many                                 |
| **Target Audience**       | Specific single device               | All devices on a network segment      | Specific group of devices                   |
| **Scope**                 | Local or across networks             | Limited to local network (subnet)     | Can be local or across multiple networks    |
| **Network Usage**         | Low to moderate                      | High (since all devices process it)   | Efficient (data sent only to group members) |
| **Use Cases**             | Web browsing, file downloads, emails | ARP, DHCP, some network announcements | IPTV, video conferencing, online gaming     |

---

### Etymology of Terms

- **Unicast**: "Uni-" comes from Latin meaning "one," referring to the transmission to a single recipient.
- **Broadcast**: "Broad-" suggests a wide range, while "cast" (from Old Norse _kasta_) means to throw, indicating data sent to all devices in range.
- **Multicast**: "Multi-" means "many," representing data transmission to a group of multiple recipients.

---

### Summary

- **Unicast** is a straightforward, one-to-one data transmission method, efficient for general internet activities.
- **Broadcast** sends data to all devices within a network, useful for network-wide messages but resource-intensive.
- **Multicast** targets a select group of devices, making it ideal for applications like video streaming where data is only needed by certain users.

Each of these transmission types has distinct use cases and impacts on network resources, helping optimize communication for specific scenarios in a computer network.
