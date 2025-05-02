  
  

### Résumé des Opérations de la Couche Réseau

1. Adressage des Terminaux : Chaque terminal doit avoir une adresse IP unique.
    
2. Encapsulation : La couche réseau encapsule les données avec des en-têtes IP contenant les adresses source et destination.
    
3. Routage : Les routeurs dirigent les paquets vers l'hôte de destination en choisissant le meilleur chemin.
    
4. Désencapsulation : L'hôte de destination vérifie et retire l'en-tête IP pour accéder aux données.
    

  
  

8.1.2 Encapsulation IP 

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfm6PTHR4X--jBlw8LAWCh08gXoBWnrbWbeAfwjnhfrDsx5f1Xc6QZDozw2t1NPOgXFDu970SvWsillebAP_y9xm3c3gpOJBaLY2qGIXfkvvIrtp4Ec0PPx8ORg-AqjBgIdHxKC?key=MnEOEuxM8Yq9frXcYCJvzYNs)

  

Encapsulation : L'IP ajoute un en-tête au segment de la couche transport pour créer un paquet IP.

Rôle de l'En-tête IP : Cet en-tête est essentiel pour acheminer le paquet vers l'hôte de destination.

Création du Paquet IP : La PDU de la couche transport est encapsulée dans la PDU de la couche réseau.

  

Encapsulation : Permet aux couches de se développer sans affecter les autres, encapsulant les segments de couche transport avec IPv4, IPv6, ou de futurs protocoles.

Examen de l'en-tête IP : Les routeurs et commutateurs de couche 3 vérifient les en-têtes IP pour acheminer les paquets.

Adresse IP : Les adresses IP restent constantes sauf en cas de NAT.

Routage : Les routeurs utilisent des protocoles de routage basés sur les en-têtes IP sans modifier les données encapsulées (comme l'UDP).

  
  

8.1.3 Caractéristiques du protocole IP 

8.1.4 Sans connexion 

  
  

Sans Connexion : L'IP n'établit pas de connexion dédiée avant l'envoi des données.

Analogies : Comparable à envoyer une lettre sans prévenir le destinataire.

Principe : Aucune connexion dédiée n'est établie avant l'envoi des paquets.

Transmission Directe : IP envoie les paquets directement sans échange préalable d'informations de contrôle.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfA3-lKqJQPlWQb3Vm5gIexKVjAxygVEmSxIBSZnG9sEvIDTtkK2-8ncSS1krtkbJ8JpzHQ8sPnyKIpbm_Un2IZk7AjuyZ53BYguOlgjKEUFTkifFpk3z04K8bKjPnw7A2RKwbLhA?key=MnEOEuxM8Yq9frXcYCJvzYNs)

  
  

### Sans connexion - Réseau

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeKuumJdZTxKC3OipwgIaYy56ee-WHyif3rR7dc9mY9GG6f-mBlmLda8TBt-pRLj0PNeNNhXScXfRwLtTl6tq6OiJG75y4HxlIQetAcKmhVxPYmhV0_YmaHrpxoP0a1R4aUEOws7g?key=MnEOEuxM8Yq9frXcYCJvzYNs)

  
  
  
  
  

### Résumé de la Remise au Mieux (Best Effort)

- Sans Champs Supplémentaires : IP ne nécessite pas de champs pour maintenir une connexion, réduisant ainsi la surcharge.
    
- Absence de Garantie : Les expéditeurs ne savent pas si les paquets sont reçus par la destination.
    
- Acheminement Non Fiable : IP ne garantit pas la réception de tous les paquets envoyés.
    
- Protocoles Complémentaires : D'autres protocoles assurent le suivi et la livraison des paquets.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcHyrP_YS2sPEE8c9v9MnOs156Xaaw2GrHkK2pFZ2U1hb5TVlFdJ-lOeDdx3MKSG0TrZy9G2eXp42TrXqWwGRZ2rKFpG5pQ3qgd20FlwZmAPooNIxQ04shP67FVoyr9Ju0NXqnd?key=MnEOEuxM8Yq9frXcYCJvzYNs)

  
  

