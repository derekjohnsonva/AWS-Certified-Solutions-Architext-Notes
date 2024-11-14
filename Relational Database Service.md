---
aliases:
  - RDS
---
A type of [[Databases]] offered by AWS
## Architecture
You pay for RDS and receive a Database Server
You can use several different DBs
* MySQL
* MariaDB
* PostgreSQL
* Oracle
* Microsoft SQL Server

Runs in subnets inside a VPC
	**Subnet Group** = what subnets RDS will use
	Will have a **primary server** and a standby **server**. These two servers will be located in different AZs in your subnet group.
	These subnets can be public meaning you can access the database from the public internet. This is bad practice though
	Each instance (primary and standby) has its own storage (provided by [[Elastic Block Store|EBS]])
	**Read Replicas** are a third type of server. It can exist in the subnet group or in another region. It uses Asynchronous Replication
	You can also use Backups which are saved to [[Simple Storage Solution|S3]]
Typical Architecture Diagram
![[Pasted image 20240925085137.png | 400]]
## Costs
You are not billed by your usage, you are billed on resource allocation (how much resources you take up)
Costs...
* Instance size and type
* Multi AZ is extra
* Storage type and amount
* Data transferred
* Backups and snapshots
* licensing (some DBs have a usage fee)
## High Availability
Historically, the only way to provide high availability was with MultiAZ (replicating data in a Standby server in another area zone)
	The replication is abstracted away. It is done differently in each DB type
You would access data using the Database CNAME.
	This CNAME would always point to the Primary instance until there was some sort of failure. At the failure point, the CNAME would change to point to Standby
There an only be one Standby replica
Failure will take 60-120 seconds
Backups are taken from the standby

A new way to get high availability is Multi AZ **Cluster** mode
There are 2 DB server types, Writers (1) and Readers(2), all in different AZs
They have..
	Cluster Endpoints - point to Writer, can be used for reads and writes
	Reader Endpoints - points to the Reader
	Instance endpoints - points to specific instance for testing
This will run on faster hardware
Replication is done using transactions logs
Failover takes ~35s + transaction log application time
Writes are committed when 1 reader has confirmed
## Backups
Automatic Backups = Transaction logs every 5 minutes so you can perform a point in time backup
	Stored in S3
	Have a 0-35 day retention policy
Snapshots = performed manually and live past the termination of an RDS instance
	Can be restored, but create a new RDS instance. This is a long process

Normally, Automatic Backups are much better
## Read Replicas
This is not the same as the Reader endpoint of a Cluster.
Read Replicas = separate instances that will store the same data
	You can have 5 per Primary Instance
	Cross region or same region
	The DB does not have knowledge of Read Replicas
	Read Replicas can have their own Read Replicas - however lag is an issue
These are good if you do more reads than writes.
## Security
volume encryption using [[Key Management Service|KMS]] can be handled on the host
	encryption can not be turned off once it is on
	The database really has no clue that it is storing encrypted data, that is all handled by the host.
MSSQL and Oracle suport Transparent Data Encryption
	encryption is handled by the DB
	These are very strong encryptions
You can configure to allow IAM Authentication
	Uses tokens created by IAM (changed every 15 min)
## Custom
Amazon RDS Custom is a managed database service for applications that require customization of the underlying operating system and database environment. Benefits of RDS automation with the access needed for legacy, packaged, and custom applications.
	Basically, you have some extra customization and can connect to the instance using SSH

## Proxy
Why would you need Proxy? 
	Establishing a connection consumes resources
A proxy establishes a pool of connections to a database
	This way users can connect to the proxy and the proxy can give them access to a connection
	You can have more connections to a proxy than connection from the proxy to the DB
 When to use Proxy
 * Too many connection errors
 * Small DB instances
 * Useful for Lambda
 * when you need low latency
 * When you need high resilience
 * Reduces the failover time (by over 60%)
 