Wordpress Staging
-----------------
```
sudo su
apt-get update
apt-get upgrade -y
apt-get autoremove
apt-get install finger
apt-get dist-upgrade -y
apt-get autoremove -y
apt-get install apache2 php5 php5-cli php5-fpm php5-gd libssh2-php libapache2-mod-php5 php5-mcrypt mysql-server php5-mysql git unzip zip postfix php5-curl mailutils php5-json phpmyadmin -y
a2enmod rewrite headers
php5enmod mcrypt

vi /etc/apache2/sites-enabled/000-default.conf
--ADD LINE-- 
Include /etc/phpmyadmin/apache.conf

<VirtualHost *:80>
        #ServerName example.com
        #ServerAlias www.example.com
        DocumentRoot /var/www/html

        <Directory /var/www/html>
                Options -Indexes
                AllowOverride All
                Order allow,deny
                Allow from all
        </Directory>
</VirtualHost>

vi /etc/phpmyadmin/config.inc.php
--ADD LINES BELOW THE PMA CONFIG AREA AND FILL IN DETAILS--
$i++;
$cfg['Servers'][$i]['host']          = '__FILL_IN_DETAILS__';
$cfg['Servers'][$i]['port']          = '3306';
$cfg['Servers'][$i]['socket']        = '';
$cfg['Servers'][$i]['connect_type']  = 'tcp';
$cfg['Servers'][$i]['extension']     = 'mysql';
$cfg['Servers'][$i]['compress']      = FALSE;
$cfg['Servers'][$i]['auth_type']     = 'config';
$cfg['Servers'][$i]['user']          = '__FILL_IN_DETAILS__';
$cfg['Servers'][$i]['password']      = '__FILL_IN_DETAILS__';

cd /var/www/html
rm -rf *
cd ../
mkdir staging
cd staging
git clone https://github.com/pakwai122/wordpress.git .
wget https://wordpress.org/latest.zip
chmod -R 755 .
chown -R www-data:www-data .

edit php upload size and post size
vi /etc/php5/apache2/php.ini

service apache2 restart
```
After Wordpress Is Configured
-----------------------------
```
define('WP_REDIS_HOST', '');
```
