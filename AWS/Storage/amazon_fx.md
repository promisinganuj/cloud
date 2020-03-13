* Amazon FSx for Windows File Server provides fully managed Microsoft Windows file servers, backed by a fully native Windows file system.

* Amazon FSx has native support for Windows file system features and for the industry-standard Server Message Block (SMB)  (supporting versions 2.0 to 3.1.1) protocol to access file storage over a network. 

* Ideally suited business applications, home directories, web serving, content management, data analytics, software build setups, and media processing workloads.

* The primary resources in Amazon FSx are file systems and backups.

### File System
* A file system is where you store and access your files and folders. 
* A file system is made up of a Windows file server and storage volumes, and is accessed with its DNS name. 
* When you create a file system, you specify an amount of storage capacity (in GiB) and an amount of throughput capacity (in MBps).
* All storage is SSD-based, providing consistent submillisecond file operation latencies.

### File Share
* A Windows file share is a specific folder (and its subfolders) within your file system that you make accessible to your compute instances with SMB.
* Your file system already comes with a default Windows file share.
* You can create and manage as many other Windows file shares as you want using the Shared Folders graphical user interface (GUI) tool on Windows

### File Share Accessibility
* You can access your shares from all Windows versions starting from Windows Server 2008 and Windows 7, as well as from current versions of Linux.
* You can map your FSx file shares on Amazon Elastic Compute Cloud (Amazon EC2) instances, as well as on Amazon WorkSpaces instances, Amazon AppStream 2.0 instances, and VMware Cloud on AWS VMs.
* You can access your file shares from on-premises compute instances using AWS Direct Connect or AWS VPN. 
* Can be shared across different Amazon VPC, AWS account, or AWS Region using VPC peering or transit gateways.


# FSx for Luster
### What is Luster?
* Luster is an open source file system designed for applications that require fast storage – where you want your storage to keep up with your compute.
* Lustre was built to quickly and cost effectively process the fastest-growing data sets in the world. 
* It provides sub-millisecond latencies, up to hundreds of gigabytes per second of throughput, and millions of IOPS.

### What is FSx for Luster?
* As a fully managed service, Amazon FSx enables you to use Lustre file systems for any workload where storage speed matters. 
* It eliminates the traditional complexity of setting up and managing Lustre file systems, allowing you to spin up a high-performance file system in minutes.
* It also provides multiple deployment options to optimize cost.

### Integration with S3
* FSx for Lustre integrates with Amazon S3, making it easy to process data sets with the Lustre file system.
* When linked to an S3 bucket, an FSx for Lustre file system transparently presents S3 objects as files and allows you to write changed data back to S3.
* FSx for Lustre tracks changes and enables you to write changed and new data on the file system back to your S3 bucket at any time.

### Security and compliance
* Automatically encrypts your data at-rest and in-transit.
* PCI-DSS, ISO, and SOC compliant, and is HIPAA eligible.
* You can also control network access via VPC Security Group rules.

### Accesibility
* You can access your file systems from Amazon EC2 instances, and from on-premises computers using AWS Direct Connect or AWS VPN.
* It also provides read-after-write consistency and supports file locking.
* Amazon FSx for Lustre is POSIX-compliant, so you can use your current Linux-based applications without having to make any changes.

