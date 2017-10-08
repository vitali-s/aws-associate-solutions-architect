# Versioning

Enables ability to track every single version for object in bucket.


## Lab

* Upload file
```
base64 /dev/urandom | head -c 5 > file-version-0.txt

aws s3api put-object --bucket aws-certificate-train-0 --key file-version-0 --body file-version-0.txt
```

* Enable versioning
```
    aws s3api put-bucket-versioning --bucket aws-certificate-train-0 --versioning-configuration Status=Enabled
```

* Generate and upload new versions
```
base64 /dev/urandom | head -c 5 > file-version-0.txt
aws s3api put-object --bucket aws-certificate-train-0 --key file-version-0 --body file-version-0.txt
```

* List object versions
```
aws s3api list-object-versions --bucket aws-certificate-train-0 --prefix file-version-0
```

* Restore version
```

```

## Summary

* Storage cost could easily go up, depending on amount of versions and large files
* Versioning is enabled for the whole bucket
* Versioning could not be disabled, only suspended (keep all versions that already uploaded)
* It integrates with life cycle rules
* Versioning MFA delete capability, provides additional level of protection and security

