Resources to go over

- [ ] [AWS Well-Architected](https://wa.aws.amazon.com/wellarchitected/2020-07-02T19-33-23/wat.map.en.html)

I will be using the cantrill course to self study

[https://learn.cantrill.io/courses/](https://learn.cantrill.io/courses/)

[[Setting up New Account]]

[[Account Details]]

[[IAM Service]]

Public Vs Private zone

public zone services are ones that can be accessed from public endpoints (such as [[Simple Storage Solution|s3]])

Private services have are inside of virtual private zones and can not be accessed by the public internet (such as [[Elastic Compute Cloud|ec2]]). You can set up a way for the public internet to access private services but they will have to go through the public zone. An example of this is setting up up public ip for an [[Elastic Compute Cloud|ec2]] instance.

Regions - the different places around the world you can deploy aws services.

Availability Zones (AZ) - isolated infrastructure inside a region. Placing services across AZs make them resilient.

Local Zones - A type of infrastructure deployment that places AWS services close to large population centers

Different services handle local zones differently. Some don't use them

Use them if you need extremely low latency

They support [[Direct Connect|DX]]

They can be an extension of a regions [[Virtual Private Cloud|VPC]]

Resilience Levels: These are helpful to know because they come up on the exam

1) Globally resilient - would take all regions to fail for it to fail. Ex = IAM

2) Region Resilient - separate services in each region. AZ can fail but the service will not fail

3) AZ resilient - if an AZ fails the service will fail.

[[Virtual Private Cloud]]

[[Elastic Compute Cloud]]

[[Simple Storage Solution]]

[[CloudFormation]]

[[CloudWatch]]

AWS has what is called a shared responsibility model. They are responsible for the security _of_ the cloud and the user is responsibility _in_ the cloud.

![[Pasted image 20240911131833.png | 400]]

High Availability (HA) = We are aiming to optimize for uptime. Does not mean it is always available.

Fault-Tolerance (FT) = The system will continue to operate properly even when some components fail. This is different because it means that there can be no downtime. The system must always be available

Disaster Recover (DR) = things that help us recover after a natural or human induced disaster.

[[Route53]]

[[Key Management Service]]

[[AWS Organizations]]

[[CloudWatch]] - Logs

[[CloudTrail]]

[[Control Tower]]

In order to get a better idea of networking inside of [[VPC]]s, we go over some stuff...

[[Stateful vs Stateless Firewalls]]

[[Network Access Control Lists]]

[[Security Groups]]

[[Network Address Translation|NAT]]

EC2 Stuff

[[Virtualization]]

[[Storage]]

[[Elastic Block Store]]

[[Elastic Network Interfaces]]

[[Amazon Machine Image]]

Container Stuff

[[Containers]]

[[Elastic Container Service]]

[[Kubernetes]]

Advanced EC2

[[Elastic Compute Cloud|EC2]]

[[Systems Manager Parameter Store]]

[[Relational Database Service]]

[[Aurora]]

[[Database Migration Service]]

[[Elastic File System]]

[[AWS Backup]]

[[Elastic Load Balancer]]

Event Driven Architecture

No constant running or waiting for things

Producers generate events when something happens

events are delivered to consumers

actions are taken and the system returns to waiting

[[Lambda]]

[[Simple Notification Service]]

[[Step Functions]]

[[AWS Simple WorkFlow]]

[[API Gateway]]

[[Simple Queue Service]]

[[Kinesis]]

[[Cognito]]

[[AWS Glue]]

[[Amazon MQ]]

[[AppFlow]]

Global Content and Delivery

[[CloudFront]]

[[AWS Certificate Manager]]

[[Global Accelerator]]

[[Border Gateway Protocol]]

[[IPSec]]

[[AWS Site-to-Site VPN]]

[[Direct Connect]]

[[AWS Transit Gateway]]

[[Storage Gateway]]

[[Snowball]]

[[AWS Directory Service]]

[[AWS DataSync]]

[[FSx]]

[[AWS Transfer Family]]

[[Secrets Manager]]

[[Web Application Firewall]]

[[AWS Shield]]

[[CloudHSM]]

[[AWS Config]]

[[Macie]]

[[Amazon Inspector]]

[[AWS GuardDuty]]

Database stuff

[[DynamoDB]]

[[Amazon Athena]]

[[ElastiCache]]

[[Redshift]]

ML Stuff

[[Amazon Comprehend]]

[[Amazon Kendra]]

[[Amazon Lex]]

[[Amazon Polly]]

[[Amazon Rekognition]]

[[Amazon Textract]]

[[Amazon Transcribe]]

[[Amazon Translate]]

[[Amazon Forecast]]

[[Amazon Fraud Detector]]

[[SageMaker]]

## Exam Specific Stuff

Cantrill says to go through questions and do the questions you can answer immediately first (approx. 25%), then do the medium questions, and finally use remaining time on the hardest questions (hardest 25%)

Exam questions start with 1-2 lines of preamble - skip this part most of the time

The question itself is what follows

Normally 4-5 multi choice or multi select

usually one question can be excluded

Plan for study

Cantrill tests

- [x] #task First test no studying ✅ 2024-10-14
- [x] #task Make a list of missed questions and identify problem areas ✅ 2024-10-14
- [x] #task Study problem areas ✅ 2024-10-16
- [x] #task Take second test ✅ 2024-10-16
- [x] #task Look into Tutorials Dojo ✅ 2024-10-16

[[Questions missed from first test]]
[[Knowledge from examtopics questions]]
[[Questions missed from TD Exam 2]]
[[Questions missed from TD Exam 3]]
[[Misc Questions I missed]]

Things to pay attention to when taking the test
* When it asks for multiple options, understand if they are happening in series or in parallel.

## Test
I thought the test went well. I got like 840 out of 1000 which seems like a pretty good grade. Topics I thought were overrepresented
* VPCs and how to connect them
* RDS (specifically Proxies)
* Load Balancers (ALB vs NLB)
* Billing
* Organizational Units
* Web Application Firewalls
Things I was surprised not to be asked about
* CloudHSM
* FSx
* Any ML stuff really
* SQS vs SMS

[[Article about Certification Journey]]