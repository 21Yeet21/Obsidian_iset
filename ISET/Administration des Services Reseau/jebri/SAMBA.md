

---

## **1. Introduction à Samba**

**Samba** est une suite logicielle libre sous licence GNU GPL 3, implémentant le protocole **SMB/CIFS** (Server Message Block/Common Internet File System) pour permettre le partage de fichiers et d'imprimantes entre systèmes Unix/Linux et Windows. Développé initialement par Andrew Tridgell, Samba est compatible avec la plupart des systèmes Unix (Linux, Solaris, BSD, macOS) et est intégré dans presque toutes les distributions Linux.

### **Historique et rôle du protocole SMB/CIFS**
- **Origine** : Créé par IBM en 1985 sous le nom LAN Manager, adopté par Microsoft pour Windows.
- **Évolution** :
  - Renommé **CIFS** en 1998 avec des améliorations (support des raccourcis, fichiers volumineux).
  - **SMB 2** (Windows Vista/7) et **SMB 3** (Windows 8+) pour plus de performance et sécurité.
- **Fonctionnement** : Modèle client-serveur où le client envoie des requêtes et le serveur répond. Optimisé pour les réseaux locaux, mais consomme beaucoup de bande passante en raison des broadcasts (service "Explorateur d'ordinateur").

### **Rôles de Samba**
- Partage de fichiers et imprimantes.
- Authentification et autorisation des utilisateurs.
- Résolution de noms via NetBIOS/WINS.
- Intégration avec des domaines Windows (PDC, membre de domaine, Active Directory).

---

## **2. Services et composants de Samba**

Samba repose sur trois démons principaux :

1. **smbd** :
   - Gère le partage de fichiers et imprimantes via SMB/CIFS.
   - Responsable de l'authentification, du verrouillage des ressources, et du support de SMB 3.
   - Ports utilisés : TCP 139 (NetBIOS Session), TCP 445 (Microsoft-DS).

2. **nmbd** :
   - Gère les noms NetBIOS et la découverte des services réseau.
   - Supporte la résolution de noms (WINS) et l'affichage du voisinage réseau.
   - Port : UDP 137 (NetBIOS Name Service).

3. **winbindd** :
   - Permet l'intégration avec des domaines Windows (NT/Active Directory) en mappant les utilisateurs et groupes Windows aux utilisateurs Unix via RPC, PAM, et NSS.
   - Utilisé pour les relations d'approbation avec des domaines Windows.

### **Ports réseau**
| Port | Protocole | Service |
|------|-----------|---------|
| 137  | UDP       | NetBIOS Name Service |
| 138  | UDP       | NetBIOS Datagram Service |
| 139  | TCP       | NetBIOS Session Service |
| 445  | TCP/UDP   | Microsoft-DS (CIFS) |

---

## **3. Authentification dans Samba**

L'authentification est un pilier central de Samba, définissant comment les utilisateurs accèdent aux ressources partagées. Elle est configurée via le paramètre `security` dans `/etc/samba/smb.conf`.

### **Modes d'authentification**
1. **security = share** :
   - Pas d'authentification requise ; accès libre aux partages (lecture seule ou écriture selon configuration).
   - Insécurisé, utilisé pour des partages publics.
2. **security = user** :
   - Authentification basée sur un login/mot de passe local géré par Samba.
   - Utilisateurs définis dans la base SAM (TDBSAM ou LDAP).
3. **security = domain** :
   - Authentification via un contrôleur de domaine NT.
   - Les identifiants sont vérifiés par un PDC (Primary Domain Controller).
4. **security = server** :
   - Délègue l'authentification à un autre serveur Samba ou Windows.
5. **security = ads** :
   - Intégration avec Active Directory, utilisant Kerberos pour l'authentification.
   - Plus sécurisé, courant dans les environnements professionnels.

### **Utilisation des jetons (tokens)**
Dans Samba, les **jetons** (ou tickets) sont principalement utilisés avec **Kerberos** dans le mode `security = ads` (Active Directory). Voici comment ils fonctionnent :

