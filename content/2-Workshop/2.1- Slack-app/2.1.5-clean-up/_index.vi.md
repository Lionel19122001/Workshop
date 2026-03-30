---
title : "Dọn dẹp"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 2.1.5 </b> "
---

Phần này giúp xóa toàn bộ tài nguyên đã tạo trong workshop để tránh phát sinh chi phí không cần thiết và giảm rủi ro bảo mật.

#### 1. Danh sách kiểm tra trước khi dọn dẹp
Trước khi xóa, hãy xác nhận các tài nguyên đã tạo trong phần setup:

- Lambda function: `myFunctionSSM`
- IAM role: `lambda-slack-ssm-role`
- SSM parameters:
	- `slack-signing-secret`
	- các parameter dùng để test (ví dụ: `/workshop/slack/test-db-password`)
- Slack app và slash commands:
	- `/create_param`
	- `/update_param`
	- `/delete_param`

#### 2. Xóa test parameters trong SSM
1. Mở **AWS Systems Manager** -> **Parameter Store**.
2. Tìm các parameter test đã tạo trong workshop.
3. Chọn từng parameter và bấm **Delete**.
4. Xóa `slack-signing-secret` nếu chỉ dùng cho bài lab này.
![overview](/images/2.1-Slack/18-ssm.png)
> Nếu môi trường của bạn đang dùng chung parameter này cho ứng dụng khác, không nên xóa.

![overview](/images/2.1-Slack/38-clean.png)
![overview](/images/2.1-Slack/39-clean.png)

#### 3. Xóa Lambda function
1. Mở **AWS Lambda**.
2. Chọn function `myFunctionSSM`.
3. Chọn **Actions** -> **Delete function**.
4. Xác nhận xóa.

![overview](/images/2.1-Slack/0001-createlambdafunction.png)
![overview](/images/2.1-Slack/40-clean.png)
![overview](/images/2.1-Slack/41-clean.png)

#### 4. Xóa CloudWatch Logs (không bắt buộc nhưng nên làm)
1. Mở **CloudWatch** -> **Log groups**.
2. Tìm log group của function này (thường là `/aws/lambda/myFunctionSSM`).
3. Chọn log group và bấm **Delete log group**.

![overview](/images/2.1-Slack/35-cloudwatch.png)
![overview](/images/2.1-Slack/42-clean.png)
![overview](/images/2.1-Slack/43-clean.png)

#### 5. Xóa IAM role và policy đi kèm
Sau khi đã xóa Lambda function:

1. Mở **IAM** -> **Roles**.
2. Chọn role `lambda-slack-ssm-role`.
3. Gỡ các inline policy hoặc attached policy đã tạo cho workshop này.
4. Xóa role.
![overview](/images/2.1-Slack/44-clean.png)
![overview](/images/2.1-Slack/45-clean.png)

#### 6. Gỡ Slack app khỏi workspace
1. Mở [Slack API apps](https://api.slack.com/apps).
2. Chọn app của workshop (ví dụ: `ssm-parameter-bot`).
3. Mở **Settings** -> **Basic Information**.
4. Trong **App Management**, chọn **Delete App** và xác nhận.

Nếu bạn muốn giữ app, ít nhất hãy tắt hoặc xóa toàn bộ slash commands đang trỏ đến Lambda URL đã xóa.
