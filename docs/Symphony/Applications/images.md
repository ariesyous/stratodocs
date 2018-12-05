# Images

## Overview

In the current release, two image formats are supported - VMware OVA image and the KVM compatible image in RAW or QCOW2 formats. The latter means that most OpenStack KVM images can be uploaded easily. All of the above are converted into the RAW format and preserved in the image repository in the cluster.

1.  Supported images must meet the following requirements:
    1.  The image must be a single bootable system disk.
    2.  The image must be configured to receive its network address via DHCP.
    3.  User access to the VM is required.
    4.  For a Windows image
        -   Use cloudbase-init to prepare your image, and then use VNC to access the VM, or, enable the Remote Access service.
    5.  For a Linux image
        -   A SSH server must be enabled
2.  Note the credentials to be used, when setting up a VM with the image.
3.  Images that you have uploaded to the system are displayed in the **Storage - Images** view:

# Creating an Image from an Uploaded Source

To create an image to be used in the creation of VMs, you must first upload an image source and then convert this source to RAW or QCOW2 format.

**To create an image from an uploaded source**

From the Main Menu open the **Applications** **> Images** view and click on the **+ Create** button, found at the top left-hand corner of the screen.  
The Create Image dialog box pops-up.

On the  **Details**  step, do the following:

1.  **Name** - enter a name for the image you are creating.  
    Note: When creating an ISO image in Symphony, the name of the Symphony image must end with the ‘.iso’ extension.
2.  **[Optional] Description** - enter the description of the image that you are uploading.
3.  **Project** - Select the project which owns this image.
4.  **Firmware Type** - Select either BIOS (Default) or UEFI.
5.  **Scope** - Determine the availability of this image for creating instances.
    -   Project - Only for those with access to the project which owns this image.
    -   Account - Only for the members of the account of the project which owns this image
    -   Public - Available for all users.
6.  **[Optional] Tags**  - Attach one or more tags to this image by which it can be identified.
7.  Click  **Next** to display the Setup step.

On the  **Setup**  step you define the source of the image. The image can be created from one of three sources: File, URL or Snapshot/Volume.  
If created from a URL or Snapshot/Volume, the image can be constituted from multiple sources, each with its own characteristics.

On the  **Setup**  step, do the following:

1.  **Create Image From** - Select the image source, either File, URL or Snapshot/Volume.
    -   If you selected  **File**, do the following:  
        >  **File** - Enter the file name by either dragging-and-dropping or browsing and selecting it.  
        >  **Storage Pool**  - Select the specific storage pool into which you want to upload this image.
    -   If you selected  **URL**, do the following in the Block Device Mapping section:  
        > **URL** - Enter the URL of the image.  
        > **Storage Pool**  - Select the specific storage pool into which you want to upload this image.  
        > **Use Legacy IDE**  - Determine whether to use the legacy IDE or the native IDE (Default).  
        >  **Override Size**  - Select if you want the image to stay the same size (Default) or be overridden. If you choose the latter enter its size.  
        > **Disk Type**  - Select if way this image will be attached as a Disk (Default) or CDROM  
        If you want your image to be created from an additional URL source, click  **Add**, found on the Block Device Mapping header, and define the parameters.
    -   If you selected  **Snapshot/Volume**, do the following in the Block Device Mapping section:  
        > **Snapshot/Volume** - Select the snapshot or volume.  
        > **Storage Pool**  - Select the specific storage pool into which you want to upload this image.  
        > **Use Legacy IDE**  - Determine whether to use the legacy IDE or the native IDE (Default).  
        >  **Override Size**  - Select if you want the image to stay the same size (Default) or be overridden. If you choose the latter enter its size.  
        > **Disk Type**  - Select if way this image will be attached as a Disk (Default) or CDROM  
        If you want your image to be created from an additional Snapshot/Volume, click  **Add**, found on the Block Device Mapping header, and define the parameters.
2.  Click the **OK** button.The image begins to be created. Its progress is displayed in the status column of the **Applications** **> Images** view.  
    When the uploading progress is completed, **Ready** will appear in the Status column.

# Creating an Image from a Volume

