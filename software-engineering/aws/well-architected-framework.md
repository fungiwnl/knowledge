# Well Architected Framwork

General Guiding Principles

- Stop guesing your capacity needs
- Test systems at production scale
- Automate to make architectural experimentation easier
- Allow for evolutionary architectures 
   - Design based on changing requirements
- Drive architectures using data
- Improve through game days
  - Simulate applications for flash sale days

## Well Architeted Framework 5 Pillars

- 1) Operational Excellence
- 2) Security
- 3) Realiability
- 4) Performance Efficiency
- 5) Cost Optimization

- They are not something to balance, or trade-offs, they're a synergy

## Also ask questions

- Look into the Well-Architected Tool
- https://console.aws.amazon.com/wellarchitected

### Practical

- Define a workload

## 1) Operational Excellence

- Includes the ability to run and monitor systems to deliver business value and to continually improve supporting processes and procedures
- Design Principles:
  - Person operations as code - Infrastructure as code
  - Annotate documentation - Automate the creation of annotated documentation after every build
  - Make frequent, small, reversible changes - So that in case of any failure, you can reverse it
  - Refine operations procedures frequently - And ensure that team members are familiar with it
  - Anticipate failure
  - Learn from all operational failures

### Operational Excellence -  AWS Services

Some examples of services (not inclusive) that drives operational excellence

- Prepare
   - AWS Cloudformation
   - AWS Config (to evaluate compliance of CF templates)
- Operate
   - AWS Cloudformation
   - AWS Config
   - AWS CloudTrail 
   - AWS CloudWatch (to monitor performance over time of your stack)
   - AWS X-Ray (trace https requests to make sure they're working correctly)
- Evolve
   - AWS Cloudfromation
   - AWS CodeBuild (CI/CD tools)
   - AWS CodeCommit
   - AWS CodeDeploy
   - AWS CodePipeline

## 2) Security

- Includes the ability to protect info, systems, and assets while delivering business value through risk assessment and mitigation strategies (you're minising risk over time, and save cost of disasters)
- Design Principles
   - Implement a strong identity foundation - Centralize priviledge management an dreduce (or even eliminate) reliance on long-term creds
   - Enable traceability - Integrate logs and metrics with systems to automatically respond and take action
   - Apply security at all layers - Like edge network, VPC, subnet, load balancer, every instance, operating system and application
   - Automate security best practices
   - Protect data in transit and at reset - Encryption, tokenization and access control
   - Keep people away from data -  Reduce or eliminate the need for direct access or manual processing of data
   - Prepare for security events - Run incident response simulations and use tools with automation to increase your speed for detection, 
     investigation and recovery

### Security AWS Services Examples

- Identity and Access management (IAM, AWS-STS, MFA tokens, AWS Organizations)
- Detective Controls (AWS Config, AWS CloudTrail, Amazon CloudWatch)
- Infrastructure Protection (Amazon CloudFront, Amazon VPC, AWS Shield, AWS WAF, Amazon Inspector)
- Data Protection (KMS, S3, ELB, EBS, RDS)
- Incident Response (IAM, AWS Cloudformation, Amazon Cloudwatch Events)

## 3) Reliability

- Ability of a system to recover from infrastructure or serviec disruptions, dynamically acquire computing resources to meet demand, and mitigate disruptions such as misconfigurations or transient network issues

- Design Principles:
   - Test recovery procedures - Use automation to simulate different failures or to recreate scenarios that led to failures before
   - Automatically recover from failure - Anticipate and remediate failures before they occur
   - Scale horizontally to increase aggregate system availability - Distribute requests across multiple- smaller resources to ensure that they dont share a common point of dailure
   - Stop guessing capapcity - Maintain the optimal level to satisfy demand without over or under provisioning - Use auto scaling
   - Manage change in automation - Use automation to make changes to infrastructure

### Relaibility AWS Service Examples

- Foundations (IAM, Amazon VPC, Service Limits, AWS Trusted Advisors)
   - IAM make sure no one has too many rights to wreck havoc
   - Amazon VPC
   - Service Limits set appropriate ones and monitor over time to not get any service disruptions
   - Trusted Advisor
- Change Management
   - Auto scaling if application gets more popular over time and dont have to change anything
   - AWS CloudTrail are we secure enough to track our API calls
   - CloudWatch to look at metrics 
   - Config
- Failure management
   - Backups to make sure application can be recovered if something bad happens
   - Cloudformation to recreate whole infrastructure at once
   - Amazon S3 for backups
   - Amazon S# Glacier
   - Route 53 change route to point to another stack

## 4) Performance Efficiency

- Includes the ability to use computing resources efficiently to meet system requirements and to maintain that efficency as demand changes and technologies evolve

- Design Principles:
  - Democratize advanced technologies - Advance technologies become servies and hence you can focus more on product development
  - Go global in minutes - Easy deployment in multiple regions
  - Use serverless architectures - Avoid burden of managing servers
  - Experiemnt more often, Easy to carry out comparitive testing
  - Mechnical sympathy - Be aware of all AWS services

### Performance Efficiency AWS Services Examples

- **Selection** 
  - AWS Auto scaling
  - AWS Lambda
  - EBS
  - S3
  - RDS
- **Review**
  - CloudFormation
  - AWS News Blog
- **Monitoring**
  - CloudWatch
  - Lambda
- **Tradeoffs**
  - RDS
  - ElastiCache
  - Snowball
  - CloudFront

## 5) Cost Optimization

- Includes the ability to run systems to deliver business value at the lowest price point
- Design Principles
   - Adopt a consumption mode - Pay only for what you use
   - Measure overall efficiency - Use CloudWatch
   - Stop spending money on data center operations - AWS does the infra part and enables customer to foucs on organization projects
   - Analyze and attribute expenditure - Accurate identification of system usage and costs, helps measure return on investment (ROI) 
     to Make sure to use tags
   - Use managed and application level services to reduce cost of ownership - As managed services operate at cloud scale, they can offer
    lower cost per transaction or service

### Cost Optimization Services Examples

- Expenditure Awarness
   - AWS Budgets
   - AWS Cost And Usage Report
   - AWS Cost Explorer
   - Reserved Instance Reporting
- Cost Effective Resources
  - Spot Instance
  - Reserved Instance
  - S3 Glacier
- Matching supply and demand
  - Auto scaling
  - Lambda
- Optimizing Over Time
  - Trusted Advisor
  - Cost and Usage Report
  - AWS News Blog
