# Challenge Sydney May 2017
## Challenge 4: HDFS Testing

Teragen command and output:
```
time hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar teragen -Ddfs.blocksize=16M -Dmapreduce.job.reduces=8 -Dmapreduce.map.java.opts.max.heap=512M 65536000 /tgen
```
