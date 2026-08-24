# System Manager
Manages S3, EC2, RDS, etc.
Need to install agent and have the right role

Components:
* Automation
  * Using YAML or Json Documents to specify automation to perform
* Run Command
* Inventory
* Compliance - can scan managed instances for patch compliance and configuration inconsistencies
* Patch Manager - apply patches and scan managed instances for patch compliance and configuration inconsistencies
* Session Manager - secure remote management of instances at scale without logging into your servers. 
  * No bastion host, ssh, RDP, PowerShell
  * All actions recorded by CloudTrail
  * Can store session logs in S3 and CloudWatch
* Parameter Store - secure hierarchical storage for configuration data and secrets management
  * No key rotation - key difference

# OpsWorks
Managed instances of Chef and Puppet

# Resource Access Manager
Share resources with accounts or organizations. RAM can be used to share:
* Transit Gateways
* Subnets
* License Manager configurations
* Route 53 Resolver rules

Use case: Share subnet from Management account to Production account. Participants cannot view or modify resources of other participants' resource.

# Personal Health Dashboard
* Provides alerts and remediation guidance whhen AWS is experiencing issues that may impact you
* Personalized view into the performance and availability of your AWS resources

# Service Dashboard
* General service status

# Elastic Disaster Recovery
* Recover from: On-premises to cloud, cloud to AWS, AWS region to region
* Recover of: Compute (to EC2), Disk storage (to EBS)

# Well-Architected Tool
* Review the state of your apps and workloads against architectural best practices
* Identify opportunities for improvement and track progress
* Customization of best practices pillars
* Integration with Organizations and Trusted Advisors
* WA Lenses extends guidance to specific industry and tech domains: Serverless Lens, SaaS Lens, FTR Lens (for Independent Software Vendors) in AWS Partner Network
