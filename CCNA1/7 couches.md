  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc8TPa7g4i1isBSyfRmAYVYTWEXg9SkR76w_71biQyZFT4_AoUNWIwILWrj3c3B5DqfGHQFmv3PMm0klYtDOtzyXG0h-02xRhXfcrj7NTeYcqcuQ1uoBcDdjq7leE2Ic9X9YeLhQ1z9BB99j72Xu-NlSf4?key=g41p4SqjIHv6s3PS7kB56_is)

  
  

les protocoles informatiques et réseau définissent la manière dont un message est transmis sur un réseau. Les protocoles informatiques communs comprennent les exigences suivantes :

- Codage des messages
    
- Format et encapsulation des messages
    
- La taille du message
    
- Synchronisation des messages
    
- Options de remise des messages
    

  

### 3.1.3 Protocoles de communication

Les communications informatiques sont régies par un ensemble de règles et de protocoles qui déterminent comment les données sont transmises et reçues sur un réseau.

### 3.1.6 Codage des messages

Les messages envoyés sur le réseau sont convertis en bits, lesquels sont codés en signaux électriques, lumineux ou micro-ondes selon le support utilisé. Le dispositif récepteur décode ces signaux pour interpréter le message.

### 3.1.7 Format et encapsulation des messages

Tout comme l'envoi d'une lettre, un message sur un réseau informatique doit suivre des règles de format spécifiques pour être correctement transmis et reçu.

### 3.1.8 Taille des messages

Les messages longs sont fragmentés en plusieurs trames pour être envoyés sur le réseau. Chaque trame doit respecter une taille minimale et maximale pour être acceptée. Les trames trop longues ou trop courtes sont rejetées. Le récepteur reconstruit le message d'origine à partir des différentes trames reçues.

### 3.1.9 Synchronisation des messages

La synchronisation des messages implique :

- Contrôle de flux : Gestion de la vitesse de transmission des données pour éviter la saturation.
    
- Délai de réponse : Détermination du temps d'attente avant de considérer une communication comme non réussie.
    
- Méthode d'accès : Définition du moment où un périphérique peut envoyer un message pour éviter les collisions.
    

  

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcvbgMydw0sgrD2pI4qiSQ_VdYKxKctJqKibQTdOap4ZaxewsTE7AbuUMPRfD3yYm8myBFyvPkPI1m6U7VdvsfNoSYg-cUTrXi35dTu_vumxWA9e8Hh-u_C5KF4L6eGjSn2U758ctkKhlANK9coPyajcTxA?key=g41p4SqjIHv6s3PS7kB56_is)

  
  
  

Ces éléments assurent une communication réseau efficace et fiable. 🚀📡

  

# 3.2 Protocoles

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcfDJhz91YTJT77uM2EI1P2RiZw1xI2K_POJAaI19jnC7d_rGC5f4CbPIpzRyedZBXLa1fs7SK_HJMgY68ny7Ki5PT4Mii2LENwKHFehO5_67EuJZL4qk2woP1MvfCTGDT3oJpJotJivTqXdhW3ulKR1gg?key=g41p4SqjIHv6s3PS7kB56_is)

  

3.2.2 Fonctions du Protocole de Réseau 

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdDC0b3aNZoMciN05tf-H7_Pj358aC0NMQxt28pJMVRR56sffGGZcwkYSj-na4o3oAoT05r0JPtw7f_lc0XHBrFIrFKeGPr_gvUVYWYUAYJzWJUFG8LORQ4EsutiTSsKX6Pp0TbzxGkU8ZVla5CEr5pgD_U?key=g41p4SqjIHv6s3PS7kB56_is)

3.2.3 Interaction entre les protocoles 

###   

Un message envoyé sur un réseau informatique utilise plusieurs protocoles, chacun ayant des fonctions et des formats spécifiques(example un message peut utiliser) :

1. HTTP (Hypertext Transfer Protocol) :
    

- Gère les interactions entre un serveur web et un client web.
    
- Décrit le contenu et la mise en forme des requêtes et réponses échangées entre le client et le serveur.
    
- Dépend d'autres protocoles pour le transport des messages.
    

1. TCP (Transmission Control Protocol) :
    

- Gère les conversations individuelles.
    
- Assure la livraison fiable des informations et contrôle le flux entre les appareils finaux.
    

1. IP (Protocole Internet) :
    

- Responsable de la remise des messages de l'expéditeur au destinataire.
    
- Utilisé par les routeurs pour transférer les messages sur plusieurs réseaux.
    

1. Ethernet :
    

