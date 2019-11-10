# [AWS CloudWatch](../README.md)

## Metrics

* Metrics for all AWS services
* Metric is a variable to monitor
* Metrics belong to __namespaces__ (groups)
* __Namespace is mandatory!__
* __Dimension__ is an attribute of a metric (instance_id, env, etc...)
* Up to 10 dimensions
* Metrics have timestamps
* Metrics exist only in the region in which they are created
* Metrics cannot be deleted, but they automatically expire in 14 days if no new data is published to them
* Retention
	* One minute data points are available for 15 days.
	* Five minute data points are available for 63 days.
	* One hour data points are available for 455 days (15 months).
* Can create a dashboard out of metrics
* Can aggregate metrics

### Custom metrics

* Possible to define your own metrics
* Able to use dimensions
* Metric resolution is 1 minute _(default)_, can go up tp every second _(extra fee)_
* API: `PutMetricData`
	* Can only publish one data point per call
* __CloudWatch aggregates the data to a minimum granularity of 1 minute__
* Time stamp can be up to __2 weeks in the past__ and up to __2 hours into the future__
* Throttle errors -> Exponential back off
* New metrics can take 15 minutes to show up in the console

### EC2 Detailed monitoring

* EC2 instance have metrics every 5 minutes (default)
* Detailed monitoring can be every 1 minute (extra cost)
* AWS free tier allows for 10 detailed monitoring metrics

## Dashboard

* Quick access for key metrics
* Dashboards are __global__
* Can include graphs from different regions
* Can change time zone and time range for dashboards
* Can set up auto refresh
* Pricing
	* 3 dashboards (up to 50 metrics): Free
	* $3/month/dashboard 
* How to create global dashboard -> Add metrics from different region
* __Cannot aggregate metrics from regional metrics!__

## Logs

* Application can send logs using CLI
* By default it stores the log data indefinitely
* Retention can be changed for each log group at any time
* AWS Services that are logging directly:
	* ElasticBeanstalk
	* ECS
	* Lambda
	* VPC Flow logs
	* API Gateway
	* CloudTrail based on filter
	* CloudWatch Log Agent
	* Route53: DNS queries
* CW Logs can be exported to S3 or ElasticSearch
* Architecture
	* `Log group`
	* `Log streams`
	* `Expire policy`
* Make sure IAMs are correct
* Logs can be encrypted using KMS at group level
* Can use filter expressions
	* Search for a specific IP
	* Set up metric filter to trigger alarms
* Log insights
	* Common queries to Dashboard

## Alarms

* Trigger notification on any metric
* Alarms can go to Auto Scaling, EC2 Actions, SNS notifications
* Alarms exist only in the region in which they are created.
* Alarm actions must reside in the same region as the alarm
* Alarm history is available for the last 14 days.
* Various options (sampling, %, min, max, etc...)
* Alarm states
	* `OK`
	* `INSUFFICIENT_DATA`
	* `ALARM`
* Period
	* Length of time to evaluate metric
	* High resolution custom metrics: only 10 or 30 seconds
* Targets
	* Stop, Terminate, Reboot, Recover EC2 instances
	* Trigger autoscaling actions
	* Send message to SNS (from which you can do pretty much anything)
* CW doesn't test or validate the action assigned
* To test an alarm use the CLI
	* `aws cloudwatch set-alarm-state --alarm name "alarm" --state-value ALARM --state-reason "Testing"`

## Events

* Source + Rule => Target
* Schedule: Cron jobs
* Event pattern: Event rules to react to a service doing something
* Triggers to Lambda functions/SQS/SNS/Kinesis ...
* Creates a small JSON document to give further information about the change

## [Back](../README.md)