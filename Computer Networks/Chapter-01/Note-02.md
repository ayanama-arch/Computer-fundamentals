## IP Address

Every node in the computer network is identified with the help of IP Address

- IP Address is logical address.
- IP can change on the basis of location of device.
- Assigned by manually or dynamically.

## IPV4

Represented in decimal and has 4 octedt(x.x.x.x)

Range from 0.0.0.0 to 255.255.255.255 (32bits)

## Mac Addressing

- MAC stands for Media Access Control.
- Every node in the LAN is identified with the help of MAC address.
- IP Address = Location of person
- MAC Address = Name of the person

* Every node in the LAN is identified with the help of MAC address.
* physical or hardware address.
* Unique
* Cannot be changed.
* Assigned by manufacturer
* Represented in hexadecimal
* `Example:` 70-20-84-00-ED-FC (48 bits)
* Separator: hyphen(-), period(.) and colon(:)

## PORT Addressing

- Every process in a node is uniquely identified using port numbers.
- Fixed port numbers: 25,80 etc,
- OS assigned dynamic port: eg 62414

## Switching

Switching is deciding the best route for data transmission.

`Switching Techinques`

1. Circuit Switching
2. Message Switching
3. Packet Switching
   - Datagram Approach
   - Virtual Circuit Approach

### Circuit Switching

- A dedicated path is established between sender and reciever.
- Before Data transfer, connection will be established first.
- `Example`: Telephone Network

**3 Phases in circuit switchign**

1. Connection establishment
2. Data transfer
3. Connection disconnection

### Message Switching

- Store and forward mechanism
- Message is transferred as a complete unit and forwarded using store and forward mechanism at the intermediar node.
- Not suited for streaming media and real-time applications.

`Example`

1. **Email Systems**: Messages are stored on a mail server and forwarded to the recipient when they come online.
2. **SMS**: Text messages are stored in intermediate servers and delivered to the recipient when their device is reachable.

### Packet Switching

Packet switching is a network communication method where data is broken into smaller packets before being transmitted. Each packet is sent independently and can take different routes to the destination. At the receiver's end, packets are reassembled into the original data.

---

### **Types of Packet Switching**

1. **Datagram Packet Switching (Connectionless)**

   - Each packet is treated independently, and packets may arrive out of order.
   - No pre-established path; packets can take any route based on availability.
   - **Example**: The Internet uses this method; data packets (e.g., web requests) may take different paths and are reassembled upon arrival.

2. **Virtual Circuit Packet Switching (Connection-Oriented)**
   - A logical path (virtual circuit) is established before sending packets, ensuring they follow the same route.
   - Packets arrive in order, reducing reassembly effort.
   - **Example**: MPLS (Multiprotocol Label Switching) networks use virtual circuits for predictable data delivery.

---

### **Examples of Packet Switching in Use**

1. **Web Browsing**: When you load a website, data (HTML, CSS, images) is sent as packets through various network paths.
2. **Video Streaming**: Services like YouTube or Netflix send video data as packets, allowing continuous playback even if packets take different routes.
3. **VoIP (Voice over IP)**: Applications like Skype or WhatsApp send voice data as packets for efficient, real-time communication.

---

### **Advantages**

- Efficient use of bandwidth.
- Robust and fault-tolerant, as packets can reroute around issues.
- Scalable for large networks like the Internet.

### **Disadvantages**

- Packets may experience delays or arrive out of order.
- Requires complex protocols (e.g., TCP/IP) for reassembly and reliability.