You can create an image from a volume, either directly from the volume or by  [using a snapshot of the volume](https://www.stratoscale.com/knowledge/creating-an-image-from-a-snapshot). Creating an image from a volume allows you to use a specific volume state as an image that will be the base for new VMs.

If the volume you want to use to create an image, is currently not attached to a running VM, you can create an image directly from it, as described below.

If the volume is attached to a running VM, and you do not want to stop the VM and detach the volume from it, you can  [create a snapshot of the volume](https://www.stratoscale.com/knowledge/creating-a-snapshot-of-a-volume), and then  [create an image from the snapshot](https://www.stratoscale.com/knowledge/creating-an-image-from-a-snapshot).

**To create an image from a volume**

1. On the  **Storage - Volumes**  view locate the volume from which you want to create an image. Then, click the Actions icon on its right and select  **Create Image**.

The Create Image dialog box appears.

2. Enter a name for the new image or accept the default name, and click  **OK**.

A new image is created, and it appears in the  **Storage - Images**  view.

# Creating an Image from a Snapshot

You can create an image from a volume using a snapshot of the volume. By using a snapshot, you can create an image from a volume that is attached to a running VM, without stopping the VM and detaching the volume from it.

Before you can create an image from a volume snapshot, you need to  [create a snapshot of the volume](https://www.stratoscale.com/knowledge/creating-a-snapshot-of-a-volume).

**To create an image from a snapshot**

1. On the  **Storage - Snapshots**  view, locate the snapshot from which you want to create an image. Then, click the Actions icon on its right and select  **Create Image**.

The Create Image dialog box appears.

2. Enter a Name for the new image, and click  **OK**.

A new image is created, and it appears on the  **Storage - Images**  view.

# Deleting an Image

**To delete an image**

1. On the  **Storage - Images**  view,locate the image you want to delete, and click the Actions icon on the right.

2. Click the  **Delete**  option.

A confirmation message appears, asking you to confirm the deletion.

3. Click  **OK**  to delete the image.

The image is deleted from the system.

# Symphony-supported AWS – AMI APIs and Parameters

Below is a list of the AWS - AMI APIs that Symphony supports, together with their supported Required and Optional request parameters.

Click on the API name to access the complete AWS documentation for that action.

Click [here](https://www.stratoscale.com/knowledge/symphony-supported-aws---ec2-apis-and-parameters) for the complete list of Symphony-supported AWS EC2 APIs.

<table class="wrapped confluenceTable"><colgroup><col><col><col></colgroup><tbody><tr><th class="confluenceTh">Name</th><th class="confluenceTh">Required Parameters</th><th class="confluenceTh">Optional Parameters</th></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_CreateImage.html" rel="nofollow">CreateImage</a></td><td class="confluenceTd"><ul><li>InstanceId</li><li>Name</li></ul></td><td class="confluenceTd"><ul><li>Description</li><li>BlockDeviceMapping</li><li>NoReboot</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DeregisterImage.html" rel="nofollow">DeregisterImage</a></td><td class="confluenceTd"><ul><li>ImageId</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeImageAttribute.html" rel="nofollow">DescribeImageAttribute</a></td><td class="confluenceTd"><ul><li>ImageId</li><li>Attribute</li></ul></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeImages.html" rel="nofollow">DescribeImages</a></td><td class="confluenceTd"></td><td class="confluenceTd"><ul><li>ExecutableBy</li><li>Filter</li><li>ImageId</li><li>Owner</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ModifyImageAttribute.html" rel="nofollow">ModifyImageAttribute</a></td><td class="confluenceTd"><ul><li>ImageId</li></ul></td><td class="confluenceTd"><ul><li>Attribute</li><li>Description</li><li>LaunchPermission</li><li>OperationType</li><li>ProductCode</li><li>UserGroup</li><li>UserId</li><li>Value</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_RegisterImage.html" rel="nofollow">RegisterImage</a></td><td class="confluenceTd"><ul><li>Name</li></ul></td><td class="confluenceTd"><ul><li>Architecture</li><li>BillingProduct</li><li>BlockDeviceMapping</li><li>Description</li><li>EnaSupport</li><li>ImageLocation</li><li>KernelId</li><li>RamdiskId</li><li>RootDeviceName</li><li>SriovNetSupport</li><li>VirtualizationType</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ResetImageAttribute.html" rel="nofollow">ResetImageAttribute</a></td><td class="confluenceTd"><ul><li>ImageId</li></ul></td><td class="confluenceTd"><ul><li>LaunchPermission</li></ul></td></tr></tbody></table>

