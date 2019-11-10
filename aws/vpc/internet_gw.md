# [Internet Gateways](../README.md)

## Internet gateway

* Helps VPC instances to connect with the internet
* Scales horizontally, Highly Available and redundant
* Must be created separately from the VPC
* 1 to 1 connection between VPC and IGW
* IGW is also a NAT for instances with Public IP
* __Route tables are required to access the internet, just an IGW is not enough__

## Egress only Internet gateway

* Only for IPv6
* Similar to NAT (but NAT is for IPv4)
* There are no private IPs in IPv6 (aka all IPs are public)
* Egress Only IGW will give access to Internet to IPv6 instances, but they won't be accessible from the internet
* After creating one, need to update the Route Tables

## [Back](../README.md)