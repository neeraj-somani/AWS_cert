# AWS secrets manager
- AWS Secrets manager is a product which can manage secrets within AWS.
- There is some overlap between it and the SSM Parameter Store - but Secrets manager is specialised for secrets.
  - In SSM you can create secure strings which allows you to store password securely.
  - The primary focus of secrets manager is to store and rotate these secrets periodically without much efforts.
  - **exam imp** on the other hand secrets manager is designed for secrets like (passwords, API keys, etc)
- **exam imp** Additionally Secrets managed is capable of automatic credential rotation using Lambda.
- **exam imp** For supported services (eg: RDS) it can even adjust the credentials of the service itself. meaning, if secrets manager rotates password inside it and hence that new password can easily be configured to RDS throught direct integration between RDS and secrets manager.
- Usable via console, CLI, API or SDK's. Hence, its easily integrated with other services
- All sercretts are safe and encrypted at rest.
- integrates with IAM permissions.

### Example when SSM parameter store is preferable compared to AWS Secret manager
- if you need to store hierarchical configuration info
- or configuration for cloudwatch agent,
- and some encrypted strings
- then SSM parameter store is better choice

- But if you just want to store secrets 
- and get automatically rotated
- and product integration is possible
- then AWS secrete manager is better choice
