
# External Identity Provider 

## Overview

Symphony users can be accessed from an LDAP compatible Identity Provider such as MS Active Directory or OpenLDAP. This is done by first connecting the Symphony account to the LDAP domain. Connection with the Identity Provider must be configured independently for each Symphony account.

Once an account becomes connected to LDAP, the newly available Active Directory users must be assigned Symphony Account Roles and Projects. This can be done either through the CLI commands or via the GUI.

Each of these users will now be able to login to Symphony with their Active Directory name and password.

# Connecting to the Identity Provider

**To connect an account to the MS Active Directory Identity Provider:**

**Note:**  If you want to connect the account to only some of the users in the Active Directory, then first tag their names or create an ad-hoc group for them. This allows you to use the filters to select only those users that should be connected to the Symphony account.

1.  Go to the **Accounts Management** > **Accounts** > view, and either
    1.  Highlight the row of the account which you wish to connect to the Identity Provider  
        An **Identity Provider** button appears in the toolbar, or
    2.  Click on the name of the account you want to connect to the Identity Provider  
        The view of the selected account will appear, with an **Identity Provider** button in the toolbar,
2.  Click the **Identity Provider** button.  
    The  **Configure Identity Provider** dialog pops-up.
3.  Enter the following information:
    1.  **Connection Details** of the MS Active Directory Server
        1.  **Server** - Enter the address of the MS Active Directory Server expressed either as a URL or DNS name. For example: 10.11.12.13 or 'mydomain.com'.
        2.  **Secure** - Check this box if you want the address to be secure
        3.  **Port** - The reserved port is 389 if the connection is not secure, 1389, if the connection is secure.
        4.  **User DN** - This is the distinguished name of a user through which one can gain access to Active Directory Server. For example: 'cn=ldap,cn=Users,dc=myorganization,dc=com'. This user need not be an administrator or member of the domain. Should be a read-only user.
        5.  **Password** - This is the MS Active Directory password of the User DN.
    2.  **LDAP Parameters**  - All parameters are expressed in the LDAP syntax.
        
        In the sample LDAP Parameter input below, the input does not include the quote marks at the beginning and end of each input.
        
        The input for the User Filter and Group Filter parameters  **does**  include the parentheses.
        
        1.  **Domain** - This is the domain of the customer in the Active Directory.  
            For example: "dc=myorganization,dc=com"
        2.  **User Tree DN** - This defines the location in the Active Directory in which the users will be scanned.  
            For example: "cn=Users,dc=myorganization,dc=com"
        3.  **User Filter** - This filters the users scanned in the User Tree.  
            For example: "(name=strato-*)" would search in the User Tree for any user beginning with 'strato-'.  
            Or "(memberOf=cn=grp-stratoldap,cn=Users,dc=myorganization,dc=com)" would search for any user who belongs to the ad-hoc group created in the Active Directory, 'cn=grp-stratoldap,cn=Users,dc=myorganization,dc=com'.
        4.  **Group Tree** - This defines the location in the Active Directory in which the groups will be scanned.  
            For example: "cn=Users,dc=myorganization,dc=com"
        5.  **Group Filter**  - This filters the groups scanned in the Group Tree.  
            For example: "(name=grp-*)" would search for any group beginning with 'grp-'.
            
            Example of a fully configured connection between a Symphony account and the MS Active Directory, Identity Provider:  
            ![](https://www.stratoscale.com/wp-content/uploads/2017-12-03_Configure20Identity20Provider20dialog_LDAP20Parameter20Filters20with20parentheses.jpg)
            
4.  Click **OK**
    1.  The selected account becomes connected to the MS Active Directory.
    2.  The users matching the filters described above will appear as users of the selected account together with their Active Directory password and email address. Their password and email address  **cannot**  be modified within Symphony.
        

Assigning Account and Project Roles

Before these users will be able to login to Symphony, you must first assign each of them:

1.  An account role
2.  A project and its role

For a detailed description of how to assign these roles to Active Directory users see the sections below:

-   [Assigning Roles to an Active Directory User via the Symphony CLI](https://www.stratoscale.com/knowledge/assigning-roles-to-an-active-directory-user-via-the-symphony-cli)
-   [Assigning Roles to an Active Directory User via the Symphony GUI](https://www.stratoscale.com/knowledge/assigning-roles-to-an-active-directory-user-via-the-symphony-gui)

# Assigning Roles to an Active Directory User via the Symphony CLI

The following CLI commands are recommended to assign the Account and Project 'Admin' roles to a user made available to Symphony via Active Directory:

**Note**: In this use case we are assuming that the Symphony account, 'new_account', which was connected to a domain in Active Directory, already contains the project, 'new_project'.

1.  Check the user list to locate the new user made available to Symphony via Active Directory. Note its domain ID.
    
    **Command:**  Symphony @ cloud_admin/default > [user list](https://www.stratoscale.com/knowledge/user-list)  -c id -c name -c domain_id  
    **Returns:**
<table class="wrapped confluenceTable"><colgroup><col><col><col></colgroup><tbody><tr><td class="confluenceTdhighlight-grey confluenceTd" colspan="1" data-highlight-colour="grey"><strong>id</strong></td><td class="confluenceTdhighlight-grey confluenceTd" colspan="1" data-highlight-colour="grey"><strong>name</strong></td><td class="confluenceTdhighlight-grey confluenceTd" colspan="1" data-highlight-colour="grey"><strong>domain_id</strong></td></tr><tr><td class="confluenceTd">c8a63b29558d4765a6cd78760729a2f7</td><td class="confluenceTd">new_user</td><td class="confluenceTd">2d27e2fe6d8a4398b901c4d84c478777</td></tr><tr><td colspan="1" class="confluenceTd">1c90791e14de48389778a00f1e984f16</td><td colspan="1" class="confluenceTd">maestro</td><td colspan="1" class="confluenceTd">default</td></tr><tr><td colspan="1" class="confluenceTd">admin</td><td colspan="1" class="confluenceTd">admin</td><td colspan="1" class="confluenceTd"><span>default</span></td></tr></tbody></table>

2. Verify that user, 'new_user', from the Active Directory list, does not already appear in another Symphony account. (The same Symphony user name can appear in more than one account even though their ID's will be unique.)

**Command:**  Symphony @ cloud_admin/default > [user list](https://www.stratoscale.com/knowledge/user-list) --name new_user -c id -c name -c domain_id  
**Returns:**
<table class="wrapped confluenceTable"><colgroup><col><col><col></colgroup><tbody><tr><td class="highlight-grey confluenceTd" colspan="1" data-highlight-colour="grey"><strong>id</strong></td><td class="highlight-grey confluenceTd" colspan="1" data-highlight-colour="grey"><strong>name</strong></td><td class="highlight-grey confluenceTd" colspan="1" data-highlight-colour="grey"><strong>domain_id</strong></td></tr><tr><td class="confluenceTd">c8a63b29558d4765a6cd78760729a2f7</td><td class="confluenceTd">new_user</td><td class="confluenceTd">2d27e2fe6d8a4398b901c4d84c478777</td></tr></tbody></table>

3. List the domains with their IDs and names.

**Command:** Symphony @ cloud_admin/default > [domain list](https://www.stratoscale.com/knowledge/domain-list)  -c id -c name  
**Returns**:
<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><td class="highlight-grey confluenceTd" colspan="1" data-highlight-colour="grey"><strong>id</strong></td><td class="highlight-grey confluenceTd" colspan="1" data-highlight-colour="grey"><strong>name</strong></td></tr><tr><td class="confluenceTd">2d27e2fe6d8a4398b901c4d84c478777</td><td class="confluenceTd">new_account</td></tr><tr><td colspan="1" class="confluenceTd">default</td><td colspan="1" class="confluenceTd">cloud_admin</td></tr></tbody></table>

4. List the projects with their IDs, names and domains.

**Command:** Symphony @ cloud_admin/default > [project list](https://www.stratoscale.com/knowledge/project-list)  -c id -c name -c domain_name  
**Returns:**
<table class="wrapped confluenceTable"><colgroup><col><col><col></colgroup><tbody><tr><th class="confluenceTh"><strong>id</strong></th><th class="confluenceTh"><strong>name</strong></th><th class="confluenceTh"><strong>domain_name</strong></th></tr><tr><td class="confluenceTd">1569c28e3a344ee2b3989640499b8eca</td><td class="confluenceTd">new_project</td><td class="confluenceTd">new_account</td></tr><tr><td class="confluenceTd">4bd79a2fa9574af2a4b9a7a87195f144</td><td class="confluenceTd">default</td><td class="confluenceTd">cloud_admin</td></tr></tbody></table>

5. List all available roles in Symphony.

**Command:** Symphony @ cloud_admin/default > [role list](https://www.stratoscale.com/knowledge/role-list)  
**Returns:**
<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><th class="confluenceTh"><strong>id</strong></th><th class="confluenceTh"><strong>name</strong></th></tr><tr><td class="confluenceTd">admin</td><td class="confluenceTd">admin</td></tr><tr><td class="confluenceTd">af822120650841b895141ea4ad7d3427</td><td class="confluenceTd">service</td></tr><tr><td class="confluenceTd">protection_manager</td><td class="confluenceTd">protection_manager</td></tr><tr><td class="confluenceTd">read_only_admin</td><td class="confluenceTd">read_only_admin</td></tr><tr><td class="confluenceTd">tenant_admin</td><td class="confluenceTd">tenant_admin</td></tr><tr><td class="confluenceTd">_member_</td><td class="confluenceTd">member</td></tr></tbody></table>

6. Check if 'new_user' has already been assigned a role in the domain, 'new_account'.

**Command:** Symphony @ cloud_admin/default > [domain list-roles-on-domain](https://www.stratoscale.com/knowledge/domain-list-roles-on-domain)2d27e2fe6d8a4398b901c4d84c478777 c8a63b29558d4765a6cd78760729a2f7  
**Returns:**
<table class="wrapped confluenceTable"><colgroup><col></colgroup><tbody><tr><th class="confluenceTh"><span>value</span></th></tr><tr><td class="confluenceTd">tenant_admin</td></tr></tbody></table>

7. If already assigned a role in the domain, 'new_account', other than 'admin' remove this role from 'new_user'.  
Else, skip to command #8.

**Command:** Symphony @ cloud_admin/default > [domain revoke-role](https://www.stratoscale.com/knowledge/domain-revoke-role)  2d27e2fe6d8a4398b901c4d84c478777 c8a63b29558d4765a6cd78760729a2f7 tenant_admin  
**Returns:**
<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><th class="confluenceTh">Field</th><th class="confluenceTh">Value</th></tr><tr><td class="confluenceTd">value</td><td class="confluenceTd">Success</td></tr></tbody></table>

8. Check if 'new_user' has already been assigned a role in the project, 'new_project'.

**Command:** Symphony @ cloud_admin/default > [project list-roles-on-project](https://www.stratoscale.com/knowledge/project-list-roles-on-project)1569c28e3a344ee2b3989640499b8eca c8a63b29558d4765a6cd78760729a2f7  
**Returns:**
<table class="wrapped confluenceTable"><colgroup><col></colgroup><tbody><tr><th class="confluenceTh">value</th></tr><tr><td class="confluenceTd">tenant_admin</td></tr></tbody></table>

9. If already assigned a role in 'new_project' other than 'admin', remove this role from 'new_user'.  
Else, skip to command #10.

****Command:**** Symphony @ cloud_admin/default > [project revoke-role](https://www.stratoscale.com/knowledge/project-revoke-role)  1569c28e3a344ee2b3989640499b8eca c8a63b29558d4765a6cd78760729a2f7 tenant_admin  
**Returns:**

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><th class="confluenceTh">Field</th><th class="confluenceTh">Value</th></tr><tr><td class="confluenceTd">value</td><td class="confluenceTd">Success</td></tr></tbody></table>

10. Assign the 'admin' role to 'new_user' in the domain, 'new_account'.

**Command:** Symphony @ cloud_admin/default > [domain grant-role](https://www.stratoscale.com/knowledge/domain-grant-role)  2d27e2fe6d8a4398b901c4d84c478777 c8a63b29558d4765a6cd78760729a2f7 admin  
****Returns:****
<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><th class="confluenceTh">Field</th><th class="confluenceTh">Value</th></tr><tr><td class="confluenceTd">value</td><td class="confluenceTd">Success</td></tr></tbody></table>

11. Assign the 'admin' role to 'new_user' in the project, 'new_project'.

**Command:** Symphony @ cloud_admin/default > [project grant-role](https://www.stratoscale.com/knowledge/project-grant-role)  1569c28e3a344ee2b3989640499b8eca c8a63b29558d4765a6cd78760729a2f7 admin  
****Returns:****
<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><th class="confluenceTh">Field</th><th class="confluenceTh">Value</th></tr><tr><td class="confluenceTd">value</td><td class="confluenceTd">Success</td></tr></tbody></table>

12. Verify that the role of 'new_user' in the domain, 'new_account', is 'admin'.

**Command:** Symphony @ cloud_admin/default > [domain list-roles-on-domain](https://www.stratoscale.com/knowledge/domain-list-roles-on-domain)2d27e2fe6d8a4398b901c4d84c478777 c8a63b29558d4765a6cd78760729a2f7  
****Returns:****
<table class="wrapped confluenceTable"><colgroup><col></colgroup><tbody><tr><th class="confluenceTh">value</th></tr><tr><td class="confluenceTd">admin</td></tr></tbody></table>

13. Verify that the role of 'new_user' in 'new_project' is 'admin.

**Command:** Symphony @ cloud_admin/default > [project list-roles-on-project](https://www.stratoscale.com/knowledge/project-list-roles-on-project)1569c28e3a344ee2b3989640499b8eca c8a63b29558d4765a6cd78760729a2f7  
****Returns:****
<table class="wrapped confluenceTable"><colgroup><col></colgroup><tbody><tr><th class="confluenceTh">value</th></tr><tr><td class="confluenceTd">admin</td></tr></tbody></table>

# Assigning Roles to an Active Directory User via the Symphony GUI

The following GUI actions are recommended to assign Symphony Account and Project roles to a user made available to Symphony via Active Directory:

**Note**: In this use case we are assuming that the Symphony account which was connected to a domain in Active Directory, already contains the new project.

1.  Locate the new user made available to Symphony via Active Directory.
    
    1.  On the **Accounts Management** > **Accounts**.> <**name of specific account**> view, click the **[Users](https://www.stratoscale.com/knowledge/working-with-users)** tab. The list of users for that account will appear.
        
    2.  Highlight the user.
2.  Set the user's account role to 'Admin'.
    
    1.  Click on the  **Modify**  button. This accesses the  **[Modify User](https://www.stratoscale.com/knowledge/modifying-a--user)**  dialog box.
        
    2.  Set the account role to 'Admin', for example, and click  **OK**. The user's account role now displays 'Admin'.
        
3.  Assign a Project to the user with the project role of 'Admin'.
    
    1.  Click on the  **Assign Project**  button. This accesses the  **[Assign Project to User](https://www.stratoscale.com/knowledge/assigning-a-project-to-a-user)** dialog box.
        
    2.  Select a project.
        
    3.  Select the 'Admin' role, for example, and click  **OK**.
        
    4.  Click on the name of the project. This displays the details about the project assigned to the user. Note that the user's project role is now 'Admin'.

