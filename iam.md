# Concepts
* User
* Group
* IAM Role - for delegation. Has
  * trust policies - examples of resource based policy
  * and permissions policies - example of identity based policy
* Principal - user or app that acn make a request for an action or operation on an AWS resource
* Policy
  * Identity-based
    * Inline policy - 1-1 relationship with the user, group or role
    * Managed Policy - AWS or customer managed
  * Resource-based policy
    * JSON docs attached to a resource
    * Define principal for the action and resource
* Role-based access control and attribute-based access control
  * Attributes - tags (key and value) which can be associated to the principals or the resources
* Permission boundry - attached to principals. 
  * IAM principals can't alter the permission boundary to allow their own permissions to access restricted services. 
  * IAM principals must attach the permission boundary to any IAM principals they create. 
  * Ensures users created has less permission than the creator, avoids situation where an IAM admin can create super user to do bad things.  

# Evaluating Policies within an Account
* Identity-based policy allows and Resource-based policy allows => Union
* Identity-based policy allows and Permission-boundary allows => Intersection
* Identity-based policy allows and Organizational SCP allows => Intersection

# Determination Rules
* By default everything is denied implicitly
* Explicit allow in Identity-based or resource-based policy overrides the implicit deny
* Explicit deny in Organizational SCP, Permission boundary or session policy overrides the explicit allow.
* An explicit deny in any policy will always override any allows
* Evaluation Order: Any explicit denies => Organization SCP => Resource-based policy (explicit allow ends flow) => Permission boundary => Session Policy => Identity-based policy (explicit allow ends flow)
