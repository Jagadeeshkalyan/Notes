* Enterprises would run lot of application workloads, so they will be using the storage for persistense
* Lets list the storage needs
  * Disk Storage
    * Physical
    * Virtual
  * Network Storage
    * File Shares
  * Backup infrastructure (Storage)
  * Disaster Recovery (Storage)
  * Archival Storage for long term
  * FTP Servers or alternative storage.
* Storage Solutions offered by Azure
  * Azure offers following Storage Solutions
    * Azure Storage Account
      * Disk Storage (Virtual Disk)
      * Azure Files (Network file Storage)
      * Azure Blob Storage (FTP/Images to be access over internet)
    * Archival Tier (Archival Storage)
    * Azure Managed disk (Virtual Disk)
    * Azure Backup
    * Azure Site Recovery
  * Azure Also has solutions to migrate the storage from on-premises to Azure
    * Online
    * Offline: Azure Data Box
  * Data Sync Solutions
  
### Storage Accounts in Azure
* Azure Storage account provides a cloud based storage service i.e. highly available, scalable, performant and durable.
* With each storage account, a number of storage services are provided
  * Blobs:
    * Provides highly scalable service for storing data objects such as text or binary data
    * There are three types of storage blobs
      * Block Blobs: Any file can be stored (Each file cannot have size greater than 4.7 TB).
      * Append Blobs: To store log files where generally we have text data which can be appended
      * Page Blobs: Generally used to store VHD (Virtual Hard disk) which is referred as un managed disk
  * Tables: Provides a NOSQL-style store for storing structured data.
  * Queues: Provides reliable message queueing between application components
  * Files: Provides managed file share that can be used by Azure VMs or on-premises
### Performance Tiers
* Standard:This tier supports all storage services
  * blobs
  * tables
  * files
  * queues
  * unmanaged Azure Virtual Machine disks
* Premium:
  * This tier is designed to support workloads with greater demands on I/O and is backed by high-performance SSD disks.
  * It only supports General Purpose Accounts with Disk Blobs & Page Blobs.
  * It also supports Block Blobs or Append Blobs with BlockBlobStorage Account & Files with FileStorage accounts

### Redundancy or Replication Options
* When we create a storage account, we can also specify how our data will be replicated for redundancy and resistance to failure.
  * Locally Redundant Storage (LRS):
    * Makes three synchronous copies of our data within a single datacenter
    * Available for both the Standard & Premium Performance Tiers
  * Zone Redundant Storage (ZRS):
    * Makes three synchronous copies of our data to three seperate availability zones within a single region
  * Geographically Redundant Storage (GRS):
    * This is same as LRS (three local copies) plus three additional asynchronous copies to a second datacenter hundreds of miles away from the primary region.
    * Data replication to other Geography typically occurs within 15 minutes (although ther is no SLA provided)
  * Geo Zone Redundant Storage:
    * This is same as ZRS (three synchronous copies across Zones), plus three additional asynchronous copies to second datacenter hunderds of miles away from the primary region.
    * Data replication to other Geography typically occurs within 15 minutes (although ther is no SLA provided)

### Access Tier
* Azure Blob Storage supports three access tiers
  * Hot:
    * An online tier optimised for storing data that is accessed or modified frequently
    * highest storage cost 
    * lowest access cost
  * Cool:
    * An online tier optimised for storing data that is accessed or modified infrequently
    * lowest storage cost 
    * highest access cost
    * stored for min 30 days
  * Archive:
    * An offline tier optimised for storing data that is rarely accessed 
    * stored for min 180 days
    * It cannot be read or download the blob
    * It takes 15hrs to rehydrate it to online tier (hot or cool)This tier is most-cost effective for storing data, but access data is more expensive than Hot or Cool tiers.

### Networking Options in Storage Acount
* Public Endpoint
* Public Endpoint over selected networks
* Private Endpoint