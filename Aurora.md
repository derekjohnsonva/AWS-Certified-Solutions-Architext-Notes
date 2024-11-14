It is technically a variation of [[Relational Database Service|RDS]]
However, the architecture is very different

Aurora uses Clusters with a single primary instance and 0 to many replicas (15 replicas in an AZ with a Primary instance)
There is no local storage. Uses a cluster volume
	This is better for availability and performance
Example Architecture =
![[Pasted image 20240925152258.png | 300]]
The Cluster Volume is SSD Based
Storage is billed based on usage

You have two endpoints
Cluster Endpoint - Points to the primary for read and writes
Reader Endpoint - Points to the replicas (load balanced)

**Backups** in Aurora work the same as RDS
**Restores** create a new cluster
**Backtracks** can offer in-place rewinds
**Fast Clones** make database cloning much faster by using copy-on-write

## Serverless
Makes it so you don't need to manage the database instances (provisioning)
Scaling is done using Aurora Capacity Units (ACU)
The service can go to 0 and be paused

The architecture is the same but you are getting hardware from a shared pool
Applications will connect to something called a **Proxy Fleet**. This Proxy Fleet will then connect to the ACU
### Use Cases
Infrequently used applications (because it scales to 0 so well)
New application - since you don't know how much capacity you will need
Unpredictable or Variable workloads

## Global Database
a feature of Aurora Provisioned clusters which allow data to be replicated globally providing significant RPO and RTO improvements for business continuity and disaster recovery planning.

Replication occurs at the storage layer and is generally ~1second between all AWS regions.
	This is good for Global read scaling

Secondary regions can have 16 replicas
Currently a max of  5 secondary regions 

## Multi-Master
A way to give us multiple writers. All instances are capable of reading and writing
An application will connect to the DB instance
	There is no longer any load balancing that takes place.
When to use Multi-Master
1) High Availability for Writes
2) Increased Write Scalability
3) Fault Tolerance
4) Geo-Distributed Applications
5) Multi-Region DR Strategy
However there is more complexity as there needs to be conflict resolution between masters