# AWS Config
- AWS Config is a service which records the configuration of resources over time (configuration items) into configuration histories.
- All the information is stored regionally in an S3 config bucket.
- AWS Config is capable of checking for compliance .. and generating notifications and events based on compliance.
- Configuration Item -- It gets created every time a resource configuration is changes.
- It doesn't prevent changes happening... no protection.
- It can also be configured to capture config details across region. Hence it supports cross-region and account aggregation details.
- Changes can generate SNS notifications and near-realtime events via EventBridge & Lambda.
- All Configuration Items for a given resource is called a configuration history.
- Config Rules - (addional powerful functionality)
  - create config rules and configuration changes evaluated agaist these rules.
  - These rules can be AWS Managed ones or custom (using lambda only as of now).
  - for example, compliance based rules vs non-compliance based rules
- EventBridge can also be intergrated with config. EventBridge can invoke lambda function based on AWS config events for automatic resource remediation.



