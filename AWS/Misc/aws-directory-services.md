### What is Microsoft Active Directory (AD)?
* Active Directory is a directory service that enables administrators to manage and secure their IT resources.
* AD stores information about network objects (e.g. users, groups, systems, networks, applications, digital assets, and many others) and their relationship to one another
* Admins can use AD to create users and grant them access to Windows laptops, servers, and applications.
* They can also use AD to control groups of systems simultaneously, enforcing security settings and software updates.
* Supported Protocols:
  * **DNS Protocol**
  * **Lightweight Directory Access Protocol (LDAP)**
  * **Kerberos**
* Please note that other protocols such as SAML and RADIUS aren't supported as of now.
* Objects are organized in trees. A group of trees is a forest.

### What is ADFS (AD Federation Services)?
* ADFS is a Single Sign0On (SSO) Solution
* It provides users with authenticated access to applications that are not capable of using Integrated Windows Authentication (IWA) through Active Directory (AD).
* SAML based assertion across 3rd parties: AWS Console, Dropbox, Office365 etc.
* Working:
  * ADFS manages authentication through a proxy service hosted between AD and the target application.
  * It uses a Federated Trust, linking ADFS and the target application to grant access to users.
  * This enables users to log onto the federated application through SSO without needing to authenticate their identity on application directly.

![Image1](https://github.com/promisinganuj/cloud/blob/master/AWS/Misc/ad-federation-service.jpg)

The authentication process generally follows these four steps:
1. The user navigates to a URL provided by the ADFS service.
2. The ADFS service then authenticates the user via the organization’s AD service.
3. Upon authenticating, the user receives a SAML assertion in the form of an authentication response from AD FS.
4. The user's browser automatically posts the SAML assertion to the AWS sign-in endpoint for SAML (https://signin.aws.amazon.com/saml). The endpoint uses the **AssumeRoleWithSAML** API to request temporary security credentials and then constructs a sign-in URL for the AWS Management Console using those credentials.
5. User's browser receives the sign-in URL and redirects to the AWS Management Console.

### What are different AWS Directory Services?
1. **AWS Managed Microsoft AD** - Enables use of managed Active Directory in the AWS Cloud
2. **AD Connector** - Enables on-premises users to access AWS services via Active Directory
3. **Simple AD** - Provides low-scale, low-cost basic Active Directory capability

## AWS Direcorry Services - AWS Managed Microsoft AD

### What is AWS Managed Microsoft AD
* Managed Service: Microsoft AD in AWS VPC
* AWS Managed Microsoft AD directories are deployed across two Availability Zones in a region by default and connected to your Amazon Virtual Private Cloud (VPC).
* Backups are automatically taken once per day, and the Amazon Elastic Block Store (EBS) volumes are encrypted to ensure that data is secured at rest.
* You can add additional domain controllers to your managed domain.
* EC2 Windows Instances:
  * EC2 Windows instances can join the domain and run traditional AD applications (sharepoint, etc)
  * Seamlessly Domain Join Amazon EC2 Instances from Multiple Accounts & VPCs
* Supports **MFA**
* Integrations:
  * RDS for SQL Server, AWS Workspaces, Quicksight…
  * AWS SSO to provide access to 3rd party applications
* It can be a standalone repository in AWS or joined to on-premise AD by establishing forest "trust"

### How do you connect AWS Managed Microsoft AD to On-Premise AD?
* As mentioned above, AWS Managed Microsoft AD can be connected to on-premise AD.
* For that, these has to be a Direct Connect(DX) or VPN connection
* Three kind of forest trust can be setup:
  * One-way trust: AWS => On-Premise
  * One-way trust: On-Premise => AWS
  * Two-way forest trust: AWS <=> On-Premise
* Please note here that forest trust is different than synchronization (replication is not supported).

### How can we minmize latency between on-premise AD and AWS Managed Microsoft AD?
* Please note that replication is not supported.
* For that, you need to deploy Microsoft AD on EC2 instance and setup self-managed replication.
* Finally, establish 2-way forest trust between the Microsoft AD on EC2 and AWS Managed Microsoft AD.

### Whar are the different use-cases for AWS Managed Microsoft AD?
The following diagram shows some of the use cases for your AWS Managed Microsoft AD directory. These include the ability to grant your users access to external cloud applications and allow your on-premises AD users to manage and have access to resources in the AWS Cloud.

![Image2](https://github.com/promisinganuj/cloud/blob/master/AWS/Misc/ms_ad_use_cases.png)

* Use Case 1: Sign In to AWS Applications and Services with AD Credentials
* Use Case 2: Manage Amazon EC2 Instances
* Use Case 3: Provide Directory Services to Your AD-Aware Workloads 
* Use Case 4: SSO to Office 365 and Other Cloud Applications
* Use Case 5: Extend Your On-Premises AD to the AWS Cloud
* Use Case 6: Share Your Directory to Seamlessly Join Amazon EC2 Instances to a Domain Across AWS Accounts

## AWS Directory Services - AD Connector

### What is AD Connector?
* AD Connector is a directory gateway to redirect directory requests to your on-premises Microsoft Active Directory
* It **doesn't have caching capability**. All authentication, lookup, and management requests are handled by on-premise Active Directory.
* You can **enable multi-factor authentication (MFA) for AD Connector**, but you’ll need to have an existing RADIUS infrastructure in your on-premises network set up to leverage this feature.
* Manage users solely on-premise, no possibility of setting up a trust
* Highly dependent on VPN or Direct Connect. If DX/VPN goes down, the AD is no longer accessible.
• Doesn’t work with SQL Server, doesn’t do seamless joining, can’t share directory

### What are some of the use-cases for AD Connector?
* **Sign in to AWS applications** such as Amazon WorkSpaces, Amazon WorkDocs, and Amazon WorkMail by using your Active Directory credentials.
* **Seamlessly join Windows instances** to your Active Directory domain either through the Amazon EC2 launch wizard or programmatically through the EC2 Simple System Manager (SSM) API.
* **Provide federated sign-in** to the AWS Management Console by mapping Active Directory identities to AWS Identity and Access Management (IAM) roles

### How does AD Connector works?
The following diagram illustrates the authentication flow and network path when you enable AWS Management Console access:

![Image3](https://github.com/promisinganuj/cloud/blob/master/AWS/Misc/ad-connector.png)

1. A user opens the secure custom sign-in page and supplies their Active Directory user name and password.
2. The authentication request is sent over SSL to AD Connector.
3. AD Connector performs LDAP authentication to Active Directory.
4. After the user has been authenticated, AD Connector calls the STS AssumeRole method to get temporary security credentials for that user. Using those temporary security credentials, AD Connector constructs a sign-in URL that users use to access the console.

**Note:** If a user is mapped to multiple roles, the user will be presented with a choice at sign-in as to which role they want to assume. The user session is valid for 1 hour.

### Additional details about AD Connector
* AD Connector comes in two sizes: small and large. A large AD Connector runs on more powerful compute resources and is more expensive than a small AD Connector.
* **AD Connector is highly available**, meaning underlying hosts are deployed across multiple Availability Zones in the region you deploy. In the event of host-level failure, Directory Service will promptly replace failed hosts. Directory Service also applies performance and security updates automatically to AD Connector.

