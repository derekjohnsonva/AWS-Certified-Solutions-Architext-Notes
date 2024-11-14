---
tags:
  - SG
---

Stateful
	You don't need to configure ephemeral ports
	An allowed request = allowed response
Implicit Deny
	Can not make an explicit deny
	Can't be used to block specific bad actors
		For this, we use [[Network Access Control Lists]]
They are able to reference logical resources
	This includes other security groups and itself. In this situation, "itself" refers to anything with the security group attached
They are attached to ENIs (Elastic Network Interface) not instances