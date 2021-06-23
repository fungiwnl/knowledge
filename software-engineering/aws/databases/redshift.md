# Redshift

- Redshift is based on PostgreSQL, but its' not used for OLTP
- It's OLAP - online analytical processing (analytics and data warehousing)
- 10x better performance than other data warehouses, scale to PBs of data
- Columnar storage of data (instead of row based)
- Massively parallel query execution (MPP), highly available
- Pay as you go based on the instances provisioned
- Has a SQL interface for performing the queries
- BI tools such as AWS Quicksight or Tableau integrate with it

## How is data loaded

- Data is loaded from S3, DynamoDB, DMS, other DBs
- From 1 node to 128 nodes, up to 160 GB of space per node
- Leader node: for query planning, results aggregation
- Compute node: for performing the queries, send results to leader
- Redshift Spectrum: perform queries directly against S3 (no need to load), which is great for adhoc queries
- Backup and restore, Security VPC / IAM / KMS, CloudWatch Monitoring
- Redshift Enhanced VPC Routing: COPY / UNLOAD goes through VPC (enhanced security, performance)

## Snapshots and disaster recovery

- Snapshots are point in time backups of a cluster, stored internnally in S3
- Snapshots are incremental (only what has changed is saved)
- You can restore a snapshot into a new cluster
- Automated: every 8 hours, every 5 GB, or on a schedule. Set retention
- Manual: snapshot is retained until you delete it

- You can configure Redshift to auto copy snapshots (auto or manual) of a cluster to another AWS region

## Redshift Spectrum

- Query data that is already in S3 without loading it 
- Must have a Redshift cluster available to start the query 
- The query is the submitted to thousands of Redshift Spectrum nodes

## Solutions Architect perspective

- Ops: similar to RDS
- Security: IAM, VPC, KMS, SSL
- Reliability: highly available, auto healing
- Performance: 10x performance vs other data warehousing, compression
- Cost: pay per node provisioned, 1/10th cost vs other warehouses

**Use Case**: Analytics / BI / Data warehousing