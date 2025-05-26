

---

## **1. Introduction au protocole HTTP**

**HTTP** (Hypertext Transfer Protocol) est un protocole de la **couche application** du modèle OSI, conçu pour l'échange de données hypermédia sur le **World Wide Web**. Il est le fondement de la communication sur Internet pour la livraison de ressources telles que des pages HTML, images, vidéos, etc. HTTP est un protocole **orienté texte** (ASCII) et **sans état** (stateless), ce qui le rend léger mais pose des défis pour maintenir des sessions.

### **Caractéristiques principales**
- **Modèle client-serveur** : Un client (navigateur comme Chrome, Firefox) envoie une requête à un serveur web (Apache, Nginx, IIS), qui répond avec la ressource demandée.
- **Transport sur TCP** : HTTP utilise TCP (port 80 par défaut, ou 443 pour HTTPS) pour un transfert fiable, déléguant la gestion des données à ce protocole.
- **Simplicité** : Ensemble réduit de commandes, enrichi par des en-têtes pour négocier des paramètres.
- **Extensibilité** : Supporte divers types de données (texte, images, vidéos) via les types MIME.
- **Sécurité** : Compatible avec SSL/T (HTTPS) pour le chiffrement.

### **Historique et versions**
- **1989** : Inventé par **Tim Berners-Lee**.
- **1996** : **HTTP/1.0** (RFC 1945), permet de gérer plusieurs serveurs sur une même machine.
- **1997-1999** : **HTTP/1.1** (RFC 2616, puis RFC 7230-7235), ajoute le pipeline (envoi de multiples requêtes), la négociation de contenu, la gestion du cache, et l'authentification.

### **RFC pertinentes (HTTP/1.1)**
- **RFC 7230** : Syntaxe et routage des messages.
- **RFC 7231** : Sémantique, méthodes, codes d'état, en-têtes.
- **RFC 7232** : Requêtes conditionnelles.
- **RFC 7233** : Requêtes partielles.
- **RFC 7234** : Gestion du cache.
- **RFC 7235** : Authentification.

---

## **2. Transactions HTTP**

Une transaction HTTP suit un modèle client-serveur :

