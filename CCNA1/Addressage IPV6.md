  
  

## 12.1.2 La coexistence des protocoles IPv4 et IPv6 

La transition vers l'IPv6 n'aura pas lieu à une date fixe. IPv4 et IPv6 coexisteront dans un proche avenir et la transition prendra plusieurs années. L'IETF a créé divers protocoles et outils pour aider les administrateurs réseau à migrer leurs réseaux vers l'IPv6. Les techniques de migration peuvent être classées en trois catégories:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeZPS108dUNdTwHUMp6Xc8VN4dPvd_CYFALDLG4Nxkr9Ga200z7ORZkin1_Z11YHTCZvPzrsW-bnfFACxVnlWrubfg9tJadCTjO0rSdkAODe3-uPt3rtj1IOSCFPql3IBxpemQhKQ?key=UPPRKkHOQa9wbf4HNKU3covr)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdG14xsDOW2psMDkplIXcufn1armhn-nymblY_cn-dR16dPXj7jNp2lU6zfTgJWEfgz2TUsD-QJ17N5SsQ0srU9fhkQylaU_WiaP6jnv9G_0bYbYkv-ovxzbfH-lYFnVyTNPf5K?key=UPPRKkHOQa9wbf4HNKU3covr)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfCNLZq7E37Mm0_ZiD9rmsxhsQdy0LVaJk7Zb5NJNJeR9Tz9DthGShgzMPYAEsr-ZN6o5m98EWUukAN32mV5XQGSG6dxt4krs7irBHYM6N5XQ4iZl-2QpUjKPsS__G0L4G0UzqXSg?key=UPPRKkHOQa9wbf4HNKU3covr)

  
  
  
  

## 12.2.1 Formats d'adresses IPv6 

  

Les adresses IPv6, bien plus étendues que celles en IPv4, mesurent 128 bits. Elles sont représentées sous forme de valeurs hexadécimales regroupées en 32 caractères, chaque caractère représentant 4 bits. Ces adresses peuvent être écrites en majuscules ou minuscules, sans distinction de casse. Leur format assure une abondance d'adresses disponibles pour les réseaux modernes.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd5AaJSdcmCY3QEpV7dsTRtswGwLR1kz9wqo3urG507im0-fQdrRShaogP5fs6S1dfmgX9D7B7AYUXcxtVHAH5Hi8rp-TV3AA4Z1EWL-rZjk5BjWXiez1FZ_-bCnQdZrx59nrVDvQ?key=UPPRKkHOQa9wbf4HNKU3covr)

  

### Résumé : Format Préféré pour les Adresses IPv6

#### Points Clés :

- Format Préféré :
    

- Les adresses IPv6 sont écrites sous la forme x:x:x:x:x:x:x:x.
    
- Chaque x correspond à quatre valeurs hexadécimales.
    

- Définition de Hextet :
    

	- Un hextet désigne :
	    
	
	- Un segment de 16 bits d'une adresse IPv6.
	    
	- Quatre caractères hexadécimaux.
    

- Longueur de l’Adresse :
    

- Une adresse IPv6 complète contient 32 caractères hexadécimaux.
    

#### Remarques :

- Ce format est standard mais pas toujours optimal pour représenter les adresses IPv6.
    
- Des règles pour simplifier cette représentation seront abordées dans les prochains modules.
    

  
  
## Simplification
### 12.2.2 Règle 1 - Omettre les zéros en début de segment 

  

Règle principale :  
Les zéros en début d’un segment de 16 bits (hextet) dans une adresse IPv6 peuvent être omis.

Exemples :

- 01AB → 1AB
    
- 09f0 → 9f0
    
- 0a00 → a00
    
- 00AB → AB
    

Points importants :
	- Uniquement pour les zéros de début : Les zéros de fin ne peuvent pas être omis.

- Éviter l’ambiguïté :
		- Exemple : abc peut signifier 0abc ou abc0, qui sont des valeurs différentes.
    

  
  

ExP:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdhmeWgKjMQ2QFrl34IegNzIiUbvgrbB0GNfrrLY73jQemPODMgvKflRrgpS0W0SWtOxKlUTLVS8NS9St9N0BqxXbhF9wRdcIcC82_A_ndBHhJ_6Gw5z9nDdHF1pk-G7TdAW5nq1g?key=UPPRKkHOQa9wbf4HNKU3covr)

  
  
  
  
  
  
  
  
  

### 12.2.3 Règle 2 - Double deux-points 

- Double deux-points (::) :
	- Remplace une chaîne unique et contiguë d'un ou plusieurs hextets composés uniquement de zéros (0:0:0).
    
- Réduit la notation en omettant les zéros initiaux des segments.
    

- Exemple valide :  
    2001:db8:cafe:1:0:0:0:1 devient 2001:db8:cafe:1::1.
    

#### Règles d'utilisation

- Usage unique du double deux-points (::) par adresse :
    

- Empêche l’ambiguïté et garantit une seule adresse possible.
    
- Exemple incorrect : 2001:db8::abcd::1234 (double usage interdit).
    

### Priorité en cas de chaînes équivalentes

- Si plusieurs chaînes de zéros :
    

- Utiliser :: pour la chaîne la plus longue.
    
- Si les chaînes sont de longueur égale, appliquer :: à la première chaîne.
    

#### Erreur commune

- Mauvais usage du double deux-points (::) peut générer plusieurs interprétations possibles.  
    Exemple incorrect : 2001:db8::abcd::1234 pourrait être interprété comme :
    

- 2001:db8::abcd:0000:0000:1234
    
- 2001:db8:0000:abcd::1234
    

Adopter ces règles garantit une notation claire et efficace en IPv6.

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdVMeLhi1Mx-JBAo51gy9wATOroBbjBVTrJvhQ_3FfnXt4chiFKTvAe4luSfn7UgngQl30TI2yRfCMHxYthxyyg-npo1BGkm6MQfrvzqdCK9KiMkiLw_IZ-bweToSFE1rdxptGQ?key=UPPRKkHOQa9wbf4HNKU3covr)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc8qpAek_YLM4H1CrJjQ8d-Kt-_812xjMvA7Fc4oetE6UfSbOglqBYeVJaZfmcSvHqA_BfKDV5kQBegItNoLstPCPhus4B_Zbx0eVqDRlXw-wfI_8d9tfANuoqamFcnEhNRLXfh?key=UPPRKkHOQa9wbf4HNKU3covr)

  
  

