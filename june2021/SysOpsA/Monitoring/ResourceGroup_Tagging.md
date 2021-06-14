# What is Tagging?
- Key-value pair that provide details about resources
- Metadata (data about data)
- Tags are case-sensitive
- Tags can sometimes be inherited
  - Autoscaling, CloudFormation, and Elastic Beanstalk can create other resources



# what is Resource Group? -- https://docs.aws.amazon.com/ARG/latest/userguide/welcome.html
- Resource groups make it easy to group your resources using the tags that are assigned to them.
- You can group resources that share one or more tags.
- Resource groups contain information such as; Region , Name , Health Checks
- Specific information
    - For EC2 - Public & Private IP Addresses 
    - For ELB - Port Configurations
    - For RDS - Database Engine etc
- You can create unlimited, single-region groups in your account, 
- use your groups to view group-related insights, and automate tasks on group resources. 
- Groups can be based on resource types and tag queries, or AWS CloudFormation stacks.
- Run complex tasks on your grouped resources by using AWS Systems Manager Automation.
- View group-specific insights from AWS Config and AWS CloudTrail.


**AWS Systems Manager** -- most imp for sysops cert
- execute automation tasks on group resources
