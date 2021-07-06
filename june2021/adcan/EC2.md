# Elastic Compute Cloud or EC2

- EC2 is AWS's implement of IAAS - Infrastructure as a service.
- It allows you to provision virtual machines known as instances with resources you select and an operating system of your choosing.

### EC2 Key facts & Features
- IAAS - provides Virtual Machines => Instances
- an instance is just an operating system, configured in a certain way with a certain set of allocated resources.
- Private service by default -- uses VPC networking
- if you want to allow public access to this private EC2 instance then VPC should also support that part
- AZ resilient - instance fails if AZ fails
- different instance sizes and capabilities
- (by default) On-demand billing - per second
- EC2 can use various storage mechanism, most commonly 2, local on-host storage or EBS

### Instance lifecycle
- Instance state - The state of instance indicates its current condition. example, power-on or power-off.
- few states --> Running, Stopped, Terminated
- once a instance is terminated, this action can no longer be reverted.
- **exam imp** -- stopped instance still incur charges for EBS.

### Amazon Machine Image (AMI) 
- it can be created from an EC2 instance and 
- It can also get created based on an instance
- An AMI is very similar to server image used to create VM
- or USB device, which is used to install OS
- An AMI contains attached permissions, which defines who can access and who can't
- An AMI can be public or owner (implicit allow) or explicit (speific AWS accounts allowed)
- An AMI contains boot volume of the instance, ROOT Volume, its the drive that boots the OS
- An AMI can also have other volumes but atleast one boot volume
- It also provides, Block Device Mapping - its a configuration which links the volumes that are attached to AMIs and connected to OS.

### EC2 status Checks
- 2 types - System status check and Instance status check
- system status check -- make sure the traffic can reach the hardware that instance is running on. This check does not validate that your OS and applications are accepting traffic. This check verifies that your instance is reachable.
- Instance status check -- It verifies that instance OS is accepting traffic. in-case of issue, reboot should or OS configuration check can resolve the issue.

### Security Groups 
- can be considered as Mini firewall
- SG attached to Network Interfaces of anything that goes inside VPC.
- on SG can be attached to one or more instances

### Virtualization 101
- a few different historical methods of performing virtualization
  - Emulated Virtualization
  - Paravirtualization
  - Hardware Assisted Virtualization
  - SR-IOV (Single Root - IO Virtualization)
- More details on this link: http://www.brendangregg.com/blog/2017-11-29/aws-ec2-virtualization-2017.html
- EC2 provides virtualization as a service, IAAS product
- Virtualization - its a process of running more than one OS on a piece of physical hardware, a server


### EC2 Architecture and Resilience
- EC2 instances are virtual machines (OS + Resources - memory, instance storage, CPU, etc)
- EC2 instances run on EC2 hosts
  - EC2 hosts are physical servers (hardwares) which AWS manages
- Shared hosts or Dedicated hosts
- Shared hosts (by default)
  - shared across different AWS customers
  - no ownership of hardware and pay for individual instances as per usage
  - every customer/user who is on shared host has complete isolation from each other. There is no visibility of it being shared.
- Dedicated Hosts 
  - you pay for the entire host
  - no seperate payment required for running any instances on it
  - and its not shared with other customers
- EC2 is a AZ resilient service
- Hosts = 1 AZ - AZ fails, host fails, instances fails
- EC2 hosts also has Instance store (local storage) attached to it. This is temporary storage memory. if instance moved from one host to another, you loose this temporary storage memory.
- EC2 hosts also has two types of networking
  - Storage Networking
    - this is used to connect to EBS (remote storage, also known as Persistent storage) 
  - Data Networking - this connects EC2 host and EC2 instance using primary elastic network interface, which is inside specific subnet. 
    - Instances can have multiple network interfaces, even in different subnets, as long as they are in same AZ.
    - meaning, one network interface can connect to many subnet in same AZ. 
- If you restart the instance, it will stay on the same Host. 
- If you stop an instance and start again then instance will move to a new host most probably.
- Most probably and ideally, instances of same type and size share the same host. But they can even mix-match as well.

