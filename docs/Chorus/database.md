# Database

## DBaaS Overview

Symphony Database as a Service allows you to provision a variety of relational and non-relational databases with the click of a button. This is an RDS-compatible solution, you can also use AWS compatible API's to work with this service.

**To set up and use the database service**:

1. First, an admin user must  [enable the database service and enable one or more engines](https://www.stratoscale.com/knowledge/manage-the-database-service).

2. Then, end users can  [create and manipulate database instances](https://www.stratoscale.com/knowledge/use-the-database-service).

# Enabling the Database Service

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.  

**Overview**

The Symphony database service lets you provision and manage the following database instances:

-   MySQL 5.5, 5.6, and 5.7
-   PostgreSQL 9.6 and 11
-   MariaDB 10.1
- MongoDB
- Redis

Functionality is exposed in the GUI under Database. In the CLI, the functionality is in the  `symp dbs`  commands.

**Required administrator tasks**

Before a user can create and access database instances, an admin user must enable the Database service and enable one or more Database engines.

**To enable the Database service**:

1. Click  **Menu**  >  **Region Management**  >  **Settings**  >  **Services & Support**.

2. Under  **Manage Cluster Services**, click the  **Database**  button to toggle from OFF to ON.

**To enable a Database engine**:

1. Click  **Menu**  >  **Database**  >  **Engines**  > select an engine.

2. Click the selected engine's  **Enabled**  button to toggle from OFF to ON.

# Using the Database Service

# Creating a Database Instance using the GUI

**Prerequisites**

Here are the prerequisites for setting up a database instance:

-   One Internal Network.
-   If you want access to the database from outside the organization, you also need an edge network attached to a router.
-   An administrator must also  [enable the database service  and one or more engines](https://www.stratoscale.com/knowledge/manage-the-database-service)  in your Symphony environment, before you can create an instance.


1. From the UI, Click  **Menu**  >  **Database > Instances > Create**.

2. Fill out the following panels in the Create Database Instance wizard and click  **Finish**  when done:

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><td class="highlight-blue confluenceTd" style="text-align: center;" colspan="2" data-highlight-colour="blue"><strong>General</strong></td></tr><tr><td class="confluenceTd"><strong>Instance Name</strong></td><td class="confluenceTd">Name you want to give the instance</td></tr><tr><td class="confluenceTd"><strong>Description</strong></td><td class="confluenceTd">Optional description.</td></tr><tr><td class="confluenceTd"><strong>Engine Version</strong></td><td class="confluenceTd">The engine version you want to base this instance on. An engine version includes an image for a particular database version, for example MySQL 5.6.</td></tr><tr><td class="confluenceTd"><strong>Parameter Group</strong></td><td class="confluenceTd"><p>Parameter group you want to use for this instance.</p><p>Parameter groups set values for various database parameters. Each engine comes with a default parameter group. These default parameter groups have names that start with default-*, for example default-mysql.5.6.</p><p>You cannot modify a default parameter group, but you can <a href="https://www.stratoscale.com/knowledge/editing-a-parameter-group">copy it and then modify the copy</a>.</p></td></tr><tr><td class="confluenceTd" colspan="1"><strong>Instance Type</strong></td><td class="confluenceTd" colspan="1">An instance type specifies the CPUs, RAM, and boot disk size to use for the instance. Select an instance type from the drop down menu.</td></tr><tr><td class="confluenceTd" colspan="1"><strong>Data Volume</strong></td><td class="confluenceTd" colspan="1">Specify the size of the instance's data disk, in GB.</td></tr><tr><td class="confluenceTd"><strong>Storage Pool</strong></td><td class="confluenceTd">The storage pool where the database instance is stored.</td></tr><tr><td class="highlight-blue confluenceTd" style="text-align: center;" colspan="2" data-highlight-colour="blue"><strong>Network</strong></td></tr><tr><td class="confluenceTd"><strong>Network</strong></td><td class="confluenceTd">Select the internal network to use with the instance.</td></tr><tr><td class="confluenceTd" colspan="1"><strong>Edge Network</strong></td><td class="confluenceTd" colspan="1">Optional. If you want to be able to access this instance from an external network, specify the edge network you want to use. The system then assigns a floating IP from that edge network to the newly created database instance.</td></tr><tr><td class="confluenceTd" colspan="1"><strong>Database Port</strong></td><td class="confluenceTd" colspan="1">Optional. If you want to specify a user-provided database port (rather than a default database port from the guest package), specify the user-provided port number here.</td></tr><tr><td class="highlight-blue confluenceTd" style="text-align: center;" colspan="2" data-highlight-colour="blue"><strong>Backup</strong></td></tr><tr><td class="confluenceTd" colspan="1"><strong>Automatic Backup</strong></td><td class="confluenceTd" colspan="1">By default, the system enables automatic backup when you create an instance. With automatic backup enabled, the system takes a daily snapshot of the instance following the values you set for start time, window duration, and retention. The snapshot(s) appear in the snapshot panel, and you can use them to restore the instance if necessary.</td></tr><tr><td class="confluenceTd" colspan="1"><strong>Start Time</strong></td><td class="confluenceTd" colspan="1">The time of day that you want the backup to start.</td></tr><tr><td class="confluenceTd" colspan="1"><strong>Window Duration</strong></td><td class="confluenceTd" colspan="1"><p>How long after the start time the backup is allowed to start.</p><p>For example, if you set <strong>Start Time</strong> to 10 AM and <strong>Window Duration</strong> to 1 hour, the backup can start any time between 10 AM and 11 AM.</p></td></tr><tr><td class="confluenceTd" colspan="1"><strong>Retention</strong></td><td class="confluenceTd" colspan="1">How long to keep each backup snapshot.</td></tr><tr><td class="confluenceTd" colspan="1"><strong>No Backup</strong></td><td class="confluenceTd" colspan="1">To turn off automatic backup, click <strong>No Backup</strong>.</td></tr><tr><td class="highlight-blue confluenceTd" style="text-align: center;" colspan="2" data-highlight-colour="blue"><strong>Credentials</strong></td></tr><tr><td class="confluenceTd" style="text-align: center;" colspan="2"><em>Instance mode: Stand alone</em></td></tr><tr><td class="confluenceTd"><strong>Database Name</strong></td><td class="confluenceTd">Name for the first database on this instance. If you want to create additional databases after instance creation, you can do so using the database client.</td></tr><tr><td class="confluenceTd" colspan="1"><strong>Master User Name</strong></td><td class="confluenceTd" colspan="1">Name of the master user. You can create subsequent users using the database client.</td></tr><tr><td class="confluenceTd" colspan="1"><strong>Master User Password</strong></td><td class="confluenceTd" colspan="1">Password for the master user.</td></tr><tr><td class="confluenceTd" style="text-align: center;" colspan="2"><p><em>Instance mode: Remote replication</em></p><p>Here is <a href="https://www.stratoscale.com/knowledge/database/set-up-and-use-the-database-service/use-the-database-service/using-database-replication/remote-database-replication/">additional information</a> about about remote replication and how to set the following remote replication parameters.</p></td></tr><tr><td class="confluenceTd" colspan="1"><strong>Master Hostname</strong></td><td class="confluenceTd" colspan="1">Hostname of the master instance for this remote replica.</td></tr><tr><td class="confluenceTd" colspan="1"><strong>Master Port</strong></td><td class="confluenceTd" colspan="1">The port the master host is using.</td></tr><tr><td class="confluenceTd" colspan="1"><strong>Master User Name</strong></td><td class="confluenceTd" colspan="1">The master instance's user name.</td></tr><tr><td class="confluenceTd" colspan="1"><strong>Master Password</strong></td><td class="confluenceTd" colspan="1">The master instance's password.</td></tr></tbody></table>

The new database instance appears in the database instances view (**Menu** > **Database > Instances**).

# Creating a Database Instance using the Symp CLI

Here is an example of how to create a database instance using the CLI:

		$ dbs instance create engine_version_id=1 name=myNewInstance
		  storage_pool_id=2 network_id=3 db_name=myDB master_user_name=user
		  master_user_password=password --port=3306 --external-network-id=4

# Editing a Parameter Group

Parameter groups set values for various database parameters. Each engine version comes with a default parameter group. These default parameter groups have names that start with default-*, for example default-mysql.5.6.

You cannot modify the default parameter groups, but you can copy a default group and then modify the copy. (You can also copy an existing copy.)

**To copy and then modify a parameter group**:

1. Click **Menu > Database > Parameter Groups**.

2. Click the parameter group you want to copy. The details page appears.

3. Click  **Copy**. This displays the Copy Parameter Group window.

4. Fill a name and description for the parameter group, then click  **OK**. Click  **Parameter Groups**  to view the new copy in the list of parameter groups.

4. Click the  **name of the copy**  >  **Edit**. This displays the parameters and their values.

6. Click the  **Value**  column for the parameter you want to change. An editing box appears.  **Type in the new value**  and press  **Enter**.

The system saves the new value. Repeat for any other parameter values you want to change.

# Modifying a Database Instance

**To modify a database instance**:

1. Click  **Menu > Database > Instances**  > name of instance you want to modify >  **Modify**.

The Modify RDS Instance window appears**.**

2. Modify some or all of the following values, then click  **OK**:

-   Instance Name
-   Description

# Attaching a Parameter Group to a Database Instance

**To attach a parameter group to an existing database instance**:

1. Click  **Menu > Database > Instances**  > name of instance you want to modify >  **More** >  **Attach Parameters.**

The Attach Parameter Group window appears.

4. Select the parameter group you want to attach and click  **OK**:

# Resizing a Database Instance

**To resize a database instance**:

1. Click  **Menu > Database > Instances**  > name of instance you want to resize >  **Resize**.

The Resize Instance window appears. Choose from the following values and click  **OK**:

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><td class="confluenceTd"><strong>Instance</strong> <strong>Type</strong></td><td class="confluenceTd">Select an instance type from the drop down menu. Instance types control VCPUs, RAM, and boot disk values for the database instance. To see the values associated with each instance type in the drop down menu, click <strong>Compute</strong> &gt; <strong>Instance Types</strong>.</td></tr><tr><td class="confluenceTd"><strong>Allocated Storage</strong></td><td class="confluenceTd">Select a value for the data storage that the database instance will use, in GB.</td></tr></tbody></table>

# Creating a Snapshot of a Database Instance

o create a snapshot of a database Instance:

1. Click  **Menu > Database > Instances**  > name of instance you want to snapshot >  **Snapshot**.

The Create window appears**.**

2. Modify some or all of the following values, then click  **OK**:

-   Name. You can either accept the default name (which has the format <instance_name>-<timestamp>), or you can select a different name.
-   Description

# Restoring a Database Instance

If you have  [created a snapshot of a database instance](https://www.stratoscale.com/knowledge/creating-a-snapshot-of-a-database-instance), and the database instance subsequently fails, you can restore the instance based on the snapshot.

To restore a database instance:

1. Click  **Menu**  >  **Database**  >  **Snapshots**  > select snapshot >  **Restore**.

The Restore Database Instance window appears.

2. Fill in the following fields and click  **Finish**.

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><td class="highlight-blue confluenceTd" colspan="2" data-highlight-colour="blue" style="text-align: center;"><strong>General</strong></td></tr><tr><td class="confluenceTd"><strong>Instance Name</strong></td><td class="confluenceTd">Name you want to give the instance</td></tr><tr><td class="confluenceTd"><strong>Description</strong></td><td class="confluenceTd">Optional description.</td></tr><tr><td class="confluenceTd"><strong>Engine Version</strong></td><td class="confluenceTd">The engine version you want to base this instance on. An engine version includes an image for a particular database version, for example MySQL 5.6.</td></tr><tr><td class="confluenceTd"><strong>Parameter Group</strong></td><td class="confluenceTd"><p>Parameter group you want to use for this instance.</p><p>Parameter groups set values for various database parameters. Each engine comes with a default parameter group. These default parameter groups have names that start with default-*, for example default-mysql.5.6.</p><p>You cannot modify a default parameter group, but you can <a href="https://www.stratoscale.com/knowledge/editing-a-parameter-group">copy it and then modify the copy</a>.</p></td></tr><tr><td colspan="1" class="confluenceTd"><strong>Instance Type</strong></td><td colspan="1" class="confluenceTd">An instance type specifies the CPUs, RAM, and boot disk size to use for the instance. Select an instance type from the drop down menu.</td></tr><tr><td colspan="1" class="confluenceTd"><strong>Data Volume</strong></td><td colspan="1" class="confluenceTd">Specify the size of the instance's data disk, in GB.</td></tr><tr><td class="confluenceTd"><strong>Storage Pool</strong></td><td class="confluenceTd">The storage pool where the database instance is stored.</td></tr><tr><td class="highlight-blue confluenceTd" colspan="2" data-highlight-colour="blue" style="text-align: center;"><strong>Network</strong></td></tr><tr><td class="confluenceTd"><strong>Network</strong></td><td class="confluenceTd">Select the internal network to use with the instance.</td></tr><tr><td colspan="1" class="confluenceTd"><strong>Edge Network</strong></td><td colspan="1" class="confluenceTd">Optional. If you want to be able to access this instance from an external network, specify the edge network you want to use. The system then assigns a floating IP from that edge network to the newly created database instance.</td></tr><tr><td colspan="1" class="confluenceTd"><strong>Database Port</strong></td><td colspan="1" class="confluenceTd">Optional. If you want to specify a user-provided database port (rather than a default database port from the guest package), specify the user-provided port number here.</td></tr><tr><td class="highlight-blue confluenceTd" colspan="2" data-highlight-colour="blue" style="text-align: center;"><strong>Credentials</strong></td></tr><tr><td class="confluenceTd"><strong>Database Name</strong></td><td class="confluenceTd">Name for the first database on this instance. If you want to create additional databases after instance creation, you can do so using the database client.</td></tr><tr><td colspan="1" class="confluenceTd"><strong>Master User Name</strong></td><td colspan="1" class="confluenceTd">Name of the master user. You can create subsequent users using the database client.</td></tr><tr><td colspan="1" class="confluenceTd"><strong>Master User Password</strong></td><td colspan="1" class="confluenceTd">Password for the master user.</td></tr></tbody></table>

# Removing a Database Instance

**To remove a database Instance**:

1. Click  **Menu > Database**  **>**  **Instances**  > name of instance you want to remove >  **Remove**.

A warning window appears**.**

2. To remove the instance, click  **OK**.


# Symphony-supported AWS – RDS APIs and Parameters

**Authentication note**

Symphony supports AWS Signature Version 4.

Below is a list of the AWS - RDS APIs that Symphony supports, together with their supported Required and Optional request parameters.

Click on the API name to access the complete AWS documentation for that action.

<table class="wrapped confluenceTable"><colgroup><col><col><col><col></colgroup><tbody><tr><th class="confluenceTh">Name</th><th class="confluenceTh">Required Parameters</th><th class="confluenceTh">Optional Parameters</th><th colspan="1" style="text-align: center;" class="confluenceTh">Introduced</th></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_CopyDBParameterGroup.html" rel="nofollow">CopyDBParameterGroup</a></td><td class="confluenceTd"><ul><li>SourceDBParameterGroupIdentifier</li><li>TargetDBParameterGroupDescription</li><li>TargetDBParameterGroupIdentifier</li></ul></td><td class="confluenceTd"></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_CreateDBInstance.html" rel="nofollow">CreateDBInstance</a></td><td class="confluenceTd"><ul><li>DBInstanceClass</li><li>DBInstanceIdentifier</li><li>Engine</li></ul></td><td class="confluenceTd"><ul><li>MasterUsername</li><li>MasterUserPassword</li><li>DBName</li><li>AllocatedStorage</li><li>DBParameterGroupName</li><li>DBSubnetGroupName</li><li>EngineVersion</li><li><span style="color: rgb(0,0,255);"><strong>PubliclyAccessible</strong></span></li></ul></td><td colspan="1" class="confluenceTd"><p><strong style="color: rgb(0,0,255);"><br></strong></p><p><strong style="color: rgb(0,0,255);"><br></strong></p><p><strong style="color: rgb(0,0,255);"><br></strong></p><p><strong style="color: rgb(0,0,255);">Symphony v.4.2.7</strong></p></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_CreateDBParameterGroup.html" rel="nofollow">CreateDBParameterGroup</a></td><td class="confluenceTd"><ul><li>DBParameterGroupName</li><li>DBParameterGroupFamily</li><li>Description</li></ul></td><td class="confluenceTd"></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_CreateDBSnapshot.html" rel="nofollow">CreateDBSnapshot</a></td><td class="confluenceTd"><ul><li>DBInstanceIdentifier</li><li>DBSnapshotIdentifier</li></ul></td><td class="confluenceTd"></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_CreateDBSubnetGroup.html" rel="nofollow">CreateDBSubnetGroup</a></td><td class="confluenceTd"><ul><li>DBSubnetGroupDescription</li><li>DBSubnetGroupName</li><li>SubnetIds</li></ul></td><td class="confluenceTd"></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DeleteDBInstance.html" rel="nofollow">DeleteDBInstance</a></td><td class="confluenceTd"><ul><li>DBInstanceIdentifier</li></ul></td><td class="confluenceTd"></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DeleteDBParameterGroup.html" rel="nofollow">DeleteDBParameterGroup</a></td><td class="confluenceTd"><ul><li>DBParameterGroupName</li></ul></td><td class="confluenceTd"></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DeleteDBSnapshot.html" rel="nofollow">DeleteDBSnapshot</a></td><td class="confluenceTd"><ul><li>DBSnapshotIdentifier</li></ul></td><td class="confluenceTd"></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DeleteDBSubnetGroup.html" rel="nofollow">DeleteDBSubnetGroup</a></td><td class="confluenceTd"><ul><li>DBSubnetGroupName</li></ul></td><td class="confluenceTd"></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DescribeDBEngineVersions.html" rel="nofollow">DescribeDBEngineVersions</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>Engine</li><li>EngineVersion</li><li>DBParameterGroupFamily</li></ul></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DescribeDBInstances.html" rel="nofollow">DescribeDBInstances</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>DBInstanceIdentifier</li></ul></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DescribeDBParameterGroups.html" rel="nofollow">DescribeDBParameterGroups</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>DBParameterGroupName</li></ul></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DescribeDBParameters.html" rel="nofollow">DescribeDBParameters</a></td><td class="confluenceTd"><ul><li>DBParameterGroupName</li></ul></td><td class="confluenceTd"></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DescribeDBSnapshots.html" rel="nofollow">DescribeDBSnapshots</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>DBInstanceIdentifier</li><li>DBSnapshotIdentifier</li></ul></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DescribeDBSubnetGroups.html" rel="nofollow">DescribeDBSubnetGroups</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>DBSubnetGroupName</li></ul></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DescribeEngineDefaultParameters.html" rel="nofollow">DescribeEngineDefaultParameters</a></td><td class="confluenceTd"><ul><li>DBParameterGroupFamily</li></ul></td><td class="confluenceTd"></td><td colspan="1" class="confluenceTd"></td></tr><tr><td colspan="1" class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_ListTagsForResource.html" rel="nofollow">ListTagsForResource</a></td><td colspan="1" class="confluenceTd"><ul><li>ResourceName</li></ul></td><td colspan="1" class="confluenceTd"></td><td colspan="1" class="confluenceTd"><span style="color: rgb(0,0,255);"><strong>Symphony v.4.2.7</strong></span></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_ModifyDBInstance.html" rel="nofollow">ModifyDBInstance</a></td><td class="confluenceTd"><ul><li>DBInstanceIdentifier</li></ul></td><td class="confluenceTd"><ul><li>AllocatedStorage</li><li>DBInstanceClass</li><li>LicenseModel</li><li>MasterUserPassword</li><li>NewDBInstanceIdentifier</li></ul></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_ModifyDBParameterGroup.html" rel="nofollow">ModifyDBParameterGroup</a></td><td class="confluenceTd"><ul><li>DBParameterGroupName</li><li>Parameters</li></ul></td><td class="confluenceTd"></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_ModifyDBSubnetGroup.html" rel="nofollow">ModifyDBSubnetGroup</a></td><td class="confluenceTd"><ul><li>DBSubnetGroupName</li><li>SubnetIds</li></ul></td><td class="confluenceTd"><ul><li>DBSubnetGroupDescription</li></ul></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_RebootDBInstance.html" rel="nofollow">RebootDBInstance</a></td><td class="confluenceTd"><ul><li>DBInstanceIdentifier</li></ul></td><td class="confluenceTd"></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_ResetDBParameterGroup.html" rel="nofollow">ResetDBParameterGroup</a></td><td class="confluenceTd"><ul><li>DBParameterGroupName</li></ul></td><td class="confluenceTd"><ul><li>Parameters</li><li>ResetAllParameters</li></ul></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_RestoreDBInstanceFromDBSnapshot.html" rel="nofollow">RestoreDBInstanceFromDBSnapshot</a></td><td class="confluenceTd"><ul><li>DBInstanceIdentifier</li><li>DBSnapshotIdentifier</li></ul></td><td class="confluenceTd"><ul><li>DBSubnetGroupName</li></ul></td><td colspan="1" class="confluenceTd"></td></tr></tbody></table>
