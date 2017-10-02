## Reference

List of all commands are available at: http://docs.aws.amazon.com/cli/latest/reference/iam/index.html#cli-aws-iam

### Example

```
# Create Groups
aws iam create-group --group-name Managers
aws iam create-group --group-name DevOps
aws iam create-group --group-name Developers
aws iam create-group --group-name QA

# Create Users
aws iam create-user --user-name Managers-Bob
aws iam create-user --user-name DevOps-Bob
aws iam create-user --user-name Developers-Bob
aws iam create-user --user-name QA-Bob

aws iam add-user-to-group --user-name Managers-Bob --group-name Managers
aws iam add-user-to-group --user-name DevOps-Bob --group-name DevOps
aws iam add-user-to-group --user-name Developers-Bob --group-name Developers
aws iam add-user-to-group --user-name QA-Bob --group-name QA

aws iam create-role --role-name Managers-Role --assume-role-policy-document file://Test-Role-Trust-Policy.json
```

