

---

## **1. Introduction à la haute disponibilité**

La **haute disponibilité (HA)** regroupe les techniques et technologies visant à assurer la disponibilité continue d’un système ou d’un service, même en cas de défaillance matérielle, logicielle ou environnementale. L’objectif est de minimiser les interruptions de service pour garantir une continuité opérationnelle, essentielle dans des contextes critiques comme les entreprises, la santé ou l’industrie.

### **1.1 Enjeux de la HA**
- **Continuité des opérations** : Les systèmes d’information doivent être disponibles 24h/24 pour répondre aux besoins des clients, employés et processus critiques (ex. commerce électronique, contrôle d’accès).
- **Réduction des temps d’arrêt** : Une indisponibilité peut entraîner des pertes financières et de productivité. Par exemple, un taux de disponibilité de **99,9%** équivaut à 8h48m d’arrêt par an, contre 5 minutes pour **99,999%**.
- **Sécurité et fiabilité** : Dans des applications critiques (ex. contrôle industriel), la HA est vitale pour prévenir des incidents graves.

### **1.2 Définitions et indicateurs**
- **Disponibilité** : Probabilité qu’un système soit opérationnel à un instant donné, exprimée en pourcentage (ex. 99,99%).
- **Fiabilité** : Probabilité qu’un système fonctionne sans panne sur une période donnée.
- **Indicateurs clés** :
  - **MTTF (Mean Time To Failure)** : Temps moyen avant une panne.
  - **MTBF (Mean Time Between Failures)** : Temps moyen entre deux pannes (MTBF = MTTF + MTTR).
  - **MTTR (Mean Time To Repair)** : Temps moyen pour réparer une panne.
  - **Formule** : Disponibilité = MTTF/MTBF.
- **Temps d’indisponibilité annuel** (extrait des slides) :
  | Taux de disponibilité | Durée d’indisponibilité par an |
  |-----------------------|---------------------------------|
  | 99%                   | 3 jours 15h             |
  | 99,9%                 | 8h 48min                |
  | 99,99%                | 53min                   |
  | 99,999%               | 5min                    |

---

## **2. Concepts fondamentaux de la HA**

### **2.1 Ressources critiques et SPOF**
- **Single Point of Failure (SPOF)** : Composant dont la défaillance entraîne l’arrêt total du système (ex. disque dur, alimentation, réseau).
- **Redondance** : Duplication des ressources critiques pour éliminer les SPOF, soit au niveau matériel (ex. alimentations multiples), soit logiciel (ex. clusters).

### **2.2 Types de clusters**
Un **cluster** est un groupe de serveurs (nœuds) fonctionnant ensemble pour offrir un service unique. Les principaux types sont :
- **Clusters HPC (High Performance Computing)** : Optimisés pour le calcul intensif.
- **Clusters de répartition de charge (Load Balancing)** : Distribuent les requêtes pour améliorer les performances.
- **Clusters HA** : Garantissent la continuité du service en cas de panne.

### **2.3 Architectures HA**
- **Failover** : Basculement automatique vers un nœud de secours en cas de panne.
- **Actif/Passif** : Un nœud actif, les autres en attente.
- **Actif/Actif** : Tous les nœuds actifs, avec partage de charge et basculement si nécessaire.

---

## **3. Solutions HA sous Linux**

### **3.1 Surveillance et répartition de charge**
- **Objectif** : Distribuer les tâches pour éviter les surcharges et maintenir la disponibilité.
- **Outils Linux** :
  - **LVS (Linux Virtual Server)** : Répartit les requêtes réseau entre plusieurs serveurs.
  - **Mon** : Surveille les services et alerte en cas de problème.
  - **MOSIX** : Répartition dynamique au niveau du noyau.

### **3.2 Mécanismes de redondance**
- **Heartbeat** : Surveille les nœuds via des "battements de cœur". En cas de silence, un nœud de secours prend le relais.
- **Fake** : Permet au nœud de secours d’adopter l’adresse IP du nœud défaillant.
- **Stockage partagé** : Utilisation de **NFS** ou **bus SCSI partagé** pour un accès commun aux données.

### **3.3 Tolérance aux pannes**
- **Objectif** : Maintenir le fonctionnement malgré des défaillances graves.
- **Techniques** :
  - **Matériel spécialisé** : Fibre optique, Fibre Channel pour des connexions fiables.
  - **Systèmes de fichiers tolérants** : **CodaFS**, **ReiserFS**, **NFS**.
  - **Redondance géographique** : Clusters sur sites distants pour résister aux catastrophes.

---

## **4. Composants avancés d’un cluster HA**

