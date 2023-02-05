# Organizations
* Management account - root of the Organization hierarchy
* Group accounts into Organizational Units (OUs)
* Create accounts programmatically using Organizations API
* Apply Service Control Policies (SCPs)
* Enable CloudTrail in management account and apply to members
* Consolidated billing
* Enable AWS SSO using on-prem directory

# Service Control Policies
* Controls the maximum available permissions (boundaries). Can't be applied in Management Account.
* Still need IAM policy to perform actual actions
* Tag policy enforces tag standardization
* Explicit denies always override any kind of allows.
* An explicit allow overrides an implicit deny (i.e. SCP not defined)

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
* It uses guardrails for governance and compliance:
  * Preventive guardrails using preconfigured SCPs and disallow API actions
  * Detective guardrails using Config rules and Lambda functions and monitor and govern compliance
* The root user in the management account are unrestricted
