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
