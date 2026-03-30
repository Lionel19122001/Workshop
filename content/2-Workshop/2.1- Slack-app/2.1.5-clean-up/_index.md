---
title : "Clean up"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 2.1.5 </b> "
---

This section removes all resources created in this workshop to avoid unnecessary cost and reduce security risk.

#### 1. Cleanup checklist
Before deleting resources, confirm what was created during setup:

- Lambda function: `myFunctionSSM`
- IAM role: `lambda-slack-ssm-role`
- SSM parameters:
	- `slack-signing-secret`
	- any test parameters (for example: `/workshop/slack/test-db-password`)
- Slack app and slash commands:
	- `/create_param`
	- `/update_param`
	- `/delete_param`

#### 2. Delete test parameters in SSM
1. Open **AWS Systems Manager** -> **Parameter Store**.
2. Search for test parameters created in this workshop.
3. Select each test parameter and choose **Delete**.
4. Delete `slack-signing-secret` if it is used only for this lab.
![overview](/images/2.1-Slack/18-ssm.png)
> If your environment shares this parameter with another app, do not delete it.

![overview](/images/2.1-Slack/38-clean.png)
![overview](/images/2.1-Slack/39-clean.png)

#### 3. Delete Lambda function
1. Open **AWS Lambda**.
2. Select function `myFunctionSSM`.
3. Choose **Actions** -> **Delete function**.
4. Confirm deletion.

![overview](/images/2.1-Slack/0001-createlambdafunction.png)
![overview](/images/2.1-Slack/40-clean.png)
![overview](/images/2.1-Slack/41-clean.png)


#### 4. Delete CloudWatch Logs (optional but recommended)
1. Open **CloudWatch** -> **Log groups**.
2. Find the log group for this function (typically `/aws/lambda/myFunctionSSM`).
3. Select the log group and choose **Delete log group**.

![overview](/images/2.1-Slack/35-cloudwatch.png)
![overview](/images/2.1-Slack/42-clean.png)
![overview](/images/2.1-Slack/43-clean.png)
#### 5. Delete IAM role and inline policy
After the Lambda function is deleted:

1. Open **IAM** -> **Roles**.
2. Select role `lambda-slack-ssm-role`.
3. Remove any inline or attached policies created for this workshop.
4. Delete the role.
![overview](/images/2.1-Slack/44-clean.png)
![overview](/images/2.1-Slack/45-clean.png)
#### 6. Remove Slack app from workspace
1. Open [Slack API apps](https://api.slack.com/apps).
2. Select your workshop app (for example: `ssm-parameter-bot`).
3. Open **Settings** -> **Basic Information**.
4. In **App Management**, choose **Delete App** and confirm.

If you prefer to keep the app, at least disable or remove all slash commands pointing to the deleted Lambda URL.
