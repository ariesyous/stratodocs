
# Installation Prerequisites

Before proceeding with the installation, verify that the following prerequisites have been met:

![](https://www.stratoscale.com/wp-content/uploads/Prerequisites.png)

1.  **Hardware  
    **
    
    1.  A minimum of 4 x86 nodes (servers) are available.
        
    2.  Each node must have the following:
        
        1.  **Storage  
            **
            
            -   One solid state drive (SSD) with a minimum of 240 GB of storage capacity for the system/boot.
                
            -   One hard disk drive (HDD) for user data.
                
        2.  **RAM  
            **
            
            -   128GB RAM minimum
                
        3.  **CPU  
            **
            
            -   Intel Xeon (Sandy Bridge or later)
                
    3.  Verify that all nodes are connected to the same physical network.
        
2.  **BIOS Configuration  
    **
    
    1.  The drive on which you are installing Symphony appears first in the boot order. It is recommended that this drive be an SSD.
        
    2.  The DOK or ISO from which you install the software should be defined as a one-time boot.
        
    3.  Virtualization is enabled in the processor settings.
        
    4.  RAID configuration options:
        
        1.  **Using RAID**. If you want redundancy from disk failure, use RAID. In this case, use 2 SSDs that are at least 200GB in size, put them in RAID 1, and install Symphony on the RAIDed disk.
        2.  **Not using RAID**. If you are not using RAID, disable RAID and leave disks in AHCI mode.
    5.  The BIOS must be configured with the legacy mode.  
          
        
3.  **Network Configuration  
    **
    
    1.  There is at least one network switch to enable clustering.
    2.  Decide which NICs you wish to aggregate as bonds.
    3.  Map the logical networks to the NICs and bonds.
    4.  Allocate a sufficient range of VLAN tags for your guest networks. This range covers both the external and internal guest networks.
    5.  Allocate a VLAN tag for each of the following subnetworks:
        1.  Management
        2.  Data
        3.  Administrative Access and API Endpoint VIP
    6.  Configure the switch's ports.
    7.  If DHCP is not enabled on the Administrative network, prepare a static IP per node.
    8.  Prepare a static IP for the API VIP. This may be on the same subnet as the Administrative or in its own subnet as long as it's routable.