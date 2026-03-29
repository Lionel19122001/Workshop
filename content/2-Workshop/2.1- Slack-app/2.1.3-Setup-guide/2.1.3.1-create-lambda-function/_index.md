---
title : "Create the Lambda function"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 2.1.3.1 </b> "
---

In this step, you will deploy a Python Lambda function that receives Slack slash command requests and creates parameters in AWS Systems Manager Parameter Store.


#### 1. Create the Lambda function
1. Go to AWS Management Console
- Find Lambda
- Select Lambda
![overview](/images/2.1-Slack/0001-createlambdafunction.png)

2. In the AWS Lambda interface
- Select Function
- Select Create function
![overview](/images/2.1-Slack/0002-createlambdafunction.png)

3. In the Create function interface
- Select Author from scratch
- Function name, enter myFunctionSSM
- Runtime, select Python 3.8
- Select x86_64
- Select Use another role
- Click Create new role
![overview](/images/2.1-Slack/0003.jpg)
![overview](/images/2.1-Slack/4-iamrole.png)

- Role name, enter lambda-slack-ssm-role
- Policy: [2.1.2-Prerequisites](../../2.1.2-Prerequisites/)
- Click Create role
![overview](/images/2.1-Slack/5-iamrole.png)
![overview](/images/2.1-Slack/6-iamrole.png)
![overview](/images/2.1-Slack/7-iamrole.png)
![overview](/images/2.1-Slack/8-iamrole.png)
- Enable Function URL
- Select NONE
- Click Create function 
![overview](/images/2.1-Slack/9-url.png)
![overview](/images/2.1-Slack/10.png)
#### 2. Add function code
Download Lambda source package
- [Download Slack-ssm.zip](/downloads/Slack-ssm.zip)

#### 3. Configure environment variables
Add environment variables in Lambda configuration:
- `SLACK_SIGNING_SECRET`
- `AWS_REGION`
- `DEFAULT_PARAMETER_TIER` (optional)

If possible, load sensitive values from Secrets Manager or Parameter Store at runtime instead of plain text environment values.

#### 4. Create Lambda Function URL (or API Gateway)
1. In Lambda, open **Function URL** and create a new URL.
2. Set authentication according to your design (commonly `NONE` for Slack webhooks).
3. Keep security at application level by validating Slack signature for every request.
4. Copy the function URL and update Slack Slash Command Request URL.

#### 6. Configure timeout and memory
Recommended baseline:
- Timeout: 10-15 seconds
- Memory: 256 MB

These settings are usually enough for Slack command processing and SSM API calls.

#### 7. Verify CloudWatch logging
1. Invoke the function with a test event.
2. Open CloudWatch Logs and verify:
- Function starts successfully
- Request parsing works
- SSM API call result is logged
- Proper error details are present when failures occur

After this step, continue to the test section to run slash commands from Slack and validate end-to-end behavior.
