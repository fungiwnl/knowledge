# SNS

- One message to many receivers

- The event producer only sends messages to one SNS topic
- As many event receivers (subscriptions) as we want to listen to the SNS topic notifications
- Each subscriber to the topic will get all messages
- Up to 10,000,000 subscriptions per topic
- 100,000 topics limit
- Subscribers can be:
   - SQS
   - HTTP / HTTPS (with delivery retries)
   - Lambda
   - Emails 
   - SMS messages

## SNS integrates with a lot of AWS services

- CloudWatch (for alarms)
- ASG notifications
- Amazon S3 for bucket events
- Cloudformation (upon state changes, faled to build, etc)
- Etc

## AWS SNS - How to publish

- Topic publsih (using the SDK)
- Create a topic
- Create a subscription (or many)
- Publish to the topic

- Direct publish (for mobile apps SDK0
   - Create platform app
   - Create paltform enfpoint
   - Publish to platform endpoint
   

## SNS - Security

- Encryption 
   - In-flight encryption using HTTPS API
   - At-rest encryption using KMS keys
   - Client-side encryption if the client wants to perform encryption/decryption itself

- Access controls: IAM policies

- Access policies
  - Useful for cross-account access to SNS topics
  - Useful for allowing other services (S3 ..) to write an SNS topic 


## SNS + SQS: Fan out

- A common architecture pattern

- Push once in SNS, receive in all SQS queues that are subscribers
- Fully decoupled, no data loss
- This allows SQS for data persistence, delayed processing, retry of work
- Also allows ability to add more SQS subscribers over time
- Make sure your SQS queue access policy allows for SNS to write

- SNS cannot send messages to SQS FIFO queues (AWS limitation)

- For S3 event to many SQS queues, use fan-out