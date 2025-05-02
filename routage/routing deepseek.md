
Got it! Let’s dive **deep** into routing tables, static/dynamic routing, and exam-critical concepts. This summary will be structured for **rote memorization** and **application** in exams.  

---

### **1. Routing Table: The Core of Routing Decisions**  
#### **Components of a Routing Entry**  
Every entry in the routing table includes:  
1. **Destination Network**: IP + Subnet Mask (e.g., `192.168.1.0/24`).  
2. **Next Hop**:  
   - IP address of the next router (e.g., `10.0.0.2`).  
   - **OR** Exit Interface (e.g., `Serial0/0/0`).  
3. **Administrative Distance (AD)**: Trustworthiness of the route source.  
   - **Key AD Values**:  
     - **0**: Directly connected networks.  
     - **1**: Static routes.  
     - **90**: EIGRP.  
     - **110**: OSPF.  
     - **120**: RIP.  
4. **Metric**: Route "cost" (e.g., hop count for RIP, bandwidth for OSPF).  

#### **Hierarchy of Route Selection**  
A router selects routes in this order:  
1. **Longest Prefix Match** (most specific subnet).  
   - Example: `/30` mask is preferred over `/24` for a destination.  
2. **Lowest Administrative Distance** (e.g., static route over RIP).  
3. **Lowest Metric** (if AD is the same).  

---

### **2. Static Routing: Manual Control**  
#### **Types of Static Routes**  
1. **Standard Static Route**:  
   ```bash  
   R1(config)# ip route [Network] [Mask] [Next-Hop/IP]  
   ```  
   Example:  
   ```bash  
   ip route 192.168.2.0 255.255.255.0 10.0.0.2  
   ```  
2. **Default Route**:  
   ```bash  
   ip route 0.0.0.0 0.0.0.0 [Next-Hop/IP]  # IPv4  
   ipv6 route ::/0 [Next-Hop/IPv6]          # IPv6  
   ```  
3. **Floating Static Route**: Backup route with higher AD.  
   ```bash  
   ip route 192.168.3.0 255.255.255.0 10.0.0.3 150  # AD = 150  
   ```  
4. **Summary Route**: Combines multiple subnets into one entry.  
   ```bash  
   ip route 172.16.0.0 255.255.0.0 10.0.0.2  # Summarizes 172.16.0.0/16  
   ```  

#### **Verification Commands**  
- `show ip route static`: Lists all static routes.  
- `show running-config | section ip route`: Shows configured static routes.  

---

### **3. Dynamic Routing: RIPv2 Deep Dive**  
#### **RIPv2 Key Features**  
- **Classless**: Supports VLSM and CIDR (unlike RIPv1).  
- **Metric**: Hop count (max 15 hops; 16 = unreachable).  
- **Updates**: Sent every 30 seconds via multicast (`224.0.0.9`).  

#### **Configuration**  
```bash  
Router(config)# router rip  
Router(config-router)# version 2  
Router(config-router)# network [Network]  # Classful network (e.g., 192.168.1.0)  
```  
Example:  
```bash  
router rip  
 version 2  
 network 192.168.1.0  
 network 10.0.0.0  
```  

#### **Loop Prevention**  
- **Split Horizon**: Don’t advertise routes back to the interface they came from.  
- **Poison Reverse**: Advertise failed routes with a metric of 16.  

#### **Verification**  
- `show ip protocols`: Displays RIP timers, version, and networks.  
- `show ip route rip`: Lists RIP-learned routes.  

---

### **4. Routing Table Lookup: Step-by-Step Process**  
When a packet arrives:  
1. **Check for Directly Connected Networks**:  
   - If the destination IP is on a local subnet, forward directly (ARP if needed).  
2. **Longest Prefix Match**:  
   - Example: For destination `192.168.1.20`, prefer `192.168.1.0/24` over `192.168.0.0/16`.  
3. **Recursive Lookup**:  
   - If the route points to a next-hop IP (not an exit interface), the router performs a **second lookup** to find how to reach the next-hop IP.  

---

### **5. CIDR & Subnetting: Exam Must-Know**  
#### **Example: `192.168.169.169/24`**  
- **Network Address**: `192.168.169.0` (First IP).  
- **Broadcast Address**: `192.168.169.255` (Last IP).  
- **Usable Hosts**: `192.168.169.1` to `192.168.169.254`.  
- **Subnet Mask**: `255.255.255.0` (24 bits).  

#### **Practice All Given CIDR Notations**  
- `/16`: Subnet mask `255.255.0.0`.  
- `/22`: Subnet mask `255.255.252.0`.  
- `/27`: Subnet mask `255.255.255.224`.  

---

### **6. Exam-Style Scenario: Static Routing Configuration**  
**Question**: Configure R2’s static routes so all networks can communicate.  
**Given Topology**:  
```  
R1 (10.5.1.1) ↔ R2 (10.5.2.1/10.5.2.2) ↔ R3 (10.5.3.1/10.5.4.1)  
```  
**Solution for R2**:  
```bash  
R2(config)# ip route 10.5.1.0 255.255.255.0 10.5.2.1    # Route to R1’s LAN  
R2(config)# ip route 10.5.4.0 255.255.255.0 10.5.3.2    # Route to R3’s LAN  
```  

---

### **7. Troubleshooting Routing Tables**  
#### **Common Issues**  
1. **Missing Route**: Check if the static route is configured or if the dynamic protocol is active.  
2. **Incorrect Next Hop**: Verify the next-hop IP is reachable (`ping` test).  
3. **Mismatched Subnet Masks**: Ensure masks match on both ends.  

#### **Key Commands**  
- `ping [IP]`: Test connectivity.  
- `traceroute [IP]`: Identify where packets are dropped.  
- `show ip interface brief`: Check interface status.  

---

### **8. Advanced: How Routers Build Tables**  
1. **Directly Connected Routes**: Added when an interface is assigned an IP and activated.  
2. **Static Routes**: Manually added; no overhead but inflexible.  
3. **Dynamic Routes**:  
   - **RIP**: Exchanges full tables periodically.  
   - **OSPF**: Builds a topology map using Dijkstra’s algorithm.  
   - **EIGRP**: Uses DUAL algorithm for fast convergence.  

---

### **9. Critical Exam Questions**  
**Q1**: Which route is preferred:  
- `192.168.1.0/24` via RIP (AD 120)  
- `192.168.1.0/26` via OSPF (AD 110)  

**Answer**: `192.168.1.0/26` (longer prefix) even though OSPF has lower AD.  

**Q2**: What is the broadcast address for `172.16.64.0/23`?  
**Answer**:  
- Subnet mask: `255.255.254.0`  
- Broadcast: `172.16.65.255`.  

---

### **10. Final Tips**  
- **Memorize AD values** and **route selection order**.  
- **Practice subnetting** until it’s second nature.  
- Use **show commands** to validate configurations in labs.  

This is the **deepest** dive into routing tables and protocols you’ll need for your exam. Let me know if you need even *more* granularity! 🎯