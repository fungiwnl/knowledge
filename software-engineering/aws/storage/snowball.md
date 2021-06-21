# Snowball

- A physical data transport solutions that helps moving TBs or PBs of data in or out of AWS
- Alternative to moving data over the network (and paying network fees)

- **Use case:**
  - Large data cloud migrations, DC decommission, disaster recovery
  - If it takes more than a week to transfer over the network use Snowball devices


## Process

1. Request snowball devices from AWS console for delivery
2. Install snowball client on your servers
3. Connect the snowball to your servers and copy files using the client 
4. Ship back the device when you're done (goes right to AWS facility)
5. Data will be loaded into S3 
6. Snowball completely wiped
7. Tracking is done using SNS, text messages and the AWS console

## Snowball Edge

- Snowball edge adds computional capability to the device
- 100TB capacity with either:
  - Storage optimized - 24 vCPU
  - Compute otpimized - 52 vCPU & optional GPU
- Supports a custom EC2 AMI so you can perform process on the go
- Supports custom Lambda functions

- Useful to pre-process data while moving 

- **Use case**: data migration, image collation, IoT capture, machine learning


## AWS Snowmobile

- Transfer exabytes of data (1 EB = 1,000 PB = 1,000,000 TBs)
- Snowmobile has 100PB of capacity 
- Better than Snowball if you transfer more than 10PB

## Solution Architecture tip:

- Snowball cannot import to Glacier directly, you have to use S3 first and then an S3 lifecycle policy