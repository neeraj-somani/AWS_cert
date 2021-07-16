# FSx (File System as a Service)
- FSx for Windows Servers provides a native windows file system as a service which can be used within AWS, or from on-premises environments via VPN, Peering or Direct Connect
- FSx is an advanced shared file system accessible over SMB, and integrates with Active Directory (either managed, or self-hosted).
- It provides advanced features such as VSS, Data de-duplication, backups, encryption at rest and forced encryption in transit.
- it can be deployed in single or multi-AZ within a VPC
- it can perform on-demand and schduled backups
- This is like EFS for Windows OS in nutshell.
- Its a shared file system for windows instances
- **exam imp** -- exam question will trick you on this, in a way which one you use in which situation. (EFS vs FSx)
- it also supports volume shadow copies (file level versioning)
- Native windows file system, supports de-duplication (subfile) distributed file system (DFS), KMS at-rest encryption and enforced encryption in-transit.
- **Exam imp**
  - VSS - User-Driven Restores
    - windows level feature that allows user to perform file and folder level restores (meaning version control)
    - Also, its natively support user-driven engagement without involving a system administrator.
  - Native file system accessible over SMB
  - Its natively supports windows permission model
  - supports DFS (distribuited file system)... scale-out file share structure
  - its a self-managed - no file server admin required
  - Integrates with Directory service (DS) and your own Active directory


### FSx for Lustre
- FSx for Lustre is a managed file system which uses the FSx product designed for high performance computing
- It delivers extreme performance for scenarios such as Big Data, Machine Learning and Financial Modeling
- https://docs.aws.amazon.com/fsx/latest/LustreGuide/performance.html#fsx-aggregate-perf
- **exam imp** -- need to understand when to use FSx for windows and FSx for Lustre
- Lustre is file system designed specifically for high performance computing.
  - It supports linux based instances in AWS and supports POSIX style permissions in file systems.
- FSx for Lustre can scale upto 100's GB/sec of throughput and offers sub millisecond latency
- FSx for Lustre - two different deployment types
  - Use Scratch --- for the absolute best performance for short term workloads but it doesn't provide resilience or high availability.
  - use persistent --- for resilience or high availability and use this for long-term storage. 
- **exam imp** -- remember Lustre is a single AZ FS because it needs to provide this really high-end performance.
- So, if any hardware fails in one AZ, it will be automatically replaced by AWS
- The data is lazy loaded from S3 repository to file system and vice versa but its not to automatically in sync.
- Persistent has replication within one AZ only
- you can back-up to S3 as well.
