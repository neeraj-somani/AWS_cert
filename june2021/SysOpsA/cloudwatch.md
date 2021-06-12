# Imp material for cert
- [AWS Official Cloudwatch Study Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
- [Cloudwatch FAQ](https://aws.amazon.com/cloudwatch/faqs/)

## Cloudwatch notes - SysOps Associate

- Its performance monitoring and logging service used across AWS and even on-premises as well
- Default Cloudwatch host level EC2 matrics
  - CPU
  - Network
  - Disk
  - Status Check
- Cloudwatch custom matrics 
  - RAM Utilization
- Cloudwatch matrics retrieve data and retention period 
  - retrieve data using the *GetMetricStatistics API*
  - retrieve data by using third party tools offered by AWS partners
  - default retention period is indefinitely
  - retention period can be changed for each log group as per need
- [High-resolution metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/publishingMetrics.html)
  - (default monitoring) Standard resolution, with data having a one-minute granularity
  - (detailed monitoring) High resolution, with data at a granularity of one second
- [AWS Prescriptive Guidance (APG) on CloudWatch](https://docs.aws.amazon.com/prescriptive-guidance/latest/implementing-logging-monitoring-cloudwatch/welcome.html)
- 
