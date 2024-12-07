## Networking

## TCP Data Transfer

TCP ensures reliable data transmission between a sender and receiver by dividing the data into segments and numbering them. It uses **acknowledgments**, **sequence numbers**, and **error-checking** to ensure the data arrives correctly and in order.

---

### **Process of TCP Data Transfer**

1. **Data Segmentation**:

   - The application layer data is divided into smaller units called TCP segments.
   - Each segment is given a **sequence number** to track its position in the overall data stream.

2. **Sending Data**:

   - Segments are sent over the network to the receiver. The sequence number in the header indicates the starting byte of the data in that segment.

3. **Acknowledgment**:

   - The receiver sends an **ACK (Acknowledgment)** back to confirm receipt of the segment.
   - The acknowledgment contains an **Acknowledgment Number**, which specifies the next byte the receiver expects.

4. **Retransmission**:

   - If a segment is lost or corrupted, the receiver does not send an acknowledgment for it.
   - After a timeout, the sender retransmits the unacknowledged segment.

5. **Flow Control**:
   - TCP uses the **window size** field to control the rate of data flow between sender and receiver to prevent overwhelming the receiver.

---

### **Acknowledgments in TCP**

TCP acknowledges received segments in one of two ways:

1. **Pure Acknowledgment**:

   - An acknowledgment segment without data payload.
   - It is sent when no new data is available to be sent but the received data needs to be acknowledged.
   - Example:
     ```
     Client: Sends data
     Server: Sends a pure ACK to confirm receipt.
     ```

2. **Piggybacking**:
   - Combines acknowledgment with data payload in a single segment.
   - It reduces the number of segments transmitted, improving efficiency.
   - Example:
     ```
     Client: Sends data
     Server: Sends ACK along with its own data in the same segment.
     ```

---

### **What is Piggybacking?**

**Piggybacking** is the process of combining acknowledgment and data into a single TCP segment instead of sending them separately.

#### **Advantages of Piggybacking**:

- **Efficiency**:
  - Reduces the number of segments transmitted, saving bandwidth.
- **Lower Overhead**:
  - Fewer segments mean fewer headers, reducing the total transmission cost.
- **Reduced Latency**:
  - Faster communication as fewer segments are exchanged.

#### **Disadvantage of Piggybacking**:

- **Delays in Acknowledgment**:
  - If the application has no data to send, acknowledgment may be delayed until the application generates data. This can lead to performance issues in time-sensitive applications.

---

### **What is Pure Acknowledgment?**

**Pure Acknowledgment** is an acknowledgment segment sent without any accompanying data payload.

#### **Advantages of Pure Acknowledgment**:

- **Timely Acknowledgment**:
  - Ensures the sender knows the data was received promptly, even when no new data is being sent.

#### **Disadvantages of Pure Acknowledgment**:

- **Higher Overhead**:
  - Sending acknowledgments without data increases the number of segments transmitted, adding to network overhead.

---

### **When Does TCP Use Each?**

1. **Piggybacking**:

   - Used when both the sender and receiver have data to exchange.
   - Example: File upload/download where data flows in both directions.

2. **Pure Acknowledgment**:
   - Used when one side has no data to send but needs to acknowledge received data.
   - Example: Web browsing where a server sends data but the client only acknowledges.

---

### **Example of Piggybacking vs Pure Acknowledgment**

**Scenario**: Client and server exchanging data.

- **Without Piggybacking**:

  ```
  Client → Server: Data Segment 1
  Server → Client: Pure ACK for Segment 1
  Server → Client: Data Segment 2
  Client → Server: Pure ACK for Segment 2
  ```

- **With Piggybacking**:
  ```
  Client → Server: Data Segment 1
  Server → Client: ACK for Segment 1 + Data Segment 2
  Client → Server: ACK for Segment 2 + Data Segment 3
  ```

---

## TCP Congestion Control

### **TCP Congestion Control**

