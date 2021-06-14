# Identity and Access Management (IAM)
- IAM is what allows additional identities to be created within an AWS account - identities which can be given restricted levels of access.
- IAM identities start with no permissions on an AWS Account, but can be granted permissions (almost) up to those held by the Account Root User.

### 3 major identity components of IAM
- user
- group 
- role
- policies - allow or deny access to AWS

### Major features of IAM
- Manages Identity - a ID provider (IDP)
- Authenticate - prove you are who you claim you to be
- Authorize - Allow or deny access to resources

### Other imp points
- IAM is free
- global service / global resilience
- allow or deny its identities on its AWS account
- No direct control on external accounts or users
- identity federation (google, facebook, amazon)
- MFA


### IAM Access Keys
- Access keys are how the AWS Command Line Tools (CLI Tools) interact with AWS accounts.
- At any given time, one user can have only 2 set of access key at max. It can be either active or inactive, doesn't matter.
- aws CLI setup link -- https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-mac.html
- 