### Whats EC2 good for?
- When you have traditional OS + Application compute need
- long-running compute
- if application is server style
- either burst or steady-state load needed
- if application need monolithic application stacks
- migrated application workloads or Disaster Recovery need

### EC2 Instance Types (family, generation, features & size)
- Helpful link 
  - https://aws.amazon.com/ec2/instance-types/
  - https://ec2instances.info/
- The most important purpose of choosing the correct type of EC2 instances gives leverage on
  - Raw CPU, Memory, Local Storage Capacity & Type
- Resource ratios (balance is imp)
- Storage and Data Network Bandwidth
- System Architecture / Vendor (ARM vs x86 , intel based vs AMD based CPU)
- Any additional features and capabilties

### EC2 categories
- General purpose ( A , M, T) - Default - Diverse (steady state) workloads, fairly even resource ratio, meaning balance between CPU, memory, storage.
- Compute Optimized (C) - Meadia processing, High Performance Computing, Scientific Modelling, gaming, Machine Learning
  - provide latest high performance CPUs, more CPU is offered then memory
- Memory Optimized (R, X, z) - Processing large in-memory datasets, some database workloads
  - large memory allocation for a given dollar or CPU amount
  - used for large in-memory caching or database related workloads
- Accelerated Computing (P, G, F, Inf) - Hardware GPU, field (custom) programmable (hardware) gate arrays (FPGAs)
  - dedicated GPUs, high scale parallel processing and modeling
- Storage Optimized (I, D, H) - Sequential and Random IO - scale-out transactional databases, data warehousing, elasticsearch, analytics workloads
  - provides large amount super fast local storage
  - designed for high sequential transfer rates, 
  - or to provide massive amounts of IO operations per second

- Read and try to memorize the EC2 types from github doc: https://github.com/acantril/aws-sa-associate-saac02/blob/master/08-EC2-Basics/00_LearningAids/InstanceTypes.png


### Decoding EC2 types
- example, R5dn.8xlarge
- consist of Instance family
- generation (version)
- instance size (determines memory and CPU of instance)
- some instance types have few letters that denotes additional capability that instance provides
  - d - NVMe storage
  - a - signifies AMD CPUs
  - n - network optimized
  - e - extra capacity (could be RAM or storage)

### EC2 SSH vs EC2 Instance Connect
- Amazon EC2 Instance Connect provides a simple and secure way to connect to your Linux instances using Secure Shell (SSH). 
- With EC2 Instance Connect, you use AWS Identity and Access Management (IAM) policies and principals to control SSH access to your instances, removing the need to share and manage SSH keys.
- aws IP range URL - https://ip-ranges.amazonaws.com/ip-ranges.json

### Storage Refresher
- Direct (local) attached storage - storage directly connected on the EC2 host
  - this is a physical disk directly connected to a device
  - also known as Instance store
  - It comes with some risk, if hardware fails, storage can be lost, 
  - if EC2 instance moves between hosts, storage can be lost
  - Ephemeral storage - temporary storage
- Network attached Storage - Volumes delivered over the network (EBS)
  - highly resilient and seperate from instance hardware
  - Persistent storage


- Block storage
  - volume presented to OS as a collection of block.. no structure provided. Mountable, bootable.
  - example, SSD or HDD
- File storage
  - file server, presented as a file share, ... has a pre-build structure. Mountable, but not bootable.
  - example HDFS, 
- Object Storage
  - collection of objects... its a flat storage, has no structure,... Not mountable. Not bootable.
  - it usually has object and metadata
  - example, S3
- IO (Block) Size (storage performance)
  - how to store data, it can be 16kb, 64kb, or 1 mb, or even larger
- IOPS (storage performance)
  - how many read/writes a storage system can accomodate in a second.
- Throughput (storage performance)
  - IO size * iops = throughput
  - rate of data a storage system can store on a particular piece of storage, either physical disk or volume.
  - generally, measured in XX MB/sec

