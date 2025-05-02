  
  
  
  
  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc3W3lan4OCQNkHiazQgz473FEUpReVhTDzuAT51XjSM7qjHAuC2LVjNO2P-FA5yJFuzSZUZF2PzOS3EfMco2oZtYusXY7vU2gOscAkwHSxoEiQELMC1qfPU8avfKIw8QDDqyLS9K6Z7m1kk7_5aQwj2Ko?key=it0QDe3ThxILgF1XY0mRmFxu)

  

1. Mode d'exécution utilisateur (>) :
    

- Fonctionnalités limitées : Pour les opérations de base et la surveillance.
    
- Commandes autorisées : Surveillance uniquement, aucune modification de la configuration.
    

1. Mode d'exécution privilégié (#) :(starts always with “enable”)
    

- Fonctionnalités étendues : Essentiel pour les commandes de configuration.
    
- Accès aux configurations supérieures : Permet d'accéder aux modes de configuration globale et autres configurations avancées.
    
- Sécurité renforcée : Utilisé par les administrateurs pour une gestion et une configuration sécurisées du réseau.
    

  

### Mode de configuration et sous-modes de configuration

Pour configurer un périphérique Cisco IOS, on doit passer par le mode de configuration globale :

1. Mode de configuration globale (config)# :(enable + configure terminal)
    

- Impacte l’ensemble du périphérique.
    
- Invite : Switch(config)#
    

1. Sous-modes de configuration :
    

- Configuration de ligne (config-line)# :(line)
    

- Configure l'accès console, SSH, Telnet, AUX.
    
- Invite : Switch(config-line)#
    

- Configuration d'interface (config-if)# :(ex:interface vlan 1)
    

- Configure les interfaces réseau des ports.
    
- Invite : Switch(config-if)#
    

### Naviguer entre les différents modes IOS

Pour naviguer entre les différents modes IOS, voici les commandes essentielles :

1. Passage du mode utilisateur au mode privilégié :
    

- enable : Passe du mode utilisateur au mode privilégié.
    
- disable : Retourne au mode utilisateur depuis le mode privilégié.
    

1. Mode de configuration globale :
    

- configure terminal : Passe au mode de configuration globale depuis le mode privilégié.
    
- exit : Retourne au mode privilégié depuis le mode de configuration globale.
    

1. Sous-modes de configuration :
    

- Configuration de ligne :
    

- line console 0 : Passe au mode de configuration de ligne.
    
- exit : Retourne au mode de configuration globale.
    

- Configuration d'interface :
    

- interface FastEthernet 0/1 : Passe au mode de configuration d'interface.
    
- exit : Retourne au mode de configuration globale.
    

1. Passage direct à un autre sous-mode :
    

- end ou Ctrl+Z : Passe du sous-mode de configuration au mode privilégié.
    

Identifiez le mode en regardant l'invite de commande :

- Switch> : Mode utilisateur
    
- Switch# : Mode privilégié
    
- Switch(config)# : Mode de configuration globale
    
- Switch(config-line)# : Mode de configuration de ligne
    
- Switch(config-if)# : Mode de configuration d'interface
    

2.3.1 Structure des commandes IOS de base 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfxUbQKjVH8URi8GQ5I9Qxk8_ezQChbXYRyx52i9KNVlRk2-vhM9Kky7O83PTeuO0JMeqdChZQXR36m52rSameLzCQr1KXMM9GmSyn8cXt3NAPY2PQDnFpRTmuddas2GYhWqhkRaJoJA0v91ekkwuBHyAz8?key=it0QDe3ThxILgF1XY0mRmFxu)

1. Mot-clé :
    

- Paramètre spécifique défini dans le système d'exploitation.
    

1. Exemple : ip protocols.
    
4. Argument :
    

- Non prédéfini; valeur ou variable définie par l'utilisateur.
    
- Exemple : 192.168.10.5.
    

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXemNNEOj9OGeWnXSFrDF9fEIy26w2Zg6WA-SeF-h_wvDwY6tjVSab5ZJ779w07Rtk8bKbC2ITJBfcQ6ONaxlzMEo6_1BQUVxC-YF_HNRC29787vRxjgpuKpMXflQ1_9AgxlzpXCUMqLtoKVRe1GcjX4zu7y?key=it0QDe3ThxILgF1XY0mRmFxu)

  
  
  
  
  
  

Help (?):

  

L'aide contextuelle ? et la vérification de syntaxe de l'IOS vous aident à trouver les commandes disponibles et à valider leur exactitude pour une utilisation efficace de l'IOS. 

  

2.3.5 Touches d’accès rapide et raccourcis  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcwSBwgRTnDeDTBkZA8XumeHBNIwHNiTW9YZYfRd6YQjgKOgEyfCF4HxUi2vzPfkoJOM4wxgiQpMV7pgv7h4MMYxoVB2KC3pXjFZ4V10K0eKTJJd7o6tb9b1qqTkChyg5Kavhk6q57sZU0azxj0W7kSRPIp?key=it0QDe3ThxILgF1XY0mRmFxu)

