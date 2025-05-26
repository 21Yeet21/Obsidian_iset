##### l'adresse locale unique

fc00::/7 à fdff::/7
1111 1011 FD
Destinées à des périphériques qui ne doivent pas être accessibles depuis l'extérieur, comme des serveurs internes ou des imprimantes.
Non routables
##### GUA IPv6 
2000::/3 JUSQUA 3FFF

2001:0DB8::/32  est réservée 

Uniques au monde et routables sur Internet

##### IPv6 LLA

fe80 (1111 1110 1000 0000)/10 à febf (1111 1110 1011 1111)
L'adresse GUA n'est pas obligatoire.
Toutefois, chaque interface réseau compatible IPv6 doit avoir une adresse LLA.

##### l'adresse MultiDiffusion

FF00::/8 JUSQUA FFFF


 ff02::1 - Groupe de multidiffusion à tous les nœuds : Tous les périphériques IPv6 sur la liaison rejoignent ce groupe, ce qui équivaut à une diffusion IPv4
 ff02::2 - Groupe de multidiffusion à tous les routeurs : Tous les routeurs IPv6 qui ont l'adresse ipv6 unicast-routing activée rejoignent ce groupe



#### **Informational Messages (NDP and MLD)**

- **Type 133: Router Solicitation (RS)**: Hosts send RS messages to request router advertisements for autoconfiguration.
- **Type 134: Router Advertisement (RA)**: Routers periodically send RA messages with network configuration info (e.g., prefixes, default gateway).
- **Type 135: Neighbor Solicitation (NS)**: Used to resolve IPv6 addresses to MAC addresses (replacing ARP) and detect duplicate addresses.
- **Type 136: Neighbor Advertisement (NA)**: Responses to NS messages, providing MAC addresses or confirming address ownership.
- **Type 137: Redirect**: Routers use this to inform hosts of a better next-hop for a destination.
- **Type 143: Multicast Listener Report**: Used by MLD to manage multicast group memberships.