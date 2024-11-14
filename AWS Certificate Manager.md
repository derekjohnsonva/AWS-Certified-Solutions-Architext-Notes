---
aliases:
  - ACM
---
Digital certificates prove web identity. The certificate is signed by a trusted authority and is thus more trustworthy.

ACM let you run a public or private Certificate Authority
	If you use private, applications need to trust your private CA

ACM can generate or import certificates
	generated certs will automatically renew
Certs can be deployed out to supported services
	[[CloudFront]] but not [[Elastic Compute Cloud|EC2]]

ACM is a regional service
	Certs cannot leave the region they are generated or imported in
	Global Services such as [[CloudFront]] operate as though they are from `us-east-1`
![[Pasted image 20241001085059.png]]
