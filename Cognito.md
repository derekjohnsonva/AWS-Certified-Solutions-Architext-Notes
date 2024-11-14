A service for Authentication, Authorization, and user management for apps
This service can be very confusing
**User Pools** - Used for Sign-in and get JSON Web Token (JWT)
	Used for 3rd party sign in using other services (i.e. google)
	This can not be used for accessing other AWS resources. For that we need AWS Credentials 
![[Pasted image 20240928104244.png | 400]]
**Identity Pools** - Temporary AWS Credentials
	Guest Users
	Federated Identities - google, facebook, twitter, ...
	basically, you are swapping one credential for another
![[Pasted image 20240928104451.png | 400]]

Normally, you will use a combination of the two
![[Pasted image 20240928104652.png | 400]]