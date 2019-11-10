# [CloudFront](../README.md)

## General

* Content Delivery Network (CDN)
* Improves performance by caching content at the edge _(~136 edge points)_
* Popular with S3 but works well with EC2 & LB as well
* Can help protect against network attacks
* Can provide SSL encryption using ACM at edge
* Can also force CloudFront to talk to the application via HTTPS
* Supports RTMP
* Origin Access Identity (CloudFront user, using bucket policy we can restrict for this user only)

## CloudFront monitoring

* Can log every request made to CloudFront into an S3 bucket
* Can get reports based on access logs, but don't have to enable access logs to get these reports
	* `Cache statistics`: Get statistics on viewer requests grouped by HTTP status code
	* `Popular objects report`: Determine what objects are frequently being accessed
	* `Top referrers`: Display a list of the 25 website domains that originated the most HTTP and HTTPS requests for objects
	* `Usage reports`: Know the number of HTTP/HTTPS requests that CloudFront responds to from edge locations
	* `Viewers report`: Determine the locations of the viewers that access your content and the types of browsers they use
* CF caches `HTTP 4xx` (user doesn't have access) and `5xx` (gateway issues) status codes returned by S3

## [Back](../README.md)