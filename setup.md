### Installation process

You will need a LAMP stack. In this process, we use Apache, MariaDB and php 8.2
- Create and set up BDD :
    - `mysql -u root -p`
    - `CREATE DATABASE yourDBName;`
    - `CREATE USER 'yourDBUser'@'localhost' IDENTIFIED BY 'YourPassword';`
    - `GRANT ALL PRIVILEGES ON yourDBName.* TO 'yourDBUser'@'localhost';`
⚠️ You will need to store the credential in the .env file !

- Install Imagick and Ghostscript
    - `apt install ghostscript`
    - `apt install php8.2-imagick imagick`
- In order to allow ImageMagick to process PDF files, you edit the following file: `/etc/ImageMagick-6/policy.xml`
    - Locate `<policy domain="coder" rights="none" pattern="PDF" />`
    - and comment it : `<!--<policy domain="coder" rights="none" pattern="PDF" />-->`
- Clone the app and move it to where you want
- run `composer install`
- run `npm install` and `npm run build`
- edit .env file
- `php artisan key:generate`
- `php artisan migrate`
- `php artisan db:seed`

An admin user is created, so you can login with : Mail : `admin@system.localhost` / Password : `d4d5ehdpdepd81 `

⚠️ Don't forget to change the password after the first login !

Create the Cron Task (for generating the thumbnails, sending notifications)
- `crontab -e -u www-data`
- add `*/5  *  *  *  * php /path/artisan queue:work --stop-when-empty`

- Create the Apache2 site file :
```
<VirtualHost *:80>
    DocumentRoot /path/to/public_folder
    ServerName blog.paulhenry.eu
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    <Directory /path/to/public_folder>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

- Optionaly, you can use Firebase to send push notifications to the users
