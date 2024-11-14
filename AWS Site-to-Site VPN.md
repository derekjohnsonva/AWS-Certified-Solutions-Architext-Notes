Allows you to connect a VPC and an on-prem network
Fully HA - if you do it right
Takes less than an hour to provision

Uses a...
* Virtual Private Gateway (VGW)
* Customer Gateway (CGW)
* VPN Connection between the two

Will not be Highly Available if there is only one Customer Gateway because there would be a single point of failure.
To fix this, we need two customer gateways with their own IPs
![[Pasted image 20241002102658.png]]

Static vs Dynamic VPNs
	The difference is how routes are handles
	Static uses Static routes (not good for load balancing and multi connection failover)
	Dynamic used [[Border Gateway Protocol]]


VPN Considerations 
* Speed Limit of 1.25 Gbps
* There can be latency due to connecting over the open internet
* Quick to setup (Hours)
* Could be used as a backup for [[Direct Connect]]

