

#### **4.1.1 What is Inter-VLAN Routing?**

- VLANs segment Layer 2 networks.
    
- Hosts in different VLANs **cannot communicate** without routing.
    
- **Inter-VLAN Routing** allows traffic between VLANs.
    

#### **Types of Inter-VLAN Routing:**

1. **Legacy Inter-VLAN Routing**
    
    - Uses **multiple physical router interfaces** (one per VLAN).
        
    - **Not scalable.**
        
2. **Router-on-a-Stick**
    
    - Uses **a single router interface with subinterfaces**.
        
    - Suitable for **small to medium networks**.
        
3. **Layer 3 Switch with SVIs (Switched Virtual Interfaces)**
    
    - Layer 3 switch performs routing internally.
        
    - **Most scalable**, best for **medium to large networks**.
        
Here’s the structured version with titles and formatting:

---

#### Legacy Inter-VLAN Routing


Legacy inter-VLAN routing uses **multiple physical interfaces** on a router, each connected to a different VLAN on the switch.

##### **Example Topology Overview:**

- **PC1**
    
    - IP: 192.168.10.10/24
        
    - VLAN 10
        
    - Connected to **S1 Fa0/11**
        
- **PC2**
    
    - IP: 192.168.20.10/24
        
    - VLAN 20
        
    - Connected to **S1 Fa0/24**
        
- **Router R1**
    
    - G0/0/0: 192.168.10.1 → Connected to **S1 Fa0/1 (VLAN 10)**
        
    - G0/0/1: 192.168.20.1 → Connected to **S1 Fa0/12 (VLAN 20)**
        
![[Pasted image 20250502211818.png]]
##### **MAC Address Table of S1:**

|Port|MAC Address|VLAN|
|---|---|---|
|F0/1|R1 G0/0/0 MAC|10|
|F0/11|PC1 MAC|10|
|F0/12|R1 G0/0/1 MAC|20|
|F0/24|PC2 MAC|20|

##### **Packet Flow Example:**

1. **PC1** sends a packet to **PC2**.
    
2. Packet goes to **default gateway**: 192.168.10.1 (R1 G0/0/0).
    
3. Router **R1** receives and routes it to **G0/0/1** (192.168.20.1).
    
4. Frame is forwarded to **S1 Fa0/12 → PC2**.
    

##### **Limitation:**

- Not scalable.
    
- **One router interface per VLAN** is required.
    
- Consumes **too many physical ports** on the router.
    

> ⚠️ **Note:** This method is outdated and not used in modern networks—explained for historical understanding only.


#### **4.1.3 Router-on-a-Stick Inter-VLAN Routing**

This method addresses the limitations of legacy inter-VLAN routing. Instead of requiring multiple physical interfaces, it uses a single physical Ethernet interface on a router to route traffic between several VLANs.

- The router’s interface is configured as an **802.1Q trunk** and connects to a switch trunk port.
    
- Multiple **subinterfaces** are created on the physical interface. Each subinterface:
    
    - Is assigned to a specific VLAN.
        
    - Has its own IP address (serving as the default gateway for the VLAN).
        
    - Is associated with a separate subnet.
        

**Routing Process:**

- When VLAN-tagged traffic arrives at the router:
    
    - It is directed to the matching subinterface.
        
    - The router makes a routing decision based on the destination IP.
        
    - If the destination is in another VLAN, the router forwards the packet via the appropriate subinterface.
        
    - The outgoing frame is tagged with the destination VLAN ID and sent back through the same physical interface.
        

**Example:**

- Subinterfaces on R1:
    
    - `G0/0/0.10` → IP: 172.17.10.1 → VLAN 10
        
    - `G0/0/0.20` → IP: 172.17.20.1 → VLAN 20
        
    - `G0/0/0.30` → IP: 172.17.30.1 → VLAN 30
        
- Switch ports:
    
    - S1: Ports F0/1-F0/3 set as trunk ports
        
    - S2: F0/11 (VLAN 10), F0/18 (VLAN 20), F0/23 (VLAN 30)
        

**Limitations:**

- The router-on-a-stick model does **not scale well beyond ~50 VLANs**.
    
- Performance may be limited due to the router handling all VLAN traffic on a single interface.
    

Thanks for the reminder. Here's the correctly **formatted** version of **4.1.4 Inter-VLAN Routing on a Layer 3 Switch** using your preferred style:

---

### **4.1.4 Inter-VLAN Routing on a Layer 3 Switch**

#### 🔹 Description

- Modern inter-VLAN routing uses **Layer 3 switches** and **Switched Virtual Interfaces (SVIs)**.
    
- An **SVI** is a virtual interface configured for a VLAN, allowing Layer 3 processing of traffic.
    
- A Layer 3 switch (multilayer switch) performs both switching and routing internally.
    

#### 🔹 Functionality

- An **SVI** acts like a router interface for its VLAN.
    
- Routing occurs **within the switch**, avoiding the need for external routers or links.
    
- Example:
    
    - VLAN 10 → `SVI: 10.1.10.1`
        
    - VLAN 20 → `SVI: 10.1.20.1`
        

#### 🔹 Advantages

- ✅ **High Speed**: Routing is done in hardware, not software.
    
- ✅ **No External Router Needed**: Routing is internal.
    
- ✅ **Supports EtherChannel**: Trunk links can be aggregated for more bandwidth.
    
- ✅ **Low Latency**: Frames do not leave the switch for routing.
    
- ✅ **Scalable for Campus LANs**.
    

#### 🔹 Disadvantage

- ❌ **Higher Cost**: Layer 3 switches are more expensive than Layer 2 switches.
    
