**Atelier5: Le protocole STP**

  

- **Tâche 1 : Configuration de base des commutateurs**

    - `hostname <nom>`

    - `no ip domain-lookup`

    - `enable password class`

    - `line console 0`

    - `password cisco`

    - `login`

    - `line vty 0 15`

    - `password cisco`

    - `login`

- **Tâche 2 : Préparation du réseau**

    - **Étape 1 : Désactivation de tous les ports laide de la commande `shutdown`**

        - `interface range fa0/1-24`

        - `shutdown`

        - `interface range gi0/1-2`

        - `shutdown`

    - **Étape 2 : Réactivation des ports utilisateur sur Comm1 et Comm2 en mode access**

        - (Pour les ports concernés)

        - `interface <interface_id>`

        - `switchport mode access` (implicite si on active pour l'accès)

        - `no shutdown`

    - **Étape 3 : Activation des ports agrgs sur Comm1, Comm2 et Comm3**

        - `interface range fa0/1, fa0/2` (exemple pour Comm1)

        - `switchport mode trunk`

        - `no shutdown`

    - **Étape 4 : Configuration de ladresse de linterface de gestion sur les trois commutateurs**

        - `interface vlan1`

        - `ip address 172.17.10.1 255.255.255.0` (exemple pour Comm1)

        - `no shutdown`

        - `ping <ip_gestion_autre_switch>`

- **Tâche 4 : Configuration du protocole Spanning Tree**

    - **Étape 1 : Examen de la configuration par dfaut du protocole STP 802.1D**

        - `show spanning-tree` (sur chaque commutateur)

- **Tâche 5 : Observation de la rponse une modification de la topologie STP 802.1D**

    - **Étape 1 : Placement des commutateurs en mode de dbogage Spanning Tree via la commande `debug spanning-tree events`**

        - `debug spanning-tree events` (sur Comm1, et implicitement sur Comm2, Comm3 pour observer)

    - **Étape 2 : Dsactivation intentionnelle du port Fa0/1 sur Comm1**

        - `interface fa0/1`

        - `shutdown`

    - **Étape 4 : Examen des modifications apportes la topologie Spanning Tree via la commande `show spanning-tree`**

        - `show spanning-tree` (sur Comm2)

spanning-tree vlan 1 priority 4096

