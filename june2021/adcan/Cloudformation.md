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



### testing
