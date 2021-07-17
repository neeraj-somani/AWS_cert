# Elastic Load Balancer (ELB)
- The Elastic Load Balancer (ELB) was introduced in 2009 with the 'now called' Classic Load Balancer
- Two new versions the v2 Application and v2 Network load balancers are now the recommended solutions.
- ELB in general terms refers to the whole family of all 3 types of load balancer

### CLB
- CLB can load balance http/https as well as lower level protocols but there are not layer 7 devices.
- CLB don't understand http and can't make decisions based on http protocols.
- there are many limitations of CLB and hence its not used any more, one example 1 SSL per CLB

### ALB
- its version 2 devices
- its truely layer 7 (application layer) devices
- it supports http/https/web-socket protocols
- hence its used for all web applications that uses above listed protocols

### NLB
- its version 2 devices
- Its a network layer devices
- supports TCP, TLS, & UDP protocols
- hence its used for all applications which don't use http or https

- NLB and ALB are faster, cheaper and support target groups and rules

## ELB Architecture
- Elastic Load Balancers are a core part of any scaling architecture within AWS.
- the job of load balancer is to accept the connection from customers
- and then distribute those connections across any registered backend compute
- hence, it integrate away the user from physical infrastructre, and hence any changes to infra doesn't impact customer
- As the infrastructure scale, there is also ELB pattern that needs to be configured accordingly to handle the scale of architecture
- meaning, are you adding more **internet** facing ELB or **internal** facing ELB
- because, internet facing ELB have given both public IP and private IP addresses
- but if you add, internal facing ELB then only given private IP addresses
- ELB (nodes) are configured with **listeners** which accepts traffic on a port & protocol and communicate with targets on a port and protocol.
- **exam imp** internet facing LB can work with both private and public EC2 instances, without any extra config as long as permissions are given accordingly.
- AWS also recommend for a /27 or larger subnet to allow for scale and 8+ free IPs per subnet for scale
- Internal LB usually allow to seperate different tier of applications and allow internal infra scaling as per need to load balance the traffic accordingly.
- LB's allow each tier to scale independently

### Cross-zone LB (feature of ELB)
- by default ELB supports this feature and traffic balance across AZ within a region

### Key points about ELB for exam
- when you provision ELB, you see it as one device but in reality it runs in two or more AZs. specifically, one subnet in each AZ
- Hence, you  are actually creating one ELB node in one subnet in each AZ.
- Hence, ELB is a DNS A record pointing at 1+ nodes per AZ
- nodes scale automatically as per traffic need
- internet-facing means nodes have public IPv4 IPs
- internal is private only IPs
- EC2 doesn't need to be public to work with a LB.
- listener configuration controls what the LB does
- LB require 8+ free IPs per subnet, and /27 or /28 subnet to allow scaling

### Application Load balancing (ALB) vs Network Load Balancing (NLB)











