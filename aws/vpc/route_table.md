# [Route table](../README.md)

* Need to associate subnets if not using the Main RT
* Public RT
	* VPC CIDR –> local
	* Anything else (`0.0.0.0/0`) –> Internet Gateway
* Private RT
	* VPC CIDR –> local
	* Anything else (`0.0.0.0/0`) –> NAT Gateway

## [Back](../README.md)