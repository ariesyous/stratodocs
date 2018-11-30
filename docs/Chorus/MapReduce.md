# Map Reduce 

**Overview**

The Symphony MapReduce service lets you run and scale big data frameworks (such as YARN or Spark) across instances in a Symphony region.

Functionality is exposed in the GUI under  **Map Reduce**. In the CLI, the functionality is in the  `symp mapreduce`commands.

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.

**Required administrator tasks**

Before a user can create and access a MapReduce cluster, an admin user must  **enable the MapReduce service**  and  **enable a MapReduce engine**.

**To enable the MapReduce service:**

1. Click  **Menu** > **Region Management**  >  **Settings**  >  **Services & Support**.

2. Under  **Manage Cluster Services**, click the  **Map Reduce**  button to toggle from OFF to ON.

**To enable a MapReduce engine**:

1. Does your Symphony system have Internet access?

-   If your Symphony system is installed in a dark site (no Internet access), you first need to  [obtain a MapReduce image and upload it into Symphony](https://www.stratoscale.com/knowledge/obtaining-a-mapreduce-image).
-   If your Symphony system has Internet access, skip this step and continue at the next step.

2. Click  **Menu**  >  **Map Reduce**  >  **Engines**  > select an engine.

3. Click the selected engine's  **Enabled**  button to toggle from OFF to ON.

## Creating a Map Reduce Cluster

**Prerequisites**

Before you can create a MapReduce cluster, an admin user must enable both the  [MapReduce service and a MapReduce engine](https://www.stratoscale.com/knowledge/manage-the-mapreduce-service).

**Instance groups and scaling**

To enable scaling (growing and shrinking a cluster over time), when you first create the cluster, you need to specify the following instance groups:

<table class="wrapped confluenceTable"><colgroup><col><col><col><col></colgroup><tbody><tr><th class="confluenceTh">Instance group name</th><th class="confluenceTh">Description</th><th class="confluenceTh">How many groups of this type in the cluster?</th><th class="confluenceTh">How many instances in this group?</th></tr><tr><td class="confluenceTd">MASTER</td><td class="confluenceTd">Manages the cluster by running software components that coordinate the distribution of data and tasks among other nodes (instances).</td><td class="confluenceTd">Exactly one.</td><td class="confluenceTd">Exactly one.</td></tr><tr><td class="confluenceTd">CORE</td><td class="confluenceTd">Contains software components that run tasks and store data in the Hadoop Distributed File System (HDFS) on your cluster.</td><td class="confluenceTd">Exactly one.</td><td class="confluenceTd">Variable. To scale the cluster, you can add and subtract nodes from the CORE instance group.</td></tr></tbody></table>

### Create a Map Reduce cluster via the GUI

1. Click  **Menu**  >  **Map Reduce**  >  **Clusters**  >  **Create**.

2. Fill out the following panels in the Create Cluster wizard and click  **Finish**  when done:

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><td class="highlight-blue confluenceTd" style="text-align: center;" colspan="2" data-highlight-colour="blue"><strong>Details</strong></td></tr><tr><td class="confluenceTd"><strong>Name</strong></td><td class="confluenceTd">Name of the cluster.</td></tr><tr><td class="confluenceTd" colspan="1"><strong>Version</strong></td><td class="confluenceTd" colspan="1">Select the engine version you want to use as the basis of this cluster.</td></tr><tr><td class="confluenceTd"><strong>Description</strong></td><td class="confluenceTd">Optional description</td></tr><tr><td class="confluenceTd" style="text-align: center;" colspan="2"><strong>Master Group</strong></td></tr><tr><td class="confluenceTd"><strong>Master Instance Type</strong></td><td class="confluenceTd"><p>Select the instance type you want to use for the master node (the one instance that is in the MASTER group). Valid values are:</p><p>m1.medium</p><p>m1.large</p><p>m1.xlarge</p></td></tr><tr><td class="confluenceTd" style="text-align: center;" colspan="2"><strong>Core Group</strong></td></tr><tr><td class="confluenceTd"><strong>Number of instances</strong></td><td class="confluenceTd">Specify how many instances you want in the core group. You can grow and shrink the cluster by adding and subtracting instances in the CORE group.</td></tr><tr><td class="confluenceTd"><strong>Slave Instance Type</strong></td><td class="confluenceTd"><p>Select the instance type you want to use for the instance(s) in the CORE group. Valid values are:</p><p>m1.medium</p><p>m1.large</p><p>m1.xlarge</p></td></tr><tr><td class="highlight-blue confluenceTd" style="text-align: center;" colspan="2" data-highlight-colour="blue"><strong>Network</strong></td></tr><tr><td class="confluenceTd"><strong>Key Pair</strong></td><td class="confluenceTd">Select the <a href="https://www.stratoscale.com/knowledge/enabling-secure-ssh-access-to-a-vm#enablingsecuresshaccesstoavm-key">key pair</a> to use for accessing this cluster. (To create a key pair on the fly, click the plus sign icon to the right of this field.)</td></tr><tr><td class="confluenceTd"><strong>Network</strong></td><td class="confluenceTd">Select the network to use for this cluster. (To create a network on the fly, click the plus sign icon to the right of this field.)</td></tr><tr><td class="confluenceTd"><strong>Master Security Group</strong></td><td class="confluenceTd">Optional.&nbsp; Select a security group to use with the master node (the one instance that is in the MASTER group).</td></tr><tr><td class="confluenceTd" colspan="1"><strong>Slave Security Group</strong></td><td class="confluenceTd" colspan="1">Optional.&nbsp; Select a security group to use with the instances in the CORE group.</td></tr><tr><td class="highlight-blue confluenceTd" style="text-align: center;" colspan="2" data-highlight-colour="blue"><strong>S3</strong></td></tr><tr><td class="confluenceTd" colspan="1"><strong>Endpoint</strong></td><td class="confluenceTd" colspan="1">If you are storing your Map Reduce data on S3, fill in the endpoint here.</td></tr><tr><td class="confluenceTd" colspan="1"><strong>Key</strong></td><td class="confluenceTd" colspan="1">S3 access key.</td></tr><tr><td class="confluenceTd" colspan="1"><strong>Secret</strong></td><td class="confluenceTd" colspan="1">S3 secret key.</td></tr></tbody></table>

**Create MapReduce cluster via the CLI**

This example creates a cluster with a master instance group and a core instance group with 2 nodes. The example also enables hive, so that you can run hive applications on the cluster.

		 # symp -k mapreduce cluster create mr mykey --instance-groups='[{"name": "mg", "instance_role": "master", "instance_type": "m1.medium"}, {"instance_role": "core", "instance_type": "m1.large", "instance_count": 2}]' --applications hive
		Starting new HTTPS connection (1): virtual-nb.service.strato

		Connecting in insecure mode!
		+--------------------------+--------------------------------------+
		| Field                    | Value                                |
		+--------------------------+--------------------------------------+
		| id                       | b063a472-bd46-44fe-bcf9-a9f0878b79c9 |
		| name                     | mr                                   |
		| status                   | Pending                              |
		| status_details           | None                                 |
		| user_id                  | admin                                |
		| account_id               | default                              |
		| tags                     | None                                 |
		| network_id               | 5243d159-2bae-41a6-b647-d77706f83474 |
		| key_name                 | mykey                                |
		| created_at               | 2018-01-25T21:31:17.029257           |
		| updated_at               | 2018-01-25T21:31:17.029257           |
		| instance_collection_type | group                                |
		| engine_revision_id       | 67703994-a1b3-497d-92d6-106a044f8d34 |
		| applications             | yarn                                 |
		| master_port_id           | None                                 |
		| engine_version_id        | 5ecd267c-3923-455b-b39c-78e622c15890 |
		| security_group_id        | a9db603c-f19c-43f1-8bda-e62f6304f92d |
		| project_id               | 8637594b9662443cb5552bac2ddf7281     |
		| description              | None                                 |
		+--------------------------+--------------------------------------+

		#  symp -k mapreduce cluster instances e43f7061-07bc-49e2-abdc-d0b8a21d0372
		Starting new HTTPS connection (1): virtual-nb.service.strato
		Connecting in insecure mode!
		+--------------------------------------+--------+------------+---------------------------+---------------------+--------------------------------------+-------------+--------------------------------------+---------------+--------------------------------------+---------+---------------------+--------------------------------------+---------------+----------------------------------+
		| id                                   | status | account_id | instance_fqdn             | updated_at          | cluster_id                           | instance_ip | vm_id                                | instance_role | group_id                             | user_id | created_at          | security_group_id                    | instance_type | project_id                       |
		+--------------------------------------+--------+------------+---------------------------+---------------------+--------------------------------------+-------------+--------------------------------------+---------------+--------------------------------------+---------+---------------------+--------------------------------------+---------------+----------------------------------+
		| 033e9b37-8817-4936-9731-094c5cc0d4da | Active | default    | host-10-47-214-6.symphony | 2018-01-25T17:08:20 | e43f7061-07bc-49e2-abdc-d0b8a21d0372 | 10.47.214.6 | 90fa8b33-c728-429c-9e45-003eb17e2de8 | core          | 1880e8d8-5056-4a8f-841f-caaf8d7208ee | admin   | 2018-01-25T17:07:52 | 80ed2025-107c-40be-b109-57de7f67e94e | m1.large      | c9d76237a0a24ecfaf967dd48a7a65d2 |
		| 090c6e29-c3bd-4653-8078-64658471f858 | Active | default    | host-10-47-214-8.symphony | 2018-01-25T17:08:19 | e43f7061-07bc-49e2-abdc-d0b8a21d0372 | 10.47.214.8 | 2a8c5b75-da0e-4e2a-ab85-b6e929d31b5c | core          | 1880e8d8-5056-4a8f-841f-caaf8d7208ee | admin   | 2018-01-25T17:07:52 | 80ed2025-107c-40be-b109-57de7f67e94e | m1.large      | c9d76237a0a24ecfaf967dd48a7a65d2 |
		| a8dde0dd-c097-4a08-b043-28ccc656c23e | Active | default    | host-10-47-214-4.symphony | 2018-01-25T17:08:22 | e43f7061-07bc-49e2-abdc-d0b8a21d0372 | 10.47.214.4 | 6f62b473-2746-4dd6-8f80-c2f681dffd32 | master        | c98c4410-a81e-49c8-b4bc-f9328c9f8302 | admin   | 2018-01-25T17:07:52 | 80ed2025-107c-40be-b109-57de7f67e94e | m1.medium     | c9d76237a0a24ecfaf967dd48a7a65d2 |
		+--------------------------------------+--------+------------+---------------------------+---------------------+--------------------------------------+-------------+--------------------------------------+---------------+--------------------------------------+---------+---------------------+--------------------------------------+---------------+----------------------------------+

**Hadoop applications you can enable on the cluster**

When you create a cluster, the creation process enables YARN by default. You can use the  `--applications`  argument to enable additional applications. Legal values for the  `--applications`  argument are:

alluxio
ambari
apex
crunch
flink
flume
giraph
gpdb
hbase
hcat
hdfs
hdfsha
hdfsnonha
hive
httpfs
hue
ignite_hadoop
kafka
kerberos
mahout
mapred
oozie
pig
qfs
solrcloud
spark
spartstandalone
sqoop
tez
yarn
ycsb
zeppelin
zookeeper

# Connect to a MapReduce Cluster

1.  [Get the IP of the master node](https://www.stratoscale.com/knowledge/map-reduce/use-the-mapreduce-service/connect-to-a-mapreduce-cluster/#ConnecttoaMapReduceCluster-IP)  (the one instance in the MASTER group).

2.  [SSH into the master node](https://www.stratoscale.com/knowledge/map-reduce/use-the-mapreduce-service/connect-to-a-mapreduce-cluster/#ConnecttoaMapReduceCluster-SSH)  and run one of your MapReduce jobs.

## **Get the IP of the master node via GUI**

**GUI**

Menu >  **MapReduce**  >  **Clusters**  > click on cluster name >  **Instances**  >  **master_instance**  >  **Networks**  > VM IP column for the cluster's network displays the master node IP.

## **Get the IP of the master node via Symp CLI**

list all clusters

		# symp -k mapreduce cluster list -f json -c name -c id

		[
		  {
		    "id": "05b6d236-fa81-42f6-b82a-512e2c4270d6",
		    "name": "my_cluster"
		  }

pass in the ID of the cluster you want and list that cluster's instances
the list of instances includes the IP of the master node

		 # symp -k mapreduce cluster instances 05b6d236-fa81-42f6-b82a-512e2c4270d6 -f json -c instance_role -c instance_ip

		[
		  {
		    "instance_role": "core",
		    "instance_ip": "10.47.214.6"
		  },
		  {
		    "instance_role": "master",
		    "instance_ip": "10.47.214.4"
		  },
		  {
		    "instance_role": "core",
		    "instance_ip": "10.47.214.8"
		  }

## SSH into the master node and run a job

When you  [created the cluster](https://www.stratoscale.com/knowledge/create-a-mapreduce-cluster), you specified a key pair to use with the cluster. Pass in this key pair's private key to  `ssh`into the master node:

		$ ssh -i mykey.pem centos@<IP_of_master_node>

Run your MapReduce job on the master node.

If you want to view a website inside the resource manager (located on the master node), you can set up a tunnel like this. This example is for a web service running on port 8888 on the master node.

		$ ssh -i mykey.pem -N -L 8088:<IP_of_master_node>:8088 centos@<IP_of_master_node>

Then connect to  http://localhost:8088  in your browser.

Note that this is just an example -- the exact syntax you need to use depends on what website you want to access and where you are accessing it from.

# Symphony-supported AWS – EMR APIs and Parameters

Below is a list of the AWS - EMR APIs that Symphony supports, together with their supported Required and Optional request parameters.

Click on the API name to access the complete AWS documentation for that action.

<table class="wrapped confluenceTable" style="font-size: 14.0px;"><colgroup><col><col><col></colgroup><tbody><tr><th class="confluenceTh">Name</th><th class="confluenceTh">Required Parameters</th><th class="confluenceTh">Optional Parameters</th></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/emr/latest/APIReference/API_DescribeCluster.html" rel="nofollow">DescribeCluster</a></td><td class="confluenceTd"><ul><li>ClusterId</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/emr/latest/APIReference/API_ListBootstrapActions.html" rel="nofollow">ListBootstrapActions</a></td><td class="confluenceTd"><ul><li>ClusterId</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/emr/latest/APIReference/API_ListClusters.html" rel="nofollow">ListClusters</a></td><td class="confluenceTd"></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/emr/latest/APIReference/API_ListInstanceGroups.html" rel="nofollow">ListInstanceGroups</a></td><td class="confluenceTd"><ul><li>ClusterId</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/emr/latest/APIReference/API_ListInstances.html" rel="nofollow">ListInstances</a></td><td class="confluenceTd"><ul><li>ClusterId</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/emr/latest/APIReference/API_ModifyInstanceGroups.html" rel="nofollow">ModifyInstanceGroups</a></td><td class="confluenceTd"><ul><li>ClusterId</li><li>InstanceGroups</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/emr/latest/APIReference/API_RunJobFlow.html" rel="nofollow">RunJobFlow</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>Name</li><li>Applications</li><li>LogUri</li><li>Instances</li><li>Ec2SubnetId</li><li>Ec2SubnetIds</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/emr/latest/APIReference/API_TerminateJobFlows.html" rel="nofollow">TerminateJobFlows</a></td><td class="confluenceTd"><ul><li>JobFlowIds</li></ul></td><td class="confluenceTd"></td></tr></tbody></table>