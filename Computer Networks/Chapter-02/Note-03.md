# Computer Networks

## Hub

In computer networks, a **hub** is a basic networking device that connects multiple devices in a local area network (LAN). It operates at the **physical layer (Layer 1)** of the OSI model and is often referred to as a multiport repeater. The hub's primary function is to forward data packets it receives from one device to all other devices connected to it. Here’s a breakdown of its function:

1. **Broadcast Transmission:** When a data packet arrives at one port of the hub, it is duplicated and sent out through all other ports. This broadcast transmission is simple and doesn't discriminate among devices, meaning all devices receive every packet regardless of whether it’s intended for them.

2. **No Data Filtering:** Hubs do not filter data or perform any routing logic. They cannot read IP addresses or differentiate between devices, so they simply repeat data to all connected devices.

3. **Half-Duplex Communication:** Hubs typically support half-duplex communication, meaning data can either be sent or received on a connection at a time, but not simultaneously. This setup often leads to **collisions**, where multiple devices attempt to communicate simultaneously, reducing network efficiency.

4. **Types of Hubs:**
   - **Passive Hub:** Simply connects devices and forwards electrical signals without amplifying them.
   - **Active Hub:** Amplifies the signals before broadcasting them to strengthen connections over longer distances.
   - **Intelligent Hub:** Provides additional management features, allowing for monitoring and error reporting.

### Etymology of "Hub"

The term **"hub"** originated from a point at the center of a wheel where the spokes connect. Similarly, in networking, a hub connects different "spokes" or devices in a star topology. The word reflects its function as a central point where multiple connections meet.

In modern networking, **switches** and **routers** are typically used in place of hubs for greater efficiency, as these devices can manage and direct data to specific devices on the network, avoiding the broadcast nature of hubs.

## Bridges

In computer networks, a **bridge** is a device that connects and filters traffic between two or more local area networks (LANs) at the **data link layer (Layer 2)** of the OSI model. Bridges help segment a network to reduce traffic and improve performance by controlling the flow of data between network segments.

### Key Functions and Features of Bridges

1. **Segmentation of Networks**: Bridges divide a large network into smaller, more manageable segments, reducing congestion. For instance, in an office network, a bridge could separate employee and visitor networks, ensuring that heavy traffic on one side doesn’t impact the other.

2. **Filtering and Forwarding**: Bridges inspect the **MAC addresses** of incoming data packets and make decisions based on those addresses. When a packet arrives at one of the bridge’s ports, it checks the destination MAC address:

   - If the destination MAC address is on the same segment as the source, the bridge filters (blocks) the packet to prevent unnecessary traffic.
   - If the destination MAC address is on a different segment, the bridge forwards the packet to the correct segment.

3. **Collision Domain Reduction**: By segmenting the network, bridges reduce the size of collision domains (the sections of a network where data packets can collide). Each network segment connected by a bridge becomes its own collision domain, lowering the chances of collisions within each segment and improving network efficiency.

4. **Types of Bridges**:
   - **Transparent Bridge**: Learns and filters traffic automatically without requiring any configuration. It "learns" the addresses in each segment and decides where to forward traffic based on its MAC address table.
   - **Source Routing Bridge**: Commonly used in **Token Ring networks**, it determines the path packets should take across the network based on the source address.
   - **Translational Bridge**: Connects different types of networks, such as Ethernet and Wi-Fi, translating data packets to bridge the communication.

### Advantages of Bridges

- **Improves Network Performance**: Bridges reduce overall traffic by only forwarding necessary data between segments.
- **Reduces Collisions**: Segmenting the network helps limit the impact of collisions to individual segments, which makes the network more efficient.
- **Simplifies Network Management**: Bridges allow network administrators to separate traffic types and prioritize network segments.

### Limitations of Bridges

- **Limited Scalability**: Bridges are generally suited for small to medium networks. Large networks may require switches, which offer better performance and scalability.
- **No Advanced Routing**: Bridges do not interpret IP addresses or offer routing functions, so they cannot direct data across complex networks as routers do.

## Switch, Hub & Bridge Explained

**Switches, hubs, and bridges** are all devices used in computer networks to connect multiple devices within a Local Area Network (LAN). They differ in how they handle data and optimize network traffic. Here’s a breakdown of each device and how they compare.

---

### 1. **Hub**

