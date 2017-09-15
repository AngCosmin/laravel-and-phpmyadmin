# Learn how to install Laravel and Phpmyadmin

## Install Apache2
``sudo apt-get install apache2 -y``

## Install PHP7
``sudo apt-get install php7.0 libapache2-mod-php7.0 php7.0-cli php7.0-common php7.0-mbstring php7.0-gd php7.0-intl php7.0-xml php7.0-mysql php7.0-mcrypt php7.0-zip -y`` 

## Get Composer
``curl -sS https://getcomposer.org/installer | php``

- Move Composer
``sudo mv composer.phar /usr/local/bin/composer``

- Go to 
``cd /var/www/html``

- Create project
``sudo composer create-project laravel/laravel your-project --prefer-dist``

## Set name and group
``sudo chown cosmin:www-data your-project/ -R``

## Set permissions
``sudo chmod 775 -R your-project/storage/``

## Enable site
- Go to ``cd /etc/apache2/sites-available/``
- Create a new file ``sudo vim your-project.conf``
- Copy this in your-project.conf

```<VirtualHost *:80>
    ServerName yourproject.local

    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/your-project/public

    <Directory /var/www/html/project>
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

## Edit hosts
- Edit file ``sudo vim /etc/hosts``
- Add this line	``127.0.0.1   your-project.local``

# Go to:
http://your-project.local/




