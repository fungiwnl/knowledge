# AWS Glue

- Managed **extract**, **transform**, **and load (ETL) service**
- Useful to prepare and transform data for analytics (e.g Redshift data warehouse, athena, EMR)
- Fully **serverless** service

## Glue Data Catalog

- Glue jobs (ETL) 
  - Glue data catalog: catalog of datasets (metaadata)
  - Glute data crawler to crawl s3, rds, dynamodb or jdbc database compatible and write metadata to glue data catalog
  - Output to analytics service such as athena, redshift, emr
