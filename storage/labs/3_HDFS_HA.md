# Enable HDFS HA

Add Journal nodes using roles in Cloudera Manager. Select one of the namenodes as part of the config. Add the Journal node directory as /data_xvdb/journal in the HDFS configurations. Click on HDFS and then from the drop down Actions select Enable HighAvailability. Select one of the other nodes (any) as a secondary failover journal. Click next through the other options till it started to enable the high availability feature. To enable HTTPFS role for HUE service to work with HDFS HA feature go to HDFS>Instances and then select Add Role Instances. Select HTTPFS and pick a host node (I have selected the namenode). After the role is added select the role and Actions for Selected>Start. Once this is done go to the HUE service and in configuration pick the HTTPFS role and save changes. Select HUE and from Actions select Restart. To upgrade Hive to use HDFS HA, stop HUE, Oozie and then Hive from CM. Click the Update Hive Metastore NameNodes and then restart all the services, Hive, Hue and Oozie
```
mysqldump -p metastore > /data_xvdb/metastore-backup.sql 
```
This will ask password for root