### Résumé : Indépendant du Support

- Non Fiable : IP ne gère pas les paquets endommagés ou non remis. Les applications ou services de couche supérieure doivent résoudre ces incidents.
    
- Efficacité : L'indépendance des supports rend le protocole IP très efficace.
    
- Support Multiple : IP peut fonctionner sur différents supports (cuivre, fibre optique, sans fil).
    
- MTU : Chaque support a une unité de transmission maximale (MTU) définissant la taille maximale des paquets.
    
- Fragmentation : Les routeurs peuvent fragmenter les paquets IPv4 pour les adapter à une MTU plus petite, ce qui peut provoquer une latence. IPv6 ne permet pas la fragmentation par les routeurs.
    

  

where is all of thi :8.2.1 En-tête de paquet IPv4 IPv4 est l'un des protocoles principaux de communication de la couche réseau. L'en-tête de paquet IPv4 est utilisé pour s'assurer que ce paquet est livré à son prochain arrêt sur le chemin de son périphérique final de destination. Un en-tête de paquet IPv4 est constitué de champs contenant des informations importantes sur le paquet. Ces champs contiennent des nombres binaires, examinés par le processus de couche 3. 8.2.2 Champs d'en-tête des paquets IPv4 Les valeurs binaires de chaque champ indiquent divers paramètres du paquet IP. Les diagrammes d'en-tête de protocole, qui sont lus de gauche à droite et de haut en bas, fournissent un visuel auquel se référer lors de la discussion des champs de protocole. Le schéma d'en-tête de protocole IP présenté dans cette figure identifie les champs d'un paquet IPv4.

## Résumé : En-tête de Paquet IPv4 et ses Champs

#### 8.2.1 En-tête de Paquet IPv4

- Protocole Principal : IPv4 est essentiel pour la communication de la couche réseau.
    
- Rôle de l'En-tête : S'assurer que le paquet atteint son prochain arrêt en route vers la destination finale.
    
- Composition : Contient des champs avec des informations importantes sous forme de nombres binaires.
    

#### 8.2.2 Champs d'En-tête des Paquets IPv4

- Valeurs Binaires : Indiquent divers paramètres du paquet IP.
    
- Diagramme d'En-tête : Fournit un visuel des champs de protocole IP, lu de gauche à droite et de haut en bas.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcH_LICgQ8WsWx1sYGmEWjfs9daaLeVByCeLov8cK0muMU2bq9Ls8YKx16Xyz2oFGkmVyNQLUfLOuhikZCXuEehdEmXfbJYbmKTOZLRZiZ59c9sW8ZobW6UYIDoiEMHdLRb4rAP?key=MnEOEuxM8Yq9frXcYCJvzYNs)

### Champs Importants de l'En-tête IPv4

- Version : 4 bits pour identifier le paquet IPv4 (0100).
    
- DiffServ (DS) : 8 bits pour la priorité du paquet (inclut DSCP et ECN).
    
- TTL (Time to Live) : 8 bits pour limiter la durée de vie d'un paquet, décrémenté par chaque routeur.
    
- Protocole : 8 bits pour identifier le protocole de niveau supérieur (ICMP, TCP, UDP).
    
- Somme de contrôle de l'en-tête : Utilisée pour détecter la corruption de l'en-tête IPv4.
    
- Adresse IPv4 source : 32 bits représentant l'adresse de l'expéditeur.
    
- Adresse IPv4 de destination : 32 bits représentant l'adresse du destinataire (monodiffusion, diffusion, ou multidiffusion).
    

  

#### Champs les plus utilisés

- Adresses IP Source et Destination : Indiquent l'origine et la destination du paquet. Ces adresses ne changent pas pendant le trajet.
    

#### Identification et Validation du Paquet

