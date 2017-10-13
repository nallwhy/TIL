## Creating EC2 instance via AWSCLI

You might know that almost every work that you can do on AWS console, you can do those via AWSCLI also.

It's possible to input all things through command arguments, but to make it more simple and repetiable, use json file.

```json
{
    "ImageId": "ami-xxxxxxxx",
    "MinCount": 1,
    "MaxCount": 1,
    "KeyName": "snappy-crawler",
    "SecurityGroupIds": [
        "sg-xxxxxxxx"
    ],
    "InstanceType": "t2.micro",
    "IamInstanceProfile": {
        "Name": "<role_for_ec2>"
    },
    "TagSpecifications": [
        {
            "ResourceType": "instance",
            "Tags": [
                {
                    "Key": "<key>",
                    "Value": "<value>"
                }
            ]
        }
    ]
}
```

If you want to use user data, because you can't include user data in json, `--user-data`.

```bash
#!/bin/bash

# awscli
apt install -y awscli
aws configure set s3.signature_version s3v4
sudo runuser -l ubuntu -c 'aws configure set s3.signature_version s3v4'
```

```bash
$ aws ec2 run-instances --cli-input-json file://bin/deploy/ec2_cli_input_#{target} --user-data file://bin/deploy/ec2_user_data
```
