# FSx

- EFS is a shared POSIX system for Linux systems
- FSx for Windwos is afully managed Windows file system share drive
- Supports SMB prtocol & Windows NTFS
- Microsoft Active Directory integration, ACLs, user quotas
- Built on SSD, scale up to 10s of GB/s, millions of IOPs, 100s PB of data
- Can be accessed from yuor on-premise infra
- Can be configured to be multi-AZ
- Data is backed up to daily to S3


## Amazon FSx for Lustre

- Lustre is a type of parallel distributed file system, for large scale computing
- Lustre is derived from "Linux" and "cluster"

- Machine learning, high performance computing (HPC)
- Video processing, financial modeling, electronic design automation
- Scales up to 100s GB/s, millions of IOPS, sub-ms latencies
- Seamless integration with S3
   - Can "read S3" as a file system (through FSx)
   - Can write the output of the computations back to S3 (throguh FSx)
- Can be used from on-premise servers