- **Function**: A hub connects multiple devices in a network, allowing them to communicate with each other.
- **Layer of Operation**: Operates at the **Physical Layer (Layer 1)** of the OSI model.
- **Transmission Method**: Broadcasts data to all devices connected to it, regardless of the intended recipient. Every device receives every packet, leading to higher network traffic.
- **Data Filtering**: Hubs have no filtering capabilities, so they do not distinguish between intended and unintended recipients.
- **Collisions and Speed**: Since hubs send data to all connected devices, they often cause data collisions and can slow down the network, particularly in high-traffic environments.
- **Use Case**: Simple, small networks where traffic is light and cost is a concern, but they’re largely obsolete now.

**Analogy**: A hub is like a loudspeaker announcing a message to everyone in a room, regardless of who the message is actually for.

---

### 2. **Bridge**

- **Function**: A bridge connects and segments two or more LAN segments, reducing congestion by controlling data flow between them.
- **Layer of Operation**: Operates at the **Data Link Layer (Layer 2)** of the OSI model.
- **Transmission Method**: Uses **MAC addresses** to filter traffic. Bridges examine each data packet's destination MAC address and decide whether to forward it to another segment or keep it within the current segment.
- **Data Filtering**: Bridges maintain a MAC address table, allowing them to selectively forward or block data, reducing unnecessary traffic across segments.
- **Collision Reduction**: Bridges reduce the size of **collision domains** by isolating segments, thus reducing the chances of data packet collisions.
- **Use Case**: Ideal for segmenting a network to improve performance by isolating traffic, especially in larger LANs.

**Analogy**: A bridge is like a bouncer checking a guest list at a party and only allowing people through if they’re supposed to be in a different room.

---

### 3. **Switch**

- **Function**: A switch connects multiple devices within a LAN and intelligently forwards data to the correct device.
- **Layer of Operation**: Primarily operates at the **Data Link Layer (Layer 2)**, though some switches (Layer 3 switches) can also operate at the **Network Layer (Layer 3)**, providing limited routing functionality.
- **Transmission Method**: Uses **MAC addresses** to direct data only to the intended device, unlike hubs that broadcast to all devices.
- **Data Filtering**: Switches build and maintain a MAC address table, so they know the specific port for each connected device. This helps them efficiently direct data, reducing unnecessary traffic.
- **Collision Domains**: Each port on a switch acts as its own collision domain, which virtually eliminates collisions within the network.
- **Full-Duplex Support**: Most modern switches support full-duplex communication, allowing simultaneous sending and receiving of data, which boosts network speed.
- **Use Case**: Essential in most modern LANs, providing efficient, scalable, and high-speed connectivity between multiple devices.

**Analogy**: A switch is like a private intercom system that delivers messages only to the intended recipient, improving privacy and reducing noise for everyone else.

---

### Comparison Summary Table

| Feature               | Hub                        | Bridge                     | Switch                            |
| --------------------- | -------------------------- | -------------------------- | --------------------------------- |
| **OSI Layer**         | Layer 1 (Physical)         | Layer 2 (Data Link)        | Layer 2 (Data Link), some Layer 3 |
| **Transmission**      | Broadcast                  | Selective forwarding       | Direct forwarding                 |
| **Data Filtering**    | None                       | Based on MAC address       | Based on MAC address              |
| **Collision Domains** | One large collision domain | Multiple segments          | Each port is a collision domain   |
| **Full Duplex**       | No                         | No                         | Yes                               |
| **Speed Efficiency**  | Low, due to collisions     | Moderate                   | High                              |
| **Cost**              | Low                        | Moderate                   | Moderate to high                  |
| **Use Case**          | Small/simple networks      | Segmenting larger networks | Modern, efficient LANs            |

### Key Takeaways

- **Hubs** are basic and inefficient, as they send all data to all devices. They’re largely outdated.
- **Bridges** provide a middle ground by segmenting the network, reducing collisions and traffic but not fully addressing network efficiency.
- **Switches** are the most efficient, forwarding data only to the intended recipient, reducing collisions, and supporting faster full-duplex communication.

Modern networks predominantly use switches due to their high performance, intelligent data handling, and scalability.

## Routers

In computer networks, a **router** is a device that directs data packets between different networks, enabling data to travel from one network to another across the internet or within large enterprise networks. Routers operate primarily at the **Network Layer (Layer 3)** of the OSI model, where they read and interpret IP addresses to make routing decisions.

