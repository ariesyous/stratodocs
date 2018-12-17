# Terraform

# Environment Creation Example

This example assumes that you have a functional Symphony cluster and you want to create a full environment that includes:

-   1 VM - simulating a server machine
-   3 VMs - simulating client machines
-   1 VM - a virtual network appliance that acts as a router / firewall

The virtual appliance is connected to both the client VMs' network and the server's network.

The sample Terraform scripts automate the creation of this environment by creating:

-   A VPC
-   2 networks within the VPC
-   5 VMs connected to each other in appropriate ways

There are 2 sample Terraform script files,  `[connect.tf](https://www.stratoscale.com/knowledge/connect.tf)`  and  `[workload.tf](https://www.stratoscale.com/knowledge/workload.tf)`:

-   `[connect.tf](https://www.stratoscale.com/knowledge/connect.tf)`  specifies the IP of the target Symphony cluster, the access and secret keys, and the AMI to use for the VMs.
-   `[workload.tf](https://www.stratoscale.com/knowledge/workload.tf)`  creates the network, subnets, and VMs.