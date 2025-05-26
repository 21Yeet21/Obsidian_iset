# Résumé du Chapitre 3 : Gérer l’Instance Oracle

Ce chapitre aborde les aspects essentiels de la gestion d'une instance Oracle, incluant les fichiers de paramètres d'initialisation, les modifications de paramètres, les procédures de démarrage et d'arrêt, ainsi que les commandes associées. Voici un résumé détaillé organisé par thèmes clés.

---

## 1. Fichiers de Pxaramètres d’Initialisation
Oracle utilise des fichiers de paramètres pour configurer l'instance lors du démarrage. Il en existe deux types :
- **PFILE (Parameter File)** : 
  - Fichier texte nommé `init<SID>.ora`.
  - Modifiable manuellement.
  - Nécessite un redémarrage de l'instance pour que les modifications prennent effet.
  - Utilisé si aucun SPFILE n'est trouvé.
- **SPFILE (Server Parameter File)** : 
  - Fichier binaire nommé `spfile<SID>.ora`.
  - Modifiable dynamiquement sans édition manuelle.
  - Les modifications persistent après redémarrage.
  - Recherché en priorité lors du démarrage.

### Paramètres Clés :
- `CONTROL_FILES` : Emplacements des fichiers de contrôle.
- `DB_FILES` : Nombre maximal de fichiers de base de données.
- `PROCESSES` : Nombre maximal de processus utilisateur.
- `DB_BLOCK_SIZE` : Taille de bloc standard pour les tablespaces.
- `SGA_TARGET` : Taille totale de la mémoire SGA.
- `MEMORY_TARGET` : Mémoire totale utilisable par Oracle.

### Commandes :
- **Créer un SPFILE à partir d'un PFILE** :
  ```sql
  CREATE SPFILE='spfile_nom.ora' FROM PFILE='pfile_nom.ora';
  ```
- **Créer un PFILE à partir d'un SPFILE** :
  ```sql
  CREATE PFILE='pfile_nom.ora' FROM SPFILE='spfile_nom.ora';
  ```

---

## 2. Modification des Paramètres d’Initialisation
Les paramètres peuvent être **statiques** (nécessitent un redémarrage) ou **dynamiques** (prennent effet immédiatement ou dans les sessions futures).

### Vues pour Inspecter les Paramètres :
- `V$PARAMETER` : Paramètres de la session courante.
- `V$SPPARAMETER` : Contenu du SPFILE.
- `V$PARAMETER2` : Paramètres actifs dans la session courante.

### Commandes :
- **Modifier un Paramètre Système** :
  ```sql
  ALTER SYSTEM SET nom_paramètre = valeur 
  [COMMENT 'texte'] 
  [SCOPE = MEMORY | SPFILE | BOTH] 
  [SID = 'SID' | '*'];
  ```
  - `SCOPE = MEMORY` : Modification temporaire (instance courante uniquement).
  - `SCOPE = SPFILE` : Modification persistante (après redémarrage).
  - `SCOPE = BOTH` : Modification temporaire et persistante.

```
ALTER SYSTEM SET PROCESSES = 150 SCOPE = SPFILE;

```

- **Modifier un Paramètre de Session** :
  ```sql
  ALTER SESSION SET nom_paramètre = valeur;
  ```

- **Afficher un Paramètre** :
  ```sql
  SHOW PARAMETER nom_paramètre;
  ```

---

## 3. Démarrage de la Base de Données
Oracle propose plusieurs modes de démarrage pour différentes tâches administratives.

### Modes de Démarrage :
1. **NOMOUNT** :
   - Seule l'instance est démarrée (allocation de la SGA, lancement des processus d'arrière-plan).
   - Utilisé pour la création d'une base ou la recréation des fichiers de contrôle.
   - Commande :
     ```sql
     STARTUP NOMOUNT;
     ```

