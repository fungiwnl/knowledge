# Networking Costs in AWS

- Free for traffic in 
- Free if using private IP

- $0.01 if using Private IP between AZ
- $0.02 if using Public IP / Elastic IP

- Use a Private IP instead of Public IP for good savings and better network performance
- Use the same AZ for minimum savings (at the cost of high availability)

## Minimizing egress traffic network cost

- Egress traffic: outbound traffic (from AWS to outside)
- Ingress traffic: inbound traffic - from outside to AWS (typically free)
- Try to keep as much internet traffic within AWS to minimize costs
- **Direct connect location that are co-locatd in the same AWS region result in lower cost**

## S3 Data Transfer Pricing - Analysis for USA

- S3 ingress: free
- S3 to Internet: $0.09 per GB
- S3 Trasnfer Accleration
  - Faster transfer times (50 to 500% better)
  - Additional cost on top of Data Trasnfer Pricing + $0.04 to $0.08 per GB
- S3 to CloudFront: $0.00 per GB
- CloudFront to INternet: $0.085 per GB (slightly cheaper than S3)
   - Caching capability (lower latency)
   - Reduce costs assocaited with S3 requests piricng (7x cheaper with CloudFront)
- S3 Cost Region Replication: $0.02 per GB

## Pricing: NAT Gateway vs Gateway VPC Endpoint

- For NAT Gateway accessing S3 
  - $0.045 NAT gateway / hour
  - $0.045 NAT Gateway data processed per GB
  - $0.09 Data transfer out to S3 (cross region)
  - $0.00 Data transfer out to S3 (same region) 

- For VPC Endpoint
   - No cost for using Gateway Endpoint. $0.01 Data transfer in/out (same-region)
