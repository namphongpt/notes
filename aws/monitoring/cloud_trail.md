# [AWS CloudTrail](../README.md)

* Provides governance, compliance and audit for your AWS account
* (Track every API call made to the account)
* Can put to CW Logs
* If a resource is deleted, look in CloudTrail _(to see who did that)_
* Stores for 90 days (then you need to store them somewhere else if you want to keep them)
* Default UI only shows `Create`, `Modify` and `Delete` events
* __CloudTrail has an option to validate file integrity__
	* E.g. Can detect if the log file has been changed after it has been written to S3
* A trail can be applied to all regions or a single region
* A single SNS topic for notifications and CloudWatch Logs log group for events would suffice for all regions
* Can create Trails
	* Detailed list of every event you select
	* Can store them in S3
	* If trails are put to S3, they have SSE-S3 encryption by default (can choose KMS)
	* Control via IAMs or Bucket policies
	* Can be region specific or global
* CloudTrail supports five trails per region
* A trail that applies to all regions counts as one trail in every region
* __For global services__ such (`IAM`, `AWS STS`, `CloudFront`) events are delivered to __any trail__ that has the __Include global services option enabled__
* `AWS OpsWorks` and `Route53` actions are logged in the __US East (N. Virginia) region__
 
## [Back](../README.md)