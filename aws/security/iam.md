# [AWS IAM](../README.md)

## IAM & MFA

* MFA adds a level of security
* Accepts both virtual and physical MDA devices
	* Virtual: Google Authenticator / Authy
* Can be configured through the dashboard or CLI for root
* Can be configured for normal users
* Credentials report
	* CSV report on all IAM users and credentials
	* Shows who has MFA enabled

### Pass role

* Ability to assign a role to an instance/resource

## STS

* Security Token Service
* Allows to grant limited and temporary access to AWS resources
* Mostly used for cross account access
* Federation (AD)
	* Provides non AWS user temporary access by linking Active Directory credentials
	* Uses SAML (Security Assertion Markup Language)
	* Allows SSO (Single Sign On) which enables users to log in to AWS console without assigning IAM credentials
* Federation with 3rd party providers (Cognito)
	* Mainly in web and mobile applications
	* Makes use of Facebook/Google/Amazon etc to federate them

### Cross account access

* Define IAM role for another account
* Define which accounts can assume this role
* Use STS to retrieve credentials and impersonate this IAM role you have access to _(Assume role API)_
* Temporary credentials can be valid from 15 min to 12 hours (cannot be longer than the role allows)

## [Back](../README.md)