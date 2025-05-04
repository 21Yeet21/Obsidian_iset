
### **4.3 Inter-VLAN Routing using Layer 3 Switches**

#### 🧠 Key Concepts

- **Router-on-a-stick** is not scalable for large networks.
    
- **Layer 3 switches** offer hardware-based routing for high performance.
    
- **Inter-VLAN routing** is done via **SVIs (Switched Virtual Interfaces)**.
    

---

#### ✅ Capabilities of a Layer 3 Switch

- Can route between VLANs using **SVIs**.
    
- Can convert a Layer 2 port into a **routed port** (Layer 3 port).
    

---

#### 🖥️ 4.3.2 Scenario Overview

- Switch **D1** acts as the Layer 3 switch.
    
- **PC1** is in **VLAN 10** (`192.168.10.10/24`)
    
- **PC2** is in **VLAN 20** (`192.168.20.10/24`)
    
- Inter-VLAN communication
- ![[Screenshot 2025-05-03 at 14-39-55 Cisco Networking Academy.png]]n is enabled through D1.
    

---

#### 🛠️ 4.3.3 Configuration Steps

1. **Create VLANs**
    

```lua
D1(config)# vlan 10
D1(config-vlan)# name LAN10
D1(config-vlan)# vlan 20
D1(config-vlan)# name LAN20
```

2. **Configure SVIs**
    

```lua
D1(config)# interface vlan 10
D1(config-if)# description Default Gateway SVI for 192.168.10.0/24
D1(config-if)# ip address 192.168.10.1 255.255.255.0
D1(config-if)# no shutdown

D1(config)# interface vlan 20
D1(config-if)# description Default Gateway SVI for 192.168.20.0/24
D1(config-if)# ip address 192.168.20.1 255.255.255.0
D1(config-if)# no shutdown
```

3. **Assign Access Ports**
    

```lua
D1(config)# interface g1/0/6
D1(config-if)# description Access port to PC1
D1(config-if)# switchport mode access
D1(config-if)# switchport access vlan 10

D1(config)# interface g1/0/18
D1(config-if)# description Access port to PC2
D1(config-if)# switchport mode access
D1(config-if)# switchport access vlan 20
```

4. **Enable IPv4 Routing**
    

```lua
D1(config)# ip routing
```

---

#### ✅ Result

- **PC1 and PC2** can now communicate across VLANs via Layer 3 switch.
    
- No need for external router or trunk port setup.
    

### **4.3.4 Layer 3 Switch Inter-VLAN Routing Verification**

- Inter-VLAN routing using a **Layer 3 switch** is easier to configure than the **router-on-a-stick** method.
    
- Once configuration is complete, verify connectivity between hosts using the `ping` command.
    
- Example IP configuration on **PC1**:
    
    ```
    IPv4 Address       : 192.168.10.10  
    Subnet Mask        : 255.255.255.0  
    Default Gateway    : 192.168.10.1
    ```
    
- Then use:
    
    ```
    ping 192.168.20.10
    ```
    
    → Successful replies confirm inter-VLAN routing is working.
    

---

### **4.3.5 Routing on a Layer 3 Switch**

- If VLANs need to communicate with **other Layer 3 devices** (like routers), their networks must be shared via **static or dynamic routing**.
    
- In that case, you need to create a **routed port** instead of an SVI.
    

#### ✔️ How to create a routed port:

- Use the command `no switchport` on a Layer 2 interface to convert it to **Layer 3 mode**.
    
- Then configure an IP address:
    
    ```bash
    D1(config)# interface gig1/0/1
    D1(config-if)# no switchport
    D1(config-if)# ip address 10.1.1.1 255.255.255.0
    D1(config-if)# no shutdown
    ```
    


### **4.3.6 Routing Scenario on a Layer 3 Switch**

- In this scenario, the **Layer 3 switch (D1)** is connected to a **router (R1)**.
    
- Both D1 and R1 are configured to use **OSPF (Open Shortest Path First)** for dynamic routing.
    
- **D1** already performs **inter-VLAN routing** between VLAN 10 and VLAN 20.
    
- Now D1 must also communicate with **external networks** via **R1** using OSPF.
    

---
![[Pasted image 20250503151228.png]]
### **Topology Overview:**

|Device|Interface|IP Address|Notes|
|---|---|---|---|
|**PC1**|–|`192.168.10.10/24`|VLAN 10, gateway: `192.168.10.1`|
|**PC2**|–|`192.168.20.10/24`|VLAN 20, gateway: `192.168.20.1`|
|**D1 (L3 Switch)**|`G0/0/1`|`10.10.10.2/24`|Connects to R1|
|**R1 (Router)**|`G0/0/1`|`10.10.10.1/24`|Connects to D1|
||`G0/0/0`|`10.10.20.1/24`|Connects to server|
|**Server**|–|`10.10.20.254/24`|Gateway: `10.10.20.1`|

---

### **Routing Purpose:**

- **R1** advertises:
    
    - `10.10.10.0/24`
        
    - `10.10.20.0/24`
        
- **D1** uses OSPF to learn about external networks beyond its local VLANs.
    
- **Result**: PC1 and PC2 can access the **server** through R1 using **OSPF routing**.
    

### **🔧 Steps to Configure Routing on D1 (L3 Switch)**

#### **Step 1: Configure the Routed Port**

- Convert `G0/0/1` into a **Layer 3 port** and assign it an IP:
    

```shell
interface GigabitEthernet0/0/1
 description routed Port Link to R1
 no switchport
 ip address 10.10.10.2 255.255.255.0
 no shut
```

#### **Step 2: Enable IP Routing**

```shell
ip routing
```

#### **Step 3: Configure OSPF Routing**

- Advertise VLAN and routed network subnets:
    

```shell
router ospf 10
 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
 network 10.10.10.0 0.0.0.3 area 0
```

Great catch. The reason it's written like this:

```
network 10.10.10.0 0.0.0.3 area 0
```

...is because the wildcard mask `0.0.0.3` targets **a very specific /30 subnet** (i.e. 4 IPs).

---

### 🔹 Why `0.0.0.3`?

Because `0.0.0.3` matches **exactly 4 IP addresses** — which corresponds to a **/30 subnet**.

- `/30` = subnet mask `255.255.255.252`
    
- IP range: `10.10.10.0 – 10.10.10.3`
    
- This is typically used for **point-to-point links** between two devices (like a router and L3 switch).
    

So:

```bash
network 10.10.10.0 0.0.0.3 area 0
```

➡️ Includes only that small link between the router and switch in OSPF.

#### **Step 4: Verify Routing Table**

Use:

```shell
show ip route
```

- You'll see connected (`C`), local (`L`), and OSPF learned (`O`) routes.
    
- Example:
    

```
O 10.10.20.0/24 [110/2] via 10.10.10.1
```

#### **Step 5: Verify PC-to-Server Connectivity**

- From **PC1 and PC2**, ping the server at `10.20.20.254`.
    
- Replies confirm successful end-to-end routing through D1 and R1.
    
