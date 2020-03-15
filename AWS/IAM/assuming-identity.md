## What are the IAM Roles? How are they different from IAM Users?
* An IAM role is an IAM identity that you can create in your account that has specific permissions.
* Similarity - Both the AWS identities with permission policies that determines what the identity can and can't do in AWS.
* Difference - IAM user is assigned to person (usually one). Role is "Assumed" by anyone who needs it.
* Difference - Roles doesn't have standard long-term credentials (password/access key etc).
* When a role is assumed, it provided temporary securtiy credentials for the session.
* You can use roles to delegate access to users, applications, or services that don't normally have access to your AWS resources.

## Who can use a Role?
* An IAM user in the same AWS account as the role
* An IAM user in a different AWS account than the role
* A web service offered by AWS such as Amazon EC2
* An external user authenticated by an external identity provider (IdP) service that is compatible with SAML 2.0 or OpenID Connect, or a custom-build identity broker.

## What are the different scenarios in which Roles can be used?
* To grant users in your AWS account access to resources they don't usually have.
* To grant users in one AWS account access to resources in another account.
* To allow a mobile app to use AWS resources without embedding AWS keys within the app.
* To give AWS access to users who already have identities defined outside of AWS, such as in your corporate directory.
* To grant acccess to third parties so that they can perform an audit on your resources.

## What is Identity Federation?
* It's the process of creating a trust relationship between an external identity provider and AWS.
* Instead of creating an IAM user, you can use existing identities from AWS Directory Service, your enterprise user directory, or a web identity provider, which is called as Federated User.
* When you use OIDC and SAML 2.0 to configure a trust relationship between these external identity providers and AWS, the user is assigned to an IAM role.
* The user also receives temporary credentials that allow the user to access your AWS resources.
* With Federation, user can:
  * Sign in to a web identity provider, such as Login with Amazon, Facebook, Google or any IdP compatible with OpenID Connect (OIDC).
  * Sign in to an enterprise identity system compatible with Security Assertion Markup Language (SAML) 2.0 such as Microsoft AD Federation Services.