## 12.3.1 monodiffusion, multidiffusion et Anycast 

  

Comme avec IPv4, il existe différents types d'adresses IPv6. En fait, il existe trois grandes catégories d'adresses IPv6:

- monodiffusion - Une adresse de monodiffusion IPv6 identifie une interface sur un périphérique IPv6 de façon unique.
    
- Multidiffusion - Une adresse de multidiffusion IPv6 est utilisée pour envoyer un seul paquet IPv6 vers plusieurs destinations.
    
- Anycast - Une adresse anycast IPv6 est une adresse de monodiffusion IPv6 qui peut être attribuée à plusieurs périphériques. Un paquet envoyé à une adresse anycast est acheminé vers le périphérique le plus proche ayant cette adresse. Les adresses anycast sortent du cadre de ce cours.
    

Contrairement à l'IPv4, l'IPv6 n'a pas d'adresse de diffusion. Cependant, il existe une adresse de multidiffusion destinée à tous les nœuds IPv6 et qui offre globalement les mêmes résultats.



## 12.3.2 Longueur de préfixe IPv6 


- Définition : Identifie la partie réseau d'une adresse IPv4.
    
- Notation :
    

- Notation décimale à point : Masque de sous-réseau (ex. : 255.255.255.0).
    
- Notation avec barre oblique : Longueur de préfixe (ex. : 192.168.1.10/24).
    

- Terme clé : /24 est appelé le préfixe.
    
-   
    

#### Préfixe IPv6

- Définition : Indique la partie réseau d'une adresse IPv6.
    
- Notation :
    

- Ne utilise pas de masque de sous-réseau en notation décimale.
    
- Utilise une longueur de préfixe (ex. : /64).
    

- Plage : La longueur de préfixe varie entre 0 et 128.
    
- Recommandation : Utiliser un préfixe /64 pour les réseaux locaux et la plupart des autres réseaux.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcs-kArpXlFBy4DgpHER8af6MrRwGV5WYBSt1Bx9Op-xw8HvI0TexUuWWUsJ86s7IglMGOmRFxR7eEIzfNNAB2PqJ-cW8zI-pmQM8X0BKghjXlfSidqZ5OFcZQcSoPmv446IkMt8w?key=UPPRKkHOQa9wbf4HNKU3covr)

  

>Il est fortement recommandé d'utiliser un ID d'interface 64 bits pour la plus Part des réseaux. En effet, la configuration automatique d'adresse sans état (SLAAC) utilise 64 bits pour l'ID d'interface. Il facilite également la création et la gestion des sous-réseaux.

  
  
  

## 12.3.3 Autres types d'adresses IPv6 de monodiffusion

  

Définition :  
Les adresses de monodiffusion IPv6 identifient de manière unique une interface sur un périphérique IPv6.

- Un paquet envoyé à une adresse de monodiffusion est reçu uniquement par l'interface correspondant à cette adresse.
    

Règles des adresses source et destination :

- L'adresse source en IPv6 doit toujours être une adresse de monodiffusion.
    
- L'adresse de destination peut être :
    

- Monodiffusion : envoyée à une seule interface spécifique.
    
- Multidiffusion : envoyée à plusieurs interfaces simultanément.
    

Visualisation :

### Adresses IPv6 de monodiffusion

  
Une figure illustre les différents types d'adresses de monodiffusion IPv6.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcw72APZVeusrYRZhOC6g0bIsgeIP-vSVoxfMoVMU-mlN9f9H8XNNIqpZ2SWrVcj9Gol1vGgrkmFrdL0kIKE3_Dgvkd1Isof_3TD8kwPkSbPYuhlW9njY8-5yEsGeyY5dcGouUnNg?key=UPPRKkHOQa9wbf4HNKU3covr)

  
  
  
  
  
  
  

Adresses IPv6 sur les périphériques

  

Les périphériques IPv6 disposent généralement de deux adresses monodiffusion :

  

    Adresse GUA (Global Unicast Address) :

        Semblable à une adresse IPv4 publique.

        Unique à l'échelle mondiale et routable sur Internet.

        Peut être configurée de manière statique ou attribuée dynamiquement.

  

    Adresse LLA (Link-Local Address) :

        Obligatoire pour chaque périphérique IPv6.

        Utilisée pour la communication sur une même liaison locale .

        Non routable au-delà de la liaison locale.

        Les routeurs ne transmettent pas de paquets avec une adresse source ou de destination link-local.

        Leur unicité est confirmée uniquement sur la liaison locale concernée.

  

## 12.3.4 Remarque à propos de l'adresse locale unique

  

Gamme d'adresses locales uniques :

- Plage : fc00::/7 à fdff::/7.
    
- Actuellement, elles ne sont pas couramment implémentées, donc ce module se concentre sur les GUA et LLA.
    

Utilisation possible des adresses locales uniques :

- Destinées à des périphériques qui ne doivent pas être accessibles depuis l'extérieur, comme des serveurs internes ou des imprimantes.
    
- Elles permettent l'adressage local au sein d'un site ou entre plusieurs sites.
    

Caractéristiques :

- Similaires aux adresses privées IPv4 (RFC 1918), mais avec des différences notables.
    
- Non routables globalement et ne sont pas traduites en adresses IPv6 globales.
    

Sécurisation du réseau :

- Certaines organisations utilisent des adresses locales uniques pour masquer leur réseau et limiter les risques.
    
- Toutefois, la sécurité ne doit pas reposer uniquement sur cette caractéristique, et des précautions de sécurité doivent être prises au niveau des routeurs connectés à Internet, conformément aux recommandations de l'IETF.
    

  
  
  
  
  

## 12.3.5 GUA IPv6 

  
Caractéristiques des GUA :

- Uniques au monde et routables sur Internet (IPv6).
    
- Équivalentes aux adresses publiques IPv4.
    

Attribution des GUA :

- L'ICANN (Internet Committee for Assigned Names and Numbers) attribue des blocs d'adresses IPv6 via l'IANA aux organismes d'enregistrement Internet locaux.
    
- Actuellement, seules les adresses monodiffusion globales commençant par 001 ou 2000::/3 sont attribuées.
    

Plage d'adresses GUA :

