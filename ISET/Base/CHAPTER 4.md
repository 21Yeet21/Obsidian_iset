# Résumé du Chapitre 4 : Sécurité des Bases de Données

Ce chapitre aborde les principes fondamentaux de la sécurité dans une base de données Oracle, incluant la gestion des utilisateurs, des privilèges, des rôles et des profils. Voici un résumé détaillé organisé par thèmes clés.

---

## A. Les Utilisateurs

### 1. Création d'un Utilisateur
Pour créer un utilisateur, plusieurs étapes sont nécessaires :
- **Choix du nom** : 30 caractères max, lettres, chiffres, et symboles `#`, `$`, `_`. Sensible à la casse si entre guillemets.
- **Authentification** :
  - Par mot de passe (stocké dans la BD) : `IDENTIFIED BY mot_de_passe`.
  - Exemple :
    ```sql
    CREATE USER ali IDENTIFIED BY 123ali;
    ```
- **Tablespaces** :
  - Définir les tablespaces accessibles (éviter `SYSTEM`).
  - Assigner des quotas (ex. `QUOTA 100M ON example`).
  - Spécifier les tablespaces par défaut :
    ```sql
    DEFAULT TABLESPACE tbs_user TEMPORARY TABLESPACE tmp_user;
    ```
- **Exemple complet** :
  ```sql
  CREATE USER aymen 
  IDENTIFIED BY 123aymen
  DEFAULT TABLESPACE example
  QUOTA 100M ON example
  TEMPORARY TABLESPACE temp
  PROFILE p_user
  PASSWORD EXPIRE
  ACCOUNT LOCK;
  ```
 
PASSWORD EXPIRE : la mot de passe expire de puis la premiere utilisation
ACOUNT LOCK : verrouiller le compte
ACOUNT UNLOCK : d'verrouiller le compte
PROFILE p_user : attribution du profile lors de la creation
DEFAULT TABLESPACE example : tablespace par default
QUOTA 100M ON example : Attribution d'un taille exacte dans un tablespace
### 2. Modification d'un Utilisateur
- Changer le mot de passe :
  ```sql
  ALTER USER aymen IDENTIFIED BY k_aymen;
  ```
- Modifier les quotas :
  ```sql
  ALTER USER aymen QUOTA 15M ON example;
  ```
- Verrouiller/Déverrouiller un compte :
  ```sql
  ALTER USER aymen ACCOUNT LOCK;
  ALTER USER aymen ACCOUNT UNLOCK;
  ```

### 3. Suppression d'un Utilisateur
- Schéma vide :
  ```sql
  DROP USER aymen;
  ```
- Schéma non vide (supprime tous les objets) :
  ```sql
  DROP USER aymen CASCADE;
  ```

### 4. Informations sur les Utilisateurs
- Vues utiles :
  - `DBA_USERS` : Détails des utilisateurs.
  - `DBA_TS_QUOTAS` : Quotas par tablespace.
  - `USER_USERS` : Informations de l'utilisateur courant.

---

## B. Les Privilèges

### 1. Types de Privilèges
- **Système** : Opérations globales (ex. `CREATE TABLE`, `CREATE SESSION`).
- **Objet** : Actions sur des objets spécifiques (ex. `SELECT`, `INSERT`,`UPDATE` ,`Delete` sur une table).

### 2. Attribution de Privilèges
- **Privilèges système** :
  ```sql
  GRANT CREATE TABLE, CREATE VIEW TO aymen;
  ```
- **Privilèges objet** :
  ```sql
  GRANT SELECT, INSERT ON SCOTT.EMP TO aymen WITH GRANT OPTION;
  ```
Attribuer le privilege select , insert to aymen sur le tableau de l'utilisateur SCOTT nommer 'EMP'
### 3. Révocation de Privilèges
- **Privilèges système** :
  ```sql
  REVOKE CREATE TABLE FROM aymen;
  ```
- **Privilèges objet** :
  ```sql
  REVOKE SELECT ON SCOTT.EMP FROM aymen;
  ```

### 4. Vues Utiles
- `DBA_TAB_PRIVS` : Privilèges sur les tables.
- `DBA_COL_PRIVS` : Privilèges sur les colonnes.

## C. Les Rôles

### 1. Création et Attribution
- **Création** :
  ```sql
  CREATE ROLE comptabilite;
  ```
