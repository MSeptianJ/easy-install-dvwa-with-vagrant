# **Easy Install DVWA with Vagrant**

This repo will explain how to install [DVWA](https://github.com/digininja/DVWA) with vagrant to make VM with debian in it. This was made for my task in my university to do a penetration test with DVWA. You can do this easily after install the tools needed, you only need to have <2 GB of free RAM in you device.

## **Tools Needed**

- [Vagrant](https://www.vagrantup.com/)
- [Virtual Box](https://www.virtualbox.org/)
- [Git](https://git-scm.com/)

## **Reference**

- <https://github.com/digininja/DVWA>
- <https://kifarunix.com/install-and-setup-dvwa-on-debian-10/>
- <https://kifarunix.com/install-lamp-stack-with-mariadb-10-on-debian-10-buster/>
- <https://www.vagrantup.com/>

## **Steps**

<details>

### **Build VM**

- make a new folder and open a terminal to that folder
- initialise vagrant

```CMD
vagrant up
```

- replace the new made VagrantFile with VagrantFile from this repo, but change the name and ip
- build the VM

```CMD
vagrant up
```

- SSH to VM using vagrant

```CMD
vagrant ssh
```

### **Apps Installation**

- install all the apps needed

```CMD
sudo apt -y install apache2 libapache2-mod-php mariadb-server mariadb-client php php-mysql php-gd git
```

- Check apache with systemctl or type your ip address on your browser

```CMD
systemctl status apache2
```

- Secure mysql db (Optional)  

```CMD
sudo mysql_secure_installation
```

### **Make A DB**

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

### **Clone DVWA**

- Delete index file inside /var/www/html

``` CMD
sudo rm -rf /var/www/html/index.html
```

- Clone the DVWA repo, change the config file and use nano to edit it

``` CMD
sudo git clone https://github.com/ethicalhack3r/DVWA /var/www/html/
sudo cp /var/www/html/config/config.inc.php.dist /var/www/html/config/config.inc.php
sudo nano /var/www/html/config/config.inc.php
```

- Change the db_password to the password db you use

```PHP
$_DVWA[ 'db_server' ]   = '127.0.0.1';
$_DVWA[ 'db_database' ] = 'dvwa';
$_DVWA[ 'db_user' ]     = 'dvwa';
$_DVWA[ 'db_password' ] = 'YOURPASSWORD';
```

### **Make a reCAPTCHA v2**

- Dont close the nano app yet, and make a reCAPTCHA v2
- Click [here](https://www.google.com/recaptcha/admin) to go to google captcha
- place the site key to public key, and secret key to private key

```PHP
$_DVWA[ 'recaptcha_public_key' ]  = '';
$_DVWA[ 'recaptcha_private_key' ] = '';
```

- Save with Ctrl + S and close nano with Ctrl + X
- then restart db

``` CMD
sudo systemctl restart mariadb
```

### **Configure PHP**

- Now open php config

``` CMD
sudo nano /etc/php/7.4/apache2/php.ini
```

- Search for these terms and change the value

```txt
allow_url_include = On
allow_url_fopen = On
display_errors = off
```

- Change the owner and restart web server

``` CMD
sudo chown -R www-data:www-data /var/www/html
sudo systemctl restart apache2
```

### **Go to browser**

- use your browser and type VM's ip address "http://YOURIP/login.php"

- If you dont secure your db, you will login automaticaly but if you dont the acount is vvv  
name : admin  
password : password

- go to setup/reset DB
- click Create/Reset Database

</details>
