# Networking

## Various Medium Access Control Protocols in Data Link Layer

Medium Access Control (MAC) protocols are part of the Data Link Layer in the OSI model and are responsible for controlling how devices in a network access and share a common communication medium. These protocols ensure efficient and collision-free transmission. Below are the various types of MAC protocols:

---

### 1. **Contention-Based Protocols (Random Access)**

These protocols allow devices to transmit data without coordination, potentially leading to collisions, which are resolved using specific techniques.

- **ALOHA:**

  - **Pure ALOHA:** Devices transmit data whenever they have data to send, leading to high chances of collisions.
  - **Slotted ALOHA:** Divides time into slots, allowing transmissions only at the start of a slot, reducing collisions compared to pure ALOHA.

- **Carrier Sense Multiple Access (CSMA):**
  - Devices sense the channel before transmitting.
  - Variants:
    - **CSMA/CD (Collision Detection):** Used in Ethernet. Devices detect collisions during transmission and retransmit after a random delay.
    - **CSMA/CA (Collision Avoidance):** Used in Wi-Fi. Devices avoid collisions by reserving the channel using techniques like RTS/CTS (Request to Send/Clear to Send).

---

### 2. **Scheduled Access Protocols (Deterministic)**

These protocols use a predefined schedule to ensure orderly access to the medium.

- **Time Division Multiple Access (TDMA):**

  - Divides time into slots, with each device assigned a specific slot for transmission.

- **Frequency Division Multiple Access (FDMA):**

  - Divides the frequency spectrum into channels, with each device assigned a specific frequency band.

- **Code Division Multiple Access (CDMA):**

  - Devices use unique codes to encode data, allowing multiple transmissions over the same frequency without interference.

- **Polling:**

  - A central controller polls each device in turn to check if it has data to send.

- **Token Passing:**
  - A token (a small data packet) circulates in the network. Only the device holding the token can transmit data.

---

### 3. **Hybrid Protocols**

These combine features of contention-based and scheduled access protocols for better performance.

- **Distributed Coordination Function (DCF):**

  - A hybrid of CSMA/CA used in Wi-Fi. It employs random backoff timers after collisions.

- **Point Coordination Function (PCF):**
  - Centralized scheduling mechanism used in Wi-Fi for time-sensitive transmissions.

---

### 4. **Reservation-Based Protocols**

These protocols allow devices to reserve the medium before transmission to avoid collisions.

- **Dynamic TDMA (D-TDMA):**

  - Dynamically allocates time slots based on demand.

- **Reservation ALOHA (R-ALOHA):**
  - Combines ALOHA with a reservation mechanism to improve efficiency.

---

### 5. **Channelization Protocols**

These protocols divide the communication medium into separate logical channels.

- **Space Division Multiple Access (SDMA):**

  - Divides the medium spatially, allowing devices to transmit simultaneously in different locations.

- **Orthogonal Frequency Division Multiple Access (OFDMA):**
  - A type of FDMA where sub-carriers are orthogonal, reducing interference.

---

### Applications of MAC Protocols

- **ALOHA, CSMA/CD:** Ethernet networks.
- **CSMA/CA:** Wireless networks (e.g., Wi-Fi).
- **TDMA, FDMA, CDMA:** Cellular networks.
- **Token Passing:** Industrial and real-time systems.
- **OFDMA:** Modern broadband (e.g., LTE, 5G).

Each protocol is suited for specific scenarios depending on network size, delay requirements, and collision handling capabilities.

## Pure Aloha

**Pure ALOHA** is one of the simplest **Medium Access Control (MAC)** protocols used to manage access to a shared communication channel in a network. It was introduced by **Norman Abramson** in the 1970s at the University of Hawaii for radio communication.

---

### **How It Works**

1. **Uncoordinated Transmission:**

   - Devices transmit data whenever they have data to send without checking whether the channel is free or busy.

2. **Collisions:**

   - If two or more devices transmit simultaneously, their data packets collide, leading to corruption. Collided packets are discarded, and retransmissions occur after a random delay.

3. **Retransmission:**
   - After a collision, devices wait for a random time before retransmitting to minimize the chance of repeated collisions.

---

### **Advantages**

1. **Simplicity:**

   - Pure ALOHA is easy to implement because it does not require carrier sensing or synchronization.

