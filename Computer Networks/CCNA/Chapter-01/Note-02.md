# Computer Networks

A computer network is a set of nodes connected by communication links.
**Nodes**: computer, camera
**Links**: wired link, wireless link
**End Devices**: PC, Printer, Server
**Intermediary Devices**: Router, Modem, internet cloud

## Characteristics of Computer Networks

1. **Fault Tolerance**

   - **Definition**: The ability of a network to continue functioning even when some components fail.
   - **Example**: In a distributed system, if one server crashes, data can still be accessed from a backup server or replicated nodes.
   - **Implementation**: Techniques like data redundancy, failover systems, and error detection/correction.

2. **Scalability**

   - **Definition**: The capacity of a network to grow (add more devices, users, or resources) without losing performance.
   - **Example**: A cloud service expanding its resources during peak hours to handle increased traffic.
   - **Implementation**: Using technologies like load balancers and distributed architectures.

3. **Quality of Service (QoS)**

   - **Definition**: The ability to prioritize certain types of traffic to ensure performance standards, like bandwidth, latency, and reliability.
   - **Example**: Video conferencing applications like Zoom prioritizing video packets over email traffic to avoid lag.
   - **Implementation**: Protocols like DiffServ and MPLS help manage and allocate resources efficiently.

4. **Security**
   - **Definition**: Protecting data and network resources from unauthorized access, attacks, or breaches.
   - **Example**: E-commerce websites use HTTPS for encrypted communication to protect users' payment data.
   - **Implementation**: Firewalls, encryption protocols (SSL/TLS), and multi-factor authentication.

## Data Communication Concepts

1. **What is Data Communication?**

   - **Definition**: The exchange of data between devices through a transmission medium (e.g., cable, wireless).
   - **Example**: Sending an email involves transferring text data from your computer to the recipient's device via servers and the internet.
   - **Key Components**: Sender, receiver, message, transmission medium, protocol.

2. **Understand Data Flow**

   - **Definition**: Refers to how data moves between devices in a network.
   - **Types**:
     - **Simplex**: Data flows in one direction (e.g., keyboard to computer).
     - **Half-duplex**: Data flows in both directions, but only one at a time (e.g., walkie-talkies).
     - **Full-duplex**: Data flows simultaneously in both directions (e.g., phone calls).

3. **Understanding the Importance of Protocol**

   - **Definition**: A protocol is a set of rules governing data communication, ensuring successful and reliable data transfer.
   - **Importance**:
     - Ensures devices understand each other (e.g., browser and server using HTTP).
     - Handles errors, data format, and timing issues.
     - Example: TCP/IP ensures reliable communication over the internet.

4. **Know the Elements of Protocol**
   - **Definition**: Protocol elements are the key aspects that define how communication occurs.
   - **Elements**:
     - **Message Encoding**: Converts data into a form suitable for transmission (e.g., text into binary).
       - **Example**: UTF-8 encoding for text in emails.
     - **Formatting & Encapsulation**: Organizes data into structured formats and packages it for transmission.
       - **Example**: HTTP headers and body encapsulated in a TCP packet.
     - **Timing**: Synchronization of data transfer speed, sequence, and response times.
       - **Example**: Video conferencing requires synchronized audio and video streams.
     - **Size**: Defines how much data can be transmitted in a single communication unit.
       - **Example**: Ethernet frames limit data to 1500 bytes per frame.
     - **Delivery Options**: Specifies how and to whom data is delivered, such as unicast (single receiver), multicast (multiple receivers), or broadcast (all devices).
       - **Example**: A router sending updates to specific devices via unicast.

## Components of a Computer Network

1. **Nodes**

   - **Definition**: Devices connected to the network that can send, receive, or process data.
   - **Examples**:
     - Computers (PCs, laptops, servers) for processing and sharing data.
     - Printers for receiving data to print.
     - IoT devices like smart home sensors.

2. **Different Media**

   - **Definition**: The transmission medium through which data is transferred.
   - **Types**:
     - **Wired Media**: Physical cables like Ethernet cables or fiber optics for high-speed connections.
       - Example: LAN setup in offices using Ethernet cables.
     - **Wireless Media**: Uses electromagnetic waves (Wi-Fi, Bluetooth, cellular networks).
       - Example: Mobile phones connected via Wi-Fi to the internet.

3. **Services Offered by Computer Networks**
   - **Definition**: Functions and resources provided by networks to users.
   - **Examples**:
     - **File Sharing**: Accessing shared documents on a network drive.
     - **Internet Access**: Browsing the web via a shared router.
     - **Communication**: Sending emails or using messaging apps like WhatsApp.
     - **Remote Access**: Connecting to a work computer via VPN.

## Classification of Computer Networks

1. **LAN (Local Area Network)**

   - **Definition**: Covers a small geographical area, such as a single building or campus.
   - **Devices Involved**:
     - Computers, switches, routers, access points, and printers.
   - **Example**: Office network connecting employee PCs to printers and file servers.

2. **MAN (Metropolitan Area Network)**

   - **Definition**: Spans a city or a large campus, connecting multiple LANs.
   - **Devices Involved**:
     - Routers, switches, fiber-optic cables, and microwave antennas.
   - **Example**: A university’s network linking multiple campus buildings.

3. **WAN (Wide Area Network)**
   - **Definition**: Covers a large geographical area, connecting multiple MANs or LANs.
   - **Devices Involved**:
     - Routers, satellites, leased lines, and public infrastructure (e.g., internet).
   - **Example**: The internet or a multinational corporation's private network.

### New Trends in Computer Networks

1. **5G Networks**: High-speed, low-latency wireless communication for mobile devices and IoT.
2. **Software-Defined Networking (SDN)**: Centralized network control using software rather than hardware.
3. **Cloud Networking**: Virtual networks hosted in cloud environments for scalability and efficiency.
4. **IoT Integration**: Connecting smart devices like wearables and home automation systems.
5. **AI in Networking**: Using AI to optimize network performance and detect security threats.

## Network Topologies

1. **Bus Topology**

   - **Definition**: All devices are connected to a single central cable (the "bus").
   - **Advantages**:
     - Simple to set up and cost-effective for small networks.
     - Requires minimal cable length.
   - **Disadvantages**:
     - A single cable failure disrupts the entire network.
     - Limited scalability and performance degradation with more devices.

2. **Star Topology**

   - **Definition**: All devices are connected to a central hub or switch.
   - **Advantages**:
     - Easy to add/remove devices without affecting the network.
     - Failure of a single device does not disrupt the network.
   - **Disadvantages**:
     - Failure of the central hub disrupts the entire network.
     - More cabling required compared to bus topology.

3. **Mesh Topology**

   - **Definition**: Each device is connected to every other device.
   - **Advantages**:
     - High reliability and fault tolerance; no single point of failure.
     - Data can take multiple paths, improving performance.
   - **Disadvantages**:
     - Expensive and complex to set up due to extensive cabling.
     - Difficult to manage and maintain.

4. **Hybrid Topology**
   - **Definition**: A combination of two or more different topologies (e.g., star-bus or star-mesh).
   - **Advantages**:
     - Flexible and scalable to suit specific network requirements.
     - Can leverage the benefits of individual topologies.
   - **Disadvantages**:
     - Complex to design and implement.
     - Higher cost due to diverse hardware and configurations.