- Le premier hextet pour les GUA commence par un chiffre hexadécimal 2 ou 3.
    
- Cela représente 1/8e de l'espace d'adressage IPv6 total, le reste étant réservé pour d'autres types d'adresses.
    

Réservation pour documentation :

- L'adresse 2001:0DB8::/32 est réservée à des fins de documentation, notamment pour des exemples.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfe_xdNFU7FISzfoimF3NZ5AMub3wpiNs6gElZP3fBtjW_CM7FhtbkysHgdvhlH7u93Lr9ldRaiEZm9ZjRh3gu7ZUE605xSV34GybgYF9ZZrzCm52HB55Njmk5xI96GH3ovjH3_HA?key=UPPRKkHOQa9wbf4HNKU3covr)

  

## Adresse IPv6 avec un préfixe de routage global /48 et un préfixe /64

  
### 12.3.6 Structure GUA IPv6 

  

- Préfixe de Routage Global :
    

- Il désigne la partie réseau de l'adresse attribuée par le fournisseur (ex. un FAI).
    
- Exemple courant : un préfixe de routage global /48 est attribué aux clients.
    
- Le préfixe détermine les 48 premiers bits de l'adresse, ce qui définit la partie réseau.
    
- Exemple : 2001:0DB8:ACAD::/48, où 2001:0DB8:ACAD représente le préfixe réseau, et les deux points (::) signalent les zéros restants dans l'adresse.
    


- ID de Sous-Réseau :
    

- C'est la zone entre le préfixe de routage global et l'ID d'interface.
    
- Utilisé pour identifier les sous-réseaux au sein d'un site ou d'une organisation.
    
- Avec un préfixe global /32, l'ID de sous-réseau peut être 32 bits, permettant 4,3 milliards de sous-réseaux.
    
- Le sous-réseau /64 est recommandé, ce qui laisse 64 bits pour l'ID d'interface.
    


- ID d'Interface :
    

- Correspond à la partie hôte de l'adresse IPv6, équivalente à l'adresse hôte IPv4.
    
- Un périphérique peut avoir plusieurs interfaces avec différentes adresses IPv6.
    
- L'ID d'interface 64 bits est recommandé pour permettre aux périphériques utilisant SLAAC (Stateless Address Autoconfiguration) de générer leur propre ID d'interface.
    
- Cela permet d'héberger un grand nombre de périphériques (jusqu'à 18 quintillions par sous-réseau).
    

### Remarques

- Sous-réseaux /64 :
    

- Recommandé pour simplifier le plan d'adressage IPv6 et permettre une configuration automatique des périphériques.
    

  

- Adresse Tout-1s et Adresse Anycast :
    

- L'adresse tout-1s (tous les bits à 1) est utilisée pour les adresses anycast de routeur, mais ne sont pas attribuées à des périphériques.
    
- L'adresse contenant uniquement des zéros est réservée pour l'adresse anycast de routeur de sous-réseau.
    

  

## 12.3.7 IPv6 LLA 

  

Définition :  
Une adresse link-local IPv6 (LLA) permet à un périphérique de communiquer avec d'autres périphériques IPv6 uniquement sur la même liaison (sous-réseau).

- Les paquets associés à une adresse LLA ne peuvent pas être acheminés au-delà de la liaison locale.
    

Obligation d'attribution :

- L'adresse GUA n'est pas obligatoire.
    
- Toutefois, chaque interface réseau compatible IPv6 doit avoir une adresse LLA.
    

Création automatique :

- Si une adresse link-local n'est pas configurée manuellement, le périphérique génère automatiquement sa propre adresse sans avoir besoin d'un serveur DHCP.
    
- Même sans adresse de monodiffusion globale IPv6, les périphériques peuvent créer des adresses LLA pour communiquer avec d'autres périphériques sur le même sous-réseau, y compris avec la passerelle par défaut (routeur).
    

Plage d'adresses LLA :

- Les adresses LLA se trouvent dans la plage fe80::/10.
    
- Le préfixe /10 indique que les 10 premiers bits sont 1111 1110 10xx xxxx.
    
- Le premier hextet varie de fe80 (1111 1110 1000 0000) à febf (1111 1110 1011 1111).
    

Exemple de communication :

- Un périphérique (ex. PC) peut communiquer directement avec un autre périphérique (ex. imprimante) à l'aide d'adresses LLA sur le même sous-réseau.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdrZ6WVW8U2UyjOlCXpds6PYH6dZk5TASIt6wgFvBahFSdtHaH845LqBFjXJAC9qjBTj0VzAGTVFLOQxH6c7wduqVarjeB8lPR-WLZpKRYT4k8YpsuPuzRg5B182iTTbSYouKlBww?key=UPPRKkHOQa9wbf4HNKU3covr)


  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXee8zgP41c8K10Hr8mV7MfZpdqtnZJmZXDmku3Bsk3wQwWwrs3_QxCFkMmBEc0Y5vWUKyIzeTKuV1c0H3BPZU30vZAsuTuQwCHfjbYdhX6jkBZGlFP6Lmr62inUcoiNL77eaHMbtg?key=UPPRKkHOQa9wbf4HNKU3covr)

  
  

## 12.4.1 Configuration GUA statique sur un routeur 
  

GUA et LLA IPv6 :

- Les GUA IPv6 (Global Unicast Addresses) sont routables sur Internet, tout comme les adresses IPv4 publiques.
    
- Les LLA IPv6 (Link-Local Addresses) permettent la communication entre périphériques sur le même sous-réseau (lien).
    

Configuration sur Cisco IOS :

- La configuration des adresses IPv6 (GUA et LLA) est similaire à celle des adresses IPv4 sur les routeurs Cisco.
    
- La différence réside dans l'utilisation de ipv6 au lieu de ip dans les commandes.
    

Exemple de commande Cisco IOS :

- Pour configurer une adresse IPv4 :
    

```
ip address ip-address subnet-mask
```

  

Pour configurer une GUA IPv6 :


```
ipv6 address ipv6-address/prefix-length
```

  

- Remarque : Il n'y a pas d'espace entre l'adresse IPv6 et la longueur du préfixe.
    

- Topologie et sous-réseaux IPv6 utilisés :
    

- 2001:db8:acad:1::/64
    
- 2001:db8:acad:2::/64
    
- 2001:db8:acad:3::/64
    

