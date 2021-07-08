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







