# AWS Organization
- benefits for businesses managing larger numbers of AWS Accounts.
- Enterprize should have only one master or standard account and can have zero or more member accounts.
- At initial step first we create Master account and then we invite or create other AWS accounts to become member of organization.
- Consolidated billing - payer account, master account, standard account, all member account bills comes to this consolidated bill.
- Consolidation of reservations and volume discounts
- We can also create a hierarchical structure of these accounts to make it more easily managable. These various accounts can be group together.
- This concept brings few key terms
  - Organization Root --> 
    - its just a container for AWS accounts, which exist at the top of this hierarchical structure. 
    - This is not AWS account root user. its just container in AWS Organizations.
    - it can contain other AWS accounts (members) or other Organizational Units.
  - Organization Units (OU) --> 
    - it can contain other AWS accounts (members) or other Organizational Units.
- you can create new AWS account with-in the organization. Just need a unique email address for this and invition to that email.

### Service Control Policies (SCP)
- a feature of AWS Organizations which allow restrictions to be placed on MEMBER accounts in the form of boundaries.
- SCPs can be applied to the organization, to OU's or to individual accounts.
- Member accounts can be affected, the MANAGEMENT account cannot.
- SCPs DON'T GIVE permission - they just control what an account CAN and CANNOT grant via identity policies.
- One exception for management account - even if SCP is attached to Management Account (master), its never affected by the SCP. It has all permissions for Organizational effects. 
- So, management account can't be restricted by SCP.
- SCPs are account permission boundaries
- They limit what the account (including account root user) can do. Since SCP limits the boundry of account, it indirectly affecting root user limit as well.
- SCP don't grant any permissions, for that we use IAM. SCP just limits the boundry of account.
- SCP establish which permissions can be granted by IAM.
- 
