
---

## 3.2.1 Defining VLAN Trunks

- **Purpose of VLAN Trunks**:
    
    - VLAN trunks enable traffic from multiple VLANs to propagate between switches, allowing devices in the same VLAN but on different switches to communicate without needing a router.
        
- **Definition**:
    
    - A **VLAN trunk** is a point-to-point link between two network devices that carries traffic for more than one VLAN.
        
    - It allows VLANs to span across multiple network devices and connects them.
        
- **Trunk Configuration**:
    
    - **IEEE 802.1Q** is used to coordinate trunks on Ethernet interfaces (Fast Ethernet, Gigabit Ethernet, and 10-Gigabit Ethernet).
        
    - By default, a Cisco Catalyst switch supports all VLANs on a trunk port.
        
- **Trunk Role**:
    
    - A trunk does not belong to a single VLAN; it acts as a conduit for multiple VLANs.
        
    - Trunks can be used between switches, routers, or devices with compatible **802.1Q-capable NICs**.
        
- **Example**:
    
    - In the example, links between switches **S1** and **S2**, and **S1** and **S3** transmit traffic for VLANs **10, 20, 30, and 99** (native VLAN).
        
![[Pasted image 20250428192502.png]]
---
---


### Network with VLANs

- **VLAN Configuration**: VLANs are configured on individual switch ports, and devices attached to those ports are unaware of VLANs. Devices have IP addressing, which aligns with the VLAN they belong to.
    
- **Segmentation**: In the scenario, two VLANs are created: Faculty devices on **VLAN 10** and Student devices on **VLAN 20**. Broadcast frames sent by a faculty device (PC1) are forwarded only to ports that support VLAN 10.
    
- **Trunk Ports**: Trunk links between switches (e.g., between S2 and S1, and S1 and S3) carry traffic for multiple VLANs. These trunk links allow VLAN 10 traffic to propagate across switches.
    
- **Traffic Forwarding**: When a broadcast frame from a faculty computer reaches switch S1 (via port F0/1), it is forwarded through port F0/3 to S3. S3 forwards the frame to port F0/11, which connects to PC4 (the faculty computer in VLAN 10). This behavior ensures broadcast traffic stays within the same VLAN.
    
- **Isolation**: Traffic (unicast, multicast, or broadcast) is confined to devices within the same VLAN. Devices in different VLANs do not receive each other’s traffic.
- ![[Pasted image 20250428193432.png]]

### VLAN Identification with a Tag

- **VLAN Tagging**: Ethernet frames do not inherently contain VLAN information, so when frames are transmitted across a trunk, VLAN identification must be added through tagging. This is done using the IEEE 802.1Q standard, which inserts a 4-byte VLAN tag into the Ethernet frame header.
    
- **Tagging Process**:
    
    - When a switch receives a frame on an access port assigned to a VLAN, it adds a VLAN tag and recalculates the Frame Check Sequence (FCS) before sending it out via a trunk port.
        
- **VLAN Tag Field Components**:
    
    1. **Type**: A 2-byte value (0x8100 for Ethernet) indicating the tag protocol ID (TPID).
        
    2. **User Priority**: A 3-bit field for quality of service (QoS) priority.
        
    3. **Canonical Format Identifier (CFI)**: A 1-bit field used for Token Ring frame compatibility.
        
    4. **VLAN ID (VID)**: A 12-bit field that specifies the VLAN ID, allowing for up to 4096 different VLANs.
        
- **Recalculation of FCS**: After the VLAN tag is inserted, the switch recalculates the FCS value and updates it in the frame.

![[Pasted image 20250428193731.png]]


### Summary: Native VLANs and 802.1Q Tagging

- **Native VLAN**: On a trunk link, untagged frames are associated with the native VLAN, which is VLAN 1 by default according to IEEE 802.1Q.
    
- **Tagged Frames on Native VLAN**:
    
    - Normally, control traffic on the native VLAN should remain untagged.
        
    - If a trunk port receives a _tagged_ frame for the native VLAN, it **drops** the frame.
        
    - Non-Cisco devices (e.g., IP phones, servers) might send native VLAN traffic with tags, so correct configuration is critical.
        
- **Untagged Frames on Native VLAN**:
    
    - Untagged frames received on a trunk are forwarded to the native VLAN (e.g., VLAN 99 if configured).
        
    - If no devices are assigned to the native VLAN or no other trunk exists, the untagged frame is **dropped**.
        
    - The Port VLAN ID (PVID) matches the native VLAN ID and controls how untagged traffic is handled.
        
- **Important Note**: Always ensure that devices on a trunk do **not** send tagged frames on the native VLAN unless specifically intended.
    



---

**Voice VLAN Tagging**

- A **separate voice VLAN** is required for VoIP to ensure quality of service (QoS) and security.
    
- A **Cisco IP phone** connects to a switch and can carry both **voice** and **data** VLANs.
    
- The IP phone includes an **integrated 3-port switch**:
    
    - Port 1: to the switch or VoIP device.
        
    - Port 2: internal connection for phone traffic.
        
    - Port 3: connection to a PC.
        ![[Pasted image 20250428194724.png]]
- **Cisco Discovery Protocol (CDP)** informs the phone how to handle tagging:
    
    - Voice VLAN traffic: **tagged** with a Layer 2 CoS value.
        
    - Access VLAN traffic: **may be tagged or untagged**.
        
- Example: PC5 is connected via a Cisco IP phone; **VLAN 150** carries voice, **VLAN 20** carries data.
    

---
```
S1# show interfaces fa0/18 switchport 
Name: Fa0/18
Switchport: Enabled
Administrative Mode: static access
Operational Mode: static access
Administrative Trunking Encapsulation: negotiate
Operational Trunking Encapsulation: native
Negotiation of Trunking: Off
Access Mode VLAN: 20 (student)
Trunking Native Mode VLAN: 1 (default)
Administrative Native VLAN tagging: enabled
Voice VLAN: 150 (voice)
```
 
