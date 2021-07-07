# Cloudformation

- CloudFormation is an Infrastructure as Code (IaC) product in AWS which allows automation infrastructure creation, update and deletion.
- Templates created in YAML or JSON can be used to automate infrastructure operations
- Templates are used to create stacks, which are used to interact with resources in an AWS account.
- one template can create one or more stack
- 

### Template sections - (V-DM-PM-CTRO)
- (no limit on number of template creation) 
- this template can have various optional sections, but "Resources" section is compulsory
  - format version --> 
    - its the template version 
    - if this is used then description is compulsory as well.
  - description --> 
    - a string that describes about template, 
    - its must follow format version
  - metadata --> 
    - additional details about the template that can help in template authentication purpose.
    - It generally used to define how you want UI to present the template in console UI
    - example, you can specify the grouping, you can control the order, add descriptions and labels
    - few other advanced features discussed later
  - parameters --> 
    - values to pass to your template at run-time when create or update stack, 
    - (variables in template, User prompted for values to enter at run-time, 
    - example- key-pair, instance type, password values, etc). 
    - You can refer to parameters from the Resources and Outputs sections of the template.
  - mapping --> 
    - behaves similar to lookup table
    - match a provided key to a set of named values 
    - {Example:- AMIs by region, Fn::FindInMap intrinsic function can be used to get details)
  - conditions --> 
    - (intrinsic functions) statements that determine when resources are created or properties are defined using logical operator (example, Env= prod, )
  - Transform --> 
    - For serverless applications (also referred to as Lambda-based applications), 
    - specifies the version of the AWS Serverless Application Model (AWS SAM) to use. 
    - When you specify a transform, you can use AWS SAM syntax to declare resources in your template. 
    - The model defines the syntax that you can use and how it is processed.
  - Resources --> AWS resources details and there properties (example: EC2 instance, S3 bucket)
  - Outputs --> 
    - output values that can be imported to other stacks, return in the response, 
    - can be viewed at cloudFormation console. 
    - (example:- “aws cloudformation describe-stacks” AWS CLI command can be used to see these details)
 
 ### Imp links
 - [CloudFormation Resource Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html)

### exam questions
- What is cloudformation logical resource and physical resource
- CloudFormation defines logical resources within templates (using YAML or JSON).
- The logical resource defines the WHAT, and leaves the HOW up to the CFN product. 
- A CFN stack creates a physical resource for every logical resource - updating or deleting them as a template changes.

### Template Parameters and Pseudo Parameters
- Template and Pseudo Parameters are two methods to provide input to a template, which can influence what resources are provisioned, and the configuration of those resources.
- Pseudo Parameters : https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/pseudo-parameter-reference.html
- Template parameters accept input - console/CLI/API
- parameters can be referenced from within logical resources
- it also influence physical resources and/or configuration
- **exam imp** can be configured with Defaults, allowedValues, Min and Max length & allowedPatterns, NoEcho & Type (string, number, list)
- Pseudo parameters
  - these are injected by AWS into the template at the time of creating stack from template, these are account and region specific.
  - You don't specify these inside the template
  - example, "aws::region" -- this always injected by default by AWS
  - Hence, "aws::region" will always reflect the region is being created in. "aws::stackName" and "aws::stackid" will match the specific stack being created and "aws::accountid" will be set by AWS to the actual accountID the stack is being created within.

###  Intrinsic Functions
- AWS CloudFormation provides several built-in functions that help you manage your stacks. Use intrinsic functions in your templates to assign values to properties that are not available until runtime.
- https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html
- physical attributes can be referenced in the template. The attributes depends on the resource type.
- !Ref Instance -- using !Ref on template or pseudo parameters returns their value. When used with logical resources - the physical ID is usually returned.
- !GetAtt LogicalResource.Attribute -- GetAtt can be used to retrieve any attribute associated with the resource. Most logical resources return detailed configuration of the physical resource.
- !select function returns an object from a list of objects. List starts with index 0.
- !GetAZs -- returns a list of AZs in the explicit region, or the current region.

### Cloudformation Mapping
- The optional Mappings section matches a key to a corresponding set of named values.
- For example, if you want to set values based on a region, you can create a mapping that uses the region name as a key and contains the values you want to specify for each specific region. 
- You use the Fn::FindInMap intrinsic function to retrieve values in a map.
- Template can contain a mapping object
- which can contain many mappings
- which map keys to values, allowing lookup
- can have one key, or Top & second level
- Common use... retrieve AMI for a given region & architecture
- **exam imp** Improve Template portability
- because, it allows you to design how the template should behave for a given input.

