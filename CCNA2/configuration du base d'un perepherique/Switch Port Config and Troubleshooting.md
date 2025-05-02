
This title covers:  
- **Duplex and Speed Configuration**: Full-duplex vs. half-duplex, manual vs. auto-negotiation.  
- **Auto-MDIX**: Automatic cable type detection for switch-to-switch or switch-to-device connections.  
- **Troubleshooting**: Common issues with duplex and speed mismatches.  

You can save this part of the module under this title for easy reference! 📂🔧  

---

### **Detailed Summary of the Section**  

---

#### **1.2.1 Duplex Communication**  
- **Full-Duplex**:  
  - **Simultaneous two-way communication** (send and receive at the same time).  
  - **No collisions** (microsegmentation ensures each port has its own collision domain).  
  - **Efficiency**: 100% in both directions (doubles bandwidth utilization).  
  - **Example**: Gigabit Ethernet and 10 Gb NICs require full-duplex.  

- **Half-Duplex**:  
  - **One-way communication** (send or receive, but not simultaneously).  
  - **Prone to collisions** (common in older devices like hubs).  
  - **Performance Issues**: Lower efficiency due to collision handling.  

**Key Takeaway**: Always use **full-duplex** for modern networks to maximize performance.  
![[Pasted image 20250225164137.png]]

---

#### **1.2.2 Switch Port Configuration (Physical Layer)**  
- **Manual Configuration**:  
  - Use the following commands in **interface configuration mode**:  
    ```  
    S1(config-if)# duplex full  
    S1(config-if)# speed 100  
    ```  
  - **Best Practice**: Manually set speed and duplex for known devices (e.g., servers, dedicated workstations).  

- **Auto-Negotiation**:  
  - Automatically detects speed and duplex settings.  
  - **Default Setting**: `duplex auto` and `speed auto`.  
  - **Limitations**:  
    - Mismatched settings can cause connectivity issues.  
    - Always verify settings during troubleshooting.  

- **Fiber Optic Ports**:  
  - Operate at predefined speeds and are always **full-duplex**.  

**Key Takeaway**: Use **auto-negotiation** for unknown devices, but manually configure for known devices to avoid mismatches.  

---

#### **1.2.3 Auto-MDIX**  
- **Purpose**: Automatically detects and adjusts for **straight-through** or **crossover** cables.  
- **Command**:  
  ```  
  S1(config-if)# mdix auto  
  ```  
- **Requirements**:  
  - Speed and duplex must be set to `auto` for Auto-MDIX to function correctly.  
- **Verification**:  
  ```  
  S1# show controllers ethernet-controller fa0/1 phy | include MDIX  
  ```  
  - Output: `Auto-MDIX : On` or `Off`.  

**Key Takeaway**: Auto-MDIX simplifies cabling by eliminating the need for specific cable types (straight-through or crossover).  

---

### **Common Commands for Switch Port Configuration**  
| Task                          | Command                                      |  
|-------------------------------|----------------------------------------------|  
| Enter global configuration mode | `S1# configure terminal`                    |  
| Enter interface configuration mode | `S1(config)# interface FastEthernet 0/1`   |  
| Set full-duplex mode           | `S1(config-if)# duplex full`                |  
| Set port speed                 | `S1(config-if)# speed 100`                  |  
| Enable Auto-MDIX              | `S1(config-if)# mdix auto`                  |  
| Save configuration             | `S1# copy running-config startup-config`    |  

---

### **Troubleshooting Tips**  
1. **Duplex/Speed Mismatch**:  
   - Symptoms: High collision rates, slow performance.  
   - Solution: Ensure both ends of the link have matching settings (e.g., both `full-duplex`).  

2. **Auto-Negotiation Failure**:  
   - Symptoms: Link down or unstable connection.  
   - Solution: Manually configure speed and duplex on both ends.  

3. **Auto-MDIX Issues**:  
   - Symptoms: No link or connectivity.  
   - Solution: Verify Auto-MDIX is enabled and speed/duplex are set to `auto`.  

