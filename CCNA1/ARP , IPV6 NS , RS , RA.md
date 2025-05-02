Le module 9.0 présente la résolution d'adresse, qui permet de résoudre une adresse logique (IP) en une adresse physique (MAC) sur un réseau local.

### 9.1.1 Destination sur le même réseau

Lorsqu'un hôte doit envoyer un message mais ne connaît que l'adresse IP de destination, il doit résoudre l'adresse MAC correspondante. Cela est essentiel pour la communication sur un réseau local (LAN).

Chaque périphérique sur un LAN Ethernet possède deux adresses principales :

- Adresse MAC (physique) : Utilisée pour la communication entre les cartes réseau sur le même réseau.
    
- Adresse IP (logique) : Utilisée pour acheminer les paquets d'une source vers la destination finale, qu'elle soit sur le même réseau ou non.
    

Les adresses physiques de couche 2 (c'est-à-dire les adresses MAC Ethernet)  permettent de transmettre des trames de données sur le même réseau. Si l'adresse IP de destination est sur le même réseau, l'adresse MAC de destination est utilisée pour acheminer la trame vers le périphérique cible.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf1xXnpvunZ65F_og3TQAmngTJyYVRkTPn7YE13JTguRwE9Yl53Nwn1U4bpbz8qp85h53oLFxunwdFwk_VDOQs4baYMKUE3wqRdI81-R1VkNUlJhu93Wyxtx03z0U56Mt6gvBT5?key=__1V76Yhrj3VZz251M-d5cHn)

  

Dans cet exemple, PC1 envoie un paquet à PC2. Le paquet contient les informations suivantes :

- Trame Ethernet (couche 2) :
    

- Adresse MAC de destination : 55-55-55 (adresse de PC2)
    
- Adresse MAC source : aa-aa-aa (adresse de PC1)
    

- Paquet IP (couche 3) :
    

- Adresse IPv4 source : 192.168.10.10 (adresse de PC1)
    
- Adresse IPv4 de destination : 192.168.10.11 (adresse de PC2)
    

Cela illustre comment les informations des couches 2 et 3 sont combinées pour acheminer les données entre les deux périphériques sur le même réseau.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdDSYNODiTZSNiE_Fd1bp10MYsOPqc5orDG08KKiy_19XtAEHxG0am7DGQykGqx_biqUKDsNufsd-0O8J1l4h56F60bKXE0osy_9EXvSXEQX5b44-hoc8yVZqZR3Z4RYDkMyJ8Rlg?key=__1V76Yhrj3VZz251M-d5cHn)

Dans cet exemple, PC1 veut envoyer un paquet à PC2, mais PC2 se trouve sur un réseau distant. L'adresse MAC de destination sera celle de la passerelle par défaut (le routeur), car l'adresse IPv4 de destination n'est pas sur le même réseau local que PC1.

Voici comment le processus se déroule :

1. PC1 envoie la trame à la passerelle par défaut (routeur), dont l'adresse MAC est utilisée comme destination.
    
2. Routeur R1 reçoit la trame et décapsule les informations de la couche 2 (Ethernet). Ensuite, R1 examine l'adresse IP de destination pour déterminer le meilleur chemin pour acheminer le paquet.
    
3. Le routeur encapsule à nouveau le paquet dans une nouvelle trame Ethernet avec de nouvelles informations de couche 2 adaptées à l'interface de sortie.
    

Ce processus permet au paquet d'être redirigé vers le réseau distant en utilisant la passerelle par défaut pour atteindre le routeur, qui poursuivra l'acheminement vers PC2.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfZpiw_BfR5KJq3uJCKyNle08ZpzTHkDmQvGz6QWCctl-8ApIUcV1Eyj95QM6SQNfnVb3Tx6SWSC06JUybcRxHfN83oLr9SWI-6sMXNu-LvAf1I3w0LGfiV8y9IrMHPAQcvHefQHQ?key=__1V76Yhrj3VZz251M-d5cHn)

  
  

Lorsque le paquet traverse le réseau :

1. R1 met à jour l'adresse MAC de destination avec celle de R2 G0/0/1 et l'adresse MAC source avec celle de R1 G0/0/1.
    
