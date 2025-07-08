Perfect. I’ll prepare a detailed and structured summary of each chapter from your document—excluding the last chapter on OSPFv3. It will include every important topic, explanation, and concept necessary to fully prepare for your exam on routing.

I'll format it like a comprehensive study guide with chapters, subtopics, key definitions, and examples to ensure you don’t miss anything crucial. I’ll let you know as soon as it’s ready for you to review.

# Chapitre 1 – Routage statique

- **Principe :** Le routage statique consiste à indiquer manuellement les routes vers les réseaux distants. Chaque route statique spécifie l’adresse réseau de destination, son masque, et l’adresse IP du prochain saut (ou l’interface de sortie). Une route statique est indiquée dans la table de routage par le code « S ». La commande Cisco « ip route » (pour IPv4) ou « ipv6 route » (pour IPv6) permet de configurer ces routes. Par exemple, `ip route 192.168.2.0 255.255.255.0 10.0.0.2` configure une route statique vers 192.168.2.0/24 via 10.0.0.2.
    
- **Route par défaut et route flottante :** Une route statique par défaut (0.0.0.0/0 pour IPv4, ::/0 pour IPv6) sert de « passerelle de dernier recours » lorsque la table ne contient pas d’autre correspondance. Une _route statique flottante_ a une distance administrative volontairement plus élevée pour agir comme secours : tant qu’une autre route (plus fiable) est active, elle est ignorée. Si la route principale disparaît, la route flottante « prend le relais ».
    
- **Avantages/Inconvénients :** Les routes statiques sont simples et offrent un contrôle précis du routage. Elles sont adaptées aux petites topologies stables, car elles **ne s’adaptent pas automatiquement** aux changements du réseau. Les routes statiques ne génèrent pas de trafic de mise à jour et consomment peu de ressources, mais nécessitent une reconfiguration manuelle en cas de panne d’un lien ou d’évolution.
    
- **Vérification et commandes :** La table de routage peut être consultée avec `show ip route` (ou `show ipv6 route` pour IPv6). Cette commande liste toutes les routes apprises, y compris les statiques. Les routes statiques y sont marquées “S” et détaillent la destination, le masque, le next-hop et l’interface de sortie. Par exemple, `show ip route static` ou `show ip route [réseau]` permet de filtrer les routes statiques. On utilise aussi des outils de diagnostic comme `ping` et `traceroute`, ainsi que `show ip protocols`, pour vérifier la configuration et le fonctionnement du routage.
    

## Chapitre 2 – Routage dynamique (vecteur de distance)

- **Concept de vecteur de distance :** Les protocoles de type _vecteur de distance_ utilisent l’algorithme de Bellman‑Ford pour calculer les meilleurs chemins. Chaque routeur échange périodiquement l’intégralité (ou des portions) de sa table de routage avec ses voisins. Ces protocoles sont simples à configurer mais convergent lentement et sont sensibles aux boucles de routage. Ils forment un réseau « plat », sans hiérarchie (chaque routeur exécute les mêmes algorithmes). L’exemple le plus connu est le protocole RIP. Cisco a aussi développé IGRP, aujourd’hui remplacé par **EIGRP** (protocole propriétaire avancé).
    
- **RIP / RIPv2 :** RIP utilise le nombre de sauts comme métrique, avec un maximum de 15 (16=infini). Par défaut, RIP classique (RIPv1) diffusait en broadcast tous les 30 s (adresse 255.255.255.255) et ne supportait pas le VLSM ni l’authentification. **RIPv2** a apporté des améliorations clés : c’est un protocole _sans classe_ (support du VLSM et CIDR), il envoie ses mises à jour en multicast à 224.0.0.9 (réduisant la charge sur les hôtes qui n’exécutent pas RIP) et il intègre l’authentification (texte clair ou MD5). RIPv2 transmet le masque de sous-réseau avec chaque route, ce qui permet d’utiliser des sous-réseaux de longueur variable. La distance administrative par défaut de RIP est 120. On active RIP sur un routeur Cisco avec `router rip`, puis `version 2`, suivi de commandes `network <réseau>` pour inclure les réseaux locaux dans le protocole. On vérifie la configuration avec `show ip protocols` ou `show ip route`.
    
