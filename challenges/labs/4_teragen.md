# Challenge Sydney May 2017
## Challenge 4: HDFS Testing

Teragen command and output :
```
time hadoop jar \
/opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar \
teragen \
-Ddfs.blocksize=16M \
-Dmapreduce.job.maps=8 \
-Dmapreduce.map.java.opts.max.heap=512M \
-Dmapreduce.job.reduces=8 \
65536000  \
/user/cate/tgen

```

Time output
```
real    2m2.091s
user    0m6.143s
sys     0m0.316s
```

HDFS LS:

```
[cate@ec2-54-206-80-163 ec2-user]$ hdfs dfs -ls /user/cate/tgen
Found 9 items
-rw-r--r--   3 cate supergroup          0 2017-05-04 22:01 /user/cate/tgen/_SUCCESS
-rw-r--r--   3 cate supergroup  819200000 2017-05-04 22:00 /user/cate/tgen/part-m-00000
-rw-r--r--   3 cate supergroup  819200000 2017-05-04 22:00 /user/cate/tgen/part-m-00001
-rw-r--r--   3 cate supergroup  819200000 2017-05-04 22:00 /user/cate/tgen/part-m-00002
-rw-r--r--   3 cate supergroup  819200000 2017-05-04 22:00 /user/cate/tgen/part-m-00003
-rw-r--r--   3 cate supergroup  819200000 2017-05-04 22:00 /user/cate/tgen/part-m-00004
-rw-r--r--   3 cate supergroup  819200000 2017-05-04 22:00 /user/cate/tgen/part-m-00005
-rw-r--r--   3 cate supergroup  819200000 2017-05-04 22:01 /user/cate/tgen/part-m-00006
-rw-r--r--   3 cate supergroup  819200000 2017-05-04 22:01 /user/cate/tgen/part-m-00007
```