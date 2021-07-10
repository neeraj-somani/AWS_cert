# WAF (Web Application Firewall)
- helps protect your web applications or APIs against common web exploits that may affect availability, compromise security, or consume excessive resources. 
- WAF gives you control over how traffic reaches your applications by enabling you to create security rules that block common attack patterns, such as SQL injection or cross-site scripting, and rules that filter out specific traffic patterns you define. 
- https://aws.amazon.com/waf/pricing/
- **exam imp** It supports at Layer 7 (HTTP/HTTPs) firewall
- **exam imp** Protects against complex Layer 7 attacks/exploits
- **exam imp** like, SQL Injections, Cross-site Scripting, Geo Blocks, Rate Awareness
- WAF implemented using WEBACL - web access control list
- This WEBACL can integrate with ALB, API Gateway and cloudfront
- Rules are added to a WEBACL and evaluated when traffic arrives
- These rules are applied and configured using WEBACL capacity Units (WCU)
- WebACL pricing -- per month per ACL, Per Rule per month, per request per month
- WebACL have a default action -- ALLOW or BLOCK
- RULE ACTION can be --- ALLOW, BLOCK, COUNT
- These rules can also be of 2 types
  - Regular Rule
  - Rate-based Rule -- mostly COUNT rate used here for ALLOW or BLOCK rule
- It can create rule for many layer 7 details like
  - IP addresses, Country or GEO location, URL Length, SQL Code, Strings in request, Scripts, headers and more



# AWS Shield
- **exam imp** Its a managed Distributed Denial of Service (DDoS) protection service that safeguards applications running on AWS.
- AWS Shield provides always-on detection and automatic inline mitigations that minimize application downtime and latency, so there is no need to engage AWS Support to benefit from DDoS protection.
- There are two tiers of AWS Shield - Standard and Advanced.
- **exam imp** Shield Standard -- Mostly its free with Route53 and cloudfront services, but doesn't support other AWS services.
- This basically provides protection against Layer 3 and Layer 4 DDOS attacks
- Shield Advanced pricing - $3000 per month per organization
- **exam imp** This Advanced comes with additional features that support many other AWS services like EC2, ELB, cloudfront, Global Accelerator, R53, etc
- **exam imp** Also, Advanced subscription comes with 24 hour support from DDOS response team from AWS and 
- **exam imp** Also, it comes with Financial Insurance for any additional resources utilized as part of DDOS attack.
