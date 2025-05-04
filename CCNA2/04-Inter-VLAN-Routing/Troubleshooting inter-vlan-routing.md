
### 🔹 Common Inter-VLAN Issues and Fixes

|**Issue**|**Explanation**|
|---|---|
|**Missing VLANs**|If the VLAN is not created or deleted, devices in that VLAN won’t communicate.|
|**Trunk Port Misconfig**|Trunk ports must carry the correct VLANs; wrong mode or native VLAN = no traffic.|
|**Access Port Misconfig**|If a PC is in VLAN 10 but the port is in VLAN 1, inter-VLAN routing won’t work.|
|**Wrong IP/Subnet on Host**|If the PC has wrong gateway or wrong subnet, it can’t reach other VLANs.|
|**Router-on-a-Stick Issues**|Subinterfaces on the router must match VLAN IDs and have correct IPs.|

---

### 🔍 Example Commands to Use

- `show vlan brief` → See which VLANs exist
    
- `show interfaces trunk` → See trunk port status and allowed VLANs
    
- `show interfaces switchport` → See port mode (access/trunk)
    
- `show ip interface brief` → See router interface/subinterface status and IP
    
- `show running-config` → Check overall config
    

### 🔧 **Troubleshooting Inter-VLAN Routing Scenario**

#### 📌 Topology Summary:



![[Pasted image 20250503154735.png]]

- **PC1**:
    
    - IP: `192.168.10.10/24`, VLAN 10, Gateway: `192.168.10.1`, connected to **S1 F0/6**
        
- **PC2**:
    
    - IP: `192.168.20.10/24`, VLAN 20, Gateway: `192.168.20.1`, connected to **S2 F0/18**
        
- **Switch S1 ↔ Switch S2**: Trunk link on **F0/1**
    
- **Switch S1 ↔ Router R1**: Trunk link on **F0/5 ↔ G0/0/1**
    
- **Router R1**: Has subinterfaces for VLAN 10 and 20
    
- **Switch Management IPs**:
    
    - S1: `192.168.99.2`
        
    - S2: `192.168.99.3`
        

---

### ⚠️ Issue Example: **Missing VLAN**

- VLAN 10 **was deleted** using:
    
    ```bash
    S1(config)# no vlan 10
    ```
    
- Result:
    
    - **Fa0/6 becomes inactive**, still tied to VLAN 10.
        
    - PC1 can’t communicate.
        

---

### 🔍 Troubleshooting Steps:

1. **Verify VLAN status**:
    
    ```bash
    show vlan brief
    ```
    
2. **Check specific port VLAN**:
    
    ```bash
    show interface fa0/6 switchport
    ```
    
    - Shows **Access Mode VLAN: 10 (Inactive)**
        
3. **Recreate VLAN 10**:
    
    ```bash
    vlan 10
    exit
    ```
    
    - Then verify again:
        
        ```bash
        show vlan brief
        ```
        
4. **Result**:
    
    - **VLAN 10 is restored**, and Fa0/6 becomes **active** again in VLAN 10.
        



✅ **Problem Summary and Solution:**

### **Identified Issue:**

- The **Fa0/5** port between **Switch S1** and **Router R1** is configured as a **trunk**, but it was **shutdown**, preventing inter-VLAN routing through the router-on-a-stick.
    

### **Symptom:**

- **PC1** can no longer communicate with **PC2** (other VLANs) after routine maintenance.
    
- The command `show interfaces trunk` does not show **Fa0/5** as an active trunk port.
    

### **Diagnosis:**

- The command `show running-config | include interface fa0/5` reveals that the port is configured as **trunk**, but it is in a **shutdown** state.
    

### **Solution Implemented:**

- Reactivated the port using the `no shutdown` command:
    

```bash
S1(config)# interface fa0/5
S1(config-if)# no shutdown
```

### **Result after Correction:**

- The command `show interfaces trunk` now shows **Fa0/5** as an active **trunk** port with the allowed VLANs (1, 10, 20, 99).
    
- Inter-VLAN routing is restored.
    

---



### **Problem Summary and Solution:**

### **Identified Issue:**

- **PC1**, which is supposed to be connected to **VLAN 10**, is unable to ping its **default gateway** (192.168.10.1).
    
- After verifying the port configuration on **Switch S1**, it was discovered that the **Fa0/6** port was not assigned to **VLAN 10**.
    

### **Symptom:**

