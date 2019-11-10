# [VPC Flow logs](../README.md)

* Captures information about IP traffic that is going into your interfaces
	* VPC Flow logs
		* Cannot enable for ENIs on EC2-Classic platform
	* Subnet Flow logs
	* Elastic Network Interface logs
* Helps to monitor & troubleshoot connectivity issues
* Logs can go directly to S3 / CloudWatch Logs
* Captures information from AWS managed interfaces too: ELB, RDS, ElastiCache, Redshift, WorkSpaces
* Syntax
	* `<version> <account-id> <interface-id> <srcaddr> <dstaddr> <srcport> <dstport> <protocol> <packets> <bytes> <start> <end> <action> <log-status>`
	* __`srcaddr`__ and __`dstaddr`__: Identify problematic IPs
	* __`srcport`__ and __`dstport`__: Identify problematic Ports
	* __`action`__: ACCEPT/REJECT due to Security groups/Network ACL
* Can be used for analytics on usage patterns, malicious behavior
	* S3 –> Athena
	* CloudWatch Logs –> CloudWatch Insights

## [Back](../README.md)