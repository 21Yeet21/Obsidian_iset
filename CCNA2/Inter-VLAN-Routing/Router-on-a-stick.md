
### **4.2.1 Router-on-a-Stick Scenario**

#### 🔹 Topology Overview

- Inter-VLAN routing is achieved using **one physical router interface** divided into **multiple subinterfaces**.
    
- The router is connected via a trunk link to the switch — this is the "stick" in **router-on-a-stick**.
    
![[Pasted image 20250502213146.png]]
#### 🔹 Physical Connections

- **PC1** → `192.168.10.10/24` (VLAN 10), connected to **S1 F0/6**
    
- **PC2** → `192.168.20.10/24` (VLAN 20), connected to **S2 F0/18**
    
- **Switch S1** trunk link:
    
    - `F0/1` (to S2 F0/1)
        
    - `F0/5` (to R1 G0/0/1)
        
- **S1 Mgmt IP** → `192.168.99.2/24`
    
- **S2 Mgmt IP** → `192.168.99.3/24`
    

#### 🔹 Router Subinterfaces (on R1 G0/0/1)

|Subinterface|VLAN|IP Address|
|---|---|---|
|G0/0/1.10|10|192.168.10.1/24|
|G0/0/1.20|20|192.168.20.1/24|
|G0/0/1.99|99|192.168.99.1/24|

#### 🔹 Scenario Summary

- PCs are in **different VLANs**, so **cannot communicate** without routing.
    
- S1 and S2 can ping each other (same VLAN for management), but are **unreachable** by PCs.
    
- Solution: Configure VLANs and trunking on switches, and subinterfaces on R1 for routing.


### **4.2.2 S1 VLAN and Trunking Configuration**

#### 🔹 Objectif

Configurer le switch **S1** avec les VLANs, l'interface de gestion, les ports d'accès et les ports en mode trunk.

---

#### 🧩 Étape 1 : Créer et nommer les VLANs

```lua
S1(config)# vlan 10
S1(config-vlan)# name LAN10
S1(config-vlan)# exit

S1(config)# vlan 20
S1(config-vlan)# name LAN20
S1(config-vlan)# exit

S1(config)# vlan 99
S1(config-vlan)# name Management
S1(config-vlan)# exit
```

---

#### 🧩 Étape 2 : Configurer l'interface de gestion (VLAN 99)

```lua
S1(config)# interface vlan 99
S1(config-if)# ip address 192.168.99.2 255.255.255.0
S1(config-if)# no shutdown
S1(config-if)# exit

S1(config)# ip default-gateway 192.168.99.1
```

---

#### 🧩 Étape 3 : Configurer le port d’accès pour PC1 (F0/6)

```lua
S1(config)# interface fa0/6
S1(config-if)# switchport mode access
S1(config-if)# switchport access vlan 10
S1(config-if)# no shutdown
S1(config-if)# exit
```

---

#### 🧩 Étape 4 : Configurer les ports trunk (vers S2 et R1)

```lua
S1(config)# interface fa0/1
S1(config-if)# switchport mode trunk
S1(config-if)# no shutdown
S1(config-if)# exit

S1(config)# interface fa0/5
S1(config-if)# switchport mode trunk
S1(config-if)# no shutdown
S1(config-if)# end
```


#### Same for S2

