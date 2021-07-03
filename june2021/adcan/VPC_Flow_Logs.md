# VPC Flow Logs
- This service provides capability to monitore or understand network flow.
- for example, Flow logs captures metadata info like Source/Destination IP, Source/Destination ports, packet size, other externally visible metadata.
- VPC FLow logs is a feature allowing the monitoring of traffic flow to and from interfaces within a VPC
- VPC Flow logs can be added at a VPC, Subnet or Interface level.
- Flow Logs DON'T monitor packet contents ..... that requires a packet sniffer.
- Flow Logs can be stored on S3 or CloudWatch Logs.
- Additional links:
  - https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs-s3.html
  - https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs-cwl.html

### Features
- **exam imp** They only capture packet metadata...... Not packet contents
- Packet content is captured by packet sniffer, that can be configured on an EC2 instance.
- for example, Flow logs captures metadata info like Source/Destination IP, Source/Destination ports, packet size, other externally visible metadata.
- **exam imp** VPC Flow logs are not realtime.
- Since, we can apply flow logs to interfaces, conceptually it can also be applied at RDS instances.

### Flow log file sturcture
- its a collection of fields
- version
- account-id
- interface-id
- **srcaddr**
- **dstaddr**
- **srcport**
- **dstport**
- **protocol**
- packets
- bytes
- start
- end
- **action**
- log-status

### Few limitations/exclusions **exam imp**
- few things that are not recorded by flow logs
- communication to and from 169.254.169.254, 169.254.169.123, DHCP, Amazon DNS server & Amazon Windows license not recorded.