- **PC1** has the correct **IPv4 address** and **default gateway**, but it cannot reach the gateway.
    

### **Diagnosis:**

- The `show interfaces fa0/6 switchport` command revealed that the port is in **access mode**, but the **Access Mode VLAN** is set to **VLAN 1**, not **VLAN 10**.
    
- The `show running-config interface fa0/6` command confirmed that the port was not explicitly configured to be part of **VLAN 10**.
    

### **Solution Implemented:**

1. Assign **Fa0/6** to **VLAN 10** using the following commands:
    
    ```bash
    S1(config)# interface fa0/6
    S1(config-if)# switchport access vlan 10
    ```
    
2. Verify the port assignment using the `show interface fa0/6 switchport` command:
    
    ```bash
    S1# show interface fa0/6 switchport
    Name: Fa0/6
    Switchport: Enabled
    Administrative Mode: static access
    Operational Mode: static access
    Access Mode VLAN: 10 (VLAN0010)
    ```
    

### **Result after Correction:**

- **PC1** can now successfully communicate with hosts on **VLAN 10** and the default gateway.
    

---





### **Problem Summary and Solution:**

### **Identified Issue:**

- **Users in VLAN 10** are unable to reach other VLANs, even though the **router (R1)** should be providing inter-VLAN routing for **VLANs 10, 20, and 99**.
    
- The issue is related to the **subinterface configuration** on the router, specifically the incorrect assignment of **VLAN IDs** to subinterfaces.
    

### **Diagnosis:**

- The **subinterfaces** on the router for **VLANs 10, 20, and 99** are operational, as confirmed by the `show ip interface brief` command.
    
- However, the **subinterface Gi0/0/1.10** was assigned to **VLAN 100** instead of **VLAN 10**. This misconfiguration was identified using the `show interfaces | include Gig|802.1Q` command.
    

### **Detailed Steps to Identify the Problem:**

1. **Initial Check**: Run `show ip interface brief` to check the status of the router interfaces and subinterfaces.
    
    ```bash
    R1# show ip interface brief
    Interface              IP-Address      OK? Method Status                Protocol
    GigabitEthernet0/0/1.10 192.168.10.1    YES manual up                    up
    GigabitEthernet0/0/1.20 192.168.20.1    YES manual up                    up
    GigabitEthernet0/0/1.99 192.168.99.1    YES manual up                    up
    ```
    
2. **VLAN Misassignment**: The `show interfaces | include Gig|802.1Q` command revealed that **Gi0/0/1.10** is assigned to **VLAN 100**, not **VLAN 10**.
    
    ```bash
    R1# show interfaces | include Gig|802.1Q
    GigabitEthernet0/0/1.10 is up, line protocol is up
      Encapsulation 802.1Q Virtual LAN, Vlan ID  100.
    ```
    
3. **Misconfiguration in Subinterface**: Check the subinterface configuration to confirm the wrong VLAN ID.
    
    ```bash
    R1# show running-config interface g0/0/1.10
    interface GigabitEthernet0/0/1.10
    description Default Gateway for VLAN 10
    encapsulation dot1Q 100
    ip address 192.168.10.1 255.255.255.0
    ```
    

### **Solution:**

- The **encapsulation dot1Q 100** configuration on **Gi0/0/1.10** was changed to **encapsulation dot1Q 10** to correctly assign it to **VLAN 10**.
    
    ```bash
    R1(config)# interface gigabitEthernet 0/0/1.10
    R1(config-subif)# encapsulation dot1Q 10
    R1(config-subif)# end
    ```
    

### **Verification:**

- After applying the correct configuration, verify the subinterface VLAN assignments again.
    
    ```bash
    R1# show interfaces | include Gig|802.1Q
    GigabitEthernet0/0/1.10 is up, line protocol is up
      Encapsulation 802.1Q Virtual LAN, Vlan ID  10.
    ```
    

### **Result after Correction:**

- Once the **subinterface** was assigned to the correct VLAN, inter-VLAN routing started functioning properly, and devices in **VLAN 10** were able to communicate with devices in other VLANs.
    

---

### **Key Takeaways:**

- **Subinterface misconfiguration**, especially with incorrect **VLAN IDs**, is a common issue in **Router-on-a-Stick** setups.
    
- Verification using commands like `show ip interface brief`, `show interfaces`, and filtering output with the `|` symbol is essential to troubleshoot efficiently.
    

---

