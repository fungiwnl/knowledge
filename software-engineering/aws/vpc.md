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


