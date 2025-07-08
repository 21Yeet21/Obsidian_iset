
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

### EIGRP
router eigrp 1 
 network 10.0.0.0
 network 192.168.0.0
 no auto-summary
 passive-interface GigabitEthernet0/1
 redistribute static

interface Serial0/0
ip summary-address eigrp 1 10.0.0.0 255.255.252.0

ip route 0.0.0.0 0.0.0.0 192.168.1.1


# === OSPFv2 ===
router ospf 1
router-id 1.1.1.1
 network 10.0.0.0 0.0.0.255 area 0
 network 192.168.0.0 0.0.0.255 area 1
 area 0 range 10.0.0.0 255.255.255.0
 summary‐address 192.168.100.0 255.255.255.0
 default‐information originate
 redistribute static subnets