---

### **Key Takeaways**  
- **Full-Duplex**: Always preferred for modern networks.  
- **Manual Configuration**: Best for known devices to avoid mismatches.  
- **Auto-MDIX**: Simplifies cabling by automatically detecting cable types.  
- **Troubleshooting**: Always check duplex, speed, and Auto-MDIX settings for connectivity issues.  



---

### **Detailed Summary of the Section**  

---

#### **1.2.4 Switch Verification Commands**  
The following commands are essential for verifying switch configurations and troubleshooting:  

| **Task**                          | **Command**                                      |  
|-----------------------------------|-------------------------------------------------|  
| Display interface status and configuration | `S1# show interfaces [interface-id]`           |  
| View startup configuration        | `S1# show startup-config`                       |  
| View running configuration        | `S1# show running-config`                       |  
| Display flash file system info    | `S1# show flash`                                |  
| Show system hardware/software info | `S1# show version`                             |  
| View command history              | `S1# show history`                              |  
| Display IP interface info         | `S1# show ip interface [interface-id]`          |  
| Display IPv6 interface info       | `S1# show ipv6 interface [interface-id]`        |  
| View MAC address table            | `S1# show mac-address-table`                    |  

**Key Takeaway**: Use these commands to verify configurations, monitor performance, and troubleshoot issues.  

---

#### **1.2.5 Verifying Switch Port Configuration**  
- **Command**: `show running-config`  
  - Example Output:  
    ```  
    interface FastEthernet0/18  
      switchport access vlan 99  
      switchport mode access  
    interface Vlan99  
      ip address 172.17.99.11 255.255.255.0  
      ipv6 address 2001:DB8:ACAD:99::1/64  
    ip default-gateway 172.17.99.1  
    ```  
  - **Key Info**:  
    - Port assigned to VLAN 99.  
    - Management VLAN (VLAN 99) configured with IPv4 and IPv6 addresses.  
    - Default gateway set for remote management.  

- **Command**: `show interfaces`  
  - Example Output:  
    ```  
    FastEthernet0/18 is up, line protocol is up (connected)  
      Hardware is Fast Ethernet, address is 0025.83e6.9092 (bia 0025.83e6.9092)  
      Full-duplex, 100Mb/s, media type is 10/100BaseTX  
    ```  
  - **Key Info**:  
    - Interface status: `up/up` (operational).  
    - Duplex: Full-duplex.  
    - Speed: 100 Mbps.  

**Key Takeaway**: Use `show running-config` and `show interfaces` to verify port settings and operational status.  



---

#### **Troubleshooting Scenarios**  

| **Interface Status**               | **Possible Issue**                              | **Solution**                                                                 |  
|-----------------------------------|------------------------------------------------|-----------------------------------------------------------------------------|  
| **Interface up, line protocol down** | - Encapsulation mismatch.                     | Verify encapsulation settings (e.g., ARPA, HDLC).                           |  
|                                     | - Remote interface down.                      | Check the status of the remote interface.                                   |  
|                                     | - Hardware issue.                             | Inspect hardware (e.g., cables, NICs) for damage or faults.                 |  
| **Interface down, line protocol down** | - Cable not connected.                       | Ensure the cable is securely connected at both ends.                         |  
|                                     | - Interface administratively shut down.       | Use `no shutdown` command to enable the interface.                          |  
| **Interface administratively down** | - Interface manually disabled.                | Check if the `shutdown` command was applied and use `no shutdown` to enable.|  

**Key Takeaway**: Use `show interfaces` to diagnose **Layer 1 (hardware)** and **Layer 2 (data link)** issues.  

---

#### **1.2.7 Interface Input/Output Errors**  

