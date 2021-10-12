# AWS KMS (Key Management Service)

- Anytime you hear “encryption” for an AWS service, it’s most likely KMS
- Easy way to control access to your data, AWS manages keys for us
- **Fully integrated with IAM for authorization**
- Seamlessly integrated into:
  - Amazon EBS: encrypt volumes
  - Amazon S3: Server side encryption of objects
  - Amazon Redshift: encryption of data
  - Amazon RDS: encryption of data
  - Amazon SSM: Parameter store
  - Etc…
- But you can also use the CLI / SDK

## KMS – Customer Master Key (CMK) Types

- **Symmetric (AES-256 keys)**
  - First offering of KMS, single encryption key that is used to Encrypt and Decrypt
  - AWS services that are integrated with KMS use Symmetric CMKs
  - Necessary for envelope encryption
  - You never get access to the Key unencrypted (must call KMS API to use)
-** Asymmetric (RSA & ECC key pairs)**
  - Public (Encrypt) and Private Key (Decrypt) pair
  - Used for Encrypt/Decrypt, or Sign/Verify operations
  - The public key is downloadable, but you can’t access the Private Key unencrypted
  - Use case: encryption outside of AWS by users who can’t call the KMS API

## AWS KMS (Key Management Service)

- Able to fully manage the keys & policies:
  - Create
  - Rotation policies
  - Disable
  - Enable
- Able to audit key usage (using CloudTrail)
- Three types of Customer Master Keys (CMK): 
  - AWS Managed Service Default CMK: free
  - User Keys created in KMS: $1 / month
  - User Keys imported (must be 256-bit symmetric key): $1 / month
- + pay for API call to KMS ($0.03 / 10000 calls)

## AWS KMS 101

- Anytime you need to share sensitive information… use KMS
  - Database passwords
  - Credentials to external service
  - Private Key of SSL certificates
- The value in KMS is that the CMK used to encrypt data can never be retrieved by the user, and the CMK can be rotated for extra security

### AWS KMS 101 pt. 2

- Never ever store your secrets in plaintext, especially in your code!
-  Encrypted secrets can be stored in the code / environment variables
-  KMS can only help in encrypting up to 4KB of data per call
-  If data > 4 KB, use envelope encryption
-  To give access to KMS to someone:
  -  Make sure the Key Policy allows the user
  -  Make sure the IAM Policy allows the API calls

## Copying Snapshots across regions

1. Take snapshot of encrypted EBS volume in region A
2. Move encrypted snapshot to region B
3. Create EBS volume from encrypted snapshot in region B
4. KMS ReEncrypt with KMS Key B

## KMS Key Policies

- Control access to KMS keys, “similar” to S3 bucket policies
- Difference: you cannot control access without them
- **Default KMS Key Policy**:
  - Created if you don’t provide a specific KMS Key Policy
  - Complete access to the key to the root user = entire AWS account
  - Gives access to the IAM policies to the KMS key
- **Custom KMS Key Policy**:
  - Define users, roles that can access the KMS key
  - Define who can administer the key
  - Useful for cross-account access of your KMS key

## Copying Snapshots across accounts

1. Create a Snapshot, encrypted with your own CMK
2. Attach a KMS Key Policy to authorize cross-account access
3. Share the encrypted snapshot
4. (in target) Create a copy of the Snapshot, encrypt it with a KMS Key in your account
5. Create a volume from the snapshot

## KMS Key Rotation

### KMS Automatic Key Rotation

- For **Customer-managed CMK** (not AWS managed CMK)
- If enabled: automatic key rotation happens **every 1 year**
- Previous key is kept active so you can decrypt old data
- New Key has the same CMK ID (only the backing key is changed)

### KMS Manual Key Rotation

- When you want to rotate key **every 90 days, 180 days, etc…**
- New Key has a different CMK ID
- Keep the previous key active so you can decrypt old data
- Better to use aliases in this case (to hide the change of key for the application)
- **Good solution to rotate CMK that are not eligible for automatic rotation (like asymmetric CMK)**

### KMS Alias Updating

- Better to use aliases in this case (to the hide change of key for the application)
- Call UpdateAlias API to point alias to the newly created key

### Summary

- If you want automatic key rotation, it will be 1 year
- If not, do manual key rotation
