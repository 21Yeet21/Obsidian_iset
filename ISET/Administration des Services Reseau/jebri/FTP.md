# Explication détaillée du protocole FTP

## 1. Définition et fonctionnement général du protocole FTP

Le **File Transfer Protocol (FTP)** est un protocole réseau conçu pour le transfert de fichiers entre un client et un serveur sur un réseau, principalement l'Internet. Il repose sur une architecture **client-serveur**, où le client initie une session en se connectant au serveur pour effectuer des opérations comme le téléchargement, l'envoi ou la gestion de fichiers. L'une des forces de FTP est son indépendance vis-à-vis des systèmes d'exploitation, permettant ainsi des transferts entre machines hétérogènes (par exemple, Windows vers Unix).

FTP se distingue par l'utilisation de **deux canaux de communication distincts** :

- ==**Canal de commandes (ou canal de contrôle)** :== Établi sur le port 21 par défaut, ce canal transporte les instructions envoyées par le client (comme "lister les fichiers" ou "télécharger") et les réponses du serveur. Il reste actif tout au long de la session.
- ==**Canal de données** :== Utilisé pour le transfert effectif des fichiers ou des informations demandées (comme une liste de répertoires). Ce canal est ouvert temporairement pour chaque opération de transfert et peut utiliser des ports dynamiques selon le mode choisi.

Ces canaux sont gérés par deux processus au niveau du serveur :

- ==**PI (Protocol Interpreter)**== : Responsable de l'interprétation des commandes reçues via le canal de contrôle et de la génération des réponses correspondantes.
- ==**DTP (Data Transfer Process)** :== Gère le canal de données, en s'assurant que les fichiers ou les données demandées soient transférés correctement.

Chaque session FTP commence par une connexion TCP au serveur sur le port 21, suivie d'une authentification, après quoi le client peut naviguer dans l'arborescence du serveur et exécuter diverses opérations.

## 2. Les modes de connexion : Actif et Passif

FTP propose deux modes pour établir le canal de données, chacun ayant des implications spécifiques, notamment en termes de compatibilité avec les pare-feux.

### Mode Actif

- **Mécanisme** :
    1. Le client ouvre un port aléatoire sur sa machine (généralement supérieur à 1024) et envoie une commande `PORT` au serveur via le canal de contrôle. Cette commande inclut l'adresse IP du client et le numéro du port choisi (par exemple, `PORT 192,168,1,10,4,1` signifie IP 192.168.1.10, port 1025 = 4*256 + 1).
    2. Le serveur initie alors une connexion TCP depuis son port 20 (port standard pour les données FTP) vers le port spécifié par le client.
    3. Une fois la connexion établie, le transfert de données peut commencer.
- **Problèmes** : Ce mode pose souvent des soucis avec les pare-feux ou les NAT (Network Address Translation), car le pare-feu du client doit autoriser une connexion **entrante** initiée par le serveur. Si cette connexion est bloquée, le transfert échoue.

### Mode Passif

- **Mécanisme** :
    1. Le client envoie une commande `PASV` au serveur via le canal de contrôle.
    2. Le serveur répond avec un message indiquant un port disponible sur lequel il écoute (par exemple, `227 Entering Passive Mode (192,168,1,20,4,2)` signifie IP 192.168.1.20, port 1026 = 4*256 + 2).
    3. Le client initie une connexion TCP vers ce port sur le serveur pour établir le canal de données.
- **Avantages** : Ce mode est plus compatible avec les environnements sécurisés, car toutes les connexions sont **sortantes** depuis le client, ce qui contourne les restrictions des pare-feux côté client. Cependant, le serveur doit être configuré pour accepter des connexions entrantes sur une plage de ports dynamiques, ce qui peut nécessiter des ajustements au niveau de son pare-feu.

### Comparaison et choix

Le choix entre ces modes dépend de la configuration réseau :

- **Mode actif** : Préférable dans des environnements sans pare-feu strict ou pour des connexions directes.
- **Mode passif** : Plus adapté aux réseaux modernes avec pare-feux ou NAT, car il simplifie la gestion des connexions sortantes.

## 3. Authentification et gestion des accès

L'accès à un serveur FTP nécessite généralement une authentification, bien qu'une variante publique existe.

### Authentification standard

- Le client doit fournir un **nom d'utilisateur** (via la commande `USER`) et un **mot de passe** (via `PASS`).
- Exemple de séquence :
    1. Connexion au serveur : `220 Service ready for new user`.
    2. `USER jean` → `331 User name okay, need password`.
    3. `PASS motdepasse` → `230 User logged in`.
- Une fois authentifié, l'utilisateur peut accéder aux répertoires et fichiers selon les permissions définies par l'administrateur du serveur.

### FTP anonyme

- Conçu pour un accès public, le FTP anonyme permet de se connecter sans compte personnel.
- Procédure :
    1. Le client envoie `USER anonymous`.
    2. Le serveur répond souvent `331 Please specify the password`.
    3. Le client fournit une adresse e-mail comme mot de passe (par convention, ex. `PASS guest@exemple.com`) → `230 Login successful`.
- Utilisation : Typiquement limité à des fichiers en lecture seule (téléchargements publics comme des logiciels ou des documents).

### Sécurité liée à l'authentification

