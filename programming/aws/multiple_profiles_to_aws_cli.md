## Configuring multiple profiles to the AWS CLI

```
$ aws configure --profile <profile_name>
```

To use a named profile, add the --profile option to your command.

```
# Exmpale
$ aws ec2 describe-instances --profile <profile_name>
```
