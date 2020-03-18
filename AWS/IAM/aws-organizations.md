## MULTI ACCOUNTS
### What would companies use multiple AWS Accounts?
* **For Security Reasons** - Some departments might not want to share their data or resources.
* **Mergers/Acqusitions** - If you want to onboard a business which already has existing AWS Account.
* **Legal Requirement** - Your organization might be working in multiple geographic area with different legal requirements.
* **Envrionmental Segregation** - You might want to have different accounts for Dev/Test/Prod

### What are some of the key considerations of having multiple AWS Accounts?
* **Service Limits** - AWS service limits works at an individual account level. So, instead of one service limit for the entire organization, each account will have it's own service limit.
* **Support Cost** - AWS support is per AWS account. Having multiple account means more cost for AWS support.
* **Reserved Instances** - The capacity reservation for an RI applies only to the account the RI was purchased on. Use OU instead.

### What are some of the best practices around multiple accounts?
* Using group aliases for account email addresses.
  * Use group aliases for all notifications on your account
* Create and enforce resource tagging standards.
  * Can be programmatically controlled using Resouce Group Tagging APIs
* Leverege AWS APIs and scripts
  * AWS APIs and custom scripts can be used to automatically and consistently apply baseline congfiguration across multiple AWS accounts.
  * For Ex: compliance-monitoring scripts

## AWS ORGANIZATIONS

## What are AWS Organizations?
* AWS Organizations is an account management service that enables you to consolidate multiple AWS accounts into an organization that you create and centrally manage.
* AWS Organizations includes account management and consolidated billing capabilities that enable you to better meet the budgetary, security, and compliance needs of your business.
* As an administrator of an organization, you can create accounts in your organization and invite existing accounts to join the organization.

## What are some of the key features of AWS Organizations?
* Hierarchical grouping of your accounts
* 
