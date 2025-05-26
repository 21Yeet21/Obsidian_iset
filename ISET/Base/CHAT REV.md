

**Propagation de privilèges (WITH GRANT OPTION)**  
3. L’utilisateur MANAGER_1 souhaite :

- accorder à EMP_2025 le droit SELECT et UPDATE sur la table VENTES,
    
- permettre à EMP_2025 de retransmettre ces privilèges à d’autres utilisateurs.
    
- rédiger la requête pour révoquer ultérieurement uniquement le droit UPDATE sans affecter le droit SELECT ou son option de retransmission.
```
GRANT SELECT,UPDATE ON VENTES TO EMP_2025 WITH GRANT OPTION
REVOQE UPDATE ON VENTES TO EMP_2025

```


**Création et audit de rôles**  
4. SCOTT veut créer un rôle R_SALES_GROUP qui regroupe :

- SELECT, INSERT, DELETE sur SALES_DATA,
    
- CREATE SESSION et UNLIMITED TABLESPACE.
    
- Écrire la ou les commandes nécessaires sachant que SCOTT ne dispose pas initialement du privilège UNLIMITED TABLESPACE.
    
- Comment SCOTT peut-il vérifier, via une vue, que le rôle contient bien tous les privilèges voulus ?
```
CREATE ROLE R_SALES_GROUP ;
GRANT SELECT,INSERT ,DELETE ON SALES_DATA TO R_SALES_DATA;
GRANT CREATE SESSION,UNLIMITED TABLESPACE TO R_SALES_DATA;
GRANT UNLIMITED TABLESPACE TO SCOTT;
SELECT * FROM DBA_SYS_PRIVS WHERE GRANTEE='R_SALES_DATA';
```


**Requêtes d’audit et diagnostic**  
5. Écrire une requête SQL pour lister tous les utilisateurs dont le profil impose un PASSWORD_LIFE_TIME inférieur à 60 jours et dont le compte est actuellement verrouillé.
```
SELECT * FROM DBA_PROFILES WHERE PASSWORD_LIFE_TIME < 60;
```


**Profils et contraintes croisées**  
6. Décrire et implémenter un profil CORP_PROFILE avec :

- FAILED_LOGIN_ATTEMPTS = 3,
    
- PASSWORD_REUSE_TIME = 30, PASSWORD_REUSE_MAX = UNLIMITED,
    
- PASSWORD_LIFE_TIME = 45, PASSWORD_GRACE_TIME = 5,
    
- IDLE_TIME = 10, CONNECT_TIME = 120.  
    Expliquez pourquoi certaines combinaisons de ces paramètres sont interdites et comment Oracle gère ces conflits.
```
CREATE PROFILE CORP_PROFILE
LIMIT
FAILED_LOGIN_ATTEMPTS = 3
PASSWORD_REUSE_TIME = 30
PASSWORD_REUSE_MAX = UNLIMITED
PASSWORD_LIFE_TIME = 45
PASSWORD_GRACE_TIME = 5
IDLE_TIME = 10
CONNECT_TIME = 120  
```

PASSWORD_REUSE_TIME = 30
PASSWORD_REUSE_MAX = UNLIMITED
PASSWORD_LIFE_TIME = 45

FAITS DES CONFLIS 


**Scénario de sécurisation récursive**  
7. Vous devez mettre en place une politique où :

- Seuls les membres du rôle R_DBA peuvent créer des utilisateurs et des profils.
    
- Les droits d’attribution de privilèges système à des rôles sont limités aux utilisateurs du rôle R_SEC.
    
- Chaque utilisateur nouvellement créé hérite automatiquement d’un rôle R_DEFAULT.  
    Décrire, étape par étape, la configuration des rôles, des privilèges et des triggers (s’il y a lieu) pour réaliser cette politique de manière automatisée.

GRANT CREATE USER , CREATE PROFILE TO R_DBA;

GRANT GRANT TO R_SEC WITH ADMIN OPTION;


- `DROP USER TEMP002;`
    SUPPRESION DE L'UTILISATEUR
- `DROP USER TEMP003 CASCADE;`
    SUPPRESION DE L'UTILISATEUR AVEC CES OBJET 
- `DROP PROFILE OLD_PROFILE CASCADE;`
    SUPPRESSION DU PROFILE ET LE SUPPRIMER FROM LES USERS QUI UTLISENT
- `DROP ROLE R_OLD;`
- SUPPRESION DU ROLE SEULEMENT