https://www.snapt.net/glossary/layer-4-vs-layer-7-load-balancing-explained

Microsoft Terminal Services Client (MSTSC)
[referhere] https://docs.microsoft.com/en-us/azure/virtual-machines/vm-naming-conventions
```
[Family] + [Sub-family]* + [# of vCPUs] + [Constrained vCPUs]* + [Additive Features] + [Accelerator Type]* + [Version]
```
Example 1: M416ms_v2
Value	Explanation
Family	M
no.of vCPUs	416
Additive Features	m = memory intensive
                    s = Premium Storage capable
Version	v2

* Azure you have two types of disks
  * Data disks: They get allocated from a different physical host in the same datacenter. For this charges will continue until you delete the disk
  * Temp disk: They get allocated from the same phyiscal host where the vm is allocated (for this no charges)

* Azure has availability options
  * Availability Set (Regions without Zones):
    * [referhere] https://docs.microsoft.com/en-us/azure/virtual-machines/availability-set-overview
    * Availability Set is the Combination of Fault Domains and update domains.
    * Each availability set can be configured with up to three fault domains and twenty update domains.
    * Update domain:
      * Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time. 
      * When more than five virtual machines are configured within a single availability set with five update domains, the sixth virtual machine is placed into the same update domain as the first virtual machine, the seventh in the same update domain as the second virtual machine, and so on.
      * The order of update domains being rebooted may not proceed sequentially during planned maintenance, but only one update domain is rebooted at a time. A rebooted update domain is given 30 minutes to recover before maintenance is initiated on a different update domain.
    * Fault Domain:
      * Fault domains define the group of virtual machines that share a common power source and network switch. By default, the virtual machines configured within your availability set are separated across up to three fault domains.
      * While placing your virtual machines into an availability set does not protect your application from operating system or application-specific failures, it does limit the impact of potential physical hardware failures, network outages, or power interruptions.
  * Availability Zone (Regions with Zones)

* Azure VM Image: 
  * It is a snapshot of a disk (compressed backup of disk) with user information removed and some metadata.
  * Operating system state:
    * Generalization:
      * In this VM Image will not have user specific information
      * The user information is set while creating a VM
      * On the first boot you can set the hostname, admin user and other vm specific configuration.
      * These images contain the Azure agent, this agent will process the parameters and signal back to the platform that the initial configuration has completed. This process is called as provisioning.
      * Provisioning in linux requires
        * Azure Linux Agent
        * Cloud init
    * Specialization:
      * These are the images that are completely configured and do not require VM or special parameters.
      * The platform will turn the VM on and you will need to handle uniqueness within the vm like setting the host name etc.
  * Azure VM Images can be stored in the following two ways
    * Managed Images:
      * Can be used to create multiple VMs, but they have a lot of limitations.
      * Managed Images can be created from a generlized source.
      * They can only be used to create VMs in the same region and they can’t be shared across subscriptions and tenants
    * Azure Compute Gallery:
      * This is recommended for creating managing and sharing the images at scale.
      * Azure Compute Gallery helps build structure and organization around your images
      * Supports both Generalized and specialized Images
      * Global replication of Image
      * Versioning and Grouping of images for easier management
      * Sharing across subscriptions and even between tenants using Azure RBAC
      * At a high level, you create a gallery and it is made up of
        * Image definition: container that holds group of images\
        * Image version: These are actual images

* Load balancer:
  [referhere] https://i0.wp.com/directdevops.blog/wp-content/uploads/2022/05/vm99.png?w=800&ssl=1

* Azure Bastion:
  * This service helps us connect to Azure VM using ssh or rdp in a secure way
* Run command:
  * It can run the linux commands from azure portal by taking help from Azure agent (waagent) in the vm.
* 