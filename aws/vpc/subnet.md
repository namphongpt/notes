# [Subnet](../README.md)

* 1 Subnet is tied to 1 AZ
* You can have multiple subnets in each AZ
* Each subnet
	* First `4` IP reserved by AWS AND Last `1` IP reserved by AWS
	* 10.0.0.0/16
		* `10.0.0.0`: Network address
		* `10.0.0.1`: AWS VPC Router
		* `10.0.0.2`: AWS DNS server
		* `10.0.0.3`: Reserved for future use
		* `10.0.0.255`: Broadcast address (But AWS doesn't support broadcast messages)
* > Need 29 IPs, what should be the subnet size?
	* /27 (32 IPs) is NOT GOOD!
	* Need at least /26. (/26 –> 64 - 5 = 59 IPs)

## [Back](../README.md)