### **4.1 Détection de pannes**
- **Heartbeat** : Messages périodiques pour vérifier l’état des nœuds.
- **Quorum** : Évite les conflits (ex. split-brain) en exigeant un consensus majoritaire (nombre impair de nœuds recommandé).
- **Fencing (STONITH)** : Isole un nœud défaillant pour protéger les ressources partagées.

### **4.2 Gestion des données**
- **Shared-Disk** : Stockage commun accessible par tous les nœuds (ex. SAN, NAS).
- **Shared-Nothing** : Chaque nœud a son propre stockage, avec réplication (ex. DRBD).

### **4.3 Réseau**
- **Bonding/Teaming** : Agrégation d’interfaces réseau pour redondance et performance.
- **Multipathing** : Multiples chemins d’accès au stockage pour éviter les interruptions.

---

## **5. Outils et technologies Linux pour la HA**

### **5.1 Clustering HA**
- **Pacemaker** : Orchestre le basculement des services dans un cluster.
- **Corosync** : Assure la communication entre nœuds.
- **DRBD (Distributed Replicated Block Device)** : Réplique les données en temps réel.

### **5.2 Répartition de charge**
- **HAProxy** : Répartiteur performant pour applications web.
- **Nginx** : Serveur web avec capacités de load balancing.

### **5.3 Surveillance**
- **Nagios** : Surveille les hôtes et services avec alertes.
- **Zabbix** : Solution avancée pour la HA.

### **5.4 Protocoles réseau**
- **VRRP (Virtual Router Redundancy Protocol)** : Redondance de routage avec IP virtuelle.
- **LACP (Link Aggregation Control Protocol)** : Agrégation de liens pour performance et redondance.

---

## **6. Exemples pratiques d’architectures HA**

### **6.1 Cluster HA simple**
- **Configuration** : Deux nœuds (actif/passif), **Heartbeat** pour la surveillance, **NFS** pour le stockage partagé, IP virtuelle basculante.
- **Utilisation** : Serveurs de messagerie (ex. Sendmail).

### **6.2 Cluster avec répartition de charge**
- **Configuration** : **LVS** ou **HAProxy** comme load balancer, plusieurs serveurs web (**Apache**/**Nginx**), base de données répliquée (**MySQL Cluster**).
- **Utilisation** : Sites web à fort trafic.

### **6.3 Tolérance aux pannes avancée**
- **Configuration** : Stockage distribué (**Ceph**, **GlusterFS**), connexion via **Fibre Channel**, surveillance via **Watchdog**.
- **Utilisation** : Serveurs FTP critiques.

---

## **7. Réplication des données**

### **7.1 Concepts**
- La réplication garantit la disponibilité des données en cas de panne, via une synchronisation entre nœuds.
- Types : Réplication matérielle (ex. RAID) ou au niveau du système de fichiers (ex. NFS).

### **7.2 Solutions matérielles**
- **RAID** :
  - **RAID 1** : Mirroring pour la sécurité.
  - **RAID 5** : Parité distribuée pour performance et disponibilité.
- **DRBD** : Réplication distante en temps réel.
- **ENBD** : Accès à des données distantes comme locales.

### **7.3 Systèmes de fichiers**
- **NFS** : Partage réseau simple.
- **CodaFS** : Tolérant aux pannes, distribué.
- **GFS** : Clustering et journalisation.

---

## **8. Conclusion et perspectives**

La HA sous Linux repose sur des outils open-source puissants et flexibles, permettant de concevoir des systèmes robustes à moindre coût par rapport aux solutions propriétaires. Elle est cruciale pour les entreprises modernes dépendantes de leurs systèmes d’information.

### **Perspectives**
- **Virtualisation** : **Kubernetes** et **Docker Swarm** intègrent la HA nativement.
- **Cloud hybride** : Combinaison de solutions on-premise et cloud (ex. AWS HA).
- **Automatisation** : Outils comme **Ansible** simplifient la gestion des clusters HA.

---
  

Cas de split brain

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdmAUSDMwlUhD8kvI-OSExBM3u0MBDF_4qSgB1SEk1BHG9qKrxQMVOnJaoaNRLGc81zrUX2nwRAEmK5anSySjw1QAerJCbswV6nzZmUflwhi3wf4ncMXB18ZtWEE2l7dpzGTVpE3A?key=LG7bQOdj7sDFB1fe-Mfoxg)


comment l”eviter : quorum

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcwf2Me7oTPCa2ORRWWrCjORum19Cz_fiWKbyCqMI03Acxruh-Zsdu8y3Ve4HCN5wSFlm2bMCcCAM3Ri6nee4x7pGOBm24RWfkhS83aJJ4wR0BGe25MZIFd_D2ucmEztzMGOX2z3g?key=LG7bQOdj7sDFB1fe-Mfoxg)