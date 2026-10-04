# Organizations
* Management account - root of the Organization hierarchy
* Group accounts into Organizational Units (OUs)
* Create accounts programmatically using Organizations API
* Invite existing accounts to join
* Move accounts between OUs
* Remove account from Organizations vs Closing an Account
* Apply Service Control Policies (SCPs)
* Enable CloudTrail in management account and apply to members. Members cannot modify it. Logs go to a central S3 bucket in a Log Archive account.
* Consolidated billing
* ALL_FEATURES vs Consolidated Billing Only

# Service Control Policies
* Controls the maximum available permissions (boundaries, guardrails, not grants).
* SCP applies to all IAM users and roles in a member account, including the root user. 
  * They do not affect service-linked roles or the management account.
* Can't be applied in Management Account.
* Still need IAM policy to perform actual actions
* Tag policy enforces tag standardization
* Permission set at a higher level does not flow down to children!!!
* Explicit denies always override any kind of allows. i.e. An explicit Deny cannot be overridden.
* An explicit allow overrides an implicit deny (i.e. SCP not defined)
* Does not restrict the management account. Do not run workloads there.

# SCP Common Patterns
* Region restriction with aws:RequestedRegion, using a NotAction exemption for global services like IAM, CloudFront, Route 53 and Support.
* Stop accounts from leaving the org (organizations:LeaveOrganization)
* Protect CloudTrail, Config and GuardDuty from being disabled
* Exempt an admin or break-glass role with aws:PrincipalArn in a condition.
* Require encryption or specific instance types

## Deny List Strategy
* The FullAWSAccess SCP is attached to every OU and account
* Explicitly allows all permissions to flow down from the root
* Can explicitly override with a deny in an SCP
* Default setup

## Allow List Strategy
* The FullAWSAccess SCP is removed from every OU and account
* To allow a permission, SCPs with allow statements must be added to the account and every OU above it including root.
* Every SCP in the hierarchy must explicitly allow the permissions required

# Control Tower
* A landing zone is a well-architected multi-account baseline
* Control Tower creates a landing zone with pre-defined OUs (Security, Sandbox, Production, etc.).
* Account Factory and Account Factory for Teraform. Default Security OU with Log Archive and Audit Accounts
* It uses guardrails for governance and compliance:
  * Preventive guardrails using preconfigured SCPs and disallow API actions
  * Detective guardrails using Config rules and Lambda functions and monitor and govern compliance
  * Proactive: CloudFormation Hooks: a feature to ensure that your CloudFormation resources, stacks, and change sets comply with your organization's security, operational, and cost optimization best practices.
* The root user in the management account are unrestricted
* Can connect to IAM Identity Center for SSO. Directory Source can be IAM Identity Center, SAML 2.0 IdP, MS AD. SCIM support.

# Other Policy Types
* Tag policies: standardize tag keys and values. Pair tag policies with SCP to enforce compliant resources and prevent untagged resources.
* AI service opt-out policies
* Chatbot policies
* Declarative policies. e.g. EC2 settings such as blocking public AMI sharing or enforcing IDMSv2

# Common Exam Traps
* An SCP won't fix a problem in the management account
* A Region-deny SCP without the global-service exemption breaks IAM, STS and other global services
* Invited accounts lack OrganizationAccountAccessRole
* Running security tooling from the management account is wrong: enable trusted access for the security service in the management account, and register a member account as the service's delegated admin.
* 