2. À chaque étape, le paquet est encapsulé dans une trame spécifique à la technologie de la liaison de données (comme Ethernet).
    
3. Si la destination finale est atteinte, l'adresse MAC de destination est celle de la carte réseau du périphérique destinataire.
    

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdq-GC03TYyrUs8nBtAfCdn6TEpH8_UmJV0ZNNK2P40HBNyC8CHJQ_DMGBfQXTAwSR76kwfPYlS3x_sATmQp9KNVoAqLKIzZdx6lduv3ECbh4-RcENo1VIEMF4kkmtQLdkqbHbGtA?key=__1V76Yhrj3VZz251M-d5cHn)

Comment les adresses IP des paquets IP d'un flux de données sont-elles associées aux adresses MAC de chaque liaison le long du chemin vers la destination ? Cette opération est effectuée selon un processus appelé protocole ARP. Pour les paquets IPv6, le processus est ICMPv6 Neighbor Discovery (ND).

  

### 9.2.1 Présentation ARP

Le protocole ARP (Address Resolution Protocol) est utilisé pour mapper les adresses IPv4 aux adresses MAC sur un réseau Ethernet. Voici comment il fonctionne :

- Adresse MAC de destination : Adresse MAC du périphérique cible sur le même réseau local. Si l'hôte est sur un autre réseau, c'est l'adresse MAC de la passerelle par défaut (routeur).
    
- Adresse MAC source : Adresse MAC de l'expéditeur (carte réseau Ethernet).
    

ARP résout le problème lorsqu'un hôte veut envoyer une trame à un autre hôte sur le même segment de réseau IPv4, mais ne connaît pas l'adresse MAC de la destination.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe0kU2nsLEy7LJQBGf2RKNDIcB_uu0wwRFX08VgaZNxNrh7pnbFcE5zC65yUV8gpT9PTVoJaohZWNuy4lCe_Hy1ROH88v6Z34VRwB9kegVCkcf_4UB7KifIYayNnzHNOQkB0rU5vw?key=__1V76Yhrj3VZz251M-d5cHn)

  
  

### Fonctionnement d'ARP

Pour envoyer un paquet à un autre hôte sur le même réseau IPv4, un hôte doit connaître à la fois l'adresse IPv4 et l'adresse MAC du périphérique de destination. L'adresse IPv4 est généralement connue ou résolue par nom, mais l'adresse MAC doit être découverte.

Le protocole ARP remplit deux fonctions principales :

1. Résolution des adresses IPv4 en adresses MAC : ARP permet de découvrir l'adresse MAC correspondant à une adresse IPv4 locale.
    
2. Maintien du tableau de mappages IPv4 vers MAC : ARP garde une table pour associer les adresses IPv4 aux adresses MAC correspondantes.
    

### Fonctions du protocole ARP

Lorsque le périphérique souhaite envoyer un paquet, il consulte sa table ARP (ou cache ARP), stockée temporairement dans la mémoire RAM, pour trouver l'adresse MAC correspondant à une adresse IPv4.

Voici les étapes :

1. Si l'adresse IPv4 de destination est sur le même réseau que l'adresse source, le périphérique recherche directement dans la table ARP.
    
2. Si l'adresse IPv4 de destination est sur un autre réseau, il cherche l'adresse de la passerelle par défaut dans la table ARP.
    

Chaque entrée de la table ARP associe une adresse IPv4 à une adresse MAC. Si l'entrée est trouvée, l'adresse MAC correspondante est utilisée comme destination dans la trame. Sinon, une requête ARP est envoyée pour découvrir l'adresse MAC.

  

### Requête ARP

Lorsqu'un périphérique ne trouve pas l'adresse MAC correspondante dans sa table ARP pour une adresse IPv4, il envoie une requête ARP. Voici comment cela fonctionne :

- Encapsulation : La requête ARP est encapsulée directement dans une trame Ethernet sans en-tête IPv4.
    

- Adresse MAC de destination : Diffusion (adresse de diffusion) pour que tous les périphériques du LAN traitent la requête ARP.
    
- Adresse MAC source : Adresse MAC de l'expéditeur de la requête ARP.
    
