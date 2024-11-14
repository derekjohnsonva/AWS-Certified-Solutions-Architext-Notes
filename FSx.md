## For Windows File Server
Provides fully managed native windows file servers
Designed for integration with windows environments
integrates with [[AWS Directory Service]]
Single or Multi-AZ within a VPC
Can perform client side and AWS backups

How is this different from [[Elastic File System|EFS]]?
	Really the only difference is this is used for windows systems

**Key Features**
VSS - User-Driven file restores
Native file system over [SMB](https://en.wikipedia.org/wiki/Server_Message_Block)
Windows Permission Model
Support DFS
Managed service

## FSx For Lustre
Used for high performance computing workloads
A managed Linux Luster filesystem
Can scale to 100s of GB/s throughput
Scratch = highly optimised for short term
persistent = longer term, highly available but only in one AZ. It is self-healing

Data is lazy loaded into the filesystem from S3.
	Data is not in sync between FSx and S3

Metadata is stored on Metadata Targets (MST)
Objects are stored on object storage targets (OST)
![[Pasted image 20241003145416.png]]

Two types of deployment types 
1) Scratch - short term workloads. No HA, no replication
2) Persistent - Replication within one AZ. Auto heals if hardware fails. You can do backups to S3

