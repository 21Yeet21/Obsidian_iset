
# === RIP v2 ===
router rip
 version 2
 no auto‐summary
 network 10.0.0.0
 network 192.168.0.0
 redistribute static
 default‐information originate

interface Serial0/0
 ip summary‐address rip 10.0.0.0 255.255.252.0
 
# Default route learned via RIP
R1# show ip route
R*   0.0.0.0/0 [120/1] via 10.0.0.2

# Static route redistributed into RIP and learned via RIP
R2# show ip route
R    172.16.0.0/16 [120/2] via 10.0.0.1

### EIGRP
router eigrp 1 
 network 10.0.0.0
 network 192.168.0.0
 no auto-summary
 passive-interface GigabitEthernet0/1
 redistribute static


interface Serial0/0
ip summary-address eigrp 100 10.0.0.0 255.255.252.0

ip route 0.0.0.0 0.0.0.0 192.168.1.1


# === OSPFv2 ===
router ospf 1
 network 10.0.0.0 0.0.0.255 area 0
 network 192.168.0.0 0.0.0.255 area 1
 area 0 range 10.0.0.0 255.255.255.0
 summary‐address 192.168.100.0 255.255.255.0
 default‐information originate
 redistribute static subnets
