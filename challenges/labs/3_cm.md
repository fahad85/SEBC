# Challenge Sydney May 2017
## Challenge 3: Install CDH 5.10

Command output for hdfs ls:
```
Found 7 items
drwxr-xr-x   - hdfs   supergroup          0 2017-05-04 21:31 /user/cate
drwxrwxrwx   - mapred hadoop              0 2017-05-04 21:25 /user/history
drwxrwxr-t   - hive   hive                0 2017-05-04 21:26 /user/hive
drwxrwxr-x   - hue    hue                 0 2017-05-04 21:27 /user/hue
drwxrwxr-x   - impala impala              0 2017-05-04 21:26 /user/impala
drwxr-xr-x   - hdfs   supergroup          0 2017-05-04 21:31 /user/jemaine
drwxrwxr-x   - oozie  oozie               0 2017-05-04 21:27 /user/oozie

```

CM API call Hosts:
```
[root@ip-172-31-9-64 ec2-user]# curl -X GET -u "admin:admin" -i http://ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com:7180/api/v14/hosts
HTTP/1.1 200 OK
Expires: Thu, 01-Jan-1970 00:00:00 GMT
Set-Cookie: CLOUDERA_MANAGER_SESSIONID=x4x6tobmwe5su8lamudegw5i;Path=/;HttpOnly
Content-Type: application/json
Date: Fri, 05 May 2017 01:36:05 GMT
Transfer-Encoding: chunked
Server: Jetty(6.1.26.cloudera.4)

{
  "items" : [ {
    "hostId" : "ad6b4c6d-1be3-4dd1-a487-b9630fac4228",
    "ipAddress" : "172.31.4.2",
    "hostname" : "ec2-54-206-103-248.ap-southeast-2.compute.amazonaws.com",
    "rackId" : "/default",
    "hostUrl" : "http://ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com:7180/cmf/hostRedirect/ad6b4c6d-1be3-4dd1-a487-b9630fac4228",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332438016
  }, {
    "hostId" : "9313e224-6ace-4a39-8dee-7f223f943d27",
    "ipAddress" : "172.31.12.181",
    "hostname" : "ec2-54-206-115-9.ap-southeast-2.compute.amazonaws.com",
    "rackId" : "/default",
    "hostUrl" : "http://ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com:7180/cmf/hostRedirect/9313e224-6ace-4a39-8dee-7f223f943d27",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332438016
  }, {
    "hostId" : "79554f35-dfb2-4322-825b-a4d7c40895a8",
    "ipAddress" : "172.31.0.116",
    "hostname" : "ec2-54-206-116-17.ap-southeast-2.compute.amazonaws.com",
    "rackId" : "/default",
    "hostUrl" : "http://ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com:7180/cmf/hostRedirect/79554f35-dfb2-4322-825b-a4d7c40895a8",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332438016
  }, {
    "hostId" : "8d954b9f-5359-4346-860b-920f6adea19d",
    "ipAddress" : "172.31.7.206",
    "hostname" : "ec2-54-206-121-18.ap-southeast-2.compute.amazonaws.com",
    "rackId" : "/default",
    "hostUrl" : "http://ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com:7180/cmf/hostRedirect/8d954b9f-5359-4346-860b-920f6adea19d",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332438016
  }, {
    "hostId" : "e65b5789-3a45-4d02-a570-0b09b7111bbd",
    "ipAddress" : "172.31.9.64",
    "hostname" : "ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com",
    "rackId" : "/default",
    "hostUrl" : "http://ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com:7180/cmf/hostRedirect/e65b5789-3a45-4d02-a570-0b09b7111bbd",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332438016
  } ]
```

