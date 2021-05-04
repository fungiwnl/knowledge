# AWS Security & Encryption

## Why encryption?

### Encryption in flight (SSL)

- Data is encrypted before sending and decrypted after receiving
- SSL certificates help with encryption (HTTPS)
- Encryption in flight ensures no MTM (man in the middle attack) can happen
- [Insert diagram]

### Server side encryption at rest

- Data is encrypted after being received by the server
- Data is decrypted before being sent
- It is stored in an encrypted form thanks to a key (usually a data key)
- The encryption / decryption keys must be managed somwewhere the server must have access to it
- [Insert diagram]

### Client side encryption

- Data is encrypted by the client and never decrypted by the server
- Data will be decrypted by a receiving client
- The server should not be able to decrypt the data
- Could leverage Envelope Encryption
- Insert [Envelope encrytpion diagram]

## KMS (Key management service)

- Anytime you hear "encrytpion" for an AWS service, it's most likely KMS
- Easy way to control access to your data, AWS manages keys for us
- Fully integrated with IAM for auth
- Seamlessly integrated into
   - EBS
   - S3
   - Redshift
   - RDS
   - SSM
   - Etc
- You can also use with CLI/SDK

### Customer Master Key (CMK) Types
 
- Symmetric (AES-256 keys)
  - First offering of KMS, single encryption ke y that is used to Encrypt and Decrypt
  - AWS services that are integrated with KMS use Symmetric CMKs
  - Necessary for envelope encryption
  - You never get access to the Key unencrypted (must call KMS API to use)
- Asymmetric (RSA & ECC key pairs)
  - Public (Encrypt) and Private Key (Decrypt) pair
  - Used for Encrypt/Decrypt or Sign/Verify operations
  - Public key is downloadable, but you can't access the Private key unencrypted
  - Use case: encryption outside of AWS by users who can't call KMS API

#### Symmetric keys

- Able to fully manage the key & policies
  - Create
  - Rotation policies
  - Disable 
  - Enable
- Able to audit key usage (via CloudTrail)
- Three types of CMK
  - AWS managed service default CMK: free
  - User keys created in KMS: $1 / month
  - User keys imported (must be 256-bit symmetric key) - $1 /month
  - + pay for API call to KMS ($0.03 / 10,000 calls)

## When would you use KMS

- Anytime you need to share sensitive info.. use KMS
  - Database passwords
  - Creds to external service
  - Private key of SSL certs

## KMS 101

- The value in KMS is that the CMK used to encrypt data can never be retrieved by te user, and the CMK can be rotated for extra security
- Never ever store your secrets in plaintext, especially in code
- Encrypted secrets can be stored in code / env vars
- KMS can only help in encrpyting up to 4KB of data per pcall
- If data > 4 KB, use envelope encryption

- To give access to KMS to someone
  - Make sure the Key Policy allows the user
  - Make sure the IAM Policy allows the API calls

## KMS Key Policies

- Control access to KMS keys, 'similar' to S3 bucket polciies
- Difference:  you cannot control access without them
- **Default KMS Key Policy**:
  - Created if you don't provide a specific KMS key policy
  - Complete access to te key to the root user = entire AWS account
  - Give access to the IAM policies to the KMS key
- **Custom KMS Key Polcy:*
  - Define users, roles that can access the KMS key
  - Define who can adminster the key
  - Useful for corss account access of your KMS keys

## Copy snapshots across accounts

1. Create a Snapshot, encrypted with your own CMK
2. Attach a KMS key policy authorize cross account access
3. Share the encrypted snapshot
4. (in target) Create a copy of the Snapshot, encrypt it with KMS key in your account
5. Create a volume from the snaphot

## KMS Hands on w/ CLI

 
