**Atelier1: Configuration de base/avancée d'un switch**

  

- **Tâche 1 : Construction du réseau et configuration des périphériques**

    - **Étape 1 : Configuration des informations de base sur le routeur et le commutateur**

        - Pour R1 et Comm1 (implicites basées sur la description) :

            - `hostname <nom>`

            -

            - `enable secret <mot_de_passe>`

            -

            - `line console 0`

            - `password <mot_de_passe_console>`

            - `login`

            -

            - `line vty 0 4` (ou `0 15`)

            - `password <mot_de_passe_vty>`

            - `login`

            - no ip domain-lookup

            -

            - (Pour Comm1) `interface vlan 1`

            - (Pour Comm1) `ip address <ip> <masque>`

            -

            - (Pour R1, sur son interface Fast Ethernet) `ip address <ip> <masque>`

            - (Pour R1 et Comm1) `no shutdown` (sur les interfaces configurées)

        - Pour enregistrer la configuration :

            - `copy running-config startup-config`

- **Tâche 3 : Vérification des données d’interface du commutateur**

    - **Étape 1 : Vérification de l’état de l’interface**

        - `show ip interface brief` (sur Comm1)

    - **Étape 2 : Vérification de la connectivité de bout en bout**

        - `ping <adresse_ip_passerelle>` (ex: `ping 192.168.1.1` depuis H1)

        - `ping <adresse_ip_H2>` (ex: `ping 192.168.1.22` depuis H1)

    - **Étape 3 : Vérification de l’état et des paramètres de l’interface**

        - `show interface <port_id> status` (pour Fast Ethernet 0/1 et Fast Ethernet 0/3 sur Comm1, bien que la commande exacte montrée dans le TP soit un `show interface status` générique qui n'existe pas tel quel, le contexte pointe vers `show interfaces <interface> status` ou simplement `show interfaces <interface>` pour voir ces détails). Le TP montre une sortie qui ressemble à `show interfaces status`.

- **Tâche 4 : Modification des paramètres bidirectionnels**

    - **Étape 1 : Définition du paramètre bidirectionnel simultané**

        - `interface FastEthernet 0/3`

        - `duplex full`

        - `show ip interface brief`

    - **Étape 2 : Définition du paramètre bidirectionnel non simultané**

        - `interface FastEthernet 0/3`

        - `duplex half`

        - `show ip interface brief`

    - **Étape 3 : Définition du paramètre bidirectionnel d’autonégociation**

        - `interface FastEthernet 0/3`

        - `duplex auto`

        - `end`

- **Tâche 5 : Modification des paramètres de vitesse**

    - **Étape 1 : Définition de la vitesse sur 100 Mbits/s**

        - `interface FastEthernet 0/3`

        - `speed 100`

        - `show ip interface brief`

    - **Étape 2 : Définition du paramètre de vitesse sur autonégociation**

        - `interface FastEthernet 0/3`

        - `speed auto` (implicite pour revenir à l'auto)

- **Tâche 6 : Définition des paramtres de mode bidirectionnel et de vitesse**

    - **Étape 1 : Définition du paramètre de mode bidirectionnel simultané et du paramètre de vitesse 100 Mbits/s pour Fast Ethernet 0/1**

        - `interface FastEthernet 0/1`

        - `duplex full`

        - `speed 100`

    - **Étape 2 : Vérification des nouveaux paramètres**

        - `show run interface FastEthernet 0/1`

- **Tâche 7 : Modification des paramètres bidirectionnels du routeur**

    - **Étape 1 : Définition du paramètre bidirectionnel non simultané de Fast Ethernet 0/0 pour R1**

        - (Sur R1) `interface FastEthernet 0/0`

        - (Sur R1) `duplex half`

        - (Sur R1) `show ip interface brief`

        - (Sur Comm1) `show ip interface brief`

        - (Sur R1) `ping 192.168.1.99` (adresse VLAN 1 du commutateur)

- **Tâche 9 : Manipulation de la table MAC et les options de sécurité**

    - **Étape 2 : Déterminez les adresses MAC que le commutateur a acquises**

        - `show mac-address-table`

    - **Étape 3 : Configurez une adresse MAC statique**

        - `mac-address-table static <adresse_mac_H3> vlan 1 interface FastEthernet0/4` ==(compléter la commande)==

    - **Étape 4 : Vérifiez les résultats**

        - `show mac-address-table`

    - **Étape 5 : Listez les options de sécurité des ports**

        - `interface fastethernet 0/4`

        - `switchport port-security ?`

        - Pour que le port n'accepte qu'un équipement (commandes nécessaires) :

            - `switchport mode access` (prérequis si ce n'est pas déjà le cas)

            - `switchport port-security`

            - `switchport port-security maximum 1`

            - `switchport port-security mac-address sticky` (une option pour apprendre dynamiquement et sécuriser) ou ==`switchport port-security mac-address <adresse_mac_H3>` (pour sécuriser statiquement H3)==

    - **Étape 6 : Vérifiez les résultats**

        - `show mac-address-table`

    - **Étape 7 : Affichez le fichier de la configuration courante**

        - `show running-config` (implicite pour voir les instructions de sécurité)

    - **Étape 8 : Limitez le nombre d’hôtes sur chaque port**

        - `interface fastethernet 0/4`

        - `switchport port-security maximum 1`

        - `ping 192.168.1.22 -n 50` (depuis H2 connecté à Fa0/4 après déconnexion de H3, pour générer trafic et potentiellement une violation si mal configuré ou si H3 était sticky)

    - **Étape 9 : Déplacez l’hôte**

        - `ping 192.168.1.22 -n 50` (depuis H3 maintenant sur Fa0/8)

        - `show mac-address-table`

    - **Étape 10 : Effacez la table MAC**

        - `clear mac-address-table dynamic`

        - `ping 192.168.1.22 -n 50` (depuis H3 sur Fa0/8)

    - **Étape 12 : Modifiez les paramtres de sécurité**

        - `show mac-address-table`

        - Supprimer la sécurité du port Fa0/4 :

            - `interface fastethernet 0/4`

            - `no switchport port-security` (ou des commandes plus spécifiques comme `no switchport port-security mac-address ...`)

        - Appliquer la sécurité (max 1 MAC) sur Fa0/8 :

            - `interface fastethernet 0/8`

            - `switchport mode access` (si nécessaire)

            - `switchport port-security`

            - `switchport port-security maximum 1`

        - Effacer la table MAC : `clear mac-address-table dynamic` (le TP demande la commande pour effacer)

    - **Étape 13 : Vrifiez les rsultats**

        - `show mac-address-table`

        - `ping` (entre les PCs)

    - **Étape 14 : Quittez le commutateur**

        - `exit`
