# Résumé détaillé sur DNS (Domain Name System)

## 1. Concepts fondamentaux de DNS

### Définition et utilité

DNS (Domain Name System) est une base de données distribuée hiérarchique qui permet d'associer des noms de domaine lisibles par les humains à des adresses IP. C'est le système qui permet, par exemple, de traduire "www.google.com" en une adresse IP comme "142.250.74.228".

### Hiérarchie DNS

La structure DNS est organisée de manière hiérarchique:

- Domaine racine (représenté par un point ".")
- Domaines de premier niveau (TLD) : .com, .org, .edu, .fr, etc.
- Domaines de second niveau : google.com, microsoft.com, etc.
- Sous-domaines : mail.google.com, drive.google.com, etc.

Le FQDN (Fully Qualified Domain Name) décrit la relation exacte entre un hôte et son domaine, par exemple: server1.sales.nwtraders.com

### Enregistrements de ressources DNS

Les enregistrements DNS (Resource Records) sont des entrées dans la base de données DNS qui contiennent des informations sur un domaine:

- **SOA** (Start of Authority) : Informations d'autorité sur une zone DNS
- **A** : Association d'un nom d'hôte à une adresse IPv4
- **AAAA** : Association d'un nom d'hôte à une adresse IPv6
- **CNAME** : Alias pour un autre nom d'hôte
- **MX** : Serveur de messagerie pour le domaine
- **NS** : Serveur de noms pour le domaine
- **PTR** : Association d'une adresse IP à un nom (résolution inverse)
- **SRV** : Emplacement des services spécifiques

## 2. Fonctionnement de DNS

### Types de recherches DNS

- **Recherche directe** : Convertit un nom d'hôte en adresse IP
- **Recherche inverse** : Convertit une adresse IP en nom d'hôte (utilise le domaine spécial in-addr.arpa)

### Types de requêtes DNS

- **Requête récursive** : Le client demande au serveur DNS de fournir une réponse complète. Le serveur DNS assume l'entière responsabilité et effectue toutes les requêtes nécessaires.
- **Requête itérative** : Le serveur DNS répond avec la meilleure information dont il dispose, ou renvoie vers un autre serveur DNS qui pourrait avoir l'information.

### Processus de résolution DNS

1. Un client envoie une requête à son serveur DNS configuré
2. Si le serveur a l'information en cache, il répond directement
3. Sinon, il utilise:
    - Des redirecteurs (forwarding) si configurés
    - Des requêtes récursives vers d'autres serveurs
    - Le processus d'indications de racine (root hints)

### Mise en cache DNS

Les réponses DNS sont stockées temporairement dans un cache pour accélérer les résolutions futures:

- Chaque enregistrement a une durée de vie (TTL - Time To Live)
- La mise en cache réduit le trafic réseau et accélère les requêtes
- Un TTL trop court augmente le trafic réseau; un TTL trop long peut retarder la propagation des changements

## 3. Zones DNS

### Définition d'une zone

Une zone DNS est une portion de l'espace de noms DNS pour laquelle un serveur DNS particulier est responsable. Elle contient les enregistrements de ressources pour cette partie de l'espace de noms.

### Types de zones DNS

- **Zone principale (master/primary)** : Zone originale en lecture/écriture
- **Zone secondaire (slave/secondary)** : Copie en lecture seule d'une zone principale
- **Zone de stub** : Contient uniquement des informations sur les serveurs de noms faisant autorité pour une zone
- **Zone de transfert (forward)** : Transfère les requêtes vers d'autres serveurs

### Zones de recherche directe et inverse

- **Zone de recherche directe** : Résout les noms en adresses IP
- **Zone de recherche inverse** : Résout les adresses IP en noms (utilise le format spécial in-addr.arpa)

## 4. Configuration et gestion DNS

### Transferts de zone

Le transfert de zone est le processus de copie des enregistrements d'une zone du serveur principal vers les serveurs secondaires:

- **AXFR** : Transfert de zone complet
- **IXFR** : Transfert de zone incrémental (uniquement les modifications)
- **DNS Notify** : Mécanisme permettant au serveur principal de notifier les serveurs secondaires quand une zone est modifiée

### Protection des transferts de zone

- Restriction des transferts à des serveurs spécifiques
- Chiffrement du trafic de transfert
- Utilisation de DNSSEC pour authentifier les réponses

### Délégation de zone

La délégation permet de diviser la responsabilité administrative d'un domaine en sous-domaines gérés par différents serveurs DNS.

### Redirecteurs (Forwarders)

- **Redirecteur standard** : Transfère toutes les requêtes vers un autre serveur DNS
- **Redirecteur conditionnel** : Transfère seulement les requêtes pour des domaines spécifiques

## 5. Implémentations DNS

### Serveur DNS (BIND)

BIND (Berkeley Internet Name Domain) est l'implémentation de serveur DNS la plus répandue:

- Fichier de configuration principal: /etc/named.conf
- Répertoire de travail: /var/named/
- Utilise des fichiers de zone pour stocker les enregistrements

### Configuration BIND

- **Déclaration acl**: Définit des groupes d'hôtes pour le contrôle d'accès
- **Déclaration options**: Options globales de configuration
- **Déclaration zone**: Définit les caractéristiques d'une zone spécifique

### Outils de diagnostic DNS

- **nslookup**: Outil interactif d'interrogation des serveurs DNS
- **dig**: Outil avancé pour l'interrogation DNS
- **host**: Outil simplifié pour l'interrogation DNS
- **Journal des événements DNS**: Pour analyser les problèmes

## 6. Sécurité DNS

### Problèmes de sécurité DNS

- Empoisonnement de cache DNS
- Attaques par déni de service
- Usurpation d'identité DNS

### DNSSEC (DNS Security Extensions)

DNSSEC est un ensemble d'extensions qui ajoutent une couche de sécurité au DNS:

- Authentification de l'origine des données DNS
- Vérification de l'intégrité des données
- Non-répudiation des enregistrements DNS

### Bonnes pratiques de sécurité

- Limitation des requêtes récursives aux clients légitimes
- Mise à jour régulière du logiciel serveur DNS
- Séparation des services DNS internes et externes

En étudiant ces concepts, vous aurez une bonne compréhension du fonctionnement de DNS pour votre examen. Si vous avez besoin d'un résumé sur DHCP également, faites-le moi savoir!