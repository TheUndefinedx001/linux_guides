# Installing MariaDB (thanks to linode.com)
For some reason, the default setup for MariaDB on Debian isn't working quite right. It skips the root password prompt, and the root password is quite a hassle to change after the password prompt.

Please ensure you are in a root environment.  
If you have sudo privileges, you can type:
```
sudo su
```

1. Update repository, upgrade several applications & install dirmngr:
```
apt update && apt upgrade && apt install dirmngr
```

2. Add the MariaDB signing key:
```
apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
```

3. Download and execute MariaDB's preperation of repository script:
```
curl -sS https://downloads.mariadb.com/MariaDB/mariadb_repo_setup | sudo bash
```

4. Update repository again, and install MariaDB
```
apt update && apt install mariadb-server
```

|Date (of last submission)|Security/Safety|Notes|
|--|--|--|
|22-11-2017|Unproven|Might need an update for newer versions of Debian. Uses Ubuntu keyserver.|
