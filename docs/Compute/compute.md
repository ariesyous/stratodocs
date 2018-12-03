# Compute Project Overview

Symphony enables you to create, configure, run, access, and manage Virtual Machines (VMs). These can be managed via the GUI, CLI, or via the AWS-compatible API endpoints along with the Symphony API endpoints.

# Creating a Virtual Machine

When creating a virtual machine in Symphony, its operating system can be uploaded in one of two ways:

-   Directly from the image from which it was created.
-   Via an Installation ISO file. This option has two flavors:
    -   A single installation file. This is the case when creating a VM with an Ubuntu OS. A single ISO file includes the entire OS and all necessary drivers.
    -   Two installation files. This is case when creating a VM with a Windows OS. The main ISO includes the entire OS and drivers except for the Storage and Network drivers which are found on the second, VirtIO ISO file.

# Creating a VM from an Image

Before creating a VM from an Image, you must have already defined in your system at least one guest network and one image.

**To create a Virtual Machine**:

1. Go to the  **Main Navigation**  pane and select  **Create VM**  from the  **Create**  option.

![](https://www.stratoscale.com/wp-content/uploads/Main20Navigation20Pane20-20Create20VM20DP28129.jpg)

– or -

On the  **Compute - Virtual Machines**  view, click the  **Create VM**  button.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Create20VM20from20VM20List20Button2061220DP.jpg)

The  **Create VM**  wizard appears, open to its first step, the  **Details**  step:

![](https://www.stratoscale.com/wp-content/uploads/Create20VM20-20Dialog20120DP.jpg)

2. Enter the information requested on Step 1 of the Create VM wizard:

**Name**  – enter a name for the new VM.

**Tags**  – enter tags for the new VM. These tags will enable you to define VM Placement Rules later on.

Click  **Next**.

![](https://www.stratoscale.com/wp-content/uploads/Create20VM20-20Dialog20220DP.jpg)

The second step of the  **Create VM**  wizard,  **Configurations**, appears.

3. Enter the information requested on Step 2 of the Create VM wizard:

-   **VM OS**  - In this field you must decide from where the virtual machine's Operating System (OS) will be uploaded. Since you are creating a VM from an image the Image radio button should be checked. This causes the Image field to be displayed.
-   **Image**  - Select the desired image from the drop-down menu. When your VM will be created it will already have its OS built into it. All you will have to do is start the VM and it will be ready for use.
-   **Network**  - select the desired network from the drop-down menu.
-   **CPUs**  - set the required numbers of CPU cores.
-   **Disk**- set a size in MB for the boot volume that is created upon the creation of a VM. The default size is automatically adjusted to the virtual size of the selected image. The disk size you enter should be equal to or larger than the size of the image you selected for the VM. If you enter a lower size, the VM will not be able to run.
    
    **Note**: If the file system in the image is self-expanding to the full volume size on the first boot, set the size to the desired virtual size, which must be larger than the size provided by the image.
    
-   **Memory**  - set the required memory size.
-   **Profile**  – select from the drop-down list a resource allocation profile for the VM. The profile determines how much CPU and Memory will be allocated to the VM when there are not enough resources to satisfy all the demands of the running VMs in a certain node, but there are resources above the bare minimum for all VMs. There are 3 built-in profiles:
    -   **Reserved** - All of the VM’s provisioned memory and CPU are always available. This type of VM is recommended for performance critical tasks. However, this profile leads to sub-optimal resource utilization, since the VMs will usually not use all the reserved resources.
    -   **On Demand** - Most of the VM’s provisioned memory and a minimal amount of CPU are always available. The rest will be allocated on-demand if there are available non-reserved resources. This type of VM is the default recommendation for standard tasks.
    -   **Spot** - Only a minimal amount of the VM’s provisioned memory and CPU are always available. The rest will be allocated on-demand if there are available non-reserved resources. Since this type of VM exists only on an ad hoc basis, it is recommended for non-critical tasks.
        
-   **High Availability**  - if this VM must always be operationally available check the High Availability checkbox. This will cause the VM to automatically restart if it is shutdown due to a malfunction.

4. Click  **Finish**  to create the new VM.

A new VM is created and it appears in the Compute - Virtual Machines view in its default status Shutoff.

![](https://www.stratoscale.com/wp-content/uploads/Create20VM20-20Success20DP.jpg)

When a VM is created, a boot volume is automatically created for it. This boot volume is a copy of the VM image.

![](https://www.stratoscale.com/wp-content/uploads/Create20VM20-20Boot20Volume2061220DP.jpg)

5. To Start the VM click on the vertical Actions ellipsis at the end of the new VM's row and select  **Start**. The VM is now ready to run.

![](https://www.stratoscale.com/wp-content/uploads/Create20VM20-20Start20VM2061220DP.jpg)

# Creating a VM from an Ubuntu ISO File

Before creating a VM from an Ubuntu ISO file you must have already defined in your system at least one guest network and one Installation image for an Ubuntu ISO file. (Any other similar ISO file may work provided that it contains all the functionality, including network and storage drivers, in a single ISO file.)

**To create a Virtual Machine**:

1. Go to the  **Main Navigation**  pane and select  **Create VM**  from the  **Create**  option.

![](https://www.stratoscale.com/wp-content/uploads/Main20Navigation20Pane20-20Create20VM20DP28329.jpg)

– or -

On the  **Compute - Virtual Machines**  view, click the  **Create VM**  button.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Ubuntu20edit20DP28229.jpg)

The  **Create VM**  wizard appears, open to its first step, the Details step:

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Create20VM20from20Ubuntu20dialog2012061220DP.jpg)

2. Enter the information requested on Step 1 of the Create VM wizard:

**Name**  – enter a name for the new VM.

**Tags**  – enter tags for the new VM. These tags will enable you to define VM Placement Rules later on.

Click  **Next**

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Create20VM20from20Ubuntu20dialog2022061220DP28629.jpg)

The second step of the Create VM wizard, Configurations, appears.

3. Enter the information requested on Step 2 of the Create VM wizard:

-   **VM OS**  - In this field you must decide from where the virtual machine's Operating System (OS) will be uploaded. Since we are creating a VM from an Ubuntu ISO file, the ISO radio button should be checked. This causes the Installation ISO and Additional ISO fields to be displayed instead of the Image field, as shown below:

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Create20VM20from20Ubuntu20dialog2022061220DP202822928229.jpg)

-   **Installation ISO**  - This field is for selecting the Installation image for the Ubuntu ISO file (or any other parallel ISO file). This file will upload the Ubuntu OS to the VM from the ISO file, after the VM has been created, started and connected to the console of the Virtual Machine. Select the Installation ISO image.
-   **Additional ISO**  - This is for adding another ISO image to the original installation image. When using a Ubuntu (or similar) ISO file, this field is unneccessary and should be left empty.
-   **Network**  - select the desired network from the drop-down menu.
-   **CPUs**  - set the required numbers of CPU cores.
-   **Disk**- set a size in MB for the boot volume that is created upon the creation of a VM. The default size is automatically adjusted to the virtual size of the selected image. The disk size you enter should be equal to or larger than the size of the image you selected for the VM. If you enter a lower size, the VM will not be able to run.
    
    **Notes**:
    
    -   The current Ubuntu installation requires at least 8 GB of disk space.
    -   If the file system in the image is self-expanding to the full volume size on the first boot, set the size to the desired virtual size, which must be larger than the size provided by the image.
-   **Memory**  - set the required memory size.
-   **Profile**  – select from the drop-down list a resource allocation profile for the VM. The profile determines how much CPU and Memory will be allocated to the VM when there are not enough resources to satisfy all the demands of the running VMs in a certain node, but there are resources above the bare minimum for all VMs. There are 3 built-in profiles:
    -   **Reserved** - All of the VM’s provisioned memory and CPU are always available. This type of VM is recommended for performance critical tasks. However, this profile leads to sub-optimal resource utilization, since the VMs will usually not use all the reserved resources.
    -   **On Demand** - Most of the VM’s provisioned memory and a minimal amount of CPU are always available. The rest will be allocated on-demand if there are available non-reserved resources. This type of VM is the default recommendation for standard tasks.
    -   **Spot** - Only a minimal amount of the VM’s provisioned memory and CPU are always available. The rest will be allocated on-demand if there are available non-reserved resources. Since this type of VM exists only on an ad hoc basis, it is recommended for non-critical tasks.
        
-   **High Availability**  - if this VM must always be operationally available check the High Availability checkbox. This will cause the VM to automatically restart if it is shutdown due to a malfunction.

4. Click  **Finish**  to create the new VM.

A new VM is created and it appears in the  **Compute - Virtual Machines**  view in its default status  **Shutoff**.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Create20VM20from20Ubuntu20VM20Created2061220DP2028229.jpg)

When creating a VM by installing from an ISO file, the boot volume is not automatically created. You must first start the VM and then connect directly to it, in order to install its OS from the ISO and create its boot volume.

5. To Start the VM click on the vertical Actions ellipsis at the end of the new VM's row and select  **Start**.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Create20VM20from20Ubuntu20VM20Start20button2061220DP2028229.jpg)

This changes the status of the VM to Active.

6. To Connect to the VM console click on the vertical Actions ellipsis at the end of the new VM's row and select  **Connect**.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Create20VM20from20Ubuntu20VM20Connect20button2061220DP2028229.jpg)

This will bring you directly to the Ubuntu Install screen.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_16_VNC_Install20Ubuntu28129.jpg)