### Elastic Block Store (EBS)
- Amazon Elastic Block Store (Amazon EBS) provides block level storage volumes for use with EC2 instances. 
- EBS volumes behave like raw, unformatted block devices.
- You can mount these volumes as devices on your instances.
- EBS volumes that are attached to an instance are exposed as storage volumes that persist independently from the life of the instance.
- You can create a file system on top of these volumes, or use them in any way you would use a block device (such as a hard drive).
- block storage -- raw disk allocations (volume) -- can be encrypted using KMS
- **exam imp** storage is provisioned in one AZ (resilient in that AZ)
- attached to one or more EC2 instances (or other services) over a storage network.
- This can also be used for clusters, but cluster application should be able to manage it, to avoid issues
- snapshot (backup) into S3. Create volume from snapshot (migrate between AZs)
- different physical storage types, different sizes, different performance profiles
- billed based on GB-month (and in some cases performance)
- EBS replicates within an AZ. Failure of an AZ means failure of a volume. for back and HA, needs to be planned better.
- hence, a solution to above problem is to create a snapshot of volume and store it in S3.
- snapshots can be copied across region provide global resilience

### EBS Volume types 
### General Purpose SSD 
  — Provides a balance of price and performance. We recommend these volumes for most workloads.
  - GP2 and GP3
  - volumes can be between 1 GB to 16 TB
  - GP2 is default
  - How many instances can a GP2 volume be attached to at the same time?? (answer - 1)
  - IOP, volume is created with IO credit allocation, 
    - one IO means, one Input Output operation
    - An IO credit is a 16KB chunk of data.
    - So, an IOP is one chunk of 16 KB in one second.
    - example, if we transferring 160 KB of data, that represents 10 IO blocks of data, so 10 blocks of 16 KB.
    - if device do that in one second, then thats 10 credits in one second, so 10 IOPs.
    - If you don't have any credit on this IO bucket, then you can't perform any IO operations on the disc.
    - The IO bucket has a capacity of 5.4 million IO credits, fills at rate of baseline performance.
    - every volume has a baseline performance based on its size with a minimum, 
    - so streaming in a bucket, refills rate with 100 IO credits per second regardless of volume size
    - Actual credit is depends on volume size
    - for GP2, beyond the 100 minimum the bucket fills with 3 IO credits per second, per GB of volume size (Baseline performance)
    - by default, GP2 can burst up to 3000 IOPs by depleting the bucket credits.
    - but in reality, All volumes get an initial 5.4 million IO credits by default. Bucket start with full credits. This allows 30 minutes @ 3000 IOPS. and even bucket is continously filling up with new credits as well, which means ideally you could burst for more than 30 min.
    - Great for boots and initial heavy workloads.
    - but this credit system is only used for volumes less or equal to 1 TB.
    - For any volume larger than 1 TB or 1000 GB, baseline is above burst. Credit system isn't used & you always achieve baseline. Baseline performance is up to max of 16,000 IO credits per second incase of GP2.
   - GP3 is newer relatively
    - GP3 removes the credit bucket architecture with something much simpler.
    - Every GP3 volume, regardless of size, starts with 3000 IOPs & data trasfer rate of 125 MB/s
    - GP3 is cheaper (~20%) vs GP2
    - extra cost for up to 16,000 IOPs or 1000 MB/s
    - overall 4x faster max throughput 1000 MB/s vs GP2 250 MB/s
  - These volume is mostly useful for virtual desktops, medium sized single instance databases such as MSSQL server and Oracle DB, low-latency interactive apps, dev & test, boot volumes

### EBS - Provisioned IOPS (IO1,IO2, blockExpress) (9:05)
- Provisioned IOPS SSD — Provides high performance for mission-critical, low-latency, or high-throughput workloads.
- choose this, If you need to be able to specify performance requirements (IOPS) independent of volume size
- with this EBS type IOPS can be adjusted independently of size.
- also, its designed to give performance with consistent low latency & even in the situation of jitter or uneasiness.
- EBS volume size --> 4 GB to 16 TB with IO1 and IO2
- but with BlockExpress - 4 GB to 64 TB
- Throughput
  - upto 4000 MB/s with BlockExpress
  - upto 256,000 IOPS per volume with BlockExpress
  - upto 1000 MB/s with IO1/IO2
  - upto 64,000 IOPS per volume with IO1/IO2 (4x GP2/GP3)
