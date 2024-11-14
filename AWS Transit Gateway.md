---
aliases:
  - TGW
---
Network Transit Hub - Connects VPC to on premises Networks
This reduces network complexity
Basically, you use this if you have multiple [[VPC]]s that you want to connect to your Client Gateway. It is an inter-VPC router
It can be used to peer VPCs in the same account, different account, same or different region and supports transitive routing between networks.
You can also peer Transit Gateways to other Transit Gateways

This is not necessarily faster but it has more predictable latency because it is not using the public internet

Considerations
* Supports transitive routing
* Can be used to create global networks
* Share between accounts using AWS RAM
* Peer across account
* Less complexity than not using it
* 