- Type : 0x806, indiquant qu'il s'agit d'un message ARP.
    

- Transmission : Comme la requête ARP est une diffusion, elle est envoyée à tous les ports du commutateur sauf le port récepteur. Tous les périphériques du LAN traitent la requête ARP.
    
- Réponse : Seul le périphérique possédant l'adresse IPv4 cible répond à la requête ARP. Les autres périphériques ignorent la requête.
    

Les routeurs ne transmettent pas les diffusions ARP par d'autres interfaces.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfY8TQkoL02rXwV16tqZAR7tLbCNYlVj2f0BVC1NZSs9gdGGviy3foIJf1G_xmBzaTS08LkMu3tnTzTjSAV_mJh1FGL4dk25dreNeadRTGCvUFnhsKUb_huPcGIXGQgmfPq_7PsJQ?key=__1V76Yhrj3VZz251M-d5cHn)

  

### Réponse ARP

Le processus de réponse ARP fonctionne comme suit :

- Réponse ARP : Seul le périphérique dont l'adresse IPv4 correspond à l'adresse cible de la requête ARP envoie une réponse. La réponse est encapsulée dans une trame Ethernet avec :
    

- Adresse MAC de destination : L'adresse MAC de l'expéditeur de la requête ARP.
    
- Adresse MAC source : L'adresse MAC de l'expéditeur de la réponse ARP.
    
- Type : 0x806, indiquant que la trame contient des données ARP.
    

- Réception : La réponse ARP est envoyée en monodiffusion au périphérique ayant émis la requête. Une fois la réponse reçue, l'adresse IPv4 et l'adresse MAC correspondante sont ajoutées dans la table ARP de l'expéditeur.
    
- Expiration des entrées ARP : Les entrées ARP sont horodatées. Si l'entrée expire sans recevoir de trame du périphérique concerné, elle est supprimée. Des entrées statiques peuvent être ajoutées manuellement, mais elles n'expirent pas.
    
- IPv6 utilise un processus similaire à ARP appelé détection des voisins ICMPv6, avec des messages de sollicitation et d'annonce.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfrXiyqV0E2lI8Y1bhL-1hkZXAyMSpbu2YmCIXhVa4J6TIgEkEkEVlEbnDQyy5xRJqVFEjuyNhHT0SYzhMTyDbIwsyy-8_JGjTs6m-7Xlc7SUKA6D47rtSrG4bjBdqdoxuF5Rsw?key=__1V76Yhrj3VZz251M-d5cHn)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdMwHAmMSBTiBrpLoUjR--frIr85OlRECqqQKObqnCENuHQV7IFV91Wb-wt1z1Ov-sazUDWidKgygJsUJ0NidK7fXSZTtqL2SGZKC-jL993StVXW8Igmw4VpTeXlh5udCikJXQk?key=__1V76Yhrj3VZz251M-d5cHn)

### Rôle d'ARP dans les communications à distance

Lorsque l'adresse IPv4 de destination ne se trouve pas sur le même réseau que l'adresse IPv4 source, le périphérique source doit envoyer la trame à sa passerelle par défaut (interface du routeur local).

Voici comment cela fonctionne :

- Comparaison des adresses IP : Lorsqu'un hôte souhaite envoyer un paquet, il compare l'adresse IPv4 de destination avec son propre réseau pour déterminer si elles se trouvent sur le même réseau de couche 3. Si l'adresse de destination est distante, il devra utiliser sa passerelle par défaut.
    
- Recherche de l'adresse MAC : Si l'adresse MAC de la passerelle par défaut n'est pas dans la table ARP de l'hôte, il envoie une requête ARP pour obtenir l'adresse MAC du routeur (passerelle).
    
