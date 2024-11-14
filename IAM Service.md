 and Access Management (IAM) is used to restrict privileges. When you log in as a root user, you can do anything. Thus, it is best practice to always use IAM for a task.
**IAM is globally resilient. Any data is always secure across all regions**

## Basics
![[Pasted image 20240905131527.png]]
Three types of identities: Users, groups, and roles.
Users for when you have one person or service that will be doing a task
Group when multiple users are going to need the same permissions.
Role when you don't know how many users or services will be using a task or when you need an external service to act on your behalf

## Policies

[[Security Policies]]
## IAM Users
5000 IAM users per account
IAM user can be a member of 10 groups
Get around this with Roles or identity federation

## IAM Groups
You can add IAM users to groups and add permissions to Groups
you can not log in to a group
No nesting of groups
300 groups per AWS account (this can be increased with a support ticket)
Groups can't be referenced as a principal in a policy

## IAM Roles
this is one of the most confusing things in AWS
Roles do not represent and individual, they represent a level of access inside of an AWS account. It can be assumed short term by other people.
There are two types of policies that can be applied
* Trust policies - Checks who should be allowed to assume the role
* Permission policies - Checks what the role should be able to do
When an identity gets validated by the Trust Policy, Temporary Security Credentials are created using the Permissions Policy 
Assuming a role is done using the Secure Token Service
### When you may use Roles
When you are trying to let AWS Lambda access another service (ex. [[Simple Storage Solution|S3]]).
	Why use a role? Otherwise, you would need to hardcode security keys into your lambda function. Also, you don't know how many instances of the lambda function are going to be run.
Emergency situations
	The helpdesk may need to get access to a lot of AWS stuff in an emergency. You can create a break glass role for these emergencies.
Adding AWS to an existing network
	You may want single sign on or you may have more than 5000 employees.
	External accounts can't be used to log in as an IAM User but it can be used to validate a Role.
Use roles when you think you may have lots of users

