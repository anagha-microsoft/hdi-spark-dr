# HDInsight-Spark - High Availability and Disaster Recovery

[High availability](README.md#1--architectural-considerations-for-high-availability)<br>
[Disaster recovery](DisasterRecovery.md)<br>

## 1.  Architectural considerations for High Availability 

HDInsight Spark service has many infrastructure and service components and when architectecting high availability of your application/solution, the following are the considerations.  To level-set, high-availability as referenced in this section has to do with *fault tolerance within the same datacenter*.

### 1.0.1. HDInsight platform infrastructure - storage
HDInsight leverages a choice of Azure objects storage and Azure Data Lake Store for HDFS compatible storage system.<BR>

**Azure Blob Storage:**
The storage service redundancy default is LRS (Locally Redundant Storage) and  automatically maintains 3 replicas of each object.  In the event of any failure, it serves up a replica, seamlessly.<BR>
 
### 1.0.2. HDInsight platform infrastructure - compute
Azure VMs have an SLA, as do HDInsight master and worker nodes.  To maintain the SLA, the HDInsight service actively montors the health of the nodes and replaces failied nodes automatically.  For the highest fault tolerance HDInsight places nodes across fault and update domains intelligently.

### 1.0.3. HDInsight platform infrastructure - metastore RDBMS
HDInsight leverages Azure SQL Database for metastore RDBMS for Ambari, Hive & Oozie.  The service can provision a metastore for you, or you can provide a metastore at provision time.  This Azure SQL Database service automatically maintains 3 copies of data and serves up a replica in the event of a failure, seamlessly.

### 1.0.4. HDInsight platform component - gateway
HDInsight service provides a HTTPS gateway to the cluster. The gateway presents SSL cert, handles cluster credentials validation, and also acts a reverse proxy to communicate with few Hadoop services running on the cluster. The gateway is highly-available out of the box in active-standby mode.  

### 1.0.5. Hadoop service component - master nodes
There are several services in Hadoop that have a master-slave architecture.  For HA of masters, HDInsight comes with two master nodes, both active and the services distributes master roles in active and standby across the two nodes for maximizing FT.  The same are provisioned intelligently for maximum FT across fault and update domains.

### 1.0.6. Hadoop service component - Zookeeper
Zookeeper is a distributed coordination service and is a foundational service.  HDInsight leverages 3 Zookeeper servers - the minimum recommended for HA.

### 1.0.7. Hadoop service component - HDFS
HDFS namenode is enabled HA out of the box and the two instances primary and standby are distributed across the two master nodes.

### 1.0.8. Hadoop service component - YARN
YARN resource manager is enabled HA out of the box and the two instances primary and standby are distributed across the two master nodes.

### 1.0.9. Hadoop service component - Hive
The Hive services like Hive metastore, HiveServer2, Hive WebHCat server are all configured HA across the two master nodes.

### 1.0.10. Hadoop service component - Oozie
Oozie server is configured HA across the two master nodes.

### 1.0.11. Hadoop service component - Spark2
- Spark2 history server is not configured HA because the service does not support HA.  In the event of a failure, you can attempt recover or deploy the component on a different node. 
- Livy server supports remote REST based interaction with Spark2 service. Livy is not configured HA because the service does not support HA.  In the event of a failure, you can attempt recover or deploy the component on a different node. 
- Thrift server is configured HA across the two master nodes.

### 1.0.12. Hadoop service component - Notebook services 
Notebok services Jupyter and Zepplin are not configured HA.  In the event of a failure, you can attempt recover or deploy the component on a different node. 

### 1.0.13. Hadoop service component - Ambari
Ambari is configured HA across the two master nodes.

### 1.0.14. What about distributed processing jobs submitted to the cluster?
By default YARN attempts each task of each job 4 times, and if it fails on one node manager, will attempt on another.  A job is failed when all the 4 attempts fail for any task that is part of the job.  This number is configurable.

Additionally - the cluster services are constantly heartbeating to notify they are alive and when out of contact beyond configured threshold - will get blacklisted and no jobs are pushed to the same node managers.

## 2.  Architectural considerations for Disaster Recovery
[Next](DisasterRecovery.md)
