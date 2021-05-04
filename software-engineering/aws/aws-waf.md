# AWS WAF - Web Application Firewall

- Protects your web apps from common web exploits (Layer 7)
- Layer 7 is HTTP (vs Layer 4 is TCP)
- Deploy on ALB, API Gateway, CloudFront

- Define Web ACL (Web Access Control List):
  - Rules can include: IP addresses, HTTP headers, HTTP body, or URI strings
  - Protects from common attack - SQL injection and Cross-Site-Scripting (XSS)
  - Size constraints, geo-match (block countries)
  - Rate-based rules (to count occurences of events) - for DDos protection

## Firewall manager

- Manages rules in all accounts of an AWS Organization

- Common set of security rules
- WAF rules
- AWS shield advanced
- Security groups of EC2 and ENI resources in VPC

## Sample Reference Architecture for DDoS Protection

- [Insert diagram]

