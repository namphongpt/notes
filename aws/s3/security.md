# [S3 Security](../README.md)

## General

* `User based`
	* __IAM policies__
* `Resource based`
	* __Bucket policies__ (bucket wide rules)
		* Allows cross account access
	* __Object Access Control List__ (`Object ACLs`): Finer grain access control
	* __Bucket Access Control List__ (`Bucket ACLs`): Less common
* Networking
	* Supports VPC endpoints (Instances in VPC without internet access can still use S3)
* Logging and Audit features
	* S3 access logs can be stored in another S3 bucket
	* API calls can be logged in CloudTrail
* User security
	* MFA required can be required to delete versioned buckets
	* Signed URLs: URL that valid only for a limited time

## Encryption for objects

* Encryption at rest
	* `SSE-S3`
		* Using AWS S3 managed keys, handled by AWS seamlessly
		* Object encrypted at server side
		* AES-256
		* Must set header when uploading: `"x-amz-server-side-encryption":"AES256"`
	* `SSE-KMS`
		* KMS to manage encryption keys
		* Similar to SSE-S3, just using KMS managed keys instead of S3
		* Advantages:
			* User control
			* Audit trail
		* Must set header when uploading: `"x-amz-server-side-encryption":"aws:kms"`
		* Still seamless
	* `SSE-C`
		* You manage your encryption keys
		* Data keys are fully managed by the customer
		* S3 won't store the keys
		* Headers required
			* `x-amz-server-side​-encryption​-customer-algorithm`
			* `x-amz-server-side​-encryption​-customer-key-MD5`
			* `x-amz-server-side​-encryption​-customer-key`
		* __HTTPS must be used__
		* Encryption keys must be provided in the header for every request! 
		* Still seamless
	* `Client side encryption`
		* Client library such as AWS S3 Encryption Client
		* Clients must encrypt the data themselves before uploading to S3
		* Clients must decrypt the data themselves after downloading from S3
		* Customer fully manages the keys and encryption cycle
* Encryption at transit _(SSL/TLS)_
	* `HTTP endpoint`: not encrypted
	* `HTTPS endpoint`: encrypted
* Can set bucket option to encrypt all files even if the files doesn't specify encryption

## MFA Delete

* First need to enable `versioning` on the bucket
* Only the bucket owner (root account) can enable/disable MFA-Delete
* Can only enable is via the CLI (as of now)
* Need to MFA before
	* Permanently deleting an object version
	* Suspend versioning
* DON'T need MFA for
	* Enabling versioning
	* Listing deleted versions
* If enabled, you can't do any permanent delete as the UI doesn't use MFA
	* Must do all permanent delete in the CLI while passing MFA token

## Bucket policy

* JSON based
	* `Resources`: Buckets or objects
	* `Actions`: Set of API actions
	* `Effect`: Allow or Deny
	* `Principal`: Account or user to apply the policy to
* Can do various things using it:
	* Cross account access
	* Force encryption on objects
	* Grant public access
* [AWS Bucket policy examples](https://docs.aws.amazon.com/AmazonS3/latest/dev/example-bucket-policies.html)

## Access Control List

* `READ`: List bucket objects / read objects and its metadata
* `READ_ACP`: Allows to read bucket/object ACL
* `WRITE`: Create, overwrite and delete any object in the bucket
* `WRITE_ACP`: Write, delete, create Object ACLs
* `FULL_CONTROL`: All previous policies

## Access logs

* Any request will be logged (Can be from another account, access denied etc..)
* Can use Data analysis tools (Amazon Athena)
* Can use prefix in logging bucket
* Can take some time for the logs to show up

## Default encryption Vs Bucket policies

* Old way: Bucket policy
* New way: Just enable default encryption on Bucket
* NOTE: Bucket policy evaluated before default encryption

## [Back](../README.md)