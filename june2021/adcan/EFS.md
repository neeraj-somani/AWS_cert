# EFS
- The Elastic File System (EFS) is an AWS managed implementation of NFS which allows for the creation of shared 'filesystems' which can be mounted within multi EC2 instances.
- EFS can play an essential part in building scalable and resilient systems.
- EBS is block storage while EFS is file storage
- EFS is a private service, and attached via mount targets inside a VPC
- EFS can be accessed from on-premises through VPN connections or AWS Direct Connect
- EFS use POSIX permissions -- its a standard for interoperability which is used by linux. so POSIX permissions file system is understand by all linux distributions.
- **exam imp** EFS only supported Linux instances
- EFS supports two modes --
  - General purpose and Max I/O performance modes
  - General purpose is ideal for latency sensitive use cases, web servers, content management systems.
  - General purpose is the default
  - Max I/O, scale at higher levels of aggregate throughput and operations per second
  - but a trade off would be increased latency
  - hence, Max I/O means, high throughput and that cause high latency
  - so, max I/O is ideal for applications that are highly parallel like big-data, media processing, scientific analysis, etc..
- There are also two throughput mode
  - Bursting -- its similar to gp2 EBS volumes, hence throughput scale with the size of data
  - Provisioned -- in this you can specify throughput requirement sepearetly from size
- EFS also comes with two storage class
  - Infrequent Access (IA)
  - Standard (default)
- you can also use object life-cycle policy in EFS, which is very similar to S3.
- 

# Lesson Links
- https://en.wikipedia.org/wiki/File_system_permissions
- https://docs.aws.amazon.com/efs/latest/ug/performance.html
- https://docs.aws.amazon.com/efs/latest/ug/storage-classes.html
- https://docs.aws.amazon.com/efs/latest/ug/lifecycle-management-efs.html
