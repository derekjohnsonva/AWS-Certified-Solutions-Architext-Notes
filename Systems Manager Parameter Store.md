---
aliases:
  - SSM Parameter Store
---
A storage for configuration and secrets
Allows us to store parameter with hierarchies and versioning
Public Service
Params can be encrypted or plaintext
Parameters can be public

You can access Parameter store from other services (compute, and code deployment pipeline services) 

A parameter is really just a name and a value
	Value can be a string, a string-list, and an encrypted string
	The name can contain `/` if you want to create a hierarchy (i.e. `/my-app/dbstring`)

To access parameter from command line use...
`aws ssm get-parameters --names /my-app/dbstring`
To get multiple use...
`aws ssm get-parameters-by-path --path /my-app/`
