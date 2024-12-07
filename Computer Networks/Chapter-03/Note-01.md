# Networking

## Data link layer

The **Data Link Layer** is the second layer in the **OSI (Open Systems Interconnection)** model and plays a crucial role in enabling reliable data transfer between nodes in a network. It provides mechanisms for error detection, correction, and framing, ensuring that data is transmitted accurately across the physical layer.

---

### **Responsibilities of the Data Link Layer**

1. **Framing**:

   - Breaks data from the network layer into manageable units called frames.
   - Adds headers and trailers to frames to include metadata like source and destination addresses.

2. **Addressing**:

   - Uses **MAC (Media Access Control)** addresses to uniquely identify devices on a local network.

3. **Error Detection and Correction**:

   - Ensures data integrity by detecting and correcting errors using mechanisms like checksums, CRC (Cyclic Redundancy Check), or parity bits.

4. **Flow Control**:

   - Manages the rate of data transmission to ensure that a fast sender doesn’t overwhelm a slow receiver.

5. **Access Control**:

   - Coordinates access to the shared physical medium to avoid collisions, using protocols like CSMA/CD (Carrier Sense Multiple Access with Collision Detection) in Ethernet.

6. **Reliable Data Transfer**:
   - Ensures the proper delivery of frames through acknowledgments and retransmissions in reliable protocols.

---

### **Sub-Layers of the Data Link Layer**

The Data Link Layer is divided into two sub-layers:

1. **Logical Link Control (LLC)**:

   - Provides logical addressing and manages error checking and flow control.
   - Interfaces with the network layer.

2. **Media Access Control (MAC)**:
   - Manages access to the physical transmission medium.
   - Ensures data is transmitted without collisions (in shared media).

---

### **Data Link Layer Services**

- **Encapsulation**: Wraps network layer packets into frames with necessary headers and trailers.
- **Error Handling**: Detects and sometimes corrects errors that occur in the physical layer.
- **Media Access Control**: Determines how devices on the same medium communicate without interfering with each other.

---

### **Protocols in the Data Link Layer**

- **Ethernet**: A widely used protocol for local area networks (LANs).
- **PPP (Point-to-Point Protocol)**: Used for direct communication between two nodes.
- **HDLC (High-Level Data Link Control)**: Provides error detection and flow control in point-to-point and multipoint networks.
- **Wi-Fi (802.11)**: A protocol for wireless LANs.
- **Token Ring**: An older protocol where devices pass a token to control access to the medium.

---

### **Key Concepts**

1. **Frames**:

   - The fundamental unit of communication in the data link layer.
   - Typically includes:
     - **Header**: Contains source and destination MAC addresses.
     - **Payload**: The actual data being transmitted.
     - **Trailer**: Often includes error-checking information like CRC.

2. **Error Control Techniques**:

   - **Parity Check**: Adds a parity bit for simple error detection.
   - **Checksum**: Computes a value based on the frame's data for verification.
   - **CRC**: Uses polynomial division to detect errors in data transmission.

3. **Flow Control Techniques**:

   - Ensures that the sender doesn't overwhelm the receiver.
   - Examples include **Stop-and-Wait ARQ** and **Sliding Window Protocol**.

4. **Access Control**:
   - Resolves contention for a shared communication medium.
   - Examples:
     - **CSMA/CD**: Used in Ethernet to detect and handle collisions.
     - **CSMA/CA**: Used in Wi-Fi to avoid collisions.

---

### **Relation to Other Layers**

- **Above the Data Link Layer (Network Layer)**:
  - The network layer sends packets to the data link layer for framing and transmission.
- **Below the Data Link Layer (Physical Layer)**:
  - Converts frames into signals (electrical, optical, or radio) for transmission.

---

### **Use Cases**

- Local Area Networks (LANs): Ethernet and Wi-Fi are data link layer technologies.
- Wide Area Networks (WANs): Protocols like PPP are used for point-to-point links.
- Wireless Communication: Ensures reliable data transmission over wireless media with protocols like 802.11.

