# Imp material for cert
- [AWS Official Cloudwatch Study Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
- [Cloudwatch FAQ](https://aws.amazon.com/cloudwatch/faqs/)

## Cloudwatch notes - SysOps Associate

- Its performance monitoring and logging service
- Cloudwatch features -
  - CloudWatch Dashboards 
    - CloudWatch dashboards built with custom widgets allow you to visually monitor resources and proactively take action if needed. Overall, the dashboards give you a central (and visual) view of how your monitored resources are behaving at specific points in time.
    - single dashboard can be build with matrics from multiple region
  - Dashboard Widgets
    - widgets can cvreated based on Matrics or logs
  - CloudWatch Metrics
    - in case of EC2 -- By auto sclaing group, by image, per-instance matrics, aggregated_by_instance_type, across_all_instances
    - in case of ALB -- {per APPELB, per AZ, per TG matrics}, {per AppELB, per AZ matrics}, {TargetGroup},
    - in case of EBS volume - VolumeReadOps, VolumeWriteOps, volumeQueueLength, VolumeStatusCheck
- can be used across AWS and even on-premises as well
  - SSM agent and cloudwatch agent needs to be installed on on-premises servers to use cloudwatch
- Default Cloudwatch host level EC2 matrics
  - CPU - (CPU Utilization)
  - Network - (Network utilization / throughput), networkIn, networkOut, 
  - Disk usage - (disk IO / throughput)
  - Status Check - (health check of Ec2 host and instance)
- Default cloudwatch per ALB matrics
  - RequestCount, consumedLCUs, TargetResponseTime, ActiveConnectionCount, ProcessedBytes, etc
- Default cloudwatch per ELB matrics  
  - VolumeReadOps, VolumeWriteOps, volumeQueueLength, VolumeStatusCheck
  - the higher the queue length, the more you max out your IOPS
  - VolumeStatusCheck is an imp matrics, "ok", "warning", "imparied", "insufficient-data"
- Cloudwatch custom matrics 
  - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/mon-scripts.html
  - RAM Utilization (how much memory EC2 utilizing)
  - physical disk storage space utilized and available
  - CRON
    - its a scheduled tasks command based utility, that you can use to run a command at any specific interval of time
    - Its available at "/etc/crontab"
    - Use the commands below for the lab.
      - /home/ec2-user/aws-scripts-mon/mon-put-instance-data.pl --mem-util --verify --verbose
      - /home/ec2-user/aws-scripts-mon/mon-put-instance-data.pl --mem-util --mem-used --mem-avail
      - */1 * * * * root /home/ec2-user/aws-scripts-mon/mon-put-instance-data.pl --mem-util --mem-used --mem-avail
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




# Cloudwatch for EBS volume
# EBS - Monitoring and Modifying EBS volume

## EBS 
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html
- Its a virtual disk that is attached to EC2
- Types - (read deatils of it from ACG lecture pdf file) 
  - ### SSD
    - General Purpose (SSD) - gp2, gp3
    - Provisioned IOPS (SSD) - io1, io2, io2 block express
  - ### HDD
    - Below 3 are type of HDD
    - can not be a boot volume, meaning you can not install OS on these volume and boot your machine
    - Throughput Optimised Hard Disk Drive - st1
      - if storage cost is imp and access data frequently
    - Cold Hard Disk Drive - sc1
      - if storage cost is imp but not accessing data frequently
    - Magnetic
  - EBS volume size can be modified on the fly, change its volume type, or (for an io1 volume) adjust its IOPS performance, all without detaching it.
  - These changes can be done on detached volume as well.
    - Issue the modification command (console or command line)
    - monitor the progress of the modification
    - 
## I/O Credits and burst performance
- The performance of gp2 volumes is tied to volume size, which determines the baseline performance level of the volume and how quickly it accumulates I/O credits;
- larger volumes have higher baseline performance levels and accumulate I/O credits faster.
- I/O credits represent the available bandwidth that your gp2 volume can use to burst large amounts of I/O when more than the baseline performance is needed.
- The more credits your volume has for I/O, the more time it can burst beyond its baseline performance level and the better it performs when more performance is needed. 
- This initial credit balance is designed to provide a fast initial boot cycle for boot volumes and to provide a good bootstrapping experience for other applications.
- Volumes earn I/O credits at the baseline performance rate of 3 IOPS per GiB of volume size. 
- When your volume requires more than the baseline performance I/O level, it simply uses I/O credits in the credit
balance to burst to the required performance level, up to a maximum of 3,000 IOPS for at least 30 minutes.
- When the baseline performance of a volume is higher than maximum burst performance, I/O credits are never spent.
- If the volume is attached to an instance built on the **####Nitro System**, the burst balance is not reported. For other instances, the reported burst balance is 100%.
- The larger a volume is, the greater the baseline performance is and the faster it replenishes (restores) the credit balance.
- 
- What happens if I empty my I/O credit balance?
  - the maximum IOPS performance of the volume remains at the baseline IOPS performance level
  - if need better performance, you should consider switching to a gp3 volume.


## Exam question scenario --
- In which scenario, which EBS volume if most suitable
- Exam Tip:
  - Know that Degraded or Severely Degraded = Warning
  - Stalled or Not Available = Impaired

## Pre-Warming EBS Volumes
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-initialize.html
- http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-volume-status.html
- (ACG PDF) New EBS volumes receive their maximum performance the moment that
 they are available and do not require initialization (formerly
 known as pre-warming). 
 - However, storage blocks on volumes that
 were restored from snapshots must be initialized (pulled down
 from Amazon S3 and written to the volume) before you can access
 the block. This preliminary action takes time and can cause a
 significant increase in the latency of an I/O operation the first
 time each block is accessed. For most applications, amortizing
 this cost over the lifetime of the volume is acceptable.
 Performance is restored after the data is accessed once.
 - you can avoid this performance hit by reading all blocks of volume before use it in application, called initialization.
