# VPC

## Understanding CIDR - IPv4 (Classless Inter-Domain Routing)

- CIDR are used for Security Groups rules, or AWS networking in general 0.0.0.0/0, 122.149.196.85/32
- They help define an IP address range
  - We've seen WW.XX.YY.ZZ/32 == one IP
  - We've seen 0.0.0.0/0 == all IPs
  - But we can define for ex: 192.168.0.0/26: 192.168.0.0 - 192.168.0.63 (64 IP)

- A CIDR has two components
  - The base IP (XX.XX.XX.XX)
  - The subnet mask (/26)

- The base IP represents an IP contained in the range
- The subnet masks defines how many bits can change in the IP

- The subnet mask can take two forms. Examples:
   - 255.255.255.0  <- less common
   - /24            <- more common

## CIDR Subnet Masks

- The subnet masks basically alows aprt of the underlying IP to get additional next values from the base IP

- /32 allows for 1 IP = 2^0
- /31 allows for 2 IP = 2^1
- /30 allows for 4 IP = 2^2
- /29 allows for 8 IP = 2^3
- /27 allows for 32 IP = 2 ^5
- /25 allows for 138 IP = 2^6
- /24 allows for 256 IP = 2 ^ 8
- /16 allows for  65,536 IP = 2 ^ 16
- /0 allows for all IPs = 2^32

## Private vs Public IP (IPv4) allowed ranges

- The Interent Assigned Numbers Authority (IANA) established certain blocks of IPV4 adresses for the use of private (LAN) and public
  (Internet) addresses.
- Private IP can only allow certain  alues
  - 10.0.0.0 - 10.255.255.255  (10.0.0.0/8) <= in big networks
  - 172.16.0.0 - 172.31.255.255 (172.16.0.0/12) <= default AWS one
  - 192.168.0.0 - 192.168.255.255 (192.168.0.0/16) <= example: home networks
- All the rest of the IP on the internet are public IP

## Default VPC Walkthrough

- All new accounts have a default VPC
- New instances are launched into default VPC if no subnet is specified
- Default VPC have internet connectivity and all instances have public IP
- We also get a public and private DNS name

## VPC in AWS - IPv4

- Virtual private cloud
- You  can have multiple VPCs in a region (max 5 per region - soft limit)
- Max CIDR per VPC is 5. For each CIDR:
   - Min size is /28 = 16 IP addresses
   - Max size is /16 = 65536 IP addresses
- Because VPC is private, only the Private IP ranges are allowed
   - 10.0.0.0 - 10.255.255.255 (10.0.0.0/8)
   - 172.1.6.0.0 - 17.31.255.255 (172.16.0.0/12)
   - 192.168.0.0 - 192.168.255.255 (192.168.0.0/16)
- Your VPC CIDR should not overlap with your other networks (e.g corporate)

## Create VPC manually

- Your VPCS
- Create VPC
- Enter name
- 10.0.0.0/16 CIDR block
- Tenancy is how we launch EC2 instances with it 

### Adding subnets

- Your Subnets
- Create Subnet
- Enter name
- Associate with created VPC
- 10.0.0.0/24 CIDR
- ap-southeast-2a AZ

- AWS reserves 5 IPs address (first 4 and last 1 IP address) in each Subnet
- These 5 IPs are not avaialble for use and cannot be assigned to an instance
- Ex if CIDR block 10.0.0.0/24 reserved IP are:
   - 10.0.0.0: Network adress
   - 10.0.0.1: Reserved by AWS for the VPC router
   - 10.0.0.2: Reserved by AWS for mapping to Amazon provided DNS
   - 10.0.0.3: Reserved by AWS for future use
   - 10.0.0.255: Network broadcast address. AWS doesn ot support broadcast in a VPC there the address is reserved

- Exam tip:
  - If you need 29 IP addresses for EC2 instances, you can't choose a Subnet of size /27 (32 IP)
  - You need at least 64 IP, Subnet size /26 (64-5 = 59 > 29, but 32-5 = 27 < 29)

### Internet Gateways & Route tables

- Internet gateways helps our VPC instances connect to the internet
- It scales horizontally and is HA and redundant
- Must be created seperately from VPC
- One VPC can only be attached to one IGW and vice versa
- Internet gateway is also a NAT for the instances that have a public IPv4

- Internet gateways on their own do not allow internet access...
- Have to edit route tables 

### Adding Internet gateway

- Go into Internet gateways
- Create internet gateway
- Attach to VPC

### Add route table

- Create seperate route tables for public and private
- Assign public route table to public subnet (same for private)
- Edit public route table to let 0.0.0.0/0 go to created IGW

### NAT instances (Network Address Translation) (outdated by still in exam)

