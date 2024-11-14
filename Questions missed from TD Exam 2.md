1 - easy mistake
2 - deep archive is cheaper so do that
3 - Use [[AWS Elastic MapReduce]]
4 - full load and change must be used to capture new changes
5 - interface endpoints vs gateway endpoints = IE don't work with dynamodb
18 - use glue when you are transforming
21 - only use kinesis if you are need real time streaming
22 - CORS = Cross Origin Resource Sharing. This is used when you need to access resources from a domain from another domain.
23 - Unless they mention it, assume that processing is being done on client side
24 - Config can enforce rules
25 - A Gateway endpoint is a type of VPC endpoint that provides reliable connectivity to Amazon S3 and DynamoDB without requiring an internet gateway or a NAT device for your VPC
26 - **S3 Object Lock in Compliance Mode** ensures that an object version cannot be overwritten or deleted by any user, including the root user of the AWS account. This mode is typically used for regulatory compliance purposes.
28 - **AWS Security Token Service (STS)** is the service that you can use to create and provide trusted users with temporary security credentials that can control access to your AWS resources
29 - ip addresses are not change, we jsut change cname records
34 - EBS stores backups to S3 not to RDS
35 - you really only use Simple Email Service when you need to send bulk emails
45 - peering is not trasitive.
51 - network load balancer for only allowing certain IPs
52 - Lambda@Edge is used to show different content to different users
60 - AWS does not want us to run DBs on EC2 instances
61 - invite child accounts to your organization



## Things to Remember
Use DataSync when you need to move a lot of data from on prem to the cloud (or vice versa) and use Cloud Gateway when you need continuous sync between on prem and cloud

WAF (Web Application Firewall) - Protects agains Layer 7 attacks, SQL injection, and Cross-Site Scripting

Bastion hosts are used in public subnets. For windows connection, use RDP

RDS Proxy helps to establish a pool of DataBase Connections