# [NAT](../README.md)

## General

* Network Address Translation
* Allow instances in the private subnets to connect to the internet

## NAT Instances

* Outdated, not recommended
* It is an EC2 instance
* AMI is managed by Amazon, pre-configured
* Not HA, not resilient
* Internet traffic bandwidth depends on instance type
* Must be launched in the Public subnet
* Must disable EC2 flag: `Source/Destination check`
* Must have EIP attached to it
* Route table must be configured to route traffic from private subnets through it
* Must create a SG for it
	* SSH (22)
	* HTTP (80) – __Only from VPC CIDR__
	* HTTPS (443) – __Only from VPC CIDR__
	* All ICMP - IPv4 (0-65535) – __Only from VPC CIDR__

## NAT Gateway

* AWS managed, higher bandwidth, better availability, no admin
* Pay by the hour + bandwidth
* Created in a specific AZ, uses an EIP
* Requires an IGW _(Private instance –> NGW –> IGW)_
* Cannot be used by an instance in the same subnet that it is deployed
* 5 GB/s bandwidth (default) that scales automatically to 45 GB/s
* No need to manage SGs

## [Back](../README.md)