Les identifiants FTP sont envoyés en texte clair sur le canal de contrôle, ce qui les rend vulnérables aux interceptions si aucune couche de chiffrement (comme SSL/TLS dans FTPS) n'est utilisée.

## 4. Formats de transfert : ASCII et Binaire

FTP propose deux formats pour transférer les fichiers, chacun adapté à un type de contenu spécifique.

### Mode ASCII

- **Description** : Utilisé pour les fichiers texte (par exemple, `.txt`, `.html`).
- **Fonctionnement** : Les caractères de fin de ligne sont ajustés pour correspondre au système d'exploitation du destinataire :
    - Sous Unix : `\n` (line feed).
    - Sous Windows : `\r\n` (carriage return + line feed).
- **Limitation** : Si ce mode est utilisé pour un fichier binaire (comme une image), les données seront corrompues en raison des conversions inadaptées.

### Mode Binaire

- **Description** : Utilisé pour les fichiers non textuels (images `.jpg`, exécutables `.exe`, etc.).
- **Fonctionnement** : Les données sont transférées octet par octet sans modification, préservant ainsi leur intégrité.
- **Avantage** : Convient à tous les types de fichiers, mais ne gère pas les conversions de fin de ligne pour les textes.

### Commandes associées

- `TYPE A` : Passe en mode ASCII.
- `TYPE I` : Passe en mode binaire (I pour "Image", synonyme de binaire dans FTP).
- Exemple : Avant de transférer un fichier texte, le client peut envoyer `TYPE A` → `200 Command okay`.

## 5. Commandes et réponses FTP

FTP utilise un ensemble standardisé de commandes et de réponses pour interagir entre le client et le serveur.

### Commandes principales

- **Navigation et gestion** :
    - `CWD chemin` : Change le répertoire courant (ex. `CWD /docs` → `250 Directory changed`).
    - `PWD` : Affiche le répertoire courant (ex. `257 "/home/user"`).
    - `LIST` : Liste les fichiers et dossiers dans le répertoire courant, envoyés via le canal de données.
- **Transfert** :
    - `RETR fichier` : Télécharge un fichier du serveur (ex. `RETR readme.txt` → `150 Opening data connection`, puis `226 Transfer complete`).
    - `STOR fichier` : Envoie un fichier au serveur.
- **Configuration** :
    - `PORT h1,h2,h3,h4,p1,p2` : Définit le port pour le mode actif.
    - `PASV` : Demande le mode passif.
- **Session** :
    - `QUIT` : Termine la session (ex. `221 Goodbye`).

### Réponses du serveur

Chaque réponse commence par un code numérique à trois chiffres suivi d’un message :

- **1xx** : Action en cours (ex. `150 File status okay; about to open data connection`).
- **2xx** : Succès (ex. `226 Transfer complete`).
- **3xx** : Action en attente (ex. `331 User name okay, need password`).
- **4xx** : Erreur temporaire (ex. `425 Can’t open data connection`).
- **5xx** : Erreur permanente (ex. `530 Login incorrect`).

### Exemple de séquence complète

1. `USER anonymous` → `331 Please specify the password`.
2. `PASS guest@exemple.com` → `230 Login successful`.
3. `CWD /pub` → `250 Directory changed`.
4. `PASV` → `227 Entering Passive Mode (192,168,1,20,4,2)`.
5. `LIST` → `150 Here comes the directory listing`, puis `226 Directory send OK`.

## 6. Sécurité et pare-feux

FTP présente des défis en matière de sécurité, notamment en raison de son architecture à deux canaux.

### Impact des pare-feux

- **Mode actif** : Le serveur doit pouvoir atteindre un port ouvert sur le client, ce qui peut être bloqué par un pare-feu mal configuré.
- **Mode passif** : Le client doit atteindre un port dynamique sur le serveur, nécessitant que ce dernier ouvre une plage de ports (ex. 49152-65535) et que son pare-feu soit ajusté.
- Solutions : Les administrateurs doivent configurer les pare-feux pour autoriser les ports nécessaires et surveiller les connexions.

### Vulnérabilités

- Les données et identifiants transitent en clair, rendant FTP sensible aux écoutes (sauf si FTPS ou SFTP est utilisé, hors scope du cours).
- Le transfert entre serveurs (FXP) peut être exploité si mal contrôlé.

## 7. Transfert entre serveurs (FXP)

FTP permet un transfert direct entre deux serveurs, appelé **FXP (File eXchange Protocol)**, sans passer par le client.

### Mécanisme

1. Le client se connecte à deux serveurs FTP (A et B).
2. Le serveur A est mis en mode passif (`PASV`), fournissant un port.
3. Le serveur B est configuré en mode actif (`PORT`) avec les coordonnées du port de A.
4. Le client ordonne à B d’envoyer un fichier à A (via `RETR` et `STOR`).

### Utilité et limites

- Utile pour les administrateurs gérant des sites distants.
- Souvent désactivé pour des raisons de sécurité, car cela peut permettre des abus (ex. surcharge de serveurs).

## Conclusion

Le protocole FTP est une solution robuste pour le transfert de fichiers, mais sa complexité réside dans la gestion des deux canaux, des modes actif/passif, des formats de transfert et des interactions avec les pare-feux. En comprenant les commandes, les réponses et les implications de sécurité, vous pouvez exploiter pleinement ses capacités tout en anticipant les problèmes potentiels.