---
title : "Slack configuration"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 2.1.3.2 </b> "
---
<div style="background-color: #fff3cd; border-left: 4px solid #f0ad4e; padding: 12px 16px; border-radius: 4px; margin-bottom: 16px;">
	<strong>Warning:</strong> Ensure your Slack workspace and app are fully set up before proceeding.
</div>
In this step, you will create and configure a Slack App that can send slash command requests to your AWS Lambda endpoint.

#### 1. Create a Slack App
1. Open the [Slack API portal](https://api.slack.com/apps).
2. Choose **Create New App**.
3. Select **From scratch**.

![overview](/images/2.1-Slack/14-slack.png)
![overview](/images/2.1-Slack/15-slack.png)

4. Enter app name: `ssm-parameter-bot` (or any name you prefer).
5. From the “Pick a workspace to develop your app in” step, select the workspace where your Slack app will be created.
6. Choose your workspace and create the app.

![overview](/images/2.1-Slack/16-slack.png)

#### 2. Get app credentials

Open **Basic Information** and copy:
- **Signing Secret**
![overview](/images/2.1-Slack/17-ssm.png)
Open **AWS Systems Manager**:
![overview](/images/2.1-Slack/18-ssm.png)
![overview](/images/2.1-Slack/19-ssm.png)
1. Select **Parameter Store**.
2. Click **Create parameter**.
3. Create a parameter for the Slack Signing Secret:
- Name: `slack-signing-secret` 
> **Note:** If you use a different parameter name, update the value in `slack_auth.py` to match.
- Description: `Slack app signing secret`
- Tier: `Standard`
- Type: `String`
- Data type: `text`
- Value: paste the **Signing Secret** from Slack
1. Click **Create parameter**.
![overview](/images/2.1-Slack/20-ssm.png)
![overview](/images/2.1-Slack/21-ssm.png)
#### 3. Enable incoming requests
1. In the app settings menu, open **Slash Commands**.
2. Choose **Create New Command**.
![overview](/images/2.1-Slack/22-slackcmd.png)
3. Configure:
- Copy URL
![overview](/images/2.1-Slack/13.png)
- Create SSM parameter 
- Command: `/create_param`
- Request URL: use your Lambda Function URL
- Short Description: `Create an SSM parameter`
- Usage Hint: `<name> <type> <value>`
- Save the command.
![overview](/images/2.1-Slack/23-slackcmd.png)

You can add more commands later, for example:
- Update SSM parameter 
- `/update_param`
- Request URL: use your Lambda Function URL
- Short Description: `Update SSM parameter`
- Usage Hint: `<name> <value>`
- Save the command.
#### 
- Delete SSM parameter 
- `/delete_param`
- Request URL: use your Lambda Function URL
- Short Description: `Delete SSM parameter`
- Usage Hint: `<name>`
- Save the command.
#### 4. Install app to workspace
1. In **Settings**.
2. choose **Install App**.
![overview](/images/2.1-Slack/24-install.png)
1. Review and allow requested permissions.
2. Confirm the app appears in your workspace app list.
3. Click Allow
![overview](/images/2.1-Slack/25-install.png)

#### 5. Basic validation
Before moving on:
- Confirm slash command is created and active.
- Confirm Request URL points to your Lambda endpoint.
- Confirm Signing Secret is stored securely.