##### **Input Errors**  
| **Error Type**       | **Description**                                | **Possible Causes**                          | **Solution**                                                                 |  
|----------------------|-----------------------------------------------|---------------------------------------------|-----------------------------------------------------------------------------|  
| **Runts**            | Frames smaller than 64 bytes.                 | - Faulty NIC.                               | Replace the faulty NIC.                                                     |  
|                       |                                               | - Excessive collisions.                     | Check for duplex mismatches or network congestion.                          |  
| **Giants**           | Frames larger than 1518 bytes.                | - Misconfigured MTU.                        | Verify MTU settings on connected devices.                                   |  
| **CRC Errors**       | Checksum mismatch.                            | - Electrical interference.                  | Replace damaged cables and eliminate noise sources.                         |  
|                       |                                               | - Loose or damaged connections.             | Inspect and secure cable connections.                                       |  
| **Ignored**          | Frames ignored due to insufficient buffer space. | - High traffic load.                       | Increase buffer size or reduce traffic load.                                |  

##### **Output Errors**  
| **Error Type**       | **Description**                                | **Possible Causes**                          | **Solution**                                                                 |  
|----------------------|-----------------------------------------------|---------------------------------------------|-----------------------------------------------------------------------------|  
| **Collisions**       | Retransmissions due to Ethernet collisions.   | - Normal in half-duplex mode.               | Switch to full-duplex mode if possible.                                     |  
|                       |                                               | - Should not occur in full-duplex mode.     | Verify duplex settings on both ends of the link.                            |  
| **Late Collisions**  | Collisions after 512 bits transmitted.        | - Excessive cable length.                   | Ensure cable length is within Ethernet standards (100m for UTP).            |  
|                       |                                               | - Duplex mismatch.                          | Configure the same duplex settings on both ends (e.g., both full-duplex).   |  

---

### **Key Takeaways**  
- **Troubleshooting Scenarios**:  
  - Use `show interfaces` to identify Layer 1 and Layer 2 issues.  
  - Common issues include encapsulation mismatches, disconnected cables, and administratively shut down interfaces.  

- **Interface Errors**:  
  - **Input Errors**: Runts, giants, CRC errors, and ignored frames indicate issues like faulty NICs, damaged cables, or high traffic loads.  
  - **Output Errors**: Collisions and late collisions are often caused by duplex mismatches or excessive cable lengths.  

Let me know if you need further refinements or additional details! 🔧🔍

**Key Takeaway**:  
- High CRC errors: Check cables for damage or interference.  
- Late collisions: Verify duplex settings and cable length.  

---

### **Common Interface Error Scenarios**  
1. **Runts**:  
   - Cause: Faulty NIC or excessive collisions.  
   - Solution: Replace NIC or check for duplex mismatches.  

2. **Giants**:  
   - Cause: Oversized frames (e.g., misconfigured MTU).  
   - Solution: Verify MTU settings on connected devices.  

3. **CRC Errors**:  
   - Cause: Electrical interference, damaged cables, or loose connections.  
   - Solution: Replace cables and eliminate noise sources.  

4. **Late Collisions**:  
   - Cause: Duplex mismatch or excessive cable length.  
   - Solution: Ensure both ends of the link use the same duplex settings.  

---

### **Key Takeaways**  
- **Verification Commands**: Use `show running-config`, `show interfaces`, and `show mac-address-table` to monitor and troubleshoot.  
- **Interface Errors**: Identify and resolve issues like runts, giants, CRC errors, and late collisions.  
- **Troubleshooting**: Always check Layer 1 (hardware) and Layer 2 (data link) status for connectivity issues.  

Let me know if you need further clarification or additional sections! 🔧🔍


---

#### **1.2.8 Troubleshooting Network Access Layer Issues**  
Most problems in a switched network occur during initial implementation. However, issues like damaged cables, configuration changes, or new device connections can arise over time, requiring ongoing maintenance and troubleshooting.  

---

#### **General Troubleshooting Process**  
Follow these steps to diagnose and resolve connectivity issues between a switch and another device:  

1. **Run `show interfaces`**:  
   - Check the interface status (up/down) and error counters (e.g., runts, giants, CRC errors).  

