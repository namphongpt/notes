# [ElastiCache](../README.md)

## General

* Managed `Redis` or `Memcached`
* Caches are in-memory databases with really high performance and low latency
* Helps reduce load off for DBs for read intensive workloads
* Helps make your application stateless
* Write Scaling: using __sharding__
* Read Scaling: using __read replicas__
* Multi AZ with failover
* AWS takes care of OS maintenance/patching, optimizations, setup, configuration, monitoring, backups

### Redis

* In memory Key-value store
* Super low latency
* Cache survives reboot by default (persistent)
* Great for
	* User sessions
	* Leaderboard
	* Distributed states
	* Relieve pressure from RDS database
	* Pub / Sub capability for messaging
* Multi AZ with auto failover
* Read replicas

### Memcached

* In memory object store
* Cache DOESN'T survive reboot

## [Back](../README.md)