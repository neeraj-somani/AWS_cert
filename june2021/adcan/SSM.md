# SSM Parameter Store
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

