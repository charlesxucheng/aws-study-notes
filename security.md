# KMS
* Manages symmetric and assymetric keys. CMK = Customer Makster Keys. HSM = Hardware Security Module
* CMKs are the primary resources in KMS. Contains key material used to encrypt and decrypt data.
* Symmetric CMKs and private keys of assymetric CMKs never leaves KMS unencrypted.
* Can import own key material
* A CMK can encrypt data up to 4KB in size
* CMK can generate, encrypt and decrypt Data Encryption Keys
* You cannot manage AWS Managed CMKs, rotate them or change their key policy
* Multi-tenant
* FIPS 140-2 Level 2 / Level 3 in some areas
* Can use CloudHSM cluster as a custom key store instead of the default KMS store

# CloudHSM
* Generate your own encryption keys on AWS. Comparison with KMS.
* Single-tenant
* Customer managed durability and availability 
Customer managed root of trust
* FIPS 140-2 Level 3
* Broad 3rd party support

# Macie
Fully managed data security and data privacy service. Use ML and pattern matching to discover, monitor and protect sensitive data in S3.
* Personal identification info
* Protected Health Info
* Regulatory docs
* secrets
* Identify changes to policy and ACLs
* Monitor security posture of S3
* Generic security findings. Integrates with Security Hub and EventBridge

# AWS Config
Evaluates the configuration against desired configurations of various services. Captures config changes and sends notifications with SNS and alerts via CW Events
* S3 bucket has server side encryption enabled.
* SSH restricted in security groups
* RDS instance is publicly accessible

# AWS Inspector
* Checks security exposures and vulns in EC2s via agent. CIS benchmarks.
* Checks Network configuration for ports reachable from outside of the VPC, processes reachable on port.
