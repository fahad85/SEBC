# Test HDFS Snapshots

Create a directory in HDFS as follows and copy the ZIP course file into it
```
sudo -u hdfs hadoop fs -mkdir /precious
```
WINSCP to the ZIP to the node's local directory and then move to HDFS location
```
sudo -u hdfs hadoop fs -put /SEBC.zip /precious
```

Enable snapshot on the drive by going to Cloudera Manager and in HDFS select File Browser. Click on the directory and enable snapshot. Screenshot attached.

Create snapshot as follows:
```
sudo -u hdfs hadoop fs -createSnapshot /precious sebc-hdfs-test
```

Delete the directory as follows:
```
sudo -u hdfs hadoop fs -rmdir /precious
```
Error is thrown that the directory cannot be deleted as it is snapshottable.

Delete the file as follows:
```
sudo -u hdfs hadoop fs -rm /precious/SEBC.zip
```

Restoring the deleted file as follows:
```
sudo -u hdfs hadoop fs -cp /precious/.snapshot/sebc-hdfs-test/SEBC.zip /precious
```