Okay, based on your notes, the exam example (`td1.pdf`), and the course material we summarized earlier, here is a study guide focusing on the routing table to help you prepare for your exam.

---

## Guide de Préparation à l'Examen de Routage – Focus sur la Table de Routage

Votre enseignant a insisté sur l'importance de la **table de routage**. Ce guide se concentre sur ce sujet crucial, en intégrant vos notes de révision et les éléments de l'examen d'exemple (`td1.pdf`).

**Objectif Principal:** Comprendre comment la table de routage est construite, comment elle est lue, et comment elle est utilisée par le routeur pour prendre des décisions.

**1. Introduction : Pourquoi la Table de Routage est Essentielle**

- La table de routage est comme la "carte routière" du routeur.
- Elle contient la liste des réseaux que le routeur connaît et comment les atteindre.
- Sans une table de routage correcte, le routeur ne peut pas acheminer les paquets vers des réseaux distants.
- Le routeur consulte cette table pour chaque paquet qu'il doit acheminer.

**2. Concepts Fondamentaux (Rappel Chapitre 1)**

- **Rôle du Routeur:** Interconnecter différents réseaux et déterminer le meilleur chemin pour acheminer les paquets.
- **Méthodes de Commutation/Transfert (Packet Forwarding):** _(Référence page 11 du cours)_
    - **Commutation de processus (Process Switching):** Ancienne méthode, le CPU est impliqué pour chaque paquet. Lent.
    - **Commutation rapide (Fast Switching):** Utilise un cache pour stocker les informations du prochain saut. Plus rapide.
    - **CEF (Cisco Express Forwarding):** Méthode la plus récente et la plus rapide. Utilise des tables pré-calculées (FIB et Adjacency Table) pour des décisions très rapides.

**3. Construction de la Table de Routage**

Un routeur apprend les routes de trois manières principales :

