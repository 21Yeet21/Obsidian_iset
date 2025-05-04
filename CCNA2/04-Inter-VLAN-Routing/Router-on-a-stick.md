
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


### **4.2.4 R1 Subinterface Configuration (Router-on-a-Stick)**

#### 🔹 Objectif

Configurer des **sous-interfaces** sur R1 pour permettre le routage inter-VLAN à travers le lien trunk connecté au switch **S1**.

---

#### 🧩 Étape 1 : Créer les sous-interfaces pour chaque VLAN

```lua
R1(config)# interface G0/0/1.10
R1(config-subif)# description Default Gateway for VLAN 10
R1(config-subif)# encapsulation dot1Q 10
R1(config-subif)# ip address 192.168.10.1 255.255.255.0
R1(config-subif)# exit

R1(config)# interface G0/0/1.20
R1(config-subif)# description Default Gateway for VLAN 20
R1(config-subif)# encapsulation dot1Q 20
R1(config-subif)# ip address 192.168.20.1 255.255.255.0
R1(config-subif)# exit

R1(config)# interface G0/0/1.99
R1(config-subif)# description Default Gateway for VLAN 99
R1(config-subif)# encapsulation dot1Q 99
R1(config-subif)# ip address 192.168.99.1 255.255.255.0
R1(config-subif)# exit
```

---

#### 🧩 Étape 2 : Activer l’interface physique trunk

```lua
R1(config)# interface G0/0/1
R1(config-if)# description Trunk link to S1
R1(config-if)# no shutdown
R1(config-if)# end
```

---



### **4.2.5 Vérification de la connectivité entre PC1 et PC2**

#### 🖥️ Étape 1 : Vérifier la configuration IP de PC1

```lua
C:\Users\PC1> ipconfig

Windows IP Configuration
Ethernet adapter Ethernet0:
  IPv4 Address      : 192.168.10.10
  Subnet Mask       : 255.255.255.0
  Default Gateway   : 192.168.10.1
```

🔍 **Vérifie que PC1 est bien dans VLAN 10 et utilise la bonne passerelle.**

---

#### 📡 Étape 2 : Ping vers PC2 (VLAN 20)

```lua
C:\Users\PC1> ping 192.168.20.10

Pinging 192.168.20.10 with 32 bytes of data:
Reply from 192.168.20.10: bytes=32 time<1ms TTL=127
Reply from 192.168.20.10: bytes=32 time<1ms TTL=127
Reply from 192.168.20.10: bytes=32 time<1ms TTL=127
Reply from 192.168.20.10: bytes=32 time<1ms TTL=127

Ping statistics for 192.168.20.10:
    Sent = 4, Received = 4, Lost = 0 (0% loss)
```

✅ **Succès : Le routage inter-VLAN fonctionne bien via le router-on-a-stick.**

---

#### 🖧 Étape 3 : Ping vers le switch S1 (IP de gestion)

```lua
C:\Users\PC1> ping 192.168.99.2

Pinging 192.168.99.2 with 32 bytes of data:
Request timed out.
Request timed out.
Reply from 192.168.99.2: bytes=32 time=2ms TTL=254
Reply from 192.168.99.2: bytes=32 time=1ms TTL=254

Ping statistics for 192.168.99.2:
    Sent = 4, Received = 2, Lost = 2 (50% loss)
```

⚠️ **Résultat mitigé :** connectivité partielle avec l’interface de gestion du switch. Cela peut être dû à un pare-feu local ou à une configuration d'accès management VLAN sur le switch.

### **4.2.6 Vérification du Routage Inter-VLAN avec Router-on-a-Stick**

#### ✅ Commande 1 : Vérifier la table de routage

```bash
R1# show ip route | begin Gateway
```

**Résultat attendu :**

- Routes connectées (C) pour chaque VLAN (10, 20, 99).
    
- Interfaces de sortie : `G0/0/1.x`.
    

```text
C  192.168.10.0/24 is directly connected, G0/0/1.10
C  192.168.20.0/24 is directly connected, G0/0/1.20
C  192.168.99.0/24 is directly connected, G0/0/1.99
```

---

#### ✅ Commande 2 : Vérifier les IPs des sous-interfaces et leur état

```bash
R1# show ip interface brief | include up
```

**Résultat attendu :**

- Chaque sous-interface (`.10`, `.20`, `.99`) est **up/up** avec la bonne adresse IP.
    

```text
Gi0/0/1.10  192.168.10.1  up  up
Gi0/0/1.20  192.168.20.1  up  up
Gi0/0/1.99  192.168.99.1  up  up
```

---

#### ✅ Commande 3 : Vérifier les détails d'une sous-interface

```bash
R1# show interfaces g0/0/1.10
```

**Points clés à valider :**

- Encapsulation : `802.1Q`
    
- VLAN ID correct : `Vlan ID 10`
    
- Adresse IP correcte
    
- Interface **up/up**
    

---

#### ✅ Commande 4 : Vérifier l’état des trunks sur le switch

```bash
S1# show interfaces trunk
```

**Résultat attendu :**

- Ports trunk actifs (`Fa0/1`, `Fa0/5`)
    
- VLANs autorisés : `1,10,20,99`
    
- VLANs en état "forwarding"
    

```text
Port      Vlans allowed on trunk     : 1-4094
Port      Vlans active               : 1,10,20,99
Port      Vlans forwarding           : 1,10,20,99
```

---

### 🔧 Remarque importante :

Même si le VLAN 1 n’est pas configuré manuellement, il est **inclus par défaut** pour le trafic de contrôle (CDP, STP, etc.).

