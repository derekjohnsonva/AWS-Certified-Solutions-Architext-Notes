Automatic scaling for EC2
	This is known as self-healing
They are defined in Launch Templates of Configurations
	Use Launch Templates over Launch configurations because they allow for versioning
	Contain Min, Desired, and Max size
Keeps the number of running instances at the desired capacity by adding and removing instances
Autoscaling Groups are free
Use cool downs to avoid rapid scaling
## Scaling Policies
Scaling policies update instance number based on metrics (i.e. CPU load)
Manual Scaling
Scheduled Scaling
Dynamic Scaling (3 Sub types)
	Simple - We use an existing alarm as a guide and always add or remove the same amount of instances
	Stepped - Adjust capacity scaling based on how far away from some metric we are
	Target Tracking - 
ASGs don't need scaling policies

## Lifecycle Hooks
Let you configure custom actions that occur during instance launches or instance terminations
	The action takes place curing a Waiting step before it is created or terminated

## Health Check
[[Elastic Load Balancer|ELB]] is healthy if it is running and passing ELB health check
	Can be application aware using [[Network Layers]]

		You need a Health check grace period - time it takes before starting checks
