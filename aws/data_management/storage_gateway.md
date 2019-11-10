# [Storage Gateway](../README.md)

## General

* Exposes S3 data to on-premise
* AWS storage types:
	* __Block__ (`EBS`, `Instance store`)
	* __File__ (`EFS`)
	* __Object__ (`S3`)
* General question
	* On premise data to Cloud => `Storage gateway`
* Detailed question
	* File access / NFS => `File gateway`
	* Volume / block storage / EBS / iSCSI => `Volume gateway`
	* VTL Tape Solution / Backup with iSCSI => `Tape gateway`

## File gateway

View files locally on-premise but they are backed in S3

* Configured S3 buckets are accessible using __NFS__ or __SMB__ protocols
* Support for all type of S3
* Bucket access using IAM roles for EACH File gateway
* Most recently used data is cached in gateway
* Can be mounted on many servers

## Volume gateway

View volumes locally on-premise but they are backed in EBS

* __iSCSI__ Protocol backed by S3
* Backed by EBS snapshots
* `Cached volumes`: Low latency access to most recent data
* `Stored volumes`: Entire dataset is on-premise, scheduled backups to S3

## Tape gateway

View archives locally on-premise but they are backed in Glacier

* Backups
* Virtual Tape Library (VTL)
* Backed by Glacier
* Summary

## [Back](../README.md)