- Allows instances in the private subnets to connect to the internet
- Must be launched in a public subnet
- Must disable EC2 flag: Source / Desintation Check
- Must have Elastic IP attached to it
- Route table must be configured to route traffic from private subnets to NAT instance

- Disable source destination check on NAT instances (doco AWS official)

- Amazon Linux AMI pre-configured are available
- Not highly avaiable / resilient setup out of the box
- => Would need to create ASG in multi AZ + resilent user-data script
- Internet traffic bandwidth depends on EC2 instance performance
- Must manage security groups & rules
  - Inbound 
    - Allow HTTP/ HTTPS Traffic coming frmo Private subnets
    - Allow SSH from your home network (access is provided through IGW)
  - Outbound 
    - Allow HTTP/ HTTPS traffic to your internet

- This is old way of doing things which is not great

### NAT Gateway

- AWS Managed NAT, higher bandwidth, better availability, no admin
- Pay by the hour for usage and bandwidth
- NAT is created in a specific AZ. uses an EIP
- Cannot be used by an instance in that subnet (only from other subnets)
- Requires an IGW (Private Subnet => NAT => IGW)
- 5 Gbps of bandwidth with autoamtic scaling up to 45 GBps
- No security group to manage

## DNS Resolution in VPC

- **enableDnsSupport: (= DNS Resolution setting)**
  - Default True
  - Helps decide if DNS resolution is supported for the VPC
  - If True, queries the AWS DNS server at 169.254.169.253
- **enableDnsHostname: (= DNS Hostname setting)**
  - False by default for newly created VPC, True by default for Default VPC
  - Won't do anything unless enableDnsSupport=true
  - If True, Assign public hostname to EC2 instance if it has a public 
- **If oyu use custom DNS domain names in a private zone in ROute 53, you must set both these attributes to true**

### Hands on 

- Enabling DNS Hostname has a public DNS 
- And then can go into Route 53 and create a private hosted zone for Amazon VPC

## Network ACLs & Security Groups

- NACL are like a firewall which control traffic from and to subnet
- Default NACL allows everything outbound and everything inbound
- **ONE NACL per Subnut, new Subnets are siggned the Default NACL**
- Define NACL rules
  - Rules have a number (1-32766) and higher precedence with a lower number
  - E.g if you define #100 ALLOW <IP> and #200 DENY <IP>, IP willbe allowed
  - Last rule is an * and denies a request in case of no rule match
  - AwS recommends adding rules by increment of 100
- Newly created NACL wil deny everything
- NACL are a great way of blocking a specific IP at the subnet level

### Network ACL vs Security Group

- [Insert table]

## VPC Peering

- Connect two VPC, privately using AWS' network
- Make them behave as if they were in the same network
- Must not have overlapping CIDR
- VPC Peering connection is not transitive (msut be established for each VPC that need to communicate with one another)
- You can do VPC peering with another AWS account
- You must update route tables in each VPC's subnets to ensure instances can communicate

### Good to knows

- VPC peering can work inter-region, cross account
- You can reference a security group of a peered VPC (works cross account)

### Hands on

- Create peering connection to connect demo VPC to default VPC

## VPC Endpoints

- Endpoints allow you to connect to AWS using a private network instead of the public www network
- They scale horizontally and are redundant
- They remove the need of IGW, NAT, etc... to access AWS services
- Interface: provisions an ENI (private IP address) as an entry point (must attach security group) -- most AWS services
- Gateway: provisions a target and must be used in a route table - S3 and DynamoDB
- In case of issues:
   - Check DNS setting resolution in your VPC
   - Check Route Tables

### Hands on

-

## VPC Flow Logs + Athena

- Capture information about IP traffic going into your interfaces
  - VPC Flow logs
  - Subnet flow logs
  - Elastic Network Interface Flow logs
- Helps to monitor & troubleshoot connectivity issues
- Flow logs data can go to S3 / CloudWatch logs
- Captures network information from AWS managed interfaces too: ELB, RDS, ElastiCache, Redshift, Workspaces

### Flog Log Syntax

- <verison> <account-id> <inteface-id> <srcaddr> <dstddr> <srcport> 
  <dstport> <protocol> <packets> <bytes> <start> <end> <action> <log-status>
- Srcaddr, dstaddr help identify problematic IP
- Srcport, dstport help identify problematic ports
- Action: success or failure of the request due to Security Group / NACL
- Can be used for analytics on usage patterns or malicious behaviour
- Flow logs example
- **Query VPC flow logs using Athena on S3 or CloudWatch Logs Insights**

### Hands on

- Create flow logs for demo VPC with cloudwatch log group and s3 bucket
- Analyze logs on s3 bucket with athena

## Bastion Hosts

- We can use a Bastion Host to SSH into our private instances
- The bastion is in the public subnet which is then connected to all other private subnets
- Bastion Host security group must be tightened
- Exam Tip: Make sure the bastion host only has port 22 traffic from the IP you need, not from the security groups of your other instances

