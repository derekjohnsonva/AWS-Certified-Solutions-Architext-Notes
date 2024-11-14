S3 is a proprietary storage technology and only way to expose S3 data on premise is using AWS Storage Gateway.

AWS Storage Gateway is a bridge between on-premise data and cloud data in S3. Our hybrid storage service will allow on-premises to seamlessly use the AWS Cloud (disaster recovery, backup & restore, tiered storage).

Types of Storage Gateway:
**S3 File Gateway** - offers file-based access to objects in Amazon S3. It allows us to store and retrieve objects in Amazon S3 using file protocols, such as NFS and SMB. Most recently used data is cached in the file gateway. It supports all S3 classes except S3 Glacier. Transition to S3 Glacier must be done using a Lifecycle Policy.
	To access our buckets we must create IAM role for each File Gateway. Also if we use SMB we can use its integration with Active Directory for user authentication.

**File Gateway** - offers native access to Amazon S3 for NFS and SMB (Linux and Windows) It has local cache for frequently accessed data. Bridges on-prem file storage and S3
![[Pasted image 20241003133406.png | 400]]
	We can use File Gateway in multiple regions to provide multi-region Disaaster Recovery
	Can be good to use [[Simple Storage Solution#Lifecycle Configuration|S3]] Lifecycles 


**Volume Gateway** - provides block storage to on-premises applications using iSCSI protocol, with data asynchronously backed up to AWS. 
There are two modes for Volume Gateway:
* Cached Volumes - frequently accessed data is cached locally, while the primary data is stored in S3. Use this as an extension of your local database.
* Stored Volumes - entire datasets are stored locally, with scheduled backups to S3. This is good for backups

**Tape Gateway** - enables us to use Amazon S3 and Glacier as a scalable, cost-effective solution for archival and backup data stored on physical tapes. It presents a virtual tape library (VTL) interface, compatible with leading backup software.
	Tape is good for things that will be written and read all at once
	Basically, we upload tapes to S3 and when then are not in use we put them in glacier