- IHL (Internet Header Length), Longueur Totale, Somme de contrôle de l'en-tête : Identifient et valident le paquet.
    

#### Remise en Ordre des Paquets Fragmentés

- Champs Identification, Indicateurs, Décalage du Fragment : Suivent les fragments d'un paquet IPv4. Utilisés lorsque le paquet doit être fragmenté pour s'adapter à une MTU plus petite.
    

#### Champs Rares

- Options et Padding : Utilisés rarement, pas couverts dans ce module
    

  
  

#### 8.3.1 Limites du Protocole IPv4

1. Épuisement des adresses IPv4
    

- Nombre limité d'adresses publiques (environ 4 milliards).
    
- Augmentation des périphériques IP et des connexions permanentes.
    

1. Manque de connectivité de bout en bout
    

- Utilisation de la NAT masque les adresses internes.
    
- Problème pour les technologies nécessitant une connectivité directe.
    

1. Complexité du réseau
    

- NAT ajoute de la complexité et de la latence.
    
- Dépannage plus difficile.
    

#### 8.3.2 Aperçu d'IPv6

1. Espace d'adressage accru
    

- Adressage de 128 bits (IPv6) vs 32 bits (IPv4).
    
- IPv6 offre 340 undecillions d'adresses uniques.
    

1. Amélioration du traitement des paquets
    

- En-tête simplifié avec moins de champs.
    

1. Élimine le besoin de NAT
    

- Nombre d'adresses publiques suffisant pour éviter la NAT.
    
- Facilite la connectivité de bout en bout.
    

  
  

### Comparaison des espaces d'adressage IPv4 et IPv6

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfrgfDOfmbJnE4Jlwn5Bp916hn7fcjo_0IV910hqgy3W5fMuRhXjcrTsDDHYU4fx6h9P-KOY9ic_VtlJeyNsW3OJjwD93I18YsTe3HJYV4Xs0YE5PPvoOO4-4wmZw2-nnEi2ng1Ng?key=MnEOEuxM8Yq9frXcYCJvzYNs)

  

#### Simplification de l'En-tête IPv6

- En-tête IPv4 : Longueur variable (20 à 60 octets), avec 12 champs de base, champs Options et Padding.
    
- En-tête IPv6 : Longueur fixe de 40 octets, simplifié pour un traitement plus efficace.
    

### En-tête de paquet IPv4

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe0JigG2SN7yEll6HVGIh8GufO5S08Nkg8wtk6VlURF0YEUHxsM1VUsoyWysBDqjShU1CbeAqGoCyXJjU9ipHdLPH7u-OvuPcNf2Mb92ONA9BzV8kTt3XgeOvE0kRHWr2flr_6f?key=MnEOEuxM8Yq9frXcYCJvzYNs)  
  

### En-tête de paquet IPv6

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdcyelmijKh3xDakYudYQCY_AUY86qqG24NpEOy4RItufDkq_Gh9J7tazEGL6jXzL_18QUKrJMd2NflDd4QJ4qvGFFH3SspEuSAKO0am_YPNHdDD5LXQ79044p5urzzw9RsAyCwCQ?key=MnEOEuxM8Yq9frXcYCJvzYNs)

Version

- 4 bits : Fixé à 0110 pour identifier le paquet comme IPv6.
    

Classe de trafic

- 8 bits : Équivalent au champ DiffServ (DS) d'IPv4, détermine la priorité du paquet.
    

Étiquette de flux

- 20 bits : Tous les paquets avec la même étiquette de flux reçoivent le même traitement par les routeurs.
    

Longueur de la charge utile

