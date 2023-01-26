# Lambda Function Invocations and Concurrency
## Synchronous
* CLI, SDK, API Gateway
* Result returned immediately
* Error handling at client side (retries, exponential backoff, etc.)

## Asynchronous
* S3, SNS, CloudWatch events etc.
* Lambda retries up to 3 times
* Processing must be idempotentent

## Event Source Mapping
* SQS, Kinesis Data Streams, DynamoDB Streams
* Lambda does the polling (polls the source)
* Records are processed in order (except for SQS Standard)

If the concurrency limit is exceeded, throttling occurs with error "Rate exceeded" or 429 "TooManyRequestsException". Throttling messages in CloudWatch Logs but no corresponding data points in the Lambda Throttles metrics means the throttling is happening on API calls in your Lambda function code.

Methods to resolve throttling:
* Configure reserved concurrency
* Use exponential backoff in your application code

# SQS
* Pull model
* Standard - high throughput, best-effort ordering, at-least-once
* FIFO - Max 300 message operations per second, FIFO, exact-once, require Message Group ID and Message Deduplication ID to be added to messages.
* Delay Queue - only makes a message visible to consumers after a period of time
* Long Polling (wait for messages for WaitTimeSeconds 0-20) - cost saving; Short Polling (returns immediately)
* Data deleted after consumed

# SNS
* Push (Pub/sub) model
* Integrates with SQS for fan-out pattern
* Data is not persisted
* No need to provision throughput

# Kinesis
* Pull model
* Routes related records to the same processor
* Multiple apps can access stream concurrently, so that multiple actions, like archiving and processing, can take place concurrently and independently. 
* Ordering at the shard level
* You can choose between an on-demand mode and a provisioned capacity mode. Capacity is in terms of Shards.

# AppFlow
Transfers data from SaaS to Amazon Services. Can do data transformation

# API Gateway
Deployment Types:
* Edge-optimized endpoint
  * For CloudFront, reduced latency for requests from around the world
* Regional endpoint
  * Reduced latency for requests originated in the same region
  * Can also configure your own CDN and protect with WAF
* Private endpoint
  * Securely expose REST APIs only to other services within your VPC or Direct Connect

Throttling:
* 10000  requests per second
* 5000 requests across all APIs within an AWS account
* 429 Too Many Requests error

Different API keys can be used for different usage plans.
