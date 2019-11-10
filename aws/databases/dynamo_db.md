# [DynamoDB](../README.md)

## General

* Fully managed NoSQL database service
	* Multi-region
	* Multi-master
	* Provides fast and predictable performance with seamless scalability
* Tables do not have fixed schemas
* Synchronously replicates data across three facilities in an AWS Region
* Supports fast in-place updates
	* A numeric attribute can be incremented or decremented in a row using a single API call
* Uses cryptographic methods to securely authenticate users and prevent unauthorized data access
* Durability, performance, reliability, and security are built in, with SSD storage
	* Automatic 3-way replication
* Allows provisioned table reads and writes
	* Scale up throughput when needed
	* Scale down throughput four times per UTC calendar day
* Automatically partitions, reallocates and re-partitions the data and provisions additional server capacity as the
	* Table size grows
	* Provisioned throughput is increased
* Global Secondary indexes (GSI)
	* Can be created upfront or added later
* Consistency
	* __Eventually Consistent Reads__ _(Default)_
	* __Strongly Consistent Reads__
* Built-in security, backup and restore, and in-memory caching

### Global Table

* Replicated between regions

## DAX (DynamoDB Accelerator)

* Fully managed, highly available, in-memory cache for DynamoDB
* Delivers up to a 10x performance improvement

## [Back](../README.md)