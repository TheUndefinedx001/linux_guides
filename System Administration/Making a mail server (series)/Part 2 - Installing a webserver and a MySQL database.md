# Part 2 - Installing the webserver & MySQL database
As said in the previous part: Apache is a webserver that will provide webapps to work. PHP will hook into apache, so files with the .php extension will be processed before sending it back to the client on a website. This guide will also explain how to install/download and edit all the applications (phpMyAdmin and PostfixAdmin.)

### Installing MariaDB (The MySQL database)
1. Update, upgrade your apt. Install dirmngr (to add the correct MariaDB package)
```
apt update && apt upgrade
apt install dirmngr
```
2. Add the MariaDB signing key:
```
apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
```
3. Download and execute MariaDB's preperation of repository script:
```
curl -sS https://downloads.mariadb.com/MariaDB/mariadb_repo_setup | bash
```
4. Update your apt repository again, and install MariaDB
```
apt update && apt install mariadb-server
```
When asked for a root password, make sure you choose a good and safe password. This guide will not provide any options on changing the root password afterwards.

### Installing Apache & PHP and configuring the webserver
1. **Download and install apache and PHP packages**
```
apt install apache2 php php-mysql php-mbstring php-imap
```
2. **Start making a structure for your webserver.**

  The current directory structure of `/var/www/` looks likes this after installation:
```
/var/www/
│
└── html
```


My personal preferred directory structure is as followed:
```
/var/www/
│
├── example.com
│   └─ www (referring to WWW.example.com)
│      ├─ public (files served to clients that connect to example.com)
│      └─ tmp (uploads/temporary files reserved by PHP or any other instance for this domain only)
└── example.org
    ├─ www (referring to WWW.example.org)
    │  ├─ public
    │  └─ tmp 
    └─ beta (referring to subdomain BETA.example.org)
       ├─ public
       └─ tmp
```

To change the current structure to my preferred way, run the following commands:
```
rm -r /var/www/html/
mkdir -p /var/www/example.com/www/public
mkdir /var/www/example.com/www/tmp
chown -R www-data:www-data /var/www
chmod -R o-wrx /var/www
```


3. Create a virtual host by creating a new Apache config file. `nano /etc/apache2/sites-available/example.com.conf`, and insert the following:
```
<VirtualHost *:80>
  ServerName example.com
  ServerAlias www.example.com

  DocumentRoot /var/www/example.com/public
  
  php_admin_value "open_basedir" "/var/www/example.com/www"
  php_admin_value "upload_tmp_dir" "/var/www/example.com/www/tmp"
  
  ErrorLog ${APACHE_LOG_DIR}/www.example.com-error.log
  CustomLog ${APACHE_LOG_DIR}/www.example.com-access.log combined
</VirtualHost>

<Directory /var/www/example.com/www>
  AllowOverride All
</Directory>
```

4. Enable the site and restart Apache

`````` 
a2ensite example.com.conf
apachectl graceful
``````

5. Retrieve an SSL certificate for the webserver, which we will also use later on when installing the mail server

```
certbot --apache
# Follow the instructions as you wish, but when asked to redirect HTTP to HTTPS, select the option to REDIRECT (number 2) as of 2020.
```

6. Now check whether or not the website is secured with an SSL connection (should display as HTTPS://example.com, and a little (green) lock will show up as well in the address bar on most browsers).

### Downloading & setting up phpMyAdmin

1. Change your current directory so that you are actually in the public space of your website

```
cd /var/www/example.com/www/public
```

2. Now download and unzip the latest version of phpMyAdmin

```
wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.zip -O phpMyAdmin.zip
unzip phpMyAdmin.zip
mv phpMyAdmin-* phpMyAdmin/
chown -R www-data:www-data phpMyAdmin
```

3. Copy the sample configuration file

```
cd phpMyAdmin
cp config.sample.inc.php config.inc.php
```

4. Edit the configuration file, and only edit the $cfg['blowfish_secret'] by typing a lot of randomized characters `nano config.inc.php`

````
......
$cfg['blowfish_secret'] = 'RaNDOmI$eTH1sSTRINGWitHASMuTSHrandomCh@ractersBlabLBABLAItDOESNTMATTERWHATYOULLPUTHEREASLONGASITISLONGANDRANDOMASDkqkejwekljqw';
.....
````

5. Now, to see if you can visit the phpMyAdmin page, go to `example.com/phpMyAdmin/`. You can log in with the root credentials you filled in before when installing MariaDB. (Username = root).

### Downloading & setting up

**Tutorial details**

*Safety & Integrity*

| Date of last update | Security/Safety | Integrity    | Notes |
| ------------------- | --------------- | ------------ | ----- |
| 09-04-2020          | Unproven        | Not finished | None  |

*Testing & Checking*

| Date of test | Operating system | Result | Tested by | Notes |
| ------------ | ---------------- | ------ | --------- | ----- |
|              |                  |        |           |       |

*Contributors*

| Name             | Date of contribution | Description of contribution                   |
| ---------------- | -------------------- | --------------------------------------------- |
| TheUndefinedx001 | 09-04-2020           | Started with the guide and did initial tests. |