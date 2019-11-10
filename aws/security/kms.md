# [AWS KMS](../README.md)

## General

* Key Management Service
* Only supports __symmetric keys__
* Fully integrated with `IAM` for authorization
* Seamlessly integrated with many services (`EBS`, `S3`, `Redshift`, `RDS`, `SSM`...)
* Can also use the CLI to encrypt ourselves
* When to use it
	* Need to share sensitive information –> KMS
* CMK _(Customer Master Key)_
	* used to encrypt data
	* can never be retrieved by the user
	* can be rotated for extra security
* __Can only encrypt up to 4 KB data per call__
* If data > 4 KB
	* __Have to use envelope encryption__
* How to give access to KMS to someone
	* Key policy allows the user
	* IAM policy for the user allows KMS API calls
* Ability to fully manage keys & policies
	* Create
	* Rotate policies
	* Disable
	* Enable
* Able to audit key usage in CloudTrail
* 3 types of Customer Master Keys _(CMK)_
	* AWS Managed Service default: Free
	* User keys: $1/month
	* User keys imported __(must be 256-bit symmetric key)__: $1/month
* Fee for API calls to KMS _($0.03/10000 calls)_
* To delete a CMK in AWS KMS you must schedule key deletion
	* The default waiting period is 30 days
	* Minimum of 7 days
	* During the waiting period
		* A CMK that is pending deletion cannot be used in any cryptographic operations.
		* AWS KMS does not rotate the backing keys of CMKs that are pending deletion.

## Encryption

* Requires migration (through snapshot/backup)
	* `EBS volumes`
	* `RDS databases`
	* `ElastiCache`
	* `EFS`
* Can encrypt in place
	* `S3`

## [Back](../README.md)