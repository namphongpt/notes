# [Bastion host & VPN & Direct Connect](../README.md)

## Bastion hosts

* An instance in the public subnet that can be used to SSH into instances in the private subnets
* Security Group rules must be tight
	* Only allow 22 from your IPs
	* Don't allow other instances

## Site to Site VPN

* `Site-to-Site VPN connection` to connect the `VPN gateway` with the `Customer gateway`
* Virtual Private Gateway (aka VPN Gateway)
	* VPN concentrator on AWS side
	* VGW is created and attached to the VPC from which you want to create the S2S connection
	* Possibility to customize ASN
* Customer Gateway
	* Software or Hardware on customer side
	* On premise
	* There are a list of tested devices
	* Requires static, internet-routable IP address
		* If behind corporate NAT (with NAT-T), use public IP of the NAT

## Direct connect

* Similar to Site to Site, but this is over private network
* Dedicated, private connection to your VPC
* Connection must be set up between your DC and one of AWS Direct Connect location
* Need to set up a Virtual Private Gateway on your VPC
* Access public resources (S3) and private (EC2) on the same connection
* Use cases
	* Increase bandwidth throughput and save costs - working with large data sets
	* More consistent network experience - applications using real-time data feeds
	* Hybrid environment (on prem + cloud)
* Supports both IPv4 and IPv6

### Direct connect gateway

* When you want to connect to multiple VPCs in many different regions __but same account for now__
* VPCs must have non-overlapping CIDRs
* It won't peer the VPCs just give you access to each

## [Back](../README.md)