# AWS Backup

- Fully managed serviced
- Centrally maange and automate backups across AWS services
- No need to create custom scripts and manual processes
- Supported services:
  - Fsx
  - EFS
  - DynamoDB
  - EC2
  - EBS
  - RDS (all DB engines0
  - Aurora
  - Storage Gateway (Volume gateway)
- Supports cross-region backups
- Supports cross-account backups

## Supports

- Supports PITR (point in time recovery) for supported services
- On-Demand and Scheduled back ups
- Tag-based backup polciies
- You create backup polciies known as Backup Plans
   - Backup frequency (Every 12 hrs, daily, weekly, monthly, cron expression)
   - Backup window
   - Transition to Cold Storage (Never, Days, Weeks, Months, Years)
   - Retention Period (Always, Days, Weeks, Months, Years)

- [Insert diagram]
