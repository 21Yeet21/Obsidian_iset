Below is a command training guide to help you memorize key commands for VLANs, trunks, OSPF, and static routing on Huawei devices (based on VRP). I’ve structured it with commands, their purposes, and examples to reinforce your learning. Practice these in a lab environment (e.g., eNSP) to solidify your memory.

---

### VLAN Commands
**Purpose**: Configure virtual LANs to segment network traffic.

- **Create a VLAN**  
  - Command: `vlan vlan-id`  
  - Example: `vlan 10` (Creates VLAN 10)  
  - Purpose: Defines a new VLAN.

- **Enter VLAN View**  
  - Command: `vlan vlan-id`  
  - Example: `vlan 20` (Enters VLAN 20 configuration mode)  
  - Purpose: Allows configuration of VLAN properties.

- **Assign a Name to VLAN**  
  - Command: `name vlan-name`  
  - Example: `name Sales` (Names VLAN 20 as "Sales")  
  - Purpose: Adds a descriptive name for easier identification.

- **Assign Interface to VLAN (Access Port)**  
  - Command: `port link-type access` + `port default vlan vlan-id`  
  - Example:  
    - `interface GigabitEthernet 0/0/1`  
    - `port link-type access`  
    - `port default vlan 30`  
  - Purpose: Configures the interface as an access port and assigns it to VLAN 30.

- **Display VLAN Configuration**  
  - Command: `display vlan`  
  - Example: `display vlan` (Shows all VLANs and their interfaces)  
  - Purpose: Verifies VLAN settings.

---

### Trunk Commands
**Purpose**: Configure trunk links to carry traffic for multiple VLANs between switches.

- **Set Interface as Trunk**  
  - Command: `port link-type trunk`  
  - Example: `interface GigabitEthernet 0/0/2` + `port link-type trunk`  
  - Purpose: Configures the interface as a trunk port.

- **Allow VLANs on Trunk**  
  - Command: `port trunk allow-pass vlan { vlan-id1 [ to vlan-id2 ] | all }`  
  - Example: `port trunk allow-pass vlan 10 20 30` (Allows VLANs 10, 20, 30)  
  - Purpose: Specifies which VLANs can traverse the trunk.

- **Set Native VLAN (PVID)**  
  - Command: `port trunk pvid vlan vlan-id`  
  - Example: `port trunk pvid vlan 1` (Sets VLAN 1 as the native VLAN)  
  - Purpose: Defines the VLAN for untagged traffic.

- **Display Trunk Configuration**  
  - Command: `display port vlan`  
  - Example: `display port vlan` (Shows VLAN assignments on ports)  
  - Purpose: Verifies trunk and VLAN settings.

---

### OSPF Commands
**Purpose**: Configure Open Shortest Path First (OSPF) for dynamic routing.

- **Enable OSPF Process**  
  - Command: `ospf [ process-id ] router-id router-id`  
  - Example: `ospf 1 router-id 1.1.1.1` (Enables OSPF process 1 with Router ID 1.1.1.1)  
  - Purpose: Starts OSPF and sets the Router ID.

- **Advertise Network**  
  - Command: `network ip-address wildcard-mask area area-id`  
  - Example: `network 192.168.1.0 0.0.0.255 area 0` (Advertises 192.168.1.0/24 into Area 0)  
  - Purpose: Specifies which interfaces participate in OSPF.

- **Set Interface Priority (for DR/BDR Election)**  
  - Command: `ospf dr-priority priority`  
  - Example: `interface GigabitEthernet 0/0/1` + `ospf dr-priority 150`  
  - Purpose: Sets the priority (0-255) to influence DR/BDR election.

- **Configure Passive Interface**  
  - Command: `ospf passive-interface { interface-type interface-number }`  
  - Example: `ospf passive-interface GigabitEthernet 0/0/2`  
  - Purpose: Prevents OSPF Hellos on the specified interface.

- **Display OSPF Neighbors**  
  - Command: `display ospf peer`  
  - Example: `display ospf peer` (Lists OSPF neighbors)  
  - Purpose: Verifies neighbor relationships.

- **Display OSPF Routing Table**  
  - Command: `display ip routing-table protocol ospf`  
  - Example: `display ip routing-table protocol ospf` (Shows OSPF routes)  
  - Purpose: Checks OSPF-learned routes.

---

### Static Routing Commands
**Purpose**: Configure manual routes for predictable traffic flow.

- **Configure a Static Route**  
  - Command: `ip route-static destination-ip-address subnet-mask { next-hop-address | interface-type interface-number } [ preference value ]`  
  - Example: `ip route-static 10.0.0.0 255.255.255.0 192.168.1.2`  
  - Purpose: Adds a static route to 10.0.0.0/24 via next hop 192.168.1.2.

- **Configure a Default Route**  
  - Command: `ip route-static 0.0.0.0 0.0.0.0 next-hop-address`  
  - Example: `ip route-static 0.0.0.0 0.0.0.0 192.168.1.1`  
  - Purpose: Sets a default gateway to 192.168.1.1.

- **Set Route Preference**  
  - Command: `ip route-static destination-ip-address subnet-mask next-hop-address preference value`  
  - Example: `ip route-static 172.16.0.0 255.255.0.0 192.168.1.3 preference 10`  
  - Purpose: Assigns a preference (lower value = higher priority) to the route.

- **Display IP Routing Table**  
  - Command: `display ip routing-table`  
  - Example: `display ip routing-table` (Shows all routes, including static)  
  - Purpose: Verifies configured static routes.

- **Delete a Static Route**  
  - Command: `undo ip route-static destination-ip-address subnet-mask`  
  - Example: `undo ip route-static 10.0.0.0 255.255.255.0`  
  - Purpose: Removes the specified static route.

---

### Memorization Tips
- **Group by Function**: Link commands by their purpose (e.g., creation, assignment, verification).
- **Use Mnemonics**: For OSPF, remember "HDDRLU" (Hello, Database Description, Link State Request, Link State Update, Ack) for packet types.
- **Practice in Context**: Simulate a network in eNSP with a switch, router, and multiple VLANs, then apply these commands step-by-step.
- **Repetition**: Write each command 5 times, then configure it in a lab to reinforce muscle memory.

Try configuring a small topology: a switch with VLAN 10 and 20, a trunk link to a router, OSPF between the router and another router, and a static route to an external network. Use the `display` commands to verify. Let me know if you’d like a quiz or scenario to test these commands!