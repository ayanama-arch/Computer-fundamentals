# Networking

## IPv4 Header Format

The **IPv4 header** is a 20-byte (minimum) structure that contains crucial information about how a packet is handled as it travels through the network. Below is a detailed breakdown of the **IPv4 header format**, field-by-field:

---

### **1. Version (4 bits)**

Indicates the version of the Internet Protocol used. For IPv4, this value is always `4`.

---

### **2. Internet Header Length (IHL) (4 bits)**

Specifies the length of the header in 32-bit words. The minimum value is `5` (20 bytes), and the maximum is `15` (60 bytes). This field accounts for optional headers.

---

### **3. Type of Service (TOS) or Differentiated Services (DS) (8 bits)**

- Originally intended to specify the priority of the packet.
- Modern use is for **Differentiated Services Code Point (DSCP)** and **Explicit Congestion Notification (ECN)**.
  - **DSCP** (6 bits): Used for Quality of Service (QoS).
  - **ECN** (2 bits): Used for congestion control.

---

### **4. Total Length (16 bits)**

Specifies the total length of the IPv4 packet, including both the header and the data, in bytes. The maximum value is `65,535` bytes.

---

### **5. Identification (16 bits)**

A unique value used to identify fragments of a single IP datagram.

---

### **6. Flags (3 bits)**

Used to control and identify fragments:

- **Bit 0**: Reserved (must be `0`).
- **Bit 1**: **Don't Fragment (DF)** flag.
- **Bit 2**: **More Fragments (MF)** flag.

---

### **7. Fragment Offset (13 bits)**

Indicates the position of a fragment in the original datagram, in 8-byte units.

---

### **8. Time to Live (TTL) (8 bits)**

Limits the lifespan of the packet. It is decremented by 1 at each hop, and the packet is discarded if it reaches `0`.

---

### **9. Protocol (8 bits)**

Specifies the protocol used in the data portion of the packet, allowing the network layer to pass data to the appropriate upper-layer protocol:

- Example values: `6` (TCP), `17` (UDP), `1` (ICMP).

---

### **10. Header Checksum (16 bits)**

Ensures the integrity of the header. It is recalculated at each hop.

---

### **11. Source Address (32 bits)**

The IPv4 address of the sender.

---

### **12. Destination Address (32 bits)**

The IPv4 address of the intended recipient.

---

### **13. Options (variable length)**

Optional field for additional features like:

- Security settings.
- Route recording.
- Timestamping.

The options field is padded to ensure the header length is a multiple of 32 bits.

---

### **14. Data (variable length)**

Contains the payload or the actual data being transmitted. The size depends on the **Total Length** minus the **Header Length**.

---

### Diagram of the IPv4 Header Format:

```
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Version|  IHL  |Type of Service|        Total Length          |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|        Identification         |Flags|    Fragment Offset    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Time to Live |   Protocol    |        Header Checksum       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                      Source Address                          |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                   Destination Address                        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Options                    |    Padding    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

This structured format enables IPv4 to efficiently handle pack

## Fragmentation of IPv4 Datagram | Identification, Flags and Fragment Offset

IPv4 fragmentation occurs when a packet is too large to be transmitted over a network with a smaller **Maximum Transmission Unit (MTU)**. To handle this, the datagram is divided into smaller fragments, which are then transmitted independently and reassembled at the destination.

Key fields involved in fragmentation are **Identification**, **Flags**, and **Fragment Offset**.

---

### **Fields Used in Fragmentation**

#### 1. **Identification (16 bits)**

- This field uniquely identifies a datagram.
- All fragments of the original datagram share the same **Identification** value.
- It helps the destination device to associate and reassemble fragments into the original datagram.

---

#### 2. **Flags (3 bits)**

Used to control the fragmentation process. The 3 bits are:

- **Bit 0: Reserved**

  - Always set to `0`.

- **Bit 1: Don’t Fragment (DF)**

  - If set to `1`, it prevents fragmentation.
  - If a packet with this flag set cannot be transmitted due to MTU constraints, it is discarded, and an **ICMP "Fragmentation Needed"** message is sent.

- **Bit 2: More Fragments (MF)**
  - If set to `1`, it indicates that more fragments of this datagram follow.
  - For the last fragment, this bit is set to `0`.

---

#### 3. **Fragment Offset (13 bits)**

- Indicates the position of a fragment within the original datagram.
- Measured in **8-byte units** (64 bits).
  - The first fragment has an offset of `0`.
  - Subsequent fragments have offsets corresponding to their position in the original datagram.

---

### **Fragmentation Process**

1. **Fragmentation Trigger**:  
   When a datagram exceeds the MTU of the outgoing network link.

2. **Dividing the Datagram**:

   - The datagram is split into fragments, ensuring each fragment is small enough to fit within the MTU.
   - Each fragment contains a copy of the original IPv4 header.

3. **Setting Fields in Fragments**:

   - **Identification**: Same for all fragments of the original datagram.
   - **Flags**:
     - **DF** remains the same as in the original packet.
     - **MF** is set to `1` for all fragments except the last.
   - **Fragment Offset**: Updated to indicate the fragment's position.

4. **Reassembly at Destination**:
   - The destination uses the **Identification** field to group fragments.
   - The **Fragment Offset** and **MF flag** are used to arrange the fragments.
   - Once all fragments are received, the datagram is reassembled.

---

### **Example of Fragmentation**

Assume a datagram has a total length of **4,500 bytes** and an MTU of **1,500 bytes**.

- **Fragment 1**:

  - **Total Length**: 1,500 bytes
  - **Fragment Offset**: 0
  - **MF**: 1

- **Fragment 2**:

  - **Total Length**: 1,500 bytes
  - **Fragment Offset**: 185 (1,480 bytes/8)
  - **MF**: 1

- **Fragment 3**:
  - **Total Length**: 1,500 bytes
  - **Fragment Offset**: 370 (2,960 bytes/8)
  - **MF**: 0

---

### **Fragmentation Diagram**

```
Original Datagram (4,500 bytes):
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
| Header |                  Data (4,480 bytes)                |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

