# Learn how to install Laravel and Phpmyadmin

# 1. Laravel

### Install Apache2
``sudo apt-get install apache2 -y``

### Install PHP7
- Install ``sudo apt-get install software-properties-common python-software-properties`` for ``add-apt-repository``
- ``sudo add-apt-repository ppa:ondrej/php``
- ``sudo apt-get update``
- ``sudo apt-get install php7.1``

### Get Composer
- Get 
``curl -sS https://getcomposer.org/installer | php``
- Move Composer
``sudo mv composer.phar /usr/local/bin/composer``
- Go to 
``cd /var/www/html``
- Create project
``sudo composer create-project laravel/laravel your-project --prefer-dist``

### Set name and group
``sudo chown cosmin:www-data your-project/ -R``

### Set permissions
``sudo chmod 775 -R your-project/storage/``

### Enable site
- Go to 
``cd /etc/apache2/sites-available/``
- Create a new file 
``sudo vim your-project.conf``
- Copy this in your-project.conf
```<VirtualHost *:80>
    ServerName yourproject.local

    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/your-project/public

    <Directory /var/www/html/your-project>
        AllowOverride All
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
- Disable default site ``sudo a2dissite 000-default.conf``
- Enable your site ``sudo a2ensite your-project.conf``
- Set mode ``sudo a2enmod rewrite``
- Reload and restart apache ``sudo service apache2 reload`` and ``sudo service apache2 restart``

### Edit hosts
- Edit file ``sudo vim /etc/hosts``
- Add this line	``127.0.0.1   your-project.local``

### Go to:
http://your-project.local/


# 2. Phpmyadmin

- Install mysql-server
``sudo apt-get install mysql-server``
- Install phpmyadmin
``sudo apt-get install phpmyadmin``

### Problems:
#### If phpmyadmin was installed with success but when you go on http://localhost/phpmyadmin you receive a not found message, then do this:
- Open file 
``sudo vim /etc/apache2/apache2.conf``
- Add this line somewhere:
``Include /etc/phpmyadmin/apache.conf``

**All tested on elementaryOS 0.4.1 Loki**

