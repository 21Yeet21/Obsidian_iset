

**Atelier Port Mirroring**

  

- **Port mirroring d’un seul port (entre port fa0/1 pc0 vers fa0/2 pc2)**

    - Le document montre une image avec :

        - `monitor session 1 source interface Fa0/1`

        - `monitor session 1 destination interface Fa0/2`

    - Ensuite, le texte explique :

        - `Switch(config)#monitor session 1 source interface fa0/1 both`

        - `Switch(config)#monitor session 1 destination interface fa0/2`

- **Vérification (implicite par la sortie montrée)**

    - `Switch#sh monitor session 1` (ou `show monitor session 1`)

  
