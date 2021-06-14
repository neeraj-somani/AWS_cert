# Monitoring ELB using Cloudwatch

3 Different Types of Elastic Load Balancers;
- Application Load Balancer (Layer 7 LB)
- Network Load Balancer (Layer 4 LB)
- Classic Load Balancer (also known as ELB) - deprecated

4 Different Ways To Monitor Your Load Balancers;
- CloudWatch metrics 
  - few matrics enabled by default on ELB
  - default matrics like, unhealthy host count, healthy host count, average latency, requests count, HTTP 5xxs count, etc
- Access logs 
  - disabled by default on ELB
  - capture detailed information about requests sent to your load balancer
  - Each log contains information such as the time the request was received, the client's IP address, latencies, request paths, and server responses
  - You can use these access logs to analyze traffic patterns and troubleshoot issues
  - After you enable access logging for your load balancer, Elastic Load Balancing captures the logs and stores them in the Amazon S3 bucket that you specify as compressed files. You can disable access logging at any time.
  - **exam imp** - Access Logs can store data where the EC2 instance has been deleted. For example say you have a fleet of EC2 instances behind an auto scaling group. For some reason your application has a load of 5XX errors which is only reported by your end customers a couple of days after the event. If you aren’t storing the web server logs anywhere persistent, it is still possible to trace these 5XX errors using Access Logs which would be stored on S3.
  - interval - can be 5 mins or 60 minutes
- Request tracing
  - Available for Application Load Balancers Only.
  - You can use request tracing to track HTTP requests from clients to targets or other services. 
  - When the load balancer receives a request from a client, it adds or updates the X-Amzn-Trace-Id header before sending the request to the target. 
  - Any services or applications between the load balancer and the target can also add or update this header. 
- CloudTrail logs
  - used for auditing
  - You can use AWS CloudTrail to capture detailed information about the calls made to the Elastic Load Balancing API and store them as log files in Amazon S3. 
  - You can use these CloudTrail logs to determine which calls were made, the source IP address where the call came from, who made the call, when the call was made, and so on.
  - example, who provisioned load balancer, decommissioning load balancer
  - changing health check configuration of ELB
  - any changes to ELB environment can be traced using cloudTrail
  - The only thing that cloudTrail can't track is matrics, like healthy host count, unhealthy host count

## Cloudwatch vs cloudTrail

- CloudWatch monitors performance.
- CloudTrail (auditing) monitors API calls in the AWS platform.
  - what a resource has been provisioned, 
  - who provisioned it
  - what IP address was used








