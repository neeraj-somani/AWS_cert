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
- 
