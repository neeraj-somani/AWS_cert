# Identity and Access Management (IAM)
- IAM is what allows additional identities to be created within an AWS account - identities which can be given restricted levels of access.
- IAM identities start with no permissions on an AWS Account, but can be granted permissions (almost) up to those held by the Account Root User.

### 3 major identity components of IAM
- user
  - identity who requiring AWS access, like humans, applications or service accounts
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

### IAM Identity Policies
- Identity Policies are attached to AWS identities and either ALLOW or DENY access to AWS resources.
- below are few points that are in sequence of priority
  - 1. Explicit DENY
  - 2. Explicit ALLOW
  - 3. Dfault DENY (Implicit)

### ARN (Amazon Resource Name)
- Uniquely identify resources within any AWS accounts
- arn:aws:s3:::catgifs --> refers to the bucket and not the objects in the bucket
- arn:aws:s3:::catgifs/* --> refers to the objects in the bucket, but not the bucket itself.

### Exam Imp
- 5000 IAM Users per account
- IAM User can be a member of 10 groups
- This has systems design impacts
- internet-scale applications
- large orgs & org merges
- IAM roles & Identity Federation fix this (more later)



