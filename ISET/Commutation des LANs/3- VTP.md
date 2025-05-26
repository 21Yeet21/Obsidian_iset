**Atelier 3: Configuration de base du protocole VTP**

  

- **Tâche 1 : Réalisation de configurations de base des commutateurs**

    - `hostname <nom>`

    - `no ip domain-lookup`

    - `enable secret class`

    - `line console 0`

    - `password cisco`

    - `login`

    - `line vty 0 15` (ou `0 4`)

    - `password cisco`

    - `login`

    - `copy running-config startup-config` (implicite par "enregistrez toutes vos configurations")

- **Tâche 3 : Configuration du protocole VTP et de la scurit des commutateurs**

    - **Étape 1 : Activation des ports utilisateur sur S2 et S3**

        - (Sur S2) `interface fa0/6`

        - (Sur S2) `switchport mode access`

        - (Sur S2) `no shutdown`

        - (Répéter pour `fa0/11` et `fa0/18` sur S2, et ports correspondants sur S3)

    - **Étape 2 : Vérification des paramtres VTP actifs sur les trois commutateurs**

        - `show vtp status` (sur S1, S2, S3)

    - **Étape 3 : Configuration du mode de fonctionnement, du nom de domaine et du mot de passe VTP sur les trois commutateurs**

        - (Sur S1) `vtp mode server`

        - (Sur S1) `vtp domain Lab4`

        - (Sur S1) `vtp password cisco`

        - (Sur S1) `end`

        - (Sur S2) `vtp mode client`

        - (Sur S2) `vtp domain Lab4`

        - (Sur S2) `vtp password cisco`

        - (Sur S2) `end`

        - (Sur S3) `vtp mode transparent`

        - (Sur S3) `vtp domain Lab4`

        - (Sur S3) `vtp password cisco`

        - (Sur S3) `end`

    - **Étape 4 : Configuration de lagrgation et du rseau local virtuel natif pour lagrgation des ports sur les trois commutateurs**

        - (Sur S1) `interface fa0/1`

        - (Sur S1) `switchport mode trunk`

        - (Sur S1) `switchport trunk native vlan 99`

        - (Sur S1) `no shutdown`

        - (Répéter pour `fa0/2` sur S1, et interfaces correspondantes `fa0/1`-`fa0/5` ou les ports pertinents sur S2 et S3)

        - (Sur S1) `end`

    - **Étape 5: Configuration des rseaux locaux virtuels sur le serveur VTP (S1)**

        - (Sur S1) `vlan 99`

        - (Sur S1) `name management`

        - (Sur S1) `exit`

        - (Répéter pour VLAN 10 "faculty/staff", VLAN 20 "students", VLAN 30 "guest")

        - (Sur S1) `show vlan brief`

    - **Étape 6 : Contrler si les rseaux locaux virtuels crs sur S1 ont t distribus sur S2 et S3**

        - `show vlan brief` (sur S2 et S3)

    - **Étape 7 : Cration dun nouveau rseau local virtuel sur S2 et S3**

        - (Sur S2) `vlan 88` (résultera en une erreur)

        - (Sur S3) `vlan 88`

        - (Sur S3) `name test`

        - Supprimer VLAN 88 de S3 :

            - (Sur S3) `no vlan 88`

    - **Étape 8 : Configuration manuelle des rseaux locaux virtuels (sur S3, car transparent)**

        - (Sur S3) `vlan 99`

        - (Sur S3) `name management`

        - (Sur S3) `exit`

        - (Répéter pour VLAN 10, 20, 30 avec leurs noms respectifs)

    - **Étape 9 : Configuration de ladresse de linterface de gestion sur les trois commutateurs**

        - (Sur S1) `interface vlan 99`

        - (Sur S1) `ip address 172.17.99.11 255.255.255.0`

        - (Sur S1) `no shutdown`

        - (Répéter pour S2 avec `.12` et S3 avec `.13`)

        - `ping <ip_S2_vlan99>` (depuis S1)

        - `ping <ip_S3_vlan99>` (depuis S1)

        - `ping <ip_S3_vlan99>` (depuis S2)

    - **Étape 10 : Affectation des ports des commutateurs aux rseaux locaux virtuels**

        - (Sur S3, exemple donné) `interface range fa0/6 - fa0/10`

        - (Sur S3) `switchport access vlan 30`

        - (Répéter pour `fa0/11 - fa0/17` vers VLAN 10, et `fa0/18 - fa0/24` vers VLAN 20)

        - (Sur S3) `end`

        - (Sur S3) `copy running-config startup-config` (et sur S2 aussi)

  