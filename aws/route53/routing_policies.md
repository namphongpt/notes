# [Route53 Routing Policies](../README.md)

## Simple routing policy

* Maps a domain to one URL
* When: Redirect to a single resource
* Can't attach health checks
* If multiple values are returned, the __Client__ chooses one randomly

## Weighted routing policy

* Control the % of the requests that go to a specific endpoint
* Can be associated with health checks –> No traffic will be sent if instance is unhealthy
* Client is unaware of multiple IPs

## Latency routing policy

* Redirects to a server which has the least latency to you
* Asks which aws region the IP is in

## Failover routing policy

* Must be a __primary__ and a __secondary__ endpoint
* Must have a health check created for the primary endpoint
* Automatically switches when health check failed

## Geolocation routing policy

* Different from Latency!
* Based on user's geological location
* Should create a default policy (in case the geo is not defined)
* E.g.: 
	* Traffic from UK goes to: `X.X.X.X`
	* Traffic from US goes to: `Y.Y.Y.Y`
	* Default goes to:         `X.X.Y.Y`

## Multi value routing policy

* Use when want to route to multiple instances & associate a health check
* Up to 8 healthy records are returned for each multi value query
* Its not a substitute for LB
* They all have the same TTL

## [Back](../README.md)