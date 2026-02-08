# EBS Multi-attach
* Only for Nitro EC2 instances
* Must be a Provisioned IOPS io1 volume
* Must be in a single AZ
* Up to 16 instances

# EBS Volume Types
* General Purpose: gp2/gp3
  * 1GiB to 16TiB
  * 16000 Max IOPS
  * Low latency interactive apps, dev and test environments

* Provisioned IOPS SSD
  * io1/io2
    * 4 GiB to 16 TiB
    * 64000
    * sustained high IOPS workload, I/O intensive database
  * io2 block express 
    * 4 GiB to 64 TiB
    * 256000
    * sub-millisecond latency, sustained high IOPS workload
    
* Throughput Optimized HDD: st1
  * 125 GiB to 16 TiB
  * 500 Max IOPS
  * Big data, data warehouse, log processing

* Cold HDD: sc1
  * 125 GiB to 16 TiB
  * 250 Max IOPS
  * For data infrequently accessed

## EBS Copying & Sharing
* An EBS volume can be copied to a snapshot in the same region
* A snapshot => another snapshot in another region, or change encryption.
* A snapshot => an encrypted volume in a different AZ
* An unencrypted snapshot => unencrypted AMI, shared with other accounts or publicly
* An encrypted snapshot => encrypted AMI, shared with other another account but not publicly

## Instance Store Volumes
* High performance local disks of the host computer on which EC2 runs
* Ephemeral
* Ideal for temporary, frequently changing data
* Cannot be detached/reattached

# EFS
* Linux only, NFS protocol
* Other VPCs, regions via VPC peering. Diff accounts no DNS only IP
* On-prem clients via VPN or Direct Connect
* EFS Infrequent Access storage class

# S3

* Key-value object store
* Max 5TB per object
* Unlimited storage
* Bucket names globally unique
* Folder is part of the key
* Exposes to a VPC via S3 Gateway Endpoint 

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
