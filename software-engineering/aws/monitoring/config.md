# AWS Config

- Helps with auditing and recording compliance of AWS resources
- Helps record config and changes over time
- Possibility of storing the config data in S3 (analyzed by Athena)
- Questions that can be solved by AWS Config
  - Is there unrestricted SSH access to my security groups?
  - Do my buckets have any public access?
  - How has my ALB config changed over time
- You can receive alerts (SNS notifications) for any changes
- Config is a per region service
- Can be aggregated across regions and accounts

## Config Resource

- View compliance of a resource over time
- View config of a resource over time
- View CloudTrail API calls if enabled
- Can use AWS managed configured ruels (over 75)
- Can make custom config rules (must be defiend in AWS Lambda)
   - Evaluate if each EBS disk in of type gp2
   - Evaluate if each EC2 instance is t2.micro
- Rules can be evaulated / triggered
  - For each config change
  - And / or at regualar time intervals
  - Can trigger CloudWatch Events if the rule is non-compliant and chain with Lambda
- Rules can be auto remeditations
  - If a resource is not compliant and can trigger an auto remediation
  - Eg: stop instances with non-approved tags
- Config rules does not prevent actions from happenning (no deny)
- Pricing: no free tier; $2 per active rule per region per month