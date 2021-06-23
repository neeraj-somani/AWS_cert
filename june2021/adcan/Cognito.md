# Cognito
- Testing

### SAML (Security Assertion Markup Language)
- Open standard used by many IDP's (Microsft AFDS)
- "Indirectly" use on-premises IDs with AWS (Console and/or CLI)


### SAML2.0 Identity Federation
- It shows how it can be used to allow API and Console UI access using existing SAML 2.0 corporate identities.
**Exam imp**
- It should be use only when Enterprise Identity provider and SAML 2.0 compatible
- or Existing Identity management team
- or you want to use Single source of truth 
- or you have more than 5000 users in an AWS account who needs access
- it uses IAM roles and AWS temporary credentials (with 12 hour validity)
- Its an application initiated process and not user entering details

### SSO - Single Sign-on 
- **Exam imp**
- enables you to manage SSO access and user permissions across all AWS accounts and external applications.
- It provides flexible identity source (stores) - its the place where all identities are centrally stored
- It has various identity stores
  - first - AWS SSO - Built-in identity store
  - second - AWS Managed Microsoft AD
  - third - on-premises microsoft AD (two way trust or AD connector)
  - fourth - External Identity provider - SAML 2.0
- **exam imp** - AWS recommend and preferred AWS SSO for identity federation, instead of traditional 'workforce' identity federation.
- Notice, in exam question, whats the scenario -
  - if its asking about enterprise or workplace identities - the AWS SSO should be preferred service.
  - if its asking about web based customer identities (example, web-application using twitter, facebook, gmail, etc) then cognito should be better option and cognito should be used
- SSO is completely free. There is no charge for using and configuring it.


### other features 
- When you enable AWS SSO, you allow it to create IAM roles for each AWS account in your AWS organization.
- You also allow other AWS accounts within your organization to assign applications access to AWS SSO users.
- The idea is to use SSO, instead of IAM to access AWS accounts.
- A basic requirement for AWS SSO is to have a valid AWS Organization created.
