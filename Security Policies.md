They are created using JSON.
Used to allow or deny access to resources
```JSON
{
  "Version": "2012-10-17",
  "Statement": [
    {
	  "Sid": "FullAccess",
      "Effect": "Allow",
      "Action": ["s3:*"],
      "Resource": ["*"]
    },
    {
	  "Sid": "DenyCatBucket",
      "Effect": "Deny",
      "Action": ["s3:*"],
      "Resource": ["arn:aws:s3:::catgifs", "arn:aws:s3:::catgifs/*"]
    },
  ]
}

```
In the above DenyCatBucket statement, the first resource represents the bucket and the `/*` represents all the objects in the bucket.
When there are overlaps, as with above, we follow the rules in the following precedence
1) Explicit deny
2) explicit allow
3) Default Deny (implicit) - aws accounts default to having no privileges.
This gets more complicated with multiple groups

 Managed policies allow us to change permissions and how them propagated to every IAM user with that managed policy

Amazon Resource Name (ARN) - Uniquely identify resources within any AWS accounts
The format for an ARN is one of the following ...
```
arn:partition:service:region:account-id:resource-id
arn:partition:service:region:account-id:resource-type/resource-id
arn:partition:service:region:account-id:resource-type:resource-id
```

![[Resource Policies]]

## Three types of Policies
When you set the permissions for an identity in IAM, you must decide whether to use an AWS managed policy, a customer managed policy, or an inline policy

**AWS Managed policy** - An AWS managed policy is a standalone policy that is created and administered by AWS. A standalone policy means that the policy has its own Amazon Resource Name (ARN) that includes the policy name.

**Customer Managed policy** - You can create standalone policies in your own AWS account that you can attach to principal entities (users, user groups, and roles). You create these _customer managed policies_ for your specific use cases, 

**Inline Policy** - An inline policy is a policy created for a single IAM identity (a user, user group, or role). Inline policies maintain a strict one-to-one relationship between a policy and an identity.
	Deleted when you delete the identity