- Processus ARP : Le processus ARP est utilisé pour résoudre l'adresse MAC de la passerelle par défaut, de la même manière que pour une destination locale.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdBtOQBgfi0DqKq3J4690Ep6ofvnuGZpZnL-KfO30LpX8g_w6PoNPGQsf2qipiGHVT3Rv3QIwYdTYkI0xirabMCUq739BhMfM7jkIwsfkR2bpxr43OxEwMbe95t3sUZMJNLH-5c-w?key=__1V76Yhrj3VZz251M-d5cHn)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfO8VEcHAVH8t13NCM3xKR1CF25o2PYJa84Ov7-3UDjqwZLTJSfduznvLtBJIkZlJu4r1M4zzNgBQVDIfYvP7SbZSxR09IGXwYosHvTcHqMj4XIgRofAv5eWOrLDdqsk2nTuXnX7w?key=__1V76Yhrj3VZz251M-d5cHn)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdWq_3-DCbGwat-lYsjsnMfXzeqbd9nyhK7Z26UoqexDOW2zHnUt09AFZb-wT9w24s-yfKko2Ex2l7T1kGQRIuIGRBCMbvQwCMOpX6YUPTznjzIqquu91_L5SkOZ2IVIWiR6mjP?key=__1V76Yhrj3VZz251M-d5cHn)

  
  

### Suppression des entrées d'une table ARP

Les entrées de la table ARP sont supprimées automatiquement si elles ne sont pas utilisées pendant une période définie. Cette période varie en fonction du système d'exploitation. Par exemple :

- Sur Windows, les entrées ARP sont stockées pendant 15 à 45 secondes avant d'être supprimées si elles n'ont pas été utilisées.
    

Cela permet de garder la table ARP à jour et d'éviter que des mappages obsolètes d'adresses IP et MAC restent dans la mémoire du périphérique.

Des commandes permettent aussi de supprimer manuellement les entrées du table ARP totalement ou partiellement. Lorsqu’une entrée est supprimée, le processus d’envoi d’une requête ARP et de réception d’une réponse ARP doit être répété pour entrer le mappage dans le tableau ARP.

Sur un routeur Cisco, la commande show ip arp permet d'afficher les mappages IP-MAC associés aux interfaces réseau du routeur. Exemple de sortie :

R1# show ip arp

Protocol  Address      Age (min)  Hardware Addr   Type   Interface

Internet  192.168.10.1        -   a0e0.af0d.e140  ARPA   GigabitEthernet0/0/0

Internet  209.165.200.225     -   a0e0.af0d.e141  ARPA   GigabitEthernet0/0/1

Internet  209.165.200.226     1   a03d.6fe1.9d91  ARPA   GigabitEthernet0/0/1

  

Sur un ordinateur Windows, la commande arp -a affiche également la table ARP pour l'interface réseau de l'ordinateur. Exemple de sortie :

  

C:\Users\PC> arp -a

Interface: 192.168.1.124 --- 0x10

  Internet Address  Physical Address  Type

  192.168.1.1       c8-d7-19-cc-a0-86 dynamic

  192.168.1.101     08-3e-0c-f5-f7-77 dynamic

  192.168.1.110     08-3e-0c-f5-f7-56 dynamic

  192.168.1.112     ac-b3-13-4a-bd-d0 dynamic

  192.168.1.117     08-3e-0c-f5-f7-5c dynamic

  192.168.1.126     24-77-03-45-5d-c4 dynamic

  192.168.1.146     94-57-a5-0c-5b-02 dynamic

  192.168.1.255     ff-ff-ff-ff-ff-ff static

  224.0.0.22        01-00-5e-00-00-16 static

  224.0.0.251       01-00-5e-00-00-fb static

  239.255.255.250   01-00-5e-7f-ff-fa static

  255.255.255.255   ff-ff-ff-ff-ff-ff static

  

Les éléments clés dans ces tables sont les suivantes :

- Adresse IP : L'adresse IP du périphérique.
    
- Adresse MAC : L'adresse physique associée à l'adresse IP.
    
- Type : Indique si l'entrée est dynamique ou statique.
    
- Âge (sur les routeurs Cisco) : Le temps (en minutes) pendant lequel l'entrée ARP a été active.
    

Dans un réseau local, les requêtes ARP sont diffusées à tous les périphériques, ce qui peut avoir un impact sur les performances du réseau, surtout dans les réseaux à grande échelle ou lorsque de nombreux périphériques sont mis sous tension en même temps. En effet, chaque périphérique qui reçoit une diffusion ARP doit vérifier si l'adresse IP de la requête correspond à son propre mappage IP-MAC, ce qui consomme des ressources réseau et processeur.