### Key Functions and Features of Routers

1. **Packet Forwarding**: Routers receive data packets and determine the best path for each packet to reach its destination. They use IP addresses in the packet header to make these routing decisions, ensuring that data takes the most efficient route.

2. **Network Segmentation and Isolation**: Routers separate broadcast domains, meaning that each network connected to a router operates independently of others. This isolation reduces network congestion and enhances security by limiting the scope of broadcast traffic.

3. **Dynamic Routing**: Routers can use dynamic routing protocols (like **OSPF**, **RIP**, and **BGP**) to communicate with other routers and update their routing tables. This allows them to adapt to network changes, like traffic congestion or outages, by choosing alternative paths automatically.

4. **Network Address Translation (NAT)**: Routers often perform NAT, which allows multiple devices on a private network to share a single public IP address for accessing external networks. NAT helps preserve IP addresses and adds a layer of security by hiding internal IP addresses.

5. **Firewall and Security**: Many modern routers have built-in firewalls that help filter incoming and outgoing traffic, blocking unwanted or suspicious packets based on security policies.

### Types of Routers

- **Wired Router**: Connects devices within a network using Ethernet cables, often used in office and enterprise settings.
- **Wireless Router**: Functions as both a router and an access point, providing both wired and wireless connectivity within a LAN.
- **Core Router**: Found within the backbone of a network, core routers support high data throughput and are essential in large, data-heavy environments like ISPs and data centers.
- **Edge Router**: Positioned at the boundary of a network, edge routers connect internal networks to external networks and perform tasks like NAT and firewall filtering.
- **Virtual Router**: A software-based router that runs on a virtual machine (VM), offering the same functionalities as a hardware router but with greater flexibility and scalability.

### Advantages of Routers

- **Efficient Data Routing**: Routers use advanced routing algorithms to find the best path for data packets, reducing latency and improving speed.
- **Network Scalability**: Routers can connect multiple LANs, enabling scalability by linking numerous devices and networks.
- **Enhanced Security**: Routers can isolate networks and enforce security policies, providing protection against unauthorized access.

### Limitations of Routers

- **Cost**: Routers are generally more expensive than switches and hubs, especially when using high-end models for large-scale networks.
- **Complex Configuration**: Routers require a certain level of expertise to configure, especially when using dynamic routing protocols.
- **Latency**: Although routers are optimized for performance, the process of examining and forwarding data at the network layer can introduce slight latency compared to switches.

### Router vs. Switch vs. Hub

| Feature                  | Router                        | Switch                            | Hub                               |
| ------------------------ | ----------------------------- | --------------------------------- | --------------------------------- |
| **OSI Layer**            | Layer 3 (Network)             | Layer 2 (Data Link)               | Layer 1 (Physical)                |
| **Transmission**         | Packet forwarding based on IP | Direct forwarding based on MAC    | Broadcast to all devices          |
| **Data Filtering**       | IP-based (Layer 3)            | MAC-based (Layer 2)               | None                              |
| **Network Segmentation** | Connects multiple networks    | Connects devices within a network | Connects devices within a network |
| **Traffic Isolation**    | High                          | Moderate                          | None                              |
| **Use Case**             | Connecting LANs or WANs       | Connecting devices within a LAN   | Small networks                    |

### Etymology of "Router"

The term **"router"** comes from the word **"route,"** meaning a path or direction. In networking, a router finds the best route or path for data to travel across multiple networks, reflecting its role in directing traffic efficiently.

In summary, routers are crucial for directing network traffic between different networks, maintaining efficient and secure data pathways across the internet and private networks.

## Collision Domain Vs. Broadcast Domain | Repeater, Hub, Bridge, Switch, Router | Networks

In computer networking, **collision domains** and **broadcast domains** are fundamental concepts that help manage and contain network traffic. Different devices, such as repeaters, hubs, bridges, switches, and routers, each affect collision and broadcast domains in specific ways. Here’s a breakdown of these concepts and the role each device plays.

---

### 1. **Collision Domain**

- **Definition**: A collision domain is a network segment where data packets can collide with each other when two devices attempt to send data simultaneously. Collisions are common in **half-duplex** networks (like those with hubs) and can slow down network performance.
- **Impact of Collisions**: Collisions cause packets to be retransmitted, leading to network delays and reduced efficiency.
- **Segmentation of Collision Domains**: Devices like **bridges**, **switches**, and **routers** create separate collision domains, isolating traffic and minimizing collisions. Each port on a switch or router represents its own collision domain.

