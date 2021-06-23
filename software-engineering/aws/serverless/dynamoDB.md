# DynamoDB

- Serverless database 
- Fully managed, highly available with replication across 3 AZ
- NoSQL database - not a relational database
- Scales to massive workloads, distributed database
- Millions of request per seconds, trillions of rows, 100s of TB of storage
- Fast and consistent performance (low latency on retrieval)
- Integrate with IMA for security, authorization and administration
- Enables event driven programming with DynamoDB Streams
- Low cost and auto scaling

## Basics

- DynamoDB is made of tables
- Each table has a primary key (must be decided at creation time)
- Each table can have an infinite number of items (= rows)
- Each item has attributes ( can be added over time - can be null)
- Maximum size of a item is 400KB
- Data types supported are:
   - ScalarTypes: String, Number, Binary, Bool, Nll
   - DocumentTypes: List, Map
   - Set Types: String set, Number set, Binary set

## Provisioned throughput

- Table must have provisioned read and write capacity units 
- Read Capacity Unit (RCU): throughputs for reads ($0.00013 per RCU)
  - 1 RCU = 1 strongly consistent read of 4 KB per sec
  - 2 RCU = 2 consistent read of 4 KB per sec
- Write Capacity Units (WCU): throughputs for writes ($0.00065 per WCU)
  - 1 WCU = 1 write of 1 KB per second
- Option to setup auto-scaling of throughput to meet demand
- Throughput can be exceeded temporarily using 'burst credit'
- If burst credit are empty, you'll get a ProvisionedThroughputException
- It's then advised to do an exponential back-off retry

## Practical

- Create a dynamoDB table
- Insert two items

## DynamoDB - DAX

- DAX = DynamoDB Acceleartor
- Seamless cache for DynamoDB, no appliaction re-write
- Writes go throguh DAX to DynamoDB
- Micro second latency for cached read & queries
- Sovles the Hot Key problem (too many reads)
- 5 minutes TTL for cache by default
- Up to 10 nodes in the cluster
- Multi AZ (3 min for prod recommended)
- Secure (Encryption at rest with KMS, VPC, IAM, Cloudtrail)

- DAX is a great way to speed up reads on your and start caching your data in DynamoDB

## DynamoDB - Streams

- Changes in DynamoDB (Create, Update, Delete can end up in a DynamoDB stream)
- This stream can be read by AWS Lambda, and you can:
   - React to changes in real time (welcome email to new users)
   - Analytics
   - Create derivative tables  / views
   - Insert into Elastic Search
- Could implement cross region replication using streams
- Streams has 24 hours of data retention

## DynamoDB - New features

- Transactions 
  - All or nothing type of operations
  - Coordinated Insert, Update & Delete across multiple tables
  - Include up to 10 unique items or up to 4 MB of data

- On Demand
  - No capacity planning needed (WCU / RCU) - scales automatically
  - 2.5x more expensive than provisioned capacity (use with care)
  - Helpful when spikes are un-predictable or the application is very low throughput

## DynamoDB - Security & Other

- Security:
  - VPC endpoints
  - IAM access
   - Encryption at rest using KMS, transit using SSL/TLS
- Back up and Restore feature available
  - Point in time restore like RDS
  - No performance impact
- Global Tables
  - Multi region, fully replicated, high performance
- Amazon DMS can be used to migrate DynamoDB (from Mongo, Oracle, MySQL, S3, etc)
- Can launch a local DynamoDB on your computer for development purposes)

## DynamoDB - Other features

- Global tables (cross region replication)
  - Active Active replcation, many regions
  - Must enable DynamoDB streams for it
  - Useful for low latency, Disaster recovery purposes

- Capacity planning
  - Planned capacity: provsion WCU & RCU can enable auto scaling
  - On-demand capcity: get unlimtied WCU & RCU, no throttle, more expensive


Streams enable DynamoDB to get a changelog and use that changelog to replicate data across regions