- **RIPng (IPv6 RIP) :** Le protocole **RIPng** (Next Generation) est l’équivalent de RIPv2 pour IPv6. C’est également un protocole IGP à vecteur de distance (algorithme Bellman-Ford) utilisant le nombre de sauts comme métrique. RIPng utilise l’adresse multicast IPv6 **FF02::9** pour diffuser ses mises à jour, et ne nécessite pas d’authentification (la sécurité en IPv6 est gérée différemment). Son principe reste similaire à RIPv2 : mise à jour périodique toutes les 30 s, délai d’invalidation à 180 s, etc. Pour configurer RIPng sous IOS, on active d’abord le routage IPv6 globalement (`ipv6 unicast-routing`), puis on crée un processus RIPng (`ipv6 router rip NOM`) et on active RIPng sur chaque interface avec `ipv6 rip NOM` (on assigne ainsi cette interface au protocole RIP pour IPv6).
    
- **EIGRP (Enhanced IGRP) :** EIGRP est un protocole _propriétaire Cisco_ évolué de type vecteur de distance (algorithme DUAL). Il supporte IPv4 et IPv6 (multi-protocoles), convergeant rapidement grâce à ses calculs avancés et routes de secours (feasible successors). La métrique EIGRP est composée (par défaut : bande passante et délai, avec des facteurs K1=1, K3=1). EIGRP permet l’égalisation de charge sur liens de coûts inégaux et gère des mises à jour partielles/incrémentielles. Sa distance administrative interne par défaut est 90 (extérieure 170), ce qui le rend prioritaire par rapport à RIP (120) mais inférieur à la route statique (1).
    
    - _Configuration EIGRP IPv4 :_ Sous IOS on tape `router eigrp <AS>` (numéro de système autonome), puis on déclare les réseaux avec `network <réseau> <wildcard>` (ou simplement `network <classe>`). Par exemple :
        
        ```
        R1(config)# router eigrp 1
        R1(config-router)# network 192.168.1.0  
        R1(config-router)# network 192.168.225.0
        ```
        
        Ces commandes incluent les interfaces connectées aux réseaux spécifiés dans le processus EIGRP. On peut utiliser `passive-interface <int>` pour empêcher les échanges de mise à jour sur certaines interfaces.
        
    - _EIGRP IPv6 :_ La configuration IPv6 se fait en deux étapes : `ipv6 router eigrp <AS>` active EIGRP pour IPv6 et permet de définir le router-id (obligatoire en EIGRP IPv6). Ensuite, on active EIGRP sur chaque interface avec `ipv6 eigrp <AS>`. Par exemple :
        
        ```
        R1(config)# ipv6 router eigrp 1
        R1(config-rtr)# eigrp router-id 1.1.1.1   (nécessaire en IPv6)
        R1(config)# interface GigabitEthernet0/0
        R1(config-if)# ipv6 eigrp 1
        ```
        
        Cette approche permet de déclarer les routes IPv6 apprises par EIGRP. La commande `show ipv6 eigrp neighbors` vérifie la formation des voisinages EIGRP IPv6.
        

## Chapitre 3 – Routage dynamique (état de liens) – OSPFv2
**Un technicien réseau a configuré manuellement l'intervalle Hello sur 15 secondes sur l'interface d'un routeur exécutant le protocole OSPFv2. Par défaut, comment l'intervalle Dead sur l'interface sera-t-il affecté ?**

- **Réponse correcte:** c. L'intervalle Dead est à présent de 60 secondes.

- **Concept OSPF :** OSPF (Open Shortest Path First) est un protocole de routage **à état de liens**. Chaque routeur OSPF recueille la carte complète du réseau (topologie) et calcule indépendamment les chemins les plus courts avec l’algorithme de Dijkstra. OSPF est hiérarchique : il utilise des _aires_ (zones) interconnectées par une aire centrale (backbone, Area 0). Cette hiérarchie améliore la scalabilité et la rapidité de convergence. OSPF supporte les adresses VLSM/CIDR et utilise une métrique appelée **coût**.
    
