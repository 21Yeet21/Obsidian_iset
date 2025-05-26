systemctl enable nfs-server

systemctl start nfs-server

mkdir /rep_new

chown nobody:nobody /rep_new

touch /rep/fichier_1

nano /etc/exports
/rep_new 160.160.1.5

exportfs -arv

showmount -e 160.160.1.5

mkdir -p /rep_partage

mount 160.160.1.5:/rep_new /rep_partage

df -h



perm : 
nano /etc/fstab

160.160.1.5:/rep_new /rep_partage nfs
auto,nofail,noatime,nolock,intr,tcp,actimeo=1800 0 0

umount /rep_partage