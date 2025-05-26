

hostnamectl  set-hostname server.institut.tn


nmcli device


nmcli connection modify ens33  ipv4.addresses 200.100.10.20/24



nmcli connection modify ens33 ipv4.method manual


nmcli connection down ens33; nmcli connection up ens33