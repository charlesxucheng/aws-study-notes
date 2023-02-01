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
  *  Gather app logs and system logs. Send to S3, Kinesis Data Streams, Data Firehose, Lambda, 
  *  Real-time log processing with subscription filters to Elasticsearch
  *  Share logs across accounts and regions - only via Data Streams
* Events (Event Bridge)

# CloudTrail
* Logs API actions for auditing
* 90 days => create a Trail to S3 for indefinite retention
* CloudWatch events can be triggered based on API calls in CloudTrail
* Events can be streamed to CloudWatch Logs

# X-Ray
Visualize your components, APM tool like AppD

Must integrate the X-Ray SDK with your app and install X-Ray agent

SDK captures metadata for requests made to MySQL and Postgres DBs and DynamoDB, SQS, SNS

# Managed Service for Prometheus
Integrates with EKS, ECS and AWS Distro for OpenTelemetry

# Managed Service for Grafana
Data visualization for monitoring and operational data



