Here is a correction of the provided IP Routing exam:

**QCM (Multiple Choice Questions)**

1. **Quelles routes sont présentes dans la table de routage?**
    
    - **Réponse correcte:** c. les connexions directes
        
    - **Explication:** Lorsqu'aucune protocole de routage dynamique ou route statique n'est configuré, la table de routage contient uniquement les réseaux directement connectés aux interfaces actives du routeur.
2. **Pour RIP Version 1. laquelle de ces assertions est vrai ?**
    
    - **Réponse correcte:** c. c'est un protocole réseau vecteur de distance
        
    - **Explication:** RIPv1 est un protocole de routage à vecteur de distance. Il n'envoie pas d'informations sur les masques de sous-réseaux, ne prend pas en charge l'authentification, et ne prend pas en charge VLSM (Variable Length Subnet Mask).
        
3. **Partons du principe que le protocole EIGRP est appliqué sur les deux routeurs et que la récapitulation automatique est activée, que devez-vous configurer pour vous assurer que RI atteigne le réseau 2.2.2.0/24 ?**
    
    - **Réponse correcte:** a. Utilisez la commande no auto-summary pour désactiver la récapitulation automatique.
        
    - **Explication:** Avec la récapitulation automatique activée et des réseaux discontinus (2.1.1.0/24 et 2.2.2.0/24 séparés par 192.168.5.0), EIGRP pourrait mal récapituler les routes. La désactivation de la récapitulation automatique permet d'annoncer les sous-réseaux spécifiques. EIGRP prend en charge VLSM, mais la récapitulation automatique peut causer des problèmes dans ce scénario.
        
4. **Pour RIP Version2. laquelle de ces assertions est fausse ?**
    
    - **Réponse correcte:** d. il utilise 12 sauts comme métrique de mesure infinie
        
    - **Explication:** RIP (v1 et v2) utilise 16 sauts comme métrique pour l'infini. Les assertions a, b et c sont vraies pour RIPv2 (protocole à vecteur de distance utilisant le nombre de sauts, utilise des compteurs de retenue et la règle "split horizon" pour prévenir les boucles).
        
