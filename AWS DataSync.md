is used to automate and accelerate the replication of data and move large amount of data to and from on-premises to AWS (need agent) or AWS to AWS. It can synchronize to S3, EFS and FSx. Replication tasks can be scheduled hourly, daily or weekly.

**Task** = job that defines what is being synced, how fast, and Location
**Agent** = Software use to read or write data
**Location** = Where it will come from and where it will go to

File permissions and metadata are preserved (NFS POSIX, SMB...).
One agent task can use 10 Gbps and we can setup a bandwidth limit.

The DataSync agent can route DataSync traffic from the on-premises storage system (source location) to the [[Direct Connect|DX]] connection.

**Key Features**
* Scalable
* Bandwidth Limiters
* Incremental
* Compression
* Encryption
* Auto recovery
* AWS Service integrations
![[Pasted image 20241003142219.png | 500]]
You need to have a Local DataSync Agent
