# Snowball
AWS Snowball is a service that accelerates transferring large amounts of data into and out of AWS using physical storage appliances, bypassing the Internet. 

## Import data

* Create import job, provide shipping and job details, such as address, region, destination S3 bucket.
* Configure security: ARN for the IAM role and Master Key (AWS KMS)
* Configure SNS notifications
* Wait until AWS Snowball Appliance will arrive.
* Connect Snowball and import data using snowball utility (http://docs.aws.amazon.com/snowball/latest/ug/transfer-data.html)
* Return Snowball Appliance

Export process is almost identical.

## Devices
* Snowball
* Snowball Edge
* Snowmobile - truck, exabyte-scale data transfer service.

## Specifications
Snowball configurations:
* 50 TB (42 TB usable space)
* 80 TB (72 TB usable space)

Snowball Edge configuration:
* 16 CPU, 16 GB RAM
