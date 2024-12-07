# Networking

## Carrier Sense Multiple Access

Carrier Sense Multiple Access (CSMA) is a **Medium Access Control (MAC)** protocol used in networks to minimize collisions and efficiently utilize a shared communication channel. The fundamental idea behind CSMA is that devices **sense the channel** for activity (carrier signal) before attempting to transmit data.

---

### **How CSMA Works**

1. **Carrier Sensing:**

   - Before transmitting data, a device listens to the channel to check if it is free or busy.

2. **Channel Availability:**

   - If the channel is free (no carrier detected), the device begins transmission.
   - If the channel is busy (carrier detected), the device waits for it to become idle.

3. **Collision Handling:**
   - Even with sensing, collisions can occur if multiple devices detect the channel as free and transmit simultaneously. Different variations of CSMA address this issue.

---

### **Types of CSMA**

1. **1-Persistent CSMA:**

   - Devices sense the channel continuously.
   - If the channel is free, they transmit immediately.
   - If busy, they keep sensing and transmit as soon as it becomes free.
   - **Disadvantage:** High chance of collisions when multiple devices wait for the channel.

2. **Non-Persistent CSMA:**

   - Devices sense the channel.
   - If busy, they wait for a random amount of time before sensing again.
   - **Advantage:** Reduces the chance of collisions.
   - **Disadvantage:** Increased delay.

3. **P-Persistent CSMA (used in slotted channels):**

   - Devices sense the channel and transmit with a probability \(p\) if free.
   - If the channel is busy or the device does not transmit, it waits for the next time slot and repeats the process.
   - Balances between 1-Persistent and Non-Persistent approaches.

4. **CSMA/CD (Collision Detection):**

   - Used in wired networks like Ethernet.
   - Devices sense the channel during transmission.
   - If a collision is detected, the device stops transmission and retries after a random delay.

5. **CSMA/CA (Collision Avoidance):**
   - Used in wireless networks like Wi-Fi.
   - Devices use mechanisms such as backoff timers and RTS/CTS (Request to Send / Clear to Send) to avoid collisions before they occur.

---

### **Advantages of CSMA**

1. Reduces the likelihood of collisions compared to random access protocols (like ALOHA).
2. Efficient for networks with moderate traffic.
3. Simple to implement and does not require synchronization.

---

### **Disadvantages of CSMA**

1. Collisions can still occur, especially in high-traffic conditions.
2. Performance degrades as the network load increases.
3. CSMA/CD is not suitable for wireless networks due to the difficulty in detecting collisions over shared radio frequencies.

---

### **Applications**

1. **CSMA/CD:**
   - Used in **Ethernet** (IEEE 802.3) for wired networks.
2. **CSMA/CA:**
   - Used in **Wi-Fi** (IEEE 802.11) for wireless networks.

---

### **Comparison with ALOHA**

| **Feature**         | **CSMA**                               | **ALOHA**                                |
| ------------------- | -------------------------------------- | ---------------------------------------- |
| Channel Sensing     | Yes                                    | No                                       |
| Collision Avoidance | Partial (depends on variant)           | None                                     |
| Efficiency          | Higher (depends on sensing)            | Lower                                    |
| Applications        | Wired/wireless (e.g., Ethernet, Wi-Fi) | Early wireless systems (e.g., ALOHA Net) |

CSMA is a foundational MAC protocol and is crucial in both wired and wireless communication systems to manage shared medium access effectively.

## Carrier Sense Multiple Access/ Collision Detection

**CSMA/CD** is a Medium Access Control (MAC) protocol used in shared communication networks to manage access to a common channel and handle collisions effectively. It is primarily used in **Ethernet (IEEE 802.3)** networks for wired communication.

---

### **How CSMA/CD Works**

1. **Carrier Sensing:**

   - A device listens to the channel to check if it is free or busy.
   - If the channel is free, it begins transmission.
   - If the channel is busy, it waits and retries after a random backoff time.

2. **Transmission:**

   - Once a device starts transmitting, it continues to monitor the channel for a collision signal.

3. **Collision Detection:**

   - If a collision occurs (multiple devices transmit simultaneously), it is detected by changes in voltage or signal patterns on the medium.

4. **Collision Resolution:**

   - When a collision is detected:
     - The device immediately stops transmitting.
     - It sends a **jamming signal** to inform all devices about the collision.
     - The devices then wait for a random amount of time (determined by the **exponential backoff algorithm**) before attempting to retransmit.

5. **Retransmission:**
   - After the random backoff period, the device senses the channel again and repeats the process.

---

### **Algorithm Steps**

1. **Sense the channel:** Check if the channel is free.
2. **Transmit data:** If free, start transmission.
3. **Monitor for collisions:** Continue sensing the channel during transmission.
4. **Handle collision:** If detected, stop and send a jamming signal.
5. **Retry after random delay:** Use the exponential backoff algorithm.

---

### **Advantages**

1. **Efficient for Low Traffic:**
   - Works well in networks with moderate traffic due to fewer collisions.
2. **Simple Mechanism:**
   - Easy to implement in wired networks where collision detection is feasible.
3. **Collision Management:**
   - Quickly detects and resolves collisions to minimize network downtime.

---

### **Disadvantages**

1. **Inefficient in High Traffic:**
   - Performance degrades as the network traffic increases, causing frequent collisions and retransmissions.
2. **Unsuitable for Wireless:**
   - Collision detection is impractical in wireless networks due to weak or overlapping signals and the hidden terminal problem.
3. **Channel Wastage:**
   - Collisions waste bandwidth, especially in large networks with many devices.

---

### **Applications**

