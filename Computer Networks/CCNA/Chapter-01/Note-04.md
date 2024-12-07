# Layering

Decomposing problmens into more manageable components.

`Example of layering architectures`

- The OSI Reference Model.
- The TCP/IP Model

## OSI Model

- Open System Interconnection
- It is a model for understanding and designing a network architecture that is flexible, robust, and interoperable.
- Developed by the international standards for organizations
- The OSI model is not a protocol.
- It is only guidline and hence it is referred as OSI reference model.
- The purpose of OSI model is to show how to facilitate communication between different systems without requiring changes to the logic of the underlying hardware and software.
- The OSI modle was never fully implemented.

## TCP/IP Model

TCP/IP (Transmission Control Protocol/Internet Protocol)

- The TCP/IP protocol suite was developed prior to the OSI model.
- The layers in this do not exactly match with OSI model.
- TCP/IP is a heirarchical protocol made up of interactive modules, each module provides specific functionality.

## OSI Reference Model

Here are the **7 layers of the OSI model** in their correct order, from top to bottom:

1. **Application Layer**
2. **Presentation Layer**
3. **Session Layer**
4. **Transport Layer**
5. **Network Layer**
6. **Data Link Layer**
7. **Physical Layer**

### **1. Application Layer**

- **Function**: The **Application Layer** is the topmost layer that interacts directly with end-user applications. It provides network services to user applications and facilitates communication between devices.
- **Responsibilities**:
  - User interface for communication.
  - Supports various services like email, file transfer, and web browsing.
  - Ensures that applications can communicate over a network.

**Examples**:

- **Web Browsing**: When you access a website using your browser, the application layer uses **HTTP** to request the web page.
- **Email**: When you send an email, the **SMTP (Simple Mail Transfer Protocol)** is used at this layer to send the message.

**Real-life Example**:

- When you open a **web browser** and visit a site, the browser (Application Layer) sends a request to the server to load the web page using the **HTTP protocol**. The web page is then displayed on your screen.

---

### **2. Presentation Layer**

- **Function**: The **Presentation Layer** is responsible for translating, encrypting, and compressing data. It ensures that the data is in a readable format for the application layer, regardless of the system or platform differences.
- **Responsibilities**:
  - Data translation: Converting data into a format that the receiving application can understand.
  - Encryption: Securing data by encoding it (e.g., SSL/TLS encryption for secure communications).
  - Compression: Reducing the data size for faster transmission.

**Examples**:

- **Data Encoding**: If one computer sends data in one format (like ASCII) and another computer expects it in another format (like EBCDIC), this layer converts the data between formats.
- **Encryption**: Secure web communication (HTTPS) encrypts data at this layer using **SSL/TLS**.

**Real-life Example**:

- When you make an **online purchase**, the **Presentation Layer** ensures that your credit card information is **encrypted** before being transmitted over the network using **SSL/TLS** encryption. This prevents unauthorized access to your sensitive data.

---

### **3. Session Layer**

- **Function**: The **Session Layer** manages sessions or connections between applications. It establishes, maintains, and terminates communication sessions. This layer controls the dialogues (conversations) between computers, ensuring data is properly synchronized.
- **Responsibilities**:
  - Session management: Establishing, maintaining, and terminating sessions.
  - Dialog control: Determines whether communication is half-duplex (one-way at a time) or full-duplex (two-way simultaneously).
  - Synchronization: For long data transfers, it can insert checkpoints to resume transmission if a failure occurs.

**Examples**:

- **File Transfer**: In a file transfer process, the **Session Layer** ensures that the connection remains open for the duration of the transfer.
- **Streaming Services**: For video or audio streaming, it ensures the session is maintained between the client (e.g., your device) and server to allow continuous media playback.

**Real-life Example**:

- During a **video conference**, the **Session Layer** keeps track of who is communicating, establishes the connection between the devices, and ensures the flow of video and audio between the participants. It also manages the session's duration, so the connection can be properly closed when the conference ends.

---

### **4. Transport Layer**

**Purpose**: The **Transport Layer** ensures reliable data transfer between two devices across a network. It is responsible for managing end-to-end communication, error correction, data flow control, and segmentation. It provides mechanisms to establish, maintain, and terminate connections.

#### **Key Functions**:

- **Segmentation and Reassembly**: Divides large data into smaller packets to ensure smooth transmission and reassembles them at the destination.
- **Connection Control**: Handles whether the communication is **connection-oriented** (TCP) or **connectionless** (UDP).
- **Flow Control**: Ensures that data is transferred at an appropriate rate to prevent congestion and loss.
- **Error Control**: Ensures the integrity of data by detecting and correcting errors in data transmission.

#### **Example**:

Imagine you are sending a large file over the internet. The **Transport Layer** breaks this file into smaller chunks (called **segments**), ensuring each piece is sent correctly and in the right order. It then reassembles the pieces at the receiving end.

- **Real-Life Example**: When you access a website, your browser uses **TCP** (Transmission Control Protocol) at the **Transport Layer** to ensure the data is sent in small packets, and any lost packets are retransmitted.

### **5. Network Layer**

**Purpose**: The **Network Layer** is responsible for determining the path data packets take from the source to the destination across different networks. It handles routing, addressing, and the selection of optimal paths.

#### **Key Functions**:

