### File Gateway
* The file gateway enables the storage and retrieval of objects in Amazon S3 and Glacier using file protocols such as NFS.
* Configure file shares that are mapped to selected S3 buckets using IAM roles.

### Tape Gateway
* The tape gateway provides backup applications with an iSCSI VTL interface consisting of a virtual media changer, virtual tape driver and virtual tapes.
  * Virtual tape data is stored in Amazon S3 or can be archived on Glacier.
  * Monitor the status of data tranfer and storage interfaces through the AWS Management Console.
  * Additionally, use the API or SDK to programmatically manager an application's interaction with the gateway.

### Stored-Volume Gateway
* Data written to a stored volume gateway is saved on on-premises storage hardware and asynchronously backed up to Amazon S3 in the form of EBS snapshots.
* Storage volumes can be created up to 16 TB in size and are mounted as iSCSI devices from on-premises application servers.

### Cached-Volume Gateway
* With the cached volume gateway, you can create storage volumes up to 32 TB in size and mount them as iSCSI devices from on-premises application servers.
  * Data written to these volumes is stored in S3, with only a cache of recently written and recently read data stored locally on on-premises storage hardware.
  * Point-in-time snapshots can be taken of volume data in S3 in form of EBS snapshots. This provides space-efficient versioned copies of volumes for data protection and various data reuse needs.
  * To prepare for upload to S3, a gateway stores incoming data in a staging area called an upload buffer.
