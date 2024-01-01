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

Don't forget to change the password !