# Uploading

Things to remember:
* 200 OK is always returned when object is uploaded successfully

## Operations overview

* S3 API: http://docs.aws.amazon.com/cli/latest/reference/s3api/index.html

* Single file/object operations, if no --recursive flag is provided.
** cp
** mv
** rm
* Folder operations
** sync
** mb
** rb
** ls
* Exclude and include files: '--exclude "*" --include "*.txt"'



## Copy Files

### Create policy with bucket access

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetBucketLocation",
                "s3:ListAllMyBuckets"
            ],
            "Resource": "arn:aws:s3:::*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::aws-certificate-train-0"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject"
            ],
            "Resource": "arn:aws:s3:::aws-certificate-train-0/*"
        }
    ]
}
```

List of S3 actions are available at: http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html

### Create policy with access to bucket and attached it to user
```
aws iam create-policy --policy-name aws-certificate-train-access --policy-document file://S3/bucket-policy.json

aws iam attach-user-policy --policy-arn arn:aws:iam::484455220000:policy/aws-certificate-train-access --user-name user-name
```

### Upload file
```
# Generate few file
base64 /dev/urandom | head -c 1 file-0.txt

# Upload file
aws s3 cp file-0.txt s3://aws-certificate-train-0/file-0.txt
```

### Copy file
```
aws s3 cp s3://aws-certificate-train-0/file-0.txt s3://aws-certificate-train-0/file-0-copied.txt
```

### Download file
File could be downloaded by following command: aws s3 cp s3://<bucket-name>/<file-path> <local-file-path>
```
aws s3 cp s3://aws-certificate-train-0/file-0-copied.txt file-0-copied.txt
```

### Download multiple files
```
aws s3 cp s3://aws-certificate-train-0 ./temp/ --recursive
```

### Upload multiple files
```
aws s3 cp ./temp s3://aws-certificate-train-0/ --recursive --exclude "*.jpg"
```

### Set ACL during copy
```
aws s3 cp s3://aws-certificate-train-0/test.txt s3://aws-certificate-train-0/test2.txt --acl public-read-write
```

### Grant permissions
```
aws s3 cp file.txt s3://aws-certificate-train-0/ --grants read=uri=http://acs.amazonaws.com/groups/global/AllUsers full=emailaddress=user@example.com
```

### List buckets
```
aws s3 ls
```

### List objects
```
aws s3 ls s3://aws-certificate-train-0

aws s3 ls s3://aws-certificate-train-0 --recursive --human-readable --summarize
```

### Create bucket
```
aws s3 mb s3://bucket-name --region us-west-1
```

### Remove bucket
```
aws s3 rb s3://bucket-name
```

### Sync 
```
# Sync with local folder
aws s3 sync s3://bucket-name .

# Sync between buckets
aws s3 sync s3://my-us-west-2-bucket s3://my-us-east-1-bucket --source-region us-west-2 --region us-east-1
```
