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
