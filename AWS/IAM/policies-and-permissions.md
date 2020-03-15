## POLICIES AND PERMISSIONS
### What are AWS Policies?
* A policy is an object in AWS that, when associated with an identity or resource, defines their permissions.
* Acces in AWS is managed by creating policies and attaching them to IAM identities (users,groups,roles) or AWS resources.
* AWS evaluates these policies when an IAM principal (user or role) makes a request. 
* Permissions in the policies determine whether the request is allowed or denied.
* Most policies are stored in AWS as JSON documents.

### What are the different policy types in AWS?
There are **SIX** different policy types available for use in AWS:
1. Identity-based policies
   * Attach **managed and inline policies** to **IAM identities (users, groups to which users belong, or roles)**. 
   * Identity-based policies grant permissions to an **identity**.

2. Resource-based policies
   * Attach **inline policies** to **resources**.
   * The most common examples of resource-based policies are Amazon S3 bucket policies and IAM role trust policies.
   * Resource-based policies **grant permissions to the principal that is specified in the policy**.
   * Principals can be in the same account as the resource or in other accounts.

3. Permissions boundaries
   * Use a **managed policy** as the permissions boundary for an IAM entity (user or role).
   * That policy defines the maximum permissions that the identity-based policies can grant to an entity, but does not grant permissions.
   * Permissions boundaries **do not define the maximum permissions that a resource-based policy can grant** to an entity.
   
4. Organizations Service Control Policies (SCPs)
   * Use an AWS Organizations service control policy (SCP) to define the maximum permissions for account members of an organization or organizational unit (OU).
   * SCPs limit permissions that identity-based policies or resource-based policies grant to entities (users or roles) within the account, but do not grant permissions.

5. Access Control Lists (ACLs)
   * Use ACLs to control which principals in other accounts can access the resource to which the ACL is attached.
   * ACLs are similar to resource-based policies, although **they are the only policy type that does not use the JSON policy document structure**.
   * ACLs are cross-account permissions policies that grant permissions to the specified principal. 
   * **ACLs cannot grant permissions to entities within the same account**.

6. Session policies
   * Pass advanced session policies when you use the AWS CLI or AWS API to assume a role or a federated user.
   * Session policies **limit the permissions that the role or user's identity-based policies grant to the session**.
   * Session policies limit permissions for a created session, but do not grant permissions.

### What are the Permissions Boundaries for IAM Entities?
