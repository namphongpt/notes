# [Instance store](../README.md)

* Physically attached to the instance
* Ephemeral storage
* Additional metrics that are only available for instance stores:
	* `DiskReadOps`
	* `DiskWriteOps`
	* `DiskReadBytes`
	* `DiskWriteBytes`
* Pros
	* Better I/O
	* Good for buffer, cache, scratch data, temporary content
	* Data survives reboot
* Cons
	* On stop/termination data is lost
	* Can't resize volume
	* Backups must be operated by the user

## [Back](../README.md)