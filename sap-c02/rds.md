# RDS Database Engines
* MariaDB
* Microsoft SQL Server
* MySQL
* Oracle
* PostgreSQL

You can only encrypt a database when you create it, not afterwards. DB encryption cannot be disabled once enabled. Replicas in the same region as master uses the same encryption key.
AWS KMS is used to manage encryption keys.
You cannot restore an unencrypted snapshot to an encrypted database instance.

All engines support AES 256 with minimal performance impact. RDS for Oracle and SQL Server can be encrypted using Transparent Data Encryption (TDE) - may have performance impact.

In order to convert an unencrypted database to encrypted, you need to attach it to an EBS volume, create a snapshot, encrypt the snapshot, and use it to create a new encrypted db instance.

## Read Replicas
* Async replication - highly scalable
* No backups configured by default
* Can be within an AZ, cross-AZ or cross-region
* Independent db engine upgrade
* Manually promoted to primary
* All read replicas will have the same encryption status as the master.

## Multi-AZ deployments
* Sync replication - highly durable
* Only primary is active
* Automated backups taken from standby
* Span 2 AZs within a single region
* Auto failover

# Multi-AZ DB instance deployments

* Multi-AZ DB instance deployment
  * has one standby DB instance
  * provides failover support, but doesn't serve read traffic
  * replicates data synchronously

* Multi-AZ DB cluster deployment. 
  * has two standby DB instances
  * provide failover support
  * can also serve read traffic.
  * replicates data using the DB engine's native replication capabilities
  * lower write latency

Amazon RDS provides high availability and failover support for DB instances using Multi-AZ deployments with a single standby DB instance. In a Multi-AZ DB instance deployment, Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability Zone to provide data redundancy and minimize latency spikes during system backups. You can't use a standby replica to serve read traffic. To serve read-only traffic, use a Multi-AZ DB cluster or a read replica instead.

# Aurora
Amazon Aurora is a fully managed relational database engine that's compatible with MySQL and PostgreSQL. Aurora includes a high-performance storage subsystem. An Aurora cluster volume can grow to a maximum size of 128 tebibytes (TiB). 

Each Aurora DB cluster can have up to 15 Aurora Replicas in addition to the primary DB instance. Aurora automatically fails over to an Aurora Replica in case the primary DB instance becomes unavailable. Aurora replicas have to be in the same region with async. Aurora MySQL Read replicas can be cross-region. Both can do read scaling and failover.

## Aurora Global Database
* cross region cluster with read scaling, fast replication, low latency reads. 
* Has primary and second regions
* A db in a secondary region can be promoted to primary in less than 1 minute
* Secondary clusters can do write-forwarding to primary region

Aurora multi-master - same region, multi-write nodes.

Aurora Serverless - on demand, autoscaling, for variable or unpredictable workloads, dev and test envs, etc.
Does not support read replicas or public IPs. Only accessible through VPC or DX, not VPN

# Other databases
* DynamoDB - KV store, Serverless
  * Can have TTL to clean up items automatically to reduce cost.
  * Fully managed. 99.99% availability SLA (99.999% for Global Tables)
  * Supports strongly consistent or eventually consistent reads. Supports ACID.
  * DynamoDB Global Tables - Multi-region multi master, async replication
  * DynamoDB DAX - Fully managed in-memory cache that Offers microsecond performance
  * DynamoDB Streams - changed data capture. -> Kinesis Client Library  
* 
* DocumentDB - MongoDB, serverless fully managed, 99.99%, 6 copies of data in 3 AZs
* Keyspaces - Cassandra, serverless fully managed, 99.99%
* Nepture - GraphDB, serverless fully managed, Gremlin, OpenCypher, SPARQL, 99.99%
* Quantum Ledger Database (QLDB) - Immutable ledger database, append only, serverless

