
### ✅ **5.2.1 STP Operations: Steps to a Loop-Free Topology**

#### 📌 **4 Main Steps of STA (Spanning Tree Algorithm)**

1. **Elect the Root Bridge**
    
    - All switches send **BPDUs** containing their **Bridge ID (BID)**.
        
    - The **lowest BID** wins.
        
    - **BID = Bridge Priority + Extended System ID + MAC address**
        
    - Default Bridge Priority: **32768**
        
    - Lower BID → more likely to be root.
        
2. **Elect the Root Ports (RP)**
    
    - Each **non-root switch** selects **one port** with the **lowest cost path** to the root bridge.
        
    - This port becomes the **Root Port**.
        
    - One **Root Port per switch** (except the root bridge, which has none).
        
3. **Elect Designated Ports (DP)**
    
    - For **each segment**, one switch is elected to **forward traffic toward the root bridge**.
        
    - The port used on this switch is the **Designated Port**.
        
    - **One Designated Port per segment**.
        
4. **Elect Alternate (Blocked) Ports**
    
    - All other ports that could create loops are **set to blocking state**.
        
    - These are **Alternate Ports** (previously known as **non-designated**).
        
    - Still listen to BPDUs, ready to take over if topology changes.
        

---

#### 🧾 **Bridge ID (BID) Structure**

|Component|Length|Description|
|---|---|---|
|**Bridge Priority**|4 bits|Default = 32768. Lower is better.|
|**Extended System ID**|12 bits|Usually the **VLAN ID** (added to priority).|
|**MAC Address**|48 bits|Used as tie-breaker if priority and extended ID are equal.|

- **Final BID value = Bridge Priority + Extended System ID + MAC Address**
    
- Example: If two switches have same priority and VLAN, **lower MAC wins**.
    ![[Pasted image 20250504192910.png]]
---


---

### 🧠 **How is a 16-bit Bridge Priority split?**

The **Bridge ID (BID)** is made of:

- **Bridge Priority** → 16 bits
    
- **Extended System ID (VLAN ID)** → 12 bits
    
- **MAC Address** → 48 bits
    

But:

> ⚠️ Only the **upper 4 bits** of the 16-bit Bridge Priority field are actually used to set the **admin-defined priority**.

---

### 🔍 **So what happens?**

- Priority can be configured in **steps of 4096**  
    (Because 2¹² = 4096 → the lower 12 bits are used for VLAN ID, not admin-settable)
    
- Example:  
    If you set `priority = 32768`, the actual 16-bit priority field becomes:  
    `priority (4 bits) = 8`, `VLAN ID (12 bits) = 0` → 32768 = 8 × 4096
    

---

### 📏 **Allowed values for priority** (multiples of 4096):

```
0, 4096, 8192, ..., 61440
```

➡️ So although the **admin-settable portion is 4 bits** (values from 0 to 15),  
the **full 16-bit field = (4-bit priority × 4096) + VLAN ID**

---

### 🔧 Example on Cisco:

```bash
Switch(config)# spanning-tree vlan 1 priority 4096
```

Would you like a binary breakdown of the Bridge ID structure?
#### 📨 **BPDU (Bridge Protocol Data Unit)**

- Sent every **2 seconds** by default.
    
- Contains BID and **path cost** to root.
    
- Used for:
    
    - Electing the root bridge
        
    - Determining port roles
        
    - Detecting topology changes
        

### ✅ **5.2.2 Step 1: Elect the Root Bridge**

#### 📌 **Root Bridge Election Process**

- **All switches** initially believe they are the **root bridge**.
    
- They start sending **BPDUs every 2 seconds** with:
    
    - Their own **Bridge ID (BID)**
        
    - Their own **Root ID** (initially same as BID)
        
- Switches **compare BPDUs**:
    
    - If a received Root ID is **lower** than its own, it updates its Root ID and forwards the better BPDU.
        
    - This process continues until all switches **agree on the switch with the lowest BID** as the **root bridge**.
        

---

#### 🧾 **What Is BID?**

