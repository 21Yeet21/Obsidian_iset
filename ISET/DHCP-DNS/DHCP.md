# Guide d'Étude Complet sur DHCP

## 1. Introduction au DHCP

**DHCP (Dynamic Host Configuration Protocol)** est un protocole réseau qui simplifie et automatise le processus d'attribution d'adresses IP et d'autres paramètres de configuration réseau aux appareils sur un réseau TCP/IP.

### 1.1 Objectif du DHCP

- **Simplifie l'administration** : Réduit le travail de configuration manuelle pour les administrateurs réseau
- **Centralise la gestion des IP** : Permet l'allocation d'adresses IP depuis un emplacement central
- **Élimine les erreurs de configuration** : Prévient les conflits d'adresses IP et les configurations incorrectes
- **Soutient la mobilité** : Facilite le déplacement des appareils entre les réseaux

### 1.2 Comparaison entre Configuration Manuelle et Automatique

| **Configuration Manuelle**                                                                     | **Configuration Automatique (DHCP)**                                                             |
| ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| Adresses IP saisies manuellement sur chaque client                                             | Adresses IP automatiquement fournies aux clients                                                 |
| Risque de saisir une adresse IP incorrecte ou non valide                                       | Les clients utilisent toujours des informations de configuration correctes                       |
| Une configuration incorrecte peut causer des problèmes de communication réseau                 | La configuration du client est automatiquement mise à jour lorsque la structure du réseau change |
| Charge administrative importante pour les réseaux où les ordinateurs sont fréquemment déplacés | Une source fréquente de problèmes réseau est éliminée                                            |

## 2. Fonctionnement du DHCP

### 2.1 Concept de Bail DHCP

Un **bail DHCP** est une allocation temporaire d'une adresse IP à un client pour une période spécifique. Le bail précise combien de temps le client peut utiliser la configuration IP avant qu'elle ne doive être libérée ou renouvelée.

### 2.2 Processus de Création de Bail DHCP (DORA)

Le protocole DHCP utilise un processus en quatre phases pour allouer des informations d'adressage IP aux clients DHCP :

1. **DHCPDISCOVER** (D) : Le client diffuse pour localiser les serveurs DHCP disponibles
2. **DHCPOFFER** (O) : Le serveur répond avec une offre de bail d'adresse IP
3. **DHCPREQUEST** (R) : Le client demande l'adresse IP offerte
4. **DHCPACK** (A) : Le serveur accuse réception et finalise le bail

#### Flux Détaillé du Processus :

1. **Le client diffuse un paquet DHCPDISCOVER**
    
    - Le nouveau client envoie un paquet de diffusion pour localiser les serveurs DHCP
    - Le paquet utilise l'IP de destination 255.255.255.255 (diffusion)
    - Le client n'a pas encore d'adresse IP
2. **Le serveur répond avec un paquet DHCPOFFER**
    
    - Le serveur répond avec une offre d'adresse IP
    - Le serveur réserve temporairement cette adresse
    - Peut inclure des paramètres de configuration supplémentaires
3. **Le client diffuse un paquet DHCPREQUEST**
    
    - Le client accepte la première offre reçue
    - La diffusion permet aux autres serveurs DHCP de savoir que leurs offres n'ont pas été acceptées
    - Ce paquet peut également être utilisé pour les renouvellements de bail
4. **Le serveur envoie un paquet DHCPACK**
    
    - L'"accusé de réception" confirme le bail
    - Contient un bail valide et une adresse IP
    - Inclut d'autres données de configuration IP
    - Ce n'est qu'après avoir reçu cela que le client initialise TCP/IP avec la configuration fournie

### 2.3 Processus de Renouvellement de Bail DHCP

Le processus de renouvellement suit ces étapes chronologiques :

1. **À 50% de la durée du bail** :
    
    - Le client envoie un DHCPREQUEST directement au serveur bailleur
    - Le serveur répond avec un DHCPACK pour confirmer le renouvellement
2. **Si le renouvellement échoue à 50%, à 87,5% de la durée du bail** :
    
    - Le client tente à nouveau le renouvellement
    - Communique toujours directement avec le serveur bailleur
3. **Si le renouvellement échoue à 87,5%, à 100% de la durée du bail** :
    
    - Le client doit redémarrer tout le processus de bail
    - Revient à la diffusion DHCPDISCOVER

## 3. Autorisation du Serveur DHCP

Dans un environnement Active Directory, les serveurs DHCP doivent être autorisés pour fonctionner correctement.

### 3.1 Processus d'Autorisation

