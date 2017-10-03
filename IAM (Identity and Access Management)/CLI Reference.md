## Reference

List of all commands are available at: http://docs.aws.amazon.com/cli/latest/reference/iam/index.html#cli-aws-iam

## Examples
All operations could be split into:
* add-*
* attach-*
* create-*
* delete-*
* get-*
* list-*
* update-*

## Users
Get current user
```
aws iam get-user
```

List users, filter by UserName
```
aws iam list-users | jq -r "..|.UserName?" | grep Bob
```

Filter users by any text
```
aws iam list-users --output text | grep DevOps
```

List users, show only 6th field (cut -f 6)
```
aws iam list-users --output text | cut -f 6
```

Create access key
```
aws iam create-access-key --user-name DevOps-Bob --output text
```

## Groups

List groups by name
```
aws iam list-groups --output text | cut -f 5
```

Create group
```
aws iam create-group --group-name DevOps
```

List attached group policies
```
aws iam list-attached-group-policies --group-name DevOps
```

## Policies
List all policies Arn
```
aws iam list-policies | jq "..|.Arn?"
```

List IAM or S3 policies
```
aws iam list-policies | jq "..|.Arn?" | grep IAM
aws iam list-policies | jq "..|.Arn?" | grep S3
```

Get Policy by Arn
```
aws iam get-policy --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess
```

Create group and attached policy
```
aws iam create-group --group-name S3ReadOnlyUsers
aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/ReadOnlyAccess --group-name S3ReadOnlyUsers

aws iam detach-group-policy --policy-arn arn:aws:iam::aws:policy/ReadOnlyAccess --group-name S3ReadOnlyUsers
aws iam delete-group --group-name S3ReadOnlyUsers
```

Create policy:
```
aws iam create-policy --policy-name my-policy --policy-document file://policy
```
Policy Example:
```
{
  "Version": "2012-10-17",
  "Statement": {
    "Effect": "Allow",
    "Action": "s3:ListBucket",
    "Resource": "arn:aws:s3:::example_bucket"
  }
}
```

## Combined
Create user, generate access key, add s3 permissions
```
aws iam create-user --user-name aws-lab-user-01
aws iam attach-user-policy --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess --user-name aws-lab-user-01
aws iam create-access-key --user-name aws-lab-user-01

aws iam detach-user-policy --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess --user-name aws-lab-user-01
aws iam delete-access-key --access-key ... --user-name aws-lab-user-01
aws iam delete-user --user-name aws-lab-user-01
```

## References
cut: http://www.thegeekstuff.com/2013/06/cut-command-examples
jq: https://stedolan.github.io/jq/manual