- **BID = Priority + Extended System ID + MAC address**
    
- **Lower = better**
    
- If two BIDs have:
    
    - Same priority → compare MAC address (lower wins)
        

---

#### 🧪 **In the Provided Topology**

|Switch|Priority|MAC Address|BID (Lower is better)|
|---|---|---|---|
|S1|24577|000A.0033.3333|✅ **Lowest BID** → **Root Bridge**|
|S2|32769|000A.0011.1111|Higher|
|S3|32769|000A.0022.2222|Higher|
![[Pasted image 20250504193122.png]]
➡️ **S1 becomes Root Bridge** because it has the **lowest priority** and thus the **lowest BID**.

### ✅ **5.2.3 Impact of Default BIDs**

#### 📌 **Default Behavior**

- **Default Bridge Priority** = `32768`
    
- When VLANs are used, **Extended System ID (VLAN ID)** is added  
    ➜ Example: VLAN 1 → `32768 + 1 = 32769`
    
- So, all switches have **priority = 32769** unless manually changed.
    

---

#### ⚠️ **Problem**: If all switches have the **same priority**, the **MAC address** becomes the tie-breaker.

#### 🧾 **MAC Address Rule**:

- Lower MAC address (in hexadecimal) wins
    
- So, the switch with the **lowest MAC** is elected as the **root bridge**
    

---

#### 🧪 **In the Provided Topology**

|Switch|Priority|MAC Address|BID (Lower is better)|
|---|---|---|---|
|S1|32769|000A.0033.3333|High|
|S2|32769|000A.0011.1111|✅ **Lowest BID → Root Bridge**|
|S3|32769|000A.0022.2222|Higher|

➡️ **S2 becomes Root Bridge** because it has the **lowest MAC address**.

---

#### ✅ **Best Practice**:

To control STP topology:

- **Manually lower the priority** of the preferred root bridge
    
- Example: Set `priority 4096` on the intended root switch
    ![[Pasted image 20250504193929.png]]

---

### 🧠 **Key Concept: Internal Root Path Cost**

- The **internal root path cost** is the **sum of all port costs** from a non-root switch to the root bridge.
    
- Each switch adds the **cost of the port** where it received the BPDU to the **root path cost in that BPDU**.
    
- The result helps determine the **shortest path to the root bridge**.
    

---

### 🔁 **Path Cost Calculation Process**:

1. The root bridge sends BPDUs with a **root path cost of 0**.
    
2. When another switch receives this BPDU:
    
    - It adds the **cost of the incoming port**.
        
    - Updates its internal path cost if the new cost is lower than the previous one.
        

---

### 🧮 **Default Port Cost Table (Short Path Cost – IEEE 802.1D)**
| Port Speed    | STP Cost (802.1D - Short) | RSTP Cost (802.1w - Long) |
| ------------- | ------------------------- | ------------------------- |
| 10 Mbps       | 100                       | 2,000,000                 |
| 100 Mbps      | 19                        | 200,000                   |
| 1 Gbps (1000) | 4                         | 20,000                    |
| 10 Gbps       | 2                         | 2,000                     |
| 100 Gbps      | N/A                       | 200                       |
| 1 Tbps        | N/A                       | 20                        |
- STP uses **shorter cost values** and works well up to 10 Gbps.
    
- RSTP uses **larger values** (long path cost) to support faster speeds (≥10 Gbps).

> 🔧 You can **manually set** the port cost to influence STP behavior.

---

### ⚙️ **Cisco Configuration Example:**

```bash
Switch(config)# interface fa0/1
Switch(config-if)# spanning-tree cost 200
```


### ✅  5.2.5: Elect the Root Ports

- Once the **Root Bridge** is elected, each **non-root switch** selects **one Root Port**.
    
- The **Root Port** is the port with the **lowest total cost** path to the Root Bridge (sum of port costs along the path).
    
- **Redundant paths** with higher costs are **blocked**.
    
- Port cost is based on **port speed** (e.g., FastEthernet = 19).
    
