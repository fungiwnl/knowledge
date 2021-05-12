# DMS - Database Migration Service

- Quickly and securely migrate databases to AWS, resilient, self healing
- The source database remains available during the migration
- Supports:
  - Homogenous migrations; ex Oracle to Oracle
  - Hetereogenous migrations: ex Microsoft SQL Server to Aurora
- Continuous Data Replication using CDC
- You must create an EC2 instance to perform the replication tasks

- For example: Source DB on premise, Run EC2 instances on DMS which will pull data from Source continuously and
 put it in target DB

## DMS Sources and Targets

- **Sources**
  - On-Premise and EC2 instance databases: oracle, MS SQL Server, MySQL, MariaDB, PostgreSQL
    MongoDB, SAP, DB2
  - Azure: Azure SQL Database
  - Amazon RDS: all including Aurora
  - S3

- **Targets**
   - On-Premise and EC2 instances databases: Oracle, MS SQL Server, MySQL, MariaDB, PostgreSQL, SAP
   - Amazon RDS
   - Amazon Redshift
   - Amazon DynamoDB
   - Amazon S3
   - ElasticSearch Service
   - Kinesis Data Streams
   - DocumentDB

## AWS Schema Conversion Tool (SCT)

- If Source database and Target database do not have the same engine we need to use SCT
- SCT will convert your Database's schema from one engine to another
- Example: OLTP: (SQL Server or Oracle) to MySQL, PostgrSQL, Aurora
- Example: PLAP: (Teradata or Oracle) to Amazon Redshift

- You do not need to use SCT if you are migrating the same DB engine
   - Ex: On-Premise PostgrSQL => RDS PostgrSQL
   - The DB engine till PostgreSQL (RDS is the platform) therefore no SCT required

## DMS - Continuous Replication

- [Insert diagram] 

## Practical

- Navigate to DMS
- Create DMS instance
- Select default VPC
- Select Multi AZ

- Navigate to Database migration tasks
- Navigate to Endpoints to create source and target


- If source database endpoint different from target database endpoint it will automatically use SCt

