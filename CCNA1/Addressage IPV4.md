  
  

REMARQUE : 

dans une entreprise qui a des serveurs ! on est dans le besoin de donner ces serveurs des adresses public pour que ces serveurs soit accessible par internet ( le public )

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfdPWmuqghN_KcyQj__J91W5D6sI26RdNDEeohsQKirsUZGUk0EHhStCBRFlA669l0s6oWbZlFpFAdGioKQc75dVf_gVfZfMQle1IUksKgqDyBIDdQPAZHgUB2uooZsiE1ak57uDQ?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  

11.1.3 Longueur de préfixe 

  
  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXecjYFYrfOPs4SxG2CctDhhhvvsXId1JrsGg0hg1IOtauV48e0vzNs9nO6ZOCwxpoRW2JufT-7lY4E0F7Qh2vJBEGJzGaCfa854KfqGLhm1KByAai793r4PcxIpXyOZ4qANra_sDQ?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  

Note: Une adresse réseau est également appelée préfixe ou préfixe réseau. La longueur du préfixe est le nombre de bits mis à 1 dans le masque de sous-réseau.

  
  
  

11.1.4 Déterminer le réseau - AND (ET)logique

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdq7ZzI2zrZ0kE5ogQ8ZPKQ2IOffJnvmRCSU_oZrCKZnBItvNiqmhHxCPHMcq4WqhF7-r-O4Siu3l4zl7uNxxJhJddK4O2uWVOLkDQB8E0hu6KT5D53UaE-N58Xw8IfxBQ7W8y7kA?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  
  
  

11.2.1 Monodiffusion

  
  

Monodiffusion: Communication un-à-un entre deux périphériques.

Paquet Monodiffusion: A une adresse IP de destination unique.

Adresses IP Source: Toujours en monodiffusion.

Plage d'Adresses d'Hôte IPv4: De 0.0.0.0 à 223.255.255.255.

Adresses Réservées: Certaines adresses dans cette plage sont réservées à des usages spécifiques.

  
  
  
  
  

11.2.2 Diffusion 

  

Diffusion: Envoi d'un message à tous les appareils d'un réseau (un-à-tous).

Paquet de Diffusion: A une adresse IP de destination avec tous les bits hôtes à 1 (par exemple, 255.255.255.255).

IPv4: Utilise des paquets de diffusion. Pas de diffusion en IPv6.

Domaine de Diffusion: Tous les hôtes du même segment réseau doivent traiter les paquets de diffusion.

Types de Diffusion:

- Diffusion Dirigée: Envoyée à tous les hôtes d'un réseau spécifique (par exemple, 172.16.4.255 pour le réseau 172.16.4.0/24).
    
- Diffusion Limitée: Envoyée à 255.255.255.255.
    

Impact sur le Réseau: Les diffusions utilisent des ressources réseau; limiter pour éviter la dégradation des performances.

Optimisation: Création de sous-réseaux pour réduire le trafic de diffusion excessif.

  
  

11.2.3 Multidiffusion 

  

Clients Multidiffusion : Hôtes qui reçoivent des paquets multicast particuliers via des services demandés par un programme client.

Adresses de Multidiffusion IPv4 : Chaque groupe est représenté par une adresse de destination unique. Les hôtes abonnés traitent les paquets envoyés à cette adresse et à leur adresse de monodiffusion.

OSPF et Multidiffusion : Les protocoles de routage comme OSPF utilisent la multidiffusion pour la communication entre routeurs (adresse 224.0.0.5 pour OSPF).

Sélectivité : Seuls les périphériques activés avec OSPF traiteront les paquets envoyés à l'adresse 224.0.0.5; les autres les ignoreront.

  
  
  
  
  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdMthliDaZIQ3dVmLN08ijbpwDhSAKrP2z9QIr7sQwNZ0Uq6hu0rUT-BDmcbXZALcTk82wQ0t8-OV1BCZKdUJULV-ckj5lQiiqaFuHIoLcLYtakA3_5CNGbLVXHafEcLK7g-XiksQ?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  

Note: Les adresses privées sont définies dans RFC 1918 et parfois appelées espace d'adressage RFC 1918.

  
  

11.3.2 Routage sur Internet 

  
Adresses Privées IPv4 : Utilisées pour adresser les périphériques internes dans les réseaux d'entreprises et domestiques.

Non Routables Globalement : Les adresses IPv4 privées ne peuvent pas être routées sur Internet.

Translation d'Adresses : Les paquets envoyés en dehors des réseaux internes avec des adresses privées doivent être filtrés ou traduits en adresses publiques avant d'être transférés à un ISP.

  
  

### Adresses IPv4 privées et traduction d'adresses de réseau (NAT)

  

Traduction d'Adresses: Avant qu'un ISP puisse transférer un paquet, l'adresse IPv4 privée source doit être traduite en adresse IPv4 publique via NAT. Cette opération est effectuée par le routeur reliant le réseau interne à l'ISP.

Fonction de NAT: Convertit les adresses IPv4 privées en adresses IPv4 publiques pour permettre la communication sur Internet.