### Cloudformation Outputs
- The optional Outputs section declares output values that you can import into other stacks (to create cross-stack references), return in response (to describe stack calls), or view on the AWS CloudFormation console. 
- For example, you can output the S3 bucket name for a stack to make the bucket easier to find.

### CloudFormation Conditions
- The optional Conditions section contains statements that define the circumstances under which entities are created or configured.
- You might use conditions when you want to reuse a template that can create resources in different contexts, such as a test environment versus a production environment
-  In your template, you can add an EnvironmentType input parameter, which accepts either prod or test as inputs. Conditions are evaluated based on predefined pseudo parameters or input parameter values that you specify when you create or update a stack.
-  Within each condition, you can reference another condition, a parameter value, or a mapping. After you define all your conditions, you can associate them with resources and resource properties in the Resources and Outputs sections of a template.
-  use the other intrinsic functions AND, EQUALS, IF, NOT, OR
-  conditions can also be nested in a template


### Cloudformation DependsOn
- With the DependsOn attribute you can specify that the creation of a specific resource follows another. 
- When you add a DependsOn attribute to a resource, that resource is created only after the creation of the resource specified in theDependsOn attribute.
- "!Ref" intrinsic function gives only implicit dependency, but "DependsOn" function can give explicit dependency.
- for example, when we want to create an "EIP" for a VPC, it requires IGW should be attached to VPC before EIP attached to IGW.
- Hence, we can achive this by creating implicit dependency between VPC and IGW
- **exam imp** and explicit dependency between EIP and IGW. Hence, EIP will be created after IGW is complete.

### CloudFormation Wait Conditions, creation policy & cfn-signal
- CreationPolicy, WaitConditions and cfn-signal can all be used together to prevent the status if a resource from reaching create complete until AWS CloudFormation receives a specified number of success signals or the timeout period is exceeded.
- The cfn-signal helper script signals AWS CloudFormation to indicate whether Amazon EC2 instances have been successfully created or updated.
- Configure cloudFormation to hold
- wait for 'X' number of success signals
- wait for timeout H:M:S for those signals (12 hour max)
- If success signals received... CREATE_COMPLETE
- If failure signal received .. creation fails
- if timeout is reached.. creation fails
- CreationPolicy or WaitCondition.
- CreationPolicy applies signal requirement (eg: 3) and timeout (eg: 15 min)
- CreationPolicy generally used for creating EC2 instance and for auto-scaling group
- WaitCondition can depend on other resources, or vice versa.
- WaitCondition relies on "WaitHandle", which is another logical resource, whose job is to generate pre-signed URL which can be used to send signals too.
- its pre-signed, hence doesn't need AWS credentials.
- Generally used when you have some external system dependency or resource dependency
- cfn-signal used to send and receive signal between these resources.

### Nested Stack
- Nested stacks allow for a hierarchy of related templates to be combined to form a single product
- A root stack can contain and create nested stacks .. each of which can be passed parameters and provide back outputs.
- Nested stacks should be used when the resources being provisioned share a lifecycle and are related.
- **exam imp** Resources in a **single stack share a lifecycle**. Hence, nested stack can be helpful.
- Also, there is stack resource limits (500). Nested stack can help in this situation as well
- Single stack resources can't be reuse in another stack. Can't easily reference in other stack. Hence, nested stack.
- multi-stack can be done in two ways - nested stack and cross-stack referencing
- Root stack & parent stack -- first stack that gets created.
- When to use this -- When you want to divide your template in a way to re-use it for other purposes. Generic template idea.
- The biggest difference is, we are using stack template in Nested stack and not reusing the resources.
- But in-case of cross-stack referenceing, we reuse resources.

### Cross-stack references 
- Cross stack references allow one stack to reference another
- Outputs in one stack reference logical resources or attributes in that stack
- They can be exported, and then using the **!ImportValue** intrinsic function, referenced from another stack.
- CFN stacks are designed to be isolated and self-contained
- example, you want to use same VPC and launch multiple resources inside the one VPC using various CFN stack.
- Outputs from one stack are normally not visible from other stacks, example, using "!Ref" function
- But nested stack can reference that way
- Outputs can be exported... making them visible from other stacks
- Exports must have a unique name in the region
- **"Fn::ImportValue** function can be used instead of "Ref", to import the exported value from another stack
- export is used to export the output of a stack... to a unique name in that region
- Exports -- per region + per account
- These exported values can be imported in another stack.
- This is mostly used in **service-orientated architecture** and different lifecycles of stack resources, and stack reuse capability

