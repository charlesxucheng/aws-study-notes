# Concepts
* User
* Group
* Principal - user or app that can make a request for an action or operation on an AWS resource
* IAM Role - for delegation

# Policies 
Identity-based vs Resource-based: https://www.jbtechbytes.com/api/html-posts/aws-iam-policies-vs-resource-policies-complete-guide.html

* Identity-based
  * Attached to users, groups and roles
  * Inline policy - 1-1 relationship with the user, group or role
  * Managed Policy - AWS or customer managed
* Resource-based policy
  * Attached to resources
  * JSON docs attached to a resource
  * Has a Principal field that defines WHO can access the resource
  * Suitable for cross-account access and service-to-service permissions
  * Still have the "Resource" field to apply further restrictions if required. Value should match the resource it is attached to.

With regard to Policies attached to roles:
* Trust policies - defines who(which principal) can assume the role
  * It is a resource based policy attached to the role as the resource
  * Typical action of the policy is sts:AssumeRole, also can have other sts actions like AssumeRoleWithWebIdentity/AssumeRoleWithSAML and TagSession.
* Permissions policies - defines what the role can do once it's assumed
  * It is an identity based policy **also** attached to the role as the implicit principal

* You can use conditions in your IAM policies to control access to AWS resources based on the tags on that resource. 
* Placeholder variables can be used in the policies to perform dynamic behavior (e.g. user can stop only EC2 instances with tag matching the username.

* Session Principals
  * Once a principal assumes the role, they become a session principal.
  * This session principal's effective permissions are the intersection of the role's identity-based policies and any optional session policies passed during the assumption request.

* Role-based access control and attribute-based access control
  * Attributes - tags (key and value) which can be associated to the principals or the resources. Tags are matched in the policy conditions.

# Permission boundries
  * Custom policy, attached to principals. Defines the max allowable access.
  * IAM principals can't alter the permission boundary to allow their own permissions to access restricted services. 
  * IAM principals must attach the permission boundary to any IAM principals they create. 
  * Ensures users created has less permission than the creator, avoids situation where an IAM admin can create another super user to do bad things.  

# Evaluating Policies within an Account
* Identity-based policy allows and Resource-based policy allows => Union
* Identity-based policy allows and Permission-boundary allows => Intersection
* Identity-based policy allows and Organizational SCP (of the account the principal belongs to) explicitly allows => Intersection

# Determination Rules
* By default everything is denied implicitly
* Explicit allow in Identity-based or resource-based policy overrides the implicit deny
* **Implicit** deny in Organizational SCP, Permission boundary or session policy overrides the explicit allow.
* An explicit deny in any type of policy will always  override any allows
* Evaluation Order: Any explicit denies => Organization SCP => Resource-based policy (explicit allow ends flow) => Permission boundary => Session Policy => Identity-based policy (explicit allow ends flow)

# IAM Best Pratices
* Lock away root user access keys
* Create individual IAM users
* Use groups to assign permission to IAM users
* Grant least privilege
* Get started with AWS managed policies
* Use customer managed policies instead of linline policies
* Use access levels to reviwe IAM permissions
* Configure a strong password policy for users
* Enable MFA
* Use roles for applications that run on Amazon EC2 instances
* Use roles to delegate permissions
* Do not share access keys
* Rotate credentials regularly
* Remove unnecessary credentials
* Use policy conditions for extra security
* Monitor activity in AWS account

SCPs do not affect any service-linked role. Service-linked roles enable other AWS services to integrate with AWS Organizations and can't be restricted by SCPs.

In IAM, you create one or more IAM roles for the federated users. In the role’s trust policy, you need to set the SAML provider as the principal, which establishes a trust relationship between your organization and AWS.

Ensure that the ARN of the SAML provider, the ARN of the created IAM role, and SAMS assertion from the IdP are all included when the federated identity web portal calls the AWS STS AssumeRoleWithSAML API

