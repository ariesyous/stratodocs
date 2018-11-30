# Load balancing

## LBaaS Overview

Symphony LBaaS is a managed load balancer service that balances the load between two or more instances hosted on a Symphony region. It can provide load balancing via TCP, HTTP, or HTTPS - acting in either an ALB or an NLB type configuration. Combined with an Autoscaling Group it can provide a methodology to rapidly expand or shrink your compute cluster based upon incoming load and allows you to maintain uptime for your services.

# Manage the Load Balancing Service

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.

When you create a load balancer, you define a target group of instances that will share the work of processing requests from an application. The application then directs its requests to the load balancer, and the load balancer distributes the work among the instances in the load balancer's target group.

Functionality is exposed in the GUI under  **Menu, Load Balancing**. In the CLI, the functionality is in the  `symp lbaas`  commands.

**Required administrator tasks  
**

Before a user can create and use a load balancer, an administrator must enable and initialize the load balancing service.  If you are on a dark site, you must initialize the load balancer following the dark site engine instructions. 

**To enable the load balancing service:**

1. Click  **Region Management**  >  **Settings**  >  **Services**.

2. Click the  **Load Balancing**  button to toggle from OFF to ON.

**To initialize the load balancing service**

1. Click  **Menu > Load Balancing > Load Balancers**.

2. Note the initialize message box and click  **Initialize**. If you do not see this message, the load balancing service has already been initialized.

# Use the Load Balancing Service

# Load Balancing Usage Overview

