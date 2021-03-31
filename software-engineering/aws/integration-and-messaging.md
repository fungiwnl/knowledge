# AWS Integration and Messaging

- When we starting deploying multiple applications, they will inevitable need to communicate with one another
- There are two pattersn of application communication

1. Synchrononous communications (app to app)
2. Asynchronous / event based (application to queue to application)

## SQS

- A simple queuing service
- Fully managed service, used to decouple applications

- Atributes;
  - Unlimited throughout, unlimited number of messages in the queue
   - Default retention of messages: 4 days, maximum of 14 days
   - Low latency (<10ms on publish and receive)
   - Limitation of 256KB per message sent
  
- Can have duplicate messages (at least once delivery, occasionally)
- Can have out of order messages (best effort ordering)

### SQS - Producing Messages

- Produced to SQS usnig the SDK (SendMessage API)
- The message is pesisted in SQS until a consumer deletes it

- Example: send an order to be processed
  - Order id
  - Customer id
  - Any attributes you want

- SQS standard: unlimted throughput

### SQS - Consuming Messages

- Consumers (running on EC2 instances, on-premise servers, AWS lambda)...
- Poll SQS for messages (receive up to 10 mesasges at a time)
- Process the messages (example: insert the message into an RDS database)
- Delete the messages using the DeleteMessage API)

### SQS - Multiple EC2 instance consumers

- Consumers receive and process messages in parallel
- At least once delviery
- Best-effort message ordering
- Consumers delete messages after processing them

### SQS with ASG


### SQS to decoupel between application tiers


### SQS - Security

- Encryption
  - In flight encryption using HTTPS API
  - At-rest encryption using KMS keys
  - Client side encryption if client wants to perform encryption/decryption iself

- Access controls: IAM policies to regulate 

- SQS Access Policies (similar to S3 bucket policies)


### SQS - Message Visibiliy Timeout 

- After a message is polled by a consumer, it becomes invisible to other consumers
- By default, the message visiblity timeout is **30 seconds**
- That means the message has 30 seconds to be processed
- After the messafe visiblity timeout is over, the message is visible in SQS

- If the message is not processed within the visibility timeout, it will be processed twice
- A consumer could call ChangeMessageVisibility API to get more time

- Visibiltiy timeout to high, consumer crashes, reprocessing will take time
- Visiblity timeout is too low, may get dupes

### SQS - Dead Letter Queues

- If a consumer fails to process a message within the Visibility Timeout the message goes back to the queue
- So we can set a threshold of howm any times a message can go back to the queue because this can be problematic
- After the MaximumRecives threshold is execeeded, the mwessage goes into a DLQ

- Useful for debugging
- Makesure to process the messages in the DLQ before they expire, so it's good to set a long retention of 14 days in DLQ

### Practical

- Set up one SQS queue
- Set up second SQS DLQ


### SQS - Delay Queue

- Delay a message (consumers don't see it immediately) up to 15 mins
- Default is 0 seconds
- Can set a default at a queue level
- Can override the default on send using DelaySeconds parameter

### SQS - FIFO Queue

- FIFO - First In First Out (ordering of messages in the queue)
- Limited throughout: 300 msgs without batching 3000msgs with 
- Exactly-once send capapbility (by removing duplicates)
- Messages are processed in order by the consumer


### SQS - Auto Scaling Group (ASG)

- EC2 auto scaled group polling for SQS messages
- More messages more EC2, less messages less EC2