### 2. **Broadcast Domain**

- **Definition**: A broadcast domain is a network segment where a broadcast packet sent by any device is received by all other devices. Broadcasts are used for tasks like finding other devices on the network or requesting IP addresses.
- **Impact of Broadcasts**: Excessive broadcasting can lead to network congestion, so limiting the size of broadcast domains is crucial, especially in larger networks.
- **Segmentation of Broadcast Domains**: **Routers** are typically used to segment broadcast domains because they do not forward broadcast traffic. Devices like hubs, switches, and bridges do not limit broadcast domains unless **VLANs** (Virtual LANs) are implemented with managed switches.

---

### Comparison of Devices in Terms of Collision and Broadcast Domains

| Device       | OSI Layer | Collision Domain                    | Broadcast Domain                                |
| ------------ | --------- | ----------------------------------- | ----------------------------------------------- |
| **Repeater** | Layer 1   | Extends existing collision domain   | Extends existing broadcast domain               |
| **Hub**      | Layer 1   | Single collision domain             | Single broadcast domain                         |
| **Bridge**   | Layer 2   | Separate collision domains per port | Single broadcast domain                         |
| **Switch**   | Layer 2   | Separate collision domains per port | Single broadcast domain (unless VLANs are used) |
| **Router**   | Layer 3   | Separate collision domains per port | Separate broadcast domains                      |

---

### Role of Each Device

#### 1. **Repeater**

- **Function**: Amplifies or regenerates signals to extend the range of a network.
- **Collision Domain**: A repeater does not segment collision domains; it simply extends the same collision domain across its network segment.
- **Broadcast Domain**: A repeater does not create new broadcast domains; it forwards broadcasts along with regular traffic.
- **Use Case**: Extending network range over longer distances.

#### 2. **Hub**

- **Function**: A hub connects multiple devices and broadcasts all incoming data to every connected device.
- **Collision Domain**: All ports on a hub belong to the same collision domain, meaning collisions can happen frequently in high-traffic environments.
- **Broadcast Domain**: A hub maintains a single broadcast domain, meaning any broadcast sent by a device is seen by all other devices on the hub.
- **Use Case**: Small, simple networks where traffic is light and costs need to be low. Hubs are largely obsolete due to high collision rates.

#### 3. **Bridge**

- **Function**: A bridge connects two network segments and filters traffic based on **MAC addresses**.
- **Collision Domain**: Each port on a bridge represents a separate collision domain, helping to reduce collisions by isolating network segments.
- **Broadcast Domain**: A bridge does not split broadcast domains, so all segments connected by a bridge share the same broadcast domain.
- **Use Case**: Used to improve network performance by segmenting traffic without completely isolating network segments.

#### 4. **Switch**

- **Function**: A switch connects multiple devices within a LAN and intelligently directs data to specific devices based on MAC addresses.
- **Collision Domain**: Each port on a switch represents its own collision domain, which reduces the chances of collisions and improves network efficiency.
- **Broadcast Domain**: All ports on a basic (unmanaged) switch share the same broadcast domain. However, managed switches support **VLANs**, allowing the segmentation of broadcast domains.
- **Use Case**: Essential for most modern LANs due to high efficiency, low collision rates, and support for larger networks.

#### 5. **Router**

- **Function**: A router connects different networks and forwards data based on **IP addresses**.
- **Collision Domain**: Each port on a router represents a separate collision domain, fully isolating connected networks from each other.
- **Broadcast Domain**: Routers separate broadcast domains, as they do not forward broadcast packets by default. Each connected network (LAN segment) is its own broadcast domain.
- **Use Case**: Connecting multiple LANs or connecting a LAN to the internet, supporting network segmentation, and enhancing security by isolating traffic.

---

### Summary

- **Collision Domain**: Limited by switches and bridges; each port on these devices reduces collisions. Hubs and repeaters do not limit collision domains and allow frequent collisions.
- **Broadcast Domain**: Limited by routers; each port on a router is a new broadcast domain, isolating network segments from one another. Switches and bridges, unless using VLANs, do not limit broadcast domains.

By using a combination of routers, switches (with VLANs if necessary), and appropriate network architecture, networks can minimize collisions and broadcast traffic, optimizing both speed and performance.
