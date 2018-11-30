# Project Overview

1.  On the main menu select **Accounts Management** > **Accounts**.and then click <name of the account > **Projects** tab.  
    A list of all of the projects in the selected account, together with their Enabled status, is displayed.
2.  Two project actions can be performed from this view:
    1.  [**Create** a new project](https://www.stratoscale.com/knowledge/creating-a-project)
    2.  [View a single existing project](https://www.stratoscale.com/knowledge/viewing-a-single-project)  
        [  
        ](https://www.stratoscale.com/knowledge/viewing-a-single-account)
3.  When a project is highlighted, six additional actions can be performed:
    1.  [**Assign** a **User** to a project](https://www.stratoscale.com/knowledge/assigning-a-user-to-a-project)
    2.  [**Disable** a project](https://www.stratoscale.com/knowledge/disabling-a-project)
    3.  [**Enable** a project](https://www.stratoscale.com/knowledge/enabling-a-project)
    4.  [**Rename** a project](https://www.stratoscale.com/knowledge/renaming-a-project)
    5.  [Configure default **EC2 Networks** for a project](https://www.stratoscale.com/knowledge/configuring-default-ec2-networks)
    6.  [**Delete** a project](https://www.stratoscale.com/knowledge/deleting-a-project)
        
        Only Tenant_Admin or Admin users can perform these actions.  
        **Note**: The 'default' project in the cloud_admin account cannot be disabled or deleted.

# Creating a Project

If you want to divide your virtual resources among numerous users within each account, you need to create different projects within the account.

The Admin (system administrator) user can create projects in any account, while the Tenant Admin can create projects only in the tenant admin's own account.

**To create a project**:

1.  On to the **Account Management** > **Accounts** > view, either
    1.  Highlight the row of the account in which you wish to create a project.  
        A **Create Project** button appears in the toolbar, or
    2.  Click on the name of the account in which you wish to create a project.  
        The view of the selected account will appear, with a **Create Project** button in the toolbar of the  **Projects**tab.
2.  Click **Create Project**.  
    The Create Project dialog box appears.
3.  Enter the following information:
    1.  **Project Name**  – enter a name for the new project. The name must be unique within the account.  
        **Note:**  The names are not case-sensitive.
    2.  **Project Description**  [Optional] – enter a description of the new project.
4.  Click  **OK**  to create the new project.  
    The new project is created and appears under the  **Projects**  tab of the specific account

# Using a VPC-Enabled Project

**Background**

When you want to use the AWS API (and its associated tools such as Terraform) to work with Symphony resources, you need to:

-   Make sure there is a shared edge network available in your Symphony region.
-   Create a project that is both:
    
    -- Dedicated for use by AWS API operations (meaning you do not use this project for any non-AWS actions)
    
    -- Enabled with a VPC
    

**About VPC-enabled projects**

When you create a VPC-enabled project:

On the API level, you are telling the project to accept only API calls from the AWS API. That means that this project can only consume workloads that were initiated using the AWS API.

In addition, the VPC-enabled project comes "pre-baked" with a set of default values for useful things such as subnets, internet gateways, route tables, and security groups. This let you get up to speed very fast. For example, you can create and use instances without having to define various required values yourself – you can simply use the defaults.

Use defaults only when you want

Note that you are not limited to using only the initial default VPC values. You can also create custom VPCs for a project. The way this works is:

-   When you first create a VPC-enabled project, the system automatically creates a VPC called  **Default VPC**. The  **Default VPC**  comes with pre-set values for: Subnet, Security Group, Route Table, and Internet Gateway. When you use this default Internet Gateway, the system automatically routes all traffic towards it.
-   Later on, you can create a custom VPC (**Menu**  >  **Networking**  >  **VPCs**  >  **Create**) where you specify your own custom values for Subnet(s) and Internet Gateway(s).

**To create a VPC-enabled project for use with the AWS API**:

**Menu**  >  **Account Management**  >  **Accounts**  > select an account >  **Create Project**  >  **Enable VPC**  > select an existing Symphony edge network for this project.

About this edge network

-   When an AWS API user creates an internet gateway and routes traffic to it, the traffic goes through this edge network.
-   Also, elastic IPs (EIPs) are allocated on this edge network.

# Assigning a User to a Project

**To assign a user to a project**:

1.  Go to the **Accounts Management** > **Accounts** > <**name of specific account**> view / **Projects** tab, and either
    1.  Highlight the row of the project to which you wish to assign a user.  
        An  **Assign User** button appears in the toolbar, or
    2.  Click on the name of the project to which you wish to assign a user.  
        The view of the selected project will appear, with an **Assign User** button in the toolbar,
2.  Click **Assign User**.  
    The  **Assign User to Project: <name of selected project>**  window appears.
3.  Do the following:
    
    1.  Select a  **User**  to assign to the project.
        
    2.  Select one of the five project **Roles**.  
        **Note**: The only role that should be selected is the user's account role. (Before assigning a user to a project go to the **Accounts Management** > **Accounts** > <**name of specific account**> view / **Users** tab to see the selected user's account role.)
        
4.  Click **OK**.  
    A message confirming the updating of the user's role for this project will pop-up in the upper right-hand corner of the screen.
    
    You can view a user's project roles on the  **Projects**  tab of the **Accounts Management** > **Accounts** > <**name of specific account**> **Users** > <**name of specific user**> view

# Disabling a Project

**Note**: The status of each project is indicated in the Enabled column of the Projects tab.

**To disable a project**:

1.  Go to the **Accounts Management** > **Accounts** > <name of specific account> view / **Projects** tab, and highlight the row of the project you wish to disable. Notice that the project is checked in the  **Enabled**  column.  
    A **Disable** button appears in the toolbar.  
    **Note**: When the selected project is "Enabled", the toolbar has an  **Disable** button instead of an **Enable** button.
2.  Click **Disable**.  
    A window pops-up informing you that the action has succeeded, and the project is no longer checked in the  **Enabled**  column.
    
    **Note**: The **default** project in the **cloud_admin** account cannot be disabled.

# Enabling a Project

**Note**: The status of each project is indicated in the  **Enabled**  column of the Projects tab.

**To enable a project**:

1.  Go to the **Accounts Management** > **Accounts** > <name of specific account> view / **Projects** tab, and highlight the row of the project you wish to enable. Notice that the project is not checked in the **Enabled** column.  
    An **Enable** button appears in the toolbar.  
    **Note**: When the selected project is "Disabled", the toolbar has an  **Enable**  button instead of a  **Disable**  button.
2.  Click **Enable**.  
    A window pops-up informing you that the action has succeeded, and the project is now checked in the **Enabled** column.

# Renaming a Project

**To rename a project**:

1.  Go to the **Accounts Management** > **Accounts** > <name of specific account> view / **Projects** tab, and either
    1.  Highlight the row of the project you wish to rename.  
        A **Rename** button appears in the toolbar, or
    2.  Click on the name of the project you want to rename.  
        The view of the selected project will appear, with a **Rename** button in the toolbar,
2.  Click **Rename**.  
    The Rename Project window appears.
3.  Make the necessary changes in the project name and its description.
4.  Click **OK**.

# Deleting a Project

**To delete a project**:

1.  Go to the **Accounts Management** > **Accounts** > <name of specific account> view / **Projects** tab, and either
    1.  Highlight the row of the project you wish to delete  
        A **Delete** button appears in the toolbar, or
    2.  Click on the name of the project you want to delete.  
        The view of the selected project will appear, with a  **Delete** button in the toolbar,
2.  Click **Delete**.  
    The Delete Project confirmation window appears.
3.  Click **OK**.  
    A message confirming the deletion of the project will pop-up in the upper right-hand corner of the screen.
    
    **Note**: You cannot delete the 'default' project in the cloud_admin account.

# Viewing a Single Project

On the  **Accounts Management** > **Accounts** > <name of specific account> >  **Projects** view, click on the name of a specific project.  
A view of the specific project appears with the following project details:

1.  Summary information
    
    1.  **Resources** widget - The amount of CPU Cores, RAM, and Volume, Image and Snapshot storage used by the project
        
    2.  **EC2 Networks** widget - The project's Internal and External networks for which the EC2 Network has been activated
        
    3.  **Virtual Assets** widget - The number of Instances, Networks, Volumes, Floating IPs, Security Groups, Kubernetes Clusters and relative DBs used by the project
        
2.  Six project actions can be performed from this view:
    
    1.  [**Assign** a **User** to a project](https://www.stratoscale.com/knowledge/assigning-a-user-to-a-project)
    2.  [**Disable** a project](https://www.stratoscale.com/knowledge/disabling-a-project)
    3.  [**Enable** a project](https://www.stratoscale.com/knowledge/enabling-a-project)
    4.  [**Rename** a project](https://www.stratoscale.com/knowledge/renaming-a-project)
    5.  [Configure default **EC2 Networks** for a project](https://www.stratoscale.com/knowledge/configuring-default-ec2-networks)
    6.  [**Delete** a project](https://www.stratoscale.com/knowledge/deleting-a-project).
        
        Only Tenant_Admin or Admin users can perform these actions.  
        **Note**: The 'default' project in the cloud_admin account cannot be disabled or deleted.
        
3.  Additional project information can be found in the seven tabs listed below:
    
    1.  **Instances**
        
    2.  **Networks**
        
    3.  **Volumes**
        
    4.  **Images**
        
    5.  **Snapshots**
        
    6.  [Project **Limits**](https://www.stratoscale.com/knowledge/project-limits)
    7.  [Placement **Rules**](https://www.stratoscale.com/knowledge/vm-placement-rules)

# Project Limits

# Project Limits Overview

Symphony allows you to set limits to the amount of Compute, Storage and Networking resources each project can use. It is recommended that each account admin (**tenant admin** user) set the available resource limits for each of the projects within their account.

### **Project Limits**

1.  On the **Accounts Management** > **Accounts** > <**name of specific account**> > **Projects** > <**name of specific project**> view, click on the **Limits** tab.  
    A list of all Compute, Storage and Networking limits of the selected project together with their current usage, is displayed.  
    Limits can be imposed on the following project resources:
    
    1.  Compute:
        1.  Cores
        2.  Instances
        3.  RAM
        4.  Number of key-pairs
    2.  Storage  
        **Note**: Storage limits are defined and displayed per storage pool, which are then aggregated to a Project limit.
        1.  Number of volumes
        2.  Volume capacity
        3.  Number of images
        4.  Image capacity
        5.  Number of snapshots
    3.  Networking
    
    1.  1.  Floating IPs
        2.  Networks
        3.  Routers
        4.  Security groups
        5.  Security group rules
        6.  Subnets
2.  The following Project resource limit actions can be performed from this view:
    1.  [**Add** a Compute resource limit to a project](https://www.stratoscale.com/knowledge/adding-a-compute-resource-limit-to-a-project)
    2.  [**Add** a Storage resource limit to a project](https://www.stratoscale.com/knowledge/adding-a-storage-resource-limit-to-a-project)
    3.  [**Edit** a Networking resource limit of a project](https://www.stratoscale.com/knowledge/editing-a-networking-resource-limit-of-a-project)
3.  Additional actions which can be performed from this view once a Project resource limit has been defined are:
    1.  [**Clear** a virtual resource limit from a Project](https://www.stratoscale.com/knowledge/clearing-a-virtual-resource-limit-from-a-project)
    2.  [**Edit** a virtual resource limit of a Project](https://www.stratoscale.com/knowledge/editing-a-virtual-resource-limit-of-a-project)

# Adding a Compute Resource Limit to a Project

Symphony allows you to limit the amount of compute resources each project can use. Compute limits affect the following resources:

1.  Cores
2.  Instances
3.  Number of key-pairs
4.  RAM

**To limit one of these resources for a project:**

1.  On the **Accounts Management** > **Accounts** > <**name of specific account**> > **Projects** > <**name of specific project**> view, click on the **Limits** tab.  
    A 3-part list of all Compute, Storage and Networking limits of the selected project together with their current usage, is displayed.
2.  Click on the  **Add**  button which is at the top-right of the  **Compute** part of the list.  
    This pops-up the  **Add Compute Limit**  window.
3.  Do the following:
    1.  Select the  **Resource**  to be limited,
    2.  Note its current  **Usage**, if any.
    3.  Enter it's  **Limit**. Verify that the limit exceeds the current usage.  
        
4.  Click  **OK**.  
    The selected resource limit will be updated on the Compute part of the list of Project resource limits.

# Adding a Storage Resource Limit to a Project

Symphony allows you to limit the amount of storage resources each project can use, per storage pool. Storage limits affect the following resources:

1.  Number of volumes
2.  Volume capacity
3.  Number of images
4.  Image capacity
5.  Number of snapshots

**To limit one of these resources for a project:**

1.  On the **Accounts Management** > **Accounts** > <**name of specific account**> > **Projects** > <**name of specific project**> view, click on the **Limits** tab.  
    A 3-part list of all Compute, Storage and Networking limits of the selected project together with their current usage, is displayed.
2.  Click on the  **Add**  button which is at the top-right of the  **Storage** part of the list.  
    This pops-up the  **Add Storage Limit**  window.
3.  Do the following:
    1.  Select the  **Resource**  to be limited,
    2.  Select the  **Storage Pool**, in which the resource will be located.
    3.  Note its current  **Usage**, if any.
    4.  Enter it's  **Limit**. Verify that the limit exceeds the current usage.  
        
4.  Click  **OK**.  
    The selected resource limit will be updated on the Storage part of the list of Project resource limits per storage pool, and aggregated to the project level.

# Editing a Networking Resource Limit of a Project

Symphony allows you to limit the amount of virtual Networking resources each project can use. Networking limits affect the following resources:

1.  Floating IPs
    
2.  Networks
    
3.  Routers
    
4.  Security Groups
    
5.  Security Group Rules
    
6.  Subnets
    

**To limit one of these resources for a project:**

1.  On the **Accounts Management** > **Accounts** > <**name of specific account**> > **Projects** > <**name of specific project**> view, click on the **Limits** tab.  
    A 3-part list of all Compute, Storage and Networking limits of the selected project together with their current usage, is displayed.
2.  Click on the  **Edit**  button which is at the top-right of the  **Networking** part of the list.  
    This pops-up the  **Edit Networking Limits**  window.
3.  For each resource either check the  **Unlimited**  box, or uncheck it and enter a limit.
4.  Click  **OK**.  
    The selected resource limit will be updated on the Networking part of the list of Project resource limits.

# Clearing a Virtual Resource Limit from a Project

**To clear a virtual resource limit from a project:**

1.  On the **Accounts Management** > **Accounts** > <**name of specific account**> > **Projects** > <**name of specific project**> view, click on the **Limits** tab.  
    A 3-part list of all Compute, Storage and Networking limits of the selected project together with their current usage, is displayed.
2.  Select a Compute or Storage resource limit and click on its **Clear** button.  
    The resource limit will be deleted from the list.


# Editing a Virtual Resource Limit of a Project

**To edit a virtual resource limit of a project:**

1.  On the **Accounts Management** > **Accounts** > <**name of specific account**> > **Projects** > <**name of specific project**> view, click on the **Limits** tab.  
    A 3-part list of all Compute, Storage and Networking limits of the selected project together with their current usage, is displayed.
2.  Select a Compute or Storage resource limit and click on its **Edit** button.  
    This pops-up the  **Edit Compute Limit**  window or the **Edit Storage Limit** window, respectively.
3.  Do the following:
    1.  Note its current  **Usage**, if any.
    2.  Modify its  **Limit**. Verify that the limit exceeds the current usage.  
        
4.  Click  **OK**.  
    The selected resource limit will be updated in the list of Project resource limits.

# VM Placement Rules Overview

Symphony allows you to define rules how the VMs should be placed on the various nodes of the cluster.

### VM Placement Rules

1.  On the **Accounts Management** > **Accounts** > <**name of specific account**> > **Projects** > <**name of specific project**> view, click on the **Rules** tab.  
    A list of all VM Placement Rules for the selected project is displayed, with the following information for each:
    1.  **Creation Date**
    2.  **Rule Type**
    3.  **Description**
    4.  **Enforcement** Level
2.  The following Placement Rule actions can be performed from this view:
    1.  [**Add** a **Rule**](https://www.stratoscale.com/knowledge/creating-a-vm-placement-rule)
        
3.  Additional actions which can be performed from this view once a Project has been selected are:
    1.  [**Simulate** a **Rule**](https://www.stratoscale.com/knowledge/simulating-a-vm-placement-rule)
    2.  [**Apply** a **Rule**](https://www.stratoscale.com/knowledge/applying-a-vm-placement-rule)
    3.  [**Remove** a Rule](https://www.stratoscale.com/knowledge/removing-a-vm-placement-rule)

# Creating a VM Placement Rule

Symphony allows you to determine how the VMs used by your projects should be placed on the physical nodes or servers. Defining a rule is a 2-stage process. First, using the tags attached to the VMs and nodes, you choose the placement rule types and set its parameters. There are three placement rule types from which you may choose:

1.  **Same tagged-VM rule**  - Placement of the VMs is a function of the common specific tag that they share.
2.  **Different-tagged VM rule**  - Placement of the VMs is a function of the different tags with which each VM was marked.
3.  **VM and Node tags**  - Placement of the VMs is a function of the specific tags with which the VM and its host Node were marked.  
    **  
    Note**: The VM and Node tags rule, can be created only by an Admin user.

After determining the rule type and setting its specific parameters, you must define the level of its enforcement. There are two options:

**Hard**  - VMs will be created only within the rule's constraints.

**Soft**  - The VMs will be created even if Symphony does not succeed to place the VMs according to the rule's constraints.

**To create a VM Placement Rule**

1.  Go to the **Accounts Management** > **Accounts** > <**name of specific account**> > **Projects** > <**name of specific project**>.view
    1.  Click on the **Rules** tab.
    2.  Click **Add Rule.  
        **The ****Create VM Placement Rule for Project**** window appears**.**
        
2.  Do the following:
    1.  Select the type of VM Placement Rule you need and define its parameters. You can select existing tags or create new tags in any of the Tag fields.
    2.  Determine whether the enforcement of the rule should be Hard or Soft.
3.  Click  **OK  
    **The new VM Placement Rule will appear on the Rules Tab for the selected project.

**Note**: You can create as many VM Placement Rules as you want per project, provided that the rule does not either duplicate, contradict or override any other rule, or that it itself is not overridden by any other rule.

# Simulating a VM Placement Rule

**To simulate a VM Placement Rule**

1.  Go to the **Accounts Management** > **Accounts** > **<name of specific account> >** **Projects >****<name of specific project>**, and click the **Rules** tab.  
    The list of all of the placement rules for this project is displayed.
2.  Highlight the row of the placement rule you wish to apply.  
    A **Simulate Rule** button appears in the toolbar.
3.  Click **Simulate Rule.  
    **The ****Simulate Rule**** information window, which inform you which instances will be potentially affected by the rule, appears.
4.  Click **OK**.

# Applying a VM Placement Rule

**To apply a VM Placement Rule**:

1.  Go to the **Accounts Management** > **Accounts** > **<name of specific account> >** **Projects >****<name of specific project>**, and click the **Rules** tab.  
    The list of all of the placement rules for this project is displayed.
2.  Highlight the row of the placement rule you wish to apply.  
    An **Apply Rule** button appears in the toolbar.
3.  Click  **Apply Rule**.  
    The **Apply Rule** confirmation window with the following information, appears:
    1.  It lists the instances will be potentially affected by the rule.
    2.  It offers you a choice of what to do with those affected instances which cannot be placed according to the rule.
        1.  To stop them, or
        2.  Leave them where they are (without stopping them)
4.  Select what to do with these instances which cannot be placed according to the rule and click **OK**.  
    A message confirming the application of the placement rule will pop-up in the upper right-hand corner of the screen.

# Removing a VM Placement Rule

**To remove a VM Placement Rule**:

1.  Go to the **Accounts Management** > **Accounts** > **<name of specific account> >** **Projects >****<name of specific project>**, and click the **Rules**  tab.  
    The list of all of the placement rules for this project is displayed.
2.  Highlight the row of the placement rule you wish to remove.  
    A **Remove** button appears in the toolbar.
3.  Click **Remove**.  
    The  **Remove Rule**  confirmation window appears.
4.  Click **OK**.  
    A message confirming the removal of the placement rule will pop-up in the upper right-hand corner of the screen.





