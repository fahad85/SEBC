# HDFS Storage Labs
## Storage Replication

Create source folder in hdfs
```
sudo -u hdfs hadoop fs -mkdir /fahad85
sudo -u hdfs hadoop fs -mkdir /irfanelahi-ds
```

Run Teragen to generate 500MB data using the following command:
```
sudo -u hdfs hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar teragen 524288000 /fahad85
```
This fails with the error that the directory already exists. Deleted the directory and ran the command above again which resulted in a mapreduce job.
The above job failed due to replication factor being 3 in HDFS and set to 0 in the teragen file. Changed the HDFS replication to 1 and reran the job after deleteing the directory /fahad85
Also set the  HDFS Replication Environment Advanced Configuration Snippet (Safety Valve) in HDFS>Configuration to one datanode and ran teh following command. For distcp the source is my partner's location and destination is my target folder as distcp is a pull not a push.

```
hadoop distcp webhdfs://ec2-52-65-127-89.ap-southeast-2.compute.amazonaws.com/irfanelahi-ds/part-m-00000 hdfs://ec2-54-252-147-158.ap-southeast-2.compute.amazonaws.com/irfanelahi-ds
```