- **Mécanisme Kerberos** :
  1. Un client demande un **TGT (Ticket Granting Ticket)** au KDC (Key Distribution Center).
  2. Le KDC authentifie le client (via mot de passe ou clé) et délivre un TGT.
  3. Le client utilise le TGT pour demander un **ticket de service** spécifique pour accéder au serveur Samba.
  4. Le serveur Samba vérifie le ticket auprès du KDC, sans échange de mot de passe sur le réseau.
- **Avantages** :
  - Sécurité renforcée : Les jetons sont temporaires et chiffrés.
  - Authentification unique (SSO) : Un seul login pour accéder à plusieurs services.
- **Exemple** :
  - Un utilisateur se connecte à un domaine Active Directory. Le ticket Kerberos permet d'accéder aux partages Samba sans réauthentification.

### **Gestion des utilisateurs**
- **Création** : Utiliser `smbpasswd` pour ajouter un utilisateur à la base SAM :
  ```
  smbpasswd -a utilisateur
  ```
- **Gestion avancée** : `pdbedit` pour gérer les profils, shells, répertoires personnels, etc.
- **Samba 4** : `samba-tool user` pour créer/supprimer des utilisateurs dans un domaine AD.

---

## **4. Configuration de Samba**

### **Fichier de configuration : `/etc/samba/smb.conf`**
Le fichier est divisé en sections :
- **[global]** : Paramètres généraux.
- **[homes]** : Partage des répertoires personnels.
- **[printers]** : Partage des imprimantes.
- **[nom_partage]** : Partages personnalisés.

**Exemple de configuration** :
```
[global]
  workgroup = SOCIETE
  netbios name = SERVEUR1
  server string = Serveur Samba
  security = user
  guest account = nobody

[public]
  path = /samba_share/public
  comment = Partage Public
  read only = no
  guest ok = yes
```

### **Sections et paramètres**
1. **[global]** :
   - `workgroup` : Nom du groupe de travail ou domaine.
   - `netbios name` : Nom réseau du serveur.
   - `security` : Mode d'authentification.
   - `bind interfaces only` : Restreint les interfaces réseau.
2. **Partages** :
   - `path` : Chemin du répertoire partagé.
   - `read only` : Lecture seule (`yes`) ou lecture/écriture (`no`).
   - `valid users` : Liste des utilisateurs autorisés.
   - `write list` : Utilisateurs avec droits d'écriture.
   - `guest ok` : Accès anonyme.

### **Vérification et rechargement**
- Vérifier la syntaxe : `testparm -s`.
- Recharger : `service samba reload` (sans interrompre les connexions).
- Redémarrer : `service samba restart`.

---

## **5. Gestion centralisée et décentralisée**

- **Centralisée** :
  - Les utilisateurs et partages sont gérés sur le serveur Samba (par exemple, avec `security = user` et TDBSAM).
  - Convient aux petits réseaux où un serveur autonome contrôle tout.
- **Décentralisée** :
  - Avec `security = ads` ou `domain`, l'authentification est gérée par un contrôleur de domaine (Active Directory ou PDC).
  - Les jetons Kerberos permettent une authentification distribuée, où le KDC gère les identifiants indépendamment du serveur Samba.

---

## **6. Accès aux ressources Samba sous Linux**

### **Client Samba**
- **Lister les partages** : `smbclient -L nom_serveur -N` (anonyme).
- **Accéder à un partage** : `smbclient //nom_serveur/ressource -U utilisateur`.

### **Montage**
1. **Manuel** :
   - Sans authentification : `mount -t cifs -o guest //SERVEUR/partage /mnt/point`.
   - Avec authentification : `mount -t cifs -o username=utilisateur //SERVEUR/partage /mnt/point`.
2. **Automatique** (via `/etc/fstab`) :
   ```
   //SERVEUR/partage /mnt/point cifs _netdev,username=utilisateur,password=motdepasse 0 0
   ```

---

## **7. Samba 3 vs Samba 4**

