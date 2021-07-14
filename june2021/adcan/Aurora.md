# Aurora
- Aurora architecture is VERY different from RDS 
- because it by default uses "cluster" of instances
- A single primary instance + 0 or more replicas
- It provides both scalability (better performance) and improved availability benefits by default
- No local storage - uses cluster volume storage, these volume storage is shared among all compute instances within a cluster
  - storage is much more resilient than RDS
  - by default it uses SSD based storage volume - hence high IOPS, low latency  
  - storage is for the cluster and not for individual instance
  - replicas can be added or removed without reuiring storage provisioning.
  - Aurora doesn't require you to provision storage volume upfront. It automatically allocates you as per your usage and billed accordingly. 
- Aurora cluster provisioning is comparatively very fast
- supports upto 15 replicas
- pricing
  - No free-tier option
  - Aurora doesn't support micro instance types
  - Beyond RDS singleAZ (micro) aurora offers better value
  - compute - hourly charge, per second, 10 minutes minimum
  - Storage - billed GB per month consumed, IO cost per request
  - storage is billed based on what's used
  - High water mark - billed for the most used
    - example if one day you consumed 50 GB and next day you lowered the storage to 40 GB. You will still be billed for 50 GB. 
    - And you can use the remaining 10 GB as and when you like. Storage which is freed up can be re-used
  - 100% DB size in backups are included in this price (no additional cost for that)
- In general there are 2 endpoints
  - cluster endpoint (writer) that connects to primary
  - reader endpoint that connects to all replicas and load balance the traffic across replicas
  -  custom endpoints can also be created as per need
- Aurora Backups / restore
  - backups in aurora work in the same way as RDS
  - Restores creates a new cluster
  - Backtrack can be used which allow in-place rewinds to a previous point in time of cluster, in-case of data corruption or DR
  - Fast clones make a new DB much faster than copying all the data - copy-on-write  



### Aurora Serverless
- All above listed points are for "Aurora Provisioned", now will discuss about serverless
- it provides a version of Aurora DB product, without statically provision based on size, or managing DB instances
- a step closer to Database-as-a-service-product
- In serverless architecture, there are few key concepts that implemented in aurora to support these features
- for scalability - ACU - Aurora Capacity Units
- you can pre-configure cluster with Min and Max ACU. 
- Everything managed automatically by Aurora based on cluster load
- it can go to 0 and be paused
- Consumption billing per-second basis
- same resilience as Aurora (6 copies across AZs)
- ACUs are shared across many AWS customers.
- Each customer gets capacity as per ACU configuration.
- One more important point, is that, any application that unitilze to Aurora, doesn't connect to it directly. All connection to Aurora happens through fleet of EC2 instances. Hence, this give better flexibility to Aurora in terms of scalability and performance.
- few suitable use-cases
  - Infreqently used applications, low volume blog sites, very limited user base application but random
  - New application, where usage is not predicatable upfront
  - variable workloads
  - unpredictable workloads
  - development and test databases workloads
  - multi-tenant applications


### Aurora global databases
- a feature of Aurora Provisioned clusters which allow data to be replicated globally providing significant RPO and RTO improvements for BC and DR planning. 
- Additionally global databases can provide performance improvements for customers .. with data being located closer to them, in a read-only form.
- Replication occurs at the storage layer and is generally ~1second between all AWS regions.
- upto 5 AWS region other than the master or main region
- secondary region can have upto 16 replicas
- no impact on DB performance, because it happens at the storage layer

### Aurora Multi-master writes
- Multi-master write is a mode of Aurora Provisioned Clusters which allows multiple instances to perform reads and writes at the same time - rather than only one primary instance having write capability in a single-master cluster. 
- Default Aurora mode is Single-master
  - Which provides one R/W and 0+ read only replicas
  - cluster endpoint can be used for read/write, read endpoint is used for load balanced reads only
  - failover takes time - replica promoted to R/W
- In multi-master mode all instances are Read/write
  - hence there is no concept of lengthy fail-over
  - there is no concept of load-balanced endpoint, application can directly connect to individual node endpoint of cluster. hence application manage that endpoint configuration.
  - whenever there is a write operation occurs, it always write simultaneously to all copies of storage volume together.
  - if all volumes accepts this write operation that it gets commited, otherwise error out
  - another important feature that this mode provides, all nodes of cluster replicates same in-memory cache objects based on read patterns. This improves performance across all nodes of cluster.










