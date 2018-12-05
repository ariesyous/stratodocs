# Data Protection Overview

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.  

![](https://www.stratoscale.com/wp-content/uploads/Data20Protection_26_Flow.jpg)

Symphony supports cluster-to-cluster Data Protection. This means that at some pre-determined time and frequency, an automatically generated snapshot of the original data in one cluster (the source cluster) is copied to a different cluster (the target cluster). Symphony Data Protection requires the creation of the following four entities:

-   **Protection Manager** - Both the Target and Source sites require Protection Managers, with the following responsibilities:
    -   Target site - This is a user with access to the Storage Pools defined in the Data Protection Target. **This** user is also responsible for defining the Protection Targets.
    -   Source site - This is the user responsible for defining the Protection Banks and Protection Plans.  
        **  
        Note**: In principle, the Protection Manager could be the Admin of the tenant, or even the "admin" user of the "cloud-admin" tenant, but this is not recommended.
-   **Protection Target** - This is the actual physical cluster and storage pool, where the protected data will be stored. By definition, this cluster is not the same cluster as that where the source data is located. The Protection Manager of the Target site creates the Data Protection Target.
    
    **Note**: To create a Protection Target, the Virtual IP for the Data Protection Connection must have already been configured.
    
-   **Protection Bank** - These are the credentials of the target destination cluster where the data is to be protected. (The credentials of the target destination cluster were sent via email by the Admin of the Target site to the Admin of the Source site on creation of the Protection Target.) The Protection Manager of the Source site creates the Data Protection Bank.
-   **Protection Plan** - This entity, created in the source site, determines the following:
    -   The Bank to be used by the Plan
    -   The number of versions, or checkpoints, of these resources that should be retained
    -   The window during which the Data Protection replication may begin
    -   The frequency of the Data Protection replication
        
        The Protection Manager of the Source site creates the Data Protection Plan.
        

After these entities are created, any user at the Source site, regardless of Role, may then protect any volume or Virtual Machine by attaching a Protection Plan to it.

# Protection Manager

Both the Target and Source sites require Protection Managers, with the following responsibilities:

-   Target site - This is a user with access to the Storage Pools defined in the Data Protection Target. This user is also responsible for defining the Protection Targets.
-   Source site - This is the user responsible for defining the Protection Banks and Protection Plans.

**Note**: In principle, any user with an Admin role, or even the "admin" user of the "cloud-admin" tenant may serve as the Protection Manager, but this is not recommended.

The Tenant Admin or Admin of the Target site  [creates the Protection Manager user](https://www.stratoscale.com/knowledge/creating-a-user)  of the Target site.

The Tenant Admin or Admin of the Source site  [creates the Protection Manager user](https://www.stratoscale.com/knowledge/creating-a-user)  of the Source site.