- there is some restrictions to understand
  - io1 50 IOPS/GB (max)
  - io2 500 IOPS/GB (max)
  - BlockExpress 1000 IOPS/GB (max)
  - there is also restrictions on per instance performance, which is influenced by below 3 choices
    - types of volumes
    - size of instance
    - type of the instance
  - In-order to deal with this above situation, you need to attach multiple EBS volumes and adjust EC2 instance type/size accordingly
- These volume is mostly useful for High performance, very low-level latency sensitive workloads. I/O-intensive NoSQL & relational DBs.
- one common usecase, when you have smaller volume but need super high performance

### EBS Volume Types - HDD-Based
- HDD means, moving bits, platters which spin little robot arms known as heads, which move across those spinning platters.
- Moving parts means slower, thats why use it cautiously
- Throughput Optimized HDD (st1) 
  — A low-cost HDD designed for frequently accessed, throughput-intensive workloads.
  - cheap
  - 125 GB to 16 TB
  - max 500 IOPS, but here block size is considered as 1 MB,
  - so Max 500 MB/s IOPS throughput
  - baseline throughput performance - 40MB/s/TB
  - and can burst upto 250MB/s/TB
  - This is designed when cost is concern but need frequent access throughput-intensive sequential process
  - These volume is mostly useful for Big-data, data warehouses, log processing
- Cold HDD (sc1) 
  — The lowest-cost HDD design for less frequently accessed workloads.
  - even cheaper
  - 125 GB to 16 TB
  - max 250 IOPS, but here block size is considered as 1 MB,
  - so Max 250 MB/s IOPS throughput
  - baseline throughput performance - 12MB/s/TB
  - and can burst upto 80MB/s/TB
  - This is designed when you want to store lots of data and doesn't care much about performance, means designed for less frequently accessed workloads
  - colder data or archieve requiring fewer scans per day


### Instance Store Volumes
- An instance store provides temporary block-level storage for your instance.
- This storage is located on disks that are physically attached to the host computer.
- Instance store is ideal for temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.
- An instance store consists of one or more instance store volumes exposed as block devices.
- The size of an instance store as well as the number of devices available varies by instance type.
- The virtual devices for instance store volumes are ephemeral[0-23].
- Instance types that support one instance store volume have ephemeral0. Instance types that support two instance store volumes have ephemeral0 and ephemeral1, and so on.
- Highest data performance on AWS
- Included in instance price
- **exam imp** -- this needs to be attached at launch time, you can't attach instance store to a EC2 instance after launch. not like EBS.
- one instance can have one or more
- If an instance moves from one host to another, data has been lost on instance store volume, because its ephemeral.
- more IOPS and throughput vs EBS

### Choosing Between the EC2 Instance Store and EBS
- cheap == ST1 or SC1
- if throughput ... streaming ... ST1
- Bootable then no to ST1 or SC1
- GP2/3 - up to 16,000 IOPS
- IO1/2 - up to 64,000 IOPS (blockExpress - 256,000 IOPS)
- RAID0 + EBS - up to 260,000 IOPS (io1/2-BE/GP2/3)
  - here RAID0 set is a set of lots of EBS volumes
- what if you need more than 260,000 IOPS
  - then use instance store volumes and EBS and EC2 combinations

### Snapshots, Restore & Fast Snapshot Restore (FSR)
- EBS Snapshots are backups of data consumed within EBS Volumes - Stored on S3.
- Snapshots are incremental, the first being a full backup - and any future snapshots being incremental.
- Snapshots can be used to migrate data to different availability zones in a region, or to different regions of AWS.
- snapshots are incremental volume copies to S3.
- **exam imp** -- snapshot is a full copy of 'data' on the volume. Snashots just copies the data used.
- EBS snapshots are smart enough, so if you do delete an incremental snapshot, it make sure the data is moved so that all the snapshots after that point still function.
- each snapshot even though its incremental, can be thought of as self-sufficient.
- snapshots are great way to create volumes if needed.
- some performance related facts
  - NEW EBS volume = full performance immediately
  - if volume restore from snapshot, it happen lazily, means fetched gradually. So performance gets impacted if some request come for data which is not yet restore from snapshot. Although requested block are fetched immidiately from snapshot upon request but still some performance impact can be observed.
  - To avoid this issue, many application perform a force read on all data block immidiately after snapshot restore. This will fetch data fast and minimize the user performance impact.
