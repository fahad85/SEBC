# Challenge Sydney May 2017
## Challenge 2: Install CM

Command output for repo:
```
ls /etc/yum.repos.d/
```
[root@ip-172-31-9-64 ec2-user]# ls /etc/yum.repos.d
cloudera-manager.repo  MariaDB.repo  redhat.repo  redhat-rhui-client-config.repo  redhat-rhui.repo  rhui-load-balancers.conf
```

Command for editing the db.conf
```
/usr/share/cmf/schema/scm_prepare_database.sh mysql cmanager cmanager cmanager -uroot -pcloudera
```
