
### **6.3.1 Verify EtherChannel**

To **verify EtherChannel**, use the following commands:

- **`show interfaces port-channel 1`**  
    → Verifies the logical Port-Channel interface status.
![[Pasted image 20250505214417.png]]
- **`show etherchannel summary`**  
    → Shows an overview of all EtherChannels, with flags like:
    
    - `SU`: Layer2, Up and in use
        
    - `SD`: Layer2, Down (error)
        
    - `P`: Port is bundled in EtherChannel
![[Pasted image 20250505214430.png]]
- **`show etherchannel port-channel`**  
    → Gives details about the port-channel’s protocol (LACP/PAgP) and members.
![[Pasted image 20250505214511.png]]

- **`show interfaces f0/1 etherchannel`**  
    → Shows the role and status of a physical interface within an EtherChannel.
    
![[Pasted image 20250505214526.png]]

---

### **6.3.2 Common Issues with EtherChannel**

Common configuration errors:

- Mismatched **VLANs**, **trunk mode**, or **native VLANs**
    
- Inconsistent **speed/duplex**
    
- Misaligned **negotiation modes**:
    
    - _LACP:_ `active` + `passive`
        
    - _PAgP:_ `desirable` + `auto`
        

⚠️ **Do not configure trunk settings on individual physical ports** — configure them on the **Port-Channel**.

---

### **6.3.3 Troubleshoot EtherChannel Example**

**Troubleshooting scenario:** EtherChannel is down between S1 and S2.

#### Step-by-step Fix:

1. **Check current status:**
    
    ```
    S1# show etherchannel summary
    → Output shows Po1(SD) – it's down.
    ```
    
2. **Check config on both switches:**
    
    ```
    show run | begin interface port-channel
    ```
    
    → S1 uses `mode on` (no protocol), S2 uses `desirable` (PAgP) ⇒ **Mismatch**
    
3. **Correct S1’s mode:**
    
    ```bash
    S1(config)# no interface port-channel 1
    S1(config)# interface range fa0/1 - 2
    S1(config-if-range)# channel-group 1 mode desirable
    S1(config)# interface port-channel 1
    S1(config-if)# switchport mode trunk
    ```
    
4. **Verify EtherChannel is active:**
    
    ```
    S1# show etherchannel summary
    → Po1(SU) PAgP      Fa0/1(P) Fa0/2(P)
    ```
    

---

