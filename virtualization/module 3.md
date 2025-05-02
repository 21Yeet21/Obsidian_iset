### Résumé : Module 3 - Configuration de la Mise en Réseau vSphere

Ce module couvre la configuration et la gestion des réseaux virtuels dans vSphere, en utilisant les Standard Switches et les Distributed Switches.

**Concepts Réseau Virtuel:**

- **Rôle:** Permet la communication entre VMs, entre VMs et le réseau physique, et supporte les services VMkernel (Management, vMotion, iSCSI, NFS, vSAN, FT Logging, etc.).
- **Commutateurs Virtuels (vSwitches):** Connectent les VMs et les ports VMkernel aux adaptateurs réseau physiques (uplinks) de l'hôte.

**Types de Commutateurs Virtuels:**

- **vSphere Standard Switch (vSS):** Configuration locale à un seul hôte ESXi. Géré individuellement sur chaque hôte.
- **vSphere Distributed Switch (vDS):** Configuration centralisée au niveau du Data Center, appliquée à plusieurs hôtes (jusqu'à 2000). Assure une configuration réseau cohérente à travers les hôtes. Nécessite une licence vSphere Enterprise Plus ou une licence vSAN. Offre des fonctionnalités avancées par rapport au vSS.

**Connexions sur un Commutateur Virtuel:**

- **Ports VM (VM Ports):** Connectent les cartes réseau virtuelles (vNICs) des VMs au vSwitch. Organisés en **Groupes de Ports VM (VM Port Groups)** qui définissent des configurations réseau communes (ex: VLAN, sécurité).
- **Ports VMkernel (VMkernel Ports):** Utilisés par l'hyperviseur ESXi pour ses propres services réseau (ex: Management, vMotion, IP Storage (iSCSI/NFS), vSAN). Chaque port VMkernel nécessite sa propre configuration IP (adresse, masque, passerelle). Organisés en **Groupes de Ports VMkernel**.
- **Ports Uplink (Uplink Ports):** Représentent les adaptateurs réseau physiques (NICs physiques, ou vmnics) de l'hôte connectés au vSwitch.

**VLANs (Virtual Local Area Networks):**

- Permettent de segmenter logiquement un réseau physique en plusieurs domaines de broadcast.
- Supporté via le standard **802.1Q tagging**.
- Configuré au niveau du **groupe de ports** en assignant un **ID VLAN**.
- **Virtual Switch Tagging (VST):** Mode où l'ESXi ajoute/retire les tags VLAN aux trames réseau. Le port physique du commutateur externe doit être configuré en mode **Trunk**. La VM n'a pas connaissance du VLAN.

**Configuration des Standard Switches (vSS):**

- Visualisation via vSphere Client ou Host Client. Par défaut, vSwitch0 est créé à l'installation d'ESXi avec un groupe de ports "VM Network" et "Management Network". Il est recommandé de séparer le trafic de gestion et le trafic VM.
- Ajout de nouveaux vSS ou modification des existants.
- Configuration des ports VMkernel : association à un vSS, configuration IP, activation des services requis (vMotion, Management, Provisioning, FT Logging, vSphere Replication, vSAN, etc.).
- Configuration des adaptateurs physiques (uplinks) : Vitesse/Duplex (recommandé : auto-négociation).

**Politiques Réseau (Networking Policies):**

- Permettent de configurer la sécurité, la performance et la disponibilité.
- Niveaux d'application :
    - vSS : Niveau switch (défaut), surchargeable au niveau groupe de ports.
    - vDS : Niveau groupe de ports distribués (défaut), surchargeable au niveau port individuel.
- **Politiques de Sécurité:** Protègent contre l'usurpation d'adresse MAC et le scan de ports indésirable.
    - **Mode Promiscuous (Promiscuous Mode):** Accepter/Rejeter (Défaut: Rejeter). Si Accepté, la vNIC voit tout le trafic passant sur le vSwitch. Utile pour IDS/Sniffers.
    - **Changements d'Adresse MAC (MAC Address Changes):** Accepter/Rejeter (Défaut: Rejeter). Autorise ou non la VM à changer son adresse MAC effective (celle vue par le vSwitch).
    - **Transmissions Usurpées (Forged Transmits):** Accepter/Rejeter (Défaut: Rejeter). Autorise ou non la VM à envoyer des trames avec une adresse MAC source différente de celle de sa vNIC.
- **Politiques de Mise en Forme du Trafic (Traffic Shaping):** Limite la bande passante consommée par une VM ou un groupe de VMs.
    - Paramètres : Débit Moyen (Average Rate), Débit de Pointe (Peak Rate), Taille de Rafale (Burst Size).
    - vSS : Contrôle uniquement le trafic sortant (VM -> vSwitch -> Réseau physique).
    - vDS : Contrôle le trafic sortant (egress) et entrant (ingress).
- **Politiques d'Agrégation de Liens et de Basculement (NIC Teaming and Failover):** Utilise plusieurs uplinks pour augmenter la bande passante et/ou fournir de la redondance.
    - **Équilibrage de Charge (Load Balancing):** Définit comment le trafic sortant est réparti entre les uplinks actifs. Différents algorithmes :
        - _Route based on Originating Virtual Port ID (Basé sur ID Port Virtuel Origine):_ Défaut sur vSS. Simple, faible charge. Le trafic d'une vNIC utilise toujours le même uplink. Limite la bande passante par vNIC à celle d'un seul uplink.
        - _Route based on Source MAC Hash (Basé sur Hash MAC Source):_ Trafic d'une vNIC utilise toujours le même uplink (basé sur sa MAC). Faible charge. Limite bande passante par vNIC.
        - _Route based on IP Hash (Basé sur Hash IP):_ Répartit le trafic basé sur les adresses IP source et destination. Peut utiliser la bande passante de plusieurs uplinks pour une seule vNIC. Nécessite une configuration sur le switch physique (agrégation de liens type EtherChannel/LACP/802.3ad). Charge la plus élevée.
        - _Route based on Physical NIC Load (Basé sur Charge NIC Physique):_ Disponible uniquement sur vDS. Recommandé pour vDS. Surveille la charge des uplinks (>75% sur 30s) et déplace le trafic des VMs les plus actives vers des uplinks moins chargés. Ne nécessite pas de configuration spéciale du switch physique.
    - **Détection de Panne Réseau (Network Failure Detection):**
        - _Link Status only (État du lien seulement):_ Défaut. Détecte les pannes physiques (câble débranché, port switch éteint).
        - _Beacon Probing (Sondage par balise):_ Optionnel. Envoie de petites trames pour détecter des pannes non visibles par le Link Status (ex: port bloqué par STP, mauvaise config VLAN). Nécessite une topologie réseau spécifique (au moins 3 uplinks).
    - **Notifier les Commutateurs (Notify Switches):** Oui/Non (Défaut: Oui). Informe le switch physique lors d'un basculement pour mettre à jour sa table MAC rapidement. Mettre à Non si utilisation de Microsoft NLB en mode unicast.
    - **Retour Arrière (Failback):** Oui/Non (Défaut: Oui). Si Oui, un uplink qui revient après une panne redevient actif immédiatement. Si Non, il reste en standby jusqu'à une nouvelle panne.
    - **Ordre de Basculement (Failover Order):** Permet de définir des uplinks Actifs, en Standby, ou Inutilisés.

**Configuration des Distributed Switches (vDS):**

- **Architecture :** Plan de Contrôle (Control Plane) géré par vCenter (configuration du vDS, des groupes de ports, etc.) et Plan d'E/S (I/O Plane) qui est un vSwitch caché sur chaque hôte ESXi gérant le trafic réel.
- **Avantages vs vSS :** Administration centralisée, migration de l'état réseau avec vMotion, fonctionnalités avancées (voir liste ci-dessus).
- **Protocoles de Découverte :** Utiles pour identifier les connexions aux switchs physiques.
    - **CDP (Cisco Discovery Protocol):** Supporté sur vSS et vDS connectés à des switchs Cisco.
    - **LLDP (Link Layer Discovery Protocol):** Standard ouvert, supporté uniquement sur vDS.
    - Modes : Listen (écoute seulement), Advertise (annonce seulement), Both (les deux).
- **Liaison de Port (Port Binding):** Définit comment/quand une vNIC est assignée à un port du vDS.
    - **Static Binding (Liaison Statique):** Défaut. vCenter assigne un port permanent à la vNIC dès sa connexion au groupe de ports. Recommandé. Allocation de ports : Elastic (ajoute des ports si besoin) ou Fixed (nombre fixe).
    - **Ephemeral (Éphémère - "no binding"):** L'hôte ESXi assigne un port à la vNIC lors de son démarrage/connexion. Le port est supprimé à l'extinction/déconnexion. Permet de connecter/modifier des VMs au réseau même si vCenter est indisponible. À utiliser principalement pour la récupération.
