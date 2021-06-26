# VPC (Virtual Private Cloud)
- A default VPC is created once per region when an AWS account is first created.
- There can only be one default VPC per region, and they can be deleted and recreated from the console UI.
- They always have the same IP range and same '1 subnet per AZ' architecture.
- used to create private network within cloud.
- VPC also used to create Hybrid env network when connecting on-premises servers with AWS private network.
- it can also be used to create multi-cloud env
- A VPC = A Virtual Network inside AWS
- A VPC is within 1 account & 1 region
- its reginally resillient
- by default, its a private and isolated unless you configure otherwise
- services deployed in one VPC can communicate with each other, but its isolated from other VPC and public internet. 
- two types of VPC - default VPC and Custom VPCs

### Default VPC
- They are pre-configured in a very specific way
- every VPC is alocated a VPC CIDR and that defines the start and end range of IP addresses that VPC can use.
- Custom VPC can have multiple CIDR ranges but default VPC only gets one CIDR and its always the same (172.31.0.0/16)
- Why and how come its always same?
- default VPC always configured in the same way and hence, its very predicatble. Its a strength, because you can utilize it accordingly if needed.
- default VPC consists of one or more AZs and each AZ has its own subnet (IP range) from the pool of CIDR range.
- its not used in prod env, because its not customizable
- by default, each VPC has IGW, Security Groups and NACL already created.
- by default subnets assign public IPv4 addresses
- each subnet is of "/20" CIDR range, which is sub-part of original "/16" CIDR.


### VPC Sizing and Structure (System Design lecture)
- the design choices around VPC design and IP planning.
- Lesson Links
  - https://aws.amazon.com/answers/networking/aws-single-vpc-design/
  - https://cloud.google.com/vpc/docs/vpc
- How to design a well-structured and scalable network inside AWS using VPC?
  - apart from VPC core functionality, this also needs to be understood
  - How to design an IP plan for a business, which includes how to design an individual network.
  - As a good Solution Architect, you should know what IP range a VPC will use in advance. Before even creating a VPC.
  - As a good Solution Architect, deciding on an IP plan and VPC structure is most imp thing to do in advance.
- VPC Considerations (things to avoid)
  - what size should the VPC be.. How many services needs to be fit into that VPC
  - Are there any network that we can or can't use
  - IP ranges can be used by other VPC's, other cloud, on-premises, partners & vendors
  - try to predict some aspects of future situations in advance
  - VPC structure - Tiers (web, application, DB) & Resiliency (Availability) Zones
  - prepare a list of systems that your application is going to interact with and what IP address range those systems currently using. This will avoid any overalap.
  - Also, what kind of application utility required, who is user of application and how many ways are they going to interact with this applications.
- VPC Considerations (things to pick)
  - VPC minimum "/28" (16 IP), maximum "/16" (65456 IPs) -- this is AWS limitations 
  - avoid common ranges - to avoid future issues
  - A good way to start planning for how many IP ranges is needed
    - is by answering, how many AWS regions the business will operate in
    - always plan for worst case, and even if needed add a few as a buffer
    - a suggession would be, reserve 2+ networks per region being used per account
    - example, 3 regions in US, 1 region in Europe, 1 region in Australia and need 2 ranges in each region
    - and in total we assume to have 4 accounts (so in total need 40 IP ranges)
- VPC Sizing
  - AWS provides 5 different options for VPC sizing
  - micro -- "/24" -- 
  - small -- "/21" --
  - medium -- "19" --
  - large -- "/18" --
  - extra large -- "/16" --
  - two imp questions needs to be answered here
    - How many subnets will you need?
    - How many IPs total? How many IPs per subnet?

### Designing a custom VPC
- **important for exam**
- VPC Limits https://docs.aws.amazon.com/vpc/latest/userguide/amazon-vpc-limits.html
- VPC is a regional service - it operate from all AZs in that region
- allows user to create isolated network
- Nothing IN or OUT without explicit configuration
- flexible configuration - simple or muti-tier
- allows hybrid networking - other cloud and on-premises
- you also get controls of deciding default tenancy or dedicated tenancy, meaning do you want to provision resources on shared hardware or dedicated hardware.
- a VPC can use IPv4 private CIDR blocks & public IPs
- the private CIDR block is main method of IP communication for VPC.
- by default, when you create a VPC, 1 Primary private IPv4 CIDR block already configured.
  - it has 2 main restrictions
    - min "/28" (16 IP) and Max "/16" (65536 IPs)
    - optionally you can get secondary IPv4 blocks by raising a support ticket
- VPC can also be configured to use IPv6 (optional), by default single IPv6 "/56" CIDR block is assigned
- with IPv6 you can't pick a block, same as you picked with IPv4. 
- Incase of IPv6, you can only use the range either alocated by AWS or only the IPv6s addresses that you already own.
- In IPv6 there is no concept of private and public IP addresses. By default all IPv6 addresses are publicly routable.
- but you still have to explicitly allow connectivity to and from the public internet.
- DNS in VPC
  - provided by Route53
  - its available inside the VPC on the base IP address of the VPC +2 address
  - example, if VPC is 10.0.0.0 then DNS IP will be 10.0.0.2
  - **exam imp** - Two options that defines how DNS works/behaves in VPC
    - enableDnsHostnames - if this sets to True, it gives instances with public IPs in a VPC a public DNS host names
    - enableDnsSupport - This indicates, DNS is enables or disabled in a VPC. If enabled, the instances in the VPC can use DNS IP address, so the VPC +2 IP address. if disabled (or default) then this is not available.
    - **exam question on this** -- if question indicates that you are having DNS issues, then these settings could be a solution.
  - DNS Resolution - The DNS resolution attribute determines whether DNS resolution through the Amazon DNS server is supported for the VPC. Helps in fast mapping of IPs with there corresponding DNS (domains).

