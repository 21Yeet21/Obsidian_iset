
Tenstep

### **Summary: Networking Concepts & OSI Model Layers**  
This material covers networking fundamentals, protocols, and their alignment with the OSI model. Below is a structured breakdown:

---

### **1. OSI Model Layer Assignments**  
#### **Layer 1 (Physical Layer)**  
- **Modem**: Encodes bits into signals (baud rate, noise/dB management, compression).  
- **codage** : (bit -> signal : Manchester , NKZ , miller)
- **5G**: Operates at the Physical layer using radio frequencies.  
- **Signal**: Physical transmission (e.g., synchronization, phase shifts).  
- **RJ45**: Physical connector for Ethernet cables.  
- **ADSL Compression**: Uses 16 amplitude levels for modulation.  
- **Fiber (monomode)**: Physical medium for high-speed data transmission.  

#### **Layer 2 (Data Link Layer)**  
- **MAC Addresses**: Unique identifiers for network interfaces.  
- **802.11 (Wi-Fi)**: Defines wireless LAN standards (e.g., CSMA/CD for collision detection).  
- **CSMA/CD**: Protocol for Ethernet collision management.  

#### **Layer 3 (Network Layer)**  
- **Routing (OSPF)**: Protocol for path selection (operates at Layer 3, but messages are generated at the Application layer).  Application (OSPF -> Message) et R(\*)
- **Routers**: Forward packets using IP addresses.   Network layer + app(\*)
- **Adressage (IP)**: Logical addressing (e.g., IPv4/IPv6).  

#### **Layer 4 (Transport Layer)**  
- **TCP**: Connection-oriented protocol with flow control and windowing.  
- **Flow Control**: Manages data flow to prevent overload (e.g., "prêt/non prêt" or ready/not-ready signals).  
- **Windowing**: Adjusts data transmission size based on network quality (QoS).  

#### **Layer 6 (Presentation Layer)**  
- **Encoding**: Converts data formats (e.g., characters, pixels) for compatibility.  
- **Compression**: Reduces data size (e.g., ADSL modulation).  

#### **Layer 7 (Application Layer)**  
- **SMTP**: Email transmission protocol.  
- **Chrome**: Web browser interacting with HTTP/HTTPS.  
- **Adressage (URLs)**: Human-readable addresses (e.g., `www.example.com`).  

---

### **2. Key Concepts & Relationships**  
- **Full Mesh (Maille)**: A network topology where every node connects to every other node (high redundancy, used in critical systems).  
- **Synchro**:  
  - **Physical Layer**: Clock synchronization, signal timing.  
  - **Session Layer**: Manages session continuity (e.g., TCP sessions).  
- **Resource Allocation**:  
  - **CPU/RAM Overcommitment**: Risks include scheduling delays (CPU) and disk swapping (RAM).  
  - **GPU Virtualization**: Tools like VMware Bitfusion pool GPU resources for tasks like machine learning.  

---

### **3. Protocol & Technology Mapping**  
| **Term**          | **Layer/Function**                          | **Example/Use Case**                  |  
|--------------------|---------------------------------------------|----------------------------------------|  
| **TCP**            | Layer 4 (Transport)                         | Reliable data transfer (e.g., web browsing). |  
| **OSPF**           | Layer 3 (Network)                           | Dynamic routing in large networks.     |  
| **CSMA/CD**        | Layer 2 (Data Link)                         | Ethernet collision detection.          |  
| **SMTP**           | Layer 7 (Application)                       | Sending emails.                        |  
| **MAC Address**    | Layer 2 (Data Link)                         | Uniquely identifies network interfaces.|  
| **5G**             | Layer 1 (Physical)                          | High-speed wireless communication.     |  

---

### **4. French Term Clarifications**  
- **Débit**: Throughput/bandwidth.  
- **Déphasage**: Phase shift (signal timing issues).  
- **Fenêtrage**: Windowing (data transmission control).  
- **Prêt/non prêt**: Ready/not-ready (flow control states).  

---

### **5. Key Takeaways**  
1. **OSI Model**: A framework for understanding network operations across layers.  
2. **Full Mesh Topology**: Ideal for high availability but costly to implement.  
3. **Layer Interactions**: Protocols like OSPF (Layer 3) rely on Application-layer messages for updates.  
4. **Compression**: Occurs at both Physical (ADSL) and Presentation layers (data formatting).  
