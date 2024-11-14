---
aliases:
  - DX
---
A way to connect from your local network to an AWS Region
You will connect from Local Network => DX Location => AWS Region

When you pay for a DX Location you are really just paying for a Port Allocation
You can get a 1, 10, or 100 Gbps physical connection

You have no resilience because you are just paying for one connection
	You can add extra ports for a cost

Advantages
* High speeds
* Low latency

Architecture:
![[Pasted image 20241002104607.png]]
How is everything connected?
From AWS DX Router to AWS Region - Multiple high speed physical connections
AWS DX Router to Customer DX Router - Physical connection
Customer DX Router to Customer Premises - Network or a physical cable (there is some way to get fast routing by working with your ISP)

Direct Connect uses Virtual Interface (VIFs) to logically separate different types of traffic. There are three primary types:
1) Private VIF -  Used to connect to our VPC for accessing resources like EC2 instances, RDS databases, etc. Used when we want a private link between our on-premises environment and AWS.
2) Public VIF - Used to access AWS public services (e.g., S3, DynamoDB, etc.) over a private connection. Public VIFs connect to AWS public endpoints and can be used to route traffic to multiple AWS Regions.
3) Transit VIF - This allows us to connect multiple VPCs across different AWS Regions using a single connection and a transit gateway.

## Resilience
There is no resilience baked in to DX
You have to eliminate all single points of failure
These points of failure are cables, building, routers, etc...
Example of a high resilience architecture...
![[Pasted image 20241002105107.png]]

## Public VIF + VPN
Neither public or private VIFS offer any form of encryption.
Public VIFs+IPSec VPN is a way to provide access to private [[Virtual Private Cloud|VPC]] resources, using an encrypted [[IPSec]] tunnel for transit.
Your [[VPN]] Connection connects the on prem router to the DX location