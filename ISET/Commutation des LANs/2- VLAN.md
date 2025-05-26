**Atelier2: Configuration de base des réseaux locaux virtuels**

  

- **Tâche 1 : Configuration de base des commutateurs**

    - `hostname <nom>`

    - `no ip domain-lookup`

    - `enable secret class`

    - `line console 0`

    - `password cisco`

    - `login`

    - `line vty 0 15` (ou `0 4`)

    - `password cisco`

    - `login`

- **Tâche 3 : Configuration des réseaux locaux virtuels sur le commutateur**

    - **Étape 1 : Création des réseaux locaux virtuels sur le commutateur S1**

        - `vlan 99`

        - `name Management&Native`

        - `exit`

        - `vlan 10`

        - `name Faculty/Staff`

        - `exit`

        - `vlan 20`

        - `name Students`

        - `exit`

        - `vlan 30`

        - `name Guest(Default)`

        - `exit`

    - **Étape 2 : Vérification des réseaux locaux virtuels crs sur le commutateur S1**

        - `show vlan brief`

    - **Étape 3 : Configuration et attribution de noms aux réseaux locaux virtuels sur les commutateurs S2 et S3**

        - (Mêmes commandes `vlan <id>` et `name <nom>` que pour S1)

        - `show vlan brief` (pour vérification sur S2 et S3)

    - **Étape 4 : Affectation des ports du commutateur aux réseaux locaux virtuels sur les commutateurs S2 et S3**

        - `interface fastEthernet0/6`

        - `switchport mode access`

        - `switchport access vlan 30`

        - `interface fastEthernet0/11`

        - `switchport mode access`

        - `switchport access vlan 10`

        - `interface fastEthernet0/18`

        - `switchport mode access`

        - `switchport access vlan 20`

        - `end`

        - `copy running-config startup-config` (sur S2)

    - **Étape 5 : Détermination des ports ajouts**

        - `show vlan id 10` (sur S2)

        - `show vlan name <nom-vlan>` (mentionnée comme alternative)

        - `show interfaces switchport` (mentionnée comme alternative)

    - **Étape 6 : Affectation du rseau local virtuel de gestion**

        - `interface vlan 99`

        - `ip address 172.17.99.11 255.255.255.0` (sur S1)

        - `no shutdown`

        - (Répéter pour S2 et S3 avec leurs IP respectives : `172.17.99.12` et `172.17.99.13`)

    - **Étape 7 : Configuration des agrégations (Trunks)**

        - `interface fa0/1`

        - `switchport mode trunk`

        - `switchport trunk native vlan 99`

        - `interface fa0/2` (sur S1)

        - `switchport mode trunk`

        - `switchport trunk native vlan 99`

        - `end`

        - (Répéter pour les interfaces correspondantes sur S2 et S3)

        - `show interface trunk` (sur S1 pour vérification)

    - **Étape 8 : Vérification de la communication entre les commutateurs**

        - `ping <ip_gestion_S2>` (depuis S1)

        - `ping <ip_gestion_S3>` (depuis S1)

    - **Étape 9 : Envoi dune requte ping plusieurs htes depuis PC2**

        - `ping 172.17.10.21` (PC1 depuis PC2)

        - `ping 172.17.99.12` (SVI S2 depuis PC2)

        - `ping <ip_PC5>` (PC5 depuis PC2)

    - **Étape 10 : Déplacement de PC1 sur le mme VLAN que PC2**

        - (Sur S2) `interface Fa0/11`

        - (Sur S2) `switchport access vlan 20` (la réaffectation)

        - `ping 172.17.10.21` (PC1 depuis PC2, après réaffectation de port mais avant changement d'IP de PC1)

    - **Étape 11 : Modification de ladresse IP et du rseau sur PC1** (Pas de commande switch/routeur ici, mais une action sur le PC)

        - `ping 172.17.20.21` (PC1 avec nouvelle IP, depuis PC2)

  
