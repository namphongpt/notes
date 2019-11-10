# [Cost management](../README.md)

## Billing alarms

* Before you can create an alarm, you must enable billing alerts on your __Accounts Preferences__ page first
* Stored in CloudWatch `us-east-1`
* For overall worldwide costs
* Overall alarms (not by project!)

## Cost explorer

* Graphical tool to visualize and analyze your costs and usage
* Review charges on accounts or organization
* Can forecast spending for next 3 months
* Get recommendations on which EC2 reserved instances to purchase
* Access to default reports
* API to build custom cost management applications
* __Reservation summary__

## AWS Budgets

* Similar to cost explorer, but
* Sends alarms when costs exceeding budget
* Types of budgets
	* Usage
	* Cost
	* Reservation
* For reserved instances (RI)
	* Track utilization
	* Supports EC2, Redshift, RDS, ElastiCache
* Up to 5 SNS notifications per budget
* Can filter by anything: Account, resource, service, tag, type, region, etc..
* Same options as costs explorer
* 2 budgets are free
* Then $0.02/day/budget

## Cost allocation tags

* Cost allocation tags: Tags that are set to be cost allocated
* Can enable detailed costing reports
* Shows up as columns in Reports
* Types
	* AWS Generated
		* Automatically applied
		* Starts with prefix: `aws:` (e.g.: `aws:createdBy`)
		* Not applied to resources created before activation
	* User created
		* Applied manually (or CLI)
		* Starts with prefix: `user:`
* Cost allocation tags only show up in the reports
* Can take 24 hours
* > Slice and dice costs by XXX
	* Use Cost allocation tags

## [Back](../README.md)