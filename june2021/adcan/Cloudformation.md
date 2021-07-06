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




