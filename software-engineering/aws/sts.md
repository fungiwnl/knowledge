# STS - Security Token Service

- Allows to grant limited and temp access to AWS resources
- Token is valid for up to one hour (must be refreshed)
- AssumeRole
  - Within your own account: for enhanced security
  - Cross Account Access: assume role in target account to perform actions there
- AssumeRoleWithSAML
  - returne creds for users logged with SAML
- AssumeRoleWithWebIdentity
  - return creds for users logged with an IdP (Facebook Login, Google Login, OIDC compatible)
  - AWS recommends against using this, and using Cognito instead
- GetSessionToken
  - for MFA, from a user or AWS account root user

## Using STS to Assume a Role

- Define an IAM role within yuor account or cross-account
- Define which principals can access this IAM role
- Use AWS STS to retrieve creds and impersonate the IMA role you have access to (AssumeRole API)
- Temp creds can be valid between 15 mins to 1 hr

## Cross account access with STS

- Insert img

## Identity Federation in AWS

- Federation lets users outside of AWS to assume temp role for accessing AWS resources
- These users assume identity provided access role

- Federations can have many flavours
  - SAML 2.0
  - Cusomt identity broker
  - Web identity fed with Cognito
  - Web identity fed without Cognito
  - SSO
  - Non SAML with AWS MicrosoftAD

- Using federation, you dont need to create IAM users (user management is outsidde of AWS)

## SAML 2.0 Federation

- To itnegrate Active Directory / ADFS with AWS (or any SAML 2.0)
- Provides access to AWS Console or CLI (through temp creds)
- No need to create an IAM user for each of your employees


