---
aliases:
  - S3
---
Regional Resilience - AZ redundancy
Public service - it can be accessed from the public internet
Storage for anything and is pretty cheap
## General
S3 does storage using objects and buckets
### Objects
An object is a file conceptually.
Each object has a key (like a filename) and a value (the sequence of binary data). The value can be from **zero bytes to 5TB**

### Buckets
Buckets store objects
Each bucket is stored in a region. The data will never leave the region unless you configure it to do so
The bucket name needs to be globally unique (across all regions and users)
A bucket can store unlimited objects
Everything in the bucket is stored in a flat structure. This means there are no folders. We can make it look like there are folders by prefixing file names with `/foldername/`
Bucket name info
1) globally unique
2) 3-63 lower cane no underscore characters
3) start with letter or number
4) cant be ip formatted

Can only have 100 buckets (soft limit. Hard limit at 1000)

### Patterns and Anti-Patterns
Object storage. Not a file or block storage
You can't mound an s3 bucket
Great for larde scale data storage
Great for offloading data from a compute instance
Use S3 as an input or output for many aws products

## Security
S3 is Private by default. The root user is the only user with default access.
Bucket Policies - A form of [[Resource Policies]]. Like an identity policy but attached to a bucket.
	allow/deny same or different accounts
	allow/deny anonymous principals
	[example](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies.html)
	If we need to provide access to anonymous users, we will use a bucket policy
	We can apply a `"Condition"` to the bucket policy

The other form of S3 security is ACLs (Access Control Lists). They are legacy and you should not use them anymore
	They are not very flexible which is why people don't use them anymore. Below is all they can do
	![[Pasted image 20240912095225.png | 500]]

Block Public Access - Created recently to avoid accidentally allowing the public to access your S3 contents.
	This is a seperate step from you Bucket Policy or your Identity Policy.
	It only applies to Public and Anonymous users.
	Done in the console when you create the bucket and can be changed after creation

### Security Overview
What type of policy should we use???
Controlling different resources - Identity Pol
You have a preference for IAM - Identity Pol
Same account - Identity Pol
Just controlling S3 - Bucket
Anonymous or Cross Account - Bucket


## Static Website Hosting
All you need to do is enable SWH and then add an Index and an Error page.
	These are HTML documents.
A website endpoint will be automatically generated. You can use a custom name but it needs to match your bucket name.

**Offloading**
	We use offloading when we have data that will be accessed by a dynamic webpage. The webpage may change but it will be pointing to static data. Thus, we can offload that static data to S3 and just point to it using our dynamic webpage.

**Out-of-band Pages**
	If the dynamic website is not working, we can point to a static version of the site on S3

## Object Versioning
This takes place on a bucket level
Once  object versioning is turned on for a bucket it can **Never Be Turned Off**. It can only be suspended
Versioning allows you to store multiple versions of an object. Does this by assigning a `version-id` field to every object you store.
This makes things more expensive because space is consumed for all versions

MFA Delete - means the MFA is required to change bucket versioning state or delete versions

## Storage Classes
![[S3 Object Storage Classes]]
## Performance Optimizations
Multipart Upload - breaks data up and uploads it separate. This is faster and safer.
	Data has to be > 100MB
	10,000 max parts. Each part between 5MB - 5GB

Accelerated Transfer
	When we are down/uploading, data may not take the fastest route. May have to pass through different regions
	AT used edge locations in order to not transit data as far. Each edge location will communicate directly with your bucket across regions.
	Enable it by creating a bucket and going to properties. It will give you a **new endpoint**
## Encryption
We don't encrypt buckets, we encrypt objects

We can either do Client-Side or Server-Side Encryption
Client-Side = object is encrypted on the user's machine
server-side = data is in its original form when it gets to S3. Then it is encrypted. Then it is stored
	AWS has made this mandatory. You can not store plaintext in S3
	Three different types of server side
	1) SSE-C - uses customer provided keys. The user provides the data and the key. S3 en/decrypts the data and then discards the data
	2) SSE-S3 - uses S3 managed keys. S3 generates and manages the keys.
	3) SSE-KMS - uses KMS keys stored in KMS keys. S3 interacts with KMS. You can manage permissions for the KMS key. This can be better than SSE-S3 in that it gives you more control.
