# CloudWatch
- CloudWatch is a core supporting service within AWS which provides metric, log and event management services.
- It's used through other AWS services for health and performance monitoring, log management and nerveless architectures.
- Collects and manages operational data
- Metrics - AWS products, Apps, on-premises
  - cloudwatch agent needs to be installed if we want metrics details from on-premises or from external to AWS services.
- Logs --> AWS products, Apps, on-premises
- Events --> based on AWS services actions and on specific schedules
- Alarms --  
  - alarms are created and linked to a specific metric
  - take actions based on some event happened based on metric configuration
  - it can be triggered based on a value of metric vs threshold ... over time
  - **exam imp** resolution of metric directly affect the configuration of alarms

### Cloudwatch terminologies
- cloudwatch support many services in AWS hence it needs a way to keep things seperate
- Every metric has metricName and Namespace
- imp cloudwatch terminologies
  - Namespace --> 
    - its a container for monitoring data
    - Although, AWS has defined a specific format for AWS services and all data related to that service will be in the folder/container in this format "AWS/service_name"
    - example, in-case of EC2, it will be "AWS/EC2"
    - each namespace contains related metric
  - Metric -->
    - collection of related data points in a time ordered structure
  - Datapoint --> 
    - consist of two things, timestamp and value at that specific timestamp
    - (optional) unit of measure
  - Dimension --> 
    - used to distinquesh between these different resources who send this datapoints at the same time
    - example, if Namespace = AWS/EC2
    - Dimensions could be in key-value format (name/value pair)
      - Name=InstanceID, value = i-xxxxxx
      - Name=InstanceType, value = t3.small
- Every metric also has Resolution
  - by default every metric produced by AWS has standard resolution (60 sec granularity)
  - the highest resolution at present is 1 second
  - this defines a metric data point for a specific service that you are collecting data for at a specific time duration/granularity.
  - every resolution has data retention period
    - between 1 sec to 59 sec retained for 3 hours
    - 60s (1 min) data retained for 15 days
    - 300s (5 min) dta retained for 63 days
    - 3600s (1 hour) data retained for 455 days
    - As data ages, its aggregated and stored for longer with less resolution.
  - some Statistics also can be used to store data .. aggregation over a period (eg: min, max, sum, average)
  - percentile -- states relative standing of a value in a dataset, and it helps in removing outliers. eg: p95, p97.5 
- Certain AWS metrics allow aggregation across dimensions, for example CPUUtilization by instance type. but doesn't include ALL EC2 type and Not allowed in Cutom metrics

### CloudWatch Architecture
- provide services to Ingestion, storage and management of metrics
- Public service -- public space AWS endpoints. Meaning, it can be accessible from AWS and on-premises environments.
- With-in AWS if any service needs integration with Cloudwatch, needs access to this public space endpoint. Usually done via IGW or via an interface endpoint within a VPC.
- For this AWS Service Integration - via management plane. This gives access to public available metric details.
- For anything that is private for AWS service, requires cloudwatch Agent install/integration to get richer metric details. Example, in case of EC2 instance
- CloudWatch can also be used as Cloudwatch as a service for On-premises integrations via Agent/API (custom metrics)

### Cloudwatch Logs
- CloudWatch Logs is a service which can accept logging data, store it and monitor it.
- CloudWatch Logs is a public service and can also be utilised in an on-premises environment and even from other public cloud platforms. store, monitor, access logging data.
- This easily integrate with AWS services like - EC2, VPC Flow Logs, Lambda, CloudTrail, R53, and more
- Can generate metrics based on logs - can perform metric filter actions
- Its a regional service
- Few terminologies 
  - Log events - contains timestamp and raw message
  - Log Streams - log events are stored in it, Log stream is a sequence of log events from the same source
  - Log Groups - contains multiple log streams from the same source for the same type of logging but at different intervals.
    - Under log groups, configuration settings can also be defined. like, retention period, permissions, metric filters
- Cloudwatch logs divided into 2 parts
  - ingestion side
    - This means getting the logs into the system
  - subscription side
    - what other products can use those logs for other activities
- There are multiple ways by which you can export this data from cloudwatch log groups
  - one way is S3 export - Create-export-task, it can take upto 12 hours to extract data and its not Realtime.
    - Remember, you can't encrypt this data with SSE-KMS, you can only encrypt it with SSE-S3
  - For real-time delivery of cloudwatch log data, subscription model is used
    - other services who wants to consume cloudwatch log data can subscribe to it and receive data in a real-time fashion
    - This real-time data can be subscribed per log-group basis

### exam review
- For any log management scenarios default to cloudwatch logs.
- On-premises and AWS
- Export to S3.. createExportTask - 12 hours
- Near realtime or persist logs -- Kinesis Firehose
- Firehose for any 'firehose destinations'
- Realtime - Lambda or Kinesis Data Stream (KCL consumers)
- Elasticsearch - AWS Managed lambda
- Metric filters -- scan log data, generate a cloudwatch metric.

### Quiz question --
- question -- Which two products can be used together for real time processing of CloudWatch Logs
- answer -- Subscription + lambda


