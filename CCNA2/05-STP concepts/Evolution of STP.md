Here is a **comparison table** of the different **Spanning Tree Protocol (STP) variants**:

|Protocol|Standard / Vendor|STP Instances|Convergence Speed|VLAN Support|Key Features|
|---|---|---|---|---|---|
|**STP**|IEEE 802.1D|One (CST)|Slow (30-50 sec)|All VLANs share 1 instance|Original version, basic loop prevention|
|**PVST+**|Cisco Proprietary|One per VLAN|Slow|Yes (per VLAN)|Cisco enhancements (PortFast, BPDU Guard), separate topology per VLAN|
|**RSTP**|IEEE 802.1w|One (CST)|Fast (1–2 sec)|All VLANs share 1 instance|Faster convergence, new port roles (Alternate, Backup)|
|**Rapid PVST+**|Cisco Proprietary|One per VLAN|Fast|Yes (per VLAN)|RSTP + VLAN separation + Cisco features|
|**MSTP**|IEEE 802.1s|Up to 64 instances|Fast|VLAN groups|Maps VLANs to STP instances, reduces resource usage|
|**MST (Cisco)**|Cisco Implementation|Up to 16 instances|Fast|VLAN groups|Cisco version of MSTP, supports all Cisco features (PortFast, Root Guard)|


### ✅ **5.3.2 RSTP Concepts**

#### 📌 **Overview of RSTP (IEEE 802.1w)**

- **RSTP** is an enhancement of **802.1D**, offering **faster convergence** and **backward compatibility** with original STP.
    

#### 📌 **Key Benefits of RSTP**

- **Faster Convergence:** Achieves network recovery in **milliseconds**.
    
- **Alternate Ports:** Ports can **transition** to **forwarding state** without waiting for full network convergence.
    

#### 📌 **Cisco's Rapid PVST+**

- **Rapid PVST+** is Cisco's implementation of **RSTP per VLAN**, supporting features like **PortFast**, **BPDU guard**, and **root guard**.


### ✅ **5.3.3 RSTP Port States and Port Roles**

#### 📌 **RSTP vs STP: Port States**

- **STP:** 5 port states: **Disabled**, **Blocking**, **Listening**, **Learning**, **Forwarding**.
    
- **RSTP:** 3 port states: **Discarding**, **Learning**, **Forwarding**.
    
    - The **STP** states **Disabled**, **Blocking**, and **Listening** are merged into **Discarding** in **RSTP**.
        ![[Pasted image 20250504204234.png]]

#### 📌 **RSTP vs STP: Port Roles**

- **STP Port Roles:** **Root Port**, **Designated Port**, **Blocked Port** (Non-Designated Port).
    
- **RSTP Port Roles:** **Root Port**, **Designated Port**, **Alternate Port**, **Backup Port**.
    
    - **Alternate Port** and **Backup Port** handle situations in **STP's Blocked Port** role.
        ![[Pasted image 20250504204253.png]]

#### 📌 **RSTP Alternate and Backup Ports**

- **Alternate Port:** Provides an alternative path to the root bridge.
    
- **Backup Port:** Acts as a backup for a shared medium (e.g., hubs, which are legacy devices).
    ![[Pasted image 20250504204333.png]]
- **Example:**
    
    - **S1 (Root Bridge)**: All ports are **Designated Ports**.
        
    - **S2**: Port to **S1** is a **Root Port**, Port to **S3** is an **Alternate Port**.
        
    - **S3**: Port to **S1** is a **Root Port**, Port to **S2** is a **Designated Port**.
        
    - One of the ports on **S3** connected to a **Hub** is a **Backup Port**.




### ✅ **5.3.4 PortFast and BPDU Guard**

#### ⚡ **PortFast Overview**

- **PortFast** allows a port to transition immediately from blocking to forwarding, bypassing the listening and learning states, preventing a **30-second delay**.
    
- **Use case**: Applied to access ports like **DHCP clients**, enabling immediate network access.
    
- **Important**: Avoid using PortFast on ports connecting to other switches to prevent **spanning tree loops**.
    

#### 🛡️ **BPDU Guard Overview**

- **BPDU Guard** disables ports that receive BPDUs when PortFast is enabled to prevent spanning tree loops.
    
- **Action**: The port enters an **error-disabled** state on receiving any BPDU, requiring manual intervention to restore service.

- ![[Pasted image 20250504204742.png]]


### ✅ **5.3.5 Alternatives to STP**

#### 🔄 **Evolution of Network Design**

- **STP** has been crucial for loop prevention but may not meet the increasing demands of modern LANs, which are larger, more resilient, and require faster convergence.
    
- As Ethernet networks evolved, from simple switch-to-router setups to **hierarchical network designs**, **Layer 3** routing has become more common, offering better redundancy and efficiency than STP.
- 
    ![[Pasted image 20250504205321.png]]

#### 🌐 **Layer 3 Routing for Redundancy**

- **Layer 3 routing** provides redundant paths without needing to block ports, unlike STP.
    
- Modern designs often transition to **Layer 3 everywhere**, except at the access layer where devices connect to switches, providing more flexibility and improved performance.
    ![[Pasted image 20250504205423.png]]
    ![[Pasted image 20250504205504.png]]

#### ⚡ **Alternatives to STP**

- **MLAG (Multi-System Link Aggregation)**: Enables the aggregation of multiple switches to create a more resilient connection.
    
- **SPB (Shortest Path Bridging)**: Ensures optimal path selection, offering better fault tolerance and faster convergence.
    
- **TRILL (Transparent Interconnection of Lots of Links)**: A newer technology designed to improve Ethernet network scalability while maintaining loop prevention.
    

These alternatives provide greater speed, efficiency, and scalability compared to traditional STP in complex, modern networks.