- **Attribution de privilèges** :
  ```sql
  GRANT SELECT ON FACTURE TO comptabilite;
  ```
- **Assignation à un utilisateur** :
  ```sql
  GRANT comptabilite TO aymen;
  ```

### 2. Rôles Standards
- `CONNECT` : `CREATE SESSION`.
- `RESOURCE` : Création d'objets (tables, séquences, etc.).
- `DBA` : Tous les privilèges.

### 3. Suppression
```sql
DROP ROLE comptabilite;
```

### 4. Vues Utiles
- `DBA_ROLES` : Liste des rôles.
- `USER_ROLE_PRIVS` : Rôles de l'utilisateur courant.

**QUELQUES VUES UTILES**
Vue 
DBA_ROLES Affiche la liste des rôles

DBA_SYS_PRIVS Liste l’ensemble des privilèges système

USER_SYS_PRIVS Liste les privilèges système accordé à l’user
courant

DBA_ROLE_PRIVS Liste l’ensemble des rôles accordés aux users

USER_ROLE_PRIVS Liste l’ensemble des rôles accordés à l’user
courant

DBA_TAB_PRIVS Liste tous les privilèges objets assignés dans
la BD

ALL_TAB_PRIVS Liste tous les privilèges objets dont l’user est
bénéficiaire

USER_TAB_PRIVS Liste les privilèges objet assignés à l’user
courant

SESSION_ROLES Liste les rôles assignés à l’user courant

SESSION_PRIVS Liste les privilèges assignés à l’user courant

---

## D. Les Profils

### 1. Création d'un Profil
- **Limitations de mot de passe** :
  - `FAILED_LOGIN_ATTEMPTS` : Tentatives de connexion max.
  - `PASSWORD_LIFE_TIME` : Durée de validité du mot de passe.  
- **PASSWORD_REUSE_TIME**  
    Définit le **nombre de jours** pendant lesquels un **ancien mot de passe ne peut pas être réutilisé**.  
    👉 Si ce paramètre reçoit une **valeur numérique**, alors **PASSWORD_REUSE_MAX doit être mis à UNLIMITED**.
    
- **PASSWORD_REUSE_MAX**  
    Indique le **nombre maximal de réutilisations autorisées** d’un même mot de passe, qu'elles soient **consécutives ou non**.  
    👉 Si ce paramètre reçoit une valeur numérique, **PASSWORD_REUSE_TIME doit être UNLIMITED**.
    
- **PASSWORD_LOCK_TIME**  
    Définit la **durée (en jours)** pendant laquelle un **compte reste verrouillé** après dépassement du nombre d’échecs définis par **FAILED_LOGIN_ATTEMPTS**.  
    👉 Le compte est automatiquement **déverrouillé** une fois ce temps écoulé.
    
- **PASSWORD_GRACE_TIME**  
    Nombre de jours accordés à l’utilisateur pour **changer son mot de passe** après expiration de celui-ci.  
    👉 C’est un **délai de grâce** avant le blocage.
    
	- **PASSWORD_LIFE_TIME**  : temps de vie d'une mot de passe

- **Limitations de ressources** :
- ``SESSIONS_PER_USER ``: nombre de sessions MAX qui peut un utilisateur d'ouvrir au meme temps
- `CONNECT_TIIME`: durée de vie d'une session
- `IDLE_TIME` : Temps d'inactivité max.

  - `CPU_PER_SESSION` : Temps CPU max par session.
  
- **Exemple** :
  ```sql
  CREATE PROFILE app_user
  LIMIT
  FAILED_LOGIN_ATTEMPTS 5
  PASSWORD_LIFE_TIME 90
  CPU_PER_SESSION UNLIMITED
  IDLE_TIME 30;
  ```

### 2. Attribution à un Utilisateur
```sql
ALTER USER aymen PROFILE app_user;
```

### 3. Modification et Suppression
- **Modification** :
  ```sql
  ALTER PROFILE app_user LIMIT IDLE_TIME 45;
  ```
- **Suppression** :
  ```sql
  DROP PROFILE app_user CASCADE;
  ```

### 4. Vues Utiles
- `DBA_PROFILES` : Liste des profils.
- `USER_RESOURCE_LIMITS` : Limitations de l'utilisateur courant.

---

Si tu es connecté en tant que `reda` :

SELECT * FROM USER_SYS_PRIVS;

SELECT * FROM DBA_SYS_PRIVS WHERE GRANTEE = 'REDA';
