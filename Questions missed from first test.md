* Look in to Health Checks and status checks
	An ELB is healthy if it is running and passing ELB health checks. A status check is a way to see if there are any software issues on and EC2 instance
* CWAgent?
	A way to log data about EC2 instances as well as on prem servers into CloudWatch. Setup an agent configuration and save to cloudwatch logs
* Review S3 storage classes. Transfer acceleration?
	storage tiers are pretty clear. Transfer acceleration uses edge locations
* Review ECS
	A managed container based compute service. Basically how we deploy containers in AWS. You can use EC2 mode or Fargate mode.
* DNS record types
	![[Route53#General DNS stuff]]
* What is cloudwatch? How about CloudTrail
	Cloudwatch is used for collecting operation data. CloudTrail logs api calls. Basically, use cloudWatch for metrics and CloudTrail for interactions.
* When to use IAM roles and when to use bucket policies. What are identity policies
	[[AWS Policy Overview]]
* EC2 connect vs session manager
	**EC2 Instance Connect** allows you to securely connect to EC2 instances over SSH using short-term credentials from the AWS Management Console or CLI, without needing to manage SSH keys. **Session Manager**, part of AWS Systems Manager, provides secure, browser-based or CLI-based shell access to EC2 instances without requiring SSH access or opening inbound ports, and it can also be used for logging, auditing, and access control.
* When is data from an ec2 instance lost?
	data is lost on termination (stop or hibernation) or hardware failure. Not on restart
* Review when to use snowball and when to use snowmobile
	Use snowball until you get to 10PB
* S3 cross-region replication
	By default replication is not retroactive and versioning needs to be on
	one-way replication. You can do bi-direction but it is a different feature
	You can replicate encrypted data but it required extra config
	Deletes will not be replicated by default
* SCP? Really I just need to create a system for how to chose what to use when trying to grant or restrict privilege from a resource
	[[AWS Policy Overview]]
* OAI? This may go with above but for S3
	![[CloudFront#Origin Access Identity (OAI)]]
* EIPs?
	An _Elastic IP address_ is a static IPv4 address designed for dynamic cloud computing. An Elastic IP address is allocated to your AWS account, and is yours until you release it. By using an Elastic IP address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account. Alternatively, you can specify the Elastic IP address in a DNS record for your domain, so that your domain points to your instance.
	You can access Elastic IPs from the public internet
* EC2 cluster placement group? How many and how are they launched
	These need to be launch at the same time and normally are the same instance type.
* RDS snapshots
	![[Relational Database Service#Backups|RDS]]
* Aurora?
	[[Aurora]] - Basically a version of [[Relational Database Service|RDS]]
* VPC peer and transit gateway for connecting two or more vpcs. Really, lets just get a detailed understanding of how networking works in aws
* Storage Gateway?
	[[Storage Gateway]]
* Different encryption types (SSE-C)
	Client-Side = object is encrypted on the user's machine
server-side = data is in its original form when it gets to S3. Then it is encrypted. Then it is stored
	AWS has made this mandatory. You can not store plaintext in S3
	Three different types of server side
	1) SSE-C - uses customer provided keys. The user provides the data and the key. S3 en/decrypts the data and then discards the data
	2) SSE-S3 - uses S3 managed keys. S3 generates and manages the keys.
	3) SSE-KMS - uses KMS keys stored in KMS keys. S3 interacts with KMS. You can manage permissions for the KMS key. This can be better than SSE-S3 in that it gives you more control.
* What is the point of cloudfront
	Use this when you need to serve content
* FSx
	FSx
* SQS polling types
	Short - gets the message as soon as they appear
	Long - will wait to poll if there are no messages on the queue
* TCP 22
	**TCP port 22** is primarily used for **SSH (Secure Shell)**