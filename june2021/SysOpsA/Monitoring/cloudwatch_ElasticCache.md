# Monitoring ElasticCache using Cloudwatch
- https://docs.aws.amazon.com/elasticache/index.html
- Elastic Cache matrics -- https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/CacheMetrics.html

## Elastic Cache
- its a caching engine used to cache most prequently used queries
- ElastiCache provides metrics that enable you to monitor your clusters.

- ElastiCache provides both host-level metrics (for example, CPU usage) and metrics that are specific to the cache engine software 
- (for example, cache gets and cache misses). 
- These metrics are measured and published for each Cache node in 60-second intervals.
- 
### Elasticache consists of two engines:
- Memcached
- Redis


## 4 imp things for cache monitoring 
- CPU Utilization
  - Memcached
    - Multi-threaded
    - **exam imp** Can handle loads of up to 90%. If it exceeds 90% add more nodes to the cluster
  - Redis
    - Not multi-threaded. 
    - To determine the point in which to scale, take 90 and divide by the number of cores
    - For example, suppose you are using a cache.m1.xlarge node, which has four cores. In this case, the threshold for CPU Utilization would be (90 / 4), or 22.5%
- Swap Usage
  - swap usage is simply the amount of the Swap file that is used.
  - The Swap File (or Paging File) is the amount of disk storage space reserved on disk if your computer runs out of ram.
  - Typically the size of the swap file = the size of the RAM.
  - So if you have 4Gb of RAM, you will have a 4GB Swap File.
    - Memcached
      - mostly swapusage is avoided, or very rarely used
      - Should be around 0 most of the time and should not exceed 50Mb. 
      - If this exceeds 50Mb you should increase the memcached_connections_overhead parameter.
      - The memcached_connections_overhead defines the amount of memory to be reserved for memcached connections and other miscellaneous overhead.
      - Learn More; http://docs.aws.amazon.com/AmazonElastiCache/latest/UserGuide/CacheParameterGroups.Memcached.html
     - Redis
      - No swapusage metric, instead use reserved-memory metric
- Evictions (very similar to tenants in apartments - analogy)
  - An Eviction occurs when a new item is added and an old item must be removed due to lack of free space in the system.
    - memcached
      - There is no recommended setting. Choose a threshold based off your application
      - **exam imp** - Either Scale Up (ie increase the memory of existing nodes) OR
      - **exam imp** - Scale Out (add more nodes)
    - Redis
      - There is no recommended setting. Choose a threshold based off your application 
      - **exam imp** - Only Scale Out (add read replicas)
- concurrent connections
  - Memcached & Redis
    - There is no recommended setting. Choose a threshold based off your application
    - If there is a large and sustained spike in the number of concurrent connections this can either mean a large traffic spike OR your application is not releasing connections as it should be
    - basically, setup cloudwatch alarm on number of concurrent connections and based on above point scenario reconfigure the application
