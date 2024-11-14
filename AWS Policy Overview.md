A policy in AWS specifies some sort of access control. There are two main types
1) identity-based policies - attached to an [[IAM Service]] user, group, or role
2) resource-based policies - you can specify who has access to the resource and what actions they can perform on it

How to identify if an action can be done
![[Pasted image 20241014200012.png]]
If an identity policy and a resource policy disagree on if you can do something, you are granted permission.

Identity based policies should be used for individual users or roles. Resources based policies should specify a component’s permissions. Resource based policies are inline policies and are therefore unmanaged. If you want to grant privileges to a user or group, use identify based policies. If you want to control privileges on a component regardless of who is using it and what rights they might have, you a resource based policy.
## Identity Based policies
Types of Identity based policies
Users - An individual IAM human or service that interacts with AWS. They have credentials associated
Groups - A collection of Users
Roles - A set of permissions that can be temporarily assumed by a human or service.

### **When to Use IAM Users, Groups, and Roles:**

| **IAM Entity** | **When to Use**                                                                                                                                    | **Example Use Case**                                                                                                            |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **IAM User**   | Use when you need to provide **long-term access** to a specific individual or service to interact directly with AWS resources.                     | A developer or admin needs access to AWS resources to manage EC2 instances and databases.                                       |
| **IAM Group**  | Use to simplify **permission management** for multiple users who require the **same level of access** to AWS resources.                            | Create a "Developers" group that has access to EC2, RDS, and S3, and assign all developers to this group for consistent access. |
| **IAM Role**   | Use for **temporary access** to AWS resources by services, users, or external entities. Also ideal for cross-account or cross-service access.      | - An EC2 instance needs to access an S3 bucket to store logs.                                                                   |
|                | Use roles for **external entities** that need temporary access without creating new IAM Users (e.g., granting external users access to resources). | - Allowing an external auditing company to access your CloudTrail logs for security auditing purposes.                          |
|                | Use when an application or service needs to **assume permissions dynamically**.                                                                    | - An application running on Lambda needs to access DynamoDB for short periods during execution.                                 |
### Service Control Policies (SCP)
a type of organization policy that you can use to manage permissions in your organization. SCPs offer central control over the maximum available permissions for the IAM users and IAM roles in your organization.
SCPs do not grant permissions to the IAM users and IAM roles in your organization. No permissions are granted by an SCP. An SCP defines a permission guardrail, or sets limits, on the actions that the IAM users and IAM roles in your organization can perform.

