# Cloudfront

- Content delivery network (CDN)
- Improves read performance, content is cached at the 'edge'
- 216 Point of Prescence globally (edge locations)
- DDoS protection, integration with Shield, AWS Web Application Firewall
- Can expose external HTTPS and can talk to internal HTTPS backends 

- Distribute reads all around the world, improve latency, and remove load from origin (S3, ALB, EC2, or HTTP endpoint)

## CloudFront - Origins

- S3 Bucket 
  - For distributing files and caching the mat the edge
  - Enhanced security with CloudFront Origin Access Identity (OAI)
  - CloudFront can be used asn an ingress (to upload files to S3)

- Custom Origin (HTTP)
  - ALB
  - EC2 Instance
  - S3 website

## CloudFront - S3 as an Origin

## CloudFront - ALB or EC2 as an Origin


## CloudFront Geo Restriction

- You can restrict who can access your distribution
  - Whitelsit
  - Blacklist 

- The country is determiend by using a 3rd party Geo-IP database
- Use case: Copyright Laws to control access to content

## Practical

- Create S3 bucket
- Create CF distrubiton
- Create OAI
- Limit the S3 bucket to be accessed only using this identity 

## CloudFront Signed URL / Signed Cookies

- You want to distribute paid shared content to premium users over the world
- You can use the Signed URL / Cookie. We attach a policy with:
   - URL expioration
   - IP ranges to 
   - Trusted signers (which AWS accounts can create signed URLs)

- How long URL should be valid for?
  - Shared cotent (movie, music); make it short ( few mins)
  - Private content (private to the user): you can make it last for years

- Signed URL = access stop invididual files (one signed URL per file)
