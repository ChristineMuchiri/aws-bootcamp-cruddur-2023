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

## Create a Cost and Usage Budget
First create a budget.json file and copy the contents below to the file
```
{
    "BudgetLimit": {
        "Amount": "100",
        "Unit": "USD"
    },
    "BudgetName": "Example Tag Budget",
    "BudgetType": "COST",
    "CostFilters": {
        "TagKeyValue": [
            "user:Key$value1",
            "user:Key$value2"
        ]
    },
    "CostTypes": {
        "IncludeCredit": true,
        "IncludeDiscount": true,
        "IncludeOtherSubscription": true,
        "IncludeRecurring": true,
        "IncludeRefund": true,
        "IncludeSubscription": true,
        "IncludeSupport": true,
        "IncludeTax": true,
        "IncludeUpfront": true,
        "UseBlended": false
    },
    "TimePeriod": {
        "Start": 1477958399,
        "End": 3706473600
    },
    "TimeUnit": "MONTHLY"
}
```
Replace with your own values.
Then create a budget-notifications with subscribers.json file.
Populate it with the following values
```
[
    {
        "Notification": {
            "ComparisonOperator": "GREATER_THAN",
            "NotificationType": "ACTUAL",
            "Threshold": 80,
            "ThresholdType": "PERCENTAGE"
        },
        "Subscribers": [
            {
                "Address": "example@example.com",
                "SubscriptionType": "EMAIL"
            }
        ]
    }
]
```
Then run the following command. You can then confirm the busget has been created using the console.
```
aws budgets create-budget \
    --account-id 111122223333 \
    --budget file://budget.json \
    --notifications-with-subscribers file://notifications-with-subscribers.json
```


# WEEKO Challenge
## Using EventBridge to hookup Health Dashboard to SNS
First create an SNS topic for your EventBridge.