- FSR (Fast Snapshot restore) - is designed to resolve above problem and it can immidiately restore volume from snapshot.
- up to 50 snaps per region ... set on snap & AZ.
- FSR cost extra compare to read block on snap restore.
- Snaps are billed at GB/month


### EBS Encryption
- When EBS encryption is disabled, there is no encryption performed at EBS level. But there is possibility of encryption can be done at OS level of EC2 instance, if needed.
- AWS Accounts now can be set-up to perform encryption on EBS volume by default using either default AWS-CMK (KMS) or using anyother CMK preferred by customer.
- CMK is not directly used to encrypt volume data, instead, a unique Data Encryption key gets generated by CMK per volume to encrypt the data. This DEK is always associated with that specific EBS volume and its associated snapshots and future volumes created from this snaps.
- Once encryption enabled on volume you can't change a volume to NOT be encrypted.
- **exam imp** -- But OS of EC2 instance is not aware of the encryption.... they encryption with AES-256 algorithm happens directly between EC2 host and EBS volume. OS just sees plaintext and not aware of any encryption task. Hence, no performance loss from EC2 instance perspective.
- If you need to perform OS level encryption then that needs to be done as "Disk Encryption". Now, this disk level encryption can be applied to both encrypted EBS volume or non-encrypted EBS volume.
- Also, when you perform OS disk level encryption there could be some performance impact at EC2 instance level.
- Hence, EBS level encryption is not at all related in any way to full disk encryption at OS level.
- Also, EBS encryption is completely free.

### Elastic Network Interfaces (ENIs)
- which can be allocated to EC2 instances - and the DNS, public, private and elastic IPs which can be assigned to those ENIs.
- Whenever you launch an EC2 instance, it by default always have one ENI (primary) attached to it by default.
- Also, if required another ENI can be attached, these ENI can be in different subnets but EC2, subnets and ENIs, all should be in same AZ.
- few components of Network Interface
  - every ENI comes with a "mac address", which is actual device physical hardware address, and its visible at EC2 level. This could be used for software licensing, etc.
  - each ENI has primary private IPv4 address, this comes from subnet IPv4 CIDR range. This is static and it never change for the life of the EC2 instance.
  - you can also have 0 or more secondary private IPv4s
  - you can also have 0 or more public IPv4s. This is a dynamic, and it always gets changed when you stop and start a instance.
  - you can also have 1 Elastic IP per private IPv4 address. 
    - Elastic IP is public IPv4 address, and they are slightly different from normal IPv4, because you can have 1 Elastic IP per private IPv4 per interface. 
    - Hence you can have more than 1 if needed Elastic IP, because you can have more than 1 private IP per interface.
    - As soon as you attach an Elastic IP to a private IP, the earlier associated normal public IP gets removed. 
    - **exam immp** If you again wants to detach Elastic IP from this private IP, AWS automatically assign a new (different) normal public IP to this private IP and elastic IP gets removed/dettached.
  - you can have 0 or more IPv6 address.
  - ENI also contains Security groups, hence when SG connects to ENI, it impacts all IP addresses on that interface.
  - Hence, when you need to apply different security features on SG, you need to create different ENI and configure them accordingly.
  - you can also enable/disable source and destination check. meaning, if traffic is on ENI, it will be discarded if its not from one of the IP addresses on the interfaces that are configured as source or destination IPs.
    - Hence, we want EC2 to work with NAT instance, this option needs to be disabled. 
- Any additional ENI that you attached to an EC2 instance can be dittached and re-attached to another EC2 instance. At minimum of EC2 instance should always have one ENI attached.
- **Exam imp**
  - Secondary ENI +  Mac Address = Licensing, this allows you to move your licensing from one instance to another
  - multiple interfaces can be used for multi-homed systems (subnets), one for management and one for data
  - different security groups -- multiple interfaces
  - OS of EC2 never sees public IPv4 address
  - IPv4 public IPs are dynamic.. stop & start == change IPv4
  - public DNS == private IP in VPC, 
  - but public DNS == public IP address everywhere else for the outside communications

