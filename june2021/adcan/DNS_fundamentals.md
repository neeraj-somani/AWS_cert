# DNS Fundamentals (Domain Name System)
- DNS is probably one of the most important distributed databases which exist today.
- It is used for service discovery, configuration and the operation of most consumer web browsing and other internet activities.
- DNS is a Discovery service, its how systems are discovered on the internet and even in private networks.
- Translates machine into human and vice-versa
- example, www.amazon.com => 104.98.34.131
- Its a huge and has to be distributed
- needs to manage billions of IPv4s
- can't even image the situation in case of IPv6s

DNS Client - your laptop, phone, tablet, PC
DNS resolver - software on your device, or a server which queries DNS on your behalf
DNS Zone - A part of the DNS database (eg - amazon.com)
Zonefile - Physical database for a zone
Nameserver - where zonefile are hosted
DNS root -
  - its a last "." dot in the domain name "www.amazon.com."


### Lesson Links
- IANA : https://www.iana.org

- Root hints : https://www.internic.net/domain/named.root
  - config points at the root servers IPs and address

- Root Servers : https://www.iana.org/domains/root/servers
  - hosts the DNS root zone

- Root Zone Database : https://www.iana.org/domains/root/db
  - generic top level domain (.com, .org)

- Root Zone File : https://www.internic.net/domain/root.zone

- Delegation Record for .com : https://www.iana.org/domains/root/db/com.html

- gTLD - generic top level domain (.com, .org)

- ccTLD - country-code top level domain (.uk, .eu, etc)
