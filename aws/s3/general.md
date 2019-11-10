# [S3](../README.md)

## General

* `Buckets` _(directories)_ are storing `objects` _(files)_
* Buckets' name must be globally unique
* S3 is a regional service
* Naming conventions
	* No uppercase
	* No underscore
	* 3-63 characters long
	* Not an IP
	* Must start with lowercase letter or number
* `Objects` have a key
	* The key is the full path
* There is no concept of directories (but in the UI does look like it)
* `ObjectValues`
	* Content of the body
	* Max size is 5 TB
	* If file is larger than 5 GB, must use `multi-part upload`
* `Metadata`
	* Key-Value pairs
* `Tags`
	* Key-value pairs
	* Maximum 10 tags
* `VersionID`
* Open a file
	* Right click -> Open: Uses correct permissions
	* Object link -> Access denied (as it is a public link)

### Storage tiers

|                            | Availability |   Durability  |
|:--------------------------:|:------------:|:-------------:|
|          Standard          |    99,99%    | 99,999999999% |
| Reduced Redundancy Storage |    99,99%    |     99,99%    |
|      Infrequent Access     |    99,99%    | 99,999999999% |
|         One Zone IA        |    99,95%    |     99,99%    |
|     Intelligent Tiering    |     99,9%    | 99,999999999% |
|           Glacier          |    99,99%    | 99,999999999% |

* `Standard`: General purpose
	* Can sustain 2 az outage
* `Reduced redundancy storage`
	* DEPRECATED
* `Infrequent Access (IA)`
	* Not accessed regularly but when it does, need quick access
	* Lower cost compared to Standard
	* Fee when accessing objects
* `One Zone Infrequent Access (One zone IA)`
	* Same as IA but only in 1 AZ
	* If AZ is DESTROYED (not down), then data is lost!
	* Lower cost than IA (~20%)
* `Intelligent Tiering`
	* Announced in 2018
	* Best of all, as it can move object to the correct tier
	* Small monthly fee for auto-tiering
* `Glacier`

## Versioning

* Have to enable at bucket settings
* Same key overwrite will increment version, and it will keep all versions
* Any file that is not versioned prior to enabling versioning will have `Version ID: null`
* Deleting a versioned file: __Adds a delete marker__, won't delete previous versions 
* Can protect against hackers, cause each version is a separate file
* Cannot delete bucket unless all objects AND all versions are deleted first
* __If an object has millions of versions, it can affect performance!__

## Lifecycle rules

* Set of rules to __move data between different tiers__ to save costs
	* `Transition actions`
		* Move objects into another tier
	* `Expiration actions`
		* Delete objects after a certain period
	* Delete incomplete multipart uploads

## Storage Class Analytics

* Daily report
* First report takes 1-2 days
* Does NOT work for `OneZone IA` or `Glacier`
* Setup analytics to __help determine when to transition objects to different tiers__

## Cross Region Replication

* Asynchronously replicate
* __Must enable source and destination bucket versioning!__
* Buckets can be in different accounts
* Must give proper IAM permissions

## Inventory

* Helps to manage storage
* __Audit and report on replication and encryption status of your objects__
* Data for the Source bucket has to go to a Target bucket (need to set up IAM permissions)

### Static website

* Can host static website
* URL Format
	* `<bucket_name>.s3-website.<aws_region>.amazonaws.com`
	* `<bucket_name>.s3-website-<aws_region>.amazonaws.com`
* If you get `403` -> Make sure bucket policy allows __Public read__ on the bucket!
* Properties -> Enable static website
	* Set index document
* Permissions -> Public access settings
	* Enable public access
* Set bucket policy to allow public read

### CORS

* Cross Origin Resource Sharing
* If you request data from another S3 bucket, need to set CORS
* Allows to limit the number of websites that can request your files (~limits your costs)

### Pre-signed URL

* Can be generated via SDKs or CLI
* Default: valid for 1 hour (3600 seconds) `--expires-in [time_in_seconds]`
* The URL will inherit your permissions], so whoever uses the link will be able what you could
* `aws configure set default.s3.signature_version s3v4`
* Set `--region` appropriately

### Consistency model

* __Read after Write consistency for PUTs of new objects__
	* As soon as the object is written, we can access it
		* `PUT 200` -> `GET 200`
	* Except!
		* `GET 404` -> `PUT 200` -> `GET 404`, but eventually will be consistent
* __Eventual consistency for DELETEs and PUTs of existing objects__
	* Might get older version after updating it
		* `PUT 200` -> `PUT 200` -> `GET 200` (might be older version)
		* `DELETE 200` -> `GET 200`

## [Back](../README.md)