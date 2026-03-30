---
title : "Tạo Lambda function"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 2.1.3.1 </b> "
---

Trong bước này, bạn sẽ triển khai một Python Lambda function để nhận request slash command từ Slack và tạo parameter trong AWS Systems Manager Parameter Store.

#### 1. Tạo Lambda function
1. Vào AWS Management Console
- Tìm Lambda
- Chọn Lambda
![overview](/images/2.1-Slack/0001-createlambdafunction.png)

2. Trong giao diện AWS Lambda
- Chọn Function
- Chọn Create function
![overview](/images/2.1-Slack/0002-createlambdafunction.png)

3. Trong giao diện Create function
- Chọn Author from scratch
- Function name: nhập `myFunctionSSM`
- Runtime: chọn Python 3.14
- Chọn x86_64
- Chọn Use another role
- Bấm Create new role
![overview](/images/2.1-Slack/0003.jpg)
![overview](/images/2.1-Slack/4-iamrole.png)

- Role name: nhập `lambda-slack-ssm-role`
- Policy: [2.1.2-Prerequisites](../../2.1.2-Prerequisites/)
- Bấm Create role
![overview](/images/2.1-Slack/5-iamrole.png)
![overview](/images/2.1-Slack/6-iamrole.png)
![overview](/images/2.1-Slack/7-iamrole.png)
![overview](/images/2.1-Slack/8-iamrole.png)
- Bật Function URL
- Chọn NONE
- Bấm Create function
![overview](/images/2.1-Slack/9-url.png)
![overview](/images/2.1-Slack/10.png)

#### 2. Thêm code cho function
Tải source package của Lambda
- [Download Slack-ssm.zip](/downloads/Slack-ssm.zip)
- Upload file Slack-ssm.zip từ máy local
![overview](/images/2.1-Slack/11.png)
![overview](/images/2.1-Slack/12.png)