Fragment 1 (1,500 bytes):
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
| Header |                Data (1,480 bytes)                  |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

Fragment 2 (1,500 bytes):
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
| Header |                Data (1,480 bytes)                  |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

Fragment 3 (1,500 bytes):
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
| Header |                Data (1,480 bytes)                  |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

---

### **Key Notes**

- **Fragmentation can degrade network performance** due to overhead and reassembly processing.
- IPv6 eliminates fragmentation by requiring the sender to handle MTU issues using Path MTU Discovery.
- In IPv4, excessive fragmentation can lead to dropped packets if any fragment is lost.

## IPv6 Header Format

The **IPv6 header** is simpler and more streamlined compared to the IPv4 header, designed to handle the growing demands of modern networks. It is a fixed size of **40 bytes** and includes fields necessary for efficient routing and network communication. Below is a detailed breakdown of the **IPv6 header format**:

---

### **Fields in IPv6 Header**

#### **1. Version (4 bits)**

- Specifies the version of the Internet Protocol.
- For IPv6, this value is always `6`.

---

#### **2. Traffic Class (8 bits)**

- Indicates the priority of the packet.
- Used for Quality of Service (QoS) and traffic differentiation.
  - **6 bits**: Differentiated Services Code Point (DSCP).
  - **2 bits**: Explicit Congestion Notification (ECN).

---

#### **3. Flow Label (20 bits)**

- Used to label packets belonging to the same flow for special handling by routers.
- Helps in improving efficiency for applications like real-time video or voice.

---

#### **4. Payload Length (16 bits)**

- Indicates the size of the data (payload) in bytes, excluding the header.
- Maximum value: `65,535`. If more is required, an extension header called the **Jumbo Payload** is used.

---

#### **5. Next Header (8 bits)**

- Identifies the type of header that follows the IPv6 header.
- It can indicate:
  - A higher-layer protocol (e.g., TCP, UDP).
  - An extension header (e.g., Routing Header, Authentication Header).

---

#### **6. Hop Limit (8 bits)**

- Similar to the **Time to Live (TTL)** field in IPv4.
- Decremented by 1 at each hop. The packet is discarded if it reaches `0`.

---

#### **7. Source Address (128 bits)**

- The IPv6 address of the packet's sender.

---

#### **8. Destination Address (128 bits)**

- The IPv6 address of the packet's recipient.

---

### **Diagram of IPv6 Header**

```
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
| Version | Traffic Class |           Flow Label              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|        Payload Length       |  Next Header  |   Hop Limit   |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
|                         Source Address                        |
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
|                      Destination Address                      |
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

---

### **Key Features of IPv6 Header**

1. **Fixed Header Size**:

   - The IPv6 header is always 40 bytes long, unlike IPv4, where the header size varies.

2. **Simplified Header**:

   - Eliminates rarely used fields (e.g., Fragment Offset, Header Checksum).
   - Handles optional features using **Extension Headers**.

3. **Improved Routing**:

   - The simplified header design makes processing faster and more efficient.

4. **Extension Headers**:
   - Additional functionalities are handled via optional **extension headers**, such as:
     - Hop-by-Hop Options Header.
     - Routing Header.
     - Fragment Header.
     - Authentication Header.

---

### **Comparison with IPv4 Header**

| **Field**      | **IPv4**                | **IPv6**                             |
| -------------- | ----------------------- | ------------------------------------ |
| Header Size    | Variable (20-60 bytes)  | Fixed (40 bytes)                     |
| Address Size   | 32 bits                 | 128 bits                             |
| Fragmentation  | Handled by IPv4 header  | Handled by Extension Headers         |
| Checksum Field | Present                 | Removed (handled by upper layers)    |
| QoS Support    | Basic (Type of Service) | Advanced (Traffic Class, Flow Label) |

---

### **Benefits of IPv6 Header Format**

- **Scalability**: Supports the growing number of devices with a vastly larger address space.
- **Performance**: Simplified header reduces router processing overhead.
- **Flexibility**: Extension headers allow for customization without affecting the base header.
- **Security**: Integrated support for IPsec ensures better security.

This design makes IPv6 ideal for modern, large-scale, and dynamic network environments.
