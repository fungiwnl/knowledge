# Resource Access Manager (RAM)

- Share AWS resources that you own with other AWS accounts
- Share with any account or within your Organisation
- Avoid resource duplication!
- **VPC Subnets**:
  - allow to have all the resoures launched in the same subnets
  - must be from the same AWS Org
  - cannot share security groups and default VPC
  - participants can manage their own resources in there
  - participants can't view, modify, delete resources that belong to other participants or the owner
- **AWS Transit Gateway**
- **Route53 Resolver Rules**
- **Licence Manager Configurations8*

## VPC example

- Insert image
- Each account
   - is responsible for its own resources
   - cannot view, modify or delete resources in other accounts 
