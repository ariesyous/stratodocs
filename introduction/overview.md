
# Symphony Overview

Symphony is the Stratoscale private cloud stack. Symphony gives you the ability to create an AWS-compatible on-prem private or public cloud within your own datacenter and on your own hardware.

At a high level:

-   A Symphony system starts with four or more bare metal servers, connected by Ethernet to one or more  [switches](https://www.stratoscale.com/knowledge/the-symphony-infrastructure-networks). These servers can be from any manufacturer, as long as they meet certain  [basic requirements](https://www.stratoscale.com/knowledge/installation-prerequisites).
-   You then install Stratoscale software on each server, so that each server becomes a node in a Symphony private cloud region. The Symphony software includes an operating system and a hypervisor, as well as other Symphony-specific features. You do not need to lay down an operating system and then install Symphony on top of it -- Symphony gives you all you need to put on top of the hardware of your choice.

Once you install Symphony on your bare metal servers to create your private cloud region, your region includes:

-   A  **full-featured compute layer**  that allows for creation, management, and manipulation of x86-based virtual machines. Symphony provides intelligent load balancing. If it finds an overloaded node, it automatically moves workloads away from that node to a node with more capacity - typically moving a VM from source to destination in about half a second.
-   The ability to use  **both external storage**  (iSCSI, Fibre Channel, and NFS),  **as well as the ability to create a “virtual SAN”**  made up of nothing more than the solid state and magnetic hard disks held within the nodes themselves.
-   A  **complete virtual networking layer**; allowing for the creation of objects ranging from internal private networks, external NAT communication networks, fixed IPs for specific VMs, and security groups to control what may flow across those networking objects and paths.
-   A  **fully distributed automation and control architecture**  that exists across all nodes. Management processes and state are replicated to every node in the region, so resources are not wasted on a single management server. In addition, you can lose one or more of your nodes to a planned or unplanned outage, but your region will still run, because each node has all it needs to manage the region.
-   An  **API**  and  **CLI**  for for scripting, automation, and control.
-   A fully-featured, browser-based  **GUI**  to handle all day-to-day operations without having to drop to the command line.

## Symphony Architecture

Symphony uses a hyperconverged architecture. This means that each Symphony node integrates compute, storage, networking, and management within the node, as opposed to dedicating separate hardware for each infrastructure function.

This provides a shared resource pool and simplified management that lets you scale and upgrade without moving data or experiencing down time. When you want to scale, you do not have to deal with storage, networking, and hypervisor issues separately - you simply add another node to the region.

Stratoscale achieves the agility and simplicity of hyperconverged infrastructure with a software-only solution. Every server runs a similar software stack, and together with the other servers forms a private cloud:

![](https://www.stratoscale.com/wp-content/uploads/Strato-Architecture-1.jpg)

Stratoscale provides compute, storage, and network virtualization across hyperconverged clusters. This virtualized infrastructure, in turn, supports a cloud manager and integration layer for centralized control.