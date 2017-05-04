## Test HDFS Performance

Create end-user and its HDFS home directory as follows:

```
sudo useradd fahad85
sudo -u hdfs hadoop fs -mkdir /user/fahad85
sudo -u hdfs hadoop fs -chmod 777 /user/fahad85
```

## Using Teragen to test performance

Teragen is invoked as follows:
```
time hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar teragen -Ddfs.blocksize=32M -Dmapreduce.job.maps=4 1073741824 /user/fahad85
```
Running this gave an error that the directory already exists. So reran the command by specifying a subdirectory inside the user's home directory. As I have been facing space issues so created the teragen file as 1GB instead of the requested 10GB.
because of space limitations, creating 1GB file instead of two. The command failed with an premature EOF file failure which I suspect is due to the space issue even though atleast 47% disk is free.