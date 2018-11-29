# The Symphony Infrastructure Networks

To ensure the successful installation of Stratoscale Symphony, it is necessary to understand the basic network concepts of the system.

Stratoscale Symphony uses six types of logical networks:

1.  Edge network
    -   This is a routable network which allows guests to connect to the office network.
    -   Guests can connect their private networks to this network via a virtual router.
    -   Floating IPs will be allocated on this network.
2.  Internal Guest Networks
    -   These private networks are used for the guest traffic, internal to the cluster (east-west).
    -   In Symphony these networks are isolated either by VLAN or VXLAN tags.
    -   During installation the admin may set the ranges for these tags.
3.  Data network
    -   This is a private network used as the virtual data fabric serving both the storage layer and the live migration of the virtual machines.
    -   Symphony must have full control over this network, and be permitted to allocate IP addresses on a subnet provided by the admin.
4.  Control network
    -   This is a private network used internally for the control path and clustering.
    -   Symphony must have full control over this network, and be permitted to allocate IP addresses on a subnet provided by the admin.
5.  API Endpoint network
    -   See [API Endpoint Virtual IP (VIP)](https://www.stratoscale.com/knowledge/deployment-and-installation/installation-and-setup/the-symphony-infrastructure-networks/#TheSymphonyInfrastructureNetworks-API_Endpoint).
6.  Administrative Access network
    -   This network allows access to the nodes and must be routable to the customer LAN.
    -   During installation the admin sets IP connectivity to this network, either by DHCP or by providing a static IP.
    -   Since this network is connected to the office network, allocation of static IPs must be coordinated with the network admin.

### Network example #1 - Multiple 10G switches

![](https://www.stratoscale.com/wp-content/uploads/Symphony20Network20Example2023120-20Multiple2010G20Switches_820p.png)

### Network example #2 - 10G + 1G switches

![](https://www.stratoscale.com/wp-content/uploads/Symphony20Network20Example2023220-2010G202B201G20Switches_820p.png)

### Network example #3 - Single 10G switch

![](https://www.stratoscale.com/wp-content/uploads/Symphony20Network20Example2023320-20Single2010G20Switch_820p.png)

**Physical Interfaces per Node**

Logical networks map to interfaces on the nodes. These may be the actual NICs or a link aggregate (bond) using the LACP protocol.

During the installation of a node the admin may configure up to 3 bonds.

**Association of Logical Networks to Interfaces**

When installing a new node, its logical networks may be associated with either NICs or bonds.

Data and Control networks and the API Endpoint VIP must be configured for only the first node of the cluster. Symphony then uses a beacon protocol on these networks to automatically configure these logical networks for all other nodes added to the cluster. The beacons are L3 broadcasts on the private VLAN provided for these networks. The node uses the beacon to configure the interface on which it received the beacon with the right VLAN, and then requests an IP address. The address it will get is from the subnet provided when the first node was installed.

In Symphony the internal guest networks are placed by default on the same interface as the data.

**API Endpoint Virtual IP (VIP)**

Symphony requires a static IP as its API endpoint. In Symphony this endpoint IP is always set on the same interface as the Administrative access network. However, while the Administrative network is unique per node the API Endpoint VIP may reside on any of the nodes. If this node fails, the VIP will automatically be set on one of the other nodes in the cluster.

**Recommendations**

Although Symphony supports full flexibility in its network configuration, the following configuration is recommended:

-   The administrative access network should not be connected to the same interface as the other networks.
-   The administrative, control and data networks should be placed on separate VLANs even if they share the same interface.