- Responsable de la remise des messages d'une carte réseau à une autre carte réseau sur le même réseau local (LAN) Ethernet.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeHUzrkKQg9XeZo-NeMXN2xhpCv-YF1OJmW3AzSv4ZGqyWXBg_hHFfdKhu4XLvzDD6hnWHRKwfMZXBygZitXa6O-7LICOPCe4yZI6GaiGLLn_vGEh86u4ICO1S5MBUlMflSSRQTOlYkCWu6Pcm-gTv5W9FT?key=g41p4SqjIHv6s3PS7kB56_is)

### Couche application

#### Systèmes

1. DNS (Système de noms de domaine) :
    

- Traduit les noms de domaine comme [cisco.com](https://cisco.com/?form=MG0AV3) en adresses IP.
    

#### Configuration des hôtes

1. DHCPv4 (Protocole de configuration dynamique des hôtes pour IPv4) :
    

- Affecte dynamiquement les informations d'adressage IPv4 aux clients DHCPv4.
    

1. DHCPv6 (Protocole de configuration dynamique des hôtes pour IPv6) :
    

- Similaire à DHCPv4, affecte dynamiquement les informations d'adressage IPv6.
    

1. SLAAC (Autoconfiguration des adresses apatrides) :
    

- Permet à un périphérique d'obtenir des informations d'adressage IPv6 sans serveur DHCPv6.
    

#### E-mail

1. SMTP (Protocole de Transfert de Courrier Simple) :
    

- Permet aux clients et serveurs de messagerie d'envoyer des courriers électroniques.
    

1. POP3 (Protocole de la Poste, version 3) :
    

- Permet de récupérer et télécharger des courriels depuis un serveur de messagerie.
    

1. IMAP (Protocole d'Accès aux Messages Internet) :
    

- Permet d'accéder et de maintenir les courriels sur un serveur de messagerie.
    

#### Transfert de fichiers

1. FTP (Protocole de Transfert de Fichiers) :
    

- Définit les règles pour accéder et transférer des fichiers entre hôtes via un réseau.
    

1. SFTP (Protocole de Transfert de Fichiers SSH) :
    

- Utilise SSH pour un transfert de fichiers sécurisé et crypté.
    

1. TFTP (Protocole de Transfert de Fichiers Trivial) :
    

- Protocole simple et sans connexion pour transférer des fichiers avec moins de surcharge que FTP.
    

#### Web et Service Web

1. HTTP (Protocole de Transfert Hypertexte) :
    

- Règles pour échanger du texte, des graphiques, des sons, des vidéos, et autres fichiers multimédia sur le web.
    

1. HTTPS (HTTP Sécurisé) :
    

- Forme sécurisée de HTTP qui crypte les données échangées sur le web.
    

1. REST (Transfert de l'État de représentation) :
    

- Utilise des API et requêtes HTTP pour créer des applications Web.
    

Couche transport

Connexion Orienté

- TCP - Protocole de Contrôle de Transmission. Permet une communication fiable entre des processus fonctionnant sur des hôtes distincts et fournit des transmissions fiables et reconnues qui confirment le succès de la livraison.
    

Sans connexion

- UDP - Protocole de Datagramme Utilisateur. Permet à un processus s'exécutant sur un hôte d'envoyer des paquets à un processus s'exécutant sur un autre hôte. Cependant, l'UDP ne confirme pas la réussite de la transmission des datagrammes.
    

  

### Couche accès réseau

#### Protocole Internet

1. IPv4 (Protocole Internet version 4) :
    

- Reçoit des segments de message de la couche transport, emballe les messages en paquets et adresse les paquets pour une livraison de bout en bout.
    
- Utilise une adresse 32 bits.
    

1. IPv6 (Protocole Internet version 6) :
    

- Similaire à IPv4 mais utilise une adresse 128 bits.
    

1. NAT (Traduction des Adresses de Réseau) :
    

- Traduit les adresses IPv4 d'un réseau privé en adresses IPv4 publiques uniques au monde.
    

#### Envoi de messages

1. ICMPv4 (Protocole de message de contrôle Internet pour IPv4) :
    

- Fournit un retour d'information d'un hôte de destination à un hôte source sur les erreurs de livraison de paquets.
    

1. ICMPv6 (ICMP pour IPv6) :
    

- Fonctionnalité similaire à ICMPv4, mais utilisée pour les paquets IPv6.
    

1. ICMPv6 ND (Détection de voisin ICMPv6) :
    

- Inclut quatre messages de protocole utilisés pour la résolution d'adresses et la détection d'adresses en double.
    

#### Protocoles de routage

1. OSPF (Open Shortest Path First) :
    

- Protocole de routage d'état de liaison qui utilise une conception hiérarchique basée sur des zones.
    
- Protocole de routage interne standard ouvert.
    

1. EIGRP (Enhanced Interior Gateway Routing Protocol) :
    

- Protocole de routage propriétaire de Cisco utilisant une métrique composite basée sur la largeur de bande, le délai, la charge et la fiabilité.
    

1. BGP (Border Gateway Protocol) :
    

- Protocole de routage de passerelle extérieure standard ouvert utilisé entre les fournisseurs de services Internet (ISPs).
    
- Utilisé également entre les ISPs et leurs clients privés plus importants pour échanger des informations de routage.
    

Couche internet

Résolution d'adresse

- ARP - Protocole de résolution des adresses. Fournit un mappage d'adresse dynamique entre une adresse IPv4 et une adresse physique.
    

Protocoles de Liaison de Données

- Ethernet - Définit les règles relatives aux normes de câblage et de signalisation de la couche d'accès au réseau.
    
- WLAN - Réseau local sans fil. Définit les règles de signalisation sans fil sur les fréquences radio 2,4 GHz et 5 GHz.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfuHViXBfp7qkC9QY-W5hHG5_Ox4-TqPvtBiDcBsndSAyJPuJOcT29acBfT4ScYNTF31hhrcodHgXYow9zR1F4n_FmLGh9zlQ1BiEP0G1nR3HCQF8XEdJBn2omjpPbPldn9GOMXa0sd1yVQykLm2ibiuWkX?key=g41p4SqjIHv6s3PS7kB56_is)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfBA5vdExOz7XwW7AqQzqZra06ro7modSXJ3WI8cKWzdHxPnfYaprGhPg0ntZBY0eBHUfW2HV0dGQUDTvmcPih8-R2YfYpmZJaMvqtP5FXBZj_AE2u2IxdSPdsdIALBBmBAzynHel0H5qxPx0NsgetQjwkq?key=g41p4SqjIHv6s3PS7kB56_is)

3.5.3 Le modèle de référence TCP/IP 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeXqmIvIDsZTU4Ihz-DFq9-o55pFJpEzu2lDba0Wu6y_ivoXEi8Y1Uql0uKNHoPKwk2iaPOHfk19ETtPoLQmjRRO971u9Xr8k8xiR8f0EGbixkqMwBWnYPk9xUkmXgYcF4A-F5YBXFBBrqCL8VGdTf5DrF1?key=g41p4SqjIHv6s3PS7kB56_is)

  

