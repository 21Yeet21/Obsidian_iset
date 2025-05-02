**HCIA Networking Fundamentals Summary**  
*(Transport Layer: TCP, UDP, and Data Transmission)*  

---

### **1. Transport Layer Overview**  
- **Purpose**: Ensures end-to-end communication between applications using **port numbers**.  
- **Key Protocols**:  
  - **TCP (Transmission Control Protocol)**: Connection-oriented, reliable, with flow/error control.  
  - **UDP (User Datagram Protocol)**: Connectionless, lightweight, low latency.  
- **PDU**: Segments (TCP/UDP headers + data).  

---

### **2. TCP vs. UDP Headers**  
#### **TCP Header (20+ bytes)**:  
![[Pasted image 20250301213015.png]]

| Field | Description |  
|-------|-------------|  
| **Source/Destination Port** | Identifies sending/receiving applications (16 bits each). |  
| **Sequence Number** | Tracks byte order for reliable delivery (32 bits). |  
| **Acknowledgment Number** | Confirms received bytes (32 bits; valid if ACK flag set). |  
| **Header Length** | Header size in 32-bit words (4 bits). |  
| **Control Bits** | Flags like SYN (connection setup), ACK (acknowledgment), FIN (connection termination). |  
| **Window Size** | Receiver’s buffer capacity for flow control (16 bits). |  
| **Checksum** | Validates header/data integrity (16 bits). |  
| **Urgent Pointer** | Marks urgent data (valid if URG flag set). |  

#### **UDP Header (8 bytes)**:  
| Field | Description |  
|-------|-------------|  
| **Source/Destination Port** | Identifies applications (16 bits each). |  
| **Length** | Total header + data length (16 bits; max 65,535 bytes). |  
| **Checksum** | Optional validation of header/data. |  

---

### **3. TCP Connection Management**  
#### **Three-Way Handshake (Connection Setup)**:  
1. **SYN**: Client sends segment with `SYN=1` and random `Seq=a`.  
2. **SYN-ACK**: Server replies with `SYN=1`, `ACK=1`, `Seq=b`, and `Ack=a+1`.  
3. **ACK**: Client confirms with `ACK=1`, `Seq=a+1`, `Ack=b+1`.  
4. ![[Pasted image 20250301213101.png]]

#### **Four-Way Handshake (Connection Termination)**:  
1. **FIN**: Host A sends `FIN=1` to close its send direction.  
2. **ACK**: Host B acknowledges the FIN.  
3. **FIN**: Host B sends its own `FIN=1`.  
4. **ACK**: Host A acknowledges B’s FIN.  
![[Pasted image 20250301213226.png]]
---

### **4. Reliability & Flow Control**  
- **Sequence & Acknowledgment Numbers**:  
  - Each byte is numbered; `Ack=N` means all bytes up to `N-1` are received.  
  - Example: If PC1 sends 12 bytes with `Seq=100`, PC2 replies with `Ack=112`.  
  - ![[Pasted image 20250301213143.png]]
- **Sliding Window**:  
  - **Window Size**: Receiver advertises available buffer space (e.g., `win=3` = 3 segments).  
  - Sender transmits data within the window; receiver updates window as buffer frees.  
  - ![[Pasted image 20250301213158.png]]

---

### **5. Port Numbers**  
- **Source Port**: Randomly chosen by client (typically >1023).  
- **Destination Port**: Fixed for services (e.g., 80 for HTTP, 23 for Telnet).  
- **Example**:  
  - Client IP: `1.1.1.1:1024` → Server IP: `2.2.2.2:80` (HTTP).  

![[Pasted image 20250301213046.png]]
---

### **6. Key Differences: TCP vs. UDP**  
| **Feature** | **TCP** | **UDP** |  
|-------------|---------|---------|  
| Connection | Connection-oriented | Connectionless |  
| Reliability | Guaranteed (retransmits lost data) | Best-effort |  
| Speed | Slower (overhead) | Faster |  
| Use Cases | Web browsing, email | Video streaming, VoIP |  

---

**Visual Aid Placeholders**:  
- Insert screenshot: **TCP Three-Way Handshake**.  
- Insert screenshot: **TCP Header Format**.  
- Insert screenshot: **Sliding Window Mechanism**.  
- Insert screenshot: **TCP Four-Way Handshake**.  

---

**Next Section Preview**:  
We will explore **Network Layer protocols (IP, ICMP, IGMP)** and routing mechanisms.