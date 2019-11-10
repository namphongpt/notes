# [Security](../README.md)

## Shared responsibility model

![Model](https://d1.awsstatic.com/security-center/Shared_Responsibility_Model_V2.59d1eccec334b366627e9295b304202faf7b899b.jpg "Responsibility Model")

## General

* `DDoS`: Distributed Denial of Service

## Protection against DDoS

* `AWS Shield Standard`
	* Protects against DDoS without any additional costs
	* Enabled by default
* `AWS Shield Advanced`
	* 24/7 premium DDoS protection
* `AWS WAF`
	* Filter specific requests based on rules
* `CloudFront` and `Route53`
	* Availability protection using global edge network
	* When combined with AWS SHield, provides attack mitigation at edge
* Be ready to scale (`AWS Auto Scaling`)
* Separate static resources (`S3/CloudFront`) from dynamic (`EC2/ALB`)

## Logging for security and compliance

* Service logs
	* `CloudTrail`: Trace API calls
	* `Config Rules`: Compliance over time
	* `CloudWatch Logs`: Data retention
	* `VPC Flow Logs`: IP Traffic within your VPC
	* `ELB Access Logs`: Metadata of request to the LBs
	* `CloudFront Logs`: Web distribution logs
	* `WAF Logs`: Full logging of all requests analyzed by the service
* All these can be put into s3 –> Analyze with `AWS Athena`
* Encrypt bucket + use IAM & bucket policies to secure, MFA delete
* Transition to `Glacier` with `Vault lock` policy

## [Back](../README.md)