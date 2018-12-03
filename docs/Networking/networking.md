
# Introduction to Networking

Guest or VM networks are virtual overlay networks, which connect workloads running within the system. In addition, they provide connectivity between the VMs and the external world. Both external and internal networks are isolated by VLANs.

The current release supports fully functional L2 and L3 connectivity of guest networks. Internal guest networks can be assigned with IP subnets and DHCP service to distribute the IP addresses. Alternatively, the guest networks can be left as plain broadcast domains for you to manage, using your own DHCP.

L3 functionality includes connecting guest networks to routers, managing L3 address ranges, routing rules and floating IPs. This is managed through the Openstack API. The routers are connected outside the cluster using external networks.

# Attaching a Network to a Virtual Machine

During the creation of a VM, you must attach it to an existing network. However, after the creation of a VM, you can also attach to it another network.

One network can be attached to numerous VMs, and one VM can be attached to numerous networks.

**To attach a network to VM**:

1. On the Networks view, locate the network you want to attach to an existing VM, and click the Actions button on the right.

A pop-up menu appears:

![](https://www.stratoscale.com/wp-content/uploads/Networking20-20Attach20Net20Button20620DP.jpg)

- or -

On the  **Networks**  widget, locate the network you want to attach, and click it to open its view:

![](https://www.stratoscale.com/wp-content/uploads/Networking20-20Attach20Net20Button20620DP202.jpg)

2. Click the  **Attach**  option.

The  **Attach Network**  dialog box appears:

![](https://www.stratoscale.com/wp-content/uploads/Networking20-20Attach20Network20620DP.jpg)

3. Select the VM you want to attach to the network from the Virtual Machine drop-down list, and click  **OK**.

The selected VM is now attached to this network, in addition to the network to which it was attached during its creation procedure:

![](https://www.stratoscale.com/wp-content/uploads/Networking20-20Attach20Network20success20620DP.jpg)


# Detaching a Network from a Virtual Machine

A VM cannot be created without a network. However, you can change the network that is currently attached to a VM by detaching it, and attaching another network to the VM. Before detaching a network from a running VM, it is recommended to stop the VM.

To detach a network from a VM

1. On the  **Networking->Networks**  view click a Network name.

![](https://www.stratoscale.com/wp-content/uploads/Networking20-20Networks20view20620DP.jpg)

On the  **Networks**  view, select the  **VM**  tab and click the Actions icon.

![](https://www.stratoscale.com/wp-content/uploads/Networking20-20Networks20detach20VM20button20620DP.jpg)

The Network view shows the VMs that are connected to the network on the VMs tab.

**Note**: You can also detach a network from a selected VM view.

2. On the  **VMs**  tab, locate the VM you want to detach from the network and click the Actions icon, and select the  **Detach**  option.

The VM will be detached from the network.


# Deleting a Network

Before deleting a network, make sure that it is not attached to any running VMs. To detach VMs, see  [Detaching a network from a VM](https://www.stratoscale.com/knowledge/detaching-a-network-from-a-virtual-machine).

**To delete a network**:

1. On the  **Networking->Networks**  view, locate the network you want to delete, and click the Actions icon on the right.

One of the options is  **Delete**.

![](https://www.stratoscale.com/wp-content/uploads/Networking20-20Creating20Edge20Network20delete20button206320DP.jpg)

2. Click the  **Delete**  option.

A confirmation message appears, asking you to approve the deletion:

![](https://www.stratoscale.com/wp-content/uploads/Networking20-20Delete20Network20warning20620DP.jpg)

3. To delete the network, click  **OK**.

The network will be deleted from the system.

# Introduction to Routers

From the main **Menu** select **Networking - Routers**. The Networking > Routers view appears.

For each router the following information is provided:

1.  **Name** - The name of the router.
2.  **Status** - The router's status, whether Active or not
3.  **External Gateway** - The edge network to which the router is attached.
4.  **Public IP** - The router's public recognized address.
5.  **Attached Networks** - The Networks which are attached to the router.
6.  **Account** - The account which owns the router.

# Introduction to Floating IPs

From the main **Menu** select **Networking - Floating IPs**. The Networking - Floating IPs view appears.

This view provides you with information about the floating IPs currently defined in your system.

For each floating IP the following information is provided:

1.  **Floating IP** - the floating IP address.
2.  **Private IP** - the private IP address
3.  **Network** - the external network of the floating IP.
4.  **Account**  - the account which owns the floating IP.
5.  **Attached VM** - The VM to which the floating IP is attached.

# Create Specific Floating IP

You can create a floating IP with a specific IP address by using the CLI.

**To create a specific floating IP**:

Log in to a stratonode and enter the CLI shell by typing:

	$ symp -u admin -d cloud_admin -p <PASSWORD> -k

Issue the  **virt-network floatingip-create**  command and pass in the name of the edge (or floating) network to use, and the specific IP address you want:

	$ virt-network floatingip-create <EDGE_NETWORK> --floating-ip-address <FLOATING_IP_ADDRESS>

# Security Groups

## Introduction to Security Groups

Security Groups define which inbound traffic a VM can receive and which outbound traffic a VM can transmit.

To access the Networking - Security Groups view, click on the **Security Groups** option in the **Networking** sub-menu.

This view provides you with information about the security groups currently defined in your system.

For each Security Group the following information is provided:

**Name** - name of the security group.

**Description** - description of the security group (optional).

**Owner** - the project to which the security group belongs.

**Networks** - Which network the security group is working with.

**VM Count** - the number of VMs attached to this security group.

Clicking on a specific Security group displays widgets listing the Security Group's rules and the Attached Virtual Machines.

# Creating a Security Group

**To create a security group**:

1. Click  **Networking** > **Security Groups**  >  **Create**.

The Create Security Group dialog box appears.

2. Enter the following information:

**Name**  – enter the name of the security group.

**Description**  (optional) - enter a description of the security group.

**Account**  - account associated with this security group.

**Project**  (optional) - select a project that can subscribe to this security group

**Rules**

**Add**  button **-** Click to define rules for the security group.

**Internet Protocol Version**  - select IPV4 or IPV6

**Direction**  - Select EGRESS for defining a rule for outbound traffic. Select INGRESS for defining a rule for inbound traffic

**Protocol**  - Specify the protocol of the traffic this rule will apply to, by selecting either 'TCP', 'UDP' or 'ICMP', or permit traffic from any protocol by selecting 'Any'.

**Start port and end port**

If Protocol = 'Any', then leave blank.

If Protocol = 'TCP' or 'UDP', then enter the port range delimiting the traffic.

If Protocol = 'ICMP', then enter the ICMP Message Type in the first field and ICMP Code in the second field.

**Remote**  - limit the traffic to or from a specific remote site by selecting either 'Group' or 'Subnet', or allow traffic to or from any remote site by selecting 'Any'.  
If you select  **Subnet**:

- If the direction is INGRESS, then specify a CIDR for allowed origin data.

- If the direction is EGRESS, then specify a CIDR for allowed target data.

**Group/Subnet**

If Group/Subnet = 'Any', then the field is not displayed.

If Group/Subnet = 'Group', then select one of the security groups.

If Group/Subnet = 'Subnet', then enter the subnet in CIDR format (10.11.12.0/24).

3. Click  **OK**  to create the security group.

The new security group appears in the Networking - Security Groups view.

# Networking Ports Used by Symphony

<table class="wrapped confluenceTable"><colgroup><col><col><col><col></colgroup><tbody><tr><th class="confluenceTh"></th><th class="confluenceTh">Service</th><th class="confluenceTh">Ports</th><th class="confluenceTh">Comments</th></tr><tr><td rowspan="6" class="confluenceTd"><strong>External</strong><p></p><p></p></td><td class="confluenceTd">Maestro</td><td class="confluenceTd">80, 443</td><td class="confluenceTd">Call home data / support data, tunnel (internet)</td></tr><tr><td class="confluenceTd">v2v</td><td class="confluenceTd">80/443</td><td class="confluenceTd">Pulling packages from Linux repositories (internet)</td></tr><tr><td class="confluenceTd">Data Protection</td><td class="confluenceTd">2828</td><td class="confluenceTd">Data-protection's data path</td></tr><tr><td class="confluenceTd">NTP</td><td class="confluenceTd">123</td><td class="confluenceTd">Clock sync (internet/internal NTP)</td></tr><tr><td class="confluenceTd">K8s Init</td><td class="confluenceTd">443</td><td class="confluenceTd">Get base images (internet)</td></tr><tr><td class="confluenceTd">RDS Init</td><td class="confluenceTd">443</td><td class="confluenceTd">Get base images (internet)</td></tr><tr><td rowspan="5" class="confluenceTd"><strong>Internal - between Symphony nodes</strong><p></p><p></p></td><td class="confluenceTd">API access</td><td class="confluenceTd">80/443</td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd">Docker</td><td class="confluenceTd">5000</td><td class="confluenceTd">Pull image requests between nodes</td></tr><tr><td colspan="1" class="confluenceTd">Openstack API</td><td colspan="1" class="confluenceTd">1060, 10100-10105</td><td colspan="1" class="confluenceTd"></td></tr><tr><td colspan="1" class="confluenceTd">VNC</td><td colspan="1" class="confluenceTd">6080</td><td colspan="1" class="confluenceTd"></td></tr><tr><td colspan="1" class="confluenceTd">Object Storage</td><td colspan="1" class="confluenceTd">1060</td><td colspan="1" class="confluenceTd">To use the object storage service, you need to allow inbound connections to port 1060 for the VIP and all node API IPs.</td></tr></tbody></table>

# Delete Subnets and VLANs

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.  

You can delete subnets and VLANs via the CLI during cluster maintenance.

This functionality is limited to subnets and VLANs without any overlay entities (Virtual IPs, traffic types, VN-Groups). This means that you can delete only subnets and VLANs that you defined after installation.

During the deletion procedure, nodes temporarily lose their network access, and VIPs are down for up to 60 seconds. You can run this procedure through Maestro.

**To delete subnets and VLANs**:

Shutdown all VMs in an orderly manner.

Move the cluster to maintenance:

	$ cluster shutdown

Wait for the cluster to shutdown.

Shutdown network agents on all nodes using the CLI:

	$ networking control agents-shutdown

Wait for the agents to shutdown:

	$ networking control agents-state

Delete the global subnet or VLAN using the CLI. You can delete multiple entities in this stage -- remove subnet first, then VLAN:

	$ networking subnets remove <global subnet uuid>
	$ networking vlans remove <global vlan uuid>

Restart the network agents on all nodes using the CLI:

	$ networking control agents-restart

Note: During this stage network connectivity to all nodes is temporarily lost (up to 20 seconds). VIP also stops working for a longer time (around 60 seconds).

Wait for the agents to return to normal operation:

	$ networking control agents-state

Return the cluster to normal operation:

	$ cluster powerup




