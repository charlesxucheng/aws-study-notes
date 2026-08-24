# Athena and Glue
Athena queries data in S3 using SQL. Can connect to other data sources with Lambda. CSV, TSV, JSON, Parquet, ORC formats. Uses AWS Glue for data catalogue / schema.

Glue - fully managed ETL. Works with data lakes (e.g. S3), data warehouses (e.g. Redshift) and RDS. Data discovery with Crawlers.

# EMR
Managed Hadoop and Spark

# Kinesis
* Data Streams - ingests data into streams. Real time (~ 200ms). Up to 7 days.
  * Each shard is processed by exactly one KCL (Kinesis Client Library) worker and has exactly one corresponding record processor. One worker can process multiple shards.
  * Order is maintained for records within a shard
  * Can process data in batch to improve performance throughput
* Data Firehose - loads data straight to destinations. Near real time (~60 sec)
  * No shards, elastic scalability
  * Can be transformed by lamda
* Data Analytics - uses Apache Flink for processing data streams
  * Real-time SQL processing for streaming data from Data Streams or Firehose
  * Destination Data Streams, Firehose, or Lambda

# Other Services
* Timestream - Time series db service, faster and cheaper than RDBMS. Recent data in memory and historical data in cost optimized storage tier. Serveless, autoscale
* Data Exchange - data marketplace. Native integration of data into AWS
* Data Pipeline - managed ETL service between AWS services. Data source can be on-premise
* Lake Formation
  * Set up secure data lakes in days. Data saved to S3
  * Data warehouse vs Data lake
* MSK Managed Streaming for Apache Kafka
  * VPC network isolation
  * Encryption at rest and in transit 