By managing communication at the node-to-node level, the data link layer plays a vital role in ensuring smooth and error-free data transfer in networks.

## Stop and Wait ARQ protocol

The **Stop-and-Wait ARQ (Automatic Repeat Request)** protocol is a fundamental error-control mechanism used in data communication to ensure reliable data transfer over unreliable or noisy networks. It is a simple, yet effective protocol that works by sending one frame at a time and waiting for an acknowledgment (ACK) before sending the next frame. If an acknowledgment is not received within a certain timeframe, the frame is retransmitted.

---

### **How Stop-and-Wait ARQ Works**

1. **Frame Transmission**:

   - The sender transmits a data frame and then stops and waits for an acknowledgment from the receiver.

2. **Acknowledgment**:

   - If the receiver successfully receives the frame, it sends an acknowledgment (ACK) back to the sender.
   - The sender, upon receiving the ACK, sends the next frame.

3. **Timeout and Retransmission**:
   - If the sender does not receive an acknowledgment within a specified timeout period, it assumes the frame was lost or corrupted and retransmits the frame.
4. **Error Handling**:
   - **Lost Frames**: If a frame is lost, the sender’s timeout mechanism will trigger a retransmission.
   - **Lost Acknowledgments**: If the acknowledgment is lost, the sender retransmits the same frame after the timeout, and the receiver discards the duplicate frame but re-sends an acknowledgment.
   - **Corrupted Frames**: The receiver discards corrupted frames and does not send an acknowledgment, prompting the sender to retransmit.

---

### **Advantages of Stop-and-Wait ARQ**

1. **Simplicity**: Easy to implement and understand due to its straightforward process.
2. **Reliability**: Ensures reliable delivery of data even over unreliable channels by using retransmissions for lost or corrupted frames.

---

### **Disadvantages of Stop-and-Wait ARQ**

1. **Inefficiency**: Only one frame can be in transmission at any time, which limits the throughput, especially over long-distance or high-latency networks.
2. **High Latency**: Because it waits for an acknowledgment for each frame, the protocol has a high latency, making it unsuitable for high-speed, long-distance networks.

---

### **Example Scenario**

Let’s consider a scenario where a sender is transmitting data frames to a receiver over a noisy channel:

1. **Frame 1 Transmission**: The sender sends Frame 1 to the receiver.
2. **Acknowledgment for Frame 1**: The receiver receives Frame 1 and sends an acknowledgment (ACK1) back to the sender.
3. **Frame 2 Transmission**: Upon receiving ACK1, the sender transmits Frame 2.
4. **Frame Loss and Timeout**: Suppose Frame 2 is lost during transmission. The sender waits but does not receive an acknowledgment, so it times out and retransmits Frame 2.
5. **Duplicate Frame Handling**: If an ACK for Frame 2 is lost, the sender resends Frame 2 upon timeout. The receiver, however, identifies it as a duplicate and discards it but resends ACK2 to keep the sender progressing.

---

### **Mathematics of Efficiency in Stop-and-Wait**

The **efficiency** of the Stop-and-Wait ARQ protocol can be defined by the ratio of the frame transmission time to the total time (transmission time + round-trip time).

Let:

- \( T\_{frame} \) = Time taken to send a frame
- \( T\_{RTT} \) = Round-trip time (the time it takes for a frame to travel to the receiver and for the acknowledgment to return)

Then, the efficiency (\( \eta \)) can be approximated as:
\[
\eta = \frac{T*{frame}}{T*{frame} + T\_{RTT}}
\]

As the round-trip time increases, the efficiency decreases significantly because the sender must wait longer for each acknowledgment.

---

### **Use Cases of Stop-and-Wait ARQ**

- **Low Bandwidth Networks**: Suitable for systems with low data rates, such as simple point-to-point links in embedded systems or low-speed networks.
- **Simple Communication Links**: Often used in situations where simplicity is more critical than high efficiency, like some IoT applications.
- **Fundamental Learning Protocol**: Serves as a basis for understanding more complex ARQ mechanisms like Go-Back-N and Selective Repeat.

