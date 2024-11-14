A directory is a store of objects with a structure
	Often used to provide organization sign in

Directory Service - AWS version of a directory

It functions in three modes
- Simple AD - An implementation of Samba 4 (compatibility with basics AD functions). Can not use with on prem
- AWS Managed Microsoft AD - An actual Microsoft AD DS Implementation. Use if you need to link with an on prem directory
- AD Connector which proxies requests back to an on-premises directory. Use if you already have an on prem directory and just want to connect it to some AWS service

When to use each mode?
* Default to Simple AD
* Move to Microsoft AD if you need MS Active Directory.
* Use AD Connector if you need a Directory for AWS Services but don't need to store any info in the cloud.