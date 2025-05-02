This network architecture uses **bridge interfaces** (br) and **VLAN tagging** to segment traffic. Let's break down the components and clarify the naming conventions:

---

### **Bridge Interfaces (br) Explanation**
1. **`br1`**:  
   - This is the primary bridge interface acting as a virtual switch, connecting multiple network segments.
   - Bridges are often used to combine physical/virtual interfaces or VLANs into a single logical network.

2. **`br1.40`**:  
   - A **VLAN-tagged sub-interface** on bridge `br1`, specifically for **VLAN 40** (e.g., VLAN INTEENIET).  
   - The `.40` denotes the VLAN ID (tag), meaning traffic on this sub-interface is segregated for VLAN 40.

3. **`br140`**:  
   - Likely a shorthand notation for `br1.40` (VLAN 40 on bridge `br1`).  
   - Some systems/applications (e.g., pfSense, Linux) may omit the dot for simplicity or due to syntax constraints, resulting in `br140` instead of `br1.40`.  
   - This is common in configurations where VLAN IDs are appended directly to interface names (e.g., `em1.16` becomes `em116` in some contexts).

---

### **Key Observations in Your Architecture**
1. **VLANs and Subnets**:  
   - Each VLAN (Guest, Technicien, Recherche, etc.) has a dedicated subnet and DHCP configuration.  
   - Example:  
     - **VLAN 16** (Guest): `172.18.0.0/18` on `em1.16`  
     - **VLAN 40** (INTEENIET): `172.20.0.0/16` on `em3.40` (static IPs).  

2. **Trunk Ports**:  
   - The **TRUNK** port aggregates multiple VLANs (e.g., VLAN 15, 16, 17, 18) over a single physical link (likely between switches or to the pfSense router).  
   - Trunking uses VLAN tagging (e.g., `bri1.16`, `bri1.17`) to distinguish traffic.

3. **pfSense on Alma Linux**:  
   - The **pfSense firewall** (virtualized or bare-metal) is hosted on Alma Linux.  
   - Physical interfaces (`em0`-`em4`) are assigned to VLANs:  
     - `em0`: WAN (public-facing, DHCP from modem).  
     - `em1`-`em4`: LAN/VLAN interfaces with tagged sub-interfaces (e.g., `em1.16` for VLAN 16).  

4. **Bridging vs. Routing**:  
   - The `br1` bridge connects VLANs locally, while pfSense handles inter-VLAN routing and firewall rules.  

---

### **Why the Mix of Naming Conventions?**
- **`bri1.16` vs. `bri116`**:  
  - **`bri1.16`**: Explicit VLAN tagging (bridge 1, VLAN 16).  
  - **`bri116`**: A shorthand where the VLAN ID is appended without a dot (common in CLI tools or scripts).  
- This inconsistency might stem from:  
  - Different subsystems (e.g., kernel vs. web UI) displaying names differently.  
  - Typos or legacy naming in the diagram.  

---

### **Recommendations**
1. **Standardize Naming**: Use either dots (`br1.40`) or concatenated names (`br140`) consistently to avoid confusion.  
2. **Verify pfSense Configuration**: Ensure VLAN sub-interfaces (e.g., `em1.16`) are properly assigned to bridges or firewall rules.  
3. **Check Trunk Ports**: Confirm that all VLANs (15, 16, 17, 18, 40) are allowed on the trunk link between switches and pfSense.  

This setup efficiently segregates traffic for different user groups (guests, technicians, researchers) while leveraging pfSense for centralized routing and security. Let me know if you need help troubleshooting specific connectivity issues! 😊