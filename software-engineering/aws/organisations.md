# Organistions

- Global service

- Allows to manage multiple AWS accounts

- The main account is the master account, which you cannot change

- Other accounts are member accounts

- Member accoutns can only be part of one org

- Consolidated billing across all accounts - single payment method

- Pricing benefits from agregated usage (volume discount for EC2, S3...)

- API is available to automate AWS account creation

  

## Multi Account Strategies

- Create accounts per department, per cost center, per dev / test / prod based on regulatory restrictions (using SCP),
 for better resource isolation, to have seperate per-account service limits, isolated accoutn for logging
- Multi Account vs One Account Multi VPC
- Use tagging standards for billing purposes
- Enable CloudTrail on all acounts, send logs to central S3 account
- Send CloudWatch Logs to central loggin account
- Establish Cross Acount Roles for Admin purposes

### Organisation Units (OU) Examples

- Business Unit 

- Environmental Lifecycle

- Project based



### Organisation



## Service Control Policies (SCP)

- Whitelist or blacklist IAm actions
- Applied at the **OU** or **Acount** level
- Does not apply to the Master Account
- SCP is applied to all the **Users** and **Roles** of the Account, including Root
- The SCP does not affect service-linked roles
   - Service linked role enabled other AWS services to integrate with AWS orgs and can't be restricted by SCPs
- SCP must have an explicit Allow (does not allow anything by default)
- Use cases
  - Restrict access to certain services (for example: can't use EMR)
  - Enforce PCI compliance by explicitly disabling services



### SCP Hierachy examples

Blacklist 

```yml
{    
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyAccessToASpecificRole",
      "Effect": "Deny",
      "Action": [
        "iam:AttachRolePolicy",
        "iam:DeleteRole",
        "iam:DeleteRolePermissionsBoundary",
        "iam:DeleteRolePolicy",
        "iam:DetachRolePolicy",
        "iam:PutRolePermissionsBoundary",
        "iam:PutRolePolicy",
        "iam:UpdateAssumeRolePolicy",
        "iam:UpdateRole",
        "iam:UpdateRoleDescription"
      ],
      "Resource": [
        "arn:aws:iam::*:role/name-of-role-to-deny"
      ]
    }
  ]
}
```

Whitelist

```yml
{    
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowEC2AndCloudwatch",
      "Effect": "Allow",
      "Action": [
        "ec2:*"
        "cloudwatch:*
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```



## Moving accounts

- To migrate accounts from one org to another

  1. Remove the member account from the old org

  2. Send an invite to the new org

  3. Accept the invite to the new org from the member account

     

- If you want the master account of the old org to also join the new org:

  1. Remove the member accounts from the org using steps above

  2. Delete the old org

  3. Repeat the process above to invite the old master account to the new org

 
