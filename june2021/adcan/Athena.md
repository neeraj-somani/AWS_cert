# Athena
- Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL
- Athena is **serverless**, so there is no infrastructure to manage, and you pay only for the queries that you run and data consumed.
- Athena is easy to use. Simply point to your data in Amazon S3, define the schema, and start querying using standard SQL. 
- Most results are delivered within seconds. 
- With Athena, there’s no need for complex ETL jobs to prepare your data for analysis.
- Original data never changed - remains on s3
- schema translate data ==> relational-like when read
- output can be sent other AWS services
- Athena can directly read many AWS data formats such as cloudTrail, EBS logs Flow Logs, cost reports, etc
- XML, JSON, CSV, AVRO, Parquet,..... etc.....
- Data Catelog -- "Tables" are defined in advance in a data catalog
- data is projects through to these tables when read, or run SQL,
- It allows SQL-like queries on data without transforming source data

### Exam powerup
- Athena has no infrastructure overhead
- Queries where loading/transformation is not needed (desired)
- Occasional / Ad-hoc queries on data in S3
- Its a native service to use to query log files like, cloudTrail, EBS logs Flow Logs, cost reports, etc
- It can also query data from AWS Glue Data Catelog and web server logs
- Athena now has capabilities to query non-s3 data sources as well.
- using Athena federated query -- uses a data source connectors to make connections and run queries on non-s3 resources.
- data source connectors -- is a piece of code (run on lambda) that can translate between a target (non-s3 resources) and Athena when you run queries.
- few very common pre-built aws provided connectors that are already available for use
  - DynamoDB, Oracle, MySQL, MSSQL, etc
  - cloudTrail, EBS logs Flow Logs, cost reports, etc
