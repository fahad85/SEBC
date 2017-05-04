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
time hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar teragen -Ddfs.blocksize=32M -Dmapreduce.job.maps=4 10485760 /user/fahad85
```
Running this gave an error that the directory already exists. So reran the command by specifying a subdirectory inside the user's home directory (test2). As I have been facing space issues so created the teragen file as 1GB instead of the requested 10GB. The command failed with an premature EOF file failure which I suspect is due to the space issue even though atleast 47% disk is free.
```
real    0m16.058s
user    0m21.455s
sys     0m0.813s
```

## Using Terasort Command

Terasort is ran using the following command:
```
time hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar terasort /fahad85/test2 /fahad85/terasort
```

```
real    0m47.227s
user    0m54.617s
sys     0m3.500s
```