## Site to Site VPN

- Customer gateway on Corporate network side
- VPN gateway on AWS side

- Customer gateway:
  - Software app or physical device on customer side of the VPN connection
  - IP Adress:
    - Use static, internet-routable IP address for your customer gateway device
    - If behind a CGW behind NAT 9with NAT-T), use the public IP addresso fthe NAT
- Virtual private gateway
  - VPN concentrator on the AWS side of the VPN connection
  - VGW is created and attached to the VPC from which you want to create the Site to Site VPN connection
  - Possibility to customize the ASN

## Direct Connect (DX)

- Provides a dedicated **private** connection from a remote network to your VPC
- Dedicated connection must be setup between your DC and AWS Direct Connection locations
- You need to setup a VPG on yuor VPC
- Access public resources (s3) and ec2 on same connection
- Use Cases:
  - Increase bandwidth throughput - working with large data sets - lower cost
  - More consistent network experience - applications using real time data feeds
  - Hybrid Environments (on prem + cloud)
- Supports IPv4, IPv6

### Direct Connection Diagram

- [Insert diagram]

## Egress 

- Egress only Internet Gateway is for IPv6 only
- Similar fnction as a NAT, but a NAT is for IPv4
- Good to know: IPv6 are all public addresses
- Therefore all our instances with IPv6 are publicly accessible 
- Egress Only Internet Gateway gives our IPv6 instances access to the internet, but they won't be directly reachable by the internet
- After creating an Egress Only Gateway, edit the route tables 

### Hands on

- Create Eghress internet gateway and add it to route table for all IPV4 ::0/

## AWS Private Link 

### Exposing services in your VPC to toher VPC

- Option 1: make it public
  - Goes through public www
  - Tough to manage access

- Option 2: VPC peering
  - Must create many pering relations
  - Opens the **whole** network

- Option 3: AWS Private Link (VPC Endpoint Services)
  - Most secure & scalable wy to expose a serivce to 1000s of VPC
  - Does not require VPC peering, internet gateway, NAT, route tables..

## AWS Classic Link & EC2-Classic (deprecated)

- EC2-Classic: instances run in a single network shared with other customers
- Amazon VPC: your instances run logically isolated to your AWS account

- ClassicLink: allows you to link EC2-Classic instances to a VPC in your account
  - Must associate with a security group
  - Enables communication using private IPv4 addresses
  - Removes the need to make use of public IPv4 addresses or Elastic IP addresses

- Likely to be distractors at the exam

## AWS VPN CloudHub

- Provide a secure communication between sites, if you have multiple VPN connections
- Low cost hub-and-spoke model for primary or secondary network connectivity between locations
- It's a VPN connection so it goes over the public internet

## Transit Gateway

- Network toplogies can become complicated, so AWS came up with Transit gateway
- For having transitive peering between thousands of VPC and on-premises, hub-and-spoke (star) connection
- Regional resource, can work cross-region
- Share cross-acount using Resource Access Manager (RAM)
- You can peer  Transit Gateways across regions
- Route Tables: limit which VPC can talk with other VPC
- Works with Direct Connect Gateway, VPN conections
- Supports IP Multicast (not supported by any other AWS service)

### Site to Site VPN ECMP

- ECMP = equal-cost multi path routing
- Routing strategy to allow forward a packet over multiple best path
- Use case: create multiple Site-to-Site VPN connections to increase the bandwidth of your connections to AWS

### Throughput with ECMP

- VPN to virtual private gateway
- 1x conection --> 1x VPC
- 1x = 1.25GBps
- 2 tunnels limit

- VPN to transit gateway
- 1x = 1x x4 VPC
- 1x = 2.5Gbps (ECMP) - 2 tunnels used
- 2x = 5.0 Gbps (ECMP)
- 3x = 7.5 Gbps (ECMP)
- +$$ per GB of TGW processed data

### Share direct connect between multiple accounts

- [Insert diagram]


## IPv6 in VPC

- *IPv4 cannot be disabled for your VPC and subnets*
- You can enable IPv6 (they're public IP addresses) to operate in dual-stack mode:
   - Example: 2001:0db...
   - Supports ~ 2^128 IPv6 addresses (vs 2^32 for IPv4) 
- Yuor EC2 instances would get at least a private internal IPv4 and a public IPv6
- They can communicate using their IPv4 or IPv6

- So if you cannot launch an instance in your subnet
  - It's not because it cannot acquire an IPv6 (the space is very large)
  - It's because there are no available IPv6 in yuor subnet
- Thus create a new IPv4 CIDR in yuor subnet 

### Hands on

- Create IPv6 VPC
- Create subnet 
- Create EC2 on IPV6
- Clean up 
