Function as a Service (FaaS) product
You write a function and specify a specific runtime environment (e.g. Python 3.8)
	You specify the amount of memory you will need
You are then billed for the duration of the function execution

key part of a [[Serverless]] architecture

There are common runtimes for popular languages as well as custom runtimes using **Layers**

You need to make sure all of your functions do not rely on side effects

**Numbers to know**
* 15 min function timeout
* 512MB temporary storage (can get up to 1024MB)
* Deployment package = 50MB zipped or 250MB unzipped

**When to Use**
* Serverless application
* File Processing
* database triggers
* Perform serverless CRON jobs
* Realtime Data Processing (maybe question this one)

## Networking
Two modes
1) Public (default) - functions can access public internet and public services. Best performance
2) VPC - they obey all [[VPC]] networking rules 
## Security
Lambda permissions is really only done with Execution Roles
However, they also can have resource policies - this can be used to communicate with S3 or other services

## Logging
output of lambda executions - [[CloudWatch]] Logs
Metrics go into [[CloudWatch]]
Distributed tracing can be integrated with X-Ray
Logs require permissions via Execution Role

## Invocations
Synchronous - Results are returned during the request. Errors have to be handled within the client.

Asynchronous - The sender of the request does not wait for a response
	The function call needs to be idempotent (re-running the operation will not change the outcome).
	Anything that fails repeatedly will be sent to a Dead Letter Queue (DLQ)

Event Source Mapping - Data will be batched with an event source mapping and lambda will run once the batch is created.
	Generally used with Kinesis Data Stream
	The source service is not delivering the data, the Event Source Mapping retrieves the data. Thus, permissions from the lambda execution role need to be able to access the data in the service

## Versions
You can specify different versions of a function
	Versions = code and configurations
	When you publish a version, it is immutable
You can create Aliases to point to a specific version
$Latest points to the latest version

## Startup Times
Cold Start = Time before executing an operation if you need to create the execution context
Warm start = execution time if execution context is reused

## Creating Lambda functions
You can add environment variables for the function to use

## Some Limitations of Lambda
Lambda is not good if you need long running data flow
If you need this type of long running data flow but still want to use a [[Serverless]] architecture, use [[Step Functions]]