- In the example:
    
    - **S2** selects **F0/1** as its Root Port (cost = 19), being the shortest path to **S1**.
        
    - **S3** also selects **F0/1** as its Root Port (direct link to S1).
        ![[Pasted image 20250504194907.png]]
        

📌 Each switch has **only one Root Port**, except the Root Bridge which has none.

### ✅  5.2.6: Elect Designated Ports

After **Root Ports** are selected, the Spanning Tree Algorithm (STA) elects **Designated Ports** to complete loop prevention.

#### 🔹 Designated Port Rules:

- **Each network segment** (link between two switches) must have **one Designated Port**.
    
- The Designated Port is the port with the **lowest path cost to the Root Bridge** on that segment.
    
- If path costs are equal, the **lowest Bridge ID** (BID) wins.
    
- **Ports that are not Root Ports or Designated Ports become blocked** to prevent loops.
    

---

#### 🔸 Key Cases:

1. **On the Root Bridge**:
    
    - **All ports** are automatically **Designated Ports** (cost to root = 0).
        ![[Pasted image 20250504195440.png]]
2. **If One End is a Root Port**:
    
    - The **other end** of the segment is a **Designated Port**.
        
    - Example: If S4's Fa0/1 is a Root Port (toward S1), then S3's Fa0/3 is the Designated Port.
    - ![[Pasted image 20250504195527.png]]
        
3. **Between Two Non-Root Switches**:
    
    - The switch with the **lower cost to Root Bridge** gets the Designated Port.
        
    - If costs tie, **lower Bridge ID** decides.
        
    - Example: Between S2 and S3, both have same cost → S2 wins due to lower BID → S2’s F0/2 becomes Designated.
    - 
        ![[Pasted image 20250504195607.png]]
        

---

#### 📌 Extra Notes:

- **Ports connected to end devices** (e.g., PCs) are always **Designated Ports**.
    
- **Designated Ports are always in a forwarding state**.
    


### 📌 Elect Alternate (Blocked) Ports

If a port is neither a **Root Port** nor a **Designated Port**, it becomes an **Alternate (Blocked) Port**, which prevents loops in the network.

---

#### ✅ 5.2.7: Elect Alternate (Blocked) Ports

When the **Spanning Tree Algorithm (STA)** finishes selecting **Root Ports** and **Designated Ports**, it elects **Alternate Ports** to maintain network stability by blocking traffic on paths that would cause loops.

#### 🔹 Alternate Port Rules:

- **Alternate Ports** are **not used for forwarding** traffic.
    
- They are placed in the **Blocking state**, meaning they **do not forward Ethernet frames**.
    
- These ports act as **backup paths** if the active path fails.
    
- **Ports not serving as Root or Designated Ports become Alternate Ports**.
    

---

#### 🔸 Key Scenarios:

1. **If a port is neither a Root Port nor a Designated Port**:
    
    - It **becomes an Alternate Port** and is placed in the **Blocking state**.
        
2. **Example in Network Topology**:
    
    - In the figure, **F0/2 on S3** is an **Alternate Port** because it is neither a **Root Port** nor a **Designated Port**.
        
    - This port will **not forward traffic** but is available as a **backup** if needed.
        ![[Pasted image 20250504200437.png]]
        

---

#### 📍 Visual Representation:

- **Blocked Ports**, like **F0/2 on S3**, show a **red blocking symbol**, indicating they are inactive for traffic forwarding.



---

### 📌 **Root Port Election with Equal-Cost Paths**

When a switch has **two or more equal-cost paths** to the **Root Bridge**, STP uses the following tie-breaker rules to elect a **Root Port**:

---

### ✅ 1. **Lowest Sender Bridge ID (BID)**

- The switch chooses the port connected to the **neighbor switch with the lowest BID**.
    
- 🧠 **Example**:
    
    - S2 is connected to **S3 (BID: 32769.5555.5555.5555)** and **S4 (BID: 32769.1111.1111.1111)**.
        
    - Both links have equal cost to the Root Bridge (S1).
        
    - Since **S4 has the lower BID**, S2 chooses the **port connected to S4** as its **Root Port**.
        ![[Pasted image 20250504200751.png]]
        

