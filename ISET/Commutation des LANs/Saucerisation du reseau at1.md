


le hub ne jamais peut marche en full duplex

Here’s a summary of the **commands used in this TP** along with their purposes. This will help you review and understand when to use each command during network configuration and troubleshooting:

---

### **1. Basic Configuration Commands**
- **`hostname <name>`**  
  - **Purpose**: Sets the hostname of the device (router or switch).  
  - **When to use**: When configuring the device for identification in the network.

- **`enable secret <password>`**  
  - **Purpose**: Sets a secure password for privileged EXEC mode.  
  - **When to use**: To secure access to the device's configuration mode.

- **`interface vlan 1`**  
  - **Purpose**: Enters VLAN 1 configuration mode.  
  - **When to use**: To configure the management VLAN (VLAN 1) on the switch.

- **`ip address <IP> <subnet mask>`**  
  - **Purpose**: Assigns an IP address to an interface or VLAN.  
  - **When to use**: When configuring the IP address for the switch or router interface.

- **`copy running-config startup-config`**  
  - **Purpose**: Saves the current configuration to the startup configuration.  
  - **When to use**: After making changes to the configuration to ensure they persist after a reboot.

---

### **2. Interface Configuration Commands**
- **`interface fastethernet <port>`**  
  - **Purpose**: Enters interface configuration mode for a specific port.  
  - **When to use**: When configuring or troubleshooting a specific port on the switch.

- **`duplex <auto | full | half>`**  
  - **Purpose**: Sets the duplex mode of an interface.  
  - **When to use**: To configure the duplex mode (e.g., full-duplex for switches, half-duplex for hubs).

- **`speed <10 | 100 | auto>`**  
  - **Purpose**: Sets the speed of an interface.  
  - **When to use**: To configure the speed of a port (e.g., 10 Mbps, 100 Mbps, or auto-negotiation).

- **`shutdown` / `no shutdown`**  
  - **Purpose**: Disables or enables an interface.  
  - **When to use**: To troubleshoot or reset an interface.

---

### **3. Verification Commands**
- **`show ip interface brief`**  
  - **Purpose**: Displays a summary of all interfaces, including their IP addresses and status.  
  - **When to use**: To verify the status of interfaces (up/down) and their IP configurations.

- **`show interface <port> status`**  
  - **Purpose**: Displays the status, speed, and duplex settings of a specific interface.  
  - **When to use**: To verify the configuration and status of a specific port.

- **`show mac-address-table`**  
  - **Purpose**: Displays the MAC address table of the switch.  
  - **When to use**: To check which MAC addresses are learned by the switch and on which ports.

- **`show running-config`**  
  - **Purpose**: Displays the current configuration of the device.  
  - **When to use**: To verify the current configuration settings.

---

### **4. Connectivity Testing Commands**
- **`ping <IP>`**  
  - **Purpose**: Tests connectivity between devices.  
  - **When to use**: To verify if a device can reach another device on the network.

- **`ping <IP> -n <number>`**  
  - **Purpose**: Sends a specific number of ICMP echo requests.  
  - **When to use**: To test connectivity with multiple packets (e.g., `ping 192.168.1.1 -n 50`).

---

### **5. MAC Address Table Manipulation**
- **`mac address-table static <MAC> vlan <VLAN> interface <port>`**  
  - **Purpose**: Adds a static MAC address entry to the switch's MAC table.  
  - **When to use**: To bind a specific MAC address to a port for security or stability.

- **`clear mac-address-table dynamic`**  
  - **Purpose**: Clears dynamically learned MAC addresses from the table.  
  - **When to use**: To reset the MAC table and allow new MAC addresses to be learned.

---

### **6. Port Security Commands**
- **`switchport port-security`**  
  - **Purpose**: Enables port security on an interface.  
  - **When to use**: To restrict access to a switch port based on MAC addresses.

- **`switchport port-security maximum <number>`**  
  - **Purpose**: Sets the maximum number of MAC addresses allowed on a port.  
  - **When to use**: To limit the number of devices that can connect to a port.

- **`switchport port-security mac-address <MAC>`**  
  - **Purpose**: Binds a specific MAC address to a port.  
  - **When to use**: To allow only a specific device to connect to a port.

- **`switchport port-security violation <protect | restrict | shutdown>`**  
  - **Purpose**: Defines the action to take when a port security violation occurs.  
  - **When to use**: To configure how the switch responds to unauthorized devices.

---

### **7. Miscellaneous Commands**
- **`exit`**  
  - **Purpose**: Exits the current configuration mode.  
  - **When to use**: To return to the previous mode (e.g., from interface configuration to global configuration).

- **`end`**  
  - **Purpose**: Exits configuration mode and returns to privileged EXEC mode.  
  - **When to use**: After completing configuration tasks.

---

### **Summary of When to Use Each Command**
1. **Initial Setup**: Use `hostname`, `enable secret`, `interface vlan 1`, and `ip address` to configure the device.
2. **Interface Configuration**: Use `interface fastethernet`, `duplex`, `speed`, and `shutdown` to configure ports.
3. **Verification**: Use `show ip interface brief`, `show interface`, `show mac-address-table`, and `show running-config` to verify configurations.
4. **Connectivity Testing**: Use `ping` to test network connectivity.
5. **MAC Table Management**: Use `mac address-table static` and `clear mac-address-table dynamic` to manage MAC addresses.
6. **Port Security**: Use `switchport port-security` and related commands to secure switch ports.
7. **Saving and Exiting**: Use `copy running-config startup-config` to save changes and `exit`/`end` to navigate modes.

---


