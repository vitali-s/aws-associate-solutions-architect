# IAM Features

* Centrilized control of AWS account
* Shared acces to AWS account
* Granular permissions
* Identity Federation (AD, Facebook, LinkedIn)
* Multifactor Authentication
* Provide temporary access
* Passwords rotation policy
* Integration with different AWS services
* Support PCI DSS Complience

# IAM Terms

* User - end user
** There is root user which has unrestricted access to all AWS resources
*** Notes: don't use root user, setup MFA, user separate accounts with limited access
** There are Fedarated Users - they are already belong to some identity provider (organization)
*** Notes: It could be done via SAML 2.0 or OpenID connect 2.0 configuration, for AD - AWS Directory Service could be used. AWS STS web identity federation supports Login with Amazon, Facebook, Google, and any OpenID Connect (OICD)-compatible identity provider.

* Groop - a collection of end users under one set of permissions

* Roles - roles are assigned to AWS resources

* Policies - a document that defined one or more permissions
** Example of policy
```
{
  "Version": "2012-10-17",
  "Statement": {
    "Effect": "Allow",
    "Action": "dynamodb:*",
    "Resource": "arn:aws:dynamodb:us-east-2:123456789012:table/Books"
  }
}
```
** "Federated users don't have permanent identities in your AWS account the way that IAM users do. To assign permissions to federated users, you can create an entity referred to as a role and define permissions for the role. When a federated user signs in to AWS, the user is associated with the role and is granted the permissions that are defined in the role."
** There are two types of policies: User-based policies (assigned to users) and Resource-based policies (assigned to resource, for example S3 bucket).

# Best Practicies

http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html

# Users

* Users described by:
** Friendly name, for example: bob
** ARN (Amazon Resource Name), for example: arn:aws:iam::account-ID-without-hyphens:user/Bob
** Unique identifier
* Users could access AWS by:
** Console password: for example for AWS Management Console
** Access keys: A combination of an access key ID and a secret access key. Primary use by programmatic calls.
** SSH keys for use with AWS CodeCommit
** Server certificates: could be used with some services

# References

* User Guide: http://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html

# Notes