### Amazon Machine Images (AMI)
- Amazon Machine Images (AMI) 's are the images which can create EC2 instances of a certain configuration.
- In addition to using AMI's to launch instances, you can customize an EC2 instance to your bespoke business requirements and then generate a template AMI which can be used to create any number of customized EC2 instances.
- AWS or community provided
- marketplace (can include commercial software)
- Its a regional ... unique ID... eg: ami-0a89798595ghgjhk676
- permissions (public or your account or specific accounts)
- Its just a logical container, which has associated information.
  - This container not only contains any configuration of EC2 instance but also snapshots of EBS for AMI to use use in future.
  - Hence, we get the entire package, when we create an AMI from EC2, boot volume and EBS volume configuration.
  - These EBS volume snapshot is configured back to AMI as block device mapping
  - what is block device mapping? -- its just a table of data, it links snapshot IDs and device ID of original EC2 instance from which it gets created. example, two lines one fro "boot /dev/xvda" and other one for "data /dev/xvdf"
  - Hence, now you can use this AMI to create exactly same configuration in future.
- **exam power-up**
  - AMI == One region, only works in that one region
  - AMI Baking .. creating an AMI from a configuraed instance+ application
  - An AMI can't be edited... launch instance, update configuration and make a new AMI
  - can be copied between regions (includes its snapshots)
  - Remember permission ... default = your account

### Copying & Sharing an AMI
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/sharing-amis.html


### EC2 Purchase Options (launch types)
- On-Demand
  - its default and perfectly balanced types, from cost and resources perspective
  - instances of different sizes run on the same EC2 hosts, consuming a defined allocation of resources
  - per-second billing while an instance is running. Associated resources such as storage consume capacity, so bill, regardless of instance state.
  - No interruption, no capacity reservation, no capacity management required, predictable pricing, no upfront cost, no discount
  - good for short-term workloads, unknown workloads, apps which can't be interrupted
- Spot
  - cheapest way to get instance
  - SPOT pricing is AWS selling unused EC2 host capacity for up to 90% discount - the spot price is based on the spare capacity at a given time.
  - Never use SPOT for workloads which can't tolerate interruptions
  - this is mostly used for Non-time critical workloads, Anything which can re-run processes, bursty capacity needs, cost sensitive workloads, anything which is stateless.
- Reserved (also known as Standard reserve)
  - this is mostly used for long-term consistent usage of EC2.
  - This reduced per second cost or completely remove that per second, which is used to be the case in on-demand
  - unused reservation still billed, once you commited to reserve the capacity you have to pay for it
  - if you reserve smaller instance type but need to use in some case the larger size of same type of instance then partial coverage of larger instance is covered under reserve capacity discount.
  - Reservations are 1 year or 3 years
  - these are ideal for consistent access and long-term usage basis need and can't tolerate interruptions.
  - pay term has different options
    - No-upfront, some saving for agreeiing to the term but billed as per second fee. 
    - pay All upfront, means no per second fee, greatest discount
    - partial upfront, some discount, reduced per second fee billed
- Dedicated host
  - you pay for the host for specific family of instance type
  - No extra cost for running instances, you can run as many instances as you wish
  - idealy, use this when you have software which is licensed based on sockets or cores in physical machine.
  - it also has feature called host affinity -- means linking instances to certain EC2 hosts. Hence, if you start and stop instance, it remains on the same host.
  - capacity management is required
- Dedicated Instance
  - No other customers use the same hardware
  - all of your instances runs on the Dedicated host
  - but you don't own or share the host. Extra charges for instances but you get dedicated hardware
  - this comes with extra cost, you pay a one-off hourly fee for any regions where you are using dedicated instances, regardless of utilization, and the dedicated instance fee as well
  - no capacity management required, thats why you pay some extra cost

### Additional details on Reserved instances
- Scheduled Reserved Instances
  - ideally for long-term usage but that doesn't need to run constantly. 
  - Example, bigdata, machine learning, etc
  - Batch processing, daily for 5 hours, hence its long-term but don't use this instance for remaining time of the day
  - you specify the frequency, the duartion and the time
  - this is slightly cheaper than on-demand
  - some limitations/restrcitions, This doesn't support all instance types or regions. 
  - also, you need to purchase a minimum of 1200 hours per year and atleast 1 year term commitment is required