### 3.6.1 Segmentation des Messages (TA9SIM)

La segmentation des messages consiste à diviser un flux de données en unités plus petites pour les transmissions sur le réseau. Voici un résumé des concepts clés :

- Modèle OSI et modèle TCP/IP :
    

- Utilisés pour comprendre comment les données sont encapsulées et déplacées sur un réseau.
    

- Segmentation des données :
    

- Processus de division des données en unités plus petites et gérables pour les envoyer sur le réseau.
    
- Prévention de problèmes causés par de grands flux de données, tels que les retards ou la perte complète des messages.
    

- Avantages de la segmentation :
    

- Augmentation de la vitesse : Permet à de grandes quantités de données d'être envoyées sans monopoliser une liaison de communication. Favorise le multiplexage, où plusieurs conversations peuvent être entrelacées sur le réseau.
    
- Augmentation de l'efficacité : En cas de perte de segment, seul ce segment doit être retransmis, et non l'intégralité du flux de données.
    

### 3.6.2 Séquençage (TAR9IM)

Le séquençage est essentiel pour reassembler les segments de messages dans leur ordre original lors de la transmission sur un réseau :

- Complexité de la segmentation et du multiplexage :
    

- Divise un long message en segments plus petits.
    
- Chaque segment doit inclure un numéro de séquence pour assurer le bon ordre.
    

- Exemple de la lettre :
    

- Une lettre de 100 pages envoyée en 100 enveloppes doit inclure des numéros de séquence pour être réassemblée correctement.
    

- Rôle de TCP :
    

- TCP (Transmission Control Protocol) est responsable du séquençage des segments individuels.
    
- Assure que les segments arrivent à la bonne destination et sont réassemblés dans le contenu du message original
    

  

  

  

  

  

### 3.6.3 Unités de données de protocole (PDU)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdmRuD8QFcJdoysgzYCwVMSARQfmzVGR5kyVn4PdriYnjDeOQpzOdZ6fDH9Sq_XXIB9HbGTWkoiKmtLDevGA-VOlej4AsHtsv4J-r8f7F0gQ_FYmewwMjUuil1uW_bilUJLChbGOjn5hsMylBhjveyW_RSq?key=g41p4SqjIHv6s3PS7kB56_is)

  

###   

Lors de la transmission des données sur un réseau, chaque couche du modèle OSI/TCP/IP ajoute ses propres informations de protocole. Ce processus est appelé encapsulation.

