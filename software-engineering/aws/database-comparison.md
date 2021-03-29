# Database Comparison

## Choosing the right database

- We have a lot of managed databases on AWS to choose from
- Questions to choose the right database based on your architecture:
  - Read-heavy, write-heavy, balanced workload? Throughput needs? Will it change, does it need to scale or fluctate during the day?
- How much data to store and for how long? Will it grow? Average object size? How are they accessed?
- Data durabiity? Source of truth for the data?
- Latency requirements? Concurrent users?
- Data model? How will you query the data? Joins? Structured? Semi-structured?
- Strong chema? More flexbility? Reporting? Search? RBDMS / NoSQL?
- Licence costs? Switch to CLoud Native DB such as Aurora?

## Database Types

- RDBMS (= SQL /OLTP); RDS, Aurora - great for joins
- NoSQL databases: DynamoDB (~JSON), ElasticCache (key / value pairs), Neptune (graphs) - no joins, no SQL
- Object Store: S3 (for big objects) / Glacier (for backups / archive)
- Data Warehouse ( = SQL Analytics / BI): Redshift (OLAP), Athena
- Search: ElasticSearch (JSON) - free text, unstructured searches
- Graphs: Neptune - displays relationships between data

## RDS

- Managed PostgresSQl / MySQL / Oracle / SQL Server
- Must provision an EC2 instance & EBS Volume type and size
- Support for read replicas and multi AZ
- Security through IAM, Security groups, KMS, SSL in transit
- Backup / Snapshot/ Point in time restore feature
- Managed and scheduled maintenance
- Monitoring through CloudWatch

- Use case:
  - Store relational datasets, perform SQL queries, transacitonal inserts, deletes, updates 

### Solutions Architect perspective

- Operations: small downtime when failovers happens, maintenacve happens, saling in read reps, ec2 nistances, restore EBS implies manual intervention and application changes
- Security: AWS responsible for OS security, we are responsible for KMS, security groups, IAM, authorizing users in DB, using SSL
- Reliability: multi-AZ, failover in case of failures
- Performance: depends on EC2 instance type, EBS volume type, ability to add read replicas. Doesn't auto scale
- Cost: pay per hour based on provisioned Ec@ and EBS

## Aurora

- Compatible API for PostgresSQL / MySQL
- Data is held in 6 replicas, across 3 AZ
- Auto healing capapbility
- Multi AZ, Auto Scaling Read Replicas
- Read Replicas can be Global
- Aurora database can be Global for DR or latency purposes
- Auto scaling of storage from 10GB to 64TB
- Define EC2 instance type for aurora instances
- Same security / monitoring / maintenance features as RDS
- "Aurora Serverless" option

- Use case: same as RDS, but with less maintenance / more flexibility / more performance

### Solutions Architect perspective

- Operations: less operations, auto scaling storage
- Security: AWS respoible for OS security, we are responsible for KMS, security groups, IAM, authorizing users in DB, using SSL
- Reliability: Multi AZ, highly available, possibly more than RDS, Aurorora serverless option
- Performance: 5x performance (according to AWS) due to architectural optimizatios. Up to 15 read replicas (only 5 for RDS)
- Cost: Pay per hour based on EC2 and storage usage: Possibly lower costs compared to Enteprise grade databases such as Oracle

### ElastiCache

- Managed Redis / Memcached (similar offering as RDS, but for caches)
- In-memory dat store, sub-millisecond latency
- Must provison an EC2 instance type
- Support for Clustering (redis) and multi AZ, read replicas (sharding)
- Security through IAM, Security Groups, KMS, Redis Auth
- Backup / Snnapshot/ Point in time restore feature
- Managed and scheduled maintenance
- Monitoring through Cloudwatch

- **Use case**: Key / value store, frequent reads, less writes, cache results for DB queries, store session data for webistes, cannot use SQL.


### Solutions Architect perspective

- Operations: same as RDS
- Security: AWS responsible for OS security, we are responsible for KMS, security groups, IAM, users (Redis Auth), using SSL
- Reliability: Clustering, Multi AZ
- Performance: Sub-millisecond performance, in memory, read replicas, sharding, very popular cache option
- Cost: Pay per hour based on EC2 and storage use

## DynamoDB

- AWS proprietary technology, managed NoSQL database
- Serverless, provisioned capacity, auto scaling, on demand capapcity (Nov 2018)
- Can replace ElastiCache as a key/value store (storing session data for example)
- Highly available, multi az by default, read and writes are decoupled, DAX for read cache
- Reads can be eventually consistent or strongly consistent (?)
- Security, authentication and authorization is done through IAM
- DynamoDB streams to integrate with AWS Lambda
- Backup / Restore feature, GlobalTable feature
- Monitoring through CloudWatch
- Can only query on primary key, sort key or indexes

- **Use Case**: Serverless applications deployment (small documents 100s Kbs), distrbuted serverless cache, doesn't have SQL query lnaguage availabel, has transactions capability now from Nov 2018

### Solutions Architect perspective

- Operations: no ops needed, auto scaling, serverless,
- Security: full security through IAM, KMS encryption, SSL in flight
- Reliability: multi-az, backups
- Performance: single digit ms performance, DAX for caching reads, performance doesn't degrade if your application scales
- Cost: Pay per provisioned capacity and storage usage (no need to guess in advance any capacity - can use auto scaling)

## S3

- S3 is a key / value store for objects
- Great for big object, not so great for small objects
- Serverless, scales infinitely, max ojbect size is 5 TB
- Eventually consistency for overwrites and deletes
- Tiers: S3 Standard, IA, One Zone IA, Glacier for backups
- Features: Versioning, Encryption, Cross Region Replication, etc
- Security: IAM, Bucket Policies, ACL
- Encryption: SSE-S#, SSE-KMS, SSE-C, client side, SSL in transit

- **Use Case**: static files, key value store for big files, website hosting

### Solutions Architect perspective

- Operations: none
- Security: IAM, Bucket policies, Encryption, SSL
- Reliability: 99.999999999% durability, 99.99% availability, multi-az, CRR
- Performance: scales to thousands of read / writes per second, transfer acceleration, multi-part for big files
- Cost: pay per storage usage, network cost, requests number

## Athena

- Fully serverless database with SQL capabilities
- Used to query data in S3
- Pay per query
- Output results back to S3
- Secured through IAM

- **Use Case**: one time SQL queries, serverless queries on S3, log analytics

### Solutions Architect perspective

- Operations: no ops, serverless
- Security: IAM + S3 security
- Reliabiltiy: managed service, Presto engine, highly available
- Performance: queries scale based on data size
- Cost: pay per query, per TB of data scanned, serverless

## ElasticSearch

- In DynamoDB- you can only find by primary key or indexes
- With ElastiSearch, you can search any field, even in partial matches
- It's commont to use ElasticSearch as a complement to another database
- ElasticSearch also as some usage for Big Data apps
- You can provision a cluster of instances
- Built-in itnegrations; Kinesis, Firehouse ,IoT, Cloudwatch logs for data ingestion
- Security through Cognito and IAM, KMS, SSL & VPC
- Comes with Kibana (visualization), Logstash (log ingestion), - ELK stack

### Solutions architect perspecptive

- Ops: similar to RDS
- Security: Cognito, IAM, VPC, KMS, SSL
- Relaibiltiy: multi-az, clustering
- Performance: based on ElasticSearch project (open resource), petabyte scale
- Cost: pay per node provisioned

- **Use Case**: Search and indexing