- 16 bits : Indique la longueur des données utiles du paquet IPv6 (sans inclure les 40 octets de l'en-tête fixe).
    

En-tête suivant

- 8 bits : Équivalent au champ du protocole d'IPv4, identifie le type de données utiles transportées.
    

  
  

Limite de saut

- 8 bits : Remplace le champ TTL d'IPv4, réduit d'un point par chaque routeur. Lorsque la valeur atteint zéro, le paquet est rejeté et un message ICMPv6 Time Exceeded est envoyé.
    

Adresse IPv6 source

- 128 bits : Identifie l'adresse IPv6 de l'hôte expéditeur.
    

Adresse IPv6 de destination

- 128 bits : Identifie l'adresse IPv6 de l'hôte récepteur.
    

  

### Résumé : En-têtes d'Extension IPv6

- En-têtes d'Extension
    

- Fonction : Fournissent des informations facultatives pour la couche réseau.
    
- Emplacement : Placés entre l'en-tête IPv6 et les données utiles.
    
- Utilisation : Fragmentation, sécurité, prise en charge de la mobilité, etc.
    

- Fragmentation
    

- IPv6 : Les routeurs ne fragmentent pas les paquets IPv6 routés, contrairement à IPv4.
    

  

8.4.1 Décisions de transmission

Avec IPv4 et IPv6, les paquets sont créés sur l'hôte source, qui doit diriger le paquet vers l'hôte de destination en utilisant des tables de routage.

La couche réseau gère la livraison des paquets vers différents hôtes :

- Vers soi-même : Un hôte peut s'envoyer un ping à 127.0.0.1 (IPv4) ou ::1 (IPv6) sur l'interface de bouclage, pour tester la pile TCP/IP.
    
- Hôte local : Un hôte de destination sur le même réseau que l'hôte source, partageant la même adresse réseau.
    
- Hôte distant : Un hôte de destination sur un réseau différent. Les adresses source et destination sont de réseaux distincts.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeU5vmVkeR_zjURZeygHZKcEBkm1oV_QpRXa8qMHh988BRE90_yCgLbcigKCHgSOoYNuiAA8tWB7l91jEaRqJjX_FbxzQHgyQGRZfzm38nytGb_jB9LioZr7v48lXE5ADIFZ5aXhQ?key=MnEOEuxM8Yq9frXcYCJvzYNs)

Figure : Connexion de PC1 à un hôte local sur le même réseau et à un hôte distant sur un autre réseau.

Pour déterminer si une destination est locale ou distante :

- IPv4 : Le périphérique source utilise son masque de sous-réseau, sa propre adresse IPv4 et l'adresse IPv4 de destination.
    
- IPv6 : Le routeur local annonce le préfixe réseau aux périphériques du réseau.
    

Dans un réseau domestique ou d'entreprise, les dispositifs sont interconnectés par un commutateur LAN ou un point d'accès sans fil(WAP), permettant aux hôtes locaux de communiquer sans dispositifs supplémentaires. Si le destinataire est sur le même réseau IP, le paquet est transmis directement via le dispositif intermédiaire.

Pour les connexions au-delà du réseau local (comme l'Internet), les hôtes distants nécessitent des routeurs pour le routage. Le routeur local agit comme passerelle par défaut pour déterminer le meilleur chemin vers la destination.

---

8.4.2 Passerelle par défaut 

La passerelle par défaut est le dispositif réseau (souvent un routeur) qui permet d’acheminer le trafic vers d’autres réseaux. Elle fonctionne comme une porte entre différents réseaux, permettant de "sortir" du réseau local.

Caractéristiques d’une passerelle par défaut :

- Elle a une adresse IP locale qui correspond à celle des autres hôtes du réseau.
    
- Elle peut recevoir des données du réseau local et les transmettre vers l'extérieur.
    
- Elle dirige le trafic vers d’autres réseaux.
    

La présence d'une passerelle par défaut est essentielle pour l'envoi de trafic en dehors du réseau local. Sans elle, le trafic ne peut quitter le réseau, que ce soit en raison d’une absence de configuration ou d’une panne de la passerelle.

  
  

8.4.3 Utilisation de la passerelle par défaut par un hôte

La table de routage d'un hôte inclut généralement une passerelle par défaut pour accéder aux réseaux distants.

- En IPv4 : L'adresse de la passerelle par défaut est soit obtenue automatiquement par le protocole DHCP, soit configurée manuellement.
    
- En IPv6 : Le routeur annonce l'adresse de la passerelle, ou elle peut être configurée manuellement.
    

Quand une passerelle par défaut est configurée, une "route par défaut" apparaît dans la table de routage du PC, indiquant le chemin à suivre pour atteindre les réseaux distants.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfm0IrI8oKZS9piPOfHTKGWSm8wPVypCeX2Qfq7GQliK0zopkBApTb4BBXeTSh2LEJrmBBKhmjyGtLd4ODA9A_e7-44WxATN2YrI5RqVJeO3qcGji77enVDEwjc8ktSaN55IkDSUQ?key=MnEOEuxM8Yq9frXcYCJvzYNs)

  

