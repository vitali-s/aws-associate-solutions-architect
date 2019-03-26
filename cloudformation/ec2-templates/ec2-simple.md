## Create default VPC

```
ec2 create-default-vpc
```

## Generate key-pair

```
ec2 create-key-pair --key-name default-key-aws
```

## Configure parameters

Configure parameters in json/yaml

## Create stack

```
# check current stacks
cloudformation list-stacks

# create stack
cloudformation create-stack --stack-name ec2-simple1 --template-body file://cloudformation/ec2-templates/ec2-simple1.json --parameters ParameterKey=KeyName,ParameterValue=default-key-aws

# in-case of issues, delete stack
cloudformation delete-stack --stack-name ec2-simple1

# if everything is fine, check output
cloudformation describe-stack --stack-name ec2-simple1

# connect
ssh ec2-user@<ip> -i ~/.ssh/default-key-aws.openssh.private
```

## DO NOT FORGET

1. About different users names
```
For Amazon Linux 2 or the Amazon Linux AMI, the user name is ec2-user.
For a Centos AMI, the user name is centos.
For a Debian AMI, the user name is admin or root.
For a Fedora AMI, the user name is ec2-user or fedora.
For a RHEL AMI, the user name is ec2-user or root.
For a SUSE AMI, the user name is ec2-user or root.
For an Ubuntu AMI, the user name is ubuntu.
Otherwise, if ec2-user and root don't work, check with the AMI provider.
```
