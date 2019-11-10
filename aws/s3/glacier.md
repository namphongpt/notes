# [Glacier](../README.md)

## General

* Low cost storage for archiving / backup
* Data is retained for a long time (10s of years)
* Alternative to on-premise magnetic tape storage
* 11 nine durability
* $0.004/GB + retrieval fee
* `Object` in other tiers = `Archive` in Glacier
* An archive can be up to 40 TB
* Archives are stored in `Vaults` (again, different naming convention)
* Operations
	* `Upload` (single, or multi part upload)
	* `Download`: Initiate a retrieval request, wait for file to be ready, limited time to download!
	* `Delete` (Use SDK or Glacier REST API)
* Restore links have an expiry date
* 3 retrieval options:
	* __Expedited__: 1 to 5 minutes retrieval, `$0.03/GB` + `$0.01/request`, Capacity units
	* __Standard__: 3 to 5 hours retrieval, `$0.01/GB` + `$0.05/ 1000 request`
	* __Bulk__: 5 to 12 hours retrieval, `$0.025/GB` + `$0.025/ 1000 request`

## Vault lock & policies

* Vault Collection of archives
* Each Vault has:
	* 1 Vault __access policy__ (JSON), similar to bucket policies
	* 1 Vault __lock policy__
		* Immutable
		* A policy that has been locked. E.g.: Can never be changed, removed
			* Example 1: `WORM policy`: Write Once, Read Many
			* Example 2: Cannot delete archives that are younger than 1 year
		* When creating a lock policy, you get a LockID: 24 hours to confirm lock policy

## [Back](../README.md)