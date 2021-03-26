# Kinesis

- Kinesis is a managed alterantive to Apache Kafka
- Great for application logs, metrics, IoT, clickstreams
- Great for "real-time" big data
- Great for stremaing processing frameworks (Spark, NiFi, etc...)
- Data is auto replicated to 3AZ

- Kinesis streams: low latency streaming ingest at scale
- Kinesis analytics: perform real-time analytics on streams using SQL
- Kinesis firehose: load streams into S3, Redshift, ElasticSearch

## Diagram

Click streams
IoT devices      ---> Amazon Kinesis Streams -> Amazon Kinesis Analytics -> Amazon Kinesis Firehose -> Amazon S3 bucket
Metrics & logs

## Kinesis Streams

- Streams are divided in ordered Shards / Partitions
- Data retention is 1 day by default, can go up to 7 days
- Ability to reprocess / replay data
- Multiple applications can consume the same stream
- Real time processing with scale of throughput
- Once data is inserted into Kinesis, it cant be deleted (immuteable)

## Kinesis Shards

- One stream is made of many different shards
- 1 MB/s or 1000 messages/s at write PER SHARD
- 2MB/s at read PER SHARD
- Billing is per shard provisioned, and as many as you want
- Batching available or per message calls
- The number of shards can be changed over time (reshard / merge) (auto scaling)
- Records are ordered per shard

## Kinesis API - Put records

- PutRecord API + Partition key that gets hashed
- The same key goes to the same partition (helps with ordering for a specific key)
- Messages sent get a sequence number
- Choose a partition key that is highly distributed (helps prevent 'hot partition')

## Kenesis API - Exceptions

- ProvisonedThroughputExceedeExceptions
  - Happens when sending more data (exceeding MB/s or TPS for any shard)

## Kenesis Security

- Control access/auth using IAM polciies
- Encryption in flight using HTTPS endpoints
- Encryption at rest using KMS 
- VPC endingpoints availabel for Kinesis to accees within VPC

## Kinesis Data Firehose

- Fully managed service, no admin, auto scaling, serverless
- Load data into RedShift, S3, ElasticSearch, Splunk
- Near Real Time
  - 60 seconds latency minimum for non full batches
  - Or minimum 32 MB of data at a time

- Pay for the amount of data going through Firehose

### Diagram



### Data streams vs Firehose

- Streams 
   - Going to write custoom code (producer / consumer)
   - Real time (200ms)
   - Must manage scaling (shard splitting / merging)
   - Data storage for 1 to 7 days, replay capability, multi consumers

- Firehose
  - Fully managed
  - Serverless data transformations with Lambda
  - Near real time
  - Automated scaling
  - No data storage

## Kinesis Data Analytics

- Perform real-time analytics on Kinesis Streams using SQL
- Auto scaling
- Managed
- Continuous: real time
- Pay for consumption rate
- Can create streams out of the real-time queries

