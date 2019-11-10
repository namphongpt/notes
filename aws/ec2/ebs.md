# [EBS](../README.md)

## General

* Network drive to attach to a running instance and persist data on it
* Can detach from an instance and attach to another __in the same AZ!__
* Can move between AZs but need to snapshot first
* Have a provisioned capacity (size in GBs, IOPS)
	* Billed on this
* Can increase capacity over time
* Boot volume can only by _GP2_ or _IO1_
* Possible to resize images
	* Can do it while the volume is being used
	* Can only increase
		* Volume size
		* IOPS _(only in IO1)_
	* After resize, __need to repartition the drive!__
* Can migrate volumes between AZs / Regions
	* Snapshot volume
	* _(Optional) Copy to another region_
	* Create a volume from the snapshot in the AZ of your choice
* EC2 won't start with EBS set as root volume
	* Make sure you didn't name it `/dev/xvda`
* If you use EBS for high-performance: Use EBS optimized instance types
* If you want to use the root volume after termination -> Set `Delete on Termination` to `No`
* Still paying for EBS volumes even if it is unused
* High wait times / Slow response from SSD
	* Increase IOPS
	* Change to IO1
* Some commands:
	* `lsblk`: List volumes
	* `df -h`: See partitions
	* `vim /etc/fstab`: Edit mount volumes on boot
* Types

|                            |               GP2               |                           IO1                          |                     SP1                    |           SC1           |
|:--------------------------:|:-------------------------------:|:------------------------------------------------------:|:------------------------------------------:|:-----------------------:|
|            Name            |         General purpose         |                    Provisioned IOPS                    |          Throughput optimized HDD          |         Cold HDD        |
|            Type            |               SSD               |                           SSD                          |                     HDD                    |           HDD           |
| Can be used as boot volume |               Yes               |                           Yes                          |                     No                     |            No           |
|         Volume Size        |           4GB - 16 TB           |                      1 GB - 16 TB                      |               500 GB - 16 TB               |      500 GB - 16 TB     |
|     Use case/workloads     | General Boot volume Low latency | I/O-intensive Critical DBs Low latency High throughput | Low-cost Big data Log processing Streaming | Lowest cost Colder data |
|       Max IOPS per GB      |         3x (Size in GB)         |                    50x (Size in GB)                    |                      -                     |            -            |
|       Max throughput       |              250 MB             |        500 MB (32000 IOPS) 1000 MB (64000 IOPS)        |                   500 MB                   |          250 MB         |

### GP2 Volume burst

* Volume is less than 1000GB (means IOPS is less than 3000) then it can burst to 3000 IOPS
* If balance is 0 all the time
	* Increase volume size
	* Switch to IO1
* Monitor via CloudWatch the I/O credit

### Computing throughput based on IOPS

* GP2
	* Throughput = `(Volume size in GiB) x (IOPS per GiB) x (I/O size in KiB)`
		* Max 250  MiB/s
* IO1
	* Throughput = `(Provisioned IOPS) x (I/O size in KiB)`
		* Max 500 MiB/s (32000 IOPS)
		* Max 1000 MiB/s (64000 IOPS)
	* The maximum ratio of provisioned IOPS to requested volume size (in GiB) is __50:1__.
	* Provisioned IOPS Volume size is 10 GiB, what is the maximum value that can be put as the IOPS?
		* 500

## EBS Snapshots

* __Incremental__: only backs up changed blocks
* Backups use the disk's I/O (don't run backup when handling workload)
* Stored in S3 _(not seen by you)_
* Max `100000` backups per Account
* Can copy snapshots between AZs / Regions
* Can create AMI from snapshot
* EBS volumes restored from snapshots need to be __pre-warmed__ (`fio` pr `dd`)
* Snapshots can be automated via `Amazon Data Lifecycle Manager`

## EBS Encryption

* All encryption is handled by Amazon _(KMS: AES-256)_
* Impact is minimal
* Data at rest is encrypted
* Data in flight is encrypted
* All snapshots are encrypted
* All volumes are encrypted
* Encrypt an un-encrypted volume
	* Create snapshot
	* Encrypt snapshot
	* Create new volume from encrypted snapshot
	* Attach new volume in place of the old

## EBS RAID

* EBS is already redundant (Replicated withing AZ)
* RAID is possible as long as the OS supports it (have to do it through OS, not an Amazon "feature")
	* `RAID 0`
		* __Increase performance__
		* If 1 disk fails, you lose data
		* Could go to 10K IOPS -> 10 disk each having 1k IOPS
		* Use cases
			* Application needs a lot of IOPS and doesn't need fault tolerance
			* DB that has replication built-in
	* `RAID 1`
		* __Increase fault tolerance by Mirroring__
		* Have to send data to 2 EBS -> 2x Network
		* Use cases
			* Application that needs to increase volume fault tolerance
	* RAID 5 - Not recommended for EBS 
	* RAID 6 - Not recommended for EBS 

## CloudWatch for EBS

### CloudWatch Metrics

* Metrics
	* `VolumeIdleTime`: Number of seconds when no read/write is submitted
	* `VolumeQueueLength`: Number of operations waiting to be executed. (High number means probably IOPS or application issue)
	* `BurstBalance`: If becomes 0, need a volume with more IOPS
* GP2: every 5 minutes
* IO1: every 1 minutes
* EBS Volume have status checks
	* `Ok`: Performing good
	* `Warning`: Performance below expected
	* `Impaired`: Stalled, performance is severely degraded
	* `Insufficient-data`: Metric data collection is in progress

### CloudWatch Events

* EBS emits notification for volume, snapshot, and encryption status changes.
* With CloudWatch Events you can establish rules that trigger programmatic actions in response
	* E.g: Trigger Lambda to copy snapshot over to another region

## [Back](../README.md)