- **Routing**: Decides the best path for data to travel from source to destination, often through intermediate routers.
- **Logical Addressing**: Uses **IP addresses** (Internet Protocol addresses) to identify devices on different networks. This is what makes it possible to send data from one network to another.

#### **Example**:

Imagine you want to send a letter to someone living in another city. You don't need to know the exact roads or routes the letter will take; you just need to know the recipient's address. Similarly, the **IP address** in the **Network Layer** directs the packet to the correct destination.

- **Real-Life Example**: When you access a website like `www.example.com`, the **Network Layer** (via the **IP protocol**) determines the **IP address** of `example.com` (e.g., `192.168.1.1`). It then routes your data to the appropriate network using routers.

---

### **6. Data Link Layer**

**Purpose**: The **Data Link Layer** ensures reliable communication between devices on the same local network. It handles the **framing**, **error detection**, and **flow control** necessary for data transfer.

#### **Key Functions**:

- **Framing**: Breaks data into **frames** that can be transmitted over the physical layer.
- **Error Detection**: Ensures data integrity by checking for errors using techniques like **CRC (Cyclic Redundancy Check)**.
- **MAC Addressing**: Identifies devices within a local network using **MAC addresses** (Media Access Control).

#### **Example**:

Think of this layer as the postal service inside your local area. It ensures that the **letter** (data) is well-packaged and correctly labeled before being handed over to the next step. If there's an issue (like a damaged package), it will try to handle it before sending the data further.

- **Real-Life Example**: In an Ethernet network, the **Data Link Layer** uses **MAC addresses** to identify your computer's network card and ensure data is properly sent to it from another device on the same network.

---

### **7. Physical Layer**

**Purpose**: The **Physical Layer** is responsible for transmitting raw bits over the physical medium, such as copper wires, fiber optic cables, or wireless radio waves. It converts the data into electrical, optical, or radio signals for transmission.

#### **Key Functions**:

- **Bit Transmission**: Converts the **binary data** (1s and 0s) into signals for transmission over the medium.
- **Media**: Handles the hardware aspects, such as the cables, connectors, and wireless channels.

#### **Example**:

Imagine sending a message using a loudspeaker at a distance. The **Physical Layer** is like the speaker itself, which turns your message into sound waves (analog signals) that can travel through the air. In networking, these are the **signals** transmitted through wires or airwaves.

- **Real-Life Example**: When you connect your computer to the internet via Ethernet, the **Physical Layer** ensures that the electrical signals travel through the copper wires or fiber optic cables. If you're using Wi-Fi, this layer would transmit signals via radio waves.

---

### **Now, Let's Summarize All 7 Layers with Real-Life Examples**:

1. **Physical Layer (Layer 1)**:

   - **Role**: Transmits raw bits over the physical medium.
   - **Real-life example**: The wires and radio waves used for transmitting data.
   - **Example**: Ethernet cables or Wi-Fi radio signals that carry the data.

2. **Data Link Layer (Layer 2)**:

   - **Role**: Provides node-to-node data transfer and error checking.
   - **Real-life example**: The postal service inside your local area, ensuring packages are well-packaged and correctly addressed.
   - **Example**: **MAC addresses** on Ethernet, which uniquely identify devices on the same network.

3. **Network Layer (Layer 3)**:

   - **Role**: Handles routing, addressing, and path selection.
   - **Real-life example**: Deciding the best route for a letter to reach another city.
   - **Example**: **IP addresses** and **routers** that ensure data packets find their way from one device to another across networks.

4. **Transport Layer (Layer 4)**:

   - **Role**: Ensures reliable data transfer, segmentation, and reassembly. It also handles flow control and error correction.
   - **Real-life example**: Breaking a large letter into several smaller ones and ensuring the pieces arrive in order.
   - **Example**: **TCP (Transmission Control Protocol)** for reliable communication or **UDP (User Datagram Protocol)** for faster, connectionless communication.

5. **Session Layer (Layer 5)**:

   - **Role**: Manages sessions between applications, controlling dialog between devices.
   - **Real-life example**: Starting a phone call and ensuring both parties can talk and hear without interruption.
   - **Example**: **Session management** during an online video conference or maintaining a login session for a web application.

6. **Presentation Layer (Layer 6)**:

   - **Role**: Ensures data is in a readable format for the application layer, handling data encryption, compression, and translation.
   - **Real-life example**: Translating a foreign language message into something you can understand.
   - **Example**: **SSL/TLS encryption** or **data format conversions** (e.g., from JPEG to PNG).

7. **Application Layer (Layer 7)**:
   - **Role**: Provides network services to the user and interacts directly with the applications.
   - **Real-life example**: The application you use to send a letter, whether it’s email, text, or a web browser.
   - **Example**: **HTTP** (HyperText Transfer Protocol) for browsing websites or **SMTP** (Simple Mail Transfer Protocol) for sending emails.

---

### **Final Summary**:

- The **Transport Layer (Layer 4)** handles end-to-end communication, ensuring data is broken down, transmitted, and reassembled correctly.
- The **Physical Layer (Layer 1)**, **Data Link Layer (Layer 2)**, and **Network Layer (Layer 3)** work together to ensure that data can be transmitted through the appropriate physical medium, correctly addressed, and routed across networks.
- The **Application Layer (Layer 7)** provides the interfaces that users interact with, while the **Session Layer (Layer 5)** and **Presentation Layer (Layer 6)** manage the data exchange and formatting.
