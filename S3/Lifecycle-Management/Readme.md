# Lifecycle
Lifecycle configuration enables you to specify the lifecycle management of objects in a bucket.

# Lifecycle Configuration

* ID - id of lifecycle configuration, up to 255 characters
* Status - could be Enabled or Disabled
* Filter - filter objects by key or tags
* Transition - specified transition from one state to another, for example:
** 

# Lifecycle configuration schema
```
{
  "Rules": [
    {
      "Expiration": {
        "Date": timestamp,
        "Days": integer,
        "ExpiredObjectDeleteMarker": true|false
      },
      "ID": "string",
      "Prefix": "string",
      "Filter": {
        "Prefix": "string",
        "Tag": {
          "Key": "string",
          "Value": "string"
        },
        "And": {
          "Prefix": "string",
          "Tags": [
            {
              "Key": "string",
              "Value": "string"
            }
            ...
          ]
        }
      },
      "Status": "Enabled"|"Disabled",
      "Transitions": [
        {
          "Date": timestamp,
          "Days": integer,
          "StorageClass": "GLACIER"|"STANDARD_IA"
        }
        ...
      ],
      "NoncurrentVersionTransitions": [
        {
          "NoncurrentDays": integer,
          "StorageClass": "GLACIER"|"STANDARD_IA"
        }
        ...
      ],
      "NoncurrentVersionExpiration": {
        "NoncurrentDays": integer
      },
      "AbortIncompleteMultipartUpload": {
        "DaysAfterInitiation": integer
      }
    }
    ...
  ]
}```

```
aws s3api put-bucket-lifecycle-configuration --bucket my-bucket --lifecycle-configuration  file://lifecycle.json
```

# Transitions and constraints
http://docs.aws.amazon.com/AmazonS3/latest/dev/lifecycle-transition-general-considerations.html

* Typical flow:
  * STANDARD or REDUCED_REDUNDANCY to STANDARD_IA
  * STANDARD_IA to GLACIER
  * Expiration (STANDARD, REDUCED_REDUNDANCY, STANDARD_IA, GLACIER)
* From the STANDARD or REDUCED_REDUNDANCY storage classes to STANDARD_IA
  * Object should be more 128K, and stored for > 30 days (transition before 30 days is not supported)
* From any storage class to GLACIER
  * Objects in the GLACIER storage class are not available in real time.
  * The transition of objects to the GLACIER storage class is one-way.
  * The GLACIER storage class objects are visible and available only through Amazon S3, not through Amazon Glacier.
* Limitations
  * You can't transition from STANDARD_IA storage class to the STANDARD or REDUCED_REDUNDANCY classes.
  * You can't transition from GLACIER to any other storage class.
  * You can't transition from any storage class to REDUCED_REDUNDANCY.


# Summary

* Can be used with versioning
* Can be applied to both current and previous versions
* Following could be done:
  * Transition to Infrequent Access Storage Class (>128kb and > 30 days after creation)
  * Archive to Glacier Storage class (>60 days)
  * Permanently delete 