2. **Is the Interface Up?**  
   - **No**:  
     - **Check Cables**:  
       - Ensure the correct cable type is used (e.g., straight-through or crossover).  
       - Inspect cables and connectors for damage. Replace if necessary.  
     - **Check Speed Settings**:  
       - Verify that speed is configured correctly on both ends.  
       - If auto-negotiation fails, manually set the same speed on both devices.  

   - **Yes**:  
     - **Check for Noise/EMI**:  
       - Look for signs of excessive noise (e.g., high runts, giants, or CRC errors).  
       - Remove sources of electromagnetic interference (EMI) if possible.  
       - Ensure cables do not exceed maximum length and are of the correct type.  
     - **Check Duplex Settings**:  
       - Verify that duplex settings match on both ends (e.g., both full-duplex).  
       - If auto-negotiation fails, manually set full-duplex on both devices.  

3. **Is the Problem Resolved?**  
   - **Yes**: The issue is fixed.  
   - **No**: Document the steps taken and escalate the problem.  
   - ![[Pasted image 20250225170833.png]]

---

#### **Key Troubleshooting Scenarios**  

| **Scenario**                        | **Possible Cause**                          | **Solution**                                                                 |  
|-------------------------------------|---------------------------------------------|-----------------------------------------------------------------------------|  
| **Interface Down**                  | - Incorrect or damaged cable.               | Replace the cable and ensure proper connections.                            |  
|                                     | - Speed mismatch.                           | Manually set the same speed on both ends.                                   |  
| **Interface Up, Connectivity Issues** | - Excessive noise (EMI).                   | Remove noise sources and check cable length/type.                           |  
|                                     | - Duplex mismatch.                          | Manually set full-duplex on both ends.                                      |  
|                                     | - Collisions or late collisions.            | Verify duplex settings and ensure no duplex mismatch.                       |  

---

#### **Common Errors and Their Causes**  

| **Error Type**       | **Description**                                | **Possible Causes**                          | **Solution**                                                                 |  
|----------------------|-----------------------------------------------|---------------------------------------------|-----------------------------------------------------------------------------|  
| **Runts**            | Frames smaller than 64 bytes.                 | - Faulty NIC or excessive collisions.       | Replace NIC or check for duplex mismatches.                                 |  
| **Giants**           | Frames larger than 1518 bytes.                | - Misconfigured MTU.                        | Verify MTU settings on connected devices.                                   |  
| **CRC Errors**       | Checksum mismatch.                            | - Electrical interference or damaged cables. | Replace cables and eliminate noise sources.                                 |  
| **Collisions**       | Retransmissions due to Ethernet collisions.   | - Normal in half-duplex mode.               | Switch to full-duplex mode if possible.                                     |  
| **Late Collisions**  | Collisions after 512 bits transmitted.        | - Excessive cable length or duplex mismatch. | Ensure proper cable length and matching duplex settings.                    |  

---

#### **Key Commands for Troubleshooting**  
- **`show interfaces`**:  
  - Displays interface status, speed, duplex, and error counters.  
  - Example:  
    ```  
    FastEthernet0/18 is up, line protocol is up (connected)  
      Hardware is Fast Ethernet, address is 0025.83e6.9092 (bia 0025.83e6.9092)  
      Full-duplex, 100Mb/s, media type is 10/100BaseTX  
    ```  

- **`show running-config`**:  
  - Verifies interface configuration (e.g., speed, duplex, VLAN assignment).  

---

### **Key Takeaways**  
- **Troubleshooting Steps**:  
  - Start with `show interfaces` to check interface status and errors.  
  - Verify cables, speed, and duplex settings if the interface is down.  
  - Check for noise, collisions, and duplex mismatches if the interface is up but connectivity issues persist.  

- **Common Issues**:  
  - **Cable Problems**: Damaged or incorrect cables.  
  - **Speed/Duplex Mismatch**: Auto-negotiation failures.  
  - **Noise/EMI**: Causes CRC errors and frame corruption.  

- **Documentation**: Always document troubleshooting steps and escalate unresolved issues.  

Let me know if you need further refinements or additional details! 🔧🔍