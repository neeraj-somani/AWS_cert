# AWS Organization - https://aws.amazon.com/organizations/getting-started/
- allows you to manage multiple AWS accounts at once
- With Organizations, you can create groups of accounts and then apply policies to those groups.
- Centrally Manage Policies Across Multiple AWS Accounts
- Control Access To AWS Services
  - create Service Control Policies (SCPs) that centrally control AWS service use across multiple AWS accounts
  - Apply service control policies (SCPs) to users, accounts, or OUs to control access to AWS resources, services, and Regions within your organization.
  - You can specifically Allow or Deny individual AWS Services
  - SCP will override any IAM permissions
- Automate AWS Account Creation And Management
  - use the AWS Organizations APIs to automate the creation and management of new AWS accounts
- Consolidate Billing Across Multiple AWS Accounts
  - set up a single payment method for all the AWS accounts in your organization through consolidated billing
  - take advantage of pricing benefits from aggregated usage, such as volume discounts for Amazon EC2 and Amazon S3.
- AWS Resource Access Manager (RAM)
  - Share AWS resources across your organization using AWS Resource Access Manager (RAM)

### Notes:-
- Once you created organization, you can create account or invite an existing account

