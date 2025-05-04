
Here's a **structured, detailed summary** of your CCNA 2 content on switch boot sequences, `boot system` commands, and LED indicators. Key terms are **bolded**, and explanations are added for clarity:

---

### **1.1.1 Switch Boot Sequence**  
When a Cisco switch powers on, it follows a **5-step boot process**:  
1. **POST (Power-On Self-Test)**:  
   - Stored in **ROM**, checks hardware components (CPU, DRAM, flash memory).  
2. **Boot Loader Execution**:  
   - A small program in **ROM** runs after POST completes.  
3. **Low-Level CPU Initialization**:  
   - Boot loader sets up CPU registers for memory mapping and speed.  
4. **Flash File System Initialization**:  
   - Prepares the switch’s **flash storage** for accessing IOS images.  
5. **IOS Image Loading**:  
   - Boot loader locates and loads the **IOS image** into memory, transferring control to the IOS.  

---

### **1.1.2 `boot system` Command**  
- **Purpose**: Manually specify the IOS image file to load during startup.  
- **Syntax**:  
  ```  
  boot system flash:/<directory>/<IOS_filename.bin>  
  ```  
  Example:  
  ```  
  S1(config)# boot system flash:/c2960-lanbasek9-mz.150-2.SE/c2960-lanbasek9-mz.150-2.SE.bin  
  ```  

#### **Command Breakdown**  
| Command Component       | Description                                                                 |  
|-------------------------|-----------------------------------------------------------------------------|  
| `boot system`           | Primary command to set the IOS boot path.                                   |  
| `flash:`                | Refers to the **flash storage device** where the IOS is stored.             |  
| `c2960-lanbasek9-mz.150-2.SE/` | Directory path in flash containing the IOS image.                          |  
| `.bin` file             | The actual IOS executable file (e.g., `c2960-lanbasek9-mz.150-2.SE.bin`).  |  

- **Key Notes**:  
  - The switch uses the **BOOT environment variable** to locate the IOS.  
  - If BOOT is unset, it loads the first executable file found in flash.  
  - Use `show boot` to verify the current IOS boot file.  

---

### **1.1.3 Switch LED Indicators**  
Cisco Catalyst switches use **LEDs** to indicate status and performance. Below are common LEDs for a Catalyst 2960:  

#### **System LEDs**  
1. **SYST (System)**:  
   - **Off**: No power.  
   - **Green**: Normal operation.  
   - **Amber**: Power present but system malfunction.  

2. **RPS (Redundant Power Supply)**:  
   - **Green**: RPS connected and ready.  
   - **Flashing Green**: RPS in use by another device.  
   - **Amber**: RPS in standby or faulty.  

#### **Port Status LEDs**  
- **STAT (Status Mode)**:  
  - **Off**: No link or port administratively shut down.  
  - **Green**: Link active.  
  - **Flashing Green**: Port transmitting/receiving data.  
  - **Amber**: Port blocked (e.g., to prevent loops).  

#### **Port Configuration LEDs**  
- **DPLX (Duplex Mode)**:  
  - **Off**: Half-duplex.  
  - **Green**: Full-duplex.  

- **SPEED**:  
  - **Green (Solid)**: 100 Mbps.  
  - **Green (Flashing)**: 10 Mbps (slow flash) or 1000 Mbps (rapid flash).  

- **PoE (Power over Ethernet)**:  
  - **Green**: PoE active.  
  - **Alternating Green/Amber**: Power denied (exceeds switch capacity).  
  - **Flashing Amber**: PoE disabled due to fault.  

---

### **Key Takeaways**  
- **Boot Process**: POST → Boot Loader → IOS load.  
- **`boot system`**: Critical for specifying IOS paths; use `show boot` for verification.  
- **LEDs**: Quickly diagnose switch health, port status, and PoE issues.  

### **1.1.4 System Recovery from Failure**  
When a switch’s IOS is corrupted or missing, use the **boot loader** to recover:  

#### **Boot Loader Access Steps**:  
1. **Connect via Console**: Use a console cable and terminal emulator (e.g., PuTTY).  
2. **Power Cycle**: Unplug and replug the switch.  
3. **Enter Boot Loader**:  
   - Within 15 seconds of powering on, press and hold the **Mode** button until the **SYST LED** blinks amber → solid green.  
4. **Boot Loader Prompt**: The `switch:` prompt appears.  

#### **Key Boot Loader Commands**:  
| Command             | Purpose                                                                 |  
|---------------------|-------------------------------------------------------------------------|  
| `help` or `?`       | Lists all available boot loader commands.                              |  
| `flash_init`        | Initializes the **flash file system** (required before accessing files).|  
| `dir flash:`        | Lists directories and files in flash storage.                          |  
| `set`               | Displays the current **BOOT environment variable** (e.g., `BOOT=flash:/...`).|  
| `BOOT=<path>`       | Sets a new IOS path (e.g., `BOOT=flash:c2960-lanbasek9-mz.150-2.SE8.bin`).|  
| `boot`              | Loads the IOS image specified in the BOOT variable.                    |  

**Example Recovery Workflow**:  
```  
switch: flash_init  
switch: dir flash:  
switch: set  
switch: BOOT=flash:c2960-lanbasek9-mz.150-2.SE8.bin  
switch: boot  
```  

**Key Uses of Boot Loader**:  
- Recover from IOS corruption.  
- Reset forgotten passwords.  
- Reinstall IOS.  

---

### **1.1.5 Switch Management Access**  
To manage a switch remotely:  
1. **Configure an SVI (Switch Virtual Interface)**:  
   - Assign an **IP address** and **subnet mask** to the SVI (default: VLAN 1).  
   - **Best Practice**: Use a non-default VLAN (e.g., VLAN 99) for security.  
2. **Set a Default Gateway**:  
   - Required for remote management across subnets.  
   - Example: `ip default-gateway 192.168.1.1` (IPv4).  

#### **Why SVI?**  
- SVI is a **virtual interface** (not a physical port) for switch management.  
- VLANs must be created and assigned to ports for the SVI to become active.  

---

### **1.1.6 Switch SVI Configuration Example**  
#### **Step 1: Configure Management VLAN and SVI**  
```  
Switch(config)# vlan 99  
Switch(config-vlan)# name MGMT  
Switch(config)# interface vlan 99  
Switch(config-if)# ip address 192.168.99.2 255.255.255.0  
Switch(config-if)# ipv6 address 2001:db8:acad:99::2/64  
Switch(config-if)# no shutdown  
```  
**Notes**:  
- The SVI will show `up/up` only if:  
  - VLAN 99 exists.  
  - At least one port is assigned to VLAN 99 and connected.  
- For IPv6: Enable dual-stack mode first:  
  ```  
  Switch(config)# sdm prefer dual-ipv4-and-ipv6 default  
  Switch(config)# reload  
  ```  

#### **Step 2: Set Default Gateway (IPv4 Only)**  
```  
Switch(config)# ip default-gateway 192.168.99.1  
```  

#### **Step 3: Verify Configuration**  
```  
Switch# show ip interface brief  
Switch# show ipv6 interface brief  
```  
**Output Notes**:  
- IPs on SVIs are **only for management**—switches do not route Layer 3 traffic by default.  

---

### **Key Takeaways**  
- **Boot Loader**: Critical for IOS recovery, password resets, and file system repairs.  
- **SVI Management**: Use a dedicated VLAN for security; always configure a default gateway for remote access.  
- **Verification**: Use `show ip interface brief` to confirm SVI status.  

Need more details? Let me know! 🔧🔍