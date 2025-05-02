Configurer le nom de l'appareil:

Router(config)# hostname hostname

  

Sécuriser le mode d'exécution privilégié:

Router(config)# enable secret password

  

Sécuriser le mode d'exécution utilisateur:

Router(config)# line console 0 

 Router(config-line)# password password 

 Router(config-line)# login

  

Sécuriser Telnet à distance / accès SSH:

Router(config-line)# line vty 0 4 

 Router(config-line)# password  password 

 Router(config-line)# login 

 Router(config-line)# transport input {    ssh  | telnet}   ”SSH OR TELNET”

  

. Sécuriser tous les mots de passe dans le fichier de configuration:

 Router(config-line)# exit 

 Router(config)# service password-encryption

  

. Fournir un avertissement légal:

Router(config)# banner motd delimiter message delimiter

  

1. Enregistrer la configuration.

 Router(config)# end 

 Router# copy running-config startup-config

  
  

AUTRE EXMPLE : 

R1(config)# enable secret class

R1(config)#

R1(config)# line console 0

R1(config-line)# password cisco

R1(config-line)# Connexion

R1(config-line)# exit

R1(config)#

R1(config)# line vty 0 4

R1(config-line)# password cisco

R1(config-line)# Connexion

R1(config-line)# transport input ssh telnet  ”SSH AND TELNET”

R1(config-line)# exit

R1(config)#

R1(config)# service password-encryption

R1(config)#

  
  
  
  

10.2.1 Configurer les interfaces des routeurs

  

Router(config)# interface type-and-number 

 Router(config-if)# description description-text 

 Router(config-if)# ip address  ipv4-address subnet-mask 

 Router(config-if)# ipv6 address  ipv6-address/prefix-length 

 Router(config-if)# no shutdown

  

Remarque:lorsque deux routeurs sont directement connectés sans passer par un commutateur Ethernet (ou un autre périphérique de commutation), les interfaces réseau des deux routeurs doivent être configurées et activées pour que la communication puisse avoir lieu.

  

exemple  : 

R1(config)# interface gigabitEthernet 0/0/0

R1(config-if)# description Link to LAN

R1(config-if)# ip address 192.168.10.1 255.255.255.0

R1(config-if)# ipv6 address 2001:db8:acad:10::1/64

R1(config-if)# no shutdown

R1(config-if)# exit

R1(config)#

*Aug  1 01:43:53.435: %LINK-3-UPDOWN: Interface GigabitEthernet0/0/0, changed state to down

*Aug  1 01:43:56.447: %LINK-3-UPDOWN: Interface GigabitEthernet0/0/0, changed state to up

*Aug  1 01:43:57.447: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to up

R1(config)#

R1(config)#

R1(config)# interface gigabitEthernet 0/0/1

R1(config-if)# description Link to R2

R1(config-if)# ip address 209.165.200.225 255.255.255.252

R1(config-if)# ipv6 address 2001:db8:feed:224::1/64

R1(config-if)# no shutdown

R1(config-if)# exit

R1(config)#

*Aug  1 01:46:29.170: %LINK-3-UPDOWN: Interface GigabitEthernet0/0/1, changed state to down

*Aug  1 01:46:32.171: %LINK-3-UPDOWN: Interface GigabitEthernet0/0/1, changed state to up

*Aug  1 01:46:33.171: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/1, changed state to up

R1(config)#

  
  
  

10.2.3 Vérifier la configuration d'une interface

  
  

R1# show ip interface brief

Interface IP-Address OK ? Method Status Protocol

GigabiteThernet0/0/0 192.168.10.1 OUI manuel up

GigabiteThernet0/0/1 209.165.200.225 OUI manuel up

Vlan1 unassigned YES unset administratively down down

R1# show ipv6 interface brief

GigabitEthernet0/0/0 [up/up]

    FE80::201:C9FF:FE89:4501

    2001:DB8:ACAD:10::1

GigabitEthernet0/0/1 [up/up]

    FE80: :201:C9FF:FE 89:4502

    2001:DB8:ALIMENTATION:224::1

Vlan1 [administratively down/down]

    unassigned

