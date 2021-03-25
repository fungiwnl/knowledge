# Storage Gateway

- AWS is pushing for hybrid cloud
  - Part of your infra is on cloud
  - Part of your infra is on-premise

## Types

- File gateway
- Volume gateway
- Tape gateway

## File Gateway

- Configured S3 buckets are accessible using the NFs and MSB protocol
- Supports S3 standard, S3 IA, S3 One Zone IA
- Bucket access using IAM roles for each File Gateway
- Most recently used data is cached in the file gateway
- Can be mounted on many servers

File access / NFS -> File Gateway (backed up S3)

## Volume Gateway

- Block storage using iSCSI protocol backed up S3
- Backed by EBS snapshots which can help restore on-premise volumes
- Cached volumes, low latency access to most recent data
- Stored volumes: entire data set is on premise, scheduled backups to S3

Volumes/ Block Storage /iSCI -> Volume gateway (backed by S3 with EBS snapshots)

## Tape Gateway

- Some companies have backup processes using physical tapes
- With Tape Gateway, companies use the same proecsses but in cloud
- Virtual Tape Library (VTL) backed by Amazon S3 and Glacier
- Back up data using existing tape-based proceses (and iSCI interface)
- Works with leading backup software vendors

VTL Tape solution / Backup with iSCI -> Tape Gateway (backed by S3 and Glacier)

## File Gateway - Hardwre appliance

- Using a file gateway means you need virtualization
- Otherwise, you can use a File Gateway Hardware Appliance
- You can buy it on amazon.com

- Helpful for daily NFS backups in small data ceneters


