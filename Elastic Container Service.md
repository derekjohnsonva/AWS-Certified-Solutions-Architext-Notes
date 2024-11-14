---
aliases:
  - ECS
---
A managed, container based compute service

Container Definition = Tells ECS where your container definition is and what port it will use
Task Definition = Represents a self contained application. A task may use multiple containers. Specify security roles (Task Role) and Resources
Task Role = Best practice way to give containers in ECS permissions. The IAM Role which the task assumes
Service Definition = Lets us scale tasks. How many copies, how to do restarts.

When should we use ECS?
	If you use containers you should definitely use ECS
## Cluster Modes
This is the infrastructure you will run your containers on.
* [[Elastic Compute Cloud|EC2]] Mode - With EC2 mode you pay for the EC2 instances regardless of container usage. This is good if you need to manage the container hosts
* [[Fargate]] Mode - Fargate mode uses shared AWS infrastructure, and ENI's which are injected into your VPC. You don't have to manage container hosts. You will only pay for containers that you are not using.
* On Premises VM - Not common
When to use each
	If you have Large workloads and are price conscious use EC2
	If you have Large workloads and are overhead conscious use Fargate
	Small/burst = Fargate
	Batch/Periodic = Fargate
## Elastic Container Registry (ECR)
This is like Docker Hub but for AWS
A managed container image registry
Each AWS account has a public and private registry
Why would you use ECR and not Docker Hub?
	it comes with [[IAM Service| IAM]] 
	it has image scanning to check for vulnerabilities
	Gives you real time metrics in [[CloudWatch]] 
	Logs to [[CloudTrail]] 
	Stores events in EventBridge
