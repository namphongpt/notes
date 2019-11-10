# [DNS Resolution](../README.md)

* `enableDnsSupport`: DNS Resolution setting
	* Default: true
	* Helps decide if DNS resolution is supported for the VPC
	* If true, it queries the AWS DNS server at `169.254.169.253`
* `enableDnsHostname`: DNS Hostname setting
	* Default: false (for newly created VPCs, but true for default)
	* Won't do anything unless `enableDnsSupport` is also true
	* If true, assigns a public hostname to EC2 instances if it has a public IP
* If you use a custom DNS domain names in a private zone R53, both must be set to true

## [Back](../README.md)