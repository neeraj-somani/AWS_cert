# Route53
- register domains
- host zones .. managed nameservers
  - zone files in AWS
  - hosted on four managed name servers
  - can be public
  - or private ... linked to VPCs
  - stores records (recordsets)
- global service ... single database
- globally resilience
- name servers 
  - the entries that AWS (DNS provider) created in nameserver and shared it to top level domain resigtrar (eg: .org)
  - thats how they are linked and delegated

DNS is capable of handling a number of different record types - which perform different tasks, as well as introducing TTL values on records.

### DNS Record Type
- Nameserver (NS) -
  - these are record type that allow delegation to occur in DNS
  - entry of NS for any specific domain is listed in top level zone and based on these NS entry, DNS delegate the request to the specific zone for domain.
  - example of NS (amazon.com -- pdns1.ultradns.net , pdns6.ultradns.co.uk)
  - these 2 NS entry, means connected to 2 different hosted zone
- A & AAAA
  - these record type maps "Host to IP" 
  - A is for IPv4
  - AAAA is for IPv6
- CNAME (Canonical Name)
  - allows you to create DNS shortcuts
  - maps "host to host"
  - example, if A record domain perform multiple tasks like, ftp, mail, www, then 
  - all CNAME records can be resolved to same A record domain
  - hence, if for any instance if A record changes, all others has no impact
  - **exam imp** -- CNAME cannot directly point to an IP address, only other names
- TXT
  - allows you to add arbitrary text to a domain
  - example, is to prove domain ownership
  - other example, fight spam emails, 
- MX
  - used for email capability
  - mx record has two parts, a priority and a value
  - for mx record, the priority of record in sequencial order
  - this is how a mail server can find a specific domain

### DNS TTL (time-to-live)
- TTL set on DNS records
- this is used by authoritative people to indicate how long this can be cached at resolver server , to have faster response to domain query.

### R53 Public Hosted Zones
- A public hosted zone is a container that holds information about how you want to route traffic on the internet for a specific domain which is accessible from the public internet.
- A R53 hosted zone is a DNS DB (zone file) for a domain eg: animals4life.org
- These records in DB are referenced via delegation using name server records.
- Globally resilient (means highly reliable and available) (multiple DNS servers)
- created with domain registration via R53 - can be created seperately
- Host DNS record (eg: A, AAAA, MX, NS, TXT ...)
- Hosted zone are what DNS system references -- Authoritative for a domain eg: animals4life.org
- Hosted on "4" R53 NS specific for the zone and use "NS record" to point at these NS (connect to global DNS)
- Resource records (RR) created within Hosted Zone
- you can even import zonefile for externally registered domains (GoDaddy) and can point at R53 public zone
- VPC instances are already configured (if enabled) with the VPC +2 address as their DNS resolver - this allow querying of R53 public and internet hosted DNS zones.

### R53 Private Hosted Zone
- A private hosted zone is a container that holds information about how you want Amazon Route 53 to respond to DNS queries for a domain and its subdomains within one or more VPCs that you create with the Amazon VPC service
- Its only accessible in those VPCs with which its associated
- you can associate private hosted zone with VPCs in your account using UI/CLI/API but in different account if you use CLI/API only.
- split-view (overlapping public & private) for public and internal use with the same zone name

### **exam imp** CNAME vs R53 Alias
- "A" record maps a NAME to an IP address
- On the other hand, CNAME maps a NAME to another NAME
- but the problem is, CNAME can't be used for apex/naked domain name. (example, catagram.io). meaning www.catagram.io can't be mapped to catagram.io name.
- its also a problem with many AWS services which provides DNS names and not IP addresses, example ELB
- with just CNAME -- ELB wouldn't be able to configured
- This problem is solved by Alias records
- Alias records map a name to an AWS resource
- Also, Alias can be used both for naked/apex and normal records
- There is no charge for Alias requests pointing at AWS resources
- for AWS services - default to picking Alias
- Alias is a subtype, the Alias can of "A" record type alias or "CNAME" record type Alias.
- Hence, for most of the AWS services we use Alias records, like API Gateway, Cloudfront, ELB, Elastic Beanstalk, Global Accelerator, & S3.

