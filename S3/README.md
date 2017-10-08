# S3 Overview

S3 (Simple Storage Service) provide object storage capabilities.

* Object storage (key-value storage)
* Files could be from 0 bytes to 5 TB
* Provides unlimited storage
* Files are stored in Bucket
* S3 has universal namespace, names must be unique globally
* Address format: https://s3-<region>, for example: https://s3-eu-west-1.amazonaws.com/bucket-name
* If file uploaded sucessfull it will always return 200 response code

# Data Consistency

* Read after Write consistency for PUTs of new Objects (you will get immidiate consistency)
* Eventual Consistency for overwrite PUTs and DELETEs (for updates and deletes, it will take some time to probagate (depending on size 0ms - 50ms, just a guess))
* Objects updates are atomic (it will be never partially updated)

# Data Model

* Account
** Bucket
*** Object
**** Key - object name (file name)
**** Value - data (sequence of bytes)
**** VersionId - id of current version
**** Metadata - metadata for object
**** Subresource - 
***** Access Control List - permissions
***** Torrent - support of bittorrent protocol

# Availability

Amazon garantee 99,9% availability and 99,99999999999 (11x9's) duarbility for S3 information

# S3 Features

* Versioning - 
* Tiered Storage: 
** S3 - 99,9 availability, designed to sustain the loss of 2 facilities concurrently
** S3 IA (Infrequently Access) - lower fee than S3, but charge for data retrival
** Reduced Redundancy Storage - designed to provide 99,99% durability and 99,99 availability
** Glacier - very cheap, used for data archival only (3-5 hours for data retrival) (no SLA)
* Lifecycle Management - 
* Encryption - 
* Security - Access Control Lists (ACL) and Bucket Policies

# S3 Charges

* Storage
* Requests
* Storage Management Pricing - 
* Data Transfer - for replication
* Transfer Acceleration - 

# References

Mandatory to read:
* S3 FAQ: https://aws.amazon.com/s3/faqs/