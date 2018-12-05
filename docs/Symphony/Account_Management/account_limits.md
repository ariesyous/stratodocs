# Account Limits Overview

Compute and storage resources can be limited per account and per project within the account. When these limits are set, Symphony tracks the usage of these resources when they are allocated or freed-up, both at the project level and at the account level. Only an **admin** user may set the available resource limits for each account. It is recommended that each account admin (**tenant admin** user) set the available resource limits for each of the projects within the account.

For a given resource, the sum of the limits **set** for each project within an account may exceed the limit set for the account itself. However the total amount of the resource actually **used** may never exceed either the project limit or account limit set for that resource. For example, if a **cloud admin** sets a 10-image limit for account A, the **account admin** of A may set a 5-image limit for each of its three member projects - P1, P2, P3. This sets the total limits of the projects at 15, even though the limit of account A is only 10. Nevertheless, users within account A will be allowed to create images only until they either reach the limit of 5 in their project, or until 10 images have been created in the account across all projects.

Networking resources can currently be limited only per project.

**Account Limits**

1.  On the **Accounts Management** > **Accounts**.> <**name of specific account**> view click the **Limits** tab.  
    A list of all Compute and Storage limits of the specific account together with their current usage, is displayed.
    
    Limits can be imposed on the following account resources:
    
    1.  Compute:
        1.  Cores
        2.  Instances
        3.  RAM
        4.  Number of key-pairs
    2.  Storage:  
        **Note**: Storage limits are defined and displayed per storage pool, which are then aggregated to an Account limit.
        
        1.  Number of volumes
        2.  Volume capacity
        3.  Number of images
        4.  Image capacity
        5.  Number of snapshots
        
2.  The following Account resource limit actions can be performed from this view:
    1.  [**Add** a Compute resource limit to an Account](https://www.stratoscale.com/knowledge/adding-a-compute-resource-limit-to-an-account)
    2.  [**Add** a Storage resource limit to an Account](https://www.stratoscale.com/knowledge/adding-a-storage-resource-limit-to-an-account)
3.  Additional actions which can be performed from this view once an Account resource limit has been defined are:
    1.  [**Clear** a virtual resource limit from an Account](https://www.stratoscale.com/knowledge/clearing-a-virtual-resource-limit-from-an-account)
    2.  [**Edit** a virtual resource limit of an Account](https://www.stratoscale.com/knowledge/editing-a-virtual-resource-limit-of-an-account)

# Adding a Compute Resource Limit to an Account

Symphony allows you to limit the amount of compute resources each account can use. Compute limits affect the following resources:

1.  Cores
2.  Instances
3.  Number of key-pairs
4.  RAM

**To limit one of these resources for an account:**

1.  On the **Accounts Management** > **Accounts** > <**name of specific account**> view, click on the **Limits** tab.  
    A 2-part list of all Compute and Storage limits of the selected account together with their current usage, is displayed.
2.  Click on the  **Add**  button which is at the top-right of the  **Compute** part of the list.  
    This pops-up the  **Add Compute Limit**  window.
3.  Do the following:
    1.  Select the  **Resource**  to be limited,
    2.  Note its current  **Usage**, if any.
    3.  Enter it's  **Limit**. Verify that the limit exceeds the current usage.  
        
4.  Click  **OK**.  
    The selected resource limit will be updated on the Compute part of the list of Account resource limits.

# Adding a Storage Resource Limit to an Account

Symphony allows you to limit the amount of storage resources each account can use, per storage pool. Storage limits affect the following resources:

1.  Number of volumes
2.  Volume capacity
3.  Number of images
4.  Image capacity
5.  Number of snapshots

**To limit one of these resources for an account:**

1.  On the **Accounts Management** > **Accounts** > <**name of specific account**> view, click on the **Limits** tab.  
    A 2-part list of all Compute and Storage limits of the selected account together with their current usage, is displayed.
2.  Click on the  **Add**  button which is at the top-right of the  **Storage** part of the list.  
    This pops-up the  **Add Storage Limit**  window.
3.  Do the following:
    1.  Select the  **Resource**  to be limited,
    2.  Select the  **Storage Pool**, in which the resource will be located.
    3.  Note its current  **Usage**, if any.
    4.  Enter it's  **Limit**. Verify that the limit exceeds the current usage.  
        
4.  Click  **OK**.  
    The selected resource limit will be updated on the Storage part of the list of Account resource limits per storage pool, and aggregated to the Account level.

# Clearing a Virtual Resource Limit from an Account

**To clear a virtual resource limit from an account:**

1.  On the **Accounts Management** > **Accounts** > <**name of specific account**> view, click on the **Limits** tab.  
    A 2-part list of all Compute and Storage limits of the selected account together with their current usage, is displayed.
2.  Select a Compute or Storage resource limit and click on its **Clear** button.  
    The resource limit will be deleted from the list.

# Editing a Virtual Resource Limit of an Account

**To edit a virtual resource limit of an account:**

1.  On the **Accounts Management** > **Accounts** > <**name of specific account**> view, click on the **Limits** tab.  
    A 2-part list of all Compute and Storage limits of the selected account together with their current usage, is displayed.
2.  Select a Compute or Storage resource limit and click on its **Edit** button.  
    This pops-up the  **Edit Compute Limit**  window or the **Edit Storage Limit** window, respectively.
3.  Do the following:
    1.  Note its current  **Usage**, if any.
    2.  Modify its  **Limit**. Verify that the limit exceeds the current usage.  
        
4.  Click  **OK**.  
    The selected resource limit will be updated in the list of Account resource limits.



