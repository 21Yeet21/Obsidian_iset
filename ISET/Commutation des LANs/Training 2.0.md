# Configuration de base

hostname SW-Nom # Définir le nom du commutateur no ip domain-lookup # Désactiver la résolution DNS enable secret motdepasse # Mot de passe chiffré pour mode privilégié line console 0 password motdepasse login line vty 0 15 password motdepasse login copy running-config startup-config # Sauvegarder la configuration

# Configuration VLAN

vlan 10 name NomVLAN interface fastethernet 0/10 switchport mode access switchport access vlan 10 interface fastethernet 0/1 switchport mode trunk switchport trunk native vlan 99 show vlan brief # Vérifier les VLANs

# Sécurité des ports

interface fastethernet 0/4 switchport mode access switchport port-security switchport port-security maximum 1 switchport port-security mac-address sticky show mac-address-table # Vérifier la table MAC

# Configuration VTP

vtp mode server vtp domain NomDomaine vtp password motdepasse show vtp status # Vérifier l’état VTP

# Routage inter-VLAN

interface fastethernet 0/0.10 encapsulation dot1q 10 ip address 192.168.10.1 255.255.255.0 show ip interface brief # Vérifier les interfaces

# Spanning Tree

debug spanning-tree events # Activer le débogage STP show spanning-tree # Vérifier l’état STP

# EtherChannel

interface range fa0/1-3 channel-group 1 mode desirable interface port-channel 1 switchport mode trunk show etherchannel summary # Vérifier EtherChannel

# Port Mirroring

monitor session 1 source interface fa0/1 both monitor session 1 destination interface fa0/2 show monitor session 1 # Vérifier la session