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

### Cloudwatch terminologies
- cloudwatch support many services in AWS hence it needs a way to keep things seperate
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
  - Dimension --> 
    - used to distinquesh between these different resources who send this datapoints at the same time
    - example, if Namespace = AWS/EC2
    - Dimensions could be in key-value format
      - Name=InstanceID, value = i-xxxxxx
      - Name=InstanceType, value = t3.small
    
