# API Gateway

- Serverless API service

- AWS Lambda + API Gateway: No infra to manage
- Support for the WebSocket Protocl
- Handle API versioning (v1, v2...)
- Handle different environments (dev, qa, prod..)
- Handle security (authenication, authorization)
- Create API keys, handle request throttling
- Swagger/OPEN API import to quickly define APIs
- Trasnform and validate requests and responses
- Generate SDK and API sepcs
- Cache API responses

## Integrations high level

- Lambda Function
  - Invoke Lambda 
  - Easy way to expose REST API backed by Lambda
- HTTP
  - Expose HTTP endpoints in the backend
  - Example: internal HTTP API on premise, ALB
  - Why? Add rate limiting, caching, user authentications, API keys, etc
- AWS Service
  - Expose any AWS API through the API gateway
  - Example: start an AWS step Function workflow, post a message to SQS
  - Why? Add authentication, deploy pubicly, rate control

## Endpoint types

- **Edge-Optimized** (default): for global clients
  - Requests are routed through the CloudFront Edge locations (improves latency)
  - The API gateway still lives in only one region
- **Regional:**
  - For clients within the same region
  - Could manially combined with CloudFront (more control over the caching strategies and distribution)
- **Private:**
  - Can only be accessed from your VPc using an interface VPC endpoint (ENI)
  - Use a resoruce policy to define access

## Practical

- Create Lambda functions
- Create API gateway
- Hook API gateway to lambda API functions
- Deploy APi gateway to dev

## Security IAM permissions

- Create an IAM policy authorixation and attach to User/ Role
- API gateway verifies IAM permissions passed by the calling application
- Good to provide access within your infrastastructure
- Leverages "Sig v4" capability where IAM credential are in headers

## Lambda Authorizer (formerly Custom Authorizers)

- Uses Lambda to validate the token in header being passed
- Option to cache result of authentication
- Helps to use OAuth / SAML/ 3rd party type of authentication
- Lambda must return an IAM policy for the user


## Security - Cognito User Pools

- Cognito fully manages user lifecycle
- API gateway verifies identity automatically from Cognito
- No custom implementation required
- Cognito only helps with authentication and not authorization

## Security Summary

- IAM:
  - Great for users/roles already within AWS account
  - Handle authentication and authorixation
  - Leverages Sig v4

- CustomAuthorizer
  - Great for 3rd party tokens
  - Very flexible in terms of what IAM policy is returned
  - Handle Authenticaiton + Authorization
  - Pay per Lambda invocation

- Cognito User Pool
  - You manage your own user pool ( can be backed by Faceboko, Google login, etc..)
  - No need to write any custoom code
  - Must implement authorization in the backend