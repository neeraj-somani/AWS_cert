# AWS Fundamentals

### AWS Public vs Private services in terms of networking only
- meaning by default no permissions to anyone aside from account root user
- When connecting to AWS service there are 2 components
  - connectivity to that service - the device like laptop, mobile, can communicate to that service using a network
  - if we connect, do we have permission to access that service
- the difference between public and private services is the connectivity, its a networking difference.
- AWS services are not directly available on public internet. You need to create a connection between AWS public zone and public internet to connect to AWS services.



### AWS Global Infrastructure - https://www.infrastructure.aws/
- AWS have created a global public cloud platform which consists of isolated 'regions' connected together by high speed global networking.
- Regions -->  area of the world that AWS selected and deployed full AWS infrastructure
  - benefits -
    - Geographic separation - isolated fault domain
    - geopolitical seperation - different goverance
    - location control - performance
- Availability Zones (AZ)
  - isolated infrastrure inside a region
  - one region can have one or more AZ
  - AZ could be one or more Data centers
  - All AZ with-in a region connected with High speed low latency (redundant) networking.
- Edge Locations --> (local) smaller than region, and numbers of EL is more than region

### Globally Resilient
- example, IAM, Route53
- if one part of the world has any disaster or issue, it wouldn't affect service or application running on it much.
- in terms of AWS, we don't select region for these services

### Regional Resilient
- services that are operate in single region
- seperate services in each region
- example, RDS instance running in Sydeny and North Virginia
- if region fails then only it impact, otherwise, AZs will take care of regional issues.

### AZ resilient
- these services completely depends on the infrasture part of that AZ.
- if AZ fails or issues occure, it can impact the service or application



