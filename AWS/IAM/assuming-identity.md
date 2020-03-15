### What are the IAM Roles? How are they different from IAM Users?
* An IAM role is an IAM identity that you can create in your account that has specific permissions.
* Similarity - Both the AWS identities with permission policies that determines what the identity can and can't do in AWS.
* Difference - IAM user is assigned to person (usually one). Role is "Assumed" by anyone who needs it.
* Difference - Roles doesn't have standard long-term credentials (password/access key etc).
* When a role is assumed, it provided temporary securtiy credentials for the session.
* You can use roles to delegate access to users, applications, or services that don't normally have access to your AWS resources.

### Who can use a Role?
* An IAM user in the same AWS account as the role
* An IAM user in a different AWS account than the role
* A web service offered by AWS such as Amazon EC2
* An external user authenticated by an external identity provider (IdP) service that is compatible with SAML 2.0 or OpenID Connect, or a custom-build identity broker.

### What are the different scenarios in which Roles can be used?
* To grant users in your AWS account access to resources they don't usually have.
* To grant users in one AWS account access to resources in another account.
* To allow a mobile app to use AWS resources without embedding AWS keys within the app.
* To give AWS access to users who already have identities defined outside of AWS, such as in your corporate directory.
* To grant acccess to third parties so that they can perform an audit on your resources.

## Common Scenarios

### Providing acccess to an IAM User in another AWS account that you own
* You can grant your IAM users permission to switch to roles within your AWS account or to roles defined in other AWS accounts that you own.
* This approach adds several layers of protection such as:
  * The users permission to assume the role has to be EXPLICITLY granted
  * The users mush actively switch to the role which can tracked and audited.
  * You can add multi-factor authentication (MFA) protection to the role so that only users who sign in with an MFA device can assume the role.
* THe "Principle of least privileges" is recommended.

### Providing access to AWS accounts owner by Third Parties
* When third parties require access to your organization's AWS resources, you can use roles to delegate access to them.
* "IAM Access Analyzer" can be used to check whether principals in accounts outside of your zone of trust (trusted organization, OU, or account) have access to assume your roles.
* Third party needs to provide the following information to you:
  * The third party's AWS account ID
  * The permissions required
  * An external ID to uniquely associate with the role. The external ID can be any secret identifier that is known by you and the third party.
  
### Providing access to an AWS Service
* Many AWS services require that you use roles to control what that service can access.
* A role that a service assumes to perform actions on your behalf is called a service role.

### Providing access to Externally authenticated users (Identity Federation)
* You can use an IAM role to specify permissions for users whose identity is federated from your organization or a third-party identity provider (IdP).
* Some examples are:
  * Federating Users of a Mobile or Web-based App with Amazon Cognito
  * Federating Users with Public Identity Service Providers or OpenID Connect (Web Identity Federation)
  * Federating users with SAML 2.0
  * Federating users by creating a custom identity broker application

### What is Identity Federation?
* It's the process of creating a trust relationship between an external identity provider and AWS.
* Instead of creating an IAM user, you can use existing identities from AWS Directory Service, your enterprise user directory, or a web identity provider, which is called as Federated User.
* When you use OIDC and SAML 2.0 to configure a trust relationship between these external identity providers and AWS, the user is assigned to an IAM role.
* The user also receives temporary credentials that allow the user to access your AWS resources.
* With Federation, user can:
  * Sign in to a web identity provider, such as Login with Amazon, Facebook, Google or any IdP compatible with OpenID Connect (OIDC).
  * Sign in to an enterprise identity system compatible with Security Assertion Markup Language (SAML) 2.0 such as Microsoft AD Federation Services.
  
### What is Web Identity Federation?
* With web identity federation, you don't need to create custom sign-in code or manage your own user identities.
*  Instead, users of your app can sign in using a well-known external identity provider (IdP), such as Login with Amazon, Facebook, Google, or any other OpenID Connect (OIDC)-compatible IdP.
* They can receive an authentication token, and then exchange that token for temporary security credentials in AWS that map to an IAM role with permissions to use the resources in your AWS account.
* For most scenarios, Amazon Cognito is recommended because it acts as an identity broker and does much of the federation work for you.
* Else, you must write code that interacts with a web IdP, such as Facebook, and then calls the "AssumeRoleWithWebIdentity" API to trade the authentication token you get from those IdPs for AWS temporary security credentials.

![Image1](https://github.com/promisinganuj/cloud/blob/master/AWS/IAM/mobile-app-web-identity-federation.png)

To get a better understanding of how web identity federation works, please try out [Web Identity Federation Playground](https://web-identity-federation-playground.s3.amazonaws.com/index.html). This interactive website lets you walk through the process of authenticating via Login with Amazon, Facebook, or Google, getting temporary security credentials, and then using those credentials to make a request to AWS. For instructions regarding using the playgroud, please check the [AWS Security Blog](https://aws.amazon.com/blogs/security/new-playground-app-to-explore-web-identity-federation-with-amazon-facebook-and-google/).