### VPC Subnets
- In most AWS documentations, blue color on subnet diagram indicates private subnets, and green color indicates public subnets.
- By defaut the subnet in VPC is private, and you can configure them to make them public.
- Its a AZ resilient feature of VPC
- A sub-network of a VPC, within a particular AZ
- Hence, as a good solution architect, we design our systems in such a way that if one system fails in a AZ or subnet, its not affect the entire application. Other AZ can handle the fail-over and support the application functionality.
- one subnet = 1 AZ, One subnet can never be in multiple AZs
- but 1 AZ can have zero or one or more subnets.
- Subnet is nothing but a IPv4 CIDR, which is a subset of the VPC CIDR
- CIDR that a subnet uses, can not overlap with any other subnets in that VPC, all subnet CIDR should be non-overlapping
- Optional IPv6 CIDR can be allocated, if VPC IPv6 is enabled (/64 subnet of the /56 VPC - space for 256)
- by default, subnets can communicate with each other subnets in the same VPC
- Some IPs in every subnet is reserved. Lets understand what those are
  - In total 5 - Reserved IP addresses in every subnet, that can't be used by user. 
  - These are reserved for AWS usage
  - example, CIDR 10.16.16.0/20 (10.16.16.0 => 10.16.31.255)
  - first reserverd for Network address (10.16.16.0)
  - second reserved is for AWS VPC router (10.16.16.1) - also known as 'network +1'
    - a VPC router is a logical network device, which moves data between subnets, and in and out of the VPC if its configured to allow that.
    - a VPC router has a network interface in every subnet and it uses this network +1 address to communicate.
   - Third reserved is for AWS VPC DNS (10.16.16.2) - also known as 'network +2'
   - fourth reserved is for future unknown requirement (10.16.16.3) - also known as 'network +3'
   - fifth reserved is network Broadcast address (10.16.31.255) - also known as 'last network IP in a subnet'
    - broadcast feature is not supported inside VPC, but this IP is still reserved regardless.  
- DHCP options set
  - its a configuration object applied to VPC
  - it stands for Dynamic Host configuration protocol
  - its how computing devices receive IP addresses automatically
  - This configuration option applied one time at VPC level and it flows through to subnet level.
  - it controls things like DNS servers, NTP servers, NET bile servers, and few other things of network.
  - you can create them but you can't edit them. So, if any changes required, you need to create new one and re-configure your VPC to use new one.
- You can also configure VPC subnet to auto assign public IPv4 to itself
- Also, auto assign IPv6
-  Subnet Calculator : https://www.site24x7.com/tools/ipv4-subnetcalculator.html
- Subnets.txt : https://github.com/acantril/aws-sysops-associate/blob/main/09-VPC-Basics/03_vpc_subnets/subnets.txt

### VPC Routing, Internet Gateway & Bastion Hosts

### VPC Router
- A highly available device available in every VPC
- This device helps in moving traffic from somewhere to somewhere else
- can handle all the traffic across all AZs
- The traffic control can be handled by configuring 'route tables' in each subnet. So, if you don't want any specific subnet not to have access in another specific subnet, that control can be done using route table.
- A VPC is created with "main route table" for each subnet, so if you don't explicitly associate a custom route table with a subnet, by default it uses the main route table of VPC.
- When a custom route table is associated with a subnet, the main route table of VPC is disassociated.
- A subnet can have only one route table associated with it at a time.
- but one route table can be associated with many subnets at a time.
- The way that route works is it matches a destination IP, that is listed in route table, that it directs traffic towards a spcific target.
- if multiple match found, that more specific "/32" takes priority.

### Internet Gateway
- Highly available (resilient) regional service attached to a VPC
- you don't need IG per AZ, one IG can cover all AZs in a Region within a VPC
- 1 VPC = 0 or 1 IGW, 1 IGW = 0 or 1 VPC
- It runs from within the AWS Public zone
- Gateways traffic between the VPC and the internet or AWS Public Zone (S3, SNS, SQS, etc)
- Its a managed gateway -- meaning AWS handles the performance

### Lots of exam questions on IPv4 address
- how it works inside a VPC
- each EC2 instance in a VPC is assigned with a private IPv4 address by default. 
- A public IPv4 address also get assigned to EC2 instance, but this public IPv4 address is maintained at IGW level. A record gets created and maintained at IGW level.
- So, EC2 instance itself was never configured with public IPv4 address, and hence at Operation Systems (OS) level of EC2, you never sees this IPv4 public address.
- Hence, this public IPv4 address never touch any services inside a VPC
- Every packet that traverse with-in VPC or outside VPC is through some kind of route, and often we create a default route, which indicates, if non of the specific route matches then the packet can use this default route.
- And thats how every packet goes from private Ec2 instance to IGW and moves on further.

### whats the case with IPv6
- all IPv6, all addresses that AWS uses are natively publicly routable by default.
- Hence, in case of IPv6, the OS of EC2 instance does have the IPv6 association at OS level

### Bastion Host / Jumpbox
- Essentially its just an EC2 instance sitting in a public subnet inside a VPC
- the importance is, they are used to allow all incoming management connection to a bastion host and then securely internal-only VPC resources connection happens from this bastion host. 
- Its kind of heavy work done which IGW can handle easily
- Hence, it acts as a middle man between private instance of a VPC to a public internet route
- This is mostly used when you setup a highly secure private VPC and wants to have only bastion host as your only point of access from internet to private services of VPC.
- The configuration is done in way to allow inbound traffic only from certain IP addresses, and to authenticate only through SSH or to integrate with your on-premises identity servers.
- In the History, that was the only way to manage private EC2 instances from internet in a secure way.









