# AWS Directory Services
- Managed Microsoft AD
  - HA pair of Windows Server Domain Controllers
  - Can connect to on-prem AD via VPN (1- or 2-way trust relationship)
  - Can synchronize users and federate identities with Azure AD or Office 365
  - Use cases:
    - Extend on-prem AD to AWS
    - Manage Windows-based workloads in AWS (EC2, FSx, RDS SQL Server)
    - Centralized ID management for AWS Services like Workspaces (Cloud PC solution)

- AD Connector
  - Proxy AD queries to on-prem AD
  - Extend on-prem AD authentication to AWS without syncing users. Avoid AD replication for compliance/security reasons

- Simple AD
  - Lightweight Samba 4 based directory
  - No trust relationship with on-prem AD
  - For small-scale apps that do not need MS AD, Standalone Linux authentication

- SAML 2.0 Identity Federation
  - Use AD to authenticate user
  - Use ADFS (IDP) to issue SAML assertion to app
  - App calls sts:AssumeRoleWithSAML to get STS token
  - App uses the token to access AWS resources

- Web Identity Federation
  - Mobile app calls OIDC Social IDPs to get OIDC JWT token
  - App calls sts:AssumeRoleWithWebIdentity to get STS token
  - App uses the token to access AWS resources
  - AWS Recommends using Cognito instead

- Cognito
  - Similar workflow as Web Identity Federation
  - Cognito User Pool: Directory for managing sign-in and sign-up for mobile apps
    - Provides **Identities**
    - Can use Lambda authorizer for JWT authorization
  - Cognito Identity Pool:  Used to obtain STS tokens for AWS services
    - Identities can come from a Cognito User Pool, or from social IDPs
  - Provides sign-up and sign-in services


- Identity Center
  - Previously AWS Single Sign-On
  - Connects to MS AD (via AD Connector or AWS Managed MS AD) or Azure AD for **centralized permissions mgmt and SSO**
  - Uses SAML 2.0
  - SSO Integrations to many business apps (Jira, Zoom, Box, GitHub, etc)
  - Integrations with AWS Organizations
  - Allows users to sign in to AWS console

