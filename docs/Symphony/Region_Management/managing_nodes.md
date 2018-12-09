
# Node Management

## Overview

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.  

**Managing Clusters and Nodes**

Symphony allows you to dynamically change the cluster size after the initial installation. This refers to adding and removing nodes, or to taking nodes down for maintenance without system downtime.

When a new node is physically added to the cluster, the system automatically detects the new node. This node is now a candidate for the cluster. Once you Accept this candidate node, the system makes the node active. The storage subsystem joins the hard drives of the new node to the cluster, and increases the total system capacity. This addition also increases the system storage performance, as more hard drives are reading and writing data. In addition, the new node starts admitting VMs on it, and increases the aggregated compute resources of the system. The automatic rebalancing starts migrating VMs to the new node, balancing the load on each of the nodes in the cluster.

When you remove a node from the cluster, the VMs running on it will automatically migrate to other nodes. After the migration is completed, the node is removed from the cluster. There is a period of time after a node removal in which the cluster is in a degraded mode. During this time, the storage subsystems rebuilds the data that was stored in the removed node on other nodes in the system.

Stratoscale cluster management system includes an automatic rebalancing feature which strives to balance the load on all the nodes of the system. This enables individual nodes and the system as a whole to accommodate spikes in resource usage of VMS, without degradation in performance.

The automatic rebalancing system continuously monitors the system and migrates workloads from nodes with high load to nodes with low load. It monitors resource usage, not the number of VMs; thus, it is possible to have a large number of idle VMs on one node, while a single busy VM occupies another node.

# Accepting a New Candidate Node

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.  

This action is intended for a newly installed node whose status after installation is Candidate.

**To accept a new node**:

Click  **Menu**  >  **Region Management**  >  **Nodes**  > select the node you want > click the  **Accept**  button.

The node's status first changes to Approved. After a few minutes its status changes to Active:

Once the node is active, the system automatically moves running VMs to it, to rebalance and optimize the cluster resources.

# Deactivating a Node

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.  

Symphony allows you to deactivate a node for a limited period of time, and to reactivate it once it is ready again for use. This option is useful when, for example, you want to perform some maintenance work on a node, and to reactivate it later, without losing any VMs or data. When a node is deactivated, the system automatically moves all of its VMs and resources to the other nodes in the cluster, before shutting it down. When the node is activated at a later stage, the VMs and resources are redistributed again, using the reactivated node. There is a storage performance penalty during this deactivation.

**To deactivate a node**:

1. Click  **Menu**  >  **Region Management**  >  **Nodes**  > select the node you want > click the  **Maintenance**  button.

The Move Node to Maintenance warning pops-up.

2. Click the  **OK**  button.

The status of the node first changes to Entering maintenance while the system moves the VMs that were on this node to another node. When all the VMs on the selected node have been moved, the node status changes to Maint.

Its Virtual Machines tab is empty of VMs.

Once the deactivated node is ready to join the cluster again, you can  [activate it](https://www.stratoscale.com/knowledge/activating-a-deactivated-node).

# Activating a Deactivated Node

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.  

You can activate a node that you previously deactivated for maintenance. When a node is reactivated, the system automatically redistributes the VMs and resources from the other nodes in the cluster to the newly reactivated node. There is a storage performance penalty during this reactivation.

**To activate a deactivated node**:

Click  **Menu**  >  **Region Management**  >  **Nodes**  > select the node you want > click the  **Activate**  button.

The node is activated and its status changes to Active.

Once the node is active again, the system rebalances the running VMs by moving some running VMs to the reactivated node. This rebalances and optimizes the cluster resources.

# Activating a Deactivated Node

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.  

You can activate a node that you previously deactivated for maintenance. When a node is reactivated, the system automatically redistributes the VMs and resources from the other nodes in the cluster to the newly reactivated node. There is a storage performance penalty during this reactivation.

**To activate a deactivated node**:

Click  **Menu**  >  **Region Management**  >  **Nodes**  > select the node you want > click the  **Activate**  button.

The node is activated and its status changes to Active.

Once the node is active again, the system rebalances the running VMs by moving some running VMs to the reactivated node. This rebalances and optimizes the cluster resources.

# Reviewing Node Details

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.  

**To display more information about a node**:

1.On the  **Nodes**  view, click on the row of the Node (but not the node name) for which you want extra information.

![](https://www.stratoscale.com/wp-content/uploads/Nodes_3_List20of20Nodes202B20Selected20Node20Details.jpg)

Summary node information appears on the bottom of the screen.

2. Click on  **More Details**  (located above the node summary information), or on the  **name of the node**  in the list of nodes above.

The view now displays the following additional information about the node:

-   Overview
-   Events
-   Interfaces
-   Monitoring
-   Disks
-   VMs
-   Services

# Node Fencing

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.  

Node fencing is a Stratoscale term that refers to a node having been put offline because of a network problem.

**How do you become aware that a node is fenced?**

Here's how you may notice that a node in a fenced state:

-   You see that some of your VMs or services have been disrupted via reboot, and that a node appears offline or in an Error state.
-   If you then  `ssh`  into the node in question, and review logs such as  `harbourd`, you see that the node is in a "fenced" state.

**What causes a node to become fenced?**

Typically, a node becomes fenced because of a hardware failure on the node, such as a NIC failure or switch failure.

This causes a node to lose its connections to the storage/control networks, and VMs cannot get access to their data. Symphony notices this and restarts these VMs on other nodes.

In addition, the monitoring mechanism among nodes (consul) notices that it is no longer getting keepalives from the failed node, and puts the failed node into a fenced state.

**How do you recover a node from a fenced state?**

The node autorecovers after 300 seconds (5 minutes).

**How can you prevent node fencing?**

Ensure that the network is stable, have stacked/lagged switches, ensure that there are multiple NICs on the hosts connecting to the switch stack in a port redundant effort.
