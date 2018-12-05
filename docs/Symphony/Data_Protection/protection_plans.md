# Protection Plans

## Overview

The Protection Plan determines the following:

-   The Bank to be used by the Plan
-   The number of versions, or checkpoints, of these resources that should be retained
-   The window during which the Data Protection replication may begin
-   The frequency of the Data Protection replication

The Protection Manager of the Source site creates the Protection Plan.

# Creating a Protection Plan

**To create a Protection Plan**:

1. Click  **Data Protection**  >  **Protection Plans**  >  **Create****.**.

The  **Protection - Protection Plans**  view with the  **Create A Protection Plan**  button appears.

The Create protection plan wizard appears.

2. Enter the following values and click  **Finish**.

**Plan Tab**:

**Name**  – enter a unique name for the Protection Plan.

**Description**  (optional) - enter a description.

**Destination**  - select one of the Protection Banks which defines the cluster where the protected data will be stored. (The "Local" option is reserved for  [creating an Automatic Snapshot Schedule](https://www.stratoscale.com/knowledge/creating-an-automatic-snapshot-schedule)  without replicating the snapshot at some target cluster.)

**Checkpoints (Retention)**  - enter the number of back versions of the data that should be saved.

**Trigger Tab**:

On this tab you define how frequently the Checkpoints will be made.

The first two fields determine the range of time during the day when this replication can begin

**Start time**  - select the hour and AM/PM, the earliest time at which the data replication can begin.

**Window duration**  - select a number from 1-24 to determine how long after the start time it is still permitted to begin this replication.

The next two fields determine the frequency of this replication.

**Recurrence**  - select hourly/daily/weekly/monthly to determine the regularity of the replication

**Every**  - this field fine-tunes the regularity.

# Deleting a Protection Plan

**To delete a Protection Plan**:

1. Click  **Data Protection**  >  **Protection Plans**  > name of the protection plan you want to delete >  **Delete**.

The Delete Plan confirmation message appears.

2. Click  **OK**. The system deletes the plan.

# Protecting a Volume

After you create a volume, you can attach one or more Data Protection Plans to it.

**Note**:You can attach a Data Protection Plan to a Volume only if the volume

is not attached to a VM

or is attached to a VM whose operational status is shutoff

if the attached VM is not shutoff, shutoff the VM before continuing, by following these instructions Stopping a Virtual Machine

**To check if a volume can be protected**:

1. On the  **Virtual Resources - Storage - Volumes**  view, locate the volume which you wish to protect and see if it is attached to a VM. If yes, hover over the name of the VM, the hover help will pop up with the VM's status.

**To protect the volume**:

2. Locate the volume which you wish to protect. Verify in the "Protected" column that it is not protected. Click on the Actions button on its right and select  **Protect**.

The Protect Volume dialog box appears.

3. In the Protection Plans dropdown, add or remove as many protection plans as you wish, and click  **OK**.

The Protected column has a checkmark indicating that the Volume is protected.

**Note**: Use this same method for removing the protection of the Volume.

# Protecting a Virtual Machine

After you create a VM, you can attach one or more Data Protection Plans to it.

**Note**:You can attach a Data Protection Plan to a VM only if its Status is Shutoff.

If its Status is Active, you must first [stop the virtual machine](https://www.stratoscale.com/pages/viewpage.action?pageId=333168). This will change its Status to Shutoff.

The following pages describe how to protect a Virtual machine from the Symphony GUI or from the Symphony CLI:

# Protecting a VM via the Symphony GUI

**To protect a VM via the Symphony GUI**

1.  On the  **Compute - Virtual Machines**  view, locate the VM which you wish to protect. Note that its Protection is not checked and that its Status is "Shutoff".
2.  Click on the Actions icon on its right and select  **Protect**.
    
    The Protect VM dialog box appears.
    
3.  In the Protection Plans dropdown, add or remove as many protection plans as you wish, and click  **OK**.
    
    In the Compute - Virtual Machines view its Protection column is checked, indicating that the VM is protected.  
    **Note**: Use the Protect VM dialog box to also remove the protection of the VM.
    
4.  To Start the Virtual Machine click the Actions icon and then the  **Start**  button.

# Protecting a VM via the Symphony CLI

**To protect a VM via the Symphony CLI**

In the example below, we will protect a VM resource called 'VM-1' with a protection plan called 'Protection_Plan-1'.

1.  Retrieve the ID of the VM,'VM-1'.  
    **Note:** The status of a VM must be 'shutoff' before it can be protected.
    
    Symphony @ cloud_admin/default > **[vm list](https://www.stratoscale.com/knowledge/vm-list)**  -c id -c name -c status

<table class="wrapped confluenceTable"><colgroup><col><col><col></colgroup><tbody><tr><th class="confluenceTh">id</th><th class="confluenceTh">name</th><th class="confluenceTh">status</th></tr><tr><td class="confluenceTd"><span style="color: rgb(255,0,0);">6a73085e-304e-49e8-9e9e-59c0a1c2b4b9</span></td><td class="confluenceTd">VM-1</td><td class="highlight-yellow confluenceTd" data-highlight-colour="yellow">shutoff</td></tr><tr><td class="confluenceTd">c02bfa9a-6ac7-4f27-a98d-11e4d441c10d</td><td class="confluenceTd">VM-2</td><td class="confluenceTd">active</td></tr></tbody></table>

2. Retrieve the ID of the protection plan, 'Protection_Plan-1.

Symphony @ cloud_admin/default > **[protection plans list](https://www.stratoscale.com/knowledge/protection-plans-list)**  -c id -c name -c enabled

<table class="wrapped confluenceTable"><colgroup><col><col><col></colgroup><tbody><tr><th class="confluenceTh">id</th><th class="confluenceTh">name</th><th class="confluenceTh">enabled</th></tr><tr><td class="confluenceTd"><span style="color: rgb(0,0,255);">f705091e-88f6-45bd-8710-f29aa94c0c65</span></td><td class="confluenceTd">Protection_Plan-1</td><td class="confluenceTd">True</td></tr></tbody></table>

3. Protect the VM, 'VM-1' with the protection plan, 'Protection_Plan-1'.

Symphony @ cloud_admin/default > **[protection definitions create](https://www.stratoscale.com/knowledge/protection-definitions-create)** VM  6a73085e-304e-49e8-9e9e-59c0a1c2b4b9 f705091e-88f6-45bd-8710-f29aa94c0c65

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><th class="confluenceTh">Field</th><th class="confluenceTh">Value</th></tr><tr><td class="confluenceTd"><div>id</div><div>post_exec_callback</div><div>plan_id</div><div>resource_id</div><div>created_at</div><div>resource_last_saved</div><div>updated_at</div><div>pre_exec_callback</div><div>project_id</div><div>resource_type</div></td><td class="confluenceTd"><div>c86955ed-897f-4a8f-9648-ebf253a5d9df</div><div>None</div><div><span style="color: rgb(0,0,255);">f705091e-88f6-45bd-8710-f29aa94c0c65</span></div><div><span style="color: rgb(255,102,0);">6a73085e-304e-49e8-9e9e-59c0a1c2b4b9</span></div><div>2018-07-09T12:55:28.253602</div><div>None</div><div>None</div><div>None</div><div>6280747c8af544fd857f442a8e19112e</div><div><span style="color: rgb(0,255,255);">VM</span>&nbsp;&nbsp;</div></td></tr></tbody></table>

4. The VM is now protected.