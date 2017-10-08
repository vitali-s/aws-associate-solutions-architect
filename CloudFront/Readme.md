# CDN

* Edge Locations - location where content will be cached
* Origin - storage of original files that will be distributed
* Distribution - name given to CDN which includes collection of Edge Locations

Content types:
* Static content
* Dynamic content
* Streaming

Distribution types:
* Web Distribution - typically used for web sites
* RTMP - used for media streaming

Types of origins:


# Lab
Create public bucket is EU/US region:
```
aws s3api create-bucket \
    --bucket aws-certificate-public \
    --region eu-west-1 \
    --acl public-read \
    --create-bucket-configuration LocationConstraint=eu-west-1

base64 /dev/urandom | head -c 5 > public-file-0.txt

aws s3 cp \
    public-file-0.txt \
    --acl public-read \
    s3://aws-certificate-public/public-file-0.txt

curl https://s3-eu-west-1.amazonaws.com/aws-certificate-public/public-file-0.txt

traceroute s3-eu-west-1.amazonaws.com
```
Traceroute took 25 hops to get the data.

Create distribution,parameters are described at: http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/GettingStarted.html

Check distribution
```
curl http://d2glgcasdveyjv.cloudfront.net/public-file-0.txt

traceroute d2glgcasdveyjv.cloudfront.net
```
Traceroute took 15 hops to get the data.

# Tips
* Edge locations are not just READ only, it is possible to write to them (PUT)
* Object are cached for TTL
* Distribution provides ability to configure Geo-Restrictions (white-list, back-list to particular countries)
* Invalidation allows to invalidate versions


# References
* [API Reference](http://docs.aws.amazon.com/cloudfront/latest/APIReference/Welcome.html)
* [Documentation](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)