Cependant, une fois que les périphériques ont résolu les adresses MAC et les ont stockées dans leur cache ARP, les requêtes suivantes sont minimisées et l'impact sur le réseau est réduit.

Usurpation d'identité ARP (ARP Spoofing) : Une menace de sécurité associée au protocole ARP est l'usurpation d'identité ARP (ARP Spoofing), où un attaquant envoie de fausses informations ARP dans un réseau. L'objectif est de rediriger le trafic réseau vers l'attaquant, ce qui peut permettre l'interception, la modification ou le blocage des communications entre les périphériques légitimes.

Les attaques ARP Spoofing peuvent être difficiles à détecter car le protocole ARP n'inclut aucune méthode d'authentification. Par conséquent, un attaquant peut usurper une adresse MAC et tromper les périphériques du réseau pour qu'ils envoient des paquets vers sa propre machine au lieu de la destination correcte.

Solutions pour limiter l'impact ARP et ARP Spoofing :

1. Fixer des entrées statiques dans la table ARP : Pour éviter l'usurpation d'identité ARP, les administrateurs peuvent configurer des entrées statiques ARP, ce qui empêche la mise à jour des adresses MAC automatiquement.
    
2. Filtrage ARP : Les routeurs ou les switchs peuvent être configurés pour filtrer les paquets ARP suspects.
    
3. Sécurisation du réseau : Utiliser des technologies comme le VLAN, le chiffrement et des mécanismes d'authentification pour limiter les risques d'attaque.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcwzvgKDLTplYUShogd2rFJ0idixkPBZM04rS02OjaY9GanQ_YzXDVUd7VO6b1Iio6CIP0ejiqM-0K3jO_XXbPijsd29S1MEe8mSTHS-Zh1fodlmhfn6LgmHFnjFUfVtjJquXWw?key=__1V76Yhrj3VZz251M-d5cHn)

  

Le protocole Neighbor Discovery (ND) est utilisé dans les réseaux IPv6 pour effectuer une fonction similaire à ARP dans les réseaux IPv4, en associant les adresses IPv6 aux adresses MAC des périphériques voisins. Il permet de découvrir et résoudre les adresses MAC associées aux adresses IPv6 sur un réseau local.

Voici les principales fonctions de ND :

- Découverte de voisins : Identifie les périphériques voisins sur un réseau local.
    
- Résolution des adresses : Permet de mapper une adresse IPv6 à une adresse MAC, tout comme ARP le fait pour IPv4.
    
- Découverte des routeurs : Permet aux hôtes de découvrir les routeurs sur un réseau IPv6.
    
- Détection des duplicatas d'adresses : Permet de vérifier qu'une adresse IPv6 n'est pas déjà utilisée sur le réseau.
    
- Annonce de la disponibilité des voisins : Les périphériques envoient des messages pour annoncer leur présence et leur disponibilité.
    

Les messages ND sont encapsulés dans des paquets ICMPv6 et utilisent des messages tels que Neighbor Solicitation (sollicitation de voisin) et Neighbor Advertisement (réponse de voisin), qui sont essentiels pour effectuer ces découvertes et résolutions d'adresses.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeH-OPCI2TXtDkDLYU4Qxar9nlM7RqJSUno3QNNcBq92Xftn9O-f0UXdIgfrpqTUx6Hk2tSDznIjXLlK6DMvdK9q3ZE2NP1Ipg9zzBib6v6kNo52P8FD8WL367Wmb0X_HoBMl4bXg?key=__1V76Yhrj3VZz251M-d5cHn)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdmlQM6VIGWmlMM4sd4ktLvqXGiC3B2h95DtIh971RPw1BCug3nEw8JgL844qOayIv9k21I4Ay9Q3S8yY_xtgm85H5QuBNsTxgiJtKNOnfLf-3zavRZzRfnwf9mtSYvUHp9yjlN7Q?key=__1V76Yhrj3VZz251M-d5cHn)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe5qhxqJHNSb1-hShpp4M2SG3SqSC7ORRFIrdpvnbuOsIkvyltid-1dat_zT42GznFbrO5dmOrVeW8w6Qqr8_0AXZwyuhLt7HA2DTX0NFFSy5_TxZsGfruguIVyc0n66EAMK4HJWw?key=__1V76Yhrj3VZz251M-d5cHn)

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfawj6zD8dNLykH94CQhCDGGxJJkN-YK0Q-3U3AwcSjB5mQuOW5fCuY6L2C2CoBy-LszArmwvhbwRVfwsFaMT098c0olnBCSLHynHeCMMT76jbauQkmYGb3XhXDpcoJEoHZHw9wag?key=__1V76Yhrj3VZz251M-d5cHn)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXceya-wEUIBtp3mUDNCbVuLupcV1EiGTm3mzZ4IClK219tVIcStzVpHcNq85pRYyxeib_51F_wJUG2OG85F-DNPuA8_cW_AR3yxtbkFivnvpvsLcB87XED1L-t5SPL6uDZ_ucgD4A?key=__1V76Yhrj3VZz251M-d5cHn)