Cette configuration permet de créer un réseau IPv6 en utilisant des sous-réseaux distincts et en attribuant des adresses statiques aux périphériques du réseau.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfWVEMn-iophfqC7q42qVmSmtG98ZlFThRacMUH5xHg8A2Jt5fa63LFSLbntaDNC7H01V2Ck21iJH048F1uyZvTIEyAjRyyFIRRgMNKyRwWC6nb10AaTOewUASft1yVlZd4yraKgQ?key=UPPRKkHOQa9wbf4HNKU3covr)

  

```shell
R1(config)# interface gigabitethernet 0/0/0

R1(config-if)# ipv6 address 2001:db8:acad:1::1/64

R1(config-if)# no shutdown

R1(config-if)# exit

R1(config)# interface gigabitethernet 0/0/1

R1(config-if)# ipv6 address 2001:db8:acad:2::1/64

R1(config-if)# no shutdown

R1(config-if)# exit

R1(config)# Interface série 0/0/0

R1(config-if)# ipv6 address 2001:db8:acad:3::1/64

R1(config-if)# no shutdown

```
  
  

- Problème avec les adresses statiques :  
    Comme avec IPv4, l'utilisation d'adresses statiques sur les clients n'est pas idéale dans les grands environnements. Cela nécessite une gestion manuelle complexe et ne scale pas bien.
    
- Méthodes d'attribution dynamique des adresses IPv6 : Un périphérique peut obtenir automatiquement une adresse de diffusion globale IPv6 de deux manières :
    

- ==SLAAC (Stateless Address Autoconfiguration) :==
    

- Permet à un périphérique de s'auto-configurer sans avoir besoin d'un serveur.
    
- Le périphérique génère son adresse à partir du préfixe réseau et de son propre identifiant d'interface.
    

- ==DHCPv6 avec état :==
    

- Utilise un serveur DHCPv6 pour attribuer des adresses aux périphériques. Cette méthode garde un état de l'adresse attribuée, ce qui permet une gestion plus précise des adresses.
    

- Remarque importante :
    

- Que vous utilisiez SLAAC ou DHCPv6, l'adresse link-local du routeur est automatiquement définie comme l'adresse de la passerelle par défaut pour les périphériques du réseau.
    

  

## 12.4.3 La configuration statique d'une adresse link-local de monodiffusion 


Avantages de la configuration manuelle des LLA :  

La configuration manuelle des adresses link-local permet de créer des adresses facilement reconnaissables et mémorisables.  
Cela est particulièrement utile pour les routeurs, car ces adresses sont utilisées :

- Comme passerelles par défaut pour les périphériques sur le réseau.
    
- Lors du routage des messages d'annonce.
    

Commande pour configurer une adresse LLA :  

Les adresses link-local peuvent être configurées manuellement à l'aide de la commande suivante :
  

```
ipv6 address link-local ipv6-link-local-address
```

  
  

- Exemple : Lorsqu'une adresse commence par un hextet dans la plage FE80 à FEBF, le paramètre link-local doit être utilisé pour indiquer qu'il s'agit d'une adresse locale.
    

Exemple de topologie :  
La figure présente une topologie où des LLA sont configurées sur chaque interface, permettant aux périphériques de communiquer efficacement

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeC5fPb9f7xWsT6wDhGzi8q_vZcy_43jehWH9QFtl2rMH0ReUr2N93gLLUTMU02CM-f6tUoBk7zP6C8Ewasji2i-Uykk2bxVZhDX4hBWqKJgWxtQ5uylVEEukcEvze2VhLimkY0?key=UPPRKkHOQa9wbf4HNKU3covr)

  

```shell
R1(config)# interface gigabitethernet 0/0/0

R1(config-if)# ipv6 address fe80::1:1 link-local

R1(config-if)# exit

R1(config)# interface gigabitethernet 0/0/1

R1(config-if)# ipv6 address fe80::2:1 link-local

R1(config-if)# exit

R1(config)# interface serial 0/1/0

R1(config-if)# ipv6 address fe80::3:1 link-local

R1(config-if)# exit

  
```
  

Objectif des LLA configurés manuellement :  

Faciliter l'identification des interfaces du routeur avec des adresses link-local (LLA) reconnaissables.

Exemple de configuration pour R1 :

- Les interfaces de R1 utilisent des LLA comme fe80::1:n où "1" représente R1 et "n" est unique pour chaque interface.
    
- Exemples : fe80::1:1, fe80::1:2, fe80::1:3.
    

Exemple pour R2 :

- Si R2 était inclus, ses interfaces seraient configurées avec fe80::2:n (par exemple, fe80::2:1, fe80::2:2, fe80::2:3).
    

Remarque sur l'unicité des LLA :

- Un même LLA peut être utilisé sur chaque lien tant qu'il est unique sur ce lien.
    
- Il est courant de configurer un LLA distinct sur chaque interface pour une identification plus facile.
    

## 12.5.1 Messages RS et RA 

  

Obtention Dynamique des GUA :

- Les périphériques obtiennent leurs adresses GUA IPv6 dynamiquement, sans configuration manuelle, grâce à des messages ICMPv6 (Internet Control Message Protocol version 6).
    

Fonctionnement des Messages :

- ==Annonce de Routeur (RA) :==
    

- Les routeurs IPv6 envoient un message RA toutes les 200 secondes à tous les périphériques IPv6 sur le réseau.
    

- ==Sollicitation de Routeur (RS) :==
    

- Un périphérique peut également envoyer un message RS pour solliciter un message RA, demandant ainsi une annonce de routeur.
    

  

Différences dans le Processus de Création de l'ID d'Interface :

- Les périphériques peuvent générer un ID d'interface soit via le processus EUI-64, soit de manière aléatoire. Ce processus de création de l'ID d'interface est un aspect clé pour comprendre la configuration dynamique des GUA.
    

Rappel :  
Les messages RS et RA sont utilisés pour faciliter l'attribution dynamique d'adresses IPv6 GUA, ce qui simplifie le processus de configuration pour les périphériques.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe7BQKGI8uSsT7bxYzRP1qO9XyoZihyVSnjY5lB2Cba_RrnxvBEsOnEiQ3cWDw4Wnda2njYo5avN4o3ToxiWRtZWCt8B0vtfbYxHwBz6sAsomokAW4eCLXTYuoU_TnHzQ_CM7SxBA?key=UPPRKkHOQa9wbf4HNKU3covr)

  

