# Supermicro Server

This guide provides a list of tasks that Stratoscale recommends you complete before starting your Stratoscale Symphony installation. Completing these tasks is important to help ensure that your installation proceeds smoothly.

It is beyond the scope of this document to advise how to determine hardware sizing or capacity planning for your installation. Note that with Stratoscale Symphony, you can add nodes to a running cluster as needed in response to new performance or capacity requirements.

Please review and complete the following seven steps prior to beginning the Stratoscale Symphony installation:

## 1. Verify Minimal Hardware Requirements

Before you start the Symphony installation process, please make sure that your environment meets the following hardware requirements.

Because Stratoscale Symphony is built with a “scale-out” architecture, a minimum of 4 servers is required for production deployments.

Each server must meet the following minimum requirements, although they do not have to be identical hardware configurations:

**Minimum Server Configuration**

CPU: Intel Xeon E3 v1 (Sandy Bridge) or newer processor

Networking: 1x 10GbE and 1x 1GbE

Storage: 1 SSD (100GB+), 2 HDDs (1TB+)

**Recommended Server Configuration**

CPU: 2x Intel Xeon E5 v4 (Broadwell) processors

Networking: 2x 10GbE and 1x 1GbE

Storage: 2x SSD (10-15% of raw HDD capacity), HDDs (see Storage Sizing)

NOTE: While it is technically possible to install Stratoscale Symphony on a single server, it is not officially supported and should not be used in production deployments.

Running Symphony on a single server results in inadequate data protection (i.e. storage is not replicated) and a single disk or server failure may result in data loss.

## 2. Configure Server BIOS Settings

There are a few BIOS settings that must be configured or verified prior to installing Stratoscale Symphony.

The following steps are required for every single server on which you will install Symphony.

TIP: Using system management tools from the server vendor is not covered within this document, but can be used to help to roll out these settings in a more consistent and automated fashion.

Upon power cycling the server, you will be prompted with a splash screen.

Press the  **DEL**  key to enter the BIOS Setup Utility

Once inside the BIOS Setup Utility, select the  **Advanced Settings**  tab

## 3. Enable Intel Virtualization Technology

Choose CPU Configuration menu item

Under “Socket 1 CPU Information”, verify that  **both Intel HT and Intel VT-x Technology is ‘Supported’**  for this server’s CPU. If this is a dual-socket server, please verify Socket 2 as well.

Back on the CPU Configuration screen,  **set Intel Virtualization Technology to ‘Enabled’**

## 4. Configure Storage Controllers (RAID / JBOD Mode)

Stratoscale Symphony includes an integrated software-defined storage (SDS) solution that aggregates local disks from every server into a single storage pool. In order to make this happen, Symphony must have access to each and every individual hard disk, without any local RAID volumes created on the disks.

In this document, we describe how to enable “JBOD” (or “Passthrough”) mode for both the SSD and hard disks within the servers.

TIP: If required, the boot SSD device can be configured in a RAID-1 volume assuming there are at least 2 identical SSDs within the same server. (See Enable RAID-1 for Boot Device)

In the BIOS Setup Utility, choose the  **SATA Configuration menu item**

Instead of using any RAID modes,  **use the built-in Intel AHCI option**

## 5. Set Disk Boot Priority

**Set 1st Boot Device to SSD drive**  (or RAID-1 volume) Symphony will be installed on

## 6. Mounting Symphony ISO using IPMI

In order to install Stratoscale Symphony via a .ISO image, you must mount the image by entering the server’s management console.

For Supermicro servers, out-of-band management is provided via a web-based portal embedded within each server.

**Enter the IPMI address**  of the server into a supported web browser and  **provide the user credentials**  for the management portal.

Once logged in,  **choose Remote Control to launch the server console**  (requires Java to be installed on your local machine/browser)

Choose  **Virtual Media**  from the menu

Select  **ISO File as the Logical Drive Type**. Then  **click “Open Image” button**  to select the Symphony .ISO image file which should be located on the local terminal

Finally,  **click the “Plug In” button**  and verify that the Virtual Media was mounted successfully.

## 7. Boot from Virtual CD / ISO

**Reboot the server and hit F11**  to enter into boot menu

TIP: If the F11 key from your keyboard isn’t being sent to the Remote Control console session, you can launch the virtual keyboard and hit F11 from there.

Select  **IPMI Virtual CDROM**  as the boot device to start booting from the mounted .ISO image

At this point, the Stratoscale Symphony installer will launch and begin the installation.

For help with the actual Stratoscale Symphony installation process, see the  [installation guide](https://www.stratoscale.com/knowledge/installing-symphony)  for detailed steps.