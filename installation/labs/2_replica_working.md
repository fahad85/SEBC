# Installing MariaDB and Replica Database
## Installing MariaDB

```
sudo yum install mariadb-server
sudo service mariadb stop
```
Update/Paste the following settings in the my.cnf file
```
[mysqld]
transaction-isolation = READ-COMMITTED
# Disabling symbolic-links is recommended to prevent assorted security risks;
# to do so, uncomment this line:
# symbolic-links = 0

key_buffer = 16M
key_buffer_size = 32M
max_allowed_packet = 32M
thread_stack = 256K
thread_cache_size = 64
query_cache_limit = 8M
query_cache_size = 64M
query_cache_type = 1

max_connections = 550
#expire_logs_days = 10
#max_binlog_size = 100M

#log_bin should be on a disk with enough free space. Replace '/var/lib/mysql/mysql_binary_log' with an appropriate path for your system
#and chown the specified folder to the mysql user.
log_bin=/var/lib/mysql/mysql_binary_log

binlog_format = mixed

read_buffer_size = 2M
read_rnd_buffer_size = 16M
sort_buffer_size = 8M
join_buffer_size = 8M

# InnoDB settings
innodb_file_per_table = 1
innodb_flush_log_at_trx_commit  = 2
innodb_log_buffer_size = 64M
innodb_buffer_pool_size = 4G
innodb_thread_concurrency = 8
innodb_flush_method = O_DIRECT
innodb_log_file_size = 512M

[mysqld_safe]
log-error=/var/log/mariadb/mariadb.log
pid-file=/var/run/mariadb/mariadb.pid
```

Installed JDK on ec2-54-252-147-158.ap-southeast-2.compute.amazonaws.com as follows:
```
cd /opt/
wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u121-b13/e9e7ea248e2c4826b92b3f075a80e441/jdk-8u121-linux-x64.tar.gz"
"http://download.oracle.com/otn/java/jdk/7u80-b15/jdk-7u80-linux-x64.tar.gz"

tar xzf jdk-8u121-linux-x64.tar.gz

cd /usr/java/jdk1.8.0_121/
alternatives --install /usr/bin/java java /usr/java/jdk1.8.0_121/bin/java 2
alternatives --config java

alternatives --install /usr/bin/jar jar /usr/java/jdk1.8.0_121/bin/jar 2
alternatives --install /usr/bin/javac javac /usr/java/jdk1.8.0_121/bin/javac 2
alternatives --set jar /usr/java/jdk1.8.0_121/bin/jar
alternatives --set javac /usr/java/jdk1.8.0_121/bin/javac
java -version

export JAVA_HOME=/usr/java/jdk1.8.0_121

export JRE_HOME=/usr/java/jdk1.8.0_121/jre

export PATH=$PATH:/usr/java/jdk1.8.0_121/bin:/usr/java/jdk1.8.0_121/jre/bin:/bin
```

Installed JDBC connectors on all the nodes using the following:
```
wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.42.tar.gz
tar zxvf mysql-connector-java-5.1.42.tar.gz
```

Create the java /usr/share/java/ as it doesnot exist and then copy the jar file to this location
```
sudo mkdir -p /usr/share/java/
sudo cp mysql-connector-java-5.1.42/mysql-connector-java-5.1.42-bin.jar /usr/share/java/mysql-connector-java.jar
```

After that created databases for Oozie, Activity Monitor, Reports Manager, Hive Metastore Server, Hue Server Sentry Server, Cloudera Navigator Audit Server, and Cloudera Navigator Metadata Server
```
mysql -u root -p
create database database DEFAULT CHARACTER SET utf8;
eg create database hue DEFAULT CHARACTER SET utf8;
grant all on database.* TO 'user'@'%' IDENTIFIED BY 'password';
eg grant all on hue.* TO 'hue'@'%' IDENTIFIED BY 'hue';
```