7. Run the OS installation program in its entirety, including "restarting" if so requested.

Your VM is now ready to run.

8. Post-Installation Cleanup

When creating a VM with an "Installation ISO", two volumes are created: the boot volume and the volume with the Installation from ISO image, labeled " ISO volume", as shown below.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Create20VM20Volumes20620DP.jpg)

To remove the volume labeled "ISO volume", do the following:

1.  [Stop the VM to which the volume is attached](https://www.stratoscale.com/knowledge/stopping-a-virtual-machine)

2.  [Detach the Volume from its VM](https://www.stratoscale.com/knowledge/detaching-a-volume-from-a-virtual-machine)

3.  [Delete the Volume](https://www.stratoscale.com/knowledge/deleting-a-volume)

# Creating a VM from a Windows ISO File and a VirtIO ISO File

Before creating a VM from a Windows ISO file and a VirtIO ISO file you must have already defined in your system at least one guest network, and two Installation images, one for for a Windows ISO file and one for the VirtIO ISO network and storage drivers. (You can upload the VirtIO ISO from  https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.iso.)

**To create a Virtual Machine**:

1. Go to the  **Main Navigation**  pane and select  **Create VM**  from the  **Create**  option.

![](https://www.stratoscale.com/wp-content/uploads/Main20Navigation20Pane20-20Create20VM20DP28429.jpg)

– or -

On the Compute - Virtual Machines view, click the Create VM button.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Ubuntu20edit20DP28129.jpg)

The Create VM wizard appears, open to its first step, the Details step:

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_4_Create20VM20wizard_Step201.jpg)

2. Enter the information requested on Step 1 of the Create VM wizard:

**Name**  – enter a name for the new VM.

**Tags**  – enter tags for the new VM. These tags will enable you to define VM Placement Rules later on.

Click  **Next**.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Create20VM20from20Ubuntu20dialog2022061220DP28529.jpg)

The second step of the Create VM wizard, Configurations, appears.

3. Enter the information requested on Step 2 of the Create VM wizard:

-   **VM OS**  - In this field you must decide from where the virtual machine's Operating System (OS) will be uploaded. Since we are creating a VM from an Installation ISO, the ISO radio button should be checked. This causes the Installation ISO and Additional ISO fields to be displayed instead of the Image field, as shown below:

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Create20VM20from20win20iso20dialog20220empty2061220DP.jpg)

