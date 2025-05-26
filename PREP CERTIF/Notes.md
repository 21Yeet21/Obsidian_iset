vlan batch 100,200

interface g0/0/1 
port link-type access
port default vlan 100

interface g0/0/2
port link-type access
port default vlan 200



interface g0/0/3 
port link-type acces
port default vlan 50

==system-view==
==interface GigabitEthernet 0/0/5==
==port link-type trunk==
==port trunk allow-pass vlan 10 20 30==
==port trunk pvid vlan 1==
==quit==
==display port vlan==


port link-type trunk
port trunk allow-pass vlan 100

ospf 1 router-id 1.1.1.1
area 0
network 192.168.12.1 0.0.0.0
interface g0/0/1 
ip address 192.168.12.1

interface g0/0/1
ip address 192.168.12.2

ospf router-id 2.2.2.2
area 0
network 192.168.12.2 0.0.0.0


R1
ospf router-id 1.1.1.1
area 0
network 192.168.1.1 0.0.0.0
ospf cost 1000

ospf router-id 2.2.2.2
area 0 
network 192.168.1.2 0.0.0.0
ospf cost 900

ospf router-id 3.3.3.3
area 0
network 192.168.1.3

area 0
network 192.168.1.1 0.0.0.0 
network 192.168.2.1 0.0.0.0

==ospf passive-interface GigabitEthernet 0/0/2==

ospf 1
==import-route direct==
quit

ip route-static 172.16.0.0 16 g0/0/1

ip route-static 10.0.0.0 24 G0/0/1

ip route-static 0.0.0.0 0 203.0113.2


system-view
vlan batch  10 20
interface g0/0/2
port link-type access
port default vlan 10
quit

interface g0/0/3
port link-type access
port default vlan 20
quit

interface g0/0/1
port link-type trunk
port trunk allow-pass vlan 10 20
port trunk pvid vlan 99
quit







