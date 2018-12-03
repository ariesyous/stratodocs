# VPC in Symphony

The VPC construct in Symphony was designed to provide a user experience that is identical to the AWS VPC. The virtual private cloud provides a routed L3 environment into which the user can deploy instances and managed services.

![](https://www.stratoscale.com/wp-content/uploads/VPC20Construct20in20Symphony_800p.png)  

### Virtual Private Cloud (VPC)

The VPC is a networking resource with a logical router at its core. When you create a VPC you specify a CIDR block. All subnets that you will create in the VPC will be carved out from this CIDR block (without overlap). The router will ensure IP connectivity between all these subnets.

### Subnet

VPC subnets are defined by the following: constraints:

1.  The CIDR block of a subnet may be either identical to the VPC's CIDR block, which is the case when there is a single subnet, or a subset of the VPC's CIDR block, when there are multiple subnets. In the latter case, the CIDR blocks of the subnets cannot overlap.The permitted block size ranges from a /28 netmask to a /16 netmask.
2.  The first four IP addresses and the last IP address in each subnet CIDR block are not available for users, and cannot be assigned to an instance.
3.  The second address of the subnet is reserved for the router.
4.  Every subnet that is created is automatically associated with the main route table of the VPC. You can change the association. A subnet can be associated with only one route table at a time.

### Internet Gateway (IGW)

An internet gateway is a logical entity that connects the VPC router to an external network. It is used as a target in the VPC route tables for Internet-routable traffic.

### Route Tables

Route tables control the IP forwarding of all traffic in the subnets with which they are associated.

1.  A VPC comes with a single built-in, modifiable, main route table.
2.  You can create additional custom route tables for your VPC.
3.  You cannot delete the main route table, but you can replace the main route table with a custom table that you've created. This table becomes the default table with which each new subnet is associated.
4.  Each route in a table specifies a destination CIDR and a target  (local/IGW).
5.  Every route table contains a local route for communication within the VPC over IPv4. You cannot modify or delete this route.

### Elastic IPs (EIPs)

Elastic IPs are used to expose instances and managed services outside of Symphony. An EIP will be used in the network address operation (NAT) of all traffic to/from the virtual network interface with which it is associated.

1.  You first allocate an Elastic IP address for use in a VPC, and then associate it with an elastic network interface (ENI) in your VPC. It can be associated with only one ENI at a time.
2.  An EIP may be attached only to an ENI that is in a VPC with an internet gateway.

### DHCP Options sets

A DHCP options set is a set of network configurations that will be delivered to your instance when its interface acquires an IP address using the DHCP protocol.

1.  DHCP options sets are associated with a project so that you can use them across all of your virtual private clouds (VPC).
2.  The supported options for a DHCP options set are as follows:
    1.  Domain-name-servers - The IP addresses of up to four domain name servers, or SymphonyProvidedDNS. The default DHCP option set specifies SymphonyProvidedDNS.  
        Although the custom DNS server is used, the DHCP-supplied DNS server to the VMs will always be SymphonyProvidedDNS and the custom DNS will be queried indirectly by SymphonyProvidedDNS.
    2.  Domain-name - This value is used to complete unqualified DNS hostnames. This is set by default to 'symphony.local'.
    3.  Ntp-servers - The IP addresses of up to four Network Time Protocol (NTP) servers.
    4.  Netbios-name-servers - The IP addresses of up to four NetBIOS name servers.
    5.  Netbios-node-type - The NetBIOS node type (1, 2, 4, or 8).

### Security Groups

Security groups are applied to the virtual network interfaces to control the inbound and outbound traffic. They are whitelists. Traffic that does not match any rule in the security group will be discarded. Security group rules are realized using stateful session tracking. This means that you must specify a rule only for the direction in which the session is initiated, with the other direction being implied.

1.  A VPC automatically includes a default security group. Each instance that you launch in your VPC is automatically associated with the default security group unless you specified a different security group when you launched the instance.
2.  When you create a security group, you must provide it with a name and a description. The following rules apply:
    1.  Names and descriptions can be up to 255 characters in length.
    2.  For AWS compatibility - names and descriptions are limited to the following characters: a-z, A-Z, 0-9, spaces, and ._-:/()#,@[]+=&;{}!$*.
    3.  A security group name cannot start with sg-.
    4.  A security group name must be unique within the VPC.
3.  For each security group, you include one set of rules that controls the inbound traffic to the instances, and a separate set of rules that controls the outbound traffic from the instances.
4.  The following are the basic components of a security group rule in a VPC:
    1.  For inbound rules only - The source of the traffic and the destination port or port range. The source can be another security group, an IPv4 or IPv6 CIDR block, or a single IPv4 or IPv6 address.
    2.  For outbound rules only - The destination for the traffic and the destination port or port range. The destination can be another security group, an IPv4 or IPv6 CIDR block, or a single IPv4 or IPv6 address.
    3.  Any protocol that has a standard protocol number (click  [here](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml)  for a complete list of Protocol Numbers). If you specify ICMP as the protocol, you can specify any or all of the ICMP types and codes.

### Default VPC

Every VPC-provisioned project has a Default VPC that is automatically created by Symphony.

1.  The Default VPC has 172.31.0.0/16 set as its CIDR block.
2.  It also contains a single subnet with 172.31.0.0/20 as its CIDR.
3.  The VPC has an Internet Gateway that connects it to the external network that was selected by the project.
4.  The route table of the subnet has a local route for the CIDR block of the VPC and a default route to the Internet gateway.
5.  A default security group is created that allows inbound traffic from all the virtual interfaces to which it is applied and allows outbound traffic to any destination.
6.  A DHCP-options set is also defined with the the domain-name option set to DHCP local.

# VPC Peering

VPC peering lets users create direct IP connectivity between any two VPCs. Direct connectivity between VPCs means that servers in a VPC can be reached from the other VPC without the need for floating IPs or traffic flowing through the edge network.

-   VPC peering is simply L3 connectivity realized using routing tables and IP connectivity.
-   VPC peering can only be achieved between VPCs that do not have an address overlap (as the connectivity is based solely on routing).
-   VPC peering is between exactly two VPCs in one Symphony region.
-   VPC peering is subject to the Symphony permission scheme, meaning that for a user to create a peering connection, that user needs to have permissions in both VPCs.
-   Unlike VPC peering in AWS, the Symphony implementation does not require the two ends of the peering connection to consent.
    
-   A peer VPC can be referenced in a security group only by the peer's CIDR.
    
-   The VPC peering functionality is supported only with the star topology and with one central VPC and 3 peered VPCs.
    

![](https://www.stratoscale.com/wp-content/uploads/vpc_peering_overview.png)

To  **create a peering**  connection using the GUI:

1. Click  **Menu**  >  **Networking**  >  **Peering Connections**  >  **Peer VPC**. In the  **Requester**  and  **Accepter**  fields, select the two VPCs you want to connect.

2. Next, to allow traffic to flow, you must create routes in the relevant route tables. A route can be to the entire VPC or to specific subnets within. The target of the route is the peering connection.

To create a route, click  **Menu**  >  **Networking**  >  **Route Tables**  > select route table >  **Routes**  >  **Create**  >  **Peering Connections**.

To  **confirm that a VPC peering connection is working**:

Ping between two VMs in two different VPCs that have a VPC peering connection between them.

# VPC DNS Support

Symphony supports VPC level DNS. VMs can now resolve all DNS addresses in the context of a single VPC.

**Related topics**

[Sample VPC DNS Terraform scenario](https://www.stratoscale.com/knowledge/networking-3/vpc-dns-support/#VPCDNSSupport-Scenario)

**To enable VPC level DNS**:

1. An admin user enables the VPC DNS engine for the entire Symphony region (**Menu**  >  **Networking**  >  **Engines**  > toggle the VPC_DNS  **Enabled**  button to ON).

![](https://www.stratoscale.com/wp-content/uploads/vpc_ennable.png)

2. After the engine is enabled, you control the feature per VPC:

EC2 API - set the  `enableDnsSupport`  property to True.

UI -  **Menu**  >  **Networking**  >  **VPCs**  > select a VPC >  **Modify**  >  **DNS Enable**:

![](https://www.stratoscale.com/wp-content/uploads/vpc_mod.png)

Upgrade consideration

If you created a VPC with the  `enableDnsSupport`  property set to True  **before**  you enabled the VPC_DNS engine, the VPC will not have DNS support. To enable DNS support for a VPC in this situation, first explicitly disable DNS support, and then re-enable it for the VPC.

3. After the engine is enabled, you can use the UI to add arbitrary DNS A records. For example, you may want to define DNS A records for services/VMs in different VPCs when using VPC peering

To add a DNS A record, click  **Menu**  >  **Networking**  >  **VPCs**  > select a VPC >  **DNS Records**  >  **Create**:

![](https://www.stratoscale.com/wp-content/uploads/create_DNS_A_record.png)

## Sample Terraform Scenario

The following scenario describes how you might use VPC DNS support with Terraform.

1. Enable the VPC engine for your Symphony region (**Menu**  >  **Networking**  >  **Engines**  > toggle the VPC_DNS  **Enabled**button to ON).

2. In the Terraform script, set the  `enable_dns_support`  flag to true, for a specific VPC.

With DNS support enabled, any VM that you create within this VPC can use the  `private_dns_name`  returned in the  **describeInstances**  response to access other VMs in the VPC.

Here is how this can work:

By default, when DNS support is enabled in a VPC, the system creates a VM with the following host name:

`host-a-b-c-d`  (where a.b.c.d is the VM IP address in the VPC)

So any VM within this VPC can do something like:

"`ping host-a-b-c-d`" instead of "`ping a.b.c.d`" and it will work.

This functionality is useful for applications that require DNS names and do not work with IP addresses.

3. In addition, you can also add DNS A records to external IPs so they will be resolved within this VPC.

For example, you can add an A record to resolve "service.<vpc-domain>" to any IP (usually external to the VPC). This lets you define a globally named services resolution that resides external to the VPC.

This DNS A record feature is useful for the same reason mentioned above -- some applications require DNS names and do not work with IP addresses.

# Symphony-supported AWS – VPC APIs and Parameters

Below is a list of the AWS - VPC APIs that Symphony supports, together with their supported Required and Optional request parameters.

Click on the API name to access the complete AWS documentation for that action.

Click [here](https://www.stratoscale.com/knowledge/symphony-supported-aws---ec2-apis-and-parameters) for the complete list of Symphony-supported AWS EC2 APIs.

<table class="wrapped relative-table confluenceTable" style="width: 37.8042%;"><colgroup><col style="width: 36.7453%;"><col style="width: 25.2964%;"><col style="width: 37.9447%;"><col></colgroup><tbody><tr><th class="confluenceTh" style="width: 31.5305%;">Name</th><th class="confluenceTh" style="width: 22.3245%;">Required Parameters</th><th class="confluenceTh" style="width: 34.4074%;">Optional Parameters</th><th class="confluenceTh" style="width: 11.0472%; text-align: center;" colspan="1">Notes</th></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AssignPrivateIpAddresses.html" rel="nofollow">AssignPrivateIpAddresses</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>NetworkInterfaceId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>PrivateIpAddress</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AssociateDhcpOptions.html" rel="nofollow">AssociateDhcpOptions</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>DhcpOptionsId</li><li>VpcId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AssociateRouteTable.html" rel="nofollow">AssociateRouteTable</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>RouteTableId</li><li>SubnetId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AttachInternetGateway.html" rel="nofollow">AttachInternetGateway</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>InternetGatewayId</li><li>VpcId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AttachNetworkInterface.html" rel="nofollow">AttachNetworkInterface</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>DeviceIndex</li><li>InstanceId</li><li>NetworkInterfaceId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AuthorizeSecurityGroupEgress.html" rel="nofollow">AuthorizeSecurityGroupEgress</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>GroupId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>IpPermissions</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateDhcpOptions.html" rel="nofollow">CreateDhcpOptions</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>DhcpConfiguration</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateInternetGateway.html" rel="nofollow">CreateInternetGateway</a></td><td class="confluenceTd" style="width: 22.3245%;"></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateNetworkInterface.html" rel="nofollow">CreateNetworkInterface</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>SubnetId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>Description</li><li>PrivateIpAddress</li><li>PrivateIpAddresses</li><li>SecondaryPrivateIpAddressCount</li><li>SecurityGroupId</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateRoute.html" rel="nofollow">CreateRoute</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>RouteTableId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>DestinationCidrBlock</li><li>GatewayId</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateRouteTable.html" rel="nofollow">CreateRouteTable</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>VpcId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateSubnet.html" rel="nofollow">CreateSubnet</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>VpcId</li><li>CidrBlock</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>AvailabilityZone</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateVpc.html" rel="nofollow">CreateVpc</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>CidrBlock</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteDhcpOptions.html" rel="nofollow">DeleteDhcpOptions</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>DhcpOptionsId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteInternetGateway.html" rel="nofollow">DeleteInternetGateway</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>InternetGatewayId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteNetworkInterface.html" rel="nofollow">DeleteNetworkInterface</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>NetworkInterfaceId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteRoute.html" rel="nofollow">DeleteRoute</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>RouteTableId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>DestinationCidrBlock</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteRouteTable.html" rel="nofollow">DeleteRouteTable</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>RouteTableId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteSubnet.html" rel="nofollow">DeleteSubnet</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>SubnetId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteVpc.html" rel="nofollow">DeleteVpc</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>VpcId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeDhcpOptions.html" rel="nofollow">DescribeDhcpOptions</a></td><td class="confluenceTd" style="width: 22.3245%;"></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>DhcpOptionsId</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeInternetGateways.html" rel="nofollow">DescribeInternetGateways</a></td><td class="confluenceTd" style="width: 22.3245%;"></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>InternetGatewayId</li><li>Filter</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeNetworkInterfaces.html" rel="nofollow">DescribeNetworkInterfaces</a></td><td class="confluenceTd" style="width: 22.3245%;"></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>NetworkInterfaceId</li><li>Filter</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeRouteTables.html" rel="nofollow">DescribeRouteTables</a></td><td class="confluenceTd" style="width: 22.3245%;"></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>RouteTableId</li><li>Filter</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeSubnets.html" rel="nofollow">DescribeSubnets</a></td><td class="confluenceTd" style="width: 22.3245%;"></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>SubnetId</li><li>Filter</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeVpcAttribute.html" rel="nofollow">DescribeVpcAttribute</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>VpcId</li><li>Attribute</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeVpcClassicLink.html" rel="nofollow">DescribeVpcClassicLink</a></td><td class="confluenceTd" style="width: 22.3245%;"></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>VpcId</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeVpcClassicLinkDnsSupport.html" rel="nofollow">DescribeVpcClassicLinkDnsSupport</a></td><td class="confluenceTd" style="width: 22.3245%;"></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>VpcId</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;" colspan="1"><span style="color: #0000ff;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeVpcPeeringConnections.html" rel="nofollow">DescribeVpcPeeringConnections</a></span></td><td class="confluenceTd" style="width: 22.3245%;" colspan="1"></td><td class="confluenceTd" style="width: 34.4074%;" colspan="1"><ul><li>VpcPeeringConnectionId</li><li>Filter</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"><span style="color: #0000ff;"><span style="color: #000000;">Introduced</span><strong><br> </strong>Symphony v5.1.1</span></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeVpcs.html" rel="nofollow">DescribeVpcs</a></td><td class="confluenceTd" style="width: 22.3245%;"></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>VpcId</li><li>Filter</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DetachInternetGateway.html" rel="nofollow">DetachInternetGateway</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>InternetGatewayId</li><li>VpcId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DetachNetworkInterface.html" rel="nofollow">DetachNetworkInterface</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>AttachmentId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>Force</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DisassociateRouteTable.html" rel="nofollow">DisassociateRouteTable</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>AssociationId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ModifyNetworkInterfaceAttribute.html" rel="nofollow">ModifyNetworkInterfaceAttribute</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>NetworkInterfaceId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>SecurityGroupId</li><li>SourceDestCheck</li><li>Description</li><li>Attachment</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ModifyVpcAttribute.html" rel="nofollow">ModifyVpcAttribute</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>VpcId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>EnableDnsHostnames</li><li>EnableDnsSupport</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ReplaceRouteTableAssociation.html" rel="nofollow">ReplaceRouteTableAssociation</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>AssociationId</li><li>RouteTableId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr><tr><td class="confluenceTd" style="width: 31.5305%;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_RevokeSecurityGroupEgress.html" rel="nofollow">RevokeSecurityGroupEgress</a></td><td class="confluenceTd" style="width: 22.3245%;"><ul><li>GroupId</li></ul></td><td class="confluenceTd" style="width: 34.4074%;"><ul><li>IpPermissions</li></ul></td><td class="confluenceTd" style="width: 11.0472%;" colspan="1"></td></tr></tbody></table>