-   **Installation ISO**  - This field is for selecting an installation files which uploads the OS to the VM from an ISO file. This occurs only after the VM has been created, started and connected to the console of the Virtual Machine. This triggers the upload of the operating system from the ISO device. Select the Installation Windows ISO image.
-   **Additional ISO**  - This is for adding another ISO image to the original installation image. This is the case by Windows, the main Windows ISO contains all of the OS functionality required by the VM except for the storage and network drivers. Select here the VirtIO ISO installation image installing these drivers.
-   **Network**  - select the desired network from the drop-down menu.
-   **CPUs**  - set the required numbers of CPU cores.
-   **Disk**- set a size in GB for the boot volume that is created upon the creation of a VM. The default size is automatically adjusted to the virtual size of the selected image. The disk size you enter should be equal to or larger than the size of the image you selected for the VM. If you enter a lower size, the VM will not be able to run. When installing from a Windows ISO your disk size must be at least 20 GB.
    
    **Note**: If the file system in the image is self-expanding to the full volume size on the first boot, set the size to the desired virtual size, which must be larger than the size provided by the image.
    
-   **Memory**  - set the required memory size. When installing from a Windows ISO the memory should be at least 2 MIB.
-   **Profile**  – select from the drop-down list a resource allocation profile for the VM. The profile determines how much CPU and Memory will be allocated to the VM when there are not enough resources to satisfy all the demands of the running VMs in a certain node, but there are resources above the bare minimum for all VMs. There are 3 built-in profiles:
    -   **Reserved** - All of the VM’s provisioned memory and CPU are always available. This type of VM is recommended for performance critical tasks. However, this profile leads to sub-optimal resource utilization, since the VMs will usually not use all the reserved resources.
    -   **On Demand** - Most of the VM’s provisioned memory and a minimal amount of CPU are always available. The rest will be allocated on-demand if there are available non-reserved resources. This type of VM is the default recommendation for standard tasks.
    -   **Spot** - Only a minimal amount of the VM’s provisioned memory and CPU are always available. The rest will be allocated on-demand if there are available non-reserved resources. Since this type of VM exists only on an ad hoc basis, it is recommended for non-critical tasks.
        
-   **High Availability**  - if this VM must always be operationally available check the High Availability checkbox. This will cause the VM to automatically restart if it is shutdown due to a malfunction.

4. Click  **Finish**  to create the new VM.

A new VM is created and it appears in the  **Compute - Virtual Machines**  view in its default status  **Shutoff**

![](https://www.stratoscale.com/wp-content/uploads/Create20VM20from20Windows20VM20VM20List2020620DP.jpg)

When creating a VM by installing from an ISO file, the boot volume is not automatically created. You must first start the VM and then connect directly to it, in order to install its OS from the ISO and create its boot volume.

5. To Start the VM click on the vertical Actions ellipsis at the end of the new VM's row and select  **Start**.

![](https://www.stratoscale.com/wp-content/uploads/Create20VM20from20Windows20VM20Start20button20620DP.jpg)

This changes the status of the VM to Active.

6. To Connect directly to the VM click on the vertical Actions ellipsis at the end of the new VM's row and select  **Connect**.

![](https://www.stratoscale.com/wp-content/uploads/Create20VM20from20Windows20VM20Connect20button20620DP.jpg)

This will bring you directly to the Windows Setup screen.

**Note**: The following instructions describe the process for creating a VM by Installing Windows 10 from an ISO file. There may differences in the installation process from other versions of Windows especially concerning the setting up of the storage and network drivers from the additional VirtIO ISO file.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_21_VNC_Pre-Install20Windows28129.jpg)

7. Enter your locale information. Click  **Next**  and  **Install now**  on the next screen. The Windows OS installation begins.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_22_VNC_Install20Windows.jpg)

7. The setup progam will shortly inform you that it cannot find a drive on which to install Windows because there is no storage driver. Do the following to locate the storage driver and drive:

a. Click on the Load Driver link. A "Load Driver" dialog pops-up.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_23_VNC_No20storage20driver.jpg)

b. Click on the Browse button of the Load Driver dialog. A browser pops-up.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_24_VNC_Load20driver28129.jpg)

c. In the "Browse for Folder" broswer double-click on the virt-io-win ISO.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_25_VNC_Browse20for20Folder_Drive.jpg)

d. In the "Browse for Folder" browser double-click on the "viostor" folder.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_26_VNC_Browse20for20Folder_viostor.jpg)

e. In the "Browse for Folder" broswer double click on the "W10" folder (Windows 10) and then select the "amd64" folder. Click OK. You have now identified the folder in which the Windows 10 storage driver is located.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_27_VNC_Browse20for20Folder_w10-amd64.jpg)

f. This storage driver now appears on the "Select the driver to install" pane. Click Next.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_28_VNC_Select20the20driver20to20Install.jpg)

g. Now that the storage driver has been installed, the VMs boot volume has been identified. Click Next.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_29_VNC_Where20to20install20Windows.jpg)

h. The setup program is now installing Windows on the selected boot volume of the VM.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_30_VNC_Installing20windows.jpg)

After Installation is completed and a few more set up screens will display, you will eventually see the Windows 10 desktop.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_31_VNC_Windows20Desktop_no20Internet28129.jpg)

# Starting a Virtual Machine

By default, after a VM is created, it is in Shutoff state. To activate the VM, you need to run it.

**To run a VM**:

1. On the Compute view Virtual Machines widget, locate your VM, click its Action icon, click  **Start**.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Start20VM20Button206120DP.jpg)

The Status on the selected VM changes to spawning, and a message box pops up in the top right hand corner with the message "VM powering on".

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Start20VM20in20process206120DP28129.jpg)

The selected VM is automatically placed on one of the nodes in the cluster, it starts running, and its status changes from  **Shutoff**  to  **Active**.

# Connecting to an Instance

You can connect to an instance and access it using VNC.

**To connect to an instance**:

1.  In the **Compute > Instances** screen **List** view, select the instance to which you want to connect.
2.  Click the **Connect** button.  
    The VNC window appears.
3.  Click the **Send Ctrl-Alt-Del** button.  
    The Instance appears, waiting to be logged into.

# Stopping a Virtual Machine

**To stop a VM**:

1. On the  **Compute**  view  **Virtual Machines**  widget, locate the required VM and select it, click the  **Action icon**.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Access20VM20620DP28129.jpg)

The Action menu for the selected VM view appears.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Stop20VM20Button20620DP.jpg)

2. Click the  **Stop**  button on the selected VM's Action menu.

The VM stops, and its status changes from  **Active**  to  **Shutoff**.

