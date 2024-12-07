# Networking commands

## Basic Commands

---

### **1. ipconfig (Windows Only)**

Displays or manages the network configuration of a computer.

#### **Usage:**

- `ipconfig`  
  Shows basic information like IP address, subnet mask, and default gateway for all network adapters.
- `ipconfig /all`  
  Displays detailed information, including DHCP status, DNS servers, MAC address, and more.
- `ipconfig /release`  
  Releases the current IP address assigned by DHCP.
- `ipconfig /renew`  
  Renews the IP address from the DHCP server.

#### **Key Scenarios:**

- Diagnosing IP-related issues (e.g., no IP assigned).
- Checking the local machine’s IP address.

---

### **2. ifconfig (Linux/Unix)**

Similar to `ipconfig`, it displays and configures network interfaces on Unix-based systems. (Replaced by `ip` in newer Linux distributions.)

#### **Usage:**

- `ifconfig`  
  Displays network interfaces and their status.
- `ifconfig eth0`  
  Shows details of a specific interface (`eth0`).
- `ifconfig eth0 down` / `ifconfig eth0 up`  
  Disables or enables a network interface.

#### **Key Scenarios:**

- Viewing network interface configurations.
- Troubleshooting or configuring Linux network settings.

---

### **3. nslookup**

Performs DNS lookups to find the IP address associated with a domain name or vice versa.

#### **Usage:**

- `nslookup <domain>`  
  Queries the DNS server to resolve the domain name to an IP address (e.g., `nslookup www.google.com`).
- `nslookup`  
  Opens an interactive mode where you can type multiple queries.

#### **Key Scenarios:**

- Checking if a domain resolves to the correct IP address.
- Debugging DNS issues.

---

### **4. ping**

Tests network connectivity to a host by sending ICMP Echo Requests and measuring the response time.

#### **Usage:**

- `ping <host>`  
  Sends packets to a host (e.g., `ping google.com`) and displays round-trip time (RTT) and packet loss.
- `ping -t <host>` (Windows)  
  Continuous ping; press `Ctrl+C` to stop.
- `ping -c 4 <host>` (Linux)  
  Sends a fixed number of packets (e.g., 4).

#### **Key Scenarios:**

- Checking if a host is reachable.
- Measuring latency to a server.

---

### **5. tracert (Windows) / traceroute (Linux/Unix)**

Traces the route packets take from your computer to a destination and lists each hop.

#### **Usage:**

- `tracert <host>` (Windows)  
  Traces the route to the host (e.g., `tracert www.google.com`).
- `traceroute <host>` (Linux)  
  Similar to `tracert`.

#### **Key Scenarios:**

- Identifying where network delays or failures occur.
- Diagnosing routing issues between your machine and a remote host.

---

### **Comparison Table**

| Command        | Function                                  | Platforms          |
| -------------- | ----------------------------------------- | ------------------ |
| **ipconfig**   | View/manage network settings              | Windows            |
| **ifconfig**   | View/manage network settings (deprecated) | Linux/Unix         |
| **nslookup**   | DNS resolution                            | Windows/Linux/Unix |
| **ping**       | Test connectivity and latency             | Windows/Linux/Unix |
| **tracert**    | Trace packet route to destination         | Windows            |
| **traceroute** | Trace packet route (Linux equivalent)     | Linux/Unix         |

---

### **Practical Example:**

To troubleshoot a connectivity issue:

1. Use `ping <IP>` to see if the destination is reachable.
2. If `ping` fails, use `tracert <IP>` to check where the failure occurs.
3. Use `ipconfig /all` to verify your machine's IP and DNS settings.
4. Use `nslookup <domain>` to verify DNS resolution.

These commands provide a foundation for diagnosing and resolving network problems.
