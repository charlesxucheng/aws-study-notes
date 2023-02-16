# EC2 Pricing Options
* On-demand
* Reserved - 1 or 3 years
* Spot instances
* Dedicated instances => run on hardware dedicated to a single customer
* Dedicated hosts => dedicated physical server; socket/core visibility; host affinity; for server-bound licenses
* Savings Plans - commitment to a consistent amount of usage (EC2+Fargate+Lambda)

Per-sec billing for Amazon Linux and Ubuntu, Windows. Per hour billing for commercial Linux distros. Per-sec billing for EBS volumes.

## RI
* Standard RI - Change AZ, instance size, networking type
* Convertibel RI - also family, OS, tenancy, payment option
  * All upfront, partial upfront, no upfront 

When attributes of a used instance match those of an RI the discount is applied.
* Family, OS, AZ, etc

Scheduled RI
* Minimum 1200 hours per year
* Reseve by recurring schedule

## Spot
* Spot instance
* Spot Fleet
* EC2 Fleet
* Spot Block - uninterrupted for 1 - 6 hours
* 2 minute warning

# EC2 Placement Groups
* Cluster - close together, low-latency, HPC workload
* Partition - spread instances across logical partitions, large distributed workloads like Hadoop, Cassandra, Kafka
* Spread - strictly places a small group of instances across distinct hardware

# Network Interfaces
* ENI - basic adapter, not for high performance requirements
* ENA - Enhanced network performance, for supported instance types
* EFA - For HPC and MPI ML use cases, for all instance types

* Public IP - lost when the instance is stopped. No charge. Cannot be moved between instances
* Pricvate IP - Retained when the instance is stopped
* Elastic IP - Static public IP address. Chargeable. Can move between instances and ENAs

IGW performs NAT between private IP and public IP
