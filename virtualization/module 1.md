
---

### Résumé : Module 1 - Vue d'ensemble de vSphere et de la Virtualisation 

Ce module introduit les concepts fondamentaux de la virtualisation et de la plateforme VMware vSphere.

**Concepts Clés de la Virtualisation:**

- **Virtualisation :** Création d'une représentation logicielle d'une unité physique (serveur, bureau, réseau, stockage). C'est un moyen efficace de réduire les coûts informatiques tout en augmentant l'efficacité et l'agilité.
- **Terminologie Essentielle :**
    - Système d'exploitation (OS) : Gère les ressources physiques pour les applications (ex: Windows, Linux).
    - Application : Logiciel s'exécutant sur un OS (ex: Microsoft Office).
    - Hyperviseur : OS spécialisé pour exécuter des machines virtuelles (VMs) (ex: ESXi).
    - Machine Virtuelle (VM) : Application spécialisée qui abstrait les ressources matérielles en logiciel.
    - Invité (Guest) : OS fonctionnant dans une VM.
    - Hôte (Host) : Ordinateur physique fournissant des ressources à l'hyperviseur ESXi.
    - vSphere : Plateforme de virtualisation VMware combinant ESXi et vCenter Server.
    - Datastore : Emplacement de stockage pour les fichiers VM.
    - Mode Maintenance : État d'un hôte ESXi ou d'un datastore avant maintenance.
    - Cluster : Groupe d'hôtes ESXi partageant leurs ressources.
    - vSphere vMotion : Migration de VMs allumées sans interruption.
    - vSphere DRS : Équilibrage de charge des VMs dans un cluster via vMotion.
    - vSphere HA : Redémarrage automatique des VMs sur d'autres hôtes en cas de panne matérielle d'un hôte.

**Infrastructure Physique vs Virtuelle:**

- **Défis Physiques :** Les serveurs physiques traditionnels entraînent une sous-utilisation des ressources, des coûts élevés (espace, énergie, refroidissement), une faible flexibilité et des processus de provisionnement longs (semaines).
- **Avantages Virtuels :** La virtualisation permet de consolider plusieurs charges de travail sur moins de serveurs physiques, réduisant les coûts et l'empreinte physique. Le provisionnement des VMs est rapide (minutes) via une interface graphique.

**Machines Virtuelles (VMs):**

- **Définition :** Représentation logicielle d'un ordinateur physique et de ses composants. Elles incluent un OS invité, les VMware Tools (pilotes pour l'interaction avec le matériel virtuel) et des ressources virtuelles (CPU, mémoire, adaptateurs réseau, disques, GPU).
- **Bénéfices :**
    - Faciles à déplacer/copier (encapsulées dans des fichiers).
    - Indépendantes du matériel physique.
    - Isolées les unes des autres sur le même matériel physique.
    - Protégées des changements matériels physiques.
    - Permettent la consolidation et l'utilisation efficace du matériel.
    - Activent des fonctionnalités avancées (provisionnement rapide, haute disponibilité, reprise après sinistre).
    - Supportent les applications et OS hérités sur du matériel récent.

**vSphere:**

- Plateforme de virtualisation comprenant deux composants administratifs principaux :
    - **ESXi :** L'hyperviseur sur lequel les VMs s'exécutent directement.
    - **vCenter Server :** La plateforme d'administration centrale pour les hôtes ESXi, VMs, stockage et réseau.
- vSphere virtualise et agrège les ressources matérielles physiques, fournissant des pools de ressources virtuelles au data center.

**Software-Defined Data Center (SDDC):**

- Concept où toute l'infrastructure (calcul, stockage, réseau, sécurité) est virtualisée et le contrôle est automatisé par logiciel.
- vSphere est la fondation du SDDC.
- Les couches typiques incluent : Physique, Infrastructure Virtuelle (hyperviseur, pools de ressources), Gestion Cloud (catalogue de services, orchestration), Gestion des Services et Automatisation, Sécurité.

**Virtualisation des Ressources par ESXi:**

- ESXi gère et alloue dynamiquement les ressources physiques (CPU, mémoire, réseau, stockage, GPU) aux VMs en tant que ressources virtuelles.
- **CPU :** Met l'accent sur la performance en exécutant les instructions directement sur les CPU physiques. Ce n'est pas de l'émulation. L'hyperviseur gère le partage du temps CPU (time-slicing) entre les VMs en cas de contention.
- **Mémoire :** Crée un espace d'adressage mémoire contigu et protégé pour chaque VM. L'allocation se fait au premier accès. Le sur-engagement de mémoire (overcommitment) est possible.
- **Réseau :** Utilise des adaptateurs Ethernet virtuels et des commutateurs virtuels (vSwitches). Les VMs communiquent entre elles via le vSwitch, même sur le même hôte. Les vSwitches se connectent au réseau externe via des adaptateurs physiques (uplinks/vmnics). Support des VLANs (802.1Q). Pas de besoin de Spanning Tree Protocol (STP) entre vSwitches sur le même hôte.
- **Stockage :** Utilise des datastores (conteneurs logiques) pour masquer les spécificités du stockage physique. Types supportés : VMFS (système de fichiers clusterisé pour stockage bloc), NFS (partage de fichiers sur NAS), vSAN (stockage software-defined utilisant les disques locaux des hôtes), vSphere Virtual Volumes (abstraction des SAN/NAS).
- **GPU :** Support des GPU physiques (NVIDIA, AMD) pour les VMs via vGPU pour les charges graphiques intensives, le calcul scientifique, l'IA/ML. vSphere Bitfusion permet de partager des GPUs entre hôtes.



---