1. Le serveur DHCP contacte le contrôleur de domaine pour obtenir la liste des serveurs DHCP autorisés
2. Si sa propre adresse IP est dans la liste :
    - Le service démarre
    - Le serveur traite les requêtes des clients DHCP
3. Si elle n'est pas dans la liste :
    - Le service ne démarre pas
    - Le serveur ne traite pas les requêtes des clients DHCP

### 3.2 Objectif de l'Autorisation

- Empêche les serveurs DHCP non autorisés de perturber le réseau
- Centralise le contrôle du service DHCP dans le domaine
- Évite les conflits d'adresses IP et les mauvaises configurations

## 4. Étendues DHCP

### 4.1 Définition

Une **étendue DHCP** est une plage définie d'adresses IP disponibles pour la location aux clients DHCP sur un sous-réseau spécifique. Chaque sous-réseau nécessite sa propre étendue DHCP unique avec une plage unique d'adresses IP.

### 4.2 Propriétés Clés des Étendues

- **Identifiant de réseau** : Identifie le segment de réseau
- **Masque de sous-réseau** (option 1) : Définit le sous-réseau pour la configuration IP
- **Plage d'adresses** : La plage continue d'adresses IP disponibles pour la location
- **Durée du bail** : Combien de temps les clients peuvent utiliser les adresses attribuées
- **Plage d'exclusion** : Adresses au sein de la plage qui ne seront pas louées
- **Nom de l'étendue** : Étiquette administrative pour l'étendue
- **Routeur/Passerelle** (option 3) : Adresse de la passerelle par défaut
- **Serveurs de noms de domaine** (option 6) : Serveurs DNS à utiliser
- **Nom d'hôte** (option 12) : Nom d'hôte pour le client
- **Nom de domaine** (option 15) : Nom de domaine pour le client
- **Adresse de diffusion** (option 28) : Adresse de diffusion pour le réseau

### 4.3 Configuration de Plusieurs Étendues

- Un seul serveur DHCP peut desservir plusieurs sous-réseaux
- Chaque sous-réseau doit avoir sa propre étendue
- Le serveur peut automatiquement attribuer la configuration appropriée en fonction du sous-réseau d'où provient la demande

## 5. Réservations DHCP

### 5.1 Définition

Une **réservation DHCP** est une adresse IP spécifique au sein d'une étendue qui est attribuée de façon permanente à un client particulier. Cela combine les avantages de l'adressage IP statique avec les avantages de gestion du DHCP.

### 5.2 Méthodes d'Identification

Les clients avec des réservations sont identifiés par :

- **Adresse MAC** (méthode préférée) : Adresse ethernet matérielle du client
- **Nom d'hôte** : Nom attribué au client

### 5.3 Considérations Importantes

- Les adresses réservées ne doivent pas faire partie de la plage d'adresses générale déclarée avec `range`
- Les réservations sont définies dans la section de déclaration `host` de la configuration DHCP
- Le paramètre `fixed-address` spécifie l'adresse IP à attribuer

### 5.4 Cas d'Utilisation

- Serveurs et périphériques réseau nécessitant un adressage cohérent
- Imprimantes et ressources partagées
- Systèmes nécessitant des configurations réseau spécifiques
- Postes de travail administratifs

## 6. Options DHCP

### 6.1 Définition

Les **options DHCP** sont des paramètres de configuration supplémentaires qu'un serveur DHCP fournit aux clients en plus de l'adresse IP et du masque de sous-réseau.

### 6.2 Options DHCP Courantes

- **Option routeur** (3) : Adresse de la passerelle par défaut
- **Option serveurs DNS** (6) : Adresses IP des serveurs DNS
- **Option nom de domaine** (15) : Nom de domaine DNS
- **Option serveurs WINS** : Serveurs Windows Internet Name Service
- **Option serveurs NTP** : Serveurs Network Time Protocol
- **Option durée du bail** (51) : Durée du bail d'adresse IP

### 6.3 Niveaux d'Application des Options

Les options DHCP peuvent être appliquées à différents niveaux, ce qui affecte leur distribution :

1. **Niveau serveur** : Les options s'appliquent à tous les clients du serveur
2. **Niveau étendue** : Les options s'appliquent à tous les clients d'une étendue spécifique
3. **Niveau client réservé** : Les options s'appliquent uniquement à des clients spécifiques avec des réservations
4. **Niveau classe** : Les options s'appliquent aux clients d'une classe spécifique

### 6.4 Précédence des Options

Lorsque des options sont définies à plusieurs niveaux, elles suivent cette précédence (de la plus haute à la plus basse) :

