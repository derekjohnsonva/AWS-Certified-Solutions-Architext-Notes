---
aliases:
  - EBS
---
EBS is Block Storage (see [[Storage]])
	They can be encrypted
They are used with [[Elastic Compute Cloud|EC2]] instances
	An instance can only attach to storage in the same availability zone
	An instance sees block devices and creates a file system
Storage is provisioned in one availability zone
	It is resilient in that AZ
You can attach to one EC2 instance over a storage network
	There is a way to attach to multiple instances but this is not normal
	They can be detached and then reattached to another
Snapshots are backups stored in S3. This gives us resilience across AZs
Billed for GB per month

EBS is typically used for database workloads
## Volume Types
General Purpose SSD (GP2)
	size between 1GB - 16TB
	flexible and usable for general storage
	good for boot volumes
	
General Purpose SSD (GP3)
	size between 1GB - 16TB
	3000 IOPS and 125 MiB/s - Standard
	Up to 16,000 IPS or 1,000 MiB/s for extra fee
	Probably should be the new default
Provisioned IPS SSD (io1/2)
	Provides high performance for low latency workloads
	64,000 iops per volume
	1000 mB/s throughput
	4GB-16TB
	Lets you have high performance with a small size
Throughput Optimized HDD (st1)
	A low-cost HDD designed for frequently accessed, throughput-intensive workloads.
	You pay for MB per second
	Used for Big data with frequent access
Cold HDD (sc1) 
	The lowest-cost HDD design for less frequently accessed workloads.
Instance Store
	Provide temporary block storage devices for your instance. They are physically attached to the host computer.
	High storage performance.
	Included in the instance price
	They have to be attached at **Launch**
	You should only use this storage for temporary storage of info that changes frequently.
### When to use different volumes
**Needed for EXAM**
Cheap = ST1 or SC1
Throughput/Streaming = ST1
Boot = Not ST1 or SC1
up to 16,000 IOPS = GP2/3
up to 64,000 IOPS = IO1/2
260,000 IOPS = RAID0 + EBS
more than 260,000 IOPS = Instance Store

![[Pasted image 20241021135057.png]]
## Snapshots
Incremental volume copies to S3
	The first snapshot is a full backup
	Any snapshot over this will keep track of the $\Delta$ between the snapshots 
	A good way to clone a volume (for moving between AZs and regions)
If you use a snapshot to restore a volume it will lazy load the data
	You can use Fast Snapshot Restore to get around this
Billed by Gigabyte-Month of used data
## Encryption
EBS uses [[KMS]] keys to encrypt data on a volume
Data is stored in an encrypted state and can only be translated to plaintext on the EC2 hose
Snapshots of encrypted volumes are stored in an encrypted state (using a data encryption key)
This is not more expensive so you should prob do it by default
you can Encrypt by Default using a default KMS key
Each volume uses 1 unique DEK
Once a volume is encrypted, it can not be unencrypted


