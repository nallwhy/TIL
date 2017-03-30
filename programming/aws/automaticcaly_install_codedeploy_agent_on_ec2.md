### Install the CodeDeploy agent on an EC2 instance **automatically** (Ubuntu)

When you create a launch configuration, you can use the **User data** field to add commands to execute when the instance starts.

```bash
#!/bin/bash
sudo apt-get update
sudo apt-get install python-pip
sudo apt-get install ruby
sudo apt-get install wget
cd /home/ubuntu
REGION=$(curl 169.254.169.254/latest/meta-data/placement/availability-zone/ | sed 's/[a-z]$//')
wget https://aws-codedeploy-$REGION.s3.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto
sudo service codedeploy-agent start
```

Reference:  
http://docs.aws.amazon.com/ko_kr/codedeploy/latest/userguide/codedeploy-agent-operations-install.html#codedeploy-agent-operations-install-ubuntu  
https://aws.amazon.com/premiumsupport/knowledge-center/codedeploy-agent-launch-configuration/
