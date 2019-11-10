# [VPC Peering](../README.md)


* Connect 2 VPCs privately using AWS's network
* Can be different account / different region
* The VPCs must have non-overlapping CIDRs
* A VPC Connection is __not transitive__ (must be established for each VPC that you want to connect)
	* A <–> B <–> C : A and C is not connected unless you also have an A <–> C VPC Peering
* Once a VPC Connection is created, it needs to be accepted
* Must update each VPC's each subnet's route table
	* A: when target IP is VPC B, route traffic to the VPC Peering Connection X
	* B: when target IP is VPC A, route traffic to the VPC Peering Connection X

## [Back](../README.md)