---

### **Comparison to Other ARQ Protocols**

- **Go-Back-N ARQ**: Allows multiple frames to be sent before receiving ACKs, improving efficiency but requiring more complex handling of retransmissions.
- **Selective Repeat ARQ**: Only retransmits frames that are actually lost or corrupted, improving both efficiency and reliability over Stop-and-Wait ARQ.

In summary, Stop-and-Wait ARQ is a basic yet reliable protocol that emphasizes simplicity and correctness over efficiency. It’s ideal for situations with minimal latency and where ease of implementation is prioritized.

## Go-Back-N ARQ

The **Go-Back-N ARQ (Automatic Repeat Request)** protocol is an error-control mechanism used to ensure reliable data transmission by allowing multiple frames to be in transit at once. Unlike the **Stop-and-Wait ARQ** protocol, which sends one frame at a time, Go-Back-N can send a sequence of up to **N frames** without waiting for individual acknowledgments. This increases efficiency by keeping the communication channel active and improves throughput, especially over long distances or high-latency networks.

---

### **How Go-Back-N ARQ Works**

1. **Sliding Window**:

   - The sender maintains a **sliding window** of up to **N frames** (the "window size") that it can send without waiting for an acknowledgment.
   - Each frame in the window has a unique sequence number.
   - Once a frame is acknowledged, the window slides forward, allowing the sender to send additional frames.

2. **Acknowledgments**:

   - The receiver only sends acknowledgments for frames received in sequence.
   - If a frame arrives out of order, the receiver discards it and does not acknowledge it, expecting the sender to resend from the last successfully received frame.

3. **Retransmission on Error**:
   - If the sender detects a missing or corrupted acknowledgment, it will **go back** and retransmit all frames starting from the last unacknowledged frame.
   - For example, if the sender has sent frames 1 to 5, and frame 3 was lost, the sender will resend frames 3, 4, and 5 once the loss is detected.

---

### **Step-by-Step Example of Go-Back-N ARQ**

Suppose a sender is transmitting a sequence of frames to a receiver, and the window size \( N = 4 \).

1. **Frame Transmission**:

   - The sender transmits frames 1, 2, 3, and 4.

2. **Acknowledgment**:
   - If the receiver successfully receives frames 1, 2, and 3, it sends an acknowledgment for each one.
3. **Frame Loss or Error**:
   - Suppose frame 4 is lost or corrupted. The receiver does not send an acknowledgment for frame 4.
4. **Go-Back Operation**:
   - When the sender times out or receives a negative acknowledgment (NACK) for frame 4, it will **go back** and retransmit frames 4 and any subsequent frames in the window (even if they were already sent correctly).
5. **Resuming Transmission**:
   - Once frame 4 is successfully received, the receiver will continue acknowledging the remaining frames, and the sender will slide its window forward to send additional frames.

---

### **Advantages of Go-Back-N ARQ**

1. **Improved Efficiency Over Stop-and-Wait**:
   - Allows multiple frames to be sent at once, using the network bandwidth more efficiently and reducing idle time on the transmission channel.
2. **Simpler Implementation**:
   - Compared to **Selective Repeat ARQ**, Go-Back-N is simpler because the receiver only needs to keep track of the next expected frame and doesn’t store out-of-order frames.

---

### **Disadvantages of Go-Back-N ARQ**

1. **Redundant Retransmissions**:
   - If a single frame is lost or corrupted, all subsequent frames in the window are retransmitted, even if they were originally received correctly. This can lead to wasted bandwidth.
2. **Receiver Simplicity, Sender Complexity**:
   - Although the protocol simplifies the receiver’s job (discarding out-of-order frames), it adds complexity on the sender side, which must track and manage retransmissions.

---

### **Mathematics of Efficiency in Go-Back-N ARQ**

The **efficiency** (\( \eta \)) of Go-Back-N ARQ increases as the window size \( N \) increases. The protocol’s efficiency can be approximated as:

