# [CIDR](../README.md)

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

## [Back](../README.md)