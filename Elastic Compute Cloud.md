---
aliases:
  - EC2
---
EC2 - Lots of questions on the exam
This is the default compute service
Private Service by default - Launches into a VPC network.
EC2 is AZ resilient

different instances have different sizes and capabilities
billing per second

Amazon Machine Image - AMI = A servers image that can be used to create virtual machines
	Comes with attached permissions: Public, owner, and explicit
	Also comes with root volumes - this is file storage
	Comes with a block device mapping - maps volumes for the device
## When to use EC2
traditional compute - you need an OS and applications
Great for long running compute
Server style applications
good for burst or steady-state load
Monolithic applications
Migrated application workloads
## Architecture
instances are [[Virtual Machines]].
Instances run on EC2 hosts. A host can be shared or dedicated. Obviously you have to pay more for dedicated hosts.
Instances will stay on a host unless AWS changes something or you stop and then restart the instance
	you can migrate an EC2 across AZs
### Instance Metadata
data the EC2 service provides to an instance
Access the metadata by accessing http://168.254.169.254/latest/meta-data/
You can get environment, networking, authentication, and user-data
This is not authenticated or encrypted on the instance
Assume that the metadata is exposed.
Use [this](https://aws.amazon.com/code/ec2-instance-metadata-query-tool/) tool to get metadata without doing curl requests
## Instance Types
What can change between instance types???
	Raw hardware resources
	Resource Ratios
	Storage and data bandwidth
	System architecture
	additional features (i.e. GPUs or FPGAs)
Difference EC2 categories
* General purpose - default
* Compute Optimized
* Memory Optimized
* Accelerated computing - GPUs/FPGAs
* Storage Optimized - good for io workloads
Naming system...
![[Pasted image 20240918100214.png | 400]]
Overview![[Pasted image 20240918100330.png | 600]]

## Storage
Two Options
1) Instance Store
	Provide temporary block storage devices for your instance. They are physically attached to the host computer.
	High storage performance.
	Included in the instance price
	They have to be attached at **Launch**
	You should only use this storage for temporary storage of info that changes frequently.
2) [[Elastic Block Store|EBS]]
### When to use each
Persistent storage? Use EBS
Resilience? Use EBS
Isolated from instance lifecycle? Use EBS
Resilience? it depends
High Performance? It depends
Super high performance? Instance Store
Cost? Instance Store
## Lunch Types
AKA Purchase Options
Order of Service - sometimes AWS will not have enough compute to cover the demand. This could be because of outages. In this case, the order of service is Reserved, On-Demand, Spot
### On-Demand
The default. No specific pros or cons. Isolated but customers share hardware. Instances consume defined allocation of resources. Does not give priority access. Pricing is predictable
### Spot
AWS sells unused EC2 host capacity at a discount. This price will be changing all the time. If the spot price goes above your max price, your instance will be terminated.
### Reserved
A commitment with AWS that you will pay for an instance type for a set amount of time. You will get resources at a reduced rate. You can reserve in an AZ or a Region. Reservations are for 1 or 3 years. You can pay all upfront, no upfront, or partial upfront. 
These are good for known, long term, consistent usage which don't run consistently.
	This is good for something like batch processing.

### Capacity Reservation
You use it when you need an absolute guarantee you'll have the compute available when you fail over after a zone or a region failure. No billing discount.
### Dedicated Instance
While your instance is running you own the hardware. Your instance may be moved around to different physical servers when it is stopped and restarted.
Generally dedicated hosts are used for applications which use physical core/socket licensing.
You can purchase on demand or with reserve options.

### Dedicated host
You pay for the host not the instance. Obviously more expensive. You also need to manage capacity.

## Billing Stuff
### EC2 Savings Plan
An hourly commitment for a 1 or 3 year term.
You commit to spend a minimum amount and you get services in that amount at a discounted rate.
After you spend all the money you reserved, you go back to using the normal rate.
You can have a savings plan for one service or a general product category
## System Health
Instance Status Checks - helps us to check to see if there are software issues with the instance (e.g. corrupted file system, OS Kernel Issues)
Auto Recovery = a way to recover from failed instance status checks
	We need to create an instance status check alarm inside of the EC2 console.

**Termination Protection** = a feature which adds an attribute to instances that means they cannot be terminated. This is good if junior admins may have access to the instances.

## Bootstrapping
The process of configuring an EC2 instance to perform automated install and configuration steps 'post launch' before an instance is brought into service.

Bootstrap using User-data which is accessed using meta-data
Anything in User Data is executed by the instance OS
	Only run at launch, not on restart.
	EC2 does not interpret, it will just run the user data
	This means it is not secure. Don't use for passwords or long term credentials
	Limited to 16kb
AWS::CloudFormation::Init is a configuration engine that lets you set desired state
	AKA: CNF Creation Policies
	Passed in through user data
	It allows you to use info about your [[CloudFormation]] stack in the bootstrapping of your EC2 instance
	This is a better way to bootstrap. It handles errors and timeouts more effectively.
	Checks that what you want to happen actually happened
### Instance Roles
![[Pasted image 20240922124114.png | 400]]
An IAM Role used for EC2 instances
Credentials are delivered in meta-data
automatically rotated - always valid
Always use instance roles instead of long term credentials

## Logging
[[CloudWatch]] is what we would first reach for when setting up logging
Unfortunately, CloudWatch can not do this without some additional setup
We need to set up a CloudWatch Agent
We need to setup an Agent Configuration as well as give the Instance Role access to CloudWatch Logs. 
A good place to store your CloudWatch Configuration file is [[Systems Manager Parameter Store|SSM Parameter Store]]
## Placement Groups
Normally, the location of the EC2 host is chosen by AWS
Placement groups allow you to chose host location
**Cluster** - Close together. Best for performance
	Can't span an AZ
	Normally, use same instance type
	Launch at same time
	10GBps single stream performance
**Spread** - Far apart. Best for resilience
	7 instances per AZ.
	Each instance on its own rack
	cant use dedicated instances or hosts
**Partition** - Close groups that are spread far apart.
	Max 7 partitions per AZ
	Each partition has its own racks
## Optimizations
### Enhanced Networking
Uses SR-IOV - the NIC is virtualization aware
required to use Partition Groups
No change
You get Higher I/O and more bandwidth
It seems like there really is no reason not to turn this on by default
### EBS Optimized
[[Elastic Block Store|EBS]] optimized means that some portion of the network has dedicated capacity for EBS.
Enabling costs extra

## Databases on EC2
This is normally bad practice
	There is a high admin overhead
	You need to handle Backup
	EC2 is in a single AZ
	EC2 is not optimized for DB performance
Why you may want to do it anyway
	You may need access to the OS of the machine running the DB
	You may need to do advanced DB tuning (DBROOT)
	You may want to run a DB that AWS does not provide