- Message de sollicitation de voisin
    
- Message d'annonce de voisin
    
- Message de sollicitation de routeur (RS)
    
- Message d'annonce de routeur (RA)
    
- Redirection du message
    

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf1ia61zUrI7b0YQIQMTSGib3r41q3b5o3V-GIaqSGz3HHya2iZYTOIqUSjuQISbXzEcp7fRN9zoSqsb7H1YV1lFjQ89ridkTn299kQUU7jo42iF_QpDCS6x9RjhLZx9u28J_CpHQ?key=__1V76Yhrj3VZz251M-d5cHn)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeSJbVPhU8kV2T4agvCHPcA3mgNQt2NYk80-DPtK8FXOH_oyopiahQziEbN2ko1ekeD8_GJq8V72CAVRPx06s4NSXXUye0-WJO0N-yZrNhI7uISJz9vhZvhGtEXL7PbNcrUFRxBUw?key=__1V76Yhrj3VZz251M-d5cHn)

Remarque: Le cinquième message ND ICMPv6 est un message de redirection qui est utilisé pour une meilleure sélection de tronçon suivant. Ces thèmes ne seront pas abordés dans ce cours.

IPv6 ND est défini dans l'IETF RFC 4861.

Remarque: Le cinquième message ND ICMPv6 est un message de redirection qui est utilisé pour une meilleure sélection de tronçon suivant. Ces thèmes ne seront pas abordés dans ce cours.

IPv6 ND est défini dans l'IETF RFC 4861.

9.3.3 Découverte de voisins IPv6 - Résolution d'adresses 

Les périphériques IPv6 utilisent le protocole Neighbor Discovery (ND) pour résoudre les adresses MAC, tout comme ARP pour IPv4. Lorsqu'un périphérique connaît une adresse IPv6 mais pas l'adresse MAC associée, il envoie un message de sollicitation de voisin (NS) via ICMPv6. Le périphérique cible répond avec un message d'annonce de voisin (NA), contenant l'adresse MAC. Ce processus est équivalent aux requêtes et réponses ARP dans IPv4.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe7slO6H8jGY87JwfWObVfzBm6-DiYxsyRODNzOgYkpgSxJ5OLTbFzIUjiGijt45wFhD-7Z0V-fX_cc5ptEXNTvGNLqrkOUW-Zx9lZaQiD4NGaPZhl8LmUGVOLx7WuzcZfdzc3EwQ?key=__1V76Yhrj3VZz251M-d5cHn)

  

Les messages de sollicitation de voisin ICMPv6 sont envoyés à une adresse de multidiffusion spéciale en Ethernet et IPv6, permettant à la carte réseau du périphérique récepteur de déterminer si le message lui est destiné, sans nécessiter un traitement par le système d'exploitation. En réponse à une sollicitation de voisin, le périphérique cible (ici PC2) envoie un message Neighbor Advertisement (NA), contenant son adresse MAC associée à l'adresse IPv6 demandée.

  

Rubrique 9.2.0 - Un commutateur de couche 2 détermine comment gérer les trames entrantes à l'aide de sa table d'adresses MAC. Lorsqu'une trame entrante contient une adresse MAC de destination qui ne figure pas dans le tableau, le commutateur transmet la trame à tous les ports, à l'exception du port sur lequel elle a été reçue.