Figure : PC1 et PC2 configurés avec l’adresse 192.168.10.1 comme passerelle par défaut pour envoyer le trafic via R1 vers les réseaux distants.

Voici un résumé pour 8.4.4 - Tables de routage des hôtes :

  
  

8.4.4 Tables de routage des hôtes

  

Sur un hôte Windows, les commandes route print ou netstat -r permettent d’afficher la table de routage, fournissant des informations sur les connexions réseau.

  
  
  
  
  
  
  

Figure : Exemple de sortie de la commande netstat -r montrant la table de routage IPv4 pour PC1.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeMOvWrNgdLcAfKUW5vK_ZrgKMR4zqkY3ZIx_6fKuV2XvYMRtSHokO7MD3xGbXLcB3nLjc5a-rx-d1VOl6n7NfEWfEFguODaW03N5BKC999Rb7GfK9kNIRAa9ktpiX_u5It7RjwGw?key=MnEOEuxM8Yq9frXcYCJvzYNs)

### Table de routage IPv4 pour PC1

C:\Users\PC1> netstat -r

Table de routage IPv4

===========================================================================

Routes actives :

Destination réseau Masque réseau Passerelle Interface Métrique

          0.0.0.0 0.0.0 192.168.10.1 192.168.10.10 25

        127.0.0.0 255.0.0.0 On-link 127.0.0.1 331

        127.0.0.1 255.255.255.255 On-link 127.0.0.1 331

  127.255.255.255 255.255.255.255 On-link 127.0.0.1 331

  192.168.1.0 255.255.255.0 On-link 192.168.1.5 281

    192.168.1.5 255.255.255.255 On-link 192.168.1.5 281

   192.168.1.255 255.255.255.255 On-link 192.168.1.5 281

        224.0.0.0 240.0.0.0 On-link 127.0.0.1 331

        224.0.0.0 240.0.0.0 On-link 192.168.1.5 281

  255.255.255.255 255.255.255.255 On-link 127.0.0.1 331

  255.255.255.255 255.255.255.255 On-link 192.168.1.5 281

  

La table de routage comprend trois sections principales :

  

    Liste des interfaces : Affiche l’adresse MAC et le numéro d’interface pour chaque carte réseau de l’hôte, y compris les adaptateurs Ethernet, Wi-Fi et Bluetooth.

    Table des routes IPv4 : Contient toutes les routes IPv4 connues, incluant les connexions directes, les réseaux locaux et les routes par défaut.

    Table des routes IPv6 : Affiche toutes les routes IPv6 connues avec les connexions directes, locales et par défaut.

8.5.1 Décisions de transmission des paquets par le routeur

Les routeurs, comme les hôtes, possèdent des tables de routage. Lorsqu'un hôte envoie un paquet vers un réseau distant, il l'envoie à la passerelle par défaut, souvent le routeur local.

Quand un paquet arrive sur une interface de routeur :

1. Le routeur examine l'adresse IP de destination du paquet et consulte sa table de routage pour déterminer le chemin de transmission.
    
2. La table de routage contient des adresses réseau connues(préfixes) et les meilleures routes pour les atteindre.
    