#### Différentes Unités de Données de Protocole (PDU)

- Données : Terme générique pour l'unité de données de protocole utilisée à la couche application.
    
- Segment : Unité de données de protocole de la couche transport (si l'en-tête est TCP, il s'agit d'un segment).
    
- Paquet : Unité de données de protocole de la couche réseau.
    
- Trame : Unité de données de protocole de la couche liaison de données.
    
- Bits : Unité de données de protocole de la couche physique utilisée pour la transmission sur le support physique.
    

#### Remarque :

- Si l'en-tête de la couche Transport est TCP, il s'agit d'un segment.
    
- Si l'en-tête de la couche Transport est UDP, il s'agit d'un datagramme.
    

### 3.7.1 Adresses

Pour garantir que les messages segmentés atteignent leur destination, il est essentiel de les adresser correctement. Voici un aperçu des adresses de réseau et leurs objectifs :

#### Couches réseau et liaison de données

1. Adresses source et destination de la couche réseau :
    

- Responsabilité : Livraison du paquet IP de la source d'origine à la destination finale.
    
- Portée : Peut être sur le même réseau ou sur un réseau distant.
    
- Exemple : Adresse IP source et destination.
    

1. Adresses source et destination de la couche de liaison de données :
    

- Responsabilité : Transmission de la trame de liaison de données d'une carte d'interface réseau (NIC) à une autre NIC sur le même réseau.
    
- Portée : Restreinte au même réseau local.
    
- Exemple : Adresse MAC source et destination.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdqg-7ali8ylfcXBnGsZTEo7gBK8XMX8cDpllMgfEUSkvFIww4IEg7Dhq6HCqhH9nd6YzuvaTvhnT1ewWqeCpQ7C0RZ90NfKC2WlSK5mnJ7LParMElhQrn9-cCwAu17408FqGe90tX-lLwCmfH-4eQ9pfDI?key=g41p4SqjIHv6s3PS7kB56_is)

  

  

  

### Adresses IP et MAC: Transmission des Données

#### Adresses Logiques de la Couche 3 (Adresse IP)

- Adresse IP source : IP de l'émetteur (ex: 192.168.1.110).
    
- Adresse IP de destination : IP du récepteur (ex: 192.168.1.9).
    
- Parties de l'adresse IP :
    

- Partie réseau (IPv4) : Indique le réseau (ex: 192.168.1).
    
- Partie hôte (IPv4) : Identifie un appareil spécifique (ex: .110).
    

#### Transmission sur le Même Réseau

- Adresse MAC source : Adresse physique de l'émetteur (ex: AA-AA-AA-AA-AA-AA).
    
- Adresse MAC de destination : Adresse physique du récepteur sur le même réseau (ex: CC-CC-CC-CC-CC-CC).
    
- Transmission directe de la trame Ethernet au récepteur.
    

#### Transmission sur un Réseau Distant

- Adresse MAC source : Adresse physique de l'émetteur (ex: AA-AA-AA-AA-AA-AA).
    
- Adresse MAC de destination : Adresse MAC de la passerelle par défaut (ex: 11-11-11-11-11-11).
    
- La trame Ethernet est envoyée à la passerelle, qui achemine le paquet vers la destination finale.
    

#### Rôle des Adresses de Liaison de Données

- Utilisées pour transmettre la trame d'une interface réseau à une autre sur le même réseau.
    
- Encapsulation du paquet IP :
    

- Adresse de la liaison de données source : MAC du NIC émetteur.
    
- Adresse de la liaison de données de destination : MAC du NIC récepteur ou du routeur de prochain saut.
    

  

  

  

  

  

  

IP vs MAC

Portée locale vs. globale :

- Adresse MAC : Identifie un appareil unique sur un segment de réseau local. Les commutateurs utilisent les adresses MAC pour acheminer les trames au sein du même réseau local.
    
- Adresse IP : Utilisée pour l'acheminement des paquets sur des réseaux différents. Les routeurs utilisent les adresses IP pour transférer les paquets d'un réseau à un autre.
    

Routage et adressage :

- Adresse IP : Contient des informations sur le réseau d'origine et le réseau de destination, permettant aux routeurs de décider où envoyer les paquets pour atteindre la destination finale, y compris à travers plusieurs réseaux.
    
- Adresse MAC : Limité à la communication locale et ne peut pas être utilisée pour le routage entre réseaux.
    

Structure hiérarchique :

- Adresse IP : A une structure hiérarchique (partie réseau et partie hôte), facilitant la gestion et le routage efficace des paquets sur Internet.
    
- Adresse MAC : Est unique pour chaque appareil, mais sans structure hiérarchique, rendant le routage complexe.