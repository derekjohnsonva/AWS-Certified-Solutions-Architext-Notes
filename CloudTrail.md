a product which logs API calls and account events as CloudTrail Events
90 days of storage by default - only store management events
To customize the service you create Trails
There are two types of data stored in CloudTrail
	Management Events = Info about management operations on services (i.e. creating and [[Elastic Compute Cloud|EC2]] instance). The default evens
	Data Events = show the resource operations performed on or within a resource in your AWS account (i.e. API call to [[Simple Storage Solution|S3]]). Need to be turned on. Cost more to store

A trail can be created as a one region trail or an all region trail
	A trail can only ever collect events from one region. An all region trail is just a collection of region trails that share metrics
Most services log events to the region they are in.
Global services (e.g. IAM) log to US-East-1
CloudTrail stores data as compressed JSON in [[Simple Storage Solution|S3]]
	Also can store to CloudWatch Logs
organizational trail = stores management events for all accounts in the organization
**Not real time Logging**