## Activation du Routage IPv6

- Routage IPv6 :
    

- Le routage IPv6 n'est pas activé par défaut sur les routeurs.
    
- Utiliser la commande ==ipv6 unicast-routing== pour activer le routage IPv6 sur un routeur.
    

#### Contenu des Messages RA

Les messages d'annonce de routeur (RA) envoyés sur les interfaces Ethernet contiennent plusieurs informations essentielles :

- Préfixe de réseau et longueur de préfixe :
    

- Indiquent le réseau auquel le périphérique appartient.
    

- Adresse de la passerelle par défaut :
    

- Fournit l'adresse link-local du routeur comme passerelle.
    

- Adresses DNS et nom de domaine :
    

- Contient les informations sur les serveurs DNS et le nom de domaine.
    

## Trois Méthodes pour la Configuration des Adresses IPv6 via RA

1. Méthode 1 : SLAAC (Stateless Address Autoconfiguration)
    

- Fournit tout ce dont le périphérique a besoin : préfixe, longueur de préfixe, et adresse de passerelle par défaut.
    

1. Méthode 2 : SLAAC avec Serveur DHCPv6 sans état
    

- Fournit les coordonnées (préfixe, passerelle par défaut), mais nécessite un serveur DHCPv6 pour compléter l'attribution, comme les adresses DNS.
    

1. Méthode 3 : DHCPv6 avec état (pas de SLAAC)
    

- Le périphérique obtient l'adresse de la passerelle par défaut via RA, mais doit demander un serveur DHCPv6 avec état pour obtenir toutes les autres informations nécessaires (adresses DNS, etc.).
    

  
  
  

### 12.5.2 Méthode 1 - SLAAC 

  

SLAAC permet à un périphérique de créer sa propre adresse IPv6 (GUA) sans avoir besoin d'un serveur DHCPv6. Voici les points clés de la méthode :

1. Message d'Annonce de Routeur (RA)
    

- Le périphérique reçoit un message RA du routeur local, qui contient les informations nécessaires pour configurer son adresse IPv6.
    

1. Processus de Création d'Adresse IPv6
    

- Le périphérique utilise deux parties pour construire son adresse GUA :
    

- Préfixe : Annoncé dans le message RA par le routeur.
    
- ID d'interface :
    

- Utilise la méthode EUI-64 (basée sur l'adresse MAC) ou
    
- Génère un ID de 64 bits de manière aléatoire selon le système d'exploitation de l'appareil.
    

1. Pas de Serveur DHCPv6 Nécessaire
    

- SLAAC est sans état, ce qui signifie qu'il n'y a pas besoin de serveur DHCPv6 pour gérer ou attribuer les adresses. Chaque périphérique crée et gère sa propre adresse à partir des informations reçues via le message RA.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdkgRXhtAh6PJd-eST_rckPZFK2Z7hz4s5QzJ4U1kn5yL079NuJ_HAsRrqtz5tVFgkoFw_OA-WE6i7x1j_MF5WrQ_fmEhzdcLT9FUexXqcSDEcj6B5yn51vsc0zbf4E2Aa1MEiYRA?key=UPPRKkHOQa9wbf4HNKU3covr)

  
  
  
  

### 12.5.3 Méthode 2 - SLAAC et DHCPv6 sans état 

  

Un routeur IPv6 peut être configuré pour utiliser SLAAC et DHCPv6 sans état, ou uniquement DHCPv6 pour envoyer des annonces de routeur. Voici ce qui se passe dans le cas où SLAAC et DHCPv6 sans état sont combinés :

1. SLAAC :  
    Le périphérique crée sa propre GUA IPv6 en utilisant les informations contenues dans le message RA (comme le préfixe de réseau).
    
2. Passerelle par défaut :  
    L'adresse link-local du routeur (l'adresse IPv6 source du message RA) est utilisée comme adresse de la passerelle par défaut.
    
3. DHCPv6 sans état :  
    Le périphérique utilise un serveur DHCPv6 sans état pour obtenir des informations supplémentaires comme :
    

- Les adresses des serveurs DNS.
    
- Le nom de domaine.
    

  

### Note importante :

- Un serveur DHCPv6 sans état ne distribue pas de GUA. Il se limite à fournir des informations supplémentaires comme les serveurs DNS et les noms de domaine.
    

  
  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfdKc2OSdlGT2Qhzt4yWztBqHJ25s-Cy-xN6hBo6RPVHWhiOI-ZHunVNCKkwfxkXRD-GPKR048A-UnNvXDXFgU-pM_u7o4UoMNfNgm0JAqADOul5-0TvU8M38ysIh8mZI9ePC5M_Q?key=UPPRKkHOQa9wbf4HNKU3covr)

  
  
  

### 12.5.4 Méthode 3 - DHCPv6 avec état

  

Lorsque le routeur IPv6 est configuré pour envoyer une annonce de routeur (RA) avec DHCPv6 avec état, voici les informations transmises et utilisées par les périphériques :

1. Passerelle par défaut :  
    L'adresse link-local du routeur (qui est l'adresse IPv6 source du message RA) sert d'adresse de passerelle par défaut.
    
2. Serveur DHCPv6 avec état :  
    Le périphérique utilise un serveur DHCPv6 avec état pour obtenir les informations suivantes :
    

- Adresse de diffusion globale (GUA).
    
- Adresse du serveur DNS.
    
- Nom de domaine.
    
- Toutes autres informations nécessaires.
    

### Remarque :

- Le DHCPv6 avec état fournit à un périphérique toutes les informations nécessaires, y compris l'adressage complet, contrairement à SLAAC, qui laisse la création de l'ID d'interface à l'appareil.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfq_LaBO7akWQixLS9XKKSLI1W08G7XzO3IlZ07kNROVKf0za_lamftLxVWxJCJmZt__vTaPB-w7eNid1hHKJ7_kJHbDCXqCwDRU8B0FI9hc4SSd7GA_tC8qlwfIwVVKYqF0OxesA?key=UPPRKkHOQa9wbf4HNKU3covr)

  

Un serveur DHCPv6 avec état attribue des adresses IPv6 aux périphériques et enregistre ces attributions, similaire à DHCP pour IPv4.