Sécurité: Bien que les adresses privées ne soient pas accessibles directement depuis Internet, elles ne sont pas considérées comme une mesure de sécurité efficace par l'IETF.

DMZ (Zone Démilitarisée): Les organisations disposant de ressources Internet, comme des serveurs Web, utilisent des adresses IPv4 publiques. Le routeur dans cette configuration effectue le routage, NAT et sert de pare-feu pour la sécurité.

  
  
  
  
  
  

11.3.4 Adresses IPv4 réservées 

  

- Adresses non Attribuables aux Hôtes : Adresses de réseau et de diffusion.
    
- Adresses Spéciales : Certaines adresses peuvent être attribuées aux hôtes avec des restrictions d'interaction.
    

#### Adresses de Bouclage

- Plage d'Adresses : 127.0.0.0 /8 ou 127.0.0.1 à 127.255.255.254
    
- Utilisation : Utilisées par un hôte pour diriger le trafic vers lui-même.
    
- Exemple Pratique : Vérification de la configuration TCP/IP via la commande ping 127.0.0.1.
    

  

### Adresses Link-Local (APIPA)

- Plage d'Adresses : 169.254.0.0/16, soit de 169.254.0.1 à 169.254.255.254.
    
- Utilisation Principale : Auto-configuration des clients DHCP Windows en l'absence d'un serveur DHCP.
    
- Usage Possible : Connexions peer-to-peer, bien que ce ne soit pas leur usage le plus courant.
    

  
  

### Attribution des Adresses IP

- Adresses IPv4 Publiques : Uniquement utilisées sur Internet et doivent être uniques.
    
- Gestion par IANA : L'Internet Assigned Numbers Authority (IANA) gère les blocs d'adresses IPv4 et IPv6.
    
- RIR : Les Registres Internet Régionaux (RIR) reçoivent les blocs d'adresses de l'IANA.
    
- Distribution :
    

- ISP : Les RIR attribuent les adresses IP aux fournisseurs de services Internet (ISP).
    
- Entreprises : Les ISP distribuent ensuite ces adresses aux entreprises et aux petits ISP.
    
- Accès Direct : Les organisations peuvent obtenir des adresses directement auprès d'un RIR, selon les politiques en vigueur.
    

  
  
  
  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdFU3DPjVyhGETHB4r-lqo-tDR9FbRtXwPVp3QrwS7oB4iqmzMsRGMjubWHEm_xhFpH-GnyfYiunaKy-HfNNi2EiRZD4kxoO0hpmDHO_dt4ZUqm-s047VItwDhcCH1tgid9QXUMWg?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  
  
  

### Domaines de Diffusion et Segmentation

- Courriels de Diffusion : Comme un courriel adressé à tous au travail, une diffusion réseau envoie des messages à tous les périphériques sur le réseau.
    
- Protocole ARP : Utilisé pour localiser d'autres périphériques sur un réseau local en envoyant des diffusions à une adresse IPv4 connue pour découvrir l'adresse MAC associée.
    
- Protocole DHCP : Utilisé pour attribuer des adresses IP aux hôtes en envoyant des diffusions pour trouver un serveur DHCP.
    
- Commutateurs : Transmettent les messages de diffusion à toutes les interfaces sauf celle d'où provient le message.
    
- Routeurs : Segmentent les domaines de diffusion et ne transfèrent pas les messages de diffusion entre interfaces.
    

### Problèmes Liés aux Grands Domaines de Diffusion

- Impact : Un grand domaine de diffusion peut entraîner un trafic de diffusion excessif, ralentissant les opérations réseau et les périphériques.
    
- Solution : Réduire la taille du domaine de diffusion en créant des sous-réseaux plus petits, ce qui limite la propagation des diffusions.
    

### Sous-Réseaux

- Création de Sous-Réseaux : Diviser un grand domaine en plus petits domaines pour réduire le trafic de diffusion. Par exemple, diviser 172.16.0.0/16 en 172.16.0.0/24 et 172.16.1.0/24.
    
- Communication Entre Réseaux : Les diffusions restent dans leur domaine, limitant leur impact.
    

### Note

- Termes Interchangeables : Les termes "sous-réseau" et "réseau" sont souvent utilisés de manière interchangeable.
    

  
  
  

Routeur : Les routeurs ne transmettent pas les paquets de diffusion IPv4 entre différents réseaux par défaut. Ils sont conçus pour isoler les segments de réseau et ne permettent pas à ces paquets de traverser les différentes interfaces du routeur.

  
  
  
  

MAGIC NUMBER TECHNNIQUE 

  