3. Le routeur sélectionne l’entrée d’itinéraire la plus appropriée pour transmettre le paquet.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeXAkKRHKq6FvAmfHcK60oFcEK8wv-NJQzIhQRpIwC-FUjDE4sfjkhlGUtVRjhXK6Qgg2AqnB3ZVX3kQH8ABc0bzrtngeXeo3-a1HZ7dG2CH4ZtZwCJIri5Xi3mRuBR6rZ_Vl8a?key=MnEOEuxM8Yq9frXcYCJvzYNs)

  

Exemple : Le paquet arrive sur l'interface du routeur R1. Après vérification de la destination, R1 décide de transmettre le paquet au routeur R2. R1 encapsule alors le paquet dans un nouvel en-tête Ethernet et le transmet à R2.

Figure : Table de routage de R1.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfcJMwEpqs_x3Mnb3kFqnguWArS_UYPBpZpLEYMBV_cvkSEO-nKsTTFn2NFlyrerrGhywHZmrE28IV1_qAn6ZEUNgYtctkcwKQSXnAzaXEwsv90CYe4fHdETH7TfM_cMQY74kZCbQ?key=MnEOEuxM8Yq9frXcYCJvzYNs)

  
  

8.5.2 Table de routage du routeur IP

  

La table de routage d'un routeur répertorie toutes les destinations réseau connues, avec trois types d'entrées principales :

  

    Réseaux directement connectés : Ce sont les interfaces actives configurées avec une adresse IP. Par exemple, sur R1, les réseaux directement connectés sont 192.168.10.0/24 et 209.165.200.224/30.

    Réseaux distants : Ce sont les réseaux connectés via d’autres routeurs. Ils peuvent être configurés manuellement par un administrateur ou appris par des protocoles de routage dynamique. Sur R1, le réseau distant est 10.1.1.0/24.

    Route par défaut : Comme pour un hôte, le routeur utilise une route par défaut en l’absence de correspondance dans la table. R1 peut ainsi transmettre tout le trafic inconnu au routeur R2.

  

Figure : Table de routage de R1 montrant les réseaux directement connectés et les réseaux distants.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc83pQIf8tIm4T58gmha8ZBj9vchFFcbFSp4DOGTM4fHdXkpuUDfKVE7xiI6ZaUWskh6hAbRaWrdY0kZRFADBO5gkZ8Tjolk145JTwMfi5MmacdpSOSCvTjM5Gd8aq6Iqufve567w?key=MnEOEuxM8Yq9frXcYCJvzYNs)

  

n routeur peut apprendre des réseaux distants de deux manières différentes :

- Manuellement - Les réseaux distants sont entrés manuellement dans le tableau des itinéraires en utilisant des itinéraires statiques.
    
- Dynamiquement - Les itinéraires à distance sont automatiquement appris en utilisant un protocole de routage dynamique.
    

Voici le résumé pour 8.5.3 - Routage statique :

  
  

8.5.3 Routage statique

Les itinéraires statiques sont des routes configurées manuellement par un administrateur, incluant l'adresse réseau distante et l'adresse IP du routeur suivant.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdg-zCM0Cg38GxdZYNjLCrIceTATHQivvH-jhuAJOF-63__iDUbTGLu1BN_crxjdOvx65h5UEU6jO0KDf_Y4JAwlUkFotSjfcEvOsLc3eKEj993BCTSJjkyn-qjcbqU20uFvM-VvA?key=MnEOEuxM8Yq9frXcYCJvzYNs)

- Exemple : R1 a une route statique vers le réseau 10.1.1.0/24 via R2. Si ce chemin devient indisponible, R1 doit être reconfiguré avec une nouvelle route vers 10.1.1.0/24, mais via R3.
    
- Le routeur R3 devra également avoir une entrée dans sa table de routage pour envoyer les paquets destinés à 10.1.1.0/24 vers R2.
    

Note : La modification de la topologie ne met pas automatiquement à jour les routes statiques, elles doivent être reconfigurées manuellement.

  
  
  
  

