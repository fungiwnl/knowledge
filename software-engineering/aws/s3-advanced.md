# S3



## S3 Replication

- Cross region replication

- Same region replication 

- Buckets can be in different accounts 

- Copying is asynchronous

- Proper IAM permissions to S3

  

### Hands on

- Bucket versioning is required
- Replication rule under bucket management tab 
- Will only replicate newer objects after creating rule 
- Delete markers not replicated by default 



## S3 Pre-signed URLs

- Can generate pre-signed URLs using SDK or CLI
   - For downloads
   - For uploads
- Valid for a default of 3600 seconds can change timeout with --expires-in [TIME_BY_SECONDS] argument


### Hands on

`aws s3 presign s3://mybucket/myobject --region my-region`



## S3 Storage Classes

- Amazon S3 Standard - General Purpose
- Amazon S3 Standard-Infrequent Access (IA)
- Amazon S3 One Zone Infrequent Access
- Amazon S3 Inteliggent Tiering
- Amazon Glacier
- Amazon Glacier Deep Archive

### S3 Standard - General Purpose

- High durability (99.99999999%) of objects across mltiple AZ
- Sustain 2 concurrent facility failure
- Uses cases: Big data analytics, mobiel and gaming apps, content distribution

### S3 Standard - Infrequent Access IA)

- Suitable for data less frqeuently accessed, but rqeuires rapid access when needed
- Low cost compared to S3 Standard
- Sustain 2 concurrent facility failure

- Use cases: As a data store for disaster recovery, backups 

### S3 One Zone IA

- Same as IA, but data is stored in a single AZ
- 99.5% availabiity
- Low cost compared to IA by 20%

- Use cases: Storing secondary backup copeies of on premise data, or storing data you can recreate 

### S3 Intelligent Tiering

- Same low latency and high throughpout of S3 standard
- Small monthly monitoring and auto tiering fee
- Auto movies objects between two acess tiers based on changing access patterns

### Amazon Glacier

- Low cost object storage meant for archiving / backup
- Data is retained for the longer term (10s of years)
- Alternative to on-premise magnetic tape storage
- Average annual durability of 99
- Cost of storage per motnmh ($0.004/GB) + retrieval cost
- Each item in Glacier is 
- Archive stored in vaults

### Amazon Glacier Deep Archive

- Amazon Gaclier - 3 retrieval options
    - Expedited (1-5 mins)
    - Standard (3 to 5 hrs)
    - Bulk (5-12 hrs
    - Minimum storage duration of 90 days 
- Amazon Glacier Deep Archive (for long term storage - cheaper)
    - Standard (12 hrs)
    - Bulk (48 hrs)
    - Minimum storage duration of 180 days

### Hands On

- File upload > Additional uplaod options -> Storage classes



## S3 Lifecycle Rules

- Transaction actions: definies when objects are transitioned to another storage class
- Expiration actions: configure objects to expire (delete) after some time 
   - Access log files can be set to delete after 365 days
   - Can be used to delete olf version of files (if versioning is enabled)
   - Can be used to delete incomplete multi-part uploads
- Rules can be created for a certain prefix (ex s3://mybucket/mp3/*)
- Rules can be created for certain object tags 


### Hands on

- Current version actions 
- Previous version actions
- Rules for different filters 



## S3 Baseline Performance

- Amazon S3 auto scales to high request rates, latency 100-200ms
- Yuor app can achieve at least 3.5k PUT/COPY/POST/DELETE and 5.5k GET/HEAD requests per prefix in a bucket
- No liits to number of prefixes in a bucket
- E.g.
    - bucket/folder1/sub1file - > folder/sub11i

### S3 KMS Limitation

- If you use SSE KMS, you may be impacted by KMS limits
- When you upload it calls

### Performance

- Multi-party upload 
    - recommend files for > 100MB
    - must use for > 5GB
    - can help parallelize uploads (speed up transfers)
- S3 Transfer Acceleration (upload only)
   - increase trasnfer speed by transferring file to an AWS edge location which will forwward the data to the S3 bucket in the target region



## S3 Event notifications

- S3Object Created, S3: ObjectRemoved, S3PReplciation
- Object name filtering possibble (*.jpg)
- Use case: generate thumbnails of images uploaded to S3



## S3 Object Lock & GlacierVault Lock

- S3 Object Lock
   - Adopt a WORM model
   - Block na object version deletion for a specified amount of time 

- Glacier Vault Lock
   - Adopt a WORM model
   - Lock the policy for future edits (can no loner be changed)
   - **Helpful for compliance and data retention**