# Adding More Networks to a Virtual Machine

During the creation of a VM, you attach the VM to a certain network. However, you can change the network you selected by detaching it and attaching another network, and you can attach more than one network to a certain VM.

The attaching and detaching of networks to/from a VM is done using the Networks widget or the Network view.

-   [To attach a network to a VM](https://www.stratoscale.com/knowledge/attaching-a-network-to-a-virtual-machine)
-   [To detach a network from a VM](https://www.stratoscale.com/knowledge/detaching-a-network-from-a-virtual-machine)

# Adding More Storage to a Virtual Machine

When you launch a VM, a boot volume based on the image you selected for that VM is automatically created. If you need more storage, you can either either extend the size of the boot volume, or attach additional volumes to the VM. Attaching a volume to a VM makes that volume available to the VM as a virtual disk that can be used for storage.

-   [Extend the size of the volume](https://www.stratoscale.com/knowledge/extending-the-size-of-a-volume)
-   [Add storage volumes to a VM](https://www.stratoscale.com/knowledge/attaching-a-volume-to-a-virtual-machine)

# Migrating a Virtual Machine to Another Node

By default, Symphony places a running VM on a certain node according to its internal analysis of the state of the cluster. When changes occur in the system load, performance, and scale, Symphony can automatically migrate the VM to another node to rebalance and optimize the system resources. In addition to the automatic placement and migration,Symphony enables you to determine on which node the VM will run, and allows you to move a VM from one node to another by using the Migrate option.

**To migrate a VM to another node**:

1. On the  **Compute**  view  **Virtual Machine**  widget, locate the required VM and select it.

The selected VM details appear on the bottom of the window:

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Migrate20VM20Button20620DP.jpg)

2. To move the Virtual Machine to another node, click the  **Migrate**  button on the selected VM's Action icon menu.

The Migrate VM dialog box appears.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Migrate20VM20Dialog20620DP.jpg)

3. From the  **Select Node**  drop-down list, select the node to which you want to migrate the VM, and click OK.

The status of the VM changes to  **Migrating**  during the migration process.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VM20-20Migrate20VM20Success20620DP.jpg)

Once the migration process ends, the status of the VM changes back to  **Active**, and it is now located on the selected node.

# Deleting a Virtual Machine

You can delete VMs that are in Shutoff status. If you want to delete a running VM, stop it first, and then delete it from the system.

**To delete a VM**:

1. On the Compute view Virtual Machines widget, locate the required VM and select it.

The selected VM details appear on the bottom of the window:

If your VM is running, click the  **Stop**  button to stop it, since you cannot delete a running machine.

2. Click the  **Delete**  button on the selected VM's Action icon menu.

A confirmation message appears, asking you to approve the deletion:

3. Click  **OK**  to delete the VM.

The VM is now deleted from the system.

# Protecting a Virtual Machine

After you create a VM, you can attach one or more Data Protection Plans to it.

**Note**:You can attach a Data Protection Plan to a VM only if its Status is Shutoff.

If its Status is Active, you must first [stop the virtual machine](https://www.stratoscale.com/pages/viewpage.action?pageId=333168). This will change its Status to Shutoff.

# Protecting a VM via the Symphony GUI

**To protect a VM via the Symphony GUI**

1.  On the  **Compute - Virtual Machines**  view, locate the VM which you wish to protect. Note that its Protection is not checked and that its Status is "Shutoff".
2.  Click on the Actions icon on its right and select  **Protect**.
    
    The Protect VM dialog box appears.
    
3.  In the Protection Plans dropdown, add or remove as many protection plans as you wish, and click  **OK**.
    
    In the Compute - Virtual Machines view its Protection column is checked, indicating that the VM is protected.  
    **Note**: Use the Protect VM dialog box to also remove the protection of the VM.
    
4.  To Start the Virtual Machine click the Actions icon and then the  **Start**  button.

# Recovering a Windows Virtual Machine

If a Windows-based VM that was  [imported from VMware or Hyper-V](https://www.stratoscale.com/knowledge/migrating-a-vm-from-vmware-into-symphony-via-the-gui), is prevented from having its storage and network drivers injected, it will not start properly (it will start in a blue screen) When this happens, the instance must first be started via the  **Recover**  button.

**To recover a Windows VM**:

1.  On the  **Compute** >  **Instances**  > view, click on the instance to be recovered.  
    This will display the detailed view of that instance.
2.  Click on the  **More**  button and select the  **Recover**  option.  
    This pops-up the **VM Recovery**  confirmation message.
    
    ![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_57_Virtual20Machines_VM20Recovery20confirmation20message.jpg)
    
3.  Click  **OK**  to recover the VM. This will install the storage and network drivers on the VM.  
    Next startup you'll be able to start the Instance via the **Start** button.

# Associating a Security Group with a Virtual Machine

To limit the inbound and outbound traffic of a VM, you can associate a security group with it.

**Note**: If a security group is not specified, a port is associated with a default security group. The default security group allows both ingress and egress traffic. Security rules can be added to the default security group to change the traffic behavior.

**To associate a security group with a VM**:

1. On the  **Compute - Virtual Machines**  view click on the name of the VM with which you wish to associate a security group.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_62_List20of20VMs.jpg)

This accesses the view of the selected VM at the Overview tab.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_63_Specific20VM2BOverview20tab.jpg)

2. Display the  **Security Groups**  tab and click  **Attach Security Group**.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_59_Specifc20Virtual20Machine_Security20Group20tab_Attach20Security20Group20button28129.jpg)

The Attach Security Group dialog box appears:

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_60_Specifc20Virtual20Machine_Security20Group20tab_Attach20Security20Group20dialog.jpg)

3. Select the Security Group which you wish to associate with the VM and the Network on the VM to whose port this Security Group will be attached, and click  **OK**.

The selected VM is now associated with a Security Group.

