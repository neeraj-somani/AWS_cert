# RDS (Relational Database systems)
- Relational Database Service (RDS) is a Database(server) as a service product from AWS which allows the creation of managed databases instances.

### Database Refresher & MODELS
- SQL vs NoSQL
- SQL (Structured Query Language)
- NoSQL -- Not only SQL things (More relax schema design)
  - key-value storage
  - used for in-memory caching storage as well
- Document DB
  - ideal scenario - interacting with whole documents or deep attribute interactions
- Columnar Storage (Redshift)
  - columns are stored together
  - ideal for reporting or when all values for a specific attribute (size) are required.
- Graph storage
  - relationship between the data is stored with data

### Databases on EC2
- Generally its not recommeded
- But why you might want to do it **exam imp**
  - Access to the DB instance OS is needed
  - Advanced DB option tuning needed (DBROOT)
  - for DB or DB version AWS don't provide
  - or its a typical company need or ask
- Now, why you shouldn't really do it
  - admin overhead - managing EC2 and DBHost
  - Backup / DR Management requires lots of additional efforts
  - EC2 is by default in a single AZ (which is risky)
  - not able to use awesome features provided by AWS
  - EC2 is ON or OFF - no serverless, no easy scaling
  - Replication - skills, setup time, monitoring & effectiveness
  - performance ... AWS invest time into optimization & features

### RDS
- managed database instance (1+ DBs)
- multiple engines MySQL, MariaDB, etc....

### RDS High-Availability (Multi-AZ)
- MultiAZ is a feature of RDS which provisions a standby replica which is kept in sync with the primary instance.
- The standby replica cannot be used for any performance scaling ... only availability.
- Backups, software updates and restarts can take advantage of MultiAZ to reduce user disruption.
- **exam imp** For this kind of set-up you access RDS only via CNAME., because at the time of failover, no configuration changes needed. Standby can directly connected by the same CNAME.
- **exam imp** RDS multi-AZ provides only High availability, it doesn't provide fault-tolerance.
- Multi-AZ is not available in Free tier. Extra cost for Stand-by replica.
- Standby replica can't be access (used) directly.
- In-case of failover, standby will become primary and then only become accessible.
- Multi-AZ is in same region only (Other AZs in the same VPC region)
- This can help in various scenarios like, AZ outage, Primary Failure, Manual failover, instance type change and software patching.
- **exam imp** synchronous replication is nothing but Multi-AZ feature of RDS

### RDS Automatic Backup, RDS Snapshots and Restore
- RDS is capable of performing Manual Snapshots and Automatic backups
- Manual snapshots are performed manually and live past the termination of an RDS instance
- Automatic backups can be taken of an RDS instance with a 0 (Disabled) to 35 Day retention.
- Automatic backups also use S3 for storing transaction logs every 5 minutes - allowing for point in time recovery.
- Snapshots can be restored .. but create a new RDS instance.
- **Recovery point objective (RPO)**
  - Its the time between last backup and the incident
  - Amount of maximum data loss
  - influences technical solution and cost
  - Generally lower the RPO values requires cost more .. because that mean the business can't tolerate the data loss, and need to build a solution that can be more roburst to take back-ups and recover data loss easily.
- **Recovery time objective (RTO)**
  - Time between the disaster recovery or failure event and the full recovery occurs
  - Influenced by process, staff, tech, and documentation
  - Generally lower value cost more, meaning, the less time business decides to make the system fixed, needs more roburst system that can recover from failure quickly.
- RDS back-up types
  - Automatic Backups
    - Overall its same as manual backup
    - Scheduled snapshots taken as per configuration
    - but there is additional feature available with this, which is transaction logs, transaction logs occur every 5 min and get stored in S3
    - Hence, in combination of automatic snapshots and trasaction logs, a low RPO/RTO can be easily achieved
    - backups are retained indefinitely by default, but can be changes to configure between 0 second to 35 days.
  - Manual snapshots
    - snapshots are always manual
    - first snapshot is full copy of the data and then incremetal copy of snapshots captures changes in data
    - **exam imp** manual snapshots don't expire, and hence if required needs to be cleaned up manually
    - **exam imp** In other term, they can live on past the lifetime of RDS instance, if you delete RDS instance manual snapshot can still exist
    - In this RPO and RTO is in full control of yours configuration
  - AWS managed S3 buckets 
    - both back-ups use this, and hence its not visible through AWS console
    - The benefit of S3 is that now this data backup files can be used across AZ in that region, to create multi-AZ architecture
    - In case of multi-AZ setup, snapshots or back-ups always occurs from stand-by

### RDS Restores -- Exam power-up
- when perform RDS restore, it creates a NEW RDS instance - new database endpoint address
- snapshots == single point in time, creation time
- Automated == any 5 minute point in time
- backup is restored and transaction logs are 'replayed' to bring DB to desired point in time state
- restores from snapshots are not fast - think about RTO
- with replication there is risk of corruption
- with snapshots the risk of corruption data failure can be easily avoided.

### RDS Read-Replicas


