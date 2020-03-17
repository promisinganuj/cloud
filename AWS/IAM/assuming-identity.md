## IAM ROLES
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

## COMMON SCENARIOS FOR USING ROLES

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

## Security Token Service (STS)
### What is AWS Security Token Service (STS)
* STS is a web service that enables you to request temporary, limited-privilege credentials for AWS IAM users or for users that you authenticate (federated users).
* Temporary security credentials are short-term, as the name implies. They can be configured to last for anywhere from a few minutes to several hours. After the credentials expire, AWS no longer recognizes them or allows any kind of access from API requests made with them.
* Temporary security credentials are not stored with the user but are generated dynamically and provided to the user when requested.

### What are the use cases for STS?
* Identity Federation
  * Enterprise identity federation (authenticated through your company's network)
    * STS supports SAML which allows for the use of Microsoft AD or your own solution.
  * Web Identity Federation (third party providers such as Facebook, Google, Twitter and Amazon)
* Roles for Cross-Account Access
  * Used for organizations that have more than one AWS account
* Roles for Amazon EC2 (and Other AWS Services)
  * Allow an application running on an EC2 instance to access other AWS services without having to embed credentials.
* Please note that for mobile applications, AWS recommends using Cognito rather than STS. Cognito provides additional mobile-specific functionality that makes the flow easier to manager.

### What are the different STS API Calls?
 1. **AssumeRole** — Cross Account Delegation and Federation Through a Custom Identity Broker
    * Supports MFA
 2. **AssumeRoleWithWebIdentity** — Federation Through a Web-Based Identity Provider
    * Caller must pass a web identity token that indicates authentication from a known identity provider
 3. **AssumeRoleWithSAML** — Federation Through an Enterprise Identity Provider Compatible with SAML 2.0
    * Caller must pass a SAML authentication response that indicates authentication from a known identity provider
 4. **GetFederationToken** — Federation Through a Custom Identity Broker
    * Default expiration period is substantially longer (12 hours instead of one hour).
 5. **GetSessionToken** — Temporary Credentials for Users in Untrusted Environments
    * Supports MFA

### What does an STS call return?
* A credential object which contains:
  * A session token
  * An access key ID
  * A secret access key
  * An expiration timestamp

## IDENTITY FEDERATION
### What is Identity Federation?
* It's the process of creating a trust relationship between an external identity provider and AWS.
* Instead of creating an IAM user, you can use existing identities from AWS Directory Service, your enterprise user directory, or a web identity provider, which is called as Federated User.
* When you use OIDC and SAML 2.0 to configure a trust relationship between these external identity providers and AWS, the user is assigned to an IAM role.
* The user also receives temporary credentials that allow the user to access your AWS resources.
* With Federation, user can:
  * Sign in to a web identity provider, such as Login with Amazon, Facebook, Google or any IdP compatible with OpenID Connect (OIDC).
  * Sign in to an enterprise identity system compatible with Security Assertion Markup Language (SAML) 2.0 such as Microsoft AD Federation Services.

### What are the different types of Identity Federation in AWS?
1. SAML 2.0
2. Custom Identity Broker
3. Web Identity Federation with Amazon Cognito
4. Web Identity Federation without Amazon Cognito
5. Single Sign On
6. Non-SAML with AWS Microsoft AD
  
### What is Web Identity Federation?
* With web identity federation, you don't need to create custom sign-in code or manage your own user identities.
*  Instead, users of your app can sign in using a well-known external identity provider (IdP), such as Login with Amazon, Facebook, Google, or any other OpenID Connect (OIDC)-compatible IdP.
* They can receive an authentication token, and then exchange that token for temporary security credentials in AWS that map to an IAM role with permissions to use the resources in your AWS account.
* For most scenarios, Amazon Cognito is recommended because it acts as an identity broker and does much of the federation work for you.
* Else, you must write code that interacts with a web IdP, such as Facebook, and then calls the **"AssumeRoleWithWebIdentity"** API to trade the authentication token you get from those IdPs for AWS temporary security credentials.

![Image1](https://github.com/promisinganuj/cloud/blob/master/AWS/IAM/mobile-app-web-identity-federation.png)

To get a better understanding of how web identity federation works, please try out [Web Identity Federation Playground](https://web-identity-federation-playground.s3.amazonaws.com/index.html). This interactive website lets you walk through the process of authenticating via Login with Amazon, Facebook, or Google, getting temporary security credentials, and then using those credentials to make a request to AWS.

For instructions regarding using the playgroud, please check the [AWS Security Blog](https://aws.amazon.com/blogs/security/new-playground-app-to-explore-web-identity-federation-with-amazon-facebook-and-google/).

### What is SAML 2.0-based Federation
* SAML 2.0 (Security Assertion Markup Language 2.0) is an open standard that many identity providers (IdPs) use.
* This feature enables federated single sign-on (SSO), so users can log into the AWS Management Console or call the AWS API operations without you having to create an IAM user for everyone in your organization.
* It provides access to AWS Console or CLI
* Here is an example:
![Image2](https://github.com/promisinganuj/cloud/blob/master/AWS/IAM/saml-based-federation.png)

1. A user in your organization uses a client app to request authentication from your organization's IdP.
2. The IdP authenticates the user against your organization's identity store.
3. The IdP constructs a SAML assertion with information about the user and sends the assertion to the client app.
4. The client app calls the AWS STS **"AssumeRoleWithSAML"** API, passing the ARN of the SAML provider, the ARN of the role to assume, and the SAML assertion from IdP.
5. The API response to the client app includes temporary security credentials.
6. The client app uses the temporary security credentials to call Amazon S3 API operations.

Please note here that if you want to allow user to access AWS Management Console, it would require the use of the **AWS SSO Endpoing** instead of directly calling the **"AssumeRoleWithSAML"** API. The endpoint calls the API for the user and returns a URL that automatically redirects the user's browser to the AWS Management Console.

![Image3](https://github.com/promisinganuj/cloud/blob/master/AWS/IAM/saml-based-sso-to-console.png)

### What is Customer Identity Broker Federation?
* It's used only if identity provider is not compatible with SAML 2.0
* The identity broker must determine the appropriate IAM policy
* Uses the STS API: **AssumeRole** or **GetFeredationToken**

![Image4](https://github.com/promisinganuj/cloud/blob/master/AWS/IAM/custom-identity-broker-application.png)

* This scenario has the following attributes:
  * The identity broker application has permissions to access IAM's token service (STS) API to create temporary security credentials.
  * The identity broker application is able to verify that employees are authenticated within the existing authentication system.
  * Users are able to get a temporary URL that gives them access to the AWS Management Console (which is referred to as single sign-on).
