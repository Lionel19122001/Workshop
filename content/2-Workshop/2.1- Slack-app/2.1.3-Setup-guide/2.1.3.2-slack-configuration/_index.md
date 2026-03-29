---
title : "Slack configuration"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 2.1.3.2 </b> "
---

In this step, you will create and configure a Slack App that can send slash command requests to your AWS Lambda endpoint.

#### 1. Create a Slack App
1. Open the [Slack API portal](https://api.slack.com/apps).
2. Choose **Create New App**.
3. Select **From scratch**.
4. Enter app name: `ssm-parameter-bot` (or any name you prefer).
5. Choose your workspace and create the app.

#### 2. Enable incoming requests
1. In the app settings menu, open **Slash Commands**.
2. Choose **Create New Command**.
3. Configure:
- Command: `/create_param`
- Request URL: use your Lambda Function URL (or API Gateway endpoint)
- Short Description: `Create an SSM parameter`
- Usage Hint: `<name> <type> <value>`
4. Save the command.

You can add more commands later, for example:
- `/update_param`
- `/delete_param`

#### 3. Get app credentials
Open **Basic Information** and copy:
- **Signing Secret**

Open **OAuth & Permissions** and copy:
- **Bot User OAuth Token** (if your Lambda posts messages back via Web API)

Store these values securely in AWS Secrets Manager or SSM Parameter Store. Do not hardcode them in source code.

#### 4. Configure bot permissions
In **OAuth & Permissions**, add required scopes.

Recommended bot token scopes:
- `commands`
- `chat:write`

If you need channel reading behavior, add only the minimum extra scopes required.

#### 5. Install app to workspace
1. In **OAuth & Permissions**, choose **Install to Workspace**.
2. Review and allow requested permissions.
3. Confirm the app appears in your workspace app list.

#### 6. Basic validation
Before moving on:
- Confirm slash command is created and active.
- Confirm Request URL points to your Lambda endpoint.
- Confirm Signing Secret is stored securely.

You will complete end-to-end testing in the test section after Lambda deployment is finished.
