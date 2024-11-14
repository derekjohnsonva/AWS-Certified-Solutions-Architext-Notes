---
aliases:
  - WAF
---
This is AWS's implementation of [[L7 Firewalls]]

You need to associate a WAF with a WEB Access Control List (ACL)

Protects agains Layer 7 attacks, SQL injection, and Cross-Site Scripting

Can be used to secure [[CloudFront]], [[API Gateway]], ALB
## WEB Access Control Lists (ACL)
The ACL will protect against bots and attackers
An ACL can either be explicit allow or explicit block
It can also be used for both global and regional services
On their own, they don't do anything. They need rule groups and rules.
Each rule takes some amount of compute
An ACL has a limited number of resources to process rules
A resource can only have one WEB ACL

Rule Groups contain rules
	They con't have default actions.
	They can be referenced by multiple WEB ACLs
	they have a WCU capacity 

Rules consist of a Type, Statement, and Action
	Type: Regular or Rate-Based. Rate-based rules will be triggered after a certain number of connections
	Statement: (What to match) or (count) or (What & Count)
		Can have multiple statements joined by `and` `or` `not`
	Action: Allow, Block, count, captcha, custom response, label
Labels can be referenced later on in a WEB ACL

