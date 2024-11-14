Default is..
## S3 standard
objects are replicated across at least 3 Area Zones in the AWS Region
This give you 11 9 redundancy.
Storage fee, transfer out fee, price per 1,000 requests.
Data is available in milliseconds

Use S3 when you need data instantly and need to make sure it is never lost.
## S3 Standard Infrequent Access
durability, stability, and latency is the same
Storage cost is less
This is done because their is now a retrieval fee for each GB of data you get out of S3
minimum capacity of 128kb per object
minimum of 30 days for storage

Don't use for temp data, small data, or data that is accessed a lot
## S3 One Zone Infrequent Access
Similar to standard IA but it is only stored in one AZ
Still has replication but only across one AZ

Use this for intermediary data.
## Glacier - Instant
like standard-IA except cheaper storage, more expensive retrieval, longer minimum
Still instant access to data
90 day minimum storage
## Glacier Flexible
similar to glacier instant except the objects are cold (they are not immediately available)
objects are really just pointers to objects. This means that any data requires a retrieval process into **S3 Standard-IA**
	The retrieval process comes in 3 flavors
	1) expedited (1-5 min)
	2) standard - 3-5 hours
	3) bulk 5-12 hours
	faster = more expensive
40 kb minimum size
## Glacier Deep Archive
Cheapest storage
40kb min size
180 day min duration
requires a retrieval into Standard-IA
	Standard - 12 hours
	bulk - 48 hours
## Intelligent-Tiering
actually has 5 different storage tiers
1) frequent access
2) infrequent access
3) archive instant access
4) archive access (optional)
5) deep archive (optional)
The tier is determined by how often it is accessed.
Cost is in the form of a management fee.
designed for long lived data with unknown access patterns

