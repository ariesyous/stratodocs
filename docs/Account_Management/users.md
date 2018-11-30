# User Overview

A user is created as a member of a single account. A user must be assigned to a project within that account in order to be able to access the system.

A user can be assigned to more than one project. The role assigned for each project must be the same as the role assigned to her account.

1.  On the **Accounts Management** > **Accounts**.> <**name of specific account**> view, click the **Users** tab.  
    A list of all of the users in the selected account is displayed.  
    The following information is displayed for each user:
    1.  **Name**
    2.  **Email** address
    3.  Account **Role**
    4.  **Projects** to which the users is assigned
    5.  **Active** status
2.  Three user actions can be performed from this view:
    1.  [**Create** a new **User**](https://www.stratoscale.com/knowledge/creating-a-user)
    2.  [Manage the **Active** status of a user](https://www.stratoscale.com/knowledge/managing-the-active-status-of-a-user)
    3.  [View a single existing user](https://www.stratoscale.com/knowledge/viewing-a-single-user)
3.  When a user is highlighted, four additional actions can be performed:
    1.  [**Assign** a **Project** to a user](https://www.stratoscale.com/knowledge/assigning-a-project-to-a-user)
    2.  [**Modify** a user](https://www.stratoscale.com/knowledge/modifying-a--user)
    3.  [**Set** the **Password** of a user](https://www.stratoscale.com/knowledge/resetting-a-user-password)
    4.  [**Delete** a user](https://www.stratoscale.com/knowledge/deleting-a-user)
        
        Only Tenant_Admin or Admin users can perform these actions.  
        **Note**: The default 'admin' user in the cloud_admin account cannot be modified, have their password set by someone else (But they can [change their own password](https://www.stratoscale.com/knowledge/change-password).) or be deleted.

# Creating a User

To create a new user, you need to be either the Admin (system administrator) user who can add users to any account, or a Tenant Admin user who can add users to the account of which she is in charge.

Users cannot be created from within Symphony, in accounts which are connected to an Identity Provider service.

**To create a user:**

1.  On to the **Account Management** > **Accounts** > view, either
    1.  Highlight the row of the account in which you wish to create a user.  
        A **Create User** button appears in the toolbar, or
    2.  Click on the name of the account in which you wish to create a user,  
        The view of the selected account will appear, together with a **Create User** button in the toolbar of the  **Users**  tab.
2.  Click  **Create User**.  
    The Create User dialog box appears.
3.  Enter the following information (all of the information is required):
    1.  **Username**  – Enter a name. All names in an account must be unique.
    2.  **Email** – Enter the user's email address.
    3.  **Password**  – Enter a password.
    4.  **Validate Password**  – Re-enter the password.
    5.  **Projects**  - Select one or more projects in the account to which you want to assign the User.
    6.  **Role**  – select a  **single**  role from the drop-down list.  
        **Note**: The role assigned here defines both the user's project role and account role.  
        You can choose from one of the following five roles:
        1.  **Member**  – This role grants a user the privileges to view, create and manage virtual resources of the projects to which the user has been assigned
        2.  **Tenant Admin**  – This role grants a user the privileges to view, create and manage all of the projects and users in the Tenant Admin's account, in addition to all of the virtual resources of all of its projects.
        3.  **Protection Manager**  - This role, assigned to a remote user in the context of Disaster Recovery data protection, grants cross-regional access to any data to which this remote user has access.
        4.  **Admin**  - This role grants a user the privileges to view, create and manage all physical entities of the cluster infrastructure, and all virtual resources, projects and users in all of its accounts. When assigned to a remote user, also grants cross-regional access to any data to which this remote user has access.
        5.  **Read-only Admin** - This role grants read-only access to all physical entities of the cluster infrastructure, and all virtual resources, projects and users of all accounts.  
            Click here for more information on roles.
4.  Click  **OK**  to create the new user.  
    The new user is created and appears under the  **Users**  tab of the specific account.

# Managing the Active Status of a User

After you have created a user, the user can log into the system. If you want to prevent the user from logging into the system without deleting the user's account from the system, you can deactivate the user's account.

The users in accounts connected to an Identity Provider service, cannot be deactivated or activated from within Symphony.

**To deactivate a user account:**

1.  On the **Accounts Management** > **Accounts** > <**name of specific account**> > view / **Users** tab, in the **Active** column of the user you wish to deactivate  
    or  
    on the **Accounts Management** > **Accounts** > <**name of specific account**> > **Users** > <**name of specific user**> view, in the **Enabled** field (in the screen header)  
    Notice the toggle button on the blue background. This means that the user is active.
2.  Slide the toggle button to the left.  
    The background turns grey and the user is deactivated.

**To activate a user account**:

1.  Slide the toggle button to the right.  
    The background turns Blue and the user is reactivated.

# Assigning a Project to a User

After creating a user, you can assign additional projects to this user.

**To assign a project to a user**:

1.  Go to the **Account Management** > **Accounts** > <**name of specific account**> view /  **Users** tab, and either
    1.  Highlight the row of the user to which you wish to assign a project.  
        An **Assign Project** button appears in the tab toolbar, or
    2.  Click on the name of the user to which you wish to assign a project.  
        The view of the selected project will appear, with an **Assign Project** button in the toolbar,
2.  Click **Assign Project**.  
    The **Assign Project to User: <name of selected user>** window appears.
3.  Do the following:
    
    1.  Select a **Project** to assign to the user.
        
    2.  Select one of the five project **Roles**.  
        **Note**:
        
        1.  The only role that should be selected is the user's account role.  
            (Before assigning a project to a user go to the **Account Management** > **Accounts** > <**name of specific account**> view / **Users** tab to see the selected user's account role.)
            
        2.  Do not select more than one role.
            
4.  Click **OK**.  
    A message confirming the updating of the user will pop-up in the upper right-hand corner of the screen.  
    The name of the newly assigned project will be displayed:
    1.  In the **Projects** column  
        If you are on the **Account Management** > **Accounts** > <**name of specific account**> view / **Users** tab,
    2.  Under the  **Projects**  tab  
        If you are on the **Account Management** > **Accounts** > <**name of specific account**> > **Users** > <**name of specific user**> view.

# Modifying a User

After creating a user, you can modify its Name, E-mail address and account Role.

The Name and E-mail address of users in accounts connected to an Identity Provider service, cannot be modified from within Symphony. The account Role can be modified from within Symphony.

**To modify a user:**

1.  Go to the **Account Management** > **Accounts** > <**name of specific account**> view / **Users** tab, and either
    1.  Highlight the row of the user which you wish to modify.  
        A **Modify** button appears in the tab toolbar, or
    2.  Click on the name of the user which you wish to modify.  
        The view of the selected user will appear, with a **Modify** button in the toolbar,
2.  Click **Modify**.  
    The **Modify User '**<**name of user**>**'** window appears.
3.  You may do any of the following:
    
    1.  Modify the  **Name**  of the user.  
        **Remember**: The name must be unique within the account and it is not case-sensitive.
        
    2.  Modify the user's  **E-mail**  address.
        
    3.  Select the user's account **Role**.  
        **Note**:
        
        1.  Do not select more than one role.
            
        2.  If you modify the account role, you must also modify the user's project role.  
            Go to the **Account Management** > **Accounts** > <**name of specific account**> > **Users** > <**name of specific User**> view /  **Projects** tab to see the selected user's project role for each of her projects.
            
4.  Click **OK**.  
    A message confirming the updating of the user will pop-up in the upper right-hand corner of the screen.  
    The modifications will be displayed:
    1.  Under the **Users** tab,  
        If you are on the **Account Management** > **Accounts** > <**name of specific account**> view
    2.  In the header of the view,  
        If you are on the **Account Management** > **Accounts** > <**name of specific account**> > **Users** > <**name of specific user**> view.

# Resetting a User Password

Once a user is created, the password can be reset by an Admin user of any account, or a Tenant Admin user of the user's account.

The password of users in accounts connected to an Identity Provider service, cannot be reset from within Symphony.

**Note**:

1.  The Tenant Admin user cannot reset the password of an Admin user or a Read Only Admin user
2.  Any Admin user cannot reset the password of the system admin (Account: cloud_admin, User: admin). Only the system admin herself can  [change her own password](https://www.stratoscale.com/knowledge/change-password).

**To reset a user password**:

1.  Go to the **Account Management** > **Accounts** > <**name of specific account**> view / **Users** tab, and either
    1.  Highlight the row of the user whose password you wish to re-set.  
        A **Set Password** button appears in the tab toolbar, or
    2.  Click on the name of the user whose password you wish to re-set.  
        The view of the selected user will appear, with a **Set Password**  button in the toolbar,
2.  Click **Set Password**.  
    The **Set Password**  window appears.
3.  Do the following:
    
    1.  Enter a  **Password**.
        
    2.  **Validate**  the  **Password**  by re-entering it.
        
4.  Click **OK**.  
    A message confirming the successful resetting of the password will pop-up in the upper right-hand corner of the screen.

# Deleting a User

When deleting a user, this user will no longer have access to Symphony. Deleting a user only removes the user from the system. It does not delete the virtual resources that this user created. Theses resources will still be accessible to all users with access to the projects for which these resources were created.

The users in accounts connected to an Identity Provider service, cannot be deleted from within Symphony.

**To delete a user:**

1.  Go to the **Account Management** > **Accounts** > <**name of specific account**> view / **Users** tab, and either
    1.  Highlight the row of the user who you wish to delete.  
        A **Delete** button appears in the tab toolbar, or
    2.  Click on the name of the user who you wish to delete.  
        The view of the selected user will appear, with a **Delete** button in the toolbar,
2.  Click **Delete**.  
    The **Delete User** confirmation window appears.
3.  Click **OK**.  
    A message confirming the deletion of the user project will pop-up in the upper right-hand corner of the screen.  
    **  
    Note**: You cannot delete the default 'admin' user in the cloud_admin account.

# Viewing a Single User

On the  **Accounts Management** > **Accounts** > <**name of specific account**> view / **Users** tab, click on the name of a specific user.  
A view of the specific user appears with the following details:

1.  Summary information
    
    1.  **Name**  of the user
        
    2.  **E-mail** address of the user
        
    3.  **Active** status of the user
        
    4.  User's **Account** and (**account role**)
    5.  **ID**  of the user
        
2.  Five user actions can be performed from this view:
    
    1.  [**Assign** a **Project** to a user](https://www.stratoscale.com/knowledge/assigning-a-project-to-a-user)
    2.  [**Modify** the name, e-mail address and account role of a user](https://www.stratoscale.com/knowledge/modifying-a--user)
    3.  [**Reset** the **Password** of a user](https://www.stratoscale.com/knowledge/resetting-a-user-password)
    4.  [**Delete** a user](https://www.stratoscale.com/knowledge/deleting-a-user)
    5.  [Manage the **Active**  status of a  user](https://www.stratoscale.com/knowledge/managing-the-active-status-of-a-user)
        
        Only Tenant_Admin or Admin users can perform these actions.  
        **Note**: The default 'admin' user in the cloud_admin account cannot be modified, be deleted, or have its password set by someone else. (But they can [change their own password](https://www.stratoscale.com/knowledge/change-password).)
        
3.  Two additional user actions can be performed from the Projects tab:
    
    1.  [Manage the user's project role](https://www.stratoscale.com/knowledge/managing-the-project-role-of-the-user)
        
    2.  [Remove a project from a user](https://www.stratoscale.com/knowledge/removing-a-project-from-a-user)

# Managing the Project Role of the User

After assigning a project and project role to a user, you may want to change the role.

**Note**:

1.  Only one role should be selected.
2.  The user's project role must be identical to the user's account role. Therefore, changing in the project role requires making the same  [change in the account role](https://www.stratoscale.com/knowledge/modifying-a--user).

**To modify a user's project role**:

1.  Go to the **Account Management** > **Accounts** > <**name of specific account**> **Users** <**name of specific user**> view /  **Projects** tab, and highlight the row of the project whose role you wish to modify.  
    A **Manage Roles** button appears in the tab toolbar.
2.  Click **Manage Roles**.  
    The **Manage Roles**  window appears.
3.  Modify the **Role** of the user.  
    **Remember**:  
    Do not select more than one role.  
    If you modify the project role, you must also modify the user's account role.
    
4.  Click **OK**.  
    A message confirming the updating of the user will pop-up in the upper right-hand corner of the screen.  
    The modified role will be displayed in the roles column of the list of projects.

# Removing a Project from a User

**To remove a project from a user:**

1.  Go to the **Account Management** > **Accounts** > <**name of specific account**> **Users** <**name of specific user**> view /  **Projects** tab, and highlight the row of the project whose role you wish to remove.  
    A **Delete** button appears in the tab toolbar.
2.  Click **Remove**.  
    The Remove Project confirmation window appears.
3.  Click **OK**.  
    The list of project will update accordingly, removing this project from the specific user.

