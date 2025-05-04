

### **🔁 Redundancy in Layer 2 Networks (5.1.1)**

- Redundancy ensures **network availability** by providing **alternate physical paths**.
    
- But **Layer 2** (Ethernet) networks **can't tolerate loops**.
    
- **Loops** cause broadcast storms, MAC table instability, and frame duplication.
    
- Ethernet has **no built-in loop protection**, so a mechanism like STP is required.
    

---

### **🛑 Spanning Tree Protocol (5.1.2)**

- **STP (Spanning Tree Protocol)** prevents **Layer 2 loops** while allowing **redundant links**.
    
- It creates a **loop-free logical topology** by selectively blocking ports.
    
- Based on **IEEE 802.1D standard** (original version).
    
- Allows **failover**: If the active path fails, a blocked path becomes active.
    
![[Pasted image 20250503193647.png]]


### **🔄 STP Recalculation (5.1.3)**

- **When a failure occurs** on the active path, STP **detects the topology change**.
    
- It begins a **recalculation process** to find a new loop-free path.
    
- A **previously blocked port** may transition to **forwarding state** to restore connectivity.
    
- This process ensures **network continuity** without manual intervention.
    
- However, **recalculation takes time**, depending on the STP version:
    
    - Traditional 802.1D: ~30–50 seconds
        
    - Rapid STP (RSTP): faster convergence
#### Example
        
![[Pasted image 20250503193950.png]]

![[Pasted image 20250503194118.png]]


### **⚠️ Issues with Redundant Switch Links (5.1.4)**

- **Redundant paths** prevent single points of failure but can cause **Layer 2 loops** if STP is not used.
    
- Layer 2 loops lead to:
    
    - ❌ **MAC table instability**
        
    - 🔁 **Broadcast storms (link saturation)**
        
    - 🧠 **High CPU usage** on switches and end devices
        
    - 📉 **Network downtime or unresponsiveness**
        

---

### ❗ Why Layer 2 is Vulnerable

- Layer 2 Ethernet **does not** have a TTL (Time To Live) like Layer 3 (IPv4/IPv6).
    
- Frames can **loop indefinitely** unless STP intervenes.
    
- STP was designed to **block redundant paths logically** to **prevent loops**.

### **🔁 Layer 2 Loops (5.1.5)**

- Without **STP**, **Layer 2 loops** can form quickly and bring down the network within seconds.
    
- A **loop** causes:
    
    - 🔄 **Endless repetition** of broadcast, multicast, and unknown unicast frames
        
    - 📉 **MAC table instability** (constantly updated)
        
    - 🧠 **High CPU usage** on switches
        
    - 🚫 **Switches unable to forward traffic properly**
        

---

### 🔍 Key Example

- **Broadcast Frame (e.g., ARP Request):**
    
    - Sent out all ports except the one it came in on.
        
    - If redundant paths exist, the frame loops endlessly.
        
- **Unknown Unicast Frame:**
    
    - Destination MAC not in table → forwarded out all ports.
        
    - Can result in **duplicate frames** at the destination.
        



![[Pasted image 20250503195644.png]]

### ✅ **5.1.6 Broadcast Storm – Key Points**

- **Definition**:  
    A **broadcast storm** is a flood of broadcast or multicast frames that overwhelms the network.
    
- **Cause**:
    
    - Typically triggered by **Layer 2 loops**.
        
    - Can also be due to **faulty hardware** (e.g., a malfunctioning NIC).
        
- **Impact**:
    
    - **Severe network disruption** within seconds.
        
    - **Switches and end devices** become overwhelmed.
        
    - **High CPU usage** and **MAC table instability**.
        
- **Examples of Affected Traffic**:
    
    - **Layer 2 broadcasts** (e.g., ARP Requests).
        
    - **Multicast traffic** (e.g., **ICMPv6 Neighbor Discovery**), treated like broadcasts.
        
- **Why It's Dangerous**:  
    Ethernet has **no built-in TTL** at Layer 2, so frames loop endlessly unless something like **STP (Spanning Tree Protocol)** stops them.
    

![[Pasted image 20250503195939.png]]



### ✅ **5.1.7 The Spanning Tree Algorithm (STA)** – Summary

#### 📌 **Overview**

- **Invented by**: Radia Perlman (1985 paper)
    
- **Purpose**: Prevent **Layer 2 loops** by creating a **loop-free logical topology**
    
- **Based on**: Selecting a **Root Bridge** and blocking redundant paths
    

---

#### 🌳 **Steps of the Spanning Tree Algorithm**
![[Pasted image 20250503200323.png]]
1. **Select Root Bridge**
    
    - All switches participate in electing the root bridge.
        
    - Usually the switch with the **lowest Bridge ID (priority + MAC)** wins.
        
    - In the scenario: **S1** is chosen as the root bridge.
        ![[Screenshot 2025-05-03 200333 1.png]]
2. **Determine Best Paths**
    
    - Each switch calculates the **least-cost path** to the root bridge (based on link cost).
        
    - **One path per switch** toward the root is selected for forwarding.
        
3. **Block Redundant Paths**
    
    - Ports that would create loops are **blocked** (not forwarding traffic).
        
    - Blocking ensures a **single logical path** between each switch and the root bridge.
        
    - Example: Ports on **S4, S5, and S8** are blocked to prevent loops.
        ![[Screenshot 2025-05-03 200442.png]]
4. **Loop-Free Topology**
    
    - Only **one active path** exists per switch to the root bridge.
        
    - The blocked links still exist **physically** for redundancy but are **disabled logically**.
        ![[Pasted image 20250503200459.png]]
5. **Recalculation on Link Failure**
    
    - If a link fails (e.g., S2 ↔ S4 goes down), STP **recalculates**.
        
    - A **previously blocked port is unblocked** (e.g., S4 ↔ S5 becomes active).
        
    - Still maintains a loop-free and connected topology.
        ![[Pasted image 20250503200520.png]]

---

#### 📘 **Key Terms**

- **Root Bridge**: Central switch all others connect to logically.
    
- **Blocked Port**: Disabled to prevent loops (doesn’t forward data).
    
- **Forwarding Port**: Active, used to send/receive frames.
    
- **STP Recalculation**: Happens when topology changes.
    
