Some businesses will have several AWS accounts, each their own login and payment info. This can get out of hand for large organizations
AWS Organizations  = a way to programmatically create new AWS accounts
	You can group accounts into different categories. These accounts will be put into Organization Roots (not to be confused with a root user)
AWS accounts go from being standard account to being member account
Organizations have 1 master account

Having one account pay for everything is good because you can get volume discounts

Creating new accounts inside of the AWS Organization is a one step process.
We can use a service called role switch that makes it so you obtain the role of other accounts in your organization
## Service Control Policies
These are AWS policies that can be attached to AWS users, Organizations, or Organization Units (sub-organizations within the larger organization)
They trickle down. Nested users/OUs will apply to those lower down in the chain.

The Management account is not affected by SCPs
	This can sometimes be an issue. It is probably best to not use the management account for tasks because you can not use the policy of least privileged access.
They limit what an account can do (they can even restrict the root user)
	An example of this would be to limit an account to only one AWS region
They can not grant permissions
Two ways to do this ...
* Allow list - All access is granted and you have to go through and deny individual resources. Probably better because new resources will be added to AWS after you create the policy.
* Deny list - The opposite
![[Pasted image 20240916114727.png | 400]]
Only the overlap are the effective permissions