1. **Ethernet (IEEE 802.3):**
   - CSMA/CD is the backbone protocol for traditional wired Ethernet networks.
2. **Local Area Networks (LANs):**
   - Often used in small to medium-sized networks for sharing resources.

---

### **Comparison with CSMA/CA (Collision Avoidance)**

| **Feature**            | **CSMA/CD**                       | **CSMA/CA**                               |
| ---------------------- | --------------------------------- | ----------------------------------------- |
| **Collision Handling** | Detects and resolves collisions.  | Avoids collisions before they occur.      |
| **Network Type**       | Suitable for wired networks.      | Designed for wireless networks.           |
| **Implementation**     | Simple; uses collision detection. | Complex; uses backoff timers and RTS/CTS. |
| **Examples**           | Wired Ethernet (IEEE 802.3).      | Wi-Fi (IEEE 802.11).                      |

---

### **Efficiency**

- **Channel Utilization:** CSMA/CD's efficiency depends on the propagation delay and the network's traffic load. For large networks or high traffic, the chances of collisions increase, reducing efficiency.
- **Maximum Efficiency:** Theoretical efficiency is around **37% for high traffic** when the propagation delay is minimal.

---

CSMA/CD was foundational for early Ethernet systems but is less relevant today as most modern Ethernet networks use **switched Ethernet**, which eliminates collisions altogether by dedicating separate communication channels to devices.

### **Carrier Sense Multiple Access with Collision Avoidance (CSMA/CA)**

**CSMA/CA** is a Medium Access Control (MAC) protocol used to minimize collisions in networks by avoiding them before transmission occurs. It is primarily used in **wireless networks** like **Wi-Fi (IEEE 802.11)** where collision detection (as in CSMA/CD) is impractical.

---

### How CSMA/CA Works

1. **Carrier Sensing:**

   - A device listens to the channel to check if it is free or busy (similar to CSMA/CD).

2. **Collision Avoidance:**

   - If the channel is free:
     - The device waits for a **contention window** (a random backoff period) before transmitting.
   - If the channel is busy:
     - The device waits until the channel is free and restarts the backoff timer.

3. **Optional RTS/CTS (Request to Send / Clear to Send):**

   - To further reduce the chance of collisions, the sender can use RTS/CTS:
     - Sender requests to send data by sending an **RTS**.
     - Receiver responds with a **CTS**, signaling that the channel is clear.
     - After receiving the CTS, the sender transmits data.

4. **Acknowledgment (ACK):**
   - The receiver sends an ACK after successfully receiving the data. If the ACK is not received, the sender assumes a collision occurred and retries.

---

### **Key Features of CSMA/CA**

- **Collision Avoidance:** It prevents collisions by waiting for a random time and optionally using RTS/CTS.
- **Backoff Timer:** Reduces the likelihood of repeated collisions by choosing random intervals for retransmission.
- **Hidden Terminal Problem:** RTS/CTS helps solve this problem where two devices, out of range of each other, can cause a collision.

---

### **Advantages**

1. **Efficient for Wireless:**
   - CSMA/CA is well-suited for wireless networks where collision detection is difficult due to weak or overlapping signals.
2. **Reduced Collisions:**
   - The protocol avoids collisions rather than detecting them, improving efficiency in wireless environments.
3. **Hidden Terminal Solution:**
   - RTS/CTS minimizes the hidden terminal problem.

---

### **Disadvantages**

1. **Increased Overhead:**
   - The use of backoff timers and optional RTS/CTS adds delays and reduces channel utilization.
2. **Lower Efficiency:**
   - Efficiency is reduced compared to CSMA/CD because of the additional steps for avoiding collisions.
3. **Performance in High Traffic:**
   - Performance decreases in highly congested networks due to frequent contention for the channel.

---

### **Applications**

- **Wi-Fi (IEEE 802.11):**
  - CSMA/CA is the fundamental MAC protocol in Wi-Fi networks.
- **Wireless Sensor Networks (WSNs):**
  - Used in sensor communication to avoid interference.
- **Ad-Hoc Wireless Networks:**
  - Enables effective communication in networks without a central coordinator.

---

### **Comparison: CSMA/CA vs. CSMA/CD**

| **Feature**            | **CSMA/CA**                               | **CSMA/CD**                                   |
| ---------------------- | ----------------------------------------- | --------------------------------------------- |
| **Collision Handling** | Avoids collisions before transmission.    | Detects collisions after transmission starts. |
| **Network Type**       | Wireless networks (e.g., Wi-Fi).          | Wired networks (e.g., Ethernet).              |
| **Mechanism**          | Uses backoff timers and optional RTS/CTS. | Monitors channel during transmission.         |
| **Implementation**     | Complex due to collision avoidance steps. | Simpler as it handles collisions reactively.  |
| **Examples**           | Wi-Fi (IEEE 802.11).                      | Ethernet (IEEE 802.3).                        |

---

### **Efficiency**

- CSMA/CA’s efficiency depends on:
  1. **Channel Conditions:** Noise and interference can reduce performance.
  2. **Network Traffic:** High contention can lead to frequent backoff and retries.
- Typically, CSMA/CA is less efficient than CSMA/CD due to the added collision avoidance steps.

---

### **Real-World Example: Wi-Fi (IEEE 802.11)**

- Devices sense the channel before transmitting.
- RTS/CTS is often used in environments with many hidden terminals (e.g., crowded Wi-Fi networks).
- Acknowledgment (ACK) ensures reliability in the transmission.

CSMA/CA is crucial for the smooth functioning of wireless networks where collisions are harder to detect and where avoiding them is critical for maintaining communication reliability.
