# [Elastic Beanstalk](README.md)

## General

* AWS manages all the underlying infrastructure 
* Runtime patches are AWS's responsibility!
* Architecture models
	* `Single instance`: Great for dev
	* `HA with LB`: LB + ASG (prod web apps)
	* `HA without LB`: ASG only (prod no-web apps)
* Components
	* Application
	* Application versions
	* Environment name
* Tiers
	* __Web server environment__
		* `ELB`, `ASG`, `EC2`
		* Host manager running on the instances
	* __Worker environment__
		* `ASG`, `EC2`, `IAM role`, `SQS queues`
		* Daemon (pulling messages/sending messages to web server)
* 1 Environment can only support 1 tier!
* An `S3 bucket` is created for each region in which environments is created `elasticbeanstalk-<region>-<account-id>`
* Log can be put into `CloudWatch logs`
* Can put Route53 Alias or CNAME on top of EB URL
* Rolling:


## Deployment modes

* `All at once`: Fastest, but has downtime
* `Rolling`: Few instances _(buckets)_ at a time, then next bucket once the previous is healthy
	* EC2 has a base AMI _(can be configure)_
	* EC2 gets the new code
	* EC2 resolves new dependencies __(can take a lot of time!)__
	* Applications are swapped
	* > Question: How to make it faster?
		* Use a golden AMI
* `Rolling with additional batches`: Rolling but extra instances (Does have additional costs)
* `Immutable`: New ASG + everything, then change, finally destroy old (High costs)
	* Temp ASG
	* 1 new instance in temp ASG -> if healthy, add remaining
	* Merge temp asg with previous
	* Terminate old version in merged ASG
* `*Blue/Green deployment`: Not a "direct feature" of Elastic Beanstalk

|                               |       Code deployed      |         Rollback        | Downtime | DNS Change |
|:-----------------------------:|:------------------------:|:-----------------------:|:--------:|:----------:|
|          All-at-once          |    Existing instances    |     Manual redeploy     |    Yes   |     No     |
|            Rolling            |    Existing instances    |     Manual redeploy     |    No    |     No     |
| Rolling with additional batch | Existing & New instances |     Manual redeploy     |    No    |     No     |
|           Immutable           |       New instances      | Terminate new instances |    No    |     No     |
|          Blue/Green*          |       New instances      |         Swap URL        |    No    |     Yes    |

## Troubleshooting

* `Environment turns to Red`
	* Review environment events
	* Pull logs
	* Rollback to previous version
* `Environment couldn't launch. EC2 instance profile doesn't exists.`
	* IAM role doesn't exists
	* IAM role doesn't have enough permissions
* `EB keeps replacing the environments`
	* Increase deployment timeout
* Make sure SG are correctly configured if accessing external resources

## [Back](README.md)