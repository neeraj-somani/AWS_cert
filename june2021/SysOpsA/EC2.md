## Some notes on EC2 from various places


- Question: whats the difference between EC2 host and instance?
  - [Dedicated instance](https://aws.amazon.com/ec2/pricing/dedicated-instances/)
    - Dedicated Instances are Amazon EC2 instances that run in a VPC on hardware that's dedicated to a single customer. Your Dedicated instances are physically isolated at the host hardware level from instances that belong to other AWS accounts. Dedicated instances may share hardware with other instances from the same AWS account that are not Dedicated instances.
  - [Dedicated Host vs Dediacted instance](https://aws.amazon.com/ec2/dedicated-hosts/)
    - You can also use Dedicated Hosts to launch Amazon EC2 instances on physical servers that are dedicated for your use. Dedicated Hosts give you additional visibility and control over how instances are placed on a physical server, and you can reliably use the same physical server over time. As a result, Dedicated Hosts enable you to use your existing server-bound software licenses like Windows Server and address corporate compliance and regulatory requirements.
- Testing


## EC2 Pricing model - used for monitoring resources
### On-Demand instances 
  - Users that want the low cost and flexibility of Amazon EC2 without any up-front payment or long-term commitment 
  - Applications with short term, spiky, or unpredictable workloads that cannot be interrupted
  - Applications being developed or tested on Amazon EC2 for the first time

### Reserved instance
 - Applications with steady state or predictable usage
 - Applications that require reserved capacity
 - Users able to make upfront payments to reduce their total computing costs even further
 - Standard RI’s (Up to 75% off on demand)
 - Convertible RI’s (Up to 54% off on demand) capability to change the attributes of the RI as long as the exchange results in the creation of Reserved Instances of equal or greater value.
 - Scheduled RI’s available to launch within the time windows you reserve. This option allows you to match your capacity reservation to a predictable recurring schedule that only requires a fraction of a day, a week, or a month.

### Spot Instance
- Applications that have flexible start and end times 
- Applications that are only feasible at very low compute prices 
- Users with urgent computing needs for large amounts of additional capacity

### Dedicated host
- Useful for regulatory requirements that may not support multi- tenant virtualization.
- Great for licensing which does not support multi-tenancy or cloud deployments.
- Can be purchased On-Demand (hourly.)
- Can be purchased as a Reservation for up to 70% off the On- Demand price.
