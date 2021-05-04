# AWS GuardDuty

- IntelligentThreat discovery to Protect AWS Account
- Uses Machine Learning algos, anamoly detectio, 3rd party data
- One click to enable (30 days trial), no need to install software

- Input data includes
  - CloudTrail Logs: unusual API calls, unauthorized deployments
  - VPC Flow Logs: unusual internal traffic, unusual IP address
  - DNS logs: compromised EC2 instances sending encoded data within DNS queries

- Can setup CloudWatch event rules to be notified in case of findings
- CloudWatch Events rules can target AWS Lambda or SNS
- Can protect against CryptoCurrency attacks (has a dedicated 'finding' for it)

## How it works

- [Insert diagram]
