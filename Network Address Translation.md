---
aliases:
  - NAT
---
A set of processes - remapping SRC or DST IPs
	Translates public to private (and reverse) IPs
IP masquerading = hiding CIDR Blocks behind **One IP**
Gives Private CIDR range outgoing internet access
**Needs to run from a public subnet**
Uses **Elastic IPs** (static IPv4s): Can't use IPv6
AZ resilient Service (high availability in each AZ)
	If you want region resilience make a NAT Gateway in each AZ

Billed hourly and for data volume

Basically, you use a NAT when you want to give instances in a private subnet connection to services outside your VPC without giving external services a connection to those services

The NAT Gateway still needs to talk to the Internet Gateway before it can access the public internet