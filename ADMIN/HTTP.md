mkdir /etc/httpd/sites-availabe

mkdir /etc/httpd/sites-enabled

mkdir -p /var/www/isetrades.org/html

mkdir -p /var/www/isetrage.org/log


chown -R $root:root /var/www/isetrades.org/html

chmod -R 755 /var/www


nano /var/www/isetrades.org/html/index.html
<html>
 <h1>voici</h1>
</html>

nano /etc/httpd/conf/httpd.conf
include /etc/httpd/sites-enabled

nano /etc/httpd/sites-available/isetrades.conf
<VirtualHost *:80>
        ServerName www.isetrades.org
         DocumentRoot /var/www/isetrades.org/html
         DirectoryIndex index.php index.html index.htm

         ErrorLog "/var/log/httpd/isetrades-error_log"
</VirtualHost>


ln -s /etc/httpd/sites-available/isetrades.conf /etc/httpd/sites-enabled/isetr>

systemctl restart httpd

tail -f /var/log/messages

nano /etc/hosts

160.160.1.5  isetrades.org
