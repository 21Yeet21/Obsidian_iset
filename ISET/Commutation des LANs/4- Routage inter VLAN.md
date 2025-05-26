**Atelier4: Routage de base entre VLAN**

  

- **Tâche 1 : Configuration de base des machines**

    - **Étape 3 : Configuration des commutateurs S1, S2 et S3**

        - `hostname <nom>`

        - `no ip domain-lookup`

        - `enable secret class`

        - `line console 0`

        - `password cisco`

        - `login`

        - `line vty 0 15` (ou `0 4`)

        - `password cisco`

        - `login`

        - `ip default-gateway <adresse_passerelle_routeur_pour_ce_vlan>`

- **Tâche 2 : Configuration des VLANs dans les commutateurs**

    - **Étape 1 : Réactivation des ports utilisateur actifs sur S2 en mode access**

        - (Sur S2) `interface fa0/6`

        - (Sur S2) `switchport mode access`

        - (Sur S2) `no shutdown`

        - (Répéter pour `fa0/11` et `fa0/18`)

    - **Étape 2 : Configuration des ports dagrgation et dsignation du rseau local virtuel natif pour les agrgations**

        - (Sur les commutateurs concernés, pour Fa0/1 à Fa0/5 ou les ports de trunk)

        - `interface <interface_id_trunk>` ou `interface range <plage_interface_trunk>`

        - `switchport mode trunk`

        - `switchport trunk native vlan 99`

        - `no shutdown` (si nécessaire)

    - **Étape 3 : Configuration des rseaux locaux virtuels sur les commutateurs S1, S2 et S3**

        - (Si VTP n'est pas utilisé ou si c'est un serveur VTP/transparent)

        - `vlan <id_vlan>` (ex: 1, 10, 20, 30, 99)

        - `name <nom_vlan>`

        - `show vlan brief` (pour vérification sur S1)

    - **Étape 4 : Configuration de ladresse de linterface de gestion sur les trois commutateurs**

        - `interface vlan 99`

        - `ip address <ip_vlan99_commutateur> <masque>`

        - `no shutdown`

        - `ping <ip_autre_commutateur_vlan99>`

    - **Étape 5 : Affectation des ports de commutateurs aux rseaux locaux virtuels sur S2**

        - (Selon la table d'affectation)

        - `interface <interface_id_acces>`

        - `switchport mode access`

        - `switchport access vlan <id_vlan_correspondant>`

- **Tâche 3 : Configuration du routeur et du serveur distant de réseau local**

    - **Étape 1 : Création dune configuration de base sur le routeur (R1)**

        - `hostname R1`

        - `no ip domain-lookup`

        - `enable password cisco` (le TP indique "mot de passe du mode d’exécution")

        - `line console 0`

        - `password cisco`

        - `login`

        - `line vty 0 4` (ou `0 15`)

        - `password cisco`

        - `login`

    - **Étape 2 : Configuration de linterface "classique" (Router-on-a-Stick) sur R1**

        - `interface fastethernet 0/1`

        - `no shutdown`

        - `interface fastethernet 0/1.1`

        - `encapsulation dot1q 1`

        - `ip address 172.17.1.1 255.255.255.0`

        - `interface fastethernet 0/1.10`

        - `encapsulation dot1q 10`

        - `ip address 172.17.10.1 255.255.255.0`

        - (Répéter pour VLAN 20, 30 avec `.20`, `.30` et leurs IP)

        - `interface fastethernet 0/1.99`

        - `encapsulation dot1q 99 native`

        - `ip address 172.17.99.1 255.255.255.0`

        - `show ip interface brief`

    - **Étape 3 : Configuration de linterface rseau du serveur sur R1**

        - `interface FastEthernet0/0`

        - `ip address 172.17.50.1 255.255.255.0`

        - `description server interface`

        - `no shutdown`

        - `end`

        - `show ip route` (implicite pour "contrôlant la table de routage")

    - **Étape 4 : Vérification du routage entre rseaux locaux virtuels**

        - `ping 172.17.50.254` (depuis PC1)

        - `ping 172.17.20.22` (depuis PC1)

        - `ping 172.17.30.23` (depuis PC1)

  