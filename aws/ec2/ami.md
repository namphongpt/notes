# [AMI](../README.md)

## General

* Amazon Machine Image
* Provides the information required to launch an instance
* Region specific! ___(AMI ID will be different in each region)___
* Stored in S3
* Use public AMIs / Rent from third parties
* Private and region locked by default
* Copy (directly)
	* Without `Create volume` permissions
		* Can't copy encrypted AMI
		* Can't copy AMI with billingProduct
		* Workaround: Launch instance from AMI then create new from it

## [Back](../README.md)