- -More- -  
    ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdv6LNhjY6b-KmKQuh2kp7GSORokpv7Dc-aN54iy8vhNBMjDUkqWlrCORgroQInDLR6opynESRUF9CKrgc31B4JuZuzcvm1t9odlSMymWAi5KcN-iUr46OcGwnvDHwrLfeGEtzAF5SnVzO3fdOo2Xx5n0I?key=it0QDe3ThxILgF1XY0mRmFxu)
    

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdN5WWfw3OGtC4BBmjqGvVN6ShBaS6sTZ-l01MyyOezCozkwydQw4qtVLY7Q_MRPjCjxKbKsCRmxTPpyLRmfWQOP7I9zoVa9lt8s6Lp8OJW_a3s1WlaL8hP4HOiRIsf0Hk2wzzJ5CHuhd-3FQNOiOHAG9ld?key=it0QDe3ThxILgF1XY0mRmFxu)

  

# 2.4 Configuration de base des périphériques

name :Switch(config)# hostname Sw-Floor-1

  
  
  
  

### Configurer les mots de passe

1. Mode d'exécution utilisateur :
    

- Sécurisé via la console.
    
- Commandes :
    

Sw-Floor-1# configure terminal

Sw-Floor-1(config)# line console 0

Sw-Floor-1(config-line)# password cisco

Sw-Floor-1(config-line)# login

Sw-Floor-1(config-line)# end

-   
    

1. Mode d'exécution privilégié :
    

Pour sécuriser l'accès au mode d'exécution privilégié, utilisez la commande de config. globale enable secret mot de passe, comme indiqué dans l’illustration.

  

- Accès complet à l'appareil.
    
- Commande :
    

Sw-Floor-1# configure terminal

Sw-Floor-1(config)# enable secret class (class here is the pass)

Sw-Floor-1(config)# exit

-   
    

1. Lignes VTY (Telnet/SSH) :
    

- Accès à distance sécurisé.
    
- Commandes :
    

Sw-Floor-1# configure terminal

Sw-Floor-1(config)# line vty 0 15

Sw-Floor-1(config-line)# password cisco

Sw-Floor-1(config-line)# login

Sw-Floor-1(config-line)# end

  

2.4.4 Chiffrer les mots de passe 

Pour sécuriser les mots de passe dans les fichiers startup-config et running-config :

1. Accéder au mode de configuration globale :
    

  

Sw-Floor-1# configure terminal

  

1. Chiffrer les mots de passe :
    

  

Sw-Floor-1(config)# service password-encryption

1.   
    
4. Vérifier que les mots de passe sont chiffrés :
    

Sw-Floor-1# show running-config

La commande service password-encryption applique un chiffrement simple pour protéger les mots de passe dans le fichier de configuration, empêchant leur lecture par des personnes non autorisée

  

### Messages de bannière

  

Pour créer une bannière MOTD (Message Of The Day) qui s'affiche à chaque tentative d'accès au périphérique :

1. Accéder au mode de configuration globale :
    
2.   
    

Sw-Floor-1# configure terminal

Sw-Floor-1(config)# banner motd #Authorized Access Only#

  