Remarque : L'adresse de la passerelle par défaut est obtenue uniquement de manière dynamique via le message d'annonce de routeur, et non par le serveur DHCPv6.

  
  
  
  

### 12.5.5 Méthode EUI-64 et génération aléatoire 

  

Lorsque le message d'annonce de routeur utilise uniquement SLAAC ou SLAAC avec DHCPv6 sans état, le client doit générer son propre ID d'interface. Il obtient le préfixe de l'adresse via l'annonce du routeur, mais crée l'ID d'interface en utilisant soit la méthode EUI-64, soit un identifiant de 64 bits généré aléatoirement.

  

### Création dynamique d'un ID d'interface

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcyPSYJJIDzFCOWQ0U6JolSOmJcXrhYvKZ1uGURm22en_6NlLty9hPxns2hG7dmnOdyR-p-qWT-O4YGgDH1Tf8Fw2sDwdtZ46JtNmxpF8aHIpqwMvoCvLyHvMK60RnF_L-xu9YPrQ?key=UPPRKkHOQa9wbf4HNKU3covr)

  

### 12.5.6 Méthode EUI-64 

  

La méthode EUI-64 crée un identifiant d'interface de 64 bits à partir de l'adresse MAC Ethernet de 48 bits d'un client. Le processus ajoute 16 bits (FFFE) au milieu de l'adresse MAC pour obtenir un ID d'interface de 64 bits. Ce processus inclut trois parties :

1. Le code OUI (Organizationally Unique Identifier) sur 24 bits, tiré de l'adresse MAC, avec inversion du septième bit pour modifier son statut de "local" ou "universel".
    
2. La valeur fixe de 16 bits "FFFE" insérée au milieu.
    
3. L'ID de périphérique de 24 bits, provenant de l'adresse MAC du client.
    

Ce processus permet de créer un ID d'interface unique et utilisable pour les adresses IPv6.

Le processus EUI-64 est présenté à la figure, avec l'adresse MAC GigabitEthernet FC99:4775:CEE0 de R1.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXejA1nLPVD2PUOQyVOQZZSZxwHJHXuOrZ8hzxEtjgN6VWCCHUmP8NX0OA5DMR60b-kilr5xK0su71lbh-LACgQpM-CnMjJ_9z3keOkcpsGDbDsV8ynQmbCWUAKrNvQPQoPPeIDdSw?key=UPPRKkHOQa9wbf4HNKU3covr)

  

La méthode EUI-64 crée des adresses IPv6 en utilisant l'adresse MAC Ethernet, facilitant l'identification du périphérique. Elle insère "FFFE" dans l'adresse MAC pour générer un ID d'interface unique. Cependant, cela soulève des problèmes de confidentialité, car l'adresse peut être liée au périphérique physique. Pour y remédier, un ID généré aléatoirement peut être utilisé à la place.

  

### ID d'interface généré par la méthode EUI-64

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdak630_HXtXmy7V1mTMFJkunbbiCuYePgLQx8p7qatIDNMRFy9IkgEMLw5f5_VShBz7x8EklaiSBJM_JOVIDtx5SXEweCYOzYFlpu7UIvsxmA6nLWciddwW1Rboj1BztmYq1k7dA?key=UPPRKkHOQa9wbf4HNKU3covr)

  

### 12.5.7 ID d'interface générés aléatoirement 

  

Les périphériques peuvent utiliser un ID d'interface généré aléatoirement, surtout à partir de Windows Vista, au lieu de l'ID basé sur l'adresse MAC via la méthode EUI-64. Les versions plus anciennes de Windows, comme XP, utilisaient l'EUI-64. Une fois l'ID généré, il est combiné avec un préfixe IPv6 pour créer une adresse de diffusion globale, comme indiqué dans l'exemple.

### ID d'interface généré par le nombre à 64 bits aléatoire

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeum1whymAOeKWG0YBxJi5gvlI1l5KVPecytH57E5_wZWBhZYnMmCaoMPYl1mCZGLvAG6FCJiCJBx4cDB4xfjz8RhExHdsXWJMrIifEQZRnObwJnj-DLMDYBgNgsufTf7FahWDF4w?key=UPPRKkHOQa9wbf4HNKU3covr)

Remarque: Pour s'assurer que les adresses de monodiffusion IPv6 sont uniques, le client peut utiliser le processus de détection d'adresse dupliquée (DAD). Le principe est similaire à une requête ARP pour sa propre adresse. En l'absence de réponse, l'adresse est unique.

  
  

## 12.6.1 LLA dynamiques 

  

Tous les périphériques IPv6 doivent avoir un LLA IPv6. Comme les GUA IPv6, vous pouvez également créer des LLA dynamiquement. Quelle que soit la façon dont vous créez vos LLA (et vos GUA), il est important de vérifier toute la configuration des adresses IPv6. Cette rubrique explique les LLA générés dynamiquement et la vérification de la configuration IPv6.

  
  
  

La figure montre que l'adresse link-local est créée dynamiquement à partir du préfixe FE80::/10 et de l'ID d'interface à l'aide de la méthode EUI-64 ou d'un nombre à 64 bits généré aléatoirement.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXchE2TSyyo08eQzrbIQo8I5YDDXa5egJ1CCpQ4Y9VQUtagldS-FNU-2b83aLdMGf89RLPP7lJpp0hXrir-rQWanzlobUKPsRNZ8Rb2FuyqFSV8iA8DHcnSab7uptcgVSBtLYeC6jw?key=UPPRKkHOQa9wbf4HNKU3covr)

## 12.6.2 LLA dynamiques sous Windows 

Les systèmes d'exploitation, tels que Windows, utilisent généralement la même méthode à la fois pour un GUA créé par SLAAC et un ALL attribué dynamiquement. Consultez les zones mises en surbrillance dans les exemples suivants qui ont été montrés précédemment.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe3038oNvwx0qktugk9e71EUzx0LGRXis64sgGdL2WwGM7dZ4En8T2FvlR8LOelHiWv41MU9ZnH6mil0WoqxXN9wt_RQsG4Y6RVBSCh2GmyQRhU9rgX1gTaLsbojCTme-Tyu18CFw?key=UPPRKkHOQa9wbf4HNKU3covr)

  

## 12.6.3 LLA dynamiques sur les routeurs Cisco 

