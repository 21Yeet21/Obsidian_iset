Voici une explication détaillée du cours sur NFS (Network File System), rédigée en français, avec un focus particulier sur l'authentification, l'utilisation des jetons (tokens), ainsi que les concepts de gestion centralisée et décentralisée. Ce contenu est basé sur le document "Cours_NFS.pdf" et suit sa structure tout en approfondissant les détails techniques.

---

## **1. Généralités sur NFS**
NFS (Network File System) est un protocole permettant d'accéder à des systèmes de fichiers distants via un réseau. Il est principalement utilisé dans les environnements Unix/Linux pour partager des fichiers entre machines. Sous Windows, on utilise généralement Samba à la place de NFS.

### **Limitations et sécurité**
- **Sécurité faible par défaut** : Les données transitent en clair sur le réseau, ce qui les rend vulnérables à l'interception par des outils comme des sniffers. L'accès est contrôlé par l'adresse IP du client, mais cela peut être contourné par une usurpation d'adresse (spoofing).
- **Confiance aveugle** : Si une machine autorisée accède à un partage NFS mal configuré, un utilisateur root sur cette machine peut accéder à tous les fichiers du partage (sauf ceux appartenant à root), car NFS se fie aux identifiants utilisateur (UID/GID) fournis par le client sans vérification.

---

## **2. Configuration du serveur NFS**

### **2.1 Configuration rapide**
- **Activation** : NFS est intégré au noyau Linux sous forme de module. Le paquet `nfs-utils` permet son activation automatique au démarrage.
- **Fichier `/etc/exports`** : Ce fichier définit les répertoires partagés et les clients autorisés. Syntaxe :
  ```
  /répertoire/à/partager machine1(option1,option2) machine2(option2)
  ```
  - Les machines peuvent être identifiées par nom DNS, adresse IP, ou plages (ex. `*.domaine.com`, `192.168.1.0/24`).
- **Options principales** :
  - `ro` : Lecture seule (par défaut).
  - `rw` : Lecture/écriture.
  - `secure` : Connexion depuis un port réservé (<1024).
  - `insecure` : Ports non réservés autorisés.
  - `sync` : Opérations disque terminées avant réponse (fiable).
  - `async` : Performances accrues, mais risque de perte de données.
  - `root_squash` : Requêtes root transformées en utilisateur `nfsnobody` (par défaut).
  - `no_root_squash` : Désactive cette protection (risqué).

**Exemple** :
```
# Exporte /tmp en lecture/écriture vers "cli"
/tmp cli(rw)
# Exporte /tmp en lecture seule pour tous
/tmp *(ro)
```

### **2.2 La commande `exportfs`**
- **Utilité** : Exporte ou désexporte des répertoires sans redémarrer NFS.
- **Options** :
  - `-r` : Rafraîchit les exports depuis `/etc/exports`.
  - `-a` : Exporte ou désexporte tout.
  - `-u` : Désexporte un répertoire spécifique.
  - `-v` : Affiche les détails.

**Exemple** :
```
exportfs -r  # Met à jour les exports
```

### **2.3 NFSv4 et `exportfs`**
- **Pseudo-système de fichiers** : NFSv4 regroupe les exports en un seul système de fichiers visible par le client, grâce à l’option `fsid=0`.
- **Exemple** :
  ```
  exportfs -o fsid=0,insecure,no_subtree_check gss/krb5p:/exports
  ```

### **2.4 Autres commandes**
- `rpcinfo -p` : Liste les services RPC.
- `nfsstat` : Statistiques d’utilisation.

---

## **3. Sécuriser NFS**
### **Pare-feu**
- Restreindre l’accès aux services RPC (`rpc.mountd`, `rpc.statd`, `nfslockd`) aux machines autorisées.
- **Ports fixes** : Configurer des ports spécifiques dans `/etc/sysconfig/nfs` pour faciliter le filtrage :
  ```
  RPCMOUNTDOPTS="-p 2048"
  STATDOPTS="-p 2046 -o 2047"
  ```

### **Authentification**
- **Par défaut (sec=sys)** : NFS utilise les UID/GID UNIX envoyés par le client, sans vérification, ce qui est peu sécurisé.
- **NFSv4 avec Kerberos** : Introduit une authentification robuste :
  - `sec=krb5` : Authentification via Kerberos V5.
  - `sec=krb5i` : Authentification + intégrité des données.
  - `sec=krb5p` : Authentification + intégrité + chiffrement.