CM API call:
```

[ec2-user@ec2-54-206-80-163 ~]$ curl -X GET -u "admin:admin" -i http://ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com:7180/api/v6/clusters/fahad85/services
HTTP/1.1 200 OK
Expires: Thu, 01-Jan-1970 00:00:00 GMT
Set-Cookie: CLOUDERA_MANAGER_SESSIONID=1vq1c9z2eab0idoswvol0af0d;Path=/;HttpOnly
Content-Type: application/json
Date: Fri, 05 May 2017 02:05:27 GMT
Transfer-Encoding: chunked
Server: Jetty(6.1.26.cloudera.4)

{
  "items" : [ {
    "name" : "hive",
    "type" : "HIVE",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com:7180/cmf/serviceRedirect/hive",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "HIVE_HIVEMETASTORES_HEALTHY",
      "summary" : "GOOD"
    }, {
      "name" : "HIVE_HIVESERVER2S_HEALTHY",
      "summary" : "GOOD"
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "Hive"
  }, {
    "name" : "zookeeper",
    "type" : "ZOOKEEPER",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com:7180/cmf/serviceRedirect/zookeeper",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "ZOOKEEPER_CANARY_HEALTH",
      "summary" : "GOOD"
    }, {
      "name" : "ZOOKEEPER_SERVERS_HEALTHY",
      "summary" : "GOOD"
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "ZooKeeper"
  }, {
    "name" : "hue",
    "type" : "HUE",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com:7180/cmf/serviceRedirect/hue",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "HUE_HUE_SERVERS_HEALTHY",
      "summary" : "GOOD"
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "Hue"
  }, {
    "name" : "oozie",
    "type" : "OOZIE",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com:7180/cmf/serviceRedirect/oozie",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "OOZIE_OOZIE_SERVERS_HEALTHY",
      "summary" : "GOOD"
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "Oozie"
  }, {
    "name" : "impala",
    "type" : "IMPALA",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com:7180/cmf/serviceRedirect/impala",
    "serviceState" : "STARTED",
    "healthSummary" : "BAD",
    "healthChecks" : [ {
      "name" : "IMPALA_ASSIGNMENT_LOCALITY",
      "summary" : "DISABLED"
    }, {
      "name" : "IMPALA_CATALOGSERVER_HEALTH",
      "summary" : "BAD"
    }, {
      "name" : "IMPALA_IMPALADS_HEALTHY",
      "summary" : "GOOD"
    }, {
      "name" : "IMPALA_STATESTORE_HEALTH",
      "summary" : "GOOD"
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "Impala"
  }, {
    "name" : "yarn",
    "type" : "YARN",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com:7180/cmf/serviceRedirect/yarn",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "YARN_JOBHISTORY_HEALTH",
      "summary" : "GOOD"
    }, {
      "name" : "YARN_NODE_MANAGERS_HEALTHY",
      "summary" : "GOOD"
    }, {
      "name" : "YARN_RESOURCEMANAGERS_HEALTH",
      "summary" : "GOOD"
    }, {
      "name" : "YARN_USAGE_AGGREGATION_HEALTH",
      "summary" : "DISABLED"
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "YARN (MR2 Included)"
  }, {
    "name" : "hdfs",
    "type" : "HDFS",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://ec2-54-206-80-163.ap-southeast-2.compute.amazonaws.com:7180/cmf/serviceRedirect/hdfs",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "HDFS_BLOCKS_WITH_CORRUPT_REPLICAS",
      "summary" : "GOOD"
    }, {
      "name" : "HDFS_CANARY_HEALTH",
      "summary" : "GOOD"
    }, {
      "name" : "HDFS_DATA_NODES_HEALTHY",
      "summary" : "GOOD"
    }, {
      "name" : "HDFS_FREE_SPACE_REMAINING",
      "summary" : "GOOD"
    }, {
      "name" : "HDFS_HA_NAMENODE_HEALTH",
      "summary" : "GOOD"
    }, {
      "name" : "HDFS_MISSING_BLOCKS",
      "summary" : "GOOD"
    }, {
      "name" : "HDFS_UNDER_REPLICATED_BLOCKS",
      "summary" : "GOOD"
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "HDFS"
  } ]

```