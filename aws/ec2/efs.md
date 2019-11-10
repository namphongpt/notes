# [EFS](../README.md)

## General

* Managed NFS that can be mounted on many EC2 instance
* Works multi AZ
* Highly available/scalable
* Expensive (~3 times the price for GP2), but pay per use
* Need to attach SG to EFS in order to use
* Can be used simultaneously from all AZs
* Uses NFSv4.1
* Compatible with Linux based AMIs (No Windows yet)
* Performance mode
	* General _(default)_
	* Max performance _(when used by 1000s of instances)_
* Can sync files from on-premise
* Can backup to another EFS (incremental, can choose frequency)
* Encryption at rest using KMS

## [Back](../README.md)