# [AWS Cloud HSM](../README.md)

* Hardware Security Model
* AWS provisions the encryption hardware only _(KMS manages the software for encryption)_
* Dedicated hardware
	* Tamper resistant
	* Can chose HW compliance
		* Eg: `FIPS 140-2 Level 3 compliance`
* You manage your own encryption keys entirely _(single tenant key storage unlike KMS which is multi tenant)_
* CloudHSM clusters are spread across multi AZ (HA)
* Supports symmetric and asymmetric keys!
* No free tier
* Must use the CloudHSM Client software (no cli)
* Deployed and managed in your VPC (accessible from within or peered VPCs)

## [Back](../README.md)