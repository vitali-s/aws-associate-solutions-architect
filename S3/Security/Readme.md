# Security

* By default, buckets are private
* Access configured by:
  * Bucket policies
  * Access Control Lists (ACL)
* S3 supports access logging of all requests to S3 to another bucket or even account

# Encryption

* In Transit - SSL/TLS
* At Rest
  * Server Side Encryption
    * S3 Managed Keys - SSE-S3 (key is encrypted with master key, master key is rotated)
    * AWS KSM - Key Management Service, SSE-KMS (managed service, audit logs of keys usage)
    * Server Side Encryption with Customer provided keys - SSE-C
  * Client Side Encryption - you responsible for data encryption

# References
[Data Encryption] (http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingEncryption.html)