R1#

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc4pMeIOVxXAsX8BMj8z0m0SlBq0OtLTrXdxGtRDqdHmuz_U2y9jznSGJS53ae9OoBLQB-pzmQWRCS7R_CplgL51L70_ofwhGtT1QMjEKqhvOgcjcuUV3P44v2p8dKbdhP8oOCpyg?key=GRdtFfUUp_nUsinyN5pTV7eK)

  
  
  
  

10.3.1 Passerelle par Défaut pour un hôte

  

Si votre réseau local (LAN) possède un seul routeur, il sert de passerelle, et tous les hôtes et commutateurs doivent être configurés en conséquence. Si plusieurs routeurs sont présents, vous devez en choisir un comme passerelle par défaut.

La passerelle par défaut permet à un périphérique final de communiquer avec des périphériques sur un autre réseau. Elle est généralement l'adresse IP de l'interface du routeur qui est connectée au réseau local. L'adresse IP de l'hôte et celle du routeur doivent être dans le même réseau.

  
  

Par exemple, dans un réseau IPv4 avec un routeur reliant deux sous-réseaux (192.168.10.0 et 192.168.11.0), chaque hôte est configuré avec la passerelle appropriée. Si PC1 envoie un paquet à PC2 dans le même réseau, la passerelle n'est pas utilisée, et le paquet est transmis directement via le commutateur.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd73GkqzBfeFhYlF35u6E5otCPJ8uYiMFuT2Yfg01BlK6kiUSdHPlHDFPm-d0Y-ofixLEWTVYPsTGSvxgpvZdlQuRRlLrejLK1ztiulIZaWBiXH_IE_EmlT-9y7XQAPU0LigJkNow?key=GRdtFfUUp_nUsinyN5pTV7eK)

  

Si PC1 envoie un paquet à PC3, qui se trouve sur un réseau différent, PC1 encapsule le paquet avec l'adresse IPv4 de PC3, mais le transmet à sa passerelle par défaut (interface G0/0/0 de R1). Le routeur R1 accepte le paquet et consulte sa table de routage pour déterminer quelle interface de sortie utiliser pour atteindre PC3. Une fois l'interface de sortie identifiée, R1 transmet

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcjoVHuNxgR7q1u-XzRnvaYjmURMe2nw7oq06W5TPrvb8Na4AmRMeJKDG0Hcy8oJnNtCdlqQTI5GGBZZ_BLnFTDjAmPFfONK3gAPX215RNELxBq7pBEbUivAfMZKbu1vNB1Go8J?key=GRdtFfUUp_nUsinyN5pTV7eK)

Le même processus se produirait sur un réseau IPv6, bien que cela ne soit pas indiqué dans la topologie. Les périphériques utiliseraient l'adresse IPv6 du routeur local comme passerelle par défaut.

  

10.3.2 Passerelle par défaut pour un commutateur

  

Un commutateur de couche 2 n'a pas besoin d'adresse IP pour fonctionner, mais une configuration IP peut être nécessaire pour l'administration à distance. Pour cela, une interface virtuelle de commutateur (SVI) doit être configurée avec une adresse IPv4 et un masque de sous-réseau. De plus, une passerelle par défaut est requise pour permettre la gestion du commutateur à distance depuis un autre réseau.

  

La passerelle par défaut sur le commutateur est généralement l'adresse IP de l'interface du routeur connectée au commutateur.

  

Pour la configurer, la commande suivante est utilisée en mode de configuration globale :

ip default-gateway <adresse_IP_routeur>.

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfztTX45vmqAU7-dkBumHGgLGnr7JEG8ybgHMFw3ay2HKmzlFuI53-CjkBSZIbu4qSV7q9X8bjFD0C4oqx80w6ZpRQ88dMczsZAymMeT7teWBSclZJGkTbR63s1Tn8A3OECADG9?key=GRdtFfUUp_nUsinyN5pTV7eK)

  
  
  
  

Dans cet exemple, l'hôte administrateur envoie un paquet à l'interface G0/0/1 de R1 via sa passerelle par défaut. R1 transmet ensuite ce paquet à S1 via son interface G0/0/0. Puisque l'adresse IPv4 source du paquet provient d'un autre réseau, S1 a besoin d'une passerelle par défaut pour pouvoir répondre et établir une connexion SSH avec l'hôte administratif.

