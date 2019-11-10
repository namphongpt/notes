# [Autoscaling](../README.md)

## High availability & Scalability

### Scalability

* __Vertical scaling__
	* Increase the size of the instance _(t2.micro -> t2.large)_
	* Common in non-distributed systems, such as databases
	* AWS terminology: `Scale up/down`
* __Horizontal scaling__
	* Increase the number of instances/services _(from 1 to 6)_
	* Common in distributed systems
	* AWS terminology: `Scale out/in`

### High availability

* Running the application in at least 2 data centers
* AWS terminology: `Multi AZ`

## AutoScaling Group

* Scale in/out instances
* Automatically register new instances with ELB
* Minimum size
* Desired capacity
* Maximum size
* Launch configuration
	* AMI + instance type
	* EC2 user data
	* EBS volume
	* Security Groups
	* SSH key pair
	* Min/Max size
	* Network & Subnet
	* Load balancer
	* IAM role
	* Scaling policies
* Scaling is based on CloudWatch Alarms
	* Built-in
		* CPU/Network/Time schedule...
		* Target average X usage
		* Number of requests
		* Average Network In/Out
	* Custom
		* Send custom metrics to CW
* __Does not reboot instances__, only terminate unhealthy ones
* Using step-scaling policy, you can specify the number of seconds that it takes for a newly launched instance to warm up
	* Until its specified warm-up time has expired, an instance is not counted toward the aggregated metrics of the Auto Scaling group
* Can create an ASG out of an Instance!
	* AutoScaling will automatically create the `Launch Configuration` based on the instance

### Scaling processes

* Can suspend processes: ASG won't do those actions!
* Processes
	* __`Launch`: Add new instance, increase capacity__
	* __`Terminate`: Remove instance, decrease capacity__
	* __`HealthCheck`: Check the health of the instance__
	* __`ReplaceUnhealthy`: Terminate unhealthy and replace it__
	* __`AZRebalance`: Balance the number of instances in across AZs__
	* `AlarmNotification`: Accept notification from CW
	* `ScheduledAction`: Performs scheduled actions that you create
	* `AddToLoadBalancer`: Add instance to the LB or Target Group
* Note on `AZRebalance`
	* If `Launch` is suspended, `AZRebalance` is implicitly disabled
	* If `Terminate` is suspended, `AZRebalance` can create, but won't be able to terminate (rebalance can add go up with __10%__ of max)

### Troubleshooting ASG

* `<number of instances> instance(s) are already running`: Increase __desired capacity__ of ASG
* Launching EC2 is failed:
	* SG is deleted
* `EC2 instance is in VPC. Failed to configure LB`
	* __Cause:__ The load balancer is in EC2-Classic but the Auto Scaling group is in a VPC
	* __Resolution:__ Make sure both are in the same network
* `EC2 instance is not in VPC. Failed to configure LB`
	* __Cause:__ The specified instance does not exist in the VPC.
	* __Resolution:__ Delete LB or Create new ASG
* ASG fails to launch for 24 hours -> `Administration suspension` All processes are suspended
	* Key pair is deleted

### CloudWatch Metrics

* Available ASG _(Opt-in)_ metrics - Every _1 minute_
	* `GroupMinSize`
	* `GroupMaxSize`
	* `GroupDesiredCapacity`
	* `GroupInServiceInstances`
	* `GroupPendingInstances`
	* `GroupStandbyInstances`
	* `GroupTerminatingInstances`
	* `GroupTotalInstances`
* Underlying EC2 metrics
	* Basic (free) - _5 minutes_
	* Detailed (extra costs) - _1 minutes_

## AutoScaling service

* `Amazon EC2`
	* Launch or terminate Amazon EC2 instances in an Amazon EC2 Auto Scaling group.
* `Amazon EC2 Spot Fleets`
	* Launch or terminate instances from an Amazon EC2 Spot Fleet
	* Automatically replace instances that get interrupted for price or capacity reasons
* `Amazon ECS`
	* Adjust ECS service desired count up or down to respond to load variations.
* `Amazon DynamoDB`
	* Enable a DynamoDB table or a global secondary index to increase its provisioned read and write capacity to handle sudden increases in traffic without
* `Amazon Aurora`
	* Dynamically adjust the number of Aurora Read Replicas provisioned for an Aurora DB cluster to handle sudden increases in active connections or workload.

## [Back](../README.md)