### Résumé : Module 4 - Configuration du Stockage vSphere 

Ce module explore les concepts de stockage dans vSphere, les différents types de datastores et protocoles (FC, iSCSI, NFS), ainsi que leur configuration et gestion.

**Concepts de Stockage:**

- **Importance :** Le choix du stockage impacte le coût, la performance et la gestion. Le stockage partagé est essentiel pour les fonctionnalités comme vMotion, HA, DRS.
- **Datastores :** Unités de stockage logiques qui masquent la complexité du matériel physique. Utilisés pour stocker les fichiers des VMs (VMDK, VMX...), les modèles, les images ISO. Peuvent agréger l'espace de plusieurs LUNs/volumes.
- **Types de Datastores vSphere:**
    - **VMFS (Virtual Machine File System):** Système de fichiers clusterisé haute performance pour le stockage bloc.
    - **NFS (Network File System):** Protocole de partage de fichiers pour accéder au stockage NAS.
    - **vSAN:** Stockage software-defined hyperconvergé utilisant les disques locaux des hôtes ESXi.
    - **vSphere Virtual Volumes (vVols):** Modèle d'abstraction du stockage SAN/NAS basé sur des objets au niveau VM.
- **Méthodes d'Accès:**
    - **Basé Blocs (Block-based):** Accès direct aux blocs de données (Local, SAN via FC/iSCSI). Utilisé par VMFS, vSAN, vVols.
    - **Basé Fichiers (File-based):** Accès via un système de fichiers hiérarchique (NAS via NFS). Utilisé par NFS, vVols.
- **Contenu des Datastores:**
    - **Fichiers :** VMFS et NFS stockent une VM comme un ensemble de fichiers dans un répertoire dédié.
    - **Objets :** vSAN et vVols stockent une VM comme un ensemble d'objets (config, disque, swap...).
- **Technologies de Stockage Supportées:**
    - **DAS (Direct-Attached Storage):** Disques internes ou externes connectés directement à l'hôte. Simple, économique, mais limite les fonctionnalités vSphere (vMotion nécessite Storage vMotion, pas de DRS).
    - **FC (Fibre Channel):** Protocole haute vitesse pour les réseaux SAN (Storage Area Network) transportant des commandes SCSI.
    - **FCoE (Fibre Channel over Ethernet):** Encapsule le trafic FC dans des trames Ethernet.
    - **iSCSI (Internet SCSI):** Transporte les commandes SCSI sur des réseaux TCP/IP standards.
    - **NAS (Network-Attached Storage):** Stockage partagé au niveau fichier sur réseau TCP/IP, typiquement via NFS.
- **Conventions de Nommage des Périphériques:**
    - **Nom Runtime (Runtime Name):** Format `vmhbaN:C:T:L`. Non persistant après redémarrage. Ex: `vmhba1:C0:T1:L0`.
    - **Cible (Target):** Identifiant unique du nœud de stockage (ex: IQN ou EUI pour iSCSI/FC).
    - **LUN (Logical Unit Number):** Identifiant unique d'une unité logique de stockage présentée par la cible.

**VMFS (Virtual Machine File System):**