1. Options au niveau du client réservé
2. Options au niveau de l'étendue
3. Options au niveau du serveur

## 7. Agents de Relais DHCP

### 7.1 Définition

Un **agent de relais DHCP** est un ordinateur ou un routeur configuré pour écouter les messages de diffusion DHCP/BOOTP des clients et les transmettre aux serveurs DHCP sur différents sous-réseaux.

### 7.2 Objectif

- DHCP utilise des messages de diffusion, qui ne traversent pas les limites des routeurs
- Sans agents de relais, chaque sous-réseau aurait besoin de son propre serveur DHCP
- Les agents de relais permettent aux serveurs DHCP centralisés de desservir plusieurs sous-réseaux

### 7.3 Fonctionnement des Agents de Relais DHCP

1. Le client diffuse DHCPDISCOVER sur son sous-réseau local
2. L'agent de relais capte la diffusion et la transmet au serveur DHCP (unicast)
3. Le serveur renvoie DHCPOFFER à l'agent de relais (unicast)
4. L'agent de relais diffuse le DHCPOFFER sur le sous-réseau du client
5. Le client diffuse DHCPREQUEST
6. L'agent de relais transmet le DHCPREQUEST au serveur
7. Le serveur envoie DHCPACK à l'agent de relais
8. L'agent de relais diffuse DHCPACK sur le sous-réseau du client

### 7.4 Paramètres de Configuration des Agents de Relais

- **Seuil du nombre de tronçons** : Nombre maximum de routeurs que le paquet peut traverser avant d'être rejeté
- **Seuil de démarrage** : Temps en secondes pendant lequel l'agent de relais attend qu'un serveur DHCP local réponde avant de transmettre les requêtes aux serveurs distants

## 8. Implémentation du Client DHCP

### 8.1 Configuration du Client

- Les clients doivent être configurés après la configuration du serveur
- Un ordinateur ne peut pas fonctionner simultanément comme client et serveur
- Les serveurs DHCP nécessitent des adresses IP statiques

### 8.2 Client DHCP Linux (`dhclient`)

- Lit la configuration depuis `dhclient.conf`
- Suit les baux dans le fichier `dhclient.leases`
- Peut réutiliser les baux précédents si le serveur DHCP est indisponible
- Peut être préchargé avec des baux statiques pour les réseaux sans serveurs DHCP

### 8.3 Gestion des Baux par le Client

- Les nouveaux baux sont ajoutés au fichier `dhclient.leases`
- Périodiquement, le client crée un nouveau fichier de bail à partir de sa base de données interne
- Les anciens baux sont conservés à des fins de secours
- Les baux expirés sont éventuellement supprimés

## 9. Exemple de Configuration DHCP

```
ddns-update-style interim;
ddns-updates on;
deny client-updates;
one-lease-per-client false;
subnet 192.168.1.0 netmask 255.255.255.0 {
    interface eth0;
    range 192.168.1.10 192.168.1.30;
    default-lease-time 6000;
    max-lease-time 7200;
    option domain-name "domaine.local";
    option subnet-mask 255.255.255.0;
    option broadcast-address 192.168.1.255;
    option routers 192.168.1.1;
    option domain-name-servers 192.168.1.254;
    option time-offset -3600;
}
```

Cet exemple montre :

- Une déclaration de sous-réseau pour 192.168.1.0/24
- Liaison d'interface à eth0
- Plage IP de 192.168.1.10 à 192.168.1.30
- Durée de bail par défaut de 6000 secondes (100 minutes)
- Durée maximale de bail de 7200 secondes (2 heures)
- Diverses options incluant le nom de domaine, le masque de sous-réseau, l'adresse de diffusion, le routeur et le DNS

## 10. Résumé des Concepts Clés DHCP

- **DHCP** est un protocole qui automatise l'attribution d'adresses IP et la configuration réseau
- Un **bail DHCP** est une allocation temporaire d'une adresse IP pour une période spécifique
- Le **processus DORA** (Découverte, Offre, Requête, Accusé de réception) établit les baux initiaux
- Le **renouvellement de bail** se produit à 50% et 87,5% de la durée du bail
- Les **étendues DHCP** définissent la plage d'adresses IP disponibles pour un sous-réseau
- Les **réservations DHCP** attribuent en permanence des IP spécifiques à des clients particuliers
- Les **options DHCP** fournissent des paramètres de configuration réseau supplémentaires
- Les **agents de relais DHCP** permettent au DHCP de fonctionner sur plusieurs sous-réseaux
- Les **clients DHCP** doivent être correctement configurés pour obtenir automatiquement les paramètres réseau