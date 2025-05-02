
**Synthèse : Allocation d'adresses IP via le protocole DHCP**

---

### **I. Introduction au DHCP**
- **Rôle** : Automatiser la configuration des paramètres IP (adresse IP, masque, passerelle, DNS) pour réduire l'administration manuelle et éviter les erreurs.
- **Avantages** :
  - Élimine les conflits d'adresses IP.
  - Centralise la gestion des configurations réseau.
  - Adapte automatiquement les paramètres en cas de modifications du réseau.

---

### **II. Fonctionnement du DHCP**
#### **Processus en 4 étapes (DORA)** :
1. **DHCPDISCOVER** : Diffusion par le client pour localiser un serveur.
2. **DHCPOFFER** : Réponse du serveur avec une offre d’adresse IP.
3. **DHCPREQUEST** : Demande du client pour accepter l’offre.
4. **DHCPACK** : Validation finale du serveur, envoyant la configuration IP.

#### **Renouvellement du bail** :
- **À 50% du bail** : Le client demande un renouvellement directement au serveur.
- **À 87,5%** : Si échec, le client diffuse une nouvelle demande (DHCPDISCOVER).
- **Expiration** : L’adresse est libérée si le bail n’est pas renouvelé.

---

### **III. Configuration du serveur DHCP**
#### **Autorisation dans Active Directory** :
- Un serveur DHCP doit être autorisé dans l’annuaire Active Directory pour éviter les serveurs non fiables.
- Vérification via un contrôleur de domaine avant de démarrer le service.

#### **Étendues (Scopes)** :
- **Définition** : Plage d’adresses IP attribuables à un sous-réseau.
- **Propriétés** :
  - Plage d’adresses (ex. : 192.168.1.10–192.168.1.30).
  - Durée du bail, exclusions d’adresses, options (DNS, passerelle).
  - Exemple de configuration dans `dhcpd.conf` (Linux).

#### **Réservations** :
- Attribution d’une adresse IP fixe à un client spécifique (ex. : serveur d’impression).
- Basée sur l’adresse MAC du client pour une identification unique.

#### **Options DHCP** :
- Paramètres supplémentaires envoyés avec l’adresse IP :
  - **Niveau serveur** : Options globales (ex. : DNS par défaut).
  - **Niveau étendue** : Options spécifiques à un sous-réseau.
  - **Niveau client** : Configurations personnalisées (ex. : routeur prioritaire).

---

### **IV. Agent de relais DHCP**
- **Rôle** : Transmettre les requêtes DHCP entre sous-réseaux lorsque le serveur n’est pas local.
- **Fonctionnement** :
  - Capture les diffusions DHCP et les transmet en unicast au serveur.
  - Gère les **tronçons** (nombre maximal de routeurs traversés) et le **seuil de démarrage** (délai avant retransmission).
- **Configuration** : Définir l’adresse du serveur DHCP cible et les règles de relayage.

---

### **V. Client DHCP**
- **Processus** :
  - Au démarrage, le client envoie une requête DHCPDISCOVER.
  - Utilise `dhclient` sous Linux pour gérer les baux.
  - Stocke les informations de bail dans `/var/lib/dhclient/dhclient-eth0.leases`.
- **Fichiers clés** :
  - `dhcpd.conf` : Configuration du serveur.
  - `dhclient.conf` : Paramètres du client.

---

### **VI. Bonnes pratiques**
- **Sécurité** : Autoriser uniquement les serveurs DHCP de confiance via Active Directory.
- **Optimisation** : 
  - Ajuster la durée des baux selon la taille du réseau.
  - Utiliser des réservations pour les équipements critiques.
  - Configurer des exclusions pour les adresses statiques.

---

**Conclusion** : Le DHCP simplifie la gestion réseau en automatisant l’allocation d’adresses IP et en offrant une flexibilité pour les configurations avancées (réservations, options). Son intégration avec des outils comme les agents de relais et Active Directory en fait une solution scalable pour les réseaux complexes.