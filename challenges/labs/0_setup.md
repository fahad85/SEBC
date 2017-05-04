# Challenge Sydney May 2017
## Challenge Setup

Cloud Provider:
```
AWS
```

Nodes IP Address and Name:
```
172.31.9.64   ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com
172.31.4.2   ec2-54-206-103-248.ap-southeast-2.compute.amazonaws.com
172.31.0.116   ec2-54-206-116-17.ap-southeast-2.compute.amazonaws.com
172.31.7.206   ec2-54-206-121-18.ap-southeast-2.compute.amazonaws.com
172.31.12.181   ec2-54-206-115-9.ap-southeast-2.compute.amazonaws.com
```

Linux Release:
```
Red Hat Enterprise Linux Server release 7.2 (Maipo)
```

Disk Space:
```
[root@ip-172-31-9-64 ec2-user]# df -k
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/xvda2      52416492 1633988  50782504   4% /
devtmpfs         7599360       0   7599360   0% /dev
tmpfs            7486540       0   7486540   0% /dev/shm
tmpfs            7486540   16628   7469912   1% /run
tmpfs            7486540       0   7486540   0% /sys/fs/cgroup
tmpfs            1497312       0   1497312   0% /run/user/1000
```

```
[root@ip-172-31-4-2 ec2-user]# df -k
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/xvda2      52416492 1633788  50782704   4% /
devtmpfs         7599360       0   7599360   0% /dev
tmpfs            7486540       0   7486540   0% /dev/shm
tmpfs            7486540   16628   7469912   1% /run
tmpfs            7486540       0   7486540   0% /sys/fs/cgroup
tmpfs            1497312       0   1497312   0% /run/user/1000
```

```
[root@ip-172-31-0-116 ec2-user]# df -k
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/xvda2      52416492 1632596  50783896   4% /
devtmpfs         7599360       0   7599360   0% /dev
tmpfs            7486540       0   7486540   0% /dev/shm
tmpfs            7486540   16628   7469912   1% /run
tmpfs            7486540       0   7486540   0% /sys/fs/cgroup
tmpfs            1497312       0   1497312   0% /run/user/1000
```

```
[root@ip-172-31-7-206 ec2-user]# df -k
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/xvda2      52416492 1632848  50783644   4% /
devtmpfs         7599360       0   7599360   0% /dev
tmpfs            7486540       0   7486540   0% /dev/shm
tmpfs            7486540   16628   7469912   1% /run
tmpfs            7486540       0   7486540   0% /sys/fs/cgroup
tmpfs            1497312       0   1497312   0% /run/user/1000
```

```
[root@ip-172-31-12-181 ec2-user]# df -k
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/xvda2      52416492 1632928  50783564   4% /
devtmpfs         7599360       0   7599360   0% /dev
tmpfs            7486540       0   7486540   0% /dev/shm
tmpfs            7486540   16628   7469912   1% /run
tmpfs            7486540       0   7486540   0% /sys/fs/cgroup
tmpfs            1497312       0   1497312   0% /run/user/1000
```

Repolist Enabled:
```
[root@ip-172-31-9-64 ec2-user]# yum repolist enabled
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                                                                                     repo name                                                                                                                  status
!rhui-REGION-client-config-server-7/x86_64                                                                  Red Hat Update Infrastructure 2.0 Client Configuration Server 7                                                                 6
!rhui-REGION-rhel-server-releases/7Server/x86_64                                                            Red Hat Enterprise Linux Server 7 (RPMs)                                                                                   14,277
!rhui-REGION-rhel-server-rh-common/7Server/x86_64                                                           Red Hat Enterprise Linux Server 7 RH Common (RPMs)                                                                            228
repolist: 14,511
```

Create Linux Users and Groups:
```
sudo useradd -u 2300 cate
sudo useradd -u 2900 jemaine
sudo groupadd kiwis
sudo groupadd aussies
usermod -aG kiwis jemaine
usermod -aG aussies cate
```

List for `/etc/passwd` cate and jemaine:
```
[root@ip-172-31-9-64 ec2-user]# cat /etc/passwd | grep cate
cate:x:2300:2300::/home/cate:/bin/bash
[root@ip-172-31-9-64 ec2-user]# cat /etc/passwd | grep jemaine
jemaine:x:2900:2900::/home/jemaine:/bin/bash
```

List for '/etc/group` kiwis and aussies:
```
[root@ip-172-31-9-64 ec2-user]# cat /etc/group | grep kiwis
kiwis:x:2901:jemaine
[root@ip-172-31-9-64 ec2-user]# cat /etc/group | grep aussies
aussies:x:2902:cate
```