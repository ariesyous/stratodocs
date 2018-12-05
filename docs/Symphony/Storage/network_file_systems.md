# Network File Systems 

## Symphony NFS Overview

The Symphony File Systems service provides file storage for your VMs (EC2 instances). You can create a filesystem instance, attach the filesystem instance to a private network (mount target), and then read and write data from other VMs to and from the filesystem.

VMs and filesystem instance must be on same subnet

-   Each VM that wants to use a given file system must be on the same subnet as the filesystem instance.
-   You cannot attach multiple mount points to a filesystem.

The Symphony file system service supports the Network File System versions 4.0 and 4.1 (NFSv4) protocol, so the applications and tools that you use today with NFSv4 work correctly with Symphony File Systems. Multiple VMs can access a Symphony file system at the same time, providing a common data source for workloads and applications running on more than one instance.

# Setting up NFS in Symphony

**To set up and use the file system service**:

1. First, an admin user must  [create a filesystem instance and mount target](https://www.stratoscale.com/knowledge/manage-the-file-systems-service).

2. Then, end users can have their  [VMs access the NFS mount point on the filesystem](https://www.stratoscale.com/knowledge/use-the-file-systems-service).

# Manage the File Systems Service

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.  

**Are you on a dark site?**

If you are on a dark site (no internet access), you need to  [get the file system image](https://www.stratoscale.com/knowledge/obtaining-a-file-system-image)  before doing the tasks in this section.

Before end users can use a file system, an admin user needs to create a filesystem instance and an associated mount target.

**To create a filesystem instance and mount target**:

1. Click  **Menu**  >  **Storage**  >  **File Systems**  >  **Create**.

Specify the name you want to use for the file system, and select the storage pool you want to use.

The new file system appears in the list of file systems.

2. Click  **filesystem_name**  >  **Mount Targets**  >  **Create**.

In the Create NFS Mount Target dialog, specify the following values:

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><th class="confluenceTh">Field</th><th class="confluenceTh">Description</th></tr><tr><td class="confluenceTd">Network</td><td class="confluenceTd"><div class="content-wrapper"><p>The network you want to attach to the filesystem instance.</p><div class="confluence-information-macro confluence-information-macro-note conf-macro output-block" data-hasbody="true" data-macro-name="note"><p class="title">All client VMs need to be on this network</p><p><span class="aui-icon aui-icon-small aui-iconfont-warning confluence-information-macro-icon"> </span></p><div class="confluence-information-macro-body"><p>Every VM that wants to access this file system must be on the same subnet as the filesystem instance.</p></div></div></div></td></tr><tr><td class="confluenceTd">Security Group</td><td class="confluenceTd">Optional. Security group to use for the filesystem instance.</td></tr><tr><td class="confluenceTd">IP Address</td><td class="confluenceTd">Optional. You can specify a specific IP address for the filesystem instance. If you leave this blank, the system automatically assigns an IP address.</td></tr></tbody></table>

# Using the File Systems Service

**Prerequisite**: An admin user must  [create a filesystem instance and mount target](https://www.stratoscale.com/knowledge/manage-the-file-systems-service).

You can access a Symphony file system from a VM, using NFS.

Your VM must be on the same network as the filesystem instance

To access a file system from a VM, the VM must be on the same subnet as the filesystem instance.

**To access a file system**:

1. Make sure your VM is on the same subnet as the filesystem instance, then note the IP address of the filesystem instance.

To check this, click  **Menu**  >  **Compute**  >  **Instances**  >  **filesystem_name**  >  **Networks**.

The network name and the IP address of the filesystem instance are both displayed.

2.  [SSH into the VM](https://www.stratoscale.com/knowledge/enabling-secure-ssh-access-to-a-vm).

3. Install an appropriate NFS client for that VM.

4. Make a directory for the mount point -- in this example the directory name is  `/mnt/filesystem/home`:

		$ sudo mkdir -p /mnt/filesystem/home

5. Mount the filesystem to the directory you just created. For example, you can use this syntax, replacing <filesystem_instance_IP> with the IP address of the filesystem:

		$ sudo mount <filesystem_instance_IP>:/var/nfs /mnt/filesystem/home

**To resize a file system instance**:

You can resize the data volume on a file system instance.

To do this, run this Symphony CLI command:

		$ symp -k nfs filesystems resize-volume <filesystem_id> <allocated_storage>

		### specify <allocated_storage> in GB 


# Symphony-supported AWS – EFS APIs and Parameters

Symphony supports the following AWS - EFS API actions. For each action, Symphony supports only the parameters listed below.

For complete AWS documentation for each action, click the action's name.

**Authentication note**

Symphony supports AWS Signature Version 4.

<table class="wrapped confluenceTable"><colgroup><col><col><col></colgroup><tbody><tr><th class="confluenceTh">Name</th><th class="confluenceTh">Required Parameters</th><th class="confluenceTh">Optional Parameters</th></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/efs/latest/ug/API_CreateFileSystem.html" rel="nofollow">CreateFileSystem</a></td><td class="confluenceTd">CreationToken</td><td class="confluenceTd">None</td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/efs/latest/ug/API_CreateMountTarget.html" rel="nofollow">CreateMountTarget</a></td><td class="confluenceTd"><p>FileSystemId</p><p>SubnetId</p></td><td class="confluenceTd"><p>IpAddress</p><p>SecurityGroups</p></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/efs/latest/ug/API_DeleteFileSystem.html" rel="nofollow">DeleteFileSystem</a></td><td class="confluenceTd">FileSystemId</td><td class="confluenceTd">None</td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/efs/latest/ug/API_DeleteMountTarget.html" rel="nofollow">DeleteMountTarget</a></td><td class="confluenceTd">MountTargetId</td><td class="confluenceTd">None</td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/efs/latest/ug/API_DescribeFileSystems.html" rel="nofollow">DescribeFileSystems</a></td><td class="confluenceTd">None</td><td class="confluenceTd"><p>CreationToken</p><p>FileSystemId</p></td></tr><tr><td colspan="1" class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/efs/latest/ug/API_DescribeMountTargets.html" rel="nofollow">DescribeMountTargets</a></td><td colspan="1" class="confluenceTd">None</td><td colspan="1" class="confluenceTd">FileSystemId</td></tr></tbody></table>
