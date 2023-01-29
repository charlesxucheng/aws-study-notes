# The 7 Rs of Migration

Effort low to high:
* Retire
* Retain
* Relocate
* Rehost
  * AWS Application Migration Service for lift and shift
  * AWS SMS and AWS VM Import/Export
* Repurchase
* Replatform
  * AWS Database Migration Service and Schema Conversion Tool (SCT)
* Refactor
  * Serverless services, event-driven architecture patterns

# Application Discovery Service
* Discovery Connector: Agentless discovery for any OS running in VMware vCenter
* Discovery Agent: VMware, HyperV, Physical. Certain Linux, Windows

# Server Migration Service
Migrates vSphere, Hyper-V, SCVMM, and Azure virtual machines to EC2. Performs automated, incremental and scheduled migrations to AMIs and then EC2s.

# DataSync
Scheduled, automated data transfer from on-prem NFS or SMB servers to S3, FSx or EFS. Data in transit is TLS encrypted.

# Snowball Family
* Snowball, Snowmobile - data migration
* Snowball Edge Compute Optimized - optional GPU, for ML
* Snowball Edge Storage Optimized - S3 compatible object storage and block storage
* Snowcone  - Small divice used for edge computing, storage and data transfer

256-bit encryption with KMS, tamper resistent enclosures with TPM. Snowball client. 80TB, 50TB, 100TB (Petabyte scale). Snowmobile up to 100PB (exabyte scale)

Use multiple instances of Snowball client in parallel for best performance

Use cases:
* Cloud data migration
* Content distribution - send data to clients or customers
* Tactical Edge computing - collect data and compute
* Machine learning - run ML directly on the device
* Manufacturing - data collection and analysis in the factory
* Remote locations with simple data - pre-processing, tagging, compression, etc.
