# Week 0 — Billing and Architecture
## Cruddur - Architectural  diagram
This diagram is subject to changes as the bootcamp progresses
![Architectural diagram](Diagrams/WEEK0.GIF)
## Installing AWS CLI
To install the latest version of AWS CLI on Linux, follow the guidelines from AWS [AWS CLI Installation](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```
Confirm the installation with the following command. If the **aws** command is not found, you might need to restart your terminal.
```
aws --version
```
## Generate AWS Credentials
First create your IAM user and generate the access keys for the User using the console. [Creating IAM Users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html#id_users_create_console)
. Use **aws configure** command to setup your AWS CLI Installation
```
$ aws configure
 AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
 AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
 Default region name [None]: us-west-2
 Default output format [None]: json
```
Replace them with your own values
