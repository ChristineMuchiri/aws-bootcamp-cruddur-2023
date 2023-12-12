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


# WEEK 0 Challenge
## Using EventBridge to hookup Health Dashboard to SNS
First create an SNS topic for your EventBridge.
Choose topic type as **Standard** and leave the all other options as default
![SNStopic](Diagrams/SNStopic.GIF).

Your created topic should be as below.
![SNS topic](Diagrams/SNStopic1.GIF)


Be sure to create a subscription to the SNS topic with *type of endpoint to subscribe as email*.

Then confirm subscription in your email.

Navigate to **Amazon EventBridge**

Create Rule
![Event](Diagrams/event1.GIF)


![Event](Diagrams/event2.GIF)

![Event](Diagrams/event3.GIF)


Select SNS as the event target, choosing Health-notification, the topic you created earlier, as your SNS topic
![Event](Diagrams/event4.GIF)

Review and Create the rule.

You have successfully used **Event Bridge** to hookup **Health Dashboard** to **SNS**
