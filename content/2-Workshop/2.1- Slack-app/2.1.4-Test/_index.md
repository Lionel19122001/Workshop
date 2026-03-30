---
title : "Test"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 2.1.4 </b> "
---

This section validates the end-to-end Slack App workflow after setup.


#### 1. Pre-test checklist
Before running test cases, confirm:

- The Slack app is installed in your workspace.
- Slash commands are created:
	- `/create_param`
	- `/update_param`
	- `/delete_param`
- Each command Request URL points to your Lambda Function URL.
- SSM parameter `slack-signing-secret` exists and contains the correct value.
- Lambda execution role has SSM permissions.

#### 2. Prepare a test naming convention
Use a unique parameter name to avoid conflicts, for example:

```text
/workshop/slack/test-db-password
```

You can use any name format accepted by SSM Parameter Store.

#### 3. Functional test cases

##### Test case A: Create parameter
1. In Slack, run:

```text
/create_param /workshop/slack/test-db-password String my-secret-123
```
![overview](/images/2.1-Slack/26-test.png)

2. Result in Slack:
- ![overview](/images/2.1-Slack/27-test.png)


3. Validate in AWS Console:
- Open **Systems Manager** -> **Parameter Store**.
- Search for `/workshop/slack/test-db-password`.
- Confirm:
	- Name is correct.
	- Type is `String`.
	- Value is stored.
![overview](/images/2.1-Slack/28-test.png)


##### Test case B: Update parameter
1. In Slack, run:

```text
/update_param /workshop/slack/test-db-password my-secret-456
```
![overview](/images/2.1-Slack/29-update.png)
2. Result in Slack:
![overview](/images/2.1-Slack/30-update.png)

3. Validate in AWS Console:
- Open the parameter and confirm the latest value is `my-secret-456`.
![overview](/images/2.1-Slack/31-update.png)


##### Test case C: Delete parameter
1. In Slack, run:

```text
/delete_param /workshop/slack/test-db-password
```
![overview](/images/2.1-Slack/32-delete.png)
2. Result in Slack:
![overview](/images/2.1-Slack/33-delete.png)

3. Validate in AWS Console:
- Search for the parameter in Parameter Store.
- Confirm it no longer exists.
![overview](/images/2.1-Slack/34-delete.png)
#### 4. CloudWatch log validation
After each test case:

1. Open **CloudWatch** -> **Log groups**.
2. Select the log group for your Lambda function.
![overview](/images/2.1-Slack/35-cloudwatch.png)
![overview](/images/2.1-Slack/36-cloudwatch.png)
![overview](/images/2.1-Slack/37-cloudwatch.png)