- **Métrique OSPF :** Le coût OSPF est inversement proportionnel à la bande passante du lien. Par défaut, la référence est 100 Mbit/s. Par exemple, un lien 100 Mbit/s a un coût de 1, un lien 10 Mbit/s a coût 10, etc. Pour un lien 1 Gbit/s, le coût calculé serait 0.1 (mais IOS arrondit à 1 par défaut). On peut ajuster manuellement le coût d’une interface (commande `ip ospf cost`) pour affiner la répartition du trafic.
    
- **Configuration OSPF :** Sous IOS on active OSPF pour IPv4 avec `router ospf <ID>`. Puis on associe les interfaces au protocole en déclarant leurs réseaux : par exemple `network 10.1.1.0 0.0.0.255 area 0` pour indiquer que les interfaces rattachées à 10.1.1.0/24 font partie de l’aire 0. Les routeurs OSPF établissent un voisinage avec ceux partageant la même aire et échangent des LSAs (Link State Advertisements). Les interfaces FastEthernet/ Gigabit échangent des paquets Hello vers le groupe multicast 224.0.0.5 (ou 224.0.0.6 pour DR/BDR).
    
- **Distance administrative :** Par défaut, OSPF interne a une distance administrative de 110. Cela le rend moins prioritaire qu’EIGRP (90) mais plus que RIP (120). Lorsqu’un routeur reçoit plusieurs routes pour une même destination via différents protocoles, il choisit celle du protocole ayant la plus faible distance administrative.
    
- **Vérification OSPF :** On peut utiliser `show ip ospf neighbor` pour vérifier les voisins, `show ip route ospf` pour voir les routes apprises par OSPF, et `show ip protocols` pour récapituler la configuration d’OSPF (analogues à RIP/EIGRP). `show ip route` affiche les routes OSPF avec le code « O » et leur coût entre crochets.


Je vais vous expliquer étape par étape pour clarifier votre confusion concernant la valeur de priorité de routeur par défaut pour tous les routeurs Cisco OSPF. La réponse correcte est **1**, et je vais vous montrer pourquoi.

### Qu'est-ce que la priorité de routeur dans OSPF ?
Dans OSPF (Open Shortest Path First), la **priorité de routeur** est une valeur attribuée à une interface d'un routeur. Elle est utilisée dans les réseaux multi-accès (comme Ethernet) pour élire deux rôles spécifiques :
- Le **Designated Router (DR)** : le routeur principal qui gère les mises à jour OSPF sur le réseau.
- Le **Backup Designated Router (BDR)** : le routeur de secours qui prend le relais si le DR tombe en panne.

Ces élections permettent de réduire le trafic OSPF sur le réseau. Voici comment cela fonctionne :
- Le routeur avec la **priorité la plus élevée** devient le DR.
- Celui avec la **deuxième priorité la plus élevée** devient le BDR.
- En cas d'égalité de priorité, le routeur avec le **Router ID** le plus élevé (une autre valeur, basée sur les adresses IP ou configurée manuellement) gagne.

### Quelle est la valeur par défaut ?
Sur tous les routeurs Cisco, la **priorité OSPF par défaut** est **1**. Cela signifie que, si vous ne modifiez pas cette valeur manuellement, chaque interface d’un routeur Cisco participant à OSPF aura une priorité de 1.

- **Priorité = 1** : Le routeur peut être élu DR ou BDR.
- **Priorité = 0** : Si vous configurez une priorité à 0, le routeur ne participera pas à l’élection (mais ce n’est pas la valeur par défaut).

### Pourquoi pourriez-vous être confus ?
Votre confusion pourrait venir de plusieurs sources possibles :
1. **Valeurs modifiées dans des configurations** : Vous avez peut-être vu des priorités différentes (comme 10 ou 100) dans des exemples ou des réseaux configurés manuellement. Cependant, sans intervention, la valeur reste 1.
2. **Confusion avec d'autres protocoles** : Par exemple, dans HSRP (un autre protocole Cisco), la priorité par défaut est 100. Mais pour OSPF, c’est bien 1.
3. **Router ID vs Priorité** : Le Router ID est une autre notion dans OSPF, utilisée pour identifier les routeurs, mais il est distinct de la priorité.

### Comment vérifier ou changer cette valeur ?
Sur un routeur Cisco, vous pouvez voir ou modifier la priorité avec la commande suivante en mode de configuration d’interface :
```bash
Router(config-if)# ip ospf priority <valeur>
```
Par exemple, pour définir une priorité de 10 :
```bash
Router(config-if)# ip ospf priority 10
```
Mais si vous ne faites rien, la valeur par défaut est **1**.