### Stack Sets
- allowing infrastructure to be deployed and managed across multiple regions and multiple accounts from a single location.
- Additionally it adds a dynamic architecture - allowing automatic operations based on accounts being added or removed from the scope of a StackSet.
- stacksets are containers in an admin account..
- contains stack instances ... which reference stacks
- stack instances & stacks are in 'target accounts'
- Each stack == 1 region in 1 account
- security == self-managed or service-managed (using IAM role)
- Concurrent Accounts -- in how many aws accounts these stack gets created concurrently
- Failure Tolerance -- how many resources failed status can be tolerated
- Retain stack -- by default delete stack is on, but you can change the settings to retain stack as and when needed.
- Use-cases and scenarios --
  - Enable AWS config in multi-region, multi-account, like MFA, EIPs, EBS Encryption settings
  - or create IAM roles for cross-account access

### Deletion Policy
- With the DeletionPolicy attribute you can preserve or (in some cases) backup a resource when its stack is deleted. 
- You specify a DeletionPolicy attribute for each resource that you want to control.
- If a resource has no DeletionPolicy attribute, AWS CloudFormation deletes the resource by default.

### Stack Roles
- Stack roles allow an IAM role to be passed into the stack via PassRole
- A stack uses this role, rather than the identity interacting with the stack to create, update and delete AWS resources.
- It allows role separation and is a powerful security feature.
- When you create a stack - CFN creates physical resources
- **exam imp** -- CFN uses the permissions of the logged in identity
- **exam imp** -- which means you need permissions for AWS to create, update and delete AWS resources.
- Hence there are 2 seperate permissions here, one the person who can create stack, second other team or person to update or support them. Example, L1, L2, L3, level support teams etc
- CFN can assume a role to gain the permission
- This lets you implement role seperation
- The identity creating the stack .. doesn't need resource permissions -- only PassRole

### aws::cloudformation::init and cfn-init
- its a tool used to perform some tasks as part of bootstraping process
- CloudFormationInit and cfn-init are tools which allow a desired state "configuration management system" to be implemented within CloudFormation
- Use the AWS::CloudFormation::Init type to include metadata on an Amazon EC2 instance for the cfn-init helper script. 
- If your template calls the cfn-init script, the script looks for resource metadata rooted in the AWS::CloudFormation::Init metadata key. cfn-init supports all metadata types for Linux systems & It supports some metadata types for Windows
- configuration directives stored in template
- UserData Script is procedural, meaning you give step-by-step script to perform tasks, you tell how you want to configure the system
- while, cfn-init is a desired state configuration, you just define what you want, AWS tasks care of how.
- example, different version script compatibility can be easily handled.
- cfn-init helper script - installed on EC2 OS (makes it so)
- In configSets -- we can define which configKeys to use and in which order to apply
- example of configKeys --> packages, groups, users, sources, files, commands, services, etc

### cfn-hub
- The cfn-hup helper is a daemon that detects changes in resource metadata and runs user-specified actions when a change is detected. 
- This allows you to make configuration updates on your running Amazon EC2 instances through the UpdateStack API action.
- cfn-init is run only once as part of bootstrapping (user-data process)
- if cloudformation::init is updated, the part doesn't re-run, even if you restart the instance.
- cfn-hub helper is a daemon which can be installed on EC2 instance
- this can also be used as a bootstraping tool
- UpdateStack API ==> updated config on EC2 instance
- in case of any changes in the config, cfn-hub executes cfn-init, which then applies new configurations
- cfn-hub just checks the metadata periodically

- cfn more complex techniques
- https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-updating-stacks-update-behaviors.html
- **exam imp** -- by default cloudformation has no idea/info about bootstraping process and its status that is running on EC2 instance.
- Hence, signal statement used to notify cfn for such bootstrapping process and its status.
- Userdata
- Userdata + cfn-signal
- cfn-init + cfn-signal
- cfn-init + cfn-signal + cfn-hup


### Cloudformation change-sets
- When you need to update a stack, understanding how your changes will affect running resources before you implement them can help you update stacks with confidence. 
- Change sets allow you to preview how proposed changes to a stack might impact your running resources, for example, whether your changes will delete or replace any critical resources,
- AWS CloudFormation makes the changes to your stack only when you decide to execute the change set, allowing you to decide whether to proceed with your proposed changes or explore other changes by creating another change set.

### Cloudformation Custom Resources
- Custom resources enable you to write custom provisioning logic in templates that AWS CloudFormation runs anytime you create, update (if you changed the custom resource), or delete stacks
- By default, cloudformation doesn't support everything that AWS offers
- custom resources let cfn integrate with anything it doesn't yet or doesn't natively support
- you can even use custom resources to provision non-aws resources, as long as you have all needed permissions
- The process is really simple, passes data to something, gets back data from something
- 










