# EBS Multi-attach
* Only for Nitro EC2 instances
* Must be a Provisioned IOPS io1 volume
* Must be in a single AZ
* Up to 16 instances

# EFS
* Linux only, NFS
* Other VPCs, regions via VPC peering. Diff accounts no DNS only IP
* On-prem clients via VPN or Direct Connect
* EFS Infrequent Access storage class

# S3
## Lifecycle Management
Can transit from high to low: Standard/Reduced Redundancy => Standard IA => Intelligent Tiering => One Zone IA => Glacier => Glacier Deep Archive

## Replication
Cross-Region and Same-Region. Cross-account. 
Replication requires versioning enabled

## Encryption
* Server-side encryption with S3 managed keys (SSE-S3)
* Server-side encryption with KMS managed keys (SSE-KMS)
* Server-side encryption with client provided keys (SSE-C)
* Client-side encryption. Can use KMS CMK.

## Storage Gateway
Types: File Gateway, Volume Gateway, Tape Gateway
* File Gateway: A virtual gateway appliance runs on Hyper-V, VMWare or EC2 on prem, exposes S3 objects as files to onprem or EC2 based apps. SMB or NFS
* Volume Gateway - iSCSI based block storage
  * Cached volume mode: Entire data set is in S3, cached data on-premise
  * Stored volume mode: Entire data set is on-prem, snapshots are async backed up to S3
* Tape Gateway: Backup server to backup data to S3 - written to S3 Standard and moved to Glacier when tape is rejected.