Figure : Exemple de modification de la route statique sur R1.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd_LYxLvAunCrku_Uq3WYcTZAIOTKbRNAiDVEq9u9XLllu6M3uyMzIA8IoNI5JirAmCfmr-66eNIEp0V5GHVOUd77ACeKVGrym__-abr78zybkJ06So7Epwy_e5IyCRN_r0md18Ug?key=MnEOEuxM8Yq9frXcYCJvzYNs)

Le routage statique présente les caractéristiques suivantes :

- Une route statique doit être configurée manuellement.
    
- L'administrateur doit reconfigurer une route statique s'il y a une modification de la topologie et si la route statique n'est plus viable.
    
- Un itinéraire statique est approprié pour un petit réseau et lorsqu'il y a peu ou pas de liaisons redondantes.
    
- Une route statique est couramment utilisée avec un protocole de routage dynamique pour configurer une route par défaut
    

Voici le résumé pour 8.5.4 - Routage dynamique :

  
  

8.5.4 Routage dynamique

  

Un protocole de routage dynamique permet aux routeurs d'apprendre automatiquement des réseaux distants et de mettre à jour leurs tables de routage, y compris les itinéraires par défaut. Ces protocoles partagent des informations de routage entre les routeurs et réagissent aux modifications de la topologie sans nécessiter d'intervention manuelle.

  

    Exemples de protocoles de routage dynamique : OSPF et EIGRP (Enhanced Interior Gateway Routing Protocol).

    Lorsque la topologie du réseau change, les routeurs mettent à jour leurs tables de routage en partageant automatiquement les nouvelles informations via le protocole de routage dynamique.

  

Figure : Exemple de partage d'informations entre R1 et R2 via OSPF.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeNIrjMrDxOSAOQqy2S0GLxpK6a222qwErMcqe0Hfnp5kKGnozJHuB740Q4GuF0TRbymutwO0agyvJgxi-TxdswAv-hTnzX6J9h0mJpbdqmpx2KUTYNetK6HovHTcMOLJEObuxxuA?key=MnEOEuxM8Yq9frXcYCJvzYNs)

8.5.4 Routage dynamique (suite)

La configuration de base d'un protocole de routage dynamique consiste uniquement à activer les réseaux directement connectés. Le processus se déroule automatiquement comme suit :

1. Découverte des réseaux distants.
    
2. Actualisation des informations de routage.
    
3. Sélection du meilleur chemin vers les réseaux de destination.
    
4. Capacité de trouver un nouveau meilleur chemin si le chemin actuel devient indisponible.
    

Lorsqu'un routeur apprend dynamiquement un réseau distant, il ajoute l'adresse réseau et l'adresse du saut suivant dans sa table de routage. En cas de changement dans la topologie, les routeurs ajustent automatiquement leur routage et cherchent un nouveau chemin optimal.

  
  
  

Figure : Exemple de mise à jour automatique de la table de routage après un changement de topologie.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfO7ERDZ1imYKOqBJyRHsBYp9BhTk_OxQnJcKCBCA2mA-MjskCjwwu4lxWbfiXk1-0z2F_xoLtW7nAZKCrwp1-cpLsJOSxVpWVWEjAYdRAfcn05d8LE3pzv5W8LcZHvlIlpMPbq?key=MnEOEuxM8Yq9frXcYCJvzYNs)

  

8.5.6 Introduction à une table de routage IPv4 

Notez dans la figure que R2 est connecté à Internet. Par conséquent, l'administrateur a configuré R1 avec une route statique par défaut envoyant des paquets à R2 lorsqu'il n'y a aucune entrée spécifique dans la table de routage qui correspond à l'adresse IP de destination. R1 et R2 utilisent également le routage OSPF pour annoncer les réseaux directement connectés.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfhVbC9z27jf5R4WM3GsIp5YO0NBj6lSLeybFR3Z6yJECSh7m6sZ8-t3zSDVAwTypWMSo_M4OcCzAehiysi8ubEJNHFkue98ngnwR_ew0zsP7G36dbDWSxc1odiETH8Wtm_1S1GAg?key=MnEOEuxM8Yq9frXcYCJvzYNs)

  
  

