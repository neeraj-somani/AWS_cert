# Elastic Compute Cloud or EC2

- EC2 is AWS's implement of IAAS - Infrastructure as a service.
- It allows you to provision virtual machines known as instances with resources you select and an operating system of your choosing.

### EC2 Key facts & Features
- IAAS - provides Virtual Machines => Instances
- an instance is just an operating system, configured in a certain way with a certain set of allocated resources.
- Private service by default -- uses VPC networking
- if you want to allow public access to this private EC2 instance then VPC should also support that part
- AZ resilient - instance fails if AZ fails
- different instance sizes and capabilities
- (by default) On-demand billing - per second
- EC2 can use various storage mechanism, most commonly 2, local on-host storage or EBS

### Instance lifecycle
- Instance state - The state of instance indicates its current condition. example, power-on or power-off.
- few states --> Running, Stopped, Terminated
- once a instance is terminated, this action can no longer be reverted.
- **exam imp** -- stopped instance still incur charges for EBS.

### Amazon Machine Image (AMI) 
- it can be created from an EC2 instance and 
- It can also get created based on an instance
- An AMI is very similar to server image used to create VM
- or USB device, which is used to install OS
- An AMI contains attached permissions, which defines who can access and who can't
- An AMI can be public or owner (implicit allow) or explicit (speific AWS accounts allowed)
- An AMI contains boot volume of the instance, ROOT Volume, its the drive that boots the OS
- An AMI can also have other volumes but atleast one boot volume
- It also provides, Block Device Mapping - its a configuration which links the volumes that are attached to AMIs and connected to OS.

### EC2 status Checks
- 2 types - System status check and Instance status check
- system status check -- make sure the traffic can reach the hardware that instance is running on. This check does not validate that your OS and applications are accepting traffic. This check verifies that your instance is reachable.
- Instance status check -- It verifies that instance OS is accepting traffic. in-case of issue, reboot should or OS configuration check can resolve the issue.

### Security Groups 
- can be considered as Mini firewall
- SG attached to Network Interfaces of anything that goes inside VPC.
- on SG can be attached to one or more instances