TCP congestion control is a mechanism used to regulate the flow of data to prevent network congestion. It ensures that the sender does not overwhelm the network or the receiver by dynamically adjusting the transmission rate based on network conditions.

---

### **Why is Congestion Control Needed?**

1. **Shared Resources**:
   - In a network, multiple devices share the same resources (e.g., bandwidth). Unregulated traffic can lead to congestion.
2. **Packet Loss**:

   - Congestion leads to packet loss, increased delays, and retransmissions, degrading network performance.

3. **Fairness**:
   - Congestion control ensures all devices get a fair share of network resources.

---

### **Phases of TCP Congestion Control**

TCP uses a **congestion window (cwnd)** to control the amount of data a sender can transmit before receiving an acknowledgment. The size of the congestion window is adjusted dynamically based on network feedback.

1. **Slow Start**:

   - The sender starts by transmitting a small amount of data (typically one segment).
   - For every acknowledgment received, the congestion window increases **exponentially** (doubles each round-trip time).
   - Purpose: Quickly determine the available capacity without causing congestion.

   **Formula**:

   ```
   cwnd = cwnd + MSS (for each ACK received)
   ```

   _MSS_: Maximum Segment Size.

   **Limit**: Growth continues until reaching the **slow start threshold (ssthresh)** or encountering packet loss.

2. **Congestion Avoidance**:

   - Once the congestion window reaches the slow start threshold, the growth rate becomes **linear**.
   - The sender increases the congestion window size by one MSS for each round-trip time.

   **Formula**:

   ```
   cwnd = cwnd + (MSS * MSS / cwnd) (per ACK)
   ```

3. **Congestion Detection and Recovery**:
   TCP detects congestion when:
   - A packet is lost (indicated by timeout or duplicate ACKs).
   - On detecting congestion, TCP reduces the transmission rate to alleviate network stress.

---

### **Congestion Detection Mechanisms**

1. **Timeout**:

   - If no acknowledgment is received within a certain period, TCP assumes congestion has occurred.

2. **Duplicate Acknowledgments**:
   - If multiple duplicate ACKs are received (typically 3), TCP interprets it as a sign of packet loss due to congestion.

---

### **TCP Congestion Control Algorithms**

1. **Tahoe**:

   - When packet loss is detected, TCP:
     - Sets `ssthresh = cwnd / 2`.
     - Resets `cwnd = 1 MSS`.
     - Enters **Slow Start** phase.

2. **Reno**:

   - Similar to Tahoe but introduces **Fast Recovery**:
     - On receiving 3 duplicate ACKs, `ssthresh = cwnd / 2`, but instead of resetting `cwnd` to 1 MSS, it sets `cwnd = ssthresh` and enters **Congestion Avoidance** directly.

3. **New Reno**:

   - Improves Reno by handling multiple packet losses within the same window without falling back to Slow Start.

4. **Vegas**:
   - Uses delay-based measurements to detect congestion early, adjusting `cwnd` before packet loss occurs.

---

### **Congestion Control Process Summary**

| **Phase**                | **Action**                                      | **Growth Pattern**            |
| ------------------------ | ----------------------------------------------- | ----------------------------- |
| **Slow Start**           | Starts with a small `cwnd` and grows rapidly.   | Exponential growth            |
| **Congestion Avoidance** | Gradually increases `cwnd` to avoid congestion. | Linear growth                 |
| **Congestion Detection** | Reduces `cwnd` upon detecting congestion.       | Reduction based on algorithm. |

---

### **Visualization of Congestion Control**

1. **Congestion Window Growth**:

   ```
   Time →
   cwnd →
            /|\                     Linear Growth
           / | \
   Exponential Growth
   ```

2. **Behavior During Congestion**:
   - When congestion is detected, `cwnd` is reduced, and the cycle repeats.

---

### **Benefits of TCP Congestion Control**

- **Reliability**:
  Ensures data is transmitted without overloading the network.
- **Efficiency**:
  Adapts to changing network conditions.

- **Fairness**:
  Prevents a single connection from dominating shared resources.

---
