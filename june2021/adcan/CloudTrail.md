# CloudTrail Service
CloudTrail Is a product which logs API calls and account events, also known as CloudTrail Event

### features
- It's very often used to diagnose security or performance issues, or to provide quality account level traceability.
- It is enabled by default in AWS accounts and logs free information with a 90 day retention.
- It can be configured to store data indefinitely in S3 or CloudWatch Logs.
- To customize the service.. create 1 or more trails
- Its a regional service
- A Trail can be set as One region or all regions
- The way it works in case of all regions trail is, it collect individual trails from each region and manage collection of all individual regional trail as one logical trail.
- Data Event and Management event can be logged in Trail

### **Exam Points** 
- Cloudtrail is enabled by default on an AWS account
- but its only 90 days event history by default
- by default no storage on S3
- For any customization to default settings, we need to configure trail
- Trails are how you configure S3 and Cloudwatch logs, you can collect the data from various other services and accounts and store them to S3 or cloudwatch logs.
- By default, cloudTrail stores management events only, example, creating an instance, stopping an instance, creating S3 bucket, deleting S3 bucket, Console user log-in activities,
- But Data events, needs to be specifically enabled, there is extra cost associated with it.
- **above point is very imp, exam test on CloudTrail pricing items**
- IAM, STS, CloudFront are global services, and they log their data as global service events in cloudTrail. And these gets logged in us-east-1 region and a specific trail needs to be configured to capture this data.
- Question - Can you use cloudTrail for real-time logging??
- Answer - It is not realtime, There is a slight delay (around 15 min), of the account activity occurring. It generally logs events multiple times in an hour.
- Points related to cloudTrail pricing
  - by default configuration, 90 days cloudTrail event history is free of cost
  - Also, one copy of management events free to every AWS account per region. Any additional trails, comes with additional charges.
  - Data events, comes with charges. At present data events only available for lambda function and S3 buckets.
  - Cloudtrail insights provides visibility into unusual operational activities in AWS account, this comes with some charges. 
  - Event history 

### points from cloudTrail demo lesson
- This CloudTrail will be configured for all regions and set to log global services events.
- We will set the trail to log to an S3 bucket and then enhance it to inject data into CloudWatch Logs.
- CloudTrail Pricing : https://aws.amazon.com/cloudtrail/pricing/
- CloudWatch Logs Pricing : https://aws.amazon.com/cloudwatch/pricing/
