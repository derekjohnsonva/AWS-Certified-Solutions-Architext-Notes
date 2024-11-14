Used to protect against DDOS Attacks
Two types
1) Standard - free
2) Advanced - has a cost

protects against...
* Volumetric attacks (L3) - saturate capacity
* Protocol Attacks (L4) - TCP SYN Flood
* Application Attacks (L7) - web request floods

Shield Standard
	Helps prevent L3 and L4 attacks
	Can not be modified
	Runs automatically
	Protects [[CloudFront]], [[Global Accelerator]], [[Route53]]

Shield Advanced
	$3,000 per month
	protects almost everything on the perimeter of your network
	Must be explicitly configured
	Cost protection for unmitigated attacks (sort of like insurance)
	You get access to the AWS Shield Response Team
	Protects against L7 attacks (using [[Web Application Firewall]])
	Health-based detection