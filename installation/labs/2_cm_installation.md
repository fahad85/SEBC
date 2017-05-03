# Installing Cloudera Manager

Downloaded the cloudera manager repo using wget
```
wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/cloudera-manager.repo
```
Edited the cloudera-manager.repo to pick CM 5.9.2 instead of 5.11
````
sudo vi cloudera-manager.repo
sudo cp cloudera-manager.repo /etc/yum.repos.d/
```

Install cloudera manager using yum install
```
sudo yum install cloudera-manager-daemons cloudera-manager-server
/usr/share/cmf/schema/scm_prepare_database.sh mysql cmanager cmanager cmanager -uroot -pcloudera 
```

Started Cloudera Manager Server host using the following command which failed:
```
sudo service cloudera-scm-server start
```
Possible cause was SELinux which was enabled so disabled that using the following command
```
sudo vi /etc/selinux/config
edit SELINUX=enforcing to disabled
reboot
```
This still did not fix the error which was now suggesting that JAVA_HOME is not correct. Opened the following file and added JAVA_HOME to it.
```
sudo vi /etc/default/cloudera-scm-server
export JAVA_HOME=/opt/jdk1.8.0_121
```

MariaDB was not set to start on reboot so there was still an error in starting Cloudera Manager. Also set JAVA_HOME again
```
sudo service mariadb stop
sudo service mariadb start
sudo service mariadb status
export JAVA_HOME=/opt/jdk1.8.0_121

export JRE_HOME=/opt/jdk1.8.0_121/jre

export PATH=$PATH:/opt/jdk1.8.0_121/bin:/opt/jdk1.8.0_121/jre/bin:/bin

sudo vi /etc/environment
JAVA_HOME=/opt/jdk1.8.0_121
JRE_HOME=/opt/jdk1.8.0_121/jre
PATH=$PATH:/opt/jdk1.8.0_121/bin:/opt/jdk1.8.0_121/jre/bin:/bin

```
added the inbound rule to allow 7180 port in the EC2 instances security group.
```

Started Cloudera Manager Wizard using
```
http://54.252.147.158:7180
username admin password admin
```

Inorder to install parcels CM requires root access
```
vi /root/.ssh/authorized_keys
```
Delete the lines at the begining of the file until you get to the words ssh-rsa.
```
vi /etc/ssh/sshd_config
```
Uncomment `PermitRootLogin` and replace with `PermitRootLogin without-password`
Once done then do the following:
```
sudo service sshd reload
```

Added all the hosts to the cluster and selected services to run on various nodes. Screenshot of services attached.
Ensure that all services using database are installed on the respective node as this caused issues when testing connection for the databases.
Changed Host Monitor, Service Monitor Storage and Zookeeper directories to /data_xvdb

Zookeeper threw an error of missing JDK directory because Cloudera Manager Wizard installed a different version of JDK than the one installed manually.
Ended up changing all JDKs to JDK1.7.80 using the following steps
```
tar xzf jdk-7u80-linux-x64.tar.gz -C /usr/java/
export JAVA_HOME=/usr/java/jdk.1.7.0_80
vi /etc/default/cloudera-scm-server
change JAVA_HOME to export JAVA_HOME=/usr/java/jdk.1.7.0_80
sudo vi /etc/environment
JAVA_HOME=/usr/java/jdk.1.7.0_80
JRE_HOME=/usr/java/jdk.1.7.0_80/jre
PATH=$PATH:/usr/java/jdk.1.7.0_80/bin:/usr/java/jdk.1.7.0_80/jre/bin:/bin
```

Recommendation would be to manually install the required JDK to all the nodes in a cluster instead of having CM install it for you so that all versions are the same.
Do not enter Java Home Directory in Hosts using Cloudera Manager as it causes conflicts with the environment settings
For nodes not having Cloudera Manager Server edit the cloudera-scm-agent file

Changed all the log directories in services and cloudera management services to /data_xvdb and also change Cloudera Management Service Command Storage Directory
Changing the config.ini for agent to data_xvdb
 https://www.cloudera.com/documentation/enterprise/5-4-x/topics/cm_ag_view_server_logs.html

sudo vi /etc/cloudera-scm-agent/config.ini
uncomment log_file add /data_xvdb
mkdir -p /data_xvdb/var/log/cloudera-scm-agent
chown cloudera-scm:cloudera-scm /data_xvdb/var/log/cloudera-scm-agent
service cloudera-scm-agent restart

Doing the above steps did not resolve the issue so ended up reverting the changes

For DNS resolution error did the following steps on all the hosts:
```
sudo vi /etc/sysconfig/network

HOSTNAME=ec2-54-252-147-158.ap-southeast-2.compute.amazonaws.com
hostnamectl set-hostname "ec2-54-252-147-158.ap-southeast-2.compute.amazonaws.com" --static

HOSTNAME=ec2-54-206-92-189.ap-southeast-2.compute.amazonaws.com 
hostnamectl set-hostname "ec2-54-206-92-189.ap-southeast-2.compute.amazonaws.com" --static

HOSTNAME=ec2-54-206-57-163.ap-southeast-2.compute.amazonaws.com 
hostnamectl set-hostname "ec2-54-206-57-163.ap-southeast-2.compute.amazonaws.com" --static

HOSTNAME=ec2-54-252-150-153.ap-southeast-2.compute.amazonaws.com 
hostnamectl set-hostname "ec2-54-252-150-153.ap-southeast-2.compute.amazonaws.com" --static

HOSTNAME=ec2-54-206-60-153.ap-southeast-2.compute.amazonaws.com 
hostnamectl set-hostname "ec2-54-206-60-153.ap-southeast-2.compute.amazonaws.com" --static

service cloudera-scm-agent stop
service cloudera-scm-agent start
```