Les routeurs Cisco créent automatiquement une adresse link-local IPv6 dès qu'une adresse de diffusion globale est attribuée à l'interface. Par défaut, les routeurs Cisco IOS utilisent la méthode EUI-64 pour générer l'ID d'interface de toutes les adresses link-local sur des interfaces IPv6. Pour les interfaces série, le routeur utilise l'adresse MAC d'une interface Ethernet. Souvenez-vous qu'une adresse link-local doit être unique seulement sur sa liaison ou son réseau. Toutefois, un inconvénient de l'utilisation de l'adresse locale-lien attribuée dynamiquement est son long ID d'interface: il est en effet difficile d'identifier et de mémoriser les adresses attribuées. L'exemple indique l'adresse MAC sur l'interface Gigabit Ethernet 0/0 de R1. Cette adresse est utilisée pour créer dynamiquement le LLA sur la même interface, ainsi que pour l'interface Série 0/1/0.

Pour simplifier l'identification et la mémorisation de ces adresses sur les routeurs, il est courant de configurer les adresses link-local IPv6 de manière statique sur les routeurs.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfQqHopSrCgEx8gLZa7Pc009nYdZTN6H0g1dX1IXtX3sq40-3rjkN2nvmmEY4uYER2TWpMRt2JEW6QsJ_NmISmEFONgiG8BfH-3IssTfTDA_2rMadBo-k3fmCRN_frO5pzBw5N8Kw?key=UPPRKkHOQa9wbf4HNKU3covr)

  
  
  
  
  
  
  
  

## 12.6.4 Vérifier la configuration des adresses IPv6 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfYg09txCSqjrwa4iU1dK2V5iaINOJDNUViNFSl_2rpmKuTofBchTziUK0fr83gr6f_a7BoD5e4X7ddGtxXHEibZilUrDrsRh63iH3LXHo6zO1i6I72Z7ea1V1rmPqhVN9jU16r?key=UPPRKkHOQa9wbf4HNKU3covr)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcPBU7q3NKgNDXmj7AllxhTloT1EUX41D_dcaGUXcYY8q6FQDHnnsmh3YwdMHC2KQepX0ylwT9Nzk6Yts8IahMP1JSi2Lxqcd0hbs46fNR-7MWuRLnVh-0A6Sx0rxiB9qeYhnAZwA?key=UPPRKkHOQa9wbf4HNKU3covr)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeOLClqtowy8gnZ4tzXm-2_3wNIMkig5V3lum5j3tQJW18dFaht8pubBqRYRrOR-uH1lUcNZhGjIaBfkuFMELOkX1Pz8p0kxPb4tMVb3Kef4YCVqpp7c9LWVCc1hz49brvzPMpt?key=UPPRKkHOQa9wbf4HNKU3covr)

  

## 12.7.1 Adresses de multidiffusion IPv6 attribuées 

  

Les adresses de multidiffusion IPv6, similaires à celles en IPv4, permettent d'envoyer un même paquet à un ou plusieurs destinataires (groupe de multidiffusion). Elles commencent par le préfixe FF00::/8. Ces adresses ne peuvent être utilisées que comme adresses de destination, pas comme source.

Il existe deux types d'adresses de multidiffusion IPv6 :

1. Adresses de multidiffusion attribuées : Ces adresses sont préalablement définies et attribuées à des groupes spécifiques.
    
2. Adresses de multidiffusion de nœud sollicité : Ces adresses sont utilisées pour des requêtes spécifiques, comme la découverte de voisins.
    

  
  
  
  
  
  

## 12.7.2 Les adresses de multidiffusion attribuées 

  

Les adresses de multidiffusion attribuées en IPv6 sont réservées pour des groupes ou périphériques spécifiques, permettant à un paquet d'être envoyé à un groupe de périphériques partageant un service ou un protocole commun, comme DHCPv6.

Deux groupes courants de multidiffusion attribués en IPv6 sont :

1. ff02::1 - Groupe de multidiffusion à tous les nœuds : Tous les périphériques IPv6 sur la liaison rejoignent ce groupe, ce qui équivaut à une diffusion IPv4. Par exemple, un routeur IPv6 utilise ce groupe pour envoyer des messages d'annonce de routeur ICMPv6.
    
2. ff02::2 - Groupe de multidiffusion à tous les routeurs : Tous les routeurs IPv6 qui ont l'adresse ipv6 unicast-routing activée rejoignent ce groupe. Les paquets envoyés à ce groupe sont reçus par tous les routeurs IPv6 sur la liaison
    

### Groupe de multidiffusion vers tous les nœuds: Message RA

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfn0YtaDxLX81924unuFcvEC0KO5M1XDOAZWiiNO6dFvg1L0pk7xpmC-y5N4STkWIg41VxVzpVv0Woio-Db5i1HoWibTJeZnGyNJxzX-aRSZlu8YqtCbxxJ-uMXLcoDIrY3a4T7Xg?key=UPPRKkHOQa9wbf4HNKU3covr)

  
  
  
  
  
  
  

## 12.7.3 Adresses de multidiffusion IPv6 de nœud sollicité 

  

Une adresse de multidiffusion de nœud sollicité en IPv6 permet à la carte réseau Ethernet de filtrer directement la trame via l'adresse MAC de destination, sans que le paquet soit envoyé au processus IPv6. Cela optimise la gestion du trafic en s'assurant que seuls les périphériques destinataires reçoivent le paquet.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc5Anzz59r7Stf9ZyMW1V3v132kVXt3Q57TZYbWijDk6w17enYfbByg99eUmEjY4T9PMDNYYqWz15frcoo3tEj4ewgkzyNB7pZaBOT6P9zKICFkOpnZimx5O7TJlpgEdrrk5bUcnQ?key=UPPRKkHOQa9wbf4HNKU3covr)

  
  

## 12.8.1 Segmenter le réseau en sous-réseaux à l'aide d'ID de sous-réseau 

  

La création de sous-réseaux en IPv6 est plus simple qu'en IPv4 grâce à un champ d'ID de sous-réseau dédié dans la GUA. Ce champ, situé entre le préfixe de routage global et l'ID d'interface, permet une segmentation efficace sans avoir besoin d'emprunter des bits de la partie hôte, contrairement à IPv4.

### Points clés qui rendent cette méthode meilleure :

