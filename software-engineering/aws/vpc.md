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