---

### ✅ 2. **Lowest Sender Port Priority**

- If the **BID is the same** (e.g. both links are to the same switch), STP compares the **port priority** of the sender (default = 128).
    
- Lower port priority wins.
    
- 🧠 **Example**:
    
    - S4 is connected to **S1** via **two ports (F0/1 and F0/2)**.
        
    - Both have **equal cost** and **same port priority (128)**.
        
    - If one port had a lower priority, the port on S4 connected to it would become the **Root Port**.
        ![[Pasted image 20250504200929.png]]
        

---

### ✅ 3. **Lowest Sender Port ID**

- If the **port priorities are also equal**, STP uses the **lowest port ID** (interface number) on the sender switch.
    
- Lower port ID wins.
    
- 🧠 **Example**:
    
    - S1 is sending BPDUs on **F0/1** and **F0/2**.
        
    - S4 receives them on **F0/6** and **F0/5**.
        
    - Since **F0/1 < F0/2**, S4 chooses the **link to F0/1** (via F0/6) as **Root Port**.
        
    - The other becomes **Alternate (Blocked)**.
        ![[Pasted image 20250504201140.png]]
        


---

### ⏱️ **STP Timers**

STP uses **three key timers** to manage convergence and prevent loops:

- **🟢 Hello Timer**
    
    - Interval between BPDU transmissions
        
    - **Default:** 2 seconds
        
    - **Range:** 1 – 10 seconds
        
- **🟡 Forward Delay Timer**
    
    - Time spent in **Listening** and **Learning** states
        
    - **Default:** 15 seconds
        
    - **Range:** 4 – 30 seconds
        
- **🔴 Max Age Timer**
    
    - Time a switch waits without BPDU before topology change
        
    - **Default:** 20 seconds
        
    - **Range:** 6 – 40 seconds
        

🔔 _Timers are set by the **Root Bridge** and propagated to the rest of the network._

📌 _IEEE recommends a **maximum of 7 switches** in STP diameter when using default timers._

---

### 🔁 **STP Port States**

STP transitions ports through a **series of states** to safely determine topology:

|**State**|**Purpose**|
|---|---|
|🔒 **Blocking**|Prevents loops. Listens for BPDUs only. No frame forwarding.|
|🗣️ **Listening**|Receives/sends BPDUs. Determines active path. No MAC learning or data forwarding.|
|📘 **Learning**|Learns MAC addresses. Prepares to forward traffic, but still doesn’t send frames.|
|🚀 **Forwarding**|Fully active. Forwards user traffic and participates in STP.|
|❌ **Disabled**|Administrative state. Not part of STP or data forwarding.|

---

🧠 _Transitions follow this order:_

- **Link Up → Blocking → Listening → Learning → Forwarding**
    ![[Pasted image 20250504201921.png]]

Each of **Listening** and **Learning** lasts for **15 seconds by default**, governed by the **Forward Delay** timer.

---
### 🧩 **Operational Details of Each STP Port State**

|**Port State**|**BPDU**|**MAC Address Table**|**Forwarding Data Frames**|
|---|---|---|---|
|🔒 **Blocking**|Receive only|❌ No update|❌ No|
|🗣️ **Listening**|Receive and send|❌ No update|❌ No|
|📘 **Learning**|Receive and send|✅ Updating table|❌ No|
|🚀 **Forwarding**|Receive and send|✅ Updating table|✅ Yes|
|❌ **Disabled**|None sent/received|❌ No update|❌ No|

### 🌐 **Per-VLAN Spanning Tree (PVST)**

- PVST runs **a separate STP instance for each VLAN**.
    
- A **unique root bridge** is elected per VLAN.
    
- This enables **different logical topologies** per VLAN.
    
- If all ports are in **VLAN 1**, only **one STP instance** runs.
    
- Used for **load balancing** across VLANs by selecting different root bridges.
    
