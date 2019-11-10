# [EC2 Instances](../README.md)

## General

* Provides resizable compute capacity in the cloud
* Can choose `Shutdown behavior`
	* __Stop__ _(default)_
	* __Terminate__
* Can set `Instance protection`
	* Protect from accidental terminates
	* If shutdown behavior is terminate, then executing `sudo shutdown now` from OS will terminate the instance!
* Possible to change instance type
	* If instance uses EBS, then it won't loose data!
	* Steps
		* Stop the instance
		* Change instance type
* Can attach `Elastic IP` to instances
* Public IP will change on reboot, shutdown
* Private IP is persistent until instance is terminated
* `m3.large` doesn't support IPv6 –> Upgrade to `m4`

## Placement groups

* __Cluster:__ 
	* Single AZ low latency
	* Same hardware/rack
	* 10 GBps
	* No T2 types
* __Spread:__
	* Multi AZ
	* Maximum 7 instances in any AZ
	* Different HW
* __Partition:__
	* 7 partitions per AZ
	* Up to 100 instances
	* Big data distributed applications (HDFS, Kafka)

## Launch types

* `On-demand`
	* Short workload, predictable pricing
* `Reserved`
	* Long workloads (1 or 3 years)
* `Convertible`
	* Reserved, but can change instance type
* `Scheduled`
	* Short window reserved
	* For at least a one-year term!
* `Spot`
	* Bidding
	* Cheap, can loose instances
	* If instance is terminated before the first hour __BY AWS__ you don't pay anything
* `Dedicated instance`
	* Not sharing hardware
	* Can share from the same account
* `Dedicated host`
	* Entire server
	* Control placement
	* 3 years

## Instance types

* [Compare online](https://ec2instances.info)
* `R`
	* RAM - memory heavy
* `C`
	* Compute/Databases
* `M`
	* Medium: between R and C (general, webapp)
* `I`
	* Good I/O, databases
* `G`
	* GPU: Video rendering, machine learning
* `T2/T3 Burstable`
* `T2/T3 Unlimited`

## Troubleshooting

### Launch troubleshooting

* `#InstanceLimitExceeded`
	* Maximum number of instances in the region is reached _(default: 20)_
	* Resolution:
		* Ticket to increase
		* Use another region
* `#InsufficientInstanceCapacity`
	* AWS ran out of on-demand instances on the __AZ__!
	* Resolution:
		* Wait
		* 1 at a time
		* Change regions
* `Instance terminates Instantly` (Pending to terminated)
	* Reached EBS volume limit
	* Corrupted EBS volume
	* EBS encrypted and no access to KMS
	* Instance store missing a part
	* Debug:
		* State transition reason
		* State transition message

### SSH troubleshooting

* `Unprotected key file`: pem doesn't have 400 permissions
* `Host key not found`: wrong username
* `Connection timeout`: SG misconfiguration or CPU is busy

## CloudWatch for EC2

### CloudWatch Logs

* Default: No logs
* Needs CW Agent installed

### CloudWatch Monitoring

* AWS provided
	* CPU, Network, Status, _Disk (only for instance store)_
	* _(Free)_ Default: 5 minutes
	* _(Paid)_ Detailed: 1 minutes
* Custom (your responsibility):
	* CloudWatch agent or scripts
	* Needs CW IAM permissions
	* 1 minute, can be more frequent up to 1 sec
	* RAM, application level metrics
	* Needs IAM role to push to CW
* CPU: Utilization + Credits if instance type is `T`
* Network: In and out traffic
* Status:
	* `Instance`: EC2 VM check
	* `System`: Hardware check
* Disk (only for instance store backed instances)
* __Aggregate statistics__ are only available for the instances that have __detailed monitoring__

## [Back](../README.md)