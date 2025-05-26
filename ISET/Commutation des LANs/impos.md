mac-address-table static <adresse_mac_H3> vlan 1 interface FastEthernet0/4

switchport port-security mac-address sticky` (une option pour apprendre dynamiquement et sécuriser) 

clear mac-address-table dynamic

- `switchport port-security mac-address sticky` is for dynamically learning a MAC address and then sticking to it.
- `switchport port-security mac-address <MAC_address>` is for manually configuring a specific static MAC address.


`switchport port-security maximum 1

switchport access vlan <id_vlan_correspondant>
switchport trunk native vlan 99



vtp mode server
vtp domain Lab4
vtp password cisco
show vtp status


interface fastethernet 0/1.1`
encapsulation dot1q 1       
ip address 172.17.1.1 255.255.255.0
`encapsulation dot1q 99 native`

show spanning-tree (sur Comm2)
spanning-tree vlan 1 priority 4096


interface range fa0/1-3`
   - `channel-group 1 mode desirable
   
   - `interface port-channel 1
   - switchport mode trunk 

monitor session 1 source interface Fa0/1
`monitor session 1 destination interface Fa0/2`

sh monitor session 1`
   
  