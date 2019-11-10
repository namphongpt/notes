# [Aurora](../README.md)

## General

* Proprietary
* Not open source BUT compatible with MySQL/PostgreSQL drivers
* Cloud optimized: 5x MySQL performance and 3x PostgreSQL performance
* Storage automatically grows in 10GB increments up to 64TB
* Up to 15 read replicas, and faster replication
* HA native, automatic failover => instantaneous
* 20% more expensive (but more efficient too)
* Backtrack (PITR without backups)

## High availability

* 6 copies of your data across 3 AZs
	* 4 copies required to Write
	* 3 copies required to Read
* Self healing with P2P replication
* Storage is stripped across 100s of volumes
* 1 master (takes read and writes)
	* Failover takes less than 30 seconds for master
* Supports cross region replication

## Aurora DB Cluster

* __Writer endpoint__
	* Always points to master
	* In case of failover, the endpoint won't change
* __Reader endpoint__
	* Connection LoadBalancing
	* Connects to all Read replicas automatically

## Aurora Serverless

* Don't need to chose instance size
* Only supports MySQL 5.6, PostgreSQL
* Can migrate between Aurora Cluster <-> Aurora Serverless
* Aurora Capacity Units (ACU)
* Billed in 5 minutes increments ACU

## [Back](../README.md)