\[
\eta = \frac{N}{1 + 2a}
\]

where:

- \( N \) is the window size.
- \( a \) is the ratio of the propagation delay to the transmission time, also known as the **bandwidth-delay product**.

When the propagation delay is high, increasing \( N \) improves the efficiency, as more frames are sent before an acknowledgment is needed.

---

### **Key Concepts in Go-Back-N ARQ**

1. **Sliding Window Protocol**:
   - Allows multiple frames to be in transit, managed by a window that “slides” forward as frames are acknowledged.
2. **Timeout Mechanism**:
   - Each frame has an associated timeout. If the sender does not receive an acknowledgment within this time, it triggers retransmission.
3. **Sender and Receiver Window**:
   - **Sender’s Window**: A buffer that holds up to \( N \) frames waiting for acknowledgment.
   - **Receiver’s Window**: Keeps track of the next expected frame and discards any frames that arrive out of order.

---

### **Go-Back-N ARQ vs. Selective Repeat ARQ**

- **Go-Back-N ARQ**: Simpler to implement but retransmits all frames after an error, resulting in lower efficiency when errors occur.
- **Selective Repeat ARQ**: Allows the receiver to accept out-of-order frames, retransmitting only those that are lost or corrupted, which is more efficient but requires more memory and complexity in implementation.

---

### **Use Cases for Go-Back-N ARQ**

- **Wireless Networks**: Often used in wireless protocols where maintaining reliability is critical but high efficiency is not necessarily required.
- **Low to Moderate Error Networks**: Suitable for networks with low to moderate error rates where retransmissions don’t heavily impact performance.
- **Simple Applications**: Ideal for scenarios where implementing complex protocols (like Selective Repeat) is unnecessary, and simplicity is prioritized.

In summary, Go-Back-N ARQ provides a balance between reliable data transfer and improved efficiency over Stop-and-Wait ARQ by allowing multiple frames in transit, although it can still result in redundant retransmissions under certain conditions.

## Selective Repeat ARQ

**Selective Repeat ARQ (Automatic Repeat Request)** is an error-control protocol that enhances transmission efficiency by only retransmitting frames that were lost or received with errors, rather than retransmitting all frames after an error is detected, as in the **Go-Back-N ARQ** protocol. This makes Selective Repeat more efficient than Go-Back-N, especially in networks with higher error rates, as it reduces redundant data transmissions.

---

### **How Selective Repeat ARQ Works**

1. **Sliding Window Protocol**:
   - Like Go-Back-N, Selective Repeat ARQ also uses a sliding window for managing frames, allowing the sender to transmit multiple frames before needing acknowledgments.
   - Both the sender and receiver maintain separate windows that can hold a certain number of frames.
2. **Acknowledgments for Individual Frames**:

   - Each frame is acknowledged individually. If a specific frame is received correctly, the receiver sends an acknowledgment (ACK) for that frame.
   - If a frame is lost or corrupted, only that frame will be retransmitted, rather than all frames following the error.

3. **Buffering Out-of-Order Frames**:
   - The receiver can accept frames even if they arrive out of order. It buffers them temporarily until any missing frames are retransmitted and received, allowing the data to be reassembled in the correct sequence.
4. **Retransmission of Specific Frames**:
   - When a timeout occurs or a negative acknowledgment (NACK) is received for a specific frame, the sender only retransmits the affected frame, rather than all frames within the window.

---

### **Example of Selective Repeat ARQ**

Suppose the sender is transmitting a sequence of frames, and the window size is \( N = 4 \).

1. **Transmission**:

   - The sender transmits frames 1, 2, 3, and 4.

2. **Acknowledgment**:

   - The receiver receives frames 1 and 2 correctly and sends acknowledgments for these frames.

3. **Frame Error**:

   - Suppose frame 3 is corrupted or lost during transmission. The receiver discards it and buffers frame 4, which arrives correctly, even though it is out of order.

4. **Selective Retransmission**:

   - The sender, after a timeout or upon receiving a NACK for frame 3, retransmits only frame 3.

