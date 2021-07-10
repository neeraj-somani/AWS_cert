# RDS (Relational Database systems)


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
