**Etherchannel (LACP – PAGP)**

  

- **Configuration Switch SW1**

    - `enable`

    - `configure terminal`

    - `interface range fa0/1-3`

    - `channel-group 1 mode desirable`

    - `interface range fa0/7-9`

    - `channel-group 2 mode desirable`

- **Configuration Switch SW2**

    - `enable`

    - `configure terminal`

    - `interface range fa0/1-3`

    - `channel-group 1 mode auto`

    - `interface range fa0/4-6`

    - `channel-group 3 mode desirable`

- **Configuration du Switch SW3**

    - `enable`

    - `configure terminal`

    - `interface range fa0/4-6` (attention à l'espace dans `fa 0/4-6` dans le doc)

    - `channel-group 3 mode auto`

    - `interface range fa0/7-9` (attention à l'espace dans `fa 0/7-9` dans le doc)

    - `channel-group 2 mode auto`

- **Pour vérifier votre configuration d’agrégation**

    - `show etherchannel summary`

- **Pour configurer le port agrégé**

    - `interface port-channel 1`

    - (Exemples de commandes dans l'interface port-channel)

        - `switchport mode trunk`

        - `port-security` (serait `switchport port-security`)

        - `bpduguard` (serait `spanning-tree bpduguard enable`)



   - `interface range fa0/1-3`
   - `channel-group 1 mode desirable`
   - `interface port-channel 1`
   - 
