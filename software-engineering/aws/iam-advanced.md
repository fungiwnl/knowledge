# IAM Advanced



## IAM Conditions

- Make IAM policies a bit more restrictive based on conditions
- **aws:SourceIP**: restrict the client IP **from** which the API calls are being made 

```
{ 
   "Version": "2012-10-17",
   "Statement": {
       "Effect": "Deny", 
       "Action": "*", 
```

- **aws:RequestedRegion**: restrict the region the API calls are made to 

```
{
  ...
    "Condition": {
      "StringEquals": {
         "aws:RequestedRegion": [
            "eu-central-1", 
            "eu-west-1"
          ]
  }
 }
}
```



### Restrict based on tags

```
{
}
```



### Force MFA

```
{
}
```



## IAM for S3

- ListBucket permissions applies to arn:aws:s3:::test
- => bucket level permission
- GetObject, PutObject, DeleteObject applies to arn:awn:s3:::test/*
- => object level permissions hence trailing star

```
{
}
```



### IAM Roles vs Resource Based Policies

- Attach a policy to a resoruce (example: S3 bucket polcy) versus attaching of a using a role as a proxy

  

- Insert graph

  

- **When you assume a role (user, application or service), you give up your original permissions and take the permissions assigned to the role **

- When using a resource based policy, the principal doesn't have to give up his permissions

- Example**: User account in account A needs to scan DynamoDB table in Account A and dump it in an S3 bucket in Account B

- Supported by S3, SNS, SQS 



## IAM Permission Boundaries

- IAM Permission boundaries are supported for users and roles (not groups)
- Advanced feature to use a managed policy to set the maximum permissions to set the maximum permissions an IAM entity can get 
- Can be used in combinations of AWS organisations SCP
- Use cases: delete responsibilities to non admins within their permissions boundaries for example create new IAM users
- Allow developers to self assign policies and manage their own permissions while making sure they can't escalate their privileges (make themselves admin)
- Useful to restrict one specific user (instead of a whole account using Organisations & SCP)



## IAM Policy Evaulation Logic

- insert image



### Example IAM Policy

```
{
   "Version": "2012-10-17",
   "Statement": [
   {
     "Action": "sqs:*"
   }
   ]
}
```



- Can you perform sqs:CreateQueue?
- Can you eprform sqs: DeleteQueue?
- Can you perform ec2:DescribeInstances? 

