# Imp material for cert
- [AWS Official Cloudwatch Study Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
- [Cloudwatch FAQ](https://aws.amazon.com/cloudwatch/faqs/)

## Cloudwatch notes - SysOps Associate

- Its performance monitoring and logging service
- Cloudwatch features -
  - CloudWatch Dashboards - CloudWatch dashboards built with custom widgets allow you to visually monitor resources and proactively take action if needed. Overall, the dashboards give you a central (and visual) view of how your monitored resources are behaving at specific points in time.
  - Dashboard Widgets
  - CloudWatch Metrics
- can be used across AWS and even on-premises as well
  - SSM agent and cloudwatch agent needs to be installed on on-premises servers to use cloudwatch
- Default Cloudwatch host level EC2 matrics
  - CPU - (CPU Utilization)
  - Network - (Network utilization / throughput)
  - Disk - (disk IO / throughput)
  - Status Check - (health check of Ec2 host and instance)
- Cloudwatch custom matrics 
  - RAM Utilization (how much memory EC2 utilizing)
  - physical disk storage space utilized and available
- Cloudwatch matrics retrieve data and retention period 
  - retrieve data using the **GetMetricStatistics API**
  - retrieve data by using third party tools offered by AWS partners
  - default retention period is indefinitely
  - retention period can be changed for each log group as per need (1 day, 2 weeks, etc)
  - data can be retrieved from any terminated EC2 or ELB instances after its termination.
    - Question:- How long it takes for terminated instance to disappear from AWS account.
- [Matric Granularity](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/publishingMetrics.html)
  - (default monitoring) Standard resolution, with data having a one-minute granularity
  - (detailed monitoring) High resolution, with data at a granularity of one second
- Cloudwatch Alarms
  - create alarm to monitor cloudwatch matric and perform event based actions
  - example, EC2 CPU utilization (auto scaling), ELB latency or bill charges alarms
- [AWS Prescriptive Guidance (APG) on CloudWatch](https://docs.aws.amazon.com/prescriptive-guidance/latest/implementing-logging-monitoring-cloudwatch/welcome.html)
- 
