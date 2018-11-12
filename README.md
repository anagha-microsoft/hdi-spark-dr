# HDInsight-Spark: Replication to DR datacenter on Azure with distcp - by example

This sample covers DR for HDInsight Spark leveraging distcp.<br>
In this example, we will provision HDInsight Spark and dependencies in US East 2 (primary) and US West 2 (secondary).  The following are steps to deploy and configure replication to DR.<br>

## 1.  Primary datacenter - USEast2 - setup

### 1.0.1. Provision resource group in USEast2
Create a resource group.<br>
![Create USE2 RG](images/1-create-rg.png)
<br><br>

### 1.0.2. Provision a virtual network in the resource group
![Create vnet 1](images/2-provision-vnet-1.png)
<br><br>
<hr>

![Create vnet 2](images/2-provision-vnet-2.png)
<br><br>
<hr>

![Create vnet 3](images/2-provision-vnet-3.png)
<br><br>
<hr>

![Create vnet 4](images/2-provision-vnet-4.png)
<br><br>
<hr>

![Create vnet 5](images/2-provision-vnet-5.png)
<br><br>
<hr>

![Create vnet 6](images/2-provision-vnet-6.png)
<br><br>
<hr>

![Create vnet 7](images/2-provision-vnet-7.png)
<br><br>
<hr>


### 1.0.3. Provision HDInsight Spark in the resource group to use the Vnet
![Create hdi 1](images/3-provision-hdi-1.png)
<br><br>
<hr>

![Create hdi 2](images/3-provision-hdi-2.png)
<br><br>
<hr>

![Create hdi 3](images/3-provision-hdi-3.png)
<br><br>
<hr>

![Create hdi 4](images/3-provision-hdi-4.png)
<br><br>
<hr>

![Create hdi 5](images/3-provision-hdi-5.png)
<br><br>
<hr>

![Create hdi 6](images/3-provision-hdi-6.png)
<br><br>
<hr>

![Create hdi 7](images/3-provision-hdi-7.png)
<br><br>
<hr>

![Create hdi 8](images/3-provision-hdi-8.png)
<br><br>
<hr>

### 1.0.3. Connect to the HDInsight Spark cluster - Ambari cluster manager
![Create hdi 9](images/3-provision-hdi-9.png)
<br><br>
<hr>

![Create hdi 10](images/3-provision-hdi-10.png)
<br><br>
<hr>

![Create hdi 11](images/3-provision-hdi-11.png)
<br><br>
<hr>

![Create hdi 12](images/3-provision-hdi-12.png)
<br><br>
<hr>

### 1.0.4. Connect to the HDInsight Spark cluster - via SSH
![Create hdi 13](images/3-provision-hdi-13.png)
<br><br>
<hr>

![Create hdi 14](images/3-provision-hdi-14.png)
<br><br>
<hr>

![Create hdi 15](images/3-provision-hdi-15.png)
<br><br>
<hr>

## 2.  Secondary datacenter - USWest2 - setup

Repeat the same steps in the secondary datacenter.<br>
2.1. Create a resource group<br>
2.2. Within the resource group, provision  virtual network with **address range that does not overlap with the virtual network in the primary datacenter**<br>
2.3. Within the resource group, provision  HDInsight Spark within the virtual network created in 2.2

## 3.  Global Vnet peering

We will now peer the virtual networks of the primary and secondary datacenters.
### 3.0.1. Peer the primary datacenter's vnet to the secondary datacenter's
![Create vnet-peer-1](images/4-global-vnet-peering-1.png)
<br><br>
<hr>

![Create vnet-peer-2](images/4-global-vnet-peering-2.png)
<br><br>
<hr>

![Create vnet-peer-3](images/4-global-vnet-peering-3.png)
<br><br>
<hr>

![Create vnet-peer-4](images/4-global-vnet-peering-4.png)
<br><br>
<hr>

![Create vnet-peer-11](images/4-global-vnet-peering-11.png)
<br><br>
<hr>

### 3.0.2. Peer the secondary datacenter's vnet to the primary datacenter's

![Create vnet-peer-5](images/4-global-vnet-peering-5.png)
<br><br>
<hr>

![Create vnet-peer-6](images/4-global-vnet-peering-6.png)
<br><br>
<hr>

![Create vnet-peer-7](images/4-global-vnet-peering-7.png)
<br><br>
<hr>

![Create vnet-peer-8](images/4-global-vnet-peering-8.png)
<br><br>
<hr>

![Create vnet-peer-9](images/4-global-vnet-peering-9.png)
<br><br>
<hr>

![Create vnet-peer-10](images/4-global-vnet-peering-10.png)
<br><br>
<hr>

## 4.  Attach storage accounts for data to each custer

### 4.1. Create storage account and attach to primary cluster

##### 4.1.1. Create storage account
![Create sa-1](images/5-create-storage-1.png)
<br><br>
<hr>

![Create sa-2](images/5-create-storage-2.png)
<br><br>
<hr>

##### 4.1.2. Attach to the cluster
![Create sa-3](images/5-create-storage-3.png)
<br><br>
<hr>

![Create sa-4](images/5-create-storage-4.png)
<br><br>
<hr>

![Create sa-5](images/5-create-storage-5.png)
<br><br>
<hr>


## 5.  Execute distcp

## 6. Validate replication

## 7. Other considerations






