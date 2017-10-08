# Replication

# Lab

* Create bucket
```
# Create bucket in eu-west-2
aws s3api create-bucket \
    --bucket aws-certificate-replica-west \
    --region us-west-2

aws s3api put-bucket-versioning \
    --bucket aws-certificate-replica-west \
    --versioning-configuration Status=Enabled


# Create bucket in eu-east-1
aws s3api create-bucket \
    --bucket aws-certificate-replica-east \
    --region us-east-1

aws s3api put-bucket-versioning \
    --bucket aws-certificate-replica-east \
    --versioning-configuration Status=Enabled


# Create Policy
aws iam create-policy \
    --policy-name certificate-replica-policy \
    --policy-document file://S3/Replication/iam-role-replication.json


# Create IAM role
aws iam create-role \
    --role-name certificate-replica-role \
    --assume-role-policy-document file://S3/Replication/iam-role-trustedrelationships.json

# Attached policy
aws iam attach-role-policy \
    --policy-arn arn:aws:iam::484455220186:policy/certificate-replica-policy \
    --role-name certificate-replica-role
```

* Enable replication
```
aws s3api put-bucket-replication \
    --bucket aws-certificate-replica-west \
    --replication-configuration  file://S3/Replication/replica-configuration.json
```

# Summary

* Versioning should be enabled for cross-region replication
* Regions must be unique
* For replicate Standart-IA (Infrequently access) could be enabled
* Existing objects are not replicated, only new objects or changed objects