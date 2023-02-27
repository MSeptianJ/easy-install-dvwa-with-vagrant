# **Instalation Steps**

## **Apps Installation**

- install all the apps needed

```CMD
sudo apt -y install apache2 libapache2-mod-php mariadb-server mariadb-client php php-mysql php-gd git
```

- Check apache with systemctl or type your ip address on your browser

```CMD
systemctl status apache2
```

- Secure db (Optional)  

```CMD
sudo mysql_secure_installation
```

## **Make A DB**

- Go to mysql and make a new database

```CMD
sudo mysql -u root -p
```

- Use these command to make a new database with new user

```SQL
create database dvwa;
-- prettier-ignore
grant all on dvwa.* to dvwa@localhost identified by 'YOURPASSWORD';
flush privileges;
quit
```

## **Clone DVWA**

- Delete index file inside /var/www/html

``` CMD
sudo rm -rf /var/www/html/index.html
```

``` CMD
sudo git clone https://github.com/ethicalhack3r/DVWA /var/www/html/
sudo cp /var/www/html/config/config.inc.php.dist /var/www/html/config/config.inc.php
sudo nano /var/www/html/config/config.inc.php
```

```PHP
$_DVWA[ 'db_server' ]   = '127.0.0.1';
$_DVWA[ 'db_database' ] = 'dvwa';
$_DVWA[ 'db_user' ]     = 'dvwa';
$_DVWA[ 'db_password' ] = 'YourMom';
```

## **Make a reCAPTCHA v2**

"https://www.google.com/recaptcha/admin"

```PHP
$_DVWA[ 'recaptcha_public_key' ]  = '';
$_DVWA[ 'recaptcha_private_key' ] = '';
```

``` CMD
sudo systemctl restart mariadb
```

## **Configure PHP**

``` CMD
sudo nano /etc/php/7.4/apache2/php.ini
```

```txt
allow_url_include = On
allow_url_fopen = On
display_errors = off
```

``` CMD
sudo chown -R www-data:www-data /var/www/html
sudo systemctl restart apache2
```

## **Go to browser**

"http://YOURIP/login.php"

- If you dont secure your db, you will login automaticaly but if you dont the acount is vvv
name : admin  
password : password

- go to setup/reset DB
- click Create/Reset Database
