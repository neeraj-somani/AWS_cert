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
