La commande banner motd utilise un délimiteur (# dans cet exemple) pour encadrer le message. Cette bannière informe les utilisateurs que l'accès est réservé aux personnes autorisées, et peut être cruciale pour des raisons légales.

### Enregistrement des configurations

2.5.1 Fichiers de configuration

- startup-config :
    

- Stocké dans NVRAM. (non volatile )
    
- Contient toutes les commandes utilisées au démarrage ou redémarrage.
    
- Non volatile : conserve son contenu même hors tension.
    

- running-config :
    

- Stocké dans la RAM.
    
- Reflète la configuration actuelle.
    
- Volatile : perd son contenu lors d'une mise hors tension ou redémarrage.
    

- Afficher la configuration en cours 
    

Sw-Floor-1# show running-config

- Afficher la configuration initiale :
    

Sw-Floor-1# show startup-config

  

- Enregistrer la configuration en cours dans la configuration initiale 
    

Sw-Floor-1# copy running-config startup-config

also : copy run start

2.5.2 Modifier la configuration en cours

- Restaurer la configuration précédente :
    

- Supprimez les commandes modifiées individuellement ou utilisez
    

reload

-   
    

- Effacer la configuration initiale :
    

Sw-Floor-1# erase startup-config

- Recharger le périphérique :
    

- Supprime le fichier de configuration en cours de la RAM.
    
- Recharge la configuration initiale.
    

Ces étapes garantissent que vos configurations sont enregistrées et peuvent être restaurées en cas de besoin. 

  

  

  

### Adresses IP

L'utilisation d'adresses IP est cruciale pour la communication de bout en bout sur Internet. Chaque périphérique final d'un réseau doit être configuré avec une adresse IP.

Exemples de périphériques finaux :

- Ordinateurs (stations de travail, ordinateurs portables, serveurs de fichiers, serveurs web)
    
- Imprimantes réseau
    
- Téléphones VoIP
    
- Caméras de surveillance
    
- Smartphones
    
- Périphériques portables mobiles (par exemple, lecteurs de codes à barres sans fil)
    

Structure d'une adresse IPv4 :

- Notation décimale à point : quatre nombres décimaux compris entre 0 et 255.
    

Adresse IPv4 et masque de sous-réseau :

- Adresse IPv4 : Par exemple, 192.168.1.10
    
- Masque de sous-réseau : 255.255.255.0
    
- Passerelle par défaut : Adresse IP du routeur, par exemple, 192.168.1.1
    

Remarque :

- "IP" fait référence aux protocoles IPv4 et IPv6.
    
- IPv6 est la version la plus récente de l'IP et remplace l'IPv4.
    

Le masque de sous-réseau différencie la partie réseau de l'adresse de la partie hôte, déterminant à quel sous-réseau spécifique le périphérique appartient.

  

  

  

  

  

  

2.6.2 Interfaces et ports

Les communications réseau dépendent des interfaces des périphériques utilisateur final, des interfaces des périphériques réseau et des câbles de connexion. Chaque interface a des caractéristiques, ou des normes, qui la définissent. Un câble de connexion à l'interface doit donc être adapté aux normes physiques de l'interface. Ces supports de transmission peuvent être des câbles en cuivre à paires torsadées, des câbles à fibres optiques, des câbles coaxiaux ou une liaison sans fil, comme illustré dans la figure.

Les différents types de supports réseau possèdent divers avantages et fonctionnalités. Tous les supports réseau n'ont pas les mêmes caractéristiques. Tous les médias ne sont pas appropriés pour le même objectif Les différences entre les types de supports de transmission incluent, entre autres:

  

    la distance sur laquelle les supports peuvent transporter correctement un signal

    l'environnement dans lequel les supports doivent être installés

    la quantité de données et le débit de la transmission

    le coût des supports et de l'installation

  

Chaque liaison à Internet requiert un type de support réseau spécifique, ainsi qu'une technologie réseau particulière. Par exemple, l'Ethernet est la technologie de réseau local (LAN) la plus répandue aujourd'hui. Les ports Ethernet sont présents sur les périphériques des utilisateurs finaux, les commutateurs et d'autres périphériques réseau pouvant se connecter physiquement au réseau à l'aide d'un câble.

  

Les commutateurs Cisco IOS de couche 2 sont équipés de ports physiques pour permettre à des périphériques de s'y connecter. Ces ports ne prennent pas en charge les adresses IP de couche 3. Par conséquent, les commutateurs ont une ou plusieurs interfaces de commutateur virtuelles (SVI). Ces interfaces sont virtuelles car il n'existe aucun matériel sur le périphérique associé. Une interface SVI est créée au niveau logiciel.

  

L'interface virtuelle est un moyen de gérer à distance un commutateur sur un réseau grâce à l'IPv4 et l'IPv6 Chaque commutateur dispose d'une interface SVI apparaissant dans la configuration par défaut prête à l'emploi. L'interface SVI par défaut est l'interface VLAN1.

  

Remarque: un commutateur de couche 2 ne nécessite pas d'adresse IP. L'adresse IP attribuée à l'interface SVI sert à accéder à distance au commutateur. Une adresse IP n'est pas nécessaire pour permettre au commutateur d'accomplir ses tâches.

##   

### Interfaces et ports

Les communications réseau dépendent des interfaces des périphériques utilisateur final, des interfaces des périphériques réseau et des câbles de connexion. Chaque interface doit être adaptée aux normes physiques correspondantes, incluant câbles en cuivre, fibres optiques, câbles coaxiaux et liaisons sans fil.

Différences entre types de supports de transmission :

- Distance de transport du signal
    
- Environnement d'installation
    
- Quantité de données et débit de transmission
    
- Coût des supports et de l'installation
    

Exemple :

- Ethernet : Technologie LAN la plus répandue, présente sur les périphériques finaux et les commutateurs.
    

Commutateurs Cisco IOS de couche 2 :

- Équipés de ports physiques, mais ne supportent pas les adresses IP de couche 3.
    
- Utilisent des interfaces de commutateur virtuelles (SVI) pour la gestion à distance via IPv4 et IPv6.
    
- Interface SVI par défaut : VLAN1.
    

Remarque : Un commutateur de couche 2 n'a pas besoin d'adresse IP pour accomplir ses tâches, mais l'adresse IP de l'interface SVI permet un accès à distance.

  

  
  
  
  

2.7.4 Configuration de l'interface de commutateur virtuelle

  

 Vlan 1 n'est pas une interface physique réelle mais une interface virtuelle :

  

Sw-Floor-1# configure terminal

Sw-Floor-1(config)# interface vlan 1

Sw-Floor-1(config-if)# ip address 192.168.1.20 255.255.255.0

Sw-Floor-1(config-if)# no shutdown  (activation d’interface)

Sw-Floor-1(config-if)# exit

Sw-Floor-1(config)# ip default-gateway 192.168.1.1

  
  
  
  

IMPORTANT : if you can ping from PC1 to PC2 but not from PC2 to PC1 you have a problem with the firewall of windows configs : is blocking the ICMP requests .(solution : turn off windows firewall)