- **Samba 3** :
  - Supporte les domaines NT (PDC, membre).
  - Pas de contrôleur Active Directory complet.
  - Backend : TDBSAM, LDAP.
- **Samba 4** :
  - Supporte Active Directory (contrôleur de domaine, GPO).
  - Intègre LDAP, Kerberos, DNS.
  - Backend : LDAP interne ou externe, Kerberos.

---

## **8. Maintenance et dépannage**

- **Outils** :
  - `smbcontrol` : Gère les démons (rechargement, arrêt).
  - `smbstatus` : Affiche les connexions et fichiers verrouillés.
  - `tdbbackup`/`tdbrestore` : Sauvegarde/restauration des bases TDB.
- **Journaux** : Configurés dans `smb.conf` (ex. `log file = /var/log/samba/log.%m`).
- **TDB** : Bases de données légères (`/var/lib/samba/*.tdb`) pour stocker les SID, ACL, etc.

---

## **9. Gestion des permissions**

- **Linux** : Permissions rwx, ACL avec `setfacl`, attributs avec `chattr`.
- **Samba** :
  - `create mask` : Définit les permissions par défaut des fichiers créés.
  - `force create mode` : Force certains bits.
  - `security mask` : Contrôle les permissions modifiables.
  - Module **VFS acl_xattr** : Stocke les ACL Windows dans des attributs étendus.

---

## **10. Gestion des utilisateurs et groupes**

- **Utilisateurs** :
  - Windows : Identifiés par SID (ex. `S-1-5-21-...-1002`).
  - Linux : UID/GID dans `/etc/passwd`.
  - Samba : Mappage via `net groupmap` ou `winbind`.
- **Outils** :
  - `smbpasswd` : Gère les mots de passe.
  - `pdbedit` : Gère les profils.
  - `samba-tool` (Samba 4) : Gère les utilisateurs AD.

---


# Résumé détaillé du cours Samba

## 1. Introduction
Samba implémente SMB/CIFS pour le partage de fichiers/imprimantes entre Unix/Linux et Windows. Optimisé pour les réseaux locaux, il supporte les domaines NT et Active Directory.

## 2. Services
- **smbd** : Partage fichiers/imprimantes (TCP 139, 445).
- **nmbd** : Résolution NetBIOS (UDP 137).
- **winbindd** : Intégration avec domaines Windows.

## 3. Authentification
- Modes : `share` (libre), `user` (local), `domain` (PDC), `server` (autre serveur), `ads` (Active Directory).
- **Jetons** : Kerberos (`security = ads`) utilise des tickets pour une authentification sécurisée sans mot de passe réseau.
- Outils : `smbpasswd`, `pdbedit`, `samba-tool`.

## 4. Configuration
- Fichier : `/etc/samba/smb.conf`.
- Sections : `[global]`, `[homes]`, `[printers]`, `[partage]`.
- Vérification : `testparm -s`.

## 5. Gestion centralisée/décentralisée
- **Centralisée** : Serveur Samba autonome.
- **Décentralisée** : Authentification via Active Directory/Kerberos.

## 6. Accès sous Linux
- `smbclient` pour lister/accéder.
- Montage : `mount -t cifs` ou `/etc/fstab`.

## 7. Samba 3 vs 4
- Samba 3 : Domaines NT, pas AD complet.
- Samba 4 : AD, Kerberos, LDAP.

## 8. Maintenance
- `smbcontrol`, `smbstatus`, `tdbbackup`.
- Journaux : `/var/log/samba`.

## 9. Permissions
- Linux : rwx, ACL, attributs.
- Samba : `create mask`, `security mask`, `VFS acl_xattr`.

## 10. Utilisateurs/Groupes
- Mappage Linux/Windows via `net groupmap`.
- Gestion : `smbpasswd`, `pdbedit`, `samba-tool`.


Ce résumé couvre exhaustivement le cours Samba, avec un focus sur l'authentification, les jetons Kerberos, et la gestion centralisée/décentralisée, tout en restant fidèle aux documents fournis.