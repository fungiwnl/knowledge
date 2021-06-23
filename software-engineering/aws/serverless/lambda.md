# Lambda

- Serverless is a new paradigm which developers don't have to manage servers anymore

- Virtual functions - no servers to manage
- Limited by time - short executions
- Run on-demand
- Scaling is automated

## Benefits of Lambda

- Easy pricing
  - Pay per request and compute time
  - Free tier of 1,000,000 AWS Lambda requests and 400,000 GBs of compute time

- Integrate with the whole AWS suite
- Integrated with many programming languages
- Easy monitoring through AWS CloudWatch
- Easy to get more resources (up to 3GB of RAM)
- Increasing RAM will also improve CPU and network

## Language support

- Node.js (Javascript)
- Python
- Java
- C#
- Golang
- C# / Powershell
- Ruby
- Custom runtime API (community supported, eg Rust)

- Docker is not for AWS lambda it's for ECS/Fargate

## Lambda Integrations (main ones)

- API Gateway
- Kinesis
- DynamoDB
- S3
- Cloudfront
- CloudWatch Events EventBridge
- CloudWatch Logs
- SNS
- SQS
- Cognito

## Example: Serverless CRON job

- Create CloudWatch event rule
- Trigger Lambda function to perform a task

## Example: Serverless thumbnail creation

- New image in S3 bucket
- Trigger Lambda function to create thumbnail 
- Push to new S3 bucket
- Push metadata to DynamoDB

## Pricing

- Pay per calls 
  - First 1,000,000 requeests are free
  - $0.20 per 1 mil requests thereafter

- Pay per duration 
  - 400,000 GB-seconds of compute time per month if FREE
  - == 400,000 seconds if function is 1GB RAM
  - == 3,200,000 seconds if function is 128MB RAM
  - After $1,00 for 600,00 0 GB-seconds

- It is usually very cheap to run AWS Lambda so it's very popular

## Limits

- Execution:
   - Memory allocation: 128MB - 3008MB (64 MB increments)
   - Maximum execution time: 900 seconds (15 mins)
   - Environmetnal variable (4kb)
   - Disk capacity in the function container in (/tmp): 512MB
   - Concurrency executions: 1000 (can be increased)

- Deployment:
   - Lambda function deployment seize (compressed .zip): 50MB
   - Size of uncompressed deployment (code + dependencies): 250MB
   - Can use the /tmp directory to load other files at startup
   - Size of environmetn variables 4kb

## Lambda@Edge

- You have deployed a CDN using CloudFront
- What if you wanted to run a global AWS Lambda alongside
- Or how to implement request filtering before reaching your application

- For this - you can use Lambda@Edge