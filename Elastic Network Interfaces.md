---
aliases:
  - ENI
---
Every EC2 instance has one (Primary) ENI
You can have secondary ENIs they just have to be in the same AZ
	These can be detached from the instance and attached to other instances
A Network Interface has
	Mac Address
	Primary IPv4 Private IP
	0 or more secondary IPs, Public IPv4, Private Elastic IP, IPv6, and Security groups
	Source/Destination Checks
 The public IP that an instance is given is dynamic
	 you need an elastic IP if you want it to stay the same
