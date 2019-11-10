# [AWS Organizations](../README.md)

## General

* Global service
* Allows to manage multiple accounts
* Main account -> Master account (can't change)
* Member accounts can only be part of one organization
* Consolidated billing accounts -> single payment method
* Pricing benefits from aggregated usage
* API is available to automate AWS account creation

### OUs and Service Control Policies

* Organize accounts in: __Organizational Units (OU)__
	* eg. dev, test, prod, finance....
* Can nest OUs in OUs
* Apply SCPs in OUs
	* Permit/Deny access to AWS services
	* Similar syntax to IAMs
	* It's a filter to IAMs
* Helpful for
	* Sandbox account creation
	* Separate dev and prod
	* Only allow approved services

## [Back](../README.md)