5. **Correct Sequence**:
   - The receiver places frame 3 in the correct position and then assembles frames 1, 2, 3, and 4 in order.

---

### **Advantages of Selective Repeat ARQ**

1. **Higher Efficiency**:

   - Only the frames with errors are retransmitted, saving bandwidth and improving efficiency, particularly in networks with higher error rates.

2. **Reduced Redundancy**:
   - Since out-of-order frames are buffered rather than discarded, only necessary retransmissions occur, minimizing redundant transmissions.

---

### **Disadvantages of Selective Repeat ARQ**

1. **Increased Complexity**:

   - Both sender and receiver need to maintain buffers for out-of-order frames and keep track of acknowledgments for each frame, which requires more memory and processing.

2. **Out-of-Order Buffering**:
   - The receiver must implement a mechanism to reorder frames if they arrive out of sequence, which adds complexity compared to Go-Back-N.

---

### **Mathematics of Efficiency in Selective Repeat ARQ**

Efficiency in Selective Repeat ARQ is calculated similarly to Go-Back-N ARQ but is generally higher due to reduced retransmissions. The efficiency (\( \eta \)) can be represented as:

\[
\eta = \frac{N}{1 + 2a}
\]

where:

- \( N \) is the window size.
- \( a \) represents the ratio of the propagation delay to the transmission time (also known as the bandwidth-delay product).

Since retransmissions are minimized, the actual performance of Selective Repeat can exceed Go-Back-N, particularly in scenarios with a significant number of errors.

---

### **Key Concepts in Selective Repeat ARQ**

1. **Individual Acknowledgment**:
   - Each frame is acknowledged independently, reducing the need for retransmitting subsequent frames after an error.
2. **Sliding Window at Sender and Receiver**:

   - Both sender and receiver windows keep track of the frames being sent, acknowledged, and buffered. This allows selective retransmission and reordering of frames.

3. **Buffering and Reordering**:
   - The receiver buffers any out-of-order frames so that data can be reassembled sequentially once missing frames arrive.

---

### **Selective Repeat ARQ vs. Go-Back-N ARQ**

- **Selective Repeat ARQ** retransmits only the frames that are lost or corrupted, leading to higher efficiency in networks with higher error rates but requiring more memory and complexity for tracking and buffering.
- **Go-Back-N ARQ** retransmits all frames from the point of error, which is simpler but can lead to redundant retransmissions and lower efficiency.

---

### **Use Cases for Selective Repeat ARQ**

- **High-Latency Networks**: Selective Repeat ARQ is suitable for networks where retransmitting large numbers of frames would be costly, such as satellite or long-distance networks.
- **Error-Prone Networks**: Effective in wireless and other error-prone environments where selective retransmissions minimize bandwidth waste.
- **Reliable Data Applications**: Applications where high data integrity and reliability are required, such as video streaming and file transfers.

In summary, Selective Repeat ARQ is a highly efficient and sophisticated protocol that improves transmission reliability by targeting specific frames for retransmission, making it well-suited for error-prone networks. However, it is more complex than Go-Back-N due to the need for extensive buffering and reordering.

## Framing in Data Link Layer | Bit Stuffing vs Byte(Character) Stuffing

**Framing** in the **Data Link Layer** is a process that involves dividing data into manageable, structured units called **frames**. These frames are essential for ensuring data integrity, synchronization, and error control during transmission across a network. Frames typically contain the data payload along with additional information like headers, error checks, and delimiters that help distinguish one frame from another.

Two common methods of framing include **Bit Stuffing** and **Byte (or Character) Stuffing**. Each has its own way of handling data and frame boundaries to maintain synchronization and manage special control information within frames.

---

### **1. Bit Stuffing**

**Bit stuffing** is used primarily in protocols that operate at the **bit level**. It ensures that data frames have a unique pattern that marks the start and end of each frame, which helps receivers recognize frame boundaries. When bit patterns in the data resemble control sequences, extra bits are inserted to differentiate them.

