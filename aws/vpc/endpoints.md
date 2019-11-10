# [VPC Endpoints](../README.md)

* Provides access to AWS services using a private network
* Scale horizontally and are redundant
* Doesn't require NAT, IGW etc... in order to access AWS services (e.g: S3, CW, DDB, API GW...)
* 2 types
	* Interface
		* Provisions an ENI (Private IP address) as an entry point
		* __Must attach security group__
	* Gateway
		* Provisions a target and must be used in a route table
		* S3, Dynamo DB
* In case of issues
	* Check DNS Setting Resolution in the VPC
	* Check route tables (for Gateway endpoints)
	* Gateway
		* S3 Endpoint is set up for eu-west-1
		* __Instance in private subnet using AWS CLI must set `--region eu-west-1`!__

## [Back](../README.md)