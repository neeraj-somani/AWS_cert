# Advanced Networking (Networking_201)

### Egress-Only Internet Gateway
- Egress-Only internet gateways allow outbound (and response) only access to the public AWS services and Public Internet for IPv6 enabled instances or other VPC based services.
- Its an IGW which allows connection to be initiated from inside of VPC to outside
- Whats need of it in AWS
  - its needed because of difference in IPv4 vs IPv6
  - with IPv4 addresses are private or public
  - NAT Gateways allows private IPv4s to access public networks, without allowing externally initiated connections.
    - hence, NAT is a process to allow private EC2 instaces to access internet and receive responses back, but doesn't allow the public internet access initiated from internet.
    - **NAT Gateway doesn't work with IPv6**
    - because all IPv6 are public by default
    - hence IG (IPv6) allows all IPs IN and OUT access
  - This problem is solved by Egress-only IGW
- **Egress-only is outbound-only for IPv6**
- Egress-only gateway is Highly Available by default across all AZs in the region - scales as required.

### VPC Gateway Endpoints
- Gateway endpoints are a type of VPC endpoint which allow access to S3 and DynamoDB without using public addressing.
- **exam imp** Gateway endpoints add 'prefix lists' to route table, allowing the VPC router to direct traffic flow to the public services via the gateway endpoint.
  - Since everything is managed at route table, application don't need any modification
- **exam imp** -- Gateway endpoint is by default Highly Available (HA) across all AZs in a region by default.
- **exam imp** -- endpoint policy is used to control what it can access
- it can be used to access services in the same Region..... Hence its a Regional... can't access cross-region services
- use-cases
  - private VPC access S3 and dynamoDB using private endpoint
  - Prevent leaky buckets - S3 buckets can be set to private only by allowing access ONLY from a gateway endpoint
  - Hence, you can configure bucket policy to accept request only from specific endpoint.
- one limitation of Gateway Endpoint
  - **exam imp** -- They are only accessible from inside of VPC

### VPC Interface Endpoints
- Interface endpoints are used to allow private IP addressing to access public AWS services.
- S3 and DynamoDB are handled by gateway endpoints - other supported services are handled by interface endpoints.
- Unlike gateway endpoints - interface endpoints are not highly available by default - they are normal VPC network interfaces and should be placed 1 per AZ to ensure full HA.
- for HA.. add one endpoint, to one subnet, per AZ used in the VPC
- network access controlled via Security Groups
- Endpoint polcies - restrict what can be done with the endpoint
- **exam imp** They currently support only TCP protocol and IPv4 addresses
- **exam imp** Interface Endpoint basically used PrivateLink, which is an AWS product that allows external services to be injected into your VPC, either from AWS or from third parties
- Interface Endpoint provides a NEW service endpoint DNS
- e.g. - vpce-123-xyz.sns.us-east-1.vpce.amazonaws.com
- Interface Endpoint supports multiple types of DNS:
  - Regional DNS -- 
  - Zonal DNS
  - Private DNS -- this overrides the default DNS of specific service and use this interface provided private DNS
    - Private DNS associates a private R53 hosted zone to the VPC changing the default service DNS to resolve to the interface endpoint ip
- Interface endpoint uses DNS and a private IP address for communication.

### VPC Peering
- VPC peering is a software define and logical networking connection between two VPC's.
- They can be created between VPCs in the same or different accounts and the same or different regions.
- **exam imp** it can only create one direct encrypted network link between only two VPCs, remember that no more than two.
- (optinal) public hostnames resolve to private IPs
- Same region SG's can reference peer SGs
- **exam imp** -- VPC peering does NOT support transitive peering, meaning if VPC-A connects to VPC-B and VPC-B connects to VPC-C, that doesn't mean VPC-A can also connects to VPC-C. if you need a connection between VPC-A and VPC-C, a seperate connection needs to be establish.
- For VPC Peering, Routing configuration is needed, SGs & NACLs can filter.
- Route tables at both sides of the peering connection are needed, directing traffic flow for the remote CIDR at the peer gateway object.
- VPC peering connections cannot be created where there is overlap in the VPC CIDRs - ideally NEVER use the same IP address ranges in the multiple VPCs
- VPC peering communication is encrypted and trasits over the AWS global network when using cross-region peering connections.















