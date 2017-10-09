# Website

You can host a static website on Amazon Simple Storage Service (Amazon S3)

* Public website DNS format (custom DNS could be also configured, http only):
```
<bucket-name>.s3-website-<region-name>.com  # (US)
<bucket-name>.s3-website.<region-name>.com  # (EU (Frankfurt))
```
https endpoint is available at:
```
https://s3-<region-name>.amazonaws.com/<bucket-name>/ß
```

* Limitations:
  * Supports only publicly readable content.
  * Supports both object-level and bucket-level redirects.
  * Supports only GET and HEAD requests on objects.
  * Does not support SSL connections.

* Traffic could be logged by enabling logging on bucket
* Support redirect configuration to external websites
* Custom error pages

# Lab

Create bucket:
```
aws s3api create-bucket \
    --bucket aws-certificate-website \
    --region us-west-2 \
    --create-bucket-configuration LocationConstraint=us-west-2 \
    --acl public-read
```

Upload index file
```
printf '<html><body><h3>Hello AWS!</h3</body></html>' > index.html

# Upload file
aws s3 cp index.html \
    s3://aws-certificate-website/index.html \
    --acl public-read
```

Define website configuration
```
{
  "ErrorDocument": {
    "Key": "string"
  },
  "IndexDocument": {
    "Suffix": "string"
  },
  "RedirectAllRequestsTo": {
    "HostName": "string",
    "Protocol": "http"|"https"
  },
  "RoutingRules": [
    {
      "Condition": {
        "HttpErrorCodeReturnedEquals": "string",
        "KeyPrefixEquals": "string"
      },
      "Redirect": {
        "HostName": "string",
        "HttpRedirectCode": "string",
        "Protocol": "http"|"https",
        "ReplaceKeyPrefixWith": "string",
        "ReplaceKeyWith": "string"
      }
    }
    ...
  ]
}
```

Enable website configuration
```
aws s3api put-bucket-website \
    --bucket aws-certificate-website \
    --website-configuration file://S3/Website/website-configuration.json
```

Load website
```
curl https://s3-us-west-2.amazonaws.com/aws-certificate-website/index.html

curl http://aws-certificate-website.s3-website-us-west-2.amazonaws.com/index.html
```

# Reference
http://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html