![[Pasted image 20240913094153.png | 400]]

[https://docs.aws.amazon.com/AmazonS3/latest/user-guide/default-bucket-encryption.html](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/default-bucket-encryption.html)
[https://docs.aws.amazon.com/kms/latest/developerguide/services-s3.html](https://docs.aws.amazon.com/kms/latest/developerguide/services-s3.html)
[https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html)
[https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html)
[https://docs.aws.amazon.com/AmazonS3/latest/dev/ServerSideEncryptionCustomerKeys.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/ServerSideEncryptionCustomerKeys.html)
### Bucket Keys
The issue with SSE-KMS is that S3 has to communicate with KMS every time you want to get anything in or out of S3. This means you are storing extra data and can have throttling issues with KMS. Bucket Keys help this.
KMS gives the bucket a **Bucket Key**. All objects in S3 use that same bucket key for en/de.
works with replication
## Features
### Lifecycle Configuration
a set of rules
rules consist of actions on a bucket or group of object
**Transaction actions** - when to move things to a new [[S3 Object Storage Classes]]
	All storage classes can transition into a lower class except for One Zone-IA can not transition into Glacier Instant Retrieval
	If objects are stored in S3 standard and you want to move to Standard-IA to One Zone-IA you must wait 30 days before transitioning.
	A single rule cannot transition to Standard-IA or One Zone-IA and THEN to glacier classes within 30 days (duration minimums)
**expiration action** - when to delete object

### Replication
S3 has two replication features which allow objects to be replicated between SOURCE and DESTINATION buckets in the same or different AWS accounts
**Cross-Region Replication** (CRR) = the process used when Source and Destination are in different AWS regions
**Same-Region Replication** (SRR) = used when the buckets are in the same region.
replication will default to maintain the storage class but this can be changed
Replication Time control - guarantees how long it will take to replicate
https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html
By default replication is not retroactive and versioning needs to be on
one-way replication. You can do bi-direction but it is a different feature
You can replicate encrypted data but it required extra config
Deletes will not be replicated by default
#### Why use replication
aggregation (SRR)
Prod and test sync (SRR)
in order to increase resilience (SRR)
global resilience (CRR)
reduce latency (CRR)


### Presigned URLs
Give other people access to resources in your AWS bucket using your credentials in a safe and secure way
presigned urls will expire after a user defined set of time
They can be used for put or get requests
They are helpful if you want to give a user access to a media bucket
You can create a presigned URL for an object you have no access to. It just won't have any access
Don't generate with a role because the URL will stop working when the temporary credentials expire

### Select
Sometimes you don't want to download all of the data for an S3 object
With Amazon S3 Select, you can use structured query language (SQL) statements to filter the contents of an Amazon S3 object and retrieve only the subset of data that you need. By using Amazon S3 Select to filter this data, you can reduce the amount of data that Amazon S3 transfers, which reduces the cost and latency to retrieve this data.

### Access Logs
access logging provides detailed records for the requests that are made to a bucket
useful for understanding patterns and security audits
### Object Lock
lets you store objects using a write-once-read-many(WORM) model
	No deletes, no overwrites
requires versioning to be turned on
You can define object lock in two ways...
1) Retention Period - specifying a number of days/year to retain the data. Two modes
	1) Compliance mode - can't be adjusted during the retention period
	2) Governance mode - can be adjusted by certain users
2) Legal Hold - you only set it to ON of OFF. You can not change or delete until the Legal Hold has been turned off
### Access Points
Sometime you may have many different types of users with different levels of permissions accessing a bucket. Access points are basically masks around a bucket that can have access policies assigned to them individually. They all eventually dump to the same bucket but to the user of the bucket they look different.
They have unique DNS addresses (different than the bucket)
The bucket policies will still apply
https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-points-vpc.html