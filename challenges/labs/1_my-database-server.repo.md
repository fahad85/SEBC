# Challenge Sydney May 2017
## Challenge 1: Install a DB Server

MariaDB Server Repo:
```
[mariadb]
name = MariaDB-5.5.39
baseurl=http://yum.mariadb.org/5.5/rhel7-amd64
# alternative: baseurl=http://archive.mariadb.org/mariadb-5.5.39/yum/rhel7-amd64/
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```

sudo yum install MariaDB-server
mkdir -p /var/log/mariadb/
chmod -R 777 /var/log/mariadb/
/etc/init.d/mysql start