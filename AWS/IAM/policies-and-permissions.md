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

### What is the Categorization of Identity-Based Policies?
* **Managed Policies**: Standalone identity-based policies that you can attach to multiple users, groups, and roles in your AWS account. You can use two types of managed policies:
  * **AWS managed policies**: Managed policies that are created and managed by AWS.
  * **Customer managed policies**: Managed policies that you create and manage in your AWS account.
  
* **Inline policies**: Policies that you create and manage and that are embedded directly into a single user, group, or role. In most cases, using inline policies **is not recommended**.

## General notes about various policy types
* Resource-based policies are **inline policies**. Ther are **no managed resource-based policies**.
* When the principal and the resource are in separate AWS accounts, you must also use an identity-based policy to grant the principal access to the resource, in addition to adding a cross-account principal to a resource-based policy.
* However, if a resource-based policy grants access to a principal in the same account, no additional identity-based policy is required.
* An IAM role is both an identity and a resource that supports resource-based policies. For that reason, you must attach both a trust policy and an identity-based policy to an IAM role.
* **Resource-based policies** that specify the user or role as the principal **are not limited by the permissions boundary.**
* **You cannot attach identity-based policies to the root user, and you cannot set the permissions boundary for the root user.**

## General notes about SCPs
* **The SCP limits permissions for entities in member accounts, including each AWS account root user.**
* SCPs aren't available if your organization has enabled only the consolidated billing features.
* SCPs affect only principals that are managed by accounts that are part of the organization.
* SCPs don't affect resource-based policies directly.
* SCPs also don't affect users or roles from accounts outside the organization.
* SCPs do not affect any service-linked role.
* **SCPs do not affect actions performed by the master account.**
* **Though SPCs affect the root users, it doesn't restict root user from managing root credentials.**

## JSON Policy Document Structure
The information in a statement is contained within a series of elements:
* **Version** – Specify the version of the policy language that you want to use. As a best practice, use the latest 2012-10-17 version.
* **Statement** – Use this main policy element as a container for the following elements. You can include more than one statement in a policy.
* **Sid (Optional)** – Include an optional statement ID to differentiate between your statements.
* **Effect** – Use Allow or Deny to indicate whether the policy allows or denies access.
* **Principal (Required in only some circumstances)** – If you create a resource-based policy, you must indicate the account, user, role, or federated user to which you would like to allow or deny access. If you are creating an IAM permissions policy to attach to a user or role, you cannot include this element. The principal is implied as that user or role.
* **Action** – Include a list of actions that the policy allows or denies.
* **Resource (Required in only some circumstances)** – If you create an IAM permissions policy, you must specify a list of resources to which the actions apply. If you create a resource-based policy, this element is optional. If you do not include this element, then the resource to which the action applies is the resource to which the policy is attached.
* **Condition (Optional)** – Specify the circumstances under which the policy grants permission.

### What is the policy evaluation logic?
* If a policy includes multiple statements, AWS applies a logical OR across the statements when evaluating them. 
* If multiple policies apply to a request, AWS applies a logical OR across all of those policies when evaluating them.
### Determining Whether a Request Is Allowed or Denied Within an Account
The following is a high-level summary of the AWS evaluation logic on those policies within a single account.
* By default, all requests are implicitly denied. (Alternatively, by default, the AWS account root user has full access.)
* An explicit allow in an identity-based or resource-based policy overrides this default.
* If a permissions boundary, Organizations SCP, or session policy is present, it might override the allow with an implicit deny.
* An explicit deny in any policy overrides any allows.

The following flow chart provides details about how the decision is made.

![Image4](https://github.com/promisinganuj/cloud/blob/master/AWS/IAM/PolicyEvaluationHorizontal.png)