Les paquets des hôtes connectés au commutateur doivent également avoir une passerelle par défaut configurée dans les systèmes d'exploitation des hôtes.

Un commutateur de groupe de travail peut aussi être configuré avec une adresse IPv6 sur un SVI, mais il n'est pas nécessaire de configurer manuellement la passerelle par défaut. Le commutateur recevra automatiquement cette passerelle via le message ICMPv6 Router Advertisement du routeur.

  

Diffences entres Les Routeurs 4000,1900,2900 :  

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd84az6hM_80hWH0T7mhGnBFhbxXfsCESMhFWhmh5cL1TCXzZcGVKXT8PrT_mBbhiSmZPe_saH2cH7Xf7jJdARLPcDkFs3Kz7Gg-nON83qfE4b3ZUe4NeZ-2SSfaDhN1vSGX_Zp6Q?key=GRdtFfUUp_nUsinyN5pTV7eK)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfE0TxEKwe3GKwlz0VCcHwcuMDYFOFFPFkT9F3FIAeEjwnEw3ZzAlxARC2Yv8CCaPW3ct5E6bKA4gCvrfuvKAZKRo2vB3KF49Ik8k-yT6ufLTxmHJtFEF8P4JVPpyn2fB2AzI3Q8A?key=GRdtFfUUp_nUsinyN5pTV7eK)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXee_POvcISLbcTxSB4Rx5hhv6s-xy51NSW4VYC9i2A2eC8xvZJdLFkyG7cG9Fs9_Kp7-y23W16O5cxFPqr5uv2uI9Pp39CVqJIXlta-T6CZAxruZLXzOq0PNJIiF9FJWdYjTUoShA?key=GRdtFfUUp_nUsinyN5pTV7eK)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfi-HRVwNH8sfKNvAMk-IbRb5XIalF24kcDL1GLK2hNNh977XdVsjoD4CLdYGk5zMrxpLRBtZHT5NhqGRoWcvk293SgUK6YGs6V9qPniOfvRabU2wzZRGuyyyKBPDe71iBZqJMz?key=GRdtFfUUp_nUsinyN5pTV7eK)

  
  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXecJ8fHPfnkdoRrJ4oAUuIMKYJSGIqdaUOLUIydNEvP0GGKUrmH7n-Wur7tLjARknNva57-JwSAb64SxBJWX6S5CBFWS1Ev-dwyCDE6DhKH-6_90R5naFf2we6qq6amJAHWyFoT?key=GRdtFfUUp_nUsinyN5pTV7eK)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcExNi7WcKqSZ_9GXPoz9xiyjIiUZY_pyjmEvxtIkCW4IApuGqTFjPWS5dfAhOGBWxwIw0cqvvcils9gV8ah8hZa89Oa52yFfMcMG1d85yv1sZdkCqOE_91EATiMnxVO4ms_j55?key=GRdtFfUUp_nUsinyN5pTV7eK)

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdi4BTAkuxe72ALVQTHEPjGA-LCGsqBs38xnxX6QSZmM3IhUN4seAtA0h_OeCen3EDGxpN3j-qW3fiEfyyNFLerpYkyVYmRvpL_7rF347HSpmKQloObBpCpQ_5rtOAFvTkb1zoEEw?key=GRdtFfUUp_nUsinyN5pTV7eK)

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfauudyPAq6LHD5j1ifFmUvhbn1fYN04-DZZJDmFrClmmgoP0m_hxRzpS7r61s0txir28A0svsHmLahPLYA3bxlp6Ejr1HsX3lS4WVj66Sn2urHK63ltkQCK05rdQRO5IH2Ou8WhA?key=GRdtFfUUp_nUsinyN5pTV7eK)

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd89HAkqTt2PQF-8ejzWqJAfXgK9Gkxbo6wWD1CgYr6TSHJG2FyZ_6gW3wHS5rwXqP7BetstfluSpnAnlqDXbG4uLY4ZQg9QYDnMzy7kjkgdpfVDYaxFE8kP8YS9HiSb0FzIqql7g?key=GRdtFfUUp_nUsinyN5pTV7eK)
