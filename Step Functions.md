A state machine inside of AWS
Standard workflow = can run for up to 1 year
Express workflow = max of 5 min

You can write your state machine using Amazon Stats Language (ASL)

You give it [[IAM Service]] Roles for permissions

Possible States
* Succeed/ Fail
* Wait
* Choice (branching)
* Parallel - create multiple branches
* Map - do something for each entry an object
* Task - Take action using different services (Lambda, SNS, ...)