5. **Pour supprimer la route par défaut du routeur R4 quelle commande faut-il utiliser ?**
    
    - **Réponse correcte:** c. R4(config)#no ip route 0.0.0.0 0.0.0.0 192.168.3.1
        
    - **Explication:** La commande `no ip route` suivie de la définition de la route (ici, la route par défaut `0.0.0.0 0.0.0.0` et l'adresse du saut suivant) supprime la route statique.
6. **Que réalise la commande suivante sur le routeur R4: R4(config)#ip route 192.168.2.0 255.255.255.0 ethernet 1/0?**
    
    - **Réponse correcte:** c. elle réalise la configuration d'une route statique
        
    - **Explication:** La commande `ip route` est utilisée pour configurer une route statique.
7. **Quelle commande permet d'enregistrer les modifications apportées à un routeur Cisco ?**
    
    - **Réponse correcte:** a. R1#copy running-config startup-config
        
    - **Explication:** Cette commande copie la configuration en cours d'exécution (RAM) vers la configuration de démarrage (NVRAM), sauvegardant ainsi les modifications en cas de redémarrage.
8. **Quelle commande permet de passer en mode de configuration global sur le routeur R1 ?**
    
    - **Réponse correcte:** a. R1#conft (une abréviation courante pour `configure terminal`)
        
    - **Explication:** La commande complète est `configure terminal`. `conft` est une abréviation acceptée.
9. **Quelle commande permet d'activer RIP sur le routeur RI?**
    
    - **Réponse correcte:** a. R1(config)#router rip
        
    - **Explication:** Cette commande entre dans le mode de configuration du protocole de routage RIP.
10. **Quel composant du routeur stocke les fichiers de configuration même lorsque le routeur est hors tension?**
    
    - **Réponse correcte:** c. La NVRAM
        
    - **Explication:** La NVRAM (Non-Volatile Random-Access Memory) stocke la configuration de démarrage (startup-config). La mémoire flash stocke l'IOS, la ROM contient le bootstrap, et la RAM contient la configuration en cours (running-config) qui est volatile.
11. **Sous CISCO, quel protocole permet de visualiser à partir d'un switch des informations sur le switch ou routeur voisin Le nom du switch ou routeur - Le port sur lequel on est connecté**
    
    - **Réponse correcte:** d. CDP
        
    - **Explication:** CDP (Cisco Discovery Protocol) est un protocole propriétaire de Cisco qui permet de recueillir des informations sur les périphériques Cisco directement connectés.
12. **Parmi les propositions suivantes, laquelle correspond au principe de la commutation?**
    
    - **Réponse correcte:** b. mettre en relation un port d'entrée et un port de sortie
        
    - **Explication:** La fonction principale d'un commutateur est de recevoir des trames sur un port et de les transmettre vers le port de destination approprié.
13. **Quelle est la valeur de priorité de routeur par défaut pour tous les routeurs Cisco OSPF?**
    
    - **Réponse correcte:** b. 1
        
    - **Explication:** La priorité OSPF par défaut sur les routeurs Cisco est 1.
14. **Le routeur du schéma ci-dessous est utilisé en routeur on stick pour router les paquets des différents PC appartenant à des VLANs différents. En supposant que les sous-interfaces du routeur sont correctement configurées. quelle commande (ou suite de commandes) est nécessaire pour router les paquets entre les sous-interfaces?**
    
    - **Réponse correcte:** a. aucune commande n'est requise
        
    - **Explication:** Si les sous-interfaces sont correctement configurées avec des adresses IP et une encapsulation 802.1Q, le routeur pourra router entre les VLANs sans configuration de protocole de routage supplémentaire pour ces réseaux directement connectés. Les protocoles de routage comme OSPF (options b et d) sont utilisés pour échanger des informations de routage avec _d'autres_ routeurs.
15. **On vous donne cette plage d'adresses: 193.14.68.32/27. Quelle est la dernière adresse IP utilisable?**
    
    - **Réponse correcte:** a. 193.14.68.62
        
    - **Explication:** Un masque /27 signifie 232−27=25=32 adresses par sous-réseau. Le réseau est 193.14.68.32. L'adresse de diffusion est 193.14.68.(32+32-1) = 193.14.68.63. La dernière adresse IP utilisable est donc 193.14.68.62.
16. **On vous donne cette plage d'adresses: 193.14.68.0/24. Quel est le premier sous-réseau de 30 machines maximum?**
    
    - **Réponse correcte:** d. 193.14.68.0/27
        
    - **Explication:** Pour 30 machines, il faut 2n−2≥30. 25−2=30. Il faut donc 5 bits pour les hôtes. Le masque sera / (32-5) = /27. Le premier sous-réseau sera 193.14.68.0/27. Un masque /28 donnerait 24−2=14 hôtes. Un masque /26 donnerait 26−2=62 hôtes. Un masque /30 donnerait 22−2=2 hôtes.
17. **Quelle est la caractéristique de RIPv2?**
    
    - **Réponse correcte:** b. supporte le VLSM: Variable length subnet mask
        
    - **Explication:** RIPv2 supporte VLSM car il envoie le masque de sous-réseau dans ses mises à jour, contrairement à RIPv1. Il envoie ses mises à jour en multicast (224.0.0.9), pas en broadcast. Il utilise Bellman-Ford (pas SPF ou DUAL ).
        
18. **Quelle est la taille minimale de l'entête d'un paquet IP?**
    
    - **Réponse correcte:** c. 160 bits (ce qui équivaut à 20 octets, l'option n'est pas directement présente mais c'est la plus proche si on considère une erreur de frappe entre bits et octets, ou une des options est incorrecte). La taille minimale de l'en-tête IPv4 est de 20 octets (160 bits). L'option a. 32 bits est incorrecte.
        
    - **Correction basée sur les options et la connaissance générale:** La taille minimale de l'en-tête IPv4 est de 20 octets. 20 octets * 8 bits/octet = 160 bits. L'option c est 160 bits.
19. **Vous devez modifier les mots de passe du routeur en raison d'une violation de sécurité. Quelles informations donnent les entrées de configuration suivantes? Router (config)# line vty 0 3 Router (config-line)# password c13c0 Router (config-line)# login**
    
    - **Réponse correcte:** a. ces entrées spécifient trois lignes Telnet pour l'accès à distance (En réalité, "line vty 0 3" spécifie _quatre_ lignes : 0, 1, 2, et 3).
        
    - **Explication:** `line vty 0 3` configure les lignes de terminal virtuel 0 à 3, typiquement utilisées pour l'accès Telnet ou SSH. `password c13c0` définit le mot de passe pour ces lignes, et `login` active la vérification du mot de passe.
20. **Pour établir une contiguïté voisine, deux routeurs OSPF échangeront des paquets hello. Quelles sont les deux valeurs dans les paquets hello qui doivent correspondre sur les deux routeurs? (Choisissez deux réponses.)**
    
    - **Réponses correctes:** b. Intervalle Hello et c. Intervalle Dead
        
    - **Explication:** Pour que deux routeurs OSPF deviennent voisins, plusieurs paramètres dans leurs paquets Hello doivent correspondre, notamment les intervalles Hello et Dead, le type de zone, et l'authentification (si configurée). L'ID de routeur doit être unique.
21. **Quelle condition l'administrateur réseau doit-il vérifier avant de tenter de mettre à niveau une image du logiciel Cisco IOS à l'aide d'un serveur TFTP?**
    
    - **Réponse correcte:** d. vérifier qu'il y a suffisamment de mémoire Flash pour la nouvelle image Cisco IOS à l'aide de la commande show flash
        
    - **Explication:** Il est crucial de s'assurer qu'il y a assez d'espace dans la mémoire Flash pour stocker la nouvelle image IOS.
22. **Lorsque l'administrateur réseau tente de sauvegarder le logiciel Cisco IOS du routeur, il obtient les informations affichées. Quelle est la raison possible de cette sortie? (%Error opening tftp:)**
    
    - **Réponse correcte:** c. le routeur ne peut pas se connecter au serveur TFTP
        
    - **Explication:** L'erreur "%Error opening tftp:" indique généralement un problème de connectivité avec le serveur TFTP (par exemple, le serveur n'est pas joignable, le service TFTP ne fonctionne pas sur le serveur, ou un pare-feu bloque la connexion).
23. **Quelle est l'adresse IP qui ne peut pas être utilisée comme adresse de machine?**
    
    - **Réponse correcte:** a. 116.74.250.10/30
        
    - **Explication:**
        
        - Pour 116.74.250.10/30: Le réseau est 116.74.250.8 (/30 donne des blocs de 4 adresses). Les adresses sont .8 (réseau), .9 (hôte), .10 (hôte), .11 (broadcast). Donc 116.74.250.10 est une adresse hôte valide.
        - Pour 208.28.220.43/30: Le réseau est 208.28.220.40. Les adresses sont .40 (réseau), .41 (hôte), .42 (hôte), .43 (broadcast). **Donc 208.28.220.43 est une adresse de broadcast et ne peut pas être une adresse de machine.**
        - Pour 192.168.10.20/30: Le réseau est 192.168.10.20. Les adresses sont .20 (réseau), .21 (hôte), .22 (hôte), .23 (broadcast). Donc 192.168.10.20 est une adresse réseau.
        - Pour 244.26.17.9/30: Le réseau est 244.26.17.8. Les adresses sont .8 (réseau), .9 (hôte), .10 (hôte), .11 (broadcast). Donc 244.26.17.9 est une adresse hôte valide.
    - **Correction basée sur l'analyse:** L'option b. 208.28.220.43/30 est une adresse de broadcast. L'option c. 192.168.10.20/30 est une adresse réseau. Les deux ne peuvent pas être utilisées comme adresse de machine. Il y a potentiellement une erreur dans la question ou les options car il y a deux réponses qui ne peuvent être des adresses de machine. Si on doit choisir _une seule_, la question est ambiguë. Cependant, l'option marquée "a" dans le document source est 116.74.250.10/30, qui est une adresse hôte utilisable. L'option **b** est une adresse de broadcast. L'option **c** est une adresse réseau.
        
        Reconsidérant la question : "Quelle est l'adresse IP qui ne peut pas être utilisée comme adresse de machine?"
        
        b. 208.28.220.43/30: Réseau 208.28.220.40, Broadcast 208.28.220.43. Non utilisable.
        
        c. 192.168.10.20/30: Réseau 192.168.10.20, Broadcast 192.168.10.23. Non utilisable (c'est une adresse réseau).
        
        Si la question demande une adresse de machine non valide, b et c le sont. Si l'intention de l'option a. était de vérifier une adresse réseau ou broadcast, elle est mal formulée car c'est une adresse hôte valide.
        
        En choisissant celle qui est explicitement une adresse de broadcast: b. 208.28.220.43/30
        
24. **Examinez l'illustration. Un administrateur réseau a configuré les minuteurs OSPF sur les valeurs illustrées dans le graphique. Quel est le résultat de la configuration manuelle des minuteurs?**
    
    - **Réponse correcte:** a. Le minuteur Dead R1 arrive à expiration entre les paquets Hello provenant de R2.
        
    - **Explication:** Pour que l'adjacence OSPF se forme, les minuteurs Hello et Dead doivent correspondre entre les voisins. Ici, R1 a Hello=5s, Dead=20s. R2 a Hello=25s, Dead=100s. R1 enverra des Hellos toutes les 5 secondes. R2 attendra 20 secondes (son Dead Interval) avant de considérer R1 comme mort. R2 enverra des Hellos toutes les 25 secondes. R1 attendra 100 secondes (son Dead Interval) pour R2. Cependant, la condition standard est que les _intervalles Hello_ doivent correspondre, et les _intervalles Dead_ doivent correspondre (ou être 4x l'intervalle Hello si par défaut). Puisque les intervalles Hello (5 vs 25) et Dead (20 vs 100) ne correspondent pas, l'adjacence ne se formera pas. Le routeur R1 s'attend à recevoir un paquet Hello de R2 dans son intervalle Dead de 20 secondes. R2 envoie des paquets Hello toutes les 25 secondes. Donc, le minuteur Dead de R1 expirera avant de recevoir un Hello de R2.
25. **Quelle affirmation est exacte à propos du protocole EIGRP?**
    
    - **Réponse correcte:** c. le protocole EIGRP envoie une mise à jour partielle de la table de routage comprenant uniquement les routes modifiées
        
    - **Explication:** EIGRP envoie des mises à jour partielles et bornées, uniquement lorsque des changements topologiques se produisent. EIGRP est propriétaire de Cisco (donc 'a' est faux ). Sa métrique infinie est de 232−1 (pas 16 ). Il utilise le multicast (224.0.0.10) pour ses mises à jour, pas la diffusion.
        
26. **Quelle affirmation caractérise l'équilibrage de charge?**
    
    - **Réponse correcte:** b. l'équilibrage de charge à coût inégal est pris en charge par le protocole EIGRP
        
    - **Explication:** EIGRP est capable d'effectuer un équilibrage de charge sur des chemins de coûts inégaux (via la commande `variance`). L'équilibrage de charge se produit lorsque plusieurs chemins vers une destination ont des métriques considérées comme égales (ou dans la plage de variance pour EIGRP).
27. **Examinez l'illustration. Quelles sont les deux routes qui seront annoncées sur le routeur ISP si la récapitulation automatique est désactivée ? (Choisissez deux réponses.)**
    
    - **Réponses correctes:** b. 10.1.2.0/24 et e. 10.1.4.0/30 (et aussi 10.1.1.0/24, 10.1.3.0/24, 10.1.4.4/30 qui ne sont pas listées comme option unique)
        
    - **Explication:** Si la récapitulation automatique est désactivée, R2 annoncera les sous-réseaux spécifiques qu'il connaît. D'après la table de routage de R2:
        - `10.1.1.0/24` est directement connecté.
        - `10.1.2.0/24` est appris.
        - `10.1.3.0/24` est appris.
        - `10.1.4.0/30` est directement connecté.
        - `10.1.4.4/30` est directement connecté. Parmi les options fournies, `10.1.2.0/24` et `10.1.4.0/30` (qui fait partie de 10.1.4.0/30 et 10.1.4.4/30) seraient annoncées. L'option `a. 10.1.0.0/16` serait une récapitulation.
28. **Que se passe-t-il sur un réseau à vecteur de distance qui n'a pas convergé ?**
    
    - **Réponse correcte:** b. des entrées de table de routage incohérentes
        
    - **Explication:** Avant la convergence, différents routeurs peuvent avoir des informations de routage différentes ou incorrectes, conduisant à des incohérences et potentiellement à des boucles de routage ou à des paquets perdus.
29. **Un technicien réseau a configuré manuellement l'intervalle Hello sur 15 secondes sur l'interface d'un routeur exécutant le protocole OSPFv2. Par défaut, comment l'intervalle Dead sur l'interface sera-t-il affecté ?**
    
    - **Réponse correcte:** c. L'intervalle Dead est à présent de 60 secondes.
        
    - **Explication:** Par défaut, l'intervalle Dead OSPF est quatre fois la valeur de l'intervalle Hello. Donc, si Hello est 15 secondes, Dead deviendra 4 * 15 = 60 secondes.
30. **Quelle commande permet de mettre sous tension une interface de routeur ?**
    
    - **Réponse correcte:** c. Router(config-if)# no shutdown
        
    - **Explication:** La commande `no shutdown` active (met sous tension) une interface.
31. **Quelles informations d'adresse un routeur modifie-t-il parmi les informations qu'il reçoit d'une interface Ethernet associée avant de les retransmettre ?**
    
    - **Réponse correcte:** a. l'adresse source et l'adresse de destination de la couche 2
        
    - **Explication:** Lorsqu'un routeur transmet un paquet d'une interface à une autre, il décapsule et ré-encapsule la trame de couche 2. Cela signifie que les adresses MAC source (remplacée par l'adresse MAC de l'interface de sortie du routeur) et destination (remplacée par l'adresse MAC du prochain saut ou de l'hôte de destination si sur le même segment) sont modifiées. Les adresses IP de couche 3 source et destination restent inchangées (sauf en cas de NAT).
32. **Quelle condition est la plus susceptible d'entraîner une boucle de routage ?**
    
    - **Réponse correcte:** c. routes statiques configurées incorrectement
        
    - **Explication:** Des routes statiques mal configurées peuvent facilement créer des boucles de routage, car elles outrepassent les mécanismes de prévention des boucles des protocoles de routage dynamiques. Un réseau qui converge trop lentement (pas trop rapidement ) est aussi une cause.
        
33. **Quelle commande active le protocole CDP sur l'interface d'un routeur ?**
    
    - **Réponse correcte:** a. Router(config-if)# cdp enable
        
    - **Explication:** CDP est activé par défaut globalement sur les routeurs Cisco. Pour l'activer (ou le désactiver) sur une interface spécifique, on utilise la commande `cdp enable` (ou `no cdp enable`) en mode de configuration d'interface.
34. **Quel est l'objectif d'une route Null0 dans la table de routage?**
    
    - **Réponse correcte:** b. Empêcher les boucles de routage
        
    - **Explication:** Une route Null0 est une interface virtuelle vers laquelle les paquets peuvent être routés pour être écartés. C'est souvent utilisé lors de la récapitulation de routes pour éviter les boucles de routage pour les adresses au sein du bloc récapitulé qui n'existent pas spécifiquement.
35. **Table de routage: quel événement peut occasionner une mise à jour déclenchée ?**
    
    - **Réponse correcte:** c. installation d'une route dans la table de routage
        
    - **Explication:** Les mises à jour déclenchées (triggered updates) sont envoyées immédiatement en réponse à un changement dans la topologie du réseau, comme l'installation d'une nouvelle route, la perte d'une route, ou un changement de métrique.
36. **Quel algorithme est exécuté par les protocoles de routage d'état des liens pour calculer le chemin le plus court vers les réseaux de destination?**
    
    - **Réponse correcte:** b. Dijkstra
        
    - **Explication:** Les protocoles d'état des liens, comme OSPF et IS-IS, utilisent l'algorithme de Dijkstra (Shortest Path First - SPF) pour calculer le chemin le plus court. DUAL est utilisé par EIGRP. Bellman-Ford est utilisé par RIP.
        
37. **Quelle est l'adresse IP réseau dans laquelle se trouve l'adresse 82.178.247.174/11?**
    
    - **Réponse correcte:** a. 82.160.0.0
    - **Explication:** Un masque /11 signifie que les 11 premiers bits sont pour le réseau. Le masque est 255.224.0.0. Adresse IP: 82.178.247.174 -> 01010010 . 10110010 . 11110111 . 10101110 Masque /11: 11111111 . 11100000 . 00000000 . 00000000 -> 255.224.0.0 Adresse réseau (ET logique bit à bit): 01010010 . 10100000 . 00000000 . 00000000 -> 82.160.0.0. L'option d. 82.128.0.0 est incorrecte.
        
38. **La table de routage choisit les meilleures routes vers une destination entre process (route statique. protocoles de routage) à partir de:**
    
    - **Réponse correcte:** c. distance administrative
        
    - **Explication:** La distance administrative (AD) est utilisée pour choisir entre des routes vers la même destination apprises via différents protocoles de routage ou par configuration statique. La route avec la plus faible AD est préférée. La métrique est utilisée pour choisir entre des routes apprises par le _même_ protocole de routage.
39. **Un administrateur réseau a attribué le bloc d'adresses IPv4 10.10.240.0/20 à un LAN. Les adresses 10.10.247.1/21 et 10.10.248.10/24 ont été attribuées à deux périphériques, situés sur deux sous-réseaux différents, mais contigus. L'administrateur doit créer un troisième sous-réseau à partir de la plage d'adresses restante. Pour optimiser l'utilisation de cet espace d'adressage, le nouveau sous-réseau doit suivre directement les sous-réseaux existants. Quelle est la première adresse d'hôte disponible dans le sous-réseau disponible suivant?**
    
    - **Réponse correcte:** b. 10.10.249.1 (si le troisième sous-réseau est /24)
    - **Explication:**
        - Bloc initial: 10.10.240.0/20. Plage: 10.10.240.0 à 10.10.255.255.
        - Premier sous-réseau utilisé (pour 10.10.247.1/21): Un masque /21 a 232−21=211=2048 adresses. Le réseau est 10.10.240.0/21 (plage 10.10.240.0 - 10.10.247.255). L'adresse 10.10.247.1/21 est dans ce bloc.
        - Deuxième sous-réseau utilisé (pour 10.10.248.10/24): Un masque /24 a 232−24=28=256 adresses. Le réseau est 10.10.248.0/24 (plage 10.10.248.0 - 10.10.248.255). L'adresse 10.10.248.10/24 est dans ce bloc.
        - Le premier bloc va jusqu'à 10.10.247.255.
        - Le deuxième bloc commence à 10.10.248.0 et va jusqu'à 10.10.248.255.
        - Le prochain sous-réseau disponible commence après 10.10.248.255, soit à 10.10.249.0.
        - La première adresse hôte disponible dans un sous-réseau 10.10.249.0/X serait 10.10.249.1 (en supposant un masque qui permet des hôtes, par exemple /24). L'option d. 10.10.255.17 est incorrecte.
            
40. **Quelle étape prend un routeur compatible OSPF immédiatement après avoir établi une contiguïté avec un autre routeur?**
    
    - **Réponse correcte:** d. échange d'annonces à l'état de lien
        
    - **Explication:** Après que deux routeurs OSPF ont établi une adjacence (état Full), ils échangent leurs bases de données d'états de liens (LSDB) en envoyant des annonces d'état de liens (LSA). Ensuite, ils exécutent l'algorithme SPF pour construire la table de routage.
        
41. **Un administrateur réseau conçoit un modèle d'adressage IPv4 et a besoin des sous-réseaux suivants: 1 sous-réseau de 100 hôtes, 2 sous-réseaux de 80 hôtes, 2 sous-réseaux de 30 hôtes, 4 sous-réseaux de 20 hôtes. Quelle combinaison de sous-réseaux et de masques fournit le meilleur plan d'adressage compte tenu de ces conditions?**
    
    - **Réponse correcte:** (Nécessite une analyse VLSM détaillée, l'option b semble la plus plausible mais il faut vérifier).
        
    - **Analyse:**
        
        - 100 hôtes: 2n−2≥100⟹27−2=126 hôtes. Nécessite un masque / (32-7) = /25 (255.255.255.128).
        - 80 hôtes: 2n−2≥80⟹27−2=126 hôtes. Nécessite un masque /25 (255.255.255.128).
        - 30 hôtes: 2n−2≥30⟹25−2=30 hôtes. Nécessite un masque / (32-5) = /27 (255.255.255.224).
        - 20 hôtes: 2n−2≥20⟹25−2=30 hôtes. Nécessite un masque /27 (255.255.255.224).
        
        Comparons avec les options:
        
        - Option a: 9 x /25 (126 hôtes). Ne correspond pas aux besoins variés.
            
        - Option b: 3 x /25 (126 hôtes) et 6 x /27 (30 hôtes).
            
            - 1 x 100 hôtes -> 1 x /25 (OK, reste de la place)
            - 2 x 80 hôtes -> 2 x /25 (OK, reste de la place)
            - Total de 3 x /25 utilisés.
            - 2 x 30 hôtes -> 2 x /27 (OK)
            - 4 x 20 hôtes -> 4 x /27 (OK)
            - Total de 6 x /27 utilisés. Cette option semble viable et utilise correctement les masques pour les besoins.
        - Option c: /25 (126 hôtes), mais dit /192 (qui est /26, 62 hôtes). /240 (qui est /28, 14 hôtes). Incohérences dans les masques et le nombre d'hôtes.
            
        - Option d: /192 (est /26, 62 hôtes) pour 126 hôtes. /224 (est /27, 30 hôtes) pour 80 hôtes (pas assez). /240 (est /28, 14 hôtes) pour 30 hôtes (pas assez).
        
        **La meilleure option basée sur l'analyse est b.**
        
42. **Le réseau représenté sur le schéma présente un problème d'acheminement du trafic qui serait dû au système d'adressage. Quel est ce problème compte tenu du système d'adressage utilisé dans la topologie?**
    
    - **Réponse correcte:** c. Le sous-réseau affecté à l'interface Serial0 du routeur 1 se trouve sur un autre sous-réseau de l'adresse attribuée à l'interface Serial0 du routeur1 2. (L'option b est marquée mais se réfère à une liaison série et l'interface Ethernet de routeur 3.)
        
    - **Analyse des adresses:**
        
        - Router1 E0: 192.1.1.65/26 (Réseau: 192.1.1.64, Broadcast: 192.1.1.127)
        - Router1 S0: 192.1.1.206/30 (Réseau: 192.1.1.204, Hôtes: .205, .206, Broadcast: 192.1.1.207)
        - Router2 S0 (connecté à R1 S0): 192.1.1.205/30 (Même réseau que R1 S0, c'est correct)
        - Router2 E0: 192.1.1.129/26 (Réseau: 192.1.1.128, Broadcast: 192.1.1.191)
        - Router2 S1: 192.1.1.245/30 (Réseau: 192.1.1.244, Hôtes: .245, .246, Broadcast: 192.1.1.247)
        - Router3 S0 (connecté à R2 S1): 192.1.1.246/30 (Même réseau que R2 S1, c'est correct)
        - Router3 E0: 192.1.1.193/28 (Réseau: 192.1.1.192, Broadcast: 192.1.1.207)
        
        Vérifions les options:
        
        - a. L'adresse attribuée à l'interface Ethernet0 du routeur 1 (192.1.1.65/26) est une adresse hôte (réseau .64, broadcast .127). Faux.
        - b. Le sous-réseau configuré sur la liaison série entre les routeurs 1 et 2 (192.1.1.204/30) chevauche le sous-réseau affecté à l'interface Ethernet0 du routeur 3 (192.1.1.192/28).
            - R1S0-R2S0: 192.1.1.204 - 192.1.1.207
            - R3E0: 192.1.1.192 - 192.1.1.207
            - Il y a un chevauchement (spécifiquement l'adresse 192.1.1.207 est le broadcast du premier et une adresse dans le second). **Ceci est un problème.**
        - c. Le sous-réseau affecté à l'interface Serial0 du routeur 1 (192.1.1.204/30) se trouve sur un autre sous-réseau de l'adresse attribuée à l'interface Serial0 du routeur 2 (192.1.1.204/30). Faux, elles sont sur le même sous-réseau.
        - d. Le sous-réseau affecté à l'interface Ethernet0 du routeur 2 (192.1.1.128/26) chevauche le sous-réseau affecté à l'interface Ethernet du routeur 3 (192.1.1.192/28).
            - R2E0: 192.1.1.128 - 192.1.1.191
            - R3E0: 192.1.1.192 - 192.1.1.207
            - Pas de chevauchement. Faux.
                
        
        **La réponse correcte est b.**
        
43. **Quelles sont les raisons de l'apparition d'une boucle de routage dans un réseau IP?**
    
    - **Réponse correcte:** a. Des routes statiques configurées incorrectement
        
    - **Explication:** Des routes statiques mal configurées sont une cause fréquente de boucles de routage. L'apprentissage de routes via deux protocoles (redistribution) peut aussi causer des boucles si ce n'est pas fait prudemment. L'absence d'une route par défaut cause des problèmes d'atteignabilité, pas directement des boucles.
        
44. **Toutes les routes sont annoncées et pleinement opérationnelles sur tous les routeurs. Quel énoncé sur le chemin que les données empruntent entre le routeur A et le routeur B est vrai?**
    
    - **Réponse correcte:** (Nécessite d'analyser les métriques pour chaque protocole).
        
    - **Analyse du schéma (en supposant des routeurs A, B, C, D dans la topologie en losange, avec A en haut à gauche, B en haut à droite, C en bas à gauche, D au milieu en bas):**
        
        - Chemins possibles de A à B (en supposant que le routeur en haut à droite est B):
            1. A -> (1.5 Mbps) -> B (direct si c'est bien B, ou via un autre routeur)
            2. A -> (1.5 Mbps) -> C -> (56 Kbps) -> D -> (1.5 Mbps) -> B
            3. A -> (1.5 Mbps) -> C -> (1.5 Mbps) -> B (si C est connecté à B en bas) Le schéma est un peu ambigu sur l'identité de B par rapport aux liens. Supposons que la topologie est: A ---1.5M--- D /  
                1.5M 1.5M /  
                C ----56K---- E ---1.5M--- B (Hypothétique pour illustrer)
        
        Il est difficile de répondre sans une topologie claire et les routeurs A et B identifiés.
        
        Cependant, en se basant sur les options:
        
        - a. Si EIGRP est utilisé, il choisit le chemin avec la meilleure métrique (composite de bande passante et délai). L'équilibrage de charge sur des chemins de coût égal est possible.
        - b. RIPv1 utilise le nombre de sauts. S'il y a plusieurs chemins avec le même nombre de sauts, il peut y avoir équilibrage.
            
        - c. Si EIGRP (AD 90 par défaut pour interne) et OSPF (AD 110 par défaut) sont utilisés, EIGRP sera préféré en raison de sa distance administrative plus faible. Donc cette affirmation est fausse.
            
        - d. RIPv2 utilise aussi le nombre de sauts.
            
        
        Sans une topologie plus claire, il est difficile de valider a, b, ou d. Cependant, c est définitivement fausse. Si on prend la topologie de la page 10, question 44. Et si A est le routeur en haut à gauche et B celui en haut à droite.
        
        Chemin 1: A -> (routeur en haut au milieu) -> B (2 sauts, bande passante limitée par le plus lent des deux liens 1.5Mbps)
        
        Chemin 2: A -> (routeur en bas à gauche) -> (routeur en bas au milieu via 56Kbps) -> (routeur en haut au milieu) -> B (4 sauts, bande passante 56Kbps)
        
        Chemin 3: A -> (routeur en bas à gauche) -> (routeur en bas à droite) -> (routeur en haut au milieu) -> B (4 sauts, bande passante 1.5Mbps)
        
        - **RIP (v1 ou v2):** Préfèrera le chemin 1 (2 sauts) aux chemins 2 et 3 (4 sauts). Pas d'équilibrage entre des chemins de nombres de sauts différents.
        - **EIGRP:** La métrique prend en compte la bande passante. Le chemin via le lien 56Kbps aura une très mauvaise métrique. EIGRP pourrait équilibrer la charge sur des chemins de coûts égaux (ou inégaux avec `variance`). Si les liens de 1.5 Mbps sont considérés comme égaux, un équilibrage sur les chemins qui n'utilisent pas le 56Kbps pourrait avoir lieu si les coûts sont égaux.
        
        Option a: "Si EIGRP est utilisé avec les configurations par défaut, les données seront également réparties entre deux chemins A. D. B et A. C. B." Cela implique une topologie spécifique où D et C sont des points intermédiaires.
        
        **Vu les options et le manque de clarté, cette question est difficile à corriger de manière définitive sans plus d'informations ou une meilleure illustration de la topologie avec A et B clairement identifiés.** Cependant, si l'on suppose une topologie symétrique simple avec deux chemins de coût égal et un chemin de coût plus élevé, EIGRP et RIP pourraient équilibrer la charge sur les chemins de coût égal.