- the differences between zonal and regional reservations
  - regional reservation provides a billing discount for valid instances launched in any AZ in that region
  - but while flexible they don't reserve capacity with-in an AZ - which is risky during major faults when capacity can be limited. 
  - Zonal reservations only apply to one AZ providing billing discounts and capacity reservation in that AZ
  - but if you launched an instance in another region, then you pay full price and no capacity reservation.
  - This also requires atleast 1 or 3 years commitment to AWS
- on-demand capacity Reservations
  - there are 2 components in every reservation, billing component and capacity component
  - the combination or only one of this component is used for this type
  - meaning, sometime you need to reserve some capacity for short-period but can't do long-term commitment
  - this can be booked to ensure you always have access to capacity in an AZ when you need it. But at full on-demand price. No term limits - but you pay regardless of if you consume it or not.
  - No billing discount applied in this, no commitment for one or three years

### EC2 savings plan
- A hourly commitment for 1 or 3 year term, in return you get some discount
- this has 2 types
  - a reservation of "general compute dollar amount" (eg: $20 per hour for 3 years)
    - approx 60% saving compare to on-demand
  - or a specific EC2 savings plan - flexibility on size & OS 
    - approx 70% saving compare to on-demand
- This is currently application for only few AWS services
  - Currently, EC2, Fargate and Lambda
- the way this works is, products have an on-demand rate and a savings plan rate
- resource usage consumes upto saving plan commitment at a reduced price (saving plan rate)
- any consumption after that commitment period over charges at on-demand rate
- Hence, a general compute saving plan gives better discount and benefit on long term

### Instance Status Checks & Auto Recovery
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-recover.html
- 2 types of checks:
  - System status checks: (this is for Host)
    - loss of system power
    - loss of network connectivity
    - host software issues
    - host hardware issues
  - Instance status checks: (this is for instance)
    - corrupted file system
    - incorrect instance networking
    - OS kernel issues

### Shutdown, Terminate & Termination Protection
- Termination Protection is a feature which adds an attribute to EC2 instances meaning they cannot be terminated while the flag is enabled.
- "disableApiTermination" instance attribute (api) is used to all enable/disable this termination.
- Similarly, you can also configure, "change shutdown behavior". Meaning, when you shutdown an instance, do you want to Stop it or terminate it.


### Horizontal & Vertical Scaling
- are two ways which systems have to deal with increasing or decreasing user-side load.
- Each has pros and cons but handles the act of scaling radically differently.
- Scaling means, when systems needs to grow or shrink in response to increases or decreases of load.
- from technical perspective, adding or removing resources to a system, such as EC2 instance
- Why need scaling:
  - Each resize requires a reboot - hence disruption
  - also, scaling for large instances ofter carry a premium cost
  - hence, it better to manage instance properly, means increase as the demands increase and descrease as demands goes down
- vertical scaling
  - in this you increase the size and type of instance, instead of adding more instances to handle the load
  - meaning, if you are using t3.large --> then you move to t3.xlarge ---> if needs you move to t3.2xlarge
  - The benefit is no application modification required
  - This works for all type of applications, even monolithic's one as well
  - but horizontal scaling resolves some issues of vertical scaling
- Horizontal scaling
  - in this you add more resources to handle the load, meaning add more EC2 instances
  - in this architecture, you are going to run multiple copies of your application on these multiple instances
  - hence, when request comes, some kind of request management is needed to distribute traffic across these instances
  - Hence, Load banacer service is introduced
  - some key concepts to keep in mind, while designing this
    - Sessions are everything to handle this load in horizontal scaling
    - It requires application support or off-host sessions (externally hosted sessions, no dependency on instance host), because you continously shifting between different instances to balance the load. Hence, everything is handled by application session and it doesn't matter which instance you connect to.
    - these sessions are stored in a DB or in some other way to use it by application
  - Hence, benefit of this 
    - no application disruption while scaling
    - no real limits to scaling
    - often less expensive - no large instance premium required mostly
    - more granular scaling can be performed, because it completely adds new instance as per need.

