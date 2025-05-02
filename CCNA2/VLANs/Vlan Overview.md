
---

## 3.1.1 VLAN Definitions

- **Virtual LAN (VLAN)**:  
    A logical network segment that provides segmentation and organizational flexibility in a switched network.
    
- **VLAN operation**:  
    Devices within a VLAN communicate as if they were on the same physical network, regardless of their actual location or switch.
    
- **VLAN segmentation**:
    
    - VLANs enable network segmentation based on factors like function, team, or application.
        
    - Devices in a VLAN act like they're in their own independent network.
        
- **Forwarding packets**:
    
    - Unicast, broadcast, and multicast packets are only forwarded to devices within the same VLAN.
        
    - Devices outside the VLAN need routing to receive packets.
        
- **Broadcast domain**:  
    VLANs create separate logical broadcast domains, which helps reduce large broadcast domains and improves network performance.
    
- **Layer 2 broadcast**:  
    Without VLANs, devices in the same Layer 2 broadcast domain receive all broadcasts, even those not intended for them.
    
- **VLANs and security**:  
    VLANs allow administrators to implement access and security policies based on user groupings.
    
- **VLAN ports**:  
    Each switch port can only belong to one VLAN, except for ports connected to IP phones or other switches.
    

---


## 3.1.2 Benefits of a VLAN Design

- **VLAN Design Considerations**:
    
    - Each VLAN corresponds to an IP network.
        
    - Requires hierarchical network addressing, applying IP addresses to network segments or VLANs.
        
    - Devices within a specific area use blocks of contiguous network addresses.
        
- **Benefits of VLAN Design**:
    

| Benefit                                        | Description                                                                                                         |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **Smaller broadcast domains**                  | Dividing the network into VLANs reduces the number of devices in each broadcast domain.                             |
| **Improved security**                          | Only users within the same VLAN can communicate directly, and a router can enforce security policies between VLANs. |
| **Improved IT efficiency**                     | VLANs simplify management by grouping similar users, and VLAN names make identification easier.                     |
| **Reduced cost**                               | VLANs maximize existing bandwidth and reduce the need for expensive network upgrades.                               |
| **Better performance**                         | Smaller broadcast domains reduce unnecessary traffic, improving network performance.                                |
| **Simpler project and application management** | VLANs help manage users and devices based on business or geographic needs, like supporting specific applications.   |

---
---

## 3.1.3 Types of VLANs

### **Default VLAN**

- **VLAN 1** is the default on Cisco switches.
    
    - **Key facts**:
        
        - All ports are assigned to VLAN 1 by default.
            
        - Native VLAN and management VLAN are both set to VLAN 1 by default.
            
        - **VLAN 1** cannot be renamed or deleted.
            
    - **Security risk**: Having the native VLAN as the same as the management VLAN can be a potential security risk.
        

**Example from the `show vlan brief` command**:

```
VLAN Name              Status   Ports
---- ----------------- -------  --------------------
1    default           active   Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                ...
1002 fddi-default      act/unsup
1003 token-ring-default act/unsup
1004 fddinet-default   act/unsup
1005 trnet-default     act/unsup
```

---

### **Data VLAN**

- **Purpose**: Separate user-generated traffic.
    
    - Called **user VLANs** because they group users or devices based on organizational requirements.
        
    - **Note**: Voice and management traffic should be kept separate from data VLANs.
        

---

### **Native VLAN**

- **Role**: Handles untagged traffic across trunk links.
    
    - **Tagged traffic**: VLAN IDs are added to the Ethernet frame.
        
    - **Untagged traffic**: Placed on the **native VLAN**.
        
    - By default, **VLAN 1** is the native VLAN, but it’s recommended to use an unused VLAN to improve security.
        

---

### **Management VLAN**

- **Purpose**: Dedicated to network management traffic (SSH, Telnet, HTTPS, HTTP, SNMP).
    
    - By default, **VLAN 1** is used as the management VLAN on Layer 2 switches.
        

---
