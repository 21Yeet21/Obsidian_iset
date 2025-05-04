### Trunk Configuration Commands

- A trunk link allows multiple VLANs to be carried over a single physical link between switches.
    
- Trunk mode must be manually configured with interface-level commands.
    
- Setting a native VLAN different from VLAN 1 is a best practice for security.
    
- You can manually restrict which VLANs are allowed on the trunk using the `allowed vlan` option.

|**Task**|**IOS Command**|
|---|---|
|Enter global configuration mode.|`Switch# configure terminal`|
|Enter interface configuration mode.|`Switch(config)# interface interface-id`|
|Set the port to permanent trunking mode.|`Switch(config-if)# switchport mode trunk`|
|Set the native VLAN to something other than VLAN 1.|`Switch(config-if)# switchport trunk native vlan vlan-id`|
|Specify the list of VLANs to be allowed on the trunk link.|`Switch(config-if)# switchport trunk allowed vlan vlan-list`|
|Return to the privileged EXEC mode.|`Switch(config-if)# end`|
###  Verify Trunk Configuration

To verify trunk configuration, use the `show interfaces interface-id switchport` command. This displays detailed interface settings including:

```
S1# show interfaces fa0/1 switchportName: Fa0/1
```

- **Administrative/Operational Mode**: Confirms the port is set to trunk.
- **Encapsulation Type**: Shows `dot1q`, the standard for VLAN tagging.
- **Native VLAN**: Verifies which VLAN is used for untagged traffic (e.g., VLAN 99).
- **Trunking VLANs Enabled**: Lists VLANs allowed over the trunk (e.g., 10, 20, 30, 99).

#### Additional Command:
- `show interfaces trunk`: Summarizes all trunk links and their allowed VLANs.


### Reset the Trunk to the Default State

To **reset trunk settings** on a switch port (e.g., Fa0/1) to their default:

#### 🔧 Reset Commands:

```bash
Switch(config)# interface fa0/1
Switch(config-if)# no switchport trunk allowed vlan
Switch(config-if)# no switchport trunk native vlan
Switch(config-if)# end
```

- **Effect**:
    
    - All VLANs are allowed again
        
    - Native VLAN is reset to VLAN 1
        

#### 🔁 Convert Trunk Port to Access Mode:

```bash
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode access
Switch(config-if)# end
```

- **Effect**: Port no longer acts as a trunk; now belongs to one access VLAN.
    

#### ✅ Verification:

Use:

```bash
Switch# show interfaces fa0/1 switchport
```

- **Trunk reset output**: Shows trunk mode with VLAN 1 as native, all VLANs allowed
    
- **Access mode output**: Shows static access mode with VLAN 1 assigned
    


### 3.5.1 Introduction to DTP (Dynamic Trunking Protocol)

#### 🔹 What is DTP?

- **DTP (Dynamic Trunking Protocol)** is a **Cisco proprietary Layer 2 protocol**.
    
- Used to **automatically negotiate trunking** between Cisco switches.
    
- Operates **point-to-point only**.
    
- Default mode on many Cisco switches like **Catalyst 2960/3650** is `dynamic auto`.
    

#### 🔹 Trunking Modes Summary

|**Mode**|**Description**|
|---|---|
|`access`|Forces the port to **permanently be an access port** (no trunking).|
|`trunk`|Forces the port to **permanently be a trunk**.|
|`dynamic auto`|Passive mode; **waits** for DTP frames to become a trunk.|
|`dynamic desirable`|Active mode; **sends DTP frames** to negotiate trunking.|
|`nonegotiate`|**Disables DTP** on the port (used with `switchport mode trunk`).|

#### 🔹 Key Commands

To **force trunking with no DTP negotiation** (recommended with non-Cisco devices):

```bash
S1(config-if)# switchport mode trunk
S1(config-if)# switchport nonegotiate
```

To **restore DTP negotiation (default)**:

```bash
S1(config-if)# switchport mode dynamic auto
```

#### ⚠️ Caution:

- DTP **should be disabled** when connecting to:
    
    - Non-Cisco devices
        
    - End-user devices (PCs, printers)
        
- Improper handling of DTP frames can cause **misconfigurations or security issues**.
    

```
Switch(config-if)# switchport mode {  access | dynamic {  auto | desirable } |  trunk }
```
###  Résultats d'une configuration DTP

Voici un tableau récapitulatif des **comportements résultants** lorsque deux ports de switch Catalyst 2960 sont configurés avec différentes **modes DTP** :

|**Port 1 (local)**|**Port 2 (voisin)**|**Trunk formé ?**|**Comportement**|
|---|---|---|---|
|`access`|`access`|❌ Non|Reste en mode access|
|`access`|`dynamic auto`|❌ Non|Reste en mode access|
|`access`|`dynamic desirable`|❌ Non|Reste en mode access|
|`trunk`|`trunk`|✅ Oui|Trunk statique|
|`trunk`|`dynamic auto`|✅ Oui|Trunk formé (auto devient trunk)|
|`trunk`|`dynamic desirable`|✅ Oui|Trunk formé|
|`dynamic auto`|`dynamic auto`|❌ Non|Pas de trunk – aucun ne prend l'initiative|
|`dynamic auto`|`dynamic desirable`|✅ Oui|Trunk formé (auto devient trunk)|
|`dynamic desirable`|`dynamic desirable`|✅ Oui|Trunk formé|
|`trunk + nonegotiate`|`trunk + nonegotiate`|✅ Oui|Trunk sans DTP, pas de négociation|
|`trunk + nonegotiate`|`dynamic auto`|❌ Non|Pas de trunk – auto attend DTP mais nonegotiate n’envoie rien|
|`dynamic desirable`|`access`|❌ Non|Pas de trunk – access ne répond pas|

✅ = Trunk opérationnel  
❌ = Pas de trunk, lien reste en mode access

> **Bonnes pratiques :** Toujours **forcer le mode trunk avec `nonegotiate`** pour éviter les problèmes DTP, surtout avec des équipements non Cisco.



✅ **Résumé de la commande `show dtp interface` :**

Cette commande affiche l'état actuel du protocole DTP (Dynamic Trunking Protocol) sur une interface spécifique. Voici les informations clés de l'exemple :

|**Champ**|**Valeur**|**Signification**|
|---|---|---|
|`TOS/TAS/TNS`|ACCESS / AUTO / ACCESS|Type d’interface : local / mode administré / état opérationnel|
|`TOT/TAT/TNT`|NATIVE / NEGOTIATE / NATIVE|Type d’encapsulation : local / admin / opérationnel|
|`FSM state`|`S2:ACCESS`|L’état DTP actuel : l’interface est en mode access|
|`# times multi & trunk`|`0`|Aucune tentative de trunk|
|`Enabled`|`yes`|DTP est activé sur cette interface|
|`In STP`|`no`|Non impliqué dans Spanning Tree Protocol|

🎯 **Bonne pratique :**

- Pour une liaison **trunk forcée** vers un équipement non Cisco :
    
    ```bash
    switchport mode trunk  
    switchport nonegotiate
    ```
    
- Pour désactiver totalement DTP sur un port :
    
    ```bash
    switchport mode access
    ```
    

Souhaites-tu que je prépare un tableau récapitulatif des options de vérification DTP ?