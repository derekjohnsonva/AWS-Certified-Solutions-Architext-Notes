---
aliases:
  - EFS
---
An AWS implementation of the NFSv4 Filesystem
These filesystems can be mounted in linux
	The data in the filesystems can be shared between many EC2 instances

Private service, via mount targets inside a VPC
	However, you can connect remotely using a VPN

The filesystems will use POSIX permissions
![[Pasted image 20240925172637.png | 400]]