2. **Decentralized:**
   - There is no need for central control or coordination among devices.

---

### **Disadvantages**

1. **Low Efficiency:**

   - Pure ALOHA has a maximum channel utilization of **18.4%**, meaning a significant portion of the time is wasted due to collisions.

2. **High Collision Rate:**
   - Since devices transmit randomly, collisions are frequent, especially as the number of devices increases.

---

### **Efficiency Analysis**

- The probability of successful transmission depends on the time when packets are sent.
- For a packet to be transmitted successfully:
  - **No other packet should start within the packet's duration.**
- This leads to a **channel efficiency** of approximately **18.4%** (derived from probability calculations).

---

### **Applications**

- Initially used in early radio communication systems like the ALOHA network.
- Basis for more advanced protocols like **Slotted ALOHA**, **CSMA**, and **CSMA/CD**.

---

### **Comparison with Slotted ALOHA**

| **Feature**           | **Pure ALOHA**            | **Slotted ALOHA**                        |
| --------------------- | ------------------------- | ---------------------------------------- |
| Time Division         | No slots (unsynchronized) | Divides time into fixed slots            |
| Collision Probability | Higher                    | Lower (restricted transmission to slots) |
| Channel Efficiency    | 18.4%                     | 36.8%                                    |

Pure ALOHA is a foundational concept in networking and paved the way for the development of more efficient MAC protocols.

## Pure Aloha Vs Slotted Aloha

| **Feature**               | **Pure ALOHA**                                                    | **Slotted ALOHA**                                                            |
| ------------------------- | ----------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| **Time Synchronization**  | No synchronization; devices transmit anytime.                     | Time is divided into slots, and devices transmit at the beginning of a slot. |
| **Collision Probability** | Higher collision probability as packets can overlap at any point. | Lower collision probability since transmissions are confined to time slots.  |
| **Efficiency**            | Maximum channel efficiency is **18.4%**.                          | Maximum channel efficiency is **36.8%**.                                     |
| **Implementation**        | Easier to implement due to no time synchronization.               | More complex due to the need for time synchronization.                       |
| **Delay**                 | Potentially higher delays due to frequent collisions.             | Lower delays as collisions are reduced by slot synchronization.              |
| **Retransmission**        | Random backoff and retransmission after collisions.               | Similar backoff but only retransmits at the start of the next slot.          |
| **Channel Utilization**   | Poor, especially as traffic increases.                            | Better channel utilization compared to Pure ALOHA.                           |

---

### **Key Differences**

1. **Time Division:**

   - Pure ALOHA: No time slots; packets can be sent anytime.
   - Slotted ALOHA: Time is divided into equal slots; packets are sent only at the beginning of a slot.

2. **Efficiency:**

   - Slotted ALOHA doubles the efficiency of Pure ALOHA by reducing the chances of collisions to within time slots.

3. **Collisions:**
   - In Pure ALOHA, collisions can occur whenever two packets overlap.
   - In Slotted ALOHA, collisions occur only if two packets are sent in the same slot.

---

### **Efficiency Analysis**

- **Pure ALOHA:**  
  Probability of successful transmission: \( e^{-2} \approx 18.4\% \).

- **Slotted ALOHA:**  
  Probability of successful transmission: \( e^{-1} \approx 36.8\% \).

---

### **Advantages**

- **Pure ALOHA:**

  - Simpler and does not require synchronization.
  - Suitable for small networks with low traffic.

- **Slotted ALOHA:**
  - Higher efficiency and better for moderate to high traffic scenarios.
  - Less frequent collisions due to slot alignment.

---

### **Disadvantages**

- **Pure ALOHA:**

  - Inefficient due to high collision probability.
  - Poor performance in high traffic conditions.

- **Slotted ALOHA:**
  - Requires synchronization of devices, increasing complexity.
  - Still suffers from collisions if multiple devices choose the same slot.

---

### **Applications**

- **Pure ALOHA:** Early wireless communication systems, like the original ALOHA network.
- **Slotted ALOHA:** Satellite communication systems, some early versions of mobile telephony, and RFID systems.

Both protocols are foundational in networking, but Slotted ALOHA offers significant improvements in efficiency over Pure ALOHA at the cost of added synchronization complexity.
