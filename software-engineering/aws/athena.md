# Athena

- Serverless service to perform analytics directly against S3 files
- Uses SQL language to query files
- Has a JBDC / ODBC driver
- Charged per query and amount of data scanned
- Supports CSV, JSON, ORC, ARvo, Parquet (built on Presto)
- Use case: BI/Analytics/Reporting, analyze & query VPC flow logs, ELB logs, CloudTrail trails
- Exam tips: Analyze directly on S3 -> Athena

## Practical

`create database s3_access_logs_db;`

https://aws.amazon.com/premiumsupport/knowledge-center/analyze-logs-athena/

```
SELECT request_uri, httpstatus, count(*) FROM "s3_access_logs_db"."mybucket_logs"
GROUP BY request_uri, httpstatus;
```

```
SELECT count(*) FROM "s3_access_logs_db"."mybucket_logs"
```

```
SELECT * FROM "s3_access_logs_db"."mybucket_logs"
where httpstatus='403';
```
