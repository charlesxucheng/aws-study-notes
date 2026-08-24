# CloudWatch
* Metrics
  * Standard monitoring - every 5 mins, free, cannot monitor memory usage and disk usage
  * Detailed monitoring - 1 min, chargeable
  * Need Unified CloudWatch Agent to monitor memory and disk usage metrics
  * Publish custom metrics using CLI or API 
    * Standard resolution - every 1 min. AWS metrics are standard resolution by default
    * High resolution - every 1 sec
* Alarms
  * metric alarm, composite alarm
* Logs
  * Install unified CloudWatch agent to collect logs to servers (EC2, On-prem) to collect app logs
  * Gather app logs and system logs. Send to S3, Kinesis Data Streams, Data Firehose, Lambda
  * E.g. Logs -> Kinesis Firehose -> Lambda -> S3 
  * Real-time log processing with subscription filters to Elasticsearch or lambda
  * Share logs across accounts and regions, e.g. to a centralized security account - only via Data Streams
* Events (Event Bridge)

# CloudTrail
* Logs API actions for auditing
* 90 days => create a Trail to S3 for indefinite retention
* CloudWatch events can be triggered based on API calls in CloudTrail
* Events can be streamed to CloudWatch Logs
* Trail can be created to S3 and enable log file integrity validation

# X-Ray
Visualize your components, APM tool like AppD

Must integrate the X-Ray SDK with your app and install X-Ray agent

SDK captures metadata for requests made to MySQL and Postgres DBs and DynamoDB, SQS, SNS

# Managed Service for Prometheus
Integrates with EKS, ECS and AWS Distro for OpenTelemetry

# Managed Service for Grafana
Data visualization for monitoring and operational data



