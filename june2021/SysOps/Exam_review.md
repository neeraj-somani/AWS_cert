# Awesome exam review links
- https://acloud.guru/forums/AWS%20Certified%20SysOps%20Administrator%20-%20Associate%20(SOA-C01)/discussion/-MNAuRrPqc32gBOcbBb4/passed_sysops_associate_27~2F11~2F
- Hey everyone,

I took and successfully passed my SysOps associate exam (SOA-C01) yesterday and wanted to provide my thoughts on the exam, preparation I took and recommendations for the content creators of the lecture on ACG.

Exam:

One of my first questions in the exam was one about CloudFormation, and how to troubleshoot a deployment issue.

As I started moving through the other questions, CloudFormation came up a lot, as did Lambda.

These 2 stuck out quite a bit, as they were things that we covered in the course, but not in a great amount of detail.

Lambda especially

Other questions had elements similar to what we had studied:

S3 - Lifecycle management, storage tiers, bucket policies and restricting access (it is covered, but I got stuck on this for a while), data consistency model for PUTs on existing objects (eventual)

AWS Config - Centralising logging to a specific account

CloudTrail - API calls made into different services, one being KMS

EC2 - ALB logging, autoscaling - Scale without impacting current resources (autoscaling came up a lot), 1 question on previous gen M series instances and what to do to improve cost (think it was relaunch so they go onto M5 then use a RI, but there was a trick in the question about replacing the classic LB to an app LB WITH the M2 series instances then do RI). ELB 5XX error code