2. **MOUNT** :
   - L'instance est démarrée et les fichiers de contrôle sont ouverts.
   - Utilisé pour les tâches de maintenance (ex. : renommer des fichiers de données, activer l'archivage).
   - Commande :
     ```sql
     STARTUP MOUNT;
     ```

3. **OPEN** :
   - L'instance est démarrée, les fichiers de contrôle et de données sont ouverts.
   - La base est accessible aux utilisateurs.
   - Commande :
     ```sql
     STARTUP OPEN;
     ```

### Options Supplémentaires :
- **RESTRICT** : Limite l'accès aux utilisateurs avec le privilège `RESTRICTED SESSION`.
  ```sql
  STARTUP RESTRICT;
  ```
- **READ ONLY** : Ouvre la base en mode lecture seule.
  ```sql
  ALTER DATABASE OPEN READ ONLY;
  ```
- **FORCE** : Force un arrêt et un redémarrage.
  ```sql
  STARTUP FORCE;
  ```
- **PFILE** : Spécifie un PFILE non par défaut pour le démarrage.
  ```sql
  STARTUP PFILE='pfile_nom.ora';
  ```

### Transition Entre Modes :
- De NOMOUNT à MOUNT :
  ```sql
  ALTER DATABASE MOUNT;
  ```
- De MOUNT à OPEN :
  ```sql
  ALTER DATABASE OPEN;
  ```

---

## 4. Arrêt de la Base de Données
Les modes d'arrêt varient selon la gestion des sessions et transactions actives.

### Modes d’Arrêt :
1. **NORMAL** :
   - Attend que tous les utilisateurs se déconnectent.
   - Aucune nouvelle connexion n'est autorisée.
   - Commande :
     ```sql
     SHUTDOWN NORMAL;
     ```

2. **TRANSACTIONAL** :
   - Attend la fin des transactions actives.
   - Aucune nouvelle transaction n'est autorisée.
   - Commande :
     ```sql
     SHUTDOWN TRANSACTIONAL;
     ```

3. **IMMEDIATE** :
   - Annule les transactions actives et déconnecte les utilisateurs.
   - Aucune attente.
   - Commande :
     ```sql
     SHUTDOWN IMMEDIATE;
     ```

4. **ABORT** :
   - Arrête l'instance sans nettoyage.
   - Nécessite une récupération au redémarrage.
   - Commande :
     ```sql
     SHUTDOWN ABORT;
     ```

### Comparaison des Modes d’Arrêt :
| Mode          | Nouvelles Connexions | Attend les Sessions | Attend les Transactions | Arrêt Propre |
|---------------|----------------------|---------------------|-------------------------|--------------|
| NORMAL        | Non                  | Oui                 | Oui                     | Oui          |
| TRANSACTIONAL | Non                  | Non                 | Oui                     | Oui          |
| IMMEDIATE     | Non                  | Non                 | Non                     | Oui          |
| ABORT         | Non                  | Non                 | Non                     | Non          |

---

## 5. Gestion des Sessions Utilisateurs
Pour terminer des sessions actives :

```sql
SELECT SID, SERIAL# FROM V$SESSION WHERE USERNAME = 'REDA';
```

```sql
ALTER SYSTEM KILL SESSION 'sid,serial#'; 
```
- `sid` et `serial#` sont obtenus depuis `V$SESSION`.
- Le processus PMON annule les transactions et libère les verrous.

---

## Points Clés à Retenir
- Oracle utilise des **PFILEs** (statiques) et des **SPFILEs** (dynamiques) pour l'initialisation.
- Les paramètres peuvent être modifiés dynamiquement ou nécessiter un redémarrage.
- Les modes de démarrage (**NOMOUNT**, **MOUNT**, **OPEN**) servent à différentes tâches administratives.
- Les modes d'arrêt varient selon leur gestion des sessions et transactions actives.
- Les commandes comme `KILL SESSION` sont utiles pour les tâches d'administration.

Ce chapitre fournit un guide complet pour gérer une instance Oracle, de la configuration aux procédures de démarrage/arrêt, assurant une administration efficace de la base de données.