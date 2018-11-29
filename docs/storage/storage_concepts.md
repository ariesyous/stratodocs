# Storage Concepts Overview

Administrator concepts:

-   After Symphony is installed, an administrator needs to  set up storage resources. This means mapping the existing physical storage (the disks in the nodes and/or external storage) to a Symphony cloud resource called a  [storage pool](https://www.stratoscale.com/knowledge/about-storage-pools).
-   An administrator may also want to set up data protection by using the Symphony  data protection and DR service.

End user concepts:

Once storage resources are set up, Symphony offers two types of self-service storage services for the end user:

-   **Symphony Block Storage Service**  
    Persistent disks (volumes) that can be attached and detached from VMs
    
    Equivalent to AWS-EBS
    
-   **Symphony Object Storage Service**  
    Share objects (files) between VMs and humans / 3rd party software
    
    Equivalent to AWS-S3

# About Storage Pools

![](https://www.stratoscale.com/wp-content/uploads/storage_pool_disk_overview.png)

The Symphony storage pool aggregates physical disks of different performance levels from different nodes into a single shared storage environment. This shared storage environment can be configured into virtual volumes of varying sizes. Factors contributing to the size of the storage pool include:

-   **Mirror or Replication count**  - how many times the data should be stored in the storage pool. Symphony recommends three times but also supports two times. This number of replications or mirrors determines the minimum number of nodes required by the storage pool.
-   **Cache disks**  - In addition to the data disks for the storing the data, the storage pool should include cache disks for accelerating the accessing of the data. Cache disks accelerate all data disks which share its node and storage pool. Datadisks are usually hard disk drives (HDDs). While cache disks are solid state drives (SSDs).

Symphony also supports the the attaching of an external storage device to the cluster. Once attached this external storage is treated like a Symphony storage pool, from which virtual volumes can be configured.

**Ceph considerations**

Symphony uses an underlying storage engine based on Ceph:

-   Ceph pools support only 3 replicas.
-   If a Ceph pool has HDDs, then you must add SSDs as cache disks.

# Storage Terms

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><th class="confluenceTh">Term</th><th class="confluenceTh">Definition</th></tr><tr><td class="confluenceTd">Provisioned capacity</td><td class="confluenceTd">&nbsp;Total size of all disks and node volumes.&nbsp;(Can be larger than total capacity.)</td></tr><tr><td class="confluenceTd">Total capacity</td><td class="confluenceTd">Net capacity of the pool (raw storage / replication factor).</td></tr><tr><td class="confluenceTd">Used capacity</td><td class="confluenceTd">Actual used capacity out of the total net capacity.</td></tr><tr><td class="confluenceTd">Free capacity</td><td class="confluenceTd">Free capacity out of the total net capacity (Total - Used).</td></tr></tbody></table>

Basically Provisioned / Used is the optimization factor. The optimization factor is the effect of the thin clone and the thin (sparse) provisioning.

