# [Network ACL & Security Group](../README.md)

## Network ACL

* Network ACL is on the subnet level (Security Groups are on the instance level)
* __Stateless__
* Evaluation order
	* Network ACL Inbound rules
	* Security group Inbound rules
		* Request reached the instance
	* Outbound traffic allowed _(stateful)_
		* Even if there is a Deny for that outbound rule, because it was allowed in, the outbound will always be allowed!
	* Network ACL Outbound rules _(stateless, aka always evaluated)_
* Acts as a firewall on the subnet level
* Default Network ACL: allows every inbound and outbound
* Automatically applies to every instance
* 1 Network ACL per subnet
* New subnets are associated with the default Network ACL
* Network ACL rules
	* Have a number (`1-32766`), with lower number having higher priorities
	* Last rule is an asterisk (*) which is a DENY –> Denies all that didn't match any rule
	* AWS Recommends to add rules with 100 increments
* The rule with the lowest number that matched will be used (aka Not all rules will be evaluated)
* Newly created Network ACLs will deny everything
* Ephemeral ports must be opened if the ACL is restrictive (High numbered ports for TCP connection)

## Security group

* Acts at an Instance level
* An instance can be assigned 5 security groups
* Each security group can have up to 50 rules
* Can only specify `Allow` rules
* Security groups are Stateful
	* If allowed inbound, outbound will be allowed regardless
	* If allowed outbound, inbound will be allowed regardless

## [Back](../README.md)