**Working with load balancers**: Start by creating a [target group of instances](https://www.stratoscale.com/knowledge/create-a-target-group). These are the instances that will share the processing work. Once you have a target group, you can [create a load balancer](https://www.stratoscale.com/knowledge/create-a-load-balancer) that uses the target group.

# Create a Target Group

A target group is a group of instances to which a load balancer directs application traffic. The instances in this group collectively do the processing work that the application requires.

**To create a target group**:

1. Click  **Menu**  >  **Load Balancing**  >  **Target Groups**  >  **Create**. The Create Target Group window appears.

2. In the Create Target Group window, specify these values, then click  **OK**:

Click Add to add an additional target.

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><th class="confluenceTh">Field</th><th class="confluenceTh">Description</th></tr><tr><td class="highlight-blue confluenceTd" colspan="2" data-highlight-colour="blue" style="text-align: center;"><strong>Details</strong></td></tr><tr><td class="confluenceTd"><strong>Name</strong></td><td class="confluenceTd">Name of the target group you are creating.</td></tr><tr><td colspan="1" class="confluenceTd"><strong>Protocol</strong></td><td colspan="1" class="confluenceTd">The protocol that the load balancer uses to access the target group. Choose either TCP or HTTP.</td></tr><tr><td colspan="1" class="confluenceTd"><strong>Port</strong></td><td colspan="1" class="confluenceTd">The port on the target group that the load balancer should use to connect to the target group.</td></tr><tr><td class="highlight-grey confluenceTd" colspan="2" data-highlight-colour="grey" style="text-align: center;"><strong>Details - Health Check</strong></td></tr><tr><td colspan="1" class="confluenceTd"><strong>Path</strong></td><td colspan="1" class="confluenceTd"><p>HTTP only. The ping path the load balancer uses to do a health check on the instances in the target group.</p><p>This is the to the application that will be using the load balancer – for example, the path to your website's home page in the format:</p><p>http://www.example.com/myApp</p></td></tr><tr><td colspan="1" class="confluenceTd"><strong>Interval</strong></td><td colspan="1" class="confluenceTd"><p>The interval, in seconds, between health checks of an individual instance.</p><p>Min: 5</p><p>Max: 300</p></td></tr><tr><td colspan="1" class="confluenceTd"><strong>Timeout</strong></td><td colspan="1" class="confluenceTd"><p>The amount of time, in seconds, during which no response means a failed health check.</p><p>This value must be less than the Interval value.</p><p>Min: 2</p><p>Max: 60</p></td></tr><tr><td colspan="1" class="confluenceTd"><strong>Healthy threshold</strong></td><td colspan="1" class="confluenceTd"><p>The number of consecutive health checks successes required before moving the instance to the Healthy state.</p><p>Min: 2</p><p>Max: 10</p></td></tr><tr><td colspan="1" class="confluenceTd"><strong>Unhealthy threshold</strong></td><td colspan="1" class="confluenceTd"><p>The number of consecutive health check failures required before moving the instance to the Unhealthy state.</p><p>Min: 2</p><p>Max: 10</p></td></tr><tr><td class="highlight-grey confluenceTd" colspan="2" data-highlight-colour="grey" style="text-align: center;"><strong>Details - Session</strong></td></tr><tr><td colspan="1" class="confluenceTd"><strong>Sticky session</strong></td><td colspan="1" class="confluenceTd">By default, a load balancer routes each request independently to the registered target group instance with the smallest load. However, you can use the sticky session feature to bind a user's session to a specific instance. This ensures that all requests from the user during the session are sent to the same instance.</td></tr><tr><td colspan="1" class="confluenceTd"><strong>Duration</strong></td><td colspan="1" class="confluenceTd">How long (in seconds) the load balancer should consistently route the user's request to the same instance.</td></tr><tr><td class="highlight-blue confluenceTd" colspan="2" data-highlight-colour="blue" style="text-align: center;"><strong>Targets</strong></td></tr><tr><td colspan="1" class="confluenceTd"><strong>Add</strong></td><td colspan="1" class="confluenceTd">Click <strong>Add</strong> to add an additional target. For each target you add, specify target type, VM name or IP, and port.</td></tr><tr><td class="confluenceTd"><p><strong>Target type (left hand drop down menu)&nbsp; </strong></p></td><td class="confluenceTd"><p>Target type can be:</p><p><strong>Instance</strong></p><p><strong>IP</strong></p><p>You can specify the instances that you want in the target group by either VM name or IP. These instances can be compute instances or database instances.</p><p>You can mix and match target types, meaning that you can create a target group where some instances are of type <strong>Instance</strong> and some are of type <strong>IP</strong>.</p></td></tr><tr><td colspan="1" class="confluenceTd"><strong>VM name or IP (middle drop down menu)</strong></td><td colspan="1" class="confluenceTd"><div class="content-wrapper"><p><strong>Instance type = Instance</strong></p><p>Select a target VM from the instance names that appear in the drop down menu.</p><p><strong>Instance type = IP</strong></p><p>Specify an IP that is in a valid range for your Symphony region.</p><div class="confluence-information-macro confluence-information-macro-note conf-macro output-block" data-hasbody="true" data-macro-name="note"><p class="title">Must be routable from the load balancer's security group</p><p><span class="aui-icon aui-icon-small aui-iconfont-warning confluence-information-macro-icon"> </span></p><div class="confluence-information-macro-body"><p>This IP must routable from the network/security group combination you associate with the load balancer.</p></div></div></div></td></tr><tr><td colspan="1" class="confluenceTd"><strong>Port</strong></td><td colspan="1" class="confluenceTd">Specify which port on the instance that the load balancer should communicate with.</td></tr></tbody></table>

# Create a Load Balancer

**To create a load balancer**:

1. Click  **Menu**  >  **Load Balancing**  >  **Load Balancer**  >  **Create**. The Create Load Balancer window appears.

2. In the Create Load Balancer window, specify these values, then click  **Finish**:

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><td class="highlight-blue confluenceTd" colspan="2" data-highlight-colour="blue" style="text-align: center;"><strong>Details</strong></td></tr><tr><td class="confluenceTd"><strong>Name</strong></td><td class="confluenceTd">Name of the load balancer you are creating.</td></tr><tr><td class="confluenceTd"><strong>Network</strong></td><td class="confluenceTd">Select the internal network to use with the instance.</td></tr><tr><td class="confluenceTd"><strong>Floating IP</strong></td><td class="confluenceTd">Optional. Select the floating IP to use with the instance.</td></tr><tr><td class="confluenceTd"><strong>Security Groups</strong></td><td class="confluenceTd">Optional. Select the <a href="https://www.stratoscale.com/knowledge/creating-a-security-group"><span class="confluence-link">security groups</span></a> to use with the instance.</td></tr><tr><td colspan="1" class="confluenceTd"><strong>Instance Type</strong></td><td colspan="1" class="confluenceTd">An instance type specifies the CPUs, RAM, and boot disk size to use for the instance. Select an instance type from the drop down menu.</td></tr><tr><td colspan="1" class="confluenceTd"><strong>High Availability</strong></td><td colspan="1" class="confluenceTd">Check to enable high availability for the load balancer. Two instances of a load balancer provide the necessary redundancy.</td></tr><tr><td class="highlight-blue confluenceTd" colspan="2" data-highlight-colour="blue" style="text-align: center;"><strong>Listeners</strong></td></tr><tr><td class="confluenceTd"><strong>Listeners</strong></td><td class="confluenceTd"><p><strong>Target group</strong>: A target group is a group of instances to which a load balancer directs application traffic. The instances in this group collectively do the processing work that the application requires.</p><p>Select a target group from the drop down menu. (If you need to <a href="https://www.stratoscale.com/knowledge/create-a-target-group">create a target group</a> on the fly here, click <strong>Create Target Group</strong>.)</p><p><strong>Protocol</strong>: Select either HTTP, HTTPS, or TCP.</p><p>If you select <strong>HTTPS</strong>, you also need to specify the SSL certificate that you want to use to enable secure communication between the outside consumer and the load balancer (SSL termination). If you have not already <a href="https://www.stratoscale.com/knowledge/importing-a-certificate">imported the SSL certificate</a>, click <strong>Menu</strong> &gt; <strong>Account Management</strong> &gt; <strong>Certificates</strong> &gt; <strong>Import</strong>.</p><p><strong>Port</strong>: specify the port on the load balancer that applications should send their requests to.</p></td></tr></tbody></table>

# Use Case: Load Balancers and Database Replication

By combining Symphony database replication with load balancing, you can improve both an application's performance (load balancing) and availability (replication).

Here is a sample scenario.

## Set up database replication

Start by  **[creating a master database instance](https://www.stratoscale.com/knowledge/creating-a-database-instance)**  (Menu > Database > Instances > Create). Once the master is created, in the details view, note **the IP of the master**.

**Set up replication for that instance**  (Menu > Database > Instances > select an instance > Replica). Once the replica is created, in the details view,  **note the IP of the replica**.

**Test replication**  by starting a client database application (whichever one you like) and connecting to the master. Add a row to a table, then establish a second connection to the replica and verify that the new row is also there in the replica.

You now have verified  **data availability via replication**.

## Set up a load balancer

Now  **create a load balancer**  to improve performance.

First step:

Start by  [creating a target group](https://www.stratoscale.com/knowledge/create-a-target-group). A target group is a group of instances to which a load balancer directs application traffic – in this case, the target group will contain the master database instance and its replica.

You can create a target group by clicking Menu > Load Balancing > Target Groups > Create.

In the  **Targets**  field,  **select the 2 database instances that are replicating**  as described above. Include the ports to use to communicate with them.

Second step:

Now  [create a load balancer](https://www.stratoscale.com/knowledge/create-a-load-balancer)  that uses the target group you just created. In the details view,  **note the IP of the load balancer**.

## Have your application connect to the load balancer

Return to your client database application and connect to the load balancer. Examine the table that you created in the master database instance and note that all the rows you observed before are present when your application connects to the load balancer.

Moving forward, your application can continue to access the load balancer for data needs and achieve both availability and performance, based on your use of Symphony database replication and load balancing.

# ELBv2 API Version Support

Symphony supports ELBv2, the 2015-12-01 API for Application Load Balancers and Network Load Balancers. It does not support the 2012-06-01 API for Classic Load Balancers.

# Symphony-supported AWS – ELB APIs and Parameters

Below is a list of the AWS - ELB APIs that Symphony supports, together with their supported Required and Optional request parameters.

Click on the API name to access the complete AWS documentation for that action.

**Authentication note**

Symphony supports AWS Signature Version 4.

<table class="wrapped confluenceTable"><colgroup><col><col><col></colgroup><tbody><tr><th class="confluenceTh">Name</th><th class="confluenceTh">Required Parameters</th><th class="confluenceTh">Optional Parameters</th></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_CreateListener.html" rel="nofollow">CreateListener</a></td><td class="confluenceTd"><ul><li>DefaultActions</li><li>LoadBalancerArn</li><li>Port</li><li>Protocol</li></ul></td><td class="confluenceTd"><ul><li>Certificates</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_CreateLoadBalancer.html" rel="nofollow">CreateLoadBalancer</a></td><td class="confluenceTd"><ul><li>Name</li><li>Subnets</li></ul></td><td class="confluenceTd"><ul><li>IpAddressType</li><li>Scheme</li><li>SecurityGroups</li><li>Tags</li><li>Type</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_CreateTargetGroup.html" rel="nofollow">CreateTargetGroup</a></td><td class="confluenceTd"><ul><li>Name</li><li>Protocol</li><li>Port</li><li>VpcId</li></ul></td><td class="confluenceTd"><ul><li>HealthCheckIntervalSeconds</li><li>HealthCheckPath</li><li>HealthCheckPort</li><li>HealthCheckProtocol</li><li>HealthCheckTimeoutSeconds</li><li>HealthyThresholdCount</li><li>UnhealthyThresholdCount</li><li>TargetType</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_DeleteListener.html" rel="nofollow">DeleteListener</a></td><td class="confluenceTd"><ul><li>ListenerArn</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_DeleteLoadBalancer.html" rel="nofollow">DeleteLoadBalancer</a></td><td class="confluenceTd"><ul><li>LoadBalancerArn</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_DeleteTargetGroup.html" rel="nofollow">DeleteTargetGroup</a></td><td class="confluenceTd"><ul><li>TargetGroupArn</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_DeregisterTargets.html" rel="nofollow">DeregisterTargets</a></td><td class="confluenceTd"><ul><li>TargetGroupArn</li><li>Targets</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_DescribeListeners.html" rel="nofollow">DescribeListeners</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>ListenerArns</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_DescribeLoadBalancerAttributes.html" rel="nofollow">DescribeLoadBalancerAttributes</a></td><td class="confluenceTd"><ul><li>LoadBalancerArn</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_DescribeLoadBalancers.html" rel="nofollow">DescribeLoadBalancers</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>LoadBalancerArns</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_DescribeTags.html" rel="nofollow">DescribeTags</a></td><td class="confluenceTd"><ul><li>ResourceArns</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_DescribeTargetGroupAttributes.html" rel="nofollow">DescribeTargetGroupAttributes</a></td><td class="confluenceTd"><ul><li>TargetGroupArn</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_DescribeTargetGroups.html" rel="nofollow">DescribeTargetGroups</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>TargetGroupArns</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_DescribeTargetHealth.html" rel="nofollow">DescribeTargetHealth</a></td><td class="confluenceTd"><ul><li>TargetGroupArn</li></ul></td><td class="confluenceTd"><ul><li>Targets</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_ModifyLoadBalancerAttributes.html" rel="nofollow">ModifyLoadBalancerAttributes</a></td><td class="confluenceTd"><ul><li>LoadBalancerArn</li><li>Attributes</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_ModifyTargetGroup.html" rel="nofollow">ModifyTargetGroup</a></td><td class="confluenceTd"><ul><li>TargetGroupArn</li></ul></td><td class="confluenceTd"><ul><li>HealthCheckIntervalSeconds</li><li>HealthCheckPath</li><li>HealthCheckPort</li><li>HealthCheckProtocol</li><li>HealthCheckTimeoutSeconds</li><li>HealthyThresholdCount</li><li>Matcher</li><li>UnhealthyThresholdCount</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_ModifyTargetGroupAttributes.html" rel="nofollow">ModifyTargetGroupAttributes</a></td><td class="confluenceTd"><ul><li>Attributes</li><li>TargetGroupArn</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_RegisterTargets.html" rel="nofollow">RegisterTargets</a></td><td class="confluenceTd"><ul><li>TargetGroupArn</li><li>Targets</li></ul></td><td class="confluenceTd"></td></tr><tr><td colspan="1" class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_SetIpAddressType.html" rel="nofollow">SetIpAddressType</a></td><td colspan="1" class="confluenceTd"><ul><li>IpAddressType</li></ul></td><td colspan="1" class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_SetSecurityGroups.html" rel="nofollow">SetSecurityGroups</a></td><td class="confluenceTd"><ul><li>LoadBalancerArn</li><li>SecurityGroups</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/elasticloadbalancing/latest/APIReference/API_SetSubnets.html" rel="nofollow">SetSubnets</a></td><td class="confluenceTd"><ul><li>LoadBalancerArn</li><li>Subnets</li></ul></td><td class="confluenceTd"><ul><li>SubnetMappings</li></ul></td></tr></tbody></table>

# AWS CLI elbv2 Examples

Symphony supports the AWS  **elbv2**  API/CLI. It does not support the  **elb**  API/CLI.

Here are some examples:

**List the load balancers**  in your system. Note that the  `LoadBalancerArn`  is a Symphony UUID.

    aws> elbv2 describe-load-balancers
    
    -------------------------------------------------------------------------------------------------------------------------------------
    
    |                                                       DescribeLoadBalancers                                                       |
    
    +-----------------------------------------------------------------------------------------------------------------------------------+
    
    ||                                                          LoadBalancers                                                          ||
    
    |+----------------------+---------------+----------------------------------------+-------------------+-----------+-------+---------+|
    
    ||      CreatedTime     |    DNSName    |            LoadBalancerArn             | LoadBalancerName  |  Scheme   | Type  |  VpcId  ||
    
    |+----------------------+---------------+----------------------------------------+-------------------+-----------+-------+---------+|
    
    ||  2018-10-01T11:05:32Z|  192.168.41.6 |  96ee2383-4a73-4494-bdf1-e879714c772b  |  dougtest         |  internal |  None |  None   ||
    
    |+----------------------+---------------+----------------------------------------+-------------------+-----------+-------+---------+|
    
    |||                                                       AvailabilityZones                                                       |||
    
    ||+-------------------------------------------------------------------------------------------------------------------------------+||
    
    |||                                                           SubnetId                                                            |||
    
    ||+-------------------------------------------------------------------------------------------------------------------------------+||
    
    |||  subnet-6715c727b6f64ab9be2c5c3094e36473                                                                                      |||
    
    ||+-------------------------------------------------------------------------------------------------------------------------------+||
    
    |||                                                        SecurityGroups                                                         |||
    
    ||+-------------------------------------------------------------------------------------------------------------------------------+||
    
    |||  sg-76423026d14f40a48921c3368d85a0b5                                                                                          |||
    
    |||  sg-fb329fe5ba2e40618bcba4aeb84adb0f                                                                                          |||
    
    ||+-------------------------------------------------------------------------------------------------------------------------------+||
    
    |||                                                             State                                                             |||
    
    ||+-------------------------------------------------------+-----------------------------------------------------------------------+||
    
    |||  Code                                                 |  active                                                               |||
    
    ||+-------------------------------------------------------+-----------------------------------------------------------------------+||
    
     
    
    aws> elbv2 describe-load-balancers --load-balancer-arns 96ee2383-4a73-4494-bdf1-e879714c772b
    
    -------------------------------------------------------------------------------------------------------------------------------------
    
    |                                                       DescribeLoadBalancers                                                       |
    
    +-----------------------------------------------------------------------------------------------------------------------------------+
    
    ||                                                          LoadBalancers                                                          ||
    
    |+----------------------+---------------+----------------------------------------+-------------------+-----------+-------+---------+|
    
    ||      CreatedTime     |    DNSName    |            LoadBalancerArn             | LoadBalancerName  |  Scheme   | Type  |  VpcId  ||
    
    |+----------------------+---------------+----------------------------------------+-------------------+-----------+-------+---------+|
    
    ||  2018-10-01T11:05:32Z|  192.168.41.6 |  96ee2383-4a73-4494-bdf1-e879714c772b  |  dougtest         |  internal |  None |  None   ||
    
    |+----------------------+---------------+----------------------------------------+-------------------+-----------+-------+---------+|
    
    |||                                                       AvailabilityZones                                                       |||
    
    ||+-------------------------------------------------------------------------------------------------------------------------------+||
    
    |||                                                           SubnetId                                                            |||
    
    ||+-------------------------------------------------------------------------------------------------------------------------------+||
    
    |||  subnet-6715c727b6f64ab9be2c5c3094e36473                                                                                      |||
    
    ||+-------------------------------------------------------------------------------------------------------------------------------+||
    
    |||                                                        SecurityGroups                                                         |||
    
    ||+-------------------------------------------------------------------------------------------------------------------------------+||
    
    |||  sg-76423026d14f40a48921c3368d85a0b5                                                                                          |||
    
    |||  sg-fb329fe5ba2e40618bcba4aeb84adb0f                                                                                          |||
    
    ||+-------------------------------------------------------------------------------------------------------------------------------+||
    
    |||                                                             State                                                             |||
    
    ||+-------------------------------------------------------+-----------------------------------------------------------------------+||
    
    |||  Code                                                 |  active                                                               |||
    
    ||+-------------------------------------------------------+-----------------------------------------------------------------------+||

**Delete one of the load balancers**  you just listed, passing in the load balancer's LoadBalancerArn:

	aws> elbv2 delete-load-balancer --load-balancer-arn 96ee2383-4a73-4494-bdf1-e879714c772b

Note that **describe-load-balancers** takes `–-load-balancer-arns` which is a comma separated list of UUIDs, and **delete-load-balancer** takes `–-load-balancer-arn` which is a single UUID.

## Boto3 Reference for ELB

	import boto3

	client = boto3.client('elbv2')

<table class="wrapped confluenceTable"><colgroup><col></colgroup><tbody><tr><th class="confluenceTh">Commonly used methods</th></tr><tr><td class="confluenceTd"><a class="external-link" href="http://boto3.readthedocs.io/en/latest/reference/services/elbv2.html#ElasticLoadBalancingv2.Client.create_load_balancer" rel="nofollow">create_load_balancer</a></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://boto3.readthedocs.io/en/latest/reference/services/elbv2.html#ElasticLoadBalancingv2.Client.delete_load_balancer" rel="nofollow">delete_load_balancer</a></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://boto3.readthedocs.io/en/latest/reference/services/elbv2.html#ElasticLoadBalancingv2.Client.describe_load_balancers" rel="nofollow">describe_load_balancers</a></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://boto3.readthedocs.io/en/latest/reference/services/elbv2.html#ElasticLoadBalancingv2.Client.create_listener" rel="nofollow">create_listener</a></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://boto3.readthedocs.io/en/latest/reference/services/elbv2.html#ElasticLoadBalancingv2.Client.delete_listener" rel="nofollow">delete_listener</a></td></tr><tr><td colspan="1" class="confluenceTd"><a class="external-link" href="http://boto3.readthedocs.io/en/latest/reference/services/elbv2.html#ElasticLoadBalancingv2.Client.describe_listeners" rel="nofollow">describe_listeners</a></td></tr><tr><td colspan="1" class="confluenceTd"><a class="external-link" href="http://boto3.readthedocs.io/en/latest/reference/services/elbv2.html#ElasticLoadBalancingv2.Client.create_target_group" rel="nofollow">create_target_group</a></td></tr><tr><td colspan="1" class="confluenceTd"><a class="external-link" href="http://boto3.readthedocs.io/en/latest/reference/services/elbv2.html#ElasticLoadBalancingv2.Client.delete_target_group" rel="nofollow">delete_target_group</a></td></tr><tr><td colspan="1" class="confluenceTd"><a class="external-link" href="http://boto3.readthedocs.io/en/latest/reference/services/elbv2.html#ElasticLoadBalancingv2.Client.describe_target_groups" rel="nofollow">describe_target_groups</a></td></tr></tbody></table>

Other ELB methods are described [here](http://boto3.readthedocs.io/en/latest/reference/services/elbv2.html).
