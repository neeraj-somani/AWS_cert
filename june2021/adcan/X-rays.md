# X-rays
- AWS X-Ray helps developers & engineers analyze and debug production, distributed applications, such as those built using a microservices architecture..
- With X-Ray, you can understand how your application and its underlying services are performing to identify and troubleshoot the root cause of performance issues and errors.
- X-Ray provides an end-to-end view of requests as they travel through your application, and shows a map of your application’s underlying components.
- Its a distributed tracing application, its designed to track sessions through an application

### Various components of X-ray
- Tracing header - first service generates this ... its a unique (Trace ID) , and used to track a request through your distributed application
- Segments -- single Data blocks - from each services -- host/ip, request, response, work done (start/end times), issues, user agent (browser)
- X-rays collect all individual segmnets to privide end-to-end flow for specific request
- Subsegments (optional) -- if configures --- more granular version of the above, calls to other services as part of a segment (endpoints etc). Its like a verbose log mode vs normal log mode.
- Service Graph -- JSON Documnet detailing services and resources which make up your application. 
  - this graph shows how different services are connected and how those components work together to service requests.
- Service Map - Visual version of the service graph showing traces

### How to configure it in your account
- every service can use it in a different way
- EC2 - X-ray agent installation is required
- ECS - agent is installed in any tasks running within that service
- Lambda - enable option
- Beanstalk - agent pre-installed
- API Gateway - per stage option
- SNS and SQS
- Requires IAM permissions


