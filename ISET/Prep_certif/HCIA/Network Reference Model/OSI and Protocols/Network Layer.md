**HCIA Networking Fundamentals Summary**  
*(Network Layer: Addressing, Routing, and Packet Forwarding)*  

---

### **1. Network Layer Overview**  
- **Purpose**: Transmits data packets from **source host** to **destination host** across networks using **logical addressing** (IP addresses).  
- **Key Functions**:  
  - **Logical Addressing**: Assigns unique IP addresses to devices.  
  - **Routing**: Determines optimal paths for packets using routing tables.  
  - **Forwarding**: Moves packets between networks via routers.  
- **Protocol Data Unit (PDU)**: **Packets** (IP headers + transport layer data).  

---

### **2. IP Addressing**  
- **IPv4**:  
  - 32-bit address written in **dot-decimal notation** (e.g., `192.168.1.1`).  
  - Divided into **network** and **host** portions (subnetting).  
- **IPv6**: 128-bit address for larger address space (e.g., `2001:0db8:85a3::8a2e:0370:7334`).  
- **Uniqueness**: Each device on a network must have a unique IP address.  

---

### **3. Packet Encapsulation & Forwarding**  
#### **Encapsulation**:  
1. **Transport Layer**: Sends data (e.g., TCP/UDP segments) to the network layer.  
2. **Network Layer**: Adds **IP header** with:  
   - Source IP (sender’s address).  
   - Destination IP (receiver’s address).  
   - Protocol type (e.g., TCP=6, UDP=17).  

#### **Forwarding**:  
1. **Routers** use **routing tables** to determine the best path.  
2. Routing tables are built using **routing protocols** (e.g., OSPF, BGP).  
3. Each router checks the destination IP, matches it to a route, and forwards the packet to the next hop.  

---

### **4. Key Network Layer Protocols**  
| **Protocol** | **Purpose** |  
|--------------|-------------|  
| **IPv4/IPv6** | Delivers packets end-to-end. |  
| **ICMP** | Sends error messages (e.g., `ping`, `traceroute`). |  
| **IGMP** | Manages multicast group memberships. |  
| **OSPF/BGP** | Dynamic routing protocols (build routing tables). |  

---

### **5. Routing Process Example**  
1. **PC1** sends a packet to **PC2** with destination IP `2.2.2.2`.  
2. **Router 1** checks its routing table:  
   - **Destination Network** | **Next Hop** | **Outbound Interface**  
   - `2.2.2.0/24` | Directly connected | `G0/0/1`  
3. Router forwards the packet via interface `G0/0/1` to **PC2**.  

---

### **6. Role of ICMP**  
- **Diagnostics**: Tests connectivity (e.g., `ping` sends ICMP Echo Requests).  
- **Error Reporting**: Notifies issues (e.g., `Destination Unreachable`).  

---

### **7. Network Layer in OSI vs. TCP/IP**  
| **OSI Model** | **TCP/IP Model** |  
|---------------|-------------------|  
| Network Layer | Internet Layer |  
| Protocols: IPv4, ICMP | Same as OSI + IGMP |  

---

**Visual Aid Placeholders**:  
- Insert screenshot: **IP Packet Header Structure**.  
- Insert screenshot: **Routing Table Example**.  
- Insert screenshot: **ICMP Packet Flow**.  

---

**Conclusion**:  
The network layer ensures data reaches its destination via logical addressing and routing. Routers act as traffic directors, using protocols like OSPF and ICMP to optimize paths and troubleshoot issues. This layer is foundational for scalable and interconnected network communication.  

**Next Section Preview**:  
We will explore **Data Link Layer protocols (Ethernet, PPP)** and MAC addressing.