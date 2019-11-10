# [SnowBall & SnowBall Edge & SnowMobile](../README.md)

## Snowball

* Physical data transport that helps move data in or out AWS __(TBs or PBs)__
* Up to `80 TB`
* Alternative to moving data over network (save network fee)
* Secure, temper resistant, KMS 256 bit encryption
* Tracking using SNS and text messages
* E-ink shipping label
* Pay per data transfer job
* "If it takes more than 2 weeks over network, choose snowball"
* Process
	* Request snowball device from Amazon
	* Install snowball client on your servers
	* Copy files over
	* Ship back device (automatically goes to the correct facility)
	* Data loaded into an S3 bucket
	* Snowball is wiped

## Snowball Edge

* Adds computational capability to the device
* __100 TB with either__
	* Storage optimized (24 vCPU) - `100TB`
	* Compute optimized (52 vCPU & optional GPU) - `42 TB`
* Supports custom AMI, so you can perform operations on the go
* Support custom Lambda function

## Snowmobile

* An actual truck
* Exabytes of data (1 EB = 1 million TB)
* 1 truck = 100 PB -> Multiple trucks in parallel
* Better than snowball if you want to transfer more than 10 PB

## [Back](../README.md)