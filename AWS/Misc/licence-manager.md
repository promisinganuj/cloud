## AWS License Manager - Main Features
* AWS License Manager makes it easy for you to manage licenses in AWS and on-premises servers from software vendors such as Microsoft, SAP, Oracle, and IBM.
* AWS License Manager lets administrators create customized licensing rules that emulate the terms of their licensing agreements, and then enforces these rules when an instance of EC2 gets launched.

* Supported Licence Types
  * vCPU
  * Cores
  * Sockets
  * Instances

* Cross-Account Usage
  * AWS License Manager works with AWS Organizations. Sign in to your Master account, link all of the accounts, and share license configurations across your Organization.
  
* Multi-Account Software Discovery
  * AWS License Manager also works with AWS Systems Manager and across accounts within an Organization.
  * The discovered data is stored in an S3 bucket and an Amazon Athena database (encrypted in both places) and is processed by a AWS Glue job.
  
* Programmatic Access
  * You can create and manage license configurations from the Console, APIs, or the AWS Command Line Interface (CLI).
  * CreateLicenseConfiguration
  * GetLicenseConfiguration
  * ListResourceInventory
  * ListUsageForLicenseConfiguration

* Pricing
  * There is no charge for AWS License Manager but there are charges for data storage and analysis.
  * AWS License Manager stores inventory data in an S3 bucket and an Amazon Athena database and processes it using AWS Glue.
