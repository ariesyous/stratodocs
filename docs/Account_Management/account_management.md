# Account Management Overview

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.  

![](https://www.stratoscale.com/wp-content/uploads/Accounts_and_Projects.jpg)

## **Accounts and Projects**

The virtual resources of the Symphony region are managed through an administrative hierarchy of accounts & projects. The Symphony region consists of one or more accounts each of which contains one or more projects. Virtual resources such as VLANs, instances, volumes, images and snapshots are created per project. Users, who are members of a account, can be assigned different projects within their account. This enables you to provide access to Symphony to numerous users, dividing and separating the resources that each user will be able to view, create, and manage.

## **Users and Roles**

If a Symphony account is connected to an Identity Provider such as MS Active Directory, users can be accessed from the Identity Provider. If an account is not connected to an identity provider, users can be created within Symphony as members of this account. Regardless of their source, each user must be assigned to one or more of the projects within that account. Users function in one of five capacities or roles:

1.  **Member** - This role grants the user access to any virtual resource belonging to projects to which the user has been assigned. The Member can also modify and delete these resources and create new resources for these projects. This is the standard role for most users
2.  **Tenant Admin** - In addition to the rights to virtual resources granted to a member, the Tenant Admin can also create and manage new projects and users in the account which he administers, and assign users to projects. It is recommended that each account have at least one user with this role.
3.  **Protection Manager** - This role, assigned to a remote user in the context of Disaster Recovery data protection, grants cross-regional access to any data to which this remote user has access.
4.  **Admin** - This role grants a user the privileges to view, create, manage and delete all physical resources, such as nodes (servers), disks, storage pools, physical networks, etc., all administrative entities such as accounts, projects and users, etc., and any virtual resource of any account or project. When assigned to a remote user, it also grants cross-regional access to any data to which this remote user has access. It is possible to create more than one user per region with Admin rights.
5.  **Read-only Admin** - This role grants read-only access to all physical and virtual resources and administrative entities (such as, Accounts, Projects and Users, and Data Protection entities) in the region. It is possible to create more than one user per region with Read-only Admin rights.

**3 rules concerning the assignment of roles**:

1.  To assign a user to a project, you must assign both a project role and an account role.
2.  The project role and account role must be identical.
3.  Only assign a single role per project or per account

When Symphony is installed, it comes with a single account containing one project and one user.

-   The account is called **cloud_admin**.
-   The project inside is called **default**.
-   The user is called **admin**.

This user who has Admin rights, comes already assigned to the project default, and serves as the System Administrator of the entire cloud. This built-in account, project and user cannot be deleted or modified in any way (except that the admin user can change his password).

## **Limits**

**Compute and Storage Resources**

Compute and storage resources can be limited per account and per project within the account. When these limits are set, Symphony tracks the usage of these resources when they are allocated or freed-up, both at the project level and at the account level. It is recommended that the **cloud admin** set the available resource limits for each account, and that each account admin set the available resource limits for each of the projects within the account.

For a given resource, the total of the limits **set** for all projects within an account may exceed the limit set for the account itself. However the total amount of the resource actually **used** may never exceed either the project limit or account limit set for that resource. For example, if a **cloud admin** sets a 10-image limit for account A, the **account admin** of A may set a 5-image limit for each of its three member projects - P1, P2, P3. This sets the total limits of the projects at 15, even though the limit of account A is only 10. Nevertheless, users within account A will be allowed to create images only until they either reach the limit of 5 in their project, or until 10 images have been created in the account across all projects.

The following compute resources can be limited:

1.  Cores
2.  Instances
3.  RAM
4.  Number of key-pairs

The following storage resources can be limited:

1.  Number of volumes
2.  Volume capacity
3.  Number of images
4.  Image capacity
5.  Number of snapshots

**Networking Resources**

Networking resources can currently be limited only per project. These include the following resources:

1.  Floating IPs
2.  Networks
3.  Routers
4.  Security groups
5.  Security group rules
6.  Subnets

# Account Overview

1.  On the main menu select **Accounts Management** > **Accounts**.  
    The **Accounts** view appears with a list of all of the accounts in the region.  
    The following information is displayed for each account:
    1.  **Name**
    2.  **Description**
    3.  Number of **Projects**
    4.  Number of **Users**
    5.  Whether **Enabled** or not
2.  Two account actions can be performed from this view:
    1.  [**Create** an account](https://www.stratoscale.com/knowledge/creating-an-account)
    2.  [View a single account](https://www.stratoscale.com/knowledge/viewing-a-single-account)
        
3.  When an account is highlighted, seven additional actions can be performed:
    1.  **[Create User](https://www.stratoscale.com/knowledge/creating-a-user)**
    2.  [**Create Project**](https://www.stratoscale.com/knowledge/creating-a-project)
    3.  [**Disable** an account](https://www.stratoscale.com/knowledge/disabling-an-account)
    4.  [**Enable** an account](https://www.stratoscale.com/knowledge/enabling-an-account)
    5.  [**Rename** an account](https://www.stratoscale.com/knowledge/renaming-an-account)
    6.  [Connect to the **Identity Provider**](https://www.stratoscale.com/knowledge/connecting-to-the-identity-provider)
    7.  [**Delete** an account.](https://www.stratoscale.com/knowledge/deleting-an-account)

# Creating an Account

When you log in to Symphony the first time, you have only one default account –  **cloud_admin**. As Admin user of this account you are able to view and manage all the physical and virtual resources of the system. However, if you want to divide your virtual resources among numerous users from different groups, or departments, you need to create different accounts.

Only an Admin (system administrator) user can create accounts.

**To create an account**:

1.  Click  **Accounts Management**  >  **Accounts**  >  **Create**.  
    The Create Account dialog box appears.
2.  Enter the following information:
    1.  **Name**  – enter a unique name for the new account.  
        **Note**: The names are  **not**  case sensitive.
    2.  **Description**  [Optional] – enter a description of the new account.
3.  Click  **OK**  to create the new account.  
    The new account is created and appears in the list of accounts.

# Disabling an Account

**To disable an account**:

1.  Go to the **Accounts Management** > **Accounts** > view, and either
    1.  Highlight the row of the enabled account you wish to disable  
        A  **Disable**  button appears in the toolbar, or
    2.  Click on the name of the enabled account you want to disable.  
        The view of the selected account will appear, with a  **Disable**  button in the toolbar,
2.  Click the **Disable**.button.  
    The system disables the account.
    
    **Note**: When the selected account is disabled  
    The  **Enable**  button is available.  
    The  **Delete**  button is available
    
    **Note**: The cloud_admin account cannot be disabled.

# Enabling an Account

**To enable an account**:

1.  Go to the **Accounts Management** > **Accounts** > view, and either
    1.  Highlight the row of the disabled account that you wish to enable  
        An **Enable** button appears in the toolbar, or
    2.  Click on the name of the disabled account you want to enable.  
        The view of the selected account will appear, with an  **Enable** button in the toolbar,
2.  Click the **Enable**.button.  
    The system enables the account.
    
    **Note**: When the selected account is enabled  
    The **Disable** button is available.  
    The **Delete** button is not available
    
    **Note**: The cloud_admin account is always enabled.

# Renaming an Account

**To rename an account**:

1.  Go to the **Accounts Management** > **Accounts** > view, and either
    1.  Highlight the row of the account you wish to rename.  
        A **Rename** button appears in the toolbar, or
    2.  Click on the name of the account you want to rename.  
        The view of the selected account will appear, with a **Rename** button in the toolbar,
2.  Click  **Rename**.  
    The Rename Account window appears.
3.  Make the necessary changes in the account name and description, and click  **OK**.  
    **Note**: The cloud_admin account cannot be renamed.

# Deleting an Account

When you delete an account, you also delete all of its projects and users. Therefore, before deleting an account, make sure that you take into consideration the full implications of this action.

A account must be disabled before it can be deleted.

**To delete an account**:

1.  Go to the **Accounts Management** > **Accounts** > view, and either
    1.  Highlight the row of the account you wish to delete  
        A **Delete** button appears in the toolbar, or
    2.  Click on the name of the account you want to delete.  
        The view of the selected account will appear, with a **Delete** button in the toolbar,
2.  Click the **Delete**.button  
    The system displays a confirmation box.
3.  Click **OK**  to delete the account and all of its projects and users.

**Note**: The cloud_admin account cannot be deleted.

# Viewing a Single Account

On the  **Accounts Management** > **Accounts** view click on the name of a specific account.  
A view of the specific account appears with the following account details:

1.  Summary information
    
    1.  **Projects & Users**  widget - The number of Projects and Users it contains
        
    2.  **Compute**  widget - The amount of VMs, CPU Cores and RAM that have been provisioned for the account
        
    3.  **Networking**  widget - The number of Networks, Floating IPs and Security Groups used in the account
        
    4.  **Storage**  widget - The number of Volumes, Images and Snapshots used in the account
        
2.  Four account actions can be performed from this view:
    
    1.  [**Disable**  an account](https://www.stratoscale.com/knowledge/disabling-an-account)
        
    2.  [**Enable**  an account](https://www.stratoscale.com/knowledge/enabling-an-account)
    3.  [**Rename**  an account](https://www.stratoscale.com/knowledge/renaming-an-account)
    4.  [Connect to the  **Identity Provider**](https://www.stratoscale.com/knowledge/connecting-to-the-identity-provider)
    5.  [**Delete**  an account  
        ](https://www.stratoscale.com/knowledge/deleting-an-account)
        
        Only an Admin user can perform these actions.  
        **Note**: The cloud_admin tenant cannot be renamed, disabled or deleted.
        
3.  Additional information can be found in the three tabs listed below:
    
    1.  [**Projects**](https://www.stratoscale.com/knowledge/working-with-projects)
        
    2.  [**Users**](https://www.stratoscale.com/knowledge/working-with-users)
        
    3.  [**Limits**](https://www.stratoscale.com/knowledge/account-limits)

