A product that provides a managed file transfer service TO of FROM [[Simple Storage Solution|S3]] and [[Elastic File System|EFS]]
	Lets to download or upload to these services
When would I use this product?
	Use it when you need to transfer in an out of these services but need to use an existing protocol 
Allows you to use different protocols
1) File transfer protocol - unencrypted
2) File Transfer Protocol Secure - TLS encryption
3) SSH - file transfer over SSH
4) Applicability Statement 2 - Used if you are required to

Managed File Transfer Workflows = A serverless way to handle file workflows

Multi-AZ - Resilient and Scalable
 ![[Pasted image 20241003150046.png]]
## Endpoint Types
Public = dynamic IP
VPC - Internet = Static internal IP with an Elastic IP for public access 
VPC - Internal = Static internal IP 