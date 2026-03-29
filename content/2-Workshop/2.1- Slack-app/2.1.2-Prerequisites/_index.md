---
title : "Prerequisites"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 2.1.2 </b> "
---

This section lists the required accounts, permissions, and tools before you start the setup.

#### 1. AWS account and region
- An active AWS account.
- Access to the region used in this workshop (recommended: `us-east-1`).
- Basic familiarity with AWS Lambda, IAM, and SSM Parameter Store.

#### 2. IAM permissions
Your IAM user/role must be able to create and run the Lambda function, read Slack secrets, write logs, and manage SSM parameters.

Use a policy similar to the following:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "SSMParameterCRUD",
            "Effect": "Allow",
            "Action": [
                "ssm:PutParameter",
                "ssm:GetParameter",
                "ssm:GetParameters",
                "ssm:GetParametersByPath",
                "ssm:DeleteParameter",
                "ssm:DeleteParameters",
                "ssm:DescribeParameters"
            ],
            "Resource": "*"
        }
    ]
}
```

#### 3. Lambda runtime and tooling
- Python 3.10+ knowledge
- Familiarity with `boto3` for calling AWS APIs.

#### 4. Slack workspace:   https://slack.com/
- A Slack workspace where you have permission to create apps.
- Ability to create and configure slash commands.
- Access to Slack app credentials:
    - `Signing Secret`
    - `Bot/User OAuth Token` (if your implementation posts messages back to channels)


#### 5. Network and endpoint access
- Internet access from Slack to your Lambda endpoint (Lambda Function URL or API Gateway).
- If your organization uses strict network controls, ensure Slack requests are not blocked.

#### 6. Recommended pre-check
Before moving to setup, confirm you can:
- Open the AWS Console in the target region.
- Create a test parameter in SSM Parameter Store.
- Create a Slack app in your workspace.

