# AWS Config
- https://aws.amazon.com/config/faq/
- https://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html
- its a region based service **exam imp**
- fully managed service that provides you with an AWS resource inventory, configuration history, and configuration change notifications to enable security and governance
- its like recording service (similar to security camera service) that records every configuration changes happening inside AWS environment all the time.
- we can go back in time and see our configuration at any given time
  - example, how our Security groups were configured 2 weeks back
  - how many instnaces were configured last month
  - you can audit your account, environment for any given time duration
 

### Features
- Compliance auditing 
- Security analysis 
- Resource tracking

### Provides
- Configuration snapshots and logs config changes to AWS resources
- Automated compliance checking

### Key components
- Config Dashboard 
- Config Rules
  - Managed
  - Custom 
- Resources 
- Settings


# Terminology:
- Configuration Items
  - Point-in-time attributes of resource
  - example, what ports are configured on security group at specific time
- Configuration Snapshots 
  - Collection of Config Items
  - taken every 1 hour, 3 hour, 6 hours
- Configuration Stream
  - Stream of changed Config Items
- Configuration History
  - Collection of config items for a resource over time 
- Configuration Recorder  
  - The configuration of Config that records and stores config items
  - stores in S3
  - Notifies using SNS
  - Logs config for account in region, basically region by region basis

### What can we see:
- Resource Type 
- Resource ID 
- Compliance check 
  - based on set Triggers / rules
    - periodic (1 hr, 2hr, 5 hr)
    - configuration snapshot delivery (filterable)
      - meaning, as soon as there is change in Security group config, compliance check gets triggered
  - Managed Rules
    - 
- Timeline
  - Configuration Details 
  - Relationships - what EC2/RDS instances belong to security groups
  - Changes
  - CloudTrail Events

### Benefits
- Continous Monitoring - you are able to continuously monitor and record configuration changes of your AWS resources.
- Continous Assesement - allows you to continuously audit and assess the overall compliance of your AWS resource configurations with your organization's policies and guidelines.
- change management - you are able to track the relationships among resources and review resource dependencies prior to making changes.
- operational troubleshooting - you can capture a comprehensive history of your AWS resource configuration changes to simplify troubleshooting of your operational issues.






