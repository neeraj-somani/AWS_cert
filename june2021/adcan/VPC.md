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