### **Utilisation des jetons (tokens)**
- Avec Kerberos, les jetons (ou tickets) sont des preuves d’identité délivrées par un serveur Kerberos (KDC - Key Distribution Center). Ces jetons permettent :
  - **Authentification sécurisée** : Aucun mot de passe n’est envoyé sur le réseau.
  - **Validation** : Le serveur NFS vérifie le jeton pour autoriser l’accès.
  - **Sécurité accrue** : Avec `sec=krb5p`, les données sont chiffrées, protégeant contre les écoutes.

---

## **4. Client NFS**

### **4.1 Montage**
- **Commande `mount`** :
  ```
  mount -t nfs -o rw,nosuid station1.domaine.com:/org/partage /partage
  ```
- **Fichier `/etc/fstab`** :
  ```
  station1.domaine.com:/org/partage /partage nfs rw,nosuid 0 0
  ```
- **Options** :
  - `hard` : Attend indéfiniment si le serveur est indisponible.
  - `soft` : Abandonne après un délai.
  - `intr` : Permet d’interrompre les requêtes.
  - `nolock` : Désactive le verrouillage.
  - `noexec` : Empêche l’exécution de binaires.
  - `nosuid` : Désactive setuid/setgid.
  - `sec=mode` : Définit le niveau de sécurité (ex. `sec=krb5`).

### **4.2 La commande `showmount`**
- `showmount -e serveur` : Liste les partages disponibles.
- `showmount -a` : Liste les clients connectés (sur le serveur).

---

## **5. Gestion centralisée et décentralisée**
- **Centralisée** : Le serveur NFS gère les fichiers, les permissions et l’accès. Les clients y accèdent comme à un système local, mais le contrôle reste centralisé sur le serveur.
- **Décentralisée** : Certains aspects, comme l’authentification avec Kerberos, sont décentralisés. Le KDC gère les jetons indépendamment, mais les données restent centralisées sur le serveur NFS.

---

## **6. Ressources supplémentaires**
- **Manuels** : `man mount`, `man fstab`, `man nfs`, `man exports`.
- **Sites** : [nfs.sourceforge.net](http://nfs.sourceforge.net), [nfsv4.org](http://nfsv4.org).
- **Livres** : "Managing NFS and NIS" (Hal Stern), "NFS Illustrated" (Brent Callaghan).

---


# Résumé du cours NFS (Network File System)

## 1. Généralités sur NFS
NFS est un protocole pour accéder à des fichiers distants, populaire sous Unix/Linux (Samba pour Windows).  
**Limitations** : Données en clair, vulnérable au spoofing, confiance aveugle aux UID/GID.

## 2. Configuration du serveur NFS
### 2.1 Configuration rapide
- Activation via `nfs-utils`.  
- Fichier `/etc/exports` :  
  ```
  /tmp cli(rw)
  /tmp *(ro)
  ```
- Options : `ro`, `rw`, `secure`, `root_squash`, etc.

### 2.2 Commande `exportfs`
- Gère les exports dynamiquement : `exportfs -r`, `-a`, `-u`.

### 2.3 NFSv4
- Pseudo-système de fichiers avec `fsid=0`.

### 2.4 Autres commandes
- `rpcinfo`, `nfsstat`.

## 3. Sécuriser NFS
- **Pare-feu** : Ports fixes dans `/etc/sysconfig/nfs`.  
- **Authentification** :  
  - `sec=sys` : UID/GID UNIX.  
  - `sec=krb5` : Kerberos (authentification).  
  - `sec=krb5p` : Chiffrement.  
- **Jetons (tokens)** : Tickets Kerberos pour authentification sécurisée.

## 4. Client NFS
### 4.1 Montage
- `mount -t nfs` ou `/etc/fstab`.  
- Options : `hard`, `soft`, `nosuid`, `sec=krb5`.

### 4.2 `showmount`
- Liste partages (`-e`) ou clients (`-a`).

## 5. Gestion centralisée et décentralisée
- **Centralisée** : Contrôle sur le serveur NFS.  
- **Décentralisée** : Authentification via Kerberos (KDC).

## 6. Ressources
- Manuels : `man nfs`, `man exports`.  
- Sites : [nfs.sourceforge.net](http://nfs.sourceforge.net).  
- Livres : "Managing NFS and NIS".


Ce cours couvre tous les aspects essentiels de NFS, avec une attention particulière à la sécurité et à la gestion des accès.