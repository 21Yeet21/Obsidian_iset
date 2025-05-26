


cp /etc/named.conf /etc/named.conf.orig

nano /etc/named.conf

add

zone "isetrades.tn" IN {
type master;
file "zone.isetrades";
allow-update { none; };
};

zone "10.100.200.in-addr.arpa" IN {
type master;
file "zone.200.100.10";
allow-update { none; };
};


quit

nano /var/named/zone.isetrades

add

$TTL 86400
@   IN  SOA server1.isetrades.tn. root.isetrades.tn. (
        2011071001  ; Serial
        3600        ; Refresh
        1800        ; Retry
        604800      ; Expire
        86400       ; Minimum TTL
)

@       IN  NS      server1.isetrades.tn.

server1 IN  A       200.100.10.1
station1 IN  A      200.100.10.21


nano /var/named/zone.200.100.10

add


$TTL 86400
@   IN  SOA     server1.isetrades.tn. root.isetrades.tn. (
        2011071001  ; Serial
        3600        ; Refresh
        1800        ; Retry
        604800      ; Expire
        86400       ; Minimum TTL
)

@       IN  NS      server1.isetrades.tn.

1       IN  PTR     server1.isetrades.tn.
21      IN  PTR     station1.isetrades.tn.



named-checkconf
named-checkzone zone.isetrades /var/named/ zone.isetrades
named-checkzone 200.100.10.21 /var/named/zone.200.100.1


chgrp named -R /var/named
chown -v root:named /etc/named.conf



nslookup server1.isetrades.tn


nslookup 200.100.10.1