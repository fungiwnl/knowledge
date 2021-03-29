# Neptune

- Fully managed graph database
- When do we use Graphs?
   - High relationship data
   - Social networking: user friends iwth users, replied to comment on post of user and likes other comments
   - Knowledge graphs (wikipedia)

## Diagram insert (todo)

- Highly available across 3 AZ, with up to 15 read replicas
- Point in time recovery, continuous backup to Amazon S3
- Support for KMS encryption at rest + HTTPS

## Solutions Architect perspective

- Ops: similar to RDS
- Security: IAM, VPC, KMS, SSL, + IAM auth
- Reliabiltiy: Multi-AZ, clustering
- Performance: best suited for graphs, clustering to improve performance
- Cost: pay per node provisioned

- **Use Case**: Neptune = Graphs