### R53 Simple Routing
- Simple routing lets you configure standard DNS records, with no special Route 53 routing such as weighted or latency. 
- With simple routing, you typically route traffic to a single resource, for example, to a web server for your website.
- Use simple routing when you want to route requests towards one service such as a web server
- Simple routing doesn't support health checks - all values are returned for a record when queried.

### R53 Health Checks
- Amazon Route 53 health checks monitor the health and performance of your web applications, web servers, and other resources. Each health check that you create can monitor one of the following:
  - The health of a specified resource, such as a web server
  - The status of other health checks
  - The status of an Amazon CloudWatch alarm
- Health checks are seperate from records, but are used by records
- health checkers are located globally
- with health checkers you can check anything that is accessible over the internet, its not limited to AWS
- by default, health checkers check every 30 sec (but every 10sec costs extra)
- checks can be TCP, HTTP/HTTPS, HTTP/HTTPS with string matching
- status can be Healthy or unhealthy
- These checks can be endpoint checks, cloudwatch alarm check or calculated checks (meaning, checks status of other health checks). 
- Cloudwatch alarm checks are for what happens when you checks fails... you want some SNS events or perform some specific tasks based on checks,

### Failover Routing
- Failover routing lets you route traffic to a resource when the resource is healthy or to a different resource when the first resource is unhealthy
- If the target of the health check is 'Healthy' the primary record is used
- If the target of the health check is 'Unhealthy'.. any queries return the secondary record of the same name
- **exam imp** use this when you want to configure active/passive failover. (primary/secondary failover)

### Multi-value routing
- Multivalue answer routing lets you configure Amazon Route 53 to return multiple values, such as IP addresses for your web servers, in response to DNS queries.
- You can specify multiple values for almost any record, but multivalue answer routing also lets you check the health of each resource, so Route 53 returns only values for healthy resources.
- its a middle-way between simple and failover routing technique
- **exam imp** - multi-value routing improves availability. It is Not a replacement for load balancing.

### R53 weighted Routing
- Weighted routing lets you associate multiple resources with a single domain name (catagram.io) and choose how much traffic is routed to each resource. 
- **exam imp** - This can be useful for a variety of purposes, **including load balancing and testing new versions of software**.
- A '0' weight means a record is never returned unless all are '0' then all are considered.
- if a chosen record is Unhealthy, the process of selection is repeated until a healthy record is chosen.

### Latency Rounting
- If your application is hosted in multiple AWS Regions, you can improve performance for your users by serving their requests from the AWS Region that provides the lowest latency and healthy.
- **exam imp** Use this when optimising for performance & user experience
- AWS maintains a database of latency between the users general location and the regions tagged in records
- latency-based routing supports one record with same name in each AWS region

### Geolocation routing
- lets you choose the resources that serve your traffic based on the geographic location of your users, meaning the location that DNS queries originate from. 
- **exam imp** It doesn't return "closest" records, only relevant (location) records.
- An IP check verifies the location of the user (normally the resolver)
- Either "US state", "country", "continent" or "default" or "no answer"
- **exam imp** 
- can be used for regional restrictions, language specific content, or load balancing across regional endpoints

### Geoproximity Routing
- Geoproximity routing lets Amazon Route 53 route traffic to your resources based on the geographic location of your users and your resources.
- You can also optionally choose to route more traffic or less to a given resource by specifying a value, known as a bias. 
- A bias expands or shrinks the size of the geographic region from which traffic is routed to a resource.
- the difference between this and latency based is distance vs time
- in this it returns based on distance using lat & long co-ordinates, but latency it depends on time
- Routing is distance based (including bias). Meaning, "+" or "-" bias can be added to rules. "+" increases a region size and decreases neighbouring regions.

### R53 Interoperability
- R53 normally has 2 jobs - domain registrar and domain hosting
- R53 can do both or either Domain registrar or domain hosting
- R53 accepts your money (domain registration fee)
- R53 allocates 4 name servers (NS) (domain hosting)
- R53 creates a zone file (domain hosting) on the above NS
- R53 communicates with the registry of the TLD (Domain Registrar)
- ... sets the NS records for the domain to point at the 4 NS above
- Registration fee, domain name and 4 x NS provided to registry.











