# Simple Systems Manager (SSM)
- Its a product that lets you view, manage and control AWS and on-premises infrastructure.
- Its a systems management solution.
- Its an agent based product that needs to be installed on servers and instances.
- It can manage inventory and patch assets
  - example, what applications are installed, the files on the instance, the network config, OS patches and host fixes, instance hardware details, services running on machine, and even custom things can be configured to collect.
  - Maintaince windows can be defined for patches
  - can also run commands
  - can also manage the desired state of instances
    - block certain ports on firewalls 
- It can even use parameter store to store config info and secrets. But AWS recommends Secrets manager service for that now-a-days.
- Session manager -- allows to securely connect to EC2.. even in private VPCs
  - as long as instance has connectivity to systems manager endpoint


### AWS Systems Manager Parameter Store
- The SSM Parameter store is a service which is part of Systems Manager which allows the storage and retrieval of parameters - string, stringlist or secure string.
- The service supports encryption which integrates with KMS, versioning and can be secured using IAM.
- The service integrates natively with many AWS services - and can be accessed using the CLI/APIs from anywhere with access to the AWS Public Spare Endpoints.
- Storage for configuration & secrets
- String, StringList, & SecureString
- License codes, Database Strings, Full configs & passwords
- Hierarchies & versioning
- plaintext and ciphertext
- public parameters - latest AMIs per region
- changes can create events..

### Example when SSM parameter store is preferable compared to AWS Secret manager
- if you need to store hierarchical configuration info
- or configuration for cloudwatch agent,
- and some encrypted strings
- then SSM parameter store is better choice

- But if you just want to store secrets 
- and get automatically rotated
- and product integration is possible
- then AWS secrete manager is better choice

### Systems Manager Run Command
- **exam imp**
- Systems Manager Run Command is a foundational feature of Systems manager which allows for commands to be executed on managed instances at scale
- It uses command documents which define WHAT is executed https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-ssm-docs.html
- **exam imp** Run 'Command documents' on managed instances
- **exam imp** No SSH/RDP Access Required to run commands
- 'Command documents' can be executed based on instances, tags or resource groups
- **exam imp** 'Command documents' can be reused & can have parameters
- you can even define Rate control - meaning concurrency & error threshold
  - here concurrency means, how many instances run at once 
- output of these commands can be sent to S3, SNS, SQS, etc
- Even EventBridge can also be used to connect multiple events with these commands

### SSM Documents
- An AWS Systems Manager document (SSM document) defines the actions that Systems Manager performs on your managed instances. Systems Manager includes more than 100 pre-configured documents that you can use by specifying parameters at runtime. Documents use JavaScript Object Notation (JSON) or YAML, and they include steps and parameters that you specify.
- JSON or YAML documents
- stored in the SSM documents store
- ask for parameter and include steps
- command document - Run command, State manager, & maintainance windows
- Automation Document - Automation, State Manager & maintainance windows
- package document - Distributor

### SSM Patch Manager
- It allows you to patch windows or linux based instances
- patch baseline -- it defines what should be installed, what patches and what hot fixes.
- patch groups - defines groups of resource within systems manager
  - AWS-RunPatchbaseline runs with a baseline and targets to patch the machines inside patch groups
- maintainance windows -- time slots when patching can take place, other tasks of patch manager
  - defines a schedule, duration, targets and tasks 
- Run command - its a base level functionality to manage the patching process
- Concurrency -- defines number of managed instance that can be patched at a given time
- Error Threshold -- defines number of errors that can occur before the whole patching process stops
- compliance -- its a checks that make sure patches are applied successfully or not
- **exam imp** key terms
  - predefined patch baselines --- Various OS (you can also create your own)
  - examples
    - for linux -- AWS-[OS]DefaultPatchBatchline, explicitly define patches
      - example, -- AWS-AmazonLinux2DefaultPatchBaseline
      - example, -- AWS-UbuntuDefaultPatchBaseline
    - Windows -- AWS-DefaultPatchBaseline - Critical and Security Updates
    - AWS-WindowsPredefinedPatchBaseline-OS -- Same as above
    - for Microsoft related apps and windows OS
      - AWS-WindowsPredefinedPatchBaseline-OS-Applications - + MS App Updates
      -  







