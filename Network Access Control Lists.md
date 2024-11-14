---
tags:
  - NACL
---

Every subnet has a NACL
**NACLs filter traffic crossing a subnet boundary inbound and outbound. Does not affect inter-subnet packets**
A NACL is **stateless**
No aware of logical resources
You make a NACL for a VPC and then **associate it with a Subnet**
	Each subnet can only have one **NACL**
They contain rules. A rule is made up of...
	DST IP/Range
	DST Port
	Allow or Deny
	Rule Number
They have an implicit deny

Rules are processed by ascending rule number. Rules after the first match are ignored.