the magic number is the last borrowed bit on the right (11’1’000)/ always the network  go up by the magic number 

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfLQluFY_P0bwz9HwYPBA9witPuHv35AojqperLebnlxW5dpfiNC3IZ4996inivAME-ciW0UIOlytoxnApG5e_IeSkiKU8mGGO4NqiC5cfecBpFbFyVd738iIgjHz-wJbZkejPsOw?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd1huGfkpsBLrGoYaWpNL2tK37s5wkXAusQRfoAimIOOz9EQkWA2hYtjH0YgeAonGLpfkvNP0r-asO4BpListpk3BjSXNifYd8gvTpNDl7twJljwIJw6cajtIxi__mbcBRmp7eBeA?key=Dx4W8DZdlv64VjEZH_yxjMiA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc1iICWuNDslBdzv1R5QUyxYr2h3GtdPrKQFZ_Xs0Rr74GJrz_G-E0raKxGMN8QWZ9NZvxp59npCzsJrUodeOpRYdn9dlDIiO28WRla3UJ6s-uyrohrppWXqjo0_xH39oabSdpUpA?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf0YpTXl3JgqX_7FYdYCmTqDbbNRmm3_ZqEpNInox5v2wjN6G8_iRDGC2VN1wNCiuVcjxAT-YHAkp45qXjdXZSDxU2zQ0prXHkTdWVSNjlqE_7yK7boFCH8oO9f9NppoSja1Jq1wg?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  
  
  
  
  
  
  
  
  
  
  
  
  
  

for class A and B the magic number works only in the network octet 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfewttmh_EA-FZR_mN9oUoHQgSSIaO2hvUmYacL0FtdsZFEVh1ITLJCoCn2EgEG9jfa2WbO21zRGQagNRn05t0iAmztMZwkQPBcoxyFMwjvGQW1b-SrEWn78cymeqmOZbB1BV0K?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd_pe6XhvTedDBkM2OtunjzqtQPBumiuQEsWEdfdhh58J6_UwFQxAMWMgIMCkPWger6LeoPEUn-OKQgxCjN3f1maY5dA_BYQ2jaCQ-2PRwbqdV0Yi3-CUnq_shIGTKp1SYH6XhD7w?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeQYcSev38b8Ur8fgoW9_6ZIvR91xgln5iLZzGAURz5zpViX1MfGKmdqrAJQ8e2TbTreDtliQYpuuGBwkeX4NzvFnBGHjiqpj2x8_aYMjookzmK-ymaA4amGDinct8VmGl4_lpw?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  
  

VLSM:

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf7MjPuG3IXpygHcTToFca7oUqFbQgkrQTzOTwli1kb7vOW0ree_6w7X-xaQwQ-1z5p1NsRLeRhJuYJN3SlPB0Mk0-alu0_DXG_BiM1qVmLc6oHJDBB_YZMJop_XuDLfSxVJQuRMQ?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  
  

exemple:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfMr41Fjqzw-5LMohQ3jnHNGL7NCAmsfEMQ_XvbpsWWSEYhnzHn_u7QAfkLauBwLNGUKxEvmXnZ89NFxEPtykewd9NtBPu2ooDDe-jgGK_yBhH_w_It4wU_Xl62zmCKzwmG2eeB?key=Dx4W8DZdlv64VjEZH_yxjMiA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcq4BP29QSGEgd1skSrPYrw8Y-wAw75ZJ70tPyEF1j7Z-Eu6LKAQk8MmkEAlcDacIBG6gIhH8MF41fW2x7W2IKvhzqMv_4NlkpHpUNQ6w8aiT6tGar9yzSbKJ85fKvWhB4lfoxA?key=Dx4W8DZdlv64VjEZH_yxjMiA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdMtdykuNCoHO4pbwtAO9-JZtK8S_Pqt6dMbWl8hzZetb3c7q8f_aVhE30NJnRce-BdtNoADbvTfjgpIxsOIUo2fWd7LSk1xqsN4Ee4GH2auZHgYAmWcf2sOp71Xzs0RHtxwyBF?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  
  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeXWCrSN0RRDKEONh-9KDmdP2oQB9ZDNuvXLH03Dz-tzRB_nxEDHLnpnn7xz3crVkOyg2TT4w1dEcBEwJB1ojuib6izgG6bUr91XxlLv0Lpm7WSlQXRNmXfiiNHLoBc87pYHJ2Yqg?key=Dx4W8DZdlv64VjEZH_yxjMiA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcr7mkcD39Be3VVQRF5DlL5VmDZZnNfi1YKcoAtV_V5q8alJDTPOFjSIUYmS8qWdR77962WGBKan8RJzoKfjIDpJTkDxk_VvrGxL9viHD5dcb1FpL_WAHRmQ4B6D3od8Mrmiipe?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfAlikj3MMrn2PKjn1uTz_q7yfG69vYeoT1axCY01lSDud0ngqjTY4YLyj1SnGB7lmq6Lo5jYftutgNSgF9fIJsvDGZTFdyJu-ZmQ-P2oH0dh5ESFtDb--tznii-FJCHyzEw1In1A?key=Dx4W8DZdlv64VjEZH_yxjMiA)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeyMIrYaib-EDl9X9wZS71cOqr1uZzKtW_LsilGkTrmgsdYvU-k0_u-IOY8OFl276NZvKrT90ZbtKgPy9GC0jrtrAGEWNL7di0pZEwhCG7o8imV9iK8OBrjhjRoN_cMgli66Bfw8Q?key=Dx4W8DZdlv64VjEZH_yxjMiA)
