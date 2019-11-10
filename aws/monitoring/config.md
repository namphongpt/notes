# [AWS Config](../README.md)

## General

* Helps with auditing and compliance of your AWS resources
* Records configuration and changes over time
* Records compliance over time
* Can store AWS Config data in S3 (and use Athena)
* Questions can be solved:
	* Is there unrestricted SSH access to my SGs
	* Is there any S3 buckets with public access
	* How my ALB configuration changed
* Use cases
	* Security Analysis & Resource Administration
	* Auditing & Compliance
	* Change Management
	* Troubleshooting
	* Discovery
* Can receive alerts _(SNS notification)_ on changes
* Regional service
* AWS Config creates configuration items for every supported resource in the region
* Can be aggregated across multiple accounts/regions
* In cases where several configuration changes are made to a resource in quick succession (within a span of few minutes), It will only record the latest configuration of that resource
* AWS Config does not cover all the AWS services
	* The configuration management process can be automated using API + code

## Config rules

* 80+ AWS managed config rules
* Can create custom rules _(must be defined in AWS Lambda)_
	* Eg.: Evaluate if all EBS disk is gp2 type
* Rules can be evaluated
	* For each config change
	* Or regular time intervals
* Pricing
	* No free tier
	* $2/active rule/region/month (less after 10 rules)
* Can integrate with CloudTrail to see who made the changes
 
## [Back](../README.md)