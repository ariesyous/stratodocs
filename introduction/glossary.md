# Glossary

**Affinity Rules**

Affinity Rules allow you to control the placement of virtual machines on hosts within a cluster by using affinity rules.

**API**

Application program interface (API) is a set of routines, protocols, and tools for building software applications. An API specifies how software components should interact and APIs are used when programming graphical user interface (GUI) components. API makes it easier to develop a program by providing all the building blocks. A programmer then puts the blocks together.

**AWS**

Amazon Web Services (AWS) is a secure Cloud services platform, offering compute power, database storage, content delivery and other functionality to businesses.

**Cloud**

Cloud computing means storing and accessing data and programs over the Internet instead of your computer's hard drive. The cloud is just a metaphor for the Internet.

**Cloud Computing**

A computing capability that provides an abstraction between the computing resource and its underlying technical architecture (e.g., servers, storage, networks), enabling convenient, on-demand network access to a shared pool of configurable computing resources that can be rapidly provisioned and released with minimal management effort or service provider interaction.” This definition states that clouds have five essential characteristics: on-demand self-service, broad network access, resource pooling, rapid elasticity, and measured service. Narrowly speaking, cloud computing is client-server computing that abstract the details of the server away;one requests a service (resource), not a specific server (machine). Cloud Computing enables Infrastructure as a Service (IaaS), Platform as a Service (PaaS), and Software as a Service (SaaS). Cloud computing means that infrastructure, applications, and business processes can be delivered to you as a service, over the Internet (or your own network).

**Clusters**

A cluster is a collection of nodes. The Symphony system runs over a cluster and uses it as a logical unit to provide:

-   Node Management – the cluster is used for suspending and removing nodes, as well as monitoring the node status and activity.
-   High Availability – The cluster is responsible for automatically detecting hardware failures, and for handling them by moving workloads from failed nodes to active ones. By performing High Availability procedures, Symphony assures that no data is lost and that the overall cluster operation remains intact.
-   Cluster health and operational status – the cluster has pre-defined events and alarms that reflects the state of the system.
    
    The events provide information about monitored actions, such as the creation and stopping of a workload or a disk failure, and they include a severity level.
    
    Alarms are notifications that are activated in response to an event, or in response to a state of a certain object in the system. They indicate a potentially major issue in the system.
    

**Data Center**

A data center is a centralized repository, either physical or virtual, for the storage, management, and dissemination of data and information organized around a particular body of knowledge or pertaining to a particular business.

**Infrastructure as a service (IaaS)**

Cloud infrastructure services or “Infrastructure as a Service (IaaS)” delivers computer infrastructure, typically a platform virtualization environment, as a service. Rather than purchasing servers, software, data center space or network equipment, clients instead buy those resources as a fully outsourced service. The service is typically billed on a utility computing basis and amount of resources consumed (and therefore the cost) will typically reflect the level of activity. It is an evolution of web hosting and virtual private server offerings.

**Interfaces**

You can communicate with your environment by using one of the three existing Symphony interfaces: REST API - the main programmable interface into the system, the CLI, or the web-based graphical User Interface.

**Hyperconverged**

Hyperconverged is a type of infrastructure system with a software-centric architecture that tightly integrates compute, storage, networking and virtualization resources and other technologies from scratch in a commodity hardware box supported by a single vendor.

**Hypervisor**

A hypervisor or virtual machine monitor (VMM) is a piece of computer software, firmware or hardware that creates and runs virtual machines.

A computer on which a hypervisor is running one or more virtual machines is defined as a host machine.

Each virtual machine is called a guest machine.

**Monitoring Agent**

A Monitoring Agent exists on each node, and it communicates with the Monitoring Service. The Agent provides the Monitoring Service with information, such as how much CPU is being used, the amount of allocated and used disk space on a given node, and more. Based on this information, the Monitoring Service is able to keep track of the system status across all nodes, and initiate changes when resources are running low.

**Multi Tenancy**

Multi Tenancy refers to a software architecture in which a single instance of software runs on a server and serves multiple tenants. A tenant is a group of users who share a common access with specific privileges to the software instance.

**Nodes**

Nodes are the physical machines that provide the infrastructure for storage, compute, and memory, and on which Symphony is installed. The minimal Symphony configuration requires 3 nodes. Nodes can be added, removed, or put in a maintenance mode after the initial installation and configuration. Virtual Machines are running on the nodes of the cluster. The placement of the Virtual Machines on the nodes is determined by a Symphony management sub-system, which also migrates Virtual Machines from one node to another according to the changing state of the Virtual Machines, nodes, and the cluster as a whole.

**Platform as a service (PaaS)**

Cloud platform services, whereby the computing platform (operating system and associated services) is delivered as a service over the Internet by the provider.

The PaaS layer offers black-box services with which developers can build applications on top of the compute infrastructure. This might include developer tools that are offered as a service to build services, or data access and database services, or billing services.

**Private Cloud**

Private cloud is a type of cloud computing that delivers similar advantages to public cloud, including scalability and self-service, but through a proprietary architecture.

Unlike public clouds, which deliver services to multiple organizations, a private cloud is dedicated to a single organization.

**Provisioning Services**

Symphony Provisioning Services are responsible for:

-   Placement – determines where to place resources.
-   Monitoring – monitors node resources and workload demands.
-   Live Migration – migrates workloads between nodes according to the node loads, the resources required by the workloads, and the priority and profile of the workloads.

**Self Service**

A feature that allows customers to provision, manage, and terminate services themselves, without involving the service provider, via a Web interface or programmatic calls to service APIs.

**Server Sprawl**

Server sprawl is a situation in which multiple, under-utilized servers take up more space and consume more resources than can be justified by their workload.

**Software as a service (Saas)**

Cloud application services, whereby applications are delivered over the Internet by the provider, so that the applications don’t have to be purchased, installed, and run on the customer’s computers. SaaS providers were previously referred to as ASP (application service providers). In the SaaS layer, the service provider hosts the software so you don’t need to install it, manage it, or buy hardware for it. All you have to do is connect and use it. SaaS Examples include customer relationship management as a service.

**Software Defined Everything**

With Software Defined Everything, the computing infrastructure is virtualized and delivered as a service. In a Software-Defined Everything environment, management and control of the networking, storage and/or data center infrastructure is automated by intelligent software rather than by the hardware components of the infrastructure. its all done with API calls.

**Storage**

Symphony supports multiple storage systems. By default, the Symphony system comes with a proprietary storage solution.

In addition, you can also attach external storage systems that will serve as additional storage pools.

**Tenant**

A Tenant is a group of users that has access to certain logical resources in a cluster. The logical resources that a user can access, are the resources that were created by all of the users who belong to the same tenant. Users in the same tenant can have different roles.

Each role defines the type of privileges the user will have. Every user in the system must belong to at least one tenant, and each tenant can include one or more users.

**Vendor lock**

Dependency on the particular cloud vendor and difficulty moving from one cloud vendor to another due to lack of standardized protocols, APIs, data structures (schema), and service models.

**Workloads**

Workloads refer to Virtual Machines (VMs).