Allows you to create and manage APIs

You create endpoint for your applications

The API gateway will sit between you applications and you integrations

Can connect to services in AWS on On-Prem

Does 3 things when it gets a request: Authorize, validate, transform
Does 3 things when it returns a response: return, prepare, transform

You deploy a gateway to a stage. The stage has a unique url and will have its own settings. This is good for separating prod and dev.
## Authentication
Can use [[Cognito]] 
Can also use a Lambda authorizer

## Endpoint Types
Edge-Optimized = Routed to nearest CloudFront POP
Regional = Clients in the same region
Private = Only accessible in the VPC

## Errors
Just the standard Error codes
4XX = Client Error
5XX = Server error
400 = bad request (generic)
403 = access denied
429 = throttle error
502 = bad gateway exception
503 = service unavailable
504 = integration failure

## Caching
TTL default is 300 seconds
min = 0 max = 3600 seconds
cache size = 500mb - 237GB
can be encrypted