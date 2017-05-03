# Cloudera Services Bootcamp Sydney May 2017
## 1_preinstall.md steps

## Setting swappiness to 1
```
cat /proc/sys/vm/swappiness
sudo su root
sudo echo 1 > /proc/sys/vm/swappiness
```

## Mount Attributes of volume
```
df -k
```
Check what devices are available:
```
lsblk
```
Is the file system installed:
```
sudo file -s /dev/xvdb
```
Showing of 'data' means no OS is installed
```
sudo mkfs -t ext4 /dev/xvdb
sudo mkdir /data_xvdb
sudo mount /dev/xvdb /data_xvdb
```
UUID of the mounted volume can be checked as follows:
```
ls -al /dev/disk/by-uuid/
```
then: 
```
sudo vi /etc/fstab: 
UUID=enter the UUID from the command above here /data_xvdb              ext4    defaults        0 2 

863a9b5e-4f12-4ce8-a74a-c641a2e80c1b Node1
fc1c96be-b9c2-4241-a623-67221b00a1bc Node2
42412fcd-7b51-4839-8845-e578e8d9920e Node3
9dc9cfce-24e1-4bd4-9116-f4dabf3e1502 Node4
8811e924-01a3-4938-ba34-42598f1f5dd4 Node5
```
Physical attributes can be checked using `df -k` or `lsblk`

## Reserve Space Listing
`sudo  tune2fs -l /dev/xvdb`

## Turn off Transparent Hugepage
```
cat /sys/kernel/mm/transparent_hugepage/enabled
sudo su root
echo never >/sys/kernel/mm/transparent_hugepage/enabled
echo never > /sys/kernel/mm/transparent_hugepage/defrag
```

## List Network Interface Configuration
`ifconfig`

## Forward Reverse Host Lookups
Change hostname 
```
sudo vi /etc/hosts
172.31.12.172   ec2-54-252-147-158.ap-southeast-2.compute.amazonaws.com
172.31.10.136   ec2-54-206-92-189.ap-southeast-2.compute.amazonaws.com
172.31.1.28   ec2-54-206-57-163.ap-southeast-2.compute.amazonaws.com
172.31.6.209   ec2-54-252-150-153.ap-southeast-2.compute.amazonaws.com
172.31.5.234   ec2-54-206-60-153.ap-southeast-2.compute.amazonaws.com
```

Used `getent hosts <IP>` to get the hostname details. Snapshot attached.
nslookup was not installed so ran the following to install utility:
`sudo yum install bind-utils`

## NSCD Service
`service nscd status`
NSCD service was not active and not installed so used the following command to install it first:
`sudo yum install nscd`
Started the nscd service
`sudo service nscd start`
Check that service is running
`service nscd status`

## NTPD Service
`service ntpd status`
NTPD service was not active and installed so used the following command to install it first:
`sudo yum install ntp`
Started the ntpd service
`sudo service ntpd start`
Check that service is running
`service ntp status`