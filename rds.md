RDS Database Engines
* MariaDB
* Microsoft SQL Server
* MySQL
* Oracle
* PostgreSQL

You can only encrypt a database when you create it, not afterwards. DB encryption cannot be disabled once enabled. Replicas in the same region as master uses the same encryption key.

All engines supports AES 256 with minimal performance impact. RDS for Oracle and SQL Server can be encrypted using Transparent Data Encryption (TDE) - may have performance impact.

In order to convert an unencrypted database to encrypted, you need to attach it to an EBS volume, create a snapshot, encrypt the snapshot, and use it to create a new encrypted db instance.

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