- Système de fichiers clusterisé permettant l'accès concurrent par plusieurs hôtes ESXi.
- Optimisé pour les grands fichiers (VMDK) mais efficace pour les petits fichiers grâce à l'adressage par sous-blocs.
- Supporte l'extension dynamique de la taille du datastore (ajout d'extent ou agrandissement d'extent existant).
- Verrouillage distribué au niveau bloc pour protéger les VMs.
- Versions : VMFS5 et VMFS6 (VMFS6 apporte support des disques 4Kn et récupération automatique d'espace - UNMAP).
- Taille max volume 64TB, fichier max 62TB.
- Création sur dispositifs bloc (FC, iSCSI, DAS SCSI/NVMe).
- Gestion : Création, augmentation de taille (ajouter extent/LUN ou agrandir extent/LUN), Mode Maintenance (vider le datastore avant maintenance), Suppression/Démontage (Démontage le rend inaccessible, Suppression détruit les données).

**NFS (Network File System):**

- Protocole de partage de fichiers utilisé pour accéder aux NAS.
- Versions supportées par ESXi : NFS v3 et NFS v4.1 sur TCP/IP.
- **Différences clés:**
    - **Multipathing :** NFS v3 utilise le NIC Teaming ESXi. NFS v4.1 supporte le multipathing natif via session trunking (si le serveur NFS le supporte).
    - **Authentification :** NFS v3 utilise AUTH_SYS (basé sur UID/GID, souvent root). NFS v4.1 supporte Kerberos (krb5, krb5i) en plus d'AUTH_SYS.
    - **Verrouillage (Locking) :** NFS v3 utilise un verrouillage propriétaire VMware côté client (fichiers .lck). NFS v4.1 utilise un verrouillage standardisé côté serveur.
    - **Gestion Erreurs :** NFS v4.1 a une meilleure gestion/récupération d'erreurs.
- **Incompatibilité :** Ne pas monter le même partage NFS avec des versions différentes (v3 et v4.1) depuis différents hôtes.
- **Compatibilité Fonctionnalités vSphere :** NFS v4.1 a des limitations avec Storage DRS, SIOC et certains modes de Site Recovery Manager.
- **Configuration :** Nécessite un port VMkernel dédié (recommandé isolé). Création du datastore en spécifiant la version (3 ou 4.1), nom du serveur NFS, chemin du partage, mode (lecture seule ou non), options Kerberos (pour v4.1).
- **Authentification Kerberos (NFS v4.1) :** Nécessite la jonction des hôtes ESXi à Active Directory, synchronisation temporelle (NTP), configuration des identifiants Kerberos sur l'hôte.
- **Multipathing NFS 4.1 :** Configuré en fournissant plusieurs adresses IP du serveur NFS lors du montage.
- **NFSv3 VMkernel Binding (8U1+) :** Permet de forcer le trafic d'un montage NFSv3 à passer par un port VMkernel spécifique.

**Stockage iSCSI:**

- Transporte les commandes SCSI sur IP.
- **Composants:**
    - **Initiateur iSCSI :** Côté hôte ESXi. Envoie les commandes SCSI. Peut être logiciel ou matériel.
    - **Cible iSCSI (Target) :** Côté baie de stockage. Reçoit les commandes et présente les LUNs.
- **Adressage:** Nœuds iSCSI (initiateurs ou cibles) identifiés par un **Nom iSCSI** unique. Formats : **IQN** (iSCSI Qualified Name, ex: `iqn.1998-01.com.vmware:esxhost-123abc`) ou **EUI** (Extended Unique Identifier).
- **Adaptateurs iSCSI sur ESXi:**
    - **Software iSCSI Adapter :** Intégré au VMkernel, utilise des adaptateurs réseau standards (vmnics) via un port VMkernel configuré pour le trafic iSCSI.
    - **Dependent Hardware iSCSI Adapter :** Carte HBA tierce qui décharge une partie du traitement iSCSI, mais dépend toujours du réseau vSphere (port VMkernel) pour la connectivité.
    - **Independent Hardware iSCSI Adapter :** Carte HBA tierce qui gère tout le traitement iSCSI et réseau. N'utilise pas de port VMkernel.
- **Configuration (Software & Dependent) :**
    - Créer un/des port(s) VMkernel sur un vSwitch dédié (physiquement ou via VLAN).
    - Activer l'adaptateur Software iSCSI (si utilisé).
    - Configurer la découverte des cibles : Statique (entrer manuellement IP/nom de la cible) ou Dynamique (SendTargets - entrer IP du serveur iSCSI qui renverra la liste des cibles).
    - Configurer la sécurité (optionnel) : **CHAP** (Challenge Handshake Authentication Protocol) pour authentifier l'initiateur par la cible (unidirectionnel) ou mutuellement (bidirectionnel). Peut être configuré globalement ou par cible.
- **Multipathing iSCSI :**
    - Pour Software et Dependent Hardware iSCSI : Utilise plusieurs vmnics, chacun connecté à un port VMkernel distinct. **Port Binding** est nécessaire pour lier ces multiples ports VMkernel à l'unique initiateur iSCSI software/dependent.
    - Pour Independent Hardware iSCSI : Utilise plusieurs cartes HBA iSCSI indépendantes.

**Stockage Fibre Channel (FC):**

- Protocole haute vitesse pour les SANs, transportant SCSI.
- **Composants:**
    - **HBA FC (Host Bus Adapter) :** Carte dans l'hôte ESXi pour se connecter au SAN.
    - **Commutateurs FC (Fibre Channel Switches) :** Interconnectent les hôtes et les baies de stockage, formant le "Fabric". La redondance (double fabric) est courante.
    - **Baies de Stockage FC :** Présentent des LUNs aux hôtes via des Storage Processors.
- **Adressage:** Chaque port sur un HBA ou un Storage Processor a un **WWPN** (World Wide Port Name) unique. Le switch FC assigne une adresse de port basée sur le WWPN.
- **Contrôle d'Accès:**
    - **Zoning :** Configuré sur les switchs FC pour segmenter le fabric et contrôler quels initiateurs (WWPN d'HBA) peuvent voir quelles cibles (WWPN de Storage Processor).
    - **LUN Masking :** Configuré sur la baie de stockage pour contrôler quels LUNs spécifiques sont visibles par quels initiateurs (WWPN d'HBA) qui ont déjà accès via le zoning.
- **Multipathing FC :** Avoir plusieurs chemins physiques entre un HBA et un LUN (via différents ports HBA, switchs, ou storage processors). Assure la redondance et permet l'équilibrage de charge. Le basculement de chemin (path failover) se produit si le chemin actif tombe.
- **Types de Baies (Multipathing) :**
    - **Active-Active :** Tous les Storage Processors peuvent servir les I/O pour un LUN simultanément.
    - **Active-Passive :** Un seul Storage Processor est actif pour un LUN à un instant T; les autres sont en standby.

**Multipathing (Général - PSA):**

- **PSA (Pluggable Storage Architecture):** Architecture modulaire du VMkernel pour gérer le multipathing. Utilise des plugins :
    - **NMP (Native Multipathing Plugin):** Fourni par VMware, gère les chemins et utilise des **PSP (Path Selection Policies)** pour choisir le chemin actif et équilibrer la charge.
    - **MPP (Third-party Multipathing Plugins):** Fournis par les vendeurs de stockage pour des fonctionnalités spécifiques à leurs baies.
- **Politiques de Sélection de Chemin (PSP) du NMP:**
    - **Fixed (Fixe) :** Utilise un chemin "préféré". Bascule si le préféré tombe, revient au préféré dès qu'il est disponible. Défaut pour baies Active-Active.
    - **MRU (Most Recently Used - Le plus récemment utilisé) :** Utilise le premier chemin fonctionnel trouvé au démarrage. Bascule si ce chemin tombe, mais ne revient pas automatiquement à l'ancien chemin. Défaut pour baies Active-Passive.
    - **Round Robin (Tourniquet) :** Fait tourner les I/O sur tous les chemins actifs disponibles. Fournit l'équilibrage de charge. Peut prendre en compte la latence et la bande passante pour choisir le meilleur chemin dynamiquement. À vérifier compatibilité avec la baie.

**Raw Device Mapping (RDM):**

- Permet à une VM d'accéder directement à un LUN SAN (FC ou iSCSI) au lieu d'utiliser un fichier VMDK sur un datastore VMFS.
- Un fichier pointeur (ex: `nom_vm-rdm.vmdk`) est stocké sur un datastore VMFS, mais les données réelles sont sur le LUN.
- Utile pour : Applications nécessitant un accès bas niveau au matériel (SAN-aware apps), utilisation de snapshots au niveau baie, migration P2V de serveurs avec de grandes données sur SAN.
- Modes :
    - **Virtual Compatibility Mode (Mode Compatibilité Virtuelle):** Le RDM apparaît à la VM comme un disque virtuel normal. Permet les fonctionnalités VM comme les snapshots VMware, le clonage. Pointeur : `-rdm.vmdk`.
    - **Physical Compatibility Mode (Mode Compatibilité Physique):** Permet à la VM d'envoyer la plupart des commandes SCSI directement au LUN. Nécessaire pour les applications SAN-aware. Ne permet pas les snapshots VMware. Pointeur : `-rdmp.vmdk`.

---

