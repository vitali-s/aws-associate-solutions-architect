# AWS CLI

The AWS CLI is an open source tool built on top of the AWS SDK for Python (Boto) that provides commands for interacting with AWS services.

* Installation
```
$ pip install awscli --upgrade --user
```

* Autocomplete configration: http://docs.aws.amazon.com/cli/latest/userguide/cli-command-completion.html

* Configuration files (default, and names profiles)
```
~/.aws              # Unix, Linux
%UserProfile%\.aws  # Windows
```

** ~/.aws/credentials
```
[default]
aws_access_key_id=AKIAIOSFODNN7EXAMPLE
aws_secret_access_key=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY

[user2]
aws_access_key_id=AKIAI44QH8DHBEXAMPLE
aws_secret_access_key=je7MtGbClwBF/2Zp9Utk/h3yCo8nvbEXAMPLEKEY
```

** ~/.aws/config
```
[default]
region=us-west-2
output=json

[profile user2]
region=us-east-1
output=text
```

* Profiles are set by --profile or environmental variable
```
aws ec2 describe-instances --profile user2
export AWS_PROFILE=user2    # Unix, Linux
set AWS_PROFILE=user2       # Windows
```



## Environment variables

AWS_ACCESS_KEY_ID – AWS access key.
AWS_SECRET_ACCESS_KEY – AWS secret key. Access and secret key variables override credentials stored in credential and config files.
AWS_SESSION_TOKEN – Specify a session token if you are using temporary security credentials.
AWS_DEFAULT_REGION – AWS region. This variable overrides the default region of the in-use profile, if set.
AWS_DEFAULT_OUTPUT – Change the AWS CLI's output formatting to json, text, or table.
AWS_PROFILE – name of the CLI profile to use. This can be the name of a profile stored in a credential or config file, or default to use the default profile.
AWS_CA_BUNDLE – Specify the path to a certificate bundle to use for HTTPS certificate validation.
AWS_SHARED_CREDENTIALS_FILE – Change the location of the file that the AWS CLI uses to store access keys.
AWS_CONFIG_FILE – Change the location of the file that the AWS CLI uses to store configuration profiles.

## Commandline options

--profile – name of a profile to use, or "default" to use the default profile.
--region – AWS region to call.
--output – output format.
--endpoint-url – The endpoint to make the call against.

## Command structure

```
aws <command> <subcommand> [options and parameters]
```

## Pagination

By default, the CLI uses a page size of 1000 and retrieves all available items. You can use the --page-size option to specify a smaller page size to solve this issue.