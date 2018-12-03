# Containers – Kubernetes

## Overview

Symphony offers Kubernetes (K8S) as a service, providing a platform for automating the deployment, scaling, and operations of application containers across clusters of hosts. Any user can create a cluster defining the number of nodes and the sizing of each node's HW (CPU, RAM and Disk), monitor its health and usage, deploy services and applications with it, and connect it to automated procedures such as Jenkins's flows.

# Create a Kubernetes Cluster

### Prerequisites for Creating a Kubernetes (K8S) Cluster

1.  Kubernetes service requires one network with DHCP enabled.
    
2.  To access the Kubernetes cluster API and UI, the master node must be reachable from the user workstation
    
3.  To access services exposed via NodePort, all Kubernetes nodes must be reachable from the user workstation.
    
4.  To access a public docker registry such as Docker Hub or [gcr.io](http://gcr.io/), the network used by the kubernetes nodes must be accessible to the internet with a valid DNS.
    
5.  To use a private registry, the network used by the kubernetes nodes must be routable to that registry address with a valid DNS.
    
6.  Each kubernetes node must have at least 2 vCPUs and 1024MB RAM
    

### **To create a Kubernetes Cluster**:

1.  On the main menu select **Containers** > **Kubernetes**.  
    The **Containers - Kubernetes** view appears with a list of all of the Kubernetes clusters in the region.  
    The following information is displayed for each cluster:
    1.  **Name**
    2.  **IP** address
    3.  Number of **Nodes**
    4.  Number of **CPUs**
    5.  Amount of **RAM**
    6.  Amount of **Storage**
    7.  **Status** whether **'**Running'**,** 'Stopped' or 'Error'
2.  Click on the **Create Cluster** button found at the upper left-hand corner of the screen.  
    The **Details** step of the Create Kubernetes Cluster wizard appears.
3.  Enter the following information:
    1.  **Name** – Enter a name for the new cluster.
    2.  **Description** - Enter a description of the cluster (optional).
    3.  **Cluster network** - Select a network for the cluster.
    4.  **Floating IP** - Select a floating IP if available (optional).
    5.  **Storage Pool** - Select the storage pool in which the Kubernetes cluster will be created.
4.  Click **Next** to access the **Nodes** step of the Create Kubernetes Cluster wizard.
5.  Enter the following information:
    1.  **Initial Nodes** - enter the initial number of nodes or VMs, to be created in the cluster.
    2.  **Node Properties**
        1.  **Instance type** - select an **Instance type** which determines the number of CPU cores, amount of RAM and disk size of each node,
        2.  **Number of additional disks** - enter the number of additional storage disks per node.
        3.  **Additional disk size** - enter the size of each of these additional storage disks.
    3.  Click **Finish**.  
        After a few moments the new cluster will appear in the **Containers - Kubernetes** view, with its status starting at 'Fetching Images', then moving to 'Creating' and when completed it becomes 'Running'.

# Registries

## Overview

**Docker registries as a service**

The registries service lets you use Docker to push a container image into a Symphony registry. Once present in the registry, you can easily deploy the container image into a Kubernetes cluster.

**To use the Symphony registries service**:

1.  [Enable the container service, then enable a Docker registry engine](https://www.stratoscale.com/knowledge/manage-the-registries-service). An admin user must perform these tasks.

2.  [Create a Symphony registry](https://www.stratoscale.com/knowledge/create-a-registry).

3. Use Docker to  [push a container image into the registry](https://www.stratoscale.com/knowledge/push-or-pull-a-registry-container-image).

4.  [Deploy the image into a Kubernetes cluster](https://www.stratoscale.com/knowledge/deploy-registry-image-into-kubernetes-cluster).

# Manage the Registries Service

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.

**Required administrator tasks**

Before a user can create and access container registries, an admin user must enable the Containers service and enable a registry engine.

**To enable the Containers service**:

1. Click  **Menu**  >  **Region Management**  >  **Settings**  >  **Services & Support**.

2. Under  **Manage Cluster Services**, click the  **Containers**  button to toggle from OFF to ON.

**To enable a registry engine**:

1. Click  **Menu**  >  **Containers**  >  **Engines**  > select a Docker engine.

2. Click the selected engine's  **Enabled**  button to toggle from OFF to ON.

# Create a Registry

**To create a container registry**:

1. Click  **Menu**  >  **Containers**  >  **Registries**  >  **Create**.

2. Fill out the following panels in the Create Registry wizard:

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><th class="confluenceTh">Field</th><th class="confluenceTh">Description</th></tr><tr><td class="confluenceTd"><strong>Name</strong></td><td class="confluenceTd">Name of the registry.</td></tr><tr><td class="confluenceTd"><strong>Descripition</strong></td><td class="confluenceTd">Optional description.</td></tr><tr><td class="confluenceTd"><strong>Instance Type</strong></td><td class="confluenceTd">Select the instance type you want to use for the registry.</td></tr><tr><td class="confluenceTd"><strong>Storage Pool</strong></td><td class="confluenceTd">Select the storage pool you want to use to store the registry.</td></tr><tr><td class="confluenceTd"><strong>Registry Size</strong></td><td class="confluenceTd">Optionally specify the registry size in GB.</td></tr><tr><td class="confluenceTd"><strong>Network</strong></td><td class="confluenceTd">Select the network you want this registry to use. Note that if you are creating the registry as part of a VPC project, only VPC-enabled networks appear in the drop down list. Similarly, if you are creating the registry as part of a non-VPC project, only non-VPC-enabled networks appear in the list.</td></tr><tr><td class="confluenceTd"><strong>Port</strong></td><td class="confluenceTd">Optionally specify the port you want the registry to use. The default is 5000.</td></tr><tr><td class="confluenceTd"><strong>Certificate</strong></td><td class="confluenceTd"><p>Because you are creating a secure Docker registry, you need to have an SSL certificate in place before users can push or pull container images from the registry. There are two ways to put the SSL certificate in place:</p><ul><li><a href="https://www.stratoscale.com/knowledge/importing-a-certificate">Import the certificate</a> before you create the registry. Then, in the create wizard's Certificate field, select the certificate you want to use.</li><li>Leave the certificate field blank when you create the registry. Then, once the registry exists:<p>Select the registry in the registry list (<strong>Menu</strong> &gt; <strong>Containers</strong> &gt; <strong>Registries</strong> &gt; select the registry.)</p><p>Click <strong>Download Certificate</strong>. The Certificate Setup box appears. Follow the instructions in this box to:</p><p>Place the .crt file under your docker certificate directory path like this:</p><p><code>/etc/docker/certs.d/10.45.242.27:5000/certificate.crt</code></p><p>Run the following Docker commands:</p><p><code>$ docker tag &lt;IMAGE_NAME&gt;:&lt;TAG&gt; 10.45.242.27:5000/&lt;IMAGE_NAME&gt;:&lt;TAG&gt;</code></p><p><code>$ docker push 10.45.242.27:5000/&lt;IMAGE_NAME&gt;:&lt;TAG&gt;</code></p></li></ul></td></tr></tbody></table>

# Push or Pull a Registry Container Image

Once you have created a Symphony registry, you can use the Docker CLI to  [push images to the registry](https://docs.docker.com/engine/reference/commandline/push/)  and  [pull images from the registry](https://docs.docker.com/engine/reference/commandline/pull/).

Examples:

	$ docker tag MyImage <registry-ip>:<registry-port>/MyImage

	$ docker push <registry-ip>:<registry-port>/MyImage

	### The push command returns "Pushed" if the push was successful.

	$ docker pull <registry-ip>:<registry-port>/MyImage

You can get the `<registry-ip>` and the `<registry-port>` from the Symphony GUI registry list: **Menu** > **Containers** > **Registries**.

# Deploy Registry Image into Kubernetes Cluster

Assuming you have  [created a registry](https://www.stratoscale.com/knowledge/create-a-registry)  and  [pushed a container image to it](https://www.stratoscale.com/knowledge/push-or-pull-a-registry-container-image), you can add the registry to a Kubernetes cluster, then deploy the image into the cluster.

**To deploy a registry image into a Kubernetes cluster**:

1. First, add the registry to the Kubernetes cluster:

**Menu**  >  **Containers**  >  **Kubernetes**  > name of the cluster >  **More**  >  **Add Registry**.

In the Add Registry dialog box, specify the registry URL using this syntax:

`<registry-ip>:<registry-port>`

You can get the  `<registry-ip>`  and the  `<registry-port>`  from the Symphony GUI registry list:  **Menu**  >  **Containers**  >  **Registries**.

2. Deploy the image into the cluster:

**Menu**  >  **Containers**  >  **Kubernetes**  > select the cluster >  **Deploy**.

In the Container Image field, use this syntax to specify the image you want to deploy:

`<registry-ip>:<registry-port>/<image-name>`