1. Conception intégrée : IPv6 inclut nativement le sous-réseautage, ce qui simplifie la configuration.
    
2. Séparation claire : Le champ ID de sous-réseau est distinct des autres parties de l'adresse (préfixe global et ID d'interface).
    
3. Flexibilité : La longueur fixe des adresses IPv6 (128 bits) offre suffisamment d'espace pour une hiérarchisation efficace.
    
4. Efficacité : Réduit la complexité par rapport à IPv4, où le sous-réseautage était ajouté après coup.
    

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdTYkqOmKqVnqcWGJQ2r9Dn4I-aWEkBVHy_xFP2jyZSTzy-7MzJGr4oU7VmhUPtDFcdNOsZNTCA_VvsClTA3DNOuydtTq-T9o5E2DBXc2jQRXqox0CfsQEqLh4G65KMOZ0B5IWD?key=UPPRKkHOQa9wbf4HNKU3covr)

  

1. Capacité exceptionnelle :
    

- ID de sous-réseau 16 bits : Jusqu'à 65 536 sous-réseaux avec un préfixe global /48.
    
- ID d'interface 64 bits : Jusqu'à 18 quintillions d'adresses d'hôtes par sous-réseau.
    

1. Simplicité :
    

- Sous-réseautage sans conversion en binaire.
    
- Utilisation simple des comptages en hexadécimal pour identifier les sous-réseaux suivants.
    

1. Flexibilité :
    

- Possibilité de sous-réseauter dans l'ID d'interface si nécessaire, bien que rarement utilisé grâce à l'espace d'adressage vaste.
    

1. Pas de gaspillage : Contrairement à IPv4, la conservation des adresses n'est pas une contrainte.
    

  
  

Remarque: La segmentation en sous-réseaux dans l'ID d'interface à 64 bits (ou partie hôte) est également possible, mais rarement nécessaire.

  
  
  
  
  

## 12.8.2 Exemple de sous-réseau IPv6 

  

Avec un préfixe de routage global de 2001:0DB8:ACAD::/48 et un ID de sous-réseau 16 bits, une entreprise peut créer des sous-réseaux /64.

---

### Points clés :

1. Structure des sous-réseaux :
    

- Le préfixe de routage global reste identique (2001:0DB8:ACAD).
    
- L’ID de sous-réseau (hextet) varie en hexadécimal pour chaque sous-réseau (exemple : 0001, 0002, etc.).
    

1. Clarté et simplicité :
    

- L’incrémentation en hexadécimal rend la gestion des sous-réseaux logique et facile à suivre.
    

1. Exploitation des 16 bits :
    

- Permet de créer jusqu’à 65 536 sous-réseaux distincts, chacun avec un espace d’adressage suffisant pour tous les hôtes possibles.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeAR2zTzMKyvYT65Ujp8VLtZP2D1PoOu8Zv2y0qljjfywzGPc3EqZu7emVDYO6zI3E9bWhEhxzTCCcpChMeHzO9cnIBVAkmdPeMzmPGkawlkDQhSpLXkYunCFVO0IYsifFk_aSYkw?key=UPPRKkHOQa9wbf4HNKU3covr)

  
  

## 12.8.3 Attribution de sous-réseaux IPv6 

  

Avec plus de 65 000 sous-réseaux disponibles, l'administrateur réseau doit concevoir un schéma logique adapté aux besoins.

---

### Points clés :

1. Flexibilité des sous-réseaux :
    

- IPv6 permet de créer des sous-réseaux uniformes pour LAN et liaisons série, tous avec la même longueur de préfixe (généralement /64).
    

1. Absence de gaspillage problématique :
    

- Contrairement à IPv4, l’utilisation d’un espace d’adresses important pour des réseaux peu peuplés (comme les liaisons série) n’est pas préoccupante.
    

1. Simplification du design :
    

- La logique IPv6 permet de concevoir des topologies cohérentes sans se soucier de la conservation d’adresses, grâce à l’énorme espace d'adressage disponible.
    

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcgNH-xv5wuT3o8_PrN63s6JLySzn0RTv43dQB_sxYchZOKjzKb2ROy0R77xeBRGCTzWVAnV36l5Wwfqqp8mWHoLpnioem1yelYd7SPjSBR-Peqa3Gw6kNCA11Ye6f3wkESqEmTqA?key=UPPRKkHOQa9wbf4HNKU3covr)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfo_EvTG-2b6U_fJEMznBgjxtwZjn2Y-y7Mb-soML6IKj4Kb1-K7RxdSuB-hkplOYqkwI-E6TTdsd2cYdComUT6vUTkeebXUbxz4TEaDX6lGt1xHWqwn__NOKHwTiiwbcHOER64jQ?key=UPPRKkHOQa9wbf4HNKU3covr)

  
  
  

## 12.8.4 Routeur est configuré avec des sous-réseaux IPv6 

  

Comme pour la configuration IPv4, l'exemple indique que chacune des interfaces du routeur a été configurée pour utiliser un sous-réseau IPv6 différent.

### Configuration de l'adresse IPv6 sur le routeur R1

  
```shell

R1(config)# interface gigabitethernet 0/0/0

R1(config-if)# ipv6 address 2001:db8:acad:1::1/64

R1(config-if)# no shutdown

R1(config-if)# exit

R1(config)# interface gigabitethernet 0/0/1

R1(config-if)# ipv6 address 2001:db8:acad:2::1/64

R1(config-if)# no shutdown

R1(config-if)# exit

R1(config)# Interface série 0/0/0

R1(config-if)# ipv6 address 2001:db8:acad:3::1/64

R1(config-if)# no shutdown

```
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd9AsOIJKZXEZiPsJzI3uXQkJCt64VtTT1AWMKfvDLra3OLYcWLsIaMTP2mjdFIEaVTskoK4SZ-4ZtmOd9JivqkEkHUw1bA4nkdg72U7-2Q8E2j-GA4bZakRuSm3iL8X5PYI9vq?key=UPPRKkHOQa9wbf4HNKU3covr)

  

CMD

  
  

```
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64

R1(config-if)# ipv6 address fe80::1:1 link-local

R1(config-if)# no shutdown

  

ipv6 unicast-routing

  

show ipv6 interface brief

  

show ipv6 route

  

ping 2001:db8:acad:1::10
```