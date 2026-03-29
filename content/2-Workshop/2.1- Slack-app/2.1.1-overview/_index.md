---
title : "Overview"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 2.1.1 </b> "
---

This project is a serverless Slack-based automation system that enables users to manage AWS SSM Parameter Store directly through Slack slash commands. By integrating Slack with AWS Lambda, the system allows users to create, update, and delete parameters without accessing the AWS Console.

The application processes incoming Slack requests, validates them using Slack signing secrets, and performs corresponding actions on SSM Parameter Store. It is designed with a focus on security, simplicity, and maintainability, leveraging IAM least privilege and modular code structure.

This solution improves operational efficiency by automating parameter management workflows and providing a user-friendly interface through Slack.

#### Architecture:
![overview](/images/5-Workshop/5.1-Workshop-overview/diagram1.jpg)



#### Components:
- **Slack**: slash command UI and request origin.
- **AWS Lambda**: request validation + parameter creation.
- **AWS SSM Parameter Store**: secure storage for configuration and secrets.
- **CloudWatch Logs:** collects and stores logs from Lambda for monitoring, debugging, and troubleshooting.

#### High-level flow:
- User sends a slash command from Slack (e.g., `/create_param`).
- Slack sends an HTTP POST request directly to AWS Lambda (via Lambda Function URL).
- Lambda validates the request (Slack signature, command format, input data).
- Lambda processes the command and attempts to create the parameter in SSM Parameter Store.
- SSM stores the parameter (or returns an error if invalid or already exists).
- Lambda formats the response message.
- Lambda returns the response to Slack.
- Slack displays the result to the user.
