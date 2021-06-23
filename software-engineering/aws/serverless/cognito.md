# Cognito

- When we want to give our users an identity so they can interact with our application

- **Cognito User Pools**
  - Sign in functionaltiy for app users
  - Integrate with API gateway

- **Cognito Identity Pools (Federated Identity)**
  - Provide AWS creds to suers so they can access AWS resources directly
  - Integrate with Cognito User Pools as an identity provider

- **Cognito Sync**
  - Synchronize data frrom device to Cognito
  - Deprecated and replaced by AppSync

## User Pools (CUP)

- Create a serverless database of user for your mobile apps
- Simple login: Username (or email) / password combination
- Possibly to verify emails and phone numbers and add MFA
- Can enable Federated Identities (Faebook, Google, SAML...)
- Sends back a JSON Web token (JWT)
- Can be integrated with API Gateway for authentication

## Federated Identity Pools

- **Goal:**
 - Provide direct access to AWS Resources from the client side

- **How:**
 - Log in to federated identity provider - or remain anon
  - Get temp AWS creds back from the FIP
  - These creds come with a pre-defined IAM policy stating permissions

- **Example:**
  - prvoide (temp) acess to write to S3 bucket using Facebook Login

## Cognito Sync

- Deprecated and should use AWS AppSync now

- Store preferences, config, state of app
- Cross device sync (any platform - iOS, Android, etc)
- Offline capability (sync when back online)
- Requires FIP (Not User Pool)
- Store data in datasets (up to 1MB ea)
- Up to 20 datasets to synchronize