1. **Connexion TCP** : Le client établit une connexion TCP au serveur sur le port 80 (ou autre port spécifié, ex. 8080).
2. **Requête HTTP** : Le client envoie une requête contenant une méthode (ex. GET), une URL, et des en-têtes optionnels.
3. **Réponse HTTP** : Le serveur traite la requête, renvoie une réponse avec un code d'état, des en-têtes, et un corps (données).
4. **Fermeture** : La connexion est fermée (sauf avec l'option **Keep-Alive** pour HTTP/1.1).

### **Exemple de transaction**
Pour l’URL `http://www.info.uqam.ca/Programmation/tcpip.html` :
1. Le client se connecte à `www.info.uqam.ca` sur le port 80.
2. Requête : `GET /Programmation/tcpip.html HTTP/1.1`.
3. Le serveur répond avec le document HTML et un code `200 OK`.
4. La connexion est fermée (mode gracieux pour assurer la réception).

### **Stateless**
HTTP est **sans état** : chaque requête est indépendante, sans mémoire des requêtes précédentes. Cela simplifie le protocole mais complique la gestion des sessions (ex. commerce électronique).

---

## **3. Les URL**

Une **URL** (Uniform Resource Locator) identifie une ressource sur le Web. Sa structure est :
```
service://NomDeDomaine:[port]/chemin
```

### **Composantes**
- **Service** : Protocole (ex. `http`, `ftp`, `mailto`).
- **Nom de domaine** : Adresse du serveur (ex. `www.info.uqam.ca`).
- **Port** : Optionnel (défaut : 80 pour HTTP, 443 pour HTTPS).
- **Chemin** : Localisation de la ressource (ex. `/Programmation/tcpip.html`).
- **Paramètres** : Après `?` (ex. `?query=oiseaux`).

### **Codage des URL (URL Encoding)**
- **Espaces** : Remplacés par `+`.
- **Caractères spéciaux** : Codés en hexadécimal ASCII avec `%` (ex. `é` → `%E9`).
- **Séparateurs** : `&` pour plusieurs paramètres.
- Exemple : `Montréal/Jazz` → `Montr%E9al%2FJazz`.

### **Exemples d’URL**
- `http://www.info.uqam.ca/index.html`
- `http://www.google.ca/search?question=M%E9t%E9o+Montr%E9al`
- `mailto:obaid.abdel@uqam.ca`

---

## **4. Requêtes et réponses HTTP**

### **4.1 Requêtes HTTP**
Une requête HTTP se compose de :
- **Ligne de requête** : `[Méthode] [Ressource] [Version HTTP]` (ex. `GET /index.html HTTP/1.1`).
- **En-têtes** : Optionnels, précisent des paramètres (ex. `Host: www.example.com`).
- **Ligne vide** : Sépare les en-têtes du corps.
- **Corps** : Optionnel, contient des données (ex. pour POST).

#### **Méthodes HTTP**
- **GET** : Récupère une ressource (idempotente, sans modification).
- **HEAD** : Récupère les en-têtes sans le corps (métadonnées).
- **POST** : Envoie des données au serveur (ex. formulaires).
- **PUT** : Crée ou remplace une ressource.
- **DELETE** : Supprime une ressource.
- **OPTIONS** : Liste les méthodes supportées.
- **TRACE** : Renvoie la requête pour diagnostic.
- **CONNECT** : Établit un tunnel (ex. pour HTTPS).

#### **Exemple de requête**
```
GET /Programmes/Panorama-des-etudes HTTP/1.1
Host: www.opt2open.com
Accept: text/html
```

### **4.2 Réponses HTTP**
Une réponse HTTP se compose de :
- **Ligne d’état** : `[Version HTTP] [Code] [Message]` (ex. `HTTP/1.1 200 OK`).
- **En-têtes** : Fournissent des métadonnées (ex. `Content-Type: text/html`).
- **Ligne vide**.
- **Corps** : Données (ex. HTML, image).

#### **Codes d’état**
- **1xx (Information)** : Ex. `100 Continue`.
- **2xx (Succès)** : Ex. `200 OK`, `201 Created`.
- **3xx (Redirection)** : Ex. `301 Moved Permanently`, `304 Not Modified`.
- **4xx (Erreur client)** : Ex. `404 Not Found`, `401 Unauthorized`.
- **5xx (Erreur serveur)** : Ex. `503 Service Unavailable`.

#### **Exemple de réponse**
```
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 420

<html>...</html>
```

---

## **5. En-têtes HTTP**

Les **en-têtes** enrichissent les requêtes et réponses en fournissant des métadonnées.

### **En-têtes de requête**
- **Host** : Nom du serveur (obligatoire en HTTP/1.1, ex. `www.example.com`).
- **Accept** : Types MIME acceptés (ex. `text/html, image/jpeg`).
- **Accept-Charset** : Jeux de caractères (ex. `utf-8`).
- **Accept-Language** : Langues (ex. `fr, en`).
- **User-Agent** : Informations sur le client (ex. `Mozilla/5.0`).
- **Referer** : URL d’origine.
- **Cookie** : Envoie des cookies au serveur.
- **If-Modified-Since** : Requête conditionnelle pour le cache.
- **Authorization** : Données d’authentification.

### **En-têtes de réponse**
- **Content-Type** : Type MIME (ex. `text/html; charset=utf-8`).
- **Content-Length** : Taille du corps en octets.
- **Content-Encoding** : Codage (ex. `gzip`).
- **Set-Cookie** : Définit un cookie.
- **Location** : Redirection (ex. pour `301`).
- **Server** : Logiciel serveur (ex. `Apache/2.4`).
- **Expires** : Date d’expiration pour le cache.

### **En-têtes communs**
- **Date** : Date/heure de la requête/réponse.
- **Connection** : Options de connexion (ex. `keep-alive`).

---

## **6. Types MIME**

Les **types MIME** (Multipurpose Internet Mail Extensions) décrivent le format des données échangées. Ils suivent la syntaxe `type/sous-type`.

### **Exemples**
- **text** : `text/html`, `text/plain`.
- **image** : `image/jpeg`, `image/gif`.
- **audio** : `audio/mpeg`, `audio/x-wav`.
- **video** : `video/mpeg`, `video/quicktime`.
- **application** : `application/pdf`, `application/zip`.

### **Paramètres**
- Ex. `Content-Type: text/html; charset=utf-8` (spécifie l’encodage).
- **multipart** : Combine plusieurs types (ex. `multipart/form-data` pour formulaires).

---

## **7. Cookies et gestion de sessions**

HTTP étant **stateless**, la gestion des sessions (ex. panier d’achat) nécessite des mécanismes pour maintenir un état.

### **Cookies**
- **Définition** : Paires `nom=valeur` envoyées par le serveur via `Set-Cookie` et renvoyées par le client via `Cookie`.
- **Attributs** :
  - `expires` : Date d’expiration.
  - `path` : Chemin d’application (ex. `/music`).
  - `domain` : Domaine (ex. `.example.com`).
- **Limites** : 300 cookies max par client, 20 par domaine, 4 Ko par cookie.
- **Problèmes** : Certains navigateurs bloquent les cookies.

#### **Exemple**
Requête :
```
GET /music/buy HTTP/1.1
Cookie: VisitorID=12345; SID_music=999
```
Réponse :
```
HTTP/1.1 200 OK
Set-Cookie: SID_music=999; path=/music; expires=Thu, 20-Nov-25 14:00:00 GMT
```

### **Autres méthodes de suivi de session**
1. **Champs cachés (HIDDEN)** :
   - Identifiant inclus dans un formulaire HTML.
   - Limite : Nécessite des formulaires, ambiguïté avec les retours en arrière.
2. **URL Rewriting** :
   - Identifiant encodé dans l’URL (ex. `?sessionid=12345`).
3. **SSL Session ID** : Utilise des identifiants de session sécurisés.

### **Session Tracking**
- Le serveur stocke l’état de la session et associe un **Session ID**.
- Le client renvoie cet identifiant à chaque requête.
- Exemple : Panier d’achat où chaque action (ajout, suppression) est liée au même Session ID.

---

## **8. CGI (Common Gateway Interface)**

**CGI** permet à un serveur HTTP d’exécuter des programmes pour générer du contenu dynamique (au lieu de servir des fichiers statiques).

### **Fonctionnement**
1. Le client envoie une requête (ex. `GET /cgi-bin/script.py`).
2. Le serveur exécute le programme CGI, passant les paramètres via :
   - **Variables d’environnement** : `REQUEST_METHOD`, `QUERY_STRING`, `REMOTE_ADDR`, etc.
   - **Entrée standard** : Données POST.
3. Le programme génère une réponse (ex. HTML) via la sortie standard.
4. Le serveur renvoie la réponse au client.

### **Exemple**
Requête :
```
GET /cgi-bin/recherche?item1+item2 HTTP/1.1
Host: www.opt2open.com
```
Le serveur exécute `recherche`, qui génère une page HTML.

### **Problèmes**
- Création d’un nouveau processus par requête, coûteux en ressources.
- Solutions alternatives : **FastCGI**, **mod_perl**, **Java Servlets**, **ISAPI**.

---

## **9. Avantages et inconvénients de HTTP**

### **Avantages**
- **Négociation** : Types de données, langues, encodages.
- **Extensibilité** : En-têtes personnalisés.
- **Légèreté** : Stateless.
- **Sécurité** : Compatible avec SSL/TLS.
- **Accessibilité** : Non filtré par les pare-feu.

### **Inconvénients**
- **Stateless** : Complique la gestion des sessions.
- **Performance** : Connexions fermées par défaut (HTTP/1.0).
- **Bande passante** : En-têtes verbeux.

---

## **10. Exemple pratique (Telnet)**

Pour tester HTTP manuellement :
```
$ telnet www.perdu.com 80
GET / HTTP/1.1
Host: www.perdu.com

HTTP/1.1 200 OK
Content-Type: text/html
...
<html><title>Vous êtes perdu ?</title>...</html>
```

---


# Résumé détaillé du cours HTTP

## 1. Introduction
HTTP est un protocole de la couche application pour le Web, utilisant TCP (port 80). Simple, extensible, stateless, il supporte divers types de données via MIME.

## 2. Transactions
- Modèle client-serveur : Requête → Réponse → Fermeture (ou Keep-Alive).
- Ex. : `GET /index.html` → `200 OK` + HTML.

## 3. URL
- Structure : `service://domaine:[port]/chemin?paramètres`.
- Codage : Espaces → `+`, spéciaux → `%XX` (ex. `Montréal` → `Montr%E9al`).

## 4. Requêtes/Réponses
- **Requêtes** : Méthode (GET, POST, etc.), URL, en-têtes, corps.
- **Réponses** : Code (200, 404, etc.), en-têtes, corps.
- Méthodes : GET, HEAD, POST, PUT, DELETE, OPTIONS, TRACE, CONNECT.

## 5. En-têtes
- **Requête** : Host, Accept, User-Agent, Cookie, Referer.
- **Réponse** : Content-Type, Set-Cookie, Location.
- **Communs** : Date, Connection.

## 6. Types MIME
- Format : `type/sous-type` (ex. `text/html`, `image/jpeg`).
- Paramètres : `charset=utf-8`.

## 7. Cookies/Sessions
- **Cookies** : `nom=valeur`, stockés côté client, limites (4 Ko, 20/domain).
- Alternatives : Champs cachés, URL rewriting, SSL ID.
- **Session Tracking** : Session ID pour lier les requêtes.

## 8. CGI
- Exécute des programmes pour contenu dynamique.
- Limite : Coût process par requête.
- Alternatives : FastCGI, Servlets.

## 9. Avantages/Inconvénients
- **Avantages** : Négociation, extensibilité, sécurité (SSL).
- **Inconvénients** : Stateless, performance.

## 10. Exemple
- Telnet : `GET / HTTP/1.1` → `200 OK` + HTML.


Ce résumé couvre exhaustivement le cours HTTP, avec un focus sur les transactions, URL, requêtes/réponses, en-têtes, MIME, cookies, et CGI, tout en restant fidèle aux documents fournis.