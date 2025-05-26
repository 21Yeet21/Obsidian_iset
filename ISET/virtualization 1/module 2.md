### Résumé : Module 2 - Déploiement et Configuration de vCenter 

Ce module détaille l'architecture, le déploiement et la gestion de vCenter Server, la plateforme d'administration centralisée de vSphere.

**Gestion Centralisée avec vCenter:**

- **Rôle :** Point d'administration central pour plusieurs hôtes ESXi et leurs VMs. Dirige les actions des VMs et des hôtes. Permet de regrouper et gérer les ressources de multiples hôtes. Active les fonctionnalités avancées comme DRS, HA, Fault Tolerance, vMotion, Storage vMotion.
- **Déploiement :** Déployé en tant qu'appliance virtuelle (vCenter Server Appliance - vCSA).

**vCenter Server Appliance (vCSA):**

- VM préconfigurée basée sur Linux (Photon OS), optimisée pour exécuter vCenter et ses services associés.
- Contient : Photon OS, base de données PostgreSQL intégrée, services vCenter. La taille de l'appliance et du stockage pour la base de données est choisie lors du déploiement.

**Services vCenter:**

- Inclus lors du déploiement de vCSA : vCenter Server, vSphere Client (interface web), service de Licence, Content Library (bibliothèque de contenu), vSphere Lifecycle Manager (mises à jour/patchs). Tous les services tournent sur une seule VM.

**Architecture vCenter:**

- Composants principaux :
    - **vSphere Client :** Interface utilisateur (HTML5) pour se connecter à vCenter et gérer l'environnement. C'est la méthode recommandée pour gérer les hôtes sous vCenter.
    - **Base de données vCenter (PostgreSQL) :** Stocke les informations critiques : inventaire, rôles de sécurité, données de performance, etc..
    - **Hôtes Gérés :** Les hôtes ESXi et leurs VMs gérés par vCenter.

**vCenter Single Sign-On (SSO):**

- Mécanisme d'authentification et de communication sécurisée par token entre les composants vSphere.
- **Fournisseurs d'Identité :**
    - **Intégré :** Par défaut, utilise le domaine `vsphere.local`. Peut utiliser Active Directory via LDAP ou LDAPS.
    - **Externe (Fédération) :** Supporte Active Directory Federation Services (AD FS). IWA est déprécié.
- **Flux de Connexion (Identité intégrée) :** Utilisateur se connecte au vSphere Client -> SSO authentifie via AD/LDAP -> Token SAML renvoyé au navigateur -> Token envoyé à vCenter -> Accès accordé.

**Enhanced Linked Mode (ELM):**

- Permet de lier jusqu'à 15 instances vCenter dans un même domaine SSO.
- **Avantages :** Connexion unique pour gérer tous les inventaires liés, vue et recherche unifiées des inventaires, réplication des rôles, permissions, licences, tags, politiques entre instances.
- **Configuration :** Peut être créé pendant ou après le déploiement vCSA, ou en "repointant" un vCenter vers un domaine SSO existant.
- **Licence Requise :** vCenter Standard (non supporté par Foundation ou Essentials).

**Communication ESXi et vCenter:**

- **vSphere Client <-> vCenter (vpxd) :** L'interface principale.
- **vCenter (vpxd) <-> ESXi (via vpxa) :** vCenter communique avec un agent (vpxa) installé automatiquement sur l'hôte ESXi lors de son ajout à l'inventaire.
- **ESXi (vpxa <-> hostd) :** L'agent vpxa relaie les commandes au démon principal de l'hôte (hostd). hostd gère la plupart des opérations sur l'hôte.
- **Client Direct (Host Client) <-> ESXi (hostd) :** Si vCenter n'est pas disponible, le Host Client communique directement avec hostd, mais la base de données vCenter n'est pas mise à jour.

**Scalabilité vCenter:**

- Supporte des environnements d'entreprise larges (ex: vCenter 8.0 supporte jusqu'à 2 500 hôtes, 40 000 VMs allumées). Les limites exactes sont sur VMware Configuration Maximums.

**Gestion de l'Inventaire vCenter:**

- **vSphere Client :** Outil principal pour gérer l'inventaire. Menu principal (icône 3 lignes) et volet de navigation.
- **Vues d'Inventaire :** Différentes vues pour organiser et naviguer : Hôtes et Clusters, VMs et Modèles, Stockage, Réseau.
- **Objets d'Inventaire :**
    - **Data Center :** Conteneur logique racine pour organiser tous les autres objets (hôtes, VMs, réseaux, datastores). Peut représenter un site géographique ou une unité organisationnelle.
    - **Dossiers (Folders) :** Utilisés pour regrouper et organiser les objets de même type dans chaque vue d'inventaire.
- **Population de l'Inventaire :** Créer des data centers, clusters, ajouter des hôtes, organiser en dossiers, configurer réseaux et stockage.
- **Tags Personnalisés :** Attacher des métadonnées (tags) aux objets pour faciliter le tri, la recherche et le regroupement (ex: taguer VMs de production, VMs par OS).

**Rôles et Permissions vCenter:**

- **Concepts :**
    - **Privilège :** Une action spécifique qui peut être effectuée.
    - **Rôle :** Un ensemble de privilèges. vCenter fournit des rôles système non modifiables (Administrateur, Lecture seule, Aucun accès, Administrateur sans cryptographie) et des rôles exemples clonables.
    - **Objet :** La cible de l'action (Data Center, Hôte, VM, Dossier...).
    - **Utilisateur/Groupe :** Qui peut effectuer l'action (peut venir d'une source d'identité comme AD).
    - **Permission :** L'association d'un utilisateur/groupe avec un rôle sur un objet spécifique.
- **Assignation et Propagation :** Les permissions sont assignées sur un objet et peuvent (par défaut) se propager aux objets enfants dans la hiérarchie. La propagation peut être désactivée.
- **Règles d'Application :**
    - Les permissions définies à un niveau inférieur peuvent surcharger celles définies à un niveau supérieur.
    - Si un utilisateur appartient à plusieurs groupes avec des permissions différentes sur le même objet, il obtient l'union des privilèges de ces groupes.
    - Une permission explicitement définie pour un _utilisateur_ sur un objet prime toujours sur les permissions de _groupe_ sur ce même objet.
- **Création de Rôles Personnalisés :** Créer des rôles avec le minimum de privilèges nécessaires pour une tâche spécifique (principe du moindre privilège). Utiliser des dossiers pour limiter la portée des permissions.
- **Permissions Globales :** S'appliquent à l'objet racine global et s'étendent à travers toutes les solutions (ex: plusieurs vCenter) connectées au même SSO. Permettent de donner des privilèges sur tous les objets de toutes les hiérarchies vCenter.