### Instance Metadata
- Instance metadata is data about your instance that you can use to configure or manage the running instance.
- Instance metadata is divided into categories, for example, host name, events, and security groups.
- **exam imp** Instance metadata is accessed from an EC2 instance using - http://169.254.169.254/latest/meta-data/
- accessible inside all instance
- usually, below details are available in meta-data
  - instance environment details, 
  - instance networking details, 
  - authentication related details
  - user-data (scripts that can be run on instance as and when needed)
  - even public IPv4 address of instance which is not visible at EC2 instance level
- There are no authentication or encryption done for this meta-data information
- anyone who can connect to an instance and gain access to it linux command line shell can by default access to meta-data.
- This can be restricted by local firewall rules, but thats an additional admin task required if needed.
- Generally, its assumed that meta-data can get exposed.

### Advance EC2
### Bootstrapping EC2 using User Data
- EC2 Bootstrapping is the process of configuring an EC2 instance to perform automated install & configuration steps 'post launch' before an instance is brought into service.
- With EC2 this is accomplished by passing a script via the User Data part of the Meta-data service - which is then executed by the EC2 Instance OS
- User Data - Accessed via the meta-data IP
- http://169.254.169.254/latest/user-data
- Anything in User Data is executed by the instance only on Launch time. This doesn't work if you stop/start or restart the instance.
- EC2 doesn't interpret, the OS needs to understand the User Data.
- Its not secure - don't use it for passwords or long term credentials (ideally)
- User data is limited to 16 KB in size
- can be modified when instance stopped
- but only executed once at launch


### EC2 Instance Roles & Profile
- EC2 Instance roles and Instance Profiles are how applications running on an EC2 instance can be given permissions to access AWS resources on your behalf.
- Short Term Temporary credentials are available via the EC2 Instance Metadata and are renewed automatically by the EC2 and STS Services.
- Instance profile -- when you create an instance role in the console, an instance profile is created with same name, but you use the CLI or cloudformation, you need to create these 2 things seperately.
- Its instance profile that gets attached to an EC2 instance, when we attach an IAM role to an instance.
- Credentials are inside meta-data
- iam --> security-credentials --> role-name
  - http://169.254.169.254/latest/meta-data/iam/security-credentials
- Automatically rotated - Always valid
- Should always be used rather than adding access keys into instance
- CLI tools will use ROLE credentials automatically

### Configuration settings and precedence
- The AWS CLI uses credentials and configuration settings located in multiple places, such as the system or user environment variables, local AWS configuration files, or explicitly declared on the command line as a parameter. Certain locations take precedence over others. The AWS CLI credentials and configuration settings take precedence in the following order:

1. Command line options – Overrides settings in any other location. You can specify --region, --output, and --profile as parameters on the command line.

2. Environment variables – You can store values in your system's environment variables.

3. CLI credentials file – The credentials and config file are updated when you run the command aws configure. The credentials file is located at ~/.aws/credentials on Linux or macOS, or at C:\Users\USERNAME\.aws\credentials on Windows. This file can contain the credential details for the default profile and any named profiles.

4. CLI configuration file – The credentials and config file are updated when you run the command aws configure. The config file is located at ~/.aws/config on Linux or macOS, or at C:\Users\USERNAME\.aws\config on Windows. This file contains the configuration settings for the default profile and any named profiles.

5. Container credentials – You can associate an IAM role with each of your Amazon Elastic Container Service (Amazon ECS) task definitions. Temporary credentials for that role are then available to that task's containers. For more information, see IAM Roles for Tasks in the Amazon Elastic Container Service Developer Guide.

6. Instance profile credentials – You can associate an IAM role with each of your Amazon Elastic Compute Cloud (Amazon EC2) instances. Temporary credentials for that role are then available to code running in the instance. The credentials are delivered through the Amazon EC2 metadata service. For more information, see IAM Roles for Amazon EC2 in the Amazon EC2 User Guide for Linux Instances and Using Instance Profiles in the IAM User Guide.


### System and Application Logging on EC2
- Cloudwatch Agent needs to be installed to perform this task
- 