#### **How Bit Stuffing Works:**

1. A special bit pattern, such as **01111110** (used in HDLC and PPP), marks the beginning and end of each frame.
2. During transmission, if a sequence of **five consecutive '1' bits** is detected in the data payload, a **'0' bit** is inserted (or "stuffed") immediately after the fifth '1'.
3. At the receiver end, when a sequence of five '1's followed by a '0' is detected, the '0' bit is removed to restore the original data.
4. If five '1's are followed by another '1' instead of a '0', it indicates an **end of frame**.

#### **Example of Bit Stuffing:**

- Data to be sent: `1111101011`
- After bit stuffing: `1111100101011`

#### **Advantages of Bit Stuffing:**

- Efficient for **bit-oriented protocols**.
- Works well for high-speed networks where processing bits is faster than processing bytes or characters.

#### **Disadvantages of Bit Stuffing:**

- Requires additional processing to add and remove stuffed bits.
- Can increase the frame size if a large number of '1' bits are present, as more bits need to be stuffed.

---

### **2. Byte (Character) Stuffing**

**Byte (or Character) Stuffing** is typically used in **byte-oriented** protocols, such as ASCII-based communications. Here, special control characters indicate the start and end of a frame or signal control sequences. If these characters appear in the data, they are "stuffed" with additional bytes to prevent misinterpretation.

#### **How Byte (Character) Stuffing Works:**

1. Special **flag bytes** or **control characters** (e.g., **ESC** for escape) are defined to mark the start and end of a frame.
2. If any data byte matches a flag or control byte, an **escape byte** (ESC) is inserted before it.
3. The receiver, upon detecting an escape byte, interprets the following byte as part of the data rather than as a control character.

#### **Example of Byte Stuffing:**

- **Special flag byte**: `F` (indicates start/end of frame).
- Data to be sent: `HelloFWorld`
- After byte stuffing: `HelloESC FWorld`

Here, `ESC F` tells the receiver that `F` is part of the data, not a frame boundary.

#### **Advantages of Byte Stuffing:**

- Simple to implement in **byte-oriented systems** where data is processed as characters.
- Easy to interpret and works well with protocols like **ASCII** and **UTF-8**.

#### **Disadvantages of Byte Stuffing:**

- Inefficient for **bit-oriented protocols** and high-speed transmission.
- Increases frame size, as additional escape bytes are added.

---

### **Bit Stuffing vs. Byte Stuffing Summary**

| Feature                      | Bit Stuffing                                                      | Byte (Character) Stuffing                                          |
| ---------------------------- | ----------------------------------------------------------------- | ------------------------------------------------------------------ |
| **Operation Level**          | Works on individual bits                                          | Works on individual bytes (characters)                             |
| **Used In**                  | Bit-oriented protocols                                            | Byte-oriented protocols                                            |
| **Special Control Sequence** | Recognizes frame boundaries through bit patterns (e.g., 01111110) | Recognizes frame boundaries through control characters (e.g., ESC) |
| **Stuffing Method**          | Inserts a '0' bit after five consecutive '1's                     | Inserts an escape character (ESC) before a control character       |
| **Efficiency**               | More efficient for bit-level protocols                            | More efficient for character-based protocols                       |
| **Complexity**               | Requires additional bit processing                                | Simpler for character-oriented systems                             |
| **Frame Size**               | Increases minimally with bit stuffing but depends on data         | Increases with additional escape characters                        |

---

### **Use Cases in Real-World Protocols**

- **Bit Stuffing**: Used in protocols like **HDLC (High-Level Data Link Control)** and **PPP (Point-to-Point Protocol)**, which are bit-oriented and commonly used in network layer communication.
- **Byte Stuffing**: Used in **ASCII-based protocols** like **SLIP (Serial Line Internet Protocol)**, often for serial data transmission.

Both **Bit Stuffing** and **Byte Stuffing** are essential for ensuring that data frames are recognized and interpreted accurately across different transmission protocols, preventing data corruption and synchronization errors in various types of networks.
