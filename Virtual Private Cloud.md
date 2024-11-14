---
aliases:
  - VPC
---
## Overview
VPC gives you a logically isolated virtual network

VPC - There will be lots of questions on the exam
Regional Service
VPC = virtual network inside AWS
Regionally Resilient
Private and Isolated. Each VPC is isolated from other VPCs
Two types 
1) Default VPS - Can only have one
2) Custom VPCs

No traffic can cross VPC bounds.
Each VPC has a [[CIDR]] rage that defines the IP addresses that will be available.
The default VPC always has the same [[CIDR]] range
Redundancy comes from subnets across AZs
![[Pasted image 20240907145734.png | 500]]
Can only have one Default VPC per region
Some services assume that the default VPC will be available.
We don't really use the Default VPC because 
## Choosing IP Ranges
Considerations when designing a VPC
* What size should the VPC
* Are there networks we can't use
* Other VPCs
* Structure  = Tiers and availability zones
A VPC can be at the smallest /28 and max /16

VPCs can use both private CIDR blocks and public IPs
You can add optional secondary IPv4 blocks
You have optional single assigned IPv6 /56 CIDR Block
	With IPv6 you can not pick the subnet Range

### ENS in a VPC
Provided by [[Route53]]
Your VPC address is `Base IP + 2`
enableDnsHostnames - gives instances DNS Names
### Cantrill Recommendations
He says that you want to assume you will use 4 availability zone
thus, your VPC will be split into 4
Additionally, allocate a range in each subnet for Web, App, DB, Extra
Thus, you will have 16 subnets. This means you will use at most a /20 subnet
You should probably pick something in the range 10.16 - 10.127
[VPC Limits](https://docs.aws.amazon.com/vpc/latest/userguide/amazon-vpc-limits.html)
## Subnets
We should put different subnets into different availability zones for resiliency
One subnet can only be in one availability zone
IPv4 CIDR is a subset of the VPC CIDR
Cannot overlap with other subnets
Subnets can communicate with other subnets in the VPC
There are 5 IP addresses in each subnet that are reserved
1) starting address = network address
2) Network + 1 = VPC router
3) Network + 2 = Reserved for DNS
4) Network + 3 = reserved for future use
5) last IP in subnet = Broadcast address
DHCP options are set on a VPC
## VPC Routing
Every VPC has a VPC router
	A VPC has a main route table, the subnet default
When a request hits the route table it can match multiple destination.
	If this is the case, The higher  postfix (more specific) route will be matched
	When a hit happens, the route points to the target
	All route pages have at least one route - the local route
### Internet Gateway
region resilient. You don't need a gateway per AZ
1-1 relationship between internet gateway and a VPC
	A VPC may not have a gateway but a gateway will always have a VPC 
Runs from within the AWS public zone
gateways traffic between the VPC and the internet or AWS public zone
AWS handles the performance
How to use an IGW
1) create IGW
2) Attach IGW to VPC
3) Create custom Route Table (RT)
4) Associate RT
5) Default Routes -> IGW
The internet Gateway is the thing that will store a public IP address. Even if an AWS service makes it seem like that public address is associated with the instance of the service, the routing actually takes place in the internet gateway
## Bastion Host / Jumpbox
BH = Jumpbox: They are the same
Used to allow incoming management connections
You can configure them only accept incoming traffic from certain IP addresses. Also they can have authentication.
They used to be the only way to access private [[Elastic Compute Cloud|EC2]] instances

## Flow Logs
Used to capture metadata about packet flow and send this data to S3 or CloudWatch Logs
You can capture packets in a VPC, Subnet, or [[Elastic Network Interfaces|ENI]]
This can not happen in real time
![[Pasted image 20241001133604.png]]
srcaddr & dstaddr - identify problematic IP.  
srcport & dstport - identify problematic ports.  
protocol - ICMP=1, TCP=6, UDP=17
action - success or failure of the request due to Security Group/NACL.

Some data is excluded
* Time server requests
* Amazon DNS server
* etc...
## Egress-Only Internet Gateway
All IPv6 IPs are public (as opposed to IPv4 which chan have private addresses)
Egress-Only Internet Gateway is used for IPv6 only (similar to a NAT Gateway bur for IPv6). It allows outbound connections over IPv6 for instances in our VPC while preventing the internet to initiate an IPv6 connection to our instances. We must update the route tables.

## VPC endpoints
Used when you need to connect to public resources inside of a private VPC
### Gateway Endpoints
Provide private access to S3 and DynamoDB

You create a gateway endpoint for your service and associate it with one or more subnet within your VPC
When you add the endpoint to a subnet, a prefix list is added to the route table with the target of the gateway endpoint.
HA across all AZs in the region by default

Use Cases:
* Used when you have a private VPC and want them to be able to access public resources
* Used for S3 Buckets set to private only by allowing access only from a gateway endpoint.
### Interface Endpoints
Used to provide private access to all AWS Public Services
Not Highly available
Uses Security Groups and Endpoint Policies
Only support TCP and IPv4
Uses PrivateLink

Interface endpoints give you a new endpoint DNS name

## VPC Peering
A way to create an encrypted network link between **TWO** VPCs
Works across regions and accounts
VPC peering is not transitive. You have to explicitly create any connections

In order to get connectivity between VPCs, you need to both add a Peering connection and update the Route tables of the two VPCs. You may also need to update the security groups of the two VPCs


