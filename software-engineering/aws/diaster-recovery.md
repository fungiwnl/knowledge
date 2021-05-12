# Diaster Recovery

- Any event that has a engative impact on a company's business contiunity or finances is a diaster
- Diaster Recovery (DR) is about preaparing for and recovering from a diaster
- What kind of diaster recovery?
   - On-premise => On premise: traditional DR and very expensive
   - On-premise => AWS Cloud: hybrid recovery
   - AWS Cloud Region A => AWS Cloud Region B

- There are to key terms for DR
   - RPO: Recovery Point Objective
   - RTO: Recovery Time Object

## RPO and RTO

- RPO is how often you run backups and how much of a data loss are you willing to accept in case of a disaster
- RTO is the downtime 
- Optimizing these does drive some architecture decisions, and smaller RPO and RTO the higher cost.

## Disaster Recovery Strategies

- Backup and Restore
- Pilot Light
- Warm Standby
- Hot Site / Multi Site Approach

### Back up and Restore (High RPO)

- Corporate data center
- AWS Cloud
- This is quite cheap, but high RPO and RTO

### Pilot Light

- A small version of the app is always running in the cloud
- Useful for the critical core (pilot light)
- Very similar to Backup and Restore
- Faster than Backup and Restore as critical systems are already up

- We get:
   - lower RPO, lower RTO

### Warm Standby

- Full system is up and running, but at minimum size
- Upon diaster, we can scale to production load

- Use route 53 to failover and autoscaling to scale up 

### Mutli Site / Hot Site Approach

- Very low RTO (minutes or seconds) -- very expensive
- Full Production Scale is running AWS and On Premise

### All AWS Multi Region

- Aurora global database to replicate and when we need to failover we can do so

## Disaster Recovery Tips

- Backup
   - EBS Snapshots, RDS automated backups / Snapshots etc
   - Regular pu shes to S3 / S# IA / Glacier, Lifecycle Policy, Cross Region Replication
   - From On-Pmreise Snowball or Storage Gateway
- High Availability:
   - Use Route53 to migrate DNS over from Region to Region
   - RDS Multi-AZ, ElastiCache, Multi AZ, EFS, S3
   - Site to Site VPN as a recovery from Direct Connect
- Replication
  - RDS Replication (Cross Regiion), AWS Aurora + Global Databases
  - Database replication from on-premise to RDS
  - Storage Gateway
- Autoamtion
  - CloudFormation / Elastic Beanstalk to re-create a whole new environment
  - Recover / Reboot EC2 instances with CloudWatch if alarms fail
  - AWS Lambda functions for customized automations
- Chaos
  - Netflix has "simian army" randomly terminating EC2

