# [VPC](../README.md)

## CIDR

* Classless Inter-Domain Routing
* Used in SGs or AWS networking in general
* Structure: (Base IP)/(Subnet mask)
	* /32 := 2^0 = 1 IP
	* /31 := 2^1 = 2 IP
	* /30 := 2^2 = 4 IP
	* /29 := 2^3 = 8 IP
	* __/28 := 2^4 = 16 IP__
	* __/27 := 2^5 = 32 IP__
	* __/26 := 2^6 = 64 IP__
	* __/25 := 2^7 = 128 IP__

## Private IP

* IANA (Internet Assigned Numbers Authority)
* Private IP ranges
	* `10.0.0.0` - `10.255.255.255` _(10.0.0.0/8)_
	* `172.16.0.0` – `172.31.255.255` _(172.16.0.0/12) AWS Default_
	* `192.168.0.0` – `192.168.255.255` _(192.168.0.0/16)_

## General

* Soft limit: 5 VPC per region (can be increased)
* Each CIDR
	* Min size: `/28` –> 16 Addresses
	* Max size: `/16` –> 65536 Addresses
* Each VPC can have a maximum of 5 CIDRs (1 primary, 4 secondary)
* Before being able to delete a VPC need to:
	* Terminate all instances
	* Delete all subnets
	* Delete custom security groups and custom route tables
	* Detach any internet gateways or virtual private gateways
* The primary Private IP address is kept until instance is terminated
* The primary Public IP address is lost on instance stop, reboot or terminate

### Default VPC

* All new accounts have a default VPC
* New instances are launched into default VPC if none specified
* Have internet connectivity and all instances have public IPs
* Also get a public and private DNS for instances
* Contents
	* 1 VPC
	* 3 Subnets
	* 1 Internet GW
	* 1 DHCP Options Set
	* 1 Network ACL
	* 1 Security group

## [Back](../README.md)