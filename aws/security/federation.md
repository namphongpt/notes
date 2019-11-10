# [Federation](../README.md)

## General

* Lets users outside of AWS to assume temporary role to access AWS resources
* Federation assumes a form of a 3rd party authentication
	* LDAP
	* MS Active directory (~SAML)
	* Singe Sign On
	* Open ID
	* Cognito
* User management is done outside of AWS __(–> don't need to create users in AWS)__

## SAML Federations for Enterprises

* Integrate with AD / ADFS / any other SAML 2.0
* Auth with your Identity provider
* That returns a SAML assertion (token)
* This is recognized by AWS and lets you
	* Use the CLI (STS)
	* Access console (SSO, in the background uses STS)

### Custom Identity Broker

* If you don't have an identity provider compatible with SAML 2.0
* You have to implement the identity provider
* Lot more manual work
	* This is like a super user, as it can
		* Get sts credentials for any policy/user

## AWS Cognito Federated Identity Pools

* For public applications
* Goal
	* Provide direct access to AWS resources from the Client side
* How
	* Log into federated identity provider - or remain anonymous
	* Get temporary credentials back from the federated identity pool (from Cognito)
	* These come with pre-defined IAM policies

## [Back](../README.md)