- **Réseaux Directement Connectés:**
    - Ajoutés automatiquement lorsque vous configurez une adresse IP sur une interface et que celle-ci est active (`no shutdown`).
    - Identifiés par `C` (Connected) et `L` (Local - adresse IP de l'interface elle-même, depuis IOS 15) dans la table de routage.
    - Distance Administrative (AD) = 0 (la plus fiable).
- **Routes Statiques:**
    - Configurées manuellement par l'administrateur.
    - Identifiées par `S` dans la table de routage.
    - AD = 1 par défaut.
- **Routes Dynamiques:**
    - Apprises automatiquement via des protocoles de routage (RIP, EIGRP, OSPF...).
    - Identifiées par une lettre spécifique au protocole (e.g., `R` pour RIP, `D` pour EIGRP, `O` pour OSPF).
    - Chaque protocole a sa propre AD par défaut (voir section 5).

**4. Routage Statique et la Table de Routage (Focus Chapitre 2 & Examen `td1.pdf`)**

- **Utilité:** Petits réseaux, réseaux d'extrémité (stub networks), routes par défaut, contrôle précis du chemin.
- **Commande `ip route`:** _(Réponse à la Q1 de l'examen `td1.pdf`)_
    - Forme 1: `ip route <destination-network> <subnet-mask> <next-hop-ip-address>`
    - Forme 2: `ip route <destination-network> <subnet-mask> <exit-interface>`
    - (Il existe aussi une forme combinant les deux, souvent recommandée pour les réseaux multi-accès comme Ethernet).
- **Recherche Récursive (Recursive Lookup):** _(Réponse à la Q2 de l'examen `td1.pdf`)_
    - **Définition:** Le routeur doit effectuer une deuxième recherche dans la table de routage pour trouver comment atteindre l'adresse IP du prochain saut (next-hop) spécifiée dans la première route statique.
    - **Quand ?** Cela se produit typiquement lorsque vous utilisez la forme `ip route ... <next-hop-ip-address>` et que le réseau pour atteindre ce `next-hop-ip-address` n'est pas directement connecté. Le routeur doit chercher la route vers le next-hop.
- **Route Statique par Défaut:**
    - Utilisée quand aucune autre route spécifique ne correspond. "Gateway of last resort".
    - Syntaxe: `ip route 0.0.0.0 0.0.0.0 <next-hop-ip | exit-interface>`
- **Route Statique Flottante:**
    - Route de secours.
    - Configurée comme une route statique standard, mais avec une AD plus élevée que la route principale.
    - Exemple: `ip route <network> <mask> <next-hop> 5` (AD de 5 au lieu de 1 par défaut).
- **Résumé de Routes Statiques:** _(Voir Exercice 3 de `td1.pdf`)_
    - Permet de regrouper plusieurs réseaux contigus en une seule route statique plus générale. Utile pour simplifier les tables de routage.
- **Pratique (Exercices 2 & 3 de `td1.pdf`):**
    - Analysez une topologie.
    - Pour chaque routeur, identifiez :
        - Les réseaux directement connectés.
        - Les réseaux distants qu'il doit atteindre.
        - Pour chaque réseau distant, déterminez le meilleur prochain saut (next hop) ou l'interface de sortie.
        - Écrivez la commande `ip route` correspondante.
    - Exemple (R2 dans `td1.pdf`, Exercice 2): R2 connaît 10.5.2.0/24 (C) et 10.5.3.0/24 (C). Il doit apprendre :
        - 10.5.1.0/24 via R1 (10.5.2.1) -> `ip route 10.5.1.0 255.255.255.0 10.5.2.1`
        - 10.5.4.0/24 via R3 (10.5.3.2) -> `ip route 10.5.4.0 255.255.255.0 10.5.3.2`
        - 10.5.5.0/24 via R4 (10.5.3.3) -> `ip route 10.5.5.0 255.255.255.0 10.5.3.3`

**5. Routage Dynamique et la Table de Routage (Focus Chapitre 3 & Notes)**

- **Objectif:** Maintenir la table de routage automatiquement.
- **Classification (Vos Notes):**
    - **IGP (Interior Gateway Protocol):** Routage _à l'intérieur_ d'un Système Autonome (AS). Ex: RIP, EIGRP, OSPF.
    - **EGP (Exterior Gateway Protocol):** Routage _entre_ différents Systèmes Autonomes. Ex: BGP.
    - **Système Autonome (AS):** Domaine de routage sous une même administration (e.g., une entreprise, un FAI).
- **Familles de Protocoles (Vos Notes):**
    - **À Vecteur de Distance (Distance Vector):**
        - Ex: RIP, EIGRP.
        - Fonctionnement: Chaque routeur annonce les réseaux qu'il connaît à ses voisins directs ("routing by rumor"). Moins précis sur la topologie globale.
        - Métriques (Q4 Examen): RIP utilise le nombre de sauts (hops). EIGRP utilise une métrique composite (bande passante, délai, charge, fiabilité).
        - RIPv1 et Masques (Q3 Examen): RIPv1 est _classful_. Il n'envoie pas le masque dans les mises à jour. Il détermine le masque :
            - En appliquant le masque _classful_ par défaut (Classe A, B, C).
            - OU, si l'interface recevant la mise à jour appartient au même réseau _majeur_ (classful) que la route annoncée, il applique le même masque que celui de son interface. C'est pourquoi RIPv1 ne supporte pas VLSM ou les réseaux discontinus.
    - **À État de Liens (Link-State):**
        - Ex: OSPF, IS-IS.
        - Fonctionnement: Chaque routeur construit une carte complète de la topologie de sa zone et calcule le meilleur chemin indépendamment.
        - Métriques (Q4 Examen): OSPF utilise le _Coût_, basé sur la bande passante de l'interface (inversement proportionnel: coût = bande passante de référence / bande passante de l'interface).
- **Distance Administrative (AD):** _(Référence page 40 & Q5 Examen)_
    - **Définition:** Valeur numérique (0-255) indiquant la **préférence** (fiabilité) d'une source de route.
    - **Importance:** Si un routeur apprend la même route via plusieurs sources (e.g., statique et OSPF), il choisit la route avec l'AD **la plus basse** pour l'installer dans la table de routage.
    - **Valeurs par Défaut (à connaître):**
        - Directement Connecté: 0
        - Statique: 1
        - EIGRP (interne): 90
        - OSPF: 110
        - RIP: 120
        - EIGRP (externe): 170

**6. Lire et Comprendre la Table de Routage (`show ip route`)**

Apprenez à décoder chaque partie d'une entrée :

```
   [Route Source] [Destination Network]/[Prefix Length] [[AD]/[Metric]] via [Next Hop] , [Time] , [Outgoing Interface]
S  192.168.4.0/24 [1/0] via 10.5.2.1 , 00:05:10 , Ethernet0/1
|      |    |      | |     |          |         |           |
|      |    |      | |     |          |         |           +--> Interface de sortie locale
|      |    |      | |     |          |         +-------------> Depuis combien de temps la route est connue
|      |    |      | |     |          +-----------------------> Adresse IP du prochain routeur
|      |    |      | |     +----------------------------------> Métrique (coût pour atteindre la destination)
|      |    |      +------------------------------------------> Distance Administrative
|      |    +-------------------------------------------------> Préfixe réseau et longueur
|      +------------------------------------------------------> Réseau de destination
+-------------------------------------------------------------> Source de la route (S=Static, C=Connected, L=Local, D=EIGRP, O=OSPF, R=RIP, *=Candidate Default)
```

- **Longest Match Rule:** Le routeur choisit TOUJOURS la route dans la table qui correspond le plus spécifiquement à l'adresse IP de destination du paquet (celle avec le préfixe le plus long). Par exemple, une route `/25` sera préférée à une route `/24` si les deux correspondent. L'AD n'intervient que si plusieurs sources proposent une route avec le _même_ préfixe.

**7. Commandes Clés à Maîtriser**

- **Vérification Table de Routage:** `show ip route`, `show ipv6 route`
- **Vérification Interfaces:** `show ip interface brief`, `show ipv6 interface brief`, `show interfaces <type/num>` (pour voir l'état, l'IP, le masque, la bande passante, le délai...)
- **Test Connectivité:** `ping <destination>`, `traceroute <destination>`
- **Configuration Statique:** `ip route ...`, `ipv6 route ...`
- **Configuration RIP (si applicable):** `router rip`, `version 2`, `network ...`, `no auto-summary`, `passive-interface ...`, `default-information originate`
- **Configuration de Base:** `hostname`, `enable secret`, `line con 0`, `line vty 0 4`, `password`, `login`, `service password-encryption`
- **Configuration Interface:** `interface <type/num>`, `description ...`, `ip address ...`, `ipv6 address ...`, `no shutdown`, `clock rate ...` (DCE)
- **Sauvegarde Config:** `copy running-config startup-config` (ou `wr`) _(Réponse Q3 Exercice 2 `td1.pdf`)_

**8. Conseils et Exercices Pratiques**

- **Refaites les exercices de `td1.pdf`** :
    - Calculs CIDR (Exercice 1).
    - Construction manuelle des tables de routage statique (Exercice 2 & 3). Écrivez les commandes IOS correspondantes.
    - Comprenez pourquoi chaque route statique est nécessaire.
- **Analysez des sorties `show ip route`:** Trouvez la source, la destination, l'AD, la métrique, le prochain saut, l'interface de sortie. Déterminez quelle route serait choisie pour une IP de destination donnée (longest match).
- **Comprendre la différence AD vs Métrique:** L'AD choisit la _source_ de la route à mettre dans la table. La métrique choisit le _meilleur chemin_ parmi ceux proposés par la _même_ source (protocole dynamique).
- **Concentrez-vous sur les Chapitres 2 (Statique) et 3 (Dynamique/Table Routage)** comme indiqué dans vos notes.

---

Bonne chance pour votre examen ! En vous concentrant sur la compréhension et l'analyse de la table de routage, vous devriez être bien préparé.