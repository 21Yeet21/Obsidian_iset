
Réponses aux Exercices

---

Exercice 1 : Calcul d'adresses réseau

Pour chaque adresse IP et masque CIDR, on calcule :
Adresse du réseau : IP & Masque
Adresse de diffusion : Dernière adresse du réseau
Première adresse machine : Adresse réseau + 1
Dernière adresse machine : Adresse de diffusion - 1

---

192.168.169.169/24
   Masque réseau : 255.255.255.0
   Adresse réseau : 192.168.169.0
   Adresse de diffusion : 192.168.169.255
   Première adresse machine : 192.168.169.1
   Dernière adresse machine : 192.168.169.254

192.168.169.169/16
   Masque réseau : 255.255.0.0
   Adresse réseau : 192.168.0.0
   Adresse de diffusion : 192.168.255.255
   Première adresse machine : 192.168.0.1
   Dernière adresse machine : 192.168.255.254

192.168.169.169/22
   Masque réseau : 255.255.252.0
   Adresse réseau : 192.168.168.0
   Adresse de diffusion : 192.168.171.255
   Première adresse machine : 192.168.168.1
   Dernière adresse machine : 192.168.171.254

192.168.169.169/27
   Masque réseau : 255.255.255.224
   Adresse réseau : 192.168.169.160
   Adresse de diffusion : 192.168.169.191
   Première adresse machine : 192.168.169.161
   Dernière adresse machine : 192.168.169.190

---

Exercice 2 : Routage statique

1. Tables de routage pour chaque routeur :

R1 :
  | Destination | Masque | Passerelle | Interface |
  |-------------|--------|------------|-----------|
  | 10.5.3.0    | 255.255.255.0 | 10.5.2.2 | e1 |
  | 10.5.4.0    | 255.255.255.0 | 10.5.2.2 | e1 |
  | 10.5.5.0    | 255.255.255.0 | 10.5.2.2 | e1 |

R2 :
  | Destination | Masque | Passerelle | Interface |
  |-------------|--------|------------|-----------|
  | 10.5.1.0    | 255.255.255.0 | 10.5.2.1 | e0 |
  | 10.5.4.0    | 255.255.255.0 | 10.5.3.2 | e1 |
  | 10.5.5.0    | 255.255.255.0 | 10.5.3.3 | e1 |

R3 :
  | Destination | Masque | Passerelle | Interface |
  |-------------|--------|------------|-----------|
  | 10.5.1.0    | 255.255.255.0 | 10.5.3.1 | e0 |
  | 10.5.2.0    | 255.255.255.0 | 10.5.3.1 | e0 |
  | 10.5.5.0    | 255.255.255.0 | 10.5.3.3 | e0 |

R4 :
  | Destination | Masque | Passerelle | Interface |
  |-------------|--------|------------|-----------|
  | 10.5.1.0    | 255.255.255.0 | 10.5.3.1 | e0 |
  | 10.5.2.0    | 255.255.255.0 | 10.5.3.1 | e0 |
  | 10.5.4.0    | 255.255.255.0 | 10.5.3.2 | e0 |

2. Commandes IOS pour R2 :

enable
configure terminal
hostname R2
interface e0
ip address 10.5.2.2 255.255.255.0
no shutdown
exit
interface e1
ip address 10.5.3.1 255.255.255.0
no shutdown
exit
ip route 10.5.1.0 255.255.255.0 10.5.2.1
ip route 10.5.4.0 255.255.255.0 10.5.3.2
ip route 10.5.5.0 255.255.255.0 10.5.3.3
end


3. Commande pour sauvegarder la configuration :

copy running-config startup-config


---

Exercice 3 : Routage statique avec résumés

Topologie simplifiée :
HO : Connecté à LAN1 (172.16.64.0/23) et LAN2 (172.16.66.0/23).
WEST : Connecté à LAN3 (172.16.70.0/25) et via liaisons série (172.16.71.0/30, 172.16.71.4/30).

Tables de routage :

HO :
  | Source      | Réseau         | Masque          | Interface |
  |-------------|----------------|-----------------|-----------|
  | Statique    | 172.16.70.0     | 255.255.255.128 | S0/0/1    |
  | Statique    | 172.16.71.4/30  | 255.255.255.252 | S0/0/1    |
  | Directe     | 172.16.64.0     | 255.255.254.0   | Fa0/1     |
  | Directe     | 172.16.66.0     | 255.255.254.0   | Fa0/1     |

WEST :
  | Source      | Réseau         | Masque          | Interface |
  |-------------|----------------|-----------------|-----------|
  | Statique    | 172.16.64.0     | 255.255.254.0   | S0/0/0    |
  | Statique    | 172.16.66.0     | 255.255.254.0   | S0/0/0    |
  | Directe     | 172.16.70.0     | 255.255.255.128 | Fa0/0     |
  | Directe     | 172.16.71.0/30  | 255.255.255.252 | S0/0/0    |

Résumé de routage possible :
Pour HO : 172.16.64.0/22 (couvre 64.0 à 67.255).
Pour WEST : 172.16.70.0/24 (simplification).

---

Réponses aux Questions de Cours

Commandes ip route :  
   ip route <réseau> <masque> <passerelle>  
   ip route <réseau> <masque> <interface>.

Recherche récursive :  
   Quand un routeur doit résoudre une adresse de passerelle indirecte en utilisant sa propre table de routage.

RIPv1 et masques :  
   Il utilise le masque de l’interface locale recevant la mise à jour.

Métriques courantes :  
   Distance administrative, nombre de sauts (RIP), coût (OSPF), bande passante (EIGRP).

Distance administrative :  
   Critère pour choisir entre plusieurs routes vers un même réseau (plus faible = préférée).