VPC - Adding CIDR blocks to an existing VPC (You can't modify existing ones (only remove), but you can add new blocks), Limiting internet access while allowing access to S3 (remove NAT GW and add S3 VPC endpoint), IPv6 access (Egresss-only IGW), flow logs to see source\dest of traffic, VPC peering

CloudFormation - Structure of templates, protecting resources from deletion, using AMI in different regions (you use the Mappings section to control this), rollback behaviour, changing existing configuration (change set)

Lambda - Came up a heap, I recommend both study on its settings and also more content in the lectures

Storage Gateway - Improving performance on a Volume gateway when cache metrics CacheHitPercent are high and CacheUsed medium (someone also got this same question and posted on the forums, so I had a bit of an edge here)

CloudWatch - How to troubleshoot if logs aren't being sent (something about agent not running and possibly a 3rd party system taking logs also. Not sure if I got that one right), question about dashboards and how to create a consolidated view (we know its widgets, but remember you need to be in the region where the resource lives)

AWS Organisations - Bringing in existing accounts into a new AWS Organisations structure (invite from the master), restricting apps using SCPs, aggregated billing

Billing - How to track spending via tags (enable cost allocation tags and use cost explorer)

SSM - Session Manager and why engineers cant connect to a Ubuntu instance (the default username had to be changed in the parameters for connecting, as all other answers were wrong), Parameter store

RDS - Redundancy for an RDS DB (Multi-AZ)

EFS - Encrypting an existing EFS FS (can't be done, need to create a new one and encrypt at creation, then move the data)

CloudFront - Improve performance for website for users in Asia, when web servers are in EU (use static content from CloudFront and R53 latency-based routing)

R53 - Routing types

Service Catalog - How to configure the same Service Catalog in one account with another (there were a few options, I think I chose share in the end but not sure if that's right)

Inspector - Vulnerabilities for a system didn't show up, how to troubleshoot? Reset agent as it was already installed

Trusted advisor - Same as Inspector; came up, don't remember question (something about remediation of patches perhaps?)

STS - There was a question about an existing LDAP directory and an IDP using SAML 2.0, and how to grant devs temp access with a sts API call. I selected GetSessionToken as I've done identity management before, which I think was right.

WAF - I think I saw WAF in one question

Shared responsibility model - VPN connection into AWS, what is AWS responsible for? Answer was something about the EC2 host the EC2 instances were running on

Artefact - Mentioning this to understand what it is, as its almost never going to be an answer

Elastic Beanstalk - Maybe came up twice, one for a red herring and one for a solution with minimal downtime for an application

OpsWorks - Saw it once I think, straightforward what it does

What didn't come up that I studied at length:

Elasticache - Didn't even see one

EC2 - EBS, placement groups, Instance-store volumes

Bastion hosts

RDS - Read replicas, Aurora

S3 - MFA delete, enforcing encryption with bucket policies

Snowball

Athena

AWS Shield - DDOS protection

VPC - DirectConnect

My preparation

Right, if you got through all that then kudos.

My preparation was as follows:

1. Watched the lectures on ACG, and took notes on everything

2. Revised notes at least once a month (kept dates of when I last studied particular section). Did this in tandem with step 1; some nights was revision, some nights was watching new lectures.

3. Took practice exam - got 60%

4. From practice exam, learnt my shortcomings so reviewed the documents provided in the practice exam feedback, took notes, and studied these

5. Read a few whitepapers

6. Read many FAQ's, and took notes on things I thought were important that I didn't already know

7. Took practice exam again - Got 77%

8. From practice exam, learnt more shortcomings which I had to review

9. Revised my practice exam notes a bit more

10. Took exam, got 779. Not the greatest score, but it happens (still 1 shot the exam, so I was happy)

Recommendations to ACG

While the lectures were great to get me a pass, as I mentioned above my score could have been better.

I would say we need more thorough content on CloudFormation, Lambda and Service Catalog.

And that's me done, good luck everyone on your own journeys.


## Another one
- https://acloud.guru/forums/AWS%20Certified%20SysOps%20Administrator%20-%20Associate%20(SOA-C01)/discussion/-MDdw8LzSVFGAXMAM_GQ/sysops_admin_course_-_missing
- Hi,

I've passed the SysOps Admin exam yesterday. Below is the list of stuff that is missing in the course based on my Exam. It would be great to update the course to cover that:

Control Tower - question how to setup and govern a new, secure multi-account AWS environment

Session Manager - question on how to login to instance without ssh. This is really cool service from System Manager and honestly you guys should cover this in the course as this is rather an essential service for SysOps in my opinion:

https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html

Autoscaling Lifecycle Hooks - how to protect instances from being removed after being marked unhealthy so that you can investigate the instances before they are being terminated

IAM Access Analyzer: it was one of the answer in a questions but rather as a red herring (still it would be good to know this):
https://aws.amazon.com/about-aws/whats-new/2019/12/introducing-aws-identity-and-access-management-access-analyzer/

Storage gateway performance - there were 2 metrics given (CacheHitPercentage < 60%, CacheUsed Percentage around 90% most of the time). They asked, how to increase the I/O performance of iSCSI (something like that): I remember three answers (change size of volumes from aws console, change block size from 64kb to 128 or 256 or 512kb, create RAID 1.

Raid 1 does not make sense as it will not help increase the I/O performance.

Changing volume size. AWS recommends adding new disks and not changing existing.

"When adding cache or upload buffer to an existing gateway, it is important to create new disks in your host (hypervisor or Amazon EC2 instance). Don't change the size of existing disks if the disks have been previously allocated as either a cache or upload buffer. Do not remove cache disks that have been allocated as cache storage."

Changing block size (that's probably the best option): https://docs.aws.amazon.com/storagegateway/latest/userguide/Performance.html#optimize-iSCSI

"You can optimize iSCSI settings on your iSCSI initiator to achieve higher I/O performance. We recommend choosing 256 KiB for MaxReceiveDataSegmentLength and FirstBurstLength, and 1 MiB for MaxBurstLength. For more information about configuring iSCSI settings, see Customizing iSCSI Settings."

Probably a good idea to look here before sitting the exam:

https://docs.aws.amazon.com/storagegateway/latest/userguide/monitoring-volume-gateway.html
https://docs.aws.amazon.com/storagegateway/latest/userguide/ManagingLocalStorage-common.html
https://docs.aws.amazon.com/storagegateway/latest/userguide/Performance.html

I generally did not expect so many questions on Storage Gateway (I had 5 or so, maybe just a bad luck). I expected more questions on VPC (things like CIDR blocks they did not ask at all). A lot of questions on ALB (logging & monitoring), AWS Budget, AWS Config, CloudTrail, Cost Explorer and AWS Organizations. Quite some questions on System Manager (run command, session manager, inventory, patch manager).

Best

