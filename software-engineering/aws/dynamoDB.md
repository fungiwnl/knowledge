# DynamoDB

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