### Résumé
- La **valeur de priorité de routeur par défaut** pour tous les routeurs Cisco OSPF est **1**.
- Cette valeur s’applique à toutes les interfaces par défaut et est utilisée pour l’élection du DR et du BDR.
- L’explication donnée ("La priorité OSPF par défaut sur les routeurs Cisco est 1") est correcte.

J’espère que cela clarifie les choses pour vous ! Si vous avez encore des doutes ou des questions sur OSPF, n’hésitez pas à me le dire.
    

## Chapitre 4 – Concepts transverses (tables, métriques, etc.)

- **Tables de routage :** Un routeur maintient une table de routage où figure l’ensemble des routes connues (connectées, statiques, ou apprises dynamiquement). Chaque entrée comporte la destination (préfixe), la métrique, le next-hop, l’interface de sortie, et un code identifiant la source (C=connected, S=static, R=RIP, O=OSPF, D=EIGRP, etc.). Par exemple, dans une sortie de `show ip route` on peut lire :
    
    ```
    R 1.1.1.1 [120/1] via 10.1.1.1,  FastEthernet0/0
    O 33.33.33.33 [110/2] via 10.2.2.3, FastEthernet1/0
    D 111.111.111.111 [90/156160] via 10.1.1.1, FastEthernet0/0
    C 10.2.2.0 is directly connected, FastEthernet1/0
    ```
    
    Ici «R» indique une route RIP, «O» OSPF, «D» EIGRP, «C» un réseau connecté. Le nombre entre crochets est `[distance_admin/métrique]`.
    
- **Métriques et Distance Administrative :** La métrique est utilisée **au sein d’un même protocole** pour comparer plusieurs chemins (plus faible est meilleur). Par exemple, ==RIP utilise le nombre de sauts, EIGRP combine bande passante/délai/charge/fiabilité, OSPF utilise un coût basé sur la bande passante. La **distance administrative (AD)** sert à départager des routes _apprises par des protocoles différents_. Chaque type de route a une AD par défaut (plus petite = plus fiable) : connectées=0, statiques=1, EIGRP int=90, OSPF=110, RIP=120, etc.. Ainsi, si une même destination est présente en statique et via RIP, la statique (AD 1) sera préférée.==
    
- **Transfert de paquets (commutation) :** Lorsqu’un paquet arrive, le routeur effectue un _longest prefix match_ sur son adresse de destination dans la table de routage. Trois méthodes de commutation existent : processus, rapide et CEF (Cisco Express Forwarding). En commutation par processus, chaque paquet déclenche un lookup CPU (méthode lente). La commutation rapide utilise un cache local après le premier paquet du flux. CEF, le mécanisme le plus courant, construit une FIB (table de commutation) et des tables de contiguïté, permettant un transfert _très rapide_ et évolutif. Après convergence, CEF est généralement actif par défaut sur IOS.
    
- **IPv4 vs IPv6 :** Les principes de routage sont analogues en IPv6, avec quelques différences de configuration. Par exemple, la commande globale `ipv6 unicast-routing` doit être activée pour effectuer du routage IPv6. Les protocoles dynamiques IPv6 ont leurs propres versions : RIPng (cf. supra) et OSPFv3 (non traité ici), EIGRP IPv6 (activation via les commandes `ipv6 router eigrp` et `ipv6 eigrp`). Les routes statiques IPv6 utilisent `ipv6 route <préfixe> <next-hop>`. Pour vérifier la table IPv6, on utilise `show ipv6 route` (et filtres comme `show ipv6 route static`). En IPv6, le multicast remplace le broadcast (par ex. RIPng utilise FF02::9, alors que RIPv2 utilise 224.0.0.9). Les adresses sites-locales ou link-local peuvent être utilisées comme next-hop pour les routes par défaut IPv6. Enfin, le champ _router-id_ (identifiant de routeur) est requis en routage IPv6 pour certains protocoles (notamment EIGRP et OSPFv3).
    

**Sources :** Synthèse et commandes issues de cours et documentation Cisco/CiscoCCNA (citations intercalées dans le texte).