### How to you grant access to resources in your account to 3rd party accounts? - The Confused Deputy Problem
* Zone of Trust - Account, Organizations that you own
* 3rd Parties - Outsize your Zone of Trust
* Use [IAM Access Analyzer](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html "Access Analyzer") to find out which resources are exposed.
* For granting access to a 3rd party:
  * The 3rd Party AWS Account ID
  * **ExternalID** (Secret Between you and the 3rd party)
    * To uniquely associate with the role between you and the 3rd party.
    * Must be provided when defining the trust and when assuming the role.
    * Must be chosen by the 3rd party.
* Define permissions in the IAM Policy

Further Reading: [The Confused Deputy Problem](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)