![](https://www.stratoscale.com/wp-content/uploads/Compute20VMs_61_Specifc20Virtual20Machine_Security20Group20tab_Newly20Associated20Security20Group.jpg)

# Enabling Secure SSH Access to a VM

You can use Symphony to enable secure SSH access to a VM, using a key pair.

To do this:

1.  [Make sure network requirements are in place (floating IP allocated to an edge network)](https://www.stratoscale.com/knowledge/compute-2/secure-ssh-access-to-a-vm/enabling-secure-ssh-access-to-a-vm/#EnablingSecureSSHAccesstoaVM-Network).
2.  [Generate a key pair and register it with Symphony](https://www.stratoscale.com/knowledge/compute-2/secure-ssh-access-to-a-vm/enabling-secure-ssh-access-to-a-vm/#EnablingSecureSSHAccesstoaVM-Key).
3.  [Create the VM and, during creation, associate the VM with the key pair you just registered with Symphony. Attach the the edge network's floating IP to the VM](https://www.stratoscale.com/knowledge/compute-2/secure-ssh-access-to-a-vm/enabling-secure-ssh-access-to-a-vm/#EnablingSecureSSHAccesstoaVM-VM).
4.  [SSH into the VM, passing in the floating IP and your private key](https://www.stratoscale.com/knowledge/compute-2/secure-ssh-access-to-a-vm/enabling-secure-ssh-access-to-a-vm/#EnablingSecureSSHAccesstoaVM-SSH).

## Make sure network requirements are in place

You need an edge network that has a floating IP allocated to it.

If these are not already present in your system:

1.  [Create an edge network (Networking>Networks>Create>Type=Edge)](https://www.stratoscale.com/knowledge/video---how-to-create-an-edge-network).
2.  [Allocate a floating IP to the edge network (Networking>Floating IPs>Allocate)](https://www.stratoscale.com/knowledge/video---how-to-allocate-a-floating-ip).

## Generate a key pair

You can either:

-   [Have Symphony generate a key pair for you](https://www.stratoscale.com/knowledge/compute-2/secure-ssh-access-to-a-vm/enabling-secure-ssh-access-to-a-vm/#EnablingSecureSSHAccesstoaVM-Sympgenerates).
    
    If you do this, Symphony automatically registers the public key, then downloads the private key to your machine.
    
-   [Generate your own key pair and register the public key with Symphony](https://www.stratoscale.com/knowledge/compute-2/secure-ssh-access-to-a-vm/enabling-secure-ssh-access-to-a-vm/#EnablingSecureSSHAccesstoaVM-Yougenerate).

### If you want to have Symphony generate a key pair for you

Click  **Compute > Key Pairs > Create**.

This displays the Generate Key Pair wizard.

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><th class="highlight-blue confluenceTh" colspan="2" data-highlight-colour="blue" style="text-align: center;">Details tab</th></tr><tr><td class="confluenceTd"><strong>Name</strong></td><td class="confluenceTd">Type in the name of the key pair you are creating.</td></tr><tr><td class="confluenceTd"><strong>Radio Buttons<br></strong></td><td class="confluenceTd">Select the radio button that asks Symphony to generate a key pair and download the private key.</td></tr><tr><td class="confluenceTd"><strong>Next</strong></td><td class="confluenceTd">Click <strong>Next</strong> to generate the key pair. The system displays the Result tab.</td></tr><tr><td class="highlight-blue confluenceTd" colspan="2" data-highlight-colour="blue" style="text-align: center;"><strong>Result tab</strong></td></tr><tr><td colspan="2" class="confluenceTd">The system generates a public key (which it keeps), and a private key (which you need to download).</td></tr><tr><td class="confluenceTd"><strong>Name</strong></td><td class="confluenceTd">The system displays the name of the key pair.</td></tr><tr><td class="confluenceTd"><strong>Fingerprint</strong></td><td class="confluenceTd">The system displays the public key's fingerprint.</td></tr><tr><td class="confluenceTd"><strong>Save</strong></td><td class="confluenceTd">The system also displays a <strong>Save</strong> button, along with a message telling you to save the private key. Click the <strong>Save</strong> button.<p></p><p>The system downloads the private key to your browser's default download location. The private key file is named:</p><p><code>&lt;name&gt;.pem</code></p><p>Where <code>&lt;name&gt;</code> is the name of the key pair you specified in the Details step.</p></td></tr></tbody></table>

### If you want to generate your own key pair and register the public key with Symphony

1. Start by using a tool of your choice to generate a key pair (public and private key). Example:

`$ ssh-keygen`

Change the file permissions on the private key to 400 or 600 to secure the key. Example:

`$ chmod 400 id_rsa`

2. Register the public key with Symphony:

Click  **Compute > Key Pairs > Create**.

This displays the Generate Key Pair wizard.

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><th class="highlight-blue confluenceTh" colspan="2" data-highlight-colour="blue" style="text-align: center;">Details tab</th></tr><tr><td class="confluenceTd"><strong>Name</strong></td><td class="confluenceTd">Type in the name of the key pair you are creating.</td></tr><tr><td colspan="1" class="confluenceTd"><strong>Radio Buttons</strong></td><td colspan="1" class="confluenceTd">Select the radio button for uploading a key pair that you created using another tool. The system displays the <strong>Public Key</strong> dialog box.</td></tr><tr><td class="confluenceTd"><strong>Public Key</strong></td><td class="confluenceTd">Drag and drop the public key file onto the dialog box, or click the <strong>Browse</strong> button and navigate to it.</td></tr><tr><td class="confluenceTd"><strong>Generate</strong></td><td class="confluenceTd">Click the <strong>Next&nbsp;</strong> button. The system displays the <strong>Result</strong> tab.</td></tr><tr><td class="highlight-blue confluenceTd" colspan="2" data-highlight-colour="blue" style="text-align: center;"><strong>Result tab</strong></td></tr><tr><td colspan="2" class="confluenceTd">This displays the public key name and fingerprint.</td></tr><tr><td class="confluenceTd"><strong>Name</strong></td><td class="confluenceTd">The system displays the name of the key pair.</td></tr><tr><td class="confluenceTd"><strong>Fingerprint</strong></td><td class="confluenceTd">The system displays the public key's fingerprint.</td></tr></tbody></table>

## Create VM and specify key pair and floating IP

You need to create a VM and, during creation, associate the VM with the key pair you just registered with Symphony. You then need to attach the edge network's floating IP to the VM.

### Associate key pair with VM:

You associate a key pair with a VM as part of the  [VM creation process](https://www.stratoscale.com/knowledge/creating-a-virtual-machine).

1. Display the  **Initialize**  tab in the Create VM wizard.

2. Click the  **Key Pair**  drop-down and select the key pair you want to inject into the VM.

### Attach floating IP to VM:

1. After you create the VM, click:

**Compute > Instances > name of VM**

This displays the details view.

2. Click the  **Floating IPs**  tab, then the  **Attach**  button. Select a floating IP from the Floating IP drop down menu.

## SSH into the VM

You can now SSH into the VM, using the following syntax:

`$ ssh -i <private_key_file> <default_username_for_image>@<floating_ip>`

In the following example, the private key file is  `id_rsa`, and the default username for the image that the VM is based on is  `fedora`. The floating IP is  `192.237.248.66`.

Example:

`$ ssh -i id_rsa fedora@192.237.248.66`


# Symphony-supported AWS – EC2 APIs and Parameters

Below is a list of the AWS - EC2 APIs that Symphony supports, together with their supported Required and Optional request parameters.

Click on the API name to access the complete AWS documentation for that action.

<table class="wrapped confluenceTable" style="font-size: 14.0px;"><colgroup><col><col><col><col></colgroup><tbody><tr><th class="confluenceTh">Name</th><th class="confluenceTh">Required Parameters</th><th class="confluenceTh">Optional Parameters</th><th class="confluenceTh" colspan="1">Notes</th></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AllocateAddress.html" rel="nofollow">AllocateAddress</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>Address</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AssignPrivateIpAddresses.html" rel="nofollow">AssignPrivateIpAddresses</a></td><td class="confluenceTd"><ul><li>NetworkInterfaceId</li></ul></td><td class="confluenceTd"><ul><li>PrivateIpAddress</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AssociateAddress.html" rel="nofollow">AssociateAddress</a></td><td class="confluenceTd"><ul><li>AllocationId</li></ul></td><td class="confluenceTd"><ul><li>InstanceId</li><li>NetworkInterfaceId</li><li>PrivateIpAddress</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AssociateDhcpOptions.html" rel="nofollow">AssociateDhcpOptions</a></td><td class="confluenceTd"><ul><li>DhcpOptionsId</li><li>VpcId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AssociateRouteTable.html" rel="nofollow">AssociateRouteTable</a></td><td class="confluenceTd"><ul><li>RouteTableId</li><li>SubnetId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AttachInternetGateway.html" rel="nofollow">AttachInternetGateway</a></td><td class="confluenceTd"><ul><li>InternetGatewayId</li><li>VpcId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AttachNetworkInterface.html" rel="nofollow">AttachNetworkInterface</a></td><td class="confluenceTd"><ul><li>DeviceIndex</li><li>InstanceId</li><li>NetworkInterfaceId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AttachVolume.html" rel="nofollow">AttachVolume</a></td><td class="confluenceTd"><ul><li>Device</li><li>InstanceId</li><li>VolumeId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AuthorizeSecurityGroupEgress.html" rel="nofollow">AuthorizeSecurityGroupEgress</a></td><td class="confluenceTd"><ul><li>GroupId</li></ul></td><td class="confluenceTd"><ul><li>IpPermissions</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_AuthorizeSecurityGroupIngress.html" rel="nofollow">AuthorizeSecurityGroupIngress</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>GroupId</li><li>GroupName</li><li>IpPermissions</li><li>CidrIp</li><li>FromPort</li><li>IpProtocol</li><li>ToPort</li><li>SourceSecurityGroupName</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateDhcpOptions.html" rel="nofollow">CreateDhcpOptions</a></td><td class="confluenceTd"><ul><li>DhcpConfiguration</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateImage.html" rel="nofollow">CreateImage</a></td><td class="confluenceTd"><ul><li>InstanceId</li><li>Name</li></ul></td><td class="confluenceTd"><ul><li>Description</li><li>BlockDeviceMapping</li><li>NoReboot</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateInternetGateway.html" rel="nofollow">CreateInternetGateway</a></td><td class="confluenceTd"></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateKeyPair.html" rel="nofollow">CreateKeyPair</a></td><td class="confluenceTd"><ul><li>KeyName</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateNetworkInterface.html" rel="nofollow">CreateNetworkInterface</a></td><td class="confluenceTd"><ul><li>SubnetId</li></ul></td><td class="confluenceTd"><ul><li>Description</li><li>PrivateIpAddress</li><li>PrivateIpAddresses</li><li>SecondaryPrivateIpAddressCount</li><li>SecurityGroupId</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateRoute.html" rel="nofollow">CreateRoute</a></td><td class="confluenceTd"><ul><li>RouteTableId</li></ul></td><td class="confluenceTd"><ul><li>DestinationCidrBlock</li><li>GatewayId</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateRouteTable.html" rel="nofollow">CreateRouteTable</a></td><td class="confluenceTd"><ul><li>VpcId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateSecurityGroup.html" rel="nofollow">CreateSecurityGroup</a></td><td class="confluenceTd"><ul><li>GroupDescription</li><li>GroupName</li><li>VpcId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateSnapshot.html" rel="nofollow">CreateSnapshot</a></td><td class="confluenceTd"><ul><li>VolumeId</li></ul></td><td class="confluenceTd"><ul><li>Description</li><li>TagSpecification</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateSubnet.html" rel="nofollow">CreateSubnet</a></td><td class="confluenceTd"><ul><li>VpcId</li><li>CidrBlock</li></ul></td><td class="confluenceTd"><ul><li>AvailabilityZone</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateTags.html" rel="nofollow">CreateTags</a></td><td class="confluenceTd"><ul><li>ResourceId</li><li>Tag</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateVolume.html" rel="nofollow">CreateVolume</a></td><td class="confluenceTd"><ul><li>AvailabilityZone</li></ul></td><td class="confluenceTd"><ul><li>Size</li><li>SnapshotId</li><li>TagSpecification</li><li>VolumeType</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateVpc.html" rel="nofollow">CreateVpc</a></td><td class="confluenceTd"><ul><li>CidrBlock</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteDhcpOptions.html" rel="nofollow">DeleteDhcpOptions</a></td><td class="confluenceTd"><ul><li>DhcpOptionsId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteInternetGateway.html" rel="nofollow">DeleteInternetGateway</a></td><td class="confluenceTd"><ul><li>InternetGatewayId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteKeyPair.html" rel="nofollow">DeleteKeyPair</a></td><td class="confluenceTd"><ul><li>KeyName</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteNetworkInterface.html" rel="nofollow">DeleteNetworkInterface</a></td><td class="confluenceTd"><ul><li>NetworkInterfaceId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteRoute.html" rel="nofollow">DeleteRoute</a></td><td class="confluenceTd"><ul><li>RouteTableId</li></ul></td><td class="confluenceTd"><ul><li>DestinationCidrBlock</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteRouteTable.html" rel="nofollow">DeleteRouteTable</a></td><td class="confluenceTd"><ul><li>RouteTableId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteSecurityGroup.html" rel="nofollow">DeleteSecurityGroup</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>GroupId</li><li>GroupName</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteSnapshot.html" rel="nofollow">DeleteSnapshot</a></td><td class="confluenceTd"><ul><li>SnapshotId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteSubnet.html" rel="nofollow">DeleteSubnet</a></td><td class="confluenceTd"><ul><li>SubnetId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteTags.html" rel="nofollow">DeleteTags</a></td><td class="confluenceTd"><ul><li>ResourceId</li><li>Tag</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteVolume.html" rel="nofollow">DeleteVolume</a></td><td class="confluenceTd"><ul><li>VolumeId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeleteVpc.html" rel="nofollow">DeleteVpc</a></td><td class="confluenceTd"><ul><li>VpcId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeregisterImage.html" rel="nofollow">DeregisterImage</a></td><td class="confluenceTd"><ul><li>ImageId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeAccountAttributes.html" rel="nofollow">DescribeAccountAttributes</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>AttributeName</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeAddresses.html" rel="nofollow">DescribeAddresses</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>AllocationId</li><li>PublicIp</li><li>Filter</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeAvailabilityZones.html" rel="nofollow">DescribeAvailabilityZones</a></td><td class="confluenceTd"></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeDhcpOptions.html" rel="nofollow">DescribeDhcpOptions</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>DhcpOptionsId</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeImageAttribute.html" rel="nofollow">DescribeImageAttribute</a></td><td class="confluenceTd"><ul><li>ImageId</li><li>Attribute</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeImages.html" rel="nofollow">DescribeImages</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>ExecutableBy</li><li>Filter</li><li>ImageId</li><li>Owner</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeImportImageTasks.html" rel="nofollow">DescribeImportImageTasks</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>Filters</li><li>ImportTaskId</li><li>MaxResults</li><li>NextToken</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeInstanceAttribute.html" rel="nofollow">DescribeInstanceAttribute</a></td><td class="confluenceTd"><ul><li>InstanceId</li><li>Attribute</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeInstanceCreditSpecifications.html" rel="nofollow">DescribeInstanceCreditSpecifications</a></td><td class="confluenceTd"><ul><li>InstanceId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeInstances.html" rel="nofollow">DescribeInstances</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>InstanceId</li><li>Filter</li><li>MaxResults</li><li>NextToken</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeInternetGateways.html" rel="nofollow">DescribeInternetGateways</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>InternetGatewayId</li><li>Filter</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeKeyPairs.html" rel="nofollow">DescribeKeyPairs</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>KeyName</li><li>Filter</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeNetworkInterfaces.html" rel="nofollow">DescribeNetworkInterfaces</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>NetworkInterfaceId</li><li>Filter</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeRegions.html" rel="nofollow">DescribeRegions</a></td><td class="confluenceTd"></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeRouteTables.html" rel="nofollow">DescribeRouteTables</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>RouteTableId</li><li>Filter</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeSecurityGroups.html" rel="nofollow">DescribeSecurityGroups</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>GroupId</li><li>GroupName</li><li>Filter</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeSnapshots.html" rel="nofollow">DescribeSnapshots</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>SnapshotId</li><li>Owner</li><li>Filter</li><li>MaxResults</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeSpotInstanceRequests.html" rel="nofollow">DescribeSpotInstanceRequests</a></td><td class="confluenceTd"></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeSubnets.html" rel="nofollow">DescribeSubnets</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>SubnetId</li><li>Filter</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeTags.html" rel="nofollow">DescribeTags</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>Filter</li><li>MaxResults</li><li>NextToken</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeVolumes.html" rel="nofollow">DescribeVolumes</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>VolumeId</li><li>Filter</li><li>MaxResults</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeVpcAttribute.html" rel="nofollow">DescribeVpcAttribute</a></td><td class="confluenceTd"><ul><li>VpcId</li><li>Attribute</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeVpcClassicLink.html" rel="nofollow">DescribeVpcClassicLink</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>VpcId</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeVpcClassicLinkDnsSupport.html" rel="nofollow">DescribeVpcClassicLinkDnsSupport</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>VpcId</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd" colspan="1"><span style="color: #0000ff;"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeVpcPeeringConnections.html" rel="nofollow">DescribeVpcPeeringConnections</a></span></td><td class="confluenceTd" colspan="1"></td><td class="confluenceTd" colspan="1"><ul><li>VpcPeeringConnectionId</li><li>Filter</li></ul></td><td class="confluenceTd" colspan="1"><p style="text-align: center;"><span style="color: #0000ff;"><span style="color: #000000;">Introduced</span><strong><br> </strong></span><span style="color: #0000ff;">Symphony&nbsp;v5.1.1</span></p></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeVpcs.html" rel="nofollow">DescribeVpcs</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>VpcId</li><li>Filter</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DetachInternetGateway.html" rel="nofollow">DetachInternetGateway</a></td><td class="confluenceTd"><ul><li>InternetGatewayId</li><li>VpcId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DetachNetworkInterface.html" rel="nofollow">DetachNetworkInterface</a></td><td class="confluenceTd"><ul><li>AttachmentId</li></ul></td><td class="confluenceTd"><ul><li>Force</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DetachVolume.html" rel="nofollow">DetachVolume</a></td><td class="confluenceTd"><ul><li>VolumeId</li></ul></td><td class="confluenceTd"><ul><li>Device</li><li>InstanceId</li><li>Force</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DisassociateAddress.html" rel="nofollow">DisassociateAddress</a></td><td class="confluenceTd"><ul><li>AssociationId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DisassociateRouteTable.html" rel="nofollow">DisassociateRouteTable</a></td><td class="confluenceTd"><ul><li>AssociationId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_GetConsoleOutput.html" rel="nofollow">GetConsoleOutput</a></td><td class="confluenceTd"><ul><li>InstanceId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_GetPasswordData.html" rel="nofollow">GetPasswordData</a></td><td class="confluenceTd"><ul><li>InstanceId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ImportImage.html" rel="nofollow">ImportImage</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>Architecture</li><li>ClientData</li><li>ClientToken</li><li>Description</li><li>DiskContainer</li><li>Hypervisor</li><li>LicenseType</li><li>Platform</li><li>RoleName</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ImportKeyPair.html" rel="nofollow">ImportKeyPair</a></td><td class="confluenceTd"><ul><li>KeyName</li><li>PublicKeyMaterial</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ModifyImageAttribute.html" rel="nofollow">ModifyImageAttribute</a></td><td class="confluenceTd"><ul><li>ImageId</li></ul></td><td class="confluenceTd"><ul><li>Attribute</li><li>Description</li><li>LaunchPermission</li><li>OperationType</li><li>ProductCode</li><li>UserGroup</li><li>UserId</li><li>Value</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ModifyInstanceAttribute.html" rel="nofollow">ModifyInstanceAttribute</a></td><td class="confluenceTd"><ul><li>InstanceId</li></ul></td><td class="confluenceTd"><ul><li>Attribute</li><li>Value</li><li>InstanceType</li><li>DisableApiTermination</li><li>Kernel</li><li>Ramdisk</li><li>InstanceInitiatedShutdownBehavior</li><li>RootDeviceName</li><li>ProductCodes</li><li>SourceDestCheck</li><li>GroupSet</li><li>EbsOptimized</li><li>SriovNetSupport</li><li>EnaSupport</li><li>UserData</li><li>BlockDeviceMapping</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ModifyNetworkInterfaceAttribute.html" rel="nofollow">ModifyNetworkInterfaceAttribute</a></td><td class="confluenceTd"><ul><li>NetworkInterfaceId</li></ul></td><td class="confluenceTd"><ul><li>SecurityGroupId</li><li>SourceDestCheck</li><li>Description</li><li>Attachment</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ModifyVolume.html" rel="nofollow">ModifyVolume</a></td><td class="confluenceTd"><ul><li>VolumeId</li></ul></td><td class="confluenceTd"><ul><li>Iops</li><li>Size</li><li>VolumeType</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ModifyVpcAttribute.html" rel="nofollow">ModifyVpcAttribute</a></td><td class="confluenceTd"><ul><li>VpcId</li></ul></td><td class="confluenceTd"><ul><li>EnableDnsHostnames</li><li>EnableDnsSupport</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_RebootInstances.html" rel="nofollow">RebootInstances</a></td><td class="confluenceTd"><ul><li>InstanceId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_RegisterImage.html" rel="nofollow">RegisterImage</a></td><td class="confluenceTd"><ul><li>Name</li></ul></td><td class="confluenceTd"><ul><li>Architecture</li><li>BillingProduct</li><li>BlockDeviceMapping</li><li>Description</li><li>EnaSupport</li><li>ImageLocation</li><li>KernelId</li><li>RamdiskId</li><li>RootDeviceName</li><li>SriovNetSupport</li><li>VirtualizationType</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ReleaseAddress.html" rel="nofollow">ReleaseAddress</a></td><td class="confluenceTd"><ul><li>AllocationId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ReplaceRouteTableAssociation.html" rel="nofollow">ReplaceRouteTableAssociation</a></td><td class="confluenceTd"><ul><li>AssociationId</li><li>RouteTableId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ResetImageAttribute.html" rel="nofollow">ResetImageAttribute</a></td><td class="confluenceTd"><ul><li>ImageId</li></ul></td><td class="confluenceTd"><ul><li>LaunchPermission</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ResetInstanceAttribute.html" rel="nofollow">ResetInstanceAttribute</a></td><td class="confluenceTd"><ul><li>InstanceId</li><li>Attribute</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_RevokeSecurityGroupEgress.html" rel="nofollow">RevokeSecurityGroupEgress</a></td><td class="confluenceTd"><ul><li>GroupId</li></ul></td><td class="confluenceTd"><ul><li>IpPermissions</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_RevokeSecurityGroupIngress.html" rel="nofollow">RevokeSecurityGroupIngress</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>GroupId</li><li>GroupName</li><li>IpPermissions</li><li>CidrIp</li><li>FromPort</li><li>IpProtocol</li><li>ToPort</li><li>SourceSecurityGroupName</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_RunInstances.html" rel="nofollow">RunInstances</a></td><td class="confluenceTd"><ul><li>MinCount</li><li>MaxCount</li><li>ImageId</li></ul></td><td class="confluenceTd"><ul><li>InstanceType</li><li>KeyName</li><li>NetworkInterface</li><li>PrivateIpAddress</li><li>SecurityGroup</li><li>SecurityGroupId</li><li>SubnetId</li><li>TagSpecification</li><li>UserData</li><li>EbsOptimized</li><li>BlockDeviceMapping</li><li>DisableApiTermination</li><li>Monitoring</li><li>Placement</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_StartInstances.html" rel="nofollow">StartInstances</a></td><td class="confluenceTd"><ul><li>InstanceId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_StopInstances.html" rel="nofollow">StopInstances</a></td><td class="confluenceTd"><ul><li>InstanceId</li></ul></td><td class="confluenceTd"><ul><li>Force</li></ul></td><td class="confluenceTd" colspan="1"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_TerminateInstances.html" rel="nofollow">TerminateInstances</a></td><td class="confluenceTd"><ul><li>InstanceId</li></ul></td><td class="confluenceTd"></td><td class="confluenceTd" colspan="1"></td></tr></tbody></table>