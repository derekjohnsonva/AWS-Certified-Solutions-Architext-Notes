A way to register domains and host zones
**Global Service** - one of only a handful
zone file = a database that contains all of the DNS information about a particular domain
Name Servers = a type of DNS server that will use our Zone File
The basic flow for registering a domain..
1) Route 53 talks to a Domain Name Registry (i.e. .org registry) to get a new domain name zone
2) Route 53 creates a Zone File with this new domain name.
3) Route 53 puts this zone file on 4 Name Servers.
4) Route 53 tells the Domain Name Registry about the Name Servers.
5) The Registry will point traffic directed at the domain name registered earlier to the Name Servers

Hosted Zones = Zone files hosted on 4 AWS managed Name Servers
	Can be either a public or private zone
	 

## General DNS stuff
Types of **DNS Records**
A - maps host names to an IPV4 address
AAAA - maps host names to an IPV6 address
CNAME (Canonical Name) - Maps a host name to another host name. This can make it so we can map multiple host names to the same IP Address
MX - (The email one). Are made up of two things: priority (lower number = higher priority) and value.
TXT - Allows you to add arbitrary text to a domain. They help you prove domain ownership.  Can also be used to fight spam.
TTL (Time to Live) - Tells us how long a DNS resolver should cache a value.
## Public Hosted Zones
A zone can be public or private
A hosted zone in a DNS database for a domain
	Globally resilient
	Hosts DNS records
A Public hosted zone is a zone file hosted on public name servers(R53)
	Accessible from public internet
	Made up of 4 Name Servers per hosted zone
## Private Hosted Zones
Basically the same as private but not accessible to the public internet.
Specifies how you want to route traffic in an Amazon VPC
![[Pasted image 20240922161157.png | 500]]
## CNAME and Alias
CNAME maps a name to another name
	You can't use a CNAME for a domain apex (The root level of your domain)
An Alias record maps a name to an AWS record
	They are more flexible because they can be used for apex records.
	They are AWS specific
## Routing Policies
### Simple Routing
1 record per name. Each record can have multiple values. All values are returned in a random order. The client chooses one value.
Simple routing doesn't support health checks
Use it when you want to route requests towards one service
You can use simple routing policy for records in a private hosted zone.
### Failover Routing
We can add multiple records of the same name.
The primary record will be used unless it fails a [[Health Check]].
### Multi Value Routing
Lets you return multiple values in response to DNS queries.
When queried, up to 8 healthy records are returned to the client
	Each record is health checked
No a load balancer but can help to increase availability.
### Weighted Routing
Lets you return different resources in response to queries. The amount each route is returned is chosen by you
This is helpful for load balancing and testing new software (only give the new version to some users)
### Latency Routing
Use when you are trying to optimize for performance
AWS maintains a database of latency between the users location and the regions tagged in records
Serves the record with the lowest latency
### Geolocation Routing
Similar to latency routing in that it takes the users location in to account
Returns the most specific record or "No Answer"
	Records are tagged with "US State", country, content, or default
This is good for providing language specific content or restricting to certain countries.
Does not take distance in to account.
### Geoproximity Routing
route traffic based on the how close the resource is to the user.
You can route more traffic to a given resource by applying a "bias" value
	Bias expands or shrinks the geographic routing region.
## Interoperability
R53 has 2 jobs
1) Domain Registrar
2) Domain Hosting
But it does not have to do both of those jobs.
## DNSSEC in Route 53
![[Pasted image 20240924194910.png | 500]]
