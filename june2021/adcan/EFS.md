# EFS
- The Elastic File System (EFS) is an AWS managed implementation of NFS which allows for the creation of shared 'filesystems' which can be mounted within multi EC2 instances.
- EFS can play an essential part in building scalable and resilient systems.
- EBS is block storage while EFS is file storage
- EFS is a private service, and attached via mount targets inside a VPC
- EFS can be accessed from on-premises through VPN connections or AWS Direct Connect
- EFS use POSIX permissions -- its a standard for interoperability which is used by linux. so POSIX permissions file system is understand by all linux distributions.
- 
- 


# Lesson Links
- https://en.wikipedia.org/wiki/File_system_permissions
- https://docs.aws.amazon.com/efs/latest/ug/performance.html
- https://docs.aws.amazon.com/efs/latest/ug/storage-classes.html
- https://docs.aws.amazon.com/efs/latest/ug/lifecycle-management-efs.html