La commande show ip route en mode EXEC privilégié est utilisée pour afficher la table de routage IPv4 sur un routeur IOS Cisco. Voici un exemple de la sortie de cette commande ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXddp4LN9RxJBfnNn1p6ov26a4y8QkdbuaQK2peX8LDNNyxpQi7cQhMbiegjzttdbk6ShCEMuu1zwe-Y6jTJsy4SW4t36BoJlQzgA4gBb2ofcfT4A9JxaDSt3hREbEoiG9DuRAuzZw?key=MnEOEuxM8Yq9frXcYCJvzYNs)sur le routeur R1 :

- L - Adresse IP de l'interface locale directement connectée
    
- C - Réseau directement connecté
    
- S - La route statique a été configurée manuellement par un administrateur
    
- O - OSPF
    
- D - EIGRP
    

La table de routage de R1 contient les routes vers les réseaux connus. Les routes directement connectées sont créées automatiquement lorsque les interfaces de routeur sont configurées avec une adresse IP. Chaque interface ajoute deux entrées : C pour le réseau connecté et L pour l'adresse IP locale. Les réseaux directement connectés dans cet exemple sont 192.168.10.0/24 et 209.165.200.224/30.

Les routeurs R1 et R2 utilisent OSPF pour échanger des informations de routage. R1 apprend dynamiquement le réseau 10.1.1.0/24 de R2 via OSPF.

Un itinéraire par défaut, identifié par l'adresse 0.0.0.0, est configuré pour les paquets dont la destination n'est pas spécifiée dans la table de routage. Une route statique est marquée par un code S*.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdFBm-_AgIy_EkmeT8nnNe2dmLsaL0dpQ7j2R1vdTHMzK-40wmGCbe_nXJkOzefgETIeLR7ZLCCaqvF6ulXq6C-SRm7KJBjoFYelqafYevLxmzJg-J3Yx8zOvLVCKSn9-f3tn08sQ?key=MnEOEuxM8Yq9frXcYCJvzYNs)

  

La métrique d'une route est un facteur qui détermine le "coût" ou l'efficacité d'une route dans un protocole de routage. Plus la valeur de la métrique est faible, plus la route est considérée comme optimale par le routeur. Par exemple, un protocole comme RIP (Routing Information Protocol) utilise le nombre de sauts comme métrique, tandis que d'autres protocoles comme OSPF ou EIGRP peuvent utiliser des critères différents comme la bande passante ou la latence.

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXffQh-pRlC0LgziZWL2fHBbVW2CwheDj6-bLp2mdIQce7ojSU7z7SkhGb2HyiZVmBsRASCR6Hkzn4r4wCiTjiIPIfY9KJzs7QiO6JqxCuS29JQDSq0W8ejhoOyspzorOZR7wPVQSA?key=MnEOEuxM8Yq9frXcYCJvzYNs)

  
  

0x806 : indique que Le type est ARP

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe-nZKzlHwsqr4UAe187YTCdfeR4mo6mn9pw6ju2Z9Cc2j7fem-AxXAkLOb1j1fr8bDh0SUkUT6DIKthkcgYcFyquLskTlAsW2COmJm9Ayxr7ZmOfhhWqOQZy8-LMkZwcC_e4W2Vg?key=MnEOEuxM8Yq9frXcYCJvzYNs)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXchhKiqzmuQDav-lkNLe2AAW8DpzAHX2D7aEiy6dgvcRCbf3Bbnmvsurges3qW4RdMAOiAgku9hCegZz6LkQuGNhfOYLxtGG5wmdRHjsOUWuhqv9MO4ikyCplAJNmRT1cDaUZo_1Q?key=MnEOEuxM8Yq9frXcYCJvzYNs)