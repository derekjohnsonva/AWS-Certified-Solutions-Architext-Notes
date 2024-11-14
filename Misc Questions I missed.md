* When you connect to the read-replicas of RDS, you get load balancing for free
* If you are talking about an EC2 connection, you need to use Security Groups
* Raid 0 is faster but Raid 1 is more fault tolerant
* RDS Failover happens by changing CNAME
* Amazon EKS supports two autoscaling products, Karpenter and Cluster Autoscaler
* EC2 metrics that are automatically recorder = CPU, Network, Disk
* There is a V-CPU limit of on demand EC2 instances you can provision
* On-Demand Capacity Reservations enable you to reserve compute capacity for your Amazon EC2 instances in a specific Availability Zone for any duration
* IAM database authentication provides the following benefits:
	1. Network traffic to and from the database is encrypted using Secure Sockets Layer (SSL).
	2. You can use IAM to centrally manage access to your database resources, instead of managing access individually on each DB instance.
	3. For applications running on Amazon EC2, you can use profile credentials specific to your EC2 instance to access your database instead of a password, for greater security
* RDS Enhanced Monitoring gathers its metrics from an agent on the instance. Thus, if we are trying to get metrics about how different tasks are using memory or cpu, we need to use Enhanced monitoring instead of Cloudwatch.
* RDS events only provide operational events such as DB instance events, DB parameter group events, DB security group events, and DB snapshot events.
* A **VPC endpoint** allows you to privately connect your VPC to supported AWS and VPC endpoint services powered by AWS PrivateLink without needing an Internet gateway, NAT computer, VPN connection, or AWS Direct Connect connection