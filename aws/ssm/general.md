# [Systems Manager (SSM)](../README.md)

## General

* Manage EC2 and on-premise
* Operational insights
* Detect problems
* Patch
* Windows & Linux
* Free
* Requires SSM agent to be installed
* Requires IAM permissions 
* __Regional__ Resource groups (based on tags) -> Easy patching
* `Documents`: yaml or json, common denominator between SSM features
* `Run command`:
	* Executes a document or just a run command
* Patch:
	* `Inventory`                          => List software on an instance
	* `Inventory + Run command`            => Patch software
	* `Patch manager + maintenance window` => Patch OS
	* `Patch manager`                      => Gives compliance
	* `State manager`                      => Ensures instances are in a compliant state
* Session manager
* Parameter Store

## (Scenario) Lost SSH key to EC2

* EBS Backed
	* Method 1: Manual
		* Stop instance
		* Detach root volume
		* Attach it to a new instance as a data volume
		* Change `~/.ssh/authorized_keys`
		* Detach / Move back to original instance
	* Method 2: SSM
		* `AWSSupport-ResetAccess`
* Instance store backed
	* Nothing to do, terminate instance
	* _(Could use SSM)_

## [Back](../README.md)