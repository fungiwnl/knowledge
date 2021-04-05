# Cloudwatch

- Cloudwatch provides metrics for every service in AWS
- Metric is variable to monitor (CPUUtilization, NetworkIn...)
- Metrics belong to namespaces
- Dimension is an attribute of a metric (instant id, environment, etc...)
- Up to 10 dimensions per metric
- Metrics have timestamps
- Can create CloudWatch dashboards of matrics

## EC2 Detailed monitoring

- EC2 instance metrics have metrics every 5 mins
- With detailed monitoring (for a cost), you get data every 1 minute
- Use detailed monitoring if you want to prompt scale your ASG

- AWS free tier allows us 10 free monitoring metrics

## Custom metrics

- Possibility to define and send your own custom metrics to CloudWatch
- Abiltiy to use dimnesions to segment metrics
  - Instance.id 
  - Environment.name

- Metric resolution:
  - Standard 1 min
  - High res: up to 1 sec (storageresolution API param) -- higher cost
- Use API call PutMetricData
- Use exponential back off in case of throttle errors

## CloudWatch dashboards

- Great way to setup dashboards for quick access to key metrics
- Dashboards are global
- Dashboards can include graphs from different regions
- You can change time zone and time range of the dashboards
- You can setup auto refresh (10s, 1m,2m,5, 15m)

Pricing:
- 3 dashboards (up to 50 metrics) for free
- $3/dashboard/month afterwards

## CloudWatch logs

- Apps can send logs to CW using the SDK
- CW can collect logs from:
  - Elastic Beanstalk
  - ECS
  - AWS Lambda
  - VPC Flow
  - API Gateway
  - CloudTrails based on filter
  - Cloudwatch log agents on EC2 machines
  - Route53: Log DNS queries

- CloudWatch logs can go to:
  - Batch exporter to S3 for archival
  - Stream to ERlasticSearh cluster for further analytics

- Logs storage architecute:
  - Log groups: arbitrary name, usually representing an app
  - Log streams: instances within app / log files / container
- Can define log expiration policies (never expire, 30 days, etc...)
- Using the AWS CLI we can tail CloudWatch logs
- To send logs to CloudWatch, make sure IAM permissions are correct
- Security: encryption using KMS group level

## Cloudwatch Logs Metric Filter & Insights
- CloudWatch logs metric filter 
  - For example, find a specific IP inside of a log
  - Metric filters can be used to trigger alarms

- CloudWatch logs insights can be used to query logs and add queries to CloudWatch Dashboards

## CloudWatch Agent

- By default, no logs from your EC2 machine will go to CloudWatch
- You need to urn a CloudWatch agent on EC2 to push the log files you want
- Make sure IAM permissions are correct
- The CloudWatch log agent can be setup on-premises too

### Log Agent and Unified Agent

- For virtual servers (EC2, on-premise servers)

- Cloudwatch Logs Agent
  - Old version of agent
  - Can only send to CloudAwatch logs

- CloudWAtch Unified Agent
  - Collect additional system level metrics such as RAM, processes, etc
  - Colects logs to send to CloudWatch logs
  - Centralised config using SSM parameter store
   
  - Collect directly on your Linux server / EC2

  - CPU
  - Disk (free, used, total) Disk IO (writesm reads, bytes, iops)
  - RAM (free, inactive, used, total, cached)
  - Netstat (number of TCP and UDP connections, net packets, bytes)
  - Processes (total dead, bloqued, idle, running, sleep)
  - Swap space

## CloudWatch Alarms

- Alarms are used to trigger notifications for any metric
- Alarms can got to Auto Scaling, EC2, SNS 
- Various options (sampling, %, max, min, etc..)
- Alarm states:
  - OK
  - INSUFFICIENT_DATA
  - ALARM
- Period:
  - Length of time in seconds to evaluate the metric
  - High res custom metrics: can only choose 10 sec or 30 sec

## EC2 Instance Recovery

- Status check:
   - Instance status = check EC2 VM
   - System status = check the underlying hardware
   
- Recovery: Same private, public, elastic IP, metadata, placement group

## CloudWatch events

- Schedule: cron jobs
- Event Pattern: event rules to react to a service doing something
  - ex: codepipleine state changes
- Triggers to Lambda functions, SQS/SNS/Kinesis messages
- CloudWatch event creates a small json document to give info about the change

## CloudTrail

- Provides governance, compliance and audit for AWS account
- CloudTrail is enabled by default
- Get an history of events / API calls made within your AWS account
  - Console
  - SDK
  - CLI
  - AWS services
- Can put logs from CloudTrail into CloudWatch logs
- If a resource is deleted in AWS, look into CloudTrail first
