
**HCIA Networking Fundamentals Summary**  
*(Continues coverage of standardization bodies and application layer protocols)*  

---

### **1. Common Protocol Standardization Organizations**  
| **Organization** | **Role** | **Key Contributions** |  
|-------------------|----------|-----------------------|  
| **IETF** (Internet Engineering Task Force) | Develops and promotes Internet protocols (TCP/IP suite) via **RFCs** (Request for Comments). | HTTP, FTP, TCP/IP standards. |  
| **IEEE** (Institute of Electrical and Electronics Engineers) | Creates standards for electronics, computing, and networking. | IEEE 802.3 (Ethernet), IEEE 802.11 (Wi-Fi). |  
| **ISO** (International Organization for Standardization) | Establishes global standards across industries. | OSI Reference Model (ISO/IEC 7498-1). |  

---

### **2. Application Layer Overview**  
- **Function**: Provides interfaces for applications to use network services.  
- **Protocol Design**: Specifies **Transport Layer protocols** (TCP/UDP) and **port numbers** for communication.  
- **Protocol Data Unit (PDU)**: Data.  

#### **Common Protocols & Port Mappings**  
| **Protocol** | **Port** | **Transport Protocol** | **Purpose** |  
|--------------|----------|------------------------|-------------|  
| **HTTP** | 80 | TCP | Web browsing (HTML pages). |  
| **FTP** | 20/21 | TCP | File transfer (download/upload). |  
| **Telnet** | 23 | TCP | Remote device management. |  
| **SMTP** | 25 | TCP | Email transmission. |  
| **TFTP** | 69 | UDP | Simple file transfer (no authentication). |  

---

### **3. Key Application Layer Protocols**  
#### **FTP (File Transfer Protocol)**  
- **Purpose**: Transfer files between client and server (C/S model).  
- **Ports**:  
  - **Port 21**: Control connection (commands).  
  - **Port 20**: Data connection (file transfer).  
- **Use Case**: Uploading/downloading files (e.g., website hosting).  

#### **Telnet**  
- **Purpose**: Remote login to devices (e.g., routers, servers).  
- **Port**: 23 (TCP).  
- **Function**: Commands entered on a local Telnet client execute on the remote server.  
- **Limitation**: Transmits data in plaintext (insecure; replaced by SSH).  

#### **HTTP (HyperText Transfer Protocol)**  
- **Purpose**: Fetch web resources (HTML, images, videos).  
- **Port**: 80 (TCP).  
- **Workflow**:  
  1. Client sends HTTP request (e.g., `GET www.huawei.com`).  
  2. Server returns HTTP response (HTML file).  
- **Evolution**: HTTPS (Port 443) adds encryption via TLS/SSL.  

---

### **4. Relationship Between Layers**  
- **Application Layer Protocols** rely on **Transport Layer** (TCP/UDP) for data delivery.  
  - **TCP**: Used for reliability (e.g., HTTP, FTP).  
  - **UDP**: Used for speed (e.g., TFTP, VoIP).  
- **Standardization Bodies** ensure protocols work seamlessly across vendors (e.g., IEEE Ethernet standards enable Huawei-Cisco compatibility).  

---

**Next Section Preview**:  
We will explore **Transport Layer protocols (TCP/UDP)** in detail, including connection management, flow control, and error recovery mechanisms.