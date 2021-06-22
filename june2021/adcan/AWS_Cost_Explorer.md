# AWS Cost Explorer
- Cost Explorer is a tool that enables you to view and analyze your costs and usage.
- You can explore your usage and costs using the main graph, the Cost Explorer cost and usage reports, or the Cost Explorer RI reports.
- You can view data for up to the last 12 months, forecast how much you're likely to spend for the next 12 months, and get recommendations for what Reserved Instances to purchase. 
- You can use Cost Explorer to identify areas that need further inquiry and see trends that you can use to understand your costs.

**Exam points**
- any question that says to explore the cost of AWS account or aws organizations
- or ask for individual users on that account
- or even evaluate a reserved instances would be beneficial for the account or not
- then cost explorer could be right answer
- forcast is also possible
- Its also able to perform cost anomaly detection
- and Rightsizing recommendations

### AWS Cost Allocation Tags
- AWS provides two types of cost allocation tags, an AWS generated tags and user-defined tags. 
- AWS defines, creates, and applies the AWS generated tags for you,
- you define, create, and apply user-defined tags. 
- You must activate both types of tags separately before they can appear in Cost Explorer or on a cost allocation report.
- This needs to be enabled individually
- either per account for standard accounts or ORG master for ORGs (organization)

### Example of tags **--imp for exam--**
- AWS Generated - eg: aws:createdBy or AWS:cloudformation:stack-name
- These are also added to resources after they are enabled by AWS
- User-defined tags can also be enabled user:something
- Both are visible in cost reports and can be used as a filter
- can take upto 24 hours to be visible and active ..

