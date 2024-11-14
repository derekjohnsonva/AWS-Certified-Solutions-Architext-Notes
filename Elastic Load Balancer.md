---
aliases:
  - ELB
---
## Types of Load Balancers
3 Types of Load Balancers in AWS. There is a V1 (which you should avoid) and V2 (which you should use)
### Classic Load Balancer 
V1 Type
Not really [[Network Layers]] so you should not use
every unique HTTPS requires an individual SSL
### Application Load Balancer (ALB)
V2 type
User for HTTP/S/WS
True Layer 7 LB (listens on HTTP or HTTPS)
No unbroken SSL - can't do end to end unbroken encrypted data sharing
	This is because the data needs to be decrypted for the LB to know how to handle it
	This allows us to have a centralized SSL management point
Slower than NLB due to more levels of the network stack to process
They can evaluate application health (because they are layer 7)
Has a set of connection rules with a priority
### Network Load Balancer (NLB)
V2 Type
Used for TCP, TLS, UDB
They are a Leyer 4 device (no understanding of headers, cooking, or session stickiness)
They are very fast because they don't do upper layers of the stack
Use them when you don't need HTTP or HTTPS
No Health checks, just handshakes
Can have static IPs which is good for whitelisting
They can use unbroken encryption with TCP
## Architecture
Used with many types of compute (not only [[Elastic Compute Cloud|EC2]])
You need to pick 1 subnet in 2 or more availability zones
	The subnet needs to have 8 free IPs. This mean your minimum subnet size is probably going to be a `/27` (technically it could be `/28`)
When you provision a Load Balancer, you are running at least one Node in the subnet of each AZ you chose
An ELB is configured with an A DNS record. This means that pointing to a load balancer will in turn be pointed to the compute instances

Listener Configuration
	External nodes  = public IPs
	Internal = private IPs. Used to separate application tiers.

## Cross-Zone LB
It used to be that each load balancer node would get an even split of traffic
This is bad because different AZs will have different resource amounts
The fix for this is cross-zone LB
	Nodes can communicate with resources in other AZs

## Auto Scaling
[[Auto Scaling Groups]]

## SSL Offload
There are three ways that ELB can handle SSL
Bridging = The connection is terminated on the ELB and needs a new certificate for the domain name 
	 The load balancer has access to the HTTP traffic
	 SSL Certificate needs to be stored on the LB as well as the instance
	 
Pass Through = No decryption, the connection is passed to backend instance
	There is no certificate exposure to AWS
Offloading = Data is encrypted from the user to the ELB. It is then unencrypted and shared to the instances. This means there is no end to end encryption.

Stickiness generates a cookie which locks the device to a single backend instance

## Gateway Load Balancers (GWLB)
Often, you will have a security application running on an instance that will monitor traffic between your app server and the internet (i.e. firewall). However, scaling these instances can become difficult
GWLB uses a tunneling protocol call GENEVE

Traffic flow
user machine -> GWLB Endpoint -> GWLB -> Security application -> GWLB -> GWLB Endpoint -> Traffic destination

You are abstracting the security away