# S3 Fundamentals (Simple Storage Service)

Created: May 8, 2019 5:26 PM
Updated: May 8, 2019 7:24 PM

Infinitely scalable storage service from AWS and one of the key building blocks for the Amazon Cloud.

No concept of directories in S3, only key-names.

Any file size over 5GB is considered a multi-part upload and the max file size is 5TB.

Metadata is totally customizable.

Versioning IDs are available for versioning.

**Versioning**

- Accomplished at the Bucket level
- Increments object version on each overwrite
- Helps:
    - Protect against deletes (restore previous)
    - Easy rollback
- Any file not versioned before enabling versioning will have “null” version
- Deleted files WITH VERSIONING are persisted and only marked “delete”

**Encryption**

Four methods:

1. SSE-S3: encrypts S3 objects using keys handled and managed by AWS
    1. Encrypted Server Side
    2. AES-256 encryption
    3. Set header on send “x-amz-server-side-encryption”: “AES256”
    4. When data is sent to S3, a S3 Managed Data Key is created for encryption
2. SSE-KMS: leverage AWS key management service to manage encryption keys
    1. More control over key rotation as well as an audit trail of the keys use
    2. Object is encrypted server side
    3. Set header on send “x-amz-server-side-encryption”: “ams:kms”
    4. When data os sent to S3, a KMS Customer Master Key (CMK) is used for encryption
3. SSE-C: you provide and manage your own encryption keys
    1. Key is managed OUTSIDE AWS
    2. Amazon will NOT store the provided encryption key
    3. HTTPS is the required protocol
    4. Every request must contain the encryption key in the HTTP headers
    5. Both the data and encryption key is sent via HTTPS to S3, AWS performs the encryption, throws away the key and stores the object
4. Client Side Encryption
    1. Use a client library like Amazon S3 Encryption Client
    2. Data must be encrypted by client before sending
    3. Data must be decrypted by client upon retrieval
    4. Customer fully manages key and encryption cycle
5. Encryption in Transit (SSL/TLS)
    1. HTTP endpoint for non encrypted traffic
    2. HTTPS endpoint for encryption in flight

**Security**

User based:

- IAM policies - which API calls should be permitted for a specific user
- MFA can be required in versioned buckets to delete objects.
- URLs can be signed for limited access to objects.

Resource Based:

- Bucket policies - bucket wide rules from the S3 console, allows for cross account.
    - JSON based policy declaring
        - Resources
        - Actions
        - Effect
        - Principal
    - Allows us to:
        - Grant access
        - Force encryption
        - Grant access to other accounts
- Object Access Control List (ACL) - fine grained control
- Bucket Access Control List (ACL) - uncommon

S3 Supports VPC endpoints, meaning that your instances without www internet can access S3. Additionally, you can enable logging and audit files.

**Performance**

Historically, S3 performance would degrade after 100 transactions per second (TPS). Performance could be optimized by fronting key-names with random characters.

Currently it can scale up to 3500 PUTS per second and 5500 GETS for EACH PREFIX.

CloudFront CDN helps improve read performance. S3 Transfer Acceleration helps with distant uploads.

SSE-KMS encryption may affect performance slightly.