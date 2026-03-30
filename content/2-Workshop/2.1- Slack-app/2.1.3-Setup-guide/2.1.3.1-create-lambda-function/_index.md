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
- Runtime, select Python 3.14
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
- Upload file Slack-ssm.zip from local
![overview](/images/2